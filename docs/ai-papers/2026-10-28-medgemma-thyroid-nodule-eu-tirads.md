---
catalog_id: "doi:10.64898/2026.10.21.26366156"
editors:
  - "Clare"
refs:
  main:
    title: "Fine-tuned Medical Vision-Language Model (MedGemma 1.5 4B) with and without Structured Radiologist Descriptors versus EU-TIRADS for Malignancy Risk Stratification of Thyroid Nodules at Ultrasound: A Tunisian Multicenter Diagnostic Accuracy Study"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf"
  abs:
    title: "medRxiv abstract page: 10.64898/2026.10.21.26366156v1"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 甲狀腺結節超音波交給微調 MedGemma 1.5 4B：只給影像與尺寸 AUROC 約 0.89，加上放射科醫師的 11 個描述詞才追平 EU-TIRADS，但 EU-TIRADS 本身就由同一組描述詞推得

## 來源

- 團隊：University of Monastir 的 Faculty of Medicine of Monastir、Mahdia 的 Taher Sfar University Hospital（內分泌科、耳鼻喉科）、Tunis 的 CERU 與 Mahdia 的放射科、Ariana 與 Sousse 的病理科，以及一位巴黎的獨立電腦工程師；作者依序為 Mohamed Nour Bou Ali（通訊作者）、Najoua Lassoued、Houssem Mahmoud、Emna Mnif、Slim Haouet、Khaled Ben Rhouma、Mohamed Khaled Elsakly、Mehdi Hasnaoui。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1)
- 論文：*Fine-tuned Medical Vision-Language Model (MedGemma 1.5 4B) with and without Structured Radiologist Descriptors versus EU-TIRADS for Malignancy Risk Stratification of Thyroid Nodules at Ultrasound: A Tunisian Multicenter Diagnostic Accuracy Study*，medRxiv v1 預印本，2026-10-24 張貼，未經同儕審查；授權 CC BY-NC-ND 4.0。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1)
- 識別碼：DOI [10.64898/2026.10.21.26366156](https://doi.org/10.64898/2026.10.21.26366156)；未見期刊版本。
- 全文：[medRxiv PDF v1](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf)。
- 程式與資料：LoRA adapter 權重與訓練、推論程式不公開；編碼後的臨床變項、預測檔、切分定義、設定檔與訓練紀錄可向通訊作者申請；公開資料集部分來自 figshare（DOI 10.6084/m9.figshare.27021604.v1）。[(ref: main p.26)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=26)
- 研究性質：完整的回顧性多中心診斷準確度研究，不是 pilot；核心方法（四種輸入設定的 LoRA 微調）已實作，在訓練前封存的 256 顆結節測試集上評估並附 95% CI。參考標準以細胞學為主，沒有前瞻或跨中心外部驗證。[(ref: main p.5, p.10, p.22–23)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=5)
- 證據邊界：本文數值以 v1 PDF 的正文與 Table 1 為準，頁碼為論文 PDF 的頁次；Table 2–8 的完整欄位、補充資料（Supplementary Table S4–S6 等）與 Figure 2–7 的圖面內容未納入本文引述，相關數字只取正文明列者。

**編輯：** Clare

作者用 1,456 顆甲狀腺結節（兩個突尼西亞中心接受細針抽吸 FNA 的結節，加上公開資料集的影像）微調 MedGemma 1.5 4B，在封存測試集上，只給 B-mode 影像與尺寸的設定 AUROC 為 0.883–0.892、顯著低於 EU-TIRADS，加入放射科醫師報告中的 11 個定性描述詞後升到 0.953，與 EU-TIRADS 的 0.948 達到預設的非劣性；作者自己也指出，EU-TIRADS 正是由同一組描述詞推得。[(ref: main p.3, p.15, p.20)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=3)

## 流程

![研究設計示意圖。最上方標題為 Study design: the same radiologist descriptors feed Config D and the EU-TIRADS comparator。四個圓角方塊：左側藍色方塊「1 Cohort」寫 2 Tunisian centers + public dataset (Hou et al.)、1,456 nodules / 1,280 patients、Reference: cytology (Bethesda II vs V-VI); histology when available、Patient-level split 942 / 258 / 256 (sealed test)；中上紫色方塊「2 Radiologist's structured report」寫 11 qualitative descriptors (composition, echogenicity, margins, ...) 與 EU-TIRADS category (rated once per nodule)；中下綠色方塊「3 MedGemma 1.5 4B + LoRA (r=64)」寫 Input: B-mode image + text fields in prompt，以及 A: image + biometry + age/sex、B: image + biometry、C: A + CoT on 5 sonographic steps、D: A + 11 descriptors (16 fields)、Auxiliary EU-TIRADS target: A, B, D、Output: malignancy probability；右側橘色方塊「4 Sealed test set (256 nodules)」寫 Model probability vs EU-TIRADS、AUROC: DeLong, non-inferiority margin 0.05、Thresholds: native / validation / test-set Youden、EU-TIRADS >=4 (prespecified)、EU-TIRADS >=5 (sensitivity analysis)。三支深灰色實線箭頭分別由藍色方塊指向綠色方塊、由紫色方塊向下指向綠色方塊、由綠色方塊指向橘色方塊；一支灰色虛線弧形箭頭由紫色方塊右緣指向橘色方塊上緣，旁邊的灰色斜體字為 comparator built from the same descriptors。底部斜體說明為 Schematic redrawn from the paper's Methods text; design counts only, no result values.](assets/medgemma-thyroid-eu-tirads-design.png)

圖：本書庫依論文 Methods 與 Table 1 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的病人流程圖為 Figure 1、輸入結構圖為 Figure 2）。三支實線箭頭表示資料與輸入的流向；灰色虛線弧形箭頭表示對照組 EU-TIRADS 與 Config D 取自同一份放射科醫師報告的描述詞。[(ref: main p.6–10, p.20, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=8)

## 背景／問題

作者引用文獻說明，EU-TIRADS 等超音波風險分級系統敏感度高、特異度有限，被抽吸的結節中有 25%–55% 是不必要的切片，五個系統的 diagnostic odds ratio 只在 2.2–4.9 之間；風險分類的讀者間一致性為 moderate，單一描述詞只有 fair。[(ref: main p.3–4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=3) 作者據此把 EU-TIRADS 4 稱為「gray zone」，這一句本身沒有另附引用。[(ref: main p.4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=4)

論文要回答的問題是：一個以醫療影像預訓練、規模只有 4B 的 VLM，經 LoRA 微調後，從 B-mode 影像（可加上臨床與報告欄位）輸出的惡性機率，能否在鑑別力上不輸給專家判讀的 EU-TIRADS，並在 EU-TIRADS ≥ 4 的抽吸門檻下減少良性結節的偽陽性。[(ref: main p.5, p.11)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=5)

## 方法摘要

**資料。** 2019-01-01 至 2025-08-01 間兩個突尼西亞中心（Mahdia、Tunis 的 CERU）接受超音波導引 FNA 的成人結節，加上 Hou 等人公開資料集中挑選的 103 張影像；共 1,456 顆結節（272 顆惡性）、1,280 位病人。[(ref: main p.5–6, p.13)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=5)

**參考標準。** 突尼西亞中心以細胞學為準，Bethesda II 為良性、V／VI 為惡性，有術後組織學時以組織學取代；Bethesda III–IV 只有在有組織學時才納入。公開資料集用其附帶的組織學診斷。[(ref: main p.7)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=7)

**模型與四種輸入。** 基礎模型為 MedGemma 1.5 4B（`google/medgemma-1.5-4b-it`），以 LoRA 微調；表格變項寫成自然語言文字放進 user prompt。Config A 為影像加尺寸（三軸徑、最大徑、體積）與年齡、性別；Config B 只有影像與尺寸；Config C 在 A 之上以五個超音波特徵步驟監督 chain-of-thought；Config D 在 A 之上再加放射科醫師報告的 11 個定性描述詞（共 16 個欄位）。A、B、D 另有 EU-TIRADS 輔助訓練目標，C 沒有。[(ref: main p.8–10, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=8)

**評估。** 病人層級切分為訓練 942、驗證 258、封存測試 256 顆結節；主要比較為模型惡性機率與專家判讀 EU-TIRADS 的 AUROC（DeLong 檢定、非劣性邊界 0.05），EU-TIRADS ≥ 4 為預設的抽吸門檻、≥ 5 為敏感度分析。[(ref: main p.10–13)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=10)

## 方法詳解

**11 個描述詞。** composition、spongiform appearance、echogenicity、shape、margins、microcalcifications、macrocalcifications、perinodular halo、central vascularity、capsular contact、echogenic foci；Doppler 影像不作輸入，central vascularity 只以文字欄位進入。[(ref: main p.8–9)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=8)

**誰給描述詞與 EU-TIRADS。** 突尼西亞中心直接取自每次檢查的例行放射報告，每顆結節只由該中心的放射科醫師判讀一次（Mahdia 至少 20 年經驗、Tunis 30 年經驗），因此沒有讀者間變異的量測；公開資料集影像由兩位 5 年經驗的放射科醫師之一、在不知道病理結果下重新判讀。兩個突尼西亞中心使用 Hitachi Ascendus 與 Fujifilm Arietta、7.5 MHz 以上的線性探頭。[(ref: main p.6–7, p.23)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=6)

**訓練設定。** 輸入解析度 896 × 896；LoRA rank 64、α 64、dropout 0.05，加在所有 linear layer，multimodal projector 全量訓練，可訓練參數約 1.57 億（約 3.5%）；AdamW、learning rate 2 × 10⁻⁴、weight decay 0.01、cosine schedule、effective batch 16、最多 10 epoch 並以驗證集 early stopping；以類別權重與加權抽樣處理惡性比例偏低；Config D 訓練時隨機遮蔽報告欄位。seed 42。[(ref: main p.9–10)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=9)

**切分與封存。** 訓練集包含資料庫前 750 筆（全部來自 Tunis、2019–2022），其餘依結果分層隨機抽樣；測試集在任何訓練前以 SHA-256 checksum 鎖定，不得目視檢查或用於調參。[(ref: main p.10)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=10)

**樣本數與假說。** 以 Buderer 公式（敏感度 0.90、特異度 0.75、盛行率 0.12）估算約 1,158 顆結節，加 20% 餘裕至約 1,390 顆；主要假說是微調模型在封存測試集的 AUROC ≥ 0.89，於評估前固定。[(ref: main p.11)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=11)

**三個操作點。** 模型的 native deployment threshold（盲用於測試集）、只由驗證集推得的 Youden 門檻 0.335、在測試集上重算的 Youden 門檻 0.321（作者明言為樂觀上限）。校準以 ECE 等指標評估，Platt recalibration 在測試集內以 5-fold cross-validation 估計；為了計算 EU-TIRADS 的 Brier 與 net benefit，作者把類別對應到工作機率（2→0.02、3→0.07、4→0.20、5→0.55）。[(ref: main p.12–13)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=12)

- **論文未交代** — 惡性機率如何從模型輸出取得（取哪個 token 的 logit），正文只說使用 softmax 輸出；Config C 的「corrected logit extraction」修正了什麼也沒有說明。
- **論文未交代** — native deployment threshold 的數值與設定方式。
- **論文未交代** — prompt 的完整文字（正文只描述結構並指向 Figure 2），以及 EU-TIRADS 與 confidence 輔助目標的實作與 loss 權重（指向 Supplementary Table S4–S6）。
- **論文未交代** — 突尼西亞中心的描述詞判讀者是否知道細胞學結果；訓練、推論程式與 adapter 權重不公開，測試集 checksum 數值也只能向作者索取。

## 資料與實驗

### 資料

| 項目 | 數量 | 說明 |
|---|---|---|
| 記錄的結節 | 1,580 | 排除 104 顆無組織學的 Bethesda III–IV（Tunis 96、Mahdia 8）與 20 張公開資料集影像 |
| 納入結節／病人 | 1,456／1,280 | 惡性 272 顆（18.7%） |
| 來源 | Tunis 1,233 顆（84.7%）；公開資料集 103 顆；其餘來自 Mahdia | 惡性比例：Tunis 18.8%、公開資料集 19.4%、Mahdia 16.7% |
| 參考標準 | 細胞學 1,342 顆（皆為突尼西亞）；組織學 114 顆（突尼西亞 11、公開 103） | 66 顆突尼西亞 Bethesda V 未經組織學確認 |
| 訓練 | 942 顆（惡性 169）、808 位病人 | 含資料庫前 750 筆（Tunis 2019–2022） |
| 驗證 | 258 顆（惡性 52）、236 位病人 | 用於 early stopping 與門檻 0.335 |
| 封存測試 | 256 顆（惡性 51）、236 位病人 | Tunis 168 顆（65.6%）；EU-TIRADS 2–3 共 112 顆（1 癌）、4 共 87 顆（3 癌）、5 共 57 顆（47 癌） |

Mahdia 的結節數未在正文單列。[(ref: main p.13–14, p.19, p.22)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=13)

### 實驗：封存測試集的鑑別力（論文 Results «Discrimination»、«Formal comparison with EU-TIRADS»）

| 模型／對照 | AUROC (95% CI) | AUPRC | ΔAUROC vs EU-TIRADS | DeLong p（Holm 校正後） |
|---|---|---|---|---|
| Config D（影像＋16 欄位） | 0.953 (0.909–0.976) | 0.834 (0.686–0.914) | +0.004 (−0.016 to +0.025) | 0.66 |
| EU-TIRADS | 0.948 (0.894–0.972) | 0.784 (0.664–0.876) | — | — |
| Config A（影像＋尺寸＋年齡性別） | 0.892 | 0.634 | −0.056 | 0.015（0.045） |
| Config B（影像＋尺寸） | 0.886 | 0.712 | −0.062 | 0.011（0.045） |
| Config C（A＋CoT） | 0.883 | 0.627 | −0.066 | 0.018（0.045） |

Config A–C 的 CI 未在正文列出；Config D 相對 A、B、C 分別高 0.061、0.067、0.070（未校正 p 0.012–0.015），A、B、C 彼此無法區分。差值的標準誤 0.010，80% power 下可偵測的最小差 0.029。驗證集 AUROC：D 0.908、A 0.817、B 0.803、C 0.779。[(ref: main p.14–15)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=14)

### 實驗：操作點（封存測試集 51 癌、205 良性）

| 操作點 | TP | FN | FP | TN | 敏感度 | 特異度 |
|---|---|---|---|---|---|---|
| EU-TIRADS ≥ 4（預設） | 50 | 1† | 94 | 111† | 98.0% (89.7–99.7) | 54.1% (47.3–60.8) |
| EU-TIRADS ≥ 5 | 47 | 4 | 10 | 195 | 92.2% | 95.1% |
| Config D，native threshold | 45 | 6 | 12 | 193 | 88.2% | 94.1% |
| Config D，驗證集門檻 0.335 | 48 | 3 | 22 | 183 | 94.1% | 89.3% |
| Config D，測試集 Youden 0.321 | 49† | 2† | 25† | 180† | 96.1% (86.8–98.9) | 87.8% (82.6–91.6) |

† 正文未直接列出，本書庫由論文報告的比例、分母與重分類數推算（例如 Youden 門檻下 94 個偽陽性有 69 個改判陰性、50 個癌中新漏 1 個）。[(ref: main p.3, p.15–17)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=15)

## 結果

- **描述詞帶來的差距** — 只有影像、尺寸與人口學資料的三種設定 AUROC 0.883–0.892，Holm 校正後都顯著低於 EU-TIRADS；加入 11 個描述詞的 Config D 升到 0.953，達到預設的非劣性（差值 +0.004，CI 下限 −0.016 高於 −0.05）。主要假說 AUROC ≥ 0.89 由 Config D 達成。[(ref: main p.14–15)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=14)
- **對 EU-TIRADS ≥ 4 的重分類** — 在只由驗證集決定的門檻 0.335 下，EU-TIRADS ≥ 4 的 94 個偽陽性中有 72 個被改判陰性，多漏 2 個癌；在測試集 Youden 門檻下為 69 個改判、多漏 1 個，NRI +0.317（95% CI +0.240 to +0.390），沒有任何良性結節被往上調。McNemar 對 ≥ 4：χ² = 64.1，p < 0.001。[(ref: main p.3, p.16–17)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=16)
- **對 EU-TIRADS ≥ 5 沒有優勢** — 與 ≥ 5（敏感度 92.2%、特異度 95.1%）比，Config D 在 native threshold 下正確分類的結節沒有更多（不一致對 1 比 5，exact p = 0.22），在另外兩個門檻下反而較少（3 比 16，p = 0.004；2 比 13，p = 0.007）。[(ref: main p.3, p.17)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=17)
- **EU-TIRADS 4 的實際分母** — 測試集中 EU-TIRADS 4 共 87 顆、只有 3 個癌；在驗證集門檻下，84 個良性中 71 個可延後抽吸，3 個癌中有 2 個也被判為良性；Youden 門檻下為 68 個良性、1 個癌。作者在 Summary Statement 明言這個結論只建立在 3 個 category 4 癌上。[(ref: main p.1, p.19)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=19)
- **校準** — Config D 原始 ECE 0.117、calibration slope 2.51；Platt scaling 後在預設 seed 為 0.019，十個 seed 介於 0.019–0.040（中位數 0.031），AUROC 變化 ≤ 0.006。Config A、B 原始輸出高度壓縮，Brier skill score 為負。[(ref: main p.17–18)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=17)
- **次族群** — Config D 的 AUROC 在女性 0.953、男性 0.935，Tunis 0.949、Mahdia 0.963、公開資料集 0.994；依結節大小則為 < 10 mm 0.647、10–20 mm 0.892、> 20 mm 0.992，微小癌層（n = 24）太小無法下結論。[(ref: main p.18)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=18)

## 限制

**作者自述的限制。** EU-TIRADS 雖未作為輸入，但在 A、B、D 是輔助訓練目標，對 D 的影響無法完全界定；參考標準以細胞學為主，66 顆 Bethesda V 未經組織學確認；排除 104 顆無組織學的 Bethesda III–IV 使樣本偏向判斷明確的病例，若納入，EU-TIRADS 的 ordinal AUROC 會降到 0.912（全當良性）或 0.867（全當惡性）；四種設定用同一個測試集比較，D 相對其他設定的優勢需要獨立世代確認；沒有拆分影像與描述詞各自貢獻的 modality ablation；Tunis 占 84.7%，訓練集包含最早的 750 筆，不構成跨中心外部驗證；公開資料集的影像經過品質挑選，可能讓該子集較容易；每顆結節只判讀一次；只用單張 2D B-mode；預測值依賴抽吸族群 18.7% 的盛行率；CI 在結節層級計算、未考慮同一病人多顆結節；沒有前瞻外部驗證。[(ref: main p.22–23)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=22)

**本書庫的觀察。**

- **追平的是同一份判讀** — 作者在 Discussion 寫明 EU-TIRADS「derived from the same qualitative descriptors that Config D receives」，近乎相等的鑑別力是預期結果；A–C 的結果顯示，不給描述詞時模型從影像學到的部分仍顯著低於專家分級。這篇的證據比較接近「模型能把放射科醫師的結構化判讀換算成連續機率」，而不是「模型能從影像讀出醫師看不到的訊號」。[(ref: main p.19–20)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=19)
- **減少偽陽性的比較基準** — 72／94 的重分類是相對於 EU-TIRADS ≥ 4；把同一份 EU-TIRADS 的門檻提高到 ≥ 5，偽陽性就從 94 降到 10、漏掉的癌從 1 增到 4，而 Config D 在三個門檻下都沒有贏過 ≥ 5。模型的附加價值要放在「4 類內部怎麼再分層」來看，而那一層在測試集只有 3 個癌。
- **樂觀的數字有標示** — 測試集 Youden 門檻與在測試集內做的 Platt recalibration 都用到了測試資料，作者已自行標為上限或限制；引用時以 native threshold 與驗證集門檻的數字為主較穩妥。

## 與書庫其他文章的關係

本篇微調的正是該技術報告介紹的 MedGemma 1.5 4B，技術報告談的是通用能力的擴充，本篇則在單一專科任務上顯示：只給影像時微調後仍輸給專家分級，要加上醫師的結構化描述詞才追平: [MedGemma 1.5：4B 模型如何讀取 3D 影像、全切片與縱向胸片？](2026-09-16-medgemma-1-5.md)

兩篇都把超音波病灶的醫師描述交給語言模型，再與既有的規則式風險系統比較；該研究用 ChatGPT 零樣本讀附件腫塊的文字描述、以手術病理為答案，本篇則微調 VLM 同時看影像與甲狀腺結節的 11 個描述詞、以細胞學為主要答案: [把超音波描述交給 ChatGPT 判良惡性：300 顆附件腫塊，和 IOTA 規則、ADNEX 與專家差多少？](2026-09-22-chatgpt-adnexal-mass-ultrasound-triage.md)

## 實務的啟發

- **可借用的評估設計** — 訓練前以 checksum 封存測試集、把 native、驗證集、測試集三種門檻分開報告，並明列哪些數字用到了測試資料，這種寫法讓讀者能自己區分可部署的估計與樂觀上限。
- **比較對象要包含更嚴的既有門檻** — 宣稱「減少不必要抽吸」時，除了對預設門檻（EU-TIRADS ≥ 4），也要對同一系統較嚴的門檻（≥ 5）做配對比較；本篇的 McNemar 結果說明，只對 ≥ 4 比較會高估模型的附加價值。
- **待驗證的方向** — 模型在 EU-TIRADS 4 內延後抽吸的效果只建立在 3 個癌上，且描述詞來自單次判讀、參考標準以細胞學為主；需要有組織學與讀者間變異的前瞻外部世代，才能判斷它作為 second reader 的價值。
- **證據強度** — 它支持「加入醫師結構化描述詞的微調 VLM，在這個回顧性族群上鑑別力不輸 EU-TIRADS」；不足以支持模型可以取代或獨立於放射科醫師的判讀，作者也把定位限定在 second reader，而非自動判讀。[(ref: main p.3, p.23)](https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf#page=23)

## References

- **main** — Bou Ali MN, Lassoued N, Mahmoud H, Mnif E, Haouet S, Ben Rhouma K, Elsakly MK, Hasnaoui M. *Fine-tuned Medical Vision-Language Model (MedGemma 1.5 4B) with and without Structured Radiologist Descriptors versus EU-TIRADS for Malignancy Risk Stratification of Thyroid Nodules at Ultrasound: A Tunisian Multicenter Diagnostic Accuracy Study*. medRxiv v1 (2026). DOI: <https://doi.org/10.64898/2026.10.21.26366156>。全文 PDF：<https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1.full.pdf>。文內引用位置：p.1（Summary Statement）、p.3（Abstract）、p.3–4（Introduction）、p.5–13（Materials and Methods）、p.13–19（Results）、p.19–23（Discussion、Limitations）、p.26（Declarations）、Table 1。
- **abs** — medRxiv abstract page：<https://www.medrxiv.org/content/10.64898/2026.10.21.26366156v1>。

[Home](../) · [AI Papers](./)
