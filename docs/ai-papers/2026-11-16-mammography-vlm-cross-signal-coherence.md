---
parent: AI Papers
nav_order: 2
title: "拿掉乳房攝影影像，MedGemma 仍以約 95 分信心給 BI-RADS"
catalog_id: "arxiv:2611.12574"
editors:
  - "Clare"
refs:
  main:
    title: "Evaluating Cross-Signal Coherence in Mammography Vision-Language Models"
    url: "https://arxiv.org/html/2611.12574v1"
  abs:
    title: "arXiv abstract page: 2611.12574v1"
    url: "https://arxiv.org/abs/2611.12574v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 拿掉乳房攝影影像，MedGemma 仍以約 95 分信心給 BI-RADS

## 來源

- 團隊：Emory University 資訊工程系（Rebeca Nam、Chase M. Fensore、Joyce C. Ho）與放射暨影像科學系（Christian A. Fauria-Robinson、Judy Gichoya）；第一作者 Rebeca Nam 同時標示 Yonsei University。[(ref: main author block)](https://arxiv.org/html/2611.12574v1)
- 論文：*Evaluating Cross-Signal Coherence in Mammography Vision-Language Models*，arXiv:2611.12574v1（cs.CV；另列 cs.CL、cs.LG），2026-11-09 提交，目前只有 v1；arXiv 頁未註記投稿或接受的會議期刊；授權為 arXiv 非專屬散布授權。[(ref: abstract)](https://arxiv.org/abs/2611.12574v1)
- 識別碼：arXiv [2611.12574](https://arxiv.org/abs/2611.12574v1)；DOI [10.48550/arXiv.2611.12574](https://doi.org/10.48550/arXiv.2611.12574)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.12574v1)、[PDF v1](https://arxiv.org/pdf/2611.12574v1)。
- 程式與資料：資料來自公開的 MammoVQA 基準；論文註腳給出的程式連結是匿名審稿用的 anonymous.4open.science 儲存庫，不是具名的長期存放處；論文未見經費與利益衝突聲明。[(ref: main author block)](https://arxiv.org/html/2611.12574v1) [(ref: main §3.2)](https://arxiv.org/html/2611.12574v1#S3.SS2)
- 研究性質：對四個公開權重 VLM 的推論稽核，不訓練模型；不是 pilot，RSNA 與 EMBED 兩個子集共約 2.5 萬題、六種條件都已實際執行並有數字；主要比例未附信賴區間，顯著性只對兩種 elicitation 擾動做 McNemar 檢定。[(ref: main §3)](https://arxiv.org/html/2611.12574v1#S3) [(ref: main §8.4)](https://arxiv.org/html/2611.12574v1#S8.SS4)
- 證據邊界：本文數值以 arXiv v1 HTML 版的正文與 Table 1–9 為準；Figure 3、5、6 的長條與曲線只引用作者在正文寫出的數字，不從圖上讀值。

**編輯：** Clare

作者讓四個開放 VLM 對 MammoVQA 的乳房攝影題同時給出答案、每個選項的信心分數與一句理由，再把影像換成無關照片、空白圖或直接拿掉；在 RSNA 的 BI-RADS 題上，MedGemma-4B 在這三種情況下仍然選 0% 的「None of the above」，對自己選的類別給出約 95 分的信心。[(ref: main §4.2)](https://arxiv.org/html/2611.12574v1#S4.SS2) [(ref: main Table 2)](https://arxiv.org/html/2611.12574v1#S4.T2)

## 流程

![左右兩欄圖。左欄標題「Six conditions per MammoVQA item (RSNA, EMBED)」，下方為兩欄共七個圓角框：左欄四個淺藍底、深藍實線框，由上而下為「Original：real mammogram + question, K options + NOTA」、「Visual: unrelated：mammogram replaced by an unrelated natural photo」、「Visual: blank：mammogram replaced by a blank grayscale image」、「Visual: no image：image omitted; question text only」；右欄最上方一個淺橘底、橘色實線框「Read 3 signals from 1 response：answer letter / per-option confidence 0-100 / one-sentence reason」，其下兩個淺藍底、深藍實線框「Elicitation: question：domain terms neutralized ("mammogram" → "image")」與「Elicitation: options：options shuffled + filler distractors added」；右欄最下方為兩行斜體小字「Target on visual conditions = NOTA」「Greedy decoding, 384 tokens」（無外框）；左下角小字「Redrawn by EFAI-RD from arXiv:2611.12574v1 Sections 3.3-3.6」。右欄為長條圖，標題「Table 2: RSNA BI-RADS, 'None of the above' selected」，縱軸「NOTA selection rate (%)」刻度 0–100；橫軸四個模型依序為 MedGemma-4B、Lingshu-7B、Qwen2-VL-7B、InternVL3-8B，每組左為灰色「Real image」、右為橘色「Visual perturbations (avg of 3)」，長條上方標示數值：MedGemma-4B 0.0、0.0；Lingshu-7B 0.0、20.6；Qwen2-VL-7B 62.8、91.7；InternVL3-8B 13.7、91.0。](assets/mammography-vlm-coherence-conditions-and-nota.png)

*圖：本書庫依論文 §3.3–3.6 重繪的六種評估條件與單次回應中讀出的三種訊號（左），以及 RSNA BI-RADS 題在真實影像與三種視覺擾動（平均）下選擇「None of the above」（NOTA）的比例（右）。數值來自 [Table 2](https://arxiv.org/html/2611.12574v1#S4.T2)。*

## 背景／問題

作者的出發點是：VLM 判讀醫學影像時，輸出不只是一個標籤，還常附帶信心與文字理由，但領域裡的評估仍以答案準確率為主。這是作者對現行評估習慣的描述，論文以胸片 VQA 基準與兩個乳房攝影 VLM 的評估方式為例，沒有另外統計有多少研究只報準確率。[(ref: main §1)](https://arxiv.org/html/2611.12574v1#S1) [(ref: main §2)](https://arxiv.org/html/2611.12574v1#S2)

既有研究多半一次只檢查一種訊號：答案對選項排列敏感、模型在沒有正確選項時傾向硬選、信心與推理各自可能不校準或不忠實。作者要問的是另一件事：同一次回應裡的答案、信心與理由彼此是否一致，三者是否都隨影像證據改變。[(ref: main §1)](https://arxiv.org/html/2611.12574v1#S1) 選乳房攝影作為測試場景，是因為乳腺密度（ACR A–D）與 BI-RADS（0–6）都是有序、多類別且有標準詞彙的任務，錯誤、信心與理由可以分級比較。[(ref: main §1)](https://arxiv.org/html/2611.12574v1#S1)

## 方法摘要

- **資料** — MammoVQA 基準中最大的兩個子集：RSNA 篩檢乳房攝影（BI-RADS 與乳腺密度兩種任務，單張影像）與 EMBED（只做 BI-RADS，一題包含整次檢查的多張影像）。[(ref: main §3.2)](https://arxiv.org/html/2611.12574v1#S3.SS2)
- **一次讀出三種訊號** — 以 Matchmaker 形式的選擇題提示，要模型寫出單一答案字母、為每個選項各給 0–100 的信心分數，再寫一句理由；選項之外一律加上「None of the above」（NOTA）。[(ref: main §3.3)](https://arxiv.org/html/2611.12574v1#S3.SS3)
- **六種條件** — 原圖，加上三種視覺擾動（換成無關照片、換成空白灰階圖、不給影像）與兩種 elicitation 擾動（改寫題目用語、打亂選項並加入填充選項）。視覺擾動下的正確反應是選 NOTA。[(ref: main §3.4)](https://arxiv.org/html/2611.12574v1#S3.SS4)
- **四個開放模型** — 醫療模型 MedGemma-4B、Lingshu-7B，通用模型 Qwen2-VL-7B、InternVL3-8B；未量化、greedy decoding。[(ref: main §3.6)](https://arxiv.org/html/2611.12574v1#S3.SS6)
- **一致性指標** — 答案與理由是否一致（A／B／C／D 四類 coherence taxonomy）、信心是否追隨證據、NOTA 是否只在證據消失時增加、打亂選項後答案是否翻轉。[(ref: main §3.5)](https://arxiv.org/html/2611.12574v1#S3.SS5)

## 方法詳解

- **題目規模** — RSNA 有 5,106 題 BI-RADS、5,821 題乳腺密度；EMBED 有 14,303 題 BI-RADS。每題為一張（RSNA）或多張（EMBED）影像，配模板化問題、固定選項與基準標籤。majority-class prior 分別為 59.4%、42.6%、62.1%。[(ref: main §3.2)](https://arxiv.org/html/2611.12574v1#S3.SS2) [(ref: main Table 4)](https://arxiv.org/html/2611.12574v1#S7.T4)
- **提示** — 要求三步：寫出單一最佳答案字母；對每個選項獨立給 0–100 的信心（不必加總為 100）；寫一句理由。不強制正規化，使模型可在證據不足時對所有選項都給低分。[(ref: main Figure 2)](https://arxiv.org/html/2611.12574v1#S3.F2) [(ref: main §3.3)](https://arxiv.org/html/2611.12574v1#S3.SS3)
- **為何加 NOTA** — 原本的 MammoVQA 是沒有拒答選項的封閉選擇題；影像被換掉之後所有原始選項都不正確，沒有 NOTA 就無法區分「有依據的拒答」與「亂猜」。作者因此同時報兩種準確率：對原始標籤，以及視覺擾動下以 NOTA 為正解的 NOTA-aware 準確率。[(ref: main §3.3)](https://arxiv.org/html/2611.12574v1#S3.SS3) [(ref: main §3.4)](https://arxiv.org/html/2611.12574v1#S3.SS4)
- **EMBED 的擾動** — EMBED 一次檢查有 1–15 個 view，模型同時看全部；擾動時保留張數，把每張換成空白圖或不同的無關照片。[(ref: main §9)](https://arxiv.org/html/2611.12574v1#S9)
- **理由的判讀** — 以規則式 matcher 從理由中抽出類別：先找「BI-RADS」或「density／ACR／category／level」等提示詞後面的類別字元，再以官方定義做語意對應（例如「almost entirely fatty」→ A）。作者隨機抽 120 句理由由一位標註者盲審，matcher 與人工的 Cohen's κ 為 0.78（80.8% 一致）；另以 gpt-oss-20b 做 LLM judge 比對，約 8,000 句上與 matcher 一致約 70.6%。無法解析的理由不計入理由準確率的分母。[(ref: main §3.5)](https://arxiv.org/html/2611.12574v1#S3.SS5) [(ref: main §8.1)](https://arxiv.org/html/2611.12574v1#S8.SS1) [(ref: main Table 6)](https://arxiv.org/html/2611.12574v1#S8.T6)
- **Coherence taxonomy** — 對有可解析理由的題目，依「答案是否正確」×「理由是否正確」分成 A（皆對）、B（答案對、理由錯）、C（答案錯、理由對）、D（皆錯）；在信心 ≥ 90 的錯誤中，C 佔 C＋D 的比例稱為 recoverable rate。[(ref: main §3.5)](https://arxiv.org/html/2611.12574v1#S3.SS5)
- **信心與 NOTA 指標** — 追蹤模型放在正確選項上的信心 c_y 與放在所選選項上的信心 c_ŷ；NOTA 敏感度以三種視覺擾動的 NOTA 選擇率平均減去真實影像的 NOTA 選擇率計算。[(ref: main §3.5)](https://arxiv.org/html/2611.12574v1#S3.SS5)
- **推論設定** — Hugging Face 預設 checkpoint（google/medgemma-4b-it、lingshu-medical-mllm/Lingshu-7B、Qwen/Qwen2-VL-7B-Instruct、OpenGVLab/InternVL3-8B），bfloat16、temperature 0、輸出上限 384 token；四個模型使用相同指令，只差各自的 chat template。作者以「公開權重、可比較醫療與通用訓練、參數量都在 4–8B」為選模理由，乳房攝影專用 VLM 因未釋出權重而未納入。[(ref: main §3.6)](https://arxiv.org/html/2611.12574v1#S3.SS6) [(ref: main Table 3)](https://arxiv.org/html/2611.12574v1#S6.T3)
- **論文未交代** — 改寫題目時被中性化的完整術語清單（只舉「mammogram」→「image」一例）、填充選項的完整清單（只舉「Not Assessable」「Not Applicable」）、無關照片的來源與空白圖的灰階值，以及 NOTA 選項在提示中的確切措辭。[(ref: main §3.4)](https://arxiv.org/html/2611.12574v1#S3.SS4)
- **論文未交代** — 主要比例（準確率、NOTA 選擇率、翻轉率）沒有信賴區間；各類別的完整標籤分布「備索」而未列出；matcher 的人工驗證只有一位標註者、120 句。[(ref: main §7)](https://arxiv.org/html/2611.12574v1#S7) [(ref: main §3.5)](https://arxiv.org/html/2611.12574v1#S3.SS5)

## 資料與實驗

### 資料

| 項目 | RSNA（MammoVQA 子集） | EMBED（MammoVQA 子集） |
|---|---|---|
| 任務 | BI-RADS（0–6）、乳腺密度（ACR A–D） | 只有 BI-RADS |
| 題數 | BI-RADS 5,106；密度 5,821 | BI-RADS 14,303 |
| 每題影像 | 單張乳房攝影 | 整次檢查，1–15 個 view 同時輸入 |
| Majority-class prior | BI-RADS 59.4%；密度 42.6% | BI-RADS 62.1%（BI-RADS 1） |
| 題型 | 模板化選擇題＋固定選項＋基準標籤 | 同左 |

[(ref: main §3.2)](https://arxiv.org/html/2611.12574v1#S3.SS2) [(ref: main Table 4)](https://arxiv.org/html/2611.12574v1#S7.T4) [(ref: main §9)](https://arxiv.org/html/2611.12574v1#S9)

### 實驗

真實影像、直接作答下的準確率與 NOTA 選擇率，節錄自 Table 1（括號為 majority-class prior）：

| Model | RSNA BI-RADS acc. % (59.4) | RSNA BI-RADS NOTA % | RSNA 密度 acc. % (42.6) | RSNA 密度 NOTA % | EMBED BI-RADS acc. % (62.1) | EMBED BI-RADS NOTA % |
|---|---|---|---|---|---|---|
| MedGemma-4B | 42.4 | 0.0 | 33.9 | 0.0 | 36.7 | 0.0 |
| Lingshu-7B | 12.0 | 0.0 | 49.3 | 0.0 | 10.3 | 0.0 |
| Qwen2-VL-7B | 2.9 | 62.8 | 24.8 | 33.2 | 15.2 | 0.7 |
| InternVL3-8B | 7.7 | 13.7 | 42.0 | 0.0 | 5.1 | 0.1 |

[(ref: main Table 1)](https://arxiv.org/html/2611.12574v1#S4.T1)

RSNA 上真實影像與三種視覺擾動（平均）的 NOTA 選擇率，節錄自 Table 2（Δ = Visual − Real，單位為百分點）：

| Model | BI-RADS Real % | BI-RADS Visual % | BI-RADS Δ | 密度 Real % | 密度 Visual % | 密度 Δ |
|---|---|---|---|---|---|---|
| MedGemma-4B | 0.0 | 0.0 | +0.0 | 0.0 | 12.7 | +12.7 |
| Lingshu-7B | 0.0 | 20.6 | +20.6 | 0.0 | 20.9 | +20.9 |
| Qwen2-VL-7B | 62.8 | 91.7 | +28.9 | 33.2 | 81.5 | +48.3 |
| InternVL3-8B | 13.7 | 91.0 | +77.3 | 0.0 | 75.3 | +75.3 |

[(ref: main Table 2)](https://arxiv.org/html/2611.12574v1#S4.T2)

打亂選項並加入填充選項後的正確性變化，節錄自 Table 8 的 Options 列（RSNA；C→W 與 W→C 為題數；* 為 McNemar exact test p < 0.05）：

| Model | Task | Orig. % | Pert. % | C→W | W→C | Net Δ (pp) |
|---|---|---|---|---|---|---|
| MedGemma-4B | BI-RADS | 42.5 | 17.7 | 1685 | 431 | −24.8* |
| MedGemma-4B | 密度 | 33.9 | 21.7 | 1406 | 697 | −12.2* |
| Lingshu-7B | BI-RADS | 14.3 | 5.5 | 433 | 68 | −8.9* |
| Lingshu-7B | 密度 | 48.5 | 39.8 | 1169 | 777 | −8.7* |
| Qwen2-VL-7B | BI-RADS | 2.4 | 1.6 | 103 | 68 | −0.8* |
| Qwen2-VL-7B | 密度 | 25.4 | 15.9 | 760 | 263 | −9.5* |
| InternVL3-8B | BI-RADS | 7.7 | 21.0 | 81 | 701 | +13.4* |
| InternVL3-8B | 密度 | 41.8 | 40.8 | 813 | 763 | −1.0 |

[(ref: main Table 8)](https://arxiv.org/html/2611.12574v1#S8.T8)

答案與理由在同一批可解析題目上的準確率，節錄自 Table 5（RSNA）與 Table 9（EMBED BI-RADS）（Δ = 理由 − 答案）：

| Model | 資料／任務 | Parsed % | Answer acc. % | Reasoning acc. % | Δ (pp) |
|---|---|---|---|---|---|
| MedGemma-4B | RSNA BI-RADS | 99.8 | 42.4 | 35.8 | −6.7 |
| Lingshu-7B | RSNA BI-RADS | 97.6 | 12.3 | 16.6 | +4.3 |
| Qwen2-VL-7B | RSNA BI-RADS | 66.3 | 3.7 | 7.1 | +3.4 |
| InternVL3-8B | RSNA BI-RADS | 96.4 | 7.9 | 11.4 | +3.5 |
| MedGemma-4B | EMBED BI-RADS | 96.3 | 36.8 | 20.9 | −15.9 |
| Lingshu-7B | EMBED BI-RADS | 99.8 | 10.3 | 57.6 | +47.3 |
| Qwen2-VL-7B | EMBED BI-RADS | 91.4 | 15.4 | 2.3 | −13.1 |
| InternVL3-8B | EMBED BI-RADS | 82.4 | 4.8 | 4.7 | −0.1 |

[(ref: main Table 5)](https://arxiv.org/html/2611.12574v1#S8.T5) [(ref: main Table 9)](https://arxiv.org/html/2611.12574v1#S9.T9)

## 結果

- **BI-RADS 沒有一個模型贏過全猜多數類** — RSNA BI-RADS 的 majority-class prior 為 59.4%，四個模型最高只有 MedGemma 的 42.4%；乳腺密度則有模型接近或超過基準（Lingshu 49.3% 對 42.6%）。真實影像上主動選 NOTA 的只有 Qwen（BI-RADS 62.8%、密度 33.2%），這也是它 BI-RADS 準確率只有 2.9% 的原因之一。[(ref: main Table 1)](https://arxiv.org/html/2611.12574v1#S4.T1)
- **答案與理由一致，但多半一起錯** — RSNA 上答案錯、理由對的 C 類在每個模型與任務都低於 5%；BI-RADS 最大的類別是兩者都錯的 D 類：MedGemma 56%、Lingshu 83%、InternVL 89%、Qwen 92%，兩者都對的 A 類只有 3–34%。乳腺密度較緩和（A 為 32–48%、D 為 52–67%）。[(ref: main §4.1)](https://arxiv.org/html/2611.12574v1#S4.SS1)
- **答對不代表理由成立** — 作者舉一張基準標籤為 BI-RADS 0 的檢查：InternVL 選 BI-RADS 0 而被算對，理由卻寫「正常、無異常」（對應 BI-RADS 1）；MedGemma 依同樣的「正常」讀法選 BI-RADS 1 而被算錯。準確率因此獎勵了理由自相矛盾的模型。[(ref: main §4.1)](https://arxiv.org/html/2611.12574v1#S4.SS1) [(ref: main Figure 4)](https://arxiv.org/html/2611.12574v1#S4.F4)
- **信心不追隨證據** — 在 RSNA BI-RADS，MedGemma 在真實影像上對正確類別的平均信心為 60.3，影像被換掉後掉到接近 0，但它仍然選一個類別，對所選答案的信心約 95；Qwen 則相反，幾乎不看影像都選 NOTA，真實影像上 c_y 只有 2.9、無效影像上 75–100。乳腺密度同樣分成兩種失效（MedGemma 43.0→1.0；Lingshu 不給影像時 46.8→0.0）。[(ref: main §4.2)](https://arxiv.org/html/2611.12574v1#S4.SS2)
- **該拒答時多半不拒答** — RSNA BI-RADS 的三種視覺擾動下，MedGemma 選 NOTA 的比例仍為 0%，密度題為 12.7%；Lingshu 只升到約 21%，等於五張無效影像中約有四張仍給出類別。只有 InternVL 與 Qwen 在多數無效影像上拒答（75–92%），但密度題仍有最多約四分之一給出類別。[(ref: main §4.3)](https://arxiv.org/html/2611.12574v1#S4.SS3) [(ref: main Table 2)](https://arxiv.org/html/2611.12574v1#S4.T2)
- **打亂選項，多數答案跟著變** — 只改選項順序並加入填充選項，RSNA 上答案改變的比例為 40–99%（BI-RADS 上 MedGemma 77%、InternVL 57%；密度 55–78%）；改變多半是由錯變錯，淨效果以傷害為主（MedGemma BI-RADS −24.8 個百分點，InternVL 則 +13.4）。Qwen 在 BI-RADS 與密度分別有 99% 與 75% 的答案改變，主要是改選新加入的 NOTA 或填充選項。八個 model × task 格中有七格的變化方向達 McNemar 顯著。[(ref: main §4.4)](https://arxiv.org/html/2611.12574v1#S4.SS4) [(ref: main Table 8)](https://arxiv.org/html/2611.12574v1#S8.T8)
- **改寫題目影響小** — 中性化題目用語後，BI-RADS 有 5–22%、密度有 3–38% 的答案改變，但淨準確率變化只在 −5.4 到 +1.8 個百分點之間；作者據此認為脆弱性來自選項結構，而不是措辭。[(ref: main §8.3)](https://arxiv.org/html/2611.12574v1#S8.SS3)
- **EMBED 的例外：Lingshu 理由對、答案錯** — 在 EMBED BI-RADS，Lingshu 的理由有 57.6% 指向正確類別，答案卻只有 10.3%，C 類達 54.6%；作者描述為無論理由如何都落在固定錯誤類別的輸出崩塌。MedGemma 在 EMBED 上對所選答案的信心從真實影像的 57 升到空白或無影像的 95，InternVL 也從 18.5 升到 57.6。[(ref: main §9.1)](https://arxiv.org/html/2611.12574v1#S9.SS1) [(ref: main §9.2)](https://arxiv.org/html/2611.12574v1#S9.SS2)

## 限制

- **題型限定** — 評估只用 MammoVQA 的模板化選擇題，部分選項順序與措辭的敏感度可能來自題型本身；作者未測自由作答或報告生成。[(ref: main §5.1)](https://arxiv.org/html/2611.12574v1#S5.SS1)
- **模型範圍** — 只測四個 4–8B 的公開權重模型；乳房攝影專用 VLM 未釋出權重而未納入，領域專用微調能否改善這些失效仍未知。[(ref: main §5.1)](https://arxiv.org/html/2611.12574v1#S5.SS1) [(ref: main §3.6)](https://arxiv.org/html/2611.12574v1#S3.SS6)
- **擾動種類** — 沒有測試臨床上更貼近的變化，例如左右側或 view 對調、同一病人的前次影像。[(ref: main §5.1)](https://arxiv.org/html/2611.12574v1#S5.SS1)
- **理由判讀的精度** — matcher 只在 120 句上做人工驗證，各模型的可解析比例差異大（RSNA BI-RADS 從 Qwen 的 66.3% 到 MedGemma 的 99.8%）；作者說明 matcher 與 LLM judge 的分歧多出現在「描述發現但未寫類別」的理由，因此 matcher 的比例是保守下限。[(ref: main §5.1)](https://arxiv.org/html/2611.12574v1#S5.SS1) [(ref: main §8.1)](https://arxiv.org/html/2611.12574v1#S8.SS1)
- **信心的定義** — 信心是模型自述的 0–100 分數，各選項獨立給分、不構成機率分布；作者未與 logit 機率比較，也無法判斷理由是模型實際決策過程還是事後合理化。[(ref: main §5)](https://arxiv.org/html/2611.12574v1#S5) [(ref: main §5.1)](https://arxiv.org/html/2611.12574v1#S5.SS1)
- **重現與揭露** — 主要比例沒有信賴區間；改寫用語、填充選項、無關照片與空白圖的完整設定未列出；完整標籤分布備索；程式只有匿名審稿連結；論文未見經費與利益衝突聲明。[(ref: main §3.4)](https://arxiv.org/html/2611.12574v1#S3.SS4) [(ref: main §7)](https://arxiv.org/html/2611.12574v1#S7)
- **本書庫的判讀** — 結果描述的是這四個 checkpoint 在「選擇題＋NOTA＋自述信心」這套 elicitation 下的行為；RSNA 一題只給單張影像，與放射科醫師看完整次檢查的篩檢判讀情境不同，因此絕對準確率不宜讀成臨床表現。

## 與書庫其他文章的關係

兩篇都用 MedGemma-4B 與 Lingshu-7B 做推論稽核並發現高信心的錯誤：氣胸稽核在胸片是非題上看到模型對陽性一律答「沒有」，本篇則在乳房攝影選擇題上看到影像被拿掉後模型仍以約 95 分信心給出類別: [胸片 VLM 稽核：兩個模型對 432 例氣胸全答「沒有」](2026-11-16-pneumothorax-silent-failure-medical-vlm.md)

CARE-MVLM 以移除病灶的反事實視圖訓練乳房攝影 VLM 棄答與給出證據框；本篇不訓練模型，而是在加入 NOTA 選項後量測現成 VLM 在影像被換掉時是否棄答，兩篇都把「證據消失時是否改口」當成乳房攝影 VLM 的必要檢查: [把病灶抹掉，VLM 會改口說無法判斷嗎？四項同時成立只有 4.75%](2026-10-07-care-mvlm-mammography-counterfactual-abstention.md)

Lingshu 原論文以醫療 VQA 平均分數呈現能力，本篇則顯示 Lingshu-7B 在 RSNA 乳腺密度上準確率 49.3% 居四個模型之首，但在 EMBED BI-RADS 上理由有 57.6% 指向正確類別、答案卻只有 10.3%: [Lingshu 靠合成資料拉高醫療 VQA，強化學習那一步沒加分](2026-09-15-lingshu-medical-vlm.md)

## 實務的啟發

1. **評估影像 VLM 時，同時檢查答案、信心與理由。** 本篇的 coherence taxonomy 與 NOTA-aware 準確率是可以借用的量測方法；作者的例子顯示，只看答案會把理由自相矛盾的回答算成正確。[(ref: main §3.5)](https://arxiv.org/html/2611.12574v1#S3.SS5) [(ref: main §4.1)](https://arxiv.org/html/2611.12574v1#S4.SS1)
2. **把「拿掉影像」與「打亂選項」列為基本對照。** 拒答率要與真實影像上的拒答率一起看，才能分辨有依據的拒答與固定的拒答傾向；選項順序一換就翻轉多數答案的模型，其準確率不能當成讀圖能力。[(ref: main §5)](https://arxiv.org/html/2611.12574v1#S5) [(ref: main §4.4)](https://arxiv.org/html/2611.12574v1#S4.SS4)
3. **不要把自述信心當成可靠度訊號。** 本篇中 MedGemma 在無效影像上仍給約 95 分；本書庫認為，若院內流程打算以信心門檻篩選自動判讀，應先在影像被移除或替換的情境下確認信心會下降，這仍是待各自驗證的前提，不是本篇已證實的做法。[(ref: main §4.2)](https://arxiv.org/html/2611.12574v1#S4.SS2)
4. **結果是警訊，不是選型排名。** 四個模型在 BI-RADS 上都低於全猜多數類，而且評估只限選擇題；本篇適合用來設計稽核項目，不適合用來決定哪個模型可用於篩檢。[(ref: main Table 1)](https://arxiv.org/html/2611.12574v1#S4.T1) [(ref: main §5.1)](https://arxiv.org/html/2611.12574v1#S5.SS1)

## References

- `main` — Nam R, Fensore CM, Fauria-Robinson CA, Gichoya J, Ho JC. *Evaluating Cross-Signal Coherence in Mammography Vision-Language Models*. arXiv:2611.12574v1, 2026. [https://arxiv.org/html/2611.12574v1](https://arxiv.org/html/2611.12574v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.12574v1)、[§1](https://arxiv.org/html/2611.12574v1#S1)、[§2](https://arxiv.org/html/2611.12574v1#S2)、[§3](https://arxiv.org/html/2611.12574v1#S3)、[§3.2](https://arxiv.org/html/2611.12574v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.12574v1#S3.SS3)、[Figure 2](https://arxiv.org/html/2611.12574v1#S3.F2)、[§3.4](https://arxiv.org/html/2611.12574v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.12574v1#S3.SS5)、[§3.6](https://arxiv.org/html/2611.12574v1#S3.SS6)、[Table 1](https://arxiv.org/html/2611.12574v1#S4.T1)、[§4.1](https://arxiv.org/html/2611.12574v1#S4.SS1)、[Figure 4](https://arxiv.org/html/2611.12574v1#S4.F4)、[§4.2](https://arxiv.org/html/2611.12574v1#S4.SS2)、[Table 2](https://arxiv.org/html/2611.12574v1#S4.T2)、[§4.3](https://arxiv.org/html/2611.12574v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.12574v1#S4.SS4)、[§5](https://arxiv.org/html/2611.12574v1#S5)、[§5.1](https://arxiv.org/html/2611.12574v1#S5.SS1)、[Table 3](https://arxiv.org/html/2611.12574v1#S6.T3)、[§7](https://arxiv.org/html/2611.12574v1#S7)、[Table 4](https://arxiv.org/html/2611.12574v1#S7.T4)、[§8.1](https://arxiv.org/html/2611.12574v1#S8.SS1)、[Table 5](https://arxiv.org/html/2611.12574v1#S8.T5)、[Table 6](https://arxiv.org/html/2611.12574v1#S8.T6)、[§8.3](https://arxiv.org/html/2611.12574v1#S8.SS3)、[§8.4](https://arxiv.org/html/2611.12574v1#S8.SS4)、[Table 8](https://arxiv.org/html/2611.12574v1#S8.T8)、[§9](https://arxiv.org/html/2611.12574v1#S9)、[§9.1](https://arxiv.org/html/2611.12574v1#S9.SS1)、[§9.2](https://arxiv.org/html/2611.12574v1#S9.SS2)、[Table 9](https://arxiv.org/html/2611.12574v1#S9.T9)
- `abstract` — arXiv abstract page, 2611.12574v1. [https://arxiv.org/abs/2611.12574v1](https://arxiv.org/abs/2611.12574v1)
- PDF v1：[https://arxiv.org/pdf/2611.12574v1](https://arxiv.org/pdf/2611.12574v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.12574](https://doi.org/10.48550/arXiv.2611.12574)

[Home](../) · [AI Papers](./)
