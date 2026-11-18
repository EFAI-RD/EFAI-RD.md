---
parent: AI Papers
nav_exclude: true
title: "HealthAdminBench：子項 78.4%，整件工作只做完 36.3%"
category: ai-papers
date: 2026-11-17
tags: [computer-use-agents, healthcare-administration, benchmark, prior-authorization, appeals-denials, DME, GUI-agent, LLM-judge, EHR, revenue-cycle, task-success, subtask-success, fine-tuning]
catalog_id: "arxiv:2604.09937"
editors:
  - "Clare"
status: published
evidence_reviewed: true
skill_version: "write-ai-paper@3.0"
refs:
  main:
    title: "HealthAdminBench: Evaluating Computer-Use Agents on Healthcare Administration Tasks（arXiv HTML v1）"
    url: "https://arxiv.org/html/2604.09937v1"
  abs:
    title: "arXiv:2604.09937 abstract page"
    url: "https://arxiv.org/abs/2604.09937"
  site:
    title: "HealthAdminBench 公開榜與互動環境（計畫網站）"
    url: "https://som-shahlab.github.io/health-admin-bench-website/"
  code:
    title: "som-shahlab/health-admin-bench（程式庫與題目 JSON）"
    url: "https://github.com/som-shahlab/health-admin-bench"
related_articles:
  - path: "../industry-watch/2026-11-17-openai-computer-use-agents-healthcare.md"
    relation: "該則公告引用本篇評測並自報 GPT-6 Astra 取得 94.3% 的 rubric points，而本篇正是那個評測的方法與完整結果；兩篇並讀可以看出同一個題庫上「子項比例」與「整件工作完成率」是兩個差了三、四十個百分點的數字"
  - path: "2026-10-13-clinician-llm-use-vs-benchmarks.md"
    relation: "該篇量到臨床人員實際把 LLM 用在文件工作的比例遠高於診斷，本篇則替那一側的工作做出可程式化驗證的題庫；兩篇合起來說明評測重心與實際用途之間的落差正在被補上"
  - path: "2026-09-16-careconnect-healthcare-agent.md"
    relation: "該篇的設計主張是把 LLM 擋在診斷之外、只讓它做掛號這類行政動作，本篇則顯示就算只做行政，跨系統的整件工作仍有近三分之二無法完成"
---

[Home](../) · [AI Papers](./)

# HealthAdminBench：子項 78.4%，整件工作只做完 36.3%

## 來源

