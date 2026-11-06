---
parent: AI Papers
nav_order: 5
title: "量測值不再逐字吐出：HAD-VLM 用 diffusion 輸出卡尺端點"
catalog_id: "arxiv:2610.32948"
editors:
  - "Clare"
refs:
  main:
    title: "Beyond Discrete Tokens: Preserving Numerical Continuity in Medical Vision-Language Models"
    url: "https://arxiv.org/abs/2610.32948v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 量測值不再逐字吐出：HAD-VLM 用 diffusion 輸出卡尺端點

## 來源

- 團隊：Dianye Huang、Zhongliang Jiang（The University of Hong Kong，MIRoC Lab；Jiang 為通訊作者），Jiamei Guo、Yue Zhou、Nassir Navab（Technical University of Munich，CAMP），Mingde Li（中山大學附屬第一醫院超聲醫學科），Yi Xiong（深圳市羅湖區人民醫院），Wei Wang（廣東省人民醫院超聲醫學科），共 8 位作者；Huang 與 Guo 為共同第一作者。單位依論文 PDF 首頁作者註腳，HTML 版未顯示單位。[(ref: main PDF v1)](https://arxiv.org/pdf/2610.32948v1)
- 論文：*Beyond Discrete Tokens: Preserving Numerical Continuity in Medical Vision-Language Models*，arXiv:2610.32948v1（cs.CV；另列 cs.AI），2026-10-23 提交，目前只有 v1；授權 CC BY 4.0；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2610.32948v1)
- 識別碼：arXiv [2610.32948](https://arxiv.org/abs/2610.32948v1)；DOI [10.48550/arXiv.2610.32948](https://doi.org/10.48550/arXiv.2610.32948)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2610.32948v1)、[PDF v1](https://arxiv.org/pdf/2610.32948v1)。
- 程式與資料：論文沒有提供程式碼或模型權重連結；評估用的 EchoNet-LVH 與 Cervical Spine X-ray Atlas（CSXA）V3.0 為公開資料集。[(ref: main §IV-A1)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS1) [(ref: main §IV-F1)](https://arxiv.org/html/2610.32948v1#S4.SS6.SSS1)
- 研究性質：方法論文，核心方法已實作並在公開資料上訓練與測試；不是 pilot：EchoNet-LVH 測試集共 4,651 張標註影格（每項量測 1,154–1,170 張）。所有表格都是單次結果，沒有信賴區間、標準差或多次重複（X 光表的 ± 為絕對誤差的標準差）。[(ref: main Table II)](https://arxiv.org/html/2610.32948v1#S3.T2) [(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1)
- 證據邊界：本文數值以 arXiv v1 HTML 版的正文與 Table I–VI 為準；流程圖為本書庫依論文文字重繪，未複製論文原圖。

**編輯：** Clare

作者把 VLM 輸出量測值的方式從「一個字一個字寫出數字」改成「在數字的位置跑一段 diffusion，直接產生連續的卡尺端點座標與長度」，在 EchoNet-LVH 四項左心室量測上，平均絕對誤差比同一骨幹逐 token 輸出低 21.4–37.6%，也低於微調 Qwen3-VL 與加 MLP 回歸頭的版本；不過這個領先需要 20 次抽樣取中位數與座標—長度一致性檢查這兩步後處理撐住。[(ref: main Abstract)](https://arxiv.org/html/2610.32948v1) [(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1) [(ref: main Table III)](https://arxiv.org/html/2610.32948v1#S4.T3)

## 流程

![HAD-VLM 流程示意圖，標題為 HAD-VLM: hybrid autoregressive-diffusion VLM for prompt-conditioned ultrasound measurement。上排由左到右四個圓角方塊，以三支實線箭頭依序相連：淺藍色「(a) Prompt-adapted encoder」（Input: ultrasound frame I；CLIP ViT-L/14 (frozen)；Visual prompt tuning: L = 4 local prompts / layer、G = 4 global prompts；f_v = [CLS ; first global prompt]）、淡紫色「(b) MLP projector」（Two-layer MLP (GELU) maps f_v to LLM embedding space；Initialized from LLaVA；User prompt p names the target measurement）、黃色「(c) Hybrid LLM」（Vicuna-7B-v1.5 backbone；Text: next-token prediction；On token '[' -> diffusion slot: embedder E_diff(x_t, t)、diffusion head -> 5-tuple、DDIM, 4 sampling steps；Append ']' and resume text）、淺綠色「(d) Post-processing」（5-tuple x0 = [us, vs, ue, ve, m]；m_coord from endpoints vs m；If |m_coord - m| <= tau: use their average, else m；tau = 85th pct on validation；R = 20 samples -> median）。下排兩個灰色方塊：左為「Training (three stages)」（1. Alignment: visual prompts + projector, L_ce; CLIP and LLM frozen (15 epochs)；2. Regression: diffusion modules with L_diff; LoRA on last 4 LLM layers (30 epochs)；3. Joint: L_ce + L_diff, all trainable parts (15 epochs)；Diffusion: v-prediction, 100 timesteps；Targets: ChatGPT-written QA prompts around annotations），右為「Evaluation」（EchoNet-LVH (parasternal long-axis echo frames): IVSd, LVIDd, LVIDs, LVPWd in one multi-task model, train 40,690 / val 1,213 / test 4,651 frames；Baselines: Vicuna token output, fine-tuned Qwen3-VL, VLM + MLP regression head；Also: medical QA (word F1, BERTScore), CSXA cervical X-ray endplate length (pixels)）。](assets/had-vlm-diffusion-ultrasound-measurement-pipeline.png)

圖：本書庫依論文 §III-A、§III-B、§III-C、§IV-A 與 Table II 的文字重繪的流程示意圖，只含架構、訓練設定與資料量，不含結果數值，未複製論文原圖（論文 Fig. 2 為架構總覽，Fig. 3 為一致性機制示意）。[(ref: main Fig. 2)](https://arxiv.org/html/2610.32948v1#S1.F2) [(ref: main §III)](https://arxiv.org/html/2610.32948v1#S3) [(ref: main Table II)](https://arxiv.org/html/2610.32948v1#S3.T2)

## 背景／問題

心臟超音波的室中隔厚度、左心室內徑等量測，臨床上是在影像上放兩個卡尺端點再讀距離。作者想用 VLM 做這件事，好處是量測目標可以用文字指定（「量舒張末期的室中隔」），多項量測共用一個模型。[(ref: main §I)](https://arxiv.org/html/2610.32948v1#S1)

作者指出的問題是輸出形式：自回歸 VLM 把「10.1」拆成「10」「.」「1」等 token 逐一生成，訓練用的是分類式的 next-token cross-entropy，猜錯一位數和猜錯小數點的懲罰跟數值差多遠無關，端點座標的微小變動也不會平滑地反映在讀出的長度上。這是作者的論證；它有引用文獻（語言模型數值表徵、REO-VLM 的回歸分支）支持，論文自己的實驗也以「同骨幹逐 token 輸出」作為對照來檢驗。[(ref: main §I)](https://arxiv.org/html/2610.32948v1#S1) [(ref: main §II-C)](https://arxiv.org/html/2610.32948v1#S2.SS3)

既有的兩條路各有缺口：EchoNet-LVH 這類專用模型在固定的量測目標與輸出格式上表現好，但不能用文字切換任務；在 VLM 上接一個 regression head（REO-VLM 的做法）可以輸出連續值，但不直接把長度和端點位置綁在一起。本篇要回答的是：把連續值生成嵌進語言模型的解碼流程裡，能不能同時保有文字介面與量測精度。[(ref: main §II-A)](https://arxiv.org/html/2610.32948v1#S2.SS1) [(ref: main §II-C)](https://arxiv.org/html/2610.32948v1#S2.SS3)

## 方法摘要

**架構。** HAD-VLM（hybrid autoregressive-diffusion VLM）沿用 LLaVA 式三段結構：CLIP 影像編碼器加上 visual prompt tuning 適應超音波，MLP projector 把影像特徵送進 Vicuna-7B-v1.5，語言模型照常逐 token 產生文字。[(ref: main §III)](https://arxiv.org/html/2610.32948v1#S3)

**數字改走 diffusion。** 模型在文字中生成「[」時切換模式：把一個帶雜訊的 5 維向量嵌入到這個位置，由語言模型讀完前面的影像與文字後，用一個小的 diffusion head 逐步去噪，得到 5-tuple——起點座標、終點座標與長度。去噪完成後系統手動補上「]」，把數值寫回文字，再繼續逐 token 生成。作者用方括號當開關，是為了不必在詞表裡新增需要訓練的特殊 token。[(ref: main §III-B1)](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS1) [(ref: main §III-B3)](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS3)

**後處理。** 同一個 5-tuple 給出兩個長度：由端點座標算出的距離，以及模型直接輸出的長度。兩者差距小於門檻 τ 時取平均，否則採直接輸出的長度（coordinate-length consistency）；每次量測獨立抽樣 20 次，取後處理後長度的中位數（ensemble）。[(ref: main §III-B2)](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS2)

**訓練。** 三階段：先只訓練 visual prompts 與 projector 做對齊，再開啟 diffusion 模組並以 LoRA 微調語言模型最後四層，最後兩種 loss 一起訓練。四項量測用同一個模型，由 prompt 指定要量哪一項。[(ref: main §III-C2)](https://arxiv.org/html/2610.32948v1#S3.SS3.SSS2) [(ref: main §IV-A2)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS2)

## 方法詳解

**影像編碼。** 骨幹為凍結的 CLIP ViT-L/14；visual prompt tuning 依 DGL 的做法，每層加 4 個 layer-specific 的 local prompts、第一層加 4 個會往後傳遞的 global prompts。送進 projector 的特徵是最後一層 class token 與第一個 global prompt 的串接；projector 是兩層 MLP（GELU），權重從 LLaVA 初始化。[(ref: main §III-A; Eq. 1–2)](https://arxiv.org/html/2610.32948v1#S3.SS1)

**5-tuple 與 diffusion head。** 量測表示為 x₀ = [u_s, v_s, u_e, v_e, m]，前四個是正規化後的起點、終點座標，m 是以像素計的長度。可學習的 embedder 把帶噪的 x_t 與 timestep t 映到語言模型的 embedding 空間、放進數值位置；diffusion head 讀該位置的 hidden state 輸出預測。推論時從標準常態分布初始化，以 4 步 DDIM 取樣。[(ref: main §III-B1; Eq. 3–6)](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS1) [(ref: main Algorithm 1)](https://arxiv.org/html/2610.32948v1#alg1)

**一致性門檻與集成。** τ 取驗證集上「座標算出的長度」與「直接輸出長度」差距的第 85 百分位數，百分位依驗證集表現選定後在測試時固定；每次量測抽 R = 20 個樣本，各自做一致性處理後取長度中位數，回傳的端點則取自對應的那個樣本。[(ref: main §III-B2; Eq. 7–9)](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS2)

**Loss 與訓練設定。** 文字部分用 autoregressive cross-entropy，數值部分用 diffusion 去噪的 MSE。三階段分別訓練 15、30、15 個 epoch，學習率 1×10⁻⁴、1×10⁻⁵、1×10⁻⁶；LoRA 套在語言模型最後四層（rank 32、α 64、dropout 0.05）；AdamW（weight decay 0.01）、batch size 8、gradient clipping 1.0，單張 A100。diffusion 使用 100 個 timesteps 與 squaredcos_cap_v2 noise schedule。[(ref: main §III-C1; Eq. 10–11)](https://arxiv.org/html/2610.32948v1#S3.SS3.SSS1) [(ref: main §IV-A2)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS2)

**比較對象。** 三個基線代表三種數值輸出策略：VLM（Vicuna）以同一個 Vicuna-7B-v1.5 逐 token 生成數字；fine-tuned Qwen3-VL 在 EchoNet-LVH 上微調後同樣逐 token 輸出，用來檢查換一個 VLM 骨幹是否足夠；VLM + MLP Regression 把 diffusion head 換成直接回歸數值的 MLP，設定沿用 REO-VLM。所有方法在相同測試樣本上評估。[(ref: main §IV-B)](https://arxiv.org/html/2610.32948v1#S4.SS2)

- **論文未交代** — EchoNet-LVH 的 87:3:10 切分是以影格、影片還是病人為單位；同一位病人或同一段影片的不同影格是否可能同時出現在訓練與測試集。
- **論文未交代** — 模型輸出的長度以像素計，表中的 MAE 以 mm 計，像素到 mm 的換算方式沒有說明。
- **論文未交代** — diffusion 的參數化前後不一：§III-B1 與 Eq. 5、Eq. 11 寫的是預測雜訊，§IV-A2 寫的是 v-prediction。
- **論文未交代** — VLM（Vicuna）基線是否也在 EchoNet-LVH 上微調、訓練多少；VLM + MLP Regression 的訓練細節只寫「沿用 REO-VLM 設定」。
- **論文未交代** — 用 ChatGPT 生成的 QA prompt 模板內容與數量；程式碼與權重未公開。
- **論文未交代** — 沒有與 EchoNet-LVH 原論文的專用量測模型直接比較；與專家變異的比較只引用另一篇研究的數值。

## 資料與實驗

**資料。** EchoNet-LVH 為約 12,000 段胸骨旁長軸（parasternal long-axis）B-mode 心臟超音波影片，附有像素座標的量測端點與舒張／收縮期標記；作者取四項量測當目標，依 87:3:10 切分，並用 ChatGPT 生成多樣化的問答模板，把標註包成「文字＋數值」的訓練對。下表重製論文 Table II（單位：標註影格數）。[(ref: main §IV-A1)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS1) [(ref: main Table II)](https://arxiv.org/html/2610.32948v1#S3.T2)

| Split | IVSd | LVIDd | LVIDs | LVPWd | Total |
|---|---|---|---|---|---|
| Training set | 10265 | 10312 | 9859 | 10254 | 40690 |
| Validation set | 310 | 309 | 284 | 310 | 1213 |
| Test set | 1163 | 1170 | 1154 | 1164 | 4651 |

四項量測分別為舒張末期室中隔厚度（IVSd）、舒張末期與收縮末期左心室內徑（LVIDd、LVIDs）、舒張末期左心室後壁厚度（LVPWd）。跨模態測試另用 CSXA V3.0 裁出 C4、C5 椎體區域共 9,926 個樣本（85:15 訓練／測試），量上終板前後端點的距離；因影像來源不一、沒有一致的像素到實際距離校正，X 光結果全部以像素計。[(ref: main §IV-A1)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS1) [(ref: main §IV-F1)](https://arxiv.org/html/2610.32948v1#S4.SS6.SSS1)

**主結果。** 下表重製論文 Table I（EchoNet-LVH 測試集；MAE、RMSE、MAD 單位為 mm；MAD 為 Tromp 等人報告的專家量測差異，作為參考值）。[(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1)

| Models | IVSd MAE | IVSd RMSE | IVSd R² | IVSd r | LVIDd MAE | LVIDd RMSE | LVIDd R² | LVIDd r | LVIDs MAE | LVIDs RMSE | LVIDs R² | LVIDs r | LVPWd MAE | LVPWd RMSE | LVPWd R² | LVPWd r |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| MAD（專家差異） | 1.20 | | | | 2.97 | | | | 3.60 | | | | 1.16 | | | |
| VLM (Vicuna) | 1.82 | 2.54 | 0.25 | 0.62 | 3.62 | 5.00 | 0.60 | 0.82 | 3.88 | 4.99 | 0.65 | 0.82 | 1.86 | 8.43 | -12.55 | 0.15 |
| Fine-tuned Qwen3-VL | 1.68 | 2.44 | 0.32 | 0.60 | 3.71 | 4.87 | 0.60 | 0.79 | 3.82 | 5.01 | 0.64 | 0.81 | 1.47 | 1.95 | 0.28 | 0.57 |
| VLM + MLP Regression | 1.41 | 2.00 | 0.54 | 0.74 | 3.00 | 3.95 | 0.74 | 0.86 | 3.42 | 4.52 | 0.71 | 0.85 | 1.28 | 1.67 | 0.47 | 0.71 |
| HAD-VLM (ours) | 1.36 | 1.96 | 0.56 | 0.75 | 2.77 | 3.62 | 0.78 | 0.89 | 3.05 | 4.00 | 0.77 | 0.88 | 1.16 | 1.54 | 0.55 | 0.74 |

**消融。** 下表重製論文 Table III 的 MAE 欄（mm；同表另有 RMSE、R²、r）。「w/o cons. w/o ens.」是不做一致性處理也不集成、只取一次抽樣的 HAD-VLM。[(ref: main Table III)](https://arxiv.org/html/2610.32948v1#S4.T3)

| Variant | IVSd | LVIDd | LVIDs | LVPWd |
|---|---|---|---|---|
| w/o prompt tuning | 1.93 | 5.07 | 5.60 | 1.58 |
| w/o cons. w/o ens. | 1.49 | 3.04 | 3.31 | 1.31 |
| w/ cons. w/o ens. | 1.46 | 2.96 | 3.34 | 1.23 |
| HAD-VLM (full) | 1.36 | 2.77 | 3.05 | 1.16 |

**單任務與多任務。** 下表重製論文 Table IV 的 MAE 與 R²（mm）：四個各自訓練的單任務模型，對比一個以 prompt 切換任務的多任務 HAD-VLM。[(ref: main Table IV)](https://arxiv.org/html/2610.32948v1#S4.T4)

| Task | Single-task MAE | Multi-task MAE | Single-task R² | Multi-task R² |
|---|---|---|---|---|
| IVSd | 1.44 | 1.36 | 0.54 | 0.56 |
| LVIDd | 3.69 | 2.77 | 0.61 | 0.78 |
| LVIDs | 3.69 | 3.05 | 0.66 | 0.77 |
| LVPWd | 1.27 | 1.16 | 0.49 | 0.55 |

**語言能力與 X 光。** 在 USPilot 論文提供的醫療問答資料上，HAD-VLM 對原始 Vicuna-7B-v1.5 的 word-level F1 為 0.320 對 0.298，BERTScore F1 為 0.882 對 0.869。CSXA 上終板長度（參考值平均 170.4 px、標準差 29.73 px）的絕對誤差為 6.7 ± 5.7 px，逐 token 的 Vicuna 基線為 11.4 ± 93.9 px。[(ref: main Table V)](https://arxiv.org/html/2610.32948v1#S4.T5) [(ref: main Table VI)](https://arxiv.org/html/2610.32948v1#S4.T6) [(ref: main §IV-F2)](https://arxiv.org/html/2610.32948v1#S4.SS6.SSS2)

## 結果

- **對逐 token 輸出：四項都較好** — 與同骨幹的 VLM（Vicuna）相比，MAE 由 1.82／3.62／3.88／1.86 mm 降到 1.36／2.77／3.05／1.16 mm（IVSd／LVIDd／LVIDs／LVPWd），降幅 25.3%、23.5%、21.4%、37.6%；R² 例如 IVSd 由 0.25 升到 0.56。逐 token 基線在 LVPWd 的 RMSE 8.43 mm、R² −12.55，作者沒有解釋，數值型態像是少數極端錯誤主導。[(ref: main §IV-B)](https://arxiv.org/html/2610.32948v1#S4.SS2) [(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1)
- **換骨幹不夠** — 微調 Qwen3-VL 仍逐 token 輸出，LVIDd、LVIDs 的 MAE 為 3.71、3.82 mm，與 Vicuna 基線同一級距，高於 HAD-VLM 的 2.77、3.05 mm。[(ref: main §IV-B)](https://arxiv.org/html/2610.32948v1#S4.SS2)
- **對 MLP 回歸頭：差距小** — MLP 回歸頭已大幅改善兩個逐 token 基線；HAD-VLM 再把 MAE 降低 0.05（IVSd）、0.23（LVIDd，7.7%）、0.37（LVIDs，10.8%）、0.12 mm（LVPWd）。作者的措辭是「在評估的設定下」支持 diffusion 優於直接回歸。[(ref: main §IV-B)](https://arxiv.org/html/2610.32948v1#S4.SS2) [(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1)
- **後處理是領先的必要條件** — 本書庫對照 Table I 與 Table III：只取一次抽樣、不做一致性處理時，HAD-VLM 的 MAE 為 1.49／3.04／3.31／1.31 mm，MLP 回歸頭為 1.41／3.00／3.42／1.28 mm，四項中只有 LVIDs 較好。作者在消融中指出的是另一面：即使沒有後處理，混合模型已勝過逐 token 基線（LVIDd 3.04 對 3.62 mm）。[(ref: main Table III)](https://arxiv.org/html/2610.32948v1#S4.T3) [(ref: main §IV-C)](https://arxiv.org/html/2610.32948v1#S4.SS3)
- **兩步後處理的貢獻不一致** — 加入一致性處理讓 LVPWd MAE 由 1.31 降到 1.23 mm，但 LVIDs 由 3.31 略升到 3.34 mm；再加入 20 次抽樣集成後四項都改善，例如 LVIDs 由 3.34 降到 3.05 mm。拿掉 visual prompt tuning 退步最多，LVIDd MAE 升到 5.07 mm。[(ref: main §IV-C)](https://arxiv.org/html/2610.32948v1#S4.SS3)
- **多任務比單任務好** — 一個模型同時學四項量測，四項 MAE 都低於各自訓練的單任務模型，LVIDd 由 3.69 降到 2.77 mm（24.9%）、LVIDs 由 3.69 降到 3.05 mm（17.3%）。[(ref: main §IV-D)](https://arxiv.org/html/2610.32948v1#S4.SS4)
- **與專家差異同一數量級，但不能當成等效** — HAD-VLM 的 LVIDd、LVIDs MAE（2.77、3.05 mm）低於 Tromp 等人報告的專家差異 2.97、3.60 mm，IVSd（1.36 對 1.20 mm）則高於、LVPWd 相同（1.16 mm）。作者自己註明資料集與評估方式不同，這個比較不能推論為與專家等效。[(ref: main §IV-B)](https://arxiv.org/html/2610.32948v1#S4.SS2)
- **語言能力沒有退化** — 醫療問答的四個分數都略高於原始 Vicuna；這只說明在這一個資料集上沒有退步，不是問答能力的完整評估。[(ref: main §IV-E)](https://arxiv.org/html/2610.32948v1#S4.SS5)
- **X 光上的穩定度差異最明顯** — CSXA 上 MAE 由 11.4 降到 6.7 px（41.2%），絕對誤差的標準差由 93.9 降到 5.7 px；作者在結論中稱之為跨模態的初步證據。[(ref: main §IV-F2)](https://arxiv.org/html/2610.32948v1#S4.SS6.SSS2) [(ref: main §VI)](https://arxiv.org/html/2610.32948v1#S6)

## 限制

作者自述的限制：[(ref: main §V)](https://arxiv.org/html/2610.32948v1#S5) [(ref: main §VI)](https://arxiv.org/html/2610.32948v1#S6)

- **只處理線性量測** — 框架目前只做兩點距離，面積、體積或更複雜的幾何量測留待後續。
- **長度準不等於位置對** — 論文 Fig. 4 的定性例子中，有些預測線段位置偏了、長度卻接近參考值；作者因此主張端點定位與數值要分開評估，但論文沒有報告端點定位誤差的定量結果。[(ref: main Fig. 4)](https://arxiv.org/html/2610.32948v1#S3.F4)
- **尚未跨機構驗證** — 作者把跨機構與跨影像條件的驗證、量測不確定性估計、與報告生成的整合列為未來工作。

本書庫另外注意到：

- **切分單位不明是最大的不確定性** — 每段影片會產生多個標註影格，論文沒有說明切分是否以病人或影片為單位；若同一段影片的影格同時落在訓練與測試集，所有方法的誤差都可能被低估，方法之間的相對排序未必受影響，但絕對值與「接近專家差異」的說法會受影響。[(ref: main §IV-A1)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS1)
- **沒有不確定性** — 對 MLP 回歸頭的差距為 0.05–0.37 mm，論文沒有信賴區間、多次訓練或統計檢定，無法判斷這個差距的穩定性。[(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1)
- **後處理的計算成本** — 每次量測要跑 20 次 4 步 DDIM 抽樣；論文沒有報告推論時間，對照的 MLP 回歸頭只需一次前向計算。[(ref: main §III-B2)](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS2)
- **沒有和專用量測模型比** — 所有基線都是 VLM 變體；EchoNet-LVH 原論文的專用模型沒有在相同切分上重跑比較，所以「文字介面的代價有多大」仍是未知數。[(ref: main §II-A)](https://arxiv.org/html/2610.32948v1#S2.SS1)
- **單一影格、單一切面** — 輸入是胸骨旁長軸影片中的單張標註影格，選影格（舒張末期或收縮末期）這一步由資料集標註提供，不在模型範圍內。[(ref: main §IV-A1)](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS1)

## 與書庫其他文章的關係

兩篇都在 EchoNet 系列心臟超音波資料上做連續量的預測，分割天花板研究問的是「多給一層左心室分割能讓射出分率回歸準多少」，本篇則問「讓 VLM 用 diffusion 直接輸出卡尺端點與長度，能否比逐 token 寫數字更準」，兩者都把誤差拆到輸出形式與輔助資訊的結構上: [先分割左心室再估射出分率？一條 10.5% 的天花板](2026-09-23-segmentation-ceiling-ef-regression.md)

VoxelSage 把幾何量測交給確定性程式、LLM 只負責調度，本篇走相反方向，讓語言模型本身產生連續的量測值，兩篇並讀可對照「量測交給工具」與「量測留在模型裡」兩種設計，以及各自缺少的對照組: [VoxelSage：肝腫瘤量測交給程式，成效數字來自二維模擬器](2026-10-06-voxelsage-liver-ct-tool-agent.md)

## 實務的啟發

- **可借用的設計：數值輸出不要只靠 token** — 對要讓 VLM 輸出量測值、劑量或分數的團隊，本篇的對照提供一個具體參考：同一骨幹改成連續輸出（diffusion 或 MLP 回歸頭）後，四項量測的 MAE 都明顯低於逐 token 生成，換一個更新的 VLM 骨幹則幫助有限。這是單一資料集、單次訓練的結果，值得在自己的任務上先做同樣的三組對照。[(ref: main Table I)](https://arxiv.org/html/2610.32948v1#S3.T1)
- **評估時把後處理拆開看** — 本篇的領先有一部分來自 20 次抽樣取中位數；比較方法時，應同時列出單次抽樣的結果與推論成本，否則容易把集成的效果算成架構的效果。[(ref: main Table III)](https://arxiv.org/html/2610.32948v1#S4.T3)
- **輸出端點、而不只是長度** — 把長度和兩個端點座標一起輸出，讓長度可以回到影像上檢查；論文的定性例子也提醒，只看長度誤差會漏掉「位置錯、長度剛好對」的情形，量測型模型的驗收至少要包含端點位置的誤差。[(ref: main Fig. 4)](https://arxiv.org/html/2610.32948v1#S3.F4)
- **待驗證：與專家差異的比較** — 「MAE 已在專家差異範圍內」需要在以病人為單位切分、同一套標註流程、外部機構的資料上重新確認，目前的證據還不足以支持臨床使用。[(ref: main §IV-B)](https://arxiv.org/html/2610.32948v1#S4.SS2)

## References

- **main** — Huang D, Guo J, Zhou Y, Li M, Xiong Y, Wang W, Navab N, Jiang Z. *Beyond Discrete Tokens: Preserving Numerical Continuity in Medical Vision-Language Models*. arXiv:2610.32948v1, 2026. [abstract](https://arxiv.org/abs/2610.32948v1)；[HTML v1](https://arxiv.org/html/2610.32948v1)；[PDF v1](https://arxiv.org/pdf/2610.32948v1)；DOI [10.48550/arXiv.2610.32948](https://doi.org/10.48550/arXiv.2610.32948)
  - 深鏈：[§I](https://arxiv.org/html/2610.32948v1#S1)、[Fig. 2](https://arxiv.org/html/2610.32948v1#S1.F2)、[§II-A](https://arxiv.org/html/2610.32948v1#S2.SS1)、[§II-C](https://arxiv.org/html/2610.32948v1#S2.SS3)、[§III](https://arxiv.org/html/2610.32948v1#S3)、[§III-A](https://arxiv.org/html/2610.32948v1#S3.SS1)、[Algorithm 1](https://arxiv.org/html/2610.32948v1#alg1)、[§III-B1](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS1)、[§III-B2](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS2)、[Table I](https://arxiv.org/html/2610.32948v1#S3.T1)、[Fig. 4](https://arxiv.org/html/2610.32948v1#S3.F4)、[§III-B3](https://arxiv.org/html/2610.32948v1#S3.SS2.SSS3)、[§III-C1](https://arxiv.org/html/2610.32948v1#S3.SS3.SSS1)、[§III-C2](https://arxiv.org/html/2610.32948v1#S3.SS3.SSS2)、[Table II](https://arxiv.org/html/2610.32948v1#S3.T2)、[§IV-A1](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS1)、[§IV-A2](https://arxiv.org/html/2610.32948v1#S4.SS1.SSS2)、[Table III](https://arxiv.org/html/2610.32948v1#S4.T3)、[§IV-B](https://arxiv.org/html/2610.32948v1#S4.SS2)、[§IV-C](https://arxiv.org/html/2610.32948v1#S4.SS3)、[Table IV](https://arxiv.org/html/2610.32948v1#S4.T4)、[§IV-D](https://arxiv.org/html/2610.32948v1#S4.SS4)、[§IV-E](https://arxiv.org/html/2610.32948v1#S4.SS5)、[§IV-F1](https://arxiv.org/html/2610.32948v1#S4.SS6.SSS1)、[Table V](https://arxiv.org/html/2610.32948v1#S4.T5)、[§IV-F2](https://arxiv.org/html/2610.32948v1#S4.SS6.SSS2)、[Table VI](https://arxiv.org/html/2610.32948v1#S4.T6)、[§V](https://arxiv.org/html/2610.32948v1#S5)、[§VI](https://arxiv.org/html/2610.32948v1#S6)

[Home](../) · [AI Papers](./)
