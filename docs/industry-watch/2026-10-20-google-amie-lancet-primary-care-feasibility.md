---
title: "Google 宣傳 AMIE 的 Lancet 研究：「鑑別診斷與醫師最終診斷相符 90%」是前七名清單的命中率，同一天更新的自家研究部落格寫著排第一名的只有 56%"
category: industry-watch
date: 2026-10-20
updated: 2026-10-22
tags: [Google, Google-DeepMind, AMIE, conversational-AI, primary-care, differential-diagnosis, The-Lancet, feasibility-study, clinical-workflow, triage, Beth-Israel-Deaconess, top-k-accuracy]
catalog_id: "google:amie-lancet-primary-care-feasibility-2026-10-08"
editors:
  - "Clarence"
source:
  orgs:
    - "Google"
    - "Beth Israel Deaconess Medical Center"
  event: "Google 發布面向一般讀者的部落格，宣傳 AMIE 在 Beth Israel Deaconess Medical Center 門診基層醫療的前瞻性可行性研究；同日該研究於 The Lancet 線上刊出，Google Research 的技術部落格亦於同日加註更新"
  event_date: "2026-10-08"
  official_url: "https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/"
related_articles:
  - path: "2026-10-19-ge-healthcare-end-tidal-control-michigan-study.md"
    relation: "兩則都是廠商宣傳一篇數值本身正確的論文，落差出在限定條件被留在原處，但被省略的限定條件種類不同：該則省略的是「這是模型對一位虛構典型病人的推算」，本則省略的是「90% 指的是前七名清單命中，排第一名只有 56%」"
  - path: "2026-10-08-medgemma-global-deployment-claims.md"
    relation: "同一家公司相隔十五天的兩則健康部落格，對證據的處理方向相反，該則是五個合作案裡只有一個報得出已完成的篩檢量、其餘用進行式帶過，本則有一份同儕審查論文與完整試驗登錄可逐項回查，問題反而出在同一組數字在自家兩個頁面上被寫成兩種強度"
  - path: "../ai-papers/2026-10-13-clinician-llm-use-vs-benchmarks.md"
    relation: "該篇用 12.8 萬筆真實提問指出臨床人員實際拿大型語言模型做的多半是文件工作、診斷只占 3.7%，本則正是少數真的把對話式模型放進真實門診流程並前瞻收案的研究，兩篇並讀可以看出「離開基準、進到流程」之後要量的是哪些東西"
  - path: "2026-10-22-openai-distributed-agents-perturb-seq-atlas.md"
    relation: "兩則都是官方部落格給出一個百分比而分母只存在於被連結的論文裡，本則的 90% 是前七名清單命中率，該則的 75% 是 20 組配對報告共 60 次判斷中的 45 次"
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "本則的 90% 是前七名清單的命中率、排第一名的只有 56%，兩個數字都在 Google 自家的技術部落格裡；該則的「結塊慢 100 倍以上」與「6 到 9 倍」同樣分屬兩層官方文件，而該則又多了一層 —— 詳細版不是另一個頁面，而是同一頁上要點開才看得到的面板，六段利益揭露也只存在於那些面板裡"
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "同一家公司相隔七天的兩則發布，可回查程度相差一整個層級：本則有同儕審查論文、開放預印本與試驗登錄可以逐項對照，爭點只在哪一個百分比被挑進標題；該則的正文裡 `peer`、`paper`、`arXiv`、`DOI` 命中數全部為零，唯一能回查的對象是一個公開資料庫條目。把兩則並讀可以看出「同一家公司的官方發布」不是一種均質的證據等級"
refs:
  blog:
    title: "Google：Study in The Lancet suggests AI could improve patient-physician relationships.（面向一般讀者的官方部落格）"
    url: "https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/"
  gr:
    title: "Google Research：Exploring the feasibility of conversational diagnostic AI in a real-world clinical study（技術部落格，2026-03-11 首發、2026-10-08 加註更新）"
    url: "https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/"
  lancet:
    title: "Brodeur PG 等，Conversational diagnostic artificial intelligence in ambulatory primary care: a prospective feasibility study，The Lancet（摘要頁；全文付費）"
    url: "https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract"
  comment:
    title: "Omar M、Nadkarni GN，Conversational diagnostic AI in primary care: what happens after it speaks?，The Lancet Comment（摘要頁；全文付費）"
    url: "https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901763-0/abstract"
  ct:
    title: "ClinicalTrials.gov：NCT06911398，AMIE's Clinical Conversational Abilities in an Urgent Care Setting（試驗登錄）"
    url: "https://clinicaltrials.gov/study/NCT06911398"
  arxiv:
    title: "Brodeur P 等，A prospective clinical feasibility study of a conversational diagnostic AI in an ambulatory primary care clinic，arXiv:2603.08448（預印本）"
    url: "https://arxiv.org/abs/2603.08448"
  amie:
    title: "Google Research：AMIE 專案頁（Articulate Medical Intelligence Explorer）"
    url: "https://sites.research.google/gr/amie/"
status: published
skill_version: "write-industry-watch@3.0"
evidence_reviewed: true
---

[Home](../) · [Industry Watch](./)

