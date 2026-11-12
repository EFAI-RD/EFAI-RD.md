---
parent: AI Papers
nav_exclude: true
title: "PathXAI：公開集 finding F1 48.8，全答「有」得 86.3"
catalog_id: "arxiv:2611.09117"
editors:
  - "Clare"
refs:
  main:
    title: "PathXAI: Evidence-guided structured pathology reporting by transferable tissue segmentation"
    url: "https://arxiv.org/html/2611.09117v1"
  abs:
    title: "arXiv abstract page: 2611.09117v1"
    url: "https://arxiv.org/abs/2611.09117v1"
  code:
    title: "PathXAI code (GitHub)"
    url: "https://github.com/zhaorui-tan/PathXAI"
  weights:
    title: "PathXAI-Seg (MedSAM3) adapter weights (Hugging Face)"
    url: "https://huggingface.co/RayTan/PathXAI-Seg"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# PathXAI：公開集 finding F1 48.8，全答「有」得 86.3

## 來源

- 團隊：Zhaorui Tan、Jun Aun Tan、Weixiang Zhong、Xiaoxi Wang、Tan Pan、Xingdong Xue、Li Liu、Jing Zhang、Jing Zhang、Weimiao Yu，共 10 位作者；單位為 A\*STAR Bioinformatics Institute（Intelligent Digital and Molecular Pathology Lab）、浙江大學醫學院附屬第一醫院病理科、復旦大學 Artificial Intelligence Innovation and Incubation Institute、重慶大學 School of Big Data and Software Engineering，以及上海長征醫院病理科。[(ref: main author block)](https://arxiv.org/html/2611.09117v1)
- 論文：*PathXAI: Evidence-guided structured pathology reporting by transferable tissue segmentation*，arXiv:2611.09117v1（cs.CV；cross-list cs.CL），2026-11-06 提交，目前只有 v1；授權為 CC BY-NC-SA 4.0；arXiv 頁的作者註記寫明後續版本會再加入實驗結果。[(ref: abstract)](https://arxiv.org/abs/2611.09117v1)
- 識別碼：arXiv [2611.09117](https://arxiv.org/abs/2611.09117v1)；DOI [10.48550/arXiv.2611.09117](https://doi.org/10.48550/arXiv.2611.09117)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.09117v1)、[PDF v1](https://arxiv.org/pdf/2611.09117v1)。
- 程式與權重：推論程式、agent prompt、報告檢視器、兩個病理師工具與評分程式放在 GitHub [(ref: code)](https://github.com/zhaorui-tan/PathXAI)；PathXAI-Seg（MedSAM3）adapter 權重在 Hugging Face，需申請存取 [(ref: weights)](https://huggingface.co/RayTan/PathXAI-Seg)。私有病例的影像、完整報告與逐例資料不公開。[(ref: main Data availability)](https://arxiv.org/html/2611.09117v1#Sx2) [(ref: main Code availability)](https://arxiv.org/html/2611.09117v1#Sx3)
- 研究性質：方法論文，核心流程已實作並在公開與私有隊列實際跑過，非 pilot；報告模型為未微調的 Qwen3.6-27B。私有病例的使用經上海長征醫院（2024SL136、CHEC2024-421）與 Tan Tock Seng Hospital（DSRB 2025-1447）倫理審查，免除知情同意。[(ref: main §3.1)](https://arxiv.org/html/2611.09117v1#S3.SS1)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文與 Supplementary Table 9、11、12、19、21、23、28、37 為準；作者表示之後的版本會補實驗，數值可能隨版本更動。

**編輯：** Clare

PathXAI 把組織分割得到的組織組成、重新取圖與「先鎖定診斷再寫報告」的流程接到未微調的 Qwen3.6-27B，公開 1,200 例的 cancer family match rate 由直接看 H&E 的 68.1% 升到 72.5%、finding F1 由 43.0 升到 48.8；但論文自己的控制組顯示，對所有 finding 一律寫「存在」在同一個公開集 finding F1 可得 86.3。[(ref: main Supp. Table 9)](https://arxiv.org/html/2611.09117v1#Sx10.T9) [(ref: main Supp. Table 19)](https://arxiv.org/html/2611.09117v1#Sx10.T19)

## 流程

![左右兩欄圖。左欄標題「PathXAI-Report workflow (complete configuration)」，六個圓角框由上而下以向下箭頭相連：前兩個為淺藍色，依序為「1 ROI ranking」（CONCH tile-prompt similarity; up to 20 candidates; VLM picks up to 3 initial diagnostic ROIs）與「2 PathXAI-Seg (MedSAM3)」（7 tissue labels -> overlays + tissue-class fractions）；中間兩個為淺橘色，依序為「3 Diagnostic candidates」（V (with KEEP knowledge) \| T (no KEEP) \| S (tissue statistics check)）與「4 Rule-based selector + reinspection」（zoom or new ROIs; <= 4 rounds, <= 11 final ROIs）；最後兩個為淺綠色，依序為「5 Diagnosis lock + grade-focused ROIs」（2 extra H&E ROIs for writing only）與「6 Claim checks -> structured report」（supported / weak / unsupported / not assessable）。左下斜體字「Backbone: Qwen3.6-27B (Q6_K), self-hosted, no weight updates; temperature 0.2」，其下灰色小字「Redrawn by EFAI-RD from arXiv:2611.09117v1 Sec. 3.2 and Fig. 6」。右欄為長條圖，標題「Supplementary Table 19: finding F1」，縱軸「Finding F1 (%)」0–100，每個方法兩根柱，藍色為「Public evaluation (997 cases, OCR-derived references)」、橘色為「Private, pathologist reference P1 (150 cases)」：Qwen + H&E 43.0／71.6、MedGemma 37.4／38.4、PathXAI-Report (core) 46.7／67.3、PathXAI-Report 48.8／76.6、Always present (control) 86.3／42.7。](assets/pathxai-workflow-finding-f1.png)

*圖：本書庫依論文 §3.2 與 Fig. 6 重繪的 PathXAI-Report 完整設定流程（左），以及 Supplementary Table 19 中四個方法與 always present 控制組在公開評估集與私有參考集 P1 的 finding F1（右）。數值來自 [Supplementary Table 19](https://arxiv.org/html/2611.09117v1#Sx10.T19)；左欄的步驟與參數取自 [§3.2](https://arxiv.org/html/2611.09117v1#S3.SS2)。*

## 背景／問題

病理報告要把多個區域、多張切片上的組織觀察整理成具體診斷與支持它的形態描述。作者的出發點是：用明確的組織組成量測來引導以 H&E 影像為基礎的報告生成，目前少有研究；這是作者對文獻現況的判斷，論文沒有量化這個缺口。[(ref: abstract)](https://arxiv.org/abs/2611.09117v1)

作者在評估設計上另引用胸片報告的研究，說明文字相似度分不出「措辭相近但診斷錯」的報告，因此自建一套分開衡量診斷身分、形態一致性與相互矛盾陳述的評估方式。[(ref: main §3.3.2)](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS2)

## 方法摘要

- **PathXAI-Seg** — 以 MedSAM3 或 SAM2 為主幹的組織分割模型，七類共用標籤（背景、腫瘤、發炎、結締、上皮、壞死、腺體），用少量逐像素標註加大量只有影像層級標籤的輔助影像一起訓練。[(ref: main §1.2.1)](https://arxiv.org/html/2611.09117v1#S1.SS2.SSS1)
- **PathXAI-Report** — 以未微調的 Qwen3.6-27B 為報告模型：先挑 ROI、跑分割，產生診斷候選，必要時再放大或加取區域，最後鎖定診斷欄位後寫出結構化報告，並把每個主張連到影像、組織統計與檢索到的疾病知識。[(ref: main §3.2)](https://arxiv.org/html/2611.09117v1#S3.SS2)
- **兩種設定** — core 版使用分割證據與自適應重新取圖；完整版另加 KEEP 疾病知識、偏向分級的 ROI 與寫作時的診斷限制。[(ref: main §1.1.1)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS1)
- **評估** — 1,200 例 TCGA 公開評估集與 152 例私有病例（兩位病理師各寫一份參考報告），以五個自訂指標自動評分；另有兩位病理師對 132 例開發集病例做排序與修正需求評讀，以及組織輸入方式的消融比較。[(ref: main §1.1.2)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS2) [(ref: main §1.1.3)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS3)

## 方法詳解

- **ROI 排序** — CONCH 編碼 1,024 像素的影像塊（0.5 µm/pixel）與正、負向診斷文字提示，排序分數為 0.70×max 正向相似度＋0.30×mean 正向相似度−0.35×max 負向相似度；每例保留最多 20 個候選，VLM 看前 8 個候選後選出最多 3 個初始診斷 ROI（預設邊長 4,096 像素），再交給 PathXAI-Seg（MedSAM3）。[(ref: main §3.2.2)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS2)
- **診斷候選** — 先由 VLM 依 ROI 影像、解剖部位與區域組織比例評估大類與亞型是否足夠（記為 S）；再以 H&E 與分割疊圖產生兩個候選：V 在完整版會收到 KEEP 疾病圖譜檢索的定義與子類候選，T 則沒有。兩個候選的提示都不含數值組織統計。[(ref: main §3.2.3)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS3)
- **規則式選擇器** — 候選以「是否有效」與「診斷特異度」（非泛稱亞型 3、非泛稱主要診斷 2、大類 1、泛稱腫瘤 0、無效 −1）比較；腫瘤家族不一致或浸潤／原位衝突時保留 V，完整版另加浸潤狀態的保護規則。選擇、知識檢索與取圖規則都在程式中執行，不另呼叫模型。[(ref: main §3.2.3)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS3) [(ref: main §3.2.1)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS1)
- **重新取圖** — 模型回報證據是否足夠、信心、缺少的影像與非影像證據，以及可否報告；不可報告時繼續取圖，缺細胞學或核細節時優先數位放大，其他影像缺口則加取新區域。上限為每輪 2 個 ROI、4 輪、一層放大、每例最多 11 個 ROI，連續兩次診斷不變也會停止。[(ref: main §3.2.4)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS4)
- **鎖定診斷後寫作** — 完整版鎖住最終診斷的身分、亞型與浸潤欄位，另取 2 個（可設到 4 個）不做分割、只供寫作的 H&E ROI 支援分級與細胞描述。寫作前先把診斷主張與影像、組織統計、知識節點連成證據圖，以啟發式規則加 VLM 判定支持程度；修稿時肯定有支持的主張、限定弱支持的主張、刪除無支持或矛盾的主張，並明確標出無法評估的欄位。[(ref: main §3.2.5)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS5)
- **推論設定** — Qwen3.6-27B-Q6_K.gguf 自架服務，temperature 0.2、每次呼叫最多 4,096 tokens，所有 VLM 關閉 thinking mode；影像最長邊縮到 768 像素、以 JPEG quality 75 傳送。提示開發與除錯只用 456 例公開開發子集。[(ref: main §3.2.1)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS1)
- **評分方式** — 自建詞彙表含 84 個實體、236 個標準或同義表達，finding 抽取涵蓋 20 個概念（浸潤及其途徑、壞死、轉移、細胞學、組織結構、間質變化、發炎浸潤、鈣化）。只有參考報告明確記載為存在或不存在的 finding 才計分，參考沒寫不當作陰性。finding F1 的單例公式為 2C/(D+A)，D 為參考記載的 finding 數、A 為生成報告有明確主張的數量、C 為極性一致的數量。[(ref: main §3.3.2)](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS2)
- **公開參考報告的來源** — 公開集的參考文字取自 WsiCaption 釋出的 TCGA 病理報告 OCR 文字，再由 Qwen3.6-27B 重整為八段格式，並以 GPT-6.1 做一致性檢查；人工檢查後排除 51 例部位描述含病名的病例。[(ref: main Supp. 2.1)](https://arxiv.org/html/2611.09117v1#Sx9.SSx2.SSSx1)
- **不確定性** — 二元比例用 Clopper–Pearson 區間，其他平均值與配對差用 4,000 次 case bootstrap；另以 Holm 法對 126 個配對比較做多重比較敏感度分析。私有隊列沒有病人層級連結，區間假設病例彼此獨立。[(ref: main §3.3.2)](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS2) [(ref: main Supp. Table 37)](https://arxiv.org/html/2611.09117v1#Sx10.T37)
- **論文未交代** — 各方法原始的嘗試、重試與失敗次數；論文只提供最終存下的報告數。[(ref: main Supp. Table 38)](https://arxiv.org/html/2611.09117v1#Sx10.T38)
- **論文未交代** — 診斷與 finding 抽取規則、以及寫作前的自動主張檢查，作者明說都未經獨立驗證（後者未經病理師驗證）。[(ref: main §3.3.2)](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS2) [(ref: main §3.2.5)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS5)
- **論文未交代** — 私有隊列各醫院的納入條件研究團隊無法取得，也未收集年齡、性別等人口學資料；樣本數依病例可得性與病理師時間決定，沒有事前樣本數計算。[(ref: main Supp. 2.1)](https://arxiv.org/html/2611.09117v1#Sx9.SSx2.SSSx1) [(ref: main §3.1)](https://arxiv.org/html/2611.09117v1#S3.SS1)

## 資料與實驗

### 資料

| 子集 | 用途 | 規模 | 參考標準 |
|---|---|---|---|
| 公開開發子集 | 提示開發、組織輸入與流程消融、病理師評讀（其中 132 例） | 456 例 TCGA | WsiCaption OCR 報告，經 Qwen3.6-27B 重整 |
| 公開評估集 | 主要自動評估 | 1,200 例 TCGA，22 種癌別、14 個器官系統 | 同上；cancer family 用 TCGA 標籤 |
| 私有隊列 | 自動評估（主要比較 151 例共同病例） | 152 例：乳房 76（Tan Tock Seng Hospital）、攝護腺 62（五家醫院）、大腸直腸 14（上海長征醫院） | 兩位病理師各自撰寫的參考報告 P1、P2 |
| 分割訓練 | PathXAI-Seg | 逐像素標註 492 張（5 個資料集）；輔助影像取自 344,604 張、18 個資料集 | 資料集原始標註，統一為 7 類 |
| 分割測試 | 內部／外部 | 內部 124 個樣本（5 個資料集）；外部 11,089 個樣本（6 個測試集），共 5 個器官 | 資料集原始標註 |

*資料：整理自 [§1.1.2](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS2)、[§1.2.1](https://arxiv.org/html/2611.09117v1#S1.SS2.SSS1) 與 [Supplementary 2.1](https://arxiv.org/html/2611.09117v1#Sx9.SSx2.SSSx1)。*

| 私有參考報告欄位 | 兩位病理師皆有明確值 | 一致數（%） | κ [95% CI] |
|---|---|---|---|
| Specific diagnosis | 127 | 122（96.1%） | 0.939 [0.886, 0.987] |
| Malignancy | 145 | 143（98.6%） | 0.951 [0.875, 1.000] |
| Invasion | 140 | 139（99.3%） | 0.970 [0.892, 1.000] |
| Necrosis | 135 | 126（93.3%） | 0.576 [0.283, 0.799] |
| Grade（同一分級系統） | 75 | 45（60.0%） | 0.036 [−0.170, 0.246] |

*表：節錄自 [Supplementary Table 23](https://arxiv.org/html/2611.09117v1#Sx10.T23)；分級的 κ 為線性加權。*

### 實驗：公開評估集主表（Supplementary Table 9）

| Method | Cancer family match rate | Exact diagnosis match rate | Finding F1 | Finding recall | Finding contradiction rate |
|---|---|---|---|---|---|
| Qwen + H&E | 68.1 | 58.9 | 43.0 | 36.6 | 16.0 |
| DeepSeek + H&E | 71.9 | 60.3 | 42.1 | 36.1 | 23.2 |
| GLM + H&E | 61.8 | 56.0 | 44.2 | 38.1 | 22.5 |
| MedGemma | 6.7 | 6.1 | 37.4 | 31.8 | 14.4 |
| PLIP-guided Qwen | 45.7 | 39.2 | 21.9 | 17.8 | 6.3 |
| PRISM2 | 53.2 | 52.6 | NA | NA | NA |
| PathXAI-Report (core) | 68.2 | 58.1 | 46.7 | 39.4 | 9.8 |
| PathXAI-Report | 72.5 | 62.3 | 48.8 | 41.6 | 11.5 |

*表：[Supplementary Table 9](https://arxiv.org/html/2611.09117v1#Sx10.T9)，單位為 %。適用病例數：cancer family 1,200、exact diagnosis 604、finding F1／recall 997；contradiction rate 依各方法自己的可比較主張計算（351–759 例）。PRISM2 只輸出診斷。原表附各格 95% 區間。*

### 實驗：配對差與多重比較（Supplementary Table 11、37）

| PathXAI-Report 減去 | Cancer family（pp） | Exact diagnosis（pp） | Finding F1（pp） | Contradiction（pp） |
|---|---|---|---|---|
| Qwen + H&E（公開） | +4.42 [1.92, 6.75]；Holm 0.024 | +3.31 [0.00, 6.62]；Holm 1.000 | +5.75 [3.63, 7.87]；Holm <0.001 | −5.52 [−8.02, −3.11]；Holm <0.001 |
| DeepSeek + H&E（公開） | +0.58 [−1.92, 3.17]；Holm 1.000 | +1.99 [−1.82, 5.79]；Holm 1.000 | +6.67 [4.29, 9.27]；Holm <0.001 | −9.19 [−12.11, −6.17]；Holm <0.001 |
| PathXAI-Report (core)（公開） | +4.33 [2.08, 6.58]；Holm 0.007 | +4.14 [1.49, 6.79]；Holm 0.171 | +2.07 [0.29, 3.88]；Holm 0.880 | +1.38 [−0.34, 3.11]；Holm 1.000 |
| Qwen + H&E（私有 P1） | +4.13；Holm 1.000 | +13.33；Holm 0.097 | +5.00；Holm 1.000 | +4.44；Holm 1.000 |

*表：公開集的差值與 95% case-bootstrap 區間取自 [Supplementary Table 11](https://arxiv.org/html/2611.09117v1#Sx10.T11)；Holm 校正 P 值與私有 P1 差值取自 [Supplementary Table 37](https://arxiv.org/html/2611.09117v1#Sx10.T37)（126 個比較為同一族）。contradiction 為負值表示 PathXAI-Report 較少矛盾。*

### 實驗：固定答案的控制組（Supplementary Table 12、19）

| 控制或方法 | 公開評估集 | 私有 P1 | 私有 P2 |
|---|---|---|---|
| 固定診斷「squamous cell carcinoma」的 cancer family match rate | 32.8 | — | — |
| PathXAI-Report 的 cancer family match rate | 72.5 | — | — |
| Always present 的 finding F1 | 86.3 | 42.7 | 52.4 |
| Always absent 的 finding F1 | 13.7 | 57.3 | 47.6 |
| Per-finding majority 的 finding F1 | 84.2 | 42.7 | 52.4 |
| PathXAI-Report 的 finding F1 | 48.8 | 76.6 | 78.9 |

*表：固定診斷控制取自 [Supplementary Table 12](https://arxiv.org/html/2611.09117v1#Sx10.T12)（該診斷只依 456 例開發子集選定）；finding F1 控制取自 [Supplementary Table 19](https://arxiv.org/html/2611.09117v1#Sx10.T19)，三種固定極性控制不看影像、對 20 種 finding 全部作答。單位為 %。*

### 實驗：病理師評讀（Supplementary Table 28）

| Outcome | MedGemma | Qwen + H&E | PLIP-guided Qwen | PathXAI-Report (core) | PathXAI-Report |
|---|---|---|---|---|---|
| Mean rank ↓（132 例） | 2.76 | 1.63 | 3.29 | 1.60 | 1.64 |
| No / minor correction ↑（264 次評讀） | 87.88 | 73.11 | 49.62 | 74.24 | 83.33 |
| Major correction / unusable ↓ | 12.12 | 26.89 | 50.38 | 25.76 | 16.67 |
| No/minor correction with complete fields ↑ | 31.06 | 34.47 | 14.02 | 37.50 | 61.74 |

*表：節錄自 [Supplementary Table 28](https://arxiv.org/html/2611.09117v1#Sx10.T28)；兩位病理師各評 132 例開發集病例，排序 1 為最佳且允許並列，其他列為 %。原表附 case-cluster bootstrap 區間。*

## 結果

- **診斷一致率小幅領先，部分差距不穩** — 公開集 PathXAI-Report 的 cancer family match rate 72.5%、exact diagnosis match rate 62.3%，都是各方法中最高；但相對 DeepSeek + H&E 的兩項差距區間都跨過零，相對 Qwen + H&E 的 exact diagnosis 差距經 Holm 校正後 P=1.000。[(ref: main Supp. Table 11)](https://arxiv.org/html/2611.09117v1#Sx10.T11) [(ref: main Supp. Table 37)](https://arxiv.org/html/2611.09117v1#Sx10.T37) 私有隊列的 cancer family match rate 為 93.4%（P1）與 93.5%（P2），exact diagnosis 為 67.4% 與 67.6%。[(ref: main §1.1.2)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS2)
- **形態描述的增益較一致** — 公開集 finding F1 48.8，比 Qwen + H&E 高 5.75 個百分點，finding contradiction rate 在 664 例配對病例上低 5.52 個百分點。[(ref: main Supp. Table 11)](https://arxiv.org/html/2611.09117v1#Sx10.T11) 私有 P1／P2 的 finding F1 為 76.6 與 78.9，也是最高，但 contradiction 反而高於 Qwen + H&E。[(ref: main §1.1.2)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS2)
- **公開集的 finding F1 被常數控制超過** — 對 20 種 finding 一律寫「存在」的控制組在公開集 finding F1 為 86.3、per-finding majority 為 84.2，都高於所有模型；作者解釋這反映公開參考報告以陽性 finding 為主，且沒寫的 finding 不計分。[(ref: main Supp. Table 19)](https://arxiv.org/html/2611.09117v1#Sx10.T19) [(ref: main §2)](https://arxiv.org/html/2611.09117v1#S2) 例如公開集的 invasion 有 612 例記為存在、29 例記為不存在。[(ref: main Supp. Table 21)](https://arxiv.org/html/2611.09117v1#Sx10.T21) 在病理師撰寫的 P1、P2 上，always present 只有 42.7 與 52.4，低於 PathXAI-Report。[(ref: main Supp. Table 19)](https://arxiv.org/html/2611.09117v1#Sx10.T19)
- **固定診斷控制** — 只依開發子集選定、一律回答 squamous cell carcinoma 的控制組，在公開評估集的 cancer family match rate 為 32.8%，PathXAI-Report 高出 39.75 個百分點（95% CI 36.42–43.00）。[(ref: main Supp. Table 12)](https://arxiv.org/html/2611.09117v1#Sx10.T12)
- **組織統計主要幫診斷，完整流程主要幫形態與分級** — 在 456 例開發子集上，H&E 加組織統計讓 exact diagnosis match rate 增加 4.5 個百分點（352 例），疊圖則幾乎無診斷增益；相對直接輸入組織統計，PathXAI-Report 的 finding F1 高 7.7 個百分點、exact diagnosis 點估計相同，三級分級的 balanced grade accuracy 高 25.0 個百分點（174 例）。[(ref: main §1.1.4)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS4)
- **病理師評讀：修正需求與正確性不同步** — PathXAI-Report 有 61.7% 的評讀同時符合「無需或僅需小修」與「適用欄位全有作答」，Qwen + H&E 為 34.5%；平均排序三者相近（1.64、1.63、1.60）。[(ref: main Supp. Table 28)](https://arxiv.org/html/2611.09117v1#Sx10.T28) MedGemma 的「無需或僅需小修」最高（87.9%），但在同一批 132 例上 cancer family match rate 只有 10.6%（14／132）。[(ref: main Supp. 3.1)](https://arxiv.org/html/2611.09117v1#Sx10.SSx3.SSSx1)
- **兩位評讀者差異大** — Reader 1 認為 73.5% 的 PathXAI-Report 報告無需或僅需小修（Qwen + H&E 53.0%），Reader 2 則為 93.2%（兩者相同）；修正類別的線性加權 κ 在各方法間為 0.017–0.077。作者說明 PathXAI-Report 對 Qwen + H&E 的修正需求差異來自其中一位評讀者。[(ref: main Supp. 3.1)](https://arxiv.org/html/2611.09117v1#Sx10.SSx3.SSSx1) [(ref: main §1.1.3)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS3)
- **分割** — PathXAI-Seg（MedSAM3）相對同主幹微調，平均 Dice 內部高 2.6、外部高 0.8 個百分點；SAM2 版外部只高 0.1。[(ref: main §1.2.2)](https://arxiv.org/html/2611.09117v1#S1.SS2.SSS2)

## 限制

- **作者列出的限制** — 組織輸入與流程比較用的病例同時用於提示開發（公開評估集與私有隊列沒有）；HistoGPT 被評估在其皮膚病訓練領域之外；分割比較中所有模型都拿到類別身分；基礎模型的預訓練重疊未知；評讀研究只有兩位病理師、用開發子集病例，重評時看得到先前評分。作者建議以固定流程在新病例上，由更多評讀者做全新、遮蔽的研究，並做前瞻性臨床流程研究。[(ref: main §2)](https://arxiv.org/html/2611.09117v1#S2)
- **公開集的形態指標分辨力有限** — 常數控制在公開集的 finding F1 高於所有模型（[Supplementary Table 19](https://arxiv.org/html/2611.09117v1#Sx10.T19)）。本書庫的解讀是：公開集的 finding F1 只適合拿來做方法之間的相對比較，不宜當成報告形態描述的絕對品質；形態方面的結論以病理師撰寫的 P1、P2 較可依靠，而 P1 上 PathXAI-Report 對 Qwen + H&E 的各項差異經 Holm 校正後都不顯著（[Supplementary Table 37](https://arxiv.org/html/2611.09117v1#Sx10.T37)）。
- **參考標準本身的不一致** — 兩位病理師的分級一致率 60.0%、κ 0.036，壞死 κ 0.576（[Supplementary Table 23](https://arxiv.org/html/2611.09117v1#Sx10.T23)）。分級與壞死相關的「改善」都要放在這個參考雜訊下解讀。
- **評估流程與報告模型同源** — 公開參考報告由 Qwen3.6-27B 重整格式（[Supplementary 2.1](https://arxiv.org/html/2611.09117v1#Sx9.SSx2.SSSx1)），PathXAI-Report 與 Qwen + H&E 也用同一個模型生成報告。本書庫的解讀是：這可能讓用同一模型寫的報告在格式與用詞上更接近參考，論文沒有檢查這個影響。
- **評讀者身分** — 兩位評讀病理師同時撰寫私有參考報告，並列名論文作者（[§3.3.1](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS1)）；首輪評讀先評四個方法、PathXAI-Report 後加入，之後才以匿名標籤重評（[§3.3.3](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS3)）。論文未說明首輪是否遮蔽方法身分。
- **病例組成** — 公開集取自 TCGA 癌症專案，作者明說不代表例行病理中良性、交界與惡性診斷的分布；私有隊列只有乳房、攝護腺與大腸直腸三個部位。[(ref: main Supp. 2.1)](https://arxiv.org/html/2611.09117v1#Sx9.SSx2.SSSx1)

## 與書庫其他文章的關係

CONCH 的導讀記錄病理圖文預訓練的零樣本能力與邊界；PathXAI 則把 CONCH 用在流程的第一步，以影像塊與診斷提示的相似度排序候選 ROI，再交給分割與 VLM: [CONCH：零樣本病理分類很強，多類腦瘤就露出邊界](2026-09-15-conch-pathology-vlm.md)

REG 2025 指出病理報告生成的榜單分數抓不到腫瘤比例與分級失真；PathXAI 自建診斷與 finding 指標並附常數控制，顯示公開集的 finding F1 會被「全答存在」超過；兩篇都說明病理報告的自動評分需要控制組與病理師參考: [REG 2025：報告生成分數上去了，腫瘤比例與分級仍會失真](2026-09-16-reg-2025-pathology-report-generation.md)

PathXAI 把 MedGemma-1.5-4B-it 當作醫療預訓練的比較對象：它在公開集 cancer family match rate 只有 6.7%，病理師評讀卻有 87.9% 判為無需或僅需小修，可補上 MedGemma 1.5 在病理報告任務上的邊界: [MedGemma 1.5：4B 吃下 3D 影像與全切片，代價一併公開](2026-09-16-medgemma-1-5.md)

## 實務的啟發

1. **自動評分前先算常數控制。** 本篇的公開集上，「全答存在」的 finding F1 比所有模型都高；院內若用自建抽取規則評病理或影像報告，應先算全陽性、全陰性與多數類控制，確認指標分得出好壞，再比較模型。這是可直接借用的量測方法。[(ref: main Supp. Table 19)](https://arxiv.org/html/2611.09117v1#Sx10.T19)
2. **把「修正需求」和「答對與否」分開記錄。** MedGemma 被判為少修正的比例最高，cancer family 卻幾乎都錯；只問病理師「要改多少」，會漏掉內容空泛或診斷錯但看起來乾淨的報告。[(ref: main Supp. 3.1)](https://arxiv.org/html/2611.09117v1#Sx10.SSx3.SSSx1)
3. **組織分割可以當作 VLM 的輔助證據，而不是只畫疊圖。** 消融顯示把組織比例寫成數值比直接給疊圖對診斷更有幫助；但這來自同時用於提示開發的開發子集，本書庫認為只能當作待驗證的設計方向。[(ref: main §1.1.4)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS4)
4. **證據連結要連「哪一張圖支持哪一句」並保留衝突。** 論文的案例把壞死描述與正、負向的區域檢查一起保留，讓審閱者知道哪裡需要重看；作者也明說自動主張檢查尚未經病理師驗證，引用這類「supported」標記時不能當成已確認。[(ref: main §1.1.5)](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS5) [(ref: main §3.2.5)](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS5)
5. **分級類指標要先看病理師之間的一致性。** 兩位病理師分級 κ 僅 0.036，任何 AI 分級改善的幅度都應和這個基準一起呈現。[(ref: main Supp. Table 23)](https://arxiv.org/html/2611.09117v1#Sx10.T23)

## References

- `main` — Tan Z, Tan JA, Zhong W, Wang X, Pan T, Xue X, Liu L, Zhang J, Zhang J, Yu W. *PathXAI: Evidence-guided structured pathology reporting by transferable tissue segmentation*. arXiv:2611.09117v1, 2026. [https://arxiv.org/html/2611.09117v1](https://arxiv.org/html/2611.09117v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.09117v1)、[§1.1.1](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS1)、[§1.1.2](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS2)、[§1.1.3](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS3)、[§1.1.4](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS4)、[§1.1.5](https://arxiv.org/html/2611.09117v1#S1.SS1.SSS5)、[§1.2.1](https://arxiv.org/html/2611.09117v1#S1.SS2.SSS1)、[§1.2.2](https://arxiv.org/html/2611.09117v1#S1.SS2.SSS2)、[§2](https://arxiv.org/html/2611.09117v1#S2)、[§3.1](https://arxiv.org/html/2611.09117v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.09117v1#S3.SS2)、[§3.2.1](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS1)、[§3.2.2](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS2)、[§3.2.3](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS3)、[§3.2.4](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS4)、[§3.2.5](https://arxiv.org/html/2611.09117v1#S3.SS2.SSS5)、[§3.3.1](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS1)、[§3.3.2](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS2)、[§3.3.3](https://arxiv.org/html/2611.09117v1#S3.SS3.SSS3)、[Data availability](https://arxiv.org/html/2611.09117v1#Sx2)、[Code availability](https://arxiv.org/html/2611.09117v1#Sx3)、[Supp. 2.1](https://arxiv.org/html/2611.09117v1#Sx9.SSx2.SSSx1)、[Supp. 3.1](https://arxiv.org/html/2611.09117v1#Sx10.SSx3.SSSx1)、[Supp. Table 9](https://arxiv.org/html/2611.09117v1#Sx10.T9)、[Supp. Table 11](https://arxiv.org/html/2611.09117v1#Sx10.T11)、[Supp. Table 12](https://arxiv.org/html/2611.09117v1#Sx10.T12)、[Supp. Table 19](https://arxiv.org/html/2611.09117v1#Sx10.T19)、[Supp. Table 21](https://arxiv.org/html/2611.09117v1#Sx10.T21)、[Supp. Table 23](https://arxiv.org/html/2611.09117v1#Sx10.T23)、[Supp. Table 28](https://arxiv.org/html/2611.09117v1#Sx10.T28)、[Supp. Table 37](https://arxiv.org/html/2611.09117v1#Sx10.T37)、[Supp. Table 38](https://arxiv.org/html/2611.09117v1#Sx10.T38)
- `abstract` — arXiv abstract page, 2611.09117v1. [https://arxiv.org/abs/2611.09117v1](https://arxiv.org/abs/2611.09117v1)
- `code` — PathXAI code. [https://github.com/zhaorui-tan/PathXAI](https://github.com/zhaorui-tan/PathXAI)
- `weights` — PathXAI-Seg (MedSAM3) adapter weights. [https://huggingface.co/RayTan/PathXAI-Seg](https://huggingface.co/RayTan/PathXAI-Seg)
- PDF v1：[https://arxiv.org/pdf/2611.09117v1](https://arxiv.org/pdf/2611.09117v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.09117](https://doi.org/10.48550/arXiv.2611.09117)

[Home](../) · [AI Papers](./)
