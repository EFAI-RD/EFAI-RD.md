---
parent: AI Papers
nav_order: 4
title: "DbC：先認徵象再組肝病診斷，未見疾病定位六勝、AP 三輸"
catalog_id: "arxiv:2611.05231"
editors:
  - "Clare"
refs:
  main:
    title: "Diagnosis by Composition: Detecting and Localizing Unseen Diseases by Composing Learned Radiological Findings"
    url: "https://arxiv.org/abs/2611.05231v1"
  code:
    title: "DiagnosisByComposition (anonymized repository)"
    url: "https://anonymous.4open.science/r/DiagnosisByComposition/"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# DbC：先認徵象再組肝病診斷，未見疾病定位六勝、AP 三輸

## 來源

- 團隊：University of California, Berkeley、Alibaba Group、Fudan University、Zhejiang University、Imperial College London、University of California, San Francisco 與 Zhejiang Lab，13 位作者，第一作者 Kaihua Hou（UC Berkeley），最後作者 Ke Yan（Alibaba Group）。[(ref: main title block)](https://arxiv.org/html/2611.05231v1)
- 論文：*Diagnosis by Composition: Detecting and Localizing Unseen Diseases by Composing Learned Radiological Findings*，arXiv:2611.05231v1（cs.CV），2026-11-03 提交，目前只有 v1；授權為 arXiv 非專屬散布授權，arXiv 頁未註記投稿會議。[(ref: abstract)](https://arxiv.org/abs/2611.05231v1)
- 識別碼：arXiv [2611.05231](https://arxiv.org/abs/2611.05231v1)；DOI [10.48550/arXiv.2611.05231](https://doi.org/10.48550/arXiv.2611.05231)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.05231v1)、[PDF v1](https://arxiv.org/pdf/2611.05231v1)。
- 程式與資料：作者寫明程式碼放在匿名程式庫 [anonymous.4open.science/r/DiagnosisByComposition](https://anonymous.4open.science/r/DiagnosisByComposition/)；訓練與內部測試資料為不公開的院內資料，外部驗證用的 MCT-LTDiag 為 CC0 公開資料。[(ref: main Reproducibility statement)](https://arxiv.org/html/2611.05231v1#Sx3)
- 研究性質：方法論文，DbC 已實作，在單一醫院 15,609 次多期相肝臟 CT 上訓練，並在內部測試、留一疾病的零樣本設定、另一家醫院的兩種罕見病與一個公開外部資料集上評估；不是 pilot。所有指標附 CT 層級 bootstrap 95% 信賴區間，資料量實驗另跑 3 個 seed；主表為單一 seed 的訓練結果。[(ref: main §4.1)](https://arxiv.org/html/2611.05231v1#S4.SS1) [(ref: main Appendix F)](https://arxiv.org/html/2611.05231v1#A6)
- 證據邊界：本文數值以 arXiv v1 的正文 Table 1–4 與附錄 A–H（Table 5–10）為準；附錄 I 的質性案例只引用圖說的文字描述，Figure 3 的曲線改以附錄 Table 10 的數值引述。

**編輯：** Clare

作者讓模型先學會在肝臟 CT 上逐 token 畫出 40 種放射徵象的機率圖，再依放射指引把「某疾病必備的徵象」以不帶參數的 soft minimum 組合成診斷圖；在留一疾病的零樣本設定下，六種沒訓練過的肝病在 Dice、IoU 與 AP50 三項定位指標上都顯著優於所有比較方法，但病例層級的 AP 有三種疾病輸給比較方法。[(ref: main Abstract)](https://arxiv.org/html/2611.05231v1) [(ref: main Table 2)](https://arxiv.org/html/2611.05231v1#S4.T2)

## 流程

![DbC 流程示意圖，分上下兩排。上排標題為 (a) Training: learn 40 finding maps (loss on findings only)，四個方塊由左到右：兩個淺藍色方塊「Image input」（Multi-phase liver CT (NC, A, PV, D)；4 channels; missing phase = all-zero；15,609 CTs, single institution；Split 12,487 / 1,559 / 1,563；SwinUNETR-V2 encoder；-> token embedding v_n；(96 x 72 x 16 token grid)）與「Text input」（40 finding names (12 categories)；Fixed prompt, frozen；BiomedCLIP text encoder -> t_m；Learned adapter phi(t_m)；a_mn = sigmoid(s_m * cos(v_n, phi(t_m)) + b_m)），接著兩個淺橘色方塊「Finding labels per lesion」（Required findings of its disease (from guidelines, by team radiologists)；Supportive findings from the report (extracted by Qwen3-Max)；One size finding (from mask)；Rasterized to the token grid；Out-of-liver tokens = hard negatives）以實線箭頭指向「Training objective」（Dice-focal loss on the 40 finding maps together；No disease head in DbC；Checkpoint: validation macro token AP）。下排標題為 (b) Inference and evaluation: compose required finding maps into a diagnosis map，三個方塊：淺綠色「Diagnostic composition」（Soft minimum over required findings (beta = 10, no learned parameters)；Example HCC: low density on NC AND non-rim arterial hyperenhancement AND non-peripheral washout AND enhancing capsule；7 diagnoses, 2-5 required findings each；Rare diseases: compositions declared at evaluation time）以實線箭頭指向淺綠色「Outputs」（Diagnosis map per disease；Detection score = max of the map (AUROC, AP, Sens. @ 95% Spec.)；Predicted lesions = connected components of thresholded map (Dice, IoU, Coverage, AP50)；95% CI: CT-level bootstrap, 2,000 replicates, paired），右側為灰色「Evaluation settings」（Fully supervised: 1,563 internal test CTs；Unseen diseases: leave-one-disease-out, 6 diseases, one model per held-out disease；Rare diseases, other institution: abscess 176, hepatoblastoma 43, controls 119；External MCT-LTDiag: 482 CTs, 4 diseases；Data scaling: 10-100% of train, seeds 42-44；Comparators: SegVol, SAT, VoxTell (fine-tuned), Disease-VL, Disease-V (matched ablations)）](assets/dbc-findings-composition-pipeline.png)

圖：本書庫依論文 §3.1–§3.4、§4.1 與 Appendix A–F 的文字重繪的流程示意圖，只含設計層級的設定與資料量，不含結果數值，未複製論文原圖（論文 Figure 2 為模型架構圖，Figure 5 為報告抽取徵象的示意圖）。[(ref: main Figure 2)](https://arxiv.org/html/2611.05231v1#S3.F2) [(ref: main Figure 5)](https://arxiv.org/html/2611.05231v1#A3.F5)

## 背景／問題

作者把現有的放射診斷模型分成「disease-first」：模型直接從影像預測疾病標籤，或在圖文對齊模型裡把影像對齊疾病名稱；這樣的模型只能處理訓練過的疾病，決策也無法用放射科醫師的語言解釋。作者對照的是放射科實務中的「findings-first」：先辨認影像上看得到的徵象（密度、邊緣、各期相的顯影型態），再依已發表的指引把徵象組合讀成疾病，並引用 LI-RADS 等指引與住院醫師訓練規範說明這個順序。[(ref: main §1)](https://arxiv.org/html/2611.05231v1#S1)

作者另以自家資料說明為什麼不能只靠報告學徵象：在他們的資料中，每個病灶在報告的 findings 段平均只對應約 1.2 個放射徵象，作為學習徵象詞彙的訊號太稀疏。[(ref: main §3.3)](https://arxiv.org/html/2611.05231v1#S3.SS3)

「findings-first 學到的表徵比 disease-first 更能泛化」是作者想檢驗的假說，不是前提；作者在討論段也明寫，把結果讀成表徵學習上的結論是「hypothesized interpretation」。檢驗它的是留一疾病實驗與兩個 matched ablation（Disease-VL、Disease-V），兩者與 DbC 共用編碼器、輸入、損失與最佳化設定，只差在直接預測疾病。[(ref: main §4.1)](https://arxiv.org/html/2611.05231v1#S4.SS1) [(ref: main §5)](https://arxiv.org/html/2611.05231v1#S5)

## 方法摘要

**唯一的學習任務是徵象圖。** 模型對每個徵象 f_m 在每個空間 token 上輸出一個 0–1 的機率，總共 40 張 finding map；這是 DbC 唯一需要訓練的任務，沒有疾病輸出頭。[(ref: main §3.1)](https://arxiv.org/html/2611.05231v1#S3.SS1)

**徵象怎麼對齊文字。** 四通道的 SwinUNETR 編碼器一次讀入可用的對比期相，把影像轉成逐 token 的特徵 v_n；每個徵象的名稱放進固定 prompt，以凍結的 BiomedCLIP 文字編碼器編碼，再經一個小 adapter 映到同一空間，兩者的 cosine similarity 乘上每個徵象自己的 scale、加上 bias 後過 sigmoid，就是該徵象在該 token 的機率。作者把這描述成 CLIP 式的類別辨識，只是改成逐 token、用密集標籤而非圖文配對訓練。[(ref: main §3.4)](https://arxiv.org/html/2611.05231v1#S3.SS4)

**疾病是徵象的組合，而且是寫死的。** 每種疾病由一組 required findings 定義（例如 HCC 需要 low density on NC、non-rim arterial hyperenhancement、non-peripheral washout 與 enhancing capsule），推論時把這幾張徵象圖以 soft minimum 逐 token 合併成診斷圖，行為類似邏輯 AND；這個運算沒有可學參數（β 設為 10）。診斷圖的最大值當作病例層級的偵測分數，門檻化後的連通區域當作預測病灶。[(ref: main §3.1)](https://arxiv.org/html/2611.05231v1#S3.SS1) [(ref: main Table 6)](https://arxiv.org/html/2611.05231v1#A2.T6)

**未見疾病怎麼做。** 零樣本診斷與一般推論是同一個計算：只要寫下新疾病的 required findings，就能組出它的診斷圖，不需要新輸出或重新訓練。比較方法則以疾病名稱當提示。[(ref: main §3.1)](https://arxiv.org/html/2611.05231v1#S3.SS1) [(ref: main §4.3)](https://arxiv.org/html/2611.05231v1#S4.SS3)

## 方法詳解

**徵象詞彙與組合規則。** 團隊中專攻肝臟影像的放射科醫師依 LI-RADS、EASL、AASLD、EASL-ILCA、ACG 等指引與影像文獻，定出 12 類共 40 個徵象（Table 5），以及 7 個診斷（HCC、ICC、metastasis、hemangioma、FNH、cyst、calcification）的組合，每個組合 2–5 個 required findings；兩種罕見病（abscess、hepatoblastoma）的組合在評估時才宣告。徵象清單是為內部資料的六種常見肝病設計的。[(ref: main §3.2)](https://arxiv.org/html/2611.05231v1#S3.SS2) [(ref: main Appendix B)](https://arxiv.org/html/2611.05231v1#A2) [(ref: main Table 5)](https://arxiv.org/html/2611.05231v1#A2.T5)

**每個病灶的徵象標籤有三個來源。** 一是該疾病的 required findings，不論報告是否提到都給；二是 Qwen3-Max 從報告的 findings 與 impression 段抽出的 supportive findings，即報告記載、但不在該疾病必備清單內的徵象，以固定 schema 輸出 JSON 與對應的報告原句；三是依遮罩尺寸給的一個大小徵象。三種標籤都用來訓練徵象圖，但推論時的組合只用 required findings。若報告沒有提到該病灶的疾病，就只保留 required 與大小徵象。一位團隊放射科醫師隨機審閱 200 筆抽取結果，作者報告全部忠於原報告。[(ref: main §3.3)](https://arxiv.org/html/2611.05231v1#S3.SS3) [(ref: main Appendix C)](https://arxiv.org/html/2611.05231v1#A3)

**標籤怎麼落到 token。** 每個 token（4×4×4 voxels，約 3×3×20 mm）指派給佔多數體素的病灶，該病灶的所有徵象在此設為陽性；與特定期相綁定的徵象只在該期相有取得的 CT 上監督；肝臟外的 token 全部當作 hard negatives。[(ref: main Appendix A)](https://arxiv.org/html/2611.05231v1#A1) [(ref: main Appendix C)](https://arxiv.org/html/2611.05231v1#A3)

**訓練設定。** 40 張徵象圖以單一 Dice-focal loss 一起訓練。AdamW、峰值學習率 5.7×10⁻⁵、weight decay 0.1、有效 batch 32 個 CT、最多 80 epochs、patience 8 的 early stopping，以驗證集 macro token AP 選 checkpoint，不做資料增強；硬體為 2 張 H200。DbC、Disease-VL、Disease-V 共用這套設定，作者稱兩者分別搜尋超參數後最佳值相同。[(ref: main Appendix D)](https://arxiv.org/html/2611.05231v1#A4) [(ref: main Table 7)](https://arxiv.org/html/2611.05231v1#A4.T7)

**比較對象。** Disease-VL 用同一模型但把文字換成疾病名稱，Disease-V 拿掉文字端、直接預測疾病（只在監督式比較出現）；SegVol、SAT、VoxTell 三個以文字提示回傳區域的已發表模型，各自從公開 checkpoint 以作者公布的訓練配方、seed 42 在本資料上微調，步數與 DbC 相同，並以臨床疾病名稱當提示；它們的單通道輸入層複製權重擴成四期相，並使用各自的 HU 視窗 [−500, 1000]（DbC 為 [−75, 250]）。[(ref: main §4.1)](https://arxiv.org/html/2611.05231v1#S4.SS1) [(ref: main Appendix E)](https://arxiv.org/html/2611.05231v1#A5) [(ref: main Appendix A)](https://arxiv.org/html/2611.05231v1#A1)

**留一疾病怎麼做。** 對每個要測的疾病 k，把所有含 k 的 CT 從訓練與驗證集移除，用剩下的資料重新訓練一個模型；比較方法也移除 k 的輸出通道，仍可在測試時以名稱提示。測試時，k 的陽性為被移除的 CT 加上原本測試集中的 k，陰性為固定測試集中不含 k 的 CT。[(ref: main Appendix D)](https://arxiv.org/html/2611.05231v1#A4)

**指標與顯著性。** 偵測以病例為單位計算 AUROC、AP 與 95% 特異度下的敏感度；定位以病灶為單位，取與真值 IoU 最大的預測連通區域計算 Dice、IoU 與 coverage，並以 IoU ≥ 0.5 計算 AP50；macro 值為各疾病的不加權平均。95% CI 來自 2,000 次 CT 層級 bootstrap，各模型共用同一組重抽樣，「顯著」定義為配對差的區間高於零。[(ref: main §4.1)](https://arxiv.org/html/2611.05231v1#S4.SS1) [(ref: main Appendix F)](https://arxiv.org/html/2611.05231v1#A6)

- **論文未交代** — Qwen3-Max 抽取 supportive findings 的完整 prompt 只以 Figure 5 的結構說明，沒有附全文；徵象名稱送進 BiomedCLIP 的「fixed prompt」原文也沒有寫出。[(ref: main Figure 5)](https://arxiv.org/html/2611.05231v1#A3.F5) [(ref: main §3.4)](https://arxiv.org/html/2611.05231v1#S3.SS4)
- **論文未交代** — 計算 Dice、IoU、coverage 時把診斷圖門檻化所用的門檻值（AP50 另寫明以 0.005 形成連通區域）。[(ref: main Appendix F)](https://arxiv.org/html/2611.05231v1#A6)
- **論文未交代** — 超參數搜尋的範圍與次數，以及報告抽取的召回率：200 筆審閱只檢查抽出的徵象是否忠於報告，沒有檢查是否漏抽。[(ref: main Appendix D)](https://arxiv.org/html/2611.05231v1#A4) [(ref: main Appendix C)](https://arxiv.org/html/2611.05231v1#A3)

## 資料與實驗

**資料。** 下表整理自論文 §4.1 與 Appendix A、G。[(ref: main §4.1)](https://arxiv.org/html/2611.05231v1#S4.SS1) [(ref: main Appendix A)](https://arxiv.org/html/2611.05231v1#A1) [(ref: main Appendix G)](https://arxiv.org/html/2611.05231v1#A7)

| Dataset | 用途 | 規模 | 切分／說明 |
|---|---|---|---|
| 內部多期相肝臟 CT | 訓練、驗證、內部測試、留一疾病 | 15,609 次 CT，附病灶遮罩與放射報告，單一醫院 | 病人層級 80/10/10（seed 42）：12,487／1,559／1,563；測試集中 533 次含病灶、共 2,571 個病灶；六種疾病 HCC、ICC、metastasis、hemangioma、FNH、cyst，另有 calcification |
| 罕見病隊列 | 零樣本外部測試 | abscess 176 次、hepatoblastoma 43 次、無肝臟病灶對照 119 次 | 來自另一家醫院；兩種疾病都不在內部資料中，以完整訓練的 checkpoint 評估 |
| MCT-LTDiag | 外部測試（僅測試） | 482 次 CT、2,169 個病灶：HCC 91／191、ICC 81／286、metastasis 216／1,240、hemangioma 94／452 | CC0 公開資料；四期相，病灶皆 ≥ 1 cm；分別以完整訓練與留一疾病的 checkpoint 評估 |

**監督式比較（內部測試集）。** 下表重製論文 Table 1，各值為七個診斷的 macro 平均，括號為 95% CI；* 表示對所有比較方法顯著較佳，† 為 matched ablation。[(ref: main Table 1)](https://arxiv.org/html/2611.05231v1#S4.T1)

| Model | Dice | IoU | Coverage | AP50 | AUROC | AP | Sens.@95% Spec. |
|---|---|---|---|---|---|---|---|
| SegVol | .055 [.039,.076] | .037 [.026,.053] | .088 [.062,.124] | .000 [.000,.000] | .806 [.759,.848] | .284 [.213,.377] | .354 [.304,.408] |
| SAT | .190 [.156,.228] | .152 [.124,.184] | .185 [.150,.225] | .000 [.000,.001] | .900 [.888,.912] | .528 [.484,.582] | .592 [.553,.630] |
| VoxTell | .096 [.075,.124] | .069 [.054,.091] | .200 [.174,.230] | .000 [.000,.000] | .810 [.794,.825] | .230 [.215,.258] | .260 [.205,.303] |
| Disease-V† | .288 [.255,.326] | .233 [.205,.266] | .287 [.254,.326] | .153 [.117,.212] | .915 [.903,.928] | .628 [.578,.678] | .678 [.633,.714] |
| Disease-VL† | .271 [.235,.311] | .220 [.189,.255] | .274 [.236,.318] | .137 [.116,.190] | .916 [.904,.927] | .582 [.538,.642] | .646 [.599,.700] |
| **DbC** | .313 [.281,.349] | .253 [.226,.284] | .314 [.282,.351] | .163 [.128,.213] | .931* [.920,.941] | .663 [.615,.708] | .699 [.659,.739] |

**零樣本：留一疾病（內部測試）。** 下表摘錄論文 Table 2 除 IoU 以外的五個欄位，CI 從略，每個疾病各自用一個從未見過該疾病的模型評估；* 表示對所有比較方法顯著較佳，各疾病最佳值以粗體標示。[(ref: main Table 2)](https://arxiv.org/html/2611.05231v1#S4.T2)

| Unseen disease | Model | Dice | AP50 | AUROC | AP | Sens.@95% Spec. |
|---|---|---|---|---|---|---|
| HCC | SegVol | .035 | .000 | .757 | .560 | .197 |
| HCC | SAT | .215 | .000 | .809 | .607 | **.212** |
| HCC | VoxTell | .206 | .000 | .811 | .528 | .018 |
| HCC | Disease-VL† | .249 | .089 | .691 | **.624** | .092 |
| HCC | DbC | **.376*** | **.158*** | **.834*** | .577 | .074 |
| ICC | SegVol | .065 | .000 | .835 | .447 | .106 |
| ICC | SAT | .206 | .000 | .804 | .420 | .089 |
| ICC | VoxTell | .292 | .000 | .870 | .501 | .113 |
| ICC | Disease-VL† | .347 | .080 | .828 | .711 | .105 |
| ICC | DbC | **.394*** | **.154*** | **.932*** | **.767*** | **.578*** |
| Metastasis | SegVol | .021 | .000 | .731 | .461 | .131 |
| Metastasis | SAT | .147 | .009 | .828 | .586 | .208 |
| Metastasis | VoxTell | .013 | .000 | .724 | .405 | .040 |
| Metastasis | Disease-VL† | .098 | .034 | .765 | .617 | .096 |
| Metastasis | DbC | **.165*** | **.063*** | **.846*** | **.624** | **.290*** |
| Hemangioma | SegVol | .051 | .000 | .764 | .705 | .101 |
| Hemangioma | SAT | .241 | .000 | .714 | .724 | **.302** |
| Hemangioma | VoxTell | .094 | .000 | .807 | .783 | .249 |
| Hemangioma | Disease-VL† | .133 | .052 | .776 | **.822** | .166 |
| Hemangioma | DbC | **.332*** | **.169*** | **.839*** | .801 | .240 |
| FNH | SegVol | .048 | .000 | .796 | .135 | .088 |
| FNH | SAT | .150 | .000 | .511 | .061 | .044 |
| FNH | VoxTell | .145 | .000 | .713 | .089 | .011 |
| FNH | Disease-VL† | .035 | .000 | .532 | .121 | .000 |
| FNH | DbC | **.265*** | **.067*** | **.801** | **.165** | **.198*** |
| Cyst | SegVol | .001 | .000 | .734 | .735 | .156 |
| Cyst | SAT | .032 | .000 | .803 | .807 | .246 |
| Cyst | VoxTell | .001 | .000 | .775 | .750 | .139 |
| Cyst | Disease-VL† | .015 | .000 | .689 | **.808** | .099 |
| Cyst | DbC | **.059*** | **.006*** | **.809** | .798 | **.257** |

**另一家醫院的罕見病與外部資料。** 下表重製論文 Table 3 與 Table 4；罕見病以無肝臟病灶的 CT 為陰性，MCT-LTDiag 的陰性為其他三種疾病的 CT。[(ref: main Table 3)](https://arxiv.org/html/2611.05231v1#S4.T3) [(ref: main Table 4)](https://arxiv.org/html/2611.05231v1#S4.T4) [(ref: main Appendix F)](https://arxiv.org/html/2611.05231v1#A6)

| Setting | Model | Dice | IoU | AUROC | AP |
|---|---|---|---|---|---|
| Abscess | SegVol | .051 | .027 | .815 | .751 |
| Abscess | SAT | .174 | .097 | .789 | .782 |
| Abscess | VoxTell | .094 | .066 | .781 | .799 |
| Abscess | Disease-VL† | .170 | .113 | .830 | .840 |
| Abscess | DbC | .238* | .163* | .890* | .865* |
| Hepatoblastoma | SegVol | .106 | .070 | .634 | .290 |
| Hepatoblastoma | SAT | .142 | .092 | .467 | .222 |
| Hepatoblastoma | VoxTell | .118 | .071 | .662 | .306 |
| Hepatoblastoma | Disease-VL† | .053 | .032 | .558 | .254 |
| Hepatoblastoma | DbC | .285* | .185* | .829* | .456* [.207,.595] |
| MCT-LTDiag zero-shot | SegVol | .044 | .026 | .489 | .245 |
| MCT-LTDiag zero-shot | SAT | .094 | .065 | .528 | .281 |
| MCT-LTDiag zero-shot | VoxTell | .064 | .042 | .466 | .238 |
| MCT-LTDiag zero-shot | Disease-VL† | .103 | .073 | .593 | .278 |
| MCT-LTDiag zero-shot | DbC | .173* | .134* | .639* | .326 |
| MCT-LTDiag full training | SegVol | .133 | .098 | .614 | .381 |
| MCT-LTDiag full training | SAT | .088 | .061 | .596 | .350 |
| MCT-LTDiag full training | VoxTell | .134 | .094 | .601 | .370 |
| MCT-LTDiag full training | Disease-VL† | .183 | .142 | .716 | .516 |
| MCT-LTDiag full training | DbC | .286* | .247* | .743* | .571* |

**資料量。** DbC 與 Disease-VL 在 10%–100% 的巢狀訓練子集上各以 seed 42、43、44 訓練三次。下表摘錄 Table 10 七個診斷的 detection AUROC 與 localization Dice（三個 seed 的平均，括號為 SD）；✓ 表示配對差的 95% CI 不含零，ns 為不顯著。[(ref: main §4.5)](https://arxiv.org/html/2611.05231v1#S4.SS5) [(ref: main Table 10)](https://arxiv.org/html/2611.05231v1#A8.T10)

| Training fraction | 10% | 20% | 40% | 60% | 80% | 100% |
|---|---|---|---|---|---|---|
| AUROC DbC | .725 (.009) | .768 (.011) | .836 (.016) | .864 (.022) | .898 (.005) | .918 (.011) |
| AUROC Disease-VL† | .700 (.006) | .758 (.007) | .822 (.004) | .855 (.013) | .882 (.008) | .903 (.014) |
| AUROC Sig. | ✓ | ns | ✓ | ✓ | ✓ | ✓ |
| Dice DbC | .070 (.010) | .103 (.011) | .164 (.019) | .219 (.014) | .275 (.019) | .312 (.006) |
| Dice Disease-VL† | .054 (.001) | .094 (.014) | .149 (.010) | .208 (.009) | .248 (.021) | .282 (.010) |
| Dice Sig. | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 結果

- **監督式：每欄最高，但只有 AUROC 顯著** — 七個診斷都有訓練時，DbC 在 Table 1 所有欄位都是最高；對所有比較方法都顯著的只有 AUROC（.931 對次佳 Disease-VL .916）。作者據 matched ablation 認為增益來自「組合徵象」而不是編碼器或架構。[(ref: main Table 1)](https://arxiv.org/html/2611.05231v1#S4.T1) [(ref: main §4.2)](https://arxiv.org/html/2611.05231v1#S4.SS2)
- **零樣本定位：六種疾病全部顯著領先** — 留一疾病時，DbC 在六種疾病的 Dice、IoU、AP50 都顯著優於所有比較方法，例如 HCC 的 Dice .376 對次佳 Disease-VL .249；作者特別指出 Disease-VL 偵測 FNH 的 AUROC 只有 .532，接近隨機。[(ref: main Table 2)](https://arxiv.org/html/2611.05231v1#S4.T2) [(ref: main §4.3)](https://arxiv.org/html/2611.05231v1#S4.SS3)
- **零樣本偵測：AUROC 全勝，其他偵測指標互有勝負** — DbC 的 AUROC 六種疾病都最高，其中四種顯著（FNH、cyst 不顯著）；但 AP 在 HCC、hemangioma、cyst 輸給 Disease-VL 或 SAT，95% 特異度下的敏感度在 HCC（.074 對 SAT .212）與 hemangioma（.240 對 SAT .302）也較低。作者在正文以 AUROC 概括「偵測較佳」，沒有討論這幾個欄位。[(ref: main Table 2)](https://arxiv.org/html/2611.05231v1#S4.T2)
- **另一家醫院的罕見病** — abscess 與 hepatoblastoma 都不在內部資料與徵象清單的設計範圍內，DbC 以評估時才宣告的組合在兩者的四個指標上都顯著領先；hepatoblastoma 的 AUROC .829，比較方法介於 .467–.662。hepatoblastoma 只有 43 例，AP 的 CI 為 [.207, .595]。[(ref: main Table 3)](https://arxiv.org/html/2611.05231v1#S4.T3) [(ref: main Appendix G)](https://arxiv.org/html/2611.05231v1#A7)
- **公開外部資料** — 在 MCT-LTDiag 上，DbC 兩種設定的 Dice、IoU、AUROC 都顯著領先，完整訓練時 AP 也顯著；零樣本設定的 AUROC .639，比較方法 .466–.593，其中三個已發表模型接近或低於 .5。附錄逐疾病結果中，零樣本 HCC 的 AUROC DbC 為 .581、低於 Disease-VL 的 .615，ICC 的 Dice 也低於 Disease-VL（.141 對 .163）。[(ref: main Table 4)](https://arxiv.org/html/2611.05231v1#S4.T4) [(ref: main Table 8)](https://arxiv.org/html/2611.05231v1#A8.T8)
- **資料量** — DbC 在每個訓練比例的 Dice 都顯著高於 Disease-VL；AUROC 在 20% 時不顯著，其餘比例顯著。作者稱相對增益在最小比例時最大。[(ref: main Table 10)](https://arxiv.org/html/2611.05231v1#A8.T10) [(ref: main §4.5)](https://arxiv.org/html/2611.05231v1#S4.SS5)
- **質性案例** — 附錄 Figure 6 在六個測試 CT 上展示：共用的徵象（如 low density）在兩種共存病灶上都被點亮，目標疾病特有的徵象只出現在目標病灶上，組合後的診斷圖因此排除了共存的另一種病灶。這是挑選的範例。[(ref: main Figure 6)](https://arxiv.org/html/2611.05231v1#A9.F6)

## 限制

作者列出兩點：結果只在單一醫院、7 個診斷的肝臟 3D CT 上展示；組合規則由專家從指引推出、且要求全部徵象同時成立，因此每個病灶的徵象標籤只會和「指引典型表現＋報告記載」一樣完整，非典型表現需要更豐富的組合規則。倫理聲明也寫明模型是研究原型，未經前瞻驗證與法規審查不應用於臨床。[(ref: main §5)](https://arxiv.org/html/2611.05231v1#S5) [(ref: main Ethics statement)](https://arxiv.org/html/2611.05231v1#Sx2)

本書庫另外注意到：

- **「零樣本」仍需要專家先寫下組合** — 未見疾病不需要訓練資料，但需要放射科醫師先定出它的 required findings；罕見病的組合由同一團隊在評估時宣告，作者稱沒有參考模型輸出，但這無法從論文外部驗證。比較方法只拿到疾病名稱，兩邊得到的先驗知識並不對等。[(ref: main §4.4)](https://arxiv.org/html/2611.05231v1#S4.SS4) [(ref: main Appendix E)](https://arxiv.org/html/2611.05231v1#A5)
- **標籤與組合來自同一份規則** — 訓練時每個病灶的 required findings 直接由疾病標籤展開，推論時再用同一組 required findings 組合；DbC 學到的「徵象」有多少是真的影像徵象、多少是疾病區域的代稱，論文只用質性圖與留一疾病實驗間接回答，沒有逐徵象的定位評估。[(ref: main §3.3)](https://arxiv.org/html/2611.05231v1#S3.SS3) [(ref: main Appendix C)](https://arxiv.org/html/2611.05231v1#A3)
- **已發表基線沒有調參** — SegVol、SAT、VoxTell 依各自公布的配方、單一 seed、與 DbC 相同步數微調，輸入層由單通道擴成四期相；DbC 與 Disease-VL 則做過超參數搜尋。三個已發表模型的 AP50 在多數設定為 .000，論文沒有分析原因。[(ref: main Appendix D)](https://arxiv.org/html/2611.05231v1#A4) [(ref: main Appendix E)](https://arxiv.org/html/2611.05231v1#A5) [(ref: main Table 1)](https://arxiv.org/html/2611.05231v1#S4.T1)
- **絕對定位品質仍低** — 即使在監督式設定，DbC 的 macro Dice 為 .313、AP50 為 .163；零樣本 cyst 的 Dice 只有 .059。「顯著領先」是相對比較，不代表病灶邊界已可用。[(ref: main Table 1)](https://arxiv.org/html/2611.05231v1#S4.T1) [(ref: main Table 2)](https://arxiv.org/html/2611.05231v1#S4.T2)
- **主表是單一 seed** — Table 1–4 的 CI 來自測試集重抽樣，反映的是測試樣本的不確定性，不含訓練變異；只有資料量實驗跑了三個 seed，100% 比例下 DbC 的 Dice 平均 .312（SD .006）。[(ref: main Appendix F)](https://arxiv.org/html/2611.05231v1#A6) [(ref: main Table 10)](https://arxiv.org/html/2611.05231v1#A8.T10)
- **圖說與表格不一致** — Figure 1(b) 說 DbC 以「四張」徵象圖組出 ICC，但 Table 6 的 ICC 組合有五個 required findings；論文沒有說明差異。[(ref: main Figure 1)](https://arxiv.org/html/2611.05231v1#S1.F1) [(ref: main Table 6)](https://arxiv.org/html/2611.05231v1#A2.T6)

## 與書庫其他文章的關係

兩篇都把放射指引寫成可執行的明確規則、讓模型只負責判斷個別條件：GDGraph 由 LLM 把指引編成決策圖、在文字病例上逐節點問答，DbC 則由放射科醫師把指引寫成徵象組合、由影像模型逐 token 畫出各徵象再以 soft minimum 組成診斷圖: [放射指引編成決策圖再逐節點作答：Jev 從 57.3% 到 90.8%](2026-11-02-gdgraph-radiology-guideline-decision-graph.md)

兩篇都在 3D CT 上用 LLM 整理報告、再把影像特徵與文字編碼對齊：MedHiVE 以 Qwen3-30B 把報告拆成器官片段、只在預訓練做整卷與器官層級的對比學習，DbC 則以 Qwen3-Max 從報告抽出病灶的徵象、配合病灶遮罩逐 token 監督 40 個徵象，並以留一疾病檢驗零樣本診斷: [MedHiVE：報告只進預訓練，有對齊的器官多 2.7、其餘只多 0.7](2026-11-11-medhive-hierarchical-moe-3d-ct-vlm.md)

本篇把 SegVol、SAT 與 VoxTell 這幾個文字提示分割模型當成基線，在肝臟 CT 上微調後比較；該綜述則從放療角度整理同一批模型，指出它們理解臨床概念（如外擴邊界）的限制，兩篇並讀可看到同一批模型在診斷與放療兩種用途上的評估: [放療勾畫綜述：VLM 對 nnU-Net 勝負未定，論點改押 CTV](2026-11-12-radiotherapy-segmentation-review-atlas-to-agentic-vlm.md)

## 實務的啟發

- **可借用的評估設計：留一疾病＋matched ablation** — 若團隊主張某種表徵「能泛化到沒見過的疾病」，DbC 的做法值得照抄：每次移除一個疾病的所有 CT 重新訓練，並放一個只差在監督目標的對照組（Disease-VL），再用配對 bootstrap 比較。這比只在已知類別上比分數更能檢驗泛化的主張。[(ref: main §4.1)](https://arxiv.org/html/2611.05231v1#S4.SS1) [(ref: main Appendix D)](https://arxiv.org/html/2611.05231v1#A4)
- **報告只當補充、指引當主幹** — 作者觀察到報告每個病灶平均只記約 1.2 個徵象，因此用指引展開的 required findings 補足密度，LLM 抽取的報告徵象只當多樣性的補充；手上只有報告的團隊，可以先量一下自己報告的徵象密度，再決定能否只靠報告監督。[(ref: main §3.3)](https://arxiv.org/html/2611.05231v1#S3.SS3)
- **待驗證：組合式診斷在偵測上的取捨** — 留一疾病的 AUROC 全勝，但 AP 與高特異度下的敏感度在部分疾病輸給比較方法；若用途是篩檢（在高特異度下抓出病例），不能只看 AUROC 與定位指標，要在自己的資料上看這兩個欄位。[(ref: main Table 2)](https://arxiv.org/html/2611.05231v1#S4.T2)
- **可審計是設計性質，不是已驗證的臨床效益** — 診斷圖可以逐徵象檢查，但論文沒有讀者研究，也沒有檢驗放射科醫師是否因此更快發現錯誤；目前只能把它當成一種可解釋的結構，而非已證實可提升判讀。[(ref: main §5)](https://arxiv.org/html/2611.05231v1#S5)

## References

- **main** — Hou K, Liu W, Huang Y, Zhang H, Jin H, Sun Y, Gao Y, Li Z, Zhang L, Alaa A, Tison GH, Han X, Yan K. *Diagnosis by Composition: Detecting and Localizing Unseen Diseases by Composing Learned Radiological Findings*. arXiv:2611.05231v1, 2026. [abstract](https://arxiv.org/abs/2611.05231v1)；[HTML v1](https://arxiv.org/html/2611.05231v1)；[PDF v1](https://arxiv.org/pdf/2611.05231v1)；DOI [10.48550/arXiv.2611.05231](https://doi.org/10.48550/arXiv.2611.05231)
  - 深鏈：[§1](https://arxiv.org/html/2611.05231v1#S1)、[Figure 1](https://arxiv.org/html/2611.05231v1#S1.F1)、[§3.1](https://arxiv.org/html/2611.05231v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.05231v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.05231v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.05231v1#S3.SS4)、[Figure 2](https://arxiv.org/html/2611.05231v1#S3.F2)、[§4.1](https://arxiv.org/html/2611.05231v1#S4.SS1)、[Table 1](https://arxiv.org/html/2611.05231v1#S4.T1)、[§4.2](https://arxiv.org/html/2611.05231v1#S4.SS2)、[Table 2](https://arxiv.org/html/2611.05231v1#S4.T2)、[§4.3](https://arxiv.org/html/2611.05231v1#S4.SS3)、[Table 3](https://arxiv.org/html/2611.05231v1#S4.T3)、[Table 4](https://arxiv.org/html/2611.05231v1#S4.T4)、[§4.4](https://arxiv.org/html/2611.05231v1#S4.SS4)、[§4.5](https://arxiv.org/html/2611.05231v1#S4.SS5)、[§5](https://arxiv.org/html/2611.05231v1#S5)、[Ethics statement](https://arxiv.org/html/2611.05231v1#Sx2)、[Reproducibility statement](https://arxiv.org/html/2611.05231v1#Sx3)、[Appendix A](https://arxiv.org/html/2611.05231v1#A1)、[Appendix B](https://arxiv.org/html/2611.05231v1#A2)、[Table 5](https://arxiv.org/html/2611.05231v1#A2.T5)、[Table 6](https://arxiv.org/html/2611.05231v1#A2.T6)、[Appendix C](https://arxiv.org/html/2611.05231v1#A3)、[Figure 5](https://arxiv.org/html/2611.05231v1#A3.F5)、[Appendix D](https://arxiv.org/html/2611.05231v1#A4)、[Table 7](https://arxiv.org/html/2611.05231v1#A4.T7)、[Appendix E](https://arxiv.org/html/2611.05231v1#A5)、[Appendix F](https://arxiv.org/html/2611.05231v1#A6)、[Appendix G](https://arxiv.org/html/2611.05231v1#A7)、[Table 8](https://arxiv.org/html/2611.05231v1#A8.T8)、[Table 10](https://arxiv.org/html/2611.05231v1#A8.T10)、[Figure 6](https://arxiv.org/html/2611.05231v1#A9.F6)
- **code** — DiagnosisByComposition（匿名程式庫）. [https://anonymous.4open.science/r/DiagnosisByComposition/](https://anonymous.4open.science/r/DiagnosisByComposition/)

[Home](../) · [AI Papers](./)
