---
catalog_id: "doi:10.64898/2026.10.16.26361411"
editors:
  - "Clare"
refs:
  main:
    title: "Clinical pathogen adjudication in metagenomic sequencing using a large language model"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf"
  abs:
    title: "medRxiv abstract page: 10.64898/2026.10.16.26361411v1"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# mNGS 報告上幾百個微生物，哪個才是致病菌？微調 Qwen3-8B 重現臨床判讀：保留集召回 92.44%、2025 年新一批 84.49%，但比樹模型多抓到的每個致病菌，要多付約 3 個假陽性

## 來源

- 團隊：上海交通大學醫學院附屬仁濟醫院檢驗科、華大研究院（BGI Research，北京／深圳）、上海交通大學醫學院與華大基因上海臨床檢驗中心，共 11 位作者；通訊作者為 Muyun Wei、Ziqing Deng、Min Li。[(ref: main p.1)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=1)
- 論文：*Clinical pathogen adjudication in metagenomic sequencing using a large language model*，medRxiv v1 預印本，2026-10-21 張貼，未經同儕審查；授權 CC BY-NC-ND 4.0。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1)
- 識別碼：DOI [10.64898/2026.10.16.26361411](https://doi.org/10.64898/2026.10.16.26361411)；未見期刊版本。
- 全文：[medRxiv PDF v1](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf)。
- 程式與資料：benchmark 與各圖原始資料預定在正式發表時以受控方式釋出（向通訊作者申請、簽資料使用協議、限非商業用途），程式碼同樣預定發表時公開。[(ref: main p.26)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=26)
- 研究性質：完整執行的單一中心回顧性研究，不是 pilot；模型實際在兩個時間點不同的測試群上執行，並與多個傳統基線比較。參考標準是治療團隊在病歷中記下的致病菌判斷，作者明言這不是微生物學上的真值；模型沒有在臨床流程中前瞻使用。[(ref: main p.3, p.14)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=3)
- 證據邊界：本文數值以 v1 PDF 正文與 Methods 明列的數字為準，頁碼依 PDF 頁序；只出現在 Figure 1e、Supplementary Figures 的個別基線數值，以及 prompt 模板全文，未納入本文引述。

**編輯：** Clare

作者把一家醫院 4,855 份 metagenomic next-generation sequencing（mNGS）報告上的每個偵測到的微生物，對上治療團隊事後在病歷記下的「致病菌」判斷，用這些標籤以 LoRA 微調 Qwen3-8B 逐列判讀：在保留集召回 92.44% 的參考判斷、每份檢體 2.00 個假陽性，換到 2025 年第一季的新一批檢體召回 84.49%；它的 average precision 高於梯度提升樹基線，但多抓到的每個致病菌要多付約 3.1 個假陽性。[(ref: main p.3)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=3)

## 流程

![研究設計示意圖。最上方標題為 Study design: LLM adjudication of culprit pathogens in clinical mNGS reports。上排由左到右四個圓角方塊，以三支深灰色實線箭頭相連：藍色方塊「1 Candidate panel」寫 One specimen = one mNGS report、Every detected organism = one row、4,855 specimens, 19 sampling sites、1,333,867 candidate rows；紫色方塊「2 Row prompt blocks」寫 9 quantitative indices (reads, rank, coverage, abundance ...)、Sampling site、Coloniser flag + organism description、Organism identity、Clinical context；綠色方塊「3 Fine-tuned LLM」寫 Qwen3-8B + LoRA (rank 8)、Trained on 2,479 specimens、Focal loss, hard-negative mixing、Argmax: 'harmful' vs 'harmless' logit per row；橘色方塊「4 Output」寫 Rows called causative per specimen、Label: treating team's recorded culprit call。下排三個方塊：灰底實線框「Test cohorts」寫 Held-out (2024 or earlier): 1,214 specimens、Later cohort (2025 Q1): 1,162 specimens 與 Metrics: row-level recall, false positives per specimen, case-level complete recall, AP；白底灰色虛線框「Additional references」寫 Blinded re-adjudication by a second hospital team: 215 specimens 與 Culture / smear / nucleic-acid confirmation: 231 organism-specimen pairs；青色方塊「Comparators」寫 Null models, single-index thresholds、Historical culprit-rate priors、Logistic regression、Gradient-boosted trees、Prompt-block masking ablation。三支深灰色實線箭頭由橘色方塊向下分別指向下排三個方塊。右下角斜體說明為 Schematic redrawn from the paper's Methods; design counts only, no result values.](assets/mngs-llm-pathogen-adjudication-design.png)

圖：本書庫依論文 Methods 文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的研究流程圖為 Figure 1）。上排四個方塊以實線箭頭表示從檢體的候選微生物清單、逐列 prompt 區塊、微調模型到逐列判讀輸出的順序；下排三個方塊是評估所用的兩個測試群、兩種額外參考標準（以虛線框與主要參考標準區隔）與比較對象。[(ref: main p.3, p.15–20, p.25)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=15)

## 背景／問題

一份臨床 mNGS 報告常列出很多微生物，其中多數是背景或定植菌，作者引用文獻說明這一點，並把「判斷哪個才是造成感染的致病菌（culprit）」視為解讀的關鍵步驟：漏判與過判都會影響處置。[(ref: main p.2)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=2) 既有做法包括報告門檻、人工整理的註記與讀序層級的計算方法，作者也引用了兩篇以 AI 輔助 mNGS 判讀的預印本。[(ref: main p.2)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=2)

作者主張，限制 AI 輔助判讀的不是資料量或算力，而是缺少把整份偵測清單連到臨床判斷的大型標註世代；這個主張在論文中沒有引用證據，應讀作作者的研究動機。[(ref: main p.2)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=2) 本篇實際回答的是較窄的問題：只用報告上已有的欄位，一個微調過的 LLM 能多大程度重現同一家醫院治療團隊記下的致病菌判斷，以及哪些證據在影響這個判斷。

## 方法摘要

**任務與標籤。** 每份檢體的 mNGS 報告展開成「候選列」，一列是一個偵測到的微生物；標籤是治療團隊是否在病歷中把該微生物記為這份檢體的致病菌。作者把病歷中的致病菌字串正規化後對回偵測列，並在較早世代做反向驗證：標籤推導的 precision 0.9731、recall 0.8594，也就是有一部分真正被記下的致病菌沒對上標籤。[(ref: main p.16–17)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=16)

**資料切分。** 2024 年（含）以前的 3,693 份檢體依檢體切成開發集 2,479 份與保留集 1,214 份；另有 2025 年第一季的 1,162 份檢體作為時間上較晚的測試群。兩個世代用同一個參考資料庫，但 2025 年第一季在建庫方式與標籤建構上不同。[(ref: main p.3, p.15)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=15)

**模型。** Qwen3-8B 以 LoRA 在開發集上監督式微調，每一列輸入包含五個 prompt 區塊：九個定量指標、採樣部位、知識庫註記（是否為常見定植菌與菌種說明）、菌種身分與臨床背景；輸出比較「harmful」與「harmless」兩個答案 token 的 logit，大者為判讀結果。[(ref: main p.19, p.25)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=19)

**評估。** 主要看列層級的致病菌召回、每份檢體的假陽性列數、檢體層級是否找回全部致病菌，以及 average precision（AP）；比較對象包括 null model、單一指標門檻、歷史致病率先驗、logistic regression 與多種梯度提升樹。另外用同院另一團隊的盲化重判（215 份檢體）與培養／塗片／核酸檢測確認（231 組微生物–檢體配對）作為額外參考。[(ref: main p.3, p.19–20)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=19)

## 方法詳解

**九個定量指標。** species-specific reads、genus-specific reads、species detection rank、genus detection rank、genome coverage、depth ratio、Shannon index、species relative abundance、genus relative abundance。病毒列沒有屬層級欄位，作者以種層級數值代入。[(ref: main p.16, p.25)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=25)

**微調設定。** LoRA rank 8、α 32、dropout 0.05，套在 query、key、value、output 與 gate、up、down 投影，可訓練參數 21.82M（約 0.266%）；AdamW、cosine schedule、warm-up ratio 0.03，一個 epoch（5,052 步），每裝置 batch 4、梯度累積 4、8 張 Ascend 910（有效 batch 128），最大序列長度 1,024，seed 42。所有評估都用第 5,052 步的 checkpoint。[(ref: main p.19)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=19)

**處理極端不平衡。** 致病列只佔候選列的 0.6%–1.3%。作者在兩個答案 token 上用帶類別權重的 focal loss，並做 hard-negative mixing：依難度分數複製致病列、以加權抽樣保留非致病列，最終訓練檔 646,600 列中有 32,330 列致病（5.00%），約為原始比例的 7.9 倍。[(ref: main p.16, p.19)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=19)

**判讀規則。** 不調門檻、不用取樣：harmful 的 logit 大於 harmless 就判為致病。基線的單一指標門檻則在開發集上以最大化 F1 決定（例如 species-specific reads ≥ 355、genome coverage ≥ 6.91）。作者提醒，各方法是在相同列上比較各自的 operating point，因此差異同時反映模型本身與門檻選擇。[(ref: main p.19–20)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=20)

**指標定義。** 列層級召回 = tp／(tp + fn)；每檢體假陽性 = 假陽性列數／評估檢體數；檢體層級 complete recall = 有致病菌的檢體中全部致病列都被找回的比例；within-unit AUC 只在至少有 5 個致病與 5 個非致病偵測的（菌種，部位）單位內計算。[(ref: main p.19–20)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=20)

**消融與情境實驗。** 把五個 prompt 區塊逐一以既有的缺值 token 遮蔽，在保留集上重評；另外試了兩種補情境的做法：附上同檢體共同偵測的 partner list，以及先跑一次、把第一輪判為致病的其他微生物放進 prompt 的 two-stage 版本。[(ref: main p.25)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=25)

**洩漏與重疊檢查。** 作者稽核文字欄位是否直接洩漏標籤，只找到一個診斷欄位標記 0.02% 的列（PPV 0.13）。保留集有 125 位病人（12.9%）也出現在開發集，2025 年第一季有 42 位（4.7%）出現在較早資料；排除重疊檢體後列層級召回只變動 +0.0061 與 −0.0012。[(ref: main p.18, p.20)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=18)

- **論文未交代** — prompt 模板全文；論文描述了五個區塊與欄位，但沒有附上實際的序列化文字。
- **論文未交代** — focal loss 的 γ 與各類別 α 值，作者自述這兩個值沒有留在訓練紀錄中、需再核對。[(ref: main p.19)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=19)
- **論文未交代** — 定序平台；臨床背景欄位缺漏嚴重，2025 年第一季的年齡與性別全部缺失，模型實際能用的臨床資訊比 prompt 區塊名稱看起來少。[(ref: main p.16)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=16)
- **論文未交代** — 研究是否預先註冊；資料與程式碼在預印本階段都還不能取得。

## 資料與實驗

### 資料

| 項目 | 開發集（≤2024） | 保留集（≤2024） | 2025 年第一季 |
|---|---|---|---|
| 檢體數 | 2,479 | 1,214 | 1,162 |
| 病人數（下限） | 1,940 | 972 | 889 |
| 候選列數 | 719,426 | 431,566 | 182,875 |
| 致病列比例 | 0.643% | 0.634% | 1.301% |
| 每檢體候選列數，中位數 | 186 | 243.5 | 102 |

[(ref: main p.15–16, p.18)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=15)

病人是由住院號與姓名在院內重建，因此病人數是下限；全體 4,855 份檢體來自 19 種採樣部位。另兩個額外參考集：2025 年 3–4 月 215 份檢體由同院另一團隊在不知原判斷下重判（兩團隊在致病菌層級 Dice 0.898、Jaccard 0.815、致病菌集合完全一致 77.2%），以及 231 組有培養、塗片或核酸檢測確認的微生物–檢體配對。[(ref: main p.3, p.15, p.17)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=17)

### 實驗：主要表現與基線（論文 Results 與 Figure 1e）

| 指標 | 保留集（≤2024） | 2025 年第一季 |
|---|---|---|
| 列層級致病菌召回 | 92.44% | 84.49% |
| 每檢體假陽性列數 | 2.00 | 0.98 |
| 檢體層級 complete recall | 84.00% | 67.89% |
| 每多找回 1 個致病菌、相對樹基線多出的假陽性 | 3.1 | 1.4 |

| 方法（較早世代） | Average precision |
|---|---|
| 微調 Qwen3-8B | 0.825 |
| 梯度提升樹（定量指標＋菌種＋部位＋報告文字） | 0.707 |
| 同一樹模型，改在 hard-negative 加權後的訓練檔上擬合 | 0.798 |

在較早世代的測試中，微調模型比樹基線多找回 252 個致病菌、同時多出 790 個假陽性。[(ref: main p.3)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=3)

另一組分析只看定量指標本身，在每個（菌種，部位）單位內計分，不能與上表的整體 AP 直接相比：

| 單位內（菌種 × 部位）規則 | ≤2024 | 2025 年第一季 |
|---|---|---|
| 最佳單一定量指標，AP | 0.595 | 0.584 |
| 五個定量指標的 logistic 合併（單位層級 5-fold），AP | 0.741 | 0.750 |

[(ref: main p.5, p.20–21)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=5)

### 實驗：依採樣部位的召回

| 部位 | 保留集（≤2024） | 2025 年第一季 |
|---|---|---|
| 支氣管肺泡灌洗液（BALF） | 96.0% | 89.0% |
| 血漿 | 93.0% | 80.6% |
| 痰 | 96.9% | 93.1% |
| 腦脊髓液（CSF） | 59.1% | 71.8% |

[(ref: main p.3, p.20)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=20)

### 實驗：遮蔽、補情境與外部參考

| 實驗 | 結果 |
|---|---|
| 遮蔽九個定量指標 | AP 0.825 → 0.296；每檢體假陽性約 2.0 → 7.44 |
| 遮蔽知識庫註記 | 每檢體假陽性升到 3.39，召回變化不大 |
| Two-stage 補情境（2025 年第一季） | 召回 84.49% → 75.96%；complete recall 67.89% → 51.04% |
| 盲化重判：兩團隊都判為致病的列（n = 359） | 模型召回 90.5% |
| 盲化重判：只有一方判為致病的列 | 原團隊 71.1%（n = 38）、重判團隊 70.6%（n = 17） |
| 盲化重判：判為致病的列數 | 模型 589、原團隊 397、重判團隊 376 |
| 微生物學確認的 231 組配對 | 原團隊判致病 194（84.0%）、模型 202（87.4%），exact McNemar p = 0.077 |

[(ref: main p.5, p.12–13)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=12)

## 結果

- **主要結果** — 在保留集上，模型找回 92.44% 的參考致病菌，每份檢體平均多判 2.00 個假陽性列；換到 2025 年第一季，召回降到 84.49%、假陽性 0.98，能找回檢體內全部致病菌的比例從 84.00% 降到 67.89%。作者指出這一批的建庫方式與標籤建構不同，下降不能只歸因於時間。[(ref: main p.3, p.14)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=3)
- **與樹模型比** — AP 0.825 高於同樣輸入的梯度提升樹 0.707，但若樹模型也用 hard-negative 加權的訓練檔，差距縮到 0.825 對 0.798；在各自的 operating point 上，模型多找回的致病菌伴隨更多假陽性（較早世代每多找回一個多 3.1 個，2025 年第一季 1.4 個）。[(ref: main p.3)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=3)
- **單一讀數不夠** — 在同一菌種、同一部位的單位內，genome coverage、species relative abundance 與 species-specific reads 的 within-unit AUC 中位數分別為 0.922、0.913、0.869，但最好的單一指標 AP 只有 0.595，五個指標合併後到 0.741；作者據此認為讀數或覆蓋度單獨不足以判定致病菌，菌種身分與採樣部位各自帶有額外資訊。[(ref: main p.5)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=5)
- **菌種與部位會改變判斷** — *Pseudomonas aeruginosa* 佔其屬內致病檢體的 91%，致病率是同屬其他菌合計的 284 倍；*E. coli* 在血漿、BALF、CSF 被判為致病的比例分別為 37.4%、11.8%、3.1%。234 個可檢定菌種中有 48 個在不同部位的致病率不同（FDR < 0.05）。被註記為常見定植菌的微生物也會被判為致病。[(ref: main p.5–6)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=5)
- **模型主要靠定量指標** — 遮蔽定量指標後 AP 從 0.825 掉到 0.296、假陽性升到每檢體 7.44；遮蔽知識庫註記主要讓假陽性增加（3.39），遮蔽菌種身分降低召回，臨床背景與部位的影響較小。[(ref: main p.5)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=5)
- **補情境沒有幫助** — partner list 沒有改善表現；two-stage 版本反而讓 2025 年第一季的召回從 84.49% 降到 75.96%，在檢體內沒有其他致病菌的分層中從 88.5% 降到 46.0%。[(ref: main p.12)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=12)
- **對照第二組人與微生物學** — 兩團隊都判致病的列模型找回 90.5%，只有一方判致病的列約 71%；模型判為致病的列（589）明顯多於兩個團隊（397、376），其中 225 列兩團隊都判為非致病。在 231 組微生物學確認的配對上，模型判致病比例 87.4%、原團隊 84.0%，差異未達統計顯著（p = 0.077）。[(ref: main p.12–13)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=13)

## 限制

**作者自述的限制。** 參考標籤是治療團隊的判斷，盲化重判也來自同一家醫院，無法排除共同的臨床偏誤；臨床背景記錄不完整；2025 年第一季在建庫與標籤建構上與較早世代不同；同一病人的多份檢體可能相關，重疊敏感度分析只涵蓋 607 份有致病菌的檢體；單一中心；共同判定模組只有核心部分穩定；研究只量測與參考判斷的一致性，沒有評估對臨床醫師、抗生素決策或病人結局的影響。[(ref: main p.14)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=14)

**本書庫的觀察。**

- **模型學的是「這家醫院怎麼判」** — 標籤是治療團隊記下的結論，模型重現的是在地判讀習慣，連同其偏誤；標籤推導本身的 recall 只有 0.8594，表示有一部分被記下的致病菌在訓練與評估裡被當成非致病。
- **假陽性的代價要一起看** — 模型判為致病的列數比任一人工團隊多約 50%，對照樹基線時每多找回一個致病菌要多 1.4–3.1 個假陽性；若用在臨床，這些多出來的「致病」會直接轉成待確認的工作量或潛在的過度治療，論文沒有評估這個成本。
- **AP 優勢與訓練資料的處理有關** — 樹模型改用同樣的加權訓練檔後 AP 從 0.707 升到 0.798，LLM 與樹模型的差距有一大部分來自資料處理，而不只是模型類型。
- **CSF 是弱點** — CSF 召回在保留集只有 59.1%，正是誤判代價最高的部位之一；作者也指出 CSF 的致病陽性數少。

## 與書庫其他文章的關係

ASA 分級那篇在術前結構化資料上比較 LoRA 微調的 Qwen 與非生成式 readout、傳統機器學習的準確度與標籤成本，本篇同樣以 LoRA 微調 Qwen3-8B 讀結構化欄位，並與梯度提升樹等傳統基線在相同列上比較，兩篇都顯示 LLM 的優勢大小取決於比較條件與資料處理: [不生成理由、只讀 A–D 選項的機率：Qwen3.5-9B 分 ASA 身體狀態，比生成式提示快約 64 倍，再用 1,000 個在地標籤調三個門檻，κ 只比 LoRA 低約 0.02，標籤再多 LoRA 仍會拉開](2026-10-28-asa-ps-llm-readout-vs-lora.md)

## 實務的啟發

- **可借用的資料設計** — 把每份 mNGS 報告展開成「每個偵測微生物一列」，用病歷中的致病菌判斷當弱標籤，並先做反向驗證（precision／recall）量出標籤本身的缺口，是把既有檢驗紀錄變成可評估資料集的具體做法。
- **可借用的評估設計** — 同時報告列層級召回、每檢體假陽性與檢體層級 complete recall，並把「多找回幾個、多付幾個假陽性」攤開比較，比只報 AP 更能看出模型放進流程後的工作量；分部位報告則能抓出像 CSF 這種整體數字掩蓋掉的弱點。
- **待驗證的方向** — 以 LLM 做 mNGS 致病菌初篩的可行性，目前只證實「能重現同院的判讀並有較高召回」；是否改善抗生素決策或病人結局、在其他醫院與定序流程上是否成立，論文沒有測試，作者也把它列為未來工作。
- **證據強度** — 它支持「在單一醫院的回顧性資料上，微調 8B 模型能以較高召回、較多假陽性重現治療團隊的致病菌判斷，而定量指標是它最依賴的證據」；不足以支持這個模型可以取代臨床微生物或感染科的判讀。[(ref: main p.14)](https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf#page=14)

## References

- **main** — Wei M, Zhao Y, Fang C, et al. *Clinical pathogen adjudication in metagenomic sequencing using a large language model*. medRxiv v1 (2026). DOI: <https://doi.org/10.64898/2026.10.16.26361411>。全文 PDF：<https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1.full.pdf>。文內引用位置：p.1（作者與單位）、p.2（Introduction）、p.3–13（Results、Figure 1–6）、p.14（Discussion 與限制）、p.15–26（Methods、資料與程式可得性）。
- **abs** — medRxiv abstract page：<https://www.medrxiv.org/content/10.64898/2026.10.16.26361411v1>。

[Home](../) · [AI Papers](./)
