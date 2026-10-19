---
catalog_id: "doi:10.21203/rs.3.rs-11013237/v1"
editors:
  - "Clare"
refs:
  main:
    title: "Are Large Multimodal Models Ready for Post-Thrombectomy mTICI Assessment? A Comparison with Physicians"
    url: "https://www.researchsquare.com/article/rs-11013237/v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 有手術報告時，GPT-5 的 mTICI 分級追得上醫師；只給 DSA 影像，一致性從 0.87 掉到 0.35：取栓後再灌流分級的多模態模型比較

## 來源

- 團隊：University Hospital Regensburg 與 medbo District Hospital（Regensburg）共 13 位作者，第一作者 Michael Knott，末位作者 Quirin D. Strotzer；論文未標示通訊作者。[(ref: main author list)](https://www.researchsquare.com/article/rs-11013237/v1)
- 論文：*Are Large Multimodal Models Ready for Post-Thrombectomy mTICI Assessment? A Comparison with Physicians*，Research Square 預印本 v1，2026-10-14 上線，標示為投稿 BMC Neurology 審查中、未經同儕審查，授權 CC BY 4.0。[(ref: main)](https://www.researchsquare.com/article/rs-11013237/v1)
- 識別碼：DOI [10.21203/rs.3.rs-11013237/v1](https://doi.org/10.21203/rs.3.rs-11013237/v1)。
- 全文：[Research Square 全文頁](https://www.researchsquare.com/article/rs-11013237/v1)、[PDF](https://www.researchsquare.com/article/rs-11013237/latest.pdf)。
- 資料與程式：作者聲明研究資料皆已包含在論文內；論文未提供程式碼連結。[(ref: main Declarations)](https://www.researchsquare.com/article/rs-11013237/v1)
- 研究性質：單一中心回顧性 reader study，不是 pilot；兩個模型都實際在 90 個病例、三種輸入條件下執行，與四位醫師在相同條件下比較，主要指標附 bootstrap 95% CI。模型只看每個 DSA 序列挑出的一張靜態影格，不看完整序列。[(ref: main Materials and Methods)](https://www.researchsquare.com/article/rs-11013237/v1)
- 證據邊界：本文數值以全文的 Table 1–3 與 Results 正文為準；補充資料（Appendix S1 完整 prompt、逐位讀者的結果表）未納入本文引述。

**編輯：** Clare

作者讓 GPT-5、MedGemma-1.5 與四位醫師分別在「只有手術報告」「只有 DSA 影像」「影像加報告」三種條件下為 90 例前循環取栓手術評 mTICI 再灌流分級：GPT-5 有報告時與醫師的一致性相當（quadratic-weighted kappa 約 0.87），只看影像時降到 0.35，醫師只看影像仍有 0.85，模型的表現幾乎全部來自報告文字。[(ref: main Abstract, Table 1)](https://www.researchsquare.com/article/rs-11013237/v1)

## 流程

![取栓後 mTICI 分級研究設計示意圖。四個圓角方塊由左到右排成一列，彼此以三支實線箭頭依序相連。藍色方塊「1 Cohort and reference」：University Hospital Regensburg、取栓 2011-2023、90 例前循環大血管阻塞；參考標準為兩位神經放射科醫師依所有可得資訊共識判定的 mTICI，六級 0／1／2a／2b／2c／3，成功定義為 mTICI ≥ 2b。綠色方塊「2 Three input conditions」：A. 只有報告（德文手術報告，移除最終 mTICI 分級）；B. 只有影像（4 張 DSA 影格，每個序列 1 張：正位與側位、取栓前與取栓後，移除燒入影像的註記）；C. 影像加報告。橘色方塊「3 Raters (all 3 inputs)」：GPT-5（gpt-5-2025-08-07，Responses API、high-detail 影像）、MedGemma-1.5 4B（本地執行、16-bit、greedy decoding）、兩個模型使用同一個零樣本 prompt（角色設定、mTICI 定義、JSON 輸出）、四位醫師讀者（兩位神經科、兩位放射科，盲判、隨機順序、至少兩週 washout）。紫色方塊「4 Evaluation」：主要指標 quadratic-weighted Cohen's kappa（wk）；次要指標六級完全一致率、mean absolute ordinal error、≥ 2b 的敏感度與特異度；CI 以 1,000 次 bootstrap 或 Wilson 法；輸入敏感度對比、模型與合併讀者的差距、讀者間一致性。](assets/lmm-mtici-study-design.png)

圖：本書庫依論文 Materials and Methods 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖。[(ref: main Materials and Methods)](https://www.researchsquare.com/article/rs-11013237/v1)

## 背景／問題

mTICI（modified Thrombolysis in Cerebral Infarction）是取栓手術後評估血管再灌流程度的標準分級，也是取栓的主要技術終點；作者引用文獻指出，mTICI 的判讀者間一致性只有中等，術者自評傾向高估，後循環與遠端阻塞的可靠度更差。[(ref: main Introduction)](https://www.researchsquare.com/article/rs-11013237/v1)

作者另引用文獻指出，大型多模態模型（large multimodal model，LMM）已被用在結構化報告與從自由文字抽取 mTICI；但模型究竟是從血管攝影「推斷」再灌流，還是只是把報告裡寫好的描述對應到分級，作者認為尚未被檢驗，這一點是作者提出的研究缺口，沒有引用文獻。開場「成功再灌流強烈預測良好預後」「標準化再灌流指標越來越常用於決策與品質保證」兩句，論文也沒有附引用，本文只當成作者的動機陳述。[(ref: main Introduction)](https://www.researchsquare.com/article/rs-11013237/v1)

## 方法摘要

**任務。** 為每一例取栓手術評六級 mTICI（0、1、2a、2b、2c、3），並以 mTICI ≥ 2b 為「成功再灌流」做二分。[(ref: main Materials and Methods)](https://www.researchsquare.com/article/rs-11013237/v1)

**三種輸入條件。** Report only：德文手術報告，移除最終的 mTICI 分級；images only：取栓前後、正位與側位共四個 DSA 序列，每個序列由研究者挑一張最具代表性的靜態影格；images + report：兩者都給。[(ref: main Reference Standard and Data Preparation)](https://www.researchsquare.com/article/rs-11013237/v1)

**評分者。** 兩個模型：GPT-5（gpt-5-2025-08-07）與 MedGemma-1.5（4B，instruction-tuned）；四位醫師讀者：神經科與放射科各兩位，每科一位資深、一位資淺。所有評分者在三種條件下評同一批病例。[(ref: main Model and Physician Assessment)](https://www.researchsquare.com/article/rs-11013237/v1)

**指標。** 主要指標是對參考標準的 quadratic-weighted Cohen's kappa（wκ）；次要指標為六級完全一致率（exact accuracy）、mean absolute ordinal error（MAE，以分級階數計），以及 ≥ 2b 的敏感度與特異度。另外計算兩種輸入敏感度對比：report increment（影像加報告減只有影像）與 imaging increment（影像加報告減只有報告）。[(ref: main Statistical Analysis, Table 2)](https://www.researchsquare.com/article/rs-11013237/v1)

## 方法詳解

**病例與參考標準。** 2011–2023 年在 University Hospital Regensburg 接受取栓的急性大血管阻塞（large vessel occlusion，LVO）連續病例，以申報碼找出；納入前循環阻塞、有取栓前後 DSA 序列與手術報告者，排除後循環阻塞、影像無法評估或缺報告者，最後 90 例。參考標準由兩位神經放射科醫師（19 年與 14 年經驗）依「所有可得資訊」共識判定，與讀者和模型的判讀各自獨立。mTICI 定義引用 Cerebral Angiographic Revascularization Grading Collaborators 的共識與後續 2c 分級文獻。[(ref: main Study Design and Cohort, Reference Standard and Data Preparation)](https://www.researchsquare.com/article/rs-11013237/v1)

**資料準備。** 兩位研究者從每個 DSA 序列挑一張代表性影格並標註時相與投照方向；可能洩漏阻塞位置或結果的燒入註記從像素中移除，但不遮住血管。報告只移除最終 mTICI 分級。[(ref: main Reference Standard and Data Preparation)](https://www.researchsquare.com/article/rs-11013237/v1)

**模型設定。** 兩個模型使用同一個零樣本 prompt：設定為資深神經介入醫師的角色、列出 mTICI 的操作型定義、要求以結構化 JSON 輸出最終分級與自由文字理由；沒有 in-context 範例，也沒有微調。GPT-5 透過 OpenAI Responses API、以 high-detail 模式輸入影像；MedGemma-1.5 在本地以 16-bit、不量化、Hugging Face transformers pipeline 的 greedy decoding 執行。每個模型每例每種條件只跑一次；無法解析的輸出當作缺值，MedGemma-1.5 在影像加報告、只有報告、只有影像三種條件下各有 4、1、11 例無法評分，GPT-5 與讀者沒有缺值。[(ref: main Model and Physician Assessment, General Results)](https://www.researchsquare.com/article/rs-11013237/v1)

**讀者設定。** 讀者看不到參考分級，病例順序隨機，不同條件之間至少間隔兩週 washout。[(ref: main Model and Physician Assessment)](https://www.researchsquare.com/article/rs-11013237/v1)

**統計。** 個別評分者的 wκ 與 MAE 以 1,000 次 case-resampled percentile bootstrap 計算 CI，配對對比保留病例層級的配對；完全一致率、敏感度、特異度用 Wilson 法；讀者合併組用 case-cluster bootstrap。CI 不含 0 的對比才視為有資訊量。[(ref: main Statistical Analysis)](https://www.researchsquare.com/article/rs-11013237/v1)

- **論文未交代** — 四位讀者的年資：Methods 中仍是未填的佔位文字（「CC years」等），參考標準與挑影格的研究者也只以佔位縮寫標示；挑影格的兩位研究者是否屬於參考標準小組也沒有說明。
- **論文未交代** — 參考標準所用的「所有可得資訊」是否包含手術報告；若包含，只有報告條件下的一致性可能部分來自共用資訊。報告除了移除最終分級之外，是否還保留了描述殘餘阻塞或再灌流程度的文字，也沒有逐例說明。
- **論文未交代** — GPT-5 的 reasoning effort 與取樣設定、模型查詢日期、送入模型的影像解析度與格式；完整 prompt 只在補充資料 Appendix S1。
- **論文未交代** — 篩檢與排除的病例數（流程圖只有圖檔）、病人年齡與性別；每例只跑一次，沒有重複執行的穩定性。

## 資料與實驗

下表整理論文 General Results 報告的病例組成與參考標準分布（n = 90）。[(ref: main General Results)](https://www.researchsquare.com/article/rs-11013237/v1)

| 項目 | 類別 | n (%) |
|---|---|---|
| 阻塞側 | 左 | 48 (53.3%) |
| 阻塞側 | 右 | 42 (46.7%) |
| 阻塞位置 | M1 | 48 (53.3%) |
| 阻塞位置 | ICA | 28 (31.1%) |
| 阻塞位置 | M2 | 13 (14.4%) |
| 阻塞位置 | M3 | 1 (1.1%) |
| 參考 mTICI | 3 | 40 (44.4%) |
| 參考 mTICI | 2c | 18 (20.0%) |
| 參考 mTICI | 2b | 16 (17.8%) |
| 參考 mTICI | 2a | 9 (10.0%) |
| 參考 mTICI | 1 | 4 (4.4%) |
| 參考 mTICI | 0 | 3 (3.3%) |
| 成功再灌流（≥ 2b） | — | 74 (82.2%) |

下表摘錄論文 Table 1，括號內為 95% CI；n 為有參考標準且有可評分輸出的評分次數（病例數 × 讀者數），MAE 以分級階數計，敏感度與特異度以 mTICI ≥ 2b 為陽性。[(ref: main Table 1)](https://www.researchsquare.com/article/rs-11013237/v1)

| 評分者 | 輸入 | n | wκ | Exact acc. (%) | MAE | Sens. (%) | Spec. (%) |
|---|---|---|---|---|---|---|---|
| GPT-5 | Report only | 90 | 0.864 (0.781–0.919) | 66.7 (56.4–75.5) | 0.41 (0.28–0.54) | 98.6 (92.7–99.8) | 81.2 (57.0–93.4) |
| GPT-5 | Images only | 90 | 0.345 (0.082–0.555) | 44.4 (34.6–54.7) | 1.01 (0.79–1.23) | 100.0 (95.1–100.0) | 18.8 (6.6–43.0) |
| GPT-5 | Images + report | 90 | 0.868 (0.781–0.921) | 67.8 (57.6–76.5) | 0.39 (0.27–0.51) | 100.0 (95.1–100.0) | 62.5 (38.6–81.5) |
| MedGemma-1.5 | Report only | 89 | 0.336 (0.162–0.527) | 47.2 (37.2–57.5) | 0.87 (0.66–1.08) | 98.6 (92.6–99.8) | 6.2 (1.1–28.3) |
| MedGemma-1.5 | Images only | 79 | 0.017 (−0.087–0.107) | 24.1 (16.0–34.5) | 1.10 (0.87–1.33) | 100.0 (94.3–100.0) | 0.0 (0.0–20.4) |
| MedGemma-1.5 | Images + report | 86 | 0.337 (0.176–0.512) | 47.7 (37.4–58.1) | 0.94 (0.72–1.19) | 97.1 (90.2–99.2) | 6.2 (1.1–28.3) |
| Neurologists | Report only | 180 | 0.843 (0.766–0.893) | 63.9 (56.1–71.7) | 0.44 (0.34–0.54) | 98.0 (95.5–100.0) | 68.8 (47.2–88.5) |
| Neurologists | Images only | 180 | 0.842 (0.753–0.902) | 63.3 (55.0–71.7) | 0.44 (0.33–0.54) | 95.9 (92.0–99.3) | 71.9 (50.0–90.6) |
| Neurologists | Images + report | 180 | 0.841 (0.757–0.894) | 56.1 (47.8–64.4) | 0.50 (0.39–0.60) | 95.9 (92.4–99.3) | 71.9 (50.0–90.6) |
| Radiologists | Report only | 180 | 0.901 (0.852–0.935) | 71.7 (65.0–78.9) | 0.33 (0.24–0.42) | 97.3 (94.5–99.4) | 81.2 (65.4–94.5) |
| Radiologists | Images only | 180 | 0.865 (0.795–0.913) | 62.8 (54.4–70.6) | 0.43 (0.33–0.54) | 95.3 (91.3–98.7) | 81.2 (62.5–96.7) |
| Radiologists | Images + report | 180 | 0.902 (0.846–0.937) | 68.9 (61.7–76.1) | 0.34 (0.26–0.42) | 95.9 (93.0–98.7) | 81.2 (62.5–97.1) |
| All readers | Report only | 360 | 0.873 (0.812–0.911) | 67.8 (61.1–74.4) | 0.39 (0.30–0.47) | 97.6 (95.6–99.3) | 75.0 (57.8–90.6) |
| All readers | Images only | 360 | 0.854 (0.783–0.903) | 63.1 (56.1–70.0) | 0.44 (0.35–0.53) | 95.6 (92.8–98.1) | 76.6 (57.7–93.2) |
| All readers | Images + report | 360 | 0.872 (0.808–0.911) | 62.5 (55.8–69.7) | 0.42 (0.34–0.49) | 95.9 (93.2–98.4) | 76.6 (57.8–93.2) |

下表摘錄論文 Table 2 的輸入敏感度對比（wκ 的變化，括號內為 95% CI）。Report increment ＝ 影像加報告減只有影像；imaging increment ＝ 影像加報告減只有報告。[(ref: main Table 2)](https://www.researchsquare.com/article/rs-11013237/v1)

| 評分者 | Report increment Δwκ | Imaging increment Δwκ |
|---|---|---|
| GPT-5 | +0.522 (0.325–0.753) | +0.004 (−0.053–0.056) |
| MedGemma-1.5 | +0.329 (0.137–0.540) | +0.011 (−0.095–0.126) |
| Neurologists | 0.000 (−0.033–0.032) | −0.002 (−0.053–0.050) |
| Radiologists | +0.037 (0.010–0.069) | +0.001 (−0.027–0.029) |
| All readers | +0.018 (−0.004–0.042) | −0.001 (−0.032–0.028) |

## 結果

- **有報告時 GPT-5 與醫師相當** — GPT-5 的 wκ 在只有報告與影像加報告時為 0.864 與 0.868，合併讀者為 0.873 與 0.872；配對差距（GPT-5 減合併讀者）為 −0.01（−0.06–0.04）與 0.00（−0.05–0.04）。[(ref: main Table 1, Model-Versus-Reader Comparison)](https://www.researchsquare.com/article/rs-11013237/v1)
- **只看影像時 GPT-5 大幅落後** — wκ 0.345，合併讀者 0.854，配對差距 −0.51（−0.74 至 −0.31）；六級完全一致率 44.4%，MAE 1.01 級。[(ref: main Table 1, Model-Versus-Reader Comparison)](https://www.researchsquare.com/article/rs-11013237/v1)
- **模型的分數來自報告，不是影像** — 給影像之後再加報告，GPT-5 的 wκ 多 +0.522、MedGemma-1.5 多 +0.329；給報告之後再加影像，兩個模型的變化都與 0 無法區分（+0.004、+0.011）。讀者的兩種對比都很小，唯一 CI 不含 0 的是放射科讀者的 report increment（+0.037）。[(ref: main Table 2, Input Sensitivity)](https://www.researchsquare.com/article/rs-11013237/v1)
- **偏向判「成功」** — 各評分者的敏感度大多在 95% 以上；GPT-5 的特異度在只有報告時為 81.2%、只有影像時 18.8%、影像加報告時 62.5%，MedGemma-1.5 的特異度在三種條件下為 0.0%–6.2%。陰性（< 2b）病例只有 16 例，特異度的 CI 很寬。[(ref: main Table 1, Agreement)](https://www.researchsquare.com/article/rs-11013237/v1)
- **MedGemma-1.5 在所有條件下都落後** — wκ 0.336、0.017、0.337，與合併讀者的配對差距為 −0.54、−0.84、−0.53，CI 皆不含 0。[(ref: main Table 1, Model-Versus-Reader Comparison)](https://www.researchsquare.com/article/rs-11013237/v1)
- **讀者之間的一致性** — 四位讀者兩兩 wκ 的平均為 0.84–0.86，放射科讀者對（0.85–0.89）高於神經科讀者對（0.78–0.82）；六級分級四人完全一致的比例只有 33.3%–38.9%。[(ref: main Table 3, Inter-Reader Agreement)](https://www.researchsquare.com/article/rs-11013237/v1)

## 限制

**作者自述的限制。** 樣本與讀者數有限，分級分布偏斜、陰性病例只有 16 例，敏感度與特異度的估計不精確；單一中心、在地的報告與手術流程，加上德文報告，可推廣性不確定，德文也可能拖累 MedGemma-1.5；只測了少數模型，模型更新很快，結果不一定適用於現在或未來的版本；影像評估用的是靜態截圖而不是完整 DSA 序列，可能低估模型表現，但作者也指出讀者用同樣的靜態影像仍能準確分級。[(ref: main Discussion)](https://www.researchsquare.com/article/rs-11013237/v1)

**本書庫的觀察。**

- **「報告在就追得上醫師」測的主要是讀報告** — Table 2 顯示 GPT-5 加入影像後一致性沒有變化，作者在 Discussion 也推測報告常直接描述殘餘阻塞、遠端分支充盈與再灌流範圍，模型可能是把這些文字對應到分級。換句話說，有報告條件下的 0.87 比較接近「從手術報告抽取 mTICI」的表現，不能解讀為模型讀懂了血管攝影。
- **參考標準與報告的關係沒有說明** — 參考標準依「所有可得資訊」判定；若其中包含同一份手術報告，模型與參考標準共用資訊來源，有報告條件下的一致性可能偏高。論文沒有交代，也沒有在參考標準只看影像的情況下重算。
- **GPT-5 只看影像時幾乎全判成功** — 依 Table 1 的特異度 18.8% 與 16 例陰性回推（本書庫計算，非論文數值），16 例未達 2b 的病例中約 13 例被判為成功；加上影像後的特異度（62.5%，約 10/16）也低於只有報告時（81.2%，約 13/16）。陰性病例少、CI 重疊，這只是值得追查的方向，不是論文檢定過的結論。
- **「上下限」的說法缺乏支撐** — 作者在 Discussion 說 GPT-5 與 MedGemma-1.5 大概代表表現範圍的上下兩端，但研究只測了兩個模型，這句話無法從結果推出。摘要的「可達醫師水準」也只建立在 GPT-5 一個模型、且有報告的條件上。
- **讀者年資未填** — 讀者經驗直接影響「醫師水準」這個比較基準的意義，而 Methods 的年資仍是佔位文字；合併讀者的數字可以引用，但「資深／資淺」的對照目前無法解讀。

## 與書庫其他文章的關係

ModaLens 以交換影像量測有報告可讀時醫療 VLM 是否仍看影像，主要模型是 MedGemma-27B、也在 MedGemma-4B 上重現；本篇用 report increment 與 imaging increment 在血管攝影的 mTICI 分級上得到同一個方向的答案：報告在時，加影像幾乎不改變模型的一致性: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎？](2026-09-17-modalens-image-sensitivity.md)

OCT 稽核把模型自己寫出的理由固定住再替換影像，量影像對治療決策的直接貢獻；本篇以三種輸入條件與醫師讀者的同條件對照拆出同一件事，兩篇都顯示端到端分數高不代表影像有出力: [抽掉影像、留下理由：VLM 在 anti-VEGF 治療決策裡，OCT 到底出了多少力？](2026-09-23-vlm-oct-image-dependence-audit.md)

## 實務的啟發

- **可借用的量測方法** — 評估多模態模型時，像本篇一樣同時跑「只有文字」「只有影像」「兩者都有」三種條件，並讓醫師讀者在相同條件下評分，再報告 report increment 與 imaging increment。只報影像加報告的單一分數，會把「讀報告」與「讀影像」的能力混在一起。
- **可借用的報告方式** — 對偏斜的分級資料，除了 wκ 之外同時列出 ≥ 2b 的特異度與陰性病例數。本篇 GPT-5 在有報告時 wκ 與醫師相當，但只看影像時特異度只有 18.8%，這種「傾向判成功」的失效模式只看 wκ 看不出來。
- **待驗證的警訊** — 若要用模型從手術報告抽取 mTICI 做品質管理或研究資料整理，本篇的結果支持這個方向值得在地驗證，但前提是報告本身已寫出再灌流描述；作者引用文獻指出術者報告本身傾向高估 mTICI，模型會一起繼承這個偏差。
- **證據強度** — 單一中心、90 例、16 例陰性、兩個模型、靜態影格的回顧性預印本，且讀者年資與參考標準的資訊來源未交代；它支持「目前這兩個模型的 mTICI 表現主要來自報告文字」，不足以支持任何只依 DSA 影像的自動分級用途。

## References

- **main** — Knott M, Napodano G, Noeva E, Zhang L, et al. *Are Large Multimodal Models Ready for Post-Thrombectomy mTICI Assessment? A Comparison with Physicians*. Research Square preprint v1, 2026. DOI: 10.21203/rs.3.rs-11013237/v1. 全文頁：<https://www.researchsquare.com/article/rs-11013237/v1>。文內引用位置：author list、Abstract、Introduction、Materials and Methods（Study Design and Cohort、Reference Standard and Data Preparation、Model and Physician Assessment、Statistical Analysis）、Results（General Results、Agreement、Input Sensitivity、Model-Versus-Reader Comparison、Inter-Reader Agreement）、Discussion、Declarations、Table 1、Table 2、Table 3。
- **pdf** — PDF 版：<https://www.researchsquare.com/article/rs-11013237/latest.pdf>。
- **doi** — <https://doi.org/10.21203/rs.3.rs-11013237/v1>。

[Home](../) · [AI Papers](./)
