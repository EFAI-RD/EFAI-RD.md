---
catalog_id: "arxiv:2610.40327"
editors:
  - "Clare"
refs:
  main:
    title: "Radiology Guideline-derived Decision Graph for Efficient Clinical Decision Support"
    url: "https://arxiv.org/abs/2610.40327v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 放射指引先由 LLM 編成決策圖、再讓小模型逐節點作答：GDGraph 在 347 個病例文字上把 Jev 從 57.3% 拉到 90.8%，高於 RAG＋GPT-4o 的 80.1%；但病例取自已發表的病例報告並經 LLM 改寫，結果沒有信賴區間

## 來源

- 團隊：香港理工大學數據科學及人工智能系（Department of Data Science and Artificial Intelligence, The Hong Kong Polytechnic University），2 位作者 Xuewen Zhou、Zhen Chen（通訊作者）；研究經費為 PolyU Start-up Fund（P0060371）。[(ref: pdf p.1)](https://arxiv.org/pdf/2610.40327v1) [(ref: main §6)](https://arxiv.org/html/2610.40327v1#S6)
- 論文：*Radiology Guideline-derived Decision Graph for Efficient Clinical Decision Support*，arXiv:2610.40327v1（cs.CV；另列 cs.AI），2026-10-29 提交，目前只有 v1；授權為 arXiv non-exclusive distribution license 1.0；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2610.40327v1)
- 識別碼：arXiv [2610.40327](https://arxiv.org/abs/2610.40327v1)；DOI [10.48550/arXiv.2610.40327](https://doi.org/10.48550/arXiv.2610.40327)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2610.40327v1)、[PDF v1](https://arxiv.org/pdf/2610.40327v1)。
- 資料與程式：病例取自公開的 PMC-Patients-V2 與 PubMed Central 開放取用病例報告，但論文沒有公開篩選後的 347 例清單；摘要寫明程式碼「將會公開」，論文未附連結。[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1) [(ref: main Abstract)](https://arxiv.org/html/2610.40327v1#abstract1)
- 研究性質：方法論文，核心流程（指引編譯成決策圖、節點問答、確定性走圖）都有實作，並在三套指引共 347 例上與直接作答、CoT 與 RAG 基線比較；不是 pilot，但所有結果都是單次執行的點估計，沒有信賴區間、標準差或顯著性檢定，也沒有拆解各編譯步驟的消融。[(ref: main §3.1; Table 3)](https://arxiv.org/html/2610.40327v1#S3.T3)
- 證據邊界：本文數值以 arXiv v1 HTML 版的正文與 Table 1–3 為準；Fig. 2 的逐指引延遲與成本只以長條圖呈現，本文只引述正文給出的範圍，不引述圖上讀值。

**編輯：** Clare

作者讓 GPT-6-Luna 把三套放射指引（加拿大泌尿科學會 CUA 2023 腎囊腫處置、O-RADS US v2022 附件腫塊、K-TIRADS 2021 甲狀腺結節）離線編成可執行的決策圖，推論時由 System One 模型 Jev 只回答圖上每個節點的單一條件、布林邏輯交給程式走完；在 347 個由病例報告改寫的文字病例上，Jev 的整體正確率從直接作答的 57.3% 升到 90.8%，高於 RAG＋GPT-4o CoT 的 80.1% 與同一張圖引導的 GPT-4o CoT 的 82.7%，每例線上 API 時間約 0.79–1.62 秒。[(ref: main Abstract; §3.3; Table 3)](https://arxiv.org/html/2610.40327v1#S3.SS3)

## 流程

![GDGraph 流程示意圖，分上下兩排。上排標題為 (a) Offline: guideline compilation (built once per guideline)，四個淺藍色圓角方塊由左到右以實線箭頭相連：「Guideline document D」（narrative text、tables、footnotes、cross-referenced definitions；Compiler LLM: GPT-6-Luna (low reasoning effort)，讀取抽出的文字與 PDF 頁面影像）→「1. Section-based chunking」（把 D 依章節切成 C1 ... Cm、表格與註腳不拆開；LLM 掃過所有 chunk 建立 global definition memory M）→「2. Local subgraph extraction」（每個 chunk 以 TF-IDF 從 M 取相關定義，LLM 抽出 states、atomic conditions、rules 成為子圖 Gi；數值門檻拆成獨立條件、陰性發現寫成 NOT）→「3. Cross-branch aggregation」（LLM 依 TF-IDF 把共享特徵或例外的子圖分組，合併等價節點、保留不等價的門檻、套用升級與例外規則，得到 decision graph G = (S, A, E, Y)）。一條實線斜箭頭由「3. Cross-branch aggregation」指向下排的「4. Node question」，旁邊以斜體標註 same graph G reused for every case。下排標題為 (b) Online: graph-guided selection (per case)，四個方塊由左到右以實線箭頭相連：淺綠色「Case input (text only)」（影像發現與臨床脈絡的文字，已改寫去除明確診斷標籤；從 entry states S0 開始走圖）→ 淺綠色「4. Node question」（每個 atomic condition 由確定性模板轉成自含的問題，System One 模型 Jev v1.13.0 選出答案）→ 淺橘色「5. Deterministic traversal」（程式依 AND、OR、NOT、AtLeast-k 判斷每條規則，沿成立的分支前進，在下一個狀態重複）→ 灰色「Output」（處置或類別選項，結論事先由 LLM 對應到任務選項；traversal log 記下每個問題、答案與走過的邊）。圖底三行文字：Evaluation: 347 text-based cases from PMC-Patients-V2 and PubMed Central case reports；CUA 2023 renal cyst management (127) | O-RADS US v2022 adnexal mass (117) | K-TIRADS 2021 thyroid nodule (103)；Metrics: case accuracy, weighted F1, MCC, mean online API time and cost per case; graph quality = node / rule precision against the source guideline](assets/gdgraph-guideline-decision-graph-pipeline.png)

圖：本書庫依論文 §2、§3.1 與 Table 1 的文字重繪的流程示意圖，只含設計層級的設定與病例計數，不含結果數值，未複製論文原圖（論文 Fig. 1 為同一框架的概觀圖，Algorithm 1 為建圖步驟）。[(ref: main §2; Fig. 1; Algorithm 1)](https://arxiv.org/html/2610.40327v1#S1.F1)

## 背景／問題

放射科的風險分層與處置規劃，常由專科指引以明確、離散的條件決定，例如腎囊腫處置、附件腫塊與甲狀腺結節的風險分級；作者指出這些條件分散在指引的敘述、表格與交叉引用的定義裡，因此要自動化就必須依序走完指引中互相依賴的判斷步驟。[(ref: main §1)](https://arxiv.org/html/2610.40327v1#S1)

作者主張，預訓練語言模型雖可直接讀報告文字作答，但常偏離既有的診斷指引；這個前提有引用支持（Hager 等人 2024 年 Nature Medicine 對 LLM 臨床決策限制的評估），論文自己的基線也呈現同一現象：不給指引時，Direct GPT-4o 與 GPT-4o CoT 在 CUA 與 K-TIRADS 的正確率都低於 60%。[(ref: main §1)](https://arxiv.org/html/2610.40327v1#S1) [(ref: main §3.2; Table 3)](https://arxiv.org/html/2610.40327v1#S3.SS2)

作者把既有做法分成兩類：RAG 系統在作答時檢索相關段落交給模型自行解讀；CPGPrompt 把切好的指引文字轉成決策樹逐步評估，但依作者的描述，該流程仰賴人工挑選相關段落並人工驗證生成的樹。本篇要補的缺口是：直接從原始指引文件**自動**建出可執行的決策結構，並把每一步交給不生成中間文字、直接對候選選項打分的「System One」模型。[(ref: main §1)](https://arxiv.org/html/2610.40327v1#S1)

## 方法摘要

**兩段式設計。** GDGraph 把「編譯指引」與「評估病例」拆開：離線時由 LLM 把一份指引編成決策圖，每套指引只建一次；線上時對每個病例走這張圖，模型只回答局部問題，布林邏輯由程式處理，最後留下可追溯的決策路徑，不需要針對任務訓練。[(ref: main §2.1)](https://arxiv.org/html/2610.40327v1#S2.SS1)

**圖的組成。** 決策圖 G = (𝒮, 𝒜, ℰ, 𝒴) 含臨床狀態 𝒮（含入口狀態 𝒮₀）、atomic conditions 𝒜、有向規則 ℰ 與候選結果 𝒴（診斷類別或處置）。每個 atomic condition 是單一可追溯的條件，包含臨床特徵與其解剖或時間範圍、比較運算子與數值（例如小於 10 cm 或有／無），以及連到定義庫的定義；每條規則以 ∧、∨、¬ 與 AtLeast-k 組合條件，並標明它是直接決定、支持或排除目標。[(ref: main §2.2)](https://arxiv.org/html/2610.40327v1#S2.SS2)

**離線建圖（Algorithm 1）。**

- **Section-based chunking** — 依文件章節切塊，表格與註腳保持完整；LLM 掃過所有 chunk 建立全域定義庫 M（術語、別名、定義）。[(ref: main §2.2)](https://arxiv.org/html/2610.40327v1#S2.SS2)
- **Local subgraph extraction** — 對每個 chunk 以 TF-IDF 從 M 取相關定義（明確引用的定義一律保留），再由 LLM 抽出狀態、條件與規則成為局部子圖。[(ref: main §2.2; Algorithm 1)](https://arxiv.org/html/2610.40327v1#algorithm1)
- **Cross-branch aggregation** — LLM 依 TF-IDF 相似度把共享特徵或例外的子圖分成可重疊的群組，依序在最新的圖上合併意義與判斷條件相同的節點，不等價的門檻保持分開；遇到指引的升級或例外條款時，更新受影響規則的條件與目標。[(ref: main §2.2)](https://arxiv.org/html/2610.40327v1#S2.SS2)

**線上推論（Graph-guided selection）。** 評估前先由 LLM 把圖上有來源支持的結論對應到該任務的標準答案選項；推論時從入口狀態出發，在每個作用中的狀態由 System One 模型回答外連條件的問題（依據病例的影像發現與附帶的定義），程式判斷規則是否成立並沿成立的分支前進，最後由走到的結論決定預測，並記錄每個問題與答案。[(ref: main §2.3)](https://arxiv.org/html/2610.40327v1#S2.SS3)

**指標。** 決策表現用 case accuracy（Acc.）、weighted F1（WF1）與 Matthews correlation coefficient（MCC），效率用每例平均線上 API 時間與成本；圖的品質用人工核對的 node precision（條件的問題與定義有來源支持的比例）與 rule precision（規則有指引支持的比例）。[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1)

## 方法詳解

**模型分工。** 建圖用 GPT-6-Luna、low reasoning effort，輸入抽出的文字並附上 PDF 頁面影像以保留表格結構與註腳；線上作答比較 System One 模型 Jev（v1.13.0）與 GPT-4o。論文對 Jev 的說明只引用一篇部落格文章（TypeSafe AI Blog），描述為不產生中間文字、直接對離散候選選項打分的模型；其架構與規模論文未說明。[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1) [(ref: main §1)](https://arxiv.org/html/2610.40327v1#S1)

**六種設定。** [(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1)

- **無檢索、無圖** — Direct Jev、Direct GPT-4o、GPT-4o CoT，只拿到病例、候選選項與選項定義。
- **RAG＋GPT-4o CoT** — GPT-4o 每例產生三個搜尋查詢，MedCPT 為每個查詢取回 top-5 個指引 chunk，再做 CoT 推理。
- **圖引導** — GDGraph＋Jev 與 GDGraph＋GPT-4o CoT 走同一張為該任務建好的圖。

**條件如何變成問題。** 具名的影像型態保留為單一條件並連到定義庫，數值門檻等附加條件拆成獨立條件，陰性發現以邏輯否定表示；每個條件與它引用的定義由確定性模板組成一個自含的問題交給模型。例如「同一病灶同時具有影像型態 P 且直徑小於 10 cm」寫成兩個條件的 ∧。[(ref: main §2.2)](https://arxiv.org/html/2610.40327v1#S2.SS2)

**病例怎麼來。** 347 例取自 PMC-Patients-V2 與 PubMed Central 病例報告，篩選有指引相關影像發現與臨床脈絡者；參考標籤取自來源中的明確標籤，或依指引條件套用到報告的發現推得；病例描述再以 GPT-6.1-sol 改寫，移除明確的診斷標籤以降低答案外洩風險。CUA 任務是依臨床脈絡選處置，O-RADS 與 K-TIRADS 是由影像描述給超音波風險類別。[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1)

- **論文未交代** — 建圖、建定義庫、分組合併與結論對應各步驟的 prompt 全文，以及把條件轉成問題的模板內容。
- **論文未交代** — TF-IDF 取回定義的數量或門檻、子圖分組的方式，以及「結論對應到答案選項」用的是哪一個 LLM。
- **論文未交代** — 347 例的篩選數量與排除條件、各指引中「來源明確標籤」與「依指引推得標籤」各占多少例，以及推得標籤與改寫結果由誰、以何種方式覆核。
- **論文未交代** — Table 2 的 node／rule precision 由誰、幾人核對；每套指引只建一次圖，建圖結果在重跑時是否穩定沒有報告。
- **論文未交代** — Jev 與 GPT-4o 的解碼設定與執行次數；API 時間與成本的計算方式（例如是否含網路延遲、以何種價目計價）。
- **論文未交代** — 程式碼尚未公開；§3.3 正文說效率比較見「Fig. 3」，但論文中的效率圖是 Fig. 2。

## 資料與實驗

**資料。** 三套指引與病例數（Table 1）。[(ref: main Table 1)](https://arxiv.org/html/2610.40327v1#S3.T1)

| Guideline | Clinical Task | Cases |
|---|---|---|
| CUA (2023) | Renal cyst management | 127 |
| O-RADS US v2022 | Adnexal mass stratification | 117 |
| K-TIRADS (2021) | Thyroid nodule stratification | 103 |
| Total | | 347 |

| 項目 | 內容 |
|---|---|
| 病例來源 | PMC-Patients-V2 與 PubMed Central 病例報告（文字病例，不含影像） |
| 參考標籤 | 來源中的明確標籤，或依指引條件套用到報告發現推得 |
| 前處理 | 以 GPT-6.1-sol 改寫病例描述、移除明確診斷標籤 |
| 倫理 | 回溯使用 PMC Open Access Subset 的開放資料，作者表示依資料授權不需倫理審查 |

資料來源：[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1) [(ref: main §5)](https://arxiv.org/html/2610.40327v1#S5)

**建圖品質（Table 2，supported/total）。** [(ref: main Table 2)](https://arxiv.org/html/2610.40327v1#S3.T2)

| Guideline | Node Prec. | Rule Prec. |
|---|---|---|
| CUA | 137/137 (100.0%) | 51/55 (92.7%) |
| O-RADS | 136/137 (99.3%) | 92/98 (93.9%) |
| K-TIRADS | 216/216 (100.0%) | 123/123 (100.0%) |
| Overall | 489/490 (99.8%) | 266/276 (96.4%) |

**決策表現（Table 3）。** Acc. 與 WF1 為百分比；原表以粗體標示各任務內的最佳值，此處不重現粗體，各任務三項指標的最高值都是 GDGraph＋Jev。[(ref: main Table 3)](https://arxiv.org/html/2610.40327v1#S3.T3)

| Task | Method | Acc. (%) | WF1 (%) | MCC |
|---|---|---|---|---|
| CUA (n=127) | Direct Jev | 61.4 | 64.1 | 0.555 |
| | GDGraph+Jev | 93.7 | 94.4 | 0.922 |
| | Direct GPT-4o | 46.5 | 54.4 | 0.412 |
| | GPT-4o CoT | 52.8 | 59.3 | 0.447 |
| | RAG+GPT-4o CoT | 86.6 | 88.0 | 0.836 |
| | GDGraph+GPT-4o CoT | 89.0 | 87.5 | 0.862 |
| O-RADS (n=117) | Direct Jev | 72.6 | 70.2 | 0.587 |
| | GDGraph+Jev | 92.3 | 93.1 | 0.884 |
| | Direct GPT-4o | 69.2 | 70.4 | 0.552 |
| | GPT-4o CoT | 57.3 | 59.7 | 0.458 |
| | RAG+GPT-4o CoT | 84.6 | 85.4 | 0.786 |
| | GDGraph+GPT-4o CoT | 78.6 | 82.9 | 0.713 |
| K-TIRADS (n=103) | Direct Jev | 35.0 | 34.6 | 0.235 |
| | GDGraph+Jev | 85.4 | 85.6 | 0.794 |
| | Direct GPT-4o | 47.6 | 49.3 | 0.342 |
| | GPT-4o CoT | 44.7 | 47.8 | 0.238 |
| | RAG+GPT-4o CoT | 67.0 | 68.4 | 0.515 |
| | GDGraph+GPT-4o CoT | 79.6 | 80.1 | 0.714 |

**整體正確率（正文）。** 347 例合計：Direct Jev 57.3%、GDGraph＋Jev 90.8%、GPT-4o CoT 51.9%、RAG＋GPT-4o CoT 80.1%、GDGraph＋GPT-4o CoT 82.7%。這些整體值等於三個任務依病例數加權的平均。[(ref: main §3.2)](https://arxiv.org/html/2610.40327v1#S3.SS2) [(ref: main §3.3)](https://arxiv.org/html/2610.40327v1#S3.SS3)

**效率（正文，Fig. 2）。** 三個任務的每例平均線上 API 時間：GDGraph＋Jev 0.79–1.62 秒、RAG＋GPT-4o CoT 6.16–7.15 秒、GDGraph＋GPT-4o CoT 17.10–34.97 秒；GDGraph＋Jev 每例 API 成本 0.56–1.07 × 10⁻³ 美元。[(ref: main §3.3; Fig. 2)](https://arxiv.org/html/2610.40327v1#S3.T3.fig2)

## 結果

- **圖本身大致忠於指引** — 490 個條件中 489 個有來源支持，276 條規則中 266 條有指引支持；不受支持的規則集中在 CUA（4 條）與 O-RADS（6 條），K-TIRADS 全部受支持。[(ref: main §3.2; Table 2)](https://arxiv.org/html/2610.40327v1#S3.T2)
- **小模型加圖後在三個任務都最好** — GDGraph＋Jev 在三個任務的 Acc.、WF1 與 MCC 都是該任務最高；提升幅度最大的是 K-TIRADS，正確率從 35.0% 升到 85.4%。[(ref: main §3.3; Table 3)](https://arxiv.org/html/2610.40327v1#S3.T3)
- **圖與 RAG 對 GPT-4o 各有勝負** — 都用 GPT-4o CoT 時，整體上圖引導 82.7%、RAG 80.1%；但 O-RADS 是 RAG 較好（84.6% vs 78.6%），K-TIRADS 是圖較好（79.6% vs 67.0%）。作者把 K-TIRADS 的差距歸因於分級要同時看結節成分、回音與可疑特徵，明確的路徑與定義有助於處理多特徵條件。[(ref: main §3.2)](https://arxiv.org/html/2610.40327v1#S3.SS2)
- **CoT 不一定比直接作答好** — 不給指引時，GPT-4o CoT 在 O-RADS 的正確率 57.3% 低於 Direct GPT-4o 的 69.2%，K-TIRADS 也是 44.7% 低於 47.6%。[(ref: main Table 3)](https://arxiv.org/html/2610.40327v1#S3.T3)
- **速度與成本** — 三個任務的每例線上 API 時間，GDGraph＋Jev 為 0.79–1.62 秒、RAG＋GPT-4o CoT 為 6.16–7.15 秒；同一張圖交給 GPT-4o CoT 走時反而最慢（17.10–34.97 秒）；作者的結論是，把指引組織成局部節點判斷與明確規則，能讓 System One 模型以低延遲與低成本處理多條件準則。[(ref: main §3.3)](https://arxiv.org/html/2610.40327v1#S3.SS3)
- **錯誤型態** — 剩下的錯誤中，11 例 K-TIRADS 把「ill-defined margins」或「irregular shape」當成「irregular margins」而走到較高風險分支，原因是節點定義沒有區分這幾個術語；3 例 O-RADS 錯在把「moderate flow」等質性血流描述對應到節點條件。[(ref: main §3.4)](https://arxiv.org/html/2610.40327v1#S3.SS4)

## 限制

作者在錯誤分析中指出的限制：放射描述的用語未經正規化、影像概念與模型表徵之間的對應不一致時，節點判斷就會出錯，因此需要正規化放射用語並對齊影像概念。[(ref: main §3.4)](https://arxiv.org/html/2610.40327v1#S3.SS4)

本書庫另外注意到的限制：

- **病例不是臨床報告** — 347 例來自已發表的病例報告，經 GPT-6.1-sol 改寫後才送評，模型讀的是整理過的文字摘要，不是放射科報告原文，也不看影像；部分參考標籤是依同一套指引條件從報告發現推得，評估的是「是否照指引走」，不是診斷是否正確。[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1)
- **沒有不確定性** — 每個任務 103–127 例，所有比較都是單次結果，沒有信賴區間或顯著性檢定；O-RADS 上 RAG 與圖引導 GPT-4o 的 6.0 個百分點差距，在 117 例下約相當於 7 例。[(ref: main Table 3)](https://arxiv.org/html/2610.40327v1#S3.T3)
- **沒有消融與人類基線** — 沒有拆開定義庫、跨分支合併或 System One 模型各自的貢獻，也沒有與 CPGPrompt 等既有決策樹方法或放射科醫師比較。[(ref: main §3.1)](https://arxiv.org/html/2610.40327v1#S3.SS1)
- **圖仍有錯而沒有人工修正流程** — Overall rule precision 96.4%，表示有 10 條不受指引支持的規則留在圖中；論文沒有報告這些錯誤規則實際影響了多少病例，也沒有描述上線前由誰審圖。[(ref: main Table 2)](https://arxiv.org/html/2610.40327v1#S3.T2)
- **重現細節** — prompt、模板、取回參數、標籤推得方式與程式碼等缺漏見「方法詳解」的論文未交代項目。

## 與書庫其他文章的關係

兩篇都把臨床規則從 LLM 的自由生成裡抽出來交給程式執行：該研究由 LLM 為 55 個醫療計算器各寫一支 Python 工具、小模型只抽參數，本篇由 LLM 把整份放射指引編成決策圖、小模型只回答節點問題；兩篇的「規則放在程式」都比同一小模型直接作答高出二十幾到三十幾個百分點，但該研究有拿掉工具的消融，本篇沒有拆解各編譯步驟: [算分交給程式、LLM 只抽參數：GPT-5.5 先把 55 個醫療計算器寫成驗證過的 Python 工具，Qwen3-8B 負責從病歷填表，MedCalc-Bench Verified 上 86.73%，剩下的錯多半出在讀病歷](2026-10-20-tool-augmented-llm-medical-calculation.md)

頸動脈斑塊那篇把 AHA 分型規則寫進 prompt、仍由 LLM 自己套規則，本篇則把指引編成可執行的決策圖、由程式走完布林邏輯，兩篇並讀可對照「規則放在 prompt」與「規則放在圖與程式」兩種把放射分型規則交給 LLM 的做法: [把 AHA 分型規則寫進 prompt，8B 本地模型從 38.9% 升到 81.5%：頸動脈斑塊 MRI 報告的 LLM 輔助判讀，四位放射科醫師對文字參考標準的一致率從 69% 升到 85%（8B）與 90%（671B DeepSeek-R1）](2026-10-19-llm-carotid-plaque-aha-report-reader-study.md)

該研究的作者在 Discussion 提議讓 LLM 只抽血管層級發現、再由規則引擎決定 CAD-RADS 類別，本篇是把這種拆法推到整份指引的一個實作，但評估的是 CUA、O-RADS 與 K-TIRADS 三套指引，不含 CAD-RADS: [三個聊天介面零樣本讀 CCTA 報告分 CAD-RADS：DeepSeek-R1 與 ChatGPT-5 約八成、ChatGPT-4o 54%，900 份高風險報告被降到 3 以下的比例 2.6%–14.1%](2026-10-22-llm-cad-rads-ccta-report-classification.md)

兩篇都把附件腫塊的超音波文字描述交給 LLM：該研究要 GPT-5 判良惡性、以手術病理為答案並對照 IOTA 規則、ADNEX 與專家，本篇則要模型依 O-RADS US v2022 給風險類別、部分參考標籤由套用指引推得，衡量的是對指引的遵循而不是診斷準確度: [把超音波描述交給 ChatGPT 判良惡性：300 顆附件腫塊，和 IOTA 規則、ADNEX 與專家差多少？](2026-09-22-chatgpt-adnexal-mass-ultrasound-triage.md)

## 實務的啟發

- **把指引拆成「條件」與「邏輯」來量** — 論文用 node precision 與 rule precision 分別核對圖與指引是否一致，再用走圖結果衡量決策；評估任何「LLM 依指引分級」的系統時，先核對規則本身、再看模型答題，這種分層檢查可以借用，至少能分辨錯在圖還是錯在讀病例。
- **生成的決策圖要當成臨床規則來審** — 276 條規則中有 10 條不受指引支持，而論文沒有交代這些規則影響了多少病例；若要借用「LLM 自動編譯指引」的做法，產出的圖仍需要專科醫師逐條審閱，不能把自動建圖的結果視為已驗證。
- **用語正規化是瓶頸** — 剩下的錯誤多半出在「ill-defined」與「irregular」這類近義描述，以及質性血流描述的對應；在真實報告上，用語變異只會更大，值得作為驗證重點。
- **結果仍待外部驗證** — 90.8% 來自改寫過的已發表病例、部分標籤由同一套指引推得、單次執行且沒有信賴區間；它支持「把指引結構化後，小模型逐節點作答可明顯勝過同一模型直接作答」，還不足以說明在真實放射報告或臨床流程中同樣可靠。

## References

- **main** — Zhou X, Chen Z. *Radiology Guideline-derived Decision Graph for Efficient Clinical Decision Support*. arXiv:2610.40327v1 [cs.CV], 2026. DOI: 10.48550/arXiv.2610.40327. Abstract：<https://arxiv.org/abs/2610.40327v1>；全文 HTML：<https://arxiv.org/html/2610.40327v1>；PDF：<https://arxiv.org/pdf/2610.40327v1>。文內引用位置：Abstract、§1 Introduction、§2 Methodology（2.1–2.3、Algorithm 1）、§3 Experiments（3.1–3.4）、§5 Compliance with Ethical Standards、§6 Acknowledgments、Table 1–3、Fig. 1、Fig. 2；深鏈 [Abstract](https://arxiv.org/html/2610.40327v1#abstract1)、[§1](https://arxiv.org/html/2610.40327v1#S1)、[Fig. 1](https://arxiv.org/html/2610.40327v1#S1.F1)、[§2](https://arxiv.org/html/2610.40327v1#S2)、[§2.1](https://arxiv.org/html/2610.40327v1#S2.SS1)、[§2.2](https://arxiv.org/html/2610.40327v1#S2.SS2)、[Algorithm 1](https://arxiv.org/html/2610.40327v1#algorithm1)、[§2.3](https://arxiv.org/html/2610.40327v1#S2.SS3)、[§3.1](https://arxiv.org/html/2610.40327v1#S3.SS1)、[Table 1](https://arxiv.org/html/2610.40327v1#S3.T1)、[Table 2](https://arxiv.org/html/2610.40327v1#S3.T2)、[Table 3](https://arxiv.org/html/2610.40327v1#S3.T3)、[Fig. 2](https://arxiv.org/html/2610.40327v1#S3.T3.fig2)、[§3.2](https://arxiv.org/html/2610.40327v1#S3.SS2)、[§3.3](https://arxiv.org/html/2610.40327v1#S3.SS3)、[§3.4](https://arxiv.org/html/2610.40327v1#S3.SS4)、[§5](https://arxiv.org/html/2610.40327v1#S5)、[§6](https://arxiv.org/html/2610.40327v1#S6)。
- **abstract** — 同上論文的 arXiv abstract 頁（作者、提交日期、主題分類、版本紀錄、授權）：<https://arxiv.org/abs/2610.40327v1>。
- **pdf** — 同上論文 PDF v1 首頁（作者單位）：<https://arxiv.org/pdf/2610.40327v1>。

[Home](../) · [AI Papers](./)
