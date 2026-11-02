---
catalog_id: "arxiv:2610.30980"
editors:
  - "Clare"
refs:
  main:
    title: "Diagnostic Loss: Asymmetric Supervision for Radiology Report Generation"
    url: "https://arxiv.org/abs/2610.30980v1"
  code:
    title: "gmum/DLoss (GitHub)"
    url: "https://github.com/gmum/DLoss"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# DLoss：訓練時把「報告該寫的診斷詞」與「不該出現的診斷詞」分開施壓，六個 3D 腹部 CT 報告模型的 GREEN 平均多 4.05 分、外部資料多 4.28 分，推論不加成本；但評分全靠自動指標，各模型增益從不到 1 分到 14 分不等

## 來源

- 團隊：Jagiellonian University、Johns Hopkins University、GAMMED、Massachusetts General Hospital 與 Harvard Medical School，7 位作者 Ignacy Kolton、Wenxuan Li、Zongwei Zhou、Jarosław B. Ćwikła、Arkadiusz Sitek、Pedro R. A. S. Bassi、Szymon Płotka；論文首頁只列出單位，沒有標出作者與單位的對應。研究經費含 National Science Center, Poland（2025/57/B/ST6/03100）。[(ref: main title block)](https://arxiv.org/html/2610.30980v1) [(ref: main Acknowledgments)](https://arxiv.org/html/2610.30980v1#Sx1)
- 論文：*Diagnostic Loss: Asymmetric Supervision for Radiology Report Generation*，arXiv:2610.30980v1（cs.CV；另列 cs.LG），2026-10-22 提交，目前只有 v1；授權為 CC BY-NC-SA 4.0；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2610.30980v1)
- 識別碼：arXiv [2610.30980](https://arxiv.org/abs/2610.30980v1)；DOI [10.48550/arXiv.2610.30980](https://doi.org/10.48550/arXiv.2610.30980)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2610.30980v1)、[PDF v1](https://arxiv.org/pdf/2610.30980v1)。
- 程式與資料：DLoss 程式碼公開於 [github.com/gmum/DLoss](https://github.com/gmum/DLoss)；訓練用的 Merlin 與 CancerVerse 為公開資料集，外部測試的院內資料不公開。[(ref: main Reproducibility statement)](https://arxiv.org/html/2610.30980v1#Sx1.SSx3)
- 研究性質：方法論文，DLoss 已實作並套到六個既有 3D 醫療 VLM 上，與同條件只用 cross-entropy 微調的版本比較；不是 pilot。主表 Table 1 每個設定只訓練一次、沒有信賴區間；不確定性只在附錄以 BTB3D 一個模型、九組 seed 的配對分析補充。所有分數都是自動指標，沒有放射科醫師評讀。[(ref: main §4.2)](https://arxiv.org/html/2610.30980v1#S4.SS2) [(ref: main Appendix F)](https://arxiv.org/html/2610.30980v1#A6)
- 證據邊界：本文數值以 arXiv v1 HTML 版的正文、Table 1–7 為準；Fig. 2 的質性範例與附錄 Fig. 3–6 的示意圖只作敘述參考，不引述圖上的病例內容。

**編輯：** Clare

作者提出一個只在訓練時加上的損失函數 DLoss：對參考報告支持的診斷詞，要求它「至少在某個位置」拿到足夠機率，對不被支持的診斷詞，則壓低它「在任何位置」的機率尖峰；套到六個 3D 腹部 CT 報告生成模型上，GREEN 平均在 Merlin 測試集多 4.05 分、在院內外部資料多 4.28 分，72 組模型－指標－測試集比較中有 71 組上升，推論流程與計算量不變。[(ref: main Abstract)](https://arxiv.org/html/2610.30980v1) [(ref: main §4.2; Table 1)](https://arxiv.org/html/2610.30980v1#S4.T1)

## 流程

![DLoss 流程示意圖，分上下兩排。上排標題為 (a) Training: cross-entropy + Diagnostic Loss (DLoss)，四個方塊由左到右以實線箭頭相連：淺藍色「Abdominal CT + report」（3D CT volume paired with its free-text radiology report；Training data (pooled): Merlin train split 20,369 scans、CancerVerse 24,168 scans）→ 淺藍色「1. Organ-level pairs」（Organs segmented with TotalSegmentator；Report parsed into findings for 11 organ groups by Qwen3-30B-A3B；One organ prompt -> one organ finding）→ 淺藍色「2. Diagnostic targets」（Offline LLM tagging maps each organ finding into a controlled target space G；D+ = supported targets、D- = unsupported alternatives；Explicitly negated concepts are excluded from both sets；Lexical forms -> token sets V）→ 淺橘色「3. Asymmetric pooling」（Mass m = sum of p(v) over V, per decoder position；D+: noisy-OR over positions, L+ = -log q+；D-: log-sum-exp (tau = 8) over log m；L = CE + s*(lambda+ L+ + lambda- L-)）。下排標題為 (b) Model and evaluation，三個方塊由左到右以實線箭頭相連：淺綠色「MedVLM backbones (6)」（Merlin (RadLLaMA-7B)、BTB3D (Llama-3.1-8B)、RadFM (MedLLaMA-13B)、fVLM / HLIP / SPECTRE (Qwen2.5-0.5B)；Visual features fixed; decoder weights frozen; only LoRA parameters and the visual-to-text projector / adapter are trained；Same inputs and LoRA setup for CE vs CE + DLoss）→ 淺綠色「Inference」（Target sets D+, D- and token sets V are discarded；Decoding is identical to the CE-trained baseline；No extra inference-time computation）→ 灰色「Evaluation」（In-distribution: Merlin official test set 5,125 scans；Out-of-distribution: in-house cohort 2,706 scans, 1,948 patients；Lexical: BLEU, ROUGE-L, METEOR, CIDEr；Clinical: GREEN, RadGraph-F1 (RadEval)；Scored per organ finding, automatic only）](assets/dloss-diagnostic-loss-training-pipeline.png)

圖：本書庫依論文 §3、§4.1、Appendix A、B、E.1 與 E.2 的文字重繪的流程示意圖，只含設計層級的設定與資料量，不含結果數值，未複製論文原圖（論文 Fig. 1 為同一方法的概觀圖，Algorithm 1 為損失的計算步驟）。[(ref: main Fig. 1)](https://arxiv.org/html/2610.30980v1#S1.F1) [(ref: main Algorithm 1)](https://arxiv.org/html/2610.30980v1#alg1)

## 背景／問題

放射報告的價值在於明確寫出影像上有哪些診斷、沒有哪些診斷；作者引用既有研究指出，現有醫療 VLM 生成的報告常讀起來像人寫的，卻會漏掉影像上存在的診斷、低估嚴重度，或寫出影像不支持的診斷，放射科醫師審閱胸片生成報告時，也把這類錯誤列為臨床上重要的錯誤。[(ref: main §1)](https://arxiv.org/html/2610.30980v1#S1)

作者的主張是：這個落差不只來自模型容量，也來自訓練目標。標準的 token-level cross-entropy 對診斷詞與敘述詞一視同仁，大量出現的敘述 token 主導梯度，少見的診斷詞權重偏低，而且沒有任何序列層級的監督去要求「該寫的診斷至少出現一次、不該寫的診斷一次都不要冒出來」。這是作者引用既有文獻（例如 Delbrouck 等人 2022 年以語意獎勵改善事實正確性的研究）提出的解釋，本篇的實驗是在固定其他條件下只換訓練目標，能檢驗「加上這個目標後自動指標是否上升」，但不直接證明漏寫與錯寫的成因就是訓練目標。[(ref: main §1)](https://arxiv.org/html/2610.30980v1#S1) [(ref: main §2)](https://arxiv.org/html/2610.30980v1#S2)

既有改動訓練目標的做法包括 unlikelihood training（壓低選定負例的機率）、token 重新加權，以及 SAT-RRG（由 LLM 找出語意錯誤位置再調整該處的訓練）；作者把 DLoss 定位為不指定詞要出現在哪個位置、只對整段序列的機率做非對稱彙總的版本，彙總方式借自 multiple-instance learning。[(ref: main §2)](https://arxiv.org/html/2610.30980v1#S2)

## 方法摘要

**加在哪裡。** DLoss 直接作用在語言解碼器已經算出的 token 機率上，不改視覺編碼器、解碼器、tokenizer 或推論程序；只要模型能吐出 decoder logits 就能套用。最終損失是 ℒ_total = ℒ_CE + ℒ_diag，推論時診斷目標集合全部丟棄。[(ref: main §3.1)](https://arxiv.org/html/2610.30980v1#S3.SS1) [(ref: main §3.2)](https://arxiv.org/html/2610.30980v1#S3.SS2)

**診斷目標從哪來。** 每份參考報告先拆成器官層級的影像－文字配對：器官由 TotalSegmentator 分割，報告由 Qwen3-30B-A3B 拆成 11 個器官群組的發現。在每個器官配對內，參考報告支持的診斷概念構成 supported set 𝒟⁺，同一器官的其他替代診斷構成 unsupported set 𝒟⁻；明確被否定的概念兩邊都不放，以免給出互相衝突的詞彙監督。每個診斷目標是一個「概念」而不是單一字串，例如 cholelithiasis、gallstones、stone 歸到同一目標，再用各模型自己的 tokenizer 轉成 token 索引集合。[(ref: main §3.1)](https://arxiv.org/html/2610.30980v1#S3.SS1) [(ref: main Appendix B)](https://arxiv.org/html/2610.30980v1#A2) [(ref: main Appendix C)](https://arxiv.org/html/2610.30980v1#A3)

**非對稱彙總。** 先把每個位置上屬於某目標的 token 機率加總成 m_{i,d,t}，接著：

- **Supported targets** — 以 noisy-OR 彙總所有位置，q⁺ = 1 − ∏(1 − m)，損失為 −log q⁺；只要某個位置給了足夠機率就會飽和，不規定詞要出現在哪。[(ref: main Eq. 5–6)](https://arxiv.org/html/2610.30980v1#S3.SS2)
- **Unsupported targets** — 對 log m 做溫度 τ 控制的 log-sum-exp，τ 越大越集中在機率最高的那個位置，因此只要有一個位置冒出尖峰就會被懲罰。[(ref: main Eq. 7)](https://arxiv.org/html/2610.30980v1#S3.SS2)
- **合併** — 兩項各自取加權平均後，以係數 λ₊、λ₋ 與樣本權重 s_i 加總，再對含至少一個目標的樣本取平均；論文所有實驗的目標權重都設為 1。[(ref: main Eq. 8–10)](https://arxiv.org/html/2610.30980v1#S3.SS2)

**怎麼比。** 六個 3D 醫療 VLM（Merlin、SPECTRE、RadFM、fVLM、BTB3D、HLIP）各自以「只用 cross-entropy」與「cross-entropy 加 DLoss」在同樣的輸入、解碼器、LoRA 設定與訓練資料下微調，用 BLEU、ROUGE-L、METEOR、CIDEr 四個詞面指標與 GREEN、RadGraph-F1 兩個臨床內容指標比較。[(ref: main §4.1)](https://arxiv.org/html/2610.30980v1#S4.SS1)

## 方法詳解

**哪些參數在訓練。** 報告生成訓練時視覺特徵固定、解碼器全權重凍結，只訓練解碼器的 LoRA 參數與視覺到文字的 projector 或 adapter；CE 與 DLoss 兩組使用同一個視覺初始化。Merlin 與 RadFM 用公開視覺權重，SPECTRE 用預訓練視覺 checkpoint，fVLM、BTB3D、HLIP 用作者在本地訓練的視覺 checkpoint。每個報告生成器一次只依一個器官提示生成該器官的發現。[(ref: main Appendix E.1)](https://arxiv.org/html/2610.30980v1#A5.SS1)

| Backbone | Decoder | LoRA（rank／alpha／dropout） | λ₊ | λ₋ |
|---|---|---|---|---|
| Merlin | RadLLaMA-7B | 512／16／0.1（query、value） | 0.001 | 0.0005 |
| BTB3D | Llama-3.1-8B-Instruct | 128／256／0.05 | 0.001 | 0.00025 |
| fVLM | Qwen2.5-0.5B | 16／32／0.05 | 0.001 | 0.00025 |
| HLIP | Qwen2.5-0.5B | 16／32／0.05 | 0.001 | 0.00025 |
| RadFM | MedLLaMA-13B | 16／32／0.05 | 0.01 | 0.01 |
| SPECTRE | Qwen2.5-0.5B | 16／32／0.05 | 0.01 | 0.005 |

上表整理自論文 Appendix E.1 正文與 Table 5；除 Merlin 外，其餘五個模型的 LoRA 套在 query、key、value、output 與 feed-forward 的 gate、up、down projection。所有執行的 τ = 8；λ 係數由「小規模 grid search」選定。[(ref: main Appendix E.1; Table 5)](https://arxiv.org/html/2610.30980v1#A5.T5)

**影像前處理。** 訓練用 CT 統一轉成 1.5 mm 等向性體素，再由各模型依原始實作做強度正規化與幾何前處理；Merlin 官方測試集以原始間距輸入。訓練使用最多四張 NVIDIA GH200（各 96 GB）。[(ref: main §4.1)](https://arxiv.org/html/2610.30980v1#S4.SS1)

**臨床內容指標怎麼算。** RadGraph-F1 與 GREEN 都經由 RadEval 框架計算：RadGraph-F1 取 complete（實體＋關係）版本，對每個器官發現計算後取平均；GREEN 使用本地的 GREEN-RadLLaMA2-7b 評估模型，而非 GPT-4 API，每例分數為「配對到的發現數 ÷（配對數＋臨床上重要的錯誤數）」再取平均。作者明寫這兩個指標都不是針對各器官的放射科醫師審閱，也不能單獨證明臨床安全性。[(ref: main Appendix E.2)](https://arxiv.org/html/2610.30980v1#A5.SS2)

- **論文未交代** — 器官提示（organ prompt）與 Qwen3-30B-A3B 拆解報告所用的 prompt 全文；做診斷概念標註與同義詞合併的是哪一個 LLM、用什麼 prompt。
- **論文未交代** — 受控目標空間 𝒢 共有多少個診斷概念，以及每個器官的 unsupported set 是取「同一器官所有其他概念」還是另有篩選。
- **論文未交代** — 學習率、訓練 epoch 數與訓練 batch size（Table 2 的批次大小 8 只用於量測訓練成本）；λ 係數的 grid search 在哪個資料切分上進行。
- **論文未交代** — Table 3 消融的 CE 基線（fVLM，BLEU-4 49.55、GREEN 65.96、F1-RG 55.55）與 Table 1 的 fVLM 基線（BLEU 39.58、GREEN 53.91、F1-RG 46.53）同樣在 Merlin 測試集上卻相差約 10 分；論文只說明消融用 seed 13、兩張 A100、以 validation CE 選 checkpoint，沒有解釋兩組數字為何不同。

## 資料與實驗

**資料。** 訓練合併兩個公開腹部 CT 資料集，評估分成同分布的 Merlin 官方測試集與不公開的院內外部資料。[(ref: main Appendix A; Table 4)](https://arxiv.org/html/2610.30980v1#A1.T4)

| Dataset | Scans | Exams | Patients | Train | Test | 說明 |
|---|---|---|---|---|---|---|
| Merlin | 25,494 | 25,494 | 18,317 | 20,369 | 5,125 | Stanford Hospital 急診 2012–2018 年腹部骨盆對比增強 CT；訓練部分再分為 15,309 訓練、5,060 驗證 |
| CancerVerse | 24,168 | 22,867 | 13,863 | 24,168 | — | University Hospital Basel 與 Medipol University Hospital 的多期 CT，全部用於訓練 |
| In-house | 2,706 | 2,706 | 1,948 | — | 2,706 | 多中心對比增強 CT，來自全國性世代中的 300 個院所；倫理審查為 University of Warmia and Mazury in Olsztyn（No. 9/2023） |
| Total | 52,368 | 50,767 | 34,128 | 44,537 | 7,831 | |

資料說明欄依論文 Appendix A.1–A.2 與 Ethics statement 整理。[(ref: main Appendix A)](https://arxiv.org/html/2610.30980v1#A1) [(ref: main Ethics statement)](https://arxiv.org/html/2610.30980v1#Sx1.SSx2)

**主實驗：六個模型加或不加 DLoss。** 下表重製論文 Table 1；M 為 Merlin 測試集、E 為院內外部資料，「＋DLoss」列為相對於同模型基線的變化量，Δ̄ 為六個模型的平均變化。F1-RG 為 RadGraph complete F1。每個設定只訓練一次。[(ref: main Table 1)](https://arxiv.org/html/2610.30980v1#S4.T1)

| Method | BLEU M | BLEU E | ROUGE-L M | ROUGE-L E | METEOR M | METEOR E | CIDEr M | CIDEr E | GREEN M | GREEN E | F1-RG M | F1-RG E |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Merlin | 20.65 | 16.63 | 44.21 | 34.30 | 18.45 | 15.21 | 13.98 | 10.89 | 53.82 | 45.01 | 35.01 | 26.36 |
| ＋DLoss | +0.01 | +0.09 | +0.05 | +0.26 | +0.01 | +0.07 | +0.18 | +0.50 | +0.83 | +1.24 | −0.01 | +0.35 |
| fVLM | 39.58 | 18.61 | 50.02 | 34.06 | 26.32 | 15.75 | 36.25 | 18.15 | 53.91 | 46.78 | 46.53 | 29.32 |
| ＋DLoss | +7.04 | +2.59 | +6.70 | +2.39 | +4.04 | +1.26 | +6.56 | +1.34 | +8.99 | +3.06 | +6.56 | +1.65 |
| BTB3D | 15.96 | 16.38 | 32.21 | 33.75 | 17.07 | 16.14 | 17.39 | 19.50 | 53.38 | 55.76 | 25.82 | 27.95 |
| ＋DLoss | +8.62 | +6.74 | +7.47 | +4.39 | +3.99 | +2.42 | +10.52 | +4.32 | +2.05 | +2.06 | +9.18 | +4.95 |
| HLIP | 40.18 | 21.54 | 52.16 | 40.70 | 26.82 | 18.07 | 37.33 | 21.73 | 56.15 | 49.54 | 48.02 | 34.22 |
| ＋DLoss | +2.44 | +2.98 | +2.02 | +3.47 | +1.51 | +1.61 | +1.74 | +2.40 | +4.09 | +4.43 | +2.18 | +3.38 |
| RadFM | 49.93 | 27.80 | 60.55 | 45.09 | 32.84 | 21.06 | 48.04 | 27.41 | 64.80 | 62.71 | 57.91 | 39.74 |
| ＋DLoss | +0.06 | +0.21 | +0.22 | +0.48 | +0.06 | +0.18 | +0.11 | +0.25 | +0.50 | +0.86 | +0.23 | +0.41 |
| SPECTRE | 31.88 | 14.20 | 42.54 | 28.14 | 22.89 | 12.64 | 32.30 | 13.58 | 45.35 | 41.34 | 41.95 | 26.53 |
| ＋DLoss | +5.11 | +10.86 | +5.41 | +10.95 | +2.79 | +6.59 | +3.01 | +10.12 | +7.84 | +14.03 | +4.79 | +7.03 |
| Δ̄ | +3.88 | +3.91 | +3.65 | +3.66 | +2.07 | +2.02 | +3.69 | +3.16 | +4.05 | +4.28 | +3.82 | +2.96 |

**九組 seed 的配對分析（只有 BTB3D、只有 Merlin 測試集）。** 作者另以九組相同 seed 各訓練 CE 與 CE＋DLoss 的 BTB3D，在 5,125 個研究、56,375 個器官發現列上計算 DLoss 減 CE 的平均差，並以 5,000 次重抽樣給出兩種 95% bootstrap CI（只重抽 seed 配對；同時重抽 seed 與研究）。下表節錄論文 Table 6 的三項指標，數值為指標原始尺度（0–1，與 Table 1 的分數尺度不同）。[(ref: main Appendix F; Table 6)](https://arxiv.org/html/2610.30980v1#A6.T6)

| Metric | Mean effect | Seed bootstrap | Seed–study bootstrap |
|---|---|---|---|
| BLEU-4 | +0.0752 | [+0.0124, +0.1483] | [+0.0127, +0.1475] |
| GREEN | +0.0455 | [+0.0197, +0.0728] | [+0.0197, +0.0732] |
| RadGraph Complete | +0.0795 | [+0.0203, +0.1447] | [+0.0203, +0.1451] |

**消融（fVLM、seed 13、Merlin 測試集）。** 下表重製論文 Table 3；CE 列為絕對分數，其餘列為相對 CE 的百分比變化。S／U 指 supported／unsupported 目標，「only」只保留 CE 加該一項，「max」「mean」為把該項的彙總方式換掉。[(ref: main Table 3)](https://arxiv.org/html/2610.30980v1#S4.T3) [(ref: main Appendix G)](https://arxiv.org/html/2610.30980v1#A7)

| Config | BLEU-4 (%) | GREEN (%) | F1-RG (%) |
|---|---|---|---|
| #1 CE | 49.55 | 65.96 | 55.55 |
| #2 S-only | −1.88 | −1.11 | −0.74 |
| #3 U-only | −2.75 | −2.62 | −1.87 |
| #4 S-max | −16.11 | −14.76 | −11.10 |
| #5 S-mean | −2.27 | −1.28 | −1.91 |
| #6 U-mean | −22.85 | −25.17 | −16.37 |
| #7 DLoss | +0.73 | +0.47 | +1.54 |

**訓練成本。** 在單張 GH200、BF16、批次 8 的條件下比較四個模型，加上 DLoss 後每步時間的平均增幅最多 4.4%（BTB3D），峰值已配置與保留記憶體的增幅最多 1.6% 與 2.9%；DLoss 只在訓練時使用，推論不增加計算。[(ref: main §4.2; Table 2)](https://arxiv.org/html/2610.30980v1#S4.T2)

## 結果

- **六個模型平均** — 加上 DLoss 後，GREEN 平均在 Merlin 測試集 +4.05、外部資料 +4.28，RadGraph-F1 平均 +3.82 與 +2.96；72 組模型－指標－測試集比較中 71 組上升，唯一下降的是 Merlin 模型在 Merlin 測試集的 F1-RG（−0.01）。[(ref: main §4.2; Table 1)](https://arxiv.org/html/2610.30980v1#S4.T1)
- **增益大小差很多** — 外部資料的 GREEN 增益從 RadFM 的 +0.86、Merlin 的 +1.24，到 SPECTRE 的 +14.03；Merlin 與 RadFM 在 12 個指標上的增益都在 1.24 分以內。[(ref: main Table 1)](https://arxiv.org/html/2610.30980v1#S4.T1)
- **不確定性** — 只在 BTB3D、Merlin 測試集上做了九組 seed 分析：GREEN 平均差 +0.0455（seed–study bootstrap 95% CI +0.0197 到 +0.0732）、RadGraph Complete +0.0795（+0.0203 到 +0.1451）；九組中 GREEN 與 RadGraph Complete 各有八組上升、BLEU-4 七組上升，seed 2718 的 GREEN 為 −0.0215，seed 2026 的 RadGraph Complete 為 −0.0611。作者明寫這些區間未做多重比較校正，也不能推及其他模型或外部資料。[(ref: main Appendix F; Table 6–7)](https://arxiv.org/html/2610.30980v1#A6.T7)
- **兩個組件缺一不可（在 fVLM 上）** — 只留 supported 或只留 unsupported 項，三個指標都比 CE 低；把 unsupported 項的 log-sum-exp 換成平均（U-mean）掉最多，GREEN −25.17%，且產生 1,423 個空白發現（2.52%），CE 只有 48 個（0.09%）。[(ref: main Table 3; Appendix G)](https://arxiv.org/html/2610.30980v1#A7)
- **質性範例** — 作者以四個 CT 研究的器官層級片段（Fig. 2）說明基線會寫出參考報告沒有的發現、也會漏掉臨床狀態更新，而加上 DLoss 的版本較少出現這兩類錯；這是挑選的範例，不是系統性的錯誤率統計。[(ref: main Fig. 2)](https://arxiv.org/html/2610.30980v1#S4.F2)

## 限制

作者自述的限制：[(ref: main §5 Limitations)](https://arxiv.org/html/2610.30980v1#S5)

- **只監督訓練報告裡出現過的概念** — 受控目標空間來自訓練報告，詞彙集合也只涵蓋訓練語料中出現的說法，不涵蓋所有同義改寫。
- **只有腹部 CT、只有自動指標** — 六個模型、兩個測試集都在腹部 CT；作者建議在 2D 胸片報告上測試並與放射科醫師判讀比較。

本書庫另外注意到：

- **沒有放射科醫師評讀** — GREEN 與 RadGraph-F1 都是以模型評分，作者在附錄也說明它們不等於放射科醫師審閱；「漏寫與錯寫的診斷變少」目前只由這兩個自動指標與挑選過的質性範例支持。[(ref: main Appendix E.2)](https://arxiv.org/html/2610.30980v1#A5.SS2)
- **主表沒有信賴區間** — Table 1 每個設定只訓練一次，九組 seed 分析也顯示同一個模型換 seed 時差值可正可負，因此單一模型、單次執行的小幅增益（例如 Merlin、RadFM 的 0.0x–1.x 分）難以和訓練變異區分。[(ref: main Appendix F; Table 7)](https://arxiv.org/html/2610.30980v1#A6.T7)
- **只對照 cross-entropy** — 比較對象是同條件的 CE 微調；論文在相關研究中提到的 unlikelihood training、token 重新加權、SAT-RRG 與強化學習獎勵等其他改訓練目標的做法，沒有一起放進實驗比較。[(ref: main §2)](https://arxiv.org/html/2610.30980v1#S2)
- **「支持／不支持」由參考報告決定** — 𝒟⁺／𝒟⁻ 由 LLM 從參考報告標註而來，報告漏寫的發現會被當成「不支持」；評估同樣以參考報告為準，因此量到的是「與參考報告一致的程度」，不是對影像的診斷正確率。[(ref: main §3.1)](https://arxiv.org/html/2610.30980v1#S3.SS1)
- **以器官發現為單位評分** — 模型一次生成一個器官的發現，指標也在器官發現層級計算，與整份報告的可讀性、跨器官一致性或印象段（impression）的品質不是同一件事。[(ref: main Appendix E.1)](https://arxiv.org/html/2610.30980v1#A5.SS1) [(ref: main Appendix E.2)](https://arxiv.org/html/2610.30980v1#A5.SS2)

## 與書庫其他文章的關係

RADAR 先用 TotalSegmentator 把腹部 CT 切成器官、再讓報告逐器官對齊做疾病分類，DLoss 也用同一套器官切分與器官層級的報告發現，但把它用在生成報告的訓練目標上，兩篇都在 Merlin 測試集上評估，fVLM 也同時出現在兩篇的比較中: [RADAR：把腹部 CT 拆成 18 個器官再對齊報告，通才模型能到專家水準嗎？](2026-09-21-radar-abdominal-ct-generalist.md)

EviGround-CT 在 CT 報告寫完之後，用 3D 驗證器替每個陽性發現句找影像證據，DLoss 則在訓練時直接壓低參考報告不支持的診斷詞機率，兩篇分別從「生成後查核」與「訓練時約束」處理 CT 報告裡沒有根據的發現: [EviGround-CT：LLM 寫的胸部 CT 報告逐句送去 3D 定位查核，整句當查詢讓 137 個生成發現中有標註支持的比例從 0.263 升到 0.365，但參考遮罩不完整、評估只有 100 例](2026-10-30-eviground-ct-sentence-grounding-report-verification.md)

CPVB-RG 靠改影像端的融合模組提升胸片報告的 F1RadGraph，DLoss 則完全不動架構、只換訓練目標，兩篇代表報告生成改進的「改模型」與「改損失」兩條路，也都以 RadGraph 類指標衡量臨床內容: [CPVB-RG：把前後兩張胸片的「變化」與「共同結構」分開處理再寫報告，82M 解碼器對最接近的 prior-aware 基線 PriorRG 在 F1RadGraph 多 0.0090、VLScore 多 0.0582](2026-10-22-cpvb-rg-prior-aware-cxr-report-generation.md)

## 實務的啟發

- **可借用的做法：把「該寫」與「不該寫」拆成兩個不同形狀的約束** — 對已在微調報告生成模型的團隊，DLoss 的設計（noisy-OR 要求至少出現一次、log-sum-exp 壓住任何一處尖峰）不改架構、推論零成本、訓練成本增幅在 5% 以內，程式碼也已公開，是低成本可試的選項；但本篇的證據是自動指標上的平均增益，要當成「待自己資料驗證的訓練技巧」，不是已證實能減少臨床錯誤的做法。[(ref: main Table 1–2)](https://arxiv.org/html/2610.30980v1#S4.T2)
- **本書庫的讀法：大解碼器上的增益很小** — Table 1 中 GREEN 增益最大的 fVLM（Merlin 測試集 +8.99）與 SPECTRE（外部 +14.03）都用 Qwen2.5-0.5B 解碼器，而 7B 的 Merlin 與 13B 的 RadFM 在 GREEN 上只多 0.50–1.24 分；但 8B 的 BTB3D 的 RadGraph-F1 在 Merlin 測試集也多了 +9.18，型態並不單純。論文沒有分析這一點，各模型之間的視覺編碼器、LoRA 設定與 λ 也都不同，所以只能當作值得在自己模型上檢查的線索。[(ref: main Table 1)](https://arxiv.org/html/2610.30980v1#S4.T1) [(ref: main Appendix E.1)](https://arxiv.org/html/2610.30980v1#A5.SS1)
- **要先有一套概念目錄** — DLoss 需要一個受控的診斷概念空間與每個概念的同義詞集合，品質取決於 LLM 標註與人工整理；中文或其他語言的報告、或器官以外的組織方式，都需要先重建這一層，論文沒有提供建置成本。[(ref: main §3.1)](https://arxiv.org/html/2610.30980v1#S3.SS1)
- **評估要補上人** — 若要宣稱「漏診與誤寫變少」，需要放射科醫師對錯誤類型計數，並報告多 seed 的變異；只看 GREEN、RadGraph 的平均分數，無法分辨增益來自臨床內容還是用詞更貼近參考報告。

## References

- **main** — Kolton I, Li W, Zhou Z, Ćwikła JB, Sitek A, Bassi PRAS, Płotka S. *Diagnostic Loss: Asymmetric Supervision for Radiology Report Generation*. arXiv:2610.30980v1, 2026. [abstract](https://arxiv.org/abs/2610.30980v1)；[HTML v1](https://arxiv.org/html/2610.30980v1)；[PDF v1](https://arxiv.org/pdf/2610.30980v1)；DOI [10.48550/arXiv.2610.30980](https://doi.org/10.48550/arXiv.2610.30980)
  - 深鏈：[§1](https://arxiv.org/html/2610.30980v1#S1)、[Fig. 1](https://arxiv.org/html/2610.30980v1#S1.F1)、[§2](https://arxiv.org/html/2610.30980v1#S2)、[§3.1](https://arxiv.org/html/2610.30980v1#S3.SS1)、[§3.2](https://arxiv.org/html/2610.30980v1#S3.SS2)、[Algorithm 1](https://arxiv.org/html/2610.30980v1#alg1)、[§4.1](https://arxiv.org/html/2610.30980v1#S4.SS1)、[§4.2](https://arxiv.org/html/2610.30980v1#S4.SS2)、[Table 1](https://arxiv.org/html/2610.30980v1#S4.T1)、[Table 2](https://arxiv.org/html/2610.30980v1#S4.T2)、[Fig. 2](https://arxiv.org/html/2610.30980v1#S4.F2)、[Table 3](https://arxiv.org/html/2610.30980v1#S4.T3)、[§5](https://arxiv.org/html/2610.30980v1#S5)、[Acknowledgments](https://arxiv.org/html/2610.30980v1#Sx1)、[Ethics statement](https://arxiv.org/html/2610.30980v1#Sx1.SSx2)、[Reproducibility statement](https://arxiv.org/html/2610.30980v1#Sx1.SSx3)、[Appendix A](https://arxiv.org/html/2610.30980v1#A1)、[Table 4](https://arxiv.org/html/2610.30980v1#A1.T4)、[Appendix B](https://arxiv.org/html/2610.30980v1#A2)、[Appendix C](https://arxiv.org/html/2610.30980v1#A3)、[Appendix E.1](https://arxiv.org/html/2610.30980v1#A5.SS1)、[Table 5](https://arxiv.org/html/2610.30980v1#A5.T5)、[Appendix E.2](https://arxiv.org/html/2610.30980v1#A5.SS2)、[Appendix F](https://arxiv.org/html/2610.30980v1#A6)、[Table 6](https://arxiv.org/html/2610.30980v1#A6.T6)、[Table 7](https://arxiv.org/html/2610.30980v1#A6.T7)、[Appendix G](https://arxiv.org/html/2610.30980v1#A7)
- **code** — gmum/DLoss. [https://github.com/gmum/DLoss](https://github.com/gmum/DLoss)

[Home](../) · [AI Papers](./)
