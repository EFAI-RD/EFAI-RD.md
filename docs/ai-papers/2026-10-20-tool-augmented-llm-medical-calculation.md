---
catalog_id: "arxiv:2610.21477"
editors:
  - "Clare"
refs:
  main:
    title: "Tool-Augmented Large Language Models for Reliable Medical Calculation from Patient Notes"
    url: "https://arxiv.org/abs/2610.21477"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 算分交給程式、LLM 只抽參數：GPT-5.5 先把 55 個醫療計算器寫成驗證過的 Python 工具，Qwen3-8B 負責從病歷填表，MedCalc-Bench Verified 上 86.73%，剩下的錯多半出在讀病歷

## 來源

- 團隊：大連理工大學計算機科學與技術學院（College of Computer Science and Technology, Dalian University of Technology）與 Air Force Communications NCO Academy（大連），共 7 位作者；第一作者 Yang Zhong。[(ref: main)](https://arxiv.org/abs/2610.21477)
- 論文：*Tool-Augmented Large Language Models for Reliable Medical Calculation from Patient Notes*，arXiv:2610.21477v1（cs.AI），2026-10-15 提交，授權 CC BY 4.0；預印本，未經同儕審查。[(ref: main)](https://arxiv.org/abs/2610.21477)
- 識別碼：arXiv [2610.21477](https://arxiv.org/abs/2610.21477)。
- 全文：[arXiv HTML 版](https://arxiv.org/html/2610.21477)。
- 資料與程式：評估資料為公開的 MedCalc-Bench Verified v1.0.7；論文在 Introduction 列出程式碼庫 <https://github.com/benjiesun/tool-augmented-medical-calculation>。[(ref: main §I; §IV-A)](https://arxiv.org/html/2610.21477#S1)
- 研究性質：完整的方法研究，不是 pilot；核心流程（規則擷取、工具生成與修復、抽取模型微調、確定性執行）都有實作，並在 1,100 題測試集上評估。只用單一 benchmark，所有自家設定都是單次執行，沒有標準差、信賴區間或顯著性檢定。[(ref: main §IV-A; Table II)](https://arxiv.org/html/2610.21477#S4.T2)
- 證據邊界：本文數值以 arXiv v1 HTML 版的正文與 Table I–VII 為準；Fig. 3、Fig. 4 只有圖、正文未給各模型或各類別的數值，本文不引述其讀值；程式碼庫內容未納入引述。

**編輯：** Clare

作者把「從病歷算醫療計算器分數」拆成兩段：先由 GPT-5.5 依擷取到的規則為 MedCalc-Bench Verified 的 55 個計算器各寫一支 Python 工具、用訓練例驗證與修復後快取，再讓 LoRA 微調的 Qwen3-8B 只負責把病歷填成計算器需要的參數、交給工具算；這套流程在 1,100 題測試集上得到 86.73% final-answer accuracy，比同一個 Qwen3-8B 的 one-shot prompting（62.73%）高 24.0 個百分點，與外部報告的 Claude Sonnet 4.6 code agent（86.24%）相當，146 題錯誤中有 80 題出在參數抽取。[(ref: main Table II; §V)](https://arxiv.org/html/2610.21477#S4.T2)

## 流程

![工具增強醫療計算流程示意圖。上方標題為 Built once per calculator (55 calculators)，上排三個方塊由左到右以實線箭頭相連：淺藍色方塊「1. Rule-grounded spec retrieval」（在 MDCalc 等計算器資源搜尋、已存在則重用；rule-curation LLM 輸出 JSON spec，rule = {name, inputs, formula, conditions, output}，schema S_c 含 required fields、value kinds、allowed units、categorical enums；55 個 schema 共 328 個 required fields）→ 淺藍色方塊「2. Tool synthesis and validation」（GPT-5.5 依 rule 與 schema 寫 Python calc(relevant)；在同一計算器的 8 個隨機訓練例上執行，錯誤與不符回饋給模型，最多 4 輪修復；驗證後快取重用）→ 灰色方塊「Cached artifacts」（rule 與 schema S_c、可執行工具 calc()、每個計算器 3 個 demonstrations，即公開 exemplar 加 2 個補足欄位覆蓋的訓練例，不用測試例）。灰色方塊以兩條實線箭頭分別指向下排的淺綠色方塊「3. Schema-constrained extraction」（輸入病歷、問題、計算器、schema S_c 與 3 個 demonstrations；抽取模型 Qwen3-8B + LoRA，rank 16、alpha 32、dropout 0.05；輸出一個 JSON 物件 z，量測值寫成 [value, unit]，無依據的欄位填 null）與淡橘色方塊「4. Deterministic execution」（載入快取工具，y = calc(z)，此階段 LLM 不做算術或套公式，答案由官方 MedCalc-Bench Verified evaluator 評分）。下排由左到右以實線箭頭相連：淺綠色方塊 → 淡橘色方塊 → 灰色方塊「Evaluation」（MedCalc-Bench Verified：10,538 training／1,100 test instances；final-answer accuracy、parameter matching rate (PMR)、tool-level accuracy，後者以 gold parameters 執行工具）。圖底標題為 Run for every case (patient note + question)](assets/tool-augmented-medical-calculation-pipeline.png)

圖：本書庫依論文 §III、§IV-A 與 Table I 的文字重繪的流程示意圖，只含設計層級的設定與資料計數，不含結果數值，未複製論文原圖（論文 Fig. 1 以 Cockcroft–Gault 肌酸酐清除率計算器示範整體流程，Fig. 2 為三段 prompt 的濃縮版）。[(ref: main §III; Fig. 1; Fig. 2)](https://arxiv.org/html/2610.21477#S3.F1)

## 背景／問題

醫療計算器把病人的觀察值轉成臨床數值或分數，例如肌酸酐清除率、HEART Score 或類固醇劑量換算；要從自由文字病歷算出來，模型得先找對計算器規則、從病歷抽出每個變數、做算術，再依指定格式輸出答案。[(ref: main Abstract; §I)](https://arxiv.org/html/2610.21477#S1)

作者主張，讓 LLM 一次生成答案時，這四件事糾纏在同一步裡，公式幻覺或小算術錯誤會悄悄改變答案，也難以判斷錯在哪一步。這個前提有證據支撐：作者引用 MedCalc-Bench 原始研究對直接 prompting 不可靠的結果，以及 AgentMD 等研究顯示把算術交給已驗證計算器可減少數值錯誤；論文自己的基線也呈現同一現象，同一個 Qwen3-8B 直接 prompting 只有 14.00%。[(ref: main §I; §II; Table II)](https://arxiv.org/html/2610.21477#S2)

作者另指出兩個缺口：既有的工具代理多半假設已有人手寫好的計算器庫，覆蓋範圍受限；而原始 MedCalc-Bench 經醫師稽核發現有錯誤、模糊或無法計算的題目，因此本研究改用修正後的 MedCalc-Bench Verified。[(ref: main §I; §II-A; §IV-A)](https://arxiv.org/html/2610.21477#S4.SS1)

## 方法摘要

**任務。** 輸入是病歷 n 與計算問題 q，輸出答案 y 必須符合參考計算器與 benchmark 規定的輸出格式（output contract）。[(ref: main §III-A)](https://arxiv.org/html/2610.21477#S3.SS1)

**三段式流程。**

- **Rule-grounded specification retrieval** — 依問題到 MDCalc 等計算器資源找目標計算器，由 rule-curation LLM 把檢索到的證據整理成 JSON：rule 含 name、inputs、formula、conditions、output 五個欄位，schema 列出所有輸入欄位的值型別、允許單位與類別值；已處理過的計算器直接重用。[(ref: main §III-B; Eq. 5)](https://arxiv.org/html/2610.21477#S3.SS2)
- **Executable tool synthesis and validation** — tool-writing LLM 依 rule 與 schema 寫出 Python `calc(relevant)`，在同一計算器的 8 個訓練例上執行，把執行錯誤、缺欄位與答案不符回饋給模型，最多修 4 輪；通過後快取，之後同一計算器的題目都重用這支工具。[(ref: main §III-C)](https://arxiv.org/html/2610.21477#S3.SS3)
- **Schema-constrained extraction and execution** — 微調過的 Qwen3-8B 讀病歷、問題、schema 與 3 個同計算器範例，只輸出 schema 要求的欄位；接著執行快取的工具算出答案，這一步 LLM 不做任何公式套用或算術。[(ref: main §III-D)](https://arxiv.org/html/2610.21477#S3.SS4)

**模型分工。** 主設定由 GPT-5.5 生成工具，Qwen3-8B 負責抽取；工具生成另以 GPT-5.3-Codex 與 Qwen3.5-Plus 比較。作者的理由是工具每個計算器只建一次，抽取卻每題都要跑，因此抽取交給可在本地部署的小模型。[(ref: main §III-D; §IV-A; Table III)](https://arxiv.org/html/2610.21477#S4.T3)

**指標。** Final-answer accuracy 由 benchmark 官方 evaluator 判定；parameter matching rate（PMR）是抽出的必要參數與 gold annotation 相符的比例；tool-level accuracy 是用 gold parameters 執行工具得到的正確率，用來單獨衡量工具品質。[(ref: main §IV-A)](https://arxiv.org/html/2610.21477#S4.SS1)

## 方法詳解

**工具的程式要求。** Tool-writing prompt 要求輸出 strict JSON，內含 `required_entities` 與 `tool_code`；程式要能接受純量、`[value, unit]`、tuple 或 dict 形式的輸入，內建數字、文字、布林、日期與單位的解析函式，實作公式或計分規則、分支、邊界情況、四捨五入與輸出格式，必要輸入缺漏時回傳 benchmark 規定的缺值輸出，且必須是確定性、無外部相依的程式。[(ref: main §III-C; Fig. 2)](https://arxiv.org/html/2610.21477#S3.F2)

**驗證例怎麼挑。** 每個計算器的 8 個驗證例從訓練集依計算器 ID 分組後隨機不放回抽出，不依難度或欄位覆蓋挑選，4 輪修復都重用同一組 8 例；作者自己指出 8 個隨機例不保證涵蓋所有分支與邊界。[(ref: main §III-C)](https://arxiv.org/html/2610.21477#S3.SS3)

**抽取的輸出規則。** 抽取模型只輸出一個 JSON 物件、只含 schema 要求的鍵：量測值寫成 `[value, unit]` 並盡量保留原始單位；病歷沒有依據的必要欄位填 null；沒提到的布林條件填 false；類別欄位有明確否定證據時對應到否定的類別值。[(ref: main §III-D; Fig. 2)](https://arxiv.org/html/2610.21477#S3.F2)

**範例怎麼選。** §IV-A 描述的作法是每個計算器先放公開的 exemplar，再以貪婪方式加入兩個能補足尚未覆蓋欄位的訓練例，3 個範例合計覆蓋全部 328 個必要欄位，不使用任何測試例；範例對每個計算器固定，不是逐題檢索。[(ref: main §IV-A)](https://arxiv.org/html/2610.21477#S4.SS1)

**抽取模型的微調設定。** Qwen3-8B 凍結 base model、加 LoRA adapter，rank／alpha／dropout 為 16／32／0.05，learning rate 5×10⁻⁵，5 個 epoch，global batch size 8，最大序列長度 8,192。[(ref: main Table I)](https://arxiv.org/html/2610.21477#S4.T1)

- **論文未交代** — 抽取模型 SFT 用了多少訓練例、gold parameters 從哪裡來，以及訓練用的硬體。
- **論文未交代** — Table II 的 SFT-only 基線怎麼做；它的 69.46% 與 Table IV「No tool」（由微調的 Qwen3-8B 直接生成答案）相同，但論文沒說兩者是同一設定。
- **論文未交代** — 所有模型的解碼設定（temperature 等）與執行次數；驗證例「通過」的判定門檻，以及 4 輪修復後仍未通過的工具如何處理。
- **論文未交代** — Table III「Direct generation」的確切定義（正文只暗示是不做檢索與修復的工具生成）與 runtime errors 的計算方式；檢索與修復兩者各自的貢獻沒有拆開。
- **論文未交代** — 範例選擇在 §III-D 寫成由 case retriever 選 k=3 個同計算器例子，與 §IV-A 的固定、覆蓋導向選法不一致；Introduction 提到最佳設定 PMR 為 97.47%，但沒有任何表格列出這個數值。

## 資料與實驗

**資料。** 評估資料為 MedCalc-Bench Verified v1.0.7，這是 MedCalc-Bench 修正標籤、輸出格式、規格與參考實作後的版本。[(ref: main §IV-A)](https://arxiv.org/html/2610.21477#S4.SS1)

| 項目 | 數值／內容 |
|---|---|
| 計算器數 | 55 |
| 計算器類別 | physical-measurement、laboratory-test、date、dosage、risk、diagnosis、severity（論文未給各類題數） |
| 訓練集 | 10,538 instances（工具驗證例與抽取範例取自此集） |
| 測試集 | 1,100 instances |
| Schema 必要欄位 | 55 個 schema 共 328 個 required fields |
| 每個計算器的工具驗證例 | 8 個（訓練集隨機抽） |
| 每個計算器的抽取範例 | 3 個（公開 exemplar ＋ 2 個訓練例） |

資料來源：[(ref: main §IV-A)](https://arxiv.org/html/2610.21477#S4.SS1)

**主要結果（Table II，MedCalc-Bench Verified 測試集）。** 星號表示該數值是在子測試集上報告；前四列為其他研究報告的數值，作者定位為脈絡參考，不是同條件比較。[(ref: main Table II)](https://arxiv.org/html/2610.21477#S4.T2)

| Method | Model | Score (%) |
|---|---|---|
| MedRaC* | LLaMA3.1-8B-Instruct | 64.68 |
| Open-book guided prompting | GLM-4.6V | 82.00 |
| Open-book prompting* | GLM-4.7 | 85.50 |
| Code agent (Python REPL) | Claude Sonnet 4.6 | 86.24 |
| Direct prompting | Qwen3-8B | 14.00 |
| Zero-shot CoT | Qwen3-8B | 31.55 |
| One-shot prompting | Qwen3-8B | 62.73 |
| One-shot prompting | DeepSeek-R1-Distill-Qwen-7B | 55.45 |
| One-shot prompting | Llama-3.1-8B | 38.36 |
| SFT-only | Qwen3-8B | 69.46 |
| Ours | GPT-5.5 tool generation + Qwen3-8B-SFT extraction | 86.73 |

**工具品質（Table III）。** Tool acc. 以 gold parameters 執行工具；Final acc. 搭配同一個 Qwen3-8B-SFT 抽取模型。[(ref: main Table III)](https://arxiv.org/html/2610.21477#S4.T3)

| Tool setting | Model | Runtime errors | Tool acc. (%) | Final acc. (%) |
|---|---|---|---|---|
| Direct generation | GPT-5.5 | 0 | 74.45 | 73.27 |
| Retrieval + repair | Qwen3.5-Plus | 21 | 84.45 | 76.18 |
| Retrieval + repair | GPT-5.3-Codex | 4 | 89.00 | 82.82 |
| Retrieval + repair | GPT-5.5 | 0 | 94.91 | 86.73 |

**元件消融（Table IV）。** [(ref: main Table IV)](https://arxiv.org/html/2610.21477#S4.T4)

| Variant | Final acc. (%) | Δ |
|---|---|---|
| Full workflow | 86.73 | – |
| No extractor SFT | 83.73 | -3.00 |
| No schema/few-shot | 79.18 | -7.55 |
| No tool | 69.46 | -17.27 |

**建構與推論成本（Table V、Table VI）。** 為 55 個計算器建工具時，GPT-5.5 呼叫 147 次、共 599,212 tokens（輸入 227,454、輸出 371,758）；Qwen3.5-Plus 為 144 次、390,921 tokens，GPT-5.3-Codex 為 159 次、397,657 tokens。固定 Qwen3-8B-SFT 抽取模型、在兩張 NVIDIA RTX 5090 上跑完 1,100 題，GPT-5.5 工具庫（retrieval + repair）共 47.17 分鐘、平均每題 2.573 秒；時間不含工具建構，作者說明這是平均吞吐量而非單次請求延遲，論文未報告金額成本。[(ref: main Table V)](https://arxiv.org/html/2610.21477#S4.T5) [(ref: main Table VI)](https://arxiv.org/html/2610.21477#S4.T6)

## 結果

- **整體準確率** — 完整流程 86.73%，比同模型 one-shot prompting 高 24.00 個百分點、比 SFT-only 高 17.27 個百分點；與外部報告、五次平均的 Claude Sonnet 4.6 code agent（86.24%）只差 0.49 個百分點，作者明言這個差距不能證明統計上較優。[(ref: main Table II; §IV-B)](https://arxiv.org/html/2610.21477#S4.T2)
- **工具品質決定上限** — 用 gold parameters 時，GPT-5.5 經檢索與修復的工具 tool-level accuracy 為 94.91%，沒有 runtime error；不做檢索與修復的直接生成只有 74.45%，最終準確率從 86.73% 降到 73.27%。不同的工具生成模型差距也明顯，Qwen3.5-Plus 的工具有 21 次 runtime error、最終 76.18%。[(ref: main Table III; §IV-C)](https://arxiv.org/html/2610.21477#S4.T3)
- **消融** — 拿掉工具執行、改由微調模型直接生成答案時降幅最大（-17.27）；拿掉 schema 與範例降 7.55；把微調抽取模型換回原始 Qwen3-8B 只降 3.00。[(ref: main Table IV; §IV-F)](https://arxiv.org/html/2610.21477#S4.T4)
- **抽取模型與 PMR** — 固定 GPT-5.5 工具、比較 Qwen3、Qwen2.5、Llama、GLM 系列抽取模型時，PMR 越高通常最終準確率越高，Qwen3 最好；但 GLM-4 的 PMR 高、最終準確率卻沒有跟著提高。[(ref: main §IV-D; Fig. 3)](https://arxiv.org/html/2610.21477#S4.SS4)
- **類別差異** — Physical-measurement 與 laboratory-test 類計算器表現最好；date 類的 PMR 與最終準確率落差最明顯；需要臨床語意判斷的 risk、diagnosis、severity 類最難。論文只以圖呈現，正文沒有各類別的數值。[(ref: main §IV-E; Fig. 4)](https://arxiv.org/html/2610.21477#S4.SS5)
- **錯誤分析** — 146 題錯誤中 80 題為抽取錯誤、66 題為生成工具錯誤。案例中，HEART Score 一題因抽取模型沒有從使用 atorvastatin 推得高膽固醇血症而少算一分（模型 4、答案 5）；Steroid Conversion 一題因工具的正規化規則先比對到「cortisone」而非「hydrocortisone」，算出 4.89 mg（答案 6.029 mg）。Estimated Gestational Age 的錯誤來自日期處理與輸出格式，Wells PE、FeverPAIN、Charlson Comorbidity Index 與 HEART Score 主要是輸入抽取錯誤。[(ref: main §V; Table VII; Fig. 5)](https://arxiv.org/html/2610.21477#S5)

## 限制

作者列出的限制：[(ref: main §V; §VI)](https://arxiv.org/html/2610.21477#S6)

- **隱含資訊** — 需要推論隱含條件（例如由用藥推得的病況）、否定或時間關係時，抽取仍會出錯。
- **工具錯誤** — 生成工具會在正規化規則、公式分支或輸出格式上出錯。
- **未測泛化** — 測試題是新病歷，但計算器與工具建構時用的是同一批 55 個；對沒見過的計算器的泛化與臨床部署都沒有測試。
- **方法範圍** — 沒有加入強化學習或代理式的參數驗證。

本書庫另外注意到的限制：

- **單次結果** — 自家設定都只報告單次結果，沒有標準差、信賴區間或顯著性檢定；與外部數值的比較混合了子測試集、五次平均與不同模型，不是同條件對照。[(ref: main Table II)](https://arxiv.org/html/2610.21477#S4.T2)
- **單一 benchmark** — 只在 MedCalc-Bench Verified 上評估，病歷與題目都來自 benchmark，沒有真實病歷或臨床人員參與的評估。[(ref: main §IV-A)](https://arxiv.org/html/2610.21477#S4.SS1)
- **工具驗證覆蓋** — 每個工具只用 8 個隨機訓練例驗證，作者自己也承認不保證涵蓋分支與邊界；Steroid Conversion 的字串比對錯誤就是這類漏網之魚。[(ref: main §III-C; Table VII)](https://arxiv.org/html/2610.21477#S5.T7)
- **重現細節** — SFT 資料量、解碼設定、驗證通過門檻等缺漏見「方法詳解」的論文未交代項目。

## 與書庫其他文章的關係

VoxelSage 把肝腫瘤的幾何量測寫成確定性技能、讓 LLM 只負責調度，本篇則把醫療計算器的公式寫成由 LLM 生成並驗證的 Python 工具、讓 LLM 只負責抽參數，兩篇都是「算的部分交給程式」，但本篇有拿掉工具的消融與 1,100 題基準，VoxelSage 缺少這組對照: [量測交給程式、LLM 只負責調度：VoxelSage 的肝腫瘤 CT 工具代理，證據停在系統測試與模擬器](2026-10-06-voxelsage-liver-ct-tool-agent.md)

頸動脈斑塊那篇把 AHA 分型規則寫進 prompt、仍由 LLM 自己套規則，本篇則把計算規則寫成程式、LLM 只填輸入，兩篇並讀可對照「規則放在 prompt」與「規則放在程式」兩種把臨床規則交給 LLM 的做法: [把 AHA 分型規則寫進 prompt，8B 本地模型從 38.9% 升到 81.5%：頸動脈斑塊 MRI 報告的 LLM 輔助判讀，四位放射科醫師對文字參考標準的一致率從 69% 升到 85%（8B）與 90%（671B DeepSeek-R1）](2026-10-19-llm-carotid-plaque-aha-report-reader-study.md)

該研究的作者在 Discussion 提議讓 LLM 只抽冠狀動脈的血管層級發現、再由規則引擎決定 CAD-RADS 類別，與本篇「規則寫成程式、LLM 只抽參數」的做法相同，但該研究本身只測了零樣本直接分類: [三個聊天介面零樣本讀 CCTA 報告分 CAD-RADS：DeepSeek-R1 與 ChatGPT-5 約八成、ChatGPT-4o 54%，900 份高風險報告被降到 3 以下的比例 2.6%–14.1%](2026-10-22-llm-cad-rads-ccta-report-classification.md)

## 實務的啟發

- **把「讀病歷」與「算分數」拆開來量** — 論文用 PMR、tool-level accuracy 與 final-answer accuracy 三個指標分別衡量抽取、工具與整體，146 題錯誤也能歸到抽取或工具其中一邊；評估任何從病歷算臨床分數的系統時，這種拆法可以直接借用，至少能知道錯誤該回頭修哪一段。
- **生成的工具要當成程式碼來審** — 本研究的工具只以 8 個隨機訓練例驗證，Steroid Conversion 的字串比對錯誤顯示這樣的測試抓不到所有分支；若要借用「LLM 寫計算器」的做法，產出的工具仍需要人工審閱與涵蓋邊界情況的測試，不能把通過 8 例視為已驗證。
- **結果仍待外部驗證** — 86.73% 是單一 benchmark、單次執行、計算器與工具建構重疊下的數字，與最強外部結果的差距也不具統計意義；它支持「工具化能明顯勝過同一個小模型直接作答」，但還不足以說明在真實病歷或未見過的計算器上同樣可靠。
- **剩下的錯在臨床語意** — 一半以上的錯誤來自抽取，且集中在需要推論的 risk、diagnosis、severity 類計算器；即使工具正確，從用藥推病況、處理否定與時間這類判斷仍是病歷抽取的老問題，值得作為驗證重點。

## References

- **main** — Zhong Y, Luo L, Zhu X, Wang Y, Sun Y, Wang J, Lin H. *Tool-Augmented Large Language Models for Reliable Medical Calculation from Patient Notes*. arXiv:2610.21477v1 [cs.AI], 2026. Abstract：<https://arxiv.org/abs/2610.21477>；全文 HTML：<https://arxiv.org/html/2610.21477>。文內引用位置：Abstract、§I Introduction、§II Related Work、§III Method（III-A–III-D、Eq. 5）、§IV Experiments（IV-A–IV-G）、§V Case Study and Error Analysis、§VI Conclusion；深鏈 [§I](https://arxiv.org/html/2610.21477#S1)、[§II](https://arxiv.org/html/2610.21477#S2)、[§III-A](https://arxiv.org/html/2610.21477#S3.SS1)、[§III-B](https://arxiv.org/html/2610.21477#S3.SS2)、[§III-C](https://arxiv.org/html/2610.21477#S3.SS3)、[§III-D](https://arxiv.org/html/2610.21477#S3.SS4)、[§IV-A](https://arxiv.org/html/2610.21477#S4.SS1)、[§V](https://arxiv.org/html/2610.21477#S5)、[§VI](https://arxiv.org/html/2610.21477#S6)、[Fig. 1](https://arxiv.org/html/2610.21477#S3.F1)、[Fig. 2](https://arxiv.org/html/2610.21477#S3.F2)、[Fig. 3](https://arxiv.org/html/2610.21477#S4.F3)、[Fig. 4](https://arxiv.org/html/2610.21477#S4.F4)、[Table I](https://arxiv.org/html/2610.21477#S4.T1)、[Table II](https://arxiv.org/html/2610.21477#S4.T2)、[Table III](https://arxiv.org/html/2610.21477#S4.T3)、[Table IV](https://arxiv.org/html/2610.21477#S4.T4)、[Table V](https://arxiv.org/html/2610.21477#S4.T5)、[Table VI](https://arxiv.org/html/2610.21477#S4.T6)、[Table VII](https://arxiv.org/html/2610.21477#S5.T7)。

[Home](../) · [AI Papers](./)
