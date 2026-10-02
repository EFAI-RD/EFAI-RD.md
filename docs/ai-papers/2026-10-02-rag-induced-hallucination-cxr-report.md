---
catalog_id: "arxiv:2609.31733"
editors:
  - "Clare"
refs:
  main:
    title: "When Retrieval Hurts: Measuring and Explaining Retrieval-Induced Hallucination in Chest X-ray Report Generation"
    url: "https://arxiv.org/html/2609.31733v1"
status: published
skill_version: "write-ai-paper@2.8"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 檢索來的前例報告，是證據還是抄本？胸片報告生成的 retrieval-induced hallucination

## 來源

- 團隊：University of Lagos、NITHUB（University of Lagos）、Machine Learning Collective、Ahmadu Bello University 與 Federal University of Agriculture, Abeokuta（FUNAAB）；共 4 位作者：Emmanuel Idoko、Abdusshakur Olabisi、Shiloh Oni、Adesola Josiah。[(ref: main)](https://arxiv.org/html/2609.31733v1)
- 論文：*When Retrieval Hurts: Measuring and Explaining Retrieval-Induced Hallucination in Chest X-ray Report Generation*，arXiv v1，2026。[(ref: abstract)](https://arxiv.org/abs/2609.31733)
- 識別碼：[arXiv:2609.31733](https://arxiv.org/abs/2609.31733)；[DOI: 10.48550/arXiv.2609.31733](https://doi.org/10.48550/arXiv.2609.31733)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2609.31733v1)。
- 證據邊界：本文依 arXiv v1 全文第 1 至 8 節與 Table 1–3 撰寫；arXiv 頁面註記全文含 4 張表，HTML 版呈現 3 張，本文只引用這 3 張。HTML 版沒有論文圖，本文的流程圖為本書庫自繪。

**編輯：** Clare

這篇論文用 100 筆 MIMIC-CXR 檢查證明，把「相似前例的報告」塞進胸片報告生成的 prompt，會讓 clinical F1 翻倍，也會讓模型把別的病人的發現、甚至整段原文抄進報告，而且檢索相似度預測不了哪一次會出事。[(ref: main Abstract)](https://arxiv.org/html/2609.31733v1#abstract1)

## 流程

![目標胸片與 400 筆檢索池經 BioMedCLIP 取前三名相似檢查，分成無檢索、prompt 檢索與病理相反的 mismatch 檢索三種條件餵給凍結的 LLaVA-1.5-7B，生成報告再以 CheXbert 標註，計算 retrieval-induced hallucination、偶然重疊基準率、逐字抄寫片段與 gating 模擬](assets/rag-induced-hallucination-cxr-report.png)

圖：本書庫依論文第 3.2、4、5 節繪製的編輯示意圖，不含成效數值。左側是檢索設定，中間是三種生成條件，下方是評估與 gating 分析；論文提出的 Retrieval-Guided Cross-Attention（RGCA）模組並未實作，因此不在圖中。[(ref: main §3.2)](https://arxiv.org/html/2609.31733v1#S3.SS2) [(ref: main §4)](https://arxiv.org/html/2609.31733v1#S4) [(ref: main §5)](https://arxiv.org/html/2609.31733v1#S5)

## 背景／問題

Retrieval-augmented generation（RAG）是讓通用 vision-language model（VLM）寫胸片報告的常見捷徑：把目標影像嵌入向量空間，取回 top-k 相似的過去檢查，再把它們的報告放進 prompt，補上通用模型缺乏的臨床脈絡。[(ref: main §1)](https://arxiv.org/html/2609.31733v1#S1)

作者指出這個機制本身就是風險來源：檢索來的報告可能提到目標影像上根本沒有的發現，模型照樣寫進輸出。論文把這種情況稱為 retrieval-induced hallucination（RIH），定義為「出現在生成報告、也出現在至少一份檢索報告、但不在目標參考報告中」的臨床發現；它比一般的 hallucination 窄，也正因為窄才能量測。[(ref: main §1)](https://arxiv.org/html/2609.31733v1#S1) [(ref: main §3.1)](https://arxiv.org/html/2609.31733v1#S3.SS1)

作者自述的貢獻有三：用一個能排除偶然重疊的對照來量測 RIH、在檢索器的嵌入幾何中找出成因，以及推導任何 relevance gate 必須滿足的經驗限制。原本要建的 RGCA 模組只給出規格，作者明言不主張它有效。[(ref: main §1)](https://arxiv.org/html/2609.31733v1#S1)

## 方法摘要

研究從 MIMIC-CXR／MIMIC-CXR-JPG 取 500 筆檢查，切成 400 筆檢索池與 100 筆評估集，以病人為單位分割、只用正面 PA／AP 影像。檢索用 BioMedCLIP 的影像嵌入取前三名相似檢查，生成器是凍結的 LLaVA-1.5-7B。[(ref: main §4.1)](https://arxiv.org/html/2609.31733v1#S4.SS1) [(ref: main §4.2)](https://arxiv.org/html/2609.31733v1#S4.SS2) [(ref: main §4.3)](https://arxiv.org/html/2609.31733v1#S4.SS3)

每筆評估檢查在三種條件下各生成一份報告：只給影像的 no retrieval、額外附上 top-3 檢索報告的 prompt retrieval，以及刻意附上病理相反報告的 mismatch retrieval。生成、參考與檢索三方的報告都用 CheXbert 標成 14 個 CheXpert 類別後比較。[(ref: main §3.2)](https://arxiv.org/html/2609.31733v1#S3.SS2) [(ref: main §4.3)](https://arxiv.org/html/2609.31733v1#S4.SS3)

在主結果之外，論文再做四件事：用沒看過檢索內容的 image-only 報告計算偶然重疊的基準率；在字串層級找逐字抄寫；檢查檢索相似度能否預測傷害；以及模擬不同 gating 訊號對「留下多少無依據內容」與「保留多少有用內容」的取捨。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2) [(ref: main §5.3)](https://arxiv.org/html/2609.31733v1#S5.SS3) [(ref: main §5.4)](https://arxiv.org/html/2609.31733v1#S5.SS4)

## 方法詳解

**問題定義** — 目標影像 x、參考報告 y_ref、檢索報告集 R(x) = {r_1,…,r_k}；某個臨床發現 p 同時出現在生成報告 y_gen 與至少一份 r_i 中、卻不在 y_ref 中，就記為一次 RIH。[(ref: main §3.1)](https://arxiv.org/html/2609.31733v1#S3.SS1)

**檢索索引** — 索引以檢查為單位，每筆存 study ID、影像路徑、報告全文、findings、impression、標籤與 split；以影像—文字嵌入相似度取回相似檢查，再把它們的報告交給生成器。[(ref: main §4.1)](https://arxiv.org/html/2609.31733v1#S4.SS1)

**資料切分與防洩漏** — 400 筆檢索池與 100 筆評估集以病人為單位分開，論文寫兩者分別涵蓋 99 位與 27 位受試者、彼此不重疊；目標不會檢索到自己或同一病人的其他檢查。種子固定，子集以 SHA-256 做內容定址，作者表示獨立的本地重跑與雲端執行取回的鄰居完全一致。[(ref: main §4.2)](https://arxiv.org/html/2609.31733v1#S4.SS2)

**生成與算力** — 生成器為 llava-hf/llava-1.5-7b-hf，最多 192 個新 token；100 筆 × 3 種條件共 300 份報告，在一張 NVIDIA T4 上約 20 至 40 分鐘。BioMedCLIP 嵌入與索引建立在筆電 GPU 上不到十分鐘，CheXbert 標註在 CPU 上數分鐘完成。[(ref: main §4.2)](https://arxiv.org/html/2609.31733v1#S4.SS2) [(ref: main §4.3)](https://arxiv.org/html/2609.31733v1#S4.SS3)

**標註方式** — 三方報告都用同一個 CheXbert 標註，處理否定語句；只有 CheXbert 判為 positive 才算有該發現，uncertain 一律視為 negative。作者說明改用同一模型的原因：先前的規則式標註器在生成端與參考端用不同詞彙，例如生成的「pulmonary edema」永遠對不上參考端的「Edema」，會被一律算成 hallucination。作者也承認自動標註無法裁定個案，個案仍以人工審閱為準。[(ref: main §4.3)](https://arxiv.org/html/2609.31733v1#S4.SS3)

**偶然重疊對照（coincidental-overlap control）** — 拿 no retrieval 條件下的報告，去比對它「本來會拿到、但實際沒看到」的檢索證據，算出純屬巧合的重疊率，作為 RIH 的基準線。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)

**逐字抄寫量測** — 在字串層級比對生成報告與檢索報告，計算含有一段「出現在檢索證據中、卻不在參考報告中」的 8 字（eight-word）連續片段的報告比例。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)

**RGCA（僅規格）** — 以目標影像嵌入與檢索報告嵌入的 cosine 相似度 α_k 加上兩者表示，經 sigmoid gate g_k 決定每份檢索報告對視覺 cross-attention 的影響程度；影像 token 當 query、檢索報告 token 當 gated key／value，再以 LayerNorm 殘差融回視覺流。作者在第 5.3 節自己否定了以 α_k 為核心的設計，表示實作前必須修改。[(ref: main §3.3)](https://arxiv.org/html/2609.31733v1#S3.SS3)

**Gating 模擬** — 在已取回的證據集上模擬不同篩選訊號，逐筆計算留下的證據含多少參考報告沒有的發現（Unsup.）、保留多少參考報告的發現（Coverage），以及正常參考報告中有幾筆完全沒有異常證據留下（Normal protected）。其中 label agreement 使用真實標籤，是 oracle。[(ref: main §5.4)](https://arxiv.org/html/2609.31733v1#S5.SS4)

## 資料與實驗

下表整理論文使用的資料與元件。[(ref: main §4.1)](https://arxiv.org/html/2609.31733v1#S4.SS1) [(ref: main §4.2)](https://arxiv.org/html/2609.31733v1#S4.SS2) [(ref: main §4.3)](https://arxiv.org/html/2609.31733v1#S4.SS3)

| 項目 | 角色 | 內容（論文所述） |
|---|---|---|
| MIMIC-CXR／MIMIC-CXR-JPG 子集 | 研究資料（PhysioNet 認證取用） | 500 筆檢查，正面 PA／AP、每筆一張影像 |
| 檢索池 | 被檢索的前例報告 | 400 筆檢查，論文寫涵蓋 99 位受試者 |
| 評估集 | 生成與評分對象 | 100 筆檢查，論文寫涵蓋 27 位受試者；與檢索池病人不重疊 |
| BioMedCLIP | 影像嵌入與 top-3 檢索 | 相似度只用影像端 |
| llava-hf/llava-1.5-7b-hf | 報告生成器（凍結） | 三種條件 × 100 筆 = 300 份報告 |
| CheXbert | 生成、參考、檢索三方報告的標註 | 14 個 CheXpert 類別；uncertain 視為 negative |
| 20 筆 pilot | 早期預試 | 用於比較 clinical F1 倍率的穩定性 |

下表重製論文 Table 1：BioMedCLIP top-3 在 100 筆評估檢查上的檢索品質。[(ref: main Table 1)](https://arxiv.org/html/2609.31733v1#S5.T1)

| Metric | Retrieval | Mismatch |
|---|---|---|
| Label Jaccard@3 | 0.267 | 0.050 |
| Label precision@3 | 0.272 | 0.000 |
| Label recall@3 (abnormal targets) | 0.604 | 0.000 |
| ≥1 shared pathology | 0.55 | 0.00 |
| Normal target → normal neighbours | 4/28 | 5/28 |
| Abnormal target → ≥1 match | 55/72 | 0/72 |

下表重製論文 Table 2：三種檢索條件下的生成結果（CheXbert 標註，各 n = 100）。Hall. 為 hallucination 率，RIH 為 retrieval-induced hallucination 率，Copy 為生成報告與檢索證據共有任一發現的比例。[(ref: main Table 2)](https://arxiv.org/html/2609.31733v1#S5.T2)

| Condition | n | Hall. | RIH | Copy | Omission | Clinical F1 |
|---|---|---|---|---|---|---|
| No Retrieval | 100 | 0.32 | 0.00 | 0.00 | 0.80 | 0.201 |
| Prompt Retrieval | 100 | 0.80 | 0.76 | 0.91 | 0.74 | 0.402 |
| Mismatch Retrieval | 100 | 0.98 | 0.98 | 1.00 | 0.78 | 0.043 |

下表重製論文 Table 3：100 筆檢查上的 gating 訊號比較。Kept 為平均保留報告數；Unsup. 為留下的證據中、參考報告沒有的平均發現數；Coverage 為保留的參考發現平均比例；Normal protected 為正常參考報告中、沒有任何異常證據留下的筆數。Label agreement 列使用真實標籤（oracle）。[(ref: main Table 3)](https://arxiv.org/html/2609.31733v1#S5.T3)

| Gating signal | Kept | Unsup. | Coverage | Normal protected |
|---|---|---|---|---|
| No gate (k = 3) | 3.00 | 2.18 | 0.60 | 4/28 |
| Cosine similarity, top-1 | 1.00 | 0.99 | 0.33 | 13/28 |
| Label agreement, J ≥ 0.2 | 1.42 | 0.84 | 0.60 | 28/28 |
| Label agreement, J ≥ 0.4 | 0.92 | 0.35 | 0.47 | 28/28 |
| Label agreement, L_k ⊆ T | 1.28 | 0.00 | 0.27 | 28/28 |

## 結果

- **檢索器不是亂抓，但對正常片特別失準** — 檢索結果與目標共享至少一種病理的比例為 55%，涵蓋目標病理的 60%，precision 只有 0.272。異常目標中 55／72 筆找到相符病理；28 筆沒有任何病理標籤的正常目標，只有 4 筆取回全是正常的鄰居，也就是 24／28 筆正常胸片至少帶回一份異常前例。[(ref: main §5.1)](https://arxiv.org/html/2609.31733v1#S5.SS1) [(ref: main Table 1)](https://arxiv.org/html/2609.31733v1#S5.T1)
- **作者對成因的解釋** — 醫療影像嵌入的相似度主要由解剖結構與攝影條件決定，而不是有沒有病灶，所以正常檢查經常配上異常報告；作者認為這正是不需任何對抗設計、RIH 就會自然出現的原因。[(ref: main §5.1)](https://arxiv.org/html/2609.31733v1#S5.SS1)
- **Clinical F1 翻倍，hallucination 率也大幅上升** — prompt retrieval 讓 clinical F1 從 0.201 升到 0.402，mismatch 則跌到 0.043；同時 hallucination 率從 0.32 升到 0.80 與 0.98，RIH 從 0.00 升到 0.76 與 0.98。作者補充，20 筆 pilot 的 F1 倍率為 1.97 倍、本次 100 筆為 2.00 倍。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2) [(ref: main Table 2)](https://arxiv.org/html/2609.31733v1#S5.T2)
- **不是證據集太大造成的巧合** — 偶然重疊的基準率在兩種證據集上都是 0.18，相對於觀察到的 RIH 0.76 與 0.98，可歸因的超額分別為 +0.58 與 +0.80，約為基準的四到五倍。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)
- **逐筆層級的雙向效果** — 100 筆中有 67 筆是 image-only 沒有無依據發現、mismatch 卻出現；另有 55 筆是檢索幫忙找回 image-only 漏掉、且參考報告支持的發現。論文舉的 study 51856263 參考報告無病理，image-only 正確地沒寫任何發現，prompt retrieval 卻寫出只存在於證據中的 lung lesion，mismatch 則引入六個無依據發現。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)
- **模型在抄字，而不只是吸收發現** — prompt retrieval 下 95% 的報告含有一段出現在檢索證據、卻不在參考報告中的 8 字連續片段，mismatch 下為 100%；最長逐字片段的中位數為 17 字、最長 70 字，image-only 報告則一份都沒有。作者列出的例子包括 PICC 導管尖端位置、先前 CT 所見的甲狀腺腫，以及「右乳缺如」這類專屬某位病人的器材、共病與手術史。[(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)
- **相似度預測不了傷害** — 有發生 RIH 的檢查 top-1 相似度平均 0.9439，沒發生的為 0.9413，差距方向相反；依相似度四分位切分，RIH 率由低到高為 0.80、0.80、0.60、0.84，沒有單調趨勢，最相似的四分位反而最有害之一。作者歸因於範圍壓縮：BioMedCLIP 的 top-1 相似度全落在 0.860 到 0.979 之間。[(ref: main §5.3)](https://arxiv.org/html/2609.31733v1#S5.SS3)
- **以病理一致性篩選，可去掉六成無依據內容而不損 coverage** — 在約保留一份報告的相同選擇性下，cosine top-1 留下 0.99 個無依據發現、coverage 0.33；label agreement J ≥ 0.4 保留更少（0.92 份），無依據發現只剩 0.35、coverage 反而較高（0.47）。J ≥ 0.2 把無依據發現從 2.18 降到 0.84（減少 61%），coverage 維持 0.60。[(ref: main §5.4)](https://arxiv.org/html/2609.31733v1#S5.SS4) [(ref: main Table 3)](https://arxiv.org/html/2609.31733v1#S5.T3)
- **但最好的 gate 目前不存在** — 作者明說 label agreement 是 oracle，用的是推論時拿不到的真實標籤，Unsup. 欄也有部分是定義使然；改用模型自己的 image-only 報告推估病理時，coverage 掉到 0.16，因此需要另一個專用的胸片分類器，這是 RGCA 的下一步。[(ref: main §5.4)](https://arxiv.org/html/2609.31733v1#S5.SS4)

## 限制

- **規模（作者自述）** — 這是 pilot 而非正式 benchmark：評估集 100 筆、檢索池 400 筆，檢索池小，檢索品質可能比全量索引悲觀。[(ref: main §6)](https://arxiv.org/html/2609.31733v1#S6)
- **生成器（作者自述）** — 使用通用 LLaVA checkpoint，不是放射科專用報告生成器；所有條件的 omission 率都在 0.74 至 0.80，結論關於「通用 VLM 如何整合檢索證據」，不代表自動報告可達的品質。[(ref: main §6)](https://arxiv.org/html/2609.31733v1#S6)
- **指標歸因（作者自述）** — RIH 率無法區分「從證據抄來」與「自己生成、碰巧也出現在證據中」；偶然重疊對照只能在群體層級設限，個案仍需人工審閱。[(ref: main §6)](https://arxiv.org/html/2609.31733v1#S6)
- **RGCA 未實作（作者自述）** — 以相似度為 gate 的設計在 n = 100 下是負面結果，RGCA 只有規格，作者不主張它能降低 hallucination。[(ref: main §6)](https://arxiv.org/html/2609.31733v1#S6)
- **本書庫補充：有效樣本可能比 100 小** — 論文寫評估集 100 筆檢查只來自 27 位受試者，同一病人的多筆檢查並非獨立樣本；正文與表格都沒有信賴區間，0.80／0.80／0.60／0.84 這類四分位比較，每格只有約 25 筆。[(ref: main §4.2)](https://arxiv.org/html/2609.31733v1#S4.SS2) [(ref: main §5.3)](https://arxiv.org/html/2609.31733v1#S5.SS3)
- **本書庫補充：一處數字前後不一** — Table 2 中 no retrieval 的 omission 率為 0.80，第 5.4 節說明 image-only 報告不適合當 gate 時寫的是 0.86；本文以 Table 2 為準，引用第 5.4 節時保留原文數字。[(ref: main Table 2)](https://arxiv.org/html/2609.31733v1#S5.T2) [(ref: main §5.4)](https://arxiv.org/html/2609.31733v1#S5.SS4)
- **本書庫補充：「翻倍」的起點很低** — prompt retrieval 下 clinical F1 為 0.402，仍屬偏低；而 mismatch 條件是刻意構造的病理相反證據，代表最壞情況，不是一般部署會遇到的檢索結果。真正與部署相關的是 prompt retrieval 那一列的 RIH 0.76。[(ref: main Table 2)](https://arxiv.org/html/2609.31733v1#S5.T2)
- **本書庫補充：只用 CheXbert 的 14 類** — 器材位置、手術史等不在 14 類中的內容，只由逐字抄寫分析間接捕捉；label-level 的 RIH 可能低估了這類病人專屬內容的轉移。[(ref: main §4.3)](https://arxiv.org/html/2609.31733v1#S4.SS3) [(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)

## 與書庫其他文章的關係

MAIRA-2 把前次影像與前次報告當作生成輸入、並以 grounding 與事實層級評分約束輸出，本篇則顯示當附上的是「別人的」前例報告且沒有這類約束時，模型會把對方的發現與文字直接帶進報告: [MAIRA-2：胸腔 X 光報告的文字正確，定位也正確嗎？](2026-09-15-maira-2-grounded-reporting.md)

ModaLens 問「有報告可讀時，醫療 VLM 還看不看影像」，本篇給出同一問題在 RAG 情境下的答案：檢索報告一進 prompt，生成內容的來源就大幅從影像轉向文字: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎？](2026-09-17-modalens-image-sensitivity.md)

RadVLM 的分節評估顯示流暢的報告不等於臨床忠實，本篇的逐字抄寫分析則指出一種特別難從流暢度察覺的失真：句子本身是真實放射科醫師寫的，只是屬於另一位病人: [報告讀起來很順，就代表寫對了嗎？RadVLM 的分節評估](2026-09-22-radvlm-section-based-report-evaluation.md)

## 實務的啟發

第一，評估任何 RAG 式報告生成，都該同時跑「檢索失敗」的情境，而不只看檢索成功時的分數。本研究最有參考價值的設計，是把 no retrieval、正常檢索與刻意錯配三種條件並排，再加上偶然重疊基準率；院內若要導入以前例報告輔助寫報告的工具，可以直接沿用這個三條件對照做驗收。

第二，不要用嵌入相似度當安全閥。論文中相似度只分布在 0.86 至 0.98 的窄帶，且與傷害無單調關係；本書庫的解讀是，「只在相似度夠高時才附上前例」這類直覺規則，在影像嵌入上可能沒有任何保護作用，篩選條件需要改成病理層級的一致性，而那需要一個獨立、可驗證的分類器。

第三，逐字抄寫是便宜又有效的稽核訊號。8 字連續片段比對不需要標註，論文中 image-only 報告為 0%、檢索條件下為 95% 以上；在上線監控中定期抽查生成報告與檢索來源的 n-gram 重疊，可以早期發現模型是否把前例報告當作範本照抄。

第四，檢索語料本身就是臨床基礎設施。作者指出正常片在小型語料中幾乎都會配到異常前例，而小型語料正是資源受限場域最可能使用的；報告中也出現另一位病人的器材、共病與手術史 [(ref: main §7)](https://arxiv.org/html/2609.31733v1#S7) [(ref: main §5.2)](https://arxiv.org/html/2609.31733v1#S5.SS2)。本書庫認為，這除了是正確性問題，也牽涉跨病人資訊外流，建置檢索語料時應同時考慮正常與異常的比例，以及報告中可識別病人特徵的處理方式。

這項研究的證據停留在 100 筆檢查、單一通用生成器與自動標註，不能推論為特定臨床系統的實際錯誤率；它的價值在於提供了一套可以複製的量測方法，以及一個清楚的負面結果。

## References

- `main`：[When Retrieval Hurts: Measuring and Explaining Retrieval-Induced Hallucination in Chest X-ray Report Generation，arXiv HTML v1](https://arxiv.org/html/2609.31733v1)；本文使用 [Abstract](https://arxiv.org/html/2609.31733v1#abstract1)、[§1 Introduction](https://arxiv.org/html/2609.31733v1#S1)、[§3.1 Problem Definition](https://arxiv.org/html/2609.31733v1#S3.SS1)、[§3.2 Baseline Pipeline](https://arxiv.org/html/2609.31733v1#S3.SS2)、[§3.3 Retrieval-Guided Cross-Attention](https://arxiv.org/html/2609.31733v1#S3.SS3)、[§4 Experimental Setup](https://arxiv.org/html/2609.31733v1#S4)、[§4.1 Dataset and Retrieval Setup](https://arxiv.org/html/2609.31733v1#S4.SS1)、[§4.2 Compute, splits, and runtime](https://arxiv.org/html/2609.31733v1#S4.SS2)、[§4.3 Generator and Evaluation](https://arxiv.org/html/2609.31733v1#S4.SS3)、[§5 Results](https://arxiv.org/html/2609.31733v1#S5)、[§5.1 Retrieval quality](https://arxiv.org/html/2609.31733v1#S5.SS1)、[§5.2 Generation under the three retrieval conditions](https://arxiv.org/html/2609.31733v1#S5.SS2)、[§5.3 Retrieval similarity does not predict harm](https://arxiv.org/html/2609.31733v1#S5.SS3)、[§5.4 What the gate should condition on](https://arxiv.org/html/2609.31733v1#S5.SS4)、[§6 Limitations](https://arxiv.org/html/2609.31733v1#S6)、[§7 Impact in African and other low-resource clinical contexts](https://arxiv.org/html/2609.31733v1#S7)、[Table 1](https://arxiv.org/html/2609.31733v1#S5.T1)、[Table 2](https://arxiv.org/html/2609.31733v1#S5.T2)、[Table 3](https://arxiv.org/html/2609.31733v1#S5.T3)。
- `abstract`：[arXiv:2609.31733](https://arxiv.org/abs/2609.31733)。
- `doi`：[10.48550/arXiv.2609.31733](https://doi.org/10.48550/arXiv.2609.31733)。

[Home](../) · [AI Papers](./)
