---
catalog_id: "doi:10.64898/2026.10.07.26364991"
editors:
  - "Clare"
refs:
  main:
    title: "RadKev: An Open-Weight Decision Model for Radiology"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 不生成文字、直接給每個選項機率：RadKev 把 decision model 專科化到放射科，15 項任務平均多 4.9 點，換到外院報告卻沒有進步

## 來源

- 團隊：Udbhav Ram 與 Ran Zhang（通訊作者），兩人皆屬 University of Wisconsin–Madison 醫學物理系與放射科。[(ref: main author block)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- 論文：*RadKev: An Open-Weight Decision Model for Radiology*，medRxiv 預印本，2026-10-13 上線，未經同儕審查；論文本身標示保留所有權利、未經許可不得再利用。[(ref: abstract page)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full)
- 識別碼：DOI [10.64898/2026.10.07.26364991](https://doi.org/10.64898/2026.10.07.26364991)。
- 全文：[medRxiv 頁面](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full)、[PDF v1](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)。
- 程式與權重：資料建構、teacher 標註、訓練、評估與統計程式碼在 [GitHub](https://github.com/udiram/RadKev)；RadKev adapter 與 pointer head 權重在 Hugging Face，以 CC BY-NC-SA 4.0 限非商業研究使用，需先同意條款。[(ref: main Data availability)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- 研究性質：回顧性基準研究，不是 pilot；核心方法（在 Kev 上做放射科專科化）有實作並釋出權重。主要比較在讀取任何結果前已寫入分析計畫附錄，其餘分析作者標為探索性。只用公開資料、只有文字輸入，沒有前瞻或臨床流程內的測試。[(ref: main Methods, Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- 證據邊界：本文數值以 PDF 正文與 Table 1 為準；逐任務的 Holm 校正結果、完整 prompt 模板與超參數放在 Supplementary（Table S2、Notes S2–S3），本文未納入引述。

**編輯：** Clare

作者把一個開放權重的 decision model（一次輸出每個允許答案的機率、不生成文字）用 36,109 筆公開放射資料專科化成 RadKev-27B，在 15 項放射任務、14,142 題上的任務平均準確率比起點 Kev-27B 高 4.9 個百分點（95% CI 3.8–6.2），也高於兩個託管 decision model 與同 backbone 的 LLM；但增益集中在訓練資料來源相同的任務，在另一家機構的 RadGraph-XL 報告上，27B 版的準確率反而略降。[(ref: main Abstract, §3.1, §3.7)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

## 流程

![RadKev 研究設計示意圖。共五個圓角方塊，以四支實線箭頭相連。左上藍色方塊「1 訓練資料（Table 1）」列出公開放射資料共 36,109 筆訓練 record 與六組來源的訓練數：Structured label extraction 8,000、Report error detection 6,000、Case diagnosis and classification 2,912、Imaging appropriateness 264、Radiology knowledge 7,490、Orders, triage and follow-up 11,443。左下綠色方塊「2 Two-teacher labeling」說明只用於 orders／triage／follow-up 訓練題、teachers 為 MedGemma-27B-text 與 Qwen3.8-27B（reasoning off，選項字母 logits softmax）、兩者第一名相同才保留、保留 22,557 / 33,000 題、label 為共同答案且 soft target 為兩分布平均。兩個左側方塊各有一支箭頭指向中間橘色方塊「3 RadKev（decision model）」，內容為起點 Kev-27B（Qwen3.8-27B backbone）與 Kev-9B（Qwen3.5-9B-Base）、backbone 凍結加 rank-16 LoRA、record 等於 state 加多個 typed questions、state 每個 request 只編碼一次且每題只 attend state 與自己、pointer head 把 decision token 與 option tokens 投影到 256 維後以 scaled dot product 接 softmax / T、1 epoch 4,620 steps AdamW one-cycle、T = 1.35（dev set 擬合）。橘色方塊有兩支箭頭指向右側：右上紫色方塊「4 評估：15 tasks、14,142 題」列出 Report reading（IU/Open-i ×3、ReXErr）、Case（Eurorad ×2、RSNA-RadioQA、RadCases ×2）、Knowledge（MedMCQA ×2、MedQA、MedXpertQA、MMLU、PubMedQA），以及 primary outcome 為 task-averaged accuracy 的 RadKev-27B − Kev-27B、cluster bootstrap 95% CI 與 Holm 校正；右下灰色方塊「對照與外部測試」列出 Kev-27B／Kev-9B、Jev、OpenAI Decisions、Qwen3.8-27B 當 LLM（零樣本，reasoning off；1,675 題另開 reasoning），以及外部 RadGraph-XL 4,037 題](assets/radkev-decision-model-workflow.png)

圖：本書庫依論文 Methods、Table 1 與 Figures 1–2 圖說的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖。[(ref: main Methods, Table 1, Figures 1–2)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

## 背景／問題

放射科有不少決策其實是在固定答案中選一個：報告有沒有描述某個所見、哪個診斷成立、要排多急。作者的出發點是，用 LLM 做這類決策有三個不便：輸出是要再解析的文字、生成（尤其開 reasoning）很慢、能力最強的模型多半託管在機構外。其中「託管模型不適合病人資料」有引用文獻；「文字需要解析」與「延遲隨輸出長度增加」是作者的論述，沒有附引用，也不是本研究要檢驗的假設。[(ref: main Introduction)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

論文所說的 decision model，是一次前向傳遞就對每個允許答案給出機率的模型；作者提到的例子有託管的 Jev 與 OpenAI Decisions API，以及開放權重、建在 Qwen backbone 上的 Kev 系列（0.8B–27B）。作者指出當時沒有專為放射科調整過的 decision model，因此提出的假設是：專科化後的 decision model 至少與通用 decision model 及同尺寸 LLM 一樣準，而延遲低得多。[(ref: main Introduction)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

## 方法摘要

**輸入格式。** 一筆 record 是一段 state（報告、病例或題目文字）加上一個或多個 typed question（yes/no、選擇或順序題），每題附上允許的答案。所有問題放在同一個 request，state 只編碼一次。[(ref: main Methods)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**專科化。** 從 Kev-27B 與 Kev-9B 出發，用 36,109 筆公開放射訓練 record 微調，得到 RadKev-27B 與 RadKev-9B。訓練資料涵蓋結構化標籤抽取、報告錯誤偵測（ReXErr）、病例診斷與分類、影像檢查適當性、放射知識題，以及由兩個 LLM teacher 標註的醫囑、檢傷與追蹤題。[(ref: main Methods, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**評估。** 15 項任務、14,142 題，分三組：報告判讀、病例診斷與分類、放射知識。主要結果在讀取結果前就已指定：RadKev-27B 減 Kev-27B 的任務平均準確率（15 項任務不加權平均）。對照包括兩個起點模型、託管的 Jev 與 OpenAI Decisions，以及把 Qwen3.8-27B 當一般 LLM 使用。次要指標包含 ECE、Brier score、confident-error rate 與 coverage at 5% error（依信心由高到低作答，在已作答題的錯誤率不超過 5% 時能答多少比例）。[(ref: main Methods, Figure 7)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

## 方法詳解

**Pointer head 架構。** Backbone 權重凍結，每個 linear projection 加上 rank-16 LoRA。每題結尾的 decision token 與每個選項的結尾 token 各自投影到 256 維，選項分數是兩者的 scaled dot product，除以溫度 T 後做 softmax 得到答案機率。每題只 attend state 與自己，不看同一 record 的其他題。T 在 development set 上以最小化 negative log-likelihood 擬合，兩個尺寸都是 1.35。[(ref: main Methods, Figure 2)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**Two-teacher labeling。** 醫囑、檢傷與追蹤題沒有人工標籤。作者從 CheXpert Plus、ReXGradient-160K、CT-RATE 與 Eurorad 產生十類候選題，交給 MedGemma-27B-text 與 Qwen3.8-27B（皆關閉 reasoning）各自作答，答案分布取選項字母 logits 的 softmax。只有兩者第一名相同才保留，共同答案當 label，兩個分布的平均當 soft target；33,000 題保留 22,557 題（68.4%）。這批題目只用於訓練、不進測試。[(ref: main Methods, Figure 1)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**訓練設定。** 36,109 筆放射 record 與 1,000 筆原 Kev record 交錯訓練，其中 155 筆超過 context 長度被排除。每輪重新打亂選項順序；單一答案題會隨機加入「none of the above」或無關干擾選項。1 個 epoch（4,620 個 optimizer step），AdamW 搭配 one-cycle schedule，peak learning rate 27B 為 3×10⁻⁵、9B 為 2×10⁻⁵，effective batch 8，以 cross-entropy 對 hard 或 soft target 訓練。四張 RTX A6000 上，27B 訓練 13.1 小時、9B 訓練 3.4 小時。[(ref: main Methods)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**LLM 對照的設定。** Qwen3.8-27B 使用與 teacher 相同的零樣本 prompt，一題一個 prompt、關閉 reasoning，以選項字母的 next-token logits 做 softmax 計分；只評選項不超過 16 個的題目，因此 225 個選項的 RadCases topic 任務沒有 Qwen 的分數。Reasoning 版只在事後抽出的 1,675 題上測。所有 LLM 比較都只用兩個系統都有作答的題目。[(ref: main Methods)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**RadCases panel 的 prior correction。** 只在 RadCases panel 任務上，把 RadCases 訓練過的模型輸出除以訓練集各選項出現頻率（add-one smoothing）再重新正規化，不重新訓練。原因是訓練集中「no topic applies」是 34% panel 題的正確答案，修正前 RadKev-27B 有 70.7% 的 panel 題選它。[(ref: main Methods, §3.1)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**統計。** 所有比較皆為配對；95% CI 以 cluster bootstrap（2,000 次，在每個來源內以 record 為單位重抽，所有系統共用同一組重抽）計算；主要比較的 15 項任務以 Holm 校正雙尾 bootstrap p 值。沒有正式的樣本數估計，測試集即全部合格的保留 record。[(ref: main Methods)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

- **論文未交代** — 正文沒有列出完整的輸入模板、teacher prompt 原文與其餘超參數，這些在 Supplementary Notes S2–S3；逐任務的 Holm 校正結果在 Supplementary Table S2。
- **論文未交代** — 分析計畫附錄的撰寫日期與存放位置；正文只說它在讀取任何結果前寫成，並區分了附錄內與事後新增的分析。
- **論文未交代** — Table 1 的 orders／triage／follow-up 訓練數（11,443）是 record 數，two-teacher 保留量（22,557 題，其中 19,945 題在訓練切分）是題數，正文沒有直接說明兩者如何對應。
- **論文未交代** — 只跑了一次訓練、一個隨機種子，沒有種子間變異。

## 資料與實驗

下表摘錄論文 Table 1。Train 與 Dev 為訓練與開發用的 record 數，Test 為保留不訓練的題數；放射基準使用其中 14,142 題，表內另含 classifier 標註的抽取題、LLM 標註的醫囑與檢傷題，以及另外分析的外部測試集。[(ref: main Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

| 資料組 | Train | Dev | Test |
|---|---|---|---|
| Structured label extraction | 8,000 | 2,797 | 16,168 |
| Report error detection | 6,000 | 500 | 2,708 |
| Case diagnosis and classification | 2,912 | 329 | 610 |
| Imaging appropriateness | 264 | 29 | 227 |
| Radiology knowledge | 7,490 | 1,644 | 1,379 |
| Orders, triage and follow-up | 11,443 | 877 | 1,025 |
| External test | – | – | 4,037 |
| **Total** | **36,109** | **6,176** | **26,154** |

基準的 14,142 題中，11,434 題為人工標註，另 2,708 題 ReXErr 的錯誤由 LLM 植入、答案依構造已知。資料以病人或病例切分；IU/Open-i、MMLU、PubMedQA 與 MedXpertQA 只用於開發與測試，不進訓練。[(ref: main Methods)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

論文正文沒有逐任務的數值表（逐任務準確率在 Figure 4、Holm 校正結果在 Supplementary Table S2），下表整理正文報告的配對差異。差異為前者減後者，單位為百分點，括號為 95% CI。[(ref: main §3.1–§3.3)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

| 比較 | 範圍 | 差異（95% CI） |
|---|---|---|
| RadKev-27B − Kev-27B（主要結果） | 15 項任務平均 | +4.9（3.8 至 6.2） |
| RadKev-27B − Kev-27B | 14 項人工標註任務平均 | +3.6（2.4 至 5.0） |
| RadKev-27B − Kev-27B | 全部 14,142 題合併 | +5.8（5.3 至 6.3） |
| RadKev-27B − Kev-27B，不做 RadCases prior correction | 15 項任務平均 | +3.3（2.1 至 4.8） |
| RadKev-27B − Jev | 15 項任務平均 | +3.0（1.7 至 4.4） |
| RadKev-27B − OpenAI Decisions | 15 項任務平均 | +4.8（3.2 至 6.4） |
| RadKev-27B − Qwen3.8-27B（LLM，reasoning off） | 選項 ≤16 的 14 項任務平均 | +4.7（3.4 至 6.0） |
| RadKev-27B − Qwen3.8-27B（LLM，reasoning on） | 1,675 題樣本、9 項任務平均 | +2.8（1.0 至 4.6） |
| RadKev-9B − Kev-9B | 15 項任務平均 | +6.9（5.5 至 8.4） |
| Kev-27B − Kev-9B（規模） | 15 項任務平均 | +5.8（4.2 至 7.5） |
| RadKev-9B − Kev-27B | 15 項任務平均 | +1.1（−0.5 至 2.7） |

在七個系統都有作答的 13 項人工標註任務上，任務平均準確率依序為 RadKev-27B 81.1%、OpenAI Decisions 79.4%、Jev 79.1%、Qwen3.8-27B 78.1%、Kev-27B 77.3%、RadKev-9B 77.0%、Kev-9B 72.0%。[(ref: main §3.2)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

## 結果

- **主要比較** — 15 項任務平均準確率 RadKev-27B 80.8%、Kev-27B 75.9%，差 4.9 點（3.8–6.2）。逐任務差異從 IU 的「finding present」0.2 點到 ReXErr 報告錯誤偵測 22.6 點（20.9–24.3）；Holm 校正後 RadKev-27B 在四項任務較準（IU normal study、Eurorad diagnosis、MedMCQA 其他科別的放射題、ReXErr），沒有任務較差。[(ref: main §3.1)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- **增益集中在訓練過的來源** — 訓練切分有納入專科化資料的 8 項任務平均增加 7.4 點，只用於評估的 7 項任務平均增加 2.1 點。在訓練中見過的指令措辭上增加 2.9 點（2.3–3.6），沒見過的措辭只增加 0.7 點（0.1–1.2）。[(ref: main §3.1, §3.5)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- **與 LLM 及託管 decision model** — RadKev-27B 高於 Jev（+3.0）、OpenAI Decisions（+4.8）與關閉 reasoning 的 Qwen3.8-27B（+4.7）。在 1,675 題的事後樣本上，Qwen 開 reasoning 從 83.6% 升到 85.1%，RadKev-27B 為 89.0%。RadKev-9B 與 Kev-27B 的差距為 +1.1（−0.5 至 2.7），區間跨 0。[(ref: main §3.2, §3.3)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- **Eurorad 的 options-only 對照** — 把病例內容拿掉、只給選項時，RadKev-27B 在 Eurorad diagnosis 從 94.2% 降到 76.9%，Kev-27B 從 82.7% 降到 47.7%，Qwen 從 84.1% 降到 50.0%。專科化帶來的增益在沒有病例時是 29.2 點，有病例時是 11.6 點；作者解讀為模型多半學會從選項本身認出病例作者的最終診斷，而不是更會讀病例。[(ref: main §3.5)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- **外部報告** — 另一家機構以 CT 與 MRI 為主的 RadGraph-XL 報告共 4,037 題；在確定所見上，準確率為 RadKev-27B 90.2%、Kev-27B 91.3%、Qwen3.8-27B 90.3%，專科化讓 27B 模型改變 −1.1 點（−1.6 至 −0.6）。1,046 題 hedged findings 上，RadKev-27B 為 39.1%、Kev-27B 為 40.7%；這類題目占外部題目 25.9%，在訓練資料的狀態答案中只占 6.7%。[(ref: main §3.7)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- **校準與選擇性作答** — 在 11,434 題人工標註題上，RadKev-27B 於 5% 錯誤率下可作答 88.4%，比 Kev-27B 多 2.9 點（1.9–3.9）；全部 14,142 題則為 90.5% 對 76.4%。ECE 為 0.015 對 0.018，但信心 ≥0.9 卻答錯的比例為 1.4% 對 0.6%。[(ref: main §3.4, Figure 7)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)
- **延遲** — 一次一個 request 時，每題延遲中位數 RadKev-27B 128 ms、RadKev-9B 43 ms；Qwen3.8-27B 以字母 logits 計分 145 ms、生成字母 234 ms、開 reasoning 16.9 秒，約為 RadKev-27B 的 132 倍；OpenAI Decisions 與 Jev 分別為 175 ms 與 185 ms。[(ref: main §3.2, §3.8)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

## 限制

**作者自述的限制。** 只用公開資料，部分測試切分與訓練來自同一資料集合；ReXErr 的錯誤由 LLM 植入。外部測試只有 RadGraph-XL 一組，仍需要在院內報告與病人亞群上驗證。部分任務題數少（例如 RSNA-RadioQA 79 題），估計不精確；主要結果對各任務等權，合併平均則由 IU/Open-i 胸片報告主導。醫囑、檢傷與追蹤題由兩個 LLM 一致標註、只用於訓練，沒有對照人工判斷驗證。LLM 對照是零樣本、單一 prompt，沒有用同一批資料微調，所以 decision 格式與微調的效果混在一起。只有一次訓練、一個隨機種子。公開考題與 Eurorad 病例可能出現在預訓練資料中。延遲只測一次一個 request，且所有輸入都是純文字。主要比較以外的分析皆為探索性。[(ref: main Discussion, Limitations)](https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf)

**本書庫的觀察。**

- **Teacher 與 backbone 是同一個模型** — Qwen3.8-27B 同時是 Kev-27B 的 backbone、two-teacher 標註的 teacher 之一，也是 LLM 對照。兩位 teacher 一致才保留的訓練題，答案分布可能偏向這個 backbone 原本就會的判斷；論文沒有檢驗這一點。
- **基準增益與外部表現方向不一致** — 15 項任務平均的 +4.9 點，在外部 RadGraph-XL 的確定所見上變成 −1.1 點；hedged findings 上 RadKev-27B 與 Kev-27B 都只有約四成準確，作者也指出這是開放與託管 decision model 共同的主要錯誤來源。對要處理院內報告的使用情境，外部結果比基準平均更接近實際條件。
- **Eurorad 增益有一部分來自選項本身** — options-only 對照顯示，沒有病例時 RadKev-27B 仍有 76.9%，作者自己也建議答案空間要獨立於正確答案建構。這提醒讀者，選擇題格式的放射基準可能高估「讀懂病例」的能力。
- **校準指標不全然同向** — ECE 與 coverage 改善，但高信心錯誤比例從 0.6% 升到 1.4%；在以信心門檻自動放行的情境，後者更直接影響安全。

## 與書庫其他文章的關係

中文報告錯誤偵測研究用真實臨床報告比較 LLM 與人類讀者抓錯的能力，本篇的最大增益正好也在報告錯誤偵測，但用的是 LLM 植入錯誤的 ReXErr，兩篇並讀可以看出合成錯誤與真實錯誤的評估落差: [中文放射科報告的真實錯誤：八個 LLM 與八位人類讀者，誰抓得出來？](2026-09-22-llm-chinese-radiology-report-error-detection.md)

腦 MRI 報告隊列研究以三個 LLM 一致才自動貼標來換取零錯誤，本篇則用單一 decision model 的答案機率做 coverage at 5% error，兩篇都在處理「哪些報告可以自動判、哪些要退回人工」的取捨: [三個 LLM 都同意才自動貼標：6,718 份腦 MRI 報告分正常／異常，參考集零錯誤的代價是約一半報告退回人工](2026-10-15-llm-consensus-brain-mri-report-cohort.md)

ASA 分級那篇在麻醉術前資料上比較同一種「讀選項機率」的 readout、生成式提示與 LoRA，並發現少量在地標籤調門檻就能讓 κ 接近 LoRA，但換成 OpenJev 實作就不成立，可與本篇的延遲與外院結果對照，看 decision model 的優勢哪些可以跨任務延續: [不生成理由、只讀 A–D 選項的機率：Qwen3.5-9B 分 ASA 身體狀態，比生成式提示快約 64 倍，再用 1,000 個在地標籤調三個門檻，κ 只比 LoRA 低約 0.02，標籤再多 LoRA 仍會拉開](2026-10-28-asa-ps-llm-readout-vs-lora.md)

NIHSS 逐字稿那篇把本篇作為比較對象之一的託管 decision model Jev，拿去與 LLM 正面對照從床邊檢查對話逐項打分，Jev 延遲約為 LLM 的四十分之一、準確率較低，且錯誤集中在少數可命名的項目型態: [從床邊檢查逐字稿直接打 NIHSS：112 個合成中風案例上，LLM 項目準確率 99.0%、decision model Jev 94.4% 但快約 40 倍；病例、逐字稿與答案卷都由 LLM 產生，人工審查尚未完成](2026-10-29-nihss-transcript-decision-model-vs-llm.md)

## 實務的啟發

- **可借用的量測方法** — 評估選擇題形式的放射 AI 時，加一組 options-only 對照（拿掉病例、只給選項），並分開報告「訓練過的來源」與「只用於評估的來源」；本篇這兩項分析讓 4.9 點的平均增益能被拆開解讀。
- **可借用的設計** — 對答案可以列舉的放射文字決策，decision model 一次輸出所有選項的機率，能直接接上信心門檻與 coverage 評估，延遲也遠低於開 reasoning 的 LLM。這是論文在離線基準上的結果，作者明列的部署建議（Table 2）都沒有前瞻測試。
- **待驗證的警訊** — 27B 版的專科化在外院報告上沒有帶來增益，RadKev-27B 在 hedged findings 的準確率約四成，且高信心錯誤比例上升；導入院內報告前，需要用當地標註資料、當地的答案頻率重新擬合溫度與門檻，並監看預測答案的分布。
- **證據強度** — 單一研究團隊、只用公開資料、單次訓練的預印本；它支持「在這組公開放射基準上，專科化 decision model 比同尺寸通用模型準、也比 LLM 快」，不足以支持在臨床流程中取代人工判讀或直接部署。

## References

- **main** — Ram U, Zhang R. *RadKev: An Open-Weight Decision Model for Radiology*. medRxiv, 2026. DOI: 10.64898/2026.10.07.26364991. PDF：<https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full.pdf>。文內引用位置：author block、Abstract、Introduction、Methods、Statistics、§3.1–§3.8、Discussion、Limitations、Data availability、Table 1、Figures 1、2、7。
- **abstract page** — medRxiv 頁面：<https://www.medrxiv.org/content/10.64898/2026.10.07.26364991v1.full>。
- **doi** — <https://doi.org/10.64898/2026.10.07.26364991>。
- **code** — 作者公開的程式碼：<https://github.com/udiram/RadKev>。

[Home](../) · [AI Papers](./)
