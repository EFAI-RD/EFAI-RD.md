---
title: "Microsoft 說開源是為了重現，兩份資料都要另外申請"
category: industry-watch
date: 2026-11-02
updated: 2026-11-02
tags: [Microsoft, Microsoft-AI, MAI-DxO, SDBench, sequential-diagnosis, diagnostic-reasoning, benchmark, NEJM-CPC, MIMIC-IV-ED, LLM-as-judge, cost-accuracy-tradeoff, clinical-workflow]
catalog_id: "microsoft:mai-dxo-sdbench-sequential-diagnosis-2026-10-22"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.0"
source:
  orgs:
    - "Microsoft AI"
  event: "發布公告 Building Medical Superintelligence，說明 Sequential Diagnosis Benchmark（SDBench）與 Microsoft AI Diagnostic Orchestrator（MAI-DxO），同日研究論文於 Science 刊出"
  event_date: "2026-10-22"
  official_url: "https://microsoft.ai/news/building-medical-superintelligence/"
related_articles:
  - path: "2026-10-20-google-amie-lancet-primary-care-feasibility.md"
    relation: "兩則都是大廠宣傳一套自家診斷 AI 勝過醫師，而關鍵的限定條件被留在被連結的論文裡：該則的 90% 實為前七名清單命中、排第一名只有 56%；本則的「準確率」是一個大型語言模型評分 4 到 5 級的比例，而被比下去的醫師是單獨作業、只能讀文字的一般科醫師"
  - path: "2026-10-22-openai-distributed-agents-perturb-seq-atlas.md"
    relation: "兩則都是官方公告與它所連結的論文對同一件事給出不同寫法，但方向相反：該則是公告把「711 倍」寫成「逾 700 篇」即把倍數寫成絕對數，本則是公告把分屬四個運作點的準確率與成本併成一句話，兩個都無法只看公告還原"
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "兩則的核心都是「評分的人與被評分的系統出自同一方」：該則的成功規格依技術報告自述是在看過結果之後才定的，本則則是 benchmark、Gatekeeper、Judge 與受測系統 MAI-DxO 全部由同一個團隊設計，論文的利益揭露列出全體作者皆為 Microsoft 員工並持有股權"
  - path: "../ai-basics/multi-agent-llm.md"
    relation: "該篇說明多代理編排的概念基礎與拓撲選擇，本則是這套編排在診斷場景的一個具體量測：論文自述跨各家模型平均讓 CPC 案例準確率比最小提示基線高 7.9 個百分點、ED 案例高 4.4 個百分點，可以當作「編排本身值多少」的一組有分母的數字"
refs:
  mai:
    title: "Microsoft AI：Building Medical Superintelligence（官方公告，2026-10-22）"
    url: "https://microsoft.ai/news/building-medical-superintelligence/"
  science:
    title: "Nori H. et al., Sequential diagnosis with language models, Science 394(6822):423-428（2026-10-22，FREE ACCESS）"
    url: "https://www.science.org/doi/10.1126/science.aeh7930"
  sdbench:
    title: "SDBench — Sequential Diagnosis Benchmark（官方專案頁）"
    url: "https://microsoft.github.io/sdbench/"
  nejmdata:
    title: "microsoft/sdbench：SDBench nejm dataset README（官方 repo）"
    url: "https://github.com/microsoft/sdbench/blob/main/data/processed_case_data/nejm/README.md"
  syndata:
    title: "microsoft/sdbench：Synthetic CPC Cases README（官方 repo）"
    url: "https://github.com/microsoft/sdbench/blob/main/data/synthetic_case_data/README.md"
  mssource:
    title: "Microsoft Source：Health 分類列表頁（官方新聞室）"
    url: "https://news.microsoft.com/source/tag/health/"
---

[Home](../) · [Industry Watch](./)

# Microsoft 說開源是為了重現，兩份資料都要另外申請

## 來源

