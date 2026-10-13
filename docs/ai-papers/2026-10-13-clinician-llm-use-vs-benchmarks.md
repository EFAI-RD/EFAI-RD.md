---
catalog_id: "arxiv:2610.11069"
editors:
  - "Clare"
refs:
  main:
    title: "Clinician use of language models diverges from how the models are evaluated"
    url: "https://arxiv.org/html/2610.11069v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 臨床人員實際拿 LLM 做什麼？12.8 萬筆提問對照 58 個公開基準：文件工作占最多、診斷只占 3.7%，基準的題目組成對不上

## 來源

- 團隊：Krithik Vishwanath、Haitong Lin、Anton Alyakin、Jin Vivian Lee、D. Brock Hewitt、Jie J. Yao、William Robert Small、Hammad A. Khan、Cordelia Orillac、Aakaash Varma、Brandon Ye、Daniel Alexander Alber、Gustavo Stolovitzky、Batia Wiesenfeld、Oded Nov、Wei Wu、Kang Zhang、Yindalon Aphinyanaphongs、Tim Requarth、Eric Karl Oermann，以及 The International Digital Twin Consortium in Healthcare and Medicine。單位以 NYU Langone Health 各科部為主，另有 NYU Tandon、NYU Stern、NYU Center for Data Science、Washington University School of Medicine、Johns Hopkins University School of Medicine、Stanford University School of Medicine、Macau University of Science and Technology 與 Peking University。[(ref: main)](https://arxiv.org/html/2610.11069v1)
- 論文：*Clinician use of language models diverges from how the models are evaluated*，arXiv v1，2026-10-08 提交，分類 cs.CL，授權 CC BY-NC-SA 4.0。[(ref: abs)](https://arxiv.org/abs/2610.11069)
- 識別碼：[arXiv:2610.11069](https://arxiv.org/abs/2610.11069)；[DOI: 10.48550/arXiv.2610.11069](https://doi.org/10.48550/arXiv.2610.11069)（arXiv 標示為待註冊）。
- 全文與資源：[arXiv HTML 全文](https://arxiv.org/html/2610.11069v1)；標註指引與程式碼 [nyuolab/RCQ-Map](https://github.com/nyuolab/RCQ-Map)，基準集 [nyuolab/CABA](https://github.com/nyuolab/CABA)（論文 Code／Data availability 列出）。臨床人員的提問原文含受保護健康資訊，未公開；標籤層級資料需經機構核准與資料使用協議申請。[(ref: main Data／Code availability)](https://arxiv.org/html/2610.11069v1#Sx5)
- 研究性質：單一醫療體系的回溯性觀察研究，不是 pilot；分析對象是臨床人員送出的提問，**沒有評估 LLM 助理的回答**，因此「潛在傷害」是假設回答錯誤時的推估，不是實際發生的傷害。全部標籤由一個 LLM 依標註指引產生，再以 100 筆提問的臨床人員盲評驗證。[(ref: main §3 Discussion, §4.7–4.8)](https://arxiv.org/html/2610.11069v1#Sx3)
- 證據邊界：本文數值以 arXiv HTML v1 正文、Table 1 與 Extended Data 圖表說明為準；完整標註指引（Supplementary Note 1）、各基準的完整分布（Supplementary Table 2）與 CABA 清單（Supplementary Data 1）未納入引述。

**編輯：** Clare

作者把一家學術醫療體系八個月內 6,342 位臨床人員對院內 LLM 助理的 127,833 則對話，以自訂的 RCQ-Map 標註，發現文件與行政工作占 36.2%、查詢知識占 28.9%、診斷只占 3.7%，而 58 個公開醫療基準個別涵蓋這份真實任務組成的中位數只有 31%，中位數基準也沒有任何文件或行政類題目。[(ref: main Abstract, §2.2, §2.6)](https://arxiv.org/html/2610.11069v1#Sx2.SSx2)

## 流程

![研究設計示意圖。上方分兩欄：左欄藍色方塊為真實使用端，127,833 則對話、6,342 位臨床人員、2025-08-12 至 2026-04-03，往下取每則對話的第一個臨床人員發言為 RCQ（不檢視助理回答）；右欄綠色方塊為公開基準端，13 個評估套件加前沿模型報告、175 個基準中納入 58 個，往下每個基準最多抽 200 題、只取第一個使用者發言、共標註 10,659 題。兩欄以箭頭匯入中間灰色方塊：同一個標註器 GPT-5.6 sol 加 RCQ-Map 指引。下方兩個淡黃色方塊：左為臨床人員驗證（100 筆 RCQ、每筆由 7 位中的 3 位盲評），右為比較任務分布（coverage = 1 − total variation distance）](assets/clinician-llm-use-vs-benchmarks-design.png)

圖：本書庫依論文 §4.1–4.9 的文字與 Fig. 1 圖說重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖。[(ref: main §4 Methods)](https://arxiv.org/html/2610.11069v1#Sx4)

## 背景／問題

醫療 LLM 的評估多半是給模型一題、看答案對不對。作者引用的文獻指出，到 2024 年初為止的 519 篇 LLM 醫療評估中只有 5% 使用真實病人照護資料，另一篇涵蓋至 2025 年 9 月、4,609 篇研究的回顧中，77.3% 沒有使用任何真實臨床資料。[(ref: main Introduction)](https://arxiv.org/html/2610.11069v1#Sx1)

作者據此指出，現行評估隱含兩個假設：基準的任務組成與臨床人員實際交給模型的任務相近；臨床人員的提問照原樣就能被好好回答。這兩個假設在此前缺少以真實部署資料做的直接檢驗，本研究就是要檢驗它們。[(ref: main Introduction)](https://arxiv.org/html/2610.11069v1#Sx1)

## 方法摘要

研究在一個多院區的都會學術醫療體系內進行，取 2025-08-12 到 2026-04-03 間臨床人員對院內安全 LLM 助理的對話，以每則對話的第一個臨床人員發言作為「真實臨床提問」（real clinical query，RCQ）。作者開發 RCQ-Map 標註架構，涵蓋任務類別、提問意圖、潛在傷害、可回答程度、最安全的回應方式等欄位，交由 GPT-5.6 sol 對整個語料逐筆標註，並以 100 筆提問的臨床人員盲評驗證標註品質。[(ref: main §4.1–4.8)](https://arxiv.org/html/2610.11069v1#Sx4)

比較端是作者整理的 Clinical AI Benchmark Atlas（CABA）：從 13 個評估套件與前沿模型技術報告中篩出 58 個可公開下載、英文、純文字、醫療專用、單一請求的基準，每個最多抽 200 題，用同一個標註器與同一份指引標註，再以 total variation distance（TVD）比較基準與 RCQ 的任務分布。[(ref: main §4.9)](https://arxiv.org/html/2610.11069v1#Sx4.SSx9)

## 方法詳解

**資料來源與隱私處理。** 回溯性觀察研究；臨床人員身分與職類由 Epic Clarity 取得，足科與牙科人員排除，專業別與科別以多數天數歸屬。研究被認定為非人體受試者研究，只匯出標籤層級資料；職類 × 專科的格子以 k = 10 做 k-anonymity，977 則對話（35 位臨床人員）被改記為 Other，3 則移除，698 則（32 位）標為 Missing。[(ref: main §4.1–4.2)](https://arxiv.org/html/2610.11069v1#Sx4.SSx1)

**RCQ 的定義。** 每則對話的第一個臨床人員發言即為 RCQ，超過 100,000 字元截斷；121 則沒有臨床人員文字的對話排除，87 則重試後仍未通過 schema 驗證。127,833 則對話中 127,625 則（99.8%）得到有效標註。[(ref: main §4.3, §2.1)](https://arxiv.org/html/2610.11069v1#Sx4.SSx3)

**RCQ-Map 標註架構。** 最終指引有 24 個強制選擇欄位；作者刪除兩個信度過低的欄位（actionability α 0.39、evidence dependence α 0.29）並合併病人與機構脈絡後，報告 20 個欄位，分六個區塊。主要欄位包括：[(ref: main §4.4, §4.6, Extended Data Table 1)](https://arxiv.org/html/2610.11069v1#Sx4.SSx4)

- **Task category** — 10 類：documentation and workflow、coding and administrative、foundational knowledge、drug information and pharmacotherapy、treatment and management、diagnosis and differential、test and result interpretation、patient education and communication、procedural guidance，以及非臨床或沒有可辨識請求的 other。10 類再歸成四種 kind of work：documentation and administration、knowledge retrieval、clinical reasoning 與 other。
- **Question intent** — 12 種意圖，分成五組：decide or verify、look up or understand、draft text or code、follow a procedure 與 other。
- **Potential harm** — minimal、low、moderate、high、critical 五級，前提是「臨床人員未經查核就照錯誤答案行動」；非臨床傷害上限為 moderate。
- **Answerability** — 照原樣能否被好好回答：high、partial（需要重大假設才能回答）、low（無法回答）。
- **Safest response** — 直接回答、以檢索到的權威來源為據回答、向臨床人員追問澄清、轉介人類專家、拒答，五選一。
- 另有是否針對特定病人、是否需要病人或機構資訊、是否需要最新文獻，以及藥名、劑量、檢驗、影像、弱勢族群、急迫情境、要求產生文字、臨床縮寫等表面特徵旗標。

**LLM 標註。** 標註器為 GPT-5.6 sol（reasoning effort 設為 none），以指引全文作為 system prompt、每筆提問作為一則 user message，輸出受嚴格 JSON schema 約束，失敗則重試。[(ref: main §4.7)](https://arxiv.org/html/2610.11069v1#Sx4.SSx7)

**臨床人員驗證。** 以 seed 42 隨機抽 100 筆 RCQ，每筆由 7 位臨床人員中的 3 位獨立盲評，同樣是強制選擇；信度以 Krippendorff's α（名目與序位）、Gwet's AC1、Fleiss' κ 等報告，α ≥ 0.800 視為可靠、≥ 0.667 視為可暫時接受。模型與臨床人員的比較採 held-out 設計：拿掉一位臨床人員，比較「該人」與「模型」各自對其餘兩人參考答案的一致率。[(ref: main §4.8, §4.10)](https://arxiv.org/html/2610.11069v1#Sx4.SSx8)

**Clinical AI Benchmark Atlas（CABA）。** 來源是 13 個評估套件（MedHELM、MultiMedQA、MedS-Bench、ClinicBench、MIRAGE、Medmarks、BRIDGE、MEDIC、MMedBench、CLUE、MedBench、HealthBench、MAST）與 Epoch AI 資料庫中前沿模型的技術報告。納入條件五項同時成立：題目免申請即可下載、英文、純文字可答、為醫療而建、單一請求。175 個被點名的基準中，下載前排除 102 個、下載後排除 15 個，剩 58 個。每個基準以 seed 20261004 從測試或評估切分隨機抽最多 200 題，移除非英文、引用未釋出影像的題目與重複題；多輪對話只取第一個使用者發言，與 RCQ 的處理一致。10,699 題中 10,659 題（99.6%）完成標註，40 題（皆來自 Med-HALT）始終未通過一致性規則。[(ref: main §4.9)](https://arxiv.org/html/2610.11069v1#Sx4.SSx9)

**Coverage 與 TVD。** 兩個任務分布的 TVD 是各類別比例差的絕對值總和的一半，0 代表相同、1 代表完全不重疊；作者把基準對 RCQ 的 coverage 定義為 1 − TVD，也就是「基準涵蓋了多少真實任務組成」。十類平均分配的假想基準，coverage 約為 55%，作者以此作為參照點。[(ref: main §4.9, §2.6)](https://arxiv.org/html/2610.11069v1#Sx4.SSx9)

**語料統計。** 盛行率的 95% CI 以臨床人員為單位做 2,000 次 cluster bootstrap；另報臨床人員加權估計，並做排除最活躍 1% 使用者、排除 Other、依職類分層的敏感度分析。高風險提問以臨床人員聚類標準誤的 logistic regression 估 adjusted odds ratio；另建一個只用 11 個文字特徵、以臨床人員分組做五折交叉驗證的高風險預測模型。報告遵循 STROBE 與 TRIPOD-LLM。[(ref: main §4.12)](https://arxiv.org/html/2610.11069v1#Sx4.SSx12)

**以臨床人員共識校正的盛行率。** 對模型給出的每一個傷害等級，估計驗證集中臨床人員多數把它放到目標類別的比例，再套用到整個語料的模型等級分布；CI 以 100 筆驗證提問做 2,000 次 bootstrap。[(ref: main §4.10–4.11)](https://arxiv.org/html/2610.11069v1#Sx4.SSx10)

- **論文未交代** — 部署給臨床人員的 LLM 助理是哪一個模型、哪一個版本，以及八個月間是否更換；論文只稱為「a secure LLM assistant」。[(ref: main §2.1, Fig. 1)](https://arxiv.org/html/2610.11069v1#Sx2.SSx1)
- **論文未交代** — 跨科分析所用的 38,647 筆「clinically anchored」RCQ 如何界定；正文只說明它們來自 31 個以器官或學科界定的專科。[(ref: main §2.3)](https://arxiv.org/html/2610.11069v1#Sx2.SSx3)
- **論文未交代** — 每一則對話只標註第一個臨床人員發言，後續追問、補充病人資料或修正提問後的內容是否改變任務類別與可回答程度，沒有量測。[(ref: main §3 Discussion)](https://arxiv.org/html/2610.11069v1#Sx3)

## 資料與實驗

下表整理論文 Table 1 的使用者組成與提問輪廓（百分比為各職類有效標註提問中的比例）。[(ref: main Table 1, §2.1)](https://arxiv.org/html/2610.11069v1#Sx2.SSx1)

| | 全部 | 主治醫師 | Fellow | 住院醫師 | APP | 護理師 |
|---|---|---|---|---|---|---|
| 臨床人員數 | 6,342 | 1,664 | 157 | 771 | 946 | 2,804 |
| 對話數（%） | 127,833（100.0） | 37,383（29.2） | 2,121（1.7） | 23,630（18.5） | 23,906（18.7） | 40,793（31.9） |
| 每人對話數，中位數（IQR） | 4（1–16） | 4（1–20） | 4（1–13） | 8（2–33） | 6（2–23） | 3（1–11） |
| Documentation & administration（%） | 36.2 | 32.1 | 37.3 | 38.0 | 35.5 | 39.1 |
| Knowledge retrieval（%） | 28.9 | 25.5 | 26.7 | 34.9 | 34.8 | 25.2 |
| Clinical reasoning（%） | 14.3 | 16.2 | 14.0 | 19.7 | 15.4 | 8.8 |
| Other（非臨床或無請求，%） | 20.6 | 26.2 | 21.9 | 7.4 | 14.4 | 26.8 |
| 針對特定病人（%） | 36.5 | 33.0 | 44.1 | 46.7 | 43.7 | 29.1 |
| 照原樣無法被好好回答（%） | 36.1 | 38.9 | 37.3 | 31.1 | 37.3 | 35.6 |
| High 或 critical 潛在傷害（%） | 13.2 | 13.5 | 16.4 | 22.6 | 15.0 | 6.2 |
| 最安全回應不是直接回答（%） | 38.8 | 44.1 | 42.6 | 35.5 | 39.8 | 35.2 |

APP 為 advanced practice provider。論文 Table 1 另有專科數、要求產生文字、需要病人或機構資訊等列，本表未全列。

下表整理 RCQ 的任務類別分布（§2.2 與 Fig. 2a 正文所列數字）。[(ref: main §2.2)](https://arxiv.org/html/2610.11069v1#Sx2.SSx2)

| Task category | RCQ 中的比例 |
|---|---|
| Documentation and workflow | 35.1% |
| Foundational knowledge | 14.8% |
| Drug information and pharmacotherapy | 14.1% |
| Treatment and management | 6.2% |
| Diagnosis and differential | 3.7% |
| Test and result interpretation | 2.7% |
| Patient education and communication | 1.2% |
| Procedural guidance | 0.5% |
| Other（非臨床或無可辨識請求） | 20.6% |

Coding and administrative 一類的比例正文未單獨列出，本表不列。

下表整理正文對個別基準的比較數字；RCQ 欄為同一指標在真實提問中的值。[(ref: main §2.6)](https://arxiv.org/html/2610.11069v1#Sx2.SSx6)

| 基準 | Diagnosis 占比 | 文件類占比 | High／critical 占比 | 對 RCQ 的 TVD |
|---|---|---|---|---|
| RCQ（真實使用） | 3.7% | 36.2%（documentation and administration） | 13.2% | — |
| MedQA | 48.0% | 0.1% | 正文未列 | 正文未列 |
| Script concordance test | 56.3% | 0.0% | 正文未列 | 0.83 |
| Real-POCQi | 正文未列 | 正文未列 | 34.5% | 正文未列 |
| MAST: NOHARM | 正文未列 | 正文未列 | 54.5% | 正文未列 |
| HealthBench Professional | 正文未列 | 25.5% | 42.7% | 0.25 |

正文對個別基準的文件類比例未註明是 task category 還是 kind of work 層級；正文拿來與基準比較的 RCQ 值是 documentation and administration 的 36.2%。TVD 0.25 與 0.83 是正文所列範圍的兩端。各基準的完整分布在論文 Supplementary Table 2，本文未納入引述。

## 結果

- **文件工作與查知識占大宗，診斷很少** — 依 kind of work，documentation and administration 占 36.2%、knowledge retrieval 占 28.9%；依 task category，documentation and workflow 35.1% 是最大類，diagnosis and differential 只占 3.7%。20.6% 是非臨床或沒有可辨識的請求，其中第一個發言裡完全沒有可辨識請求的提問占全部 RCQ 的 9.0%。[(ref: main §2.2)](https://arxiv.org/html/2610.11069v1#Sx2.SSx2)
- **使用高度集中** — 最活躍的 10% 臨床人員產生 63.3% 的對話，Gini 係數 0.76；每人對話數中位數為 4（IQR 1–16）。[(ref: main §2.1)](https://arxiv.org/html/2610.11069v1#Sx2.SSx1)
- **提問常跨出自己的科別** — 在 38,647 筆 clinically anchored RCQ 中，43.9%（95% CI 40.6–47.1%）涉及由另一個臨床科部負責的病症。[(ref: main §2.3)](https://arxiv.org/html/2610.11069v1#Sx2.SSx3)
- **高風險提問的比例與集中處** — 依標註器的判斷，13.2%（95% CI 12.4–14.0%）的 RCQ 屬 high 或 critical 潛在傷害。藥物資訊類占全部 RCQ 的 14.1%，卻占 high／critical RCQ 的 38.8%。調整任務類別與職類後，提及特定病人（adjusted OR 3.20，95% CI 2.88–3.55）與急性或急迫情境（OR 3.07，95% CI 2.52–3.74）是最強的相關特徵。只用 11 個文字特徵的模型交叉驗證 AUC 為 0.78，但要抓到 90% 的高風險提問，需要標記 60% 的全部提問。[(ref: main §2.4)](https://arxiv.org/html/2610.11069v1#Sx2.SSx4)
- **13.2% 是上限估計** — 驗證集上，標註器把 24% 的提問評為 high／critical，三位臨床人員多數只評 6%。以臨床人員共識校正後，語料中 high／critical 的盛行率為 3.7%（95% CI 1.2–5.9%），作者把 13.2% 視為高風險使用的保守上限。[(ref: main §4.11)](https://arxiv.org/html/2610.11069v1#Sx4.SSx11)
- **超過三分之一的提問照原樣答不好** — 36.1%（95% CI 34.8–37.5%）的 RCQ 照原樣無法被好好回答：23.4% 需要重大假設、12.7% 完全無法回答。high／critical 提問中這個比例為 66.8%，較低風險提問為 31.4%。[(ref: main §2.5)](https://arxiv.org/html/2610.11069v1#Sx2.SSx5)
- **最安全的回應多半是直接回答或先追問，幾乎從不是拒答** — 直接回答被評為最安全的占 61.2%（95% CI 59.7–62.6%），追問澄清 26.8%，以檢索來源為據回答 12.0%；轉介人類專家只有 32 筆、拒答只有 50 筆被評為最安全。[(ref: main §2.5)](https://arxiv.org/html/2610.11069v1#Sx2.SSx5)
- **公開基準只涵蓋真實任務組成的一小部分** — 58 個基準個別對 RCQ 任務組成的 coverage 中位數為 31%（IQR 21–39%），低於十類平均分配的約 55%。中位數基準沒有任何文件或行政類題目（IQR 0–3%），只有 13 個基準的文件類比例達到 5%。前沿模型報告使用的 12 個基準 coverage 中位數 40%（IQR 36–50%），其中 9 個的 diagnosis 比例高於真實使用的 3.7%；來自評估套件的 29 個基準中位數 35%（IQR 26–39%），兩組差異 −5.5 個百分點（95% CI −21.2 至 0.3）。[(ref: main §2.6)](https://arxiv.org/html/2610.11069v1#Sx2.SSx6)
- **最接近與最遠離的基準** — HealthBench Professional 是唯一涵蓋全部任務類別的基準，文件類占 25.5%，TVD 0.25；script concordance test 的 TVD 為 0.83。MedQA 缺少的類別占真實使用的 36%，NOHARM 缺少的類別占 76%。[(ref: main §2.6)](https://arxiv.org/html/2610.11069v1#Sx2.SSx6)
- **標註器與臨床人員的一致性** — 在 23 個判斷欄位的 held-out 比較中，模型與參考答案一致 84.6%，被拿掉的臨床人員為 83.0%。但臨床人員之間的一致性因欄位而差異很大：task category 的 α 為 0.64（95% CI 0.55–0.73），potential harm 的序位 α 只有 0.36（95% CI 0.23–0.48）；個別臨床人員把 0% 到 26% 的提問評為 high／critical。[(ref: main §2.6, §4.11)](https://arxiv.org/html/2610.11069v1#Sx4.SSx11)

作者的結論是：公開基準與臨床部署之間存在落差，挑難題能讓基準有鑑別力，但不能代表實務中的錯誤率；而且大量提問的關鍵不在答對，而在先釐清或補足脈絡。[(ref: main §3 Discussion)](https://arxiv.org/html/2610.11069v1#Sx3)

## 限制

- 作者列出的限制：單一機構、單一助理；臨床人員同時使用的其他工具無法觀察；只標註第一個發言；沒有評估助理回答，量到的是潛在而非實際傷害；標籤只由 LLM 產生，驗證只在 RCQ 上做；基準採立意選取，且 CABA 限英文與純文字；臨床人員在傷害欄位上的一致性有限；使用量集中在少數活躍使用者。[(ref: main §3 Discussion)](https://arxiv.org/html/2610.11069v1#Sx3)
- 驗證規模：標註品質的驗證只有 100 筆提問；potential harm 的序位 α 0.36、AMA use case 的 α 0.25 都低於作者自訂的 0.667 門檻，與傷害等級相關的結果應視為粗估。13.2% 與校正後 3.7% 之間差了三倍以上，本文兩個數字並列。[(ref: main §4.11)](https://arxiv.org/html/2610.11069v1#Sx4.SSx11)
- 基準端只取每題的第一個使用者發言、最多 200 題，並以同一個 LLM 標註；基準題目的寫法（例如完整病例描述）與臨床人員的短句、縮寫、指令式提問差異很大，標註器在兩種文本上的錯誤型態是否相同，論文沒有分開驗證。[(ref: main §4.9)](https://arxiv.org/html/2610.11069v1#Sx4.SSx9)
- 本書庫補充：「真實使用」本身受到部署條件影響。助理是哪個模型、能否讀取病歷、介面如何引導，都會改變臨床人員願意拿它做什麼；診斷只占 3.7%，可能部分反映了使用者對這個工具的定位，而不只是臨床需求。論文沒有交代部署模型，這一點無法從本研究判斷。
- 本書庫補充：coverage 比的是任務類別的比例，不是題目難度或錯誤代價。一個基準 coverage 低，不代表它量到的能力不重要；它說明的是「用這個分數推論整體實務表現」時需要另外的依據。

## 與書庫其他文章的關係

醫療 LLM 評估落差那篇從文獻層級指出臨床級評估證據供給偏低，本篇則用一家醫療體系 12.8 萬筆真實提問，量出公開基準與實際使用的任務組成差多少: [醫療 LLM 評估落差：研究更嚴謹，為何證據反而更舊？](2026-09-17-medical-llm-evaluation-gap.md)

PrecepTron 處理的是「怎麼評一個回答」，本篇處理的是「該拿哪些題目來評」，而且本篇指出超過三分之一的真實提問照原樣就答不好，單純評正確性的量表抓不到這一層: [PrecepTron：把醫師評分學成 LLM 評審，能讓醫療 AI 評估更可重現嗎？](2026-09-17-preceptron-clinical-ai-evaluation.md)

EntQA 的新指標建立在 MedQA 等選擇題庫上，本篇則顯示 MedQA 有 48.0% 是診斷題、文件類只有 0.1%，與真實使用中診斷 3.7%、文件與行政 36.2% 的組成相差很遠: [答對選項，也講到病人的關鍵線索了嗎？EntQA 用實體覆蓋率評醫療問答 LLM：模型層級與準確率同向，逐題訊號很弱](2026-10-11-entqa-entity-coverage-medical-qa-evaluation.md)

## 實務的啟發

- **先量自己的使用組成，再挑評估集** — 本研究的做法（取第一個發言、以固定指引標註任務類別，再與基準分布算 TVD）可以借用到任何已經上線的院內 LLM 工具；若自己的使用以文件工作為主，拿診斷選擇題的分數做採購或上線判斷，依據會很薄弱。這是可借用的量測方法，不是現成的評估集，RCQ-Map 在其他機構的信度尚未驗證。
- **評估項目要包含「該不該直接回答」** — 論文估計三分之一以上的提問照原樣答不好，而且最安全的回應常是追問而非拒答。院內評估若只計正確率，會漏掉這一類行為；這一點在論文中是由標註器判斷、驗證一致性中等，宜當作需要在自家資料上確認的訊號。
- **傷害分級不宜直接沿用 LLM 標註的盛行率** — 13.2% 與校正後 3.7% 相差三倍以上，臨床人員彼此對傷害等級的一致性也低。若要以 LLM 做高風險提問的篩選或監測，需要先在自家資料上做臨床人員校正。
- **文件工作的資料治理要先到位** — 論文報告文件類請求有 68.9% 針對特定病人，作者在討論中也指出這類用途牽涉受保護健康資訊與病歷規範；部署前應先確認資料流與留存政策，而不是事後補。[(ref: main §2.2, §3 Discussion)](https://arxiv.org/html/2610.11069v1#Sx3)

## References

- `main`：[Clinician use of language models diverges from how the models are evaluated（arXiv HTML v1）](https://arxiv.org/html/2610.11069v1)；本文使用 Abstract、Introduction、§2.1–2.6 Results、§3 Discussion、§4.1–4.12 Methods、Data availability、Code availability、Table 1，以及 Fig. 1、Fig. 2 與 Extended Data Figs. 6–8、Extended Data Tables 1–2 的圖表說明。章節深鏈：[#Sx1](https://arxiv.org/html/2610.11069v1#Sx1)、[#Sx2.SSx1](https://arxiv.org/html/2610.11069v1#Sx2.SSx1)、[#Sx2.SSx2](https://arxiv.org/html/2610.11069v1#Sx2.SSx2)、[#Sx2.SSx3](https://arxiv.org/html/2610.11069v1#Sx2.SSx3)、[#Sx2.SSx4](https://arxiv.org/html/2610.11069v1#Sx2.SSx4)、[#Sx2.SSx5](https://arxiv.org/html/2610.11069v1#Sx2.SSx5)、[#Sx2.SSx6](https://arxiv.org/html/2610.11069v1#Sx2.SSx6)、[#Sx3](https://arxiv.org/html/2610.11069v1#Sx3)、[#Sx4](https://arxiv.org/html/2610.11069v1#Sx4)、[#Sx4.SSx1](https://arxiv.org/html/2610.11069v1#Sx4.SSx1)、[#Sx4.SSx3](https://arxiv.org/html/2610.11069v1#Sx4.SSx3)、[#Sx4.SSx4](https://arxiv.org/html/2610.11069v1#Sx4.SSx4)、[#Sx4.SSx7](https://arxiv.org/html/2610.11069v1#Sx4.SSx7)、[#Sx4.SSx8](https://arxiv.org/html/2610.11069v1#Sx4.SSx8)、[#Sx4.SSx9](https://arxiv.org/html/2610.11069v1#Sx4.SSx9)、[#Sx4.SSx10](https://arxiv.org/html/2610.11069v1#Sx4.SSx10)、[#Sx4.SSx11](https://arxiv.org/html/2610.11069v1#Sx4.SSx11)、[#Sx4.SSx12](https://arxiv.org/html/2610.11069v1#Sx4.SSx12)、[#Sx5](https://arxiv.org/html/2610.11069v1#Sx5)。
- `abs`：[arXiv:2610.11069 摘要頁](https://arxiv.org/abs/2610.11069)。
- `doi`：[10.48550/arXiv.2610.11069](https://doi.org/10.48550/arXiv.2610.11069)（arXiv 標示為待註冊）。
- `code`：[nyuolab/RCQ-Map](https://github.com/nyuolab/RCQ-Map)；[nyuolab/CABA](https://github.com/nyuolab/CABA)（論文列出）。

[Home](../) · [AI Papers](./)
