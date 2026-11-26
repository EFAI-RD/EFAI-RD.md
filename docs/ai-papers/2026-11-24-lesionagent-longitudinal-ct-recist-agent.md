---
parent: AI Papers
nav_order: 5
title: "LesionAgent：固定規則誤判惡化 33 次，加上代理判讀只剩 2 次"
catalog_id: "arxiv:2611.27876"
editors:
  - "Clare"
refs:
  main:
    title: "LesionAgent: Training-Free Agentic Tumor Tracking and Response Assessment in Longitudinal CT"
    url: "https://arxiv.org/abs/2611.27876"
  html:
    title: "LesionAgent: Training-Free Agentic Tumor Tracking and Response Assessment in Longitudinal CT (arXiv HTML v1)"
    url: "https://arxiv.org/html/2611.27876v1"
  code:
    title: "LesionAgent (GitHub; URL listed in paper)"
    url: "https://github.com/MIC-DKFZ/LesionAgent"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# LesionAgent：固定規則誤判惡化 33 次，加上代理判讀只剩 2 次

## 來源

- 團隊：德國癌症研究中心（DKFZ）Division of Medical Image Computing、Heidelberg University（Faculty of Mathematics and Computer Science、Medical Faculty）、Heidelberg University Hospital 放射腫瘤科 Pattern Analysis and Learning Group、National Center for Tumor Diseases（NCT）Heidelberg、HIDSS4Health、Microsoft Research 與 Stanford University；第一作者 Maximilian Rokuss，末位作者 Klaus Maier-Hein，共 7 位作者。[(ref: main)](https://arxiv.org/html/2611.27876v1)
- 論文：*LesionAgent: Training-Free Agentic Tumor Tracking and Response Assessment in Longitudinal CT*，arXiv 預印本，2026-11-20 提交（v1），分類 cs.CV，授權 CC BY 4.0，未註記 venue。[(ref: abstract)](https://arxiv.org/abs/2611.27876)
- 識別碼：arXiv [2611.27876](https://arxiv.org/abs/2611.27876)；DOI [10.48550/arXiv.2611.27876](https://doi.org/10.48550/arXiv.2611.27876)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.27876v1)（含附錄 A–I）。
- 程式：論文寫明 LesionAgent 與 napari 讀片應用程式公開於 [GitHub](https://github.com/MIC-DKFZ/LesionAgent)，完整 skill prompt 隨程式釋出；本文未核對程式實作。[(ref: main Abstract)](https://arxiv.org/html/2611.27876v1) [(ref: main App. I)](https://arxiv.org/html/2611.27876v1#A9)
- 研究性質：已實作、程式公開的方法論文（不是 pilot），核心代理與所有工具都實際執行；評估全部使用公開資料。四個縱向 CT 資料集各只有 11–33 位病人，主要表格每個 study 只讀一次並附 bootstrap 標準差，只有 TumorMap 重讀三次；skill 的開發與所有消融都在 HCUCH 上進行，因此 HCUCH 的結果不是保留集；沒有放射科醫師讀者研究，「與放射科醫師比較」是對公開資料的參考標註或多讀者標註。[(ref: main §4)](https://arxiv.org/html/2611.27876v1#S4) [(ref: main §5 Limitations)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px8)
- 證據邊界：本文數值以 arXiv HTML v1 的正文、Table 1–4 與附錄 Table S2–S5 為準；Fig. 3 與 Fig. S1 只引用正文或圖說寫出的數字，不從圖面讀值。

**編輯：** Clare

DKFZ 團隊讓一個 LLM 代理操作五個凍結的 3D 模型，從多次 CT 直接讀出 RECIST 1.1 療效判定：用同一批模型、改以固定規則串接時，56 次追蹤有 33 次被誤判為惡化，代理只有 2 次；同一個 LLM 放進一般的 Claude Code 環境、給同樣的模型，基準期病灶偵測 F1 只有 41%，放進作者的 harness 則是 78%。[(ref: main Abstract)](https://arxiv.org/abs/2611.27876) [(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px2) [(ref: main Table 3)](https://arxiv.org/html/2611.27876v1#S5.T4)

## 流程

![左右兩個面板的圖。左側 A 標題「One LesionAgent read (redrawn from Sec. 3, Fig. 2, Tab. 1)」，七個實線圓角框：上排由左到右為灰色「CT scans (baseline + follow-ups)」、橘色「LLM in a tool-use loop (Claude Opus 5.5 or Qwen3.8-27B) 18 typed tools, no shell / code」、藍色「Frozen 3D models VoxTell, nnInteractive, uniGradICON, LongiTrack, TotalSegmentator」；CT 框以箭頭指向 LLM 框，LLM 框與 3D 模型框之間有兩支反向箭頭，分別標「calls」與「masks」。中排由左到右為藍色「Coordinate-labelled 2D views + second-opinion checks」、綠色「Lesion registry (lesions x visits: mask or status)」、紫色「Deterministic RECIST 1.1 engine (every number and category)」；LLM 框與左側藍框之間為雙向箭頭，LLM 框向下箭頭指向綠框，綠框以箭頭指向紫框。紫框向下箭頭指向最下方白色框「Output per follow-up: response (CR / PR / SD / PD) with every lesion, mask and tool call checkable」。右側 B 標題「Same task, with and without the harness」為水平長條圖，橫軸「Baseline lesion detection F1 (%), HCUCH, automatic」，由上而下六根長條：深橘「LesionAgent (Opus 5.5)」78、淺橘「LesionAgent (Qwen3.8)」73、藍色「Fixed-rule pipeline」62、灰色「Claude Code + same 3D models」41、灰色「Claude Code (no 3D models)」31、灰色「Opus 5.5 one-shot」21；下方小字「Source: Tab. 2 and Tab. 3 (ablations) of arXiv:2611.27876v1. HCUCH = 14 patients, 17 series.」。左下角小字「Redrawn by EFAI-RD from Rokuss M, et al. arXiv:2611.27876v1 (Fig. 2, Tab. 1-3). No CT images reproduced.」](assets/lesionagent-harness-and-detection-f1.png)

*圖：本書庫依論文 [§3](https://arxiv.org/html/2611.27876v1#S3)、[Fig. 2](https://arxiv.org/html/2611.27876v1#S2.F2) 與 [Table 1](https://arxiv.org/html/2611.27876v1#S3.T1) 重繪的一次判讀流程（左，七個實線框：LLM 透過工具呼叫凍結 3D 模型、在座標標記的 2D 視圖中檢查結果、把病灶寫進 registry，再由確定性 RECIST 引擎算出每次追蹤的療效類別）；右為 HCUCH 全自動設定下六種做法的基準期病灶偵測 F1（[Table 2](https://arxiv.org/html/2611.27876v1#S4.T2) 與 [Table 3](https://arxiv.org/html/2611.27876v1#S5.T4)；橘色為 LesionAgent、藍色為同批模型的固定規則串接、灰色為沒有 harness 的 LLM 做法）。圖中不含任何 CT 影像。*

## 背景／問題

RECIST 1.1 判讀要在每次追蹤 CT 上找出所有病灶、選出最多五個 target lesion 並量測、把同一病灶跨次對上、判斷新出現的影像是否為新病灶，再套用指引規則決定療效類別。作者引用既有研究說明這個判讀在讀者間差異很大：兩位放射科醫師選到相同 target lesion 的病人只有 41%，肺結節的偵測敏感度在 51–83% 之間。[(ref: main §1)](https://arxiv.org/html/2611.27876v1#S1)

作者的出發點是：3D foundation model 已能零樣本完成其中單一步驟（文字提示偵測與分割、點擊分割、配準、縱向追蹤），但沒有一個模型做完整個判讀；端到端訓練需要目前不存在的大規模縱向標註，而現有多模態 LLM 無法一次輸入多個 3D volume，作者引用的 benchmark 也顯示操作臨床檢視器的前沿代理幾乎找不到追蹤 CT 上的新病灶。論文要回答的是：不做任務專屬訓練，只把凍結模型當工具交給 LLM 代理，能否完成整個縱向判讀，而差異來自 LLM 本身還是外圍的 harness。[(ref: main §1)](https://arxiv.org/html/2611.27876v1#S1) [(ref: main §2)](https://arxiv.org/html/2611.27876v1#S2)

## 方法摘要

- **分工** — 3D 模型負責感知病灶；LLM 只判斷工具判斷不了的事：某個發現是不是病灶、是不是同一個病灶、哪些當 target、新發現是否 unequivocal；所有數字與療效類別交給確定性的 guideline engine 計算。[(ref: main §3 The read)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px1)
- **代理與工具** — LLM 在 tool-use loop 中只能透過 18 個有型別的工具行動（感知、檢視、registry、決策、詢問臨床醫師五組），沒有 shell、檔案或程式執行權限；Claude Opus 5.5 與開放權重的 Qwen3.8-27B 使用同一份 skill 文件。[(ref: main §3 Agent)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px2) [(ref: main Table 1)](https://arxiv.org/html/2611.27876v1#S3.T1)
- **凍結模型** — VoxTell 以文字提示提出候選病灶，nnInteractive 從一次點擊分割，uniGradICON 配準各次掃描，LongiTrack 以前一次遮罩為脈絡在追蹤掃描上分割，TotalSegmentator 標出器官；四個縱向資料集都不在這些工具的訓練資料中。[(ref: main §3 Tools)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px3) [(ref: main §4)](https://arxiv.org/html/2611.27876v1#S4)
- **Lesion registry 與自我驗證** — 判讀狀態存在 LLM 之外的「病灶 × 次別」表格；每個被接受的遮罩都由 nnInteractive 給 second opinion，追蹤結果異常時強制並排檢視，新病灶必須先與基準期同位置比對才能記錄。[(ref: main §3 Lesion registry)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px4) [(ref: main §3 Self-verification)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px6)
- **評估** — 四個公開縱向 CT 資料集（HCUCH、TumorMap-Lung、PanTrack、NCI-MATCH），分「每個基準期病灶給一次點擊」的 interactive 與只給影像的 automatic 兩種設定；對照固定規則串接同批模型、專門的 tracker、Claude Code 與 one-shot LLM，另以 DeepLesion 評估單純追蹤、以 LIDC-NLST501 把代理當第五位讀者。[(ref: main §4)](https://arxiv.org/html/2611.27876v1#S4)

## 方法詳解

- **在 3D 中透過 2D 行動** — 每張視圖的座標軸都標上絕對 voxel 索引與病人方向，代理從圖上讀到的位置可以直接成為 3D 工具的點擊提示；代理自行要求所需視圖：單一病灶的切片或 montage、同一病灶各次並排（含配準落點）、新發現與基準期同位置並排，或以連續 10 mm slab 的 maximum-intensity projection 掃肺找偵測器漏掉的結節。[(ref: main §3 Acting in 3D)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px5)
- **自我驗證的門檻** — 被接受的 VoxTell 遮罩與每個追蹤遮罩，都在中心點做一次 nnInteractive 點擊；兩者長軸差超過 max(5 mm, 30%)（約為讀者間差異範圍）時，代理必須看兩個遮罩並選一個。追蹤遮罩為空、體積變化超過 3 倍或小於 0.3 倍、沒涵蓋配準點、分裂或碰到其他病灶時，要求跨次並排檢視。新病灶小於 10 mm、沒有成長或附近有基準期發現時，代理必須說明為何確定；距療效門檻 5 mm 內的次別與只因一個新病灶判為惡化的次別都要重查。[(ref: main §3 Self-verification)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px6) [(ref: main App. D)](https://arxiv.org/html/2611.27876v1#A4)
- **Target 選擇** — 代理先為每個可量測的基準期病灶打 0–1 的再現性分數（邊界不清、壞死或融合會降分），程式再列舉所有符合 RECIST 的 target 組合（≤ 5 個、每器官 ≤ 2 個），依涵蓋器官數與分數加權大小排序；代理採用第一組或說明理由改選，也可在 napari 應用中交給臨床醫師挑。[(ref: main §3 Target selection)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px7)
- **Guideline engine** — 在遮罩上量測每個病灶並套用 RECIST 1.1 的全部慣例（淋巴結用短軸、太小無法量測的 target 記 5 mm 等）；作者指出換成 iRECIST、mRECIST、RANO 或 Lugano 只需換 engine，不必改代理，但論文只實作與評估了 RECIST 1.1。[(ref: main §3 Target selection)](https://arxiv.org/html/2611.27876v1#S3.SS0.SSS0.Px7)
- **Skill** — 一份純文字策略文件，描述判讀流程、何時驗證、RECIST 規則（每條註明指引出處）與 VoxTell 提示清單；論文以 Fig. S5–S6 列出主要內容並省略預設提示、數值預設與報告格式，完整版隨程式釋出。所有 LesionAgent 數字來自同一個凍結版本的程式與 skill。[(ref: main App. I)](https://arxiv.org/html/2611.27876v1#A9)
- **對照組設計** — 固定規則 pipeline 用同一批模型：VoxTell 偵測、uniGradICON 與 LongiTrack 追蹤、候選全部接受，追蹤時距所有基準期發現 ≥ 20 mm 且 ≥ 10 mm 的 VoxTell 候選即算新病灶。Claude Code 跑同一個 Claude Opus 5.5（相同 effort），可寫任意 Python，沒有 skill；第二次執行另以 Python 函式給它同樣五個 3D 模型，但沒有視圖工具、registry、驗證或 engine。One-shot LLM 一次收到所有次別影像，輸入格式先在 HCUCH 子集上比較多種做法後取最佳。[(ref: main App. C)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px2) [(ref: main App. H)](https://arxiv.org/html/2611.27876v1#A8) [(ref: main App. G)](https://arxiv.org/html/2611.27876v1#A7)
- **指標** — F1：基準期可量測參考病灶（≥ 0.5 ml）以遮罩重疊判定是否找到；Track：連結的參考病灶在下一次仍被重疊找到的比例（從未找到算失敗）；LD：target 長軸對臨床量測或參考遮罩的中位絕對誤差；Resp.：每次追蹤整體療效的 balanced accuracy（永遠答 stable disease 得 33%）。Table 2 的 ± 為 1,000 次 bootstrap 的標準差，病人層級比較另以 4,000 次配對 bootstrap 估 95% CI。[(ref: main App. C Metrics)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px3) [(ref: main Table S2)](https://arxiv.org/html/2611.27876v1#A3.T2)
- **執行環境** — 工具跑在一張 24 GB GPU；Claude Opus 5.5 透過 Claude Agent SDK 呼叫，Qwen3.8-27B 用同一個 harness 本地執行。評估時沒有人回答 ask_clinician，代理自行決定。[(ref: main §4 Implementation)](https://arxiv.org/html/2611.27876v1#S4.SS0.SSS0.Px4)
- **論文未交代** — 兩個 LLM 的取樣設定（temperature 等）與 reasoning 強度，只寫 Claude Code 對照用「相同 effort」。
- **論文未交代** — 每次判讀的實際耗時；只報工具呼叫次數與 API 成本，Qwen3.8 的成本是以最低公開 API 價格估算的自有 GPU 成本。
- **論文未交代** — 除 LesionAgent（Opus 5.5）在 TumorMap 上重讀三次外，Qwen3.8 代理、Claude Code 與 one-shot 對照都只跑一次（作者以成本為由），這些對照的執行間變異未知。

## 資料與實驗

### 資料

| 資料集 | 內容 | 規模 | 用途 |
|---|---|---|---|
| HCUCH | 胸腹部 CT，七種癌別，放射科醫師臨床 RECIST 1.1 target 量測 | 14 位病人、17 個 series、47 次掃描；23 次追蹤有療效參考 | 端到端（skill 開發與所有消融也在此） |
| TumorMap-Lung | 轉移性非小細胞肺癌免疫治療前後胸部 CT，所有 ≥ 1 cm 肺腫瘤跨次連結 | 33 位病人、33 次追蹤 | 端到端 |
| PanTrack | 官方驗證集，病灶跨最多 10 次連結，只有胰臟腫瘤每次都標註 | 15 位病人、52 次就診 | 偵測（recall）、追蹤、量測 |
| NCI-MATCH | 臨床試驗 CT，每次最多 5 個病灶與部分新病灶 | 11 位病人、23 次掃描 | 偵測（recall）、追蹤、量測 |
| DeepLesion DLS | 官方測試病灶配對，兩次都有放射科醫師 RECIST 線 | 105 位病人、480 對（960 個有向配對） | 單純追蹤 |
| LIDC-NLST501 | NLST 篩檢 CT，每例由 20 位中的 4 位放射科醫師獨立判讀 | 436 次掃描（148 次有 ≥ 10 mm 結節） | 第五位讀者比較 |

[(ref: main §4 Data)](https://arxiv.org/html/2611.27876v1#S4.SS0.SSS0.Px1) [(ref: main App. B)](https://arxiv.org/html/2611.27876v1#A2) [(ref: main App. C)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px5)

### 實驗：全自動設定的端到端結果（Table 2，automatic 部分）

| 方法 | HCUCH F1 | HCUCH Track | HCUCH LD (mm) | HCUCH Resp. | TumorMap F1 | TumorMap Track | TumorMap LD (mm) | TumorMap Resp. | PanTrack Rec. | PanTrack Track | NCI-MATCH Rec. | NCI-MATCH Track |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Pipeline（VoxTell→LongiTrack，固定規則） | 62 | 86 | 4.5 | 40 | 52 | 54 | 8.1 | 37 | 93 | 84 | 52 | 39 |
| Qwen3.8 one-shot | 6 | 14 | 12.6 | 28 | 18 | 10 | 13.0 | 40 | 0 | 0 | 13 | 10 |
| MedGemma 1.5 one-shot | 3 | 0 | – | 18 | 0 | 0 | – | 35 | 0 | 0 | 0 | 0 |
| Opus 5.5 one-shot | 21 | 53 | 6.2 | 88 | 40 | 27 | 8.4 | 69 | 53 | 22 | 42 | 39 |
| Claude Code | 31 | 63 | 2.4 | 80 | 50 | 37 | 4.4 | 74 | 60 | 54 | 36 | 29 |
| **LesionAgent（Opus 5.5）** | 78 | 88 | 1.9 | 95 | 62 | 75 | 4.0 | 79 | 93 | 97 | 55 | 55 |
| LesionAgent（Qwen3.8） | 73 | 82 | 4.4 | 62 | 50 | 58 | 10.3 | 52 | 87 | 89 | 61 | 58 |

單位為 %，LD 為 mm，Resp. 為 balanced accuracy；原表另附 bootstrap 標準差與 PanTrack／NCI-MATCH 的 LD，此處省略。Claude Code 列為未提供 3D 模型的版本。[(ref: main Table 2)](https://arxiv.org/html/2611.27876v1#S4.T2)

### 實驗：HCUCH 消融與無 harness 對照（Table 3）

| 設定 | F1 | Track | LD (mm) | Resp. | 工具呼叫（中位數） | 每次成本（美元） |
|---|---|---|---|---|---|---|
| LesionAgent | 78 | 88 | 1.9 | 95 | 101 | 2.7 |
| − guideline engine（LLM 自行判療效） | 同上 | 同上 | 同上 | 79 | 101 | 2.7 |
| − skill | 68 | 80 | 2.6 | 95 | 60 | 1.3 |
| − self-verification | 76 | 86 | 2.5 | 91 | 42 | 0.8 |
| − all 3D models | 36 | 61 | 2.0 | 61 | 65 | 1.9 |
| with Qwen3.8 | 73 | 82 | 4.4 | 62 | 169 | 0.4（自有 GPU 估算） |
| Claude Code＋同批 3D 模型（無 harness） | 41 | 86 | 1.6 | 93 | 61 | 1.6 |
| Pipeline（固定規則） | 62 | 86 | 4.5 | 40 | – | 0 |

[(ref: main Table 3)](https://arxiv.org/html/2611.27876v1#S5.T4)

### 實驗：DeepLesion 零樣本追蹤（Table 4）

| 方法 | CPM@10 | MED (mm) | 空遮罩比例 | LD (mm) |
|---|---|---|---|---|
| DLT（在本基準訓練，論文數字） | 0.789 | 7.0 | – | – |
| TLT（在本基準訓練，論文數字） | 0.874 | 6.0 | – | – |
| LesionLocator | 0.556 | 14.5 | 37% | 4.0 |
| LongiTrack | 0.796 | 6.2 | 20% | 9.1 |
| LesionAgent（零樣本） | 0.890 | 4.4 | 0.2% | 2.0 |

CPM@10：預測中心落在參考中心 min(r, 10 mm) 內的比例；MED：平均中心誤差。原表另列 Affine、VoxelMorph、DEEDS、TransT。[(ref: main Table 4)](https://arxiv.org/html/2611.27876v1#S5.T4) [(ref: main App. C DeepLesion)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px4)

## 結果

- **全自動對照中最強，但不是每格都贏** — 對固定規則 pipeline、one-shot LLM 與 Claude Code，LesionAgent（Opus 5.5）在四個資料集的 Track 與量測誤差都較好；偵測在 PanTrack 與 pipeline 同為 93。HCUCH 上 F1 比同批模型的 pipeline 高 16 點（病人層級 95% CI 5–24），量測誤差不到一半。開放權重的 Qwen3.8 代理在 NCI-MATCH 的 recall 與 Track（61、58）反而高於 Opus 版（55、55）。[(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px1) [(ref: main Table 2)](https://arxiv.org/html/2611.27876v1#S4.T2) [(ref: main Table S2)](https://arxiv.org/html/2611.27876v1#A3.T2)
- **固定規則把模型錯誤變成假惡化** — 在 HCUCH 與 TumorMap 共 56 次追蹤中，pipeline 誤判 progression 33 次，LesionAgent 2 次；固定規則分不出「新病灶」與「基準期漏掉的病灶」，代理則在記錄新病灶前先回頭比對基準期。療效 balanced accuracy 對 pipeline 的病人層級差距為 HCUCH +54 點（95% CI 25–86）、TumorMap +42 點（22–57）。[(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px2) [(ref: main Fig. S1)](https://arxiv.org/html/2611.27876v1#A3.F1) [(ref: main Table S2)](https://arxiv.org/html/2611.27876v1#A3.T2)
- **差別主要在 harness** — 只給影像時，Opus 5.5 one-shot 只找到 HCUCH 13% 的病灶，Qwen3.8 與 MedGemma 幾乎為零；Claude Code 能寫任意程式，F1 31%，給了同樣的 3D 模型後追蹤與量測追上（Track 86、LD 1.6 mm），F1 仍只有 41%，LesionAgent 為 78%。Qwen3.8 在 harness 內從 one-shot 的 6% 升到 73%。[(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px4) [(ref: main Table 3)](https://arxiv.org/html/2611.27876v1#S5.T4)
- **每個元件都有貢獻，但大小不一** — 拿掉 3D 模型時偵測減半（F1 36）、療效降到 61；改由 LLM 自行判療效時 95 降到 79，因為它會把第一次看到的小點算成新病灶並改選 target；拿掉 skill 時 F1 68，療效仍為 95；拿掉自我驗證各指標都小幅下降（F1 76、療效 91）。[(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px5) [(ref: main Table 3)](https://arxiv.org/html/2611.27876v1#S5.T4)
- **開放權重版本的差距在療效** — HCUCH 上 Qwen3.8 代理 F1 73 對 78 無顯著差異（差 +5，95% CI −7 至 16），療效 62 對 95（差 +33，11–77）；TumorMap 上 F1 50 對 62。[(ref: main Table S2)](https://arxiv.org/html/2611.27876v1#A3.T2)
- **零樣本追蹤勝過在 DeepLesion 訓練的 tracker** — 沒有在其病灶配對上訓練，CPM@10 0.890、平均中心誤差 4.4 mm，優於最佳的已訓練 tracker TLT（0.874、6.0 mm）；同為會分割的 LongiTrack 與 LesionLocator 有 20% 與 37% 回傳空遮罩，LesionAgent 0.2%，長軸對放射科醫師的中位誤差 2.0 mm。作者指出 LesionAgent 用的就是 LongiTrack，差別來自模型失誤時代理的補救。[(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px6) [(ref: main Table 4)](https://arxiv.org/html/2611.27876v1#S5.T4)
- **量得準，但找得少** — 在 LIDC-NLST501 當第五位讀者時，對 ≥ 10 mm 結節的敏感度 67%（95% CI 60–74），四位放射科醫師為 83%（78–87）；每次掃描偽陽性 0.07 對 0.14，長軸誤差 4.2 對 4.1 mm。[(ref: main App. C LIDC)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px5)
- **HCUCH 臨床追蹤的療效一致性** — 23 次追蹤中 20 次與放射科醫師的臨床判定相同，包含全部四次療效改變；12 個 series 中 11 個的 time to progression 相符；選中放射科醫師 25 個 target 中的 17 個（68%），固定排序的 pipeline 為 64%。這組資料同時是 skill 開發與消融所用的資料。[(ref: main §5)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px7) [(ref: main App. C Target selection)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px8) [(ref: main §4)](https://arxiv.org/html/2611.27876v1#S4)
- **重讀的變異與錯誤型態** — TumorMap 三次重讀的 F1、Track、LD、療效為 61.2 ± 1.5、72.6 ± 3.5、4.3 ± 0.3 mm、77.4 ± 1.5；33 次追蹤中 26 次三次判定相同（兩兩 Cohen's κ 0.76–0.80），6 次三次都錯。56 次追蹤中的 11 次錯誤多在療效門檻附近或選了不同 target；TumorMap 的 11 次惡化漏了 5 次，其中 2 次是代理等待下一次掃描確認新病灶，而該資料集沒有下一次。[(ref: main Table S3)](https://arxiv.org/html/2611.27876v1#A3.T3) [(ref: main App. C Wrong responses)](https://arxiv.org/html/2611.27876v1#A3.SS0.SSS0.Px9)
- **代理會在關鍵處提問** — 50 次全自動判讀中共提出 19 個 ask_clinician 問題，幾乎都關於療效取決的決定；11 次錯誤中有 4 次，代理事先問的正是決定結果的那一點。評估時無人回答，臨床醫師的回答能改善多少，作者留待讀者研究。[(ref: main App. F)](https://arxiv.org/html/2611.27876v1#A6.SS0.SSS0.Px1)

## 限制

作者自述：

- LesionAgent 只會和它操作的模型一樣強；小病灶是它與放射科醫師之間的主要差距，取決於偵測器；改用開放權重 LLM 時療效判定仍落後最佳封閉模型。[(ref: main §5 Limitations)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px8)
- 有臨床判讀的公開縱向資料集仍小，HCUCH 只記錄放射科醫師的 target lesion，沒有 non-target 與新病灶的判定，因此療效參考只由 target 決定。[(ref: main §5 Limitations)](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px8) [(ref: main App. B)](https://arxiv.org/html/2611.27876v1#A2.SS0.SSS0.Px1)
- LesionAgent 是研究系統，未經臨床使用驗證；會漏掉小病灶，看起來完整的報告可能引發過度依賴，每個判定都應由放射科醫師確認。[(ref: main App. B Data use)](https://arxiv.org/html/2611.27876v1#A2.SS0.SSS0.Px2)

本書庫另外注意到：

- **療效判定的樣本很小** — 端到端療效只在 56 次追蹤（HCUCH 23、TumorMap 33）上評分，病人層級 95% CI 很寬（例如對 pipeline 的 HCUCH 差距 25–86 點）；PanTrack 與 NCI-MATCH 因標註不完整只評 recall，沒有評療效。
- **HCUCH 不是保留集** — skill 開發與全部消融都在 HCUCH 進行，one-shot 對照的輸入格式也在 HCUCH 子集上挑選；HCUCH 的 20/23 與消融數字應視為開發資料上的結果，TumorMap 上的療效為 79%。
- **Claude Code 對照的意義有界線** — 它沒有 skill，也就沒有拿到作者整理的 RECIST 判讀流程；「harness 比 LLM 重要」的比較，同時混合了工具介面、registry、驗證與領域文件四種差異，消融只在 HCUCH 上拆開其中幾項。
- **TumorMap 的療效參考是由遮罩推導** — 依 RECIST 規則從專家分割自動選 target 與計算，不是臨床醫師的判讀；與 HCUCH 的臨床參考性質不同。
- **尚未經同儕審查** — 目前為 arXiv v1 預印本。

## 與書庫其他文章的關係

VoxelSage 同樣把量測交給確定性程式、LLM 只負責調度，但評估用參考遮罩、沒有「不給工具」的對照；LesionAgent 則以固定規則串接同批模型、Claude Code 加同批模型與 one-shot LLM 三組對照，拆出工具、harness 與 LLM 各自的貢獻: [VoxelSage：肝腫瘤量測交給程式，成效數字來自二維模擬器](2026-10-06-voxelsage-liver-ct-tool-agent.md)

兩篇都讓代理自己在 CT 體積中找東西；急診 VLM 代理那篇的模型自己翻切片、很早寫下的假設多半不會修正，LesionAgent 則把判讀狀態放在 LLM 之外的 lesion registry，並強制每個新病灶與基準期並排比對後才能記錄: [VLM 代理自己翻 CT／MRI：第一個假設錯，最後只有 12% 答對](2026-11-19-vlm-agent-ct-mri-navigation-first-hypothesis.md)

放療勾畫綜述構想以 LLM 控制器呼叫 VoxTell 等 3D 文字提示分割模型、但承認尚無系統實作；LesionAgent 是同一類控制器加工具架構在腫瘤療效判讀上的實作，並以 VoxTell 作為偵測工具: [放療勾畫綜述：VLM 對 nnU-Net 勝負未定，論點改押 CTV](2026-11-12-radiotherapy-segmentation-review-atlas-to-agentic-vlm.md)

## 實務的啟發

- **評估工具代理時，至少拆三組對照** — 本研究用「同批模型的固定規則串接」「同一個 LLM 但沒有 harness」「只有 LLM」三組對照，才看得出 HCUCH 上偵測 F1 的差距主要來自 harness（41% 對 78%），而不是 LLM 或模型本身；只和 one-shot LLM 比較會高估代理架構的貢獻，也看不出固定規則在新病灶判斷上的失誤。這是可借用的實驗設計。
- **數字與類別交給程式，LLM 只做判斷** — 消融中讓 LLM 自行判療效時，HCUCH 的療效 balanced accuracy 從 95 降到 79；若自己的代理流程有明確規則可循（如分級標準），把計算與規則套用放在確定性程式中是值得先試的設計，但本研究只在 23 次追蹤上量到這個差距。
- **把「新發現 vs 漏掉的舊發現」當成專門檢查** — 固定規則的 33 次假惡化多數來自這個混淆；任何以「新出現」作為觸發條件的縱向影像流程，都值得加上與前一次同位置並排比對的步驟。
- **這仍是小型公開資料上的研究結果** — 每個縱向資料集 11–33 位病人、無讀者研究、偵測敏感度低於放射科醫師（67% 對 83%）；在院內使用前需要在自己的病人與 CT 協定上重新驗證，臨床醫師回答 ask_clinician 能補多少也尚未量測。

## References

- `main` — Rokuss M, Valanarasu JMJ, Lozano A, Hamm B, Kirchhoff Y, Isensee F, Maier-Hein K. *LesionAgent: Training-Free Agentic Tumor Tracking and Response Assessment in Longitudinal CT*. arXiv:2611.27876v1, 2026. [https://arxiv.org/abs/2611.27876](https://arxiv.org/abs/2611.27876)
  - 深鏈：[§1 Introduction](https://arxiv.org/html/2611.27876v1#S1)、[§2 Related Work](https://arxiv.org/html/2611.27876v1#S2)、[Fig. 2](https://arxiv.org/html/2611.27876v1#S2.F2)、[§3 LesionAgent](https://arxiv.org/html/2611.27876v1#S3)、[Table 1](https://arxiv.org/html/2611.27876v1#S3.T1)、[§4 Experiments](https://arxiv.org/html/2611.27876v1#S4)、[Table 2](https://arxiv.org/html/2611.27876v1#S4.T2)、[§5 Results](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px1)、[Table 3–4](https://arxiv.org/html/2611.27876v1#S5.T4)、[Limitations](https://arxiv.org/html/2611.27876v1#S5.SS0.SSS0.Px8)、[App. B Data](https://arxiv.org/html/2611.27876v1#A2)、[App. C Evaluation Protocol](https://arxiv.org/html/2611.27876v1#A3)、[Table S2](https://arxiv.org/html/2611.27876v1#A3.T2)、[Fig. S1](https://arxiv.org/html/2611.27876v1#A3.F1)、[Table S3](https://arxiv.org/html/2611.27876v1#A3.T3)、[App. D Tools](https://arxiv.org/html/2611.27876v1#A4)、[App. F Interactive Application](https://arxiv.org/html/2611.27876v1#A6)、[App. G One-Shot Baselines](https://arxiv.org/html/2611.27876v1#A7)、[App. H Claude Code Baseline](https://arxiv.org/html/2611.27876v1#A8)、[App. I The Skill](https://arxiv.org/html/2611.27876v1#A9)
- `html` — arXiv HTML v1 全文. [https://arxiv.org/html/2611.27876v1](https://arxiv.org/html/2611.27876v1)
- `code` — LesionAgent（論文所列程式碼與 napari 應用網址）. [https://github.com/MIC-DKFZ/LesionAgent](https://github.com/MIC-DKFZ/LesionAgent)

[Home](../) · [AI Papers](./)
