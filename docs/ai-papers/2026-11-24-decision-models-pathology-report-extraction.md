---
parent: AI Papers
nav_order: 3
title: "病理報告抽取：Nimble 一次問 25 題，pT 準確率只剩 0.49"
catalog_id: "arxiv:2611.20129"
editors:
  - "Clare"
refs:
  main:
    title: "Can decision models extract clinical data from cancer pathology reports? An evaluation of accuracy, calibration, and failure modes"
    url: "https://arxiv.org/html/2611.20129v1"
  abs:
    title: "arXiv abstract page: 2611.20129v1"
    url: "https://arxiv.org/abs/2611.20129v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 病理報告抽取：Nimble 一次問 25 題，pT 準確率只剩 0.49

## 來源

- 團隊：印度加爾各答 Tata Medical Center，作者為放射腫瘤科 Indranil Mallick 與病理科 Paromita Roy。[(ref: main author block)](https://arxiv.org/html/2611.20129v1)
- 論文：*Can decision models extract clinical data from cancer pathology reports? An evaluation of accuracy, calibration, and failure modes*，arXiv:2611.20129v1（cs.CL；交叉列於 cs.AI、cs.LG），2026-11-15 提交，目前只有 v1，未註記投稿或接受的 venue；授權 CC BY 4.0。[(ref: abstract)](https://arxiv.org/abs/2611.20129v1)
- 識別碼：arXiv [2611.20129](https://arxiv.org/abs/2611.20129v1)；DOI [10.48550/arXiv.2611.20129](https://doi.org/10.48550/arXiv.2611.20129)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.20129v1)、[PDF v1](https://arxiv.org/pdf/2611.20129v1)。
- 程式與資料：論文沒有程式碼或資料釋出聲明，也沒有經費與利益衝突聲明；25 題 decision model 題目與每個選項的說明完整列在附錄 Table S2，九條一致性規則列在 Table S1。[(ref: main Supplementary)](https://arxiv.org/html/2611.20129v1#Ax1)
- 研究性質：單一中心、回顧性的完整研究，不是 pilot；兩個 decision model 與兩個生成式對照模型都實際跑過全部 1,113 份報告，主要指標附病例層級 bootstrap 95% CI，欄位比較附 Holm 校正。參考標準是臨床資料庫，不是為本研究重新標註的金標準。[(ref: main §2.1)](https://arxiv.org/html/2611.20129v1#S2.SS1) [(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文與表格為準；只以圖呈現的逐欄位準確率熱圖（Figure 2）、混淆矩陣（Figure 3）與 reliability diagram（Figure 4）的個別讀值未納入本文引述。

**編輯：** Clare

作者把 decision model（每題從固定選項中選一個、並對每個選項給機率，不生成文字）拿來從 1,113 份口腔癌病理報告抽 25 個欄位：4B 的 Tev1 平均欄位準確率 0.917，與 9B 生成式模型 Qwen3.5 相同、快四倍；但同為 decision model 的 Nimble 9B 在 25 題一次送出時，pT 只答對 0.488，改成一次兩題後在同一批抽樣報告上升到 0.850。[(ref: main §3.2)](https://arxiv.org/html/2611.20129v1#S3.SS2) [(ref: main §3.3)](https://arxiv.org/html/2611.20129v1#S3.SS3) [(ref: main §3.9)](https://arxiv.org/html/2611.20129v1#S3.SS9)

## 流程

![左右兩欄圖。左欄為流程圖，標題「Decision-model extraction with escalation (Sections 2.4, 2.7, 3.7)」：上排兩個淺藍底、深藍實線圓角框，左為「State: one pathology report (1,113 oral cavity SCC reports, single centre)」，右為「25 typed "choice" questions (fixed option lists; all 25 in one request)」；兩支箭頭指向中間淺藍底、深藍實線框「Decision model (Tev1 4B / Nimble 9B) returns 1 option per question + a probability for every option」；再分出兩支箭頭，左下為淺綠底、綠色實線框「p of chosen option >= 0.94 Keep the answer」，右下為淺橘底、橘褐色實線框「p < 0.94 Escalate that question to GLM-5.3-flash」；下方文字「Simulated cascade, Tev1 4B: MFA 0.917 alone -> 0.982 with 37.7% of answer cells escalated (GLM-5.3-flash alone 0.986)」；左下角小字「Redrawn by EFAI-RD from arXiv:2611.20129v1 Sections 2.4-2.7 and 3.7」。右欄為長條圖，標題「Table 6: pT accuracy on 200 sampled reports, original option order」，縱軸「pT accuracy」刻度 0.0–1.0；兩組長條，灰色為「25 questions per request」、藍色為「2 questions per request」：Nimble 9B 為 0.490 與 0.850，Tev1 4B 為 0.990 與 0.990。](assets/decision-model-cascade-and-request-size.png)

*圖：本書庫依論文 §2.4–2.7 與 §3.7 重繪的抽取與升級流程（左；機率門檻 0.94、升級到 GLM-5.3-flash 為論文的模擬情境），以及同一批 200 份抽樣報告上，一次問 25 題與一次問 2 題的 pT 準確率（右）。數值來自 [§3.7](https://arxiv.org/html/2611.20129v1#S3.SS7) 與 [Table 6](https://arxiv.org/html/2611.20129v1#S3.T6)。*

## 背景／問題

作者的出發點是：口腔鱗狀細胞癌的病理報告承載分期與輔助治療決策所需的大部分資訊，但仍有許多報告是敘述式文字，要變成登記、稽核與研究用的結構化資料得靠人工摘錄；作者認為人工摘錄慢、成本高、本身也會出錯，這一點論文沒有另外引用數據。[(ref: main §1)](https://arxiv.org/html/2611.20129v1#S1)

作者引用文獻指出，生成式 LLM 已能從病理報告高準確度抽取欄位，但仍有兩個問題：答案以文字輸出，需要再解析、比對允許值；而且沒有直接的「這個值有多可能是對的」訊號，口述信心校準不佳，以 token 機率估計則要額外計算或校準步驟。[(ref: main §1)](https://arxiv.org/html/2611.20129v1#S1)

decision model 是 2026 年 9 月出現的一類語言模型：輸入一段文字「state」與一組型別化問題，每題從固定選項中選一個，並回傳每個選項的機率。作者表示就其所知，這類模型尚未在臨床文字上被評估過；兩個可本機執行的開放權重 decision model 都沒有用臨床文字訓練，Nimble 的開發者也註明其機率是選項間的正規化分數，不是校準過的正確機率。[(ref: main §1)](https://arxiv.org/html/2611.20129v1#S1) 本篇要問的是：這類模型在長而專門的病理報告上能抽得多準、它給的機率能不能拿來決定哪些答案要再查。

## 方法摘要

- **任務** — 從 1,113 份口腔鱗狀細胞癌手術病理報告抽 25 個欄位（16 個類別欄位、3 個照報告抄錄的分期欄位、6 個轉成類別的數值欄位），以前瞻維護的臨床資料庫為參考標準。[(ref: main §2.1)](https://arxiv.org/html/2611.20129v1#S2.SS1) [(ref: main §2.3)](https://arxiv.org/html/2611.20129v1#S2.SS3)
- **模型** — 兩個 decision model：Nimble 9B（Qwen3.5-9B 加 LoRA adapter）與 Tev1 4B（Qwen3.5 4B 的實驗性微調）；兩個生成式對照：本機的 Qwen3.5 9B，以及經雲端 API 呼叫的 GLM-5.3-flash。[(ref: main §2.4)](https://arxiv.org/html/2611.20129v1#S2.SS4) [(ref: main §2.5)](https://arxiv.org/html/2611.20129v1#S2.SS5)
- **主要指標** — mean field accuracy（MFA）：全部 25 個欄位、所有報告的「報告×欄位」格子中答對的比例；另報 Cohen's kappa、14 項臨床關鍵發現的 sensitivity／specificity。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)
- **機率分析** — 以 decision model 對所選選項的機率預測答案是否正確：AUROC、expected calibration error（ECE）、Brier score，以及只接受高於門檻的答案時的保留比例與準確率。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)
- **cascade 模擬** — 機率低於門檻 t 的答案改用另一個模型（Qwen3.5 9B 或 GLM-5.3-flash）或假設全對的人工覆核答案取代。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)
- **穩健性** — 在 200 份抽樣報告上改變 pT 與切緣題的選項順序，並對 100 份報告重跑全部 25 題檢查可重複性。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)

## 方法詳解

- **報告與排除** — 單一三級癌症醫院 2012–2020 年接受原發手術切除的病人，報告去識別化；1,194 份中排除 58 份（25 個欄位寫不到 5 個）與 23 份（原發腫瘤不在口腔），留下 1,113 份，長度中位數 2,102 字元（IQR 1,773–2,567）。倫理委員會豁免知情同意。[(ref: main §2.1)](https://arxiv.org/html/2611.20129v1#S2.SS1)
- **參考標準** — 病人照護期間建立、由一位臨床專家與一位病理科醫師對照報告核對過的臨床資料庫；建立或修正參考標準時沒有用到任何模型輸出。資料庫值再映射成 25 個研究欄位。[(ref: main §2.2)](https://arxiv.org/html/2611.20129v1#S2.SS2)
- **數值欄位改成類別** — 因為 decision model 只能選選項，腫瘤大小、侵犯深度（depth of invasion）、腫瘤厚度、陽性淋巴結數、檢查淋巴結數、最大受侵淋巴結大小六個欄位都切成類別；剛好落在切點的值歸入較低類別。每個欄位的空白值代表「報告未記載」，視為有效標籤。[(ref: main §2.3)](https://arxiv.org/html/2611.20129v1#S2.SS3) [(ref: main Table 1)](https://arxiv.org/html/2611.20129v1#S2.T1)
- **decision model 設定** — 兩個模型都以 Ollama 0.40.6 在一台 Intel Arc GPU（Intel Core Ultra 7、32 GB RAM）的機器上執行，Nimble 為 Q8_0。state 是報告全文前加兩句說明報告類型的文字；25 題全部是「choice」型，題目文字與選項標籤取自給生成式模型的欄位定義，並以程式確認每個選項都對得上生成式 schema 的允許值。25 題一次送出；伺服器端會為每一題各組一個 prompt，等於報告被處理 25 次。同分時取第一個列出的選項。題目在看到結果後沒有修改。[(ref: main §2.4)](https://arxiv.org/html/2611.20129v1#S2.SS4)
- **生成式對照設定** — 同一份 prompt 檔（system prompt、user template 與各欄位定義），每份報告一個請求，輸出以列出允許值的 JSON schema 約束，temperature 0、每請求 context 8,192 tokens；本機模型關閉 thinking，雲端模型保留 thinking；每個模型在 2026-10-08 至 10-11 只跑一次。生成式模型輸出的數值再用與參考標準相同的函式切成類別。[(ref: main §2.5)](https://arxiv.org/html/2611.20129v1#S2.SS5)
- **計分** — 正規化大小寫與空白後完全相符才算對；請求失敗算全空白（四個模型都沒有發生）。decision model 的「Not reported」視為空白（皮膚欄位例外，因為參考標準本身就有這個標籤）。部分欄位 decision model 沒有空白選項，作者另做把空白與替代選項合併的敏感度分析。[(ref: main §2.6)](https://arxiv.org/html/2611.20129v1#S2.SS6)
- **統計** — MFA 的 95% CI 來自病例層級 percentile bootstrap（2,000 次）；模型間差異用配對病例層級 bootstrap；逐欄位準確率附 Wilson 區間，以 exact McNemar 比較並在每一對模型內對 25 個欄位做 Holm 校正。ECE 用 10 個等寬區間。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)
- **一致性規則** — 九條同一份報告不可能違反的規則，例如 pN0 卻有陽性淋巴結、皮質骨侵犯卻是 pT1–T3；規則同時套用在各模型答案與參考標準上，參考標準的違反數代表真實報告本身的矛盾頻率。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7) [(ref: main Table S1)](https://arxiv.org/html/2611.20129v1#Ax1.T1)
- **請求大小的比較是事後分析** — 選項順序實驗每個請求只送 pT 與切緣兩題，主實驗送 25 題；作者利用原始順序那一組，在同一批報告上事後比較兩種請求大小。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7)
- **論文未交代** — 生成式模型使用的 prompt 檔全文；decision model state 前那兩句報告類型說明的原文；正文說模型 digest 列於 Table S2，但 HTML 版 Table S2 的內容是 25 題題目與選項，未見 digest；Nimble 在每題 prompt 中帶入整組題庫的解釋，作者明說沒有檢查伺服器如何組 prompt，屬推論。[(ref: main §2.4)](https://arxiv.org/html/2611.20129v1#S2.SS4) [(ref: main §4)](https://arxiv.org/html/2611.20129v1#S4)

## 資料與實驗

### 資料

| 項目 | 內容 |
|---|---|
| 報告 | 1,113 份口腔鱗狀細胞癌手術病理報告（1,194 份中排除 81 份），單一中心，2012–2020 年治療 |
| 原發部位 | 舌 501（45.0%）、頰黏膜 362（32.5%）、下齒槽 144（12.9%），其餘部位各 13–34 份 |
| 頸部廓清 | 1,101 份 |
| 常未記載的欄位 | 腫瘤厚度 711 份、WPOI 697 份、AJCC 版本 702 份、侵犯深度 370 份、pT 118 份 |
| 欄位 | 25 個：原發腫瘤 15、淋巴結 7、分期 3、轉成類別的數值 6 |
| 參考標準 | 前瞻維護的臨床資料庫，經臨床專家與病理科醫師對照報告核對；23 份紀錄本身違反至少一條一致性規則 |

[(ref: main §2.1)](https://arxiv.org/html/2611.20129v1#S2.SS1) [(ref: main §2.3)](https://arxiv.org/html/2611.20129v1#S2.SS3) [(ref: main §3.1)](https://arxiv.org/html/2611.20129v1#S3.SS1) [(ref: main Table 2)](https://arxiv.org/html/2611.20129v1#S3.T2) [(ref: main §3.6)](https://arxiv.org/html/2611.20129v1#S3.SS6)

| 模型 | 類型 | 執行方式 | 每份報告平均時間 |
|---|---|---|---|
| GLM-5.3-flash | Generative | Ollama Cloud API，保留 thinking | 23.6 s（雲端，與本機時間不可比） |
| Qwen3.5 9B | Generative | 本機，關閉 thinking | 60.8 s |
| Tev1 4B | Decision | 本機 Ollama | 15.0 s |
| Nimble 9B | Decision | 本機 Ollama，Q8_0 | 44.3 s |

[(ref: main §2.4)](https://arxiv.org/html/2611.20129v1#S2.SS4) [(ref: main §2.5)](https://arxiv.org/html/2611.20129v1#S2.SS5) [(ref: main §3.8)](https://arxiv.org/html/2611.20129v1#S3.SS8)

### 實驗

主要結果，節錄論文 Table 3（MFA 括號為 95% CI；時間為每份報告平均，雲端時間與本機不可比）：

| Model | Type | MFA (95% CI) | Primary tumour | Nodal | Staging | Binned numeric | Mean kappa | Reports fully correct | Time (s) |
|---|---|---|---|---|---|---|---|---|---|
| GLM-5.3-flash | Generative, cloud | 0.986 (0.984–0.987) | 0.984 | 0.983 | 0.998 | 0.985 | 0.951 | 73.3% | 23.6 |
| Qwen3.5 9B | Generative, local | 0.918 (0.916–0.921) | 0.887 | 0.971 | 0.953 | 0.971 | 0.822 | 5.7% | 60.8 |
| Tev1 4B | Decision, local | 0.917 (0.913–0.920) | 0.905 | 0.927 | 0.951 | 0.868 | 0.810 | 10.0% | 15.0 |
| Nimble 9B | Decision, local | 0.862 (0.858–0.866) | 0.834 | 0.962 | 0.769 | 0.871 | 0.740 | 1.8% | 44.3 |

[(ref: main Table 3)](https://arxiv.org/html/2611.20129v1#S3.T3)

部分臨床關鍵發現的 sensitivity／specificity，節錄論文 Table 4（n 為參考標準陽性數）：

| Finding | n | Tev1 4B | Nimble 9B | Qwen3.5 9B | GLM-5.3-flash |
|---|---|---|---|---|---|
| PNI present | 464 | 1.000 / 1.000 | 1.000 / 0.998 | 1.000 / 0.997 | 1.000 / 0.998 |
| Cortical bone invasion | 239 | 0.983 / 0.994 | 0.987 / 0.999 | 0.983 / 0.994 | 0.996 / 1.000 |
| Margin involved | 33 | 0.485 / 0.997 | 0.758 / 0.994 | 0.697 / 0.997 | 0.939 / 0.999 |
| Margin close or involved | 207 | 0.657 / 0.939 | 0.961 / 0.752 | 0.348 / 0.996 | 0.990 / 0.990 |
| Depth of invasion > 10 mm | 327 | 0.511 / 0.990 | 0.838 / 0.879 | 1.000 / 0.997 | 0.997 / 1.000 |
| ENE present | 239 | 0.929 / 0.999 | 0.992 / 0.999 | 0.987 / 0.999 | 0.996 / 0.999 |
| pT4 | 285 | 1.000 / 0.998 | 0.814 / 0.994 | 1.000 / 0.998 | 1.000 / 1.000 |

[(ref: main Table 4)](https://arxiv.org/html/2611.20129v1#S3.T4)

200 份抽樣報告上，請求大小與選項順序對 pT 與切緣準確率的影響，搬自論文 Table 6（括號為答案與原始順序相同的比例；最後一欄只更動 pT 選項，切緣題不變）：

| Model | Field | 25 questions (main run) | 2 questions, original order | Reversed | Shuffled | Without Tx, T0, Tis |
|---|---|---|---|---|---|---|
| Nimble 9B | pT | 0.490 | 0.850 | 0.840 (92.5%) | 0.830 (95.0%) | 0.855 (92.5%) |
| Nimble 9B | Margin | 0.785 | 0.850 | 0.795 (94.5%) | 0.855 (98.5%) | 0.860 (99.0%) |
| Tev1 4B | pT | 0.990 | 0.990 | 1.000 (99.0%) | 0.995 (99.5%) | 0.995 (98.5%) |
| Tev1 4B | Margin | 0.895 | 0.900 | 0.895 (95.5%) | 0.875 (94.5%) | 0.885 (98.5%) |

[(ref: main Table 6)](https://arxiv.org/html/2611.20129v1#S3.T6)

## 結果

- **整體準確率** — Tev1 的 MFA 0.917 與 Qwen3.5 9B 的 0.918 沒有差異（差 −0.002，95% CI −0.005 至 0.001，p = 0.26）；Nimble 0.862，比自己的 base model Qwen3.5 9B 低 0.056；GLM-5.3-flash 0.986，比 Tev1 高 0.069。把空白與替代選項合併只讓 MFA 變動約 0.0002。[(ref: main §3.2)](https://arxiv.org/html/2611.20129v1#S3.SS2)
- **同分不同錯** — Tev1 與 Qwen3.5 9B 錯在不同欄位：Tev1 在原發腫瘤欄位高 0.018，在淋巴結欄位低 0.044、在轉成類別的數值欄位低 0.103。[(ref: main §3.2)](https://arxiv.org/html/2611.20129v1#S3.SS2)
- **有規律的錯誤** — Nimble 的 pT 準確率 0.488（Tev1 為 0.992）：332 個 T2 中有 194 個答成 T0、211 個 T1 中 73 個答成 Tx、164 個 T3 中 76 個答成 Tis。Tev1 從未選「Bone not resected」，使 532 份標本中沒有骨頭的報告都被標成「Not involved」，骨侵犯欄位準確率 0.503。Nimble 在 179 份報告標出 basaloid 組織型（參考標準為 0），把切緣判為 close 或 involved 的報告有 424 份（參考標準 207 份）。[(ref: main §3.3)](https://arxiv.org/html/2611.20129v1#S3.SS3)
- **數值欄位最弱** — 兩個 decision model 在侵犯深度（Tev1 0.795、Nimble 0.686）與腫瘤厚度（0.835、0.770）最差，兩個生成式模型都在 0.980 以上；作者指出 Tev1 有 143 份侵犯深度超過 10 mm 的報告被判成 5–10 mm。[(ref: main §3.3)](https://arxiv.org/html/2611.20129v1#S3.SS3) [(ref: main §4)](https://arxiv.org/html/2611.20129v1#S4)
- **臨床關鍵發現** — PNI、LVI、WPOI-5 與皮質骨侵犯的 sensitivity 四個模型都在 0.98–1.00；Tev1 只抓到 33 個 involved margin 中的 16 個（0.48），Nimble 對 close 或 involved margin 的 PPV 為 0.47。[(ref: main §3.4)](https://arxiv.org/html/2611.20129v1#S3.SS4)
- **機率與校準** — 全部欄位合併時，所選選項機率預測答對的 AUROC 為 Nimble 0.878、Tev1 0.844，ECE 0.022 與 0.026，Brier score 0.089 與 0.067。只接受機率 ≥ 0.9 的答案時，Nimble 保留 65.7%、準確率 97.3%，Tev1 保留 69.7%、準確率 97.7%；門檻 0.95 時為 58.0%／98.6% 與 60.0%／98.9%。但有系統性錯誤的欄位校準最差：Tev1 骨侵犯欄位平均機率 0.845、實際準確率 0.503，ECE 0.370。[(ref: main §3.5)](https://arxiv.org/html/2611.20129v1#S3.SS5)
- **一致性** — 違反至少一條規則的報告數：參考標準 23、GLM-5.3-flash 22、Qwen3.5 9B 66、Tev1 91、Nimble 112。[(ref: main §3.6)](https://arxiv.org/html/2611.20129v1#S3.SS6) [(ref: main Table 5)](https://arxiv.org/html/2611.20129v1#S3.T5)
- **cascade** — 機率低於 0.94 的答案升級給 GLM-5.3-flash 時，Tev1 達 0.982（37.7% 的格子被升級）、Nimble 達 0.981（40.1%）；升級給 Qwen3.5 9B 最多只到 0.927。以假設全對的人工覆核取代機率低於 0.95 的答案，Tev1 達 0.993、覆核 40.0% 的格子。但門檻從 0.8 往上，至少 89% 的報告都有一個以上被升級的格子。[(ref: main §3.7)](https://arxiv.org/html/2611.20129v1#S3.SS7)
- **選項順序不是原因，請求大小才是** — 反轉、打亂或拿掉 Tx／T0／Tis，兩個模型的 pT 準確率變動都不超過 0.02（p ≥ 0.12），Nimble 的錯誤答案也沒有跟著選項位置移動。同一批 200 份報告改成一次兩題，Nimble 的 pT 從 0.490 升到 0.850（p < 0.001），在 170 份有記載 pT 的報告中從 0.576 升到 0.994；Tev1 兩種請求大小的 pT 答案完全相同。[(ref: main §3.9)](https://arxiv.org/html/2611.20129v1#S3.SS9)
- **可重複性與成本** — 100 份報告重跑 25 題，Nimble 改變 3／2,500 個答案、Tev1 改變 6／2,500 個。同樣 25 題，Tev1 每份報告平均用 26,559 個輸入 tokens，Nimble 用 146,515 個。[(ref: main §3.9)](https://arxiv.org/html/2611.20129v1#S3.SS9) [(ref: main §3.8)](https://arxiv.org/html/2611.20129v1#S3.SS8)

## 限制

- **單一中心、單一癌別** — 報告來自一家醫院、一種語言與書寫風格、一個癌症部位，作者明說結果不一定能轉移到其他報告格式。[(ref: main Limitations)](https://arxiv.org/html/2611.20129v1#S4.SS0.SSS0.Px1)
- **參考標準本身有錯** — 臨床資料庫有 23 筆紀錄違反一致性規則；對模型與資料庫不一致答案的病理科覆核仍在進行，論文 v1 沒有這部分結果。[(ref: main Limitations)](https://arxiv.org/html/2611.20129v1#S4.SS0.SSS0.Px1)
- **任務被簡化** — 數值欄位只比對類別，比抽出實際量測值粗；題目只寫一次、沒有調整，作者認為改寫「未記載／未切除」這類標籤的題目可能提高準確率。[(ref: main Limitations)](https://arxiv.org/html/2611.20129v1#S4.SS0.SSS0.Px1)
- **Nimble 的數字低估了模型本身** — 主實驗一次送 25 題，作者明說這低估了 Nimble；一次兩題的結果只有 200 份抽樣報告，且是事後比較，全隊列重跑留待後續。[(ref: main Limitations)](https://arxiv.org/html/2611.20129v1#S4.SS0.SSS0.Px1) [(ref: main §5)](https://arxiv.org/html/2611.20129v1#S5)
- **比較條件不完全對稱** — 雲端 GLM-5.3-flash 保留 thinking、本機模型關閉；它是作者設定的準確率上限，作者也指出雲端處理在院內常規使用未必可接受。[(ref: main §2.5)](https://arxiv.org/html/2611.20129v1#S2.SS5) [(ref: main §4)](https://arxiv.org/html/2611.20129v1#S4)
- **其他** — 只測兩個早期版本的 decision model，時間數據來自一台機器；cascade 是在既有答案上的模擬，人工覆核假設全對，不是前瞻流程。[(ref: main §2.7)](https://arxiv.org/html/2611.20129v1#S2.SS7) [(ref: main Limitations)](https://arxiv.org/html/2611.20129v1#S4.SS0.SSS0.Px1)

## 與書庫其他文章的關係

兩篇都在問 LLM 抽取報告時附帶的機率訊號能不能決定哪些答案要再查；CCTA 那篇用生成式模型的 token 不確定性區分讀錯報告與檢查本身不一致，本篇則用 decision model 直接回傳的選項機率做門檻與升級，並顯示系統性錯誤（如骨侵犯欄位）會在高機率下出現: [LLM 不確定性抓得出讀錯報告，抓不出 CCTA 與心導管落差](2026-11-17-llm-uncertainty-extraction-vs-clinical-discordance.md)

RadKev 把 decision model 用公開放射資料專科化，並以答案機率做 coverage at 5% error；本篇改用未經臨床專科化的開放權重 decision model 抽病理報告欄位，並發現同一組權重的表現會隨一次送出的題數大幅改變，因此作者「首次在臨床文字上評估」的說法應讀成作者自己的文獻範圍: [RadKev：放射專科化後平均多 4.9 點，換一家醫院就沒了](2026-10-15-radkev-radiology-decision-model.md)

## 實務的啟發

- **把請求設計當成模型的一部分來驗證** — 同一組權重的 pT 準確率可以是 0.49 或 0.99，差在一次送幾題；這在本研究只有 200 份報告的事後比較，但足以作為待驗證的警訊：評估 decision model 或任何批次抽取設定時，驗證的配置要和上線時一模一樣。
- **數值欄位不要問成選擇題** — 本研究中 decision model 在侵犯深度、腫瘤厚度等轉成類別的欄位最弱，作者建議改由生成式模型或規則抽出數值，再用程式切類別；這是可借用的作法，但在本研究中沒有直接測試其效果。
- **合併的校準數字看不到單一欄位的系統性錯誤** — ECE 0.022–0.026 很好看，Tev1 在骨侵犯欄位卻以平均 0.845 的機率答對一半；以機率門檻決定自動接受前，應逐欄位驗證，並加上類似本篇九條規則的一致性檢查。
- **升級要以欄位為單位** — 門檻 0.8 以上時至少 89% 報告有被升級的格子，整份報告送審不會省工；作者提出的「只把可靠欄位交給 decision model、低機率答案單題升級、規則檢查後再送人工」流程，目前只是在單一中心既有答案上的模擬，前瞻與外院驗證都還沒有做。
- **升級的對象要明顯更強** — 升級到同級的 Qwen3.5 9B 最多只到 0.927；若更強的模型只能在雲端，報告文字就會離開醫院，作者也指出這在禁止雲端處理的環境需要另找強的本機模型。

## References

- **main** — Mallick I, Roy P. *Can decision models extract clinical data from cancer pathology reports? An evaluation of accuracy, calibration, and failure modes*. arXiv:2611.20129v1, 2026. HTML: https://arxiv.org/html/2611.20129v1 ；deep links used: [§1](https://arxiv.org/html/2611.20129v1#S1)、[§2.1](https://arxiv.org/html/2611.20129v1#S2.SS1)、[§2.2](https://arxiv.org/html/2611.20129v1#S2.SS2)、[§2.3](https://arxiv.org/html/2611.20129v1#S2.SS3)、[Table 1](https://arxiv.org/html/2611.20129v1#S2.T1)、[§2.4](https://arxiv.org/html/2611.20129v1#S2.SS4)、[§2.5](https://arxiv.org/html/2611.20129v1#S2.SS5)、[§2.6](https://arxiv.org/html/2611.20129v1#S2.SS6)、[§2.7](https://arxiv.org/html/2611.20129v1#S2.SS7)、[§3.1](https://arxiv.org/html/2611.20129v1#S3.SS1)、[Table 2](https://arxiv.org/html/2611.20129v1#S3.T2)、[§3.2](https://arxiv.org/html/2611.20129v1#S3.SS2)、[Table 3](https://arxiv.org/html/2611.20129v1#S3.T3)、[§3.3](https://arxiv.org/html/2611.20129v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.20129v1#S3.SS4)、[Table 4](https://arxiv.org/html/2611.20129v1#S3.T4)、[§3.5](https://arxiv.org/html/2611.20129v1#S3.SS5)、[§3.6](https://arxiv.org/html/2611.20129v1#S3.SS6)、[Table 5](https://arxiv.org/html/2611.20129v1#S3.T5)、[§3.7](https://arxiv.org/html/2611.20129v1#S3.SS7)、[§3.8](https://arxiv.org/html/2611.20129v1#S3.SS8)、[§3.9](https://arxiv.org/html/2611.20129v1#S3.SS9)、[Table 6](https://arxiv.org/html/2611.20129v1#S3.T6)、[§4](https://arxiv.org/html/2611.20129v1#S4)、[Limitations](https://arxiv.org/html/2611.20129v1#S4.SS0.SSS0.Px1)、[§5](https://arxiv.org/html/2611.20129v1#S5)、[Supplementary](https://arxiv.org/html/2611.20129v1#Ax1)、[Table S1](https://arxiv.org/html/2611.20129v1#Ax1.T1)
- **abs** — arXiv abstract page: https://arxiv.org/abs/2611.20129v1 ；DOI: https://doi.org/10.48550/arXiv.2611.20129 ；PDF: https://arxiv.org/pdf/2611.20129v1

[Home](../) · [AI Papers](./)
