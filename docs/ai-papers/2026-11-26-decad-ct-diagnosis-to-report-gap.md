---
parent: AI Papers
nav_order: 3
title: "CT 報告模型問得出卻寫不出：先列發現再寫，F1 15.9→39.0"
catalog_id: "arxiv:2611.30458"
editors:
  - "Clare"
refs:
  main:
    title: "Decompose and Describe: Narrowing the Diagnosis-to-Report Gap in 3D CT Report Generation"
    url: "https://arxiv.org/html/2611.30458v1"
  abs:
    title: "arXiv abstract page: 2611.30458v1"
    url: "https://arxiv.org/abs/2611.30458v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# CT 報告模型問得出卻寫不出：先列發現再寫，F1 15.9→39.0

## 來源

- 團隊：Zhisong Wang、Wanxing Chang（共同第一作者）、Weiwei Cao、Fenghe Tang、Bowen Shi、Ruifeng Yuan、Yong Xia、Jianpeng Zhang（後兩位為通訊作者）；單位為 DAMO Academy（Alibaba Group）、Hupan Lab（杭州）、寧波市第二醫院放射科，以及江蘇省多模態數位孿生技術重點實驗室（蘇州）。[(ref: PDF v1 title page)](https://arxiv.org/pdf/2611.30458v1) [(ref: abstract)](https://arxiv.org/abs/2611.30458v1)
- 論文：*Decompose and Describe: Narrowing the Diagnosis-to-Report Gap in 3D CT Report Generation*，arXiv:2611.30458v1（cs.CV），2026-11-23 提交，目前只有 v1；作者註記為 30 頁、9 張圖、14 張表（含附錄）；未註記發表場合；授權為 arXiv 非專屬散布授權 1.0。[(ref: abstract)](https://arxiv.org/abs/2611.30458v1)
- 識別碼：arXiv [2611.30458](https://arxiv.org/abs/2611.30458v1)；DOI [10.48550/arXiv.2611.30458](https://doi.org/10.48550/arXiv.2611.30458)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.30458v1)、[PDF v1](https://arxiv.org/pdf/2611.30458v1)。
- 程式與資料：論文沒有提供程式或模型權重的連結；資料為公開的 CT-RATE（胸部）與 Merlin（腹部），依官方切分。[(ref: main Appendix A)](https://arxiv.org/html/2611.30458v1#A1)
- 研究性質：方法研究，三層分解都實際訓練與推論，不是 pilot 規模，並在五個現成醫療 VLM 與一個自建 VLM 上重複比較；所有數字都是單次執行，沒有信賴區間、標準差或多個隨機種子。報告中的疾病標籤由 RadBERT（CT-RATE）與作者自訓的 ModernBERT（Merlin）分類器抽取，作者明說沒有專家評估。[(ref: main §2.1)](https://arxiv.org/html/2611.30458v1#S2.SS1) [(ref: main Limitations)](https://arxiv.org/html/2611.30458v1#S6.SS0.SSS0.Px1)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、表 1–4 與附錄表 5–14 為準；論文圖 1、圖 3、圖 8–9 只引用正文寫出的數值；論文以圖片呈現的訓練與推論 prompt 未納入引述。

**編輯：** Clare

同一批胸部 CT，五個醫療視覺語言模型逐病問「有沒有」時的 macro-F1 都高於自己寫出的報告，作者把這個落差稱為 diagnosis-to-report gap，並顯示只要讓模型在寫報告前先輸出一份陽性發現清單，報告的 macro-F1 就能大幅上升（自建 Qwen3-4B 版在 CT-RATE 從 15.9 到 39.0）。[(ref: main Table 1)](https://arxiv.org/html/2611.30458v1#S3.T1) [(ref: main Table 3)](https://arxiv.org/html/2611.30458v1#S3.T3)

## 流程

![左右兩個面板。左側面板標題「(a) 四種訓練／推論設定（架構相同，只改輸出順序與可見的視覺 token）」，由上而下四列，每列左邊是彩色實線圓角框寫設定名稱、右邊是白色實線圓角框寫說明，左側框之間以向下箭頭相連：第一列灰色框「Report Adaptation」，說明「CT 全體積 → 報告」；第二列淺橘色框「Diagnostic decomposition」，說明「CT 全體積 → 陽性發現清單 a → 報告 r」；第三列淺藍色框「+ Regional textual」，說明「依區域 z 各問一次：CT 全體積 + 區域指令 → a_z → r_z（CT-RATE：肺、心臟、主動脈／縱膈、食道）」；第四列淺綠色框「+ Regional visual」，說明「同上，但 LLM 只看得到區域 z 對應的視覺 token（Qwen3-4B 版每個區域 32 個）」。左下角註記「推論時陽性發現清單由模型自己生成；各區域描述串接成最終報告，清單不納入評分。」右側面板標題「(b) 論文 Table 3：Qwen3-4B + region-level 對齊編碼器」，縱軸「報告 macro-F1（%）」刻度 0–60，四組直條由左至右為「Report Adaptation」「+ Diag.」「+ Diag. + Text」「+ Diag. + Text + Visual」，每組左邊橘色為 CT-RATE（胸部，18 類）：15.9、39.0、41.6、52.1；右邊藍色為 Merlin（腹部，30 類）：16.6、23.2、34.1、39.4，每根直條上方標數值。](assets/decad-decomposition-flow-and-ablation.png)

*圖：本書庫依論文圖 2 與 [§3](https://arxiv.org/html/2611.30458v1#S3)、[§4.1](https://arxiv.org/html/2611.30458v1#S4.SS1) 重繪的設定示意（左），區域劃分取自 [Appendix B.2](https://arxiv.org/html/2611.30458v1#A2.SS2)；右側數值取自論文表 3 中以 region-level 對比式預訓練編碼器搭配 Qwen3-4B 的四列，編碼器、LLM 初始化與訓練配對在四種設定間相同。左圖四個彩色框由上而下是對照組 Report Adaptation 與逐步加上的三層分解；右圖橘色直條為 CT-RATE、藍色直條為 Merlin。[(ref: main Figure 2)](https://arxiv.org/html/2611.30458v1#S3.F2) [(ref: main Table 3)](https://arxiv.org/html/2611.30458v1#S3.T3)*

## 背景／問題

作者引用先前研究指出，3D CT 報告生成難以同時做到流暢與診斷正確，流暢的報告不保證發現寫得完整。論文自己的對照把這個問題具體化：同一份 CT、同一組疾病類別與參考標籤下，一種問法是逐病問「Looking at these CT slices, is there <disease>? Answer yes or no.」，另一種是要模型「Generate a comprehensive radiology report」，再用報告分類器把報告轉成疾病標籤，兩者都算 macro precision、recall 與 F1。[(ref: main §1)](https://arxiv.org/html/2611.30458v1#S1) [(ref: main §2.1)](https://arxiv.org/html/2611.30458v1#S2.SS1)

在 CT-RATE 的 18 類胸部異常上，五個模型（CT-CHAT、MedGemma-1.5-4B、Lingshu-7B、HuluMed-7B、RadSight-8B）的逐病問答 macro-F1 都高於直接寫報告，差距 6.9–25.0 點；HuluMed-7B 從 46.3 掉到 21.3，recall 從 87.2 掉到 15.4。Merlin 的 30 類腹部異常上有同樣方向的落差。作者把這叫做 diagnosis-to-report gap，並問兩件事：用成對 CT-報告資料直接微調（作者稱 Report Adaptation）能不能補上？若不能，把報告生成拆成較小的步驟是否有效？[(ref: main §2.2)](https://arxiv.org/html/2611.30458v1#S2.SS2) [(ref: main Table 2)](https://arxiv.org/html/2611.30458v1#S3.T2)

這個落差有一部分來自比較方式本身。逐病問答等於把疾病清單交給模型，而 macro-F1 在類別不平衡時會獎勵「一律答有」：作者另算的 always-positive 基線在 CT-RATE 的 macro-F1 為 31.0，MedGemma-1.5 與 Lingshu-7B 的逐病問答（20.6、24.6）其實低於它，CT-CHAT（31.4）與它相當。作者以打亂影像的對照顯示問答分數確實依賴影像，並承認 yes/no 作答傾向是落差的一部分；因此「模型看得出卻寫不出」應讀成任務依賴的現象，而不是模型已具備、只是沒說出口的診斷能力。[(ref: main Table 13)](https://arxiv.org/html/2611.30458v1#A5.T13) [(ref: main Appendix E.3.2)](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS2) [(ref: main Table 12)](https://arxiv.org/html/2611.30458v1#A5.T12)

## 方法摘要

- **Report Adaptation（對照）** — 以成對 CT-報告資料直接微調 x → r，模型架構與視覺輸入不變。[(ref: main §2.3)](https://arxiv.org/html/2611.30458v1#S2.SS3)
- **Diagnostic decomposition** — 訓練目標改為 x → a → r：先輸出陽性發現清單 a（由參考報告抽出的陽性發現組成），再寫報告。架構、視覺輸入、訓練配對與報告目標都和 Report Adaptation 相同，只多了寫報告前的診斷監督；推論時清單由模型自己生成，不需外部標籤。[(ref: main §3.1)](https://arxiv.org/html/2611.30458v1#S3.SS1)
- **Regional textual decomposition** — 每個解剖區域 z 各問一次 (x, q_z) → a_z → r_z，仍保留全體積視覺輸入；各區域描述串接成完整報告。[(ref: main §3.2)](https://arxiv.org/html/2611.30458v1#S3.SS2)
- **Regional visual decomposition** — 文字任務不變，但 LLM 只能看到該區域的視覺 token。[(ref: main §3.3)](https://arxiv.org/html/2611.30458v1#S3.SS3)
- **兩組受試模型** — 一是五個現成醫療 VLM（以官方權重與前處理微調）；二是作者自建、沒有醫療 VQA 預訓練的標準 VLM：3D ResNet 編碼器＋投影層＋Qwen3-4B，編碼器先做 region-level 或 whole-image 的 CT-報告對比式預訓練後凍結。full DeCAD 指自建 VLM 搭配 region-level 編碼器與三層分解。[(ref: main §4.1)](https://arxiv.org/html/2611.30458v1#S4.SS1)
- **指標** — 主指標為報告抽出標籤後的 macro-F1；另報 METEOR、BLEU-4（文字相似度）與 RaTEScore、RadGraph-F1、GREEN（臨床報告品質，GREEN 用官方 GREEN-RadLlama2-7B）。[(ref: main Appendix A)](https://arxiv.org/html/2611.30458v1#A1)

## 方法詳解

- **訓練目標怎麼做出來** — 以 Qwen-Max 分兩步處理每份參考報告：先把 Findings 與 Impression 切成區域段落（CT-RATE 為肺、心臟、主動脈／縱膈、食道），再從各區段抽出明確陽性的異常、排除否定與不確定的描述並正規化同義詞。CT-RATE 得到 64 個獨特疾病標籤，Merlin 為 15 個區域加整體層級共 120 個；這些擴充詞彙只用於訓練，評估仍用 CT-RATE 18 類與 Merlin 30 類。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.30458v1#A2.SS1) [(ref: main Appendix B.2)](https://arxiv.org/html/2611.30458v1#A2.SS2) [(ref: main Appendix B.3)](https://arxiv.org/html/2611.30458v1#A2.SS3)
- **現成 VLM 的微調** — 兩個 epoch、learning rate 2×10⁻⁵、cosine 排程、warmup 0.03、每 GPU batch 1、梯度累積 8 步；Merlin、HuluMed-7B、Lingshu-7B、RadSight-8B 用 LoRA（r = 128、α = 256），CT-CHAT 用 LLaVA 式調整，MedGemma-1.5-4B 全參數微調。各模型沿用自己的 CT 前處理，問答與報告兩種設定用同一條輸入管線。[(ref: main Appendix A)](https://arxiv.org/html/2611.30458v1#A1)
- **自建 VLM 的編碼器** — region-level 預訓練以 3D ResNet-18 搭配輔助器官分割分支，器官遮罩內的特徵經兩層 MLP 產生 32 個 soft assignment 聚成 32 個區域 token，與報告中對應器官的描述做對比式學習（加 Dice 分割損失）；下游報告生成用未池化的 32 個 token。whole-image 預訓練則把整個體積與整份報告對齊。零樣本疾病 AUC：region-level 在 CT-RATE 與 Merlin 為 0.789 與 0.824，whole-image 為 0.744 與 0.762。[(ref: main Appendix C.1)](https://arxiv.org/html/2611.30458v1#A3.SS1)
- **自建 VLM 的報告訓練** — 凍結編碼器後聯合訓練投影層與整個 Qwen3-4B 五個 epoch（learning rate 2×10⁻⁵）；CT-RATE 體積補齊或裁切為 112×256×352、Merlin 為 96×256×384，HU 截斷在 [−1000, 1000]。訓練使用 32 張 NVIDIA H20。[(ref: main Appendix A)](https://arxiv.org/html/2611.30458v1#A1) [(ref: main Appendix C.2)](https://arxiv.org/html/2611.30458v1#A3.SS2)
- **報告標籤抽取** — CT-RATE 用公開的 RadBERT 分類器，作者以官方標籤驗證得 F1 98.1%；Merlin 用作者自訓的 ModernBERT-base（149M 參數，正類加權、句子順序打亂增強），在 Merlin 測試集上 macro AUC 98.8%、macro-F1 95.3%。[(ref: main Appendix D.1)](https://arxiv.org/html/2611.30458v1#A4.SS1) [(ref: main Appendix E.3.3)](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS3)
- **論文未交代** — 程式與權重是否公開；CT-RATE 與 Merlin 測試集的病例數（只寫「依官方切分」）；所有結果的變異（無信賴區間、無重複種子）；Qwen-Max 產生的區域段落與陽性清單是否經人工抽查；表 4 中各既有方法的數值是作者重跑還是引用文獻（其中 MedGemma-1.5、CT-CHAT、RadSight-8B 三列與表 1 未微調的 Direct 列相同）；附錄表 14 標為「whole-image」的基線與全病例診斷監督兩列，macro 數值與表 3 region-level 編碼器的對應兩列相同，論文沒有說明此處 whole-image 指的是整份報告生成還是 whole-image 編碼器。[(ref: main Table 4)](https://arxiv.org/html/2611.30458v1#S3.T4) [(ref: main Table 14)](https://arxiv.org/html/2611.30458v1#A5.T14) [(ref: main Appendix B.1)](https://arxiv.org/html/2611.30458v1#A2.SS1)

## 資料與實驗

### 資料

| 資料集 | 部位 | 規模（論文所述） | 評估類別 | 報告標籤抽取 |
|---|---|---|---|---|
| CT-RATE | 非顯影胸部 CT | 25,692 次檢查／21,304 位病人，配放射報告 | 18 類胸部異常 | RadBERT（公開） |
| Merlin | 腹部 CT | 25,494 次掃描，配放射報告 | 30 類常見影像發現 | ModernBERT-base（作者自訓） |

兩者都依官方切分；論文沒有寫出測試集病例數。[(ref: main Appendix A)](https://arxiv.org/html/2611.30458v1#A1) [(ref: main §2.1)](https://arxiv.org/html/2611.30458v1#S2.SS1)

### 實驗：CT-RATE 上五個現成醫療 VLM（論文表 1，macro-F1／P／R，%）

| Setting | CT-CHAT F1 | MedGemma-1.5-4B F1 | Lingshu-7B F1 | HuluMed-7B F1 | RadSight-8B F1 |
|---|---|---|---|---|---|
| Diagnostic VQA | 31.4 | 20.6 | 24.6 | 46.3 | 49.7 |
| Direct | 17.8 | 13.7 | 7.1 | 21.3 | 34.6 |
| Report Adapt. | 17.7 | 19.8 | 21.5 | 37.7 | 37.2 |
| Diagnostic Decomp. | 30.7 | 32.3 | 30.8 | 45.0 | 42.2 |
| Diag.+Text Decomp. | 36.6 | 34.2 | 33.4 | 51.4 | 45.8 |
| Diag.+Text+Visual | 35.7 | 34.3 | 33.9 | 49.9 | 46.4 |

| Setting | CT-CHAT R | MedGemma-1.5-4B R | Lingshu-7B R | HuluMed-7B R | RadSight-8B R |
|---|---|---|---|---|---|
| Diagnostic VQA | 85.0 | 27.9 | 59.3 | 87.2 | 66.8 |
| Direct | 18.1 | 12.4 | 5.4 | 15.4 | 30.9 |
| Report Adapt. | 15.1 | 19.5 | 17.8 | 33.2 | 33.7 |
| Diagnostic Decomp. | 30.1 | 28.9 | 27.8 | 42.9 | 40.6 |
| Diag.+Text Decomp. | 42.0 | 30.1 | 29.5 | 48.6 | 49.2 |
| Diag.+Text+Visual | 42.0 | 32.3 | 30.3 | 48.1 | 50.6 |

論文表 1 另有各模型的 macro precision，本文未轉載。[(ref: main Table 1)](https://arxiv.org/html/2611.30458v1#S3.T1)

### 實驗：Merlin 上三個模型（論文表 2，macro-F1，%）

| Setting | Merlin | HuluMed-7B | RadSight-8B |
|---|---|---|---|
| Diagnostic VQA | – | 17.3 | 40.4 |
| Direct | 16.8 | 3.8 | 19.8 |
| Report Adapt. | 25.5 | 10.8 | 32.5 |
| Diagnostic Decomp. | 27.2 | 16.5 | 36.9 |
| Diag.+Text Decomp. | 30.7 | 23.9 | 38.7 |
| Diag.+Text+Visual | 29.0 | 22.2 | 33.4 |

[(ref: main Table 2)](https://arxiv.org/html/2611.30458v1#S3.T2)

### 實驗：沒有醫療 VQA 預訓練的自建 VLM（論文表 3，macro，%）

| Encoder pretraining | Diag. | Text | Visual | CT-RATE F1 | CT-RATE P | CT-RATE R | Merlin F1 | Merlin P | Merlin R |
|---|---|---|---|---|---|---|---|---|---|
| Region-level align. | – | – | – | 15.9 | 37.6 | 15.1 | 16.6 | 32.6 | 14.1 |
| Region-level align. | ✓ | – | – | 39.0 | 45.7 | 39.0 | 23.2 | 26.2 | 27.7 |
| Region-level align. | ✓ | ✓ | – | 41.6 | 47.2 | 42.8 | 34.1 | 37.1 | 38.3 |
| Region-level align. | ✓ | ✓ | ✓ | 52.1 | 55.6 | 54.2 | 39.4 | 43.1 | 42.3 |
| Whole-image align. | ✓ | ✓ | – | 46.9 | 51.5 | 45.8 | 33.6 | 30.7 | 39.0 |
| Whole-image align. | ✓ | ✓ | ✓ | 46.0 | 54.0 | 44.1 | 30.9 | 29.4 | 38.9 |

第一列沒有任何分解，即此模型的 Report Adaptation。[(ref: main Table 3)](https://arxiv.org/html/2611.30458v1#S3.T3) [(ref: main §4.2)](https://arxiv.org/html/2611.30458v1#S4.SS2)

### 實驗：與既有方法比較（論文表 4，CT-RATE，%）

| Method | F1 | P | R | MET | BLEU | RaTE | RG | GR |
|---|---|---|---|---|---|---|---|---|
| Lingshu-32B | 9.3 | 19.7 | 8.4 | 10.4 | 1.0 | 50.4 | 5.7 | 10.8 |
| RadFM | 11.6 | 19.5 | 11.2 | 3.7 | 0.1 | 34.8 | 0.8 | 1.3 |
| MedGemma-1.5 | 13.7 | 39.4 | 12.4 | 7.1 | 0.7 | 49.6 | 10.3 | 11.1 |
| Reg2RG | 17.1 | 39.6 | 12.5 | 24.6 | 23.5 | 66.9 | 25.2 | 37.9 |
| BTB3D | 17.3 | 21.0 | 15.9 | 20.4 | 15.8 | 59.0 | 15.1 | 22.2 |
| CT-CHAT | 17.8 | 37.4 | 18.1 | 23.6 | 23.6 | 66.9 | 22.2 | 42.2 |
| Dia-LLaMA | 30.4 | 45.8 | 26.2 | 24.0 | 24.3 | 66.2 | 25.7 | 41.7 |
| RadSight-8B | 34.6 | 43.9 | 30.9 | 23.0 | 21.2 | 65.7 | 21.6 | 38.6 |
| HuluMed-32B | 38.0 | 48.0 | 37.0 | 22.5 | 17.9 | 64.1 | 17.0 | 39.8 |
| ViSD-Boost | 39.4 | 42.2 | 39.8 | 24.8 | 21.4 | 65.8 | 22.3 | 34.9 |
| AdaRAG-CT-8B | 41.8 | 45.1 | 46.7 | 24.6 | 24.2 | 65.7 | 25.8 | 26.3 |
| Ours (full DeCAD) | 52.1 | 55.6 | 54.2 | 26.3 | 27.1 | 66.5 | 23.6 | 42.0 |

F1／P／R 為 macro 診斷指標；MET、RaTE、RG、GR 分別為 METEOR、RaTEScore、RadGraph-F1、GREEN。[(ref: main Table 4)](https://arxiv.org/html/2611.30458v1#S3.T4)

### 實驗：診斷資訊的其他給法（論文表 10、表 11，CT-RATE macro-F1，%）

| 對照 | CT-CHAT | MedGemma-1.5-4B | Lingshu-7B | HuluMed-7B | RadSight-8B |
|---|---|---|---|---|---|
| Direct（不微調） | 17.8 | 13.7 | 7.1 | 21.3 | 34.6 |
| Disease Prompt（不微調，提示中給疾病清單） | 27.2 | 20.6 | 10.8 | 36.1 | 38.0 |
| Report Adapt.（微調） | 17.7 | 19.8 | 21.5 | 37.7 | 37.2 |
| Diagnostic Decomp.（微調） | 30.7 | 32.3 | 30.8 | 45.0 | 42.2 |

在自建 VLM 上，改由線性探測分類器預測標籤、再以 Dia-LLaMA 式提示交給報告模型（classifier guidance）得 macro-F1 50.7（P 44.8、R 67.9），模型自己先寫清單的 full DeCAD 為 52.1（P 55.6、R 54.2）。[(ref: main Table 11)](https://arxiv.org/html/2611.30458v1#A5.T11) [(ref: main Table 10)](https://arxiv.org/html/2611.30458v1#A5.T10)

## 結果

- **只微調補不上** — Report Adaptation 讓多數模型的報告 macro-F1 上升（例如 Lingshu-7B 7.1 → 21.5、HuluMed-7B 21.3 → 37.7），但 CT-RATE 上五個模型都仍低於各自的逐病問答；CT-CHAT 微調後反而持平（17.8 → 17.7）。Merlin 上 HuluMed-7B 與 RadSight-8B 仍落後問答 6.5 與 7.9 點。[(ref: main §2.3)](https://arxiv.org/html/2611.30458v1#S2.SS3)
- **先寫清單，五個模型都上升** — 相對 Report Adaptation，Diagnostic decomposition 在 CT-RATE 讓五個模型的 macro-F1 分別多 13.0、12.5、9.3、7.3、5.0 點，recall 全部上升；Merlin 上三個模型多 1.7、5.7、4.4 點。再依區域拆文字任務，CT-RATE 再多 1.9–6.4 點、Merlin 再多 1.8–7.4 點。[(ref: main §3.1)](https://arxiv.org/html/2611.30458v1#S3.SS1) [(ref: main §3.2)](https://arxiv.org/html/2611.30458v1#S3.SS2)
- **只給區域影像，現成模型沒受益** — 在五個現成模型上，加上 regional visual decomposition 的 CT-RATE macro-F1 變化為 −1.5 到 +0.6；Merlin 上三個模型都下降（−1.7、−1.7、−5.3）。[(ref: main §3.3)](https://arxiv.org/html/2611.30458v1#S3.SS3)
- **沒有醫療 VQA 預訓練也成立** — 自建 Qwen3-4B 版在 CT-RATE 從 15.9（Report Adaptation）到 39.0（加診斷）再到 41.6（加區域文字）；Merlin 從 16.6 到 23.2 再到 34.1；macro precision 同時上升（CT-RATE 37.6 → 47.2）。[(ref: main §4.2)](https://arxiv.org/html/2611.30458v1#S4.SS2)
- **區域影像要靠區域對齊的編碼器** — 用 region-level 編碼器時，加上 regional visual decomposition 讓 macro-F1 再多 10.5（CT-RATE，41.6 → 52.1）與 5.3（Merlin）；用 whole-image 編碼器時反而下降（46.9 → 46.0、33.6 → 30.9）。[(ref: main §4.3)](https://arxiv.org/html/2611.30458v1#S4.SS3)
- **診斷分數最高，臨床品質指標沒有領先** — full DeCAD 在 CT-RATE 的 macro-F1 52.1、precision 55.6 為表 4 最高，比次高的 AdaRAG-CT-8B 多 10.3 點，METEOR 與 BLEU-4 也最高；RaTEScore、GREEN、RadGraph-F1 則分別比最佳值低 0.4、0.2、2.2 點。逐類看差異很大：胸腔積液 F1 81.2，Medical material 的 recall 只有 15.2。[(ref: main §4.3)](https://arxiv.org/html/2611.30458v1#S4.SS3) [(ref: main Table 9)](https://arxiv.org/html/2611.30458v1#A5.T9)
- **給清單的提示能補一部分，訓練補更多** — 不微調、只在提示裡給疾病清單，五個模型的 macro-F1 都上升，其中三個超過 Report Adaptation；但 Diagnostic decomposition 在每個模型上都更高。作者據此認為疾病清單這類線索是落差的一部分原因，明確的診斷監督再往上加。[(ref: main Appendix E.2.2)](https://arxiv.org/html/2611.30458v1#A5.SS2.SSS2)
- **自己寫清單與外部分類器各有取捨** — 分類器引導的 recall 較高（67.9 對 54.2）、precision 較低（44.8 對 55.6），F1 相近（50.7 對 52.1）；作者明說這不代表自我診斷普遍優於分類器引導。[(ref: main Appendix E.2.1)](https://arxiv.org/html/2611.30458v1#A5.SS2.SSS1)
- **機制分析** — 在自建 VLM 上，寫清單階段分配給 CT 視覺 token 的平均注意力占比為 14.4%，Report Adaptation 為 5.0%；清單階段的陽性發現 micro recall 48.1%、隨後報告 47.3%，Report Adaptation 為 22.2%。只給「正常／異常」二元判斷沒有幫助（macro-F1 13.9 對 15.9）；三分之一訓練病例有清單監督時 micro precision 從 44.9% 升到 53.7%，監督涵蓋率越高 recall 越高（31.3% → 37.5% → 47.3%）。注意力占比是相關性的觀察，不是因果證據。[(ref: main §4.4)](https://arxiv.org/html/2611.30458v1#S4.SS4) [(ref: main Appendix E.4)](https://arxiv.org/html/2611.30458v1#A5.SS4)
- **問答確實依賴影像，但不全是** — 把 CT 換成別的病人後，五個模型的逐病問答 macro AUC 下降 13.1–30.5 點；always-positive 基線只在 CT-CHAT 上能解釋整個落差（13.2 對 13.6），在 HuluMed 與 RadSight 上不能（9.7 對 25.0、−3.6 對 15.1）。[(ref: main Appendix E.3.1)](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS1) [(ref: main Appendix E.3.2)](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS2)

## 限制

- **評估只到標籤層級** — 作者明說診斷評估限於 CT-RATE 與 Merlin 的標註類別，並依賴 RadBERT 與 ModernBERT 抽取報告標籤；沒有專家評估，未來需擴到更廣的臨床情境。分類器高 F1 是對參考報告的表現，對模型生成報告的抽取正確率沒有另外驗證。[(ref: main Limitations)](https://arxiv.org/html/2611.30458v1#S6.SS0.SSS0.Px1) [(ref: main Appendix E.3.3)](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS3)
- **沒有不確定性** — 所有比較都是單次執行；部分相鄰設定的差距只有 0.1–2 點（例如現成模型上的 regional visual decomposition），無法判斷是否超出隨機變異。[(ref: main Table 1)](https://arxiv.org/html/2611.30458v1#S3.T1)
- **落差的量法本身有偏** — 逐病問答把疾病清單交給模型，macro-F1 又會獎勵一律答有；三個模型的問答 F1 低於或接近 always-positive 基線。用「問答 F1 減報告 F1」量化模型「看得出卻寫不出」多少，需要連同作答傾向一起解讀。[(ref: main Table 13)](https://arxiv.org/html/2611.30458v1#A5.T13)
- **比較表的基準不一** — 表 4 混合了未針對 CT-RATE 微調的通用醫療 VLM 與專為 CT 報告訓練的方法，且未說明數值來源；Merlin 上宣稱的最佳表現只有表 2 三個模型可對照，沒有與其他已發表的腹部 CT 報告方法並列。[(ref: main Table 4)](https://arxiv.org/html/2611.30458v1#S3.T4) [(ref: main Table 2)](https://arxiv.org/html/2611.30458v1#S3.T2)
- **訓練目標由 LLM 生成** — 區域段落與陽性清單由 Qwen-Max 從參考報告抽出，論文沒有報告這一步的錯誤率；清單監督的品質直接影響報告品質。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.30458v1#A2.SS1)

## 與書庫其他文章的關係

DLoss 在訓練時改損失函數、分開處理該寫與不該寫的診斷詞，DeCAD 則不動損失也不改架構，只把訓練目標改成「先列陽性發現再寫報告」；兩篇都處理 3D CT 報告漏寫或亂寫發現，也都有 Merlin 腹部 CT 的結果: [DLoss：訓練時分開施壓該寫與不該寫的診斷詞，GREEN 多 4 分](2026-11-02-dloss-diagnostic-loss-ct-report-generation.md)

CT 報告修訂規則庫在報告寫完後以獨立影像證據修訂草稿，DeCAD 則在生成時就先讓模型自己寫出陽性發現清單；兩篇都在 CT-RATE 上以 RadBERT 抽出 18 類異常的 macro-F1 評估，兩篇的增益都以 recall 上升最明顯: [CT 報告修訂規則庫：有影像證據 CE-F1 多 11.5，只看草稿學不到](2026-11-25-ct-report-rulebank-independent-evidence.md)

DeCAD 把 Lingshu-7B 列為五個受試醫療 VLM 之一，它在 CT-RATE 直接寫報告的 macro-F1 只有 7.1、逐病問答 24.6，先列發現再寫的微調可升到 30.8；Lingshu-32B 未微調寫報告為 9.3，補上本篇 VQA 平均分數看不到的 3D CT 報告邊界: [Lingshu 靠合成資料拉高醫療 VQA，強化學習那一步沒加分](2026-09-15-lingshu-medical-vlm.md)

本篇處理的是模型「問得出卻寫不出」的判讀到文字落差，該則的產業產品則把同一段切開：判讀留在放射科醫師身上，AI 只把口述與前次報告組成結構化草稿: [不碰判讀只做文書：InteleOrchestrator Clarity 拆解](../industry-watch/2026-11-26-ge-healthcare-inteleorchestrator-clarity-reporting.md)

## 實務的啟發

- **可借用的設計** — 想提升 CT 報告的發現涵蓋率時，「先輸出陽性發現清單、再以清單與影像為條件寫報告」只改訓練目標、不改架構，在本研究的六個模型上都提高了以標籤計的 macro-F1；成本主要是要從參考報告抽出清單。[(ref: main §3.1)](https://arxiv.org/html/2611.30458v1#S3.SS1) [(ref: main §4.2)](https://arxiv.org/html/2611.30458v1#S4.SS2)
- **可借用的量測方法** — 拿同一批影像比較「逐病問答」與「自由寫報告」的標籤 F1，是檢查報告模型漏寫的簡單診斷工具；但要同時放 always-positive 與打亂影像兩個對照，才能分出作答傾向、影像依賴與真正的表達落差。[(ref: main Table 12)](https://arxiv.org/html/2611.30458v1#A5.T12) [(ref: main Table 13)](https://arxiv.org/html/2611.30458v1#A5.T13)
- **評估時先放「提示給清單」的便宜對照** — 不微調、只在提示中列出疾病清單，就讓五個模型都上升、三個超過一般微調；任何結構化或分解式報告生成方法，都應先證明自己贏過這個對照。[(ref: main Table 11)](https://arxiv.org/html/2611.30458v1#A5.T11)
- **待驗證的警訊** — 區域限定的視覺輸入在現成模型上沒有幫助、在 Merlin 上還下降，只有搭配區域對齊的編碼器才有效；臨床品質指標（GREEN、RadGraph-F1）也沒有隨診斷 F1 一起領先。在有放射科醫師審閱、附不確定性並在其他醫院資料上驗證之前，不應把標籤 F1 的提升讀成報告臨床品質的提升。[(ref: main §3.3)](https://arxiv.org/html/2611.30458v1#S3.SS3) [(ref: main Table 4)](https://arxiv.org/html/2611.30458v1#S3.T4)

## References

- `main` — Zhisong Wang, Wanxing Chang, Weiwei Cao, Fenghe Tang, Bowen Shi, Ruifeng Yuan, Yong Xia, Jianpeng Zhang. *Decompose and Describe: Narrowing the Diagnosis-to-Report Gap in 3D CT Report Generation*. arXiv:2611.30458v1, 2026. HTML：https://arxiv.org/html/2611.30458v1 ；用到的深鏈：[§1](https://arxiv.org/html/2611.30458v1#S1)、[§2.1](https://arxiv.org/html/2611.30458v1#S2.SS1)、[§2.2](https://arxiv.org/html/2611.30458v1#S2.SS2)、[§2.3](https://arxiv.org/html/2611.30458v1#S2.SS3)、[§3](https://arxiv.org/html/2611.30458v1#S3)、[Figure 2](https://arxiv.org/html/2611.30458v1#S3.F2)、[Table 1](https://arxiv.org/html/2611.30458v1#S3.T1)、[Table 2](https://arxiv.org/html/2611.30458v1#S3.T2)、[§3.1](https://arxiv.org/html/2611.30458v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.30458v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.30458v1#S3.SS3)、[Table 3](https://arxiv.org/html/2611.30458v1#S3.T3)、[Table 4](https://arxiv.org/html/2611.30458v1#S3.T4)、[§4.1](https://arxiv.org/html/2611.30458v1#S4.SS1)、[§4.2](https://arxiv.org/html/2611.30458v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.30458v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.30458v1#S4.SS4)、[Limitations](https://arxiv.org/html/2611.30458v1#S6.SS0.SSS0.Px1)、[Appendix A](https://arxiv.org/html/2611.30458v1#A1)、[Appendix B.1](https://arxiv.org/html/2611.30458v1#A2.SS1)、[Appendix B.2](https://arxiv.org/html/2611.30458v1#A2.SS2)、[Appendix B.3](https://arxiv.org/html/2611.30458v1#A2.SS3)、[Appendix C.1](https://arxiv.org/html/2611.30458v1#A3.SS1)、[Appendix C.2](https://arxiv.org/html/2611.30458v1#A3.SS2)、[Appendix D.1](https://arxiv.org/html/2611.30458v1#A4.SS1)、[Table 9](https://arxiv.org/html/2611.30458v1#A5.T9)、[Appendix E.2.1](https://arxiv.org/html/2611.30458v1#A5.SS2.SSS1)、[Table 10](https://arxiv.org/html/2611.30458v1#A5.T10)、[Appendix E.2.2](https://arxiv.org/html/2611.30458v1#A5.SS2.SSS2)、[Table 11](https://arxiv.org/html/2611.30458v1#A5.T11)、[Appendix E.3.1](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS1)、[Table 12](https://arxiv.org/html/2611.30458v1#A5.T12)、[Appendix E.3.2](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS2)、[Table 13](https://arxiv.org/html/2611.30458v1#A5.T13)、[Appendix E.3.3](https://arxiv.org/html/2611.30458v1#A5.SS3.SSS3)、[Appendix E.4](https://arxiv.org/html/2611.30458v1#A5.SS4)、[Table 14](https://arxiv.org/html/2611.30458v1#A5.T14)
- `abstract` — arXiv abstract page, 2611.30458v1：https://arxiv.org/abs/2611.30458v1 （PDF：https://arxiv.org/pdf/2611.30458v1 ；DOI：https://doi.org/10.48550/arXiv.2611.30458）

[Home](../) · [AI Papers](./)
