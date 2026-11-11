---
parent: AI Papers
nav_order: 1
title: "MedHiVE：報告只進預訓練，有對齊的器官多 2.7、其餘只多 0.7"
catalog_id: "arxiv:2611.08185"
editors:
  - "Clare"
refs:
  main:
    title: "Multimodal Hierarchical Mixture-of-Experts for 3D Medical Vision-Language Modeling"
    url: "https://arxiv.org/abs/2611.08185v1"
  code:
    title: "szczurek-lab/MedHiVE (GitHub)"
    url: "https://github.com/szczurek-lab/MedHiVE"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# MedHiVE：報告只進預訓練，有對齊的器官多 2.7、其餘只多 0.7

## 來源

- 團隊：Helmholtz Munich、Technical University of Munich、Munich Center for Machine Learning、Jagiellonian University、Johns Hopkins University、GAMMED、Massachusetts General Hospital、Harvard Medical School、University of Warsaw 與 LMU Munich，8 位作者 Gizem Mert、Szymon Płotka、Pedro R. A. S. Bassi、Wenxuan Li、Zongwei Zhou、Jarosław B. Ćwikła、Arkadiusz Sitek、Ewa Szczurek；通訊作者為 Gizem Mert（Helmholtz Munich）。[(ref: main title block)](https://arxiv.org/html/2611.08185v1)
- 論文：*Multimodal Hierarchical Mixture-of-Experts for 3D Medical Vision-Language Modeling*，arXiv:2611.08185v1（cs.CV），2026-11-05 提交，目前只有 v1；arXiv 頁註記已被 WACV 2027 接受，授權為 arXiv 非專屬散布授權，著作權屬 IEEE。[(ref: abstract)](https://arxiv.org/abs/2611.08185v1)
- 識別碼：arXiv [2611.08185](https://arxiv.org/abs/2611.08185v1)；DOI [10.48550/arXiv.2611.08185](https://doi.org/10.48550/arXiv.2611.08185)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.08185v1)、[PDF v1](https://arxiv.org/pdf/2611.08185v1)。
- 程式：作者寫明程式碼在 [github.com/szczurek-lab/MedHiVE](https://github.com/szczurek-lab/MedHiVE)（MIT 授權；本文撰寫時 repo 首頁只列出 README、LICENSE 與 .gitignore）；論文未提到是否釋出權重。預訓練用的 Merlin 與微調用的 PANORAMA、AMOS-CT、KiTS 2023、GEPAR3D 為公開資料，PDAC 與腎臟病灶的院內資料不公開。[(ref: abstract)](https://arxiv.org/abs/2611.08185v1) [(ref: main §5.1)](https://arxiv.org/html/2611.08185v1#S5.SS1)
- 研究性質：方法論文，MedHiVE 已實作並在四個分割基準與一個院內 PDAC 資料上與 11 個方法比較；不是 pilot。所有結果都是單次數字，沒有信賴區間、標準差或多個 seed；分類與偵測只寫了「p<0.05, Wilcoxon signed-rank test」，沒有說明配對單位。[(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2)
- 證據邊界：本文數值以 arXiv v1 的正文 Table 1–2 與附錄 A–D 為準；Table 12 只引用正文 §5.3 轉述的兩個平均值，附錄 E–J（含 Table 9、Table 12 全表、臨床影響與限制段）未納入本文引述。

**編輯：** Clare

作者把 3D 腹部 CT 的放射報告拆成 14 個器官的片段，只在預訓練時用兩層 Soft Mixture-of-Experts 讓影像與文字 token 一起路由、再做整卷與器官層級的對比學習，微調與推論時只看影像；在四個分割基準與院內 PDAC 偵測上，它的七個效能欄都高於 11 個比較方法，而在 AMOS 上，報告與遮罩有涵蓋的 12 個器官比純影像基線平均多 2.7 mDSC，沒涵蓋的 3 個器官只多 0.7。[(ref: main Abstract)](https://arxiv.org/html/2611.08185v1) [(ref: main Table 1)](https://arxiv.org/html/2611.08185v1#S5.T1) [(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)

## 流程

![MedHiVE 流程示意圖，分上下兩排。上排標題為 (a) Pre-training (Merlin: 25,494 CT scans with reports)，四個方塊由左到右以實線箭頭相連：淺藍色「Inputs」（3D CT volume；Organ masks for 14 anatomies (from Merlin, Appendix A.1)；Full radiology report；Report snippets per anatomy (extracted by Qwen3-30B, reviewed by radiologists)）→ 淺藍色「Text side」（Frozen Clinical-Longformer；Report tokens；Snippet representation for each anatomy；Text tokens enter encoder stages 3-4 only）→ 淺橘色「Encoder: Mamba stages + HiVEL」（Stages 1-2: vision tokens only；Stages 3-4: vision + text tokens；Level 1: soft MoE routing of token groups to global experts, anatomy vectors to local experts；Level 2: concatenated slots routed again, fused back by residual connection）→ 淺橘色「Training objectives」（Segmentation: Dice + CE；Global InfoNCE: whole scan <-> whole report；Anatomy InfoNCE: masked organ feature <-> snippet (negatives: other anatomies in the same scan)；EMA-based loss weighting）。下排標題為 (b) Fine-tuning and inference: image only (no masks, no report)，四個方塊由左到右以實線箭頭相連：淺綠色「Input」（3D CT (or CBCT) volume；No report text；No anatomy masks）→ 淺綠色「Pre-trained encoder」（Same encoder and HiVEL weights；UNETR-style decoder with skip connections；Fine-tuned per benchmark; all compared methods share pre-training data and fine-tuning setup）→ 灰色「Segmentation (mDSC)」（PANORAMA (pancreas, PDAC)；AMOS-CT (15 organs)；KiTS 2023 (kidney, tumor, cyst)；GEPAR3D (dental CBCT, 32 tooth classes; outside pre-training anatomy)）→ 灰色「PDAC (in-house CT)」（Patient-level sensitivity, specificity；Detection mAP；Kidney lesions: qualitative comparison with reports only）](assets/medhive-pretraining-and-finetuning-pipeline.png)

圖：本書庫依論文 §4.1–§4.3、§5.1–§5.2 與 Appendix A.1、B 的文字重繪的流程示意圖，只含設計層級的設定與資料量，不含結果數值，未複製論文原圖（論文 Fig. 1 為框架概觀圖，Fig. 2 為 HiVEL 層的細部圖）。[(ref: main Fig. 1)](https://arxiv.org/html/2611.08185v1#S1.F1) [(ref: main Fig. 2)](https://arxiv.org/html/2611.08185v1#S4.F2)

## 背景／問題

作者的出發點是 3D 醫療視覺語言模型（VLM）的表徵粒度：有的模型只把整卷 CT 與整份報告做全域對齊，有的只對齊局部影像區塊，也有模型用器官先驗，但把影像與文字的階層分開處理；作者另指出，他們自己這條線的前作 MambaHoME 已在視覺端做階層式路由，卻沒有把報告的語意階層納入。[(ref: main §1)](https://arxiv.org/html/2611.08185v1#S1)

作者因此提出的缺口是「還沒有方法在同一個可微分框架中，同時對 3D 影像 token 的階層與報告的語意階層做路由」。這段論述只由文獻回顧支持，引言沒有給出量化證據說明這個缺口造成多少損失；本篇的消融實驗才是檢驗「加入報告文字是否有幫助」的地方，而那個檢驗只在 Merlin 預訓練、四個分割基準上做。[(ref: main §1)](https://arxiv.org/html/2611.08185v1#S1) [(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)

## 方法摘要

**報告只在預訓練出現。** 預訓練時，每個 CT 搭配 14 個腹部結構的器官遮罩、整份報告，以及從報告抽出的各器官片段；微調與推論時，作者明寫模型「只看影像」，沒有遮罩也沒有報告。因此 MedHiVE 在下游的用途是分割、分類與偵測，不是報告生成。[(ref: main §4.1)](https://arxiv.org/html/2611.08185v1#S4.SS1) [(ref: main §4.2.1)](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS1)

**HiVEL：兩層 Soft MoE。** 編碼器以 SegMamba 式的 Mamba 區塊為主，在後段插入作者稱為 HiVEL 的層：

- **Soft MoE** — 每個 expert 是一個前饋網路，一組可學的 slot 向量把輸入 token 加權分組，每個 slot 交給一個 expert；不做 top-k 的稀疏選擇。[(ref: main §3)](https://arxiv.org/html/2611.08185v1#S3)
- **第一層路由** — 影像 token 與報告 token 依位置切成相同的群組，各自生成 slot 後送進共用的 global experts；各器官的影像向量與片段向量則送進 local experts。[(ref: main §4.2.2)](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS2)
- **第二層路由** — 把上述四種輸出串接後再路由一次，按模態拆回去，以 residual 方式融合回影像與文字 token。[(ref: main §4.2.2)](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS2)
- **文字進哪幾段** — 前兩個 stage 只有影像 token，文字 token 只在第 3、4 stage 加入。[(ref: main §4.2.2)](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS2) [(ref: main Fig. 2)](https://arxiv.org/html/2611.08185v1#S4.F2)

**三個訓練目標。** 分割用 Dice＋cross-entropy；整卷影像的平均特徵與整份報告做對稱 InfoNCE（global）；以器官遮罩取出的影像特徵與該器官的報告片段做對稱 InfoNCE（anatomy），負例是同一個病例內的其他器官。兩個對比損失的權重依各損失大小的 EMA 自動調整並設上下限。[(ref: main §4.3)](https://arxiv.org/html/2611.08185v1#S4.SS3)

**怎麼比。** 作者稱所有方法都用同一個預訓練資料、在每個基準上以相同方式微調；比較對象包括 8 個純影像分割模型（Hermes、Swin SMT、VSmTrans、uC 3DU-Net、Swin UNETR、SuPreM、SegMamba、MambaHoME）與 3 個 3D 醫療 VLM（Merlin、fVLM、BTB3D），分割模型以相同器官遮罩預訓練，VLM 則同時用影像與文字。[(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2)

## 方法詳解

**器官片段怎麼來。** 14 個結構為脾臟、左右腎、膽囊、肝臟、胃、胰臟、左右腎上腺、小腸、十二指腸、大腸、膀胱與攝護腺（Table 3）；遮罩來自 Merlin 的半自動、人機協作標註。報告先以正規表示式的同義詞表配合 Qwen3-30B 判斷各器官是否被提及，再由 Qwen3-30B 轉成以器官為索引的 JSON：只保留「目前」的發現，比較、時間、病史、檢查方式與括號內容都刪去，未提及的器官填「Unremarkable」，雙側器官的敘述分左右處理。片段再由四位至少 5 年經驗的放射科醫師審閱、一位超過 30 年經驗的資深放射科醫師修訂。[(ref: main Appendix A.1–A.5)](https://arxiv.org/html/2611.08185v1#A1) [(ref: main Table 3)](https://arxiv.org/html/2611.08185v1#A1.T3)

**文字編碼。** 報告與片段都用凍結的 Clinical-Longformer 編碼；整份報告的 token 序列會補齊或截斷到與影像 token 等長，以便第一層路由逐位置分組。[(ref: main §4.2.1)](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS1) [(ref: main §4.3)](https://arxiv.org/html/2611.08185v1#S4.SS3)

**訓練設定。** AdamW、初始學習率 1e-4 搭配 cosine annealing、weight decay 1e-5、batch size 2、float32，以 Dynamic Tanh 取代正規化層。預訓練在 Merlin 上 100 epochs、128³ patch、1.5 mm 等向性、HU 截在 [−175, 250]，用 8 張 H100；微調 PANORAMA、AMOS、KiTS 各 500 epochs，GEPAR3D 1,000 epochs，用單張 H100 80GB。比較方法使用官方實作與預設超參數、相同 epoch 數。[(ref: main Appendix C)](https://arxiv.org/html/2611.08185v1#A3)

**指標定義。** mDSC 為各類別 Dice 的平均（逐類計算後平均）；PDAC 的 sensitivity 與 specificity 以病人為單位，一位病人的預測體積超過門檻 θ 即判為陽性；mAP 為各類 AP 的平均，偵測與真值區域的 IoU 達門檻（論文寫「typically IoU ≥ 0.5」）即算 TP。[(ref: main Appendix D)](https://arxiv.org/html/2611.08185v1#A4)

- **論文未交代** — HiVEL 的 expert 數、slot 數、群組數（正文只說沿用 MambaHoME 的消融結果），以及 InfoNCE 溫度 τ、EMA 平滑係數 β、權重上下限 α_min／α_max 的數值。[(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)
- **論文未交代** — 病人層級分類的體積門檻 θ 的數值，以及 mAP 的 IoU 門檻在本研究實際用多少。[(ref: main Appendix D)](https://arxiv.org/html/2611.08185v1#A4)
- **論文未交代** — PDAC 分類與偵測：正文稱為「independent external test set」，附錄 B.3.2 描述的院內資料為 2,577 次掃描、1,740 位病人；論文沒有說明模型在這個任務上是否另做微調、用哪些資料微調，也沒有說明 Wilcoxon 檢定以什麼為配對單位、比較了哪些方法。[(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2) [(ref: main Appendix B.3)](https://arxiv.org/html/2611.08185v1#A2.SS3)
- **論文未交代** — 隨機 seed 與重複執行；Qwen3-30B 抽取片段的 prompt 只以規則與 JSON 範例描述，沒有附全文。[(ref: main Appendix A.4)](https://arxiv.org/html/2611.08185v1#A1.SS4)

## 資料與實驗

**資料。** 下表整理自論文 §5.1 與 Appendix B、C.2；切分欄為作者實際使用的方式。[(ref: main §5.1)](https://arxiv.org/html/2611.08185v1#S5.SS1) [(ref: main Appendix B)](https://arxiv.org/html/2611.08185v1#A2)

| Dataset | 用途 | 規模 | 作者使用的切分 | 說明 |
|---|---|---|---|---|
| Merlin | 預訓練 | 25,494 次 CT、18,321 位病人，附報告 | 未說明 | Stanford Hospital；97% 為門脈期 |
| PANORAMA | 微調／分割 | 2,238 次對比增強 CT（676 PDAC、1,562 非 PDAC） | 1,571 訓練、393 驗證 | 1,964 次來自五家歐洲中心，其餘為 NIH 與 MSD 公開資料；胰臟實質與胰管合併為一類 |
| AMOS-CT | 微調／分割 | 500 次 CT，15 個器官標籤 | 200 次訓練（再 80:20 切訓練／驗證），公開驗證集 100 次當測試 | 公開標籤只涵蓋 300 次 |
| KiTS 2023 | 微調／分割 | 599 次對比增強 CT（489 公開訓練、110 隱藏測試） | 從公開訓練集隨機切 400／89 | 作者註明分數不能與官方排行榜比較 |
| GEPAR3D | 微調／分割 | 98 次 CBCT，32 個牙齒（FDI）類別 | 沿用官方切分 | 不在預訓練的器官清單內 |
| 院內 PDAC 分割集 | 外部分割測試 | 60 次對比增強 CT，來自 40 個醫療中心 | 測試 | 病理確診 PDAC，胰臟與腫瘤有逐體素標註 |
| 院內腹部 CT | PDAC 分類與偵測 | 2,577 次對比增強 CT、1,740 位病人，414 次為病理確診 PDAC | 未說明 | 來自 80 個醫療中心的縱向研究，倫理審查 University of Warmia and Mazury in Olsztyn No. 9/2023 |
| 院內腎臟病灶 | 質性比較 | 100 次腹部 CT | — | 沒有逐體素標註，只與報告比對 |

**主實驗：與 11 個方法比較。** 下表重製論文 Table 1。mDSC 為分割（%），Sens.／Spec.／mAP 為院內 PDAC 的病人層級分類與偵測（%）；VRAM 越低越好、Speed（MV/s）越高越好。所有數字為單次結果。[(ref: main Table 1)](https://arxiv.org/html/2611.08185v1#S5.T1)

| Method | Params (M) | VRAM (GB) | Speed (MV/s) | PANO | AMOS | KiTS | GEPAR3D | Sens. | Spec. | mAP |
|---|---|---|---|---|---|---|---|---|---|---|
| Hermes | 44.5 | 4.1 | 12.9 | 77.6 | 85.3 | 65.7 | 84.0 | 75.4 | 79.1 | 62.3 |
| Swin SMT | 170.8 | 3.6 | 14.7 | 73.4 | 81.6 | 47.2 | 84.1 | 77.2 | 80.5 | 64.1 |
| VSmTrans | 47.6 | 3.1 | 26.2 | 74.7 | 84.8 | 54.6 | 84.6 | 78.8 | 81.3 | 65.8 |
| uC 3DU-Net | 21.7 | 3.1 | 50.2 | 75.0 | 82.9 | 60.6 | 83.8 | 73.5 | 77.2 | 60.4 |
| Swin UNETR | 72.8 | 4.1 | 27.5 | 72.6 | 83.8 | 48.3 | 82.6 | 80.1 | 82.8 | 67.5 |
| SuPreM | 62.2 | 4.1 | 27.5 | 74.6 | 86.3 | 57.0 | 80.6 | 81.6 | 84.4 | 69.2 |
| SegMamba | 66.8 | 3.3 | 25.5 | 72.8 | 84.8 | 56.8 | 86.7 | 83.2 | 85.9 | 71.4 |
| MambaHoME | 170.1 | 3.7 | 21.0 | 74.1 | 85.5 | 60.1 | 86.1 | 84.7 | 87.1 | 73.8 |
| Merlin | 256.8 | 3.0 | 96.0 | 77.6 | 85.6 | 64.3 | 86.5 | 85.5 | 87.9 | 76.2 |
| fVLM | 110.0 | 0.6 | 360.0 | 74.6 | 85.2 | 55.4 | 84.1 | 82.3 | 85.1 | 72.4 |
| BTB3D | 101.1 | 1.4 | 60.6 | 77.8 | 86.1 | 55.1 | 84.0 | 84.9 | 87.2 | 74.4 |
| **MedHiVE** | 177.9 | 3.7 | 20.8 | 78.7 | 87.8 | 66.7 | 87.7 | 87.3 | 89.5 | 77.2 |

**消融：拿掉哪一塊。** 下表重製論文 Table 2，數值為 mDSC（%）；CL 為對比學習。每個消融都以 Merlin 預訓練、相同設定訓練。#1 的數值與 Table 1 的 MambaHoME 相同，即沒有文字的純影像版本。[(ref: main Table 2)](https://arxiv.org/html/2611.08185v1#S5.T2) [(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)

| # | Configuration | PANO | AMOS | KiTS | GEPAR3D | Avg. |
|---|---|---|---|---|---|---|
| 1 | w/o text & CL | 74.1 | 85.5 | 60.1 | 86.1 | 76.5 |
| 2 | w/o CL | 75.6 | 86.7 | 63.2 | 88.6 | 78.5 |
| 3 | w/o SMoE | 72.8 | 84.8 | 56.8 | 86.7 | 75.3 |
| 4 | w/o global CL | 71.2 | 86.1 | 50.0 | 86.2 | 73.4 |
| 5 | w/o 2nd-level routing | 58.2 | 67.1 | 38.7 | 54.1 | 54.5 |
| 6 | w/o local routing | 74.2 | 86.8 | 63.7 | 83.9 | 77.2 |
| 7 | text in all stages | 74.6 | 87.5 | 61.1 | 86.4 | 77.4 |
| 8 | text in last stage | 74.8 | 86.6 | 65.8 | 81.6 | 77.2 |
| 9 | top-k MoE | 75.5 | 87.9 | 68.3 | 84.2 | 79.0 |
| 10 | w/o EMA | 77.1 | 87.6 | 64.6 | 86.9 | 79.1 |
| 11 | MedHiVE | 78.7 | 87.8 | 66.7 | 87.7 | 80.2 |

## 結果

- **每一欄都最高** — MedHiVE 在四個分割基準的 mDSC 與 PDAC 的 sensitivity、specificity、mAP 七欄都是表中最高；各欄次佳分別為 PANORAMA 的 BTB3D 77.8、AMOS 的 SuPreM 86.3、KiTS 的 Hermes 65.7、GEPAR3D 的 SegMamba 86.7，以及 PDAC 三欄的 Merlin 85.5／87.9／76.2，差距在 0.9–1.8 個百分點之間。作者另稱分類與偵測的增益達顯著（p<0.05，Wilcoxon signed-rank test）。[(ref: main Table 1)](https://arxiv.org/html/2611.08185v1#S5.T1) [(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2)
- **文字的貢獻** — 在同一個架構上，純影像版本（#1）平均 76.5，加入報告文字但不做對比學習（#2）為 78.5，完整模型（#11）為 80.2；作者據此說文字監督本身就有幫助，多粒度對比學習再帶來增益。[(ref: main Table 2)](https://arxiv.org/html/2611.08185v1#S5.T2) [(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)
- **增益集中在有對齊的器官** — 作者以附錄 Table 12 說明：AMOS 的 15 個器官中，被 14 結構清單涵蓋的 12 個器官從純影像基線到完整模型平均多 2.7 mDSC，清單外的 3 個器官只多 0.7；牙科 CBCT 的 GEPAR3D 不在清單內，完整模型仍比基線多 1.6。[(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)
- **第二層路由拿掉就崩** — 拿掉第二層路由（#5）平均掉到 54.5，四個基準都比純影像基線低 16–32 個百分點；拿掉 global 對比學習（#4）在 KiTS 掉到 50.0。論文只把這些列為「效能下降」，沒有分析為何拿掉一個元件會比完全沒有文字還差。[(ref: main Table 2)](https://arxiv.org/html/2611.08185v1#S5.T2)
- **速度** — MedHiVE 每秒處理 20.8 MV，與 MambaHoME（21.0）相近，但約為 Merlin（96.0）的五分之一、fVLM（360.0）的十七分之一；正文沒有討論這一點。[(ref: main Table 1)](https://arxiv.org/html/2611.08185v1#S5.T1)
- **腎臟病灶的質性比較** — 在沒有逐體素標註的院內腎臟病灶資料上，作者稱 MedHiVE 的分割與報告描述一致，Merlin 與 fVLM 則會超出病灶邊界或在報告未描述的腎臟分割出病灶；這是挑選的範例，不是量化結果。[(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2)

## 限制

作者在正文結論只提到未來會延伸到縱向資料；附錄 I 另有限制與未來方向一節，本文未納入引述。[(ref: main §6)](https://arxiv.org/html/2611.08185v1#S6)

本書庫另外注意到：

- **沒有任何不確定性** — Table 1、Table 2 都是單次結果，沒有信賴區間、標準差或多 seed；許多欄位的領先幅度在 1 個百分點左右（例如 PANORAMA 78.7 對 77.8、GEPAR3D 87.7 對 86.7），無法和訓練變異區分。Wilcoxon 檢定只出現在 PDAC 分類與偵測，配對單位與比較對象都沒有寫。[(ref: main Table 1)](https://arxiv.org/html/2611.08185v1#S5.T1) [(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2)
- **KiTS 用作者自己的切分** — KiTS 2023 的分數來自從公開訓練集切出的 89 例，作者自己也註明不能與官方排行榜比較；PANORAMA 只描述訓練／驗證切分，沒有獨立測試集。[(ref: main Appendix C)](https://arxiv.org/html/2611.08185v1#A3)
- **「有對齊的器官多 2.7」只是一組平均** — 這個對比只在 AMOS 一個基準、12 對 3 個器官的平均上，器官數不對等，論文也沒有給逐器官的不確定性；它支持「報告監督的效益偏向有被對齊的器官」這個方向，但還不足以量化這個效果。[(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)
- **基線是否公平取決於重訓品質** — 11 個比較方法都由作者以官方實作、預設超參數、相同 epoch 數在 Merlin 上重新預訓練與微調，而 MedHiVE 的消融與架構選擇也在同一批基準上進行；論文沒有說明基線是否做過任何調參。[(ref: main §5.2)](https://arxiv.org/html/2611.08185v1#S5.SS2) [(ref: main Appendix C)](https://arxiv.org/html/2611.08185v1#A3)
- **只有腹部 CT 的報告** — 預訓練的器官清單與報告都來自 Merlin（單一美國醫院、以門脈期為主），片段抽取規則與放射科醫師審閱也針對這 14 個結構；換成其他部位或語言的報告，片段抽取與審閱都要重做。[(ref: main Appendix A)](https://arxiv.org/html/2611.08185v1#A1) [(ref: main Appendix B.1)](https://arxiv.org/html/2611.08185v1#A2.SS1)

## 與書庫其他文章的關係

DLoss 與 MedHiVE 出自部分重疊的作者群（Jagiellonian University、Johns Hopkins University、GAMMED、MGH），都以 Merlin 腹部 CT 與器官層級的報告片段為基礎，也都把 fVLM、BTB3D、Merlin 當比較對象，但 DLoss 用器官片段約束報告生成的訓練目標，MedHiVE 則只在預訓練用片段對齊影像、下游做分割與偵測: [DLoss：訓練時分開施壓該寫與不該寫的診斷詞，GREEN 多 4 分](2026-11-02-dloss-diagnostic-loss-ct-report-generation.md)

RADAR 把腹部 CT 拆成器官、讓報告逐器官對齊做多疾病分類，MedHiVE 同樣做器官層級的圖文對比學習，但把文字也送進編碼器內的 Soft MoE 路由，並在 AMOS 上比較有對齊與沒對齊器官的增益: [RADAR：腹部 CT 拆成 18 個器官對齊報告，146 種徵象可查](2026-09-21-radar-abdominal-ct-generalist.md)

該研究在胸片上固定資料與編碼器、比較九種不同粒度的圖文預訓練目標，MedHiVE 則在 3D CT 上同時使用整卷與器官兩種粒度的對比學習，並以消融拿掉 global 或 local 部分檢驗各自的貢獻: [胸片編碼器該學全域還是局部？九種預訓練目標、五項任務](2026-09-30-cxr-vlp-granularity-controlled-study.md)

## 實務的啟發

- **可借用的量測方法：把增益拆成「有對齊」與「沒對齊」的結構** — 若團隊用報告或標註做器官層級的預訓練，可以照 MedHiVE §5.3 的做法，把下游分數依「是否在預訓練對齊清單內」分組比較；這比只看整體平均更能看出報告監督實際幫到哪裡。但本篇只在一個基準上做了一組平均，要當成值得複製的檢查方式，而不是已量化的效果大小。[(ref: main §5.3)](https://arxiv.org/html/2611.08185v1#S5.SS3)
- **報告可以只在預訓練用** — MedHiVE 推論時不需要報告，部署形態與一般分割模型相同；對手上有大量「影像＋報告」但下游任務是分割或偵測的團隊，這是報告資料的一種用法。代價是編碼器較重，Table 1 的處理速度約為 Merlin 的五分之一。[(ref: main §4.2.1)](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS1) [(ref: main Table 1)](https://arxiv.org/html/2611.08185v1#S5.T1)
- **片段抽取需要人工審閱** — 作者的器官片段由 LLM 抽取後再經五位放射科醫師審閱修訂，論文沒有報告審閱前後的差異或所花的時間；要在自己的報告上重做，這一步的成本需要另外估計。[(ref: main Appendix A.5)](https://arxiv.org/html/2611.08185v1#A1.SS5)
- **待驗證的警訊：1 個百分點的領先** — 在沒有多 seed 與信賴區間的情況下，Table 1 多數欄位的領先幅度不足以排序方法；若要據此選模型，至少要在自己的資料上重跑 MedHiVE 與次佳方法數次，再比較差距。

## References

- **main** — Mert G, Płotka S, Bassi PRAS, Li W, Zhou Z, Ćwikła JB, Sitek A, Szczurek E. *Multimodal Hierarchical Mixture-of-Experts for 3D Medical Vision-Language Modeling*. arXiv:2611.08185v1, 2026（WACV 2027 accepted）. [abstract](https://arxiv.org/abs/2611.08185v1)；[HTML v1](https://arxiv.org/html/2611.08185v1)；[PDF v1](https://arxiv.org/pdf/2611.08185v1)；DOI [10.48550/arXiv.2611.08185](https://doi.org/10.48550/arXiv.2611.08185)
  - 深鏈：[§1](https://arxiv.org/html/2611.08185v1#S1)、[Fig. 1](https://arxiv.org/html/2611.08185v1#S1.F1)、[§3](https://arxiv.org/html/2611.08185v1#S3)、[§4.1](https://arxiv.org/html/2611.08185v1#S4.SS1)、[§4.2.1](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS1)、[§4.2.2](https://arxiv.org/html/2611.08185v1#S4.SS2.SSS2)、[Fig. 2](https://arxiv.org/html/2611.08185v1#S4.F2)、[§4.3](https://arxiv.org/html/2611.08185v1#S4.SS3)、[§5.1](https://arxiv.org/html/2611.08185v1#S5.SS1)、[§5.2](https://arxiv.org/html/2611.08185v1#S5.SS2)、[Table 1](https://arxiv.org/html/2611.08185v1#S5.T1)、[§5.3](https://arxiv.org/html/2611.08185v1#S5.SS3)、[Table 2](https://arxiv.org/html/2611.08185v1#S5.T2)、[§6](https://arxiv.org/html/2611.08185v1#S6)、[Appendix A](https://arxiv.org/html/2611.08185v1#A1)、[Appendix A.4](https://arxiv.org/html/2611.08185v1#A1.SS4)、[Appendix A.5](https://arxiv.org/html/2611.08185v1#A1.SS5)、[Table 3](https://arxiv.org/html/2611.08185v1#A1.T3)、[Appendix B](https://arxiv.org/html/2611.08185v1#A2)、[Appendix B.1](https://arxiv.org/html/2611.08185v1#A2.SS1)、[Appendix B.3](https://arxiv.org/html/2611.08185v1#A2.SS3)、[Appendix C](https://arxiv.org/html/2611.08185v1#A3)、[Appendix D](https://arxiv.org/html/2611.08185v1#A4)
- **code** — szczurek-lab/MedHiVE. [https://github.com/szczurek-lab/MedHiVE](https://github.com/szczurek-lab/MedHiVE)

[Home](../) · [AI Papers](./)
