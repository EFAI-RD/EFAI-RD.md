---
parent: AI Papers
nav_exclude: true
title: "低劑量 CT 品質評分：MLLM 讀量測值追平競賽冠軍，卻高估過度平滑影像"
catalog_id: "arxiv:2611.08754"
editors:
  - "Clare"
refs:
  main:
    title: "Measurement-Aware Multimodal LLM for No-Reference Low-Dose CT Quality Assessment"
    url: "https://arxiv.org/abs/2611.08754"
  html:
    title: "Measurement-Aware Multimodal LLM for No-Reference Low-Dose CT Quality Assessment (arXiv HTML v1)"
    url: "https://arxiv.org/html/2611.08754v1"
  code:
    title: "agentic-ct-iqa (GitHub; URL listed in paper, not yet publicly viewable)"
    url: "https://github.com/itu-biai/agentic-ct-iqa"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 低劑量 CT 品質評分：MLLM 讀量測值追平競賽冠軍，卻高估過度平滑影像

## 來源

- 團隊：Istanbul Technical University 電子與通訊工程系、Istanbul University 電機電子工程系；作者 Kerem Basim、Tolga Demiroglu（共同第一作者）、Mehmet Ozan Unal、Metin Ertas、Isa Yildirim。[(ref: main author block)](https://arxiv.org/html/2611.08754v1)
- 論文：*Measurement-Aware Multimodal LLM for No-Reference Low-Dose CT Quality Assessment*，arXiv 預印本，2026-11-05 提交（v1），分類 eess.IV（交叉列 cs.CV）；arXiv 註記為投稿 IEEE ISBI 2027，尚非已接受版本。[(ref: main)](https://arxiv.org/abs/2611.08754)
- 識別碼：arXiv [2611.08754](https://arxiv.org/abs/2611.08754)；DOI [10.48550/arXiv.2611.08754](https://doi.org/10.48550/arXiv.2611.08754)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.08754v1)（5 頁短文，2 張圖、3 張表）。
- 程式：論文寫明程式碼公開於 [GitHub](https://github.com/itu-biai/agentic-ct-iqa)，但本文發布時該網址尚無可公開瀏覽的內容，因此本文未核對程式實作。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- 研究性質：完整實作的方法論文，模型實際訓練並在公開 benchmark 的官方測試集上評估，主表與消融表附配對 bootstrap 95% 信賴區間、Holm 校正與三個訓練 seed 的標準差；不是 pilot，但只用一個 benchmark、一個 LLM，訓練資料來自 7 位病人。[(ref: main Table I)](https://arxiv.org/html/2611.08754v1#S2.T1) [(ref: main §IV)](https://arxiv.org/html/2611.08754v1#S4)
- 證據邊界：本文數值以 arXiv v1 的 Table I–III 與正文為準；Fig. 2 的長條與部分相依曲線只引用正文明寫的數字。

**編輯：** Clare

作者把六個傳統 CT 影像量測值換成百分位、寫成文字餵給微調過的 Qwen3.8-27B，讓它預測放射科醫師會給低劑量 CT 切片的品質分數：在 LDCT-IQA 2023 測試集上 Overall 2.735，與重新訓練的競賽冠軍持平；但同一組量測文字讓模型在排序去噪結果時偏好過度平滑的影像，平均 Kendall τ 只有 0.140（MedSigLIP-FiLM 為 0.480）。[(ref: main Abstract)](https://arxiv.org/abs/2611.08754) [(ref: main Table I)](https://arxiv.org/html/2611.08754v1#S2.T1)

## 流程

![左右兩部分的圖。左側四個淺藍底、深藍實線圓角框由上而下排列，以三支向下箭頭相連：「1. Input：Low-dose abdominal CT slice (LDCT-IQA 2023: 1000 train / 300 test slices)」、「2. Six measurements -> percentiles：noise: residual noise, noise score; sharpness: structure, gradient deviation; HF residual; streak anisotropy」、「3. Qwen3.8-27B + measurement text：Phase 1: tune vision encoder (10 epochs); Phase 2: merger + LoRA r=16 + linear head (3 epochs); 5-fold ensemble」、「4. Output：Predicted radiologist MOS (0-4) scored by Overall = PLCC + SROCC + KROCC」；左下角小字「Redrawn by EFAI-RD from Basim K, et al. arXiv:2611.08754v1 (Sec. II-III; Fig. 1; Tables I-II)」。右側兩個並排的水平長條圖共用同一組六列模型名稱（由上而下：Qwen3.8-27B zero-shot agent、Q-Align、ResNeXt-50、Challenge winner、MedSigLIP-FiLM、Ours: Qwen3.8-27B + meas.），前五列灰色、最後一列橘色。左長條圖標題「LDCT-IQA 2023 test (300 slices)」，橫軸「Overall (max 3)」，數值 2.180、2.557、2.683、2.735、2.713、2.735；右長條圖標題「Ranking 12 reconstructions (192 slices)」，橫軸「mean Kendall tau vs. SSIM」，數值 n/a、0.392、0.029、0.436、0.480、0.140。底部小字「Source: Table I. Grey = comparison models; orange = proposed model. Higher is better in both panels.」](assets/ldct-iqa-measurement-aware-mllm.png)

*圖：本書庫依論文 §II–§III 與 Fig. 1 重繪的模型流程（左），以及 [Table I](https://arxiv.org/html/2611.08754v1#S2.T1) 中六個模型在官方測試集的 Overall（中）與去噪影像排序的平均 Kendall τ（右）。零樣本代理沒有去噪排序的數值；LMM-IQA 與 MedGemma 的引用值未畫入。*

## 背景／問題

低劑量 CT 降低輻射劑量，但會增加雜訊與條紋偽影；深度學習去噪器可以去掉它們，也可能把細微解剖結構抹平。比較劑量協定與去噪器因此需要和放射科醫師判斷一致的影像品質評估（image quality assessment，IQA），而臨床上沒有全劑量參考影像，所以必須是 no-reference：只看一張切片，預測醫師給分的平均（mean opinion score，MOS）。作者引用 LDCT-IQA 2023 挑戰賽的論文說明人工評分難以大規模進行。[(ref: main §I)](https://arxiv.org/html/2611.08754v1#S1)

在這個 benchmark 上，訓練過的 CNN／transformer 網路與醫療基礎模型（如 MedSigLIP-FiLM）已和 MOS 高度相關，但只輸出一個分數。多模態大型語言模型（multimodal large language model，MLLM）可以用文字說明分數，但作者整理的既有結果顯示，只靠 prompt 的 MLLM 在 CT 上明顯落後訓練過的網路。[(ref: main §I)](https://arxiv.org/html/2611.08754v1#S1) 「MLLM 能解釋分數」是作者的動機；本篇自己的分析反而顯示代理的理由並不可靠地對應分數（見〈結果〉）。

作者要回答兩件事：把傳統的物理量測寫成文字交給 MLLM 並加以微調，準確度能不能追上訓練過的 CT IQA 網路；以及模型是否真的在用這些量測。另外，作者把評估協定先固定下來，分開報告四捨五入到 MOS 格點與在測試集上挑設定這兩種會灌高分數的做法。[(ref: main §I)](https://arxiv.org/html/2611.08754v1#S1)

## 方法摘要

- **六個量測值** — 雜訊兩個（median filter 殘差的標準差、noise score）、銳利度兩個（Sobel 梯度第 95 百分位的 structure、gradient deviation）、細紋理一個（HF residual）、條紋一個（streak anisotropy）；每個值換算成在 1000 張訓練切片中的百分位，這一步不使用 MOS。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **量測寫成文字** — 六個兩位數百分位填進固定 prompt，接在影像 token 後面一起交給 Qwen3.8-27B。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2) [(ref: main Fig. 1)](https://arxiv.org/html/2611.08754v1#S1.F1)
- **兩階段微調** — Phase 1 先把通用視覺編碼器調到 CT；Phase 2 凍結編碼器，訓練 merger、LoRA 與最後一個 token 上的線性頭，以 MSE 回歸 MOS；測試時平均五折模型。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **零樣本代理對照** — 同一個 Qwen3.8-27B 不訓練，以 file-read 呼叫讀取預先算好的量測檔與七種視覺視圖，寫出分數與理由。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **用了什麼的檢查** — 消融、測試時打亂量測值、逐組打亂、部分相依分析，以及代理理由引用哪組量測、方向是否與實際百分位一致。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)

## 方法詳解

- **百分位的方向** — 百分位定義為「訓練切片中量測值比它大的比例」，因此對雜訊量測來說，百分位越高代表雜訊比一般少。noise score 是 residual noise、gradient deviation、HF residual 三個百分位的平均。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **Phase 1** — 在視覺編碼器的 pooled token 上接一個小回歸頭，加上六個百分位，以標準化 MOS 的 MSE 訓練 10 個 epoch。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **Phase 2** — 編碼器凍結；更新把影像 token 投影進語言模型的 merger、語言模型全部 64 層所有投影上的 rank 16 LoRA（bf16），以及最後一個 prompt token 隱藏狀態上的線性頭 q̂ = wᵀh_T，MSE 訓練 3 個 epoch。輸出是迴歸分數，不是生成的文字。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **交叉驗證** — 1000 張訓練切片約來自 100 張基底切片、各自加上多個降質層級；五折依基底切片分組。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- **指標** — Overall = |PLCC| + |SROCC| + |KROCC|（KROCC 用 Kendall τ_b，最大值 3），即挑戰賽的分數。MOS 是醫師分數的平均，落在 0.2 的格點上；預測值四捨五入到格點會製造同分對、改變 KROCC，因此每個自己跑的模型都同時報兩種 Overall。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **統計** — 信賴區間來自對 300 張測試切片的配對 bootstrap（2000 次），每張表內做 Holm 校正；所有比較與檢定在第一次碰測試集之前就固定。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- **去噪排序 τ̄** — 去噪影像沒有 MOS，作者改量模型能否依保真度排序同一切片的 12 個重建（一個低劑量雜訊版加 11 個去噪器輸出，例如 BM3D、RED-CNN、DnCNN）：預測品質與「對全劑量參考的 SSIM」之間的 Kendall τ，對切片取平均。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2) [(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- **基線重建方式** — MedSigLIP-FiLM 以原作者程式與 checkpoint、三個 seed 訓練；挑戰賽冠軍的 transformer 分類器與 Q-Align 依各自做法在同樣的折上重新訓練；另加 ResNeXt-50 作為標準 CNN。LMM-IQA（o3）與 MedGemma-4B QLoRA 是引用各自論文的數字，後者用的是自己的資料切分。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3) [(ref: main Table I)](https://arxiv.org/html/2611.08754v1#S2.T1)
- **論文未交代** — 完整 prompt 全文：正文只引用 prompt 的片段；零樣本代理的 prompt 與七種視覺視圖的具體設定也沒有列出。
- **論文未交代** — Phase 1／Phase 2 的學習率、batch size、優化器與運算資源。
- **論文未交代** — 每張切片的 MOS 由幾位放射科醫師評分；本文只寫 MOS 來自醫師評分、範圍 0（最差）到 4（最好），細節引用挑戰賽論文。

## 資料與實驗

### 資料

| 資料 | 用途 | 規模 | 標註 |
|---|---|---|---|
| LDCT-IQA 2023 訓練集 | 訓練、五折交叉驗證、百分位參考分布 | 1000 張腹部切片，來自 7 位病人（約 100 張基底切片 × 多個降質層級） | 放射科醫師 MOS，0–4，0.2 格點 |
| LDCT-IQA 2023 測試集 | 主評估（官方測試集） | 300 張腹部切片，來自 5 位病人 | 同上 |
| DeepLesion 衍生去噪集 | 只用來算去噪排序 τ̄ | 192 張軟組織切片，來自 30 位病人；每張有全劑量參考與 12 個重建 | 無 MOS；以對全劑量參考的 SSIM 作排序依據 |

[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3) [(ref: main §I)](https://arxiv.org/html/2611.08754v1#S1)

### 實驗：主表（Table I，節錄）

| Method | PLCC ↑ | SROCC ↑ | KROCC ↑ | Overall ↑ | Overall, grid ↑ | Δ vs MedSigLIP-FiLM [95% CI] | τ̄ ↑ |
|---|---|---|---|---|---|---|---|
| LMM-IQA, o3（引用） | .8122 | .8180 | .6347 | 2.2649 | - | - | - |
| Qwen3.8-27B agent（Z3） | .7825 | .7859 | .6117 | 2.1802 | 2.1919 | −0.533 [−0.668, −0.415] | - |
| MedGemma-4B QLoRA, own split（引用） | .791 | .795 | - | - | - | - | - |
| Q-Align | .9095 | .9055 | .7422 | 2.5572† | 2.5779 | −0.156 [−0.210, −0.109] | 0.392 |
| ResNeXt-50 | .9426 | .9410 | .7989 | 2.6825† | 2.6968 | −0.031 [−0.049, −0.013] | 0.029 |
| Challenge winner | .9534 | .9543 | .8275 | 2.7352 | 2.7363 | +0.022 [−0.002, +0.045] | 0.436 |
| MedSigLIP-FiLM | .9490 ± .0103 | .9491 ± .0051 | .8152 ± .0098 | 2.7132 ± .0251 | 2.7327 | reference | 0.480 |
| Ours: Qwen3.8-27B + meas. | .9543 ± .0015 | .9537 ± .0015 | .8265 ± .0031 | 2.7345 ± .0060 | 2.7581 | +0.021 [+0.002, +0.041] | 0.140 |

± 為三個訓練 seed 的標準差；† 為對本文模型 Holm 校正後 p < 0.05。表下另列在測試集上挑設定或已發表的分數（不可與上表比較）：ClinReadNet 2.7690、MedSigLIP-FiLM test-selected 2.7694、Ours test-selected 2.7767（皆為 grid）。[(ref: main Table I)](https://arxiv.org/html/2611.08754v1#S2.T1)

### 實驗：消融（Table II）

| | Configuration | Overall ↑ | Δ vs 上一列 [95% CI] | τ̄ ↑ |
|---|---|---|---|---|
| Z1 | Zero-shot, image only | 1.370 | - | - |
| Z2 | + meas. as text | 2.157 | +0.787 [+0.545, +1.028]† | - |
| Z3 | + agent loop (files, views) | 2.180 | +0.023 [−0.125, +0.173] | - |
| Z4 | + 80 examples with MOS | 2.483 | +0.302 [+0.179, +0.436]† | - |
| T0 | Meas. only (boosting) | 2.611 | - | 0.056 |
| T1 | Frozen enc. + ridge | 2.569 | - | 0.442 |
| T2 | Tuned enc. | 2.704 | +0.135 [+0.098, +0.174]† | 0.213 |
| T3 | + meas. in head (Phase 1) | 2.719 | +0.015 [+0.008, +0.022]† | 0.150 |
| T4 | Frozen enc. + LLM + meas. | 2.711 | - | 0.149 |
| T5 | Tuned enc. + LLM, no meas. | 2.719 | - | 0.250 |
| T6 | Tuned enc. + LLM + meas.（本文模型） | 2.7345 | +0.015 [+0.005, +0.025]† | 0.140 |
| T7 | Ours, meas. shuffled at test | 2.687 | −0.048 [−0.070, −0.027]† | 0.222 |

[(ref: main Table II)](https://arxiv.org/html/2611.08754v1#S3.T2)

## 結果

- **與最強網路持平，但差距不顯著** — 本文模型 Overall 2.735，比 MedSigLIP-FiLM 高 0.021（95% CI +0.002 到 +0.041），Holm 校正後 p = 0.11；三種 seed 配對下都領先。與重新訓練的競賽冠軍差 −0.001（−0.018 到 +0.016）；Q-Align 與 ResNeXt-50 顯著較低。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3) [(ref: main Table I)](https://arxiv.org/html/2611.08754v1#S2.T1)
- **評估協定的影響比模型差距大** — 四捨五入到 0.2 格點讓本文模型多 0.024、冠軍只多 0.001（冠軍的 21 類輸出本來就在格點上）；這個效應大於本文模型與 MedSigLIP-FiLM 之間的 0.021。在測試集上挑設定，MedSigLIP-FiLM 可升到 2.769，等於另一篇論文報告的 ClinReadNet 分數。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- **去噪排序反轉** — 在去噪影像上，本文模型 τ̄ 0.140，MedSigLIP-FiLM 0.480、冠軍 0.436。量測文字把 τ̄ 從 0.250（T5，無量測）拉低到 0.140，測試時打亂量測又回到 0.222；作者的解讀是量測讓模型給過度平滑的去噪影像較高分。[(ref: main Table II)](https://arxiv.org/html/2611.08754v1#S3.T2) [(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- **不訓練時，量測文字是最大的一步** — 零樣本 Qwen3.8-27B 只看影像 Overall 1.370，加上量測文字 2.157；代理迴圈再加 0.023（不顯著），給 80 個附 MOS 的範例也只到 2.483。[(ref: main Table II)](https://arxiv.org/html/2611.08754v1#S3.T2)
- **訓練後，量測文字只多 0.015** — 調整視覺編碼器帶來最大的改進（T2 對 T1，+0.135），調過的編碼器對雜訊的 linear-probe R² 0.91（預訓練 0.83）；LLM 拿到量測後，調過與凍結的編碼器差異不再顯著（T6 對 T4）。量測文字本身加 0.015（T6 對 T5），測試時打亂則掉 0.048，超過它帶來的增益。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- **模型主要靠雜訊** — 一次只打亂一組量測，只有雜訊組顯著降低 Overall（−0.024）；部分相依分析中，平均預測隨雜訊百分位變動 0.32 MOS，其他組最多 0.09。[(ref: main Table III)](https://arxiv.org/html/2611.08754v1#S3.T3) [(ref: main Fig. 2)](https://arxiv.org/html/2611.08754v1#S3.F2)
- **代理的理由不可靠地解釋分數** — 零樣本代理每張影像都讀量測檔，66% 的影像另開視覺視圖，以最差的影像（MOS 0–1）最常開；理由裡 99.7% 提到雜訊，但所述方向與實際百分位一致的只有 76.8%（95% CI 72.0–81.9）。拿掉雜訊工具後 41% 的分數變動超過 0.25 MOS，Overall 卻不變。作者據此認為代理的理由描述了量測，但沒有可靠地解釋分數。[(ref: main Table III)](https://arxiv.org/html/2611.08754v1#S3.T3) [(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)

## 限制

作者自述：

- 只有 7 位訓練病人、一個 benchmark、一個 LLM；去噪集沒有 MOS。[(ref: main §IV)](https://arxiv.org/html/2611.08754v1#S4)
- 同一位病人的切片可能跨折，交叉驗證分數高估測試表現（Overall 差 0.118；把可能同病人的切片也分開後差 0.017）。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3)
- 事先固定的選模規則依 out-of-fold 分數選中的是 Phase 1 模型，Phase 2 模型是在看過測試結果後才被升為主模型；作者以同 seed 重跑重現了它的分數。[(ref: main §II)](https://arxiv.org/html/2611.08754v1#S2)
- 代理理由的關鍵字規則經人工確認的只有銳利度、HF（κ = 0.88）與雜訊方向（96%），條紋組沒有確認（κ < 0.7）。[(ref: main §III)](https://arxiv.org/html/2611.08754v1#S3) [(ref: main Table III)](https://arxiv.org/html/2611.08754v1#S3.T3)

本書庫另外注意到：

- **測試集只有 5 位病人** — 300 張測試切片的 bootstrap 以切片為單位重抽，信賴區間不反映病人層級的變異；跨醫院、跨掃描儀、腹部以外部位都沒有評估。
- **去噪排序以 SSIM 為準** — τ̄ 把「與全劑量參考的 SSIM」當作保真度的代理，不是醫師評分；τ̄ 低代表與 SSIM 排序不一致，至於醫師會不會也偏好較平滑的影像，論文沒有資料可答。
- **「可解釋」沒有落在主模型上** — 主模型以線性頭輸出分數，不產生文字理由；論文評估理由忠實度的對象是零樣本代理，而結果顯示理由與分數的對應並不可靠。

## 與書庫其他文章的關係

ModaLens 固定報告、只交換影像來量醫療 VLM 是否仍看影像，本篇則在 CT 品質評分上固定影像、只打亂寫成文字的量測值，量到訓練後的 MLLM 仍明顯依賴那段文字（主要是雜訊組）: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎](2026-09-17-modalens-image-sensitivity.md)

轉診文字研究顯示一句臨床線索就能改變 MRI 判讀，本篇在影像品質評分上看到同一種文字主導：量測文字能把零樣本 Overall 從 1.370 拉到 2.157，也會把去噪排序帶往偏好過度平滑的方向: [轉診單一句話就改變 MRI 判讀，叫模型忽略只有一個做得到](2026-10-28-referral-text-overrides-mri-mllm-glioma-abscess.md)

本篇顯示寫成文字的量測值會主導 MLLM 的 CT 品質評分；CT 標頭研究在另一種 CT 輸入檢查（系列涵蓋範圍）上看到文字型 metadata 的影響，且影響大小取決於它在對話中的送達位置: [CT 品管 VLM：同一個錯誤標頭，晚一輪送到就推翻正確判斷](2026-11-19-ct-dicom-header-order-vlm-qc.md)

本篇量到 MLLM 在 CT 品質評分上會高估過度平滑影像；該則的光子計數 CT 以預設開啟、可調三檔去雜訊強度的 CNN 作為原生重建，正是會系統性改變 CT 雜訊紋理與平滑程度的來源: [先過審再收證據：GE Photonova Spectra 七機構評估解析](../industry-watch/2026-11-19-ge-healthcare-photonova-spectra-pcct-collaborations.md)
## 實務的啟發

- **評估 CT 品質模型時，固定四捨五入與選模規則** — 本研究中格點四捨五入的效應（+0.024）大於頂尖方法之間的差距（0.021），在測試集上挑設定又能讓 MedSigLIP-FiLM 的 grid 分數從 2.733 升到 2.769；比較供應商或自建的品質評分模型時，應先把這兩件事寫進協定，否則排名可能只是協定差異。
- **在有 MOS 的資料之外，加一個去噪排序的檢查** — 同一個模型在 MOS 相關性上與冠軍持平，排序去噪結果卻明顯較差；若品質分數會被用來挑去噪器或劑量協定，這類「是否偏好過度平滑」的檢查是可借用的量測方法，但它以 SSIM 為準，仍需醫師評分驗證。
- **把手工量測交給 MLLM 前，先做打亂測試** — 測試時打亂量測、逐組打亂與比對理由方向，成本不高，卻能看出模型到底用了哪個輸入、理由是否對得上分數；本研究的結果是一個待驗證的警訊：量測文字能提升相關性，也可能把模型綁在單一量測（雜訊）上。

## References

- `main` — Basim K, Demiroglu T, Unal MO, Ertas M, Yildirim I. *Measurement-Aware Multimodal LLM for No-Reference Low-Dose CT Quality Assessment*. arXiv:2611.08754v1, 2026. [https://arxiv.org/abs/2611.08754](https://arxiv.org/abs/2611.08754)
  - 深鏈：[Abstract](https://arxiv.org/html/2611.08754v1#abstract1)、[§I](https://arxiv.org/html/2611.08754v1#S1)、[Fig. 1](https://arxiv.org/html/2611.08754v1#S1.F1)、[§II](https://arxiv.org/html/2611.08754v1#S2)、[Table I](https://arxiv.org/html/2611.08754v1#S2.T1)、[§III](https://arxiv.org/html/2611.08754v1#S3)、[Fig. 2](https://arxiv.org/html/2611.08754v1#S3.F2)、[Table II](https://arxiv.org/html/2611.08754v1#S3.T2)、[Table III](https://arxiv.org/html/2611.08754v1#S3.T3)、[§IV](https://arxiv.org/html/2611.08754v1#S4)
- `html` — arXiv HTML v1 全文. [https://arxiv.org/html/2611.08754v1](https://arxiv.org/html/2611.08754v1)
- `code` — agentic-ct-iqa（論文所列網址；本文發布時尚無公開內容）. [https://github.com/itu-biai/agentic-ct-iqa](https://github.com/itu-biai/agentic-ct-iqa)

[Home](../) · [AI Papers](./)
