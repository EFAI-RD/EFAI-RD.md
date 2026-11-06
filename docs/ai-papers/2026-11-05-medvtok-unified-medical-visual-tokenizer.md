---
parent: AI Papers
nav_order: 4
title: "MedVTok：影像任務平均領先，接上 LLM 的 VQA 只多 1.1 分"
catalog_id: "arxiv:2610.35842"
editors:
  - "Clare"
refs:
  main:
    title: "MedVTok: A General-Purpose Medical Visual Tokenizer"
    url: "https://arxiv.org/abs/2610.35842v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# MedVTok：影像任務平均領先，接上 LLM 的 VQA 只多 1.1 分

## 來源

- 團隊：Fudan University、Shanghai Innovation Institute、Stanford University School of Medicine、Shanghai Artificial Intelligence Laboratory、Monash University、Shanghai Jiao Tong University 與 Ant Group 的 Ant Healthcare；作者欄共 21 位，第一作者 Chenglong Ma（前四位標註同等貢獻），最後兩位以 † 標註的是 Junjun He 與 Hongming Shan。[(ref: main title block)](https://arxiv.org/html/2610.35842v1)
- 論文：*MedVTok: A General-Purpose Medical Visual Tokenizer*，arXiv:2610.35842v1（eess.IV；另列 cs.CV），2026-10-26 提交，目前只有 v1；arXiv 頁註記 NeurIPS 2026；授權為 CC BY 4.0。[(ref: abstract)](https://arxiv.org/abs/2610.35842v1)
- 識別碼：arXiv [2610.35842](https://arxiv.org/abs/2610.35842v1)；DOI [10.48550/arXiv.2610.35842](https://doi.org/10.48550/arXiv.2610.35842)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2610.35842v1)、[PDF v1](https://arxiv.org/pdf/2610.35842v1)；專案頁 [masaaki-75.github.io/medvtok](https://masaaki-75.github.io/medvtok)。
- 程式與權重：論文寫明程式碼與模型權重「將」以 Apache 2.0 授權釋出，並聲明僅供研究使用。[(ref: main Appendix B.2)](https://arxiv.org/html/2610.35842v1#A2.SS2) [(ref: main Appendix D)](https://arxiv.org/html/2610.35842v1#A4)
- 研究性質：方法論文，不是 pilot；核心方法（Slice Differential Regularization 與 Multi-Expert Representation Alignment）都已實作並訓練完成，所有下游評估都凍結 tokenizer 進行；VQA 與報告生成以三個 random seed 報告平均與 95% 信賴區間，沒有臨床讀者研究。[(ref: main §4.2)](https://arxiv.org/html/2610.35842v1#S4.SS2) [(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)
- 證據邊界：本文數值以 arXiv HTML v1 的表格與正文為準；Fig. 5 消融結果只畫在圖上，本文不從圖面讀數引述。

**編輯：** Clare

MedVTok 把 2D 影像與 3D 體積、九種成像模態放進同一個凍結的視覺 tokenizer，在重建、分類、檢索、分割與合成的平均分數上領先比較對象，但接上 LLM 後，VQA 平均準確率只比前一個醫學統一 tokenizer MedITok 多 1.09 個百分點，CT 報告生成的 GREEN 平均多 0.027。[(ref: main Table 5)](https://arxiv.org/html/2610.35842v1#S4.T5) [(ref: main Table 6)](https://arxiv.org/html/2610.35842v1#S4.T6)

## 流程

![MedVTok 訓練與凍結評估的示意圖，最上方標題為 MedVTok: training a unified 2D/3D medical visual tokenizer, then evaluating it frozen。上排由左到右：淺藍色「Input」方框（2D image (T = 1) or 3D volume (T > 1)；Training corpus: 28,769,502 images + 70,144 volumes, 9 imaging modalities）以箭頭連到淺藍色「Encoder E」方框（Non-overlapping patches with position coordinates; mixed 2D/3D batches；Transformer + RoPE -> per-patch tokens h；KL term (Gaussian latent)）。Encoder E 以兩支箭頭分別連到右上淺橘色「Structural fidelity」方框（Decoder D reconstructs input；L_R: L1 + L2 + LPIPS + adversarial；L_SliDR: 1st/2nd-order slice differences (3D only)）與其下方淺綠色「Clinical semantics: MERA」方框（Aggregation head f -> r；L_shared: contrastive to projected expert features；L_expert: cosine in each expert's own space）。最右側淺紫色「Frozen expert encoders」方框列出 DermLIP (dermoscopy)、RetCLIP (fundus)、Conch (pathology)、PeskaVLP (endoscopy)、MedImageInsight (CT, MR, US, X-ray, other)、Spectre (CT 3D)*、HLIP (MR 3D)*，並註明 * Stage 2 only，以向左箭頭指向 MERA 方框。中間一條橫跨全寬的淺灰色「Two-stage training」長框：Stage 1: 2D images only (lambda_SliDR = 0)；Stage 2: alternating 2D and 3D batches, lambda_SliDR = 0.1; lambda_MERA = 1, lambda_KL = 1e-6，下方以一支向下箭頭連到下排。下排三個方框：淺藍色「Vision-only probes (frozen tokens)」（Reconstruction: PSNR / SSIM；Classification: k-NN accuracy；Retrieval: Recall@1；Segmentation: linear head, Dice；Synthesis: latent diffusion trained from scratch, FID）、淺綠色「VQA (LLaVA-Med setup)」（Frozen tokenizer -> 2-layer MLP -> Mistral-7B-Instruct + LoRA；6 benchmarks, LLM-as-judge (Qwen3-235B-A22B; GPT-5 re-score)；3 seeds, mean +/- 95% CI；Compared: PUMIT, MedVAE, MedITok）、淺綠色「CT report generation (LaMed)」（AMOS-MM: 1,287 train / 400 test CT-report pairs；Frozen tokenizer -> 3D avg pooling -> Llama-3.1-8B-Instruct + LoRA；BLEU, ROUGE-L, METEOR, RaTEScore, GREEN; 3 seeds；Compared: PUMIT, MedVAE-3D, MedITok）。](assets/medvtok-training-and-frozen-evaluation.png)

圖：本書庫依論文 §3、§4.1、Appendix A–C 的文字重繪的訓練與評估示意圖，只含設定與樣本數，不含結果數值，未複製論文原圖。[(ref: main §3)](https://arxiv.org/html/2610.35842v1#S3) [(ref: main Table 7)](https://arxiv.org/html/2610.35842v1#A1.T7) [(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)

## 背景／問題

視覺 tokenizer 是把影像轉成一串 token、交給多模態模型使用的前端。作者的出發點是：多模態醫療 AI 需要一個共同的視覺介面，把不同來源的影像證據編碼進同一個空間；而現有的醫學視覺 tokenizer 多半綁定單一維度（2D 或 3D）與單一模態，下游模型只好自己吸收跨模態適應的負擔。這是論文的動機前提，作者引用相關工作說明現況，但論文本身沒有實驗去比較「共用一個 tokenizer」與「各模態各用專屬編碼器」在病人層級多模態建模上的差異。[(ref: main §1)](https://arxiv.org/html/2610.35842v1#S1)

作者把建構通用 tokenizer 的難處拆成兩個：

- **跨維度的結構保真** — CT、MRI 的器官、血管與病灶邊界在相鄰切片間連續延伸，只做逐像素／逐體素重建的 tokenizer 可能每張切片都對，卻在 through-plane 方向不連續。
- **跨模態的臨床語意** — 病理看的是細胞與組織形態，CT、MRI 看的是器官層級解剖；既有作法多半對齊單一個預訓練語意編碼器，作者認為這會低估該編碼器訓練分布以外的模態語意。

[(ref: main §1)](https://arxiv.org/html/2610.35842v1#S1)

## 方法摘要

MedVTok 是一個 transformer 編碼器加解碼器的 tokenizer：2D 影像與 3D 體積都切成不重疊的 patch、附上原始位置座標後串成一個序列，因此同一個 batch 可以混合不同解析度與維度。編碼器輸出的 per-patch tokens 同時接受兩種監督：

- **Slice Differential Regularization（SliDR）** — 在一般重建損失之外，比較原始與重建體積的相鄰切片一階、二階差分，懲罰切片之間轉變不一致的地方。
- **Multi-Expert Representation Alignment（MERA）** — 把 token 聚合成一個整體表徵，對齊多個依模態分派的凍結專家編碼器：一方面在共享空間做對比式對齊，另一方面把表徵反投影回各專家自己的空間、以 cosine similarity 保留模態特有的資訊。

訓練分兩階段：先只用 2D 影像，再交替餵 2D 與 3D 資料並啟用 SliDR。推論時 tokenizer 直接凍結使用，不再為下游任務微調。[(ref: main §3.1)](https://arxiv.org/html/2610.35842v1#S3.SS1) [(ref: main §3.4)](https://arxiv.org/html/2610.35842v1#S3.SS4)

評估全部凍結 tokenizer，只訓練下游的輕量頭或語言模型端，目的是比較 token 本身的品質，而不是做出最好的任務專用模型。[(ref: main §4.2)](https://arxiv.org/html/2610.35842v1#S4.SS2)

## 方法詳解

**輸入與編碼。** 輸入表示為 C×T×H×W，T = 1 為影像、T > 1 為體積；切成 C×Pt×Ph×Pw 的 patch，每個 patch 帶一個記錄其原始位置的座標，編碼器以由座標導出的 rotary position embeddings（RoPE）處理整個序列。per-patch tokens 經投影與 reparameterization 受 KL 項約束（潛在維度 d_z = 48），並由解碼器重建輸入。[(ref: main §3.1)](https://arxiv.org/html/2610.35842v1#S3.SS1) [(ref: main Appendix B.2)](https://arxiv.org/html/2610.35842v1#A2.SS2)

**重建損失 L_R。** 由 ℓ1、ℓ2、LPIPS 與 adversarial loss 組成，adversarial 權重依 VQGAN 的作法自適應調整。[(ref: main Appendix B.2)](https://arxiv.org/html/2610.35842v1#A2.SS2)

**SliDR。** 對有 T > 2 張切片的體積，定義第 k 張的一階差分 Δk(x) = x(k+1) − x(k) 與二階差分 x(k+1) − 2x(k) + x(k−1)，以 ℓ1 懲罰重建與原始體積在兩種差分上的差距；第一項對齊切片間的轉變，第二項保留 through-plane 曲率。[(ref: main §3.2 Eq. 1)](https://arxiv.org/html/2610.35842v1#S3.SS2)

**MERA。** 每個輸入依模態送到對應的專家編碼器，專家特徵經線性投影到共享空間，與 MedVTok 的聚合表徵 r 做雙向 InfoNCE 對比損失 L_shared（可學溫度）；同時以各模態專屬的 backprojector 把 r 映回專家空間，用 1 − cosine similarity 作 L_expert。L_MERA = L_shared + L_expert。聚合頭採 mean pooling（消融中取代 attention pooling）。專家特徵事先離線計算，訓練時不載入專家模型。[(ref: main §3.3 Eq. 2–4)](https://arxiv.org/html/2610.35842v1#S3.SS3) [(ref: main §4.3)](https://arxiv.org/html/2610.35842v1#S4.SS3) [(ref: main Appendix A)](https://arxiv.org/html/2610.35842v1#A1)

| Index | Expert Encoder | Domains | d_j |
|---|---|---|---|
| 0 | DermLIP | Dermoscopy | 768 |
| 1 | RetCLIP | CFP | 768 |
| 2 | Conch | Pathology | 1024 |
| 3 | PeskaVLP | Endoscopy | 2048 |
| 4–8 | MedImageInsight | CT, MR, US, X-ray, Other | 2048 |
| 9 | Spectre | CT 3D | 2160 |
| 10 | HLIP | MR 3D | 2048 |

表：MERA 使用的專家編碼器，重製自論文 Table 7；9–10 兩個 3D 專家只在 Stage 2 使用。[(ref: main Table 7)](https://arxiv.org/html/2610.35842v1#A1.T7)

**總損失與訓練。** L = L_R + λ_KL·L_KL + λ_SliDR·L_SliDR + λ_MERA·L_MERA，λ_KL = 10⁻⁶、λ_MERA = 1、λ_SliDR = 0.1（Stage 1 為 0）。AdamW（β = 0.9, 0.95），兩階段各約 100K steps，學習率 Stage 1 從 10⁻⁴ 降到 10⁻⁵、Stage 2 從 2×10⁻⁵ 降到 2×10⁻⁶；Stage 2 偶數步跑 2D batch（有效 batch size 600）、奇數步跑 3D batch（48），3D batch 內 CT 與 MR 約各半；影像解析度混合 256、384、512。訓練在 16 張 NVIDIA H200 上進行，Stage 1 約 15.75 小時、Stage 2 約 43.5 小時。[(ref: main §4.1)](https://arxiv.org/html/2610.35842v1#S4.SS1) [(ref: main Appendix B.2)](https://arxiv.org/html/2610.35842v1#A2.SS2)

**下游評估協定。**

- **分類與檢索** — 對凍結特徵做 k-NN 分類，k ∈ {10, 20, 100, 200}，每個 tokenizer 報告四個 k 中最高的準確率；檢索以訓練集為 gallery、測試集為 query，依 cosine similarity 報 Recall@1。[(ref: main §4.2)](https://arxiv.org/html/2610.35842v1#S4.SS2)
- **分割** — 在凍結 patch tokens 上訓練單一 linear segmentation head，學習率在 {10⁻², 10⁻³, 10⁻⁴} 中依驗證集選最佳。[(ref: main §4.2)](https://arxiv.org/html/2610.35842v1#S4.SS2)
- **VQA** — 沿用 LLaVA-Med 架構：凍結 tokenizer → 兩層 MLP connector → Mistral-7B-Instruct。第一階段只訓 connector（約 509,369 組圖文對，來自 PubMedVision 與 MM-Skin）；第二階段對語言模型所有線性層加 LoRA（rank 128、α 256）與 connector 一起微調，用 140,151 題 VQA 訓練資料。推論溫度 0.2，以 Qwen3-235B-A22B 作 LLM-as-judge 做對錯二元判分。[(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)
- **報告生成** — 沿用 LaMed 架構：凍結 tokenizer → 2× 3D average pooling → Llama-3.1-8B-Instruct（LoRA rank 8、α 16），在 AMOS-MM 上訓練 15 epochs，依腹部、胸部、骨盆三區生成 findings，溫度 0.2、top-p 0.9。MedITok 只支援 2D，作者把深度軸當成一批 2D 切片分別編碼再沿深度串接。[(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)

- **論文未交代** — VQA 的 LLM-as-judge 判分 prompt 與判定規則。
- **論文未交代** — k-NN 的 k 是在驗證集還是測試集上挑選；文中只寫「報告四個 k 中最高的準確率」。
- **論文未交代** — 主文 Table 2 與附錄 Table 10 中 MedVTok 的分類準確率不同（例如 CFP 為 90.25 與 90.54±1.05），論文沒有說明兩者的執行差異。[(ref: main Table 2)](https://arxiv.org/html/2610.35842v1#S4.T2) [(ref: main Table 10)](https://arxiv.org/html/2610.35842v1#A3.T10)
- **論文未交代** — 程式碼與權重目前寫的是「將」釋出，論文版本無法據以重跑。

## 資料與實驗

**訓練資料。** 全部來自公開醫學影像資料集，共 28,769,502 張 2D 影像（115 個資料集）與 70,144 個 3D 體積（37 個資料集、CT 與 MR 兩種模態）。為了不讓常見的小型 benchmark 進入訓練池，作者只收 2D 至少 9,000 張、3D 至少 180 個體積的資料集，並沿用 MedITok 的自動品質過濾加人工排除非臨床圖片；作者聲明所有評估資料集都已從訓練語料中排除。[(ref: main Appendix B.1)](https://arxiv.org/html/2610.35842v1#A2.SS1) [(ref: main Appendix C.1)](https://arxiv.org/html/2610.35842v1#A3.SS1)

| 任務 | 資料集（模態） | 樣本數 |
|---|---|---|
| 重建／分類／檢索 | ChestCTScan (CT)、JSIEC (CFP)、HAM10K (Dermoscopy)、PolypDiag (Endoscopy)、BRISC (MRI)、OCTDL (OCT)、LungHist700 (Pathology)、BUSBRA (Ultrasound)、Kermany (X-ray) | 1,000／1,000／10,015／2,202／5,023／3,236／691／1,875／5,856 |
| 分割 | MaplesDR (CFP)、MosMedDataPlus (CT)、HAM10K (Dermoscopy)、PolypDB (Endoscopy)、BRISC (MRI)、PanNuke (Pathology)、BUSBRA (Ultrasound)、VinDr-RibCXR (X-ray) | 192／2,729／10,015／3,843／4,746／7,901／1,875／245 |
| 3D 重建 | AMOS-MM (CT)、MRISegmenter (MRI) | 100／240 |
| 影像合成 | GMAI-VL-5.5M (Multi-modality) | 70,000 |
| VQA（測試基準） | Fundus-MMBench (CFP)、GMAI-MMBench (Multi-modality)、Kvasir-VQA-x1 (Endoscopy)、MM-Skin (Dermoscopy)、PathVQA (Pathology)、SLAKE (Radiography) | 620／4,550／15,955／5,481／6,719／2,094 |
| 報告生成 | AMOS-MM (CT) | 1,687（訓練 1,287、測試 400） |

表：評估資料集，整理自論文 Table 8 與 Appendix C.2。[(ref: main Table 8)](https://arxiv.org/html/2610.35842v1#A3.T8) [(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)

**比較對象。** 重建、分類、檢索、分割的比較包含通用 tokenizer（SDVAE、TokenFlow、MingTok、UniTok、AToken）、醫學 tokenizer（PUMIT、MedVAE、MedITok），分類、檢索與分割另加語意編碼器（BiomedCLIP、MedSigLIP、MedImageInsight）。影像合成、VQA 與報告生成只比較三個醫學 tokenizer：PUMIT、MedVAE（報告生成用 MedVAE-3D）與 MedITok。[(ref: main Table 1–6)](https://arxiv.org/html/2610.35842v1#S4.SS2)

**VQA 結果（重製自 Table 5，Accuracy %↑，三個 seed 平均 ± 95% CI）**

| Method | FundusMM | MM-Skin | Kvasir | PathVQA | SLAKE | GMAI-MM | Avg. |
|---|---|---|---|---|---|---|---|
| PUMIT | 29.84±0.42 | 34.74±0.38 | 69.50±0.51 | 52.97±0.63 | 36.44±0.55 | 28.16±0.47 | 41.94±0.33 |
| MedVAE | 28.39±0.56 | 34.21±0.44 | 66.64±0.72 | 51.15±0.58 | 31.57±0.67 | 27.61±0.53 | 39.93±0.41 |
| MedITok | 31.29±0.35 | 36.18±0.41 | 70.63±0.29 | 58.46±0.52 | 45.61±0.38 | 30.15±0.26 | 45.39±0.28 |
| MedVTok | 33.39±0.31 | 37.49±0.28 | 72.98±0.34 | 57.24±0.45 | 45.94±0.37 | 31.81±0.29 | 46.48±0.22 |

[(ref: main Table 5)](https://arxiv.org/html/2610.35842v1#S4.T5)

**CT 報告生成結果（重製自 Table 6，AMOS-MM 測試集，三個 seed 平均 ± 95% CI）**

| Metrics | Method | Abdomen | Chest | Pelvis | Avg. |
|---|---|---|---|---|---|
| BLEU-2 (↑) | PUMIT | 0.289±0.008 | 0.193±0.003 | 0.164±0.007 | 0.215±0.005 |
| BLEU-2 (↑) | MedVAE-3D | 0.249±0.038 | 0.185±0.020 | 0.152±0.010 | 0.195±0.013 |
| BLEU-2 (↑) | MedITok | 0.256±0.013 | 0.219±0.020 | 0.294±0.017 | 0.257±0.012 |
| BLEU-2 (↑) | MedVTok | 0.272±0.005 | 0.263±0.045 | 0.288±0.017 | 0.274±0.009 |
| RaTEScore (↑) | PUMIT | 0.604±0.005 | 0.511±0.035 | 0.201±0.015 | 0.439±0.006 |
| RaTEScore (↑) | MedVAE-3D | 0.613±0.022 | 0.497±0.053 | 0.187±0.003 | 0.432±0.011 |
| RaTEScore (↑) | MedITok | 0.610±0.006 | 0.501±0.008 | 0.594±0.031 | 0.568±0.015 |
| RaTEScore (↑) | MedVTok | 0.619±0.005 | 0.570±0.074 | 0.612±0.006 | 0.600±0.006 |
| GREEN (↑) | PUMIT | 0.421±0.017 | 0.204±0.010 | 0.124±0.019 | 0.250±0.009 |
| GREEN (↑) | MedVAE-3D | 0.401±0.024 | 0.186±0.003 | 0.105±0.064 | 0.230±0.179 |
| GREEN (↑) | MedITok | 0.412±0.025 | 0.256±0.010 | 0.492±0.026 | 0.386±0.013 |
| GREEN (↑) | MedVTok | 0.425±0.005 | 0.300±0.078 | 0.515±0.044 | 0.413±0.020 |

[(ref: main Table 6)](https://arxiv.org/html/2610.35842v1#S4.T6)

**純影像任務的平均分數（摘自 Table 1–4）**

| 任務（指標） | MedVTok | 次佳 |
|---|---|---|
| 2D 重建（PSNR dB↑／SSIM %↑，九模態平均） | 40.18／94.16 | AToken 38.22／91.72 |
| 分類（k-NN Accuracy %↑，平均） | 80.23 | MedImageInsight 76.21 |
| 檢索（Recall@1 %↑，平均） | 79.18 | MedImageInsight 77.34 |
| 分割（Dice %↑，平均） | 76.07 | MedSigLIP 74.62 |
| 影像合成（FID↓，平均） | 101.73 | MedITok 109.76 |

[(ref: main Table 1)](https://arxiv.org/html/2610.35842v1#S4.T1) [(ref: main Table 2)](https://arxiv.org/html/2610.35842v1#S4.T2) [(ref: main Table 3)](https://arxiv.org/html/2610.35842v1#S4.T3) [(ref: main Table 4)](https://arxiv.org/html/2610.35842v1#S4.T4)

## 結果

- **純影像任務平均最佳** — MedVTok 在 2D 重建九種模態的 PSNR 與 SSIM 都排第一，3D MRI 與 3D CT 重建也最高；分類、檢索、分割與影像合成的平均分數都高於所有比較對象，包含專為表徵學習訓練的語意編碼器。[(ref: main Table 1)](https://arxiv.org/html/2610.35842v1#S4.T1) [(ref: main Table 2)](https://arxiv.org/html/2610.35842v1#S4.T2) [(ref: main Table 3)](https://arxiv.org/html/2610.35842v1#S4.T3) [(ref: main Table 4)](https://arxiv.org/html/2610.35842v1#S4.T4)
- **平均之下並非每格都贏** — 分類上皮膚鏡（MedImageInsight 85.87 對 74.16）與病理（MedSigLIP 84.10 對 82.69）、分割上 X-ray（MedSigLIP 62.48 對 61.13）、影像合成上 CT 與內視鏡（MedITok 的 FID 142.46 與 58.38，對 MedVTok 146.39 與 82.39）都由其他方法領先。[(ref: main Table 2)](https://arxiv.org/html/2610.35842v1#S4.T2) [(ref: main Table 3)](https://arxiv.org/html/2610.35842v1#S4.T3) [(ref: main Table 4)](https://arxiv.org/html/2610.35842v1#S4.T4)
- **專家本身在病理上仍較強** — 與 MERA 用來對齊的專家編碼器相比，MedVTok 在九項分類中有七項高於 MedImageInsight、八項分割全數高於 MedImageInsight，但病理專家 Conch 的分類（93.08±2.44 對 78.97±1.65）與分割（83.77±1.39 對 77.74±1.56）都仍高於 MedVTok。[(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2) [(ref: main Table 10)](https://arxiv.org/html/2610.35842v1#A3.T10) [(ref: main Table 11)](https://arxiv.org/html/2610.35842v1#A3.T11)
- **VQA 的差距是 1 分級** — 平均準確率 MedVTok 46.48±0.22、MedITok 45.39±0.28，相差 1.09 個百分點；PathVQA 上 MedITok 較高（58.46 對 57.24）。作者指出 MedVTok 訓練不使用圖文對，MedITok 則用了數百萬筆文字 caption。[(ref: main Table 5)](https://arxiv.org/html/2610.35842v1#S4.T5) [(ref: main §4.2 VQA)](https://arxiv.org/html/2610.35842v1#S4.SS2)
- **VQA 對照實驗名次不變** — 凍結語言模型、只訓 connector 時 MedVTok 29.86 對 MedITok 24.76，差距較大；把判分模型從 Qwen3-235B-A22B 換成 GPT-5 重評，四個 tokenizer 的名次不變（MedVTok 46.02、MedITok 44.82）。[(ref: main Table 15)](https://arxiv.org/html/2610.35842v1#A3.T15)
- **報告生成平均最佳，但分區有例外** — 平均 BLEU-2 0.274、RaTEScore 0.600、GREEN 0.413 皆為最高（MedITok 為 0.257、0.568、0.386）；但腹部 BLEU-2 PUMIT 較高（0.289 對 0.272），骨盆 BLEU-2 MedITok 較高（0.294 對 0.288），胸部 GREEN 的 95% CI 為 ±0.078。[(ref: main Table 6)](https://arxiv.org/html/2610.35842v1#S4.T6)
- **同資料重訓仍領先，但只看影像指標** — 把 AToken、MedITok、MedVTok 都改在 MedITok 的 200 萬張圖文資料上重訓，MedVTok 的 PSNR（39.71）、分類（71.70%）與分割（73.21%）仍最高；這組控制比較沒有包含 VQA 與報告生成。[(ref: main Table 19)](https://arxiv.org/html/2610.35842v1#A3.T19)
- **未見過的模態** — 在訓練中沒有出現的血球顯微影像資料集 PBC 上，凍結特徵的 k-NN 與線性分類準確率分別為 94.78% 與 96.84%，皆為比較中最高。[(ref: main Appendix C.3)](https://arxiv.org/html/2610.35842v1#A3.SS3)

## 限制

**作者自述。** 訓練資料集中在常見成像模態，其他模態、臨床照片與文獻插圖尚未涵蓋；MERA 使用凍結的專家編碼器，若預算允許，聯合微調或加入新專家可能擴大涵蓋範圍。[(ref: main §5)](https://arxiv.org/html/2610.35842v1#S5)

**本書庫補充。**

- **語言任務的比較對象很窄** — VQA 與報告生成只和三個醫學 tokenizer 比，沒有放入在分類、分割上表現接近的語意編碼器（MedSigLIP、MedImageInsight）或通用 tokenizer（AToken、UniTok），因此無法得知 MedVTok 在接上 LLM 後是否也勝過這些編碼器。[(ref: main Table 5)](https://arxiv.org/html/2610.35842v1#S4.T5) [(ref: main Table 6)](https://arxiv.org/html/2610.35842v1#S4.T6)
- **報告生成測試集小** — AMOS-MM 測試只有 400 組 CT－報告配對，只用自動指標評分，沒有放射科醫師審閱；MedITok 在這個任務上是經作者改造為逐切片編碼後參賽。[(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)
- **VQA 判分依賴 LLM judge** — 準確率由 LLM 做二元判分，判分 prompt 未公開；換用 GPT-5 重評名次不變，但兩個 judge 都是語言模型。[(ref: main Table 15)](https://arxiv.org/html/2610.35842v1#A3.T15)
- **資料重疊只能靠作者聲明** — 作者以資料集大小門檻排除小型 benchmark，並聲明評估資料集都不在 tokenizer 的訓練語料中；但 VQA 訓練另用了 50 萬組 PubMedVision 圖文對，這些訓練影像與 PathVQA、SLAKE 等測試題影像之間是否重疊，論文沒有報告核對結果。[(ref: main Appendix C.1)](https://arxiv.org/html/2610.35842v1#A3.SS1) [(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2)
- **分類的 k 選擇與表格不一致** — 見「方法詳解」的論文未交代條目。

## 與書庫其他文章的關係

DLoss 固定視覺特徵、只改報告生成的訓練目標，本篇則固定 LLM 端的訓練協定、只換凍結的視覺 tokenizer，兩篇都以 GREEN 評估 3D CT 報告生成，而 DLoss 當作 backbone 比較的 SPECTRE 與 HLIP，正是本篇 MERA 的兩個 3D 專家編碼器: [DLoss：訓練時分開施壓該寫與不該寫的診斷詞，GREEN 多 4 分](2026-11-02-dloss-diagnostic-loss-ct-report-generation.md)

本篇把 Conch 當作病理模態的專家編碼器來對齊，而附錄的對照顯示 Conch 自己在病理分類與分割上仍高於對齊後的通用 tokenizer: [CONCH：零樣本病理分類很強，多類腦瘤就露出邊界](2026-09-15-conch-pathology-vlm.md)

本篇用 VQA 準確率比較不同視覺 tokenizer，該研究則顯示病理切片層級的 VQA 在拿掉切片後答對率幾乎不變，提醒讀者 VQA 分數的差距未必全部來自影像表徵: [語言替病理 VLM 加了什麼？拿掉切片，答對率只掉 0.4 個百分點](2026-11-04-pathology-vlm-language-controlled-probes.md)

## 實務的啟發

- **可借用的評估協定** — 「凍結視覺端、固定 connector 與 LLM、只換 tokenizer、三個 seed 加 CI」是比較視覺 backbone 時乾淨的作法；再加上 connector-only 與換 judge 兩組對照，可以檢查差距是否只來自 LLM 端的補償。在自己的胸片或 CT 報告生成管線挑選視覺編碼器時，可照這個模式做 A/B。[(ref: main Appendix C.2)](https://arxiv.org/html/2610.35842v1#A3.SS2) [(ref: main Table 15)](https://arxiv.org/html/2610.35842v1#A3.T15)
- **影像指標的大幅領先不等於語言任務的大幅領先** — 本篇分類平均比 MedITok 多約 6.7 個百分點，VQA 平均只多 1.09；若目標是報告生成或問答，應該直接在語言任務上量測候選編碼器，而不是用 k-NN 或線性探測的成績代替。這是本書庫依 Table 2 與 Table 5 的讀法，論文沒有分析兩者落差的原因。[(ref: main Table 2)](https://arxiv.org/html/2610.35842v1#S4.T2) [(ref: main Table 5)](https://arxiv.org/html/2610.35842v1#S4.T5)
- **單一模態仍要和專家比** — 若應用只涉及一種模態（例如只做病理），通用 tokenizer 不一定勝過該模態的專家編碼器；本篇自己的附錄就顯示 Conch 在病理上較強。[(ref: main Table 10)](https://arxiv.org/html/2610.35842v1#A3.T10)
- **待驗證** — 「一個 tokenizer 服務所有模態」對病人層級多模態建模是否有幫助，論文沒有實驗；權重釋出後，需要在自己的資料與完整報告生成流程上重測，才能判斷是否值得替換現有編碼器。

## References

- **main** — Chenglong Ma, Yuanfeng Ji, Junzhi Ning, Jiyao Liu, et al. *MedVTok: A General-Purpose Medical Visual Tokenizer*. arXiv:2610.35842v1, 2026. <https://arxiv.org/abs/2610.35842v1>（DOI [10.48550/arXiv.2610.35842](https://doi.org/10.48550/arXiv.2610.35842)）
  - 深鏈：[§1](https://arxiv.org/html/2610.35842v1#S1)、[§3](https://arxiv.org/html/2610.35842v1#S3)、[§3.1](https://arxiv.org/html/2610.35842v1#S3.SS1)、[§3.2](https://arxiv.org/html/2610.35842v1#S3.SS2)、[§3.3](https://arxiv.org/html/2610.35842v1#S3.SS3)、[§3.4](https://arxiv.org/html/2610.35842v1#S3.SS4)、[§4.1](https://arxiv.org/html/2610.35842v1#S4.SS1)、[§4.2](https://arxiv.org/html/2610.35842v1#S4.SS2)、[§4.3](https://arxiv.org/html/2610.35842v1#S4.SS3)、[§5](https://arxiv.org/html/2610.35842v1#S5)、[Table 1](https://arxiv.org/html/2610.35842v1#S4.T1)、[Table 2](https://arxiv.org/html/2610.35842v1#S4.T2)、[Table 3](https://arxiv.org/html/2610.35842v1#S4.T3)、[Table 4](https://arxiv.org/html/2610.35842v1#S4.T4)、[Table 5](https://arxiv.org/html/2610.35842v1#S4.T5)、[Table 6](https://arxiv.org/html/2610.35842v1#S4.T6)、[Appendix A](https://arxiv.org/html/2610.35842v1#A1)、[Table 7](https://arxiv.org/html/2610.35842v1#A1.T7)、[Appendix B.1](https://arxiv.org/html/2610.35842v1#A2.SS1)、[Appendix B.2](https://arxiv.org/html/2610.35842v1#A2.SS2)、[Appendix C.1](https://arxiv.org/html/2610.35842v1#A3.SS1)、[Table 8](https://arxiv.org/html/2610.35842v1#A3.T8)、[Appendix C.2](https://arxiv.org/html/2610.35842v1#A3.SS2)、[Table 10](https://arxiv.org/html/2610.35842v1#A3.T10)、[Table 11](https://arxiv.org/html/2610.35842v1#A3.T11)、[Table 15](https://arxiv.org/html/2610.35842v1#A3.T15)、[Appendix C.3](https://arxiv.org/html/2610.35842v1#A3.SS3)、[Table 19](https://arxiv.org/html/2610.35842v1#A3.T19)、[Appendix D](https://arxiv.org/html/2610.35842v1#A4)
- **abstract** — arXiv abstract page（提交日期、授權、NeurIPS 2026 註記）：<https://arxiv.org/abs/2610.35842v1>

[Home](../) · [AI Papers](./)
