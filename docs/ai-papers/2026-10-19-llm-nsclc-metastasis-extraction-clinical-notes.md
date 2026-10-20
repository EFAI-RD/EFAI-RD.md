---
catalog_id: "doi:10.2196/99573"
editors:
  - "Clare"
refs:
  main:
    title: "Metastasis Extraction From Non–Small Cell Lung Cancer Clinical Notes Using Large Language Model–Based Classification: Retrospective Comparative Study"
    url: "https://cancer.jmir.org/2026/1/e99573"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 癌症登記缺了 54% 的轉移欄位，病歷補得回來嗎？NSCLC 病歷上，零樣本 MedGemma、Llama 3.1 與微調 GatorTron 的比較

## 來源

- 團隊：Emory University 的 Department of Biomedical Informatics（Emory School of Medicine）、Rollins School of Public Health 流行病學系、Winship Cancer Institute 資訊部門與血液腫瘤科，共 8 位作者；第一作者 Sweta Balaji，通訊作者 Selen Bozkurt。[(ref: main author block)](https://cancer.jmir.org/2026/1/e99573)
- 論文：*Metastasis Extraction From Non–Small Cell Lung Cancer Clinical Notes Using Large Language Model–Based Classification: Retrospective Comparative Study*，JMIR Cancer 2026;12:e99573，2026-10-16 正式刊出（預印本 2026-04-27 首次公開），授權 CC BY。[(ref: main)](https://cancer.jmir.org/2026/1/e99573)
- 識別碼：DOI [10.2196/99573](https://doi.org/10.2196/99573)。
- 全文：[JMIR Cancer 全文頁](https://cancer.jmir.org/2026/1/e99573)。
- 資料與程式：病歷資料受 HIPAA 與院內規範限制，不公開。[(ref: main Data Availability)](https://cancer.jmir.org/2026/1/e99573)
- 研究性質：單一機構回顧性比較研究，不是 pilot；三種方法都有實作，在保留的測試病人上評估，附 10,000 次 bootstrap 95% CI，沒有做模型間的顯著性檢定。參考標準在 cohort 1 是癌症登記、在 cohort 2 是人工標註，兩者不同。[(ref: main Methods)](https://cancer.jmir.org/2026/1/e99573)
- 證據邊界：本文數值以出版社全文頁的正文與 Table 1–7 為準；提示詞全文與關鍵字清單在論文的 Multimedia Appendix 1，本文未納入引述。

**編輯：** Clare

作者在 Emory 的非小細胞肺癌（NSCLC）病歷上比較三種從臨床筆記判斷「是否轉移」與「是否腦／中樞神經系統（CNS）轉移」的方法：微調的 GatorTron-base，與零樣本的 MedGemma-27B-text-it、Llama 3.1-70B-Instruct；在以癌症登記為參考的 116／115 位測試病人上，整體轉移 F1 為 0.72、0.80 與 0.76，CNS 轉移 F1 為 0.50、0.76 與 0.79，但信賴區間大幅重疊，作者明說不能據此排名。[(ref: main Abstract, Table 5, Table 6)](https://cancer.jmir.org/2026/1/e99573#table5)

## 流程

![NSCLC 病歷轉移擷取的研究設計示意圖。由左到右四欄：藍色方塊「1. Input notes」列出 cohort 1（Winship registry 2023-2025、579 位病人分析整體轉移、576 位分析 brain/CNS、24,887 份筆記、69 種筆記類型、診斷日前後 30 天）與 cohort 2（22 位病人、2 個試驗、2010-2021、644 份放射報告）；實線箭頭指向綠色方塊「2. Preprocessing」（CLEVER 字典加自訂腫瘤學詞彙的關鍵字過濾，保留含關鍵字的句子，沒有命中的筆記保留全文，cohort 1 每位病人的筆記串成一份文件）；綠色方塊以三條實線箭頭分別指向三個橘色方塊：3a GatorTron-base（345M，cohort 1 以 80/20 分割微調，512-token chunk、stride 128，病人層級取 chunk 最大機率）、3b MedGemma-27B-text-it（零樣本、greedy decoding、輸出 Metastasis: YES／NO、不微調）、3c Llama 3.1-70B-Instruct（零樣本、greedy decoding、與 MedGemma 相同的 prompt 結構與輸出格式）；三個橘色方塊各以箭頭指向右上灰色方塊「4. Evaluation」（整體轉移與 brain/CNS 轉移兩項任務；cohort 1 測試 116／115 位病人、以癌症登記為參考；cohort 2 病人層級與筆記層級、以兩位摘錄員加腫瘤科醫師裁決為參考；accuracy、precision、recall、F1，10,000 次 bootstrap 95% CI）。右下另一個灰色方塊「5. Additional analyses」沒有箭頭連入，列出探索性的 missingness recovery（675 位登記欄位缺漏或未知的病人，人工檢查 20 例）與只用 MedGemma 的部位別分析（骨、肝、遠處淋巴結）](assets/nsclc-metastasis-llm-extraction-workflow.png)

圖：本書庫依論文 Methods 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文 Figure 2 為前處理與推論流程圖）。[(ref: main Methods, Figure 2)](https://cancer.jmir.org/2026/1/e99573#figure2)

## 背景／問題

轉移狀態是肺癌研究分層、隊列建立與臨床試驗篩選常用的變項，結構化來源通常是癌症登記。本研究自己的資料顯示這個來源並不完整：cohort 1 一開始找到的 1,260 位 NSCLC 病人中，有 675 位（約 54%）的登記轉移欄位缺漏或標為未知。[(ref: main Results, Table 2)](https://cancer.jmir.org/2026/1/e99573#table2)

作者因此問兩件事：一是從診斷前後的臨床筆記能不能可靠判斷整體轉移與 CNS 轉移；二是需要標註資料微調的 encoder（GatorTron），和不微調、直接零樣本使用的指令模型（MedGemma、Llama 3.1）相比如何。「病歷可以補登記的缺口」是作者的動機，論文只用 20 例人工檢查的探索性分析初步支持，沒有在 675 位缺漏病人上系統驗證。[(ref: main Introduction, Results)](https://cancer.jmir.org/2026/1/e99573)

## 方法摘要

**任務。** 兩個病人層級的二元分類：是否有任何部位的轉移（overall metastasis），以及是否有 brain/CNS 轉移。另外只用 MedGemma 做骨、肝、遠處淋巴結三個部位的分類。[(ref: main Methods)](https://cancer.jmir.org/2026/1/e99573)

**三種方法。**

- **GatorTron-base（345M encoder）** — 在 cohort 1 的訓練集上微調，輸入切成 512-token chunk，搭配由 CLEVER 衍生的轉移詞、NegEx 否定與不確定性表述特徵，接前饋分類頭；病人層級取各 chunk 的最大機率，門檻在驗證集上選定（整體 0.58、CNS 0.40），原封不動用到 cohort 2。[(ref: main Methods, Model Development and Inference)](https://cancer.jmir.org/2026/1/e99573)
- **MedGemma-27B-text-it** — 零樣本，greedy decoding（do_sample=False），限制只輸出 "Metastasis: YES" 或 "Metastasis: NO"。[(ref: main Methods)](https://cancer.jmir.org/2026/1/e99573)
- **Llama 3.1-70B-Instruct** — 零樣本，與 MedGemma 相同的 prompt 結構、解碼方式與輸出格式。[(ref: main Methods)](https://cancer.jmir.org/2026/1/e99573)

三種方法都只用開放權重模型，在院內符合 HIPAA 的環境本地執行。作者強調三者代表不同策略（監督式微調對照零樣本），不是同條件下的架構比較。[(ref: main Methods, Discussion)](https://cancer.jmir.org/2026/1/e99573)

**指標。** Accuracy、precision、recall 與 F1，依模型、cohort 與預測層級（病人／筆記）分別報告，95% CI 以 10,000 次 bootstrap 計算。[(ref: main Methods, Data Partitioning and Model Evaluation)](https://cancer.jmir.org/2026/1/e99573)

## 方法詳解

**Cohort 1 的建立。** 來源是連結喬治亞州癌症登記的 Winship Cancer Registry，2023–2025 年。1,260 位病人中排除 663 位至少缺一個登記轉移欄位者、12 位標為未知且沒有確認陽性部位者、6 位沒有癌症相關筆記內容者，剩 579 位用於整體轉移；再排除 3 位腦轉移紀錄未確認者，剩 576 位用於 CNS 轉移。筆記限定在正式診斷日前 30 天到後 30 天。[(ref: main Methods, Data Sources and Cohorts; Figure 1)](https://cancer.jmir.org/2026/1/e99573#figure1)

**資料分割。** 整體轉移任務以 80/20 分成訓練與測試，訓練部分再分出驗證集：370／93／116 位病人；CNS 任務為 369／92／115 位。三種方法用同一個測試集。[(ref: main Methods, Data Partitioning and Model Evaluation)](https://cancer.jmir.org/2026/1/e99573)

**前處理。** 以公開的 CLEVER（Clinical Event Recognizer）字典加研究團隊自訂的腫瘤學詞彙做關鍵字過濾，只保留含關鍵字的句子；沒有任何命中的筆記保留全文。Cohort 1 每位病人的筆記串接成一份文件後輸入模型。[(ref: main Methods, Clinical Note Preprocessing)](https://cancer.jmir.org/2026/1/e99573)

**Cohort 2 與人工標註。** 來自兩個已完成的隨機試驗（2010–2021），22 位病人、644 份放射報告，不設時間窗，三種方法不重新訓練直接套用。兩位受訓摘錄員在腫瘤科醫師督導下獨立標註，分四輪（10、100、200、334 份筆記），不一致時討論或由腫瘤科醫師裁決；作者報告最終 Cohen κ 整體 0.93、CNS 0.88。[(ref: main Methods, Manual Annotation of Cohort 2; Table 3)](https://cancer.jmir.org/2026/1/e99573#table3)

**錯誤分析與探索性分析。** 作者把錯誤分成四類：預測錯誤、文字模稜兩可、預測正確但登記標籤錯、臨床文字缺漏（Table 4）。Missingness recovery 分析把模型套到 675 位登記欄位缺漏的病人，人工檢查其中 20 例（10 例預測陽性、10 例預測陰性），檢查者先標註、再看模型預測。[(ref: main Methods, Error Analysis; Table 4)](https://cancer.jmir.org/2026/1/e99573#table4)

**部署與成本。** Python 3.10，2 張 NVIDIA RTX 6000 Ada；GatorTron 訓練約 32 分鐘，每個模型每個測試集推論約 4.5 分鐘（約每份筆記 2.3 秒）。[(ref: main Methods)](https://cancer.jmir.org/2026/1/e99573)

- **論文未交代** — GatorTron 微調的 learning rate、epoch 數與 batch size；零樣本模型「固定最大輸出長度」的實際數值。
- **論文未交代** — MedGemma 與 Llama 3.1 讀的是整位病人串接後的文件，論文沒有說明文件超過模型 context 長度時如何處理，也沒有說明零樣本模型的病人層級判定是否有其他彙總規則。
- **論文未交代** — precision、recall、F1 以哪一類為正類（通常是「有轉移」，但正文未明寫）；三種方法之間沒有正式的統計檢定。
- **論文未交代** — 沒有規則式或傳統機器學習的對照組；唯一的額外基線是未微調的 GatorTron（F1 0.46）。

## 資料與實驗

下表摘錄論文 Table 2 的兩個 cohort。[(ref: main Table 2)](https://cancer.jmir.org/2026/1/e99573#table2)

| 特徵 | Cohort 1 | Cohort 2 |
|---|---|---|
| 參考標準 | 癌症登記 | 人工標註 |
| 紀錄期間 | 2023–2025 | 2010–2021 |
| 找到的 NSCLC 病人 | 1,260 | 22 |
| 登記轉移欄位缺漏／未知，n (%) | 675 (54) | 0 (0) |
| 分析病人數（整體轉移） | 579 | 22 |
| 分析病人數（brain/CNS） | 576 | 22 |
| 臨床筆記數 | 24,887 | 644 |
| 筆記類型 | 69 種 | 只有放射報告 |
| 整體轉移陽性，n (%) | 239 (41) | 22 (100) |
| Brain/CNS 轉移陽性，n (%) | 89 (15) | 8 (36) |

下表摘錄論文 Table 5 的整體轉移結果，括號內為 95% CI。[(ref: main Table 5)](https://cancer.jmir.org/2026/1/e99573#table5)

| 模型 | 資料（層級，n） | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|---|
| GatorTron（微調） | Cohort 1（病人，116） | 0.74 (0.66–0.83) | 0.71 (0.65–0.81) | 0.74 (0.65–0.84) | 0.72 (0.63–0.80) |
| GatorTron（微調） | Cohort 2（病人，22） | 0.95 (0.86–1.0) | 1.0 (1.0–1.0) | 0.95 (0.86–1.0) | 0.98 (0.93–1.0) |
| GatorTron（微調） | Cohort 2（筆記，644） | 0.71 (0.67–0.74) | 0.65 (0.61–0.70) | 0.91 (0.88–0.94) | 0.76 (0.73–0.79) |
| Llama 3.1-70B | Cohort 1（病人，116） | 0.76 (0.68–0.84) | 0.69 (0.58–0.80) | 0.85 (0.74–0.94) | 0.76 (0.67–0.84) |
| Llama 3.1-70B | Cohort 2（病人，22） | 1.0 (1.0–1.0) | 1.0 (1.0–1.0) | 1.0 (1.0–1.0) | 1.0 (1.0–1.0) |
| Llama 3.1-70B | Cohort 2（筆記，644） | 0.87 (0.85–0.90) | 0.84 (0.80–0.88) | 0.92 (0.89–0.95) | 0.88 (0.85–0.91) |
| MedGemma-27B | Cohort 1（病人，116） | 0.80 (0.72–0.87) | 0.75 (0.64–0.86) | 0.85 (0.76–0.94) | 0.80 (0.72–0.87) |
| MedGemma-27B | Cohort 2（病人，22） | 1.0 (1.0–1.0) | 1.0 (1.0–1.0) | 1.0 (1.0–1.0) | 1.0 (1.0–1.0) |
| MedGemma-27B | Cohort 2（筆記，644） | 0.93 (0.91–0.95) | 0.97 (0.95–0.99) | 0.88 (0.85–0.92) | 0.93 (0.90–0.95) |

下表摘錄論文 Table 6 的 brain/CNS 轉移結果，括號內為 95% CI。[(ref: main Table 6)](https://cancer.jmir.org/2026/1/e99573#table6)

| 模型 | 資料（層級，n） | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|---|
| GatorTron（微調） | Cohort 1（病人，115） | 0.88 (0.80–0.96) | 0.50 (0.38–0.64) | 0.50 (0.26–0.71) | 0.50 (0.34–0.66) |
| GatorTron（微調） | Cohort 2（病人，22） | 0.73 (0.55–0.91) | 0.57 (0.30–0.82) | 1.0 (1.0–1.0) | 0.72 (0.46–0.90) |
| GatorTron（微調） | Cohort 2（筆記，644） | 0.81 (0.78–0.84) | 0.35 (0.28–0.42) | 0.83 (0.75–0.92) | 0.50 (0.42–0.67) |
| Llama 3.1-70B | Cohort 1（病人，115） | 0.96 (0.91–0.99) | 0.91 (0.69–1.0) | 0.71 (0.46–0.94) | 0.79 (0.59–0.96) |
| Llama 3.1-70B | Cohort 2（病人，22） | 0.95 (0.86–1.0) | 0.88 (0.62–1.0) | 1.0 (1.0–1.0) | 0.93 (0.77–1.0) |
| Llama 3.1-70B | Cohort 2（筆記，644） | 0.96 (0.95–0.98) | 0.82 (0.73–0.90) | 0.90 (0.82–0.97) | 0.86 (0.79–0.91) |
| MedGemma-27B | Cohort 1（病人，115） | 0.95 (0.90–0.98) | 0.83 (0.58–1.0) | 0.72 (0.45–0.94) | 0.76 (0.54–0.92) |
| MedGemma-27B | Cohort 2（病人，22） | 0.82 (0.74–0.95) | 0.83 (0.43–1.0) | 0.63 (0.25–1.0) | 0.70 (0.33–0.93) |
| MedGemma-27B | Cohort 2（筆記，644） | 0.97 (0.95–0.98) | 0.83 (0.75–0.92) | 0.89 (0.81–0.96) | 0.86 (0.79–0.91) |

下表摘錄論文 Table 7 的部位別結果（只有 MedGemma，n=116），括號內為 95% CI。[(ref: main Table 7)](https://cancer.jmir.org/2026/1/e99573#table7)

| 部位 | 盛行率 | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|---|
| 骨 | 0.16 | 0.93 (0.88–0.97) | 0.79 (0.58–0.95) | 0.79 (0.59–0.95) | 0.79 (0.62–0.91) |
| 肝 | 0.12 | 0.96 (0.91–0.99) | 0.80 (0.57–1.0) | 0.86 (0.64–1.0) | 0.82 (0.64–0.96) |
| 遠處淋巴結 | 0.02 | 0.92 (0.87–0.96) | 0.18 (0.00–0.45) | 1.0 (0.00–1.0) | 0.31 (0.00–0.62) |

## 結果

- **整體轉移，cohort 1** — MedGemma F1 0.80、Llama 3.1 0.76、微調 GatorTron 0.72；論文另報告未微調的 GatorTron 基準 F1 為 0.46。三者的 95% CI 互相重疊，作者明說這些差異不應解讀為某種方法較好。[(ref: main Results, Table 5)](https://cancer.jmir.org/2026/1/e99573#table5)
- **CNS 轉移，cohort 1** — Llama 3.1 F1 0.79、MedGemma 0.76、GatorTron 0.50；三者 accuracy 都在 0.88 以上，但 CNS 轉移盛行率只有 15%，F1 與 recall 的區間很寬（例如 Llama 3.1 recall 0.71，CI 0.46–0.94）。[(ref: main Results, Table 6)](https://cancer.jmir.org/2026/1/e99573#table6)
- **Cohort 2 的時間外驗證** — 筆記層級的整體轉移 F1：MedGemma 0.93、Llama 3.1 0.88、GatorTron 0.76；CNS 轉移筆記層級 F1：MedGemma 與 Llama 3.1 皆 0.86、GatorTron 0.50。GatorTron 在 cohort 2 的 CNS 筆記層級 precision 只有 0.35（recall 0.83）。[(ref: main Table 5, Table 6)](https://cancer.jmir.org/2026/1/e99573#table6)
- **錯誤的來源不全在模型** — 整體轉移任務中，MedGemma 的 23 個錯誤有 9 個被歸為「預測正確但登記標籤錯」、6 個為臨床文字缺漏、6 個為文字模稜兩可，只有 2 個是預測錯誤；GatorTron 的 30 個錯誤中有 13 個是預測錯誤。CNS 任務中 Llama 3.1 的 5 個錯誤有 4 個是臨床文字缺漏。[(ref: main Results, Error Analysis; Table 4)](https://cancer.jmir.org/2026/1/e99573#table4)
- **部位別** — MedGemma 的肝轉移 F1 0.82、骨轉移 0.79；遠處淋巴結盛行率只有 0.02，F1 0.31，CI 下界為 0。[(ref: main Table 7)](https://cancer.jmir.org/2026/1/e99573#table7)
- **補回缺漏的登記欄位（探索性）** — 在 675 位缺漏病人中人工檢查的 20 例上，accuracy 0.90、F1 0.89。[(ref: main Abstract, Results)](https://cancer.jmir.org/2026/1/e99573)

## 限制

**作者自述的限制。** 癌症登記標籤本身不完美，也無法反映之後的病情進展，模型與登記不一致時可能是登記錯；cohort 2 只有 22 位病人、來自試驗、只有放射報告，而且整體轉移全數陽性，所以病人層級指標看不出區辨力，筆記層級估計也可能因重複用語而偏樂觀；兩個 cohort 的參考標準不同；微調與零樣本方法的評估方式不同；GatorTron 的 512-token 視窗有限；關鍵字前處理可能丟掉隱含脈絡；單一機構，需要更廣的外部驗證；missingness recovery 分析樣本小且屬探索性；遠處淋巴結的估計不穩定。[(ref: main Discussion)](https://cancer.jmir.org/2026/1/e99573)

**本書庫的觀察。**

- **Cohort 2 病人層級的 1.0 不代表完美** — 整體轉移在 cohort 2 是 22 位全數陽性，沒有陰性病人，precision 只要有預測陽性就是 1.0，accuracy 等於 recall；這組數字只說明「沒有漏掉」，不能說明「不會誤判」。
- **參考標準會壓低零樣本模型的分數** — MedGemma 的整體轉移錯誤中有 9/23 被歸為登記標籤錯；若這些判斷成立，以登記為參考的 cohort 1 數值低估了它的實際表現。反過來說，這個歸類是研究團隊的事後判讀，不是獨立盲評，只能當成方向性的訊號。
- **「零樣本」仍依賴人工設計的前處理** — 三種方法都吃同一套 CLEVER 加自訂腫瘤詞的關鍵字過濾，零樣本模型省掉的是標註訓練資料，不是領域知識；換到另一家醫院的筆記格式，過濾規則本身也需要重新檢查。
- **文中有幾處數字前後不一** — Cohort 1 筆記數在摘要與 Table 2 為 24,887、Results 一處為 24,898；CNS 標註 κ 正文寫 0.88、Table 3 第四輪為 0.91；遠處淋巴結 F1 正文寫 0.29、Table 7 為 0.31，盛行率正文寫 1.7%、Table 7 為 0.02。本文表格一律採用論文表格的數值。
- **補缺漏的證據只有 20 例** — 其餘 655 位缺漏病人的實際補回品質沒有被估計；「病歷可以補登記」目前只是可行性訊號。

## 與書庫其他文章的關係

腦 MRI 報告那篇用三個 LLM 是否一致決定自動貼標或退回人工，本篇則比較單一模型從病歷判斷轉移的準確度，兩篇處理的都是用 LLM 從自由文字建立研究隊列時的標籤可靠度: [三個 LLM 都同意才自動貼標：6,718 份腦 MRI 報告分正常／異常，參考集零錯誤的代價是約一半報告退回人工](2026-10-15-llm-consensus-brain-mri-report-cohort.md)

老年照護構念基準在四家院所比較規則引擎、GPT-4o 與微調小模型的病歷抽取，本篇則在單一機構的腫瘤病歷上比較微調 encoder 與兩個零樣本開放權重模型，兩篇都顯示參考標準與資料來源會左右「哪種方法較好」的結論: [規則引擎、GPT-4o 與微調小模型，誰讀得懂病歷裡的老年照護？四家院所、41 個構念的基準](2026-09-24-llm-geriatric-ehr-multisite-benchmark.md)

假釋／緩刑偵測那篇完全不用真實病歷標註、只用 LLM 合成資料訓練或提供範例，本篇則比較零樣本模型與以真實病歷標註微調的 GatorTron，兩篇對照可以看出「省掉標註」的兩種做法在真實病歷上各自付出的代價: [一筆真實標註都不用：GPT-4o-mini 生成的 7,579 句訓練資料，換到 293 份 VA 病歷偵測假釋／緩刑，Llama 守在 81–87% macro-F1，encoder 跌到 30%](2026-10-20-llm-synthetic-data-parole-probation-detection.md)

時間關係抽取那篇在 i2b2 出院摘要上把 GatorTron 與 LLaMA3.1-8B、MeLLaMA-13B 放進同一組微調與 PEFT 策略比較，本篇則在真實腫瘤病歷上比較微調 GatorTron-base 與零樣本 LLM，兩篇合起來看可以區分「模型選擇」與「調適方式」各自對病歷抽取表現的影響: [病歷時間關係抽取該怎麼調模型？i2b2 2012 上只調 query／value 的 QLoRA 讓 LLaMA3.1-8B 達 89.15% micro-F1，但每類只給一例時沒有一種做法超過 60%](2026-10-20-llm-clinical-temporal-relation-extraction-adaptation.md)

## 實務的啟發

- **可借用的設計** — 用病歷判斷轉移這類已有結構化欄位的變項時，把錯誤拆成「模型錯」「文字模稜兩可」「病歷沒寫」「參考標準錯」四類來報告，比只報 F1 更能看出瓶頸在模型還是在資料；本篇的零樣本模型錯誤大多不屬於第一類。
- **可借用的量測方法** — 同時報告病人層級與筆記層級、並把在開發集選定的門檻原封不動搬到另一組資料上，能看出微調模型的門檻是否可攜；本篇 GatorTron 在 cohort 2 的 CNS 筆記層級 precision 只有 0.35（cohort 1 病人層級為 0.50），兩者層級不同、不能直接相減，但這種落差只有在門檻跨資料搬移時才看得到，值得在自己的資料上複驗。
- **待驗證的警訊** — 外部驗證的 cohort 2 只有 22 位病人且整體轉移全數陽性，病人層級的 1.0 不能當成外部效度的證據；要評估是否能在另一家院所部署，需要含陰性病人、病人數足夠的外部資料。
- **證據強度** — 單一機構、回顧性、以不完整的登記為主要參考標準，模型之間沒有統計檢定且區間大幅重疊；它支持「零樣本開放權重模型在這組 NSCLC 病歷上可達到與微調 encoder 相近或更高的轉移判斷表現，且不需要標註訓練資料」，不足以支持直接用來取代登記摘錄員或補齊登記資料。

## References

- **main** — Balaji S, Campbell K, Smith D, et al. *Metastasis Extraction From Non–Small Cell Lung Cancer Clinical Notes Using Large Language Model–Based Classification: Retrospective Comparative Study*. JMIR Cancer. 2026;12:e99573. DOI: 10.2196/99573. 全文：<https://cancer.jmir.org/2026/1/e99573>。文內引用位置：author block、Abstract、Introduction、Methods（Data Sources and Cohorts、Clinical Note Preprocessing、Manual Annotation of Cohort 2、Model Development and Inference、Data Partitioning and Model Evaluation、Error Analysis）、Results、Discussion、Data Availability；深鏈 [Figure 1](https://cancer.jmir.org/2026/1/e99573#figure1)、[Figure 2](https://cancer.jmir.org/2026/1/e99573#figure2)、[Table 2](https://cancer.jmir.org/2026/1/e99573#table2)、[Table 3](https://cancer.jmir.org/2026/1/e99573#table3)、[Table 4](https://cancer.jmir.org/2026/1/e99573#table4)、[Table 5](https://cancer.jmir.org/2026/1/e99573#table5)、[Table 6](https://cancer.jmir.org/2026/1/e99573#table6)、[Table 7](https://cancer.jmir.org/2026/1/e99573#table7)。
- **doi** — <https://doi.org/10.2196/99573>。

[Home](../) · [AI Papers](./)
