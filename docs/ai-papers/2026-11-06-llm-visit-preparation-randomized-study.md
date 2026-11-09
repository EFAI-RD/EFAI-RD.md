---
parent: AI Papers
nav_order: 2
title: "只改系統提示：病人備診感 57%→74%，自評與醫師評分無顯著相關"
catalog_id: "arxiv:2610.41437"
editors:
  - "Clare"
refs:
  main:
    title: "A prospective randomized study of patient-centered AI for clinical visit preparation"
    url: "https://arxiv.org/html/2610.41437v1"
  abs:
    title: "arXiv abstract page: 2610.41437v1"
    url: "https://arxiv.org/abs/2610.41437v1"
  pdf:
    title: "arXiv PDF v1 (main text and appendix A.1–A.8)"
    url: "https://arxiv.org/pdf/2610.41437v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 只改系統提示：病人備診感 57%→74%，自評與醫師評分無顯著相關

## 來源

- 團隊：Google Research，共 36 位作者（第一作者 Xincheng Tan，末位 Jackie M. Barr；通訊信箱為 caratan 與 mikeshake@google.com）。研究由 Alphabet 出資，作者聲明身為 Alphabet 員工者可能持有公司股票。[(ref: main author block)](https://arxiv.org/html/2610.41437v1) [(ref: main Competing Interests)](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx4)
- 論文：*A prospective randomized study of patient-centered AI for clinical visit preparation*，arXiv:2610.41437v1（cs.HC；另列 cs.CL、cs.LG），2026-10-30 提交，目前只有 v1；授權為 CC BY 4.0；預印本，未經同儕審查；全文 50 頁（正文 16 頁、附錄 34 頁）。[(ref: abs)](https://arxiv.org/abs/2610.41437v1)
- 識別碼：arXiv [2610.41437](https://arxiv.org/abs/2610.41437v1)；DOI [10.48550/arXiv.2610.41437](https://doi.org/10.48550/arXiv.2610.41437)；試驗登錄 ClinicalTrials.gov NCT07552311，Advarra IRB 核准（Protocol No. Pro00089880）。[(ref: main §2.1)](https://arxiv.org/html/2610.41437v1#S2.SS1)
- 全文：[arXiv HTML v1](https://arxiv.org/html/2610.41437v1)（正文）、[PDF v1](https://arxiv.org/pdf/2610.41437v1)（正文與附錄 A.1–A.8）。
- 程式與資料：沒有訓練或修改任何模型權重；三組的 system prompt 全文收在附錄 A.2，對話與摘要範例收在附錄 A.1，未釋出受試者對話資料。[(ref: main Code Availability)](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx3) [(ref: main Data Availability)](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx2) [(ref: pdf A.2, p.20)](https://arxiv.org/pdf/2610.41437v1#page=20)
- 研究性質：前瞻性、三組隨機分派的線上研究，完整研究而非 pilot；被比較的是同一個 Gemini 2.5 Flash 套上三種 system prompt，沒有訓練新模型。主要結果是病人自評，次要結果是臨床醫師盲評；所有比例附 95% Wilson CI，組間檢定以 Benjamini–Hochberg 控制 false discovery rate。分析採 modified intention-to-treat，只納入至少有一段實質健康對話的受試者。[(ref: main §2.1)](https://arxiv.org/html/2610.41437v1#S2.SS1) [(ref: main §2.2)](https://arxiv.org/html/2610.41437v1#S2.SS2) [(ref: main §2.5)](https://arxiv.org/html/2610.41437v1#S2.SS5)
- 證據邊界：正文數值以 arXiv v1 HTML 正文為準；HTML 版未收錄附錄，附錄內容（system prompt、評分 rubric、三組分開比較、首段對話敏感度分析）以 PDF v1 的頁碼標示。文中流程與結果圖為本書庫依論文 §2–3 正文數字重繪，未轉載論文圖片；Figure 4–6 的逐格長條數值與附錄 Figure A.6 的完整迴歸係數未納入本文引述。

**編輯：** Clare

Google 在自家 Google Health app 上做了一個三組隨機研究：同一個 Gemini 2.5 Flash，只把 system prompt 從「照常回答健康問題」換成五步驟的看診前準備流程，病人自評「覺得準備好了」的比例由 57.0% 升到 73.8%，臨床醫師盲評的完整度由 50.6% 升到 67.2%、安全性兩組都在 93% 以上，但同一批對話的病人自評與醫師評分之間，校正多重比較後沒有任何一組達到顯著相關。[(ref: main §3.2.2)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS2) [(ref: main §3.3.1)](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS1) [(ref: main §3.4)](https://arxiv.org/html/2610.41437v1#S3.SS4)

## 流程

![左右兩欄圖。左欄標題「A. Participant and conversation flow」，由上而下五個淺藍底、深藍實線外框的圓角方框，以四支深色向下箭頭相連，文字依序為：「Consented and randomized 1:2:2 / 5,960 adults (Google Health app, US)」、「Initiated the study experience / 1,656 participants / 1,957 conversations」、「Analysed (modified ITT) / 802 participants / 866 conversations / Control 141 | Visit preparation 725」、「Completed the full preparation flow / 500 conversations」、「Blinded clinician evaluation / 272 sessions (Control 83 | Visit prep 189)」；方框下方灰字「Patient surveys: 460 immediate post-surveys; 95 day-14 follow-ups」，左下角小字「Redrawn by EFAI-RD from arXiv:2610.41437v1 Sections 2-3 (Figure 3 text)」。右欄標題「B. Positive-rating rates by arm (* P<0.05, ** P<0.01)」，標題下方圖例為灰色「Control (minimal prompt)」與深藍「Visit preparation (standard + concise)」；九列水平長條，每列上方灰色為 Control、下方深藍為 Visit preparation，橫軸 0–100（Sessions with a positive rating, %），前四列與後五列之間有一條淺灰橫線。由上而下：Clinician: medical safety 96.4 / 93.7；Clinician: appropriateness 91.6 / 93.7；Clinician: comprehensiveness * 50.6 / 67.2；Clinician: patient alignment ** 90.4 / 98.9；Patient: visit preparedness ** 57.0 / 73.8；Patient: knowing what to ask ** 67.1 / 81.4；Patient: making the most of visit * 69.6 / 81.4；Patient: satisfaction * 62.0 / 74.0；Patient: likelihood of reuse * 65.8 / 76.6。](assets/llm-visit-preparation-study-flow-outcomes.png)

*圖：本書庫依論文 §3.1 正文與 Figure 3 說明重繪的受試者與對話流向（左），以及 §3.2–3.3 報告的兩組正向評分比例（右；臨床醫師四個維度為「所有適用步驟都給 4 或 5 分」的 session 比例，病人五項為立即問卷給 4 或 5 分的比例）。數值來自 [§3.1](https://arxiv.org/html/2610.41437v1#S3.SS1)、[§3.2](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS1)、[§3.3.1](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS1)；星號依論文標示（BH 校正後）。*

## 背景／問題

作者的出發點有兩層。第一層是使用現況：作者引用 Gallup 2026 年的民調，稱約四分之一美國成人用 AI 工具查健康資訊，其中約六成會在看診前用它研究病情、整理想法；另引用文獻指出美國基層門診常只有 15 到 20 分鐘。[(ref: main §1)](https://arxiv.org/html/2610.41437v1#S1) 這些是作者引用的二手數據，本篇沒有自行測量。

第二層是既有做法的缺口：Question Prompt List（QPL）這類靜態問題清單已有文獻顯示能增加病人提問，但需要臨床人力編製、依病種固定、並假設病人已有診斷與足夠的健康識讀能力；作者主張對話式 LLM 能動態依病人情境產生問題，但在研究前，LLM 直接對病人做結構化看診準備的安全性與幫助程度沒有被前瞻性地檢驗過。[(ref: main §1)](https://arxiv.org/html/2610.41437v1#S1) [(ref: main §4.1)](https://arxiv.org/html/2610.41437v1#S4.SS1)

「看診前準備做得好，看診就更有效率、診斷與遵從性更好」這一點，論文是引用臨床溝通研究的既有文獻支持，本研究本身沒有量測看診結果或健康結果；本篇把它當作研究動機，不是本研究證實的事。[(ref: main §1)](https://arxiv.org/html/2610.41437v1#S1)

## 方法摘要

- **三組隨機分派** — 受試者以 1:2:2 分到 Control、standard 與 concise 三種 agent；三組用同一個 Gemini 2.5 Flash 與同一個 app 介面，只差在受試者看不到的 system prompt。主分析把 standard 與 concise 合併成「visit preparation」組，與 Control 比較。[(ref: main §2.3)](https://arxiv.org/html/2610.41437v1#S2.SS3)
- **介入內容** — visit preparation agent 依受試者開場勾選的目標，走 context gathering、visit expectation setting、general health information、agenda topic generation、summarization 五個步驟；Control 只被要求回答健康問題、不給醫療建議，但同樣要每輪更新一份結構化看診摘要。[(ref: main §2.3)](https://arxiv.org/html/2610.41437v1#S2.SS3)
- **主要結果：病人自評** — 對話結束後立即填五題 5 分 Likert：visit preparedness、confidence in knowing what to ask、confidence in making the most of the visit、satisfaction、likelihood of reuse；14 天後另有探索性的追蹤問卷。[(ref: main §2.4.2)](https://arxiv.org/html/2610.41437v1#S2.SS4.SSS2)
- **次要結果：臨床醫師盲評** — 三位基層醫療醫師在不知道分組與模型的情況下，依 rubric 對每個步驟評 medical safety、appropriateness、comprehensiveness、patient alignment 四個維度。[(ref: main §2.4.1)](https://arxiv.org/html/2610.41437v1#S2.SS4.SSS1)
- **兩種觀點的對照** — 對同時有醫師評分與病人問卷的 session，計算每題問卷與每項醫師評分的 Spearman 相關，檢查兩者是否一致。[(ref: main §2.5.4)](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS4)

## 方法詳解

**受試者與排除。** 研究在 2025-11-19 至 2026-05-15 透過美國 Google Health app 線上進行，收案條件是住在美國、會說英語、18 歲以上、使用 Android 手機的 app 使用者；已知有精神疾病、性傳染病或懷孕者排除。同意後即開放使用 agent，因此作者另以 LLM 標記對話中提到排除類病症的案例，再由臨床醫師逐一人工覆核後剔除。[(ref: main §2.1)](https://arxiv.org/html/2610.41437v1#S2.SS1) [(ref: main §2.2)](https://arxiv.org/html/2610.41437v1#S2.SS2) 排除篩選與事後的看診類型、疾病領域分類都用 Gemini-3.6-Flash 加結構化輸出完成，prompt 全文在附錄 A.3。[(ref: pdf A.3, p.33)](https://arxiv.org/pdf/2610.41437v1#page=33)

**三組 prompt 的差別。** 附錄 A.2 逐字收錄三組 system prompt，並以 Figure A.2 對照：Control 只限定健康話題、聲明不能給醫療建議並規定摘要 JSON 格式，不規定對話流程；standard 是依使用者目標排序的 10 步驟準備流程，每輪簡短、一次問一題；concise 用同一流程但節奏更緊，回覆理想上少於 70 字、目標 10–15 輪、可一次併問 2–3 題，並多了討論費用／交通等實際障礙與區分預期症狀和紅旗症狀的範例。[(ref: pdf A.2, p.20)](https://arxiv.org/pdf/2610.41437v1#page=20) 不平均的 1:2:2 配置是為了取得更多 AI 準備對話供分析。[(ref: main §2.3)](https://arxiv.org/html/2610.41437v1#S2.SS3)

**醫師評分怎麼做。** 只有「完成整個準備流程」（對話涵蓋受試者開場勾選的所有目標）的 session 才進入醫師評分；每組最多隨機抽 102 段，再隨機平均分派給三位醫師之一，三位醫師都是取得專科資格、住院醫師訓練後至少 7 年經驗的基層醫療醫師。每個步驟的四個維度各給 1–5 分，4 或 5 分視為正向；patient alignment 只評 agenda topics 與 summary 兩步。[(ref: main §2.4.1)](https://arxiv.org/html/2610.41437v1#S2.SS4.SSS1) 各步驟、各維度的 rubric 定義在附錄 Table A.1，例如 summary 的 medical safety 是「不含有害幻覺」、agenda topics 的 safety 是「不太可能造成病人困擾或不當影響醫師判斷」。[(ref: pdf Table A.1, p.40)](https://arxiv.org/pdf/2610.41437v1#page=40)

**指標與檢定。** 臨床端有 4 個 dimension-level 端點（某維度所有適用步驟都給正向評分的 session 比例，以兩比例 z 檢定比較）與 17 個 step-level 端點（以 Mann–Whitney U 比較 Likert 分布），p 值以 BH 校正。另把每個 session 交叉分成 clinical reliability（safety 與 appropriateness 全部正向）× clinical utility（comprehensiveness 與 patient alignment 全部正向）四類，這一組比較未做多重比較校正。[(ref: main §2.5.1)](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS1) 病人五題問卷分成 visit readiness & confidence（三題）與 user experience（兩題）兩族各自 BH 校正；14 天追蹤兩題不校正。[(ref: main §2.5.2)](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS2) 影響因子分析用多變項 logistic regression，作者明寫為探索性、未校正。[(ref: main §2.5.3)](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS3) 相關分析以 |ρ| > 0.30 為預先設定的中度相關門檻，每題問卷內以 BH 校正。[(ref: main §2.5.4)](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS4)

**重複參與與兩個變體。** 少數受試者有多段對話，作者另只取每人第一段合格對話重做主分析（附錄 A.6）；standard 與 concise 也在附錄 A.4 以三組兩兩比較、Holm 校正分開報告。[(ref: main §2.5)](https://arxiv.org/html/2610.41437v1#S2.SS5) [(ref: pdf A.4, p.37)](https://arxiv.org/pdf/2610.41437v1#page=37) [(ref: pdf A.6, p.41)](https://arxiv.org/pdf/2610.41437v1#page=41)

- **論文未交代** — 醫師評分的評分者間一致性：每段 session 只由三位醫師中的一位評分，正文與附錄都沒有雙評或 inter-rater agreement 的數據。
- **論文未交代** — 樣本數與檢定力的事前估算，以及主要結果在試驗登錄時如何預先指定；正文只寫了已登錄 NCT07552311 並依 CONSORT 報告。
- **論文未交代** — Gemini 2.5 Flash 的 decoding 設定（例如 temperature）與研究期間模型版本是否更動。

## 資料與實驗

### 受試者與對話流向

| 階段 | Control | Visit preparation（standard + concise） | 合計 |
|---|---|---|---|
| 同意並隨機分派 | — | — | 5,960 人 |
| 開始使用（人／對話） | 321／378 | 1,335／1,579 | 1,656／1,957 |
| 排除：空白或非健康對話 | 173 | 662 | 835 |
| 排除：不是從研究入口進入 | 58 | 145 | 203 |
| 排除：受試者不符收案條件 | 6 | 47 | 53 |
| 納入分析（人／對話） | 135／141 | 667／725 | 802／866 |
| 中途結束未完成流程 | 41.1% | 42.5% | 366 段（完成 500 段，57.7%） |
| 醫師盲評 session | 83 | 189（standard 92、concise 97） | 272 |
| 立即問卷回覆 | 79 | 381（standard 196、concise 185） | 460 |
| 14 天追蹤回覆（其中有看診） | 22（13） | 73（46） | 95（59） |

[(ref: main §3.1)](https://arxiv.org/html/2610.41437v1#S3.SS1) [(ref: pdf A.4, p.37)](https://arxiv.org/pdf/2610.41437v1#page=37)

納入分析的 866 段對話中，女性 548 段（63.3%）、男性 315 段（36.4%），平均年齡 50.5 ± 14.5 歲；最常見的是專科門診（33.1%）、年度健檢（21.8%）、慢性病基層門診（17.0%）與急性問題基層門診（13.6%）。兩組人口學與疾病領域大致相近，但看診類型有中度差異：visit preparation 組較多專科門診（35.2% 對 22.7%）、較少急性基層門診（12.0% 對 22.0%）。看診類型與疾病領域是由 LLM 從對話中解析。[(ref: main §3.1)](https://arxiv.org/html/2610.41437v1#S3.SS1) [(ref: main Figure 3)](https://arxiv.org/html/2610.41437v1#S3.F3)

### 臨床醫師盲評（dimension-level，所有適用步驟皆給 4–5 分的 session 比例）

| 維度 | Control | Visit preparation | 檢定結果 |
|---|---|---|---|
| Medical safety | 96.4% | 93.7% | 無顯著差異 |
| Appropriateness | 91.6% | 93.7% | 無顯著差異 |
| Comprehensiveness | 50.6% | 67.2% | P < 0.05 |
| Patient alignment | 90.4% | 98.9% | P < 0.01 |

[(ref: main §3.2.1)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS1) [(ref: main §3.2.2)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS2)

### 臨床醫師盲評（step-level，正向評分比例）

| 步驟 × 維度 | Control | Visit preparation | 檢定結果 |
|---|---|---|---|
| Context gathering — comprehensiveness | 63.9% | 74.6% | P < 0.01 |
| Visit expectation — comprehensiveness | 86.5% | 94.8% | P < 0.01 |
| General health information — comprehensiveness | 86.4% | 92.1% | P < 0.01 |
| Agenda topics — comprehensiveness | 88.5% | 89.0% | 不顯著 |
| Summary — comprehensiveness | 85.5% | 93.7% | P < 0.01 |
| Agenda topics — patient alignment | 92.3% | 98.9% | P < 0.01 |
| Summary — patient alignment | 94.0% | 100.0% | 不顯著 |
| Context gathering — medical safety | 97.6% | 94.2% | 不顯著 |
| General health information — medical safety | 100.0% | 98.3% | 不顯著 |
| Visit expectation — medical safety | 97.3% | 100.0% | 不顯著 |

[(ref: main §3.2.1)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS1) [(ref: main §3.2.2)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS2)

### Clinical reliability × clinical utility 交叉分類

| 類別 | Control | Visit preparation | 檢定結果（未校正） |
|---|---|---|---|
| 高 reliability（全部 safety 與 appropriateness 正向） | 89.2% | 88.4% | — |
| 高 reliability 且高 utility | 50.6% | 64.6% | P < 0.05 |
| 高 reliability 但 utility 不足 | 38.6% | 23.8% | P < 0.05 |
| 高 utility 但 reliability 不足 | 0.0% | 2.6% | — |

[(ref: main §3.2.3)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS3)

### 病人自評（立即問卷給 4–5 分的比例）

| 題目 | Control | Visit preparation | 檢定結果（BH 校正） |
|---|---|---|---|
| Visit preparedness | 57.0% | 73.8% | P < 0.01 |
| Confidence in knowing what to ask | 67.1% | 81.4% | P < 0.01 |
| Confidence in making the most of the visit | 69.6% | 81.4% | P < 0.05 |
| Satisfaction | 62.0% | 74.0% | P < 0.05 |
| Likelihood of reuse | 65.8% | 76.6% | P < 0.05 |
| 14 天追蹤：看診符合 agent 事先說明的預期（有看診者） | 69.2%（n = 13） | 78.3%（n = 46） | 不顯著 |
| 14 天追蹤：看診時有提出準備好的議題（有看診者） | 69.2%（n = 13） | 71.7%（n = 46） | 不顯著 |

[(ref: main §3.3.1)](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS1) [(ref: main Figure 5)](https://arxiv.org/html/2610.41437v1#S3.F5)

## 結果

- **安全性沒有拉開差距** — 兩組在所有適用步驟都拿到正向 medical safety 評分的比例分別為 96.4%（Control）與 93.7%（visit preparation），appropriateness 為 91.6% 與 93.7%，BH 校正後各步驟都沒有顯著差異。[(ref: main §3.2.1)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS1)
- **完整度與貼合度上升** — comprehensiveness 由 50.6% 升到 67.2%（P < 0.05）、patient alignment 由 90.4% 升到 98.9%（P < 0.01）；step-level 的完整度在五個步驟中有四個顯著較高，agenda topics 是例外（88.5% 對 89.0%）。[(ref: main §3.2.2)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS2)
- **多出來的是「安全又有用」的 session** — 高 reliability 的比例兩組相近（89.2% 對 88.4%），但其中 utility 不足的比例由 38.6% 降到 23.8%，兩者皆高的比例由 50.6% 升到 64.6%（皆 P < 0.05，未校正）；作者稱為「unsafe helpfulness」的高 utility、低 reliability 類別在 visit preparation 組占 2.6%，Control 為 0.0%。[(ref: main §3.2.3)](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS3)
- **病人自評五題全部較高** — visit preparedness 73.8% 對 57.0%（多 16.8 個百分點，P < 0.01），其餘四題也都顯著較高；14 天追蹤只有 59 位回覆者在期間內看過診，兩題都沒有達到顯著。[(ref: main §3.3.1)](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS1)
- **調整共變項後大致仍在** — 多變項 logistic regression 中，visit preparation 組與「覺得準備好」「知道要問什麼」「滿意」顯著相關；「充分利用看診」與「願意再用」方向一致但未達顯著。這組分析作者明寫為探索性、未校正多重比較。[(ref: main §3.3.2)](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS2)
- **病人自評與醫師評分沒有顯著相關** — 對同時有兩種評分的 session，校正多重比較後，沒有任何一題問卷與任何一個步驟、維度的醫師評分達到顯著相關；作者據此主張病人滿意度不能代替臨床品質，反之亦然。[(ref: main §3.4)](https://arxiv.org/html/2610.41437v1#S3.SS4) [(ref: pdf A.8, p.49)](https://arxiv.org/pdf/2610.41437v1#page=49)
- **兩個變體分開看** — standard 與 concise 在任何結果上都沒有顯著差異（例如 comprehensiveness 66.3% 對 68.0%）；與 Control 兩兩比較、Holm 校正後，完整度合成指標兩個變體都不再顯著，病人端只有 standard 的四題仍顯著，concise 五題都不顯著。作者說明這組分析未針對兩兩比較設計檢定力。[(ref: pdf A.4, p.37)](https://arxiv.org/pdf/2610.41437v1#page=37) [(ref: pdf A.4.3, p.38)](https://arxiv.org/pdf/2610.41437v1#page=38)
- **只取每人第一段對話** — 結論不變：comprehensiveness 66.7% 對 49.4%、patient alignment 98.9% 對 90.1%、visit preparedness 74.2% 對 56.4%，safety 與 appropriateness 仍無顯著差異。[(ref: pdf A.6, p.41)](https://arxiv.org/pdf/2610.41437v1#page=41)

## 限制

作者自列的限制：[(ref: main §4.2)](https://arxiv.org/html/2610.41437v1#S4.SS2)

1. **流程完成率** — 納入分析的對話有 42.3% 沒走完準備流程，降低有效樣本與次群組分析的檢定力。
2. **醫師評分的存活者偏差** — 醫師只評完成流程的 session；若有人因 agent 表現不佳而中途離開，醫師評分會高估整體對話品質。作者指出兩組中途結束率相近，因此較不影響組間比較，但絕對分數只代表完成的對話。
3. **追蹤樣本太小** — 14 天追蹤回覆少、期間內真的看診者更少，無法確認準備效果是否延續到實際看診。
4. **族群代表性** — 受試者是主動使用 Google Health app 並自願加入研究的 Android 使用者，科技參與度與健康識讀可能高於一般病人；研究沒有收集教育、社經、語言、種族與保險等變項。

本書庫補充的閱讀限制：

5. **分析前的大量排除** — 5,960 人同意並分派後只有 1,656 人開始使用，開始使用的 1,957 段對話中又有 1,091 段在分析前被排除（空白或非健康對話、非研究入口、不符條件）；Control 組排除比例（237／378，62.7%）高於 visit preparation 組（854／1,579，54.1%），這是依論文 §3.1 計數換算的結果，論文沒有討論兩組排除比例差異的影響。[(ref: main §3.1)](https://arxiv.org/html/2610.41437v1#S3.SS1)
6. **主要結果是自評、回覆率約五成** — 立即問卷只回收 866 段中的 460 段；主要結果是受試者自填的感受，不是看診中的溝通品質或健康結果。[(ref: main §3.1)](https://arxiv.org/html/2610.41437v1#S3.SS1)
7. **單一評分者** — 每段 session 只有一位醫師評分，論文未報告評分者間一致性，醫師端比例的不確定性只反映抽樣，不反映評分者差異。[(ref: main §2.4.1)](https://arxiv.org/html/2610.41437v1#S2.SS4.SSS1)
8. **自家產品、自家模型** — 研究由 Alphabet 出資、全體作者來自 Google Research，評估的是 Google Health app 上以 Gemini 建構的 agent；論文已揭露利益衝突。結果只涵蓋 Gemini 2.5 Flash 一個模型與一種介面。[(ref: main Competing Interests)](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx4) [(ref: main §2.3)](https://arxiv.org/html/2610.41437v1#S2.SS3)
9. **比較的是「結構化 prompt」對「幾乎沒有 prompt」** — Control 是刻意極簡的 prompt，用來近似一般人不特別下指令時的體驗；這組結果說明結構化流程勝過放任回答，不能直接推到與靜態 QPL、護理衛教或其他設計的比較。[(ref: main §2.3)](https://arxiv.org/html/2610.41437v1#S2.SS3)

## 與書庫其他文章的關係

兩篇都把 LLM 放在病人面前並同時收集病人與醫師兩種評價，結論方向一致：米蘭那篇病人 63.3% 偏好 AI 改寫的乳房報告、醫師卻只認為 72.0% 至少正確，本篇則發現病人自評與醫師評分在同一批對話上沒有顯著相關，兩篇都說明病人偏好不能當作臨床品質的代理指標: [病人 63.3% 選 AI 改寫的乳房報告，醫師只給 72%「正確」](2026-11-03-llm-breast-report-simplification-patient-preference.md)

該文量出醫療 LLM 文獻中 randomized／controlled／prospective 設計只占 2.5%、評估落後模型發布約 18 個月；本篇是少見的前瞻性隨機研究，但收案在 2025-11 至 2026-05、評估的是 Gemini 2.5 Flash，正好同時示範了證據等級的提升與模型新鮮度的落差: [醫療 LLM 研究愈來愈嚴謹，評到的模型卻愈來愈舊](2026-09-17-medical-llm-evaluation-gap.md)

## 實務的啟發

以下是本書庫的解讀，不是論文的結論。

- **「同一模型換 prompt」是可借用的實驗設計** — 三組只差 system prompt，讓組間差異能歸到互動流程本身，而不是模型能力；要評估自家的病人端 LLM 流程時，先準備一個極簡 prompt 的對照組，比只和「不用 AI」比較更能看出流程設計的貢獻。這個設計的前提是附上完整 prompt，本研究在附錄 A.2 做到了。
- **病人自評與醫師評分要分開收、分開報** — 本研究兩者沒有顯著相關，代表只看滿意度或只看醫師 rubric 都會漏掉另一半；在缺乏評分者間一致性數據的情況下，醫師端也應至少抽一部分做雙評。
- **安全性結論的強度有限** — 「兩組 safety 都在 93% 以上、沒有顯著差異」是在單一評分者、只評完成流程的 session、樣本 272 段下得到的；它是不劣於極簡 prompt 的初步訊號，不是已證實安全。2.6% 的高 utility 低 reliability 案例，更適合當作逐案檢視失效模式的起點。
- **自評改善不等於看診改善** — 本研究沒有量測看診中的溝通、決策或健康結果，14 天追蹤只有 59 位看過診的回覆者；把這類工具放進院內流程前，仍需要以醫師端回饋或臨床結果為終點的研究。

## References

- `main` — *A prospective randomized study of patient-centered AI for clinical visit preparation*, arXiv HTML v1: <https://arxiv.org/html/2610.41437v1>
  - 深鏈：[§1](https://arxiv.org/html/2610.41437v1#S1)、[§2.1](https://arxiv.org/html/2610.41437v1#S2.SS1)、[§2.2](https://arxiv.org/html/2610.41437v1#S2.SS2)、[§2.3](https://arxiv.org/html/2610.41437v1#S2.SS3)、[§2.4.1](https://arxiv.org/html/2610.41437v1#S2.SS4.SSS1)、[§2.4.2](https://arxiv.org/html/2610.41437v1#S2.SS4.SSS2)、[§2.5](https://arxiv.org/html/2610.41437v1#S2.SS5)、[§2.5.1](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS1)、[§2.5.2](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS2)、[§2.5.3](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS3)、[§2.5.4](https://arxiv.org/html/2610.41437v1#S2.SS5.SSS4)、[§3.1](https://arxiv.org/html/2610.41437v1#S3.SS1)、[Figure 3](https://arxiv.org/html/2610.41437v1#S3.F3)、[§3.2.1](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS1)、[§3.2.2](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS2)、[§3.2.3](https://arxiv.org/html/2610.41437v1#S3.SS2.SSS3)、[§3.3.1](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS1)、[Figure 5](https://arxiv.org/html/2610.41437v1#S3.F5)、[§3.3.2](https://arxiv.org/html/2610.41437v1#S3.SS3.SSS2)、[§3.4](https://arxiv.org/html/2610.41437v1#S3.SS4)、[§4.1](https://arxiv.org/html/2610.41437v1#S4.SS1)、[§4.2](https://arxiv.org/html/2610.41437v1#S4.SS2)、[Data Availability](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx2)、[Code Availability](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx3)、[Competing Interests](https://arxiv.org/html/2610.41437v1#S5.SS0.SSSx4)
- `abs` — arXiv abstract page 2610.41437v1: <https://arxiv.org/abs/2610.41437v1>；DOI: <https://doi.org/10.48550/arXiv.2610.41437>
- `pdf` — arXiv PDF v1（正文與附錄）: <https://arxiv.org/pdf/2610.41437v1>
  - 深鏈：[A.2 system prompts（p.20）](https://arxiv.org/pdf/2610.41437v1#page=20)、[A.3 post-analysis prompts（p.33）](https://arxiv.org/pdf/2610.41437v1#page=33)、[A.4 three-way comparison（p.37）](https://arxiv.org/pdf/2610.41437v1#page=37)、[A.4.3（p.38）](https://arxiv.org/pdf/2610.41437v1#page=38)、[Table A.1 rubrics（p.40）](https://arxiv.org/pdf/2610.41437v1#page=40)、[A.6 first-session analysis（p.41）](https://arxiv.org/pdf/2610.41437v1#page=41)、[A.8 joint analysis（p.49）](https://arxiv.org/pdf/2610.41437v1#page=49)

[Home](../) · [AI Papers](./)
