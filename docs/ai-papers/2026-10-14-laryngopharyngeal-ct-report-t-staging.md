---
catalog_id: "arxiv:2610.06837"
editors:
  - "Clare"
refs:
  main:
    title: "Anatomy-aware Fine-grained Multimodal Fusion for Laryngopharyngeal Cancer T-Staging Prediction Using CT and Radiology Report"
    url: "https://arxiv.org/pdf/2610.06837v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 把喉咽 CT 拆成七個器官節點，再讓放射報告逐器官補證據：喉咽癌 T 分期多模態模型在三個外部中心的表現

## 來源

- 團隊：Xingyue Zhao（DAMO Academy, Alibaba Group；北京協和醫院神經外科）、Yanzhou Su（DAMO Academy；Hupan Laboratory）、Fang Zhang（復旦大學附屬眼耳鼻喉科醫院放射科）為共同第一作者；通訊作者為 Jian Wang（復旦大學附屬中山醫院放射科）、Dakai Jin（DAMO Academy）、Na Shen（復旦大學附屬中山醫院耳鼻咽喉頭頸外科；中山醫院廈門醫院）。其餘作者來自 DAMO Academy、福州大學、北京協和醫院神經外科、復旦大學附屬中山醫院耳鼻咽喉頭頸外科與長庚紀念醫院核子醫學科，全文共 15 位作者。[(ref: main author block)](https://arxiv.org/pdf/2610.06837v1)
- 論文：*Anatomy-aware Fine-grained Multimodal Fusion for Laryngopharyngeal Cancer T-Staging Prediction Using CT and Radiology Report*，arXiv v1，2026-10-05 提交，分類 cs.CV，目前只有一個版本。[(ref: abs)](https://arxiv.org/abs/2610.06837)
- 識別碼：[arXiv:2610.06837](https://arxiv.org/abs/2610.06837)。
- 全文：[arXiv PDF v1](https://arxiv.org/pdf/2610.06837v1)。論文未標示期刊或會議出處。
- 資料與程式：論文正文未說明程式碼或院內資料是否釋出；四個資料來源中只有 TCGA 為公開資料。[(ref: main §IV-A)](https://arxiv.org/pdf/2610.06837v1)
- 研究性質：完整方法論文，不是 pilot；核心方法有實作，在單一中心做 5-fold 交叉驗證，並在三個外部中心共 217 位病人上測試。T 分期標準答案來自病理（AJCC 第 8 版），不是從 CT 報告抽出。外部測試中的 TCGA 105 人沒有原始臨床報告，CT 報告是由一位放射專科醫師為本研究撰寫、再經第二位判讀者複核。[(ref: main §IV-A, Table III)](https://arxiv.org/pdf/2610.06837v1)
- 證據邊界：本文數值以 PDF v1 的正文與 Table II、III、IV、VII 為準；Table II 的「±」論文未定義其意義，本文照錄但不解讀為信賴區間。Table IV 中「AOG＋OCA」一列只引用正文有寫出的兩個 F1 數值，其餘儲存格未納入引述。

**編輯：** Clare

作者用四個中心 656 位喉咽癌病人的 CT 與放射報告，訓練一個把喉咽拆成七個器官節點、讓報告逐器官補上侵犯證據的 T 分期模型；在三個外部中心 217 人上，二分類 macro F1 為 76.46%、三分類為 60.27%，都高於八個對照方法，但外部測試有近一半病人的報告是為本研究另外撰寫。[(ref: main Abstract, §IV-A, Table II)](https://arxiv.org/pdf/2610.06837v1)

## 流程

![喉咽癌 T 分期模型的研究設計示意圖。上排三個方塊：左邊藍色方塊為 CT 輸入（1 mm 等向重取樣後縮放為 128x128x128、HU 視窗 center 50／width 450、Continual Segment 涵蓋 143 個器官並產生 7 個器官遮罩且未針對院所微調、Swin Transformer 編碼器以 CT 乘上遮罩得到器官特徵）；中間綠色方塊為 (a) AOG 器官圖（3 個原發部位節點 supraglottic、glottic、subglottic 彼此全連接，4 個候選侵犯節點 esophagus、thyroid gland、trachea、oral cavity，每個原發部位連到每個候選器官）；右邊橘色方塊為放射報告輸入（凍結的 BioBERT token 表徵、[CLS] 作為全域文字節點、Claude 3.5 Haiku 判斷四個器官中哪些被描述為受侵犯，只取正向陳述並以 JSON 輸出）。左方塊以箭頭指向中間方塊；中間方塊與右方塊各以箭頭指向下排中間的紫色方塊 (b) OCA＋(c) REG（每個器官節點對報告 token 做 cross-attention；文字節點連到原發部位與 LLM 標出的器官；Graph Attention Network 接分類器），紫色方塊再以箭頭指向右下灰色方塊 Output: T-stage（二分類 T1-T2 vs T3-T4、三分類 T1／T2／T3-T4、標準答案為病理 AJCC 8th、loss 為 cross-entropy）。左下灰色方塊為資料（656 位病人：FUZH 439 人做 5-fold 交叉驗證；外部測試 217 人：CGMH 25、EENT 87、TCGA 105；TCGA 報告為本研究撰寫），沒有箭頭連出](assets/laryngopharyngeal-t-staging-organ-graph-design.png)

圖：本書庫依論文 §III、§IV 與 Table III 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖。[(ref: main §III–IV, Table III)](https://arxiv.org/pdf/2610.06837v1)

## 背景／問題

T 分期描述原發腫瘤的範圍與向周邊結構的侵犯，是喉咽癌治療決策的依據。作者在引言中主張，現行做法仰賴侵入性切片，而以 CT 判斷 T 分期困難，因為腫瘤向周邊結構的侵犯型態複雜；這是論文的問題設定，本研究本身沒有比較切片與影像分期的臨床流程。[(ref: main Abstract, §I)](https://arxiv.org/pdf/2610.06837v1)

作者指出既有電腦輔助方法有兩個缺口：一是沒有把「腫瘤從原發部位侵犯到哪些器官」的解剖結構寫進模型，二是影像與放射報告只做整體層級的融合，沒有把報告中描述某個器官的句子對到影像上的那個器官。放射報告對分期有幫助這一點，論文以自己的消融實驗檢驗，而不是當成前提直接採用。[(ref: main §I, §IV-D Table IV)](https://arxiv.org/pdf/2610.06837v1)

## 方法摘要

**器官圖（Anatomy-Structured Organ Graph, AOG）。** 用現成的全身 CT 分割模型 Continual Segment 切出七個結構：三個原發部位（supraglottic、glottic、subglottic）與四個可能受侵犯的器官（esophagus、thyroid gland、trachea、oral cavity）。每個結構的影像特徵當成一個圖節點；原發部位之間全連接，每個原發部位再連到每個候選器官，候選器官彼此之間不連邊。[(ref: main §III-B)](https://arxiv.org/pdf/2610.06837v1)

**器官對報告的對齊（Organ-Anchored Cross-Modal Alignment, OCA）。** 報告以凍結的 BioBERT 編碼成 token 表徵；每個器官節點以自己的影像特徵當 query，對整份報告的 token 做 cross-attention，把與該器官相關的文字證據以殘差方式加回節點。[(ref: main §III-C)](https://arxiv.org/pdf/2610.06837v1)

**報告強化的圖修正（Report-Enhanced Graph-Refinement, REG）。** 以報告的 [CLS] 表徵建立一個文字節點，連到三個原發部位；再請 LLM（Claude 3.5 Haiku）判斷四個候選器官中，哪些在報告裡被明確描述為受侵犯，文字節點也連到這些器官。最後以 Graph Attention Network（GAT）做訊息傳遞並輸出 T 分期。[(ref: main §III-D)](https://arxiv.org/pdf/2610.06837v1)

**任務與評估。** 兩種設定：二分類（T1–T2 vs. T3–T4）與三分類（T1、T2、T3–T4）。指標為 accuracy 與 macro F1（各類 F1 的未加權平均）。[(ref: main §IV-A–B)](https://arxiv.org/pdf/2610.06837v1)

## 方法詳解

**CT 前處理與影像特徵。** 整卷 CT 重取樣到 1 mm 等向、縮放為 128×128×128，HU 視窗 center 50、width 450 後縮放到 [0, 1]。器官特徵由 CT 與各器官遮罩逐元素相乘後送入「以醫學影像預訓練」的 Swin Transformer 取得。分割模型 Continual Segment 涵蓋 143 個全身 CT 器官，論文明言未針對各院所微調。[(ref: main §III-B, §IV-B)](https://arxiv.org/pdf/2610.06837v1)

**LLM 在流程中的角色。** Claude 3.5 Haiku 只負責一件事：讀報告、列出被描述為受侵犯的器官，提示要求排除否定句，並區分 thyroid gland 與 thyroid cartilage，輸出為 JSON 清單。作者表示 GPT-4o 與 Qwen-2.5-72B 在全部 439 份訓練報告上給出相同結果，抽取結果也經人工確認。因為 LLM 的輸出決定文字節點連到哪些器官，抽取錯誤會直接改變圖的拓撲。[(ref: main §III-D)](https://arxiv.org/pdf/2610.06837v1)

**訓練設定。** 損失為 cross-entropy；Adam，學習率以 cosine 排程從 1×10⁻⁶ 降到 1×10⁻⁷，weight decay 1×10⁻⁵，batch size 8；單張 NVIDIA H20 GPU、PyTorch。BioBERT 在最終模型中凍結。[(ref: main §IV-B)](https://arxiv.org/pdf/2610.06837v1)

**驗證設計。** FUZH（復旦大學附屬中山醫院）439 人做 5-fold 交叉驗證；CGMH（長庚紀念醫院）、EENT（復旦大學附屬眼耳鼻喉科醫院）與 TCGA 合計 217 人作為外部測試集。[(ref: main §IV-A–B)](https://arxiv.org/pdf/2610.06837v1)

- **論文未交代** — 外部測試的預測如何產生：是五個 fold 模型的集成，還是逐一評估再平均；Table II「±」代表的是 fold、隨機種子或其他來源的變異。
- **論文未交代** — 訓練 epoch 數、Swin Transformer 的具體版本與預訓練權重、GAT 的層數、特徵維度，以及 fold 的切分方式。
- **論文未交代** — 收案條件（期間、是否連續收案、排除條件）；只有 FUZH 註明為增強 CT，其他三個來源的掃描期相與是否施打顯影劑未說明；CGMH 與 EENT 的報告如何取得。
- **論文未交代** — 與放射科醫師比較時，醫師的年資、看到的是 CT 單獨或 CT 加報告、是否盲測；「每類各抽 20 例、共 80 例」對應的是哪一種分類（三分類只有三類）。
- **論文未交代** — Table IV 的全模型二分類 F1 為 83.96，與 Table II 的內部結果 80.83 不同，Table IV 圖說稱其為「代表性的內部 fold」，正文沒有說明兩者的關係。

## 資料與實驗

下表為論文 Table III 的病人數，依中心與病理 T 分期列出。[(ref: main §IV-A, Table III)](https://arxiv.org/pdf/2610.06837v1)

| 中心 | 用途 | T1 | T2 | T3 | T4 | 合計 |
|---|---|---|---|---|---|---|
| FUZH | 5-fold 交叉驗證 | 151 | 116 | 99 | 73 | 439 |
| CGMH | 外部測試 | 2 | 4 | 4 | 15 | 25 |
| EENT | 外部測試 | 20 | 29 | 17 | 21 | 87 |
| TCGA | 外部測試（報告為本研究撰寫） | 24 | 27 | 18 | 36 | 105 |
| 合計 | — | 197 | 176 | 138 | 145 | 656 |

下表摘錄論文 Table II 的 macro F1（%），內部為 FUZH 交叉驗證、外部為三個外部中心合併。對照方法包含三個只用影像的模型（SwinViT、VDPF、MRSN）與五個影像加報告的多模態模型（CPAM、TGCAM、MMBCD、LViT、MMI）。[(ref: main §IV-C, Table II)](https://arxiv.org/pdf/2610.06837v1)

| 方法 | 二分類 內部 F1 | 二分類 外部 F1 | 三分類 內部 F1 | 三分類 外部 F1 |
|---|---|---|---|---|
| SwinViT | 58.82±0.57 | 43.64±3.74 | 42.02±2.49 | 33.10±3.51 |
| VDPF | 71.47±3.71 | 61.99±3.42 | 51.53±2.72 | 42.40±4.27 |
| MRSN | 59.68±4.13 | 49.10±3.14 | 43.57±3.31 | 34.53±3.59 |
| CPAM | 74.83±3.09 | 69.99±5.03 | 56.08±3.97 | 45.39±3.67 |
| TGCAM | 76.04±3.23 | 74.09±3.11 | 55.94±2.14 | 50.93±3.97 |
| MMBCD | 77.35±3.00 | 73.54±4.47 | 58.44±4.84 | 46.35±2.89 |
| LViT | 75.54±2.39 | 68.83±4.44 | 55.92±5.50 | 49.12±10.21 |
| MMI | 77.59±4.01 | 69.88±5.11 | 57.26±1.57 | 51.54±4.74 |
| 本文方法 | 80.83±5.35 | 76.46±1.35 | 61.43±3.25 | 60.27±3.03 |

下表摘錄論文 Table IV 的消融結果（macro F1，%），論文說明為三個隨機種子的平均 ± 標準差。[(ref: main §IV-D, Table IV)](https://arxiv.org/pdf/2610.06837v1)

| AOG | OCA | REG | 二分類 F1 | 三分類 F1 |
|---|---|---|---|---|
| — | — | — | 58.76±2.68 | 39.16±1.60 |
| ✓ | — | — | 77.96±1.23 | 52.80±2.31 |
| — | ✓ | — | 80.97±1.28 | 58.47±1.06 |
| ✓ | ✓ | — | 81.63±1.71 | 61.52 |
| ✓ | ✓ | ✓ | 83.96±0.50 | 64.53±0.70 |

## 結果

- **外部測試** — 本文方法的二分類 macro F1 為 76.46%（accuracy 76.50%），三分類為 60.27%（accuracy 63.78%）；八個對照方法中，外部二分類最高的是 TGCAM（74.09%），外部三分類最高的是 MMI（51.54%）。[(ref: main §IV-C, Table II)](https://arxiv.org/pdf/2610.06837v1)
- **內部與外部的落差** — 本文方法二分類從內部 80.83% 降到外部 76.46%，三分類從 61.43% 降到 60.27%；只用影像的 SwinViT 同期從 58.82% 降到 43.64%。[(ref: main Table II)](https://arxiv.org/pdf/2610.06837v1)
- **消融** — 以整卷 CT 為輸入的基線二分類 F1 為 58.76%；單獨加入 AOG 或 OCA 分別到 77.96% 與 80.97%，三個模組全上為 83.96%。[(ref: main §IV-D, Table IV)](https://arxiv.org/pdf/2610.06837v1)
- **穩健性** — 對器官分割施加 ±5% 與 ±10% 的擾動，F1 分別下降 1.1 與 2.8 個百分點；把報告改寫得更簡略或更詳細（CT 與模型不變），macro F1 維持在 80.4%–82.1%，最大變動 1.7 個百分點。[(ref: main §IV-E)](https://arxiv.org/pdf/2610.06837v1)
- **與放射科醫師比較** — 在外部測試集抽出的 80 例上，二分類 F1 為模型 76.25%、兩位放射科醫師 76.16% 與 74.98%；三分類為模型 59.71%、醫師 53.03% 與 53.63%。[(ref: main §IV-H, Table VII)](https://arxiv.org/pdf/2610.06837v1)
- **錯誤分析** — 在 Fold 1 的 88 例中有 16 例分錯，9 例分期過高、7 例過低；9 例分期過高中有 7 例是報告明確寫了軟骨侵犯、但病理未證實。[(ref: main §IV-H, §V)](https://arxiv.org/pdf/2610.06837v1)

## 限制

**作者自述的限制。** 方法依賴預訓練的器官分割模型，不同掃描協定與廠牌可能影響表現，作者建議部署前做院所層級驗證；各院放射報告的用語與詳略不同，可能影響 OCA 與 REG；仍需要在疾病分布不同的獨立世代上做前瞻驗證；當報告對侵犯的描述不可靠時，可能把邊界病例推向錯誤的分期。[(ref: main §V)](https://arxiv.org/pdf/2610.06837v1)

**本書庫的觀察。**

- **外部測試有一部分是研究用報告** — TCGA 105 人占外部測試 217 人的近一半，其 CT 報告是為本研究撰寫並經複核，用語與詳略未必等同臨床日常報告；論文在討論中稱報告是例行臨床文件、而非研究整理的文字，這個描述不適用於 TCGA。論文沒有分中心列出外部結果，讀者無法分開看 CGMH／EENT 與 TCGA 的表現。
- **模型讀了放射科醫師的判讀** — 模型的輸入包含報告，而報告本身就是放射科醫師對侵犯範圍的判讀；與兩位放射科醫師的比較沒有交代醫師看到哪些資料，因此 Table VII 不能直接解讀為「模型比醫師會看 CT」。
- **變異的意義不明** — Table II 的「±」沒有定義，也沒有信賴區間或配對檢定；外部二分類 76.46% 對 TGCAM 74.09% 的差距為 2.37 個百分點，小於 TGCAM 自己的「±3.11」。
- **內部數字不一致** — 全模型內部二分類 F1 在 Table II 為 80.83%、在 Table IV 為 83.96%，論文未解釋。

## 與書庫其他文章的關係

RADAR 在腹部 CT 上先把影像拆成 18 個器官、再與報告做器官層級的對齊；本篇在喉咽 CT 上把七個結構做成圖節點，並讓報告在分期時逐器官提供侵犯證據，兩篇都以現成的器官分割作為圖文對齊的前提: [RADAR：把腹部 CT 拆成 18 個器官再對齊報告，通才模型能到專家水準嗎？](2026-09-21-radar-abdominal-ct-generalist.md)

CARA-VL 把預測的解剖佔位圖壓成 VLM 的注意力偏置，本篇則把器官遮罩做成圖節點、以解剖拓撲限制訊息傳遞，兩篇都是把解剖先驗寫進模型結構的做法，也都受分割品質影響: [先教 VLM 看對地方：CARA-VL 用解剖結構導引注意力，心臟 MRI 問答能走多遠？](2026-10-02-cara-vl-cardiac-mri-anatomy-routed-attention.md)

## 實務的啟發

- **可借用的設計** — 讓 LLM 只做一件可核對的小事（從報告列出被描述為受侵犯的器官，排除否定句），再把結果當成圖的連邊，而不是讓 LLM 直接給分期；這種輸出容易人工抽查，論文也報告了三個 LLM 結果一致。換到自己的報告語料時，抽取結果仍要重新抽查。
- **可借用的量測方法** — 對分割遮罩施加擾動、把報告改寫成不同詳略，再看模型表現的變化，是評估「依賴分割與報告」的多模態模型時成本不高的檢查；論文的結果顯示這兩項擾動下的變動在 3 個百分點以內，但只測了論文設定的擾動幅度。
- **待驗證的警訊** — 模型一旦以報告為輸入，就部分繼承了報告者的判讀，包括錯誤：論文的錯誤分析顯示，報告寫了軟骨侵犯而病理未證實的病例會被分期過高。若要評估這類模型的增益，需要比較「同樣拿到報告的醫師」與模型，並分中心報告外部結果。
- **證據強度** — 這是單一回顧性研究，外部測試合計 217 人，有近一半使用研究用報告，且未報告信賴區間；它支持「器官層級的影像與報告融合在這組資料上優於所列對照方法」，不足以支持取代病理或改變臨床分期流程。

## References

- **main** — Zhao X, Su Y, Zhang F, et al. *Anatomy-aware Fine-grained Multimodal Fusion for Laryngopharyngeal Cancer T-Staging Prediction Using CT and Radiology Report*. arXiv:2610.06837v1, 2026. PDF：<https://arxiv.org/pdf/2610.06837v1>。文內引用位置：author block、Abstract、§I、§III-B、§III-C、§III-D、§IV-A、§IV-B、§IV-C、§IV-D、§IV-E、§IV-H、§V、Table II、Table III、Table IV、Table VII。
- **abs** — arXiv 摘要頁：<https://arxiv.org/abs/2610.06837>。

[Home](../) · [AI Papers](./)
