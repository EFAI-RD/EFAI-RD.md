---
parent: AI Papers
nav_exclude: true
title: "查表就追平最佳模型：胸片＋EHR 不平衡基準的病人洩漏"
catalog_id: "arxiv:2611.07950"
editors:
  - "Clare"
refs:
  main:
    title: "Leakage- and Label-Aware Benchmarking of Class-Imbalance Strategies for Multimodal Chest X-Ray and EHR Classification"
    url: "https://arxiv.org/html/2611.07950v1"
  abs:
    title: "arXiv abstract page: 2611.07950v1"
    url: "https://arxiv.org/abs/2611.07950v1"
  code:
    title: "Official code repository (release v1.0.0)"
    url: "https://github.com/buidangkhoa-vn/Benchmarking-of-Class-Imbalance-Strategies-for-Multimodal-Chest-X-Ray-and-EHR-Classification"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 查表就追平最佳模型：胸片＋EHR 不平衡基準的病人洩漏

## 來源

- 團隊：Dang-Khoa Bui（通訊作者）、Quang-Huy Tran、Minh-Khoi Nguyen-Bui、Duc-Tuan Ngo、Thanh-Trong Tran、Tuan-Khoi Nguyen、Hoang-Anh Ngo（資深作者），共 7 位作者；單位為 Ho Chi Minh City University of Technology（HCMUT）Faculty of Computer Science and Engineering、Vietnam National University Ho Chi Minh City，以及 AK Technologies Company Limited 的 Applied AI & Data Science Division。[(ref: main author block)](https://arxiv.org/html/2611.07950v1)
- 論文：*Leakage- and Label-Aware Benchmarking of Class-Imbalance Strategies for Multimodal Chest X-Ray and EHR Classification*，arXiv:2611.07950v1（cs.LG；另列 cs.CV），2026-11-05 提交，目前只有 v1；授權為 CC BY-SA 4.0；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2611.07950v1)
- 識別碼：arXiv [2611.07950](https://arxiv.org/abs/2611.07950v1)；DOI [10.48550/arXiv.2611.07950](https://doi.org/10.48550/arXiv.2611.07950)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.07950v1)、[PDF v1](https://arxiv.org/pdf/2611.07950v1)。
- 程式與資料：論文提供每個步驟的程式碼（release v1.0.0，含 embedding 抽取設定與影像特徵清單）[(ref: code)](https://github.com/buidangkhoa-vn/Benchmarking-of-Class-Imbalance-Strategies-for-Multimodal-Chest-X-Ray-and-EHR-Classification)；MIMIC 衍生資料不重新散布，需自行經 PhysioNet 申請。[(ref: main §VII)](https://arxiv.org/html/2611.07950v1#S7)
- 研究性質：評估方法與基準稽核（audit），不是新模型；完整研究而非 pilot。稽核對象是作者自己先在一個已發表的 MIMIC CXR–EHR 隊列上跑出的 record-split 基準，再以病人切分、重建標籤與多種基線重跑，總計 64,160 次模型擬合；區間與檢定以 5 個 fold 的值做 corrected resampled t-test，並做 Bonferroni／Holm 校正。[(ref: main §I)](https://arxiv.org/html/2611.07950v1#S1) [(ref: main §IV-D)](https://arxiv.org/html/2611.07950v1#S4.SS4) [(ref: main §IV-F)](https://arxiv.org/html/2611.07950v1#S4.SS6)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文與 Table I–VI 為準。論文致謝段寫明以 Claude（Anthropic）協助修改程式與起草文字。[(ref: main Acknowledgment)](https://arxiv.org/html/2611.07950v1#Sx1)

**編輯：** Clare

作者稽核一個胸片＋EHR 的 class-imbalance 基準，發現在 record-level 切分下，一張「照抄同一 EHR 向量在開發集的標籤」的查表就拿到 0.788 macro F2，幾乎追平最佳 EHR 模型的 0.791；改成病人切分後，所有模型都跌回「全部判陽性」的水準。[(ref: main Table III)](https://arxiv.org/html/2611.07950v1#S5.T3)

## 流程

![左右兩欄圖。左欄由上而下三個藍色實線圓角框，以兩支向下箭頭相連：「1. Initial benchmark (record split)：29,083 MIMIC-CXR radiographs / 10,479 patients；8 ICD-keyword targets; EHR-only wins every target」、「2. Leakage + label audit：L1 patient duplication, L2 EHR vector = identifier, L3 admission misalignment; labels rebuilt from MIMIC-IV」、「3. Leakage-aware re-benchmark：Splits P1-P5; labels R / A / C / CheXpert; imbalance strategies x classifiers x representations」；左下角小字「Redrawn by EFAI-RD from arXiv:2611.07950v1 Sections III-IV」。右欄為長條圖，標題「Table III: macro F2 by split」，縱軸為 macro outer-test F2（8 個目標、釋出標籤，刻度 0–0.9），橫軸三組為 P1 record、P2 patient-grouped、P3 patient-level；每組由左到右為深藍「EHR only (selected model)」、橘色「EHR lookup table (no learning)」、灰色「All-positive baseline」。數值：P1 為 0.791、0.788、0.282；P2 為 0.280、0.286、0.282；P3 為 0.320、0.313、0.310。](assets/cxr-ehr-imbalance-leakage-audit.png)

*圖：本書庫依論文 §III–IV 重繪的稽核流程（左），以及 Table III 中 EHR-only 模型、EHR 查表與全部判陽性三者在三種切分下的 macro F2（右）。數值來自 [Table III](https://arxiv.org/html/2611.07950v1#S5.T3)。*

## 背景／問題

胸片與結構化 EHR 變數合併做臨床預測，在 MIMIC-CXR 與 MIMIC-IV 公開後很容易大規模進行；許多診斷目標稀少，研究常加上 oversampling、class weighting 或 balanced ensemble 等不平衡處理，再拿「策略 × 表徵 × 分類器」的基準給出「哪種 sampler 好、哪個模態有訊號、融合有沒有幫助」的建議。[(ref: main §I)](https://arxiv.org/html/2611.07950v1#S1)

作者的出發點是：在 MIMIC 衍生隊列裡，一位病人通常貢獻多張胸片；若標籤與 EHR 變數掛在病人層級，record-level 切分就會把同一病人、同一標籤、同一 EHR 向量的副本放在訓練與測試兩側。record-wise 與 subject-wise 評估的落差，以及洩漏造成的不可重現結果，作者引用既有文獻支持 [5]–[7]；但這類洩漏對「不平衡策略基準」的影響有多大，作者認為很少被量化。[(ref: main §I)](https://arxiv.org/html/2611.07950v1#S1) [(ref: main §II)](https://arxiv.org/html/2611.07950v1#S2)

摘要寫「這類基準常以 record-level 切分評估」，這個「常見」的程度論文沒有做文獻計數，證據是本篇這一個案例；本文把它當作作者的前提，而不是已量化的事實。[(ref: abstract)](https://arxiv.org/abs/2611.07950v1)

作者先在一個已發表的隊列（沿用自一篇 transfer-learning 研究 [8]、[9]）上以 radiograph 隨機切分跑了初始基準，得到看似清楚的結論：EHR-only 在每個目標都贏（macro F2 0.737，early fusion 0.457，image-only 0.283）、Random Forest 與 Extra Trees 在每個目標都贏、不同目標由不同 oversampler 勝出。本篇要檢驗的是這些結論在洩漏與標籤都處理過後還剩多少。[(ref: main §I)](https://arxiv.org/html/2611.07950v1#S1)

## 方法摘要

- **洩漏稽核** — 從原始資料表拆出三條洩漏管道：L1 病人層級複製、L2 EHR 向量本身就是病人識別碼、L3 標籤與入院紀錄錯位。[(ref: main §III-B)](https://arxiv.org/html/2611.07950v1#S3.SS2)
- **標籤溯源** — 回到 MIMIC-IV v2.2 的 75,339 筆入院與 113 萬個 ICD 碼，找出能完全重現釋出標籤的規則，再檢查每個關鍵字實際匹配到哪些碼。[(ref: main §III-C)](https://arxiv.org/html/2611.07950v1#S3.SS3)
- **不需重訓的診斷** — EHR 查表、seen／unseen 病人拆分、全部判陽性基線與 prior-diagnosis 規則，用來判斷一個分數到底來自臨床訊號還是記住身分。[(ref: main §III-D)](https://arxiv.org/html/2611.07950v1#S3.SS4)
- **重跑基準** — record、patient-grouped、patient-level 與 calendar-time 四類切分（P1–P5），配上釋出（R）、admission-aligned（A）、rule-refined（C）與 CheXpert（CX）四種標籤，比較不平衡策略、分類器與影像表徵。[(ref: main §IV-A)](https://arxiv.org/html/2611.07950v1#S4.SS1)

## 方法詳解

**隊列與輸入。** 分析檔有 29,083 張胸片（每次入院一張）、10,479 位病人；平均每人 2.78 張、最多 68 張，6,074 位病人有多於一張。八個二元目標（pneumonia、tuberculosis、bronchitis、arthritis、fracture、lung cancer、scoliosis、lung infection）由 ICD 診斷標題推得。EHR 為 7 個連續變數（年齡、血氧、心率、體溫、血紅素、紅血球與白血球計數）與 4 個二元變數（糖尿病、HIV、吸菸、咳嗽），其中血氧、心率、體溫缺值分別為 93.8%、75.9%、76.1%。[(ref: main §III-A)](https://arxiv.org/html/2611.07950v1#S3.SS1)

**影像輸入其實只有 11 個分數。** 作者用 TorchXRayVision 的 CheXpert DenseNet-121 重新抽取，證實分析檔的影像欄位是 18 個病灶頭的 pre-sigmoid 輸出，其中 7 欄恆為零，所以影像輸入是 11 個 pathology score，不是學到的潛在表徵；視角混雜（AP 51.0%、PA 18.8%、lateral 28.3%）。[(ref: main §III-A)](https://arxiv.org/html/2611.07950v1#S3.SS1)

**三條洩漏管道。**

- **L1 病人層級複製** — 6,074 位多張胸片的病人，八個標籤與 11 個 EHR 變數在該病人所有胸片上完全相同，即使相隔數年。[(ref: main §III-B)](https://arxiv.org/html/2611.07950v1#S3.SS2)
- **L2 EHR 向量是識別碼** — 29,083 張胸片只有 9,821 個不同的 EHR 向量，每位病人恰好一個，只有 152 個向量跨病人共用；能記住精確特徵組合的模型（深樹、最近鄰）可以藉此認出病人並照抄標籤。[(ref: main §III-B)](https://arxiv.org/html/2611.07950v1#S3.SS2)
- **L3 入院錯位** — 標籤來自每位病人的單一次入院，套到該病人所有胸片；只有 36.0% 的胸片帶著自己那次入院的標籤，31.9% 繼承較早、32.0% 繼承較晚的入院。前一研究程式中的檢驗與生命徵象取自未排序、無時間窗的查詢，可能晚於拍片時間。[(ref: main §III-B)](https://arxiv.org/html/2611.07950v1#S3.SS2) [(ref: main §III-C)](https://arxiv.org/html/2611.07950v1#S3.SS3)

**標籤怎麼來的。** 一條規則在 10,479 位病人中重現 10,477 位的全部八個標籤：某次入院的任一 ICD long title 含目標關鍵字（不分大小寫）即為陽性，而那次入院是分析檔中該病人的最後一筆紀錄（不按日期）。lung cancer 匹配任何部位的「malignant neoplasm」，lung infection 匹配任何以「infection」結尾的標題。關鍵字也會匹配到個人／家族史、篩檢、疫苗與否定式的碼：tuberculosis 陽性病人只有 11.1% 有真正的結核診斷，lung cancer 陽性只有 14.4% 是原發肺或支氣管惡性腫瘤，lung infection 只有 5.4% 是肺或呼吸道感染。[(ref: main §III-C)](https://arxiv.org/html/2611.07950v1#S3.SS3)

**切分與標籤組合。** 除 P5 外都用 5-fold 交叉驗證（iterative multilabel stratification）加內層驗證集。P1 依 radiograph 分 fold（同初始基準）；P2 保留 radiograph 層級但依病人分 fold；P3 每位病人一列，影像特徵取正面胸片平均；P5 依估計的實際年份做單一 calendar-time 切分，以 1,000 次病人層級 bootstrap 給 95% CI。A 標籤是把重建規則套到每張胸片自己的入院；C 標籤再剔除病史、篩檢、疫苗、tuberculin reaction、「Encounter for…」與否定式標題，並把 lung cancer 限縮為原發肺／支氣管、lung infection 限縮為肺或呼吸道感染。[(ref: main §IV-A)](https://arxiv.org/html/2611.07950v1#S4.SS1) [(ref: main §IV-E)](https://arxiv.org/html/2611.07950v1#S4.SS5)

**策略、分類器與選模。** 不平衡策略為 no augmentation、class weighting、random oversampling（ROS）、naive SMOTE、type-aware SMOTE-NC（把二元與缺值指示欄宣告為類別），以及 Balanced Random Forest 與 EasyEnsemble。分類器為 logistic regression（L2、C=1）、Random Forest、Extra Trees（各 300 棵、不限深度）、LightGBM 與 XGBoost，版本與 seed 全部列出。每個 outer fold 內，前處理與模型只在內層訓練集擬合，以內層驗證 F2 選門檻（0.01–0.99）與（策略、分類器）組合，再在 outer test fold 評一次。[(ref: main §IV-B)](https://arxiv.org/html/2611.07950v1#S4.SS2) [(ref: main §IV-D)](https://arxiv.org/html/2611.07950v1#S4.SS4)

**指標與統計。** 主要指標是 outer-test F2（recall 權重為 precision 的四倍，作者明說這是比較指標、不是臨床效用證據），並列 PR-AUC、AUROC 與 Brier score。macro 指「先在每個 fold 內對 8 個目標取平均，再對 5 個 fold 平均」；all-positive 的 F2 為 5p/(4p+1)。因為各 fold 的訓練集重疊，作者不把目標、分類器、fold 當獨立樣本，而是每個 fold 取一個 macro 值、用 corrected resampled t-test（變異數因子以 1/n + n_test/n_train 取代 1/n）。[(ref: main §IV-D)](https://arxiv.org/html/2611.07950v1#S4.SS4)

**更強的影像表徵與時間對齊的病史。** 另加兩種影像 embedding：同一 CheXpert DenseNet 的 1024 維 pooled 特徵，以及 RAD-DINO（ViT-B/14、DINOv2 自監督）的 768 維 CLS，各降到 64 個主成分；RAD-DINO 公開的訓練清單包含本隊列 96.6% 的胸片，所以作者把沒看過 MIMIC-CXR 的 CheXpert DenseNet 當對照。時間對齊的病史向量為拍片當次入院的年齡，加上 8 個「該目標是否在更早且已結束的入院中被編碼」旗標。[(ref: main §IV-C)](https://arxiv.org/html/2611.07950v1#S4.SS3) [(ref: main §IV-F)](https://arxiv.org/html/2611.07950v1#S4.SS6)

- **論文未交代** — 檢驗值與生命徵象沒有依入院重新抽取，也沒有限制在拍片之前，所以「EHR 沒有訊號」只適用於釋出的這組變數，時間對齊後的檢驗值是否有用未被測試。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **論文未交代** — rule-refined 標籤是作者自訂的規則，沒有經過臨床人員審查。[(ref: main §IV-E)](https://arxiv.org/html/2611.07950v1#S4.SS5)
- **論文未交代** — 原始分析檔中 EHR 值如何合併到每位病人的那一步不在公開程式裡，作者只能從年齡 99.99% 吻合推測它來自同一次入院。[(ref: main §III-C)](https://arxiv.org/html/2611.07950v1#S3.SS3)

## 資料與實驗

### 資料

| 項目 | 內容 | ref |
|---|---|---|
| 來源 | MIMIC-IV／MIMIC-CXR（MIMIC-CXR-JPG），PhysioNet credentialed 存取 | [(ref: main §III-A)](https://arxiv.org/html/2611.07950v1#S3.SS1) |
| 規模 | 29,083 張胸片、10,479 位病人；平均每人 2.78 張，最多 68 張 | [(ref: main §III-A)](https://arxiv.org/html/2611.07950v1#S3.SS1) |
| 目標 | 8 個 ICD 關鍵字標籤；scoliosis 只有 45 位陽性病人 | [(ref: main Table I)](https://arxiv.org/html/2611.07950v1#S3.T1) |
| EHR | 7 個連續＋4 個二元變數，每位病人一組 | [(ref: main §III-A)](https://arxiv.org/html/2611.07950v1#S3.SS1) |
| 影像 | 11 個 CheXpert DenseNet pathology score；另加 DenseNet pooled 與 RAD-DINO embedding（各 64 PC） | [(ref: main §IV-C)](https://arxiv.org/html/2611.07950v1#S4.SS3) |
| 第二標籤源 | MIMIC-CXR-JPG 的 CheXpert 報告標籤，8 個觀察項，U-zeros | [(ref: main §IV-F)](https://arxiv.org/html/2611.07950v1#S4.SS6) |
| 擬合數 | 主網格 680 個任務、15,680 次擬合；全部合計 64,160 次 | [(ref: main §IV-D)](https://arxiv.org/html/2611.07950v1#S4.SS4) [(ref: main §IV-F)](https://arxiv.org/html/2611.07950v1#S4.SS6) |

釋出標籤（R）的稽核，節錄自 Table I（own-neg.：釋出陽性中在該胸片自己入院為陰性的比例；cons.：來源入院有符合 rule-refined 定義之碼的陽性病人比例）：

| Target | 陽性胸片 | 陽性病人 | Prev. % | own-neg. % | cons. % | C: prev. %（病人） |
|---|---|---|---|---|---|---|
| Pneumonia | 7,980 | 4,318 | 27.44 | 33.4 | 89.5 | 28.03 (6,434) |
| Lung cancer | 7,787 | 2,822 | 26.78 | 13.1 | 14.4 | 3.54 (518) |
| Fracture | 2,078 | 918 | 7.15 | 40.2 | 75.6 | 5.12 (1,222) |
| Bronchitis | 1,485 | 678 | 5.11 | 40.5 | 100.0 | 5.74 (1,231) |
| Arthritis | 1,191 | 428 | 4.10 | 33.2 | 99.5 | 4.07 (691) |
| Lung infection | 952 | 336 | 3.27 | 56.4 | 5.4 | 0.39 (96) |
| Tuberculosis | 771 | 315 | 2.65 | 43.1 | 11.1 | 0.29 (64) |
| Scoliosis | 150 | 45 | 0.52 | 48.0 | 100.0 | 0.45 (86) |

[(ref: main Table I)](https://arxiv.org/html/2611.07950v1#S3.T1)

### 實驗

**切分的影響（釋出標籤）**，節錄自 Table III：outer-test 指標先對 8 個目標取 macro，再對 5 個 fold 平均（mean±SD）；Δ 為 F2 減 all-positive F2，CI 來自 corrected resampled t-test，* 為 Bonferroni 校正後顯著。

| 切分 | Representation | F2 | Δ [95% CI] | AUROC |
|---|---|---|---|---|
| P1 record | EHR only | 0.791±0.012 | +0.509* [+0.484, +0.533] | 0.960±0.005 |
| P1 record | Image: 11 scores | 0.283±0.003 | +0.001 [−0.004, +0.007] | 0.569±0.007 |
| P1 record | EHR lookup（hit 78.4%） | 0.788±0.008 | +0.506 | — |
| P1 record | All-positive | 0.282 | — | 0.500 |
| P2 patient-grouped | EHR only | 0.280±0.008 | −0.002 [−0.013, +0.009] | 0.592±0.017 |
| P2 patient-grouped | Image: RAD-DINO | 0.296±0.010 | +0.014 [−0.003, +0.031] | 0.614±0.020 |
| P2 patient-grouped | EHR lookup（hit 7.2%） | 0.286±0.004 | +0.004 | — |
| P3 patient-level | EHR only | 0.320±0.005 | +0.010 [+0.000, +0.020] | 0.607±0.011 |
| P3 patient-level | Fusion: RAD-DINO | 0.348±0.016 | +0.038 [+0.007, +0.070] | 0.661±0.018 |
| P3 patient-level | All-positive | 0.310 | — | 0.500 |

[(ref: main Table III)](https://arxiv.org/html/2611.07950v1#S5.T3)

**重建標籤後（admission-aligned A、rule-refined C）**，節錄自 Table IV，格式同上；‡ 為沒看過 MIMIC-CXR 的 CheXpert DenseNet 對照，在 Table V 另做 Holm 校正。

| 切分／標籤 | Representation | F2 | Δ [95% CI] | AUROC |
|---|---|---|---|---|
| P1-A record | EHR only | 0.421±0.013 | +0.131* [+0.112, +0.149] | 0.719±0.012 |
| P4 patient, A | EHR only | 0.294±0.007 | +0.004 [−0.008, +0.015] | 0.579±0.008 |
| P4 patient, A | Image: RAD-DINO | 0.316±0.004 | +0.025* [+0.015, +0.036] | 0.637±0.011 |
| P4 patient, A | History (P4-H) | 0.439±0.014 | +0.149* [+0.124, +0.173] | 0.741±0.003 |
| P4 patient, A | Fusion: RAD-DINO + history | 0.444±0.010 | +0.154* [+0.134, +0.173] | 0.766±0.003 |
| P4 patient, A | All-positive / prior diagnosis | 0.291 / 0.385 | — | — |
| P4-C patient, C | EHR only | 0.193±0.009 | +0.007 [−0.010, +0.024] | 0.578±0.012 |
| P4-C patient, C | Image: DenseNet‡ | 0.209±0.005 | +0.022 [+0.012, +0.032] | 0.607±0.017 |
| P4-C patient, C | Image: RAD-DINO | 0.240±0.011 | +0.054* [+0.031, +0.077] | 0.677±0.016 |
| P4-C patient, C | History (P4-C-H) | 0.371±0.018 | +0.184* [+0.148, +0.220] | 0.713±0.015 |
| P4-C patient, C | Fusion: RAD-DINO + history | 0.384±0.021 | +0.197* [+0.157, +0.238] | 0.762±0.015 |
| P4-C patient, C | All-positive / prior diagnosis | 0.186 / 0.337 | — | — |

[(ref: main Table IV)](https://arxiv.org/html/2611.07950v1#S5.T4)

## 結果

- **record split 的成績幾乎全是記住身分** — P1 的 EHR-only 0.791 與不需學習的 EHR 查表 0.788 幾乎相同，查表在 78.4% 的測試胸片找得到完全相同的 EHR 向量；在 P1 內部，seen 病人 F2 0.942±0.003、unseen 病人 0.227±0.014（重選門檻後 0.336，等於 all-positive 的 0.335）。[(ref: main §V-A)](https://arxiv.org/html/2611.07950v1#S5.SS1)
- **病人切分後沒有表徵明顯勝過全部判陽性** — P2 與 P3 下，任何表徵超過 all-positive 的 macro F2 不到 0.038，最佳 AUROC 0.661；稀有目標崩得最兇，例如 scoliosis 的 EHR-only 從 P1 的 0.860 掉到 P3 的 0.000。[(ref: main §V-A)](https://arxiv.org/html/2611.07950v1#S5.SS1)
- **分類器排名隨切分反轉** — EHR 輸入、no augmentation 時，P1 由 Extra Trees（0.793）、Random Forest（0.788）領先，logistic regression 只有 0.313；P2、P3 改由 logistic regression 最好（0.297、0.326），樹模型最差。限制樹深為 3 就讓 P1 的樹優勢消失，但洩漏的驗證集在 80 次選擇中有 75 次仍選不限深度。[(ref: main §V-A)](https://arxiv.org/html/2611.07950v1#S5.SS1) [(ref: main Table VI)](https://arxiv.org/html/2611.07950v1#S5.T6)
- **不平衡策略沒有可靠的贏家** — P2、P3 下相對 no augmentation 的配對平均變化落在 −0.002 到 +0.006，58 個策略檢定經 Holm 校正後只有兩個顯著、都是 P1 下的退步；SMOTE-NC 從未贏過 naive SMOTE。重新平衡讓 Brier score 在 P2、P3 增加 0.02–0.08。[(ref: main §V-B)](https://arxiv.org/html/2611.07950v1#S5.SS2)
- **重建標籤後，訊號來自影像與病史，不是釋出的 EHR** — P4 下釋出 EHR 與 11 個 score 停在 all-positive 水準，RAD-DINO 影像與融合分別高出 0.025、0.027；P4-C 下 RAD-DINO 比 EHR 高 0.047 F2、0.099 AUROC。只用「先前入院是否編碼過該目標」的規則就有 0.385（P4）與 0.337（P4-C），高於所有用釋出特徵訓練的模型；用時間對齊病史訓練的模型達 0.439 與 0.371。[(ref: main §V-D)](https://arxiv.org/html/2611.07950v1#S5.SS4)
- **影像加到病史上的增益未確立** — RAD-DINO＋病史的 AUROC 比只用病史高 0.025 與 0.049（未校正 p ≤ 0.010），F2 只多 0.005 與 0.013 且不顯著；換成沒看過 MIMIC-CXR 的 DenseNet，F2 與 AUROC 都沒有顯著增益。作者因此不主張影像對時間對齊病史有加成，RAD-DINO 的 AUROC 增益是編碼器較強還是預訓練重疊所致無法分辨。[(ref: main §V-D)](https://arxiv.org/html/2611.07950v1#S5.SS4) [(ref: main Table V)](https://arxiv.org/html/2611.07950v1#S5.T5)
- **換成每張胸片自己的 CheXpert 標籤，record split 幾乎不灌水** — EHR-only 在 record 與 patient split 只差 0.021（0.394 對 0.373），查表降到 0.297、低於 all-positive 的 0.370；作者解讀為洩漏主要在「標籤跨同一病人紀錄複製」時放大成績，但也說明兩種標籤的定義與盛行率不同，這個比較無法單獨歸因。[(ref: main §V-E)](https://arxiv.org/html/2611.07950v1#S5.SS5)
- **操作點不足以支持篩檢用途** — P4-C 下 RAD-DINO 融合的 macro recall 0.41、precision 0.11、specificity 0.78，作者明寫 precision 太低、無法建立篩檢用途。[(ref: main Table VI)](https://arxiv.org/html/2611.07950v1#S5.T6)

## 限制

作者列出的限制：

- **單一隊列** — 只用一個醫療體系的一個隊列。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **檢驗與生命徵象未重新對齊** — 只有年齡與病史做了時間對齊，檢驗與生命徵象維持釋出值，可能晚於拍片。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **RAD-DINO 預訓練重疊** — RAD-DINO 預訓練看過 96.6% 的胸片（無標籤），病人切分無法移除這個重疊，其結果可能偏樂觀；DenseNet 對照在架構、目標與訓練資料上都不同，沒有對得上的「未見過這批病人」編碼器可比。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **凍結編碼器** — 影像編碼器都凍結使用，可能低估微調後的影像表現。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **標籤品質** — CheXpert 報告標籤是自動抽取、有雜訊，只用 U-zeros；rule-refined 定義是作者自訂。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **變異來源只做了一部分** — calendar-time 切分依 3 年 anchor-year 群組且只切一次；model seed 只對 P4-C、P4-C-H 的病史單獨模型與 P5-A 變動，病史融合只有一個 seed；fold assignment 只對 logistic regression 變動。門檻來自固定網格，校準只報 Brier。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
- **檢定力低** — 只有 5 個 fold 的值，不顯著不代表等價；稀有目標每個測試 fold 的陽性病人只有 7–23 位（釋出標籤的 scoliosis 只有 9 位），單一目標的 F2 高度不確定。[(ref: main §IV-D)](https://arxiv.org/html/2611.07950v1#S4.SS4) [(ref: main §V-F)](https://arxiv.org/html/2611.07950v1#S5.SS6)

本書庫補充的閱讀限制：

- **稽核對象是作者自己的初始跑分** — 被推翻的三個結論來自作者在已發表隊列上自己跑的 record-split 基準，論文沒有逐一檢查其他已發表的 CXR＋EHR 不平衡研究是否犯同樣錯誤；「這類基準常用 record split」的普遍程度因此未被量化。[(ref: main §I)](https://arxiv.org/html/2611.07950v1#S1)
- **任務定義不是影像判讀** — A／C 標籤是預測「該次入院被編碼的診斷」，作者明說這些診斷不一定能在胸片上看到，也不一定在拍片當下存在；scoliosis、arthritis 這類目標的分數不能讀成胸片判讀能力。[(ref: main §IV-E)](https://arxiv.org/html/2611.07950v1#S4.SS5)

## 與書庫其他文章的關係

胸片結核 VLM 的稽核改換提示詞與負類，檢驗醫療 VLM 的結論換條件後還剩多少；本篇則改換資料切分與標籤定義，檢驗胸片＋EHR 不平衡基準的結論，兩篇都得到「排名與勝負會被評估條件改寫」: [換一個評估條件，胸片結核 VLM 的結論還剩幾條站得住](2026-09-21-cxr-tb-vlm-portability-audit.md)

AgentRx 的導讀在 ICU 多模態預測（含 CXR 與 EHR）上把病人層級切分與 leakage 稽核列入重現清單，本篇則實際量出不做這一步時分數會被灌到什麼程度: [AgentRx：ICU 預測多加模態有用，多代理協作沒穩定勝出](2026-09-17-agentrx-multimodal-clinical-prediction.md)
本篇揭露 EHR 向量即病人識別碼造成的洩漏，文字引導分割的稽核則揭露 caption 尺寸詞由評分遮罩計算的洩漏，兩篇都先用不需學習的對照（查表、只看 caption 的迴歸）量出洩漏程度: [文字引導分割的增益：只留病灶範圍詞就拿回 84–98%](2026-11-12-extent-leakage-text-guided-segmentation.md)

## 實務的啟發

1. **院內做多模態預測基準時，先跑兩個不需學習的基線。** 本篇的查表與全部判陽性兩條基線，一條揭露「模型在認病人」，一條揭露「模型沒學到東西」，成本幾乎為零；作者的 checklist 也把它們列為必備。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
2. **切分層級要對齊標籤的定義層級。** 標籤若掛在病人或某次入院，就依病人切分、在標籤所屬的層級評估；有 record split 時一併報 seen／unseen 病人的分數。這是作者 checklist 的第 1 與第 4 項，本篇的數字顯示不做會差多少。[(ref: main §VI)](https://arxiv.org/html/2611.07950v1#S6)
3. **ICD 關鍵字標籤要回到原始碼逐項核對。** 「tuberculosis」只有 11.1%、「lung infection」只有 5.4% 是名實相符的診斷；院內若用碼表推標籤，至少要抽查匹配到的碼標題、確認來自哪一次入院。[(ref: main §III-C)](https://arxiv.org/html/2611.07950v1#S3.SS3)
4. **會復發的診斷，先放一條 prior-diagnosis 基線。** 在本篇的任務上，「之前是否被編碼過」就勝過所有用釋出特徵的模型；評估影像模型的增益時，應拿它和這條基線、以及時間對齊的病史比較，而不是和未對齊的 EHR 比較。[(ref: main §V-D)](https://arxiv.org/html/2611.07950v1#S5.SS4)
5. **公開預訓練編碼器要查訓練清單。** RAD-DINO 看過本隊列 96.6% 的胸片，病人切分擋不住這種重疊；本書庫認為，用公開編碼器在公開資料集上報成績時，應同時列出一個未接觸該資料集的對照編碼器。[(ref: main §IV-C)](https://arxiv.org/html/2611.07950v1#S4.SS3)

本篇的正面發現（影像與病史有訊號）仍屬單一隊列、操作點 precision 偏低的結果，作者自己也不主張篩檢價值；可直接借用的是稽核方法與 checklist，而不是任何策略或模態的排名。[(ref: main §VII)](https://arxiv.org/html/2611.07950v1#S7)

## References

- `main` — Bui D-K, Tran Q-H, Nguyen-Bui M-K, Ngo D-T, Tran T-T, Nguyen T-K, Ngo H-A. *Leakage- and Label-Aware Benchmarking of Class-Imbalance Strategies for Multimodal Chest X-Ray and EHR Classification*. arXiv:2611.07950v1, 2026. [https://arxiv.org/html/2611.07950v1](https://arxiv.org/html/2611.07950v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.07950v1)、[§I](https://arxiv.org/html/2611.07950v1#S1)、[§II](https://arxiv.org/html/2611.07950v1#S2)、[§III-A](https://arxiv.org/html/2611.07950v1#S3.SS1)、[Table I](https://arxiv.org/html/2611.07950v1#S3.T1)、[§III-B](https://arxiv.org/html/2611.07950v1#S3.SS2)、[§III-C](https://arxiv.org/html/2611.07950v1#S3.SS3)、[§III-D](https://arxiv.org/html/2611.07950v1#S3.SS4)、[§IV-A](https://arxiv.org/html/2611.07950v1#S4.SS1)、[§IV-B](https://arxiv.org/html/2611.07950v1#S4.SS2)、[§IV-C](https://arxiv.org/html/2611.07950v1#S4.SS3)、[§IV-D](https://arxiv.org/html/2611.07950v1#S4.SS4)、[§IV-E](https://arxiv.org/html/2611.07950v1#S4.SS5)、[§IV-F](https://arxiv.org/html/2611.07950v1#S4.SS6)、[§V-A](https://arxiv.org/html/2611.07950v1#S5.SS1)、[Table III](https://arxiv.org/html/2611.07950v1#S5.T3)、[§V-B](https://arxiv.org/html/2611.07950v1#S5.SS2)、[§V-D](https://arxiv.org/html/2611.07950v1#S5.SS4)、[Table IV](https://arxiv.org/html/2611.07950v1#S5.T4)、[Table V](https://arxiv.org/html/2611.07950v1#S5.T5)、[§V-E](https://arxiv.org/html/2611.07950v1#S5.SS5)、[§V-F](https://arxiv.org/html/2611.07950v1#S5.SS6)、[Table VI](https://arxiv.org/html/2611.07950v1#S5.T6)、[§VI](https://arxiv.org/html/2611.07950v1#S6)、[§VII](https://arxiv.org/html/2611.07950v1#S7)、[Acknowledgment](https://arxiv.org/html/2611.07950v1#Sx1)
- `abstract` — arXiv abstract page, 2611.07950v1. [https://arxiv.org/abs/2611.07950v1](https://arxiv.org/abs/2611.07950v1)
- `code` — Official code repository, release v1.0.0. [https://github.com/buidangkhoa-vn/Benchmarking-of-Class-Imbalance-Strategies-for-Multimodal-Chest-X-Ray-and-EHR-Classification](https://github.com/buidangkhoa-vn/Benchmarking-of-Class-Imbalance-Strategies-for-Multimodal-Chest-X-Ray-and-EHR-Classification)
- PDF v1：[https://arxiv.org/pdf/2611.07950v1](https://arxiv.org/pdf/2611.07950v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.07950](https://doi.org/10.48550/arXiv.2611.07950)

[Home](../) · [AI Papers](./)
