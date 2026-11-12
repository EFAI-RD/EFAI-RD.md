---
parent: AI Papers
nav_order: 2
title: "文字引導分割的增益：只留病灶範圍詞就拿回 84–98%"
catalog_id: "arxiv:2611.13970"
editors:
  - "Clare"
refs:
  main:
    title: "Counterfactual Analysis of Extent Leakage from Annotation-Derived Prompts in Vision-Language Medical Image Segmentation"
    url: "https://arxiv.org/html/2611.13970v1"
  abs:
    title: "arXiv abstract page: 2611.13970v1"
    url: "https://arxiv.org/abs/2611.13970v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 文字引導分割的增益：只留病灶範圍詞就拿回 84–98%

## 來源

- 團隊：Niran Nataraj（通訊作者）與 Kenji Kawashima，University of Tokyo Graduate School of Information Science and Technology 的 Department of Information Physics and Computing；Ankita Das 與 C. Krishna Mohan，Indian Institute of Technology Hyderabad 的 Department of Computer Science and Engineering；共 4 位作者。[(ref: main author block)](https://arxiv.org/html/2611.13970v1)
- 論文：*Counterfactual Analysis of Extent Leakage from Annotation-Derived Prompts in Vision-Language Medical Image Segmentation*，arXiv:2611.13970v1（eess.IV；另列 cs.CV、cs.LG），2026-11-10 提交，目前只有 v1；授權為 arXiv 非專屬散布授權；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2611.13970v1)
- 識別碼：arXiv [2611.13970](https://arxiv.org/abs/2611.13970v1)；DOI [10.48550/arXiv.2611.13970](https://doi.org/10.48550/arXiv.2611.13970)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.13970v1)、[PDF v1](https://arxiv.org/pdf/2611.13970v1)。
- 程式與資料：七個資料集，以及 MedCLIPSeg 與 RecLMIS 釋出的 caption 與 checkpoint 都是公開的；作者自己的修改版 caption、逐圖分數與產生全文數字的分析程式，寫明在論文被接受後才會公開於 GitHub（felirox/ExtentProbe），在此之前只依要求提供給編輯與審稿人。[(ref: main Data availability)](https://arxiv.org/html/2611.13970v1#Sx4)
- 研究性質：基準稽核（audit），完整研究而非 pilot。核心分析都已實作並有結果：對公開 checkpoint 做測試時的 caption 編輯、在三個訓練集上各以 5 組 caption × 3 個 seed 重訓（準則 R0–R4 事先寫定）、只看 caption 的洩漏分數，以及四個不使用測試遮罩的方法（含作者自建的 ExtentSeg）。[(ref: main §1)](https://arxiv.org/html/2611.13970v1#S1) [(ref: main §4.4)](https://arxiv.org/html/2611.13970v1#S4.SS4)
- 利益衝突與證據邊界：Kenji Kawashima 持有手術機器人公司 RiverField Inc. 的股份；本研究沒有特定經費。準則的「事先寫定」以作者自己的研究紀錄與版本控制為據，未使用外部登錄平台，且部分準則的第一個 commit 晚於單一 seed 的結果。本文數值以 arXiv v1 HTML 版的正文、Table 1–5 與附錄 A–D 為準。[(ref: main Competing interest)](https://arxiv.org/html/2611.13970v1#Sx2) [(ref: main Funding)](https://arxiv.org/html/2611.13970v1#Sx3) [(ref: main Appendix A)](https://arxiv.org/html/2611.13970v1#A1)

**編輯：** Clare

作者稽核三種影像的公開文字引導分割基準，發現 caption 帶來的 Dice 增益多半來自一個從評分遮罩算出、或由基準標註者寫下的病灶範圍詞：在五個大腸鏡測試集上只保留尺寸詞就拿回 84.1–98.3% 的增益，胸片只保留肺區片語則拿回 90.9%。[(ref: main Table 2)](https://arxiv.org/html/2611.13970v1#S5.T2)

## 流程

![左右兩欄圖。左欄由上而下四個淺藍底、深藍實線的圓角框，以三支向下箭頭相連：「1. Caption edits on published checkpoints：MedCLIPSeg (7 test sets) + RecLMIS (QaTa-COV19); empty / mismatched / matched caption; ablate, isolate or force one attribute」、「2. Retrain MedCLIPSeg with edited captions：Original / Size-blind / Size-only / Mismatched / Text-free; Kvasir-SEG, BUSI, QaTa-COV19; 3 seeds each; criteria R0-R4 fixed in advance」、「3. Caption-only leakage score：ridge regression: caption words -> log lesion area (R2_cap) + mutual-information score I_ext」、「4. Methods without the test mask：edge-aligned threshold, image-only describer, Text-free model, ExtentSeg」；左下角小字「Redrawn by EFAI-RD from arXiv:2611.13970v1 Sections 4.1-4.8」。右欄為長條圖，標題「Table 2: Dice by caption condition」，縱軸為「Dice (published MedCLIPSeg checkpoints)」，刻度 40–100；橫軸七組依序為 Kvasir-SEG、CVC-ClinicDB、CVC-300、BKAI-IGH、CVC-ColonDB、BUSI、QaTa-COV19，每組由左到右為灰色 Empty caption、橘色 Mismatched caption、深藍 Matched caption，長條頂端以直書數字標示數值：Kvasir-SEG 81.0、81.0、90.2；CVC-ClinicDB 69.9、76.1、80.8；CVC-300 65.3、79.5、80.8；BKAI-IGH 54.5、73.8、79.2；CVC-ColonDB 59.2、61.0、71.9；BUSI 71.7、59.5、85.7；QaTa-COV19 60.2、70.7、83.4。](assets/extent-leakage-audit-and-caption-dice.png)

*圖：本書庫依論文 §4.1–4.8 重繪的四段稽核流程（左），以及 Table 2 中公開 MedCLIPSeg checkpoint 在七個測試集上分別給空白、他圖、本圖 caption 時的 Dice（右；長條上的數字四捨五入到小數一位）。數值來自 [Table 2](https://arxiv.org/html/2611.13970v1#S5.T2)。*

## 背景／問題

文字引導分割（text-guided segmentation）模型同時接收影像與一句描述病灶的短文字（論文稱 caption，內容如病灶數量、大小、位置）。MedCLIPSeg 的原論文報告 caption 不完整時整體 Dice 會掉 26.9 分；本篇作者在其公開 checkpoint 上量到，改給空白 caption 會掉 9.11 到 24.61 分，依測試集而定。[(ref: main §1)](https://arxiv.org/html/2611.13970v1#S1)

問題在 caption 的來源。大腸鏡與乳房超音波（BUSI）的 caption 逐張等於 Poudel 等人以固定模板產生的提示：數量、尺寸、位置三個詞由參考遮罩計算，顏色與形狀則由對影像的 VQA 查詢產生。尺寸詞依遮罩佔影像面積切成 small（< 8%）、medium（8–30%）、large（≥ 30%）；作者用這條規則重現了 2,633 句單一病灶 caption 中的 2,617 句，其餘 16 句都在門檻 0.006 以內。[(ref: main §3.2)](https://arxiv.org/html/2611.13970v1#S3.SS2) 胸片 QaTa-COV19 的 caption 則是 LViT 作者為基準撰寫的受累肺區，不是遮罩的固定函數（最佳規則只重現 51.5% 的測試影像），左右以影像位置命名、與放射科慣例相反，因此也不是取自放射報告。[(ref: main §3.2)](https://arxiv.org/html/2611.13970v1#S3.SS2) [(ref: main Appendix E)](https://arxiv.org/html/2611.13970v1#A5)

測試時模型拿到的 caption 也是同一套，等於輸入裡含有從「要拿來評分的那張遮罩」算出的資訊，而臨床上遮罩正是模型要產出的東西。[(ref: main §1)](https://arxiv.org/html/2611.13970v1#S1) 「文字能改善分割」是既有基準上的報告數字；本篇要檢驗的是這個增益裡有多少是描述影像、多少是抄自標籤。至於醫師實際寫下的描述能否幫助分割，作者明說沒有測試。[(ref: main §6.1)](https://arxiv.org/html/2611.13970v1#S6.SS1)

## 方法摘要

- **Caption 編輯** — 對公開的 MedCLIPSeg checkpoint（Kvasir-SEG、BUSI、QaTa-COV19 三個模型，七個測試集）與 RecLMIS（只有 QaTa-COV19）逐項改 caption：matched、empty、mismatched、ablated、isolated、forced 六種。[(ref: main §4.1)](https://arxiv.org/html/2611.13970v1#S4.SS1)
- **拆解文字增益** — 以 text gain *G*、prior gain *P* 與 prior share *π* 分出「任何一句 caption 都給得到」與「只有本圖 caption 給得到」的部分，再以 sufficiency *S* 與 necessity *N* 衡量每個屬性的貢獻。[(ref: main §4.2)](https://arxiv.org/html/2611.13970v1#S4.SS2)
- **重訓** — 依公開配方重訓 MedCLIPSeg，比較 5 組訓練 caption，各 3 個 seed，以事先寫定的 R0–R4 與 *ρ* 判定。[(ref: main §4.4)](https://arxiv.org/html/2611.13970v1#S4.SS4) [(ref: main §4.5)](https://arxiv.org/html/2611.13970v1#S4.SS5)
- **Caption-only leakage score** — 不訓練分割模型，只用 caption 的字詞迴歸病灶面積（*R*²_cap），另以互資訊量 *I*_ext 輔助。[(ref: main §4.6)](https://arxiv.org/html/2611.13970v1#S4.SS6)
- **不讀測試遮罩的方法** — edge-aligned threshold、image-only describer、Text-free 模型，以及從影像估計病灶範圍再據以分割的 ExtentSeg。[(ref: main §4.7)](https://arxiv.org/html/2611.13970v1#S4.SS7) [(ref: main §4.8)](https://arxiv.org/html/2611.13970v1#S4.SS8)

## 方法詳解

- **六種 caption** — matched 為該圖原本的 caption；empty 固定為「a medical image」；mismatched 是另一張測試影像的 caption（每個測試集抽一次不讓任何影像拿回自己 caption 的重排，所有模型共用）；ablated 刪掉單一屬性；isolated 只留單一屬性；forced 把某屬性換成指定值。QaTa-COV19 只有 191 種不同的測試 caption，因此 2,113 張中有 230 張（10.9%）拿到的 mismatched caption 與自己的相同。[(ref: main §4.1)](https://arxiv.org/html/2611.13970v1#S4.SS1)
- **Text gain 與 prior share** — *G* 為 matched 與 empty 的平均 Dice 差；*P* 為 mismatched 與 empty 的平均 Dice 差，*π* = *P*／*G*。*π* 衡量「別張圖的 caption 就能拿到」的比例；別圖 caption 比沒有 caption 還差時，*π* 為負。[(ref: main §4.2)](https://arxiv.org/html/2611.13970v1#S4.SS2)
- **Sufficiency 與 necessity** — *S*_a 是只保留屬性 a 時拿回 *G* 的比例，*N*_a 是只刪掉 a 時失去 *G* 的比例；其他字詞若重複 a 的資訊，*N* 會低於 *S*。範圍屬性（extent attribute）在大腸鏡與 BUSI 是尺寸詞，在 QaTa-COV19 是肺區片語，記為 *S*_ext、*N*_ext。[(ref: main §4.2)](https://arxiv.org/html/2611.13970v1#S4.SS2)
- **Size response** — 把尺寸詞從 small 強制改為 large 時，預測為病灶的影像面積比例平均變化多少；QaTa-COV19 則比較單一肺區「the lower right lung」與六區「all left lung and all right lung」。[(ref: main §4.3)](https://arxiv.org/html/2611.13970v1#S4.SS3)
- **重訓配方** — 100 epochs、Adam、學習率以 cosine 從 3×10⁻⁴ 降到 10⁻⁴、batch size 24；訓練 caption 為 Original、Size-blind（刪尺寸詞）、Size-only（只留尺寸詞）、Mismatched、Text-free（全用空白 caption）。QaTa-COV19 以肺區片語代替尺寸詞（Zone-blind、Zone-only），且沒有訓練 Mismatched 模型；BUSI 的 Size-only 同時刪掉診斷詞。所有重訓模型取最後一個 epoch，以釋出的測試 caption 評估。[(ref: main §4.4)](https://arxiv.org/html/2611.13970v1#S4.SS4)
- **事先寫定的準則** — R0：Original 模型與公開 checkpoint 相差 1.5 分以內；R1：Size-blind 的 size response 低於 Original 的 25%；R2：Size-blind 保留的 *G* ≤ 50% 且信賴區間上界低於 50%；R3：Size-only 保留的 *G* ≥ 75% 且下界高於 75%；R4：Mismatched 的 |*G*| ≤ 1，且其空白 caption 分數與 Text-free 相差 1 分以內。BUSI 與 QaTa-COV19 訓練前另加 R4 的區間要求、*ρ* > 0 的第六條準則，並把「點估計達標但區間碰到門檻」稱為 consistent。[(ref: main §4.4)](https://arxiv.org/html/2611.13970v1#S4.SS4)
- ***ρ*（只看影像時的差距）** — 給空白 caption 時，某組訓練 caption 的模型減去 Original 模型的平均 Dice；為正代表該模型只看影像時分割得更好。[(ref: main §4.5)](https://arxiv.org/html/2611.13970v1#S4.SS5)
- **Caption-only leakage score** — 對每張有病灶的影像，以 caption 的字詞與字詞對做 ridge regression 預測 log 病灶面積，五折交叉驗證，報告 out-of-fold 的 *R*²_cap；打亂 caption 為機率水準。*I*_ext 是範圍詞與面積三分位之間、扣除 200 次置換平均後的互資訊，除以三分位熵，最小可能 p 值約 0.005。折是依影像切分，不依影片或受試者。[(ref: main §4.6)](https://arxiv.org/html/2611.13970v1#S4.SS6)
- **ExtentSeg** — 以學習的 extent token 取代 MedCLIPSeg 的文字分支、保留影像編碼器與 adapter。病灶面積依 Kvasir-SEG 訓練集分位數切成 20 個 bin，bin 上的機率分布映射成 8 個 token；第一次前向以均勻分布條件估計範圍，第二次以估計值條件產生分割。訓練時各以 0.45、0.45、0.10 的機率給真實範圍（略為模糊）、模型自己的估計或不給範圍；損失為 Dice＋BCE＋範圍 head 的 CE＋面積項（λ 皆為 0.1）。測試時只用自己的估計；改給真實範圍則作為讀取遮罩的上限參考。[(ref: main §4.8)](https://arxiv.org/html/2611.13970v1#S4.SS8)
- **統計** — 95% percentile paired bootstrap（以測試影像重抽 10⁴ 次），重訓模型每張影像先對 3 個 seed 取平均。敏感度分析另以大腸鏡影片序列（273 個 cluster）或 QaTa-COV19 的 474 位受試者重抽，並在部分分析中連同 seed 一起重抽。[(ref: main §4.9)](https://arxiv.org/html/2611.13970v1#S4.SS9) [(ref: main Appendix D)](https://arxiv.org/html/2611.13970v1#A4)
- **論文未交代** — 公開 MedCLIPSeg checkpoint 是第幾個 epoch；釋出的評估設定只載入最新的 checkpoint 檔。[(ref: main Appendix C)](https://arxiv.org/html/2611.13970v1#A3)
- **論文未交代** — 修改版 caption、逐圖分數與分析程式尚未公開，讀者目前無法重跑本文數字；caption-only score 也沒有以影片或受試者分組重做交叉驗證。[(ref: main Data availability)](https://arxiv.org/html/2611.13970v1#Sx4) [(ref: main §6.3)](https://arxiv.org/html/2611.13970v1#S6.SS3)

## 資料與實驗

### 資料

節錄自 Table 1（MedCLIPSeg 釋出版本的影像數；括號內的切分未使用，大腸鏡只用 Kvasir-SEG 訓練）：

| Dataset | Modality | Total | Train | Val | Test | Extent attribute |
|---|---|---|---|---|---|---|
| Kvasir-SEG | colonoscopy | 1000 | 800 | 100 | 100 | size word |
| CVC-ClinicDB | colonoscopy | 612 | (490) | (61) | 61 | size word |
| CVC-300 | colonoscopy | 66 | (6) | - | 60 | size word |
| CVC-ColonDB | colonoscopy | 380 | (20) | - | 360 | size word |
| BKAI-IGH | colonoscopy | 999 | (799) | (100) | 100 | size word |
| BUSI | ultrasound | 780 | 624 | 78 | 78 | size word |
| QaTa-COV19 | chest X-ray | 9258 | 5716 | 1429 | 2113 | lung zones |

[(ref: main Table 1)](https://arxiv.org/html/2611.13970v1#S3.T1)

| 資料品質項目 | 內容 | ref |
|---|---|---|
| 大腸鏡測試影像 | 五個測試集共 681 張，只找到 1 張近似重複（Kvasir-SEG） | [(ref: main §3.1)](https://arxiv.org/html/2611.13970v1#S3.SS1) |
| BUSI 近似重複 | 78 張測試影像中 20 張（15 張有病灶）與訓練或驗證影像近似重複，可能來自同一病人 | [(ref: main §3.1)](https://arxiv.org/html/2611.13970v1#S3.SS1) |
| CVC-300 | 60 張測試影像中 55 張也出現在 CVC-ColonDB，合併統計會重複計算 | [(ref: main §3.1)](https://arxiv.org/html/2611.13970v1#S3.SS1) |
| BKAI-IGH | 3 張測試影像的 caption 寫「no polyp」，遮罩卻有息肉 | [(ref: main §3.1)](https://arxiv.org/html/2611.13970v1#S3.SS1) |
| QaTa-COV19 | 測試受試者未出現在訓練或驗證中，但 2,354 張訓練、597 張驗證影像缺受試者識別碼 | [(ref: main §3.1)](https://arxiv.org/html/2611.13970v1#S3.SS1) |
| 評估設定 | 30 次隨機前向平均、門檻 0.5，在原始解析度計算 Dice（0–100 分）；所有影像縮放到 224×224 輸入 | [(ref: main §3.3)](https://arxiv.org/html/2611.13970v1#S3.SS3) |

### 實驗

公開 checkpoint 在三種 caption 下的 Dice 與增益拆解，節錄自 Table 2（*π*、*S*_ext、*N*_ext 單位為 %）：

| Test set | Empty | Mism. | Match. | *G* | *π* | *S*_ext | *N*_ext | *R*²_cap |
|---|---|---|---|---|---|---|---|---|
| MedCLIPSeg Kvasir-SEG | 81.04 | 81.04 | 90.15 | 9.11 | −0.1 | 87.7 | 51.8 | 0.70 |
| MedCLIPSeg CVC-ClinicDB | 69.92 | 76.06 | 80.80 | 10.87 | 56.5 | 84.1 | 67.4 | 0.54 |
| MedCLIPSeg CVC-300 | 65.32 | 79.49 | 80.84 | 15.53 | 91.3 | 85.9 | 67.2 | 0.24 |
| MedCLIPSeg BKAI-IGH | 54.55 | 73.75 | 79.16 | 24.61 | 78.0 | 92.0 | 77.2 | 0.59 |
| MedCLIPSeg CVC-ColonDB | 59.17 | 60.96 | 71.89 | 12.72 | 14.1 | 98.3 | 68.2 | 0.71 |
| MedCLIPSeg BUSI† | 71.73 | 59.50 | 85.73 | 14.00 | −87.4 | 30.6 | 57.2 | 0.60 |
| MedCLIPSeg QaTa-COV19 | 60.24 | 70.67 | 83.41 | 23.17 | 45.0‡ | 90.9 | 63.4 | 0.77 |
| RecLMIS QaTa-COV19 | 70.53 | 72.66 | 85.21 | 14.68 | 14.5 | 87.8 | 58.0 | - |

† *S*_ext 與 *N*_ext 只算 65 張有病灶的影像。‡ 排除 mismatched caption 與自己相同的影像後為 36.2%。[(ref: main Table 2)](https://arxiv.org/html/2611.13970v1#S5.T2)

重訓結果對照事先寫定的準則，節錄自 Table 3（MedCLIPSeg，每個模型 3 個 seed；QaTa-COV19 的範圍屬性為肺區片語）：

| Criterion | Kvasir-SEG (n=681) | BUSI (n=78；R1–R3、*ρ*：65) | QaTa-COV19 (n=2113) |
|---|---|---|---|
| R0 Original 與公開 checkpoint 差 ±1.5 內 | 76.00 vs. 77.23（−1.22）yes | 85.26 vs. 85.73（−0.47）yes | 83.66 vs. 83.41（+0.25）yes |
| R1 Size-blind 的 size response < Original 的 25% | 1.2%（0.13 vs. 11.1 pp）yes | 1.3%（0.11 vs. 8.0 pp）yes | 0.0%（0.00 vs. 7.9 pp）yes |
| R2 Size-blind 保留 *G* ≤ 50%（CI） | 37.4% [28.5, 46.8] yes | 39.1% [21.9, 58.3] consistent | 9.0% [7.1, 11.0] yes |
| R3 Size-only 保留 *G* ≥ 75%（CI） | 89.7% [80.4, 99.8] yes | 49.9% [37.6, 60.7] no | 91.0% [88.8, 93.2] yes |
| R4 Mismatched：\|*G*\| ≤ 1；空白 caption 分數與 Text-free 差 ±1 內 | *G* = −0.53 [−0.78, −0.28]；+0.31 [−0.18, +0.80] yes | *G* = −1.13 [−2.52, −0.10]；+0.54 [−0.46, +1.74] no | - |
| *ρ* Size-blind 只看影像更好（*ρ* > 0，CI） | +2.39 [+1.62, +3.16]（未事先登錄） | +8.43 [+4.38, +13.02] yes | +11.28 [+10.55, +12.00] yes |

pp：影像面積的百分點。[(ref: main Table 3)](https://arxiv.org/html/2611.13970v1#S5.T3)

有無讀取測試遮罩的方法比較，節錄自 Table 5（五個大腸鏡測試集，n=681；unseen 為四個外院測試集，n=581；Δ 為與公開模型＋matched caption 的配對差）：

| Method | Dice all | Dice unseen | Δ, all (95% CI) |
|---|---|---|---|
| Published, empty caption | 63.21 | 60.14 | −14.02 [−15.63, −12.41] |
| Edge-aligned threshold | 73.84 | 71.41 | −3.39 [−4.45, −2.39] |
| Image-only describer | 72.38 | 69.71 | −4.84 [−5.91, −3.80] |
| Text-free (trained without text) | 72.65 | 70.14 | −4.57 [−5.67, −3.52] |
| Extent-free control | 74.09 | 71.67 | −3.14 [−4.19, −2.10] |
| ExtentSeg without area loss | 73.85 | 71.42 | −3.38 [−4.39, −2.35] |
| ExtentSeg | 74.59 | 72.26 | −2.63 [−3.62, −1.68] |
| ExtentSeg, true extent（讀遮罩） | 75.85 | 73.64 | −1.38 [−2.27, −0.50] |
| Retrained, matched caption（讀遮罩） | 76.00 | 73.65 | −1.22 [−2.01, −0.44] |
| Published, matched caption（讀遮罩） | 77.23 | 75.00 | - |

[(ref: main Table 5)](https://arxiv.org/html/2611.13970v1#S5.T5)

## 結果

- **增益有一部分不需要本圖的 caption** — 五個大腸鏡測試集合併時，別張圖的 caption 就拿回 39.7% [27.3, 50.8] 的增益；以影片序列重抽時區間放寬到 [4.9, 58.6]。沒有 caption 時，大腸鏡模型平均把外院影像的 12.3% 標成息肉，真實值為 6.8%；給別圖 caption 時降到 5.7%，作者據此認為 prior gain 主要是在校正「標多少面積」。[(ref: main §5.1.1)](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS1) [(ref: main Table D.2)](https://arxiv.org/html/2611.13970v1#A4.T2)
- **本圖特有的增益幾乎都在範圍詞上** — 大腸鏡五個測試集只留尺寸詞拿回 84.1–98.3%、刪掉它失去 51.8–77.2%；顏色詞比沒有 caption 還差，刪位置詞只損失 11.3% [7.9, 15.1]，刪數量詞沒有損失。QaTa-COV19 只留肺區片語，MedCLIPSeg 拿回 90.9%、RecLMIS 87.8%；事先登錄的刪除測試以 MedCLIPSeg 的措辭進行，損失 43.6% [41.3, 45.8]，未達 50% 的門檻。[(ref: main §5.1.2)](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS2)
- **BUSI 的 caption 還洩漏了診斷** — 65 句病灶 caption 中有 30 句寫出 benign 或 malignant，而且全部正確；只留尺寸詞拿回 30.6%，加上診斷詞 69.7%，刪尺寸詞失去 57.2%。[(ref: main §5.1.2)](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS2)
- **模型回應的是內容，不是醫學字彙** — 把 polyp 換成 rock，大腸鏡分數 +0.22；自創字「a zlorb region in the image.」只拿回 14.02 分增益中的 1.55 分；換成四種文體（含臨床句式）合併分數最多只差 2.1 分，但保留文體、清空內容則損失 16.1 到 24.0 分。[(ref: main §5.1.2)](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS2) [(ref: main Table D.4)](https://arxiv.org/html/2611.13970v1#A4.T4)
- **尺寸詞的作用不等於調門檻** — 對每個尺寸詞擬合一個固定 logit 偏移，在外院測試集只拿回尺寸詞效益的 44.7% [37.7, 51.7]；即使用每張圖自己的遮罩調偏移，也只到 70.98，低於只給尺寸詞的 74.49（n=578）。尺寸詞也會讓病灶消失：給 matched caption 時，681 個大腸鏡病灶有 22 個預測為空，給空白 caption 時沒有。[(ref: main §5.1.3)](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS3)
- **增益集中在小病灶** — 746 張有病灶的大腸鏡與 BUSI 影像中，面積小於 7.0% 的病灶增益 +19.13 [+17.02, +21.26]，7.0–17.9% 為 +4.91，大於 17.9% 為 +2.68 [−0.79, +6.31]。[(ref: main §5.1.3)](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS3)
- **依賴來自訓練 caption** — 大腸鏡五條準則全部達標；Size-only 只剩 19 種不同訓練 caption，仍保留 89.7% 的增益。QaTa-COV19 執行的準則全部達標（Zone-blind 只留 9.0%，Zone-only 91.0%）。BUSI 的 R3 未達標（49.9%），R4 未達標主要因無病灶影像。連 seed 一起重抽時，大腸鏡 R2 為 [26.0, 51.3]、R3 為 [50.7, 132.9]，兩者區間都跨過門檻，點估計仍在要求的一側。[(ref: main §5.2)](https://arxiv.org/html/2611.13970v1#S5.SS2) [(ref: main Appendix D)](https://arxiv.org/html/2611.13970v1#A4)
- **代價是只看影像時變差** — 給空白 caption 時，大腸鏡 Size-blind 比 Original 高 +2.39、Text-free 高 +2.82 [+2.11, +3.53]；BUSI 的 Size-blind 與 Text-free 分別高 +8.43 與 +13.43 [+8.41, +18.74]；QaTa-COV19 的 Zone-blind 高 +11.28。Mismatched 模型訓練時同樣沒見過空白 caption，卻高 +3.14 [+2.41, +3.86]，所以差距不是「caption 缺席」本身造成的。[(ref: main §5.3)](https://arxiv.org/html/2611.13970v1#S5.SS3)
- **只看 caption 就量得到洩漏** — 七個測試集中有六個的 *R*²_cap 在 0.54–0.77；CVC-300 只有 0.24，因為 60 句中 58 句都寫 small，但模型在該集的 *S*_ext 仍為 85.9%，作者因此指出低分不能證明基準乾淨。[(ref: main §5.4)](https://arxiv.org/html/2611.13970v1#S5.SS4)
- **不讀測試遮罩時沒有方法追上報告值** — 最佳的 ExtentSeg 為 74.59，比公開模型＋matched caption 的 77.23 低 2.63 [−3.62, −1.68]，比同配方的 Text-free 高 1.94 [+1.36, +2.55]；但「估計範圍」這個輸入相對 extent-free control 只多 0.59 [−0.02, +1.18]，未達事先登錄的門檻。[(ref: main §5.5)](https://arxiv.org/html/2611.13970v1#S5.SS5) [(ref: main Table B.1)](https://arxiv.org/html/2611.13970v1#A2)

## 限制

- **涵蓋範圍** — 公開 checkpoint 只有兩種架構、三種影像；重訓只做 MedCLIPSeg；RecLMIS 只在 QaTa-COV19 做測試時編輯；ExtentSeg 只在大腸鏡評估；只看影像時的退步發生在網路哪裡沒有分析。[(ref: main §6.3)](https://arxiv.org/html/2611.13970v1#S6.SS3)
- **BUSI 樣本小** — 範圍詞的貢獻只建立在 65 張影像上，排除 15 張近似重複的病灶影像後 *S*_ext 從 30.6% 變為 20.4%，重訓結論不變。[(ref: main §6.3)](https://arxiv.org/html/2611.13970v1#S6.SS3)
- **重訓結論對 seed 敏感** — 文字增益在三個 Original seed 之間差很多（大腸鏡 5.15–7.53、QaTa-COV19 10.85–19.10），連 seed 一起重抽時 R2／R3 的部分區間跨過門檻。[(ref: main §5.2)](https://arxiv.org/html/2611.13970v1#S5.SS2) [(ref: main Appendix D)](https://arxiv.org/html/2611.13970v1#A4)
- **準則登錄屬作者自律** — 「事先寫定」依作者的研究紀錄與 commit 時間；Kvasir-SEG 的準則在看過 R0–R2 單一 seed 結果後才首次 commit，RecLMIS 與文體測試的準則在結果之後才 commit，作者已在附錄逐項揭露。[(ref: main Appendix A)](https://arxiv.org/html/2611.13970v1#A1)
- **未測臨床文字** — 研究沒有測試醫師實際寫的描述；人口學與取像設備資訊多數資料集未提供；所有模型只在 224×224 輸入下測試。[(ref: main §6.1)](https://arxiv.org/html/2611.13970v1#S6.SS1) [(ref: main §6.3)](https://arxiv.org/html/2611.13970v1#S6.SS3)
- **重現性與利益衝突** — 作者的程式與修改版 caption 尚未公開；一位作者持有手術機器人公司股份。[(ref: main Data availability)](https://arxiv.org/html/2611.13970v1#Sx4) [(ref: main Competing interest)](https://arxiv.org/html/2611.13970v1#Sx2)
- **本書庫的判讀** — 本篇證明的是「這三個基準與這兩個模型的文字增益大多來自範圍洩漏」，不是「文字引導分割沒有用」；作者也指出臨床描述若能提供範圍，模型確實會用。[(ref: main §6.1)](https://arxiv.org/html/2611.13970v1#S6.SS1)

## 與書庫其他文章的關係

放療勾畫綜述把 counterfactual prompt 與 language ablation 列為尚未驗證的提示遵循測試提案，本篇在大腸鏡、乳房超音波與胸片的文字引導分割上實際執行這兩類測試，發現增益主要來自洩漏的病灶範圍: [放療勾畫綜述：VLM 對 nnU-Net 勝負未定，論點改押 CTV](2026-11-12-radiotherapy-segmentation-review-atlas-to-agentic-vlm.md)

病理 VLM 的控制實驗拿掉或換掉切片，看語言撐起多少答對率；本篇反過來逐項刪改文字提示，看分割增益靠的是哪一個字，兩篇都在問多模態模型的語言到底加了什麼: [語言替病理 VLM 加了什麼？拿掉切片，答對率只掉 0.4 個百分點](2026-11-04-pathology-vlm-language-controlled-probes.md)

胸片＋EHR 稽核發現 EHR 向量等於病人識別碼、查表就追平最佳模型，本篇則發現 caption 的尺寸詞由評分遮罩算出；兩篇都是基準的輸入帶進了測試時不該有的標籤資訊，也都先用不需學習的對照量出洩漏: [查表就追平最佳模型：胸片＋EHR 不平衡基準的病人洩漏](2026-11-06-cxr-ehr-imbalance-benchmark-patient-leakage.md)

## 實務的啟發

1. **評估吃文字的分割或 VLM 模型時，固定報三種 caption 的分數。** empty、mismatched、matched 三組加上 prior share，以及模板 caption 各屬性的 sufficiency／necessity，是作者的第 2 項建議；這組對照不需要新資料，就能分出「描述影像」與「給了答案的大小」。[(ref: main §6.2)](https://arxiv.org/html/2611.13970v1#S6.SS2)
2. **先查提示是怎麼產生的。** 測試時的 caption 若由遮罩計算，或由看著遮罩的標註者撰寫，就等於把部分標籤交給模型（作者第 1 項建議）。本書庫認為，院內若以報告句子當提示，也應確認報告是在判讀當下寫成，而不是依分割結果回頭補寫。[(ref: main §6.2)](https://arxiv.org/html/2611.13970v1#S6.SS2)
3. **釋出帶文字的資料集前，先跑 caption-only 分數。** 只需一個迴歸就能看出文字是否預告病灶大小；但 CVC-300 顯示分數低不代表沒有洩漏，仍需搭配 caption 編輯。[(ref: main §5.4)](https://arxiv.org/html/2611.13970v1#S5.SS4)
4. **對照同配方的 text-free 模型，並報多個 checkpoint。** 同一配方三個 seed 的文字增益可以差到近一倍，單一 checkpoint 的「文字帶來 X 分」不宜當作模型能力的定論。[(ref: main §5.2)](https://arxiv.org/html/2611.13970v1#S5.SS2)

這些是可借用的稽核方法；ExtentSeg 是本研究的參考上限，未經臨床或外部資料驗證，不宜視為可直接採用的分割方案。[(ref: main §5.5)](https://arxiv.org/html/2611.13970v1#S5.SS5)

## References

- `main` — Nataraj N, Das A, Mohan CK, Kawashima K. *Counterfactual Analysis of Extent Leakage from Annotation-Derived Prompts in Vision-Language Medical Image Segmentation*. arXiv:2611.13970v1, 2026. [https://arxiv.org/html/2611.13970v1](https://arxiv.org/html/2611.13970v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.13970v1)、[§1](https://arxiv.org/html/2611.13970v1#S1)、[§3.1](https://arxiv.org/html/2611.13970v1#S3.SS1)、[Table 1](https://arxiv.org/html/2611.13970v1#S3.T1)、[§3.2](https://arxiv.org/html/2611.13970v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.13970v1#S3.SS3)、[§4.1](https://arxiv.org/html/2611.13970v1#S4.SS1)、[§4.2](https://arxiv.org/html/2611.13970v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.13970v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.13970v1#S4.SS4)、[§4.5](https://arxiv.org/html/2611.13970v1#S4.SS5)、[§4.6](https://arxiv.org/html/2611.13970v1#S4.SS6)、[§4.7](https://arxiv.org/html/2611.13970v1#S4.SS7)、[§4.8](https://arxiv.org/html/2611.13970v1#S4.SS8)、[§4.9](https://arxiv.org/html/2611.13970v1#S4.SS9)、[§5.1.1](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS1)、[§5.1.2](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS2)、[§5.1.3](https://arxiv.org/html/2611.13970v1#S5.SS1.SSS3)、[Table 2](https://arxiv.org/html/2611.13970v1#S5.T2)、[§5.2](https://arxiv.org/html/2611.13970v1#S5.SS2)、[Table 3](https://arxiv.org/html/2611.13970v1#S5.T3)、[§5.3](https://arxiv.org/html/2611.13970v1#S5.SS3)、[§5.4](https://arxiv.org/html/2611.13970v1#S5.SS4)、[§5.5](https://arxiv.org/html/2611.13970v1#S5.SS5)、[Table 5](https://arxiv.org/html/2611.13970v1#S5.T5)、[§6.1](https://arxiv.org/html/2611.13970v1#S6.SS1)、[§6.2](https://arxiv.org/html/2611.13970v1#S6.SS2)、[§6.3](https://arxiv.org/html/2611.13970v1#S6.SS3)、[Competing interest](https://arxiv.org/html/2611.13970v1#Sx2)、[Funding](https://arxiv.org/html/2611.13970v1#Sx3)、[Data availability](https://arxiv.org/html/2611.13970v1#Sx4)、[Appendix A](https://arxiv.org/html/2611.13970v1#A1)、[Table B.1](https://arxiv.org/html/2611.13970v1#A2)、[Appendix C](https://arxiv.org/html/2611.13970v1#A3)、[Appendix D](https://arxiv.org/html/2611.13970v1#A4)、[Table D.2](https://arxiv.org/html/2611.13970v1#A4.T2)、[Table D.4](https://arxiv.org/html/2611.13970v1#A4.T4)、[Appendix E](https://arxiv.org/html/2611.13970v1#A5)
- `abstract` — arXiv abstract page, 2611.13970v1. [https://arxiv.org/abs/2611.13970v1](https://arxiv.org/abs/2611.13970v1)
- PDF v1：[https://arxiv.org/pdf/2611.13970v1](https://arxiv.org/pdf/2611.13970v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.13970](https://doi.org/10.48550/arXiv.2611.13970)

[Home](../) · [AI Papers](./)
