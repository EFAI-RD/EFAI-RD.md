---
parent: AI Basics
nav_order: 3
title: "LFM：名字來自液態時間常數網路，主幹卻是閘控短卷積"
category: ai-basics
date: 2026-11-18
catalog_id: "topic:liquid-foundation-models"
editors:
  - "Clara"
refs:
  ltc:
    title: "Liquid Time-constant Networks"
    url: "https://arxiv.org/abs/2006.04439"
  cfc:
    title: "Closed-form continuous-time neural networks"
    url: "https://www.nature.com/articles/s42256-022-00556-7"
  cfc_arxiv:
    title: "Closed-form Continuous-time Neural Models"
    url: "https://arxiv.org/abs/2106.13898"
  liquid_s4:
    title: "Liquid Structural State-Space Models"
    url: "https://arxiv.org/abs/2209.12951"
  star:
    title: "STAR: Synthesis of Tailored Architectures"
    url: "https://arxiv.org/abs/2411.17800"
  lfm1:
    title: "Liquid Foundation Models: Our First Series of Generative AI Models"
    url: "https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models"
  lfm2_blog:
    title: "Introducing LFM2: The Fastest On-Device Foundation Models on the Market"
    url: "https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models"
  lfm2:
    title: "LFM2 Technical Report"
    url: "https://arxiv.org/abs/2511.23404"
    html_url: "https://arxiv.org/html/2511.23404v1"
  lfm25:
    title: "Introducing LFM2.5: The Next Generation of On-Device AI"
    url: "https://www.liquid.ai/blog/introducing-lfm2-5-the-next-generation-of-on-device-ai"
  lfm3:
    title: "Introducing LFM3: Every Modality for Specialized Intelligence"
    url: "https://www.liquid.ai/blog/lfm3"
  models:
    title: "Liquid Foundation Models (model catalogue)"
    url: "https://www.liquid.ai/models"
  ecg:
    title: "Efficient Edge-AI Models for Robust ECG Abnormality Detection on Resource-Constrained Hardware"
    url: "https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/"
status: published
skill_version: "write-ai-basic@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Basics](./)

# LFM：名字來自液態時間常數網路，主幹卻是閘控短卷積

## 來源

