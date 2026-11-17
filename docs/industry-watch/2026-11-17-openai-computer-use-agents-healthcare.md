---
parent: Industry Watch
nav_order: 1
title: "API 到不了就改用點擊：OpenAI 醫療 computer use 解析"
category: industry-watch
date: 2026-11-17
tags: [OpenAI, computer-use-agents, ChatGPT-for-Healthcare, ChatGPT-for-Clinicians, EHR, prior-authorization, HealthAdminBench, GPT-6-Astra, GPT-6-Luna, clinical-workflow, administrative-workflow, HIPAA, audit-log, CVS-Health, Cigna, Abridge, Ambience]
catalog_id: "openai:computer-use-agents-healthcare-2026-11-16"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.2"
source:
  orgs:
    - "OpenAI"
  event: "OpenAI 發布醫療場景的 computer-use agents，公布 GPT-6 Astra 在 EHR 收件匣任務上的臨床安全與有用性評分、GPT-6 Luna 在 HealthAdminBench 上的成績與每題成本，並列出 CVS Health、Cigna Healthcare、Abridge、Ambience 四家機構的開發與部署情形"
  event_date: "2026-11-16"
  official_url: "https://openai.com/index/advancing-computer-use-for-healthcare-teams/"
  single_source: false
  single_org: true
related_articles:
  - path: "2026-10-07-openai-gpt-6-1-sol-launch.md"
    relation: "同一家公司談便宜型號接得住多少工作的兩則，揭露方式剛好相反：該則只給相對成本比而不給絕對分數，本則給了 GPT-6 Luna 的絕對分數 91.8% 與每題 8.5 美分，卻沒說它跑在評測的哪一種觀察模式下"
  - path: "2026-11-02-microsoft-mai-dxo-sdbench-sequential-diagnosis.md"
    relation: "兩則都把成本當成評測裡與準確率並列的一軸：該則是逐步問診時每個檢查的花費，本則是行政流程每題 8.5 美分；差別在該則的成本與準確率出自同一個公開評測，本則的成本只出現在供應商的公告句裡"
  - path: "2026-11-05-google-health-ai-evaluation-framework.md"
    relation: "該則整理的健康 AI 評估框架主張門檻由各團隊自訂，本則正是一份照那類方法做出來的評估：醫師以五點量表評有用性、以是否可能造成病人傷害評安全性，而公告同樣沒有給任何可供比較的門檻或對照組"
refs:
  cua:
    title: "Advancing computer-use agents for healthcare teams（OpenAI 官方公告，2026-11-16）"
    url: "https://openai.com/index/advancing-computer-use-for-healthcare-teams/"
  healthcare:
    title: "More ways to move care forward with ChatGPT for Healthcare（OpenAI 官方公告，2026-11-16）"
    url: "https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/"
  habench:
    title: "HealthAdminBench v1.0 公開榜與資料（Stanford University／Kinetic Systems／Stanford Healthcare）"
    url: "https://som-shahlab.github.io/health-admin-bench-website/"
  agentkit:
    title: "CVS Health Agent Kit（公告所指向的開源程式庫）"
    url: "https://github.com/cvs-health/cua-agent-kit"
---

[Home](../) · [Industry Watch](./)

# API 到不了就改用點擊：OpenAI 醫療 computer use 解析

## 來源

