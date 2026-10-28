---
catalog_id: "arxiv:2610.05425"
editors:
  - "Clare"
refs:
  main:
    title: "Unmentioned Checklist Findings Change How Reinforcement Learning Appears to Improve Chest Radiograph Report Checking"
    url: "https://arxiv.org/pdf/2610.05425v1"
  abs:
    title: "arXiv abstract page: 2610.05425"
    url: "https://arxiv.org/abs/2610.05425"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 「沒提到」算不算「沒有」？RL 訓練的胸片 checklist 讓報告句查核在保留病人上 Y 升 12.6%，但換一個查核模型或格式，量到的增益就跟著變

## 來源

- 團隊：University of Rochester 的 Department of Computer Science、Department of Electrical and Computer Engineering、Department of Biomedical Engineering，與 University of Rochester Medical Center（URMC）Department of Imaging Sciences；作者為 Ali Vosoughi（通訊作者）、Akhil Kasturi、Chenliang Xu、Axel Wismueller。[(ref: main author block)](https://arxiv.org/pdf/2610.05425v1)
- 論文：*Unmentioned Checklist Findings Change How Reinforcement Learning Appears to Improve Chest Radiograph Report Checking*，arXiv v1，2026-10-04 投稿；分類 cs.CV、cs.CL、cs.LG。[(ref: abs)](https://arxiv.org/abs/2610.05425)
- 識別碼：[arXiv:2610.05425](https://arxiv.org/abs/2610.05425)；未見期刊或會議版本。
- 全文：[arXiv PDF v1](https://arxiv.org/pdf/2610.05425v1)（含 Supplementary Information）。
- 程式與資料：作者表示程式、prompts、配對識別碼、存下的 checklist 與判定結果會隨 GitHub repository `ali-vosoughi/VerifyGRPO-Rad` 釋出；CheXpert Plus 影像須依其研究使用協議另行申請，不隨論文重新散布。[(ref: main Code availability, Data availability)](https://arxiv.org/pdf/2610.05425v1)
- 研究性質：完整研究，不是 pilot；核心方法（盲化 checklist 模型的 GRPO 訓練）已實作，以 3 個 seed 重複訓練並附病人群組 bootstrap 95% 區間。標籤由 CheXpert labeler 從報告文字自動抽取，沒有放射科醫師判定；保留測試病人來自同一個資料集，不是外部驗證。[(ref: main Methods, Discussion)](https://arxiv.org/pdf/2610.05425v1)
- 證據邊界：本文數值以 v1 PDF 的正文與 Table 1–4 為準；Supplementary Information 的逐次執行數值（如 Table S5、S6）、OLMo-2-7B 與 Qwen3-VL-30B-A3B 的接受率只在補充資料中呈現，未納入本文引述。

**編輯：** Clare

作者訓練一個只看胸片、看不到待查句子的 checklist 模型，再讓另一個只看 checklist 與句子的模型判定句子是否成立；在保留測試病人上，兩個未參與訓練的查核方式量到的 pair-level Youden index（Y）分別升了 12.6 與 11.8 個百分點，但把 checklist 換成訓練時的格式、或換一個查核模型，量到的增益就往不同方向移動，原因是各模型對「checklist 沒提到的發現」如何解讀並不一致。[(ref: main Abstract, Table 2)](https://arxiv.org/pdf/2610.05425v1)

## 流程

![盲化兩步驟設計示意圖。四個圓角方塊由左到右排成一列，以三支實線箭頭依序相連；最上方標題為 Blinded two-step design: the image reaches the verdict only through the checklist。藍色方塊「1 Matched pairs (CheXpert Plus)」：Two frontal studies: report-derived labels agree on 11 findings, differ on the target finding；Sentence: real report sentence from the source study；Train 4,501 images / 3,974 pts；Val 237 pairs, held-out 273 pairs。綠色方塊「2 Checklist model (sees image only)」：Qwen3-VL-8B-Instruct + LoRA；Input: radiograph + fixed instruction, never the sentence；Output: 12-finding checklist (present/absent, side, box, note)；Findings may be left unmentioned。橘色方塊「3 Checker (sees checklist + sentence)」：Never sees the image；Training checker: frozen Qwen3-VL-8B；Independent checker: MedGemma-4B；Rule-based check: no language model；Verdict: supported / unsupported。紫色方塊「4 Metrics per pair」：Right = accept on source image, reject on matched image；Y = G - B (pair-level Youden)；FA = rejection of label-consistent sentence on source image；Labels: CheXpert labeler, not radiologist-adjudicated。一支灰色虛線弧形箭頭從橘色方塊下緣指回綠色方塊下緣，下方斜體文字為 Training only: reward 1 if the training checker's verdict matches the label (GRPO, 16 checklists per image)。](assets/unmentioned-findings-rl-cxr-checking-design.png)

圖：本書庫依論文 Methods、Figure 2 與 Table 1 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的研究設計圖為 Figure 2）。四個方塊以實線箭頭表示評估時的資料流；虛線弧形箭頭只在訓練時存在，表示 reward 由凍結的 training checker 判定後回饋給 checklist 模型。[(ref: main Methods, Figure 2, Table 1)](https://arxiv.org/pdf/2610.05425v1)

## 背景／問題

作者在開頭引用兩篇文獻，說明 AI 已被用來比對放射報告的敘述與影像。[(ref: main Introduction)](https://arxiv.org/pdf/2610.05425v1) 論文要處理的問題比較窄：若讓模型先把影像寫成一份結構化 checklist，再由另一個模型依 checklist 判斷某句報告是否成立，checklist 沒有提到的發現該算「不存在」還是「沒評估」？作者主張，除非事先規定，查核模型沒有共同的約定，只能自己決定。這個主張在引言中沒有引用文獻，證據來自論文自己的實驗：八個查核模型對同一類句子的接受率從 1.0% 到 97.0% 不等（見下方「結果」）。[(ref: main Introduction, Table 4)](https://arxiv.org/pdf/2610.05425v1)

這個問題之所以會影響「訓練有沒有效」的判斷，是因為 reward 由某一個凍結的查核模型給出。如果訓練時把未提到的發現一律補成「absent」，而評估時換成另一個模型或另一種格式，量到的增益就混進了「格式約定」的效果，而不只是「checklist 是否更忠實描述影像」。論文的主要貢獻是把這兩者拆開量測。[(ref: main Results «Switching to the training format…»)](https://arxiv.org/pdf/2610.05425v1)

## 方法摘要

**任務。** 每個樣本是一對 CheXpert Plus 正面胸片（matched pair）：兩份檢查由報告抽出的 12 項標籤有 11 項相同，只在目標發現上不同；待查句是來源檢查報告中的真實句子（例如 "No pleural effusions."），對來源影像成立、對配對影像不成立。[(ref: main Methods «Data and matched pairs»)](https://arxiv.org/pdf/2610.05425v1)

**盲化兩步驟。** checklist 模型（Qwen3-VL-8B-Instruct 加 LoRA）只看胸片與固定指令、看不到句子，輸出 12 項發現的 checklist（present／absent、側別、可選的框與註記），允許某些發現不寫；查核模型只看 checklist 與句子、看不到影像，回傳 supported 或 unsupported。影像只能經由 checklist 影響判定。[(ref: main Methods «Blinded checklist model and checking model»)](https://arxiv.org/pdf/2610.05425v1)

**訓練。** 以 GRPO 訓練 checklist 模型：每張影像取 16 份 checklist，凍結的 training checker（同一個 Qwen3-VL-8B 基礎模型）判定結果與報告標籤一致則 reward 為 1，否則為 0。訓練時 checklist 會先被修整成固定順序、未提到的發現補成 absent，這就是論文所說的 training format。[(ref: main Methods «Reward and training»)](https://arxiv.org/pdf/2610.05425v1)

**評估。** 三種查核方式：training checker、未參與訓練的 independent checker（MedGemma-4B），以及不用語言模型的 rule-based check。主要指標是 pair-level Youden index `Y = G − B`（G 為兩張影像都判對的比例，B 為兩張都判錯的比例；不看影像的查核器得 0），與 false-alarm rate（FA，來源影像上與標籤一致的句子被否定的比例）。[(ref: main Methods «Metrics», Table 1)](https://arxiv.org/pdf/2610.05425v1)

## 方法詳解

**配對篩選。** 驗證池原有 507 對（943 位病人），保留測試集原有 548 對；兩者都再加一條規則：句子在不給影像時須被基礎模型接受，避免句子因與影像無關的理由在配對影像上被否定。篩選後驗證集為 238 對（458 位病人、221 個病人群組），終點分析用 237 對；保留測試集 274 對，終點分析用 273 對、格式重讀用 270 對。[(ref: main Methods «Data and matched pairs»)](https://arxiv.org/pdf/2610.05425v1)

**12 項 checklist。** Enlarged Cardiomediastinum、Cardiomegaly、Lung Opacity、Lung Lesion、Edema、Consolidation、Pneumonia、Atelectasis、Pneumothorax、Pleural Effusion、Pleural Other、Fracture。[(ref: main Supplementary S2.2)](https://arxiv.org/pdf/2610.05425v1)

**訓練設定。** LoRA rank 16、α 32，只加在語言層、影像編碼器凍結；GRPO 每張影像 16 份 checklist、temperature 1、最多 1,024 個新 token、每步 8 張影像、learning rate 1e-4、KL penalty 0.01、共 40 步並使用 dynamic sampling；每次訓練用 3 張 48 GB A6000，三個 seed 為 101、202、303。[(ref: main Methods «Reward and training», Supplementary S4)](https://arxiv.org/pdf/2610.05425v1)

**rule-based check。** 若 checklist 對句子所指發現的 present／absent 標記與句子的極性一致即判 supported；未提到的發現視為 absent。它的判定不隨 checklist 格式改變。[(ref: main Methods «Checkers and checklist formats»)](https://arxiv.org/pdf/2610.05425v1)

**四種 checklist 格式。** (1) as generated：模型自己的順序，未提到的留空，這是評估預設；(2) 固定順序、未提到的省略；(3) 模型的順序、未提到的補成 absent；(4) training format：固定順序、未提到的補成 absent。作者特別指出，補上 absent 等於替模型加了一句它沒說過的話。[(ref: main Methods «Checkers and checklist formats», Table 3)](https://arxiv.org/pdf/2610.05425v1)

**預先設定與統計。** 複製實驗的判準是：每個未參與訓練的查核方式，三次訓練平均的 ΔY ≥ 5% 且區間下限大於 0，同時 ΔFA 的單側 95% 上限 ≤ 5%。這份判準在訓練工作啟動後、讀取任何複製實驗的 checklist 之前寫定；兩個查核器在 training format 下的差異也是預先設定。格式差異拆成「順序」與「補上 absent」兩部分、保留測試集的格式重讀、其餘六個查核模型則是事後分析。作者說明這些紀錄是有日期的專案紀錄，未登錄在公開 registry，會隨程式一起釋出。統計採病人群組層級的配對 bootstrap（2,000 次）、雙尾 95% percentile 區間；探索性與事後區間未做多重比較校正。[(ref: main Methods «Prespecification and statistics»)](https://arxiv.org/pdf/2610.05425v1)

**對照與延伸。** 以 training checker 先讀句子、再讀影像的 sentence-first reading 作為參考判定（可加 chain-of-thought）；未訓練的 checklist 作為基線；另有懲罰未提到發現的 reward 變體、以 supervised learning 直接學寫 checklist 的 direct supervision、換成 Qwen2.5-VL-7B 的第二個 checklist 模型，以及在 VQA v2／COCO 2014 照片上的純推論對照研究（516 對）。[(ref: main Methods «Reference verdicts», «Direct supervision», «Photograph study»)](https://arxiv.org/pdf/2610.05425v1)

- **論文未交代** — 保留測試集的病人人數（正文只給配對數與 245 個病人群組）與 CheXpert Plus 的總抽取規模。
- **論文未交代** — 論文本身的授權條款；預先設定的紀錄未在公開 registry 登錄，讀者目前無法獨立核對哪些分析在讀資料前已定案。
- **論文未交代** — direct supervision 與 Qwen2.5-VL-7B 都只做單次或開發階段比較，沒有與主實驗相同的三 seed 重複，兩者的增益差距沒有不確定性可以對照。

## 資料與實驗

### 資料

| 用途 | 來源 | 規模 | 說明 |
|---|---|---|---|
| 訓練 | CheXpert Plus 正面胸片 | 4,501 張單影像 prompt，3,974 位病人 | 另有 64 張影像（53 位病人）的訓練監測集 |
| 驗證 | CheXpert Plus matched pairs | 原 507 對（943 位病人）→ 238 對（458 位病人、221 群組）；終點 237 對 | 經「無影像時句子須被接受」規則篩選 |
| 保留測試 | CheXpert Plus matched pairs（訓練與驗證以外的病人） | 原 548 對 → 274 對；終點 273 對、格式重讀 270 對（245 群組） | 同一資料集內的病人切分，非外部資料 |
| 照片對照 | VQA v2／COCO 2014 complementary pairs | 516 對 | 純推論，20 種物件是否存在 |

標籤皆由 CheXpert labeler 從報告文字自動抽出。[(ref: main Methods «Data and matched pairs», «Photograph study»)](https://arxiv.org/pdf/2610.05425v1)

### 實驗：訓練前後的 Y 與 FA（論文 Table 2）

數值為百分比；ΔY 與 ΔFA 為三次訓練的平均變化，ΔY 附 95% 區間，ΔFA 括號內為單側 95% 上限。預設判準只適用於未參與訓練的兩種查核方式。

| 查核方式 | 族群 | 訓練前 Y | 訓練前 FA | ΔY [95%] | ΔFA（上限） |
|---|---|---|---|---|---|
| Rule-based check | 驗證（237 對） | 3.0 | 45.1 | +8.3 [+2.0, +14.1] | +1.7（+6.6） |
| Independent checker（MedGemma-4B） | 驗證（237 對） | 2.1 | 36.3 | +7.0 [+0.4, +13.3] | +4.4（+9.6） |
| Training checker（Qwen3-VL-8B） | 驗證（237 對） | 4.6 | 46.0 | +3.8 [−1.0, +8.2] | +12.0（+15.9） |
| Rule-based check | 保留測試（273 對） | 3.3 | 40.7 | +12.6 [+6.9, +18.2] | −2.7（+1.9） |
| Independent checker（MedGemma-4B） | 保留測試（273 對） | 2.2 | 35.9 | +11.8 [+5.2, +18.6] | +3.4（+8.8） |
| Training checker（Qwen3-VL-8B） | 保留測試（273 對） | 4.0 | 49.1 | +6.6 [+2.3, +11.0] | +6.8（+11.2） |

[(ref: main Table 2)](https://arxiv.org/pdf/2610.05425v1)

### 實驗：查核模型如何解讀「未提到」（論文 Table 4 節錄）

接受率指：句子否定某發現、而 checklist 沒有提到該發現、且句子與標籤一致時，查核模型判 supported 的比例（預設指令；驗證 100 個判定、保留測試 127 個判定）。

| 查核模型 | 接受率，驗證（%） | 接受率，保留測試（%） |
|---|---|---|
| Training checker（Qwen3-VL-8B） | 64.0 | 53.5 |
| MedGemma-4B | 79.0 | 74.0 |
| Gemma-3-4B | 1.0 | 1.6 |
| Gemma-3-12B | 91.0 | 91.3 |
| Gemma-3-27B | 56.0 | 50.4 |

Phi-4-mini 在驗證集為 97.0%（見正文，未列於 Table 4）。[(ref: main Table 4, Results «Checking models disagree…»)](https://arxiv.org/pdf/2610.05425v1)

## 結果

- **保留測試的增益** — rule-based check 的 Y 升 12.6 個百分點 [6.9, 18.2]、ΔFA 上限 1.9%，是唯一同時通過增益與誤報兩項判準的查核方式；MedGemma-4B 升 11.8 個百分點 [5.2, 18.6]，但 ΔFA 上限 8.8%，未通過誤報判準。驗證集上兩者的增益判準都通過，誤報判準都沒有通過，因此預設的聯合判準在驗證集上不成立。[(ref: main Table 2, Methods «Prespecification and statistics»)](https://arxiv.org/pdf/2610.05425v1)
- **格式讓兩個查核器往反方向走** — 改用 training format 讀同一批 checklist，training checker 的 ΔY 從 +3.8 升到 +6.0，independent checker 從 +7.0 降到 +3.1；預先設定的兩查核器差異為 +6.2 個百分點 [2.0, 10.5]（驗證 237 對），保留測試的事後重讀為 +7.7 [2.8, 12.8]（270 對）。[(ref: main Table 3, Results «Switching to the training format…»)](https://arxiv.org/pdf/2610.05425v1)
- **查核模型之間的分歧** — 對「checklist 沒提到、句子否定該發現」的同一類句子，八個查核模型的接受率從 1.0%（Gemma-3-4B）到 97.0%（Phi-4-mini）。[(ref: main Abstract, Table 4)](https://arxiv.org/pdf/2610.05425v1)
- **照片上沒有對應效應** — VQA v2／COCO 照片對照中，兩查核器的差異為 −0.7 個百分點 [−2.1, +0.7]。[(ref: main Results «No comparable effect…»)](https://arxiv.org/pdf/2610.05425v1)
- **懲罰未提到的發現** — reward 扣去「未提到發現比例 × 0.25」後，三次訓練的 checklist 都列滿 12 項；training checker 的 FA 上升幅度減少 5.5 個百分點，rule-based check 的 FA 上升增加 3.5 個百分點，Y 沒有偵測到變化。[(ref: main Results «Penalizing unmentioned findings…»)](https://arxiv.org/pdf/2610.05425v1)
- **增益集中在少數發現** — 作者指出增益跟著 reward 有訊號的地方走：訓練時 edema 與 pleural effusion 有 42%–48% 的樣本群組帶有 reward 訊號（16 份 checklist 的平均 reward 介於 0 與 1 之間），pneumothorax、lung lesion、fracture 只有 2%–4%；在保留測試集拿掉 48 對 pleural effusion 後，兩個未參與訓練的查核方式仍有 +9.2 [3.3, 15.1] 與 +9.8 [2.3, 17.3]。shuffle 對照中，三次訓練的 rule-based check 真實 Y 為 13.9%、12.2%、7.6%，各自高於打亂 checklist 後的最大值 8.8%、8.0%、6.7%。[(ref: main Results «The trained checklists carry image-specific information…», Figure 3b, Supplementary S1.5)](https://arxiv.org/pdf/2610.05425v1)
- **對照組的位置** — sentence-first reading 在驗證集為 Y 10.1%、FA 37.0%（加 chain-of-thought 為 11.3%、21.0%）；單次的 direct supervision 讓 rule-based check 的 Y 升 15.1 個百分點 [7.3, 22.6]，同一比較中 RL 為 +9.7；換成 Qwen2.5-VL-7B 當 checklist 模型只有 +2.1 [−3.3, +7.7]，模型收斂到只列一項發現。[(ref: main Methods «Reference verdicts», Results «Direct supervision and a second checklist model…»)](https://arxiv.org/pdf/2610.05425v1)

## 限制

**作者自述的限制。** 標籤自動抽取、未經放射科醫師判定；保留病人來自同一資料集，不是外部驗證；只用單一正面影像，沒有前次影像或臨床脈絡；independent checker 的誤報判準未成立；增益集中在 pleural effusion、edema、consolidation 等少數發現；配方無法轉移到 Qwen2.5-VL-7B；區間只反映病人變異，條件於僅有的三個訓練模型；direct supervision 的單次增益較大；格式拆分與保留測試重讀是事後分析；新增的六個查核模型每個尺寸只有一個，無法分開模型家族、大小與醫療微調的影響；照片對照接近天花板，沒有重現效應也無法解釋原因。[(ref: main Discussion)](https://arxiv.org/pdf/2610.05425v1)

**本書庫的觀察。**

- **Y 的起點很低** — 訓練前三種查核方式的 Y 只有 2.1%–4.6%，訓練後最好的保留測試值約 16%（3.3 + 12.6）；這是「看得出配對兩張圖差別」的比例扣掉「兩張都錯」，絕對值仍小，且不採盲化 checklist 的 sentence-first reading 在驗證與保留測試上有 10.1%–16.1%（含 chain-of-thought 版本）。論文的重點是增益怎麼被量到，不是這套查核已經堪用。
- **「判對」是對報告標籤而言** — 所有 Y 與 FA 都以 CheXpert labeler 的輸出為準，標籤本身的錯誤會同時進入 reward 與評估。
- **格式效應本身是一個量測工具** — 同一批 checklist 只改格式、不改模型，就能讓兩個查核器的增益差 6 個百分點；這說明比較兩篇以 LLM 判定為指標的報告查核研究時，查核模型與 checklist 格式需要一起報告。

## 與書庫其他文章的關係

兩篇都在檢驗「換一個評估條件，結論還剩多少」：該稽核在胸片結核篩檢上逐項替換提示詞、負類與閾值，本篇則固定 checklist、只替換查核模型與格式，結果同樣是排名與增益隨評估約定移動: [稽核胸片結核篩檢的醫療 VLM：換一個評估條件，哪一種結論還站得住？](2026-09-21-cxr-tb-vlm-portability-audit.md)

該研究顯示胸片報告的語意相似度不能代理 Findings 的結構保真度，本篇則顯示即使改用結構化 checklist，以 LLM 判定句子是否成立時，「未提到」的解讀約定仍會改變量到的分數，兩篇都在拆解胸片報告評估指標本身的假設: [報告讀起來很順，就代表寫對了嗎？RadVLM 的分節評估](2026-09-22-radvlm-section-based-report-evaluation.md)

## 實務的啟發

- **可借用的量測方法** — 用 LLM 當評審或 reward 時，把 checklist 的格式與「未提到」的約定當成實驗變因：同一批輸出換一個未參與訓練的評審、換一種格式各讀一次，若增益方向不一致，就表示部分增益來自約定而非內容。
- **報告查核指標應附誤報率** — 本篇只有 rule-based check 在保留測試同時守住增益與誤報；只看 Y 或準確率會漏掉「把正確的否定句判錯」這一側的代價。
- **待驗證的方向** — 結果來自單一資料集、報告標籤、三次訓練與 8B 以下的模型；這套盲化 checklist 能否在放射科醫師判定的標籤、外部資料或前後次比較上維持增益，論文沒有測試。
- **證據強度** — 它支持「RL 讓 checklist 帶有影像特異資訊，但量到的增益大小取決於評審與格式」；不足以支持這套 checklist 查核可直接用於臨床報告品管，作者也明言標籤未經放射科醫師判定。

## References

- **main** — Vosoughi A, Kasturi A, Xu C, Wismueller A. *Unmentioned Checklist Findings Change How Reinforcement Learning Appears to Improve Chest Radiograph Report Checking*. arXiv:2610.05425v1 (2026). 全文 PDF：<https://arxiv.org/pdf/2610.05425v1>。文內引用位置：author block、Abstract、Introduction、Results 各小節、Discussion、Methods（Data and matched pairs、Blinded checklist model and checking model、Reward and training、Checkers and checklist formats、Metrics、Reference verdicts、Direct supervision、Prespecification and statistics、Photograph study、Code availability）、Data availability、Table 1–4、Figure 2、Figure 3b、Supplementary S1.5、S2.2、S4。
- **abs** — arXiv abstract page：<https://arxiv.org/abs/2610.05425>。

[Home](../) · [AI Papers](./)
