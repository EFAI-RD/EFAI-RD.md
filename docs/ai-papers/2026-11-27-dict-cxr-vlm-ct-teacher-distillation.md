---
parent: AI Papers
nav_order: 2
title: "胸片 VLM 向 CT 老師學推理：一個主幹勝過重建 CT，另一個仍落後"
catalog_id: "arxiv:2611.32344"
editors:
  - "Clare"
refs:
  main:
    title: "DiCT: Teaching X-ray Vision-Language Models to Reason via Imagining CT"
    url: "https://arxiv.org/html/2611.32344v1"
  abs:
    title: "arXiv abstract page: 2611.32344v1"
    url: "https://arxiv.org/abs/2611.32344v1"
  pdf:
    title: "DiCT PDF v1"
    url: "https://arxiv.org/pdf/2611.32344v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 胸片 VLM 向 CT 老師學推理：一個主幹勝過重建 CT，另一個仍落後

## 來源

- 團隊：Zhenghao Lu、Xiaotian Zhang（共同第一作者）、Songtao Jiang、Siming Fu、Hualiang Wang 與 Zuozhu Liu（Zhejiang University；Wang 與 Liu 為通訊作者），以及 Yiqun Lin（University College London）。[(ref: pdf p.1)](https://arxiv.org/pdf/2611.32344v1) [(ref: abstract)](https://arxiv.org/abs/2611.32344v1)
- 論文：*DiCT: Teaching X-ray Vision-Language Models to Reason via Imagining CT*，arXiv:2611.32344v1（cs.CV；cross-list cs.AI），2026-11-24 提交，目前只有 v1；未註記發表場合；授權為 arXiv 非專屬散布授權。[(ref: abstract)](https://arxiv.org/abs/2611.32344v1)
- 識別碼：arXiv [2611.32344](https://arxiv.org/abs/2611.32344v1)；DOI [10.48550/arXiv.2611.32344](https://doi.org/10.48550/arXiv.2611.32344)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.32344v1)、[PDF v1](https://arxiv.org/pdf/2611.32344v1)。
- 程式與資料：論文附 GitHub 程式庫 [HongYep/DiCT](https://github.com/HongYep/DiCT)，本文未核對其內容；資料為公開的 CT-RATE、DRR-RATE、3D-RAD 與 ReXVQA，其中 3D-RAD 的四選一題與 ReXVQA 的開放式量測題由作者自行改寫建構。[(ref: main abstract)](https://arxiv.org/html/2611.32344v1#abstract1) [(ref: main §4.1)](https://arxiv.org/html/2611.32344v1#S4.SS1)
- 研究性質：完整方法研究，三個訓練階段都在兩個 4B 主幹上實際執行，並與 CT 重建管線、只用胸片訓練的對照比較；所有結果為單次執行，沒有報告種子重複、標準差或信賴區間。開放式問答的評分與 GRPO 的部分 reward 由 LLM judge（Qwen3.8-27B）給出，SFT 的推理文字也由同一個模型合成；論文沒有放射科醫師評估。[(ref: main §4.1)](https://arxiv.org/html/2611.32344v1#S4.SS1) [(ref: main LLM Usage Statement)](https://arxiv.org/html/2611.32344v1#Sx1)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、表 1–3 與附錄表 5–13 為準；論文圖 1、圖 3–5 的病例影像與 token activation map 未轉載，也未引用其中只在圖上出現的數值。

**編輯：** Clare

DiCT 讓只看胸部 X 光的 VLM 在訓練時由看得到配對 CT 的老師模型逐 token 評分，在由 CT 模擬出的 X 光（DRR）上，Hulu-4B 學生的四選一異常辨識準確率 47.53% 超過「先從 X 光重建 CT 再判讀」的管線（45.87%），運算量約為其 1/13；換成 Qwen3-VL-4B 學生則只有 38.36%，仍低於兩條重建管線。[(ref: main Table 1)](https://arxiv.org/html/2611.32344v1#S4.T1)

## 流程

![上方 (a) 標題「DiCT training stages (paper Sec. 3, Table 13)」，由左至右四個圓角方框以箭頭相連：前三個淺藍底、深藍框，依序為「Stage 1 Structured SFT」（回答分成 Thinking with X-ray、Thinking with CT、Answer 三段，輸入只有 X 光（DRR），10,113 examples）、「Stage 2 CT-guided OPD」（凍結的 CT 老師看配對 CT，為學生的 CT 推理與答案 token 評分；X 光 token 以 KL 拉向 SFT 參考，40,938 questions）、「Stage 3 Clinical GRPO」（ReXVQA Measurement 真實 X 光加 3D-RAD 問題（DRR），KL 拉向 OPD checkpoint，5,371 questions）；第四個灰底灰框為「Inference」（X 光輸入、輸出答案，不用 CT、不重建）。左下 (b) 為 3D-RAD 四選一異常辨識準確率的橫條圖，由上而下：深灰「ClinFusion-8B-SFT, CT input (teacher)」56.07；淺灰「TF-PRDiT recon + CT teacher」45.87、「X2CT-GAN recon + CT teacher」42.20、「ClinFusion-8B-SFT, X-ray input」36.56；藍色系「Hulu-4B base」26.17、「Hulu-4B X-ray SFT→GRPO」41.37、「Hulu-4B DiCT」47.53、「Qwen3-VL-4B base」18.09、「Qwen3-VL-4B X-ray SFT→GRPO」34.69、「Qwen3-VL-4B DiCT」38.36，顏色由淺到深代表 base、只用 X 光訓練的對照、DiCT；一條深灰色垂直虛線標在 45.87。右下 (c) 為 ReXVQA 真實胸片異常辨識準確率的分組直條圖，六組依序為 Base、Structured SFT、SFT→GRPO、OPD w/o SFT、OPD checkpoint、DiCT，每組左側橘色為 Qwen3-VL-4B（50.87、45.64、51.13、63.48、66.90、67.74），右側深藍為 Hulu-4B（82.87、78.15、78.86、83.13、83.00、83.65），數值直排標在直條上方，圖例在左上角。](assets/dict-ct-teacher-stages-and-accuracy.png)

*圖：本書庫依論文 [§3](https://arxiv.org/html/2611.32344v1#S3) 與 [表 13](https://arxiv.org/html/2611.32344v1#A4.T13) 的訓練流程（上），以及 [表 1](https://arxiv.org/html/2611.32344v1#S4.T1)（左下）與 [表 6](https://arxiv.org/html/2611.32344v1#A1.T6)（右下）的數值重繪；未轉載論文圖。左下的虛線標出 TF-PRDiT 重建管線的 45.87%，只有 Hulu-4B DiCT 的橫條越過它；右下的 ReXVQA 異常辨識題沒有用於 GRPO 訓練。[(ref: main §4.1)](https://arxiv.org/html/2611.32344v1#S4.SS1)*

## 背景／問題

作者的出發點是：用 X 光診斷常需要推想異常在 3D 空間中的位置以及與周邊結構的關係，而 2D 投影讓這種推理變難；CT 有完整的 3D 資訊，但輻射較高、較不普及。論文以此為動機，沒有另外提出證據說明現有胸片 VLM 的錯誤主要來自缺乏 3D 推理。[(ref: main §1)](https://arxiv.org/html/2611.32344v1#S1)

一條直接的路是先從 X 光重建 CT 體積（例如 X2CT-GAN、TF-PRDiT），再交給 CT VLM 判讀；作者認為這會增加推論運算並帶入重建誤差。DiCT 改走知識蒸餾：訓練時用同一位病人的 CT 當作「特權資訊」，由看得到 CT 的老師引導只看得到 X 光的學生，推論時只需要 X 光。作者指出這與一般 on-policy distillation（OPD）不同的地方在於老師與學生看到的影像不一樣，若對整段回答一律套用老師的評分，學生可能把只在 CT 上看得到的發現寫成自己在 X 光上看到的。[(ref: main §1)](https://arxiv.org/html/2611.32344v1#S1) [(ref: main §2.2)](https://arxiv.org/html/2611.32344v1#S2.SS2) [(ref: main §3.3)](https://arxiv.org/html/2611.32344v1#S3.SS3)

## 方法摘要

- **Instruct the dreamer（structured SFT）** — 把學生的回答固定成三段：「Thinking with X-ray」（從 2D 投影看得到的東西）、「Thinking with CT」（以配對 CT 報告為依據的解剖、空間關係與量測推理）與「Answer」。訓練目標由 Qwen3.8-27B 合成：X 光段由影像與問題生成並經 rejection sampling 篩選，CT 段由 CT 報告與問題生成，學生的視覺輸入只有 X 光。[(ref: main §3.2)](https://arxiv.org/html/2611.32344v1#S3.SS2)
- **Visualize the dream（CT-guided OPD）** — 學生自己生成回答，凍結的 CT 老師在看得到配對 CT 的條件下逐 token 打分，token advantage 是老師與舊學生的 log-probability 差。老師的訊號只作用在「Thinking with CT」與「Answer」段；「Thinking with X-ray」段改以 KL 拉向 SFT 參考模型，段落標題等格式 token 另以重播的 SFT 樣本監督。[(ref: main §3.3)](https://arxiv.org/html/2611.32344v1#S3.SS3)
- **Manifest the dream（clinical GRPO）** — 前兩階段的 X 光都是 DRR；最後用 GRPO 在真實胸片的 ReXVQA 量測題（混入少量 3D-RAD 題）上調整，並以 KL 拉向 OPD checkpoint，避免偏離蒸餾學到的行為。reward 依題型而定：選擇題對錯、量測題以誤差的指數函數、開放式問答由 LLM judge 給 1–10 分再正規化。[(ref: main §3.4)](https://arxiv.org/html/2611.32344v1#S3.SS4)
- **評估** — 在 3D-RAD（DRR 輸入）的五類任務與 ReXVQA（真實胸片）的量測與異常辨識題上，比較三種推論路徑：直接看 CT、先由 X 光重建 CT 再交給同一個 CT 老師、直接看 X 光；另設「只用 X 光訓練」的 X-ray SFT 與 X-ray SFT→GRPO 對照，以及逐階段的消融。[(ref: main §4.1)](https://arxiv.org/html/2611.32344v1#S4.SS1)

## 方法詳解

- **老師與學生** — CT 老師是 ClinFusion-8B 在 30,662 組 CT 問答（附合成推理）上微調一個 epoch 後凍結的 ClinFusion-8B-SFT；學生主幹為 Qwen3-VL-4B 與 Hulu-4B，三階段都只更新語言模型、凍結視覺編碼器與 aligner。[(ref: main §4.1 Training Details)](https://arxiv.org/html/2611.32344v1#S4.SS1.SSS0.Px3)
- **超參數** — structured SFT 10,113 筆、learning rate 1×10⁻⁵；OPD 40,938 題、1×10⁻⁶、temperature 0.9、λ_T 0.5、λ_ref 0.02、λ_fmt 0.1、ε 0.2；GRPO 每題取樣 8 個回答、λ_KL 0.02。三個階段各一個 epoch，使用四張 NVIDIA H20。[(ref: main §4.1 Training Details)](https://arxiv.org/html/2611.32344v1#S4.SS1.SSS0.Px3) [(ref: main Table 13)](https://arxiv.org/html/2611.32344v1#A4.T13)
- **老師看到的內容** — 評分時只把學生取樣出的 CT 推理段與答案接在老師的題目提示後面（老師看配對 CT 體積）；學生則在含 X 光推理段的完整上下文中為同一段內容計分。回答缺少可辨識的 CT 推理段或完整答案時，不施加老師的損失。[(ref: main Appendix D.2)](https://arxiv.org/html/2611.32344v1#A4.SS2)
- **3D-RAD 的改寫** — 原始的是非題中 82.0% 答案為陰性，作者把它改成四選一異常辨識：每個陽性發現出一題，三個干擾選項取自同一體積中標為陰性的發現，正確答案在 A–D 平均分布，共 4,223 題、1,134 個體積。主測試集 11,788 題分屬五類任務；需要前次影像的時序題被排除。訓練與測試集只核對了體積名稱與影像路徑不重疊，作者說明沒有獨立的病人識別碼可供檢查。[(ref: main Appendix C.1)](https://arxiv.org/html/2611.32344v1#A3.SS1)
- **ReXVQA 的改寫** — 量測題拿掉選項改成開放式數值題，以原正確選項換算成公釐作參考值；244 題測試題中 223 題問的是氣管內管等管路尖端到隆凸的距離。異常辨識題從官方測試集選出 1,547 題四選一，保留原措辭、選項順序與正確答案（1,471 個 study、1,306 位病人），與 GRPO 用的量測訓練題不共用病人或 study。[(ref: main Appendix C.2)](https://arxiv.org/html/2611.32344v1#A3.SS2)
- **評分** — 選擇題以同一個 parser 抽出框選答案，抽不到算錯；3D-RAD 的開放式觀察與異常描述題由 Qwen3.8-27B 依 1–10 分評比，量測題報告 MAE 與可解析比例（Matched／Valid）。運算量以每題平均 FLOPs 估算，重建成本由同一體積的題目分攤，不含 DRR 合成、前處理與評分 judge。[(ref: main Appendix E.1)](https://arxiv.org/html/2611.32344v1#A5.SS1) [(ref: main Appendix E.2)](https://arxiv.org/html/2611.32344v1#A5.SS2)
- **論文未交代** — 沒有報告種子重複、標準差或信賴區間，也沒有任何統計檢定；論文沒有限制章節；X 光段與 CT 段的推理文字由 LLM 合成，論文沒有檢查「Thinking with CT」段的內容是否與配對 CT 一致，也沒有量測學生是否把 CT 才看得到的發現寫進 X 光段；3D-RAD 開放式題與部分 GRPO reward 依賴 LLM judge，未與人工評分對照；「CT-informed 3D 推理」的證據只有準確率變化與三個定性例子的 token activation map；程式庫內容本文未核對。[(ref: main §4.1)](https://arxiv.org/html/2611.32344v1#S4.SS1) [(ref: main §4.4)](https://arxiv.org/html/2611.32344v1#S4.SS4) [(ref: main LLM Usage Statement)](https://arxiv.org/html/2611.32344v1#Sx1)

## 資料與實驗

### 資料

| 資料／階段 | 影像 | 規模 | 用途 |
|---|---|---|---|
| CT 老師 SFT | CT（CT-RATE） | 30,662 組問答 | 微調後凍結的老師 |
| Structured SFT | DRR（DRR-RATE，正面＋側面） | 10,113 筆 | 學生第一階段 |
| CT-guided OPD | DRR＋配對 CT | 40,938 題、12,896 個 CT 體積 | 學生第二階段 |
| Clinical GRPO | 真實胸片＋DRR | 4,027 題 ReXVQA 量測＋1,344 題 3D-RAD | 學生第三階段 |
| 3D-RAD 測試 | DRR（老師看 CT） | 11,788 題：觀察 1,024、異常偵測 2,666、量測 1,002、四選一異常辨識 4,223、縱向診斷 2,873 | 主要評估 |
| ReXVQA 量測測試 | 真實胸片 | 244 題（223 題為管路尖端到隆凸距離） | 真實影像量測 |
| ReXVQA 異常辨識測試 | 真實胸片 | 1,547 題、1,306 位病人 | 未用於 GRPO 的保留評估 |

[(ref: main Table 13)](https://arxiv.org/html/2611.32344v1#A4.T13) [(ref: main Appendix C.1)](https://arxiv.org/html/2611.32344v1#A3.SS1) [(ref: main Appendix C.2)](https://arxiv.org/html/2611.32344v1#A3.SS2) [(ref: main Appendix D.1)](https://arxiv.org/html/2611.32344v1#A4.SS1)

### 實驗：3D-RAD（論文表 1，節錄）

| Method | Abnormality Identification Acc. (%) | Longitudinal Diagnosis Acc. (%) | Obs. Judge (1–10) | Abn. Judge (1–10) | Measurement MAE (mm) | TFLOPs |
|---|---|---|---|---|---|---|
| ClinFusion-8B-SFT（CT 輸入，老師） | 56.07 | 79.74 | 5.32 | 4.87 | 8.50 | 22.17 |
| TF-PRDiT 重建 + ClinFusion-8B-SFT | 45.87 | 78.28 | 5.00 | 4.73 | 8.92 | 132.66 |
| X2CT-GAN 重建 + ClinFusion-8B-SFT | 42.20 | 77.97 | 4.96 | 4.56 | 9.48 | 22.69 |
| ClinFusion-8B-SFT（X 光輸入） | 36.56 | 79.50 | 4.88 | 4.40 | 9.87 | 23.31 |
| Hulu-4B | 26.17 | 64.46 | 4.70 | 4.08 | 12.40 | 7.38 |
| Hulu-4B（X-ray SFT→GRPO） | 41.37 | 79.50 | 4.57 | 4.08 | 14.22 | 7.24 |
| Hulu-4B-DiCT | 47.53 | 79.60 | 4.97 | 4.58 | 9.86 | 10.39 |
| Qwen3-VL-4B | 18.09 | 65.37 | 3.53 | 3.13 | 15.77 | 11.75 |
| Qwen3-VL-4B（X-ray SFT→GRPO） | 34.69 | 80.06 | 4.41 | 4.03 | 12.22 | 7.01 |
| Qwen3-VL-4B-DiCT | 38.36 | 78.70 | 4.60 | 4.32 | 10.99 | 10.44 |

Obs.／Abn. 為 LLM judge 對觀察與異常描述題的 1–10 分；MAE 只計可解析的長度；TFLOPs 含重建。論文表 1 另列 OmniCT-3B／7B（CT 輸入）、HealthGPT-Pro-4B 與量測 Matched 欄，本表未節錄。[(ref: main Table 1)](https://arxiv.org/html/2611.32344v1#S4.T1)

### 實驗：ReXVQA 真實胸片（論文表 2、表 5、表 6 合併）

| Backbone／Stage | Measurement Valid (%) | Measurement MAE (mm) | Abnormality Identification Acc. (%) |
|---|---|---|---|
| ClinFusion-8B-SFT（外部參考） | 96.3 | 14.54 | 82.03 |
| Qwen3-VL-4B base | 59.4 | 24.93 | 50.87 |
| Qwen3-VL-4B structured SFT | 100.0 | 20.59 | 45.64 |
| Qwen3-VL-4B SFT→GRPO（無 OPD） | 100.0 | 14.03 | 51.13 |
| Qwen3-VL-4B OPD w/o SFT | 100.0 | 20.57 | 63.48 |
| Qwen3-VL-4B OPD checkpoint | 100.0 | 18.44 | 66.90 |
| Qwen3-VL-4B DiCT | 100.0 | 14.12 | 67.74 |
| Qwen3-VL-4B X-ray SFT→GRPO | 100.0 | 14.35 | 35.42 |
| Hulu-4B base | 100.0 | 15.60 | 82.87 |
| Hulu-4B structured SFT | 100.0 | 14.45 | 78.15 |
| Hulu-4B SFT→GRPO（無 OPD） | 100.0 | 13.54 | 78.86 |
| Hulu-4B OPD w/o SFT | 100.0 | 20.52 | 83.13 |
| Hulu-4B OPD checkpoint | 100.0 | 16.66 | 83.00 |
| Hulu-4B DiCT | 100.0 | 13.78 | 83.65 |
| Hulu-4B X-ray SFT→GRPO | 100.0 | 13.43 | 75.11 |

Valid 為 244 題中有可用預測的比例，MAE 只在有效預測上計算；異常辨識為 1,547 題。「SFT→GRPO（無 OPD）」是 structured SFT 後直接 GRPO；「X-ray SFT→GRPO」是不含 CT 推理段的純 X 光對照。[(ref: main Table 2)](https://arxiv.org/html/2611.32344v1#S4.T2) [(ref: main Table 5)](https://arxiv.org/html/2611.32344v1#A1.T5) [(ref: main Table 6)](https://arxiv.org/html/2611.32344v1#A1.T6) [(ref: main Table 8)](https://arxiv.org/html/2611.32344v1#A1.T8)

### 實驗：3D-RAD 原始是非題（論文表 9，節錄）

| Method | Acc. (%) | Balanced Acc. (%) |
|---|---|---|
| ClinFusion-8B-SFT（CT 輸入，老師） | 81.16 | 64.86 |
| TF-PRDiT 重建 + ClinFusion-8B-SFT | 72.21 | 61.01 |
| Hulu-4B | 80.97 | 51.53 |
| Hulu-4B-DiCT | 78.07 | 61.86 |
| Qwen3-VL-4B | 78.70 | 49.78 |
| Qwen3-VL-4B-DiCT | 80.73 | 53.40 |

23,472 個答案中 19,249 個為陰性，全部答「沒有」即得 82.0% accuracy、50.0% balanced accuracy。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.32344v1#A2.SS1) [(ref: main Table 9)](https://arxiv.org/html/2611.32344v1#A2.T9)

## 結果

- **DRR 上勝過純 X 光訓練** — 與 X-ray SFT→GRPO 相比，DiCT 把 3D-RAD 四選一異常辨識從 34.69% 提高到 38.36%（Qwen3-VL-4B）、從 41.37% 提高到 47.53%（Hulu-4B），開放式問答的 judge 分數與量測 MAE 也較好，縱向診斷大致持平。[(ref: main §4.2)](https://arxiv.org/html/2611.32344v1#S4.SS2) [(ref: main Table 1)](https://arxiv.org/html/2611.32344v1#S4.T1)
- **與重建管線比較只對一個主幹成立** — Hulu-4B-DiCT 的 47.53% 比 TF-PRDiT 重建管線高 1.66 點，每題運算量 10.39 對 132.66 TFLOPs（約 1/12.8），也在準確率與運算量上都勝過 X2CT-GAN 管線（42.20%、22.69 TFLOPs）。Qwen3-VL-4B-DiCT 的 38.36% 則低於兩條重建管線。兩條重建管線的量測 MAE（8.92、9.48 mm）都低於 DiCT，TF-PRDiT 管線的開放式題 judge 分數也較高；作者同樣說明重建方法在部分量測與開放式題上仍較強。[(ref: main §4.2)](https://arxiv.org/html/2611.32344v1#S4.SS2) [(ref: main Table 1)](https://arxiv.org/html/2611.32344v1#S4.T1)
- **OPD 是主要增益來源** — 在 3D-RAD 上，OPD 把異常辨識從 structured SFT 後的 31.54% 提高到 40.07%（Qwen）、37.96% 到 46.18%（Hulu）。Hulu 的消融中，structured SFT 加 OPD（46.18%）高於只做 OPD（40.94%）與 SFT 後直接 GRPO（38.34%）。[(ref: main §4.2)](https://arxiv.org/html/2611.32344v1#S4.SS2) [(ref: main Table 3)](https://arxiv.org/html/2611.32344v1#S4.T3)
- **真實胸片：兩個主幹差很多** — ReXVQA 異常辨識上，Qwen3-VL-4B 從 base 的 50.87% 升到 DiCT 的 67.74%；Hulu-4B 的 base 已有 82.87%，DiCT 為 83.65%，只多 0.78 點。OPD checkpoint 尚未用任何真實胸片訓練就已達 66.90%／83.00%，作者以此說明 DRR 上學到的能力可轉移到真實影像。[(ref: main §4.3)](https://arxiv.org/html/2611.32344v1#S4.SS3) [(ref: main Table 6)](https://arxiv.org/html/2611.32344v1#A1.T6)
- **純 X 光對照在真實胸片上反而退步** — X-ray SFT→GRPO 讓 Qwen3-VL-4B 的 ReXVQA 異常辨識從 50.87% 降到 35.42%、Hulu-4B 從 82.87% 降到 75.11%；structured SFT 也讓兩者下降（45.64%、78.15%）。DiCT 相對這個對照的優勢，有一部分是對照組本身退步。另外，不經 structured SFT、對整段回答做標準 OPD 的「OPD w/o SFT」已達 63.48%／83.13%，與 DiCT 相差不到 4.3 點。[(ref: main Table 6)](https://arxiv.org/html/2611.32344v1#A1.T6) [(ref: main Table 8)](https://arxiv.org/html/2611.32344v1#A1.T8)
- **量測沒有贏過沒有 OPD 的版本** — ReXVQA 量測 MAE，DiCT 為 14.12／13.78 mm，SFT 後直接 GRPO 為 14.03／13.54 mm，純 X 光對照為 14.35／13.43 mm；作者寫作「具競爭力，但未一致勝出」。[(ref: main §4.3)](https://arxiv.org/html/2611.32344v1#S4.SS3) [(ref: main Table 5)](https://arxiv.org/html/2611.32344v1#A1.T5)
- **原始是非題上陽性仍大多漏掉** — 3D-RAD 原始是非題中全答陰性即有 82.0% accuracy；Qwen3-VL-4B-DiCT 的 80.73% 低於這個數字，4,223 個陽性只答對 453 個（約 10.7%），陰性答對 18,495／19,249。Hulu-4B-DiCT 的 balanced accuracy 61.86%，略低於 CT 老師的 64.86%。[(ref: main Appendix B.2)](https://arxiv.org/html/2611.32344v1#A2.SS2) [(ref: main Table 9)](https://arxiv.org/html/2611.32344v1#A2.T9)
- **推論成本高於純 X 光模型** — DiCT 每題約 10.4 TFLOPs，高於同主幹的 X-ray SFT→GRPO（Hulu 7.24、Qwen 7.01），論文沒有分析差距來源；12.77 倍的節省是相對 TF-PRDiT 重建管線而言。[(ref: main Table 1)](https://arxiv.org/html/2611.32344v1#S4.T1)

## 限制

- **沒有不確定性估計** — 所有數字都是單次執行，DiCT 與對照的差距（例如 Hulu-4B 在 ReXVQA 的 0.78 點、量測 MAE 的 0.1–0.4 mm）是否超出隨機波動無從判斷。[(ref: main §4.1)](https://arxiv.org/html/2611.32344v1#S4.SS1)
- **主要評估在模擬影像上** — 3D-RAD 的「X 光」是由 CT 算出的 DRR，與老師的 CT 來自同一體積；與重建管線的比較只在 DRR 上進行。真實胸片的評估只有 ReXVQA，而其量測題幾乎都是管路尖端到隆凸的距離。[(ref: main Appendix C.1)](https://arxiv.org/html/2611.32344v1#A3.SS1) [(ref: main Appendix C.2)](https://arxiv.org/html/2611.32344v1#A3.SS2)
- **基準由作者改寫，切分只核對到體積層級** — 四選一題與開放式量測題由作者建構；3D-RAD 訓練與測試只確認體積名稱與路徑不重疊，作者表明沒有病人識別碼可檢查。[(ref: main Appendix C.1)](https://arxiv.org/html/2611.32344v1#A3.SS1)
- **合成監督與 LLM 評分** — SFT 推理文字、開放式題評分與部分 reward 都來自 Qwen3.8-27B，論文沒有與人工評分對照，也沒有臨床讀者研究。[(ref: main LLM Usage Statement)](https://arxiv.org/html/2611.32344v1#Sx1)
- **「3D 推理」未直接驗證** — 論文以準確率與三個定性例子支持「學生學會以想像 CT 推理」，沒有檢查 CT 推理段內容的正確性或它與答案的因果關係。論文本身沒有限制章節，以上為本書庫依全文整理。[(ref: main §4.4)](https://arxiv.org/html/2611.32344v1#S4.SS4)

## 與書庫其他文章的關係

DeCAD 在 CT-RATE 上量到 HuluMed-7B 等醫療 VLM 逐病問答遠勝直接寫報告，DiCT 則用 CT-RATE 體積算出的 DRR 與 Hulu-4B，把看 CT 的老師的判讀蒸餾給只看胸片的學生；DiCT 的評估只有問答與量測，沒有報告生成: [CT 報告模型問得出卻寫不出：先列發現再寫，F1 15.9→39.0](2026-11-26-decad-ct-diagnosis-to-report-gap.md)

胸片 VLM 稽核發現整體準確率會遮住某些徵象一律答「沒有」；DiCT 附錄的 3D-RAD 是非題也是如此，Qwen3-VL-4B-DiCT 的準確率接近全答陰性，4,223 個陽性只答對 453 個: [胸片 VLM 稽核：兩個模型對 432 例氣胸全答「沒有」](2026-11-16-pneumothorax-silent-failure-medical-vlm.md)

## 實務的啟發

- **可借用的訓練設計** — 有成對 CT 與胸片時，讓看得到 CT 的模型只在「推理與答案」段給學生 token 級訊號、X 光描述段另外約束，是一種不需推論時重建 CT 的做法；但本研究中它對已經很強的主幹（Hulu-4B 在真實胸片 82.87%）幾乎沒有加分，要在自己的主幹與資料上先驗證。[(ref: main §3.3)](https://arxiv.org/html/2611.32344v1#S3.SS3) [(ref: main Table 6)](https://arxiv.org/html/2611.32344v1#A1.T6)
- **對照組要檢查是否退步** — 本研究的純 X 光 SFT→GRPO 對照在真實胸片異常辨識上比未訓練的 base 低 7.8–15.5 點；評估新方法時，除了與對照比，也要與未微調的 base 比，否則對照退步會被讀成方法增益。[(ref: main Table 8)](https://arxiv.org/html/2611.32344v1#A1.T8)
- **四選一與是非題要一起看** — 同一批 3D-RAD 標籤，改成四選一後 DiCT 有明顯增益，回到原始是非題則陽性召回仍約一成、準確率不如全答陰性；拿這類模型做篩檢式「有沒有異常」判斷前，需要看陽性召回與 balanced accuracy，而不是選擇題準確率。[(ref: main Table 9)](https://arxiv.org/html/2611.32344v1#A2.T9)
- **待驗證的警訊** — DRR 上的增益、LLM judge 給的分數與單次執行的小差距，都還需要在真實胸片、人工評分與多種子重複下確認；「學生在想像 CT」目前只是作者對準確率變化的解讀。[(ref: main §4.4)](https://arxiv.org/html/2611.32344v1#S4.SS4)

## References

- `main` — Zhenghao Lu, Xiaotian Zhang, Songtao Jiang, Yiqun Lin, Siming Fu, Hualiang Wang, Zuozhu Liu. *DiCT: Teaching X-ray Vision-Language Models to Reason via Imagining CT*. arXiv:2611.32344v1, 2026. HTML：https://arxiv.org/html/2611.32344v1 ；用到的深鏈：[abstract](https://arxiv.org/html/2611.32344v1#abstract1)、[§1](https://arxiv.org/html/2611.32344v1#S1)、[§2.2](https://arxiv.org/html/2611.32344v1#S2.SS2)、[§3](https://arxiv.org/html/2611.32344v1#S3)、[§3.2](https://arxiv.org/html/2611.32344v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.32344v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.32344v1#S3.SS4)、[§4.1](https://arxiv.org/html/2611.32344v1#S4.SS1)、[§4.1 Training Details](https://arxiv.org/html/2611.32344v1#S4.SS1.SSS0.Px3)、[§4.2](https://arxiv.org/html/2611.32344v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.32344v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.32344v1#S4.SS4)、[Table 1](https://arxiv.org/html/2611.32344v1#S4.T1)、[Table 2](https://arxiv.org/html/2611.32344v1#S4.T2)、[Table 3](https://arxiv.org/html/2611.32344v1#S4.T3)、[Table 5](https://arxiv.org/html/2611.32344v1#A1.T5)、[Table 6](https://arxiv.org/html/2611.32344v1#A1.T6)、[Table 8](https://arxiv.org/html/2611.32344v1#A1.T8)、[Appendix B.1](https://arxiv.org/html/2611.32344v1#A2.SS1)、[Appendix B.2](https://arxiv.org/html/2611.32344v1#A2.SS2)、[Table 9](https://arxiv.org/html/2611.32344v1#A2.T9)、[Appendix C.1](https://arxiv.org/html/2611.32344v1#A3.SS1)、[Appendix C.2](https://arxiv.org/html/2611.32344v1#A3.SS2)、[Appendix D.1](https://arxiv.org/html/2611.32344v1#A4.SS1)、[Appendix D.2](https://arxiv.org/html/2611.32344v1#A4.SS2)、[Table 13](https://arxiv.org/html/2611.32344v1#A4.T13)、[Appendix E.1](https://arxiv.org/html/2611.32344v1#A5.SS1)、[Appendix E.2](https://arxiv.org/html/2611.32344v1#A5.SS2)、[LLM Usage Statement](https://arxiv.org/html/2611.32344v1#Sx1)
- `abstract` — arXiv abstract page, 2611.32344v1：https://arxiv.org/abs/2611.32344v1 （DOI：https://doi.org/10.48550/arXiv.2611.32344）
- `pdf` — PDF v1（作者單位取自第 1 頁）：https://arxiv.org/pdf/2611.32344v1

[Home](../) · [AI Papers](./)
