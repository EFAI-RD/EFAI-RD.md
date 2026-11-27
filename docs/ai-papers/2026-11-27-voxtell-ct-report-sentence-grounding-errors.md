---
parent: AI Papers
nav_order: 1
title: "CT 報告逐句分割：VoxTell 沒有一例分錯邊，錯在範圍與小病灶"
catalog_id: "arxiv:2611.33958"
editors:
  - "Clare"
refs:
  main:
    title: "Where Does Free-Text 3D Grounding Fail? An Error Analysis of Report-Sentence Segmentation in Chest CT"
    url: "https://arxiv.org/html/2611.33958v1"
  abs:
    title: "arXiv abstract page: 2611.33958v1"
    url: "https://arxiv.org/abs/2611.33958v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# CT 報告逐句分割：VoxTell 沒有一例分錯邊，錯在範圍與小病灶

## 來源

- 團隊：Abdullah Arif Sheikh（Department of Artificial Intelligence, Vidya Jyothi Institute of Technology, Hyderabad）、Kamalaker Dadi（通訊作者）與 Raju S. Bapi（IHub-Data, International Institute of Information Technology, Hyderabad）。[(ref: main title block)](https://arxiv.org/html/2611.33958v1) [(ref: abstract)](https://arxiv.org/abs/2611.33958v1)
- 論文：*Where Does Free-Text 3D Grounding Fail? An Error Analysis of Report-Sentence Segmentation in Chest CT*，arXiv:2611.33958v1（cs.CV），2026-11-25 提交，目前只有 v1；未註記發表場合；授權為 CC BY-NC-SA 4.0。[(ref: abstract)](https://arxiv.org/abs/2611.33958v1)
- 識別碼：arXiv [2611.33958](https://arxiv.org/abs/2611.33958v1)；DOI [10.48550/arXiv.2611.33958](https://doi.org/10.48550/arXiv.2611.33958)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.33958v1)、[PDF v1](https://arxiv.org/pdf/2611.33958v1)。
- 程式與資料：推論、評估與分析程式「可向通訊作者索取」，沒有公開網址；資料為公開的 CT-RATE 與 ReXGroundingCT（MICCAI 2026 challenge 版本）。[(ref: main Code availability)](https://arxiv.org/html/2611.33958v1#Sx1) [(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- 研究性質：錯誤分析研究，不提出新模型。作者以公開釋出的 VoxTell v1.1 權重實際推論 ReXGroundingCT 驗證集全部 381 個發現，並在隱藏標註的 300 例測試集上以官方排行榜複核；主要數值附以病人為單位的 bootstrap 95% CI。只分析一個模型，作者在限制中說明。論文致謝註明 AI 助手（Claude）協助撰寫分析程式與初稿，作者表示已核對所有實驗與結果。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1) [(ref: main §4)](https://arxiv.org/html/2611.33958v1#S4)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文與表 1、表 2 為準；論文圖 1–4 的病例影像未轉載，圖中個別病例的 Dice 只引用圖說寫出的數值。

**編輯：** Clare

把胸部 CT 報告的每一句話當成提示、要求模型在 3D 體積裡分割出那句話所指的區域，目前公開的 VoxTell 權重在 381 個驗證發現中命中 53.5%；它的失誤幾乎從不是找錯邊或認錯是哪一句，而是範圍畫太大、落在同側鄰近病灶，或完全漏掉小病灶。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3)

## 流程

![左右兩個面板的長條圖。左側 (a) 標題「Outcome per finding, full-sentence prompt (paper Sec. 2.3 / Sec. 3, validation set)」，由上而下六列：綠色長條「Hit (Dice ≥ 0.1)」204，四條橘色長條「Partial」61、「Elsewhere」61、「Empty」50、「Swapped」5，最後一列「Wrong side」標示 0、沒有長條；橫軸「Number of findings (n = 381)」。右側 (b) 標題「Hit rate by finding group and prompt (paper Table 1)」，縱軸「Hit rate (%)」，六組直條由左至右為 All (381)、Nodule (155)、Opacity/consolid. (57)、Atelectasis/scar (87)、Pleural (29)、Airway/emphysema (41)，每組三根：深藍「Full sentence」、淺藍「Location words removed」、灰色「Label only」，數值依序為 53.5／27.6／27.6、53.5／32.9／38.7、71.9／40.4／29.8、56.3／8.0／6.9、69.0／55.2／58.6、14.6／14.6／7.3，每根直條上方標數值。](assets/voxtell-grounding-error-types-and-prompt-ablation.png)

*圖：本書庫依論文 [§2.3](https://arxiv.org/html/2611.33958v1#S2.SS3) 的錯誤分類與 [§3](https://arxiv.org/html/2611.33958v1#S3) 的計數（左），以及 [表 1](https://arxiv.org/html/2611.33958v1#S3.T1) 的分組命中率（右）重繪；未轉載論文圖。左圖每個發現只歸入第一個符合的類型，綠色長條為命中、橘色長條為失誤類型，Wrong side 為 0 所以沒有長條；右圖的「Location words removed」與「Label only」是同一模型、同一批發現只改提示文字的對照。[(ref: main Table 1)](https://arxiv.org/html/2611.33958v1#S3.T1)*

## 背景／問題

free-text 3D grounding 指的是：給一句放射報告的句子（例如某肺葉某節段有兩顆 2 mm 結節），模型要在 CT 體積中分割出這句話所指的那個區域。作者引用 ReXGroundingCT 的論述，認為這可以讓讀者從報告句跳到對應病灶、在追蹤時比對報告過的發現、標出沒有影像證據的句子，並把報告庫轉成體素層級標註；這些是作者的應用設想，論文本身沒有驗證任何一項。[(ref: main §1)](https://arxiv.org/html/2611.33958v1#S1)

與固定類別分割或只接受短類別名稱的 label-prompted 模型不同，一句報告同時帶有發現類型、位置、數量、大小與描述詞。作者指出，label-prompted 基礎模型在 ReXGroundingCT 上大多失敗，而以大型語言模型編碼器嵌入自由文字的 VoxTell 在公開排行榜上領先；另一個先提出病灶候選、再把候選配給句子的兩階段方法則報告配對步驟貢獻了大部分增益，暗示「哪個病灶對應哪一句」是主要難點。作者認為尚無研究逐個發現量測最好的自由文字模型實際上怎麼失敗，因此做這份錯誤分析。[(ref: main §1)](https://arxiv.org/html/2611.33958v1#S1)

## 方法摘要

- **受試模型** — VoxTell v1.1 公開權重（voxtell 套件 v0.1.2），3D 卷積影像編碼器搭配凍結的 Qwen3-Embedding-4B 文字編碼器與多尺度視覺語言融合；作者不做任何訓練，使用官方 sliding-window 推論、不加 test-time augmentation 與後處理，每一句獨立嵌入與分割。[(ref: main §2.2)](https://arxiv.org/html/2611.33958v1#S2.SS2)
- **指標** — 依 challenge 協定，每個發現算預測與參考遮罩的 Dice，Dice ≥ 0.1 記為命中（hit）；case-level Dice 是一個病例所有發現 Dice 的平均，即排行榜排序指標。另把遮罩拆成連通元件（18-connectivity），以 Dice ≥ 0.2 一對一配對，算 instance precision、recall 與 F1。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- **錯誤分類** — 每個驗證發現歸入第一個符合的類型：hit、empty（完全沒有預測）、swapped（同一病例另一句的預測命中此病灶）、partial（有重疊但 Dice < 0.1）、wrong side（無重疊、句子指明一側，且 ≥ 70% 預測在中線另一側）、elsewhere（其餘失誤）。再依體積、發現類別、focal／non-focal 與句中指明的側別分層。[(ref: main §2.3)](https://arxiv.org/html/2611.33958v1#S2.SS3)
- **提示對照** — 刪除側別、肺葉、節段與區域詞後重跑；另只給短類別名稱（例如「lung nodule」），模擬 label-prompted 模型會收到的輸入。[(ref: main §2.4)](https://arxiv.org/html/2611.33958v1#S2.SS4)
- **文字衍生的後處理** — 三條不需訓練的規則：刪除句子指明側別對側的預測體素；刪除不在句中所指肺葉內的元件（肺葉遮罩取自 TotalSegmentator，元件至少有比例 t 落在肺葉內才保留）；只保留句子寫出的病灶數量。門檻在原公開驗證切分的 50 例上選定、在其餘 150 例上測試。[(ref: main §2.4)](https://arxiv.org/html/2611.33958v1#S2.SS4)

## 方法詳解

- **資料版本** — 使用 ReXGroundingCT 的 MICCAI 2026 challenge 版本：訓練 2,992 例、驗證 200 例（遮罩已公開，381 個發現）、測試 300 例（遮罩隱藏，582 個發現），驗證與測試不在訓練切分中。每個發現是一句報告句，附 focal（離散病灶）或 non-focal（瀰漫型態如肺氣腫）類別與一個可含多個病灶的 3D 遮罩。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- **遮罩對齊檢查** — 遮罩以 identity affine、CT 原生體素順序儲存，CT 則帶 LPS 標頭；若像 VoxTell 那樣把 CT 轉到 RAS 卻不對遮罩做同樣轉換，遮罩會在平面內旋轉 180°，例如實變遮罩落到含氣肺上（平均 −613 HU，原生對齊時為 −158 HU）。作者保留遮罩原生順序，把預測反轉回去再評估。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- **VoxTell 訓練資料與排行榜版本** — 依 VoxTell 作者的說法（論文標為 personal communication），公開權重的訓練資料涵蓋 158 個公開資料集（超過 62K 個體積），其中包含 ReXGroundingCT 訓練切分，但取樣頻率很低。VoxTell 論文與排行榜上的 ReXGroundingCT 成績來自另一個在該訓練切分上再微調、並使用 test-time augmentation 的版本，權重未公開。[(ref: main §2.2)](https://arxiv.org/html/2611.33958v1#S2.SS2)
- **分層方式** — 體積分三層：small（< 1,000 體素）、medium（1,000–10,000）、large（> 10,000）；發現類別由句子關鍵字分成 nodule、opacity/consolidation、atelectasis/scar、pleural、airway/emphysema 與 other。作者以參考遮罩所在側核對關鍵字抽出的側別，指明單側的 176 個發現中 175 個一致。[(ref: main §2.3)](https://arxiv.org/html/2611.33958v1#S2.SS3)
- **不確定性** — 95% CI 取自 2,000 次以 200 個病例為單位的 bootstrap，同一病人的發現一起重抽；設定間的差異用配對重抽。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- **硬體** — 每例推論 10–60 秒，使用 12 GB 的 RTX 3080 Ti。[(ref: main §2.2)](https://arxiv.org/html/2611.33958v1#S2.SS2)
- **論文未交代** — 程式只能向作者索取；刪除位置詞時用的詞表或規則、每個發現對應的 label-only 提示如何決定（只舉「lung nodule」一例）、分組用的關鍵字清單都沒有列出；VoxTell 公開權重的訓練資料是否含 ReXGroundingCT 訓練切分，只有 VoxTell 作者的私下說明作為依據；測試集比較用的三個排行榜前段方法沒有寫出名稱。[(ref: main §2.2)](https://arxiv.org/html/2611.33958v1#S2.SS2) [(ref: main §2.4)](https://arxiv.org/html/2611.33958v1#S2.SS4) [(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3)

## 資料與實驗

### 資料

| 切分（ReXGroundingCT，MICCAI 2026 版） | 病例數 | 發現數 | 遮罩 | 本研究用途 |
|---|---|---|---|---|
| 訓練 | 2,992 | 未列 | 公開 | 未使用（不做訓練） |
| 驗證 | 200 | 381（1,415 個病灶 instance） | 公開 | 主要錯誤分析與提示對照；後處理以其中 50 例選門檻、150 例測試 |
| 測試 | 300 | 582 | 隱藏 | 透過官方排行榜複核 |

ReXGroundingCT 為 CT-RATE 的 3,142 例非顯影胸部 CT 配上放射科醫師畫的 3D 遮罩；驗證集遮罩比訓練集標得更完整（每個發現平均 3.71 對 1.95 個 instance）。驗證發現體積從 17 體素到超過 300 萬體素（中位數 3,410，IQR 369–22,790），36% 小於 1,000 體素。[(ref: main §1)](https://arxiv.org/html/2611.33958v1#S1) [(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)

### 實驗：分層結果（論文表 1，驗證集 200 例、381 個發現）

| Stratum | n | Hit (%) | Dice | Empty (%) | No loc. Hit (%) | Label Hit (%) |
|---|---|---|---|---|---|---|
| All | 381 | 53.5 | 0.225 | 13.1 | 27.6 | 27.6 |
| Size：Small（< 10³） | 137 | 43.1 | 0.192 | 24.1 | 24.1 | 30.7 |
| Size：Medium | 100 | 42.0 | 0.171 | 9.0 | 19.0 | 22.0 |
| Size：Large（> 10⁴） | 144 | 71.5 | 0.295 | 5.6 | 36.8 | 28.5 |
| Group：Nodule | 155 | 53.5 | 0.237 | 20.0 | 32.9 | 38.7 |
| Group：Opacity/consolid. | 57 | 71.9 | 0.307 | 1.8 | 40.4 | 29.8 |
| Group：Atelectasis/scar | 87 | 56.3 | 0.201 | 13.8 | 8.0 | 6.9 |
| Group：Pleural | 29 | 69.0 | 0.332 | 6.9 | 55.2 | 58.6 |
| Group：Airway/emphysema | 41 | 14.6 | 0.052 | 7.3 | 14.6 | 7.3 |
| Focal | 329 | 59.0 | 0.249 | 13.7 | 29.2 | 29.2 |
| Non-focal | 52 | 19.2 | 0.076 | 9.6 | 17.3 | 17.3 |
| Side：Left | 76 | 68.4 | 0.323 | 3.9 | 30.3 | 35.5 |
| Side：Right | 100 | 63.0 | 0.271 | 14.0 | 15.0 | 26.0 |
| Side：Both | 168 | 43.5 | 0.167 | 14.9 | 34.5 | 27.4 |
| Side：None | 37 | 43.2 | 0.166 | 21.6 | 24.3 | 16.2 |

Hit = Dice ≥ 0.1；Hit、Dice、Empty 為完整句子提示；最後兩欄為刪除位置詞與只給類別名稱時的命中率。表中「Small」「Large」的體積單位為體素；「other」組的 12 個發現計入總數但未列出。[(ref: main Table 1)](https://arxiv.org/html/2611.33958v1#S3.T1)

### 實驗：提示對照與文字衍生後處理（論文表 2）

| Prompt（381 個發現） | Hit (%) | Dice | F1（instance） | Empty (%) | Wrong side |
|---|---|---|---|---|---|
| Full sentence | 53.5 | 0.225 | 0.174 | 13.1 | 0 |
| Location words removed | 27.6 | 0.104 | 0.122 | 30.2 | 33 |
| Label only | 27.6 | 0.123 | 0.122 | 31.2 | 19 |

| Post-processing rule（150 例保留病例） | Hit (%) | Dice | ΔDice 95% CI |
|---|---|---|---|
| None | 55.6 | 0.230 | – |
| Lobe（t = 0.25） | 55.6 | 0.231 | [−0.001, +0.001] |
| Lobe（t = 0.5） | 53.8 | 0.223 | [−0.016, −0.000] |
| Count | 55.3 | 0.229 | [−0.005, +0.001] |

Wrong side 為預測落在句子所指側對側的失誤數；ΔDice 為與不做後處理相比的配對、病人層級 bootstrap 95% CI。[(ref: main Table 2)](https://arxiv.org/html/2611.33958v1#S3.T2)

## 結果

- **整體** — 381 個驗證發現中命中 53.5%（95% CI 48.6–58.4），平均 Dice 0.225（0.203–0.250），case-level Dice 0.234。預測的病灶一旦對上參考病灶，分割品質不錯（Dice 0.517），但 instance precision 只有 0.131、recall 0.256：大約八個預測病灶中只有一個是放射科醫師標記的，標記病灶也只找到約四分之一。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3) [(ref: main Table 1)](https://arxiv.org/html/2611.33958v1#S3.T1)
- **失誤類型** — 177 個失誤中 partial 61、elsewhere 61、empty 50、swapped 5，wrong side 為 0。partial 失誤多是範圍太大：預測體積中位數為參考的 5.3 倍，62% 超過兩倍，以 airway/emphysema 與 atelectasis/scar 最常見。elsewhere 失誤中 28／61 是結節，模型在正確的一側分割了一顆結節，但不是句子描述的那顆。完全沒有預測的情形集中在小發現（small 24.1%，large 5.6%）。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3)
- **分層** — non-focal 發現的命中率遠低於 focal（19.2% 對 59.0%），airway/emphysema 最差（14.6%）；指明單側的句子命中 63–68%，雙側或未指明位置的句子 43%，後者多為瀰漫或多病灶發現。[(ref: main Table 1)](https://arxiv.org/html/2611.33958v1#S3.T1)
- **位置詞被實際使用** — 刪除位置詞後命中率從 53.5% 降到 27.6%（配對 95% CI −31.3 到 −21.0 點），Dice 從 0.225 降到 0.104（−0.144 到 −0.100），empty 從 13.1% 升到 30.2%，並出現 33 個 wrong side 失誤。只給類別名稱的命中率同為 27.6%，所以在同一個模型上，完整句子比類別名稱多約 26 點命中率（95% CI 21.1–31.0；Dice +0.080 到 +0.124）。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3) [(ref: main Table 2)](https://arxiv.org/html/2611.33958v1#S3.T2)
- **哪裡最靠位置詞** — 下降最多的是影像本身難以分辨的發現：atelectasis/scar 56.3% → 8.0%、nodule 53.5% → 32.9%、右側發現 63.0% → 15.0%；位置在影像上就很明顯的 pleural 只從 69.0% 降到 55.2%；airway/emphysema 原本就很少命中，兩種提示都是 14.6%。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3) [(ref: main Table 1)](https://arxiv.org/html/2611.33958v1#S3.T1)
- **解剖規則沒有幫助** — 側別規則在 381 個發現上 Dice 不變（0.225 → 0.225，差值 95% CI 0.0000–0.0002），因為根本沒有對側預測可刪。150 例保留病例上，肺葉規則寬門檻時中性、嚴門檻時有害，數量規則沒有提高 Dice；被刪掉的元件常含真病灶體素，因為參考遮罩會超出句中所指肺葉，或比句子寫的病灶數更多。刪除位置詞之後，側別規則才有小幅幫助（Dice 0.104 → 0.110，增益 95% CI 0.002–0.011）。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3) [(ref: main Table 2)](https://arxiv.org/html/2611.33958v1#S3.T2)
- **隱藏測試集** — 300 例（582 個發現）官方排行榜上，公開權重的 case-level Dice 0.210、排行榜命中率 48.5%、instance precision／recall／F1 為 0.080／0.250／0.122；前三名加上任務專屬訓練，case-level Dice 0.362–0.375。驗證集的型態在測試集重現：non-focal 命中 20.5%（15／73）、focal 52.5%（267／509），肺氣腫仍最難（27 個中命中 1 個）。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3)
- **作者的解讀** — 兩階段方法報告的配對瓶頸不適用於 VoxTell；主要錯誤在範圍估計與小病灶敏感度。對 non-focal 發現，模型會分割整個型態（例如所有增厚的支氣管壁），參考遮罩只標代表性區域，作者因此認為這類發現可能需要依發現類型調整的評估方式。[(ref: main §4)](https://arxiv.org/html/2611.33958v1#S4)

## 限制

- **只有一個模型、公開版本** — 作者明說只分析釋出形式的單一模型。VoxTell 作者在 ReXGroundingCT 上微調並使用 test-time augmentation 的版本，在較早的 50 例公開驗證切分上報告 28.2% Dice，公開權重在同 50 例上為 21.4%，其錯誤型態可能不同。論文沒有對其他 grounding 模型做同樣的分析。[(ref: main §4)](https://arxiv.org/html/2611.33958v1#S4)
- **分組與解剖遮罩是自動產生** — 發現類別由關鍵字切分，肺葉遮罩來自 TotalSegmentator，作者只核對了側別一項（175／176 一致）。[(ref: main §4)](https://arxiv.org/html/2611.33958v1#S4) [(ref: main §2.3)](https://arxiv.org/html/2611.33958v1#S2.SS3)
- **單一機構資料** — CT-RATE 來自單一機構，作者把在其他模型與外部多中心資料（包括印度族群）上重複分析列為未來工作。[(ref: main §4)](https://arxiv.org/html/2611.33958v1#S4)
- **寬鬆的命中門檻** — Dice ≥ 0.1 的命中定義獎勵「找到位置」而非範圍正確；命中率 53.5% 與平均 Dice 0.225 之間的落差，正是作者指出的範圍問題，讀者在引用命中率時應同時看 Dice 與 instance precision。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- **重現細節不足** — 程式只能索取，位置詞刪除規則、label-only 提示與分組關鍵字未列出，VoxTell 訓練資料的組成只有私下說明作為依據。[(ref: main Code availability)](https://arxiv.org/html/2611.33958v1#Sx1) [(ref: main §2.2)](https://arxiv.org/html/2611.33958v1#S2.SS2)

## 與書庫其他文章的關係

EviGround-CT 自己訓練一個以整句為查詢的 3D 驗證器、在 ReXGroundingCT 保留子集上查核生成報告，本篇則在同一資料集的完整驗證集上拆解現成 VoxTell 的失誤；兩篇都碰到參考遮罩與句子內容不完全對應的問題: [EviGround-CT：CT 報告逐句送去定位查核，參考遮罩並不完整](2026-10-30-eviground-ct-sentence-grounding-report-verification.md)

文字引導分割那篇發現 2D 分割的文字增益主要來自洩漏的病灶範圍詞，本篇在 3D CT 上用同樣的刪詞對照，發現 VoxTell 真正依賴的是位置詞，而範圍反而是它最弱的部分: [文字引導分割的增益：只留病灶範圍詞就拿回 84–98%](2026-11-12-extent-leakage-text-guided-segmentation.md)

LesionAgent 把 VoxTell 當成以文字提示提出候選病灶的工具，再用其他模型與代理自我驗證；本篇量出 VoxTell 單獨使用時 instance precision 只有 0.131、小病灶常漏，與 LesionAgent 在工具外層加上驗證的設計相呼應: [LesionAgent：固定規則誤判惡化 33 次，加上代理判讀只剩 2 次](2026-11-24-lesionagent-longitudinal-ct-recist-agent.md)

## 實務的啟發

- **可借用的量測方法** — 評估以報告句為提示的分割模型時，除了命中率與 Dice，加上「逐發現的錯誤分類（empty／swapped／partial／wrong side／elsewhere）」與「刪除位置詞、只給類別名稱」兩個同模型對照，能分出模型是不會讀位置、還是讀得懂但範圍估錯。這套對照不需重新訓練。[(ref: main §2.3)](https://arxiv.org/html/2611.33958v1#S2.SS3) [(ref: main §2.4)](https://arxiv.org/html/2611.33958v1#S2.SS4)
- **先檢查遮罩方向** — ReXGroundingCT 的遮罩與 CT 標頭方向不同，重新定向時沒同步處理會讓遮罩旋轉 180°；用公開 grounding 資料做評估前，先以 HU 值之類的簡單檢查確認遮罩落在對的位置。[(ref: main §2.1)](https://arxiv.org/html/2611.33958v1#S2.SS1)
- **待驗證的警訊** — 本研究中，依句子內容加的解剖後處理沒有提高 VoxTell 的完整句子輸出，嚴格的肺葉規則還有害；若要在報告—影像連結流程中加規則，應先用類似的保留集證明有效。這個結論只在一個模型、一個單機構資料集上成立。[(ref: main Table 2)](https://arxiv.org/html/2611.33958v1#S3.T2) [(ref: main §4)](https://arxiv.org/html/2611.33958v1#S4)
- **把命中率讀成「找到位置」** — 公開權重的 instance precision 0.131 代表多數預測病灶沒有對應的參考標記，小病灶與瀰漫型發現又最常失敗；在把這類模型的輸出當成體素標註或追蹤比對依據之前，需要依發現類型與大小分開驗證。[(ref: main §3)](https://arxiv.org/html/2611.33958v1#S3) [(ref: main Table 1)](https://arxiv.org/html/2611.33958v1#S3.T1)

## References

- `main` — Abdullah Arif Sheikh, Kamalaker Dadi, Raju S. Bapi. *Where Does Free-Text 3D Grounding Fail? An Error Analysis of Report-Sentence Segmentation in Chest CT*. arXiv:2611.33958v1, 2026. HTML：https://arxiv.org/html/2611.33958v1 ；用到的深鏈：[§1](https://arxiv.org/html/2611.33958v1#S1)、[§2.1](https://arxiv.org/html/2611.33958v1#S2.SS1)、[§2.2](https://arxiv.org/html/2611.33958v1#S2.SS2)、[§2.3](https://arxiv.org/html/2611.33958v1#S2.SS3)、[§2.4](https://arxiv.org/html/2611.33958v1#S2.SS4)、[§3](https://arxiv.org/html/2611.33958v1#S3)、[Table 1](https://arxiv.org/html/2611.33958v1#S3.T1)、[Table 2](https://arxiv.org/html/2611.33958v1#S3.T2)、[§4](https://arxiv.org/html/2611.33958v1#S4)、[Code availability](https://arxiv.org/html/2611.33958v1#Sx1)
- `abstract` — arXiv abstract page, 2611.33958v1：https://arxiv.org/abs/2611.33958v1 （PDF：https://arxiv.org/pdf/2611.33958v1 ；DOI：https://doi.org/10.48550/arXiv.2611.33958）

[Home](../) · [AI Papers](./)