- **單位／團隊**：Stanford University；Kinetic Systems；Stanford Healthcare。[(ref: abs)](https://arxiv.org/abs/2604.09937)
- **作者**：Suhana Bedi、Ryan Welch、Ethan Steinberg、Michael Wornow、Taeil Matthew Kim、Haroun Ahmed、Peter Sterling、Bravim Purohit、Qurat Akram、Angelic Acosta、Esther Nubla、Pritika Sharma、Michael A. Pfeffer、Sanmi Koyejo、Nigam H. Shah。
- **完整篇名**：*HealthAdminBench: Evaluating Computer-Use Agents on Healthcare Administration Tasks*。
- **年份與版本**：arXiv v1 於 2026-04-10 提交，分類 cs.AI，僅有 v1；論文自述 24 頁、5 張圖、5 張表。
- **識別碼**：[arXiv:2604.09937](https://arxiv.org/abs/2604.09937)；[DOI: 10.48550/arXiv.2604.09937](https://doi.org/10.48550/arXiv.2604.09937)。
- **原文**：[arXiv HTML 全文](https://arxiv.org/html/2604.09937v1)。
- **其他資源**：[計畫網站與公開榜](https://som-shahlab.github.io/health-admin-bench-website/)（四個環境可直接開啟操作）；[程式庫與題目 JSON](https://github.com/som-shahlab/health-admin-bench)。本文未檢視程式庫內容。
- **研究性質**：完整的 benchmark 論文，不是 pilot。環境、題目、驗證器與評測管線皆已實作並公開，七組代理程式設定全部實際跑過，主要結果附 95% bootstrap 信賴區間。文中唯一屬於初步性質的是 §4.4 的微調實驗（測試集僅 35 題，作者自己標明需留意統計雜訊）。
- **證據邊界**：本文數值以 arXiv HTML v1 的正文、Table 1–10 與 Appendix B–E 為準。Figure 3、4、5、6、7 的各模型逐點數值只存在於圖面，未在正文列出者本文不引用；本文引用的 78.4%／89.7% 與 36.3%／51.9% 四個數字，皆取自 Appendix D.1 正文的文字敘述。

**編輯：** Clare

這篇論文做了一件先前沒有人做的事：把醫院行政端真正吃人力的三種工作（事前授權、申覆與否准處理、耐用醫材訂購）做成可程式化驗證的題庫，讓代理程式用滑鼠和鍵盤去跑，結果發現子項做得不錯、整件工作卻大多做不完 —— 最強的 Claude Opus 4.6 CUA 子項成功率 78.4%，但整件工作只有 36.3% 全部過關。

## 流程

![左右兩部分的圖。左半部為流程圖，五個圓角框。左上為淺藍底、深藍實線框「1. Four simulated GUI environments」，內列 EHR (prior auth / denials / DME worklists)、Payer portal A · Payer portal B、eFax portal、synthetic patient data, schema validation；以向右箭頭連到右上淺藍底、深藍實線框「2. 135 expert-defined tasks」，內列 Prior Authorization 60、Appeals & Denials Mgmt. 60、DME Order Processing 15、easy / medium / hard。左上框另以向下箭頭連到左中淺橘底、橘褐色實線框「3. Agent loop (POMDP, Playwright)」，內列 observe: screenshot OR accessibility tree、act: click / type / select / upload / scroll、scratch space = external memory、stops at task end or step budget；右上框以向下箭頭連到右中淺橘底、橘褐色實線框「4. 1,698 verifiable subtasks」，內列 1,177 deterministic JMESPath checks、521 LLM judge (GPT-5.4), rubric-based、binary pass/fail, NO partial credit、judge-vs-human agreement 93.3%。左中框以向右箭頭連到右中框。兩者下方以一個灰色向下箭頭連到底部淺灰底、灰色實線的寬框「5. Two metrics — the whole point of the paper」，內列 subtask success = fraction of subtasks passed、task success = ALL subtasks of that task passed (strict end-to-end)、7 agent configurations × 2 prompting strategies × 2 observation modes、primary setting: Task Description + Portal Guidance, screenshot-only。左半部底框下方置中的灰色小字「Redrawn by EFAI-RD from arXiv:2604.09937v1 Sections 3.1-3.7, 4, Appendix B」。右半部為分組長條圖，標題兩行「Subtask vs end-to-end task success」與「(both pairs quoted verbatim in Appendix D.1)」，圖例置於圖上方、兩項分別為藍色 subtask success 與橘色 task success (all subtasks)，縱軸「success rate (%)」由 0 到 100。橫軸兩組：左組「Claude Opus 4.6 CUA (screenshot)」藍柱 78.4%、橘柱 36.3%；右組「Claude Opus 4.6 harness (accessibility tree)」藍柱 89.7%、橘柱 51.9%。每組內有一條暗紅色虛線向下箭頭，自藍柱頂指向橘柱頂，箭頭左側標註文字，左組為「-42.1 pt」、右組為「-37.8 pt」。](assets/healthadminbench-design-and-task-subtask-gap.png)

*圖：本書庫依論文 §3.1–§3.7、§4 與 Appendix B 重繪的 HealthAdminBench 評測結構（左），以及 Appendix D.1 正文逐字給出的兩組「子項成功率對整件工作成功率」對照（右）。兩個差距標註 -42.1 與 -37.8 個百分點由本文代為計算（78.4 − 36.3、89.7 − 51.9）。數值出處見 [§3](https://arxiv.org/html/2604.09937v1#S3)、[Appendix B](https://arxiv.org/html/2604.09937v1#A2) 與 [Appendix D.1](https://arxiv.org/html/2604.09937v1#A4.SS1)。*

## 背景／問題

論文開篇指出，醫療領域的 LLM 評估長期集中在診斷推理與分流這類臨床任務，而事前授權、申請送件、病人報到這些行政工作仍少有人碰 —— 儘管它們在美國佔每年超過一兆美元的醫療支出。這個前提論文有引用來源（Sahni 等人 2023 年），不是作者自己的斷言 [(ref: main §1)](https://arxiv.org/html/2604.09937v1#S1)。

論文接著給出做這件事的技術理由：這些工作需要在缺乏 API 支援的老舊企業系統之間來回多步操作，因此無法直接用程式自動化。能觀察並操作軟體介面的 computer-use agents（CUA）是可能的解法，但既有的評測抓不到這類工作的跨系統複雜度 —— 先前的工作集中在公開網站的網頁瀏覽，或一般企業流程。Table 1 把這個缺口列成四欄比較 [(ref: main Table 1)](https://arxiv.org/html/2604.09937v1#S2.T1)：

| Benchmark | Cross-App Workflows | Strict Forms & Commits | Objective Success | Healthcare Admin |
|---|---|---|---|---|
| WebShop (2022) | x | ✓ | ✓ | x |
| Mind2Web (2023) | x | x | x | x |
| WebArena (2023) | x | ✓ | ✓ | x |
| WorkArena (2024) | x | ✓ | ✓ | x |
| OSWorld (2024) | ✓ | ✓ | ✓ | x |
| REAL (2025) | x | ✓ | ✓ | x |
| MedAgentBench (2025) | x | ✓ | ✓ | x |
| MedHELM (2026) | x | x | ✓ | •（部分） |
| HealthAdminBench | ✓ | ✓ | ✓ | ✓ |

四欄依序為：跨多個不相連應用程式的流程、具嚴格 schema 驗證與終端送出動作的介面、可程式化驗證的成功條件、以醫療行政為題材。

## 方法摘要

論文把醫療行政工作形式化為部分可觀測馬可夫決策過程（POMDP）：潛在狀態是所有瀏覽器工作階段的完整組態，代理程式只看得到其中一部分 —— 一張截圖，或一份結構化的介面表示。每一步代理程式選一個動作，由 Playwright 執行並確定性地推進環境狀態；回合在任務完成或用盡互動預算時結束 [(ref: main §3)](https://arxiv.org/html/2604.09937v1#S3)。

評測由四個模擬環境、135 道專家定義的任務、1,698 個可驗證子項，以及兩個指標組成。關鍵設計是**子項全過才算整件工作成功**，沒有部分給分。

## 方法詳解

- **四個環境** — 一個仿 Epic 的 EHR 檢視器（含事前授權、否准、耐用醫材三種工作清單）、兩個版面與政策各異的保險方授權入口（仿 Anthem 與 Availity）、一個傳真送件入口（仿 RightFax）。論文寫明這些環境是依超過一百小時的真實行政工作觀察設計的，以 REAL 框架實作成網站，具型別輸入、schema 驗證、政策檢查與真實的失效模式（例如必填欄位缺漏）[(ref: main §3.1)](https://arxiv.org/html/2604.09937v1#S3.SS1)。資料與環境皆為合成，但依真實的保險方政策與文件要求設計。論文明說**刻意移除** CAPTCHA、多因素驗證與工作階段逾時這類部署端限制，以便在可重現的條件下只衡量流程執行本身。
- **觀察空間** — 兩種：瀏覽器可視範圍的截圖，或由 accessibility tree 衍生的結構化表示（互動元素以穩定的 `data-testid` 索引）。論文自己註明，真實的 EHR 與保險方系統通常**不會**暴露這種乾淨穩定的識別碼 [(ref: main §3.2)](https://arxiv.org/html/2604.09937v1#S3.SS2)。
- **動作空間** — 以使用者意圖層級的自然語言表達（例如 click submit、enter text），再對應到可執行的瀏覽器操作；完整列舉見 Table 5。截圖模式的代理程式用同一組動作，但必須額外推斷每個動作在畫面上的位置。**Claude Opus 4.6 CUA 與 GPT-5.4 CUA 兩組例外**：它們用各家原生的 computer-use 工具而非本論文的自訂動作集，但跑在同一個瀏覽器工作階段與環境狀態上，並以相同方式依子項完成度評分 [(ref: main §3.3)](https://arxiv.org/html/2604.09937v1#S3.SS3)。
- **任務與專家驗證** — 135 道任務全部與執業的醫療行政人員共同設計。另對事前授權 20 題、申覆與否准 20 題共 40 題做了正式稽核，由兩位合計數十年大型醫院營收循環經驗的專家各自獨立審查，判斷任務目標是否實際、步驟是否反映真實作業、成功條件是否恰當。論文寫明審查意見主要落在領域慣例而非核心設計，並將修正系統性套用到相關任務；耐用醫材那一組流程較標準化，是以反覆測試而非正式專家審查驗證 [(ref: main §3.4)](https://arxiv.org/html/2604.09937v1#S3.SS4)。
- **子項與驗證器** — 1,698 個子項中，1,177 個以確定性檢查驗證（對入口狀態下 JMESPath 查詢），521 個（30.7%）由 LLM judge（GPT-5.4）依預先寫好的評分標準判斷代理程式的自由文字輸出。所有驗證器一律二元通過／失敗 [(ref: main §3.5)](https://arxiv.org/html/2604.09937v1#S3.SS5)。
- **LLM judge 的驗證** — 取 Claude Opus 4.6 的 60 個 LLM 判定子項做分層抽樣（判定失敗 30 個、判定成功 30 個），每個由兩位人類審查者在不看 judge 結果與理由的情況下複審，共 120 次人工審查。人類之間一致率 93.3%（95% CI 83.8%–98.15%），人類與 judge 一致率同為 93.3%（95% CI 87.4%–97.1%）[(ref: main Appendix B)](https://arxiv.org/html/2604.09937v1#A2)。
- **記憶** — 任務的互動長度常超過代理程式的有效脈絡長度，因此論文提供一個持續存在的 scratch space 作為外部記憶，代理程式每一步可寫入，下一步再回填給它 [(ref: main §3.6)](https://arxiv.org/html/2604.09937v1#S3.SS6)。
- **兩種提示策略** — `Task Description` 只給環境說明與高層次任務描述；`Task Description + Portal Guidance` 另加上入口導覽模式與常見作業限制的一般性指引。論文另有第三種 `Task-Specific Step-by-Step` 提示，會明確寫出預期的工作步驟，**僅用於開發與軌跡收集，不用於主要評測** [(ref: main §3.7)](https://arxiv.org/html/2604.09937v1#S3.SS7)。
- **論文未交代** — Figure 3 的各代理程式整體子項成功率、Figure 4 與 Figure 7 的提示 × 觀察模式網格逐點數值、Figure 5 與 Figure 6 的步數與成本分布，都只以圖呈現，正文未逐一列出；本文因此只引用正文與表格中出現過的數字。兩個 CUA 代理程式的 API 成本**未納入**比較，論文說明原因是兩家 harness 的成本記帳方式不一致，難以公平比較 [(ref: main Appendix C)](https://arxiv.org/html/2604.09937v1#A3)。步數上限的具體數值只畫在 Figure 5 的紅色虛線上，正文未給。人類審查者的四人資歷與專業背景未說明；LLM judge 的驗證只取自 Claude Opus 4.6 一個模型。

## 資料與實驗

**題庫組成**（§3.4、§3.5）：

| 項目 | 數量 | 備註 |
|---|---|---|
| 環境 | 4 | EHR、兩個保險方入口、eFax |
| 任務 | 135 | Prior Authorization 60、Appeals & Denials 60、DME 15 |
| 子項 | 1,698 | 確定性檢查 1,177、LLM judge 521（30.7%） |
| 子項類型 | 6 | 見下表 |
| 受測模型 | 5 | 閉源 3：Claude Opus 4.6、GPT-5.4、Gemini 3.1 Pro；開源 2：Kimi K2.5、Qwen-3.5-27B |
| 代理程式設定 | 7 | 五個模型配本論文 harness，另加兩家原生 CUA |

六種子項類型與數量（§3.5）：Information Retrieval 419、Documentation 515、Form Completion 292、Task Resolution 200、Document Handling 149、Clinical Reasoning 123。六者合計 1,698（由本文代為加總，與論文所述相符）。

各任務類型中「至少含一個該類子項」的任務百分比 [(ref: main Table 2)](https://arxiv.org/html/2604.09937v1#S3.T2)：

| Subtask | Prior Authorization | Appeals & Denials Management | DME |
|---|---|---|---|
| Information Retrieval | 93.3% | 100.0% | 33.3% |
| Documentation | 100.0% | 100.0% | 100.0% |
| Form Completion | 58.3% | 3.3% | 66.7% |
| Task Resolution | 98.3% | 96.7% | 100.0% |
| Document Handling | 53.3% | 23.3% | 100.0% |
| Clinical Reasoning | 60.0% | 71.7% | 6.7% |

**主要評測設定**：除另有說明外，一律為截圖觀察加 `Task Description + Portal Guidance` 提示 [(ref: main §4)](https://arxiv.org/html/2604.09937v1#S4)。

## 結果

**依任務類型的整件工作成功率** [(ref: main Table 3)](https://arxiv.org/html/2604.09937v1#S4.T3)：

| Agent | Prior Authorization | Appeals & Denials Management | DME |
|---|---|---|---|
| Claude Opus 4.6 CUA | 38.3% | 25.0% | 73.3% |
| GPT-5.4 CUA | 26.7% | 18.3% | 60.0% |
| Kimi K2.5 | 18.3% | 13.3% | 13.3% |
| Claude Opus 4.6 | 16.7% | 16.7% | 0.0% |
| Qwen 3.5 | 16.7% | 5.0% | 33.3% |
| Gemini 3.1 Pro | 23.3% | 3.3% | 0.0% |
| GPT-5.4 | 6.7% | 3.3% | 13.3% |

**依子項類型的成功率** [(ref: main Table 4)](https://arxiv.org/html/2604.09937v1#S4.T4)：

| Agent | Information Retrieval | Documentation | Form Completion | Task Resolution | Document Handling | Clinical Reasoning |
|---|---|---|---|---|---|---|
| Claude Opus 4.6 CUA | 96.5% | 74.3% | 88.9% | 70.7% | 92.3% | 61.3% |
| GPT-5.4 CUA | 96.1% | 84.4% | 84.9% | 66.2% | 94.3% | 77.0% |
| Kimi K2.5 | 87.7% | 45.6% | 53.2% | 45.3% | 58.1% | 39.3% |
| Claude Opus 4.6 | 88.5% | 43.0% | 23.4% | 40.5% | 49.3% | 32.0% |
| Qwen 3.5 | 87.4% | 54.0% | 44.6% | 51.6% | 52.0% | 44.5% |
| Gemini 3.1 Pro | 90.2% | 63.3% | 87.8% | 70.3% | 68.9% | 55.1% |
| GPT-5.4 | 83.0% | 27.5% | 36.7% | 38.5% | 44.3% | 22.3% |

- **最強的仍然做不完三分之二的工作** — 摘要與 §5 都寫明：表現最好的 Claude Opus 4.6 CUA 整件工作成功率只有 36.3%，而 GPT-5.4 CUA 拿到最高的子項成功率 82.8% [(ref: main abs)](https://arxiv.org/abs/2604.09937)。Appendix D.1 另逐字給出兩組對照：Claude Opus 4.6 CUA 子項 78.4% 對整件 36.3%；Claude Opus 4.6 在 Portal Guidance 加 accessibility tree 下子項 89.7% 對整件 51.9% [(ref: main Appendix D.1)](https://arxiv.org/html/2604.09937v1#A4.SS1)。
- **原生 CUA 與自訂 harness 的差距很大** — 論文把這解讀為系統層級編排（system-level orchestration）的重要性：同一個 Claude Opus 4.6，走原生 CUA 的整件成功率 36.3%，走本論文 harness（截圖、Portal Guidance）則落在個位數到十幾的區間（見 Table 3 各欄）。
- **評測分得出模型差異** — 42 組兩兩比較中有 33 組達統計顯著 [(ref: main §4)](https://arxiv.org/html/2604.09937v1#S4)。Table 6 的整件工作差距中，Claude Opus 4.6 CUA 對 GPT-5.4 CUA 為 9.6 個百分點（95% CI 2.2%–17.8%）；但在子項指標上（Table 7）方向相反，GPT-5.4 CUA 反而高 4.4 個百分點（95% CI −8.8% 至 −0.3%）[(ref: main Appendix D.2)](https://arxiv.org/html/2604.09937v1#A4.SS2)。
- **難的是申覆、容易的是耐用醫材** — 跨代理程式一致：DME 成功率最高、事前授權居中、申覆與否准最低。論文把原因歸到動作序列較長，以及 Clinical Reasoning 與 Information Retrieval 子項佔比較高。
- **提示與觀察模式都有效，但後者在真實部署常不可得** — Portal Guidance 一致優於只給任務描述，accessibility tree 一致優於只給截圖，兩者併用增益最大；論文同時提醒後者「在真實部署中往往不可得」[(ref: main §4.3)](https://arxiv.org/html/2604.09937v1#S4.SS3)。
- **少量領域微調的增益大於換更強的前沿模型** — 把 135 題切成 100 題訓練、35 題測試，以 Task-Specific Step-by-Step 提示產生軌跡當監督資料，對 Qwen-3.5-27B 做 LoRA 微調（單一 epoch、學習率 3.4e-4、LoRA rank 8、batch size 16、最大序列長度 24,574，使用 Tinker API）[(ref: main Appendix E)](https://arxiv.org/html/2604.09937v1#A5)：

| Model | Task Success Rate | Subtask Success Rate | Fine Tuned? |
|---|---|---|---|
| Claude Opus 4.6 | 25.7% | 75.0% | - |
| Qwen-3.5 | 17.1% | 65.4% | - |
| Qwen-3.5-Kinetic-SFT | 40.0% | 83.3% | ✓ |

  論文自己做了 bootstrap 檢定並誠實報告：微調版對 Claude Opus 4.6 的**子項**增益 8.4 個百分點（95% CI 1.2%–15.4%）統計顯著，而**整件工作**的 14.3 個百分點（95% CI −2.9%–31.4%）**不顯著** [(ref: main Table 9)](https://arxiv.org/html/2604.09937v1#A5.T9) [(ref: main Table 10)](https://arxiv.org/html/2604.09937v1#A5.T10)。
- **三種反覆出現的失效模式** — 論文以人工檢視 Claude Opus 4.6 的軌跡歸納（並稱其他模型型態相似）[(ref: main §4.5)](https://arxiv.org/html/2604.09937v1#S4.SS5)：
  - **隱藏的長程相依** — 許多任務要先在 EHR 取得資訊、稍後才在保險方入口或傳真系統用到，而需求往往一開始看不出來。人類會回頭補，代理程式很少回頭，常耗盡步數預算。
  - **迴避檔案操作** — 雖然支援上傳下載，代理程式常迴避或忽略這些動作；由於文件傳遞是事前授權與耐用醫材流程的必要環節，這直接造成文件處理子項大量失敗。
  - **長流程中的資訊遺失** — 代理程式在有限脈絡下通常只看得到最近幾步，先前資訊除非明確寫入外部記憶否則會被遺忘；論文雖提供 scratch space，代理程式仍常未記下關鍵細節。

## 限制

論文的 §5 自述（本書庫未增補）[(ref: main §5)](https://arxiv.org/html/2604.09937v1#S5)：

- 環境與題目仍是生產系統的**簡化代理**；評測是靜態且回溯的，沒有捕捉介面隨時間漂移、保險方政策演變，或真實醫院部署的完整異質性。
- accessibility tree 設定雖讓評測可控可重現，但真實入口通常不會提供這種乾淨穩定的識別碼，且頻繁的介面更新會降低依賴它的代理程式的穩健性。
- 代理程式在有限脈絡視窗下運作；論文評的是**單次軌跡**，沒有人類那樣的回復行為。
- 刻意抽離了多因素驗證、CAPTCHA 與工作階段逾時這些部署限制。
- 論文自己在同一段寫下警告：行政自動化雖可能降低成本與負擔，但**過早部署代理式系統會帶來具財務或臨床後果的作業錯誤**，因此需要嚴謹評估與人工監督。

本書庫另外要讀者注意三點（屬本書庫判斷，非論文自述）：

- 論文的主要設定是截圖加 Portal Guidance，而 Portal Guidance 是一份由評測方寫好的一般性入口導覽。真實導入時這份指引要由誰寫、寫多細、改版後誰維護，論文不處理。
- LLM judge 佔 521 個子項（30.7%），其驗證只抽自一個模型（Claude Opus 4.6）的 60 個判定；若受測模型的輸出風格與 Claude 差異大，該一致率不必然轉移。
- 微調那一組的測試集只有 35 題，整件工作的增益未達顯著 —— 這組結果適合當作「值得再做大規模驗證的方向」，不適合當作「微調已證實優於前沿模型」。

## 與書庫其他文章的關係

該則公告引用本篇評測並自報 GPT-6 Astra 取得 94.3% 的 rubric points，而本篇正是那個評測的方法與完整結果；兩篇並讀可以看出同一個題庫上「子項比例」與「整件工作完成率」是兩個差了三、四十個百分點的數字: [API 到不了就改用點擊：OpenAI 醫療 computer use 解析](../industry-watch/2026-11-17-openai-computer-use-agents-healthcare.md)

該篇量到臨床人員實際把 LLM 用在文件工作的比例遠高於診斷，本篇則替那一側的工作做出可程式化驗證的題庫；兩篇合起來說明評測重心與實際用途之間的落差正在被補上: [臨床人員實際用 LLM 做什麼？文件工作 36%，診斷只有 3.7%](2026-10-13-clinician-llm-use-vs-benchmarks.md)

該篇的設計主張是把 LLM 擋在診斷之外、只讓它做掛號這類行政動作，本篇則顯示就算只做行政，跨系統的整件工作仍有近三分之二無法完成: [CareConnect：把 LLM 擋在診斷之外，只讓它做掛號](2026-09-16-careconnect-healthcare-agent.md)

## 實務的啟發

- **採購或評估這類工具時，問的應該是整件工作完成率** — 本篇最可直接借用的就是這個區分。子項成功率看起來漂亮（78.4%、89.7%），但行政送件是全有全無的：少填一個欄位、漏附一份文件，整件就得重來。要求供應商提供「整件工作完成率」及其定義，是本篇提供的最實際的一把尺。
- **把三種失效模式當成驗收測試的題型** — 隱藏的長程相依、迴避檔案操作、長流程資訊遺失，這三類都是可以自己設計案例去打的。例如刻意設計一個「必須先到 EHR 取號、最後才在入口用到」的案例，看代理程式會不會回頭。
- **先確認自家系統給不給 accessibility tree** — 本篇顯示觀察模式對成績影響很大，而論文自己提醒真實入口通常不提供穩定識別碼。評估前先確認自家 EHR 與保險方入口實際能暴露什麼，再決定該參考哪一組數字。
- **把「代理程式該停下來」寫進需求** — 論文的 DME 困難題型就包含「文件無效或缺漏時應中止處理」。能不能正確地**不做**，與能不能做完一樣需要驗收。
- **領域微調值得試，但目前只能當成待驗證的方向** — 100 題軌跡就讓開源模型的整件成功率從 17.1% 升到 40.0%，方向很有吸引力；但測試集 35 題、整件增益未達統計顯著，現階段適合當作內部試驗題目，不適合寫進採購理由。
- **別把這套分數直接當成自家環境的預期值** — 環境是合成的，而且刻意移除了多因素驗證、CAPTCHA 與工作階段逾時。真實環境只會更難，這些分數應視為上界而非預估值。

## References

- `main` — HealthAdminBench: Evaluating Computer-Use Agents on Healthcare Administration Tasks（arXiv HTML v1；本文引用 §1、§2、§3.1–§3.7、§4–§4.5、§5、Table 1–4、Appendix B、C、D.1、D.2、E 與 Table 8–10）  
  <https://arxiv.org/html/2604.09937v1>
- `abs` — arXiv:2604.09937 摘要頁（作者、單位、提交日期 2026-04-10、版本、DOI、摘要中的 36.3% 與 82.8%）  
  <https://arxiv.org/abs/2604.09937>
- `site` — HealthAdminBench 計畫網站與公開榜（四個環境可直接開啟操作；本文未以其數值取代論文數值）  
  <https://som-shahlab.github.io/health-admin-bench-website/>
- `code` — som-shahlab/health-admin-bench 程式庫與題目 JSON（本文未檢視程式內容）  
  <https://github.com/som-shahlab/health-admin-bench>

[Home](../) · [AI Papers](./)
