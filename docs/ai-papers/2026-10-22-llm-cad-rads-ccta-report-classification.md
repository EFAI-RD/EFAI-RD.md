---
catalog_id: "doi:10.3389/fcvm.2026.1909068"
editors:
  - "Clare"
refs:
  main:
    title: "Large language model-assisted CAD-RADS classification: structured report extraction, accuracy, and clinical decision-making risk of ChatGPT-4o/5 and DeepSeek-R1"
    url: "https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 三個聊天介面零樣本讀 CCTA 報告分 CAD-RADS：DeepSeek-R1 與 ChatGPT-5 約八成、ChatGPT-4o 54%，900 份高風險報告被降到 3 以下的比例 2.6%–14.1%

## 來源

- 團隊：南方醫科大學第八附屬醫院（佛山）放射科、臨床檢驗科、超音波科與順德樂從醫院臨床檢驗科共 12 位作者；第一作者 Haorong Rong、最後作者 Baoliang Guo。[(ref: main author list)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full)
- 論文：*Large language model-assisted CAD-RADS classification: structured report extraction, accuracy, and clinical decision-making risk of ChatGPT-4o/5 and DeepSeek-R1*，Frontiers in Cardiovascular Medicine 第 13 卷、文章編號 1909068（2026），Original Research；2026-06-14 投稿、2026-09-15 接受、2026-10-09 出版，開放取用（CC BY 4.0）。[(ref: main)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full)
- 識別碼：DOI [10.3389/fcvm.2026.1909068](https://doi.org/10.3389/fcvm.2026.1909068)。本篇無 arXiv 預印本。
- 全文：[Frontiers 全文頁](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full)。
- 資料與程式：作者表示原始資料可向作者索取；未提供程式碼或資料庫連結。prompt 寫在 Methods 正文。[(ref: main Statements)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#h7)
- 研究性質：單一中心回顧性診斷準確度研究，不是 pilot；三個模型實際對 2,100 份報告各跑一次並附 95% CI。輸入是翻譯成英文、只含 findings 的報告文字，參考標準由兩位放射科醫師依同一份文字判定，不是影像或血管攝影答案；報告依類別配額抽樣，每類 300 份，準確率不代表臨床盛行率下的表現。[(ref: main Methods)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s2)
- 證據邊界：本文數值以全文正文與 Table 1–5 為準；Figure 2–5 只以圖呈現的逐類別準確率與混淆矩陣計數未納入本文引述，正文未寫出的 prompt 全文細節也不在本文轉述範圍。

**編輯：** Clare

作者把 2,100 份冠狀動脈電腦斷層血管攝影（coronary CT angiography，CCTA）的 findings 文字交給三個網頁版 LLM 零樣本指定 CAD-RADS 主類別，DeepSeek-R1（Deep Thinking）與 ChatGPT-5（Thinking）的完全一致率為 82.57% 與 80.19%，ChatGPT-4o（標準模式）為 53.62%，而 900 份參考標準為高風險（4A–5）的報告被降到 3 以下的比例分別是 2.56%、4.11% 與 14.11%。[(ref: main Abstract, Table 3, Table 5)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T3)

## 流程

![CAD-RADS 報告分類研究設計示意圖。四個圓角方塊由左到右排成一列，彼此以三支實線箭頭依序相連。藍色方塊「1 Reports and reference」：Single center, Mar 2022 - Oct 2025；CCTA findings-only reports；Chinese -> English (medical translator)；Quota sampling: 300 per category；7 categories x 300 = 2,100 patients；Categories: 0, 1, 2, 3, 4A, 4B, 5；Reference: 2 radiologists (10 y) + 3rd radiologist for 12 disagreements。綠色方塊「2 Zero-shot prompting」：Fixed prompt: "Assume you are a radiologist." -> one main CAD-RADS category；No rule text, no few-shot, no retrieval, no web search；Each report once, in a new chat；Consumer web interfaces, no API；Oct 15 - Nov 30, 2025。橘色方塊「3 Model configurations」：ChatGPT-4o (standard mode)；ChatGPT-5 (Thinking mode)；DeepSeek-R1 (Deep Thinking mode)；Model and mode vary together；Backend snapshot, temperature, top-p, seed: not disclosed；Output scored: main category only。紫色方塊「4 Analysis」：Exact-match accuracy, Wilson 95% CI；Cochran's Q + exact McNemar (Holm)；Gwet AC1 vs reference；Management groups: low 1-2 / intermediate 3 / high 4A-5；High-risk downgrades: DSA within 3 months (subset)。](assets/llm-cad-rads-ccta-study-design.png)

圖：本書庫依論文 Methods 與 Table 1–2 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的研究流程圖為 Figure 1）。[(ref: main Methods, Figure 1, Table 1, Table 2)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#F1)

## 背景／問題

CCTA 可非侵入性地評估冠狀動脈狹窄與動脈粥狀硬化負擔，CAD-RADS 2.0 則把 CCTA 結果標準化成類別並附上處置建議，這兩點作者都有引用文獻。放射科報告的 LLM 資訊抽取、分類與結構化，以及 BI-RADS、LI-RADS、Lung-RADS、PI-RADS 等分類系統的 LLM 評估，作者也引用了既有研究；既有的 LLM CAD-RADS 研究則被作者描述為方法異質。[(ref: main Introduction)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s1)

作者的切入點是：該院的 CCTA 報告通常沒有明確寫出 CAD-RADS 類別，若能自動把敘述式報告轉成類別，可用於資料庫、登錄研究、世代篩選與品質稽核。「自動結構化能支援這些用途」「結果取決於模型、prompt、報告結構、病例組成、語言與目標定義」兩句論文沒有附引用，本文只當成作者的動機陳述；本研究本身也沒有評估任何下游用途。[(ref: main Introduction)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s1)

## 方法摘要

**任務。** 輸入一份 CCTA 報告的 findings 文字（已去除結論、病史與識別資訊），要求模型給出單一 CAD-RADS 主類別：0、1、2、3、4A、4B 或 5。plaque burden、modifiers 與處置建議都不要求、也不計分。[(ref: main Methods)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s2)

**三種模型設定。** ChatGPT-4o（標準模式）、ChatGPT-5（Thinking 模式）與 DeepSeek-R1（Deep Thinking 模式），全部透過一般使用者網頁介面、不用 API，也不做微調。模型世代與推理模式同時改變，作者明言兩者的效果無法分開。[(ref: main Methods, Table 2)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T2)

**Prompt。** 固定的簡短零樣本 prompt，以 "Assume you are a radiologist." 開頭，請模型把報告描述段歸入一個 CAD-RADS 類別；不附 CAD-RADS 規則文字、範例、檢索或網路搜尋，prompt 在推論前定案、沒有在研究病例上調整。[(ref: main Methods)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s2)

**指標。** 主要指標是對參考標準的 exact-match accuracy（95% Wilson CI）；三模型的配對比較用 Cochran's Q，再做兩兩 exact McNemar 並以 Holm 校正；一致性用 unweighted Gwet AC1。另把類別分成低（1–2）、中（3）、高（4A–5）三個處置組，0 單獨看，分析跨組的升降級；參考標準為高風險、模型降到 3 以下的報告，再查三個月內是否有數位減影血管攝影（digital subtraction angiography，DSA）。[(ref: main Statistical analysis)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s2)

## 方法詳解

**病例與抽樣。** 2022 年 3 月至 2025 年 10 月單一中心 PACS 中的 CCTA 報告，每位病人只取一次檢查；排除報告記載偽影、冠狀動脈錯位，或狹窄描述不完整以致無法分類者。以敘述內容的暫定分層做非隨機配額抽樣（暫定分層不當參考標準），最後每個類別 300 份、共 2,100 份。年齡、性別與臨床適應症沒有保留在分析資料中。[(ref: main Study population, Table 1)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T1)

**翻譯。** 原始報告為中文，由一位有 10 年經驗的醫學翻譯把 2,100 份 findings 譯成英文；人類讀者與三個模型看的是同一份固定譯文。[(ref: main Study population)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s2)

**參考標準。** 兩位各有 10 年 CCTA 經驗的放射科醫師獨立閱讀英文 findings 文字，不看影像、結論、模型輸出或工具；兩人在 2,088/2,100 份（99.43%）一致，其餘 12 份由第三位 10 年經驗的放射科醫師決定。分類依 CAD-RADS 2.0：0 為無斑塊或狹窄，1 為 1–24%，2 為 25–49%，3 為 50–69%，4A 為一或兩條血管 70–99%，4B 為左主幹 ≥ 50% 或三條血管皆 70–99%，5 為完全阻塞。[(ref: main Study protocol, Table 4)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T4)

**推論設定。** 2025-10-15 至 11-30 之間，每份報告在新的對話中送出一次，不給回饋、更正或對話歷史；模型名稱是網頁介面顯示的標籤，後端 snapshot、temperature、top-p、最大輸出長度與 seed 都無法設定也未揭露，因此沒有評估重複性。輸出若含說明文字，只取其中明確給出的單一類別計分。[(ref: main Study protocol, Table 2)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T2)

**DSA 查核。** 對參考標準為 4A–5、模型降到 3 以下的報告，查院內紀錄三個月內是否做過 DSA；若血管攝影的嚴重度與高風險 CCTA 相符，視為不支持降級。分析只限於有 DSA 的這個子集。[(ref: main Statistical analysis, Table 5)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T5)

- **論文未交代** — PACS 初篩的報告總數與各排除原因的人數；Figure 1 有流程，正文沒有逐步計數。
- **論文未交代** — 翻譯是否經過覆核或回譯；模型輸出沒有類別、給出多個類別或附帶 modifier 時如何計分（作者在 Discussion 承認需要明確規則），以及由誰判讀模型輸出。
- **論文未交代** — 掃描儀與報告寫法（是否有固定模板）；三個介面的後端版本與解碼參數無法得知，每份報告只跑一次。
- **論文未交代** — 沒有規則式文字抽取、不同 prompt（例如寫入 CAD-RADS 規則或附範例）或 API 固定版本的對照，因此無法分辨錯誤來自模型、推理模式、prompt 還是翻譯。

## 資料與實驗

下表摘錄論文 Table 1 的資料集構成。[(ref: main Table 1)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T1)

| 項目 | 內容 |
|---|---|
| 研究設定 | 單一中心、回顧性診斷準確度研究 |
| 報告期間 | 2022 年 3 月至 2025 年 10 月 |
| 來源 | 院內 PACS |
| 抽樣 | 非隨機、依類別配額、類別平衡 |
| 分析樣本 | 2,100 份 CCTA 報告，來自 2,100 位不同病人 |
| 類別組成 | 參考標準每類 300 份（0、1、2、3、4A、4B、5） |
| 原始報告語言 | 中文 |
| 人與模型的輸入 | 英文譯文，只含 findings |
| 既有 CAD-RADS 欄位 | 平時未記錄；輸入中也沒有 |
| 人口學與轉診資訊 | 年齡、性別、臨床適應症未保留 |

下表合併論文 Table 3 與 Table 4 的整體結果（n = 2,100）。[(ref: main Table 3, Table 4)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T3)

| 比較 | 正確數 | Accuracy (%) | 95% Wilson CI | Gwet AC1 (95% CI) |
|---|---|---|---|---|
| Reader 1 vs Reader 2（裁決前） | 2,088 | 99.43 | 99.00–99.67 | 0.987 (0.973–1.000) |
| ChatGPT-4o（standard） | 1,126 | 53.62 | 51.48–55.74 | 0.460 (0.435–0.485) |
| ChatGPT-5（Thinking） | 1,684 | 80.19 | 78.43–81.84 | 0.769 (0.749–0.789) |
| DeepSeek-R1（Deep Thinking） | 1,734 | 82.57 | 80.89–84.13 | 0.797 (0.778–0.816) |

下表摘錄論文 Table 5 的升降級與 DSA 查核；未註明分母者為 2,100 份中的筆數（%）。[(ref: main Table 5)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T5)

| 轉移 | ChatGPT-4o | ChatGPT-5 | DeepSeek-R1 |
|---|---|---|---|
| 任何升級 | 447 (21.29%) | 95 (4.52%) | 158 (7.52%) |
| 0 → 任何較高類別 | 3 (0.14%) | 0 (0.00%) | 3 (0.14%) |
| 1/2 → 3 | 112 (5.33%) | 18 (0.86%) | 30 (1.43%) |
| 3 → 4A/4B/5 | 13 (0.62%) | 4 (0.19%) | 45 (2.14%) |
| 1/2 → 4A/4B/5 | 0 | 0 | 0 |
| 任何降級 | 527 (25.10%) | 321 (15.29%) | 208 (9.90%) |
| 任何較高類別 → 0 | 6 (0.29%) | 0 | 0 |
| 3 → 1/2 | 28 (1.33%) | 0 | 5 (0.24%) |
| 4A/4B/5 → 1/2 | 6 (0.29%) | 4 (0.19%) | 7 (0.33%) |
| 4A/4B/5 → 3 | 121 (5.76%) | 33 (1.57%) | 16 (0.76%) |
| 參考標準高風險被分到 0–3（/900） | 127 (14.11%) | 37 (4.11%) | 23 (2.56%) |
| 其中三個月內有 DSA | 65/127 (51.18%) | 13/37 (35.14%) | 7/23 (30.43%) |
| DSA 支持原本的高風險判定 | 56/65 (86.15%) | 11/13 (84.62%) | 6/7 (85.71%) |
| DSA 支持降級 | 9/65 (13.85%) | 2/13 (15.38%) | 1/7 (14.29%) |

## 結果

- **整體準確率** — DeepSeek-R1 82.57%、ChatGPT-5 80.19%、ChatGPT-4o 53.62%；Cochran's Q = 657.87（df = 2，P < 0.001），Holm 校正後 DeepSeek-R1 與 ChatGPT-5 的差異 P = 0.026，兩者對 ChatGPT-4o 皆 P < 0.001。[(ref: main Overall accuracy and agreement, Table 3)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s3)
- **一致性仍低於人** — 三個模型對參考標準的 AC1 為 0.460–0.797，兩位放射科醫師裁決前彼此的 AC1 為 0.987。[(ref: main Table 4)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T4)
- **ChatGPT-4o 的錯誤在低類別邊界** — 參考標準為 1 的報告只有 18.0% 分對、77.7% 被分成 2；參考標準為 2 的報告 63.3% 分對、35.0% 被分成 3。[(ref: main Category-specific error patterns, Figure 3)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#F3)
- **ChatGPT-5 的錯誤在 4B 與 5** — 4B 準確率 42.0%、5 為 52.0%，常見錯誤是 4B 判成 4A、完全阻塞判成 4A 或 4B。[(ref: main Category-specific error patterns, Figure 4)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#F4)
- **DeepSeek-R1 的錯誤偏向升級** — 參考標準為 3 的報告有 14.7% 被分成 4A；3 → 4A/4B/5 的筆數（45）是三個模型中最多。[(ref: main Category-specific error patterns, Table 5)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T5)
- **高風險被降到 3 以下** — 900 份參考標準高風險報告中，ChatGPT-4o 降級 127 份（14.11%）、ChatGPT-5 37 份（4.11%）、DeepSeek-R1 23 份（2.56%）；其中有 DSA 的子集裡，DSA 支持原本高風險判定的比例為 84.62%–86.15%。[(ref: main Analysis by clinical management grouping, Table 5)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#T5)
- **作者的解讀** — 錯誤集中在需要組合多條規則的類別（左主幹優先、三血管條件、重度狹窄與完全阻塞的區分），作者因此建議未來把「彈性抽取血管層級發現」與「確定性套用 CAD-RADS 規則」拆開，並主張 LLM 可評估用於沒有類別的報告做批次結構化，不應覆寫放射科醫師已寫的類別或決定處置。[(ref: main Discussion, Conclusion)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s4)

## 限制

**作者自述的限制。** 單一中心、回顧性，輸入是中文報告的英文譯文且沒有影像與臨床資訊，測的是文字分類而非影像判讀；翻譯可能對某些模型較有利，排名只適用於這份英文輸入；配額抽樣讓高類別比例偏高，準確率與轉移率不是依盛行率加權；DSA 只涵蓋部分被降級的高風險病例；每份報告只送一次、沒有測重複性；網頁介面不揭露 snapshot、解碼參數與 seed，且可能隨時間改變；模型世代與推理模式混在一起；prompt 沒有做實驗性變化，不能確立 prompt 的因果效果；只評主類別；兩位讀者經驗相同；沒有評估臨床使用者的理解、效率或轉診決策。[(ref: main Limitations)](https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full#s4)

**本書庫的觀察。**

- **「準確率」是「與英文文字共識一致」** — 參考標準與模型讀的是同一份英文譯文，兩位讀者在 99.43% 的報告一致，說明這份文字對人而言大多可以直接套規則；模型落在 53.62%–82.57%，差距來自規則套用而非報告模糊的可能性較高，但翻譯本身若有錯，人與模型會一起錯，這個設計測不出來。
- **降級多數沒有跨出處置組** — ChatGPT-5 共降級 321 份，跨到 3 以下的只有 37 份；依 Table 5 相減，其餘 284 份是不跨處置組的降級（論文提到的 4B 判成 4A、完全阻塞判成 4A／4B 屬於這類），正文沒有逐項拆分。4B 與 5 在 CAD-RADS 裡分別牽涉左主幹或三血管病變與完全阻塞，這類同組內的降級仍可能有臨床意義，只看跨組轉移會低估它。
- **DSA 子集太小、也有選擇性** — ChatGPT-5 與 DeepSeek-R1 有 DSA 的降級只有 13 與 7 份；這個查核只說明「被降級的高風險病例裡，有做 DSA 的多數確實是高風險」，不能換算成整體的漏判率。
- **比較的是設定，不是模型** — 三者同時改變模型世代、推理模式與介面，又都是 2025 年秋季的網頁版；結果描述的是當時那三種使用方式，不能推論到 API 版本或之後的同名模型。

## 與書庫其他文章的關係

兩篇都讓 LLM 從放射報告文字套用分型規則、參考標準也都是醫師依同一份文字判定；頸動脈那篇把 AHA 準則寫進 prompt 並與只下指令的 prompt 對照，本篇只用不含規則的零樣本 prompt、沒有 prompt 對照，因此本篇在 4B／5 的錯誤能否靠寫入規則改善仍未經測試: [把 AHA 分型規則寫進 prompt，8B 本地模型從 38.9% 升到 81.5%：頸動脈斑塊 MRI 報告的 LLM 輔助判讀，四位放射科醫師對文字參考標準的一致率從 69% 升到 85%（8B）與 90%（671B DeepSeek-R1）](2026-10-19-llm-carotid-plaque-aha-report-reader-study.md)

本篇作者在 Discussion 提議讓 LLM 只抽血管層級發現、再由規則引擎決定最終類別，該研究正是「規則寫成程式、LLM 只抽參數」的實作，並有拿掉工具的消融可以參考這種拆法的效果: [算分交給程式、LLM 只抽參數：GPT-5.5 先把 55 個醫療計算器寫成驗證過的 Python 工具，Qwen3-8B 負責從病歷填表，MedCalc-Bench Verified 上 86.73%，剩下的錯多半出在讀病歷](2026-10-20-tool-augmented-llm-medical-calculation.md)

## 實務的啟發

- **可借用的量測方法** — 除了整體準確率，再按處置組報告升降級筆數，並對參考標準為高風險、被降級的病例做獨立來源（本篇為 DSA）查核。這種拆法能讓「準確率差不多」的兩個模型顯出不同的錯誤方向：本篇 ChatGPT-5 偏向降級、DeepSeek-R1 在 3 → 4A 偏向升級。
- **類別平衡抽樣要和盛行率分開讀** — 每類 300 份的設計適合看各類別的錯誤型態，但整體準確率不是臨床資料上的表現；若要估計批次結構化的實際錯誤量，需要在依盛行率抽樣的資料上再驗證。
- **待驗證的方向** — 作者提議的「LLM 抽血管層級發現＋規則引擎指定類別」與「在 prompt 寫入 CAD-RADS 2.0 規則」都還沒有在本研究中測試；本篇只能說明零樣本 prompt 下的錯誤集中在多規則組合的類別，可作為設計驗證時的重點。
- **證據強度** — 單一中心、翻譯後的英文文字、每份報告一次、無法固定版本的網頁介面；它支持「這三種設定在零樣本下彼此差距明顯、且仍低於人類讀者間一致性」，不足以支持任何一個模型可直接用於自動產生 CAD-RADS 類別，作者也明言不應用來覆寫醫師類別或決定處置。

## References

- **main** — Rong H, Huang X, Chen X, Ouyang L, Li Y, Lin X, Pan J, Li Y, Xie F, Ouyang F, Hu Q, Guo B. *Large language model-assisted CAD-RADS classification: structured report extraction, accuracy, and clinical decision-making risk of ChatGPT-4o/5 and DeepSeek-R1*. Frontiers in Cardiovascular Medicine 13:1909068 (2026). DOI: 10.3389/fcvm.2026.1909068. 全文頁：<https://www.frontiersin.org/journals/cardiovascular-medicine/articles/10.3389/fcvm.2026.1909068/full>。文內引用位置：author list、Abstract、Introduction（#s1）、Methods（#s2：Study population、Study protocol、Statistical analysis）、Results（#s3：Overall accuracy and agreement、Category-specific error patterns、Analysis by clinical management grouping）、Discussion 與 Limitations（#s4）、Conclusion、Statements（#h7）、Table 1–5（#T1–#T5）、Figure 1、3、4（#F1、#F3、#F4）。
- **doi** — <https://doi.org/10.3389/fcvm.2026.1909068>。

[Home](../) · [AI Papers](./)
