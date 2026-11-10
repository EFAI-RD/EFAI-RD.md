---
parent: AI Papers
nav_order: 2
title: "MedChain-R1：換上別題的推理，定位 mIoU 掉 12 點"
catalog_id: "arxiv:2611.00041"
editors:
  - "Clare"
refs:
  main:
    title: "Think Before You Locate: Clinical Chain-of-Though Supervision for Sequential Medical Image Grounding"
    url: "https://arxiv.org/html/2611.00041v1"
  abs:
    title: "arXiv abstract page: 2611.00041v1"
    url: "https://arxiv.org/abs/2611.00041v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# MedChain-R1：換上別題的推理，定位 mIoU 掉 12 點

## 來源

- 團隊：Adinath Madhavrao Dukre、Govinda Kolli、Yifan Lu、Ziyun Zou、Azmine Toushik Wasi、Sara Atito、Behzad Bozorgtabar、Dwarikanath Mahapatra、Muhammad Awais、Imran Razzak，共 10 位作者；單位為 Mohamed bin Zayed University of Artificial Intelligence（MBZUAI）、Vitalverse、University of Surrey（CVSSP）、Aarhus University 與 Khalifa University；Behzad Bozorgtabar 在 HTML 版作者欄未列單位。[(ref: main author block)](https://arxiv.org/html/2611.00041v1)
- 論文：*Think Before You Locate: Clinical Chain-of-Though Supervision for Sequential Medical Image Grounding*（arXiv 頁上的篇名即寫作 Chain-of-Though），arXiv:2611.00041v1（cs.CV；cs.AI），2026-10-08 提交，目前只有 v1；授權為 CC BY 4.0。論文內文稱方法為 MedChain-R1、資料集為 MedChain。[(ref: abstract)](https://arxiv.org/abs/2611.00041v1)
- 識別碼：arXiv [2611.00041](https://arxiv.org/abs/2611.00041v1)；DOI [10.48550/arXiv.2611.00041](https://doi.org/10.48550/arXiv.2611.00041)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.00041v1)、[PDF v1](https://arxiv.org/pdf/2611.00041v1)。
- 程式與資料：論文的 Reproducibility Statement 表示訓練與評估程式、逐例預測、重疊稽核結果與 checkpoint metadata 放在補充材料；arXiv 版正文沒有提供公開的程式或資料下載連結。[(ref: main Reproducibility Statement)](https://arxiv.org/html/2611.00041v1#S6.SSx3)
- 研究性質：方法論文，資料建構、三個規模的微調與 GRPO 都已實作並在 MedSG-Bench 全部 9,630 題測試題上評估，非 pilot；只用公開基準，不涉及新收病人。[(ref: main §4)](https://arxiv.org/html/2611.00041v1#S4) [(ref: main Ethics Statement)](https://arxiv.org/html/2611.00041v1#S6.SSx2)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文與附錄表格（Table 1–3、5、7–9、14–17）為準。

**編輯：** Clare

MedChain-R1 用兩個大型多模態模型替 15 萬筆「多張醫學影像中找出目標框」的訓練題寫推理過程，再拿來微調 Qwen3.5；在同一個 4B 模型上，加推理監督比只學答案的版本 mIoU 高 3.56 點，但增益集中在差異偵測與追蹤，三個外觀比對任務反而下降，而推論時換上別題的推理會讓 mIoU 掉 12.18 點。[(ref: main §5.2)](https://arxiv.org/html/2611.00041v1#S5.SS2) [(ref: main Table 17)](https://arxiv.org/html/2611.00041v1#A3.T17)

## 流程

![左右兩欄圖。左欄標題「MedChain-R1 training pipeline」，六個圓角框由上而下以向下箭頭相連：前兩個為淺藍色，依序為「1 Training example」（image sequence + clinical query + annotated box）與「2 Stage 1: FlemingVL-38B」（caption-like pseudo-CoT of each image）；中間兩個為淺橘色，依序為「3 Stage 2: Qwen3.5-397B-A17B」（re-reads images; SEES the annotated box; writes cross-image rationale）與「4 Filter + deduplicate」（drop malformed / box-mismatch outputs -> 182,573 IDs）；最後兩個為淺綠色，依序為「5 dCoT-SFT (Qwen3.5 4B / 9B / 27B)」（150,573 SFT IDs; <think> rationale </think><answer> box </answer>）與「6 GRPO (4B / 9B)」（32,000 held-out IDs; reward = IoU + format; G = 8）。左下斜體字「Evaluation: MedSG-Bench test, 9,630 questions, 8 tasks; mIoU and Acc@0.5」，其下灰色小字「Redrawn by EFAI-RD from arXiv:2611.00041v1 Sec. 3, Algorithm 1 and Fig. 2」。右欄為長條圖，標題「Qwen3.5-4B, same 9,630 test questions (Table 17)」與「error bars: 95% paired bootstrap CI」，縱軸「dCoT-SFT minus answer-only SFT, mIoU (pp)」，九根柱各標數值：RDG +16.10、NRDG +14.67、MV -2.20、OT +6.50、VCG +1.61、VPG -2.45、CMG +2.56、RG -3.18 為八個任務，正值為藍色、負值為橘色；最右一根深灰色為 Overall +3.56。](assets/medchain-r1-pipeline-task-delta.png)

*圖：本書庫依論文 §3、Algorithm 1 與 Fig. 2 重繪的 MedChain 建構與訓練流程（左），以及 Table 17 中同一 Qwen3.5-4B 主幹「推理監督（dCoT-SFT）減去只學答案（answer-only SFT）」在八個任務與整體的 mIoU 差值與 95% 配對 bootstrap 區間（右）。左欄步驟與數量取自 [§3](https://arxiv.org/html/2611.00041v1#S3)，右欄數值取自 [Table 17](https://arxiv.org/html/2611.00041v1#A3.T17)。*

## 背景／問題

這篇處理的是 sequential medical grounding：給一串醫學影像（前後期、不同切面、不同模態或放大倍率）與一個臨床問題，模型要在正確的那一張影像上輸出目標的框。基準 MedSG-Bench 把八個任務分成兩類：image difference grounding 要找出兩張影像之間的變化；image consistency grounding 要在視角、切片、模態或尺度改變後找回同一個結構，有時還要先選出是哪一張影像。[(ref: main §3)](https://arxiv.org/html/2611.00041v1#S3)

作者的出發點是：臨床上比對前後片、跨切面追蹤是常見的讀片方式，而現有的序列定位模型多半只用框來訓練，框只說明目標在哪裡，沒有說明為什麼是這一區。[(ref: abstract)](https://arxiv.org/abs/2611.00041v1) 「明確寫出跨影像推理能改善定位」是論文要檢驗的假設，不是既定事實；作者以同主幹的對照實驗檢驗它，結果是整體有增益、但不是每個任務都受益（見下方結果）。

## 方法摘要

- **MedChain** — 以兩階段流程替 MedSG-Bench 的訓練題寫推理文字：先由醫療 VLM FlemingVL-38B 描述每張影像，再由多模態的 Qwen3.5-397B-A17B 看著原始影像、問題、任務說明與標註框，寫出含跨影像比較與自我檢查的推理。過濾與去重後共 182,573 個 ID，跨 8 個任務、10 種影像模態。[(ref: main §3.1)](https://arxiv.org/html/2611.00041v1#S3.SS1)
- **dCoT-SFT** — deliberative chain-of-thought supervised fine-tuning：以 `<think>` 推理 `</think><answer>` 框 `</answer>` 的格式，對 Qwen3.5 4B、9B、27B 做全參數微調，讓模型先寫跨影像推理再輸出座標。[(ref: main §3.2)](https://arxiv.org/html/2611.00041v1#S3.SS2)
- **GRPO 第二階段** — 在 4B 與 9B 的 dCoT-SFT 模型上，再以 IoU 加格式檢查為 reward 做 GRPO，檢驗 reward 最佳化能否在推理監督之外再加分。[(ref: main §3.2)](https://arxiv.org/html/2611.00041v1#S3.SS2)
- **評估** — MedSG-Bench 全部 9,630 題測試題，指標為 mIoU 與 Acc@0.5；另做同主幹的 answer-only 對照、推論時拿掉或替換推理的控制、訓練／測試重疊稽核，以及零樣本基線的座標慣例敏感度分析。[(ref: main §4)](https://arxiv.org/html/2611.00041v1#S4)

## 方法詳解

- **第一階段教師的選擇** — 作者比較六個候選模型（Qwen3-VL 30B、GPT-4o、Lingshu 32B、QoQ-Med-VL 32B、FlemingVL 38B、MedSeq-Grounder 7B），各在同一批 100 個樣本上用六種提示產生推理，依推理品質、與任務及影像序列的一致性、臨床合理性挑出 FlemingVL-38B。作者說它的輸出偏像影像描述，很少寫出影像之間的關係。[(ref: main Appendix A.1)](https://arxiv.org/html/2611.00041v1#A1.SS1) [(ref: main §3.1)](https://arxiv.org/html/2611.00041v1#S3.SS1)
- **第二階段推理是「看著答案寫的」** — Qwen3.5-397B-A17B 會收到標註框，被要求從可見證據說明為什麼是這一區、與鄰近候選對照、加一兩個簡短自我檢查，並且不得提到框是給定的。作者明說，因為它看得到答案，寫出的推理是對標註答案的解釋，不是任何模型實際找到答案的過程記錄。[(ref: main §3.1)](https://arxiv.org/html/2611.00041v1#S3.SS1)
- **過濾規則** — 輸出格式錯誤、超過第一階段 8K tokens 的上下文、或第二階段最後的框與標註框不一致者丟棄，失敗案例以調整後的上下文切分重跑；另有品質門檻 τ。之後去重並以 seed 42 切出 32,000 個 GRPO ID（每任務 4,000），其餘 150,573 個 ID 作為 SFT 資料（釋出為 152,396 列）。[(ref: main §3.1)](https://arxiv.org/html/2611.00041v1#S3.SS1)
- **訓練設定** — LLaMA-Factory、AdamW、cosine 學習率、學習率 5×10⁻⁶、有效 batch size 64、seed 42、8 張 GPU；4B 與 9B 訓練 2 epoch、warmup 3%、weight decay 0.05，27B 為 6 epoch、warmup 1.5%、weight decay 0；以最小驗證損失選 checkpoint（4B 第 2,000 步、9B 第 2,500 步、27B 第 4,500 步）。[(ref: main Appendix A.8)](https://arxiv.org/html/2611.00041v1#A1.SS8)
- **GRPO 設定** — 每個提示取樣 8 個回答，reward 為預測框與標註框的 IoU 加格式分；KL 係數 0.04、clipping 0.2、學習率 10⁻⁶、最多 3,000 步，在保留的開發集上選 checkpoint。[(ref: main §3.2)](https://arxiv.org/html/2611.00041v1#S3.SS2)
- **零樣本基線的提示** — 所有基線用同一個零樣本提示，只在尾端加上各模型的輸出格式說明，要求只輸出一個框、不寫推理。[(ref: main Appendix A.6)](https://arxiv.org/html/2611.00041v1#A1.SS6) Qwen3.5 零樣本分數接近零，作者另把同一批答案改用 0–1000 正規化座標重算：thinking-off 重跑時 27B 的 mIoU 由 2.64 升到 13.30，仍遠低於微調模型。[(ref: main Appendix A.7)](https://arxiv.org/html/2611.00041v1#A1.SS7)
- **推理依賴性的控制** — 在固定的 4B dCoT-SFT checkpoint 上做兩種推論時介入：forced no-think 在回答開頭直接接 `<answer>`，逼模型立刻輸出框；cross-task rationale 則把另一個任務的推理（依固定規則指派）預先填進去再接 `<answer>`。兩者都用決定性解碼與同一個答案解析器。[(ref: main Appendix C.4)](https://arxiv.org/html/2611.00041v1#A3.SS4)
- **統計方法** — 配對分析以題目 ID 對齊預測，用 100,000 次題目層級 bootstrap（推理控制為 10,000 次）與 sign-flip 檢定；作者說明這些區間只反映測試題抽樣的不確定性，不包含不同訓練回合之間的變異。[(ref: main §4)](https://arxiv.org/html/2611.00041v1#S4)
- **論文未交代** — 推理稽核只由一位醫療專家看 2,000 筆，專科與資格「Not recorded」，沒有錯誤類別細分、逐筆標記或第二位評分者。[(ref: main Appendix A.4)](https://arxiv.org/html/2611.00041v1#A1.SS4)
- **論文未交代** — 品質門檻 τ 的數值與計算方式；第一階段 Algorithm 1 有這個門檻，但正文與附錄未給出具體定義。[(ref: main §3.1)](https://arxiv.org/html/2611.00041v1#S3.SS1)
- **論文未交代** — answer-only 對照與 dCoT-SFT 在有效 batch、optimizer 實作與 checkpoint 選擇規則上不同，兩者都只訓練一次、沒有多個 seed；27B 的訓練排程也與 4B／9B 不同。[(ref: main §5.2)](https://arxiv.org/html/2611.00041v1#S5.SS2) [(ref: main Appendix E)](https://arxiv.org/html/2611.00041v1#A5)

## 資料與實驗

### 資料

| 子集 | 用途 | 規模 | 說明 |
|---|---|---|---|
| MedChain SFT | dCoT-SFT 與 answer-only SFT | 150,573 個 ID（釋出 152,396 列） | 推理由 FlemingVL-38B＋Qwen3.5-397B-A17B 產生 |
| MedChain GRPO | GRPO | 32,000 個 ID（每任務 4,000） | 與 SFT 不重疊 |
| 推理稽核樣本 | 臨床合理性檢查 | 2,000 筆 | 一位醫療專家；接受 1,965 筆（98.25%） |
| GRPO 開發集 | GRPO 對照實驗 | 1,385 題 | 作者標為探索性 |
| MedSG-Bench 測試集 | 主要評估 | 9,630 題 | RDG 1,000、NRDG 1,000、MV 1,148、OT 1,000、VCG 1,000、VPG 1,000、CMG 2,000、RG 1,482 |
| 排除重疊後的測試子集 | 洩漏敏感度分析 | 9,466 題 | 排除與 SFT 共用影像或來源序列的 164 題 |

*資料：整理自 [§3.1](https://arxiv.org/html/2611.00041v1#S3.SS1)、[Appendix A.4](https://arxiv.org/html/2611.00041v1#A1.SS4)、[Appendix A.5](https://arxiv.org/html/2611.00041v1#A1.SS5) 與 [Appendix C.5](https://arxiv.org/html/2611.00041v1#A3.SS5)。任務縮寫：RDG／NRDG 為 registered／non-registered difference grounding，MV 為 multi-view，OT 為 object tracking，VCG 為 concept，VPG 為 patch，CMG 為 cross-modal，RG 為 referring grounding。*

| 訓練／測試重疊定義 | 共用數 | 受影響測試題 |
|---|---|---|
| 編碼檔 SHA-256 | 55 | 144 |
| 解碼像素 SHA-256 | 56 | 147 |
| 完整影像序列 | 0 | 0 |
| 依任務的來源序列／病例 | 12 | 17 |
| 來源序列＋標註框 | 0 | 0 |
| 影像或序列重疊聯集（排除） | — | 164 |

*表：節錄自 [Table 7](https://arxiv.org/html/2611.00041v1#A1.T8)。*

### 實驗：MedSG-Bench 主結果（Table 1，平均欄）

| Model | Size | Avg. mIoU | Avg. Acc@0.5 |
|---|---|---|---|
| Qwen2.5-VL（零樣本） | 72B | 13.35 | 6.12 |
| Migician（零樣本） | 7B | 20.29 | 11.39 |
| Qwen3.5（零樣本） | 27B | 4.42 | 3.15 |
| MedGemma（零樣本） | 27B | 4.94 | 2.14 |
| MedSeq-Grounder | 7B | 72.55 | 79.71 |
| MedChain-R1（dCoT-SFT） | 4B | 74.96 | 82.37 |
| MedChain-R1（+GRPO） | 4B | 75.32 | 82.89 |
| MedChain-R1（dCoT-SFT） | 9B | 76.60 | 83.55 |
| MedChain-R1（+GRPO） | 9B | 76.90 | 83.82 |
| MedChain-R1（dCoT-SFT） | 27B | 77.24 | 85.20 |

*表：節錄自 [Table 1](https://arxiv.org/html/2611.00041v1#S3.T1)，單位為 %；原表另列八個任務的分數，完整基線見 [Table 10](https://arxiv.org/html/2611.00041v1#A3.T10)。MedSeq-Grounder 與 MedChain-R1 的主幹與訓練資料不同，作者把這個比較視為描述性。*

### 實驗：同主幹對照與推理控制（Table 2，mIoU）

| Qwen3.5-4B | RDG | NRDG | MV | OT | VCG | VPG | CMG | RG | Overall |
|---|---|---|---|---|---|---|---|---|---|
| Answer-only SFT | 66.76 | 66.64 | 56.21 | 58.27 | 69.03 | 92.66 | 80.83 | 72.85 | 71.39 |
| dCoT-SFT | 82.86 | 81.30 | 54.01 | 64.77 | 70.64 | 90.21 | 83.39 | 69.67 | 74.96 |
| dCoT-SFT, forced no-think | 82.15 | 80.94 | 49.72 | 55.26 | 69.40 | 87.55 | 81.44 | 66.36 | 72.02 |
| dCoT-SFT, cross-task rationale | 65.19 | 80.16 | 39.55 | 46.74 | 65.12 | 86.03 | 65.78 | 56.88 | 62.77 |

*表：取自 [Table 2](https://arxiv.org/html/2611.00041v1#S5.T2) 的 mIoU 列，單位為 %；四列都用同一組 9,630 題。原表另列 Acc@0.5。各任務差值的 95% 區間見 [Table 17](https://arxiv.org/html/2611.00041v1#A3.T17)，推理控制的配對差見 [Table 14–16](https://arxiv.org/html/2611.00041v1#A3.T15)。*

### 實驗：GRPO 在 dCoT-SFT 之後（Table 3）

| Evaluation | GRPO variant | Δ mIoU | Δ Acc@0.5 |
|---|---|---|---|
| Test, all tasks（n=9,630，4B） | IoU+format | +0.37 [0.05, 0.69] | +0.52 [−0.04, 1.08] |
| Test, concept task（4B） | IoU+format | −4.55 | −6.70 |
| Test 9B, all tasks | IoU+format | +0.30 | +0.27 |
| Dev, all tasks | direct, step 50, 3 seeds | +0.06（SD 0.08） | +0.24（SD 0.15） |
| Dev, multi-view（n=59） | direct, step 50, 3 seeds | +4.45（SD 0.63） | +7.35（SD 1.96） |

*表：節錄自 [Table 3](https://arxiv.org/html/2611.00041v1#S5.T3)，差值為相對 dCoT-SFT 起點的百分點；方括號為 95% bootstrap 區間，SD 為三個訓練 seed 的標準差。開發集結果作者標為探索性。*

## 結果

- **整體超過先前最佳，但比較對象主幹不同** — dCoT-SFT 在 4B、9B、27B 的平均 mIoU 為 74.96、76.60、77.24，都高於 MedSeq-Grounder 的 72.55；作者指出部分差距來自主幹：只學答案的 4B 模型已在 RG、VPG、CMG 上超過 MedSeq-Grounder，平均則是靠推理監督才從 71.39 拉到 74.96。[(ref: main §5.1)](https://arxiv.org/html/2611.00041v1#S5.SS1) 從 MedSeq-Grounder 的公開 checkpoint 接著做 dCoT-SFT，mIoU／Acc@0.5 由 72.55／79.71 升到 75.71／82.34，但沒有對應的 answer-only 接續訓練可比。[(ref: main Appendix C.2)](https://arxiv.org/html/2611.00041v1#A3.SS2)
- **同主幹對照：整體加 3.56 點** — 4B dCoT-SFT 比 answer-only SFT 的 mIoU 高 3.56 個百分點（95% CI 3.13–4.00）、Acc@0.5 高 2.06（1.36–2.75）；排除 164 題重疊題後為 +3.61（3.17–4.04）與 +2.01（1.31–2.70）。[(ref: main §5.2)](https://arxiv.org/html/2611.00041v1#S5.SS2) [(ref: main Appendix A.5)](https://arxiv.org/html/2611.00041v1#A1.SS5)
- **增益集中在比對類任務，外觀比對反而下降** — RDG +16.10、NRDG +14.67、OT +6.50 mIoU；MV −2.20、VPG −2.45、RG −3.18，三者區間都不含零；VCG +1.61 不顯著（p=0.063）。VPG 的 Acc@0.5 兩邊都是 99.7，作者解讀為框的貼合度變差而不是漏找目標。[(ref: main Table 17)](https://arxiv.org/html/2611.00041v1#A3.T17) [(ref: main Appendix C.5)](https://arxiv.org/html/2611.00041v1#A3.SS5) 作者也承認 multi-view 同樣需要跨影像比較卻下降，無法用「比對任務才受益」解釋，因此只把這個模式當作經驗觀察。[(ref: main §5.2)](https://arxiv.org/html/2611.00041v1#S5.SS2)
- **換上別題的推理掉 12 點** — 同一個 4B checkpoint，強制不寫推理 mIoU 由 74.96 降到 72.02（−2.93，95% CI −3.29 到 −2.58）；預填另一個任務的推理則降到 62.77（−12.18，−12.75 到 −11.60）。降幅最大的是 OT（−18.0）、RDG（−17.7）、CMG（−17.6）與 MV（−14.5），NRDG 只降 1.1。[(ref: main §5.2)](https://arxiv.org/html/2611.00041v1#S5.SS2) [(ref: main Table 16)](https://arxiv.org/html/2611.00041v1#A3.T16) 作者強調這只顯示定位對推理內容敏感，不證明推理文字忠實記錄了模型的內部計算，而且預填別題推理本身就是一種分布位移。[(ref: main Appendix C.4)](https://arxiv.org/html/2611.00041v1#A3.SS4)
- **GRPO 加分很小且依任務而異** — 4B 全測試集 mIoU +0.37（0.05–0.69，p=0.025），Acc@0.5 +0.52 不顯著；object tracking 加 3.1 mIoU，concept grounding 掉 4.55。開發集上三個 seed 的整體變化只有 +0.06（SD 0.08）；作者先前看到的 3–5 點下降，後來查出是 GRPO 匯出時存了解析度上限較低的 image processor。[(ref: main §5.3)](https://arxiv.org/html/2611.00041v1#S5.SS3)
- **取樣中有更好的答案，GRPO 沒有轉成分數** — 在四個最難任務的 128 個訓練提示上，單一樣本 IoU≥0.5 的平均比例為 67.7%，8 個樣本至少一個成功的比例為 84.4%；但 128 個中有 20 個八個樣本全錯。作者提出 reward 只看重疊、不看語意正確等可能原因，標明為待驗證的假設。[(ref: main §5.3)](https://arxiv.org/html/2611.00041v1#S5.SS3)
- **零樣本模型普遍做不到** — 沒有任何零樣本模型超過 21 mIoU；InternVL3-78B 低於其 8B 版，MedGemma 27B 為 4.94。[(ref: main §5.1)](https://arxiv.org/html/2611.00041v1#S5.SS1) [(ref: main Table 1)](https://arxiv.org/html/2611.00041v1#S3.T1)

## 限制

- **作者列出的限制** — 兩階段推理都會繼承生成模型的盲點，且最後的推理以標註框為條件，應視為事後解釋而非忠實的內部推理；單人稽核只涵蓋 2,000 筆；answer-only 與 dCoT-SFT 的訓練條件不完全相同、沒有多 seed；147 題測試題與 SFT 共用影像，影像或檢查層級的切分未建立；只在 MedSG-Bench 評估；GRPO 結論只適用於本文的 IoU＋格式 reward 與設定。作者建議後續以配對多 seed 對照、病人／檢查層級切分、多專科稽核與更豐富的 reward 驗證。[(ref: main Appendix E)](https://arxiv.org/html/2611.00041v1#A5)
- **推理監督的「品質」沒有獨立量尺** — 98.25% 的接受率來自單一、資格未記錄的評分者，且所有被標記的 35 筆框都正確（本來就因框不一致而過濾）。本書庫的解讀是：這個稽核只能說明多數推理讀起來合理，無法說明推理中的臨床描述（例如「新出現的肺結節」）在影像上是否正確，因為生成模型是在已知答案的情況下寫的。[(ref: main Appendix A.4)](https://arxiv.org/html/2611.00041v1#A1.SS4) [(ref: main Fig. 2)](https://arxiv.org/html/2611.00041v1#S1.F2)
- **與先前最佳的差距混有主幹差異** — 先前最佳 MedSeq-Grounder 用 Qwen2.5-VL-7B 與 188K 訓練樣本，MedChain-R1 用 Qwen3.5；作者自己把這個比較定位為描述性。[(ref: main §5.1)](https://arxiv.org/html/2611.00041v1#S5.SS1) [(ref: main §5.2)](https://arxiv.org/html/2611.00041v1#S5.SS2) [(ref: main Appendix C.2)](https://arxiv.org/html/2611.00041v1#A3.SS2)
- **規模趨勢不能單獨歸因於參數量** — 27B 用不同的 epoch、warmup 與 weight decay，驗證損失也較高（0.3644 對 9B 的 0.2633），從 9B 到 27B 兩個 difference grounding 任務各降約 2 點。[(ref: main §5.1)](https://arxiv.org/html/2611.00041v1#S5.SS1) [(ref: main Appendix A.8)](https://arxiv.org/html/2611.00041v1#A1.SS8)
- **程式與資料的取得** — 作者說明可重現材料放在補充材料，arXiv 版正文未提供公開下載位置；本文無法核對 MedChain 推理文字本身。

## 與書庫其他文章的關係

MedSIGHT 讓模型在單張影像上同時寫診斷與輸出像素級分割；MedChain-R1 則把定位延伸到多張影像之間的比對，並用推理文字監督框的預測，可對照「輸出端 grounding」與「推理端 grounding」兩種做法的評估方式: [MedSIGHT：一邊寫診斷，一邊把病灶分割出來](2026-09-17-medsight-grounded-medical-vlm.md)

Lingshu 是 MedChain-R1 第一階段六個候選推理教師之一（最後選用 FlemingVL-38B）；兩篇也都觀察到在監督微調之後再加強化學習，整體分數幾乎沒有增加: [Lingshu 靠合成資料拉高醫療 VQA，強化學習那一步沒加分](2026-09-15-lingshu-medical-vlm.md)

## 實務的啟發

1. **推理監督的效益要逐任務報告。** 同一個模型、同一份資料，推理監督讓差異偵測多 16 點，卻讓 referring grounding 少 3 點；院內若評估「讓模型先寫推理」的做法，只看平均值會掩蓋任務間相反的效果。[(ref: main Table 17)](https://arxiv.org/html/2611.00041v1#A3.T17)
2. **用「換掉推理」檢查模型是否真的依賴它。** 拿掉推理與換上不相干的推理是成本很低的推論時控制，可直接借用來檢查自家微調模型的推理文字是不是裝飾；但這只能說明輸出對推理內容敏感，不能當作推理忠實的證明。[(ref: main Appendix C.4)](https://arxiv.org/html/2611.00041v1#A3.SS4)
3. **看著答案寫出的推理，不等於臨床上正確的推理。** MedChain 的推理由看得到標註框的模型產生，只做過單人稽核；把這類合成推理拿去訓練或展示給臨床使用者時，本書庫認為應先以多位專科醫師逐筆檢查其中的影像描述，這是待驗證的前提，不是已確認的品質。[(ref: main §3.1)](https://arxiv.org/html/2611.00041v1#S3.SS1) [(ref: main Appendix A.4)](https://arxiv.org/html/2611.00041v1#A1.SS4)
4. **零樣本基線先排除座標與格式問題。** Qwen3.5 零樣本接近零分，有一部分來自座標慣例與無法解析的輸出；比較通用 VLM 的定位能力前，應先確認座標系、解析器與可解析比例。[(ref: main Appendix A.7)](https://arxiv.org/html/2611.00041v1#A1.SS7)
5. **評估流程本身也要做 save-and-reload 檢查。** 本篇 GRPO 一度看似退步 3–5 點，原因是匯出的 image processor 解析度不同；任何訓練後匯出的模型，都值得先確認零學習率重存能重現原預測。[(ref: main §5.3)](https://arxiv.org/html/2611.00041v1#S5.SS3)

## References

- `main` — Dukre AM, Kolli G, Lu Y, Zou Z, Wasi AT, Atito S, Bozorgtabar B, Mahapatra D, Awais M, Razzak I. *Think Before You Locate: Clinical Chain-of-Though Supervision for Sequential Medical Image Grounding*. arXiv:2611.00041v1, 2026. [https://arxiv.org/html/2611.00041v1](https://arxiv.org/html/2611.00041v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.00041v1)、[§3](https://arxiv.org/html/2611.00041v1#S3)、[§3.1](https://arxiv.org/html/2611.00041v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.00041v1#S3.SS2)、[§4](https://arxiv.org/html/2611.00041v1#S4)、[§5.1](https://arxiv.org/html/2611.00041v1#S5.SS1)、[§5.2](https://arxiv.org/html/2611.00041v1#S5.SS2)、[§5.3](https://arxiv.org/html/2611.00041v1#S5.SS3)、[Ethics Statement](https://arxiv.org/html/2611.00041v1#S6.SSx2)、[Reproducibility Statement](https://arxiv.org/html/2611.00041v1#S6.SSx3)、[Fig. 2](https://arxiv.org/html/2611.00041v1#S1.F2)、[Table 1](https://arxiv.org/html/2611.00041v1#S3.T1)、[Table 2](https://arxiv.org/html/2611.00041v1#S5.T2)、[Table 3](https://arxiv.org/html/2611.00041v1#S5.T3)、[Appendix A.1](https://arxiv.org/html/2611.00041v1#A1.SS1)、[Appendix A.4](https://arxiv.org/html/2611.00041v1#A1.SS4)、[Appendix A.5](https://arxiv.org/html/2611.00041v1#A1.SS5)、[Table 7](https://arxiv.org/html/2611.00041v1#A1.T8)、[Appendix A.6](https://arxiv.org/html/2611.00041v1#A1.SS6)、[Appendix A.7](https://arxiv.org/html/2611.00041v1#A1.SS7)、[Appendix A.8](https://arxiv.org/html/2611.00041v1#A1.SS8)、[Table 10](https://arxiv.org/html/2611.00041v1#A3.T10)、[Appendix C.2](https://arxiv.org/html/2611.00041v1#A3.SS2)、[Appendix C.4](https://arxiv.org/html/2611.00041v1#A3.SS4)、[Table 14](https://arxiv.org/html/2611.00041v1#A3.T15)、[Table 16](https://arxiv.org/html/2611.00041v1#A3.T16)、[Appendix C.5](https://arxiv.org/html/2611.00041v1#A3.SS5)、[Table 17](https://arxiv.org/html/2611.00041v1#A3.T17)、[Appendix E](https://arxiv.org/html/2611.00041v1#A5)
- `abstract` — arXiv abstract page, 2611.00041v1. [https://arxiv.org/abs/2611.00041v1](https://arxiv.org/abs/2611.00041v1)
- PDF v1：[https://arxiv.org/pdf/2611.00041v1](https://arxiv.org/pdf/2611.00041v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.00041](https://doi.org/10.48550/arXiv.2611.00041)

[Home](../) · [AI Papers](./)