# Google 宣傳 AMIE 的 Lancet 研究：「鑑別診斷與醫師最終診斷相符 90%」是前七名清單的命中率，同一天更新的自家研究部落格寫著排第一名的只有 56%

## 來源

- **組織** — **Google**（發布方，研究由 Google Research 與 Google DeepMind 參與）與 **Beth Israel Deaconess Medical Center**（BIDMC，波士頓的學術醫學中心，為本研究的試驗主辦機構）。面向一般讀者的部落格具名作者為 Google 的 Research Lead `Mike Schaekermann` [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)；技術部落格另具名 Google DeepMind 的 `Alan Karthikesalingam` [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **事件** — Google 發布部落格宣傳 **AMIE**（`Articulate Medical Intelligence Explorer`，Google 的研究用醫療對話 AI）在 BIDMC 門診基層醫療的前瞻性可行性研究；同日該研究於 *The Lancet* 線上刊出，Google Research 的技術部落格也在同日加註 `UPDATE` 說明此工作已完成同儕審查發表 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **日期** — **2026-10-08**。部落格頁面可見標示為 `Oct 08, 2026`；頁內 JSON-LD 結構化資料的 `datePublished` 為 `2026-10-08T22:30:00+00:00`、`dateModified` 為 `2026-10-08T22:30:00.588497+00:00`，另有 `article:published_time` 為 `2026-10-08` 的 meta 欄位；本文日期即取自這三處一致的頁面標示，未作推斷 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。*The Lancet* 摘要頁標示 `ARTICLES Online first October 08, 2026`，`citation_online_date` meta 為 `2026/10/08` [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。
- **官方入口** — [Study in The Lancet suggests AI could improve patient-physician relationships.](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)
- **來源狀態** — **本則不是單源**。除 Google 自家的兩個部落格頁與 AMIE 專案頁外，另有三個 Google 以外的入口可以回查：*The Lancet* 的論文摘要（公開可讀，全文付費）、同日刊出的獨立 Comment（*The Lancet* 的特約評論文章體例，作者為 Mahmud Omar 與 Girish N Nadkarni，頁面標示的通訊信箱網域為 `mountsinai.org`，首段公開可讀）、以及 ClinicalTrials.gov 的試驗登錄 `NCT06911398`（主辦機構為 BIDMC，合作方列 `Google LLC.`） [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract) [(ref: comment)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901763-0/abstract) [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。但獨立性有明確邊界，必須同時說明：論文經費聲明只有一行 `Funding: Alphabet.`，且 48 位作者中有 **33 位**掛名 Google Research（21 位）或 Google DeepMind（12 位），非 Google 掛名者為 BIDMC 12 位與 Harvard Medical School 3 位，另有一位（`Adam Rodman`）同時掛 Google Research 與 BIDMC [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。亦即這篇論文經過同儕審查、經費與單位揭露完整，但不是與廠商無關的獨立驗證。

**編輯：** Clarence

Google 在 2026-10-08 以一篇 288 個英文字的部落格，向一般讀者宣布 AMIE 的第一份真實臨床環境研究登上 *The Lancet*。這篇短文給了三個數字：98 位病人、安全準則下**零次中斷**、以及「AMIE 的鑑別診斷與醫師的最終診斷**相符 90%**」。逐項核對後，三個數字都能在原始資料裡找到對應，真正的落差在**它們各自的分母與定義**，而且對照組就在 Google 自己家裡 —— 同一天加註更新的 Google Research 技術部落格，在描述同一項結果時寫的是：AMIE 的最終診斷命中發生在**前七名鑑別診斷清單之內**，占 90%；若只看它排在**第一順位**的那一個診斷，命中率是 **56%**。面向一般讀者的那篇把「前七名之內」這個限定拿掉了，也沒有出現 56% 這個數字。同一組落差也出現在另外兩處：75% 的分母不是 98 位病人而是 44 份問卷，而論文摘要裡寫著安全監督者「注意到一次幻覺、並在五次互動中補充臨床資訊」—— 這句話在 Google 的兩個部落格頁上都找不到。

## 背景

1. **這一天在本案中的位置** — 2026-10-08 是 *The Lancet* 線上刊出日，也是 Google 兩個部落格頁同步動作的日子，但**不是**這項研究第一次公開。同一份研究的預印本早在 **2026-03-09** 就以 `arXiv:2603.08448` 投出（最新版 v3 為 2026-03-15），Google Research 的技術部落格首發日期為 **2026-03-11**，當天即公布了 90%、75% top-3 等數字；該頁在 2026-10-08 才加上一行 `UPDATE`，說明「自本文首次發布以來，這項工作已刊登於 *The Lancet*」 [(ref: arxiv)](https://arxiv.org/abs/2603.08448) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。也就是說，本則嚴格來說是**同一份結果的第二次發布**，差別在這一次有了同儕審查的背書與面向一般讀者的改寫。
2. **AMIE 是什麼，以及它在本研究中做什麼** — AMIE 是 Google 以大型語言模型為基礎的醫療對話研究系統，跨 Google Research、Google DeepMind、Google Platforms and Devices 與 Google for Health [(ref: amie)](https://sites.research.google/gr/amie/)。在本研究中，它做的**不是**診斷，而是**看診前的病史詢問**（history taking）：病人在門診約診前最多 5 天，透過安全網頁與 AMIE 進行純文字對話，系統產生逐字稿與摘要，在看診前交給該病人的基層照護醫師（primary care provider，PCP）參考 [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
3. **為何需要這種研究** — AMIE 先前的成績來自模擬情境。*The Lancet* 同日刊出的獨立 Comment 把這一點寫得很直接：AMIE 在文字門診中曾勝過基層照護醫師，`but its patients were patient actors`（但它的病人是標準化病人演員），而「在 AI 給出診斷或其他可據以行動的臨床產出**之後**，病人與臨床人員如何反應」這一塊的證據仍然稀少 [(ref: comment)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901763-0/abstract)。Google 自己的 AMIE 專案頁也用同一個邏輯說明為何要做前瞻研究：`Trust in clinical AI cannot be benchmarked into existence`（臨床 AI 的信任無法靠跑基準跑出來） [(ref: amie)](https://sites.research.google/gr/amie/)。
4. **這是一項什麼等級的研究** — *The Lancet* 論文標題與摘要都明寫 `prospective, single-centre, single-arm feasibility study`（前瞻、單一中心、單組的**可行性研究**） [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。ClinicalTrials.gov 的登錄把研究型態列為 `Observational`（觀察性），正式標題為 `A Prospective Cohort Study of the Articulate Medical Intelligence Explorer's Ability to Take an Initial Triage History From Patients Prior to an Urgent Care Visit`，並在詳細描述中寫明 `As this is a pilot study, the primary endpoint will be recruitment`（既然這是先導研究，主要終點將是收案），目標 100 至 200 人 [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。
5. **收案與時間線** — 試驗登錄的 `Study Start (Actual)` 為 **2025-04-02**、`Primary Completion (Actual)` 為 **2026-01-05**、`Study Completion (Actual)` 為 **2026-04-06**；登錄首次公開於 2025-04-04，最後更新張貼於 2026-04-20，`Last Verified` 為 2025-05，且 `No Results Posted`（登錄端未張貼結果） [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。*The Lancet* 摘要寫的收案期間為 `From April to November, 2025` [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。
6. **這是不是醫材** — 試驗登錄的文件資訊欄明寫 `Studies a U.S. FDA-Regulated Device Product: No`（本研究未涉及受美國食品藥物管理局 Food and Drug Administration，FDA 規管的裝置產品） [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。本研究走的是研究用途路徑，兩個部落格頁全文都沒有出現 FDA、法規或醫材許可相關字樣 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。

## 事實（可核對）

### 面向一般讀者的部落格寫了什麼

- **標題與結論句** — 標題為 `Study in The Lancet suggests AI could improve patient-physician relationships.`，結語為 `the findings suggest the potential for AI to enhance the patient-physician relationship and ease the strain on healthcare workers`。兩句都帶 `suggests`／`potential` 的保留語氣，開頭也寫了 `larger clinical trials are needed to assess patient-facing AI at scale` [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **三個數字** — `98 patients consulted AMIE`；`not a single conversation needed to be interrupted based on predefined safety criteria`；`clinicians reported that the AI summaries helped them prepare for visits in 75% of cases and influenced their approach to care in more than half`；`AMIE's differential diagnoses also matched the doctors' final diagnoses 90% of the time` [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **90% 那一句沒有任何保留語氣** — 相對於標題與結語的 `suggests`，這一句是直述句，沒有限定清單長度，也沒有說明「相符」如何定義 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **全文規模與結構** — 正文共 288 個英文字；全頁只出現兩個百分號（75% 與 90%）；**沒有任何上標註腳**（`<sup>` 元素數為 0），正文外連只有三個：BIDMC 官網、AMIE 專案頁，以及指向 *The Lancet* 的短網址 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **哪些詞完全沒有出現** — 以頁面可見文字逐詞計數：`feasibility`（可行性）0 次、`control`（對照）0 次、`top`（前幾名）0 次、`limitation`（限制）0 次、`hallucination`（幻覺）0 次、`Alphabet` 與 `fund`（經費）各 0 次、`FDA` 與 `device`（裝置）各 0 次；數字 `56`、`100`、`114` 亦各 0 次 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。研究設計的三個關鍵限定詞（可行性、單一中心、單組無對照）與經費揭露，在這一頁上都不存在。
- **一項關於 Google 自己的宣稱** — `As Google's first-ever publication in the main journal of The Lancet, this research marks a significant milestone.`（這是 Google 首次在 *The Lancet* 主刊發表）。此為 Google 自述，本文未另行核對 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。

### 同一天更新的自家技術部落格怎麼寫同一組數字

- **90% 的完整定義** — `AMIE successfully matched the final diagnosis within its top 7 diagnostic possibilities in 90% of cases.`（AMIE 在**前七個**診斷可能性之內命中最終診斷，占 90% 的病例）。緊接的下一句是：`Furthermore, the system accurately identified the final diagnosis as its single most likely diagnosis in 56% of all cases evaluated.`（在所有受評病例中，系統把最終診斷列為**最可能的單一診斷**者占 56%） [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **中間還有一個 75%** — 同頁另一處寫 `AMIE's DDx included the final diagnosis, per chart review 8 weeks post-encounter, in 90% of cases, with 75% top-3 accuracy`。DDx 為 `differential diagnosis`（鑑別診斷）。亦即這三個數字是同一條 top-k（前 k 名）曲線上的三個點：**前一名 56%、前三名 75%、前七名 90%** [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。預印本摘要同樣寫 `in 90% of cases, with 75% top-3 accuracy`，但**未**寫出清單長度為七，也**未**出現 56% 這個數字 —— `top 7` 與 56% 目前只見於技術部落格 [(ref: arxiv)](https://arxiv.org/abs/2603.08448) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **最終診斷怎麼來的** — 由看診後 **8 週**的病歷回顧（chart review）建立。另做了次族群分析：在 **46 位**最終診斷經檢驗、微生物、病理或影像等客觀方式確認的病人中，準確率維持；而在最終診斷**僅由醫師推定**（presumptive）的病例上，整體準確率反而更高 [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **與醫師對比的部分** — 三位未參與該次門診的臨床評估者以盲化、隨機方式評分，取三人中位數。結果為 AMIE 與基層照護醫師在鑑別診斷與處置計畫（management plan，Mx plan）的整體品質相近，鑑別診斷以及處置計畫的適當性與安全性都沒有顯著差異；但**基層照護醫師在處置計畫的實用性與成本效益上勝過 AMIE** [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。預印本摘要給了對應的 p 值：鑑別診斷 `p = 0.6`、處置適當性 `p = 0.1`、處置安全性 `p = 1.0`、實用性 `p = 0.003`、成本效益 `p = 0.004` [(ref: arxiv)](https://arxiv.org/abs/2603.08448)。
- **Google 自己寫的理由** — 技術部落格解釋這兩項落後是可預期的，因為 `AMIE did not have access to the patient's EHR, did not have the ability to perform a physical exam, or integrate multimodal user input`（AMIE 沒有電子病歷存取權、不能做理學檢查、也無法整合多模態輸入） [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **技術部落格自列的限制** — 其中一條與本則的宣傳語直接相關：`this study did not include controlled comparisons and therefore does not support quantitative claims on the efficacy of this intervention compared to a baseline workflow`（本研究未設對照比較，因此**不支持**關於本介入相較於既有工作流程之成效的量化宣稱）。另兩條為純文字介面無法涵蓋臨床照護的多模態性質，以及未窮盡探討健康識能、科技識能與聊天機器人使用經驗的影響 [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **這一頁同樣沒有的東西** — 以頁面可見文字逐詞計數：`hallucination` 0 次、`48%` 0 次、`114` 0 次、`FDA` 0 次、`regulat`（法規）0 次、`pregnan`（懷孕）0 次、`psychiatric`（精神科）0 次、`English`（英語）0 次；全頁百分號僅 4 次 [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。

### 回到 The Lancet 摘要與試驗登錄核對

- **書目與取用狀態** — Brodeur PG、Koshy JM、Palepu A 等 48 人，`Conversational diagnostic artificial intelligence in ambulatory primary care: a prospective feasibility study`，*The Lancet*，2026-10-08 線上先行，DOI `10.1016/S0140-6736(26)01535-7`，PMID `42849491`。摘要公開可讀，**全文為付費牆**（頁面寫 `Log in, subscribe or purchase for full access`），故本文所有引述僅限摘要與其他公開來源 [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。
- **到底有幾位病人** — 三個官方入口給的是三個不同的數字，並不矛盾，但指的是三件事：*The Lancet* 摘要寫 `114 patients were enrolled with 98 completing both the AMIE interaction and the PCP appointment`（114 人收案、98 人同時完成 AMIE 互動與門診）；技術部落格寫 `The study involved 100 adult patients who completed a pre-visit interaction with AMIE. Of these, 98 attended their scheduled ambulatory primary care appointment.`（100 人完成 AMIE 互動，其中 98 人出席門診）；試驗登錄的 `Enrollment (Actual)` 欄則填 **100** [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/) [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。亦即完整的漏斗是 **114 收案 → 100 完成 AMIE 對話 → 98 出席門診**。面向一般讀者的部落格把 98 寫成「與 AMIE 對話的人數」，與這條漏斗相比，實際與 AMIE 對話完成的是 100 人 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **零次中斷之外還發生了什麼** — *The Lancet* 摘要在 `Zero conversation safety stops were required` 的**下一句**寫著：`Safety supervisors noted one hallucination and added clinical information in five interactions.`（安全監督者注意到**一次幻覺**，並在**五次**互動中補充了臨床資訊） [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。試驗登錄的詳細描述也事先寫明，監督醫師會在通話結束時 `discuss with the patient and correct any errors, hallucinations, or problems with the AI`（與病人討論並更正 AI 的任何錯誤、幻覺或問題）—— 亦即「現場更正」本就是設計的一部分，而非意外 [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。Google 的兩個部落格頁都只寫了零次中斷 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **四條中斷準則** — 技術部落格列出觸發安全中斷的四個條件：對自己或他人有立即傷害之虞、病人因 AI 互動表現出顯著情緒困擾、監督者依對話內容判斷有臨床傷害之可能、病人明確要求結束。亦即「零次中斷」的意思是這四條都沒被觸發，不等於對話中沒有出錯 [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **75% 的分母是 44 不是 98** — *The Lancet* 摘要寫 `PCPs completed post-surveys in 60 of 98 cases, including 44 cases in which they reviewed the AMIE transcript before the visit. PCPs found AMIE helpful for visit preparation in 33 of 44 cases and reported that it might have changed their behaviour in 25 of 44 cases.`。33／44 正是 75.0%，25／44 為 56.8%（即「過半」）。但分母是**醫師既填了問卷、又在看診前讀過逐字稿**的那 44 次；基層照護醫師總共只回收了 60／98 份問卷。以全部 98 次門診為分母，33／98 約為 33.7% [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。面向一般讀者的部落格寫的是 `in 75% of cases`，未說明是哪一種 case [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **「影響了照護方式」與原文的語氣差距** — 摘要的用詞是 `might have changed their behaviour`（**可能**改變了他們的行為，醫師自評），部落格寫成 `influenced their approach to care`（影響了他們的照護方式） [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract) [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)。
- **對話品質的評分範圍，包含一個 48%** — 摘要寫 `AMIE's conversations were rated favourably in 87–100% of cases (17 criteria) by clinical evaluators, and 48–96% (16 criteria) by patients.`。臨床評估者的 17 項準則全部落在 87% 至 100%；**病人端 16 項準則的下緣是 48%**。摘要只給範圍，未逐項列出是哪一項落在 48%，而該資訊在付費全文中 [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。這個 48% 不出現在 Google 的任何一個部落格頁 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。
- **對話品質是主要終點，診斷準確率不是** — *The Lancet* 摘要列的主要終點只有三項：安全中斷次數、臨床評估者評定的對話品質、以及病人與醫師的問卷經驗 [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。試驗登錄把八項列為 `Primary Outcome Measures`，其中三項以標準化評分表評定對話品質：`General Medical Council Patient Questionnaire`（GMCPQ）、`Practical Assessment of Clinical Examination Skills`（PACES）、`Patient-Centered Communication Best Practice`（PCCBP），而 `Diagnostic accuracy`（比較 AMIE 的鑑別診斷與最終診斷）列在 `Secondary Outcome Measures` [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。面向一般讀者的部落格拿來當結尾的 90%，在研究設計上是**次要終點**。
- **那些診斷沒有進到診間** — 試驗登錄的詳細描述寫明，AMIE 產生的診斷與處置計畫 `will not be shared with the patient or physician, but will be generated after the fact and compared with the actual diagnosis and management plan`（不會提供給病人或醫師，而是事後產生並與實際診斷及處置計畫比較） [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。交給醫師的是病史逐字稿與摘要 [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract) [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。因此 90% 這個數字描述的是**離線比對的結果**，不是任何一位病人的照護實際採用過的判斷。
- **誰被排除在外** — 試驗登錄的排除條件包含：未滿 18 歲、電子病歷未列英語為主要語言、**就診原因與懷孕相關**、**就診原因為精神科問題**、以及初次建立照護關係或回診追蹤 [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。亦即這項「看診前先由 AI 問診」的可行性研究，事先排除了產科與精神科這兩類主訴。
- **樣本與整體就診人口的落差** — 技術部落格寫明，相較於同期該診所的 `1,452` 次急件門診，參與研究的病人**偏年輕**，因為該期間全部急件門診中有超過一半為 60 歲以上；性別與族裔分布則與整體相符 [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。作為粗略的參與規模概念：100 位參與者對照同期 1,452 **次**急件門診約為 6.9%，但分子是人數、分母是就診次數，兩者量綱不同，技術部落格未提供同期的不重複病人數。
- **經費** — *The Lancet* 摘要的經費欄只有一行：`Funding: Alphabet.` [(ref: lancet)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)。試驗登錄的主辦機構為 BIDMC、責任方為 BIDMC 的 Marc Cohen，合作方列 `Google LLC.` [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。
- **獨立 Comment 怎麼定位這項研究** — 同日刊出的 Comment 由 Mahmud Omar 與 Girish N Nadkarni 撰寫，可讀首段寫明他們要分三層檢視這項研究：診斷表現、病人與臨床人員的想法、以及模型做出診斷之後的安全性。全文為付費牆，本文未取得其餘段落 [(ref: comment)](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901763-0/abstract)。

## 本書庫解讀（評論）

- **一個數字的三種寫法，全部來自同一家公司** — 本則最值得記下的不是 Google 寫錯了什麼，而是**同一組結果在三個官方出口上被寫成三種強度**：預印本摘要寫「鑑別診斷清單含最終診斷者 90%，top-3 為 75%」；技術部落格補上清單長度為七、並主動給出前一名 56%；面向一般讀者的部落格只留下「與醫師最終診斷相符 90%」。每一步都沒有改動數值，但限定條件被逐層剝掉，最後留給讀者的印象是「AMIE 十次有九次診斷和醫師一樣」，而實際上「排第一名就對」的比例是 56%。要發現這件事不必打開付費全文，只要點進 Google 自己的技術部落格即可 —— 但那個連結不在面向一般讀者的那一頁上。
- **top-k 是醫療 AI 評估裡最容易被滑過去的量綱** — 「前七名之內命中」在鑑別診斷研究裡是常見且有意義的指標，因為臨床上醫師本來就會維持一份鑑別清單；問題不在用 top-7，而在**公開傳播時不說明 k 是多少**。k 愈大，命中率必然愈高，而一份七項的鑑別診斷清單對基層診間的決策價值，與一個明確的首選診斷差距極大。本書庫的建議是：任何「診斷準確率」宣稱，第一個要問的問題永遠是「這是 top 幾」。
- **分母換了，75% 的意思就換了** — 75% 的原始分母是 44 份「醫師既填了問卷、又在看診前讀過逐字稿」的回覆，而全部門診為 98 次、問卷回收為 60 次。回收率本身就是一個發現：**有 38 次門診的醫師根本沒回問卷**，而未回覆者是否就是覺得不太有用的那一群，無法從現有公開資料判斷。把 75% 寫成 `in 75% of cases` 而不說明是哪一種 case，會讓讀者以為四分之三的門診都受益；以全部門診為分母則約三分之一。
- **「零次中斷」是真的，但它回答的不是讀者以為的那個問題** — 四條中斷準則都是**高門檻**的事件：自傷傷人之虞、顯著情緒困擾、臨床傷害之可能、病人要求終止。零次代表這四件事都沒發生，這本身是有價值的安全訊號。但同一份摘要的下一句寫著監督者注意到一次幻覺、並在五次互動中補充臨床資訊，而試驗登錄更把「現場更正錯誤與幻覺」寫進設計。把這兩句一起讀，正確的結論是：**在每一場對話都有一位醫師全程在線的條件下，沒有發生需要緊急中止的事**。Google 的兩個部落格都只寫了前半句。
- **最該被宣傳的那句話，寫在 Google 自己的限制段裡** — 技術部落格明寫本研究未設對照比較，因此不支持關於本介入相較既有流程之成效的量化宣稱。而面向一般讀者的那一頁，標題就是「AI 可能改善醫病關係」。嚴格說這句話用了 `suggests`／`could`，並非量化宣稱，因此不構成與限制段的直接牴觸；但兩頁放在一起看，仍然呈現出一個方向一致的現象 —— **限定條件留在技術頁，結論句進到傳播頁**。
- **這項研究本身的品質，和它的宣傳品質是兩件事** — 必須把話說清楚：以醫療 AI 的真實世界證據而言，這是一份**少見地紮實**的研究。它事先登錄、公布排除條件、前瞻收案、設安全監督、用三套標準化評分表、以盲化隨機方式讓三位評估者對照醫師、承認樣本偏年輕、並主動報告自家系統在處置計畫實用性與成本效益上輸給醫師（`p = 0.003`、`p = 0.004`）。願意把自己輸的那一欄寫進技術部落格，與本書庫先前記錄過的多則「只給有利數字」的公告完全不同。本則批評的對象是那 288 個字的傳播改寫，不是這項研究。
- **醫療橋接** — 本則的題材是文字對話而非醫學影像，但這份研究示範的評估清單，正是影像 AI 目前最缺的；它把三件影像 AI 公告幾乎從不做的事做了出來。第一，**事先把次要終點登錄起來**，使得「診斷準確率」這類最適合拿來宣傳的數字，在設計上就被標明不是主要問題。第二，**把 top-k 曲線完整報出來**（56／75／90），而影像判讀模型的公告經常只報一個數字，不說它對應的是最高信心輸出、前幾名候選，還是任一命中。第三，**說明受測者沒有拿到什麼**（無電子病歷、無理學檢查、無多模態輸入），因此輸掉的那兩欄可以被正確解讀；影像模型的評估同樣高度受制於它看不看得到臨床資訊與先前檢查，而這一點很少被寫進成績旁邊。把這三件事搬到影像上並不需要新技術，只需要在報分數時一併交代分母、清單長度與模型可取得的脈絡。

## 產業／生態影響

- **可行性研究正在被當成里程碑宣傳，這會逐步拉低「臨床驗證」的語意** — 本研究的正式分類是 single-arm feasibility study（單組可行性研究），在證據階梯上屬於最前端。把它寫成「*The Lancet* 研究顯示 AI 可能改善醫病關係」在字面上站得住，但若這類改寫成為常態，醫療機構採購端會逐漸難以從公開語言分辨「已在真實門診跑過一次、沒出大事」與「已證實對照既有流程更好」。前者是本研究，後者需要的是 Google 自己承諾的後續隨機對照研究。
- **期刊發表正在成為科技公司的產品里程碑** — 公告裡 `Google's first-ever publication in the main journal of The Lancet` 這句話透露了論文在此扮演的角色：它既是科學成果，也是信任背書的取得。這不是壞事 —— 本書庫一貫主張「廠商的佐證是否能被你自己打開」是可區分的品質訊號，而本則確實給了可打開的摘要、可查的試驗登錄與開放的預印本，層級高於以編號引用的廠內未公開報告。但也要注意：論文由 Alphabet 出資、48 位作者中 33 位掛 Google，背書的獨立性與期刊的威望不是同一回事。
- **「人在線上」的監督模式短期內是部署的必要成本** — 本研究的安全結論成立於每一場對話都有一位醫師透過視訊與螢幕分享全程監看。這個設計在研究階段合理，但它同時也標出了規模化的瓶頸：若監督是安全的前提，那麼「AI 問診節省醫師時間」的經濟模型就必須先回答由誰監督。Google 技術部落格已提到正在探索非同步的監督流程，這是後續最值得追蹤的一條線。
- **試驗登錄正在成為核對廠商公告最有效的單一工具** — 本則的多項關鍵限定（診斷準確率是次要終點、AI 的診斷不交給醫師、排除產科與精神科主訴、未滿 18 歲與非英語者排除、非 FDA 規管裝置）全部來自 ClinicalTrials.gov 的公開登錄，而不是任何一份廠商文件。對台灣的醫院與研究單位而言，這是一個成本極低的動作：看到任何「某某 AI 在某某醫院完成臨床研究」的消息，先找出試驗編號，再去登錄頁對照主要終點與排除條件。

## 與書庫其他文章的關係

兩則都是廠商宣傳一篇數值本身正確的論文，落差都出在限定條件被留在原處，但被省略的東西種類不同：該則省略的是「這兩個百分比是論文為一位虛構典型病人以調整後模型推算的差異」，本則省略的是「90% 指的是七項鑑別診斷清單之內命中，排第一名的只有 56%」；兩則並讀可以看出同一種改寫手法在兩個不同量綱上的樣子 —— 一個換掉了受測對象，一個換掉了清單長度: [GE HealthCare 發布密西根大學 End-tidal Control 研究：新聞稿裡的 62.3% 是論文為「典型病人」建構的模型推算值，而出面肯定這項研究的 GE 高層是論文共同作者](2026-10-19-ge-healthcare-end-tidal-control-michigan-study.md)

同一家公司相隔十五天的兩則健康部落格，可查核程度差距很大：該則五個合作案裡只有一個報得出已完成的篩檢量，其餘用進行式帶過且無任何敏感度與特異度；本則有同儕審查論文、開放預印本與完整試驗登錄可以逐項回查，問題反而出在同一組數字在自家兩個頁面上被寫成兩種強度 —— 這說明「有沒有可查核物」與「傳播時有沒有保留限定條件」是兩道各自獨立的關卡: [Google 公布 MedGemma 全球落地案例：五個合作案裡只有一個報出已完成的篩檢量](2026-10-08-medgemma-global-deployment-claims.md)

該篇以 12.8 萬筆真實提問對照 58 個公開基準，指出臨床人員實際拿大型語言模型做的多半是文件工作、診斷只占 3.7%，而基準的題目組成對不上實際用途；本則正是少數真的把對話式模型放進門診流程、前瞻收案並事先登錄終點的研究，而它交給醫師的也恰好是病史摘要這類文件產出，AI 的診斷清單並未進入診間，兩篇並讀可以看出「離開基準、進到流程」之後真正被量到的是什麼: [臨床人員實際拿 LLM 做什麼？12.8 萬筆提問對照 58 個公開基準：文件工作占最多、診斷只占 3.7%，基準的題目組成對不上](../ai-papers/2026-10-13-clinician-llm-use-vs-benchmarks.md)

兩則是同一種改寫手法的兩個樣本：官方部落格給出一個百分比，而它的分母只存在於被連結的論文裡；本則的 90% 實為前七名清單命中率，該則的 75% 實為 20 組配對報告、每組三位評審共 60 次判斷中的 45 次，兩則並讀可以看出「官方頁有連結到論文」與「官方頁保留了限定條件」是兩回事: [OpenAI 公布以 AI 代理群解讀全腦 Perturb-seq 圖譜：公告寫「引用逾 700 篇」，它所連結的論文寫的是「711 倍」](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md)

本則的 90% 是前七名清單的命中率、排第一名的只有 56%，兩個數字都在 Google 自家的技術部落格裡；該則的「結塊慢 100 倍以上」與「6 到 9 倍」同樣分屬兩層官方文件，而該則又多了一層 —— 詳細版不是另一個頁面，而是同一頁上要點開才看得到的面板，六段利益揭露也只存在於那些面板裡: [Anthropic 公布 Claude 參與的六個藥物開發合作案：公告說抗體「結塊慢 100 倍以上」，技術報告寫明那是單一個孔的讀數，而判定成功的規格是看過結果之後才定的](2026-10-28-anthropic-drug-development-case-studies.md)

同一家公司相隔七天的兩則發布，可回查程度相差一整個層級：本則有同儕審查論文、開放預印本與試驗登錄可以逐項對照，爭點只在哪一個百分比被挑進標題；該則的正文裡 `peer`、`paper`、`arXiv`、`DOI` 命中數全部為零，唯一能回查的對象是一個公開資料庫條目。把兩則並讀可以看出「同一家公司的官方發布」不是一種均質的證據等級: [Google DeepMind 示範用 Antigravity 搜尋抗菌胜肽：「數天變成一次對話」「in hours」「數小時變成數分鐘」三種加速說法分屬三個官方位置，沒有一個附得出絕對數值；而那個候選分子在 UniProt 的名稱，證據欄寫的是 Google:ProtNLM](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

## 實務的啟發

- **看到診斷準確率，先問「這是 top 幾」** — 本則提供了一組現成的對照：同一個系統、同一批病例，前一名 56%、前三名 75%、前七名 90%。差距達 34 個百分點。任何沒有說明清單長度的「診斷相符率」，都應視為尚未說完。
- **看到百分比，先問分母是哪一群** — 本則的 75% 分母是 44 份特定條件下的問卷，不是 98 次門診。把同一個分子換上全部門診的分母，比例降到約三分之一。問法可以很簡單：「分子幾個、分母幾個」，而不是「百分之幾」。
- **把試驗編號當成閱讀廠商公告的第一個動作** — ClinicalTrials.gov 登錄頁是免費、結構化且事先寫下的，能在幾分鐘內回答三個最關鍵的問題：哪些是主要終點、哪些人被排除、研究型態是什麼。本則幾乎所有關鍵限定都來自這一頁。
- **「零不良事件」要配上事件定義才有意義** — 本則的零次中斷對應的是四條具體且高門檻的準則。評估任何 AI 工具的安全宣稱時，應要求對方列出觸發條件；沒有定義的「零事件」無法比較，也無法複製。
- **讀公告時，順手找一下同一家公司的技術版本** — 本則的關鍵限定（top 7、56%、未設對照）全部來自 Google 自家的研究部落格，不需要訂閱期刊。許多公司都同時維護面向一般讀者與面向研究者的兩套頁面，後者往往保留了被前者刪去的限定條件。
- **評估院內導入時，把「誰監督」寫進成本** — 本研究的安全結論建立在每場對話都有醫師全程在線。若要把類似流程搬進自家門診，監督人力是必須先算清楚的項目，否則研究條件與部署條件不對等，安全結論也就不能沿用。

## 後續追蹤

- Google 已宣布與 Included Health 合作一項全國性的隨機研究，用以評估對話式 AI 在真實虛擬照護流程中的表現 [(ref: amie)](https://sites.research.google/gr/amie/)。該研究若設有對照組，將可直接回答本研究明言無法回答的成效問題，值得追蹤其登錄編號與主要終點設計。
- *The Lancet* 全文為付費牆，本文的引述僅限公開摘要；病人端 16 項評分中落在 48% 的是哪一項、以及鑑別診斷清單的完整長度分布，均在全文中。若日後出現可公開取用的版本，可補充核對。
- 試驗登錄 `NCT06911398` 目前標示 `No Results Posted`，`Last Verified` 停在 2025-05。登錄端若補張貼結果，可與論文數字逐項對照。
- 本研究排除了懷孕相關與精神科主訴兩類就診原因 [(ref: ct)](https://clinicaltrials.gov/study/NCT06911398)。後續若有研究把這兩類納入，是檢驗「看診前 AI 問診」安全邊界最直接的一步。
- 技術部落格提到正在探索非同步的醫師監督流程 [(ref: gr)](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)。監督密度一旦降低，安全結論是否仍然成立，是這條產品線能否離開研究階段的關鍵。
- Google 在未來引用自家研究的傳播文稿中，是否會保留 top-k 的 k 值與問卷分母，可作為該公司宣傳品質的持續觀察指標。

## References

- `blog` — Google，[Study in The Lancet suggests AI could improve patient-physician relationships.](https://blog.google/innovation-and-ai/technology/health/amie-clinical-study-lancet/)（面向一般讀者的官方部落格，頁面標示 Oct 08, 2026，JSON-LD `datePublished` 為 2026-10-08T22:30:00+00:00）。底 URL：`https://blog.google/innovation-and-ai/technology/health/`
- `gr` — Google Research，[Exploring the feasibility of conversational diagnostic AI in a real-world clinical study](https://research.google/blog/exploring-the-feasibility-of-conversational-diagnostic-ai-in-a-real-world-clinical-study/)（技術部落格，頁面標示 March 11, 2026，頁首加註 `UPDATE • OCT 08, 2026`）。底 URL：`https://research.google/blog/`
- `lancet` — Brodeur PG、Koshy JM、Palepu A 等，[Conversational diagnostic artificial intelligence in ambulatory primary care: a prospective feasibility study](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901535-7/abstract)，*The Lancet*，2026-10-08 線上先行，DOI `10.1016/S0140-6736(26)01535-7`，PMID `42849491`（摘要公開可讀，全文付費）。底 URL：`https://www.thelancet.com/journals/lancet/`
- `comment` — Omar M、Nadkarni GN，[Conversational diagnostic AI in primary care: what happens after it speaks?](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736%2826%2901763-0/abstract)，*The Lancet* Comment，2026-10-08 線上先行（首段公開可讀，全文付費）。底 URL：`https://www.thelancet.com/journals/lancet/`
- `ct` — ClinicalTrials.gov，[NCT06911398：AMIE's Clinical Conversational Abilities in an Urgent Care Setting](https://clinicaltrials.gov/study/NCT06911398)（主辦機構 Beth Israel Deaconess Medical Center，合作方 Google LLC.）。底 URL：`https://clinicaltrials.gov/`
- `arxiv` — Brodeur P 等，[A prospective clinical feasibility study of a conversational diagnostic AI in an ambulatory primary care clinic](https://arxiv.org/abs/2603.08448)，arXiv:2603.08448（v1 2026-03-09，v3 2026-03-15；預印本，未經同儕審查）。底 URL：`https://arxiv.org/`
- `amie` — Google Research，[AMIE 專案頁](https://sites.research.google/gr/amie/)（Articulate Medical Intelligence Explorer）。底 URL：`https://sites.research.google/`

[Home](../) · [Industry Watch](./)