- 組織：Microsoft AI（公告署名 `MAI Health Team`；論文作者全部為 Microsoft 員工）
- 事件：發布公告 `Building Medical Superintelligence`，發表 `Sequential Diagnosis Benchmark`（SDBench，循序診斷基準）與 `Microsoft AI Diagnostic Orchestrator`（MAI-DxO，微軟 AI 診斷編排器），並開源 benchmark 程式碼
- 日期：2026-10-22（公告頁可見 `October 22, 2026`，JSON-LD `datePublished` 為 `2026-10-22T18:01:00+00:00`、`dateModified` 為 `2026-10-22T19:32:05+00:00`，三處一致）
- 官方入口：<https://microsoft.ai/news/building-medical-superintelligence/>
- 本則**不是單源**：公告所依據的研究同日刊於 `Science`，為 FREE ACCESS 全文可逐項回查 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)；benchmark 專案頁與原始碼 repo 亦為公開 [(ref: sdbench)](https://microsoft.github.io/sdbench/)。但**獨立性有邊界**：論文的 Competing interests 載明全體作者皆為 Microsoft 員工並持有公司股權，其中八位為美國專利申請案 `19/722,651` 的發明人，該案由 Microsoft 提出、內容即循序診斷的自動化評估框架；Funding 欄寫明 `No funds external to Microsoft were acquired for these studies` [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)

**編輯：** Clarence

Microsoft AI 在 2026-10-22 發表 SDBench 與 MAI-DxO，同日論文刊於 `Science`。公告的開場段落寫道，MAI-DxO 在 NEJM 臨床病理討論會（clinicopathological conference，CPC）案例上「比使用教科書與網路的醫師準確超過兩倍，比不使用這些資源的醫師準確近四倍」，並緊接著寫「而它做到這件事只花一半甚至三分之一的成本」。逐項對回論文後，這兩個子句來自不同的運作點：被引用的準確率屬於無預算限制的配置，該配置每案平均估計成本為 5,431 美元，高於開書醫師的 4,725 美元與閉書醫師的 3,049 美元；成本只有一半或約四分之一的，是準確率 80.9% 與 79.6% 的兩個預算受限配置。公告後段的「某一配置以不到一半成本達到 81% 準確率」把這組對應關係寫對了，開場的摘要句則把兩者併在一起。

另一項是開源的涵蓋範圍。公告寫「我們正在為部分 NEJM 案例開源 SDBench —— 包含 benchmark、Gatekeeper、Judge 與成本估算程式碼 —— 讓研究者可以重現這項評估、測試其他模型，並挑戰或延伸這些發現」。程式碼確實以 MIT 授權公開，但產生已發表數值的兩個資料集都不在 repo 內：NEJM 案例的 README 寫著 `We are unable to directly distribute this dataset`，取得方式是以 NEJM 訂閱帳號的電子郵件向 `elicensing@nejm.org` 申請授權；MIMIC-IV-ED 子集需完成 PhysioNet 認證與資料使用同意。repo 內隨附、可無條件取用的只有五個全合成案例，而該目錄的 README 自己寫著 `These cases are not suitable for reporting actual diagnostic performance`。

## 背景

SDBench 與 MAI-DxO 的時間線如下，全部取自公告頁與論文本身：

- MAI-DxO 的開發起點是 GPT-4.1 仍為當時最強模型的時期；之後以 GPT-5 評估，並在論文出版前以 GPT-5.5 重跑整套評估，期間未修改提示或編排 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- 成本估算所用的收費資料取自 Kaiser Permanente Washington Central Hospital 的 `Standard Charges file`（chargemaster，醫院公告收費表），取用時間為 2026 年 4 月；該檔案依美國 CMS 的 Hospital Price Transparency 規則（45 CFR Part 180）公開 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- 2026-10-22：論文 `Sequential diagnosis with language models` 刊於 `Science` 第 394 卷第 6822 期第 423 至 428 頁，DOI `10.1126/science.aeh7930`，標示為 FREE ACCESS [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- 2026-10-22 18:01 UTC：Microsoft AI 公告 `Building Medical Superintelligence` 發布 [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/)
- 2026-10-23：Microsoft 自家新聞室 Microsoft Source 的 Health 分類列表，以標題「Can AI diagnose like a team of doctors? New research puts it to the test」收錄同一則公告，列表標示日期為 `October 23, 2026`，比公告頁自身的日期晚一天 [(ref: mssource)](https://news.microsoft.com/source/tag/health/)

公告另連結一篇標題為 `The Building Blocks of Medical Superintelligence`、發表於 `BMJ Digital Health and AI` 的文章 [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/)。該文內容不在本文的引述範圍，本文未以其支撐任何陳述。

## 事實（可核對）

### SDBench 的組成與計分方式

- SDBench 把 304 個 NEJM CPC 案例與 325 個 MIMIC-IV-ED 急診收治病例轉成互動式、逐步揭露的診斷情境；受測者（AI 代理或醫師）從一段簡短病歷摘要開始，可以提問、開檢查，或直接下診斷 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- **Gatekeeper 會生成不存在的檢查結果** — 論文原文：當被要求的發現不在原始病歷中時，Gatekeeper `generates diagnostically neutral synthetic results`，目的是避免「查無此項」本身洩漏線索 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- **「準確率」是評分模型給的等第** — 最終診斷由一個 Judge 代理依五級、由醫師撰寫的評分準則與參考診斷判定，`4` 或 `5` 級（論文定義為「不會改變處置的診斷」）計為正確 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)；SDBench 專案頁把同一件事寫成 1 到 5 的 Likert 量表、4 到 5 計為正確 [(ref: sdbench)](https://microsoft.github.io/sdbench/)
- 已發表的成績是在**驗證集與測試集合併**後報告的；訓練集用於開發、不納入回報 [(ref: sdbench)](https://microsoft.github.io/sdbench/)
- 成本為依 CPT 代碼對應的估計值，病史詢問與理學檢查併入一筆固定的看診費用 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)

### 各運作點的準確率與成本（NEJM CPC 案例）

論文列出的 DxO with GPT-5 配置與醫師對照如下 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)：

| 對象 | 準確率 | 每案平均估計成本 |
|---|---|---|
| DxO，追求診斷卓越的配置 | 84.5% | $8,945 |
| DxO，無預算限制 | 83.2% | $5,431 |
| DxO，預算受限之一 | 80.9% | $2,241 |
| DxO，預算受限之二 | 79.6% | $1,303 |
| 醫師（開書，可用搜尋與參考資料） | 36.1% | $4,725 |
| 醫師（閉書） | 22.3% | $3,049 |
| 表現最佳的單一醫師 | 51.8% | 論文未單獨列出 |

公告引用的 83.2%（寫成 83%）對應的是 5,431 美元這一列。「超過兩倍」是 83.2 比 36.1，「近四倍」是 83.2 比 22.3；而「一半甚至三分之一的成本」要成立，必須換到 2,241 美元與 1,303 美元這兩列，它們的準確率分別是 80.9% 與 79.6% [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/)。公告後段另寫「當更積極地針對成本最佳化時……在 NEJM 案例上，某一配置以不到相比系統一半的成本達到 81% 準確率」，這一句與 2,241 美元那一列相符。

### 急診案例這一組，沒有任何一個運作點符合「一半甚至三分之一」

| 對象 | 準確率 | 每案平均估計成本 |
|---|---|---|
| DxO，無預算限制 | 80.3% | $4,979 |
| DxO，預算受限之一 | 73.2% | $2,634 |
| DxO，預算受限之二 | 69.5% | $2,037 |
| 醫師（一般科） | 46.8% | $3,400 |
| 表現最佳的單一醫師（40 案） | 62.5% | $3,332 |

公告的「1.7 倍」對應 80.3% 比 46.8%，而該配置每案 4,979 美元高於醫師的 3,400 美元；成本最低的配置為 2,037 美元，相當於醫師的六成，不是一半、也不是三分之一 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)。

### 被比下去的是哪一種醫師，在什麼條件下

- 受試醫師為執業中的基層醫療與住院／急重症醫師（含內科次專科、急重症與急診醫師），**單獨作業**、**純文字**條件 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- CPC 的醫師研究使用 **56 個在開發期間保留、未用於工程調校的案例**；參與者平均完成 36.4 案（閉書）與 34.8 案（開書），合計 764 與 662 筆人類診斷 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- 公告把 83% 與 22%／36% 並列，未提到醫師研究跑的是這 56 個保留案例，而系統的已發表成績是在驗證集與測試集合併後回報；論文正文未敘明這兩個百分比是否以同一批案例計算 [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/)
- 論文對這項比較自設的界線，公告未引用：`These comparisons do not establish superiority over specialists, multidisciplinary teams, or real-world clinical practice`，以及 `We would expect the performance gap to narrow when comparing DxO with expert specialists or multidisciplinary specialist teams selected to match the content of each case` [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- 論文並指出 CPC 案例是為教學價值而挑選，且經常已包含專科醫師的反思與結論 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)

### 開源涵蓋到哪裡

| 項目 | repo 內是否附上 | 取得條件 |
|---|---|---|
| Benchmark 程式碼（Gatekeeper、Judge、Cost Estimator、baseline 編排） | 是 | MIT 授權公開 |
| NEJM CPC 案例資料集 | 否 | 須以 NEJM 訂閱帳號信箱向 `elicensing@nejm.org` 申請非商業研究授權 |
| MIMIC-IV-ED 子集 | 否 | 須完成 PhysioNet 認證、訓練與 MIMIC-IV 資料使用同意 |
| 五個全合成 CPC 風格案例 | 是 | 無條件 |

- NEJM 資料集 README 原文：`We are unable to directly distribute this dataset.` 與 `To run SDBench on the nejm dataset you will need to license the SDBench dataset from NEJM.`；建議的信件範本要求申請者填入自己的 NEJM 訂閱信箱 [(ref: nejmdata)](https://github.com/microsoft/sdbench/blob/main/data/processed_case_data/nejm/README.md)
- 合成案例 README 原文：`These cases are not suitable for reporting actual diagnostic performance.`，並寫明任何真實或比較性效能都應在 NEJM、MIMIC 或其他臨床來源的資料集上量測，而非在這些合成案例上 [(ref: syndata)](https://github.com/microsoft/sdbench/blob/main/data/synthetic_case_data/README.md)
- 這五個案例由一位臨床醫師與 `Claude Opus 4.8` 共同撰寫，再以 `Gemini 3.1 Pro` 與 `GPT-5.5` 獨立檢查內部一致性與臨床合理性 [(ref: syndata)](https://github.com/microsoft/sdbench/blob/main/data/synthetic_case_data/README.md)
- 論文的資料可得性聲明與上述一致，並載明 MIMIC-IV-ED 子集 `will be released on PhysioNet alongside publication`，仍須通過認證與資料使用同意 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)

### 換到 GPT-5.5 之後，論文說的是哪一個量變大了

- 公告寫：「當我們以包含 GPT-5.5 在內的較新模型重跑評估時，這些增益持續存在，而且更好了」 [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/)
- 論文對應段落寫的是：DxO 繼續定義 Pareto 前緣，而且**它相對於基線提示（baseline prompt）的準確率優勢**在 GPT-5.5 上擴大；絕對準確率的數值被放在補充資料，正文未列 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)
- 論文另給出一組有分母的編排效益：跨所有受測模型，DxO 編排讓急診案例的診斷準確率平均提高 4.4 個百分點、CPC 案例平均提高 7.9 個百分點 [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)

### 名稱在兩份文件裡不同

公告稱這套系統為 `MAI-DxO`／`Microsoft AI Diagnostic Orchestrator`，論文全文稱之為 `DxO`／`Diagnostic Orchestrator` [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/) [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)。

### 論文自列、公告未引用的限制

以下各項全部出自論文的 Discussion [(ref: science)](https://www.science.org/doi/10.1126/science.aeh7930)：

- **沒有任何多模態資料** — 原文：`Nor did the test sessions capture multimodal data such as imaging, waveforms, or pathology slides that are central to real diagnostic workflows.`
- **不是床邊表現，也不是病人結果** — 原文：SDBench `measures diagnostic reasoning under idealized information conditions rather than bedside performance or patient outcomes`
- **案件組成不反映常規臨床** — benchmark 只收病理性案例，CPC 可能過度代表診斷困難的病例，兩個資料集都排除健康或良性就診，整體案件組成與疾病盛行率與常規臨床不同
- **沒有真實世界的雜訊** — 測試過程不含文件不完整、病人遺漏或忘記資訊造成的不確定性，也不含對初步處置的生理反應等時間動態
- **成本只是美國標準定價的近似** — 無法涵蓋真實世界的變異，也未納入出結果所需時間、侵入性、病人不適與可取得性
- **Judge 只判到疾病層級** — 不評估治療適當性、安全性或長期照護品質

## 本書庫解讀（評論）

以下為本書庫的判讀，不是上述來源的結論。

**第一，這則公告的可回查程度其實偏高，爭點不在遮蔽而在併句。** 論文是 FREE ACCESS，程式碼是 MIT 授權，資料取得途徑寫得清楚，論文自列的限制相當完整。本書庫在近兩個月收錄的同類公告裡，多數連一份可逐項回查的文件都沒有。真正的問題集中在公告開場那一句把「近四倍準確率」與「一半甚至三分之一成本」寫成同一件事 —— 這兩個量分屬四個運作點中的不同者，而公告後段其實把正確的對應關係寫出來了。差別在於，會被轉引、被放進簡報、被貼進採購說明的是開場那一句。

**第二，「準確率」這個詞在這裡的意思需要還原。** SDBench 的計分不是把系統的答案與參考診斷做字串或編碼比對，而是由另一個大型語言模型依五級準則打分，4 分與 5 分計為正確，其中 4 分的定義是「不會改變處置」。這個設計有其道理 —— 診斷的對錯本來就不是二元的 —— 但它意味著 83.2% 這個數字同時承載了受測系統的能力與評分模型的寬嚴，而兩者由同一個團隊設計。對醫療 AI 的採購端而言，這不是「有沒有驗證」的問題，而是「驗證的尺由誰刻、刻在哪裡」的問題；本書庫記錄過的 Anthropic 六個藥物開發合作案是同一個問題的另一種版本，那一則的規格依技術報告自述是在看過結果之後才定的。

**第三，Gatekeeper 會生成不存在的檢查結果，這一點會往下影響每一個數字。** 當受測系統開出一項原始病歷沒有的檢查時，系統不會得到「查無此項」，而會得到一個由模型生成、被設計成「診斷上中性」的結果。這個設計是為了防止資訊洩漏，邏輯上成立；但它也意味著在這個環境裡，開出沒有價值的檢查幾乎不會受到資訊面的懲罰，只會累加成本。真實臨床裡，一項非必要檢查帶來的不只是帳單，還有偽陽性、後續追查、延遲與病人負擔 —— 而成本欄位只抓到了第一項。論文在限制段也承認成本估計未納入時間、侵入性與不適。

**第四，對一個以醫學影像為核心的書庫，論文那句話必須被放到最前面：這套評估完全沒有影像。** 原文寫得毫不含糊 —— 測試過程沒有涵蓋 `imaging, waveforms, or pathology slides`，而論文自己接著說這些是「真實診斷流程的核心」。也就是說，MAI-DxO 在 SDBench 裡「開一張胸部 X 光」得到的是一段文字描述，不是一張影像。這條邊界決定了這則成果能被外推到哪裡：它量到的是以文字為介面的病史採集與檢查選擇策略，不是影像判讀，也不是影像與臨床脈絡的整合。把 83% 當成「AI 診斷能力」的通用指標，會跨過這條線。

**第五，開源的敘述與實際取得條件之間的落差，對研究社群有實際後果。** 公告的句子是「開源……讓研究者可以重現這項評估」。能無條件取得的只有五個合成案例，而 repo 自己禁止用它們報告診斷效能。要重現 83.2% 或 80.3%，研究者必須先持有 NEJM 訂閱並取得授權，或完成 PhysioNet 認證。這兩道門檻都不是 Microsoft 單方面能拆除的 —— NEJM CPC 案例的權利在 NEJM，MIMIC 的規則在 PhysioNet，論文致謝也寫明使用 CPC 敘事與資料是經 NEJM Group 許可。本書庫認為該被標示出來的不是 Microsoft 沒有開放，而是「開源以供重現」這個說法在這個案子裡只對程式碼成立。一個不帶資料的 benchmark 仍然很有用 —— 它讓第三方能檢視 Gatekeeper 與 Judge 的提示詞、質疑計分準則 —— 但那是「可檢視」，不是「可重現」。

**第六，編排效益那組數字，比準確率總分更值得抄進筆記本。** 跨各家模型平均 7.9 個百分點（CPC）與 4.4 個百分點（ED），是這篇論文裡少數有明確分母、而且是對照自家最小提示基線的量。它回答的是一個可移植的問題：在同一個模型上，把「維持明確鑑別診斷清單、讓模擬專家互相質疑、逐步評估每項檢查的邊際價值」這套流程外加上去，值多少。這個量才是其他團隊能拿去套用的；83% 不是。

## 產業／生態影響

**benchmark 的設計權正在變成一種位置。** SDBench 把 304 個 NEJM 案例與 325 個 MIMIC 案例轉成互動情境，並定義了 Gatekeeper 的行為、Judge 的準則與成本換算的來源。之後任何宣稱「在循序診斷上勝過 X」的系統，若使用 SDBench，就等於接受了這一整套定義。論文的專利申請案 `19/722,651` 標的正是這個自動化評估框架。對同業而言，值得追蹤的是第三方評估機構與學會是否會採用、修改或另起爐灶。

**資料的瓶頸不在模型，而在授權。** 這則案子具體示範了一件事：即使程式碼完全開源、論文完全開放，一個醫療 benchmark 仍可能因為案例素材的權利歸屬而無法被真正重現。CPC 案例屬 NEJM，去識別化病歷屬 PhysioNet 的治理框架。台灣的研究團隊若要建立對應的本地基準，取得端的工作量很可能超過模型端。

**「成本」會成為下一個被爭奪的指標。** 這篇論文把成本與準確率放進同一張 Pareto 圖，是一個方法上的推進。但它用的是一家美國醫院的公告收費表，而公告收費表與實際給付金額、與台灣健保的點值結構，都不是同一個量。這套方法可以移植，數字不行。

**前瞻驗證才剛要開始。** 公告寫明將透過與 Beth Israel Deaconess Medical Center 的新合作，在前瞻研究中讓病人直接與系統互動，並以醫師的獨立評估作為對照 [(ref: mai)](https://microsoft.ai/news/building-medical-superintelligence/)。在那組結果出來之前，83% 與 80% 的適用範圍就是論文自己劃的那條線：理想化資訊條件下的診斷推理。

## 與書庫其他文章的關係

兩則都是大廠宣傳一套自家診斷 AI 勝過醫師，而真正決定數字意義的限定條件被留在被連結的論文裡：該則的 90% 實為前七名鑑別診斷清單的命中率、排第一名的只有 56%；本則的「準確率」是另一個大型語言模型依五級準則給出 4 到 5 分的比例，而被比下去的是單獨作業、只能讀文字的一般科醫師。兩則並讀可以看出「有同儕審查論文可回查」與「公告保留了限定條件」仍是兩回事: [AMIE 的 90% 是前七名命中率，排第一的只有 56%](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

兩則都是官方公告與它所連結的論文對同一組結果給出無法互相還原的寫法，方向卻相反：該則是把論文的「711 倍」寫成公告的「引用逾 700 篇」，一個倍數被寫成絕對數；本則是把分屬四個運作點的準確率與成本併進同一句話，讀者只看公告無法知道那個準確率對應的成本其實高於被比較的醫師: [公告寫「引用逾 700 篇」，它連的論文寫的是「711 倍」](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md)

兩則的核心都是「訂標準的人與被評分的系統出自同一方」：該則的成功規格依技術報告自述是在看過結果之後才定下的；本則則是 benchmark、Gatekeeper、Judge 與受測系統 MAI-DxO 由同一個團隊設計，論文的利益揭露列出全體作者皆為 Microsoft 員工並持有股權、八位為相關專利申請案的發明人。差別在於本則把整套評分程式碼開源了，讓外部至少能檢視那把尺怎麼刻: [「結塊慢 100 倍」出自單一個孔，成功標準是事後才定的](2026-10-28-anthropic-drug-development-case-studies.md)

該篇說明多代理編排的概念基礎與拓撲選擇，本則提供這套編排在診斷場景的一組有分母的量測：論文自述跨各家受測模型，DxO 編排讓 CPC 案例的準確率比最小提示基線平均高 7.9 個百分點、急診案例高 4.4 個百分點，而 DxO 的拓撲正是該篇描述的「模擬專家小組互相質疑」那一型: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md)

## 實務的啟發

- **讀到「準確率」先問這個數字是誰判的。** 在 SDBench 裡它是一個語言模型依五級準則給的等第，4 分的定義是「不會改變處置」。評估自家或外購系統時，把「誰判對錯、用什麼準則、準則由誰寫」列成三個固定欄位，和準確率本身並列記錄。
- **把準確率與成本的運作點綁在一起看。** 一個系統可以同時有「最準」與「最便宜」兩個配置，但它們通常不是同一個。要求供應商提供的是整條曲線上的若干點，每一點同時標示準確率與成本，而不是分別挑出最好看的兩個數字。
- **確認評估環境裡有沒有影像。** 這則成果完全沒有影像、波形或病理切片。任何以文字 benchmark 取得的分數，都不能直接外推到影像判讀或影像與臨床脈絡的整合；這是本書庫多數讀者的工作現場，也是這條界線最常被跨過的地方。
- **「開源」要拆成程式碼與資料兩問。** 程式碼開源讓外部能檢視評分邏輯，這有實質價值；但能不能重現已發表數字，取決於資料的授權條件。對外宣稱或對內評估時，把「可檢視」與「可重現」分開寫。
- **真正能帶走的是編排效益，不是總分。** 7.9 與 4.4 個百分點是對照同一模型的最小提示基線測出來的，回答的是「加上這套流程值多少」。在自家任務上複製這個量法，比追逐別人的 83% 有用。
- **注意 Gatekeeper 這類設計對行為的誘導。** 當環境對「開出無用的檢查」只收成本、不給資訊懲罰時，受測系統學到的檢查選擇策略未必能原封不動搬到真實門診。評估自家代理時，想清楚你的模擬環境在獎勵什麼。

## 後續追蹤

- Beth Israel Deaconess Medical Center 的前瞻研究設計與登錄資訊是否公開，以及其主要終點是否為診斷準確率
- MIMIC-IV-ED 子集在 PhysioNet 上的實際釋出狀態與版本
- 補充資料中 GPT-5.5 的絕對準確率與成本數值
- 是否有 Microsoft 以外的團隊取得 NEJM 授權並發表獨立的 SDBench 評估結果
- 公告所連結、發表於 `BMJ Digital Health and AI` 的 `The Building Blocks of Medical Superintelligence` 一文的主張範圍
- Judge 準則與 Gatekeeper 提示詞在開源後是否收到外部質疑或修訂

## References

| ref | 標題 | 底 URL | 實際使用的深鏈 |
|---|---|---|---|
| `mai` | Microsoft AI：Building Medical Superintelligence（官方公告，2026-10-22） | <https://microsoft.ai/news/building-medical-superintelligence/> | 同左 |
| `science` | Nori H. et al., Sequential diagnosis with language models, *Science* 394(6822):423-428（2026-10-22，FREE ACCESS，DOI 10.1126/science.aeh7930） | <https://www.science.org/doi/10.1126/science.aeh7930> | 同左 |
| `sdbench` | SDBench — Sequential Diagnosis Benchmark（官方專案頁） | <https://microsoft.github.io/sdbench/> | 同左 |
| `nejmdata` | microsoft/sdbench：SDBench nejm dataset README（官方 repo） | <https://github.com/microsoft/sdbench> | <https://github.com/microsoft/sdbench/blob/main/data/processed_case_data/nejm/README.md> |
| `syndata` | microsoft/sdbench：Synthetic CPC Cases README（官方 repo） | <https://github.com/microsoft/sdbench> | <https://github.com/microsoft/sdbench/blob/main/data/synthetic_case_data/README.md> |
| `mssource` | Microsoft Source：Health 分類列表頁（官方新聞室） | <https://news.microsoft.com/source/tag/health/> | 同左 |

[Home](../) · [Industry Watch](./)
