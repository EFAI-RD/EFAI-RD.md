---
catalog_id: "arxiv:2609.23950"
editors:
  - "Clare"
refs:
  main:
    title: "ORION-CMR: On-scanner Reporting with Integrated Foundation Model for End-to-End Cardiac MRI Analysis and Interpretation"
    url: "https://arxiv.org/html/2609.23950v1"
status: published
skill_version: "write-ai-paper@2.8"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 報告在病人下檢查台前就寫好：ORION-CMR 把整條心臟 MRI 判讀搬上掃描儀

## 來源

- 團隊：Philips North America 的 MR Clinical Science 部門，與 Mayo Clinic Rochester 放射科；第一作者 Omer Burak Demirel，作者群另含 Timothy L. Kline、Panagiotis Korfiatis、Ivana Isgum 與 Tim Leiner。[(ref: main author block)](https://arxiv.org/html/2609.23950v1)
- 論文：*ORION-CMR: On-scanner Reporting with Integrated Foundation Model for End-to-End Cardiac MRI Analysis and Interpretation*。
- 識別碼：[arXiv:2609.23950](https://arxiv.org/abs/2609.23950)；[DOI: 10.48550/arXiv.2609.23950](https://doi.org/10.48550/arXiv.2609.23950)。
- 全文：[arXiv HTML v1 版](https://arxiv.org/html/2609.23950v1)；[PDF 版](https://arxiv.org/pdf/2609.23950v1)。
- HTML 版提供逐節與逐表錨點（`#S2.SS1`、`#S2.T1`、`#S3.T4` 等），本文的章節層級 ref 以此為主。本次取用時 `arxiv.org/abs` 與 `doi.org` 皆持續回傳 HTTP 429，因此投稿日期、分類代碼與授權條款未經核對，本文不引述這些欄位；上列 DOI 為 arXiv 制式配發的形式，本回合未能實際解析。

**編輯：** Clare

這篇論文把心臟 MRI 從「掃完、送出、排隊等人判讀」改成「掃完之後約 90 秒，掃描儀自己吐出一份結構化報告」，並且用一個刻意設計的分工讓語言模型不碰影像。[(ref: main Abstract)](https://arxiv.org/html/2609.23950v1#abstract1)

## 流程

![左上為掃描儀端四個階段的耗時長條：sequence classification 11.2 秒、cine SAX segmentation 51.6 秒、LGE 與疾病分類 9.7 秒、報告生成 11.2 秒，四段合計 83.7 秒，論文自述端到端約 90 秒；左下為 68 份生成報告的專家評分分布，concordant 81.4%、intermediate 13.7%、discordant 4.9%；右側為保留臨床測試集上 ORION-CMR 與 ResNet-18 基線的 AUC 對照，含 95% 信賴區間，涵蓋 LGE、normal-vs-abnormal 與三個疾病類別](assets/orion-cmr-on-scanner-reporting.png)

圖：本書庫依論文 2.6 節的耗時數據、3.2 節的報告評分分布，以及 Table 4 與 Table 5 的 AUC 與信賴區間重畫，數值均直接取自原文，不含本文額外推論。[(ref: main §2.6)](https://arxiv.org/html/2609.23950v1#S2.SS6) [(ref: main §3.2)](https://arxiv.org/html/2609.23950v1#S3.SS2) [(ref: main Table 4)](https://arxiv.org/html/2609.23950v1#S3.T4) [(ref: main Table 5)](https://arxiv.org/html/2609.23950v1#S3.T5)

## 背景／問題

心臟磁振造影（cardiovascular magnetic resonance，CMR）是心臟結構與功能評估的參考標準，但論文開篇就指出它「因為取像、後處理與判讀都複雜而始終被低度使用」。[(ref: main Abstract)](https://arxiv.org/html/2609.23950v1#abstract1)

作者把這個低度使用拆成兩個具體的供給面數字：全美判讀 CMR 的醫師不到一千人，而接近七千萬名美國人住在距離 CMR 服務五十英里以外的地方。[(ref: main §1)](https://arxiv.org/html/2609.23950v1#S1)

既有的 AI 研究多半處理單一任務——分割、單一疾病分類、或單獨的報告生成——而不是一條能接進臨床工作流程的完整路徑。論文把自己的定位寫成第一個「經過臨床評估的、掃描儀原生（scanner-native）的端到端 CMR 基礎模型」。[(ref: main §1)](https://arxiv.org/html/2609.23950v1#S1) [(ref: main Abstract)](https://arxiv.org/html/2609.23950v1#abstract1)

值得先標記的是這條路徑的邊界：它要解決的不是「模型能不能比人準」，而是「整套判讀能不能在取像現場完成、而且不把病人資料送出機器」。[(ref: main §2.6)](https://arxiv.org/html/2609.23950v1#S2.SS6)

## 方法摘要

一個共用的 Vision Transformer（ViT）編碼器以自監督方式預訓練，之後接上五個下游任務：序列分類、cine 短軸（short-axis，SAX）分割、延遲釓顯影（late gadolinium enhancement，LGE）偵測、疾病分類，以及報告生成。[(ref: main §2.1)](https://arxiv.org/html/2609.23950v1#S2.SS1)

關鍵的分工在最後一步。影像端的四個任務把結果收斂成一份**確定性的結構化表示**（量測值與類別標籤），語言模型只從這份結構化表示寫成放射科風格的報告，不直接讀影像。[(ref: main §4)](https://arxiv.org/html/2609.23950v1#S4)

整條管線部署在一台裝有 GPU 的臨床掃描儀上，由序列分類自動觸發對應的下游任務，最後把報告以 DICOM series 輸出，全程不對外連網。[(ref: main §2.6)](https://arxiv.org/html/2609.23950v1#S2.SS6)

## 方法詳解

**自監督預訓練。** 採 DINO 式的 teacher–student 架構，骨幹為 ViT-Base，比較了 16×16 與 8×8 兩種 patch 尺寸（ViT-B16 與 ViT-B8）。每張影像取兩個 224×224 的 global view 與六個 96×96 的 local view；增強包含強度裁切、隨機縮放裁切、水平翻轉、旋轉、亮度與對比抖動、高斯模糊、彈性形變與加性高斯雜訊。最佳化器為 AdamW，基礎學習率 5 × 10⁻⁵，cosine 衰減搭配 10 個 epoch 的 warmup；teacher momentum 以 cosine 排程由 0.996 升至 1.0，teacher temperature 在 warmup 期間由 0.04 升到 0.07。[(ref: main §2.3)](https://arxiv.org/html/2609.23950v1#S2.SS3)

**序列分類。** 院內影像由四位放射科醫師歸類成 11 種 CMR 序列（localizer、cine 2／3／4 腔與短軸、LGE、flow、perfusion，以及 T1／T2／T2* mapping）。取最後兩個 transformer block 的串接 embedding（1,536 維）送進 MLP 分類器，損失為 cross-entropy。[(ref: main §2.4.1)](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS1)

**分割。** 影像縮放到 256×256、強度正規化並轉成三通道；取最後四個 block 的 patch token 串接後重塑成空間特徵圖，再由一個輕量卷積解碼器產生全解析度分割。訓練 50 個 epoch，AdamW 學習率 2 × 10⁻⁴、weight decay 10⁻⁴、batch size 8，損失為類別加權 cross-entropy 加 soft Dice。ACDC 的目標是右心室（RV）、心肌（Myo）與左心室（LV），EMIDEC 則是心肌與疤痕（scar）。[(ref: main §2.4.2)](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS2)

**LGE 與疾病分類。** 取 classification token（CLS）embedding，在受試者層級做平均池化與 L2 正規化，再用校準過的線性支持向量機（SVM）分類。ACDC 疾病分類用最後四個 block 的 3,072 維表示；LGE 二元梗塞分類用最後兩個 block 的 1,536 維表示；院內四類疾病分類則把 cine 2 腔、4 腔、短軸與 LGE 短軸的 CLS embedding 串成 4 × 1,536 維。[(ref: main §2.4.3)](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS3)

**報告生成。** 分割輸出、LGE 分類與疾病分類先整合成一份結構化的檢查表示；心室容積、射出分率與指標化左心室質量依 Healthy Hearts Consortium（HHC）2024 的年齡、性別與族裔別參考值判讀。這份結構化結果再交給本機部署、透過 Ollama 執行的 Qwen2.5-14B-Instruct，生成放射科風格的 CMR 報告。[(ref: main §2.4.4)](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS4)

**評估設計。** 對照組包含監督式基線（序列分類用 ResNet-50、分割用 U-Net、疾病與 LGE 分類用 ResNet-18）、先前發表的 CMR-FM，以及各資料集已發表的 state of the art。分割指標為 Dice 係數與 Hausdorff 距離（dH，單位 mm），分類指標為 AUC、準確率、敏感度與特異度；報告以 concordant／intermediate／discordant 三級量表評分，讀者間一致性以 Cohen's κ 計算，顯著水準設在 P < 0.05。[(ref: main §2.5)](https://arxiv.org/html/2609.23950v1#S2.SS5)

**掃描儀端實作。** 完整管線部署於一台 Philips 1.5T Ambition X MRI，搭配 NVIDIA RTX A6000 GPU。序列分類的結果自動觸發對應下游任務，量測值與發現逐步累積進結構化表示，最後由語言模型生成報告並以 DICOM series 匯出，過程中不與外部網路通訊。[(ref: main §2.6)](https://arxiv.org/html/2609.23950v1#S2.SS6)

## 資料與實驗

下表是本書庫依 2.2 節整理的資料設計。預訓練與臨床驗證用的是同一家機構的院內資料，公開基準則另外兩套。[(ref: main §2.2)](https://arxiv.org/html/2609.23950v1#S2.SS2)

| 面向 | 內容 |
|---|---|
| 預訓練資料 | 12,896,733 張 CMR 影像切片，來自 9,258 份多廠牌檢查 |
| 來源與年份 | Mayo Clinic 回溯收集，2017–2025；GE Healthcare 與 Siemens 掃描儀 |
| 族群特徵 | 平均年齡 55.5 ± 17.2 歲；女性佔 45.9%（4,247／9,258） |
| 涵蓋序列 | localizer、cine、LGE、T1／T2／T2* mapping、perfusion、phase-contrast flow |
| 公開基準一 | ACDC（cine 短軸）：疾病分類與心室分割 |
| 公開基準二 | EMIDEC（PSIR-LGE）：梗塞分類與疤痕分割 |
| 臨床驗證世代 | 426 位受試者（正常 168、先天性心臟病 66、擴張型心肌病 80、心肌梗塞 112） |
| 開發／測試切分 | 開發 358 位；保留測試 68 位（正常 25、先天性心臟病 7、擴張型心肌病 15、心肌梗塞 21） |
| 掃描儀端硬體 | Philips 1.5T Ambition X＋NVIDIA RTX A6000 |

下表重製論文 Table 1，是兩個公開基準上的分類 AUC。[(ref: main Table 1)](https://arxiv.org/html/2609.23950v1#S2.T1)

| 方法 | ACDC cine-SAX 疾病分類 | EMIDEC LGE-SAX 梗塞分類 |
|---|---:|---:|
| ResNet-18（監督式基線） | 0.480 | 0.667 |
| CMR-FM | 0.700 | 0.733 |
| ORION-CMR（ViT-B16 消融） | 0.740 | 0.870 |
| **ORION-CMR（ViT-B8）** | **0.820** | **0.930** |
| 已發表 state of the art | 0.960 | 0.920 |

單位為 AUC。請注意兩欄的方向並不一致：EMIDEC 上 ORION-CMR 超過已發表最佳值，ACDC 上則明顯落後。[(ref: main §3.1)](https://arxiv.org/html/2609.23950v1#S3.SS1)

下表重製論文 Table 2 的分割結果，Dice 越高越好、Hausdorff 距離（dH，mm）越低越好。CMR-FM 該列原文未列出 dH。[(ref: main Table 2)](https://arxiv.org/html/2609.23950v1#S2.T2)

| 資料集／結構 | U-Net | CMR-FM | ORION-CMR（ViT-B8） | 已發表 SoTA |
|---|---:|---:|---:|---:|
| ACDC — LV Dice | 0.932 | 0.933 | 0.942 | **0.949** |
| ACDC — LV dH | 12.853 | — | 8.527 | **7.150** |
| ACDC — Myo Dice | 0.833 | 0.879 | 0.878 | **0.922** |
| ACDC — Myo dH | 29.549 | — | 16.417 | **8.700** |
| ACDC — RV Dice | 0.837 | 0.907 | 0.899 | **0.910** |
| ACDC — RV dH | 30.285 | — | 13.606 | **11.650** |
| EMIDEC — Myo Dice | 0.817 | 0.844 | **0.915** | 0.879 |
| EMIDEC — Myo dH | 18.655 | — | **6.110** | 13.010 |
| EMIDEC — Scar Dice | 0.395 | — | **0.799** | 0.712 |
| EMIDEC — Scar dH | 9.182 | — | **3.034** | 3.120 |

下表重製論文 Table 4，是保留臨床測試世代（n = 68）上的兩組分類結果，括號內為 95% 信賴區間。[(ref: main Table 4)](https://arxiv.org/html/2609.23950v1#S3.T4)

| 任務／模型 | AUC | 準確率 | 敏感度 | 特異度 |
|---|---|---|---|---|
| LGE — ResNet-18 | 0.706（0.600–0.803） | 0.650（0.550–0.740） | 0.708（0.660–0.885） | 0.520（0.377–0.661） |
| LGE — ORION-CMR | 0.826（0.722–0.918） | 0.797（0.680–0.822） | 0.774（0.622–0.913） | 0.816（0.686–0.927） |
| 正常 vs 異常 — ResNet-18 | 0.761（0.632–0.874） | 0.765（0.667–0.852） | 0.804（0.691–0.906） | 0.680（0.476–0.864） |
| 正常 vs 異常 — ORION-CMR | 0.960（0.906–0.998） | 0.912（0.838–0.971） | 0.954（0.881–1.000） | 0.840（0.682–0.964） |

下表重製論文 Table 5，是四類疾病的 one-vs-rest AUC。[(ref: main Table 5)](https://arxiv.org/html/2609.23950v1#S3.T5)

| 類別（測試集 n） | ResNet-18 | ORION-CMR |
|---|---|---|
| 正常（25） | 0.761（0.633–0.879） | 0.960（0.906–0.998） |
| 先天性心臟病（7） | 0.821（0.730–0.913） | 0.848（0.667–1.000） |
| 擴張型心肌病（15） | 0.674（0.517–0.814） | 0.845（0.691–0.967） |
| 心肌梗塞（21） | 0.720（0.594–0.836） | 0.877（0.767–0.964） |

序列分類（Table 3）未另立表：ORION-CMR 的整體準確率為 0.992，ResNet 基線為 0.925；差距主要出現在 mapping 序列，基線在 T2 只有 0.033、T1 只有 0.456，而 ORION-CMR 分別為 0.975 與 0.991。[(ref: main Table 3)](https://arxiv.org/html/2609.23950v1#S2.T3)

## 結果

- **公開基準上的成績是分裂的** — EMIDEC 梗塞分類 0.930 超過已發表最佳值 0.920，ACDC 疾病分類 0.820 則明顯低於最佳值 0.960；兩者都大幅超過 CMR-FM（0.733 與 0.700）與監督式基線（0.667 與 0.480）。論文指出 ACDC 相對監督式基線的差距具統計顯著性（P < 10⁻²）。[(ref: main §3.1)](https://arxiv.org/html/2609.23950v1#S3.SS1) [(ref: main Table 1)](https://arxiv.org/html/2609.23950v1#S2.T1)
- **LGE 分割是最強的一項** — EMIDEC 上心肌 Dice 0.915、疤痕 Dice 0.799，均超過已發表最佳值（0.879 與 0.712），Hausdorff 距離也同步下降（心肌 6.110 對 13.010）。cine 短軸分割則與最佳值相當但未超越，心肌一項落差最大（0.878 對 0.922）。[(ref: main §3.1)](https://arxiv.org/html/2609.23950v1#S3.SS1) [(ref: main Table 2)](https://arxiv.org/html/2609.23950v1#S2.T2)
- **patch 尺寸的影響一致而明確** — ViT-B8 在每一項下游任務都優於 ViT-B16，作者因此把 B8 用於後續全部實驗，並認為較細的 patch 表示更能捕捉小型解剖結構與局部心肌異常。[(ref: main §3.1)](https://arxiv.org/html/2609.23950v1#S3.SS1) [(ref: main §4)](https://arxiv.org/html/2609.23950v1#S4)
- **臨床世代的正常／異常判別最突出** — AUC 0.960（0.906–0.998）、準確率 0.912、敏感度 0.954、特異度 0.840，明顯高於 ResNet-18 的 0.761。四類疾病的 one-vs-rest AUC 介於 0.845 到 0.960。[(ref: main §3.2)](https://arxiv.org/html/2609.23950v1#S3.SS2) [(ref: main Table 4)](https://arxiv.org/html/2609.23950v1#S3.T4) [(ref: main Table 5)](https://arxiv.org/html/2609.23950v1#S3.T5)
- **生成報告與原始臨床判讀的相符率為 81.4%** — 68 份報告中 81.4% ± 1.7% 評為 concordant、13.7% ± 3.7% 為 intermediate、4.9% ± 2.2% 為 discordant；讀者兩兩之間的觀察一致率為 76.5–88.2%，Cohen's κ 介於 0.41 到 0.61。[(ref: main §3.2)](https://arxiv.org/html/2609.23950v1#S3.SS2) [(ref: main Figure 2)](https://arxiv.org/html/2609.23950v1#S3.F2)
- **端到端約 90 秒，瓶頸在分割** — 序列分類 11.2 ± 3.9 秒、cine 短軸分割 51.6 ± 15.5 秒、LGE 與疾病分類 9.7 ± 3.3 秒、報告生成 11.2 ± 3.2 秒。四段相加為 83.7 秒，論文自述的端到端時間約 90 秒。[(ref: main §2.6)](https://arxiv.org/html/2609.23950v1#S2.SS6)

## 限制

論文自列五項限制。第一，臨床驗證只在單一中心、規模相對小的世代上完成，其中先天性心臟病子群僅 7 人。第二，心室量測是對照原始臨床報告驗證，而非對照專家重新描繪的輪廓。第三，各管線元件的消融研究有限。第四，語言模型的提示詞設計與結構化資料 schema 仍需進一步評估。第五，雖然在配備 GPU 的掃描儀上證實可行（約 90 秒），能否擴展到沒有 GPU 的機型並不清楚。[(ref: main §4)](https://arxiv.org/html/2609.23950v1#S4)

以下幾點是本書庫對照全文與表格後的觀察，不是論文的結論：

- **真正可搬走的是那道分工，而不是 90 秒** — 影像端輸出確定性的量測與類別，語言模型只負責把這份結構寫成句子。這讓「模型憑空生出一個沒看到的發現」這件事在架構上就難以發生，代價則是報告的內容上限被前一段的結構化 schema 鎖死：schema 沒有的欄位，報告就不可能提到。這是一個明確的取捨，不是純粹的改良。
- **81.4% 的分母是原始臨床報告，不是重新建立的金標準** — 論文自己說明心室量測對照的是原始報告。同一份原始報告既是比較基準，也可能帶有當初判讀者的誤差；再加上讀者間 κ 只有 0.41–0.61（中等），這個數字能承載的推論比表面上窄。它說明的是「與現行報告相符」，不是「比現行報告正確」。
- **先天性心臟病那一格的區間幾乎不帶資訊** — AUC 0.848 的 95% 信賴區間是 0.667–1.000，來自 7 個陽性案例。這一格與其說是結果，不如說是提醒：四類疾病的表格在視覺上等寬，實際的證據強度卻差了數倍。
- **「基礎模型」的價值在這篇裡是廣度而非單點最佳** — ACDC 疾病分類 0.820 對已發表最佳值 0.960 是很大的落差。把這篇讀成「全面超越」會誤讀；比較貼近的讀法是：同一個編碼器在五個任務上都達到可用水準，而且能在掃描儀上跑完，這個組合是既有的單點最佳模型做不到的。
- **要壓縮時間，該動的是分割** — 51.6 秒佔了四段合計的六成以上，而且標準差 15.5 秒也是四段裡最大的。任何關於「能不能更快」或「能不能上非 GPU 機型」的討論，若不先處理 cine 短軸分割，其餘三段加起來也只有 32 秒左右的空間。
- **不對外連網是一項獨立的設計價值** — 報告以 DICOM series 就地輸出、全程不與外部通訊。在跨境資料傳輸受限或院內網路政策嚴格的環境裡，這一點往往比 AUC 差幾個百分點更能決定一套系統能不能進場；論文把它寫在方法裡，而不是當成賣點。

## 與書庫其他文章的關係

分割天花板那篇的結論是「把左心室遮罩當成輔助輸入餵給 EF 回歸模型不會變準」，本篇則把分割放在另一個位置——用來產生要寫進報告的量測值，而不是當成回歸模型的額外輸入通道，兩篇合起來說明分割的價值取決於它被放在管線的哪一段: [先把左心室框出來，射出分率就會更準嗎？一條 10.5% 的分割天花板](2026-09-23-segmentation-ceiling-ef-regression.md)

nMAS 把射出分率當成心衰竭特徵工程的上游欄位使用，本篇則處理那個欄位在心臟 MRI 端如何被自動量測、判讀並寫成報告: [Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）](2026-09-15-tracing-the-heart.md)

RadVLM 的分節評估拆解的是「報告讀起來順不順」與「寫得對不對」的落差，本篇的 81.4% 相符率同樣是整份報告層級的單一數字，兩篇對照可以看出報告品質的評估粒度差異: [報告讀起來很順，就代表寫對了嗎？RadVLM 的分節評估](2026-09-22-radvlm-section-based-report-evaluation.md)

CORAL 讓模型先定位病灶、再敘述臨床概念以換取可檢視性，本篇則更進一步把敘述權交給一個只讀結構化量測的語言模型，兩篇代表「報告可檢視性」的兩種強度: [CORAL：先找病灶、再說臨床概念，能讓醫療影像報告更可檢視嗎？](2026-09-17-coral-concept-grounded-report-generation.md)

## 實務的啟發

第一，要降低報告生成的幻覺風險，最有效的介入點往往不在語言模型本身。本篇的做法是讓語言模型只看得到一份確定性的結構化量測，它想編也沒有素材可編。在院內專案裡，這個設計的實作成本遠低於為生成式模型加一層事後查核，而且失敗模式更容易預測——問題會退化成「schema 少了一個欄位」，而不是「報告裡出現了一個不存在的發現」。

第二，驗收報告生成時，先問清楚比較基準是什麼。81.4% 相符率對照的是原始臨床報告，而讀者間一致性只有中等。同一套評估如果改成對照重新建立的共識判讀，數字通常會變動。驗收文件裡值得固定記下三件事：基準是誰寫的、讀者有幾位、他們彼此的一致性是多少。

第三，把部署環境當成規格的一部分來評估，而不是等模型選定之後再談。本篇的 90 秒是在一台配了 RTX A6000 的掃描儀上量到的，論文也明說非 GPU 機型的可行性未知。院內採購若只比較離線基準的分數，很容易在導入階段才發現分數最高的模型跑不進現場的時間窗。

第四，讀多任務基礎模型的成績表時，分開看「贏過誰」。本篇贏過先前的 CMR 基礎模型與監督式基線是一致的，但對照各資料集已發表的最佳值則有輸有贏。把這兩種比較混在一起講，會同時高估通用模型的單點能力，也低估它在廣度與部署上的真正價值。

第五，小子群的信賴區間要當成閘門，不是註腳。先天性心臟病 7 例撐出來的 0.667–1.000，在任何臨床決策討論裡都不足以支撐結論。與其在表格裡與其他類別並列呈現，不如在評估計畫階段就先訂好每個子群的最低案例數，達不到的就標為未驗證。

## References

- `main`：[arXiv HTML 全文 v1](https://arxiv.org/html/2609.23950v1)；本文使用其 [Abstract](https://arxiv.org/html/2609.23950v1#abstract1)、[§1 Introduction](https://arxiv.org/html/2609.23950v1#S1)、[§2.1 ORION-CMR Framework](https://arxiv.org/html/2609.23950v1#S2.SS1)、[§2.2 Patient and Data Characteristics](https://arxiv.org/html/2609.23950v1#S2.SS2)、[§2.3 Self-Supervised Foundation Model Training](https://arxiv.org/html/2609.23950v1#S2.SS3)、[§2.4.1 Sequence Classification](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS1)、[§2.4.2 Segmentation](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS2)、[§2.4.3 LGE and Disease Classification](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS3)、[§2.4.4 Report Generation](https://arxiv.org/html/2609.23950v1#S2.SS4.SSS4)、[§2.5 Evaluation](https://arxiv.org/html/2609.23950v1#S2.SS5)、[§2.6 On-Scanner Implementation](https://arxiv.org/html/2609.23950v1#S2.SS6)、[§3.1 Public Benchmark Results](https://arxiv.org/html/2609.23950v1#S3.SS1)、[§3.2 Report Evaluation](https://arxiv.org/html/2609.23950v1#S3.SS2)、[§4 Discussion](https://arxiv.org/html/2609.23950v1#S4)、[Table 1](https://arxiv.org/html/2609.23950v1#S2.T1)、[Table 2](https://arxiv.org/html/2609.23950v1#S2.T2)、[Table 3](https://arxiv.org/html/2609.23950v1#S2.T3)、[Table 4](https://arxiv.org/html/2609.23950v1#S3.T4)、[Table 5](https://arxiv.org/html/2609.23950v1#S3.T5)、[Figure 1](https://arxiv.org/html/2609.23950v1#S1.F1) 與 [Figure 2](https://arxiv.org/html/2609.23950v1#S3.F2) 等章節與圖表。
- `pdf`：[arXiv PDF 全文](https://arxiv.org/pdf/2609.23950v1)，與 HTML 版同一 v1。
- `abs`：[arXiv 摘要頁](https://arxiv.org/abs/2609.23950)（canonical 入口）。本次取用時該頁持續回傳 HTTP 429，投稿日期、分類與授權條款未經核對，文中未引述。
- `doi`：[10.48550/arXiv.2609.23950](https://doi.org/10.48550/arXiv.2609.23950)（arXiv 制式配發形式；本次取用時 doi.org 回傳 HTTP 429，未能實際解析）。
- `acdc`：[ACDC（Automated Cardiac Diagnosis Challenge）官方頁](https://www.creatis.insa-lyon.fr/Challenge/acdc/)，論文用於 cine 短軸疾病分類與心室分割基準。
- `emidec`：[EMIDEC（Emidec Challenge）官方頁](https://emidec.com/)，論文用於 PSIR-LGE 梗塞分類與疤痕分割基準。

[Home](../) · [AI Papers](./)
