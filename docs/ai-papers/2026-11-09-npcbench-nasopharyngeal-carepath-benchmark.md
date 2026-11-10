---
parent: AI Papers
nav_order: 3
title: "NPCBench：照護題答對近九成，同一位鼻咽癌病人全對最多 23%"
catalog_id: "arxiv:2611.08369"
editors:
  - "Clare"
refs:
  main:
    title: "NPCBench: A Clinical Apprenticeship Benchmark for Multimodal Care-Pathway Reasoning in Nasopharyngeal Carcinoma"
    url: "https://arxiv.org/html/2611.08369v1"
  abs:
    title: "arXiv abstract page: 2611.08369v1"
    url: "https://arxiv.org/abs/2611.08369v1"
  code:
    title: "NPCBench evaluation code (GitHub)"
    url: "https://github.com/pidneuralode/NPCBench"
  data:
    title: "NPCBench dataset (Hugging Face)"
    url: "https://huggingface.co/datasets/pengkaiScience/NPCBench"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# NPCBench：照護題答對近九成，同一位鼻咽癌病人全對最多 23%

## 來源

- 團隊：Pengkai Wang、Wei-Wei Zhang、Yan Li、Min Tang 等 16 位作者（末位為 Ying Sun、Hongxia Yang）；單位為 The Hong Kong Polytechnic University、infix.ai、Sun Yat-sen University、Sun Yat-sen University Cancer Center 與 Monash University。HTML 版作者欄標出共同第一作者與通訊作者，但未逐一對應作者與單位，本文不列對應關係。[(ref: main author block)](https://arxiv.org/html/2611.08369v1)
- 論文：*NPCBench: A Clinical Apprenticeship Benchmark for Multimodal Care-Pathway Reasoning in Nasopharyngeal Carcinoma*，arXiv:2611.08369v1（cs.AI），2026-11-05 提交，目前只有 v1；授權為 CC BY 4.0；arXiv 頁註記已被 NeurIPS 2026 Evaluations and Datasets Track 接受。[(ref: abstract)](https://arxiv.org/abs/2611.08369v1)
- 識別碼：arXiv [2611.08369](https://arxiv.org/abs/2611.08369v1)；DOI [10.48550/arXiv.2611.08369](https://doi.org/10.48550/arXiv.2611.08369)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.08369v1)、[PDF v1](https://arxiv.org/pdf/2611.08369v1)。
- 程式與資料：評估程式碼在 GitHub（作者自有程式碼 MIT 授權）[(ref: code)](https://github.com/pidneuralode/NPCBench)，去識別化的題目、影像資產與參考標註在 Hugging Face（原始資料與標註 CC BY 4.0）[(ref: data)](https://huggingface.co/datasets/pengkaiScience/NPCBench)；回溯性使用臨床資料經 IRB 核准（B2026-465-01）。[(ref: main App. A)](https://arxiv.org/html/2611.08369v1#A1)
- 研究性質：評估基準（benchmark）論文，不提出新模型；完整研究而非 pilot，30 個模型全部實際跑過，含配對控制實驗與醫師對 LLM judge 的校準。[(ref: main §4.1)](https://arxiv.org/html/2611.08369v1#S4.SS1)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、Table 1–2 與附錄 Table A2、A19 為準；各模型的取樣參數論文只寫「依釋出的評估程式碼」，未納入本文引述。[(ref: main App. C)](https://arxiv.org/html/2611.08369v1#A3)

**編輯：** Clare

作者用鼻咽癌（nasopharyngeal carcinoma，NPC）建了一個從指引題到同一病人完整照護路徑的基準，測 30 個模型後發現：照護決策單題可答對近九成，但要求同一位病人的病理、MRI T 分期與每一個照護答案全對時，21 個多模態模型最高只有 23%。[(ref: main Table 1)](https://arxiv.org/html/2611.08369v1#S4.T1)

## 流程

![左右兩欄圖。左欄標題「NPCBench ladder (L1-L6) + consultation suite (O1)」，六個圓角框由上而下以向下箭頭相連：前四個為淺藍色，依序為「L1 G-Mem: guideline memory／250 MCQ (CSCO / NCCN)」「L2 A-App: atomic guideline application／185 short-vignette MCQ」「L3 MM-EG: pathology + MRI evidence grounding／69 pathology; 400 T + 400 N stage; 200 sequence」「L4 C-Plan: case-level planning／165 MCQ over 84 patients」；後兩個為淺橘色，依序為「L5 L-Rev: longitudinal revision／305 turns over 100 patients」「L6 CP-Epi: CarePath episodes／100 patients: 100 pathology + 100 MRI T + 217 care」。右側一個淺綠色圓角框「O1 C-Rub」，內文「103 free-text consultations／42 cases／1,726 rubric criteria」與「LLM judge + physician audits」。左下斜體字「Strict (per patient) = pathology correct AND MRI T correct AND every care answer correct」，其下小字「Redrawn by EFAI-RD from arXiv:2611.08369v1 Sec. 3.3 and Table A2」。右欄為長條圖，標題「Table 1 / Table A19: CarePath (L6), six of 21 multimodal models」，縱軸 0–100%，每個模型兩根柱，藍色為「Care accuracy (217 decisions)」、橘色為「Strict success (100 patients)」：Gemini-3.1-Pro-Preview 89.9／11.0、Gemini-2.5-Pro 80.6／15.0、Claude-Sonnet-4.6 80.6／23.0、GPT-5.1 71.0／2.0、Lingshu-32B 55.3／2.0、Hulu-Med-32B 47.5／10.0。](assets/npcbench-ladder-carepath-strict.png)

*圖：本書庫依論文 §3.3 與 Table A2 重繪的 NPCBench 六層能力階梯與 O1 會診題組（左），以及 CarePath 上六個多模態模型的 Care 準確率與 Strict 成功率（右）。數值來自 [Table 1](https://arxiv.org/html/2611.08369v1#S4.T1) 與 [Table A19](https://arxiv.org/html/2611.08369v1#A3.T19)。*

## 背景／問題

醫療 LLM 與多模態 LLM（MLLM）在醫學考題、醫療 VQA 與大型評測組合上已有很高的分數；作者的出發點是，考題式準確率看不出模型能否在次專科照護中整合疾病指引、多模態證據與隨時間變化的病人狀態。[(ref: main §1)](https://arxiv.org/html/2611.08369v1#S1)

「單題分數高不代表同一病人的決策彼此一致」這個前提，論文以自身的實驗支持（見下文 CarePath 結果），引用的既有工作則多是說明方向，而非量化這個落差的大小。[(ref: main §1)](https://arxiv.org/html/2611.08369v1#S1) [(ref: main §2)](https://arxiv.org/html/2611.08369v1#S2)

作者選鼻咽癌，理由是它的診斷、分期與風險評估需要同時整合病理、多序列 MRI 與血漿 EBV DNA，治療與追蹤期間的腫瘤反應、毒性與復發又會改變後續決策；論文為這些臨床描述引用了指引與流行病學文獻。[(ref: main §1)](https://arxiv.org/html/2611.08369v1#S1)

## 方法摘要

- **能力階梯** — 依專科醫師訓練的順序分六層：L1 指引記憶、L2 指引的單點應用、L3 病理與 MRI 證據判讀、L4 單一時點的個案規劃、L5 縱向病程中的決策修正、L6 同一病人的 CarePath 照護路徑；另有 O1 開放式會診題組。[(ref: main §3.1)](https://arxiv.org/html/2611.08369v1#S3.SS1)
- **病人層級終點** — CarePath 同時報兩個數：Care 是 217 個照護決策逐題平均的準確率；Strict 要求同一位病人的病理判讀、MRI T 分期與所有被計分的照護答案全部正確，以病人為單位計算。[(ref: main §4.1 Eq. 1)](https://arxiv.org/html/2611.08369v1#S4.SS1)
- **配對控制** — 固定病人與題目，只換一個條件：拿掉選項改簡答、完整病史對去掉時間標記的快照、病史行序打亂、以參考的影像判讀取代模型自己的判讀。[(ref: main §4.3)](https://arxiv.org/html/2611.08369v1#S4.SS3) [(ref: main §4.5)](https://arxiv.org/html/2611.08369v1#S4.SS5)
- **Judge 校準** — O1 的自由文字回答由 GPT-OSS-120B 依 rubric 逐條判分，再用兩組醫師標註（Targeted Audit 與 Expanded Audit）檢查四個 judge 與醫師的一致性。[(ref: main §4.4)](https://arxiv.org/html/2611.08369v1#S4.SS4)

## 方法詳解

- **題目來源與審查** — L1–L2 由 CSCO 與 NCCN 指引改寫；L3 用病理切片與多序列 MRI；L4–L6 與 O1 取自去識別化的真實病歷。腫瘤、病理與放射專科審查者檢查臨床效度、證據是否足以支持單一答案，以及參考標準；設計原則之一是「證據邊界控制」：只給到該決策時點為止的資訊，移除之後的治療、結果與會洩題的線索。[(ref: main §3.2)](https://arxiv.org/html/2611.08369v1#S3.SS2) [(ref: main §3.1)](https://arxiv.org/html/2611.08369v1#S3.SS1)
- **影像標註** — 例行臨床由 1–3 年資歷醫師初判、五年以上次專科醫師定稿；病理參考標籤取自定稿報告。MRI 的結構侵犯與 T 分期標籤由另一位醫師獨立重判，分歧由三位資深鼻咽癌放射腫瘤科醫師共識決定。T／N 分期標籤依第八版 AJCC/UICC、由報告推得。[(ref: main App. D.1)](https://arxiv.org/html/2611.08369v1#A4.SS1) [(ref: main App. A.2)](https://arxiv.org/html/2611.08369v1#A1.SS2)
- **MRI 輸入形式** — T 分期中 100 位病人以每人 27 張以結構為中心的影像卡呈現（這 100 人構成 18 個基礎結構的解剖面板），其餘 300 位與全部 N 分期病人則以同一平面對齊的序列組呈現（軸位 T1、T2、增強 T1 上下堆疊），每張切片保留 512×512 顯示格。[(ref: main App. C)](https://arxiv.org/html/2611.08369v1#A3)
- **CarePath 的組成** — 100 位病人中 25 位有本人配對的病理切片，另外 75 位使用「指定的」病理標本作為代理（全部為 NPC 陽性），MRI 與臨床紀錄則都與病人本人連結。照護題在提示中帶入模型自己預測的病理與 T 分期，部分題目另給參考的 N／M／整體分期；主要協定不提供模型先前的照護答案。[(ref: main App. A.3)](https://arxiv.org/html/2611.08369v1#A1.SS3) [(ref: main App. C.3.5)](https://arxiv.org/html/2611.08369v1#A3.SS3.SSS5)
- **CarePath 的難度富集** — 四個「建構用模型」（HealthGPT-Pro-8B、Qwen3-VL-8B、Qwen3-VL-30B-A3B、Qwen3.5-27B）參與挑選：在 25 位配對病人之外，其餘 86 位審查過的病人依建構模型的錯誤數排序取前 75 位，並把四個模型全答對的檢查點移出計分，得到 217 個決策，其中 93 個是至少兩個建構模型答錯的題。作者在結果表中以 † 標出這四個模型。[(ref: main App. C.3.5)](https://arxiv.org/html/2611.08369v1#A3.SS3.SSS5)
- **答案擷取與計分** — 選擇題以明確的最終答案為準，缺漏或互相矛盾的答案記為錯且留在分母；多選題須與參考答案集合完全相同才給分。O1 每條正向要求依權重加分、觸發 major／minor error 各扣 2／1 分，題目層級下限為零後正規化到 0–100。[(ref: main App. C)](https://arxiv.org/html/2611.08369v1#A3) [(ref: main §3.3)](https://arxiv.org/html/2611.08369v1#S3.SS3)
- **提示與輸出上限** — 各子任務的提示模板列在附錄 E（例如 L1–L4 要求直接輸出選項字母）。CarePath 的輸出上限為本機模型 1,024 tokens、API 模型 8,192 tokens；O1 的主要 judge 用 temperature 0、top-p 1。[(ref: main App. E)](https://arxiv.org/html/2611.08369v1#A5) [(ref: main App. C)](https://arxiv.org/html/2611.08369v1#A3)
- **不確定性** — Care 準確率與配對比較用病人層級 cluster bootstrap 的 95% 區間；Strict 用 100 位病人的 exact binomial（Clopper–Pearson）區間；醫師校準用回答層級的 cluster 重抽。作者註明多模型區間是描述性的，未做多重比較校正。[(ref: main App. C.2.3)](https://arxiv.org/html/2611.08369v1#A3.SS2.SSS3)
- **論文未交代** — 各模型的取樣參數（temperature 等）論文只寫在釋出的評估程式碼中，正文與附錄沒有逐模型列出。
- **論文未交代** — 參與審查與兩組 Audit 的醫師人數，正文與附錄只描述流程與標註數量，未給審查者總人數。

## 資料與實驗

### 資料

| 子集 | 評估單位 | 規模 | 來源 | 參考標註 |
|---|---|---|---|---|
| L1 G-Mem | 指引記憶選擇題 | 250 題（153 題 CSCO 與 NCCN 皆支持、80 題僅 CSCO、17 題僅 NCCN） | NPC 指引 | 專家驗證的指引知識 |
| L2 A-App | 短情境選擇題 | 185 題（初始根治治療 84、復發 30、轉移／全身治療 44、毒性或禁忌 27） | 臨床情境 | 專科審查答案 |
| L3 MM-EG | 病理／MRI 多模態題 | 69 個病理總覽、2,700 張 MRI 結構卡、400 例 T 分期、400 例 N 分期、200 題序列辨識 | 病理與 MRI 影像 | 專家驗證的病理、影像與分期標籤 |
| L4 C-Plan | 個案選擇題 | 165 題，84 位病人 | 臨床情境 | 專科審查的治療計畫 |
| L5 L-Rev | 縱向逐輪選擇題 | 100 位真實病人、305 題 | 去識別化縱向病歷 | 醫師裁定的決策輪次 |
| L6 CP-Epi | CarePath 照護決策 | 100 位病人、417 個計分任務（病理 100、MRI T 100、照護 217） | 臨床病程 | 裁定的照護決策；75 例病理為代理 |
| O1 C-Rub | 開放式會診 | 103 題、42 個案例、1,726 條 rubric（正向 1,069、錯誤 657） | 會診情境 | 結構化計分錨點 |

*資料：整理自 [Table A2](https://arxiv.org/html/2611.08369v1#A1.SS1)、[App. A.1](https://arxiv.org/html/2611.08369v1#A1.SS1) 與 [Table A5](https://arxiv.org/html/2611.08369v1#A1.SS3)。*

| MRI 隊列 | 病人數 | 類別分布 | 檢查期間 |
|---|---|---|---|
| T 分期（含 100 人解剖面板） | 400 | T1／T2／T3／T4 = 50／50／150／150 | 2021-03 至 2024-06 |
| N 分期（與 T 隊列病人不重疊） | 400 | N0／N1／N2／N3 = 80／160／80／80 | 2021-03 至 2024-06 |
| 外部 T 分期（Nanfang Hospital） | 53（另 2 例無確定參考標籤未計分） | T1／T2／T3／T4 = 4／8／31／10 | 2023-01 至 2024-12 |

*資料：[App. A.2](https://arxiv.org/html/2611.08369v1#A1.SS2)。主要 L3 MRI 任務共 874 位不重複病人；EHR 任務的原始病歷日期跨 2008–2025。*

### 實驗：主表節錄（Table 1）

30 個模型中，9 個純文字模型只做 L1、L2、L4、L5、O1，21 個多模態模型另做 L3 與 L6。下表節錄 10 個模型；數值為百分比，C-Rub. 為 GPT-OSS-120B judge 下的 0–100 分，† 為 CarePath 建構用模型，– 為無影像介面。

| Model | G-Mem. | A-App. | Path. | T-Stg. | N-Stg. | C-Plan | L-Rev. Turn | L-Rev. All-turn | CP-Epi. Care | CP-Epi. Strict | C-Rub. |
|---|---|---|---|---|---|---|---|---|---|---|---|
| HuatuoGPT-o1-72B | 88.4 | 73.9 | – | – | – | 46.9 | 63.9 | 26.0 | – | – | 10.1 |
| DeepSeek-V3.1 | 90.0 | 81.0 | – | – | – | 51.8 | 74.4 | 42.0 | – | – | 28.2 |
| Hulu-Med-32B | 86.0 | 74.5 | 60.9 | 29.0 | 20.0 | 53.4 | 70.2 | 37.0 | 47.5 | 10.0 | 7.6 |
| Lingshu-32B | 85.6 | 61.0 | 59.4 | 37.5 | 20.0 | 53.3 | 70.5 | 37.0 | 55.3 | 2.0 | 9.0 |
| Qwen3.5-27B† | 89.2 | 75.8 | 71.0 | 37.0 | 27.3 | 61.0 | 76.4 | 46.0 | 62.7 | 1.0 | 46.8 |
| Qwen3.6-27B | 87.6 | 71.4 | 71.0 | 37.5 | 42.8 | 50.3 | 79.7 | 53.0 | 65.9 | 5.0 | 47.2 |
| GPT-5.1 | 90.4 | 80.9 | 62.3 | 27.3 | 32.8 | 63.5 | 75.7 | 45.0 | 71.0 | 2.0 | 58.4 |
| Gemini-3.1-Pro-Preview | 94.0 | 92.5 | 63.8 | 31.0 | 38.5 | 71.9 | 87.9 | 71.0 | 89.9 | 11.0 | 47.8 |
| Gemini-2.5-Pro | 93.2 | 85.8 | 60.9 | 37.5 | 26.0 | 67.0 | 82.0 | 56.0 | 80.6 | 15.0 | 38.5 |
| Claude-Sonnet-4.6 | 93.2 | 86.1 | 56.5 | 33.5 | 27.3 | 69.2 | 85.2 | 63.0 | 80.6 | 23.0 | 47.5 |

*表：節錄自 [Table 1](https://arxiv.org/html/2611.08369v1#S4.T1)；原表另有 Seq.（MRI 序列）與 Struct.（結構辨識）兩欄。T-Stg.／N-Stg. 各為 400 例；A-App. 與 C-Plan 為群組／病人層級 macro 平均。*

### 實驗：CarePath 的區間（Table A19）

| Model | T | Bal. T | Care [95% CI] | All-care | Strict [95% CI] |
|---|---|---|---|---|---|
| Hulu-Med-32B | 52.0 | 26.3 | 47.5 [41.3, 53.5] | 19.0 | 10.0 [4.9, 17.6] |
| Lingshu-7B | 45.0 | 26.3 | 44.2 [37.3, 50.8] | 16.0 | 9.0 [4.2, 16.4] |
| GPT-5.1 | 39.0 | 28.7 | 71.0 [64.4, 77.0] | 46.0 | 2.0 [0.2, 7.0] |
| Gemini-3.1 | 19.0 | 22.4 | 89.9 [85.4, 93.9] | 83.0 | 11.0 [5.6, 18.8] |
| Gemini-2.5-Pro | 26.0 | 19.1 | 80.6 [75.0, 86.2] | 71.0 | 15.0 [8.6, 23.5] |
| Claude-4.6 | 40.0 | 24.1 | 80.6 [75.3, 85.6] | 64.0 | 23.0 [15.2, 32.5] |

*表：節錄自 [Table A19](https://arxiv.org/html/2611.08369v1#A3.T19)。T 與 Bal. T 為 100 位病人的 MRI T 分期準確率與平衡準確率；Care 為 217 個決策；All-care 與 Strict 為 100 位病人。Care 的區間為病人 cluster bootstrap，Strict 為 exact binomial。*

### 實驗：judge 與醫師的一致性（Table 2）

| Judge | Targeted Audit 一致率（n=548） | Targeted κ | Expanded Audit 一致率（n=1,013） | Expanded κ |
|---|---|---|---|---|
| GPT-4.1 | 77.7 | 0.553 | 77.6 | 0.547 |
| GPT-OSS-120B | 81.4 | 0.610 | 70.5 | 0.387 |
| Qwen3-30B | 73.2 | 0.472 | 76.9 | 0.538 |
| Qwen3.6-27B | 79.4 | 0.578 | 77.8 | 0.544 |

*表：[Table 2](https://arxiv.org/html/2611.08369v1#S4.T2)；n 為 criterion 層級的標註數，κ 為 Cohen's κ。Expanded Audit 的 1,013 條標註來自九個模型在六個案例上的 54 份回答。*

## 結果

- **指引記得住，不等於個案規劃得好** — L1 指引記憶最高超過 92%，L4 個案規劃最高只有 71.9%（Gemini-3.1-Pro-Preview）；GPT-5.1 與 DeepSeek-V3.1 的 L1、L2 相近，L4 卻是 63.5% 對 51.8%。在 71 題經醫師審核的 L1 題目上拿掉選項，Gemini-3.1-Pro-Preview、GPT-4.1、GPT-5.1 分別掉 7.0、12.7、15.5 個百分點。[(ref: main §4.2)](https://arxiv.org/html/2611.08369v1#S4.SS2)
- **MRI 分期接近多數類基線** — 400 例 T 分期最高 43.5%，多數類基線為 37.5%；400 例 N 分期最高 42.8%，多數類基線為 40.0%。N 分期最高的 Qwen3.6-27B 平衡準確率只有 31.9%。[(ref: main §4.3)](https://arxiv.org/html/2611.08369v1#S4.SS3)
- **分期對了，解剖證據多半不對** — 在 100 人解剖面板上，T 分期直接準確率最高 43.0%，但 18 個結構侵犯全對、以及「結構標籤與最終分期都對」的成功率都低於 5.0%。給參考的結構判讀時，固定規則與固定的 GPT-OSS-120B 分期器都達 99.0%；改成只給正確解剖位置、侵犯由模型判讀時，Gemini-3.1 降到 49.0%，全部由模型判讀時為 36.0%。[(ref: main §4.3)](https://arxiv.org/html/2611.08369v1#S4.SS3)
- **縱向病史有修正也有新錯** — L5 上 Gemini-3.1-Pro-Preview 逐輪 87.9%、整位病人全對 71.0%，Claude-Sonnet-4.6 為 85.2% 與 63.0%。完整病史對去掉時間標記的快照，20 個模型中有 19 個的病人 bootstrap 區間跨過零；GPT-5.1 有 22 題只在完整病史下答對、19 題只在快照下答對，逐輪準確率淨升 1.0 個百分點，整位病人全對卻降 1.0 個百分點。[(ref: main §4.3)](https://arxiv.org/html/2611.08369v1#S4.SS3)
- **CarePath 的組合落差** — Gemini-3.1 的 Care 為 89.9%（195／217）、All-care 為 83.0%，Strict 只有 11.0%；Claude-4.6 的 Care 80.6%、All-care 64.0%，Strict 為 21 個多模態模型中最高的 23.0%（95% CI 15.2–32.5%）。Gemini-3.1 有 72 位病人照護答案全對但病理或 T 分期至少一項錯，Claude-4.6 為 41 位；反過來，Hulu-Med-32B 有 38 位病人兩個診斷標籤都對、照護答案至少錯一題。[(ref: main §4.5)](https://arxiv.org/html/2611.08369v1#S4.SS5)
- **T 分期是 Strict 的主要瓶頸** — CarePath 上固定回答 T3 可得 58%，高於最佳模型的 52%；平衡 T 準確率最高 30.5%，固定回答為 25%。[(ref: main §4.5)](https://arxiv.org/html/2611.08369v1#S4.SS5) 依 Table A19，21 個模型的 CarePath T 準確率介於 4.0% 到 52.0%。[(ref: main Table A19)](https://arxiv.org/html/2611.08369v1#A3.T19)
- **給正確的影像判讀，照護答案也沒有一致變好** — 在 25 位配對病人的 146 題上，14 個本機模型改用參考的病理、T 分期與侵犯判讀後，病人平均照護準確率的變化在 −3.2 到 +4.1 個百分點，14 個區間中有 12 個包含零。[(ref: main §4.5)](https://arxiv.org/html/2611.08369v1#S4.SS5)
- **會診分數高，錯誤也不少** — O1 最高分的 GPT-5.1 為 58.4 分，主要 judge 判定其 14.6% 的回答觸發 major error、40.8% 觸發 minor error；改以 42 個案例等權重計分，各模型分數只變動 −2.0 到 +0.1 分。[(ref: main §4.4)](https://arxiv.org/html/2611.08369v1#S4.SS4)
- **主要 judge 漏抓的比例不低** — 在 Expanded Audit 上，GPT-OSS-120B 與醫師的一致率為 70.5%（95% CI 66.2–77.7%），sensitivity 51.8%、specificity 85.8%；作者說明「陽性」指該 criterion 成立（包括錯誤確實存在），漏判錯誤等於少扣分。[(ref: main §4.4)](https://arxiv.org/html/2611.08369v1#S4.SS4)

## 限制

- **作者列出的限制** — 主要為單一中心資料；CarePath 有 75 例使用由模型挑選的指定病理標本；分數對類別分布與病程長度敏感；Expanded Audit 只有六個案例。作者認為需要更多多中心、模態完整配對的隊列與前瞻研究，才能確認基準分數的提升是否改善照護。[(ref: main §5)](https://arxiv.org/html/2611.08369v1#S5) 附錄另列出疾病特定的回溯資料、以 2D 影像卡呈現 MRI、各任務計分深度不一，以及依賴自動會診 judge。[(ref: main App. A.1)](https://arxiv.org/html/2611.08369v1#A1.SS1)
- **難度富集影響絕對數值的解讀** — CarePath 的病人與決策是依四個建構模型的錯誤挑選，並移除四者全答對的檢查點（[App. C.3.5](https://arxiv.org/html/2611.08369v1#A3.SS3.SSS5)）。本書庫的解讀是：Care 與 Strict 的絕對值描述的是「這批刻意偏難的決策」上的表現，不宜直接當成一般臨床病程中的答對率；建構模型（†）與其他模型之間的比較也不完全對等。
- **病理代理讓 Strict 主要反映 T 分期** — 75 位指定標本的病人病理全為陽性，圖 4 註明 CarePath 病理的多數類基線為 99%；因此 Strict 的差異大多來自 MRI T 分期，而 T 分期準確率又低於固定答 T3 的基線。[(ref: main Fig. 4)](https://arxiv.org/html/2611.08369v1#S4.F4)
- **參考標籤取自報告** — T／N 分期標籤由報告推得，結構侵犯標籤由一位醫師重判後再由三位資深醫師裁決分歧；標註者間一致性在正文與附錄都沒有報告。[(ref: main App. D.1)](https://arxiv.org/html/2611.08369v1#A4.SS1)
- **評估方式的邊界** — 照護題是選擇題、逐題獨立作答，主要協定不讓模型看到自己先前的照護答案；O1 的分數依賴一個與醫師一致率 70.5% 的 judge。多模型區間未做多重比較校正。[(ref: main App. C.3.5)](https://arxiv.org/html/2611.08369v1#A3.SS3.SSS5) [(ref: main App. C.2.3)](https://arxiv.org/html/2611.08369v1#A3.SS2.SSS3)

## 與書庫其他文章的關係

Lingshu 的導讀記錄這個通用醫療 VLM 的資料與訓練配方；本篇把 Lingshu-7B 與 32B 放進鼻咽癌的病理、MRI 分期與照護路徑評估，32B 的 CarePath Care 為 55.3%、Strict 為 2.0%，可補上它在次專科病程任務上的邊界: [Lingshu 靠合成資料拉高醫療 VQA，強化學習那一步沒加分](2026-09-15-lingshu-medical-vlm.md)

喉咽癌那篇把七個解剖結構做成圖節點，讓模型依結構侵犯證據做 CT T 分期；本篇的 L3 解剖面板則用 18 個結構的侵犯判讀檢查 MRI T 分期是否有證據支持，兩篇都把「分期標籤背後的結構侵犯」當成評估對象: [喉咽癌 T 分期拆成七個器官節點，外部驗證報告近半是補寫的](2026-10-14-laryngopharyngeal-ct-report-t-staging.md)

## 實務的啟發

1. **評估臨床決策模型時，同時報病人層級的全對率。** 本篇顯示逐題準確率 89.9% 可以對應到 11.0% 的病人全對；院內驗證若只看逐題平均，會看不到「同一位病人哪裡出錯」。這是可直接借用的量測方法，不代表任何模型已可用於鼻咽癌照護。[(ref: main §4.5)](https://arxiv.org/html/2611.08369v1#S4.SS5)
2. **影像分期要和多數類基線、平衡準確率一起看。** T 分期最佳模型仍低於固定答 T3 的基線；評估 VLM 讀 MRI 分期時，應先列出多數類與平衡準確率，再談模型差異。[(ref: main §4.5)](https://arxiv.org/html/2611.08369v1#S4.SS5)
3. **檢查「答案對」是否有對的證據。** 解剖面板把 T 分期拆成結構侵犯判讀，揭露分期對、證據錯的情況；本書庫認為，院內若要以 VLM 輔助分期，至少要抽查它所依據的結構判讀，而不是只比對最終分期。[(ref: main §4.3)](https://arxiv.org/html/2611.08369v1#S4.SS3)
4. **LLM judge 要附醫師校準與錯誤偵測的 sensitivity。** 本篇的主要 judge 對醫師標記成立的 criterion 只抓到約一半；用 LLM judge 為開放式臨床回答打分時，應同時報 judge 與醫師的一致率，並把 major error 率和總分分開呈現。[(ref: main §4.4)](https://arxiv.org/html/2611.08369v1#S4.SS4)
5. **挑題方式要寫清楚。** CarePath 用部分受測模型的錯誤來富集難題；借用這種設計時，應像作者一樣標出參與挑題的模型，並把它們與其他模型分開解讀。[(ref: main App. C.3.5)](https://arxiv.org/html/2611.08369v1#A3.SS3.SSS5)

## References

- `main` — Wang P, Zhang W-W, Li Y, Tang M, Hou Z, Liu Z, Zhu G, Wang Y, Gu Y, Wang W, Ni M, Xie C, Sang Z, Wu J, Sun Y, Yang H. *NPCBench: A Clinical Apprenticeship Benchmark for Multimodal Care-Pathway Reasoning in Nasopharyngeal Carcinoma*. arXiv:2611.08369v1, 2026. [https://arxiv.org/html/2611.08369v1](https://arxiv.org/html/2611.08369v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.08369v1)、[§1](https://arxiv.org/html/2611.08369v1#S1)、[§2](https://arxiv.org/html/2611.08369v1#S2)、[§3.1](https://arxiv.org/html/2611.08369v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.08369v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.08369v1#S3.SS3)、[§4.1](https://arxiv.org/html/2611.08369v1#S4.SS1)、[Table 1](https://arxiv.org/html/2611.08369v1#S4.T1)、[§4.2](https://arxiv.org/html/2611.08369v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.08369v1#S4.SS3)、[Fig. 4](https://arxiv.org/html/2611.08369v1#S4.F4)、[§4.4](https://arxiv.org/html/2611.08369v1#S4.SS4)、[Table 2](https://arxiv.org/html/2611.08369v1#S4.T2)、[§4.5](https://arxiv.org/html/2611.08369v1#S4.SS5)、[§5](https://arxiv.org/html/2611.08369v1#S5)、[App. A](https://arxiv.org/html/2611.08369v1#A1)、[App. A.1](https://arxiv.org/html/2611.08369v1#A1.SS1)、[App. A.2](https://arxiv.org/html/2611.08369v1#A1.SS2)、[App. A.3](https://arxiv.org/html/2611.08369v1#A1.SS3)、[App. C](https://arxiv.org/html/2611.08369v1#A3)、[App. C.2.3](https://arxiv.org/html/2611.08369v1#A3.SS2.SSS3)、[App. C.3.5](https://arxiv.org/html/2611.08369v1#A3.SS3.SSS5)、[Table A19](https://arxiv.org/html/2611.08369v1#A3.T19)、[App. D.1](https://arxiv.org/html/2611.08369v1#A4.SS1)、[App. E](https://arxiv.org/html/2611.08369v1#A5)
- `abstract` — arXiv abstract page, 2611.08369v1. [https://arxiv.org/abs/2611.08369v1](https://arxiv.org/abs/2611.08369v1)
- `code` — NPCBench evaluation code. [https://github.com/pidneuralode/NPCBench](https://github.com/pidneuralode/NPCBench)
- `data` — NPCBench dataset on Hugging Face. [https://huggingface.co/datasets/pengkaiScience/NPCBench](https://huggingface.co/datasets/pengkaiScience/NPCBench)
- PDF v1：[https://arxiv.org/pdf/2611.08369v1](https://arxiv.org/pdf/2611.08369v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.08369](https://doi.org/10.48550/arXiv.2611.08369)

[Home](../) · [AI Papers](./)