- 本文定位：常青概念文，不是單篇論文筆記。說明 Liquid AI 的 **Liquid Foundation Models（LFM）** 從哪一條研究線來、現在的架構實際長什麼樣，以及讀醫療 AI 文獻時該怎麼看待這類裝置端小模型。
- 觸發的 papers：書庫的醫療 VLM 與 3D CT 文章多半以 Transformer 或 Mamba 為主幹；LFM 是另一條「為裝置端搜尋架構」的路線，本篇補上它的譜系語言。
- 核心 landmark
  - [Liquid Time-constant Networks（LTC）](https://arxiv.org/abs/2006.04439)（Hasani、Lechner、Amini、Rus、Grosu；arXiv 2020，AAAI-21 接受）
  - [Closed-form continuous-time neural networks（CfC）](https://www.nature.com/articles/s42256-022-00556-7)（Hasani 等；Nature Machine Intelligence 4, 992–1003，2022；arXiv 版 [2106.13898](https://arxiv.org/abs/2106.13898)）
  - [Liquid Structural State-Space Models（Liquid-S4）](https://arxiv.org/abs/2209.12951)（Hasani 等；arXiv 2022）
  - [STAR: Synthesis of Tailored Architectures](https://arxiv.org/abs/2411.17800)（Thomas、Parnichkun、Amini、Massaroli、Poli；arXiv 2024）
  - [LFM 第一代公告](https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models)（Liquid AI，2024-09-30）
  - [LFM2 Technical Report](https://arxiv.org/abs/2511.23404)（Liquid AI Team；arXiv 2025-11-28）與 [LFM2 公告](https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models)（2025-07-10）
  - [LFM2.5 公告](https://www.liquid.ai/blog/introducing-lfm2-5-the-next-generation-of-on-device-ai)（2026-01-05）與 [LFM3 公告](https://www.liquid.ai/blog/lfm3)（2026-10-27）
- 證據邊界：LFM2 的架構與速度以技術報告為準；LFM 第一代、LFM2.5、LFM3 只有官方公告，沒有同行審查的技術報告，文中凡出自公告者皆為廠商自述。醫療相關段落只引用有全文可核對的研究。

**編輯：** Clara

LFM 的名字來自 MIT 團隊的液態時間常數網路（LTC），但 Liquid AI 以裝置端延遲與記憶體為目標做架構搜尋後，LFM2 與 LFM3 的大多數層是閘控短卷積，再配少量注意力層，而不是逐步求解微分方程的液態神經元。[(ref: lfm2 §2.1)](https://arxiv.org/html/2511.23404v1#S2.SS1) [(ref: lfm3)](https://www.liquid.ai/blog/lfm3)

## 流程

![左右兩欄圖。左欄標題「Lineage: from liquid neurons to Liquid Foundation Models」，八個圓角框由上而下以向下箭頭相連，左側標年份：前三個淺藍底、深藍實線框為「2020 LTC (Hasani et al., AAAI-21)：linear 1st-order ODE + nonlinear gates; input-dependent ('liquid') time constants」、「2021-22 CfC (Nature Mach. Intell. 2022)：closed-form approx. of LTC dynamics; no numerical ODE solver needed」、「2022 Liquid-S4：LTC-style input-dependent transition inside an S4 state-space model」；後五個淺橘底、橘色實線框為「2024 STAR (LIV operators)：linear input-varying search space; evolutionary architecture search」、「2024-09 LFM 1st gen (1B / 3B / 40B MoE)：weights not released; now deprecated」、「2025-07 LFM2 family (350M-8.3B, open weights)：gated short convolutions + few GQA blocks; hardware-in-the-loop search on phone/laptop CPUs」、「2026-01 LFM2.5：same LFM2 backbone; 28T tokens + RL post-training」、「2026-10 LFM3 (~2B, open weights)：tri-hybrid: short conv + sliding-window + global attention; 256K context (text)」；左欄下方小字說明藍色為學術的連續時間／狀態空間路線、橘色為 Liquid AI 的架構搜尋與 LFM 產品。右上為水平堆疊長條圖，標題「Most LFM layers are short convolutions, not ODE cells」，橫軸「number of sequence-mixing layers」0–30：LFM2-1.2B (16 layers) 為橘色 10 加深藍 6；LFM2-2.6B (30 layers) 為橘色 22 加深藍 8；LFM3-1.7B (24 layers) 為橘色 13、淺藍 5、深藍 6；圖例在下方：橘色 gated short convolution、淺藍 sliding-window attention、深藍 global attention (GQA)。右下為淺灰底、灰色虛線框，標題「Medical touchpoints in the reviewed sources」，列出五點：CfC: PhysioNet 2012 ICU mortality; 160x faster training than ODE-RNN；Liquid-S4: BIDMC vital signs dataset among benchmarks；ECG study (2024): ConvLSTM2D + LTC/CfC (NCP) on STM32F746G; external CPSC test, mean F1 69.9% (LTC) / 72.1% (CfC)；LFM2-VL: trained without grounding signals (authors' limitation)；LFM tech report / LFM3 post: no medical evaluation reported。右下角小字列出出處：arXiv:2006.04439, 2106.13898, 2209.12951, 2411.17800, 2511.23404; Liquid AI LFM / LFM2 / LFM2.5 / LFM3 posts; Huang et al. 2024 (PMC11371854)。](assets/liquid-foundation-models-lineage.png)

*圖：本書庫依各 landmark 原文自繪，非重製原圖。左欄是從 LTC 到 LFM3 的譜系；右上的層數取自 [LFM2 技術報告 Table 1](https://arxiv.org/html/2511.23404v1#S2.T1)（總層數減去注意力層數）與 [LFM3 公告](https://www.liquid.ai/blog/lfm3)；右下是本文引用來源中出現的醫療相關資料點。*

## 為何需要

Transformer 的自注意力讓每個 token 都能看見整段上下文，代價是推論時要保存隨上下文成長的 KV cache。在手機、筆電或嵌入式裝置上，單一請求（batch 1）的首字延遲、逐字解碼速度與峰值記憶體，往往比伺服器上的吞吐量更決定能不能用。LFM2 技術報告把設計目標直接寫成「edge-first」：在 CPU 與 NPU 的延遲與峰值記憶體預算內，盡量提高下游品質。[(ref: lfm2 §2.1)](https://arxiv.org/html/2511.23404v1#S2.SS1)

另一方面，LTC 這條研究線原本處理的是連續時間的序列：輸入隨時間到來、取樣不規則，系統狀態要隨輸入調整反應速度。這類問題在醫療很常見，例如 ICU 生命徵象與穿戴裝置訊號。[(ref: cfc PhysioNet)](https://www.nature.com/articles/s42256-022-00556-7#Sec22) LFM 的故事，就是這條研究線如何被併入「為裝置端找最佳架構」的工程問題。

## 核心概念

1. **Liquid time-constant（液態時間常數）** — LTC 把網路建成一階線性動態系統，再以非線性閘門調變，使時間常數隨輸入與隱藏狀態改變；輸出需要數值微分方程求解器計算。作者主張這類模型行為有界、表達力高於一般 neural ODE。[(ref: ltc)](https://arxiv.org/abs/2006.04439)
2. **Closed-form 近似** — CfC 對 LTC 動態中原本沒有閉式解的積分給出緊的近似，時間直接出現在公式裡，不再需要數值求解器；作者報告訓練與推論比微分方程版本快一到五個數量級。[(ref: cfc_arxiv)](https://arxiv.org/abs/2106.13898)
3. **Input-dependent 狀態轉移** — Liquid-S4 把 LTC 式、依輸入改變的狀態轉移放進 S4 狀態空間模型，同時保留卷積式的平行計算路徑。[(ref: liquid_s4)](https://arxiv.org/abs/2209.12951)
4. **LIV operator（linear input-varying）** — 權重由輸入即時生成的線性算子；Liquid AI 用這個框架把卷積、遞迴、注意力等層放進同一個可搜尋的設計空間，STAR 則在這個空間上以演化演算法搜尋架構。[(ref: lfm2_blog)](https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models) [(ref: star)](https://arxiv.org/abs/2411.17800)
5. **Gated short convolution** — LFM2 的主力區塊：輸入經線性投影分成兩個閘門與一份特徵，先乘上閘門、做核長 3 的 depthwise 短卷積、再乘上第二個閘門後輸出。官方部落格把它描述為「有限時間內收斂到零的一階線性系統」，這是它與液態網路在概念上的連結。[(ref: lfm2 §2.2)](https://arxiv.org/html/2511.23404v1#S2.SS2) [(ref: lfm2_blog)](https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models)
6. **Hardware-in-the-loop 架構搜尋** — 候選架構直接在目標裝置（Galaxy S24 Ultra 與 AMD Ryzen HX 370，llama.cpp／ExecuTorch）上量首字延遲、解碼延遲與峰值記憶體，超出預算者淘汰，再以 50 項以上內部評測挑品質—延遲—記憶體的 Pareto 前緣。[(ref: lfm2 §2.1)](https://arxiv.org/html/2511.23404v1#S2.SS1)

## 發展譜系與 landmark

| 年份 | Landmark | 據原文的主要貢獻 |
|---|---|---|
| 2020 | [LTC](https://arxiv.org/abs/2006.04439) | 以非線性閘門調變一階線性動態系統，時間常數隨輸入改變；在多個時間序列預測實驗與經典及現代 RNN 比較。[(ref: ltc)](https://arxiv.org/abs/2006.04439) |
| 2021–22 | [CfC](https://www.nature.com/articles/s42256-022-00556-7) | LTC 動態的閉式近似，免數值求解器；PhysioNet 2012 ICU 死亡預測上表現與基線相當，訓練時間比 ODE-RNN 快 160 倍。[(ref: cfc PhysioNet)](https://www.nature.com/articles/s42256-022-00556-7#Sec22) |
| 2022 | [Liquid-S4](https://arxiv.org/abs/2209.12951) | LTC 式狀態轉移併入 S4；Long Range Arena 平均 87.32%，Speech Commands 96.78% 且參數比 S4 少 30%；評測涵蓋影像、文字、音訊與醫療時間序列。[(ref: liquid_s4)](https://arxiv.org/abs/2209.12951) |
| 2024 | [STAR](https://arxiv.org/abs/2411.17800) | 以 LIV 理論建立階層化的架構搜尋空間，用演化演算法同時最佳化品質與效率指標。[(ref: star)](https://arxiv.org/abs/2411.17800) |
| 2024-09 | [LFM 第一代](https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models) | 1.3B、3.1B 兩個 dense 模型與 40.3B MoE（啟用 12B）；公告稱由動態系統、訊號處理與數值線性代數的計算單元構成，當時不釋出權重，現已標示 deprecated。[(ref: lfm1)](https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models) |
| 2025 | [LFM2](https://arxiv.org/abs/2511.23404) | 350M–8.3B（含 8.3B 總參數、1.5B 啟用的 MoE），32K 上下文，開放權重；主幹為閘控短卷積加少量 GQA，報告稱 CPU 上 prefill 與 decode 最多快 2 倍；另有 LFM2-VL、LFM2-Audio、LFM2-ColBERT。[(ref: lfm2)](https://arxiv.org/abs/2511.23404) |
| 2026-01 | [LFM2.5](https://www.liquid.ai/blog/introducing-lfm2-5-the-next-generation-of-on-device-ai) | 沿用 LFM2 的裝置端架構，預訓練由 10T 增加到 28T tokens，並加入強化學習後訓練（廠商自述）。[(ref: lfm25)](https://www.liquid.ai/blog/introducing-lfm2-5-the-next-generation-of-on-device-ai) |
| 2026-10 | [LFM3](https://www.liquid.ai/blog/lfm3) | 「tri-hybrid」：24 層中 13 層閘控短卷積（核長 7）、5 層 256-token 視窗的 sliding-window attention、6 層全域注意力；22T tokens 預訓練，文字模型 256K 上下文，首批六個約 2B 的文字、視覺、音訊、omni 與 decision 模型，開放權重（廠商自述）。[(ref: lfm3)](https://www.liquid.ai/blog/lfm3) |

**LFM2 的架構搜尋實際選了什麼。** 候選區塊包含 sliding-window attention、多種 linear attention，以及 S4、Liquid-S4、S5、Mamba、Mamba2 等狀態空間區塊和 CfC。在同樣的裝置端效能預算下，搜尋反覆選出的是「大多數為閘控短卷積、少數為 GQA」的最簡混合；作者寫到，再加上 linear attention、狀態空間或其他卷積算子不會提高整體品質，通常還讓裝置端指標變差。[(ref: lfm2 §2.1)](https://arxiv.org/html/2511.23404v1#S2.SS1)

**LFM2 的層數配置**（節錄自技術報告 Table 1）[(ref: lfm2 Table 1)](https://arxiv.org/html/2511.23404v1#S2.T1)

| Model | Params（總／啟用） | Layers | Attn. Blocks | Conv k | 上下文 |
|---|---|---|---|---|---|
| LFM2-350M | 350M／— | 16 | 6 | 3 | 32,768 |
| LFM2-700M | 700M／— | 16 | 6 | 3 | 32,768 |
| LFM2-1.2B | 1.2B／— | 16 | 6 | 3 | 32,768 |
| LFM2-2.6B | 2.6B／— | 30 | 8 | 3 | 32,768 |
| LFM2-8B-A1B | 8.3B／1.5B | 24 | 6 | 3 | 32,768 |

*上下文長度出自 [§2.2](https://arxiv.org/html/2511.23404v1#S2.SS2) 與摘要；LFM2-8B-A1B 除前兩層外皆為 MoE（32 個 expert、啟用 4 個）。*

**裝置端速度的一個例子。** 在 Galaxy S25（Snapdragon 8 Elite，llama.cpp Q4_0，batch 1）上，LFM2-700M 的 1K prompt prefill 為每秒 522 tokens、Qwen3-0.6B 為 318；1K 前綴後的 decode 為每秒 104.2 對 76.7 tokens。[(ref: lfm2 Table 2)](https://arxiv.org/html/2511.23404v1#S2.T2) 這些數字由 Liquid AI 自行量測。

## 與醫療 AI 的連結

**LFM 本身。** 本文查閱的 LFM2 技術報告與 LFM3 公告都沒有醫療任務的評估。技術報告提到的醫療相關內容只有一句：LFM2-ColBERT 目前以一般領域檢索訓練，生醫文獻等專門領域「可能」受益於領域調適。[(ref: lfm2 §9.2)](https://arxiv.org/html/2511.23404v1#S9.SS2) 視覺模型方面，作者自承 LFM2-VL 訓練時沒有 bounding box、mask 等 grounding 訊號，預期細部定位較弱。[(ref: lfm2 §9.2)](https://arxiv.org/html/2511.23404v1#S9.SS2) LFM2-VL 是以 SigLIP2 影像編碼器經 PixelUnshuffle 與 MLP connector 接上 LFM2 語言主幹。[(ref: lfm2 §5.1)](https://arxiv.org/html/2511.23404v1#S5.SS1)

**液態網路這條研究線。** 醫療資料點來自上游研究，而不是 LFM：

- **ICU 時間序列** — CfC 在 PhysioNet Challenge 2012（約 8,000 位 ICU 病人、入院後 48 小時、37 項特徵、不規則取樣）預測死亡，作者稱表現與基線相當，訓練時間比 ODE-RNN 快 160 倍、比 continuous latent models 快 220 倍。[(ref: cfc PhysioNet)](https://www.nature.com/articles/s42256-022-00556-7#Sec22)
- **生命徵象** — Liquid-S4 的評測包含醫療時間序列，作者在論文中指的是 BIDMC vital signs 資料集，並稱在該資料集的所有設定（all modes）上達到最佳。[(ref: liquid_s4 PDF)](https://arxiv.org/pdf/2209.12951v1)
- **嵌入式 ECG** — 雪梨大學團隊以 ConvLSTM2D 前接 LTC 或 CfC 神經元（以 neural circuit policy 排列）偵測六種 ECG 異常，部署在 STM32F746G 開發板（340 KB RAM），模型功耗約 137.4 mW、10 秒 ECG 推論約 1 秒；在外部 CPSC 2018 的四類測試上平均 F1 為 69.9%（LTC）與 72.1%（CfC）。[(ref: ecg 部署)](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/#Sec23) [(ref: ecg Table 4–5)](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/#Sec24) 不過論文的比較表只列其他研究各自報告的 F1，沒有在同一資料上訓練非液態基線作對照。[(ref: ecg Table 6)](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/#Tab6)

**本書庫的解讀。** 對醫療場域而言，LFM 這類模型值得注意的是「在院內裝置或本機上跑」：資料不必離開設備，延遲與記憶體可以在部署硬體上直接量。但目前沒有可引用的醫療評估，能說的只是它提供了一種裝置端選項，不是臨床能力的證據。

## 常見誤解

- **「LFM 是用 LTC 液態神經元堆出來的」** — LFM2 的搜尋空間裡確實有 CfC 與 Liquid-S4，但最後選出的主幹是閘控短卷積加少量 GQA；LFM3 也仍以閘控短卷積占一半以上層數。[(ref: lfm2 §2.1)](https://arxiv.org/html/2511.23404v1#S2.SS1) [(ref: lfm3)](https://www.liquid.ai/blog/lfm3) 「Liquid」描述的是研究血緣與依輸入調整的設計理念，技術報告的寫法是 LTC 依輸入調整有效時間感受野的能力，啟發了 LFM2 對局部與全域上下文的處理方式。[(ref: lfm2 §8.2)](https://arxiv.org/html/2511.23404v1#S8.SS2)
- **「LFM 的記憶體不隨上下文成長」** — 「near-constant inference time and memory」是第一代 LFM 公告的說法。[(ref: lfm1)](https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models) LFM2 與 LFM3 都保留全域注意力層；技術報告的說法是長上下文的峰值記憶體比注意力較多的配置低，與 KV cache 減少一致，而不是不再成長。[(ref: lfm2 §2.1)](https://arxiv.org/html/2511.23404v1#S2.SS1)
- **「CPU 上快 2 倍，代表在任何硬體上都比較快」** — 作者明說架構搜尋與部署配方是針對 batch 1、少數手機與筆電 CPU 與特定量化格式調的，不主張在大批次伺服器或特定加速器上也最佳。[(ref: lfm2 §9.2)](https://arxiv.org/html/2511.23404v1#S9.SS2)
- **「開放權重就等於可以任意商用」** — 官方模型頁寫的是：下載、執行、微調（含商用）免費，條件是公司年營收未超過 1,000 萬美元，超過者要另看授權與定價；LFM 第一代則根本沒有釋出權重。[(ref: models)](https://www.liquid.ai/models) [(ref: lfm1)](https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models)
- **「小模型評測分數高，就能直接用在臨床」** — 作者自承 LFM2 受容量限制，最適合短到中等上下文、任務導向的裝置端工作。[(ref: lfm2 §9.2)](https://arxiv.org/html/2511.23404v1#S9.SS2) 醫療用途需要自己的驗證。

## 與書庫其他文章的關係

LFM2-VL 以 SigLIP2 編碼器接上 LFM2 語言主幹，屬於醫療 VLM 譜系中 LLaVA 式的對話路線；技術報告自承訓練未使用 grounding 訊號，正好落在該譜系強調的「有定位報告」分岔之外: [醫療視覺語言模型：從 CLIP 對齊到有定位報告](medical-vlm.md)

MedHiVE 的 3D CT 編碼器以 Mamba 區塊為主；LFM2 的硬體在迴路搜尋把 Mamba、S4、Liquid-S4、CfC 等序列區塊都列為候選，在手機與筆電 CPU 的預算下卻選出閘控短卷積加少量注意力，提醒同一類序列算子的取捨會隨硬體目標改變: [MedHiVE：報告只進預訓練，有對齊的器官多 2.7、其餘只多 0.7](../ai-papers/2026-11-11-medhive-hierarchical-moe-3d-ct-vlm.md)

## 實務的啟發

- **在部署硬體上量，而不是看參數量** — LFM2 的做法是把首字延遲、解碼延遲與峰值記憶體在目標裝置上實測後再選架構；評估院內裝置端模型時，這是可以借用的量測方法，比只看參數量或伺服器吞吐量更貼近實際使用。
- **把廠商自述與可核對的報告分開** — LFM2 有技術報告可核對，LFM2.5 與 LFM3 目前只有公告；選型時應以能重現的數字為準，並在自己的硬體與資料上重測。
- **醫療用途要自己補驗證** — LFM 目前沒有可引用的醫療評估，LFM2-VL 也沒有 grounding 訓練；若考慮用在影像或病歷相關的裝置端任務，需要另做任務層級的評估與定位檢查，並先確認授權門檻。
- **液態網路仍是時間序列的候選** — CfC 在 ICU 不規則時間序列上的速度優勢、以及嵌入式 ECG 的部署經驗，讓這條研究線值得放進生理訊號模型的比較清單；但現有醫療證據規模小，嵌入式 ECG 研究也缺少同資料的非液態基線，宜視為待驗證的選項。

## References

- `ltc` — Hasani R, Lechner M, Amini A, Rus D, Grosu R. *Liquid Time-constant Networks*. arXiv:2006.04439（AAAI-21）. [https://arxiv.org/abs/2006.04439](https://arxiv.org/abs/2006.04439)
- `cfc` — Hasani R, Lechner M, Amini A, Liebenwein L, Ray A, Tschaikowski M, Teschl G, Rus D. *Closed-form continuous-time neural networks*. Nature Machine Intelligence 4, 992–1003 (2022). [https://www.nature.com/articles/s42256-022-00556-7](https://www.nature.com/articles/s42256-022-00556-7)
  - 深鏈：[PhysioNet Challenge](https://www.nature.com/articles/s42256-022-00556-7#Sec22)
- `cfc_arxiv` — 同上 arXiv 版 *Closed-form Continuous-time Neural Models*. [https://arxiv.org/abs/2106.13898](https://arxiv.org/abs/2106.13898)
- `liquid_s4` — Hasani R, Lechner M, Wang T-H, Chahine M, Amini A, Rus D. *Liquid Structural State-Space Models*. arXiv:2209.12951. [https://arxiv.org/abs/2209.12951](https://arxiv.org/abs/2209.12951)
  - 全文：[PDF v1](https://arxiv.org/pdf/2209.12951v1)
- `star` — Thomas AW, Parnichkun R, Amini A, Massaroli S, Poli M. *STAR: Synthesis of Tailored Architectures*. arXiv:2411.17800. [https://arxiv.org/abs/2411.17800](https://arxiv.org/abs/2411.17800)
- `lfm1` — Liquid AI. *Liquid Foundation Models: Our First Series of Generative AI Models*. 2024-09-30. [https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models](https://www.liquid.ai/blog/liquid-foundation-models-our-first-series-of-generative-ai-models)
- `lfm2_blog` — Liquid AI. *Introducing LFM2: The Fastest On-Device Foundation Models on the Market*. 2025-07-10. [https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models](https://www.liquid.ai/blog/liquid-foundation-models-v2-our-second-series-of-generative-ai-models)
- `lfm2` — Liquid AI Team. *LFM2 Technical Report*. arXiv:2511.23404. [https://arxiv.org/abs/2511.23404](https://arxiv.org/abs/2511.23404)
  - 深鏈：[§2.1](https://arxiv.org/html/2511.23404v1#S2.SS1)、[§2.2](https://arxiv.org/html/2511.23404v1#S2.SS2)、[Table 1](https://arxiv.org/html/2511.23404v1#S2.T1)、[Table 2](https://arxiv.org/html/2511.23404v1#S2.T2)、[§5.1](https://arxiv.org/html/2511.23404v1#S5.SS1)、[§8.2](https://arxiv.org/html/2511.23404v1#S8.SS2)、[§9.2](https://arxiv.org/html/2511.23404v1#S9.SS2)
- `lfm25` — Liquid AI. *Introducing LFM2.5: The Next Generation of On-Device AI*. 2026-01-05. [https://www.liquid.ai/blog/introducing-lfm2-5-the-next-generation-of-on-device-ai](https://www.liquid.ai/blog/introducing-lfm2-5-the-next-generation-of-on-device-ai)
- `lfm3` — Liquid AI. *Introducing LFM3: Every Modality for Specialized Intelligence*. 2026-10-27. [https://www.liquid.ai/blog/lfm3](https://www.liquid.ai/blog/lfm3)
- `models` — Liquid AI. *Liquid Foundation Models*（模型與授權頁）. [https://www.liquid.ai/models](https://www.liquid.ai/models)
- `ecg` — Huang Z, Herbozo Contreras LF, Leung WH, Yu L, Truong ND, Nikpour A, Kavehei O. *Efficient Edge-AI Models for Robust ECG Abnormality Detection on Resource-Constrained Hardware*. J Cardiovasc Transl Res. 2024;17(4):879–892. doi:10.1007/s12265-024-10504-y. [https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/)
  - 深鏈：[Model Deployments on Micro-controller](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/#Sec23)、[Generalization of Models](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/#Sec24)、[Table 6](https://pmc.ncbi.nlm.nih.gov/articles/PMC11371854/#Tab6)

[Home](../) · [AI Basics](./)
