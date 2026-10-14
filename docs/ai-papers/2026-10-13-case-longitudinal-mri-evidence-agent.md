---
catalog_id: "arxiv:2609.39566"
editors:
  - "Clare"
refs:
  main:
    title: "From Given to Gathered Evidence: Agentic Learning for Longitudinal Medical Reasoning"
    url: "https://arxiv.org/pdf/2609.39566v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 不把影像餵給模型，讓它自己去調：CASE 在 UK Biobank 縱向 MRI 上訓練 8B 證據蒐集代理，問題是標籤不一定看得見

## 來源

- 團隊：Minye Shao（Durham University；DAMO Academy, Alibaba Group）、Chaohui Yu（DAMO Academy；Hupan Laboratory，通訊作者）、Yixuan Wu、Fan Wang（DAMO Academy）、Ling Shao（University of the Chinese Academy of Sciences）、Yang Long（Durham University，通訊作者）；另列 Jing Wang、Hangjie Yuan、Shang Liu（DAMO Academy；Hupan Laboratory）為 contributors。[(ref: main)](https://arxiv.org/pdf/2609.39566v1)
- 論文：*From Given to Gathered Evidence: Agentic Learning for Longitudinal Medical Reasoning*，arXiv v1，2026-09-30 提交，分類 cs.CV，目前只有一個版本。[(ref: abs)](https://arxiv.org/abs/2609.39566)
- 識別碼：[arXiv:2609.39566](https://arxiv.org/abs/2609.39566)。
- 全文：[arXiv PDF v1](https://arxiv.org/pdf/2609.39566v1)（arXiv 未提供 HTML 版）。
- 資料與程式：研究使用 UK Biobank（申請編號 603483）。作者表示將釋出實作、紀錄的軌跡、基準與評估程式、prompt 與訓練設定；UK Biobank 的個人層級資料不能直接轉散布，基準將透過 UKB-RAP 提供給核准的研究者。[(ref: main Ethics／Reproducibility Statement)](https://arxiv.org/pdf/2609.39566v1)
- 研究性質：完整方法論文，不是 pilot；核心方法有實作、訓練並在 455 位受試者、4,850 題的保留測試集上評估。題目的正確答案來自醫師診斷與 ICD-10 紀錄，**不是**由放射科醫師依影像判讀產生，論文也沒有臨床人員審核題目或標籤；推理品質與部分訓練訊號由大型語言模型（large language model, LLM）評審給分。[(ref: main §4, §5, §7)](https://arxiv.org/pdf/2609.39566v1)
- 證據邊界：本文數值以 PDF v1 的正文、Table 1–3 與 Table 7 為準。附錄 C–I（含 baseline 的 prompt、訓練超參數表、對 teacher 的 participant-bootstrap 區間 Table 14、移除證據來源的消融 Table 16）未納入引述。

**編輯：** Clare

作者把縱向醫療推理改寫成「代理自己調閱影像、分割量測與報告再作答」的任務，在 UK Biobank 前後兩次 MRI 上建了 50,401 題的基準，並把 Qwen3-VL-8B 後訓練成 CASE；在保留測試集上，CASE 的 Micro 準確率 76.1%，高於同樣拿到相同工具的 GPT-5.4（65.3%）與 Claude Opus 4.8（68.6%），但「受影響的疾病系統」一類所有模型都只有 2.9–10.9%，而答案來自診斷紀錄、未必能從影像看出。[(ref: main Abstract, §4, §6.2 Table 1)](https://arxiv.org/pdf/2609.39566v1)

## 流程

![CASE 研究設計示意圖。上排三個方塊：左邊藍色方塊為 UK Biobank 縱向基準（4,739 位受試者、50,401 題、前後兩次 MRI 中位間隔 2.26 年、心臟／腦／胰臟／肝臟／全身五個器官區域、10 個題型分層、標籤來自醫師診斷與 ICD-10 紀錄、保留集 455 人 4,850 題）；中間綠色方塊為同一個 Qwen3-VL-8B-Instruct 策略配三種角色 prompt：Radiologist 3 個工具、上限 6 次呼叫，Anatomist 3 個工具、上限 4 次，Consultant 10 個工具、上限 12 次（含 MedGemma-27B 報告與 recall_skills／write_skill）；右邊橘色方塊為後訓練：teacher Qwen3.8-Max 147,434 筆紀錄、RSFT 篩選條件（至少一次工具呼叫、可解析的 insight、Kimi K2.6 評分 ≥ 0.4），以及每題 8 個 rollout 的 agentic RL（GRPO、RLAIF、OPSD）。左右兩個方塊各以箭頭指向中間方塊，中間方塊再以箭頭向下接到灰色方塊：最終回應的五個階段 P1 plan → P2 multi-source review → P3 cross-visit comparison → P4 key insight → P5 answer，以及評分方式](assets/case-longitudinal-mri-evidence-agent-design.png)

圖：本書庫依論文 §4、§5、Table 7 的文字與 Fig. 1、Fig. 2 圖說重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖。[(ref: main §4–5, Table 7)](https://arxiv.org/pdf/2609.39566v1)

## 背景／問題

既有的醫療視覺語言模型（vision-language model, VLM）評估多半把影像與病史一次交給模型、再看答案。作者主張縱向推理不是這樣運作：證據散落在病歷、不同影像序列、量測與追蹤檢查之間，需要先決定要看什麼、再去取得。作者在引言中把這個主張連到代理與互動式基準的一般文獻，**沒有提供「這種任務設計較貼近臨床判讀」的實證**；這是論文的立論框架，本研究檢驗的是在此框架下，小模型能否學會蒐集與綜合證據。[(ref: main §1)](https://arxiv.org/pdf/2609.39566v1)

因此論文同時做兩件事：建立一個答案被藏起來、證據要靠工具調閱的縱向 MRI 基準，以及提出一套讓 8B VLM 學會「去找證據」而不只是模仿 teacher 的後訓練方法。[(ref: main §1, §3)](https://arxiv.org/pdf/2609.39566v1)

## 方法摘要

**基準。** 以 UK Biobank 的 Instance 2（基線）與 Instance 3（追蹤）MRI 為環境，前後兩次中位間隔 2.26 年，涵蓋心臟、腦、胰臟、肝臟與全身五個器官區域。4,739 位受試者共 50,401 題，分 10 個任務 × 題型分層（是非、單選、多選）；答案來自醫師診斷與 ICD-10 紀錄，誘答選項從世代中抽、排除受試者自己的診斷。受試者以 MD5 雜湊切分，保留集 455 人、4,850 題。[(ref: main §4, Table 3)](https://arxiv.org/pdf/2609.39566v1)

**代理。** CASE 是同一個策略模型配三種角色 prompt 與工具清單：Radiologist 調閱與比對 MRI 影像，Anatomist 用 Vista3D 分割的量測與疊圖看器官變化，Consultant 可用前兩者的全部工具，另外能讀 MedGemma-27B 預先產生的報告、調用與寫入文字技能。論文明言三個角色不是分別訓練的模型，也不是彼此對話的委員會。最終回應分五個階段：plan、multi-source review、cross-visit comparison、key insight（P4）、answer（P5）。[(ref: main §5.1, Table 7)](https://arxiv.org/pdf/2609.39566v1)

**後訓練。** 先用 teacher（Qwen3.8-Max）的工具互動紀錄做 rejection-sampling supervised fine-tuning（RSFT，以篩選後的示範做監督式微調），再做 agentic reinforcement learning（RL）：每題 8 個 rollout，以 Group Relative Policy Optimization（GRPO）優化答案正確性與格式，加上 LLM 評審的 rubric 回饋（reinforcement learning from AI feedback, RLAIF）與 on-policy privileged self-distillation（OPSD）。[(ref: main §5.2–5.5)](https://arxiv.org/pdf/2609.39566v1)

**評估。** 主要指標是 first-pass exact answer-set accuracy：答案集合與參考答案完全相同才算對，缺漏、失敗或無法解析記 0 分。Micro 每題等權，Macro 對 10 個分層等權；Table 1 為三個角色的平均。另有 Insight 分數（0–1），由一個固定版本、未用於訓練獎勵的外部評審判斷 P4 insight 與 P5 答案的邏輯連結。[(ref: main §6.1)](https://arxiv.org/pdf/2609.39566v1)

## 方法詳解

**任務形式。** 每題給代理一個 prompt（角色、臨床問題、選項與初始病人脈絡），參考答案在互動期間不揭露；代理面對的是該受試者專屬、可重播的證據環境。論文沒有把它寫成 POMDP，而是寫成會與工具互動的策略。[(ref: main §3)](https://arxiv.org/pdf/2609.39566v1)

**資訊邊界。** 代理看得到的文字只有敘述脈絡與一題問題。MedGemma-27B 報告是離線從固定的 MRI montage 產生，快取前移除其中的 ICD-10 代碼，檢索時再遮蔽類似 ICD 的字串，每次最多回傳相關摘要欄位的 400 個字元。[(ref: main §4, Appendix A)](https://arxiv.org/pdf/2609.39566v1)

**誘答選項。** 目標答案搭配從世代抽出的誘答選項，排除受試者自己的診斷；ICD-10 題補足到四個誘答，心血管與呼吸道題用 max(2, 4 − n+) 個誘答，部分題目加入「None of the above」。[(ref: main Appendix A)](https://arxiv.org/pdf/2609.39566v1)

**工具與呼叫上限。** Anatomist：`vista3d_segment`、`vista3d_compare_stations`、`vista3d_compare_visits`，上限 4 次；Radiologist：`list_available_images`、`view_image`、`compare_visits`，上限 6 次；Consultant：前六個工具加上 `list_available_reports`、`get_report`、`recall_skills`、`write_skill`，共 10 個，上限 12 次。互動另限最多 10 個 assistant 回合、6,144 個續寫 token、每次工具回應 2,048 token。[(ref: main Table 7, §5.3)](https://arxiv.org/pdf/2609.39566v1)

**RSFT。** teacher Qwen3.8-Max 產生 147,434 筆紀錄，保留至少有一次工具呼叫、P4 insight 可解析，且 Kimi K2.6 評分至少 0.4 的軌跡，正文稱保留約 140,000 筆示範。篩選條件**不要求答案正確**。[(ref: main §4, §5.2)](https://arxiv.org/pdf/2609.39566v1)

**Agentic RL 的獎勵。** 每題 8 個 rollout（G = 8）；結果獎勵為答對 +1、答錯 −1、無法解析 −2，另加格式項、Kimi K2.6 的 rubric 分數，以及每組前兩名 insight 的 linkage 獎勵。OPSD 讓同一策略在額外拿到提示（參考答案、可解析的選項文字，以及選擇性的已紀錄 insight）時充當 self-teacher，以前 128 個 token 截斷的 Causal-KL 計算學生與它的差距，作為懲罰從每個 rollout 的回報中扣除。[(ref: main §5.3–5.5)](https://arxiv.org/pdf/2609.39566v1)

**比較條件。** 論文稱同一表內的方法共用 prompt、病人證據、執行上限與解析規則，所有方法都拿到相同工具；跨角色的比較只作描述用途。[(ref: main §6.1–6.2)](https://arxiv.org/pdf/2609.39566v1)

- **論文未交代** — 摘要寫 SFT 使用「14,734 條」前沿模型互動軌跡，正文則寫 147,434 筆紀錄、保留約 140,000 筆示範；兩個數字差約十倍，正文沒有解釋。[(ref: main Abstract, §4)](https://arxiv.org/pdf/2609.39566v1)
- **論文未交代** — 代理一開始拿到的「初始病人脈絡」敘述包含哪些欄位，以及它與答案來源（診斷與 ICD-10 紀錄）之間如何隔離；正文只說明報告中的 ICD 字串會被遮蔽。[(ref: main §3, §4)](https://arxiv.org/pdf/2609.39566v1)
- **論文未交代** — Insight 分數所用的固定外部評審是哪個模型（正文只說它版本固定、未用於訓練獎勵，名稱在附錄）；題目樣板的具體寫法（正文只說原始題目生成器建構五種基本任務）。[(ref: main §4, §6.1)](https://arxiv.org/pdf/2609.39566v1)
- **論文未交代（正文範圍內）** — 解碼設定、重複次數與學習率等超參數放在附錄；本文引用的 Table 1 與 Table 2 都是單次點估計，沒有信賴區間。

## 資料與實驗

下表整理論文 Table 3 的十個分層（B 是非題、S 單選、M 多選）。[(ref: main Table 3)](https://arxiv.org/pdf/2609.39566v1)

| 分層 | 題型 | 題數 |
|---|---|---|
| Cancer | B | 4,710 |
| Diabetes | B | 4,718 |
| Cardiovascular condition identification | S | 4,685 |
| Cardiovascular condition set | M | 4,739 |
| Essential hypertension（I10） | B | 4,037 |
| Respiratory／allergy condition identification | S | 5,013 |
| Respiratory／allergy condition set | M | 4,733 |
| Multisystem ICD-10 condition identification | S | 10,092 |
| Multisystem affected disease systems | M | 3,637 |
| Medical history | B | 4,037 |
| 合計 | — | 50,401 |

題型合計：是非 17,502（34.7%）、單選 19,790（39.3%）、多選 13,109（26.0%）。保留測試集為 455 位受試者、4,850 題；論文沒有直接列出訓練集的受試者與題數。[(ref: main §4)](https://arxiv.org/pdf/2609.39566v1)

下表整理受試者的影像組合（W 全身 Dixon、H 心臟 cine、P 胰臟、B 腦、L 肝臟 IDEAL）。[(ref: main Appendix A)](https://arxiv.org/pdf/2609.39566v1)

| 器官群數 | 組合（受試者數） | 小計 |
|---|---|---|
| 3 | WHP 1,404；WHB 929；WHL 527；WPB 438；WPL 267；WBL 1 | 3,566 |
| 2 | WH 843；HB 78；WB 8 | 929 |
| 1 | B 142；H 102 | 244 |

下表重製論文 Table 1：三個角色平均的臨床準確率（%）。欄位依序為 Cancer（B）、Diabetes（B）、Cardiovascular condition（S）、Cardiovascular condition set（M）、Hypertension（B）、Respiratory condition（S）、Respiratory condition set（M）、ICD-10 condition（S）、Disease systems（M）、Medical history（B）。[(ref: main §6.2 Table 1)](https://arxiv.org/pdf/2609.39566v1)

| 方法 | Onc | Endo | CV-C | CV-S | HTN | Resp-C | Resp-S | ICD | Sys | Hist | Micro | Macro |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Qwen3-VL-8B（base） | 67.7 | 46.1 | 72.9 | 70.0 | 38.4 | 52.5 | 49.3 | 26.9 | 5.8 | 41.1 | 46.0 | 47.1 |
| Lingshu-32B | 85.0 | 70.4 | 55.0 | 54.6 | 48.8 | 58.9 | 51.6 | 35.2 | 2.9 | 40.5 | 49.9 | 50.3 |
| Lingshu-7B | 65.4 | 83.1 | 48.6 | 40.3 | 65.8 | 50.7 | 38.6 | 28.5 | 3.3 | 42.8 | 45.5 | 46.7 |
| MedGemma-27B | 42.2 | 34.5 | 18.1 | 17.6 | 30.5 | 25.7 | 24.2 | 29.1 | 3.9 | 48.9 | 27.8 | 27.5 |
| MedGemma-1.5-4B | 55.0 | 51.8 | 37.5 | 65.1 | 48.4 | 40.7 | 44.0 | 26.9 | 3.4 | 40.9 | 40.5 | 41.4 |
| Kimi K2.6 | 48.4 | 41.5 | 41.8 | 46.5 | 41.9 | 47.8 | 42.9 | 44.2 | 4.6 | 60.1 | 42.8 | 42.0 |
| Kimi K3 | 86.8 | 91.9 | 85.4 | 91.3 | 64.3 | 91.0 | 66.9 | 59.3 | 6.4 | 51.3 | 70.2 | 69.5 |
| Qwen3.7-Plus | 87.0 | 87.5 | 89.6 | 92.2 | 72.7 | 81.2 | 67.2 | 45.1 | 6.1 | 48.2 | 67.0 | 67.7 |
| Qwen3.8-Max | 75.8 | 66.4 | 71.5 | 78.0 | 38.4 | 72.4 | 59.5 | 57.8 | 5.6 | 57.4 | 59.7 | 58.3 |
| Gemini-3.5-Flash | 71.7 | 77.7 | 65.9 | 73.3 | 53.7 | 79.7 | 53.8 | 42.2 | 3.0 | 42.2 | 56.3 | 56.3 |
| GPT-5.4-0305 | 73.0 | 89.5 | 73.4 | 81.2 | 76.8 | 84.3 | 63.3 | 49.8 | 5.4 | 59.8 | 65.3 | 65.7 |
| Claude Opus 4.8 | 73.4 | 80.2 | 77.7 | 82.2 | 57.5 | 85.9 | 68.1 | 76.3 | 8.0 | 49.0 | 68.6 | 65.8 |
| CASE（8B） | 87.8 | 94.4 | 94.0 | 92.5 | 75.7 | 94.3 | 71.8 | 69.6 | 10.9 | 59.7 | 76.1 | 75.1 |

Qwen3.8-Max 是產生 SFT 示範的 teacher；Kimi K2.6 同時是 RSFT 篩選與 RLAIF rubric 的評審。

下表重製論文 Table 2：從同一個 RSFT 起點加入各後訓練元件的消融（三個角色平均）。[(ref: main §6.3 Table 2)](https://arxiv.org/pdf/2609.39566v1)

| GRPO | RLAIF | OPSD | Micro（%） | Macro（%） | Insight（0–1） |
|---|---|---|---|---|---|
| – | – | – | 65.7 | 65.0 | 0.43 |
| ✓ | – | – | 69.3 | 68.2 | 0.47 |
| ✓ | ✓ | – | 70.6 | 69.5 | 0.63 |
| ✓ | – | ✓ | 73.8 | 72.4 | 0.57 |
| ✓ | ✓ | ✓ | 76.1 | 75.1 | 0.68 |

第一列為只做 RSFT，最後一列為完整 CASE-8B。

## 結果

- **整體準確率** — CASE 的 Micro 76.1%、Macro 75.1%，高於表中所有比較對象；Micro 次高為 Kimi K3（70.2%），其次是 Claude Opus 4.8（68.6%）與 Qwen3.7-Plus（67.0%）。摘要所稱「相對 GPT-5.4 與 Claude Opus 4.8 分別提升超過 16% 與 10%」，以 Micro 換算為 76.1／65.3 ≈ 1.165 與 76.1／68.6 ≈ 1.109（本書庫換算）。[(ref: main Abstract, §6.2 Table 1)](https://arxiv.org/pdf/2609.39566v1)
- **從 base 到 CASE** — 同一個 Qwen3-VL-8B，base 的 Micro 46.0%，只做 RSFT 為 65.7%，完整後訓練為 76.1%。[(ref: main Table 1, Table 2)](https://arxiv.org/pdf/2609.39566v1)
- **學生超過 teacher** — 提供示範的 Qwen3.8-Max 在同一測試集的 Micro 為 59.7%，低於只做 RSFT 的 CASE（65.7%）。作者在附錄 Table 14 以 participant-bootstrap 區間檢驗相對 teacher 的增益，該表本文未納入引述。[(ref: main §6.2, Table 1)](https://arxiv.org/pdf/2609.39566v1)
- **並非每一類都領先** — CASE 在 Hypertension（75.7 對 GPT-5.4 的 76.8）、ICD-10 condition（69.6 對 Claude Opus 4.8 的 76.3）與 Medical history（59.7 對 Kimi K2.6 的 60.1、GPT-5.4 的 59.8）不是最高。[(ref: main Table 1)](https://arxiv.org/pdf/2609.39566v1)
- **一個所有模型都失敗的分層** — Disease systems（多選）一欄，十三個方法介於 2.9% 到 10.9%；正文沒有討論這一欄為何普遍偏低。[(ref: main Table 1)](https://arxiv.org/pdf/2609.39566v1)
- **醫療專用模型落在後段** — 在同一套工具條件下，MedGemma-27B 的 Micro 27.8% 是全表最低，Lingshu-32B 為 49.9%，低於 Kimi K3、Qwen3.7-Plus、Qwen3.8-Max、Gemini-3.5-Flash、GPT-5.4 與 Claude Opus 4.8，只略高於 base 的 Qwen3-VL-8B（46.0%）。[(ref: main Table 1)](https://arxiv.org/pdf/2609.39566v1)
- **消融** — 在 RSFT 上只加 GRPO 為 69.3%，GRPO + RLAIF 為 70.6%，GRPO + OPSD 為 73.8%，三者全加為 76.1%；Insight 分數從 0.43 升到 0.68。作者描述沒有 OPSD 時，GRPO + RLAIF 會一味優化 rubric、答案正確性的獎勵在訓練後期崩落。[(ref: main §6.3 Table 2)](https://arxiv.org/pdf/2609.39566v1)
- **證據依賴** — 作者報告拿掉影像調閱或移除任一證據來源時準確率都會下降；具體數值在附錄 Table 16，本文未納入引述。[(ref: main §6.3)](https://arxiv.org/pdf/2609.39566v1)

## 限制

- 作者列出的限制：臨床標籤可能無法從現有影像觀察到；產生的證據（分割、報告）與評審都可能出錯；跨世代的泛化、在此世代以外的效用與效率留待未來研究；真實臨床會用到更廣的工具與各專科的流程。[(ref: main §7)](https://arxiv.org/pdf/2609.39566v1)
- 標籤來源：答案取自醫師診斷與 ICD-10 紀錄，不是依影像判讀，論文也沒有臨床人員審核。準確率因此混合了「從影像看出病變」與「從脈絡推得診斷」兩種能力，本研究沒有把兩者分開。Disease systems 一欄全部模型都在 11% 以下，也可能與這一點有關，但論文沒有分析。[(ref: main §4, §7)](https://arxiv.org/pdf/2609.39566v1)
- 評審與比較對象重疊：Kimi K2.6 既是 RSFT 篩選與 RLAIF rubric 的評審，也在 Table 1 被比較，而它自己的 Micro 只有 42.8%。Insight 分數改由一個未具名、未用於訓練獎勵的評審給分；論文沒有報告任何一個評審與臨床人員的一致性。[(ref: main §5.2, §5.5, Table 1)](https://arxiv.org/pdf/2609.39566v1)
- 比較條件的細節：論文稱所有方法共用工具與執行上限，但 baseline 的完整 prompt 在附錄；主表為單次點估計、沒有區間，前沿模型的版本代號以表中標示為準。[(ref: main §6.1–6.2)](https://arxiv.org/pdf/2609.39566v1)
- 資料存取：基準以 UK Biobank 為底，只能透過 UKB-RAP 給核准研究者使用，外部要重現需先取得資料授權。[(ref: main Reproducibility Statement)](https://arxiv.org/pdf/2609.39566v1)
- 本書庫補充：受試者為基線時 45–85 歲的 UK Biobank 影像世代，影像來自研究用的成組 MRI 協定；CASE 在這裡學到的「先調哪些序列」策略，搬到序列組合與缺漏都更不規則的院內影像是否仍成立，本研究沒有證據。[(ref: main Appendix A)](https://arxiv.org/pdf/2609.39566v1)

## 與書庫其他文章的關係

MammoClaw 讓凍結的 MLLM 從失敗軌跡歸納文字技能、不更新模型權重，CASE 則把 recall_skills／write_skill 當成代理的工具之一，並改用 RSFT 加 agentic RL 直接更新 8B 模型，兩篇對照了「改提示詞」與「改權重」兩種讓代理學會用工具的路線: [工具給齊了，凍結的 MLLM 就會讀乳房攝影嗎？MammoClaw 用失敗軌跡演化出的技能補上「怎麼用」](2026-10-01-mammoclaw-skill-evolving-mammography-agent.md)

VoxelSage 與 CASE 都把 VISTA3D 分割後的量測交給代理調用，VoxelSage 停在系統測試與模擬器，CASE 則在 4,850 題保留集上與十二個模型比較，但兩篇都沒有臨床人員參與的評估: [量測交給程式、LLM 只負責調度：VoxelSage 的肝腫瘤 CT 工具代理，證據停在系統測試與模擬器](2026-10-06-voxelsage-liver-ct-tool-agent.md)

Lingshu-32B 與 Lingshu-7B 在 CASE 的同工具條件下 Micro 準確率為 49.9% 與 45.5%，可對照 Lingshu 原論文的評估，看醫療 VLM 換成需要自己調閱證據的縱向任務後落在什麼位置: [Lingshu：醫療 VLM 如何整合影像、文字與合成資料，RL 又帶來多少改變？](2026-09-15-lingshu-medical-vlm.md)

MedGemma 家族在 CASE 裡同時扮演兩個角色：MedGemma-27B 預先產生代理可調閱的影像報告，MedGemma-1.5-4B 則是受測對象之一，在同工具條件下 Micro 準確率為 40.5%: [MedGemma 1.5：4B 模型如何讀取 3D 影像、全切片與縱向胸片？](2026-09-16-medgemma-1-5.md)

## 實務的啟發

- **「代理自己調證據」可以當作評估設計借用** — 把答案藏起來、要求模型透過工具取得影像與量測，再以完全相符的答案集合計分，比一次餵完所有資料更能看出模型有沒有去找關鍵證據。這是可借用的評估框架；它是否更貼近臨床判讀，論文沒有提供證據。
- **標籤來源要先確認看不看得見** — 若自建類似基準，答案取自診斷碼時，需要另外標出哪些題目的答案能從影像觀察到，否則準確率會混入與影像無關的推論。CASE 的 Disease systems 一欄是一個值得在自家資料上先檢查的警訊。
- **LLM 評審不宜同時當選手** — 若用 LLM 篩選訓練資料或給 rubric 分數，選一個不在比較表中的評審，並報告評審與臨床人員的一致性；CASE 的 Insight 分數與 RLAIF 收益都建立在未經臨床人員驗證的 LLM 評審上。
- **小模型可以超過 teacher，但前提要寫清楚** — 只做 RSFT 的 8B 模型就超過提供示範的 Qwen3.8-Max，說明篩選條件與工具使用紀錄本身就有訓練價值；但篩選不要求答案正確、示範筆數在摘要與正文不一致，要沿用這套資料配方前，應先等附錄與程式釋出後核對。

## References

- `main`：[From Given to Gathered Evidence: Agentic Learning for Longitudinal Medical Reasoning（arXiv PDF v1）](https://arxiv.org/pdf/2609.39566v1)；本文使用 Abstract、§1 Introduction、§3 Preliminaries、§4 benchmark、§5.1–5.5、§6.1–6.3、§7 Conclusion and Limitations、Ethics Statement、Reproducibility Statement、Appendix A，以及 Table 1、Table 2、Table 3、Table 7 與 Fig. 1、Fig. 2 圖說。arXiv 未提供 HTML 版。
- `abs`：[arXiv:2609.39566 摘要頁](https://arxiv.org/abs/2609.39566)。

[Home](../) · [AI Papers](./)