- 組織／產品：OpenAI — 醫療場景的 computer-use agents（以點擊、輸入與切換應用程式的方式操作既有軟體的代理程式），取用管道為 OpenAI API、ChatGPT for Healthcare 與 ChatGPT for Clinicians。
- 事件：公布醫療情境的模型評估結果（臨床安全性、有用性、行政任務成績與每題成本），並列出四家醫療機構的開發與部署情形。
- 日期：2026-11-16（公告頁首可見文字為 `November 16, 2026`；該頁無 JSON-LD、無 `article:published_time`，頁內三個 `<time>` 元素全部屬於文末 Keep reading 卡片，故另以 openai.com 新聞列表頁標示的同一日期互為佐證，未推斷）
- 官方入口：[Advancing computer-use agents for healthcare teams](https://openai.com/index/advancing-computer-use-for-healthcare-teams/)
- 其他官方頁面：[More ways to move care forward with ChatGPT for Healthcare](https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/)（同日發布的配套公告，本文用它核對取用條件與 ChatGPT for Healthcare 的其餘兩項更新）。
- 可獨立查核的第三方來源：[HealthAdminBench v1.0 公開榜](https://som-shahlab.github.io/health-admin-bench-website/)（Stanford University、Kinetic Systems 與 Stanford Healthcare 共同發布，含完整題目與逐筆成績資料）。本文用它核對公告所引用的評測本身，但公告宣稱的兩個分數並未出現在該榜上，說明見證據邊界一節。
- **評估數字為單一組織自報**：臨床安全性、有用性與行政任務成績全部由 OpenAI 自行發布，無獨立第三方複現；四家機構的部署敘述與兩段引言亦刊載於 OpenAI 自己的頁面。相關限定條件集中列在後段的證據邊界一節。

**編輯：** Clarence

OpenAI 在 2026-11-16 發布醫療場景的 computer-use agents [(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/)。公告描述的作法是：代理程式以「clicking, typing, and moving between applications」的方式，在醫療團隊既有的軟體裡完成多步驟流程 —— 也就是走使用者介面，而不是走系統介接。公告開宗明義給的理由是醫療資訊系統彼此割裂：臨床醫師建議做 MRI 時，保險方需要的資料就在病人的病歷裡，但仍得由團隊成員手動取出、再輸入到另一個入口網站才能完成事前授權（prior authorization）。同日另一份配套公告把這項能力與改良過的 trusted clinical search、以及逾二十個新的醫療外掛並列為 ChatGPT for Healthcare 的三項更新 [(ref: healthcare)](https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/)。對臨床與研究工作流程來說，這則發布的意義不在模型變強，而在**導入位置改變**：過去要讓 AI 接上 EHR（Electronic Health Record，電子病歷系統）或保險方入口，前提是對方開放 API；這條路線主張連沒有 API 的系統也能接，代價是把代理程式放進人類原本操作的那個畫面上。

## 背景

- **2026-10-07** — OpenAI 發布 GPT-6.1 Sol，官方標題句點名的三個領域之一即為 computer use；該則只給相對成本比，未給該領域的絕對分數（見文末關聯段）。
- **2026-11-16（本則事件）** — OpenAI 同日發布兩份公告：`Advancing computer-use agents for healthcare teams` 公布醫療情境的評估結果與合作機構，`More ways to move care forward with ChatGPT for Healthcare` 把它放進產品面的三項更新之一。
- **公告發布時的取用狀態** — 兩份公告都寫明這項能力「available today」，而非預告或候補名單；公告頁未出現任何 `waitlist`、`beta` 或 `pilot program` 的字樣（`pilot` 全文僅一次，且用於描述合作機構的試行）。

本則無配圖。公告頁的示意影像與示範影片為 OpenAI 與各合作機構的自有素材，不重製；本文可核對的數值已以文字與表格完整呈現。

## 代理程式實際做的事（事實）

公告以一個合成病人資料（`synthetic patient data`）的示範說明整條流程 [(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#from-a-patients-message-to-an-mri-authorization-request)：

- 病人傳訊息給臨床醫師，主訴下背痛。
- 代理程式在 EHR 中調閱該病人的就診紀錄、物理治療紀錄與既往影像。
- 代理程式草擬 MRI 醫囑、一份就診紀錄（encounter note），以及一則回覆病人的訊息，交由臨床醫師審閱。
- 代理程式再以同一批紀錄，在保險方的入口網站上準備事前授權申請，交由授權專員審閱。

兩個環節都以「交人審閱」作結，公告未描述任何由代理程式自行送出的情境。公告列出的適用範圍為事前授權申請、轉診（referrals）、出院規劃（discharge planning）與就診之間的追蹤聯繫（outreach between visits）。

## 官方自報的臨床評估（事實）

- **受測模型與任務** — 公告評估的是 GPT-6 Astra，任務為臨床醫師在 EHR 收件匣（EHR inbox）中處理的工作，由醫師參與設計，同時測試「對縱向病人脈絡的臨床推理」與「複雜介面的操作」[(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#evaluating-helpfulness-safety-and-cost)。審查者同時檢視模型的操作軌跡與它產出的紀錄、醫囑與病人訊息。
- **臨床安全性** — 判定方式是評估模型產出中的錯誤、遺漏或操作是否「可能合理地導致病人傷害」（`could plausibly lead to patient harm`）。結果為**325 件受審任務中有 99% 被評為安全**。
- **有用性** — 醫師以五點量表評分，**646 次評估中有 93% 選了「very helpful」或「extremely helpful」**。
- **公告舉出的收件匣工作例** — ibuprofen 劑量、PSA（prostate-specific antigen，攝護腺特異抗原）數值偏高、digoxin 續領三類。

## 行政任務成績與成本（事實）

公告引用 HealthAdminBench，並稱之為「an independent benchmark from Stanford researchers」[(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#evaluating-helpfulness-safety-and-cost)。公告所報的數字如下：

| 模型 | 公告所報成績 | 每題成本 | 公告寫法 |
|---|---|---|---|
| GPT-6 Astra | 可得 rubric points 的 94.3% | 未揭露 | `earned 94.3% of available rubric points` |
| GPT-6 Luna | 可得 rubric points 的 91.8% | 8.5 美分 | `despite costing 98% less at 8.5 cents per task` |

- 兩者差距為 2.5 個百分點（由本文代為計算）。
- 公告寫明兩個模型都在 maximum reasoning effort 下受測。
- 公告未給 GPT-6 Astra 的每題成本；若以「便宜 98%」反推，Astra 約為 Luna 的 50 倍、每題約 4.25 美元（由本文代為計算；98% 為概數，反推值僅能視為量級）。
- 行政任務的範圍，公告列為事前授權、申覆（appeals）與醫療器材訂購（medical equipment orders）。

HealthAdminBench 本身的公開資料可以核對到：該評測為 v1.0，作者群來自 Stanford University、Kinetic Systems 與 Stanford Healthcare（通訊列最末為 Nigam Shah），題庫 135 題、1,698 個子項、4 個 GUI 環境，三個工作領域為 Prior Authorization 60 題、Durable Medical Equipment 15 題、Appeals & Denials 60 題（合計 135，由本文代為加總）[(ref: habench)](https://som-shahlab.github.io/health-admin-bench-website/)。該站同時提供論文與程式庫連結。公告所報的兩個分數與該榜的對應關係，見證據邊界一節。

## 四家機構的開發與部署（事實）

公告具名四家機構 [(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#developing-computer-use-with-healthcare-organizations)：

- **CVS Health — 已在生產環境運行** — 用於跨臨床系統的重複性工作，包括寄送文件、處理轉診與支援專科會診；公告寫明代理程式操作既有應用程式，是為了完成「APIs do not fully support」的步驟。公告舉兩個生產流程：一個代理程式在一個週末內清掉積壓數月的文件寄送工作，另一個每天處理數萬件會診的系統操作步驟。該公司以驗證檢查與人工監督搭配，並以截圖與操作紀錄核對代理程式的動作與應用程式狀態。公告並稱其將以 OpenAI Agents SDK 建置的 Agent Kit 開源 [(ref: agentkit)](https://github.com/cvs-health/cua-agent-kit)。引言出自工程執行總監 Lagan Khare。資料留在 CVS Health 企業控管的基礎設施內，生產資料不用於訓練基礎模型。
- **Abridge — 開發中，住院情境為規劃階段** — 以臨床對話為基礎，加上 EHR 資訊與護理師、醫師的脈絡，協助跨應用程式執行照護計畫，包含沒有 API 的系統。公告舉的例子是臨床醫師請 Abridge Assistant 協助解決病人的出院障礙，由多個代理程式同時處理用藥取得與居家照護協調，並在需要臨床判斷時把醫師拉回決策。公告對住院情境用的詞是 `planned`。
- **Cigna Healthcare — 已部署** — 屬於 The Cigna Group 與 OpenAI 更大範圍合作的一部分，用於把跨系統的給付與保障、醫療提供者、預約與過往互動等資訊彙整給照護團隊。公告寫明在此之前，個案管理師需要操作超過十個獨立的臨床與行政系統才能蒐齊這些脈絡。引言出自資訊長 Madhu Nutakki，稱「從概念到部署不到八週」。
- **Ambience — 示範可治理性** — 針對「每一個動作都要可控、可稽核」這個前提建置額外控制項。示範內容是依病歷證據在保險方網站上準備事前授權申請；當病歷記載模稜兩可時，代理程式會停下來詢問臨床醫師，等待核准後才送出。醫療體系可設定代理程式能執行哪些動作、隨時暫停，並取得逐步操作紀錄供稽核。

公告另列出五家以代理程式切入照護流程的新創：Assort、Bunkerhill、Forus、Gravity、Tennr。

## 資料控管與取用條件（事實）

- **控管機制** — ChatGPT for Healthcare 提供角色為基礎的存取控制與稽核紀錄；機構可在流程中加入審查與核准步驟，並設定代理程式可使用的應用程式與環境，將其存取範圍限縮到該任務所需的紀錄與動作。機構資料不用於訓練 OpenAI 的基礎模型 [(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#patient-data-security-and-agent-controls)。
- **HIPAA 條件** — HIPAA 指美國的 Health Insurance Portability and Accountability Act（健康保險可攜與責任法）。涉及受保護健康資訊（protected health information）的流程，機構必須使用其與 OpenAI 簽訂的 Business Associate Agreement（BAA，業務夥伴協議）所涵蓋的合格服務，並套用指定的安全與保存設定；配套公告另要求把這些保護措施延伸到所連接的系統 [(ref: healthcare)](https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/)。
- **取用管道** — 公告寫明這項能力當日起可在 ChatGPT for Healthcare、ChatGPT for Clinicians 與 OpenAI API 使用；既有客戶需由工作區管理員在 ChatGPT Work 與 Codex 中啟用 [(ref: cua)](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#get-started-with-computer-use-agents)。
- **個別臨床醫師的條件** — ChatGPT for Clinicians 對**美國境內通過資格驗證的臨床醫師**免費，用於查閱醫學證據與準備臨床文件 [(ref: healthcare)](https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/)。
- **同日的其餘兩項更新** — 配套公告另稱改良了 trusted clinical search 找尋、評估與引用醫學證據的方式，並新增逾二十個醫療外掛（該頁逐項列出 21 個名稱，由本文代為計數），全部於當日在 ChatGPT for Healthcare 可用。

## 證據邊界（事實）

上列評估數字全部由 OpenAI 自行發布。下列限定條件集中列在這裡，供引用時一併帶上：

- **公告所報的兩個分數不在 HealthAdminBench 的公開榜上** — 該榜標示「5 MODELS EVALUATED」，榜上七列為五個模型加兩種代理框架設定，其中 OpenAI 最新的型號是 GPT-5.4；`GPT-6`、`Astra`、`Luna` 在該站全文命中皆為 0 [(ref: habench)](https://som-shahlab.github.io/health-admin-bench-website/)。因此 94.3% 與 91.8% 屬於供應商在第三方題庫上的自測結果，不是該評測團隊發布的成績，外部目前無法在該榜上核對。
- **公告引用的指標與該榜的頭條指標不是同一個** — 該站提供兩種指標：`Score` 與 `Subtask Score (score / max_score)`。公告寫的「rubric points 的百分比」對應的是後者，而該榜預設檢視（提示 `Task Description`、觀察模式 `Screenshot`）列出的 `SCORE` 最高僅 36.3%（Claude Opus 4.6 CUA），最低 5.9%（GPT-5.4）；把觀察模式切到 `Axtree` 後最高為 51.9%。兩種指標數量級差距很大，不可互相換算。
- **該指標對設定極度敏感，而公告未說明設定** — 依該站公布的逐筆 `score`／`max_score` 紀錄加總（由本文代為計算），同一個 GPT-5.4 在同一組提示設定下，subtask 百分比在 `Axtree` 觀察模式為 84.6%、在 `Screenshot` 為 43.5%；其任務級 `Score` 則分別為 32.6% 與 5.9%。公告只寫明兩個模型都在 maximum reasoning effort 下受測，未說明觀察模式與提示策略，因此 94.3% 這個數字落在什麼條件下取得，外部無從判斷。
- **臨床安全性與有用性的分母不同，且未說明兩者關係** — 安全性為 325 件受審任務，有用性為 646 次評估；公告未說明這 646 次評估對應多少件任務、由多少位醫師做出，也未說明一件任務是否被多人重複評分。
- **兩項指標的判定方式寬嚴不同** — 安全性是二分判定（是否可能合理導致病人傷害），有用性是五點量表取前兩級合計。兩者都未揭露評分者人數、資歷分布、專科分布或評分者間一致性。
- **沒有對照組，也沒有人類基準** — 公告未提供同一批任務在不使用代理程式時的結果，也未提供人類基準。全文 `baseline` 命中為 0。
- **未通過的案例沒有內容** — 325 件中 1% 未被評為安全、646 次中 7% 未達前兩級，公告未描述這些案例屬於哪一類錯誤。對要評估風險的單位來說，失敗模式比通過率更關鍵，而這部分未公開。
- **示範使用的是合成資料** — MRI 事前授權那段示範明寫 `synthetic patient data`，不是真實病歷上的結果。
- **部署成效只有敘述，沒有可核對的量測** — CVS Health 的「一個週末清掉積壓數月的文件寄送」「每天數萬件會診」未附時間、件數定義、錯誤率或前後對照；Cigna Healthcare 的「不到八週從概念到部署」出自該公司資訊長的引言；Abridge 的住院情境寫明仍是 `planned`。四段敘述皆刊載於供應商自己的公告頁。
- **全文沒有任何醫材法規或臨床研究的字樣** — `FDA`、`study`、`trial`、`peer`、`arXiv` 在公告中命中皆為 0。這是一則產品與評估的發布，不含任何醫療器材法規狀態的宣稱，亦未聲稱經過臨床驗證。
- **配套公告的 clinical search 改善只給方向不給數值** — 該頁寫在一次盲測中、逾 1,300 次審閱裡，醫師對更新後的體驗在所評估的八個維度上評分都更高，但未給任何分數、差距或分母，亦未列出八個維度的完整清單（該句僅舉出 factual correctness、safety、actionability、source authoritativeness 四項）[(ref: healthcare)](https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/)。
- **發布日期的取得方式** — 公告頁無 JSON-LD、無 `article:published_time`，頁內三個 `<time>` 元素全部屬於文末 Keep reading 的三張卡片。本文採用的 2026-11-16 取自頁首可見文字與 openai.com 新聞列表頁兩處，未推斷、未以取得當日日期代替。

## 本書庫解讀（評論）

- **這則發布真正改變的是導入位置，不是模型能力** — 過去醫療 AI 要接進日常流程，門檻通常卡在對方系統有沒有開放介接；沒有 API 就只能等廠商、等標案、等版本。公告把路線換成操作使用者介面：既然人類是靠點擊完成這些步驟，代理程式也照樣點。CVS Health 那句「完成 API 無法完全支援的步驟」是這整則發布最有資訊量的一句話 —— 它說明這不是效能最佳化，而是繞過介接談判的一條路。這條路線的代價也在同一處：介面一改版、欄位一搬家，流程就可能默默失效，而這種失效不會像 API 回傳錯誤那樣明顯。
- **事前授權與申覆被選為主戰場，是合理的切入點** — 公告點名的流程 —— 事前授權、申覆、轉診、出院規劃 —— 共同點是高量、規則化、跨系統、且目前大量佔用臨床與行政人力，同時錯了也還有人工覆核這一層。相較於診斷或治療建議，這類工作的監理暴露小得多，這也解釋了為什麼全文沒有任何 FDA 字樣：這些流程本來就不落在醫材法規的範圍內。對醫療機構而言，這代表這類工具可能在完全沒有法規審查的情況下進入院內流程，院內治理因此必須自己補上。
- **第三方題庫上的自測成績，價值介於「廠商自報」與「獨立驗證」之間** — 公告選擇在一個公開、可下載、有論文的題庫上報分數，這比只給內部評測好；但分數不在該題庫的公開榜上，指標又選了比頭條指標寬鬆的那一個，而該指標在該題庫自己的資料裡會隨觀察模式在 43.5% 與 84.6% 之間擺盪。本書庫的建議是：引用 94.3% 時一律連同「供應商自測、未標示觀察模式與提示策略、採 rubric point 比例而非任務完成率」一起寫；只寫數字會讓讀者誤以為這是一個已完成的任務成功率。
- **99% 安全與 93% 有用這兩個數字，目前只能當作方向** — 把安全性定義成「是否可能合理導致病人傷害」並由審查者判定，方向是對的：它量的是後果而不是文字相似度。但沒有對照組、沒有人類基準、兩個指標分母不同、失敗案例不揭露，使得這兩個數字無法回答任何一個部署前會被問到的問題 —— 那 1% 是什麼、在哪種病人身上出現、人工覆核攔不攔得住。這一點與本庫先前整理過的健康 AI 評估框架所指出的缺口完全一致：方法有了，門檻與對照仍然缺席。
- **Ambience 那段的「遇到模稜兩可就停下來問」，比任何分數都更接近可部署的形狀** — 在醫療流程裡，代理程式的價值上限不是它能做多少，而是它知不知道何時該停。把「病歷記載不明確時停下、等核准才送出」寫成產品行為，再配上可設定的動作白名單、隨時暫停與逐步操作紀錄，這才是院內資安與醫品單位真正會審查的那一層。值得注意的是，這段控制項是由合作廠商自行建置的，不是平台預設提供的能力。

## 產業影響

- **介接談判的籌碼改變** — 若操作介面這條路線可行，EHR 與保險方系統的 API 開放程度就不再是 AI 導入的唯一瓶頸。這會同時影響兩邊：導入方多了一條不必等對方的路，而系統供應商對「誰能在我的畫面上自動操作」這件事會開始有立場，條款與偵測機制可以預期會跟上。
- **行政端先於臨床端落地的趨勢更明確** — 本則公告具名的生產環境案例全部落在行政流程（文件寄送、轉診、會診步驟、事前授權），臨床端仍停在草擬後交人審閱。這與本書庫近月追蹤到的其他發布一致：醫療 AI 的實際收入與部署正集中在不需醫材法規許可的那一側。
- **成本開始被當成評測的一軸公布** — 公告把每題 8.5 美分與成績並列，意味著供應商預期買方會以「每件行政工作多少錢」來比價。對高量流程而言這是合理的比價單位，但前提是分子分母都有定義；目前只有便宜那一端給了數字。
- **稽核紀錄成為產品規格** — 角色存取控制、逐步操作紀錄、截圖與動作紀錄被寫進公告正文而非附註，顯示這類能力在醫療場域已從加分項變成入場條件。

## 與書庫其他文章的關係

同一家公司談便宜型號接得住多少工作的兩則，揭露方式剛好相反：該則只給相對成本比而不給絕對分數，本則給了 GPT-6 Luna 的絕對分數 91.8% 與每題 8.5 美分，卻沒說它跑在評測的哪一種觀察模式下: [OpenAI 發布 GPT-6.1 Sol：標準輸入／輸出價格為 GPT-6 Astra 的 1/5；科學研究評測仍由 Astra 以 68.1% 居首](2026-10-07-openai-gpt-6-1-sol-launch.md)

兩則都把成本當成評測裡與準確率並列的一軸：該則是逐步問診時每個檢查的花費，本則是行政流程每題 8.5 美分；差別在該則的成本與準確率出自同一個公開評測，本則的成本只出現在供應商的公告句裡: [把診斷評估改成逐步問診並計成本：SDBench 與 MAI-DxO 解析](2026-11-02-microsoft-mai-dxo-sdbench-sequential-diagnosis.md)

該則整理的健康 AI 評估框架主張門檻由各團隊自訂，本則正是一份照那類方法做出來的評估：醫師以五點量表評有用性、以是否可能造成病人傷害評安全性，而公告同樣沒有給任何可供比較的門檻或對照組: [給了框架不給門檻：Google 健康 AI 評估三法十七維解讀](2026-11-05-google-health-ai-evaluation-framework.md)

## 實務的啟發

- **把「代理程式能不能操作我們的系統」與「我們允不允許」分開討論** — 這條路線的技術前提是畫面可被操作，而院內的決定權在於要不要開放。建議在評估前先盤點哪些系統的操作會留下不可逆後果（送出申請、更改排程、寄出文件），對這些系統一律要求人工核准步驟，而不是以代理程式的成績高低作為放行依據。
- **要求供應商說明評測的觀察模式與提示策略，再比較分數** — 本則顯示同一個模型在同一題庫上，僅因觀察模式不同就能差上一倍。採購或技術評估時，應把「哪一版題庫、哪一種觀察模式、哪一種提示策略、評的是任務完成率還是 rubric point 比例」列為必填欄位；缺其中任何一項，分數不具可比性。
- **把稽核紀錄的欄位需求寫進導入條件** — 公告提到的截圖、逐步操作紀錄與動作紀錄，是事後重建流程的唯一依據。導入前應確認這些紀錄能否匯出、保存多久、是否涵蓋代理程式讀取了哪些病人紀錄；研究用途上若無法取得完整軌跡，等同於放棄該次作業的可重現性。
- **介面變更要納入維運計畫** — 操作使用者介面的流程會因對方改版而靜默失效。建議對每條上線流程設定定期的回歸測試樣本與失敗告警，而不是等使用者回報；這與傳統 API 介接的維運假設不同，需要另行編列人力。
- **先量自家的失敗模式，不要沿用公告的通過率** — 公告未揭露未通過案例的內容。可行的作法是選一條量大但後果可逆的流程（例如轉診資料彙整），以人工全覆核跑一段期間，自行統計錯誤類型與攔截率，再決定要不要降低覆核密度。

## 後續追蹤

- HealthAdminBench 的公開榜是否會納入 GPT-6 Astra 與 GPT-6 Luna，以及該團隊自行量測的成績與供應商自測是否一致。
- OpenAI 是否補充 94.3% 與 91.8% 所採用的觀察模式、提示策略與題庫版本。
- 325 件任務中未被評為安全的案例、646 次評估中未達前兩級的案例，是否會有分類揭露。
- GPT-6 Astra 的每題成本是否公布，使 98% 的成本差距可被核對。
- CVS Health 的 Agent Kit 開源後，其驗證檢查與人工監督的實作細節是否可供外部檢視。
- Abridge 規劃中的住院情境是否進入生產環境，以及是否有前後對照的成效資料。
- EHR 與保險方系統的供應商對「由代理程式操作其使用者介面」的條款與偵測機制如何回應。
- 台灣的醫院在導入這類跨系統操作的代理程式時，如何對應既有的資訊系統驗證、個資保護與病歷稽核要求。

## References

- `cua` — Advancing computer-use agents for healthcare teams（OpenAI 官方公告，2026-11-16，含示範流程、臨床評估、HealthAdminBench 成績與成本、四家機構的部署敘述、資料控管與取用條件）  
  <https://openai.com/index/advancing-computer-use-for-healthcare-teams/>  
  深鏈：[示範流程](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#from-a-patients-message-to-an-mri-authorization-request)、[評估與成本](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#evaluating-helpfulness-safety-and-cost)、[合作機構](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#developing-computer-use-with-healthcare-organizations)、[資料控管](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#patient-data-security-and-agent-controls)、[取用方式](https://openai.com/index/advancing-computer-use-for-healthcare-teams/#get-started-with-computer-use-agents)
- `healthcare` — More ways to move care forward with ChatGPT for Healthcare（OpenAI 官方公告，2026-11-16，含三項更新、外掛清單、clinical search 盲測敘述與取用條件）  
  <https://openai.com/index/more-ways-to-move-care-forward-with-chatgpt-for-healthcare/>
- `habench` — HealthAdminBench v1.0 公開榜與資料（Stanford University／Kinetic Systems／Stanford Healthcare；含作者群、題庫規模、兩種指標與逐筆成績資料）  
  <https://som-shahlab.github.io/health-admin-bench-website/>
- `agentkit` — CVS Health Agent Kit（公告所指向的開源程式庫；本文未檢視其程式內容）  
  <https://github.com/cvs-health/cua-agent-kit>

[Home](../) · [Industry Watch](./)
