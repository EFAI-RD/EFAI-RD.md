---
catalog_id: "doi:10.64898/2026.09.23.26363835"
editors:
  - "Clare"
refs:
  main:
    title: "CARE-MVLM: Counterfactual Abstention and Region-Grounded Evidence in Mammography Vision-Language Models"
    url: "https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full"
status: published
skill_version: "write-ai-paper@2.9"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 把病灶從乳房攝影上抹掉，VLM 會改口說「無法判斷」嗎？CARE-MVLM 用反事實三聯組訓練棄答與證據框

## 來源

- 團隊：Bowen Qu、Weixin Liu、Matthew Murrow、Matthew Burger、Xingyi Guo、Mihir Sachin Vaidya、Susannah L. Rose、Murat Kantarcioglu、Bradley A. Malin、Zhijun Yin；單位為 Vanderbilt University、Vanderbilt University Medical Center 與 Virginia Tech。通訊作者為 Zhijun Yin。[(ref: main)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 論文：*CARE-MVLM: Counterfactual Abstention and Region-Grounded Evidence in Mammography Vision-Language Models*，medRxiv 預印本 v1，2026-09-25 張貼，Radiology and Imaging 分類；著作權聲明為 all rights reserved（未經許可不得再利用）。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1)
- 識別碼：[DOI: 10.64898/2026.09.23.26363835](https://doi.org/10.64898/2026.09.23.26363835)。
- 全文：[medRxiv 全文 HTML](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)；資料來源依論文 Data Availability 列出 [MammoVQA](https://github.com/PiggyJerry/MammoVQA)、[CBIS-DDSM（TCIA）](https://www.cancerimagingarchive.net/collection/cbis-ddsm/) 與一個 [University of Cambridge repository 項目](https://www.repository.cam.ac.uk/items/b6a97f0c-3b9b-40ad-8f18-3d121eef1459)。[(ref: main Data Availability)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 研究性質：完整方法研究，不是 pilot；三個模組皆已實作並在 1,578 個測試三聯組上評估，與同骨幹的四個基線、一個去除 selector 的版本及兩個商用 VLM 比較。主要比較只報點估計，信賴區間只出現在消融實驗；沒有讀者研究或臨床工作流程評估。[(ref: main §3.1–3.5)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 證據邊界：本文數值以 medRxiv v1 全文的正文敘述為準；Table 1 的逐格數值與論文中以方程式呈現的損失函數、JR 公式未納入引述，只引用正文明列的數字與文字定義。

**編輯：** Clare

作者把乳房攝影上已標註的病灶「抹掉」做成反事實影像，訓練一個建在凍結 Qwen2.5-VL-7B-Instruct 上的三模組系統：病灶還在時回答並畫出證據框，病灶被抹掉時改為棄答；在 1,578 個測試三聯組上，它對抹掉病灶的影像棄答 47.97%，同骨幹基線的棄答差距（ASG）最多 1.14 個百分點、它則是 21.48，但要求「答對、框對、無關編輯不受影響、病灶抹掉會棄答」同時成立的 Joint Reliability 只有 4.75%。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

## 流程

![左側為同一題目的三個版本：原始影像 x_O、在無病灶區域做相同編輯的 random removal x_R、把標註病灶以周圍組織重建的 target removal x_T。三者送入凍結的 Qwen2.5-VL-7B-Instruct 骨幹，再分給三個模組：讀骨幹特徵的答案頭、以答案為條件產生框的 evidence generator（自有 LoRA）、決定回答或棄答的 selector（自有 LoRA、prompt MLP 與局部 MIL 分支）。右側為期望行為：x_O 答對並給出對應標籤的框、x_R 仍答對、x_T 棄答](assets/care-mvlm-counterfactual-triplet-workflow.png)

圖：本書庫依論文 §2–§3 的文字與 Fig. 1 圖說重繪的編輯示意圖，不含成效數值，未複製論文原圖。[(ref: main §2, Fig. 1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

## 背景／問題

作者的出發點是：乳房攝影判讀要把每個發現連到影像上的依據，依據不存在時就不該下判斷，VLM 也應該如此。作者主張現有 VLM 很少同時做到答對、指出對應病灶、並在病灶證據被移除後棄答；這個主張的主要依據是作者團隊自己先前的預印本（論文參考文獻 [10]），另引用一篇整張影像替換的研究（[9]），該研究報告換掉影像後準確度最多只掉 6.5 個百分點。[(ref: main §1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

作者把問題拆成三件需要分開檢查的事：答案對不對、證據框是不是真的落在支持該標籤的病灶上、以及棄答是不是對「證據消失」有反應。作者認為沒有經過證據移除測試的棄答，無法和一般性的保守區分；這一點論文沒有另附引用，是作者的論證。[(ref: main §1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

## 方法摘要

每一筆影像加問題被擴成一個三聯組：原始影像 x_O、random removal x_R（在無病灶區域套用與病灶數量、寬高相符的同一種編輯，病灶保留）、target removal x_T（把每個標註病灶以周圍非病灶組織重建）。x_R 的作用是對照：如果模型只是對「影像被編輯過」起反應，x_R 也會觸發棄答。[(ref: main §2.1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

系統建在 Qwen2.5-VL-7B-Instruct 上，骨幹權重從不更新，分成三個分階段訓練、推論時凍結的模組：答案頭直接讀骨幹特徵；evidence generator 與 selector 各自插入一組 LoRA adapter。評估同時看答案（Cov、Sel-Acc、CCR）、定位（GA）與反事實行為（ASG、CF-H、GCF-H、JR）。[(ref: main §2.2–2.4, §3.2)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

## 方法詳解

**任務與標籤。** 輸入是乳房攝影 x 與問題 q，輸出是答案加證據框，或棄答。Pathology 題為 Benign／Malignant 二選一；Abnormality 題的答案是九類異常的子集（正文舉 Mass、Calcification 為例），九類對應方式沿用論文參考文獻 [17]。[(ref: main §2.1, §3.1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

**答案頭。** 以問題為條件的分數從凍結的視覺 token 中挑出至多 K_v 個做加權 pooling，再與問題表徵經 MLP 融合。Pathology 用 softmax 頭；Abnormality 用 sigmoid 輸出加一個預測要保留幾個標籤的 cardinality 頭。訓練項包括：x_O 與 x_R 上的加權 cross-entropy（稀有 Abnormality 類別的負項做 focal 調整）、cardinality 的 cross-entropy，以及三個跨視圖項：讓 x_O 與 x_R 的預測一致、以 margin δ_tar 讓真實標籤在 x_O／x_R 的分數高於 x_T、以及讓 x_O 與 x_R 的表徵比其他配對更接近（權重 β_repr）。[(ref: main §2.2)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

**Answer-conditioned evidence generation。** evidence generator 以獨立 LoRA 產生框，條件是答案：訓練時用真實標籤、推論時用預測標籤。作者的設計理由是讓定位去解釋一個已固定的答案，而不是和答案競爭。框座標以正規化網格上的整數 token 輸出，訓練目標是座標 token（L_coord）與其餘輸出 token（L_structure）的加權 cross-entropy；推論時只保留幾何上有效、且與預測標籤相符的框。[(ref: main §2.3)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

**Counterfactual answerability selection。** selector 由另一組 LoRA、prompt MLP 與一個以問題為條件、pooling 至多 K_v 個局部視覺 token 的 MIL 分支組成，並有可訓練的 gate。作者特別說明 selector 看不到監督答案 token、真實框或視圖身分。訓練目標包括：以接受 x_O、x_R 並拒絕 x_T 為目標的 view-weighted BCE；以 margin δ_pair 讓 x_O、x_R 排在 x_T 之上的 pairwise 項；以及 margin δ_ctr 的 contrastive 項。推論時，分數 s(x,q) 加上偏移 a 達到門檻 τ_acc 才回答，否則棄答。[(ref: main §2.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

**比較對象。** 同骨幹基線：B0 為零樣本；B1 只用原始視圖做答案監督；B2 在 B1 上加證據框監督，但不看移除視圖；B3 再在單一 generator 內加入以 target removal 為目標的棄答監督，沒有獨立 selector。另有關閉選擇功能的 CARE-MVLM w/o selector，以及在同一批三聯組、同一協定、temperature 0 下評估的 GPT-5.6 與 Gemini-3.5-flash。[(ref: main §3.3)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

**訓練設定。** LoRA rank 16、每批 16 個三聯組、seed 42；答案頭訓練 5 個 epoch、學習率 3e-4；evidence refinement 2 個 epoch、學習率 1e-5。λ_coord 從 {0.2, 0.5, 0.8} 中依 Train-dev 上的 GA 選定（以平均 matched IoU 決勝），測試用 0.8；偏移 a 從 {−ln4, −ln2, 0, ln2, ln4} 中依 Train-dev 上的 JR 選定（以 CF-H 決勝），測試用 ln2。[(ref: main §3.3)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

**指標。** [(ref: main §3.2)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

- **Cov** — 有效且未棄答的回答比例；Sel-Acc 是這些回答中的正確率；CCR = Cov × Sel-Acc，即全部題目中被回答且答對的比例。
- **GA**（grounded accuracy）— 每個預測框都要與一個標籤相容的參考框 IoU ≥ 0.3。
- **ASG** — target removal 的棄答率減去 random removal 的棄答率。
- **CF-H** — target removal 棄答率與 x_O／x_R 平均答對率的調和平均；**GCF-H** 把答對率換成同時要求嚴格定位的版本。
- **JR**（Joint Reliability）— 最嚴格的指標，要求同一個三聯組內同時成立：x_O 回答且答對、x_R 答對、x_O 定位正確、x_T 有效棄答；無效輸出不算有效棄答。

- **論文未交代** — 本地模型與 GPT-5.6、Gemini-3.5-flash 的 prompt 全文，以及商用模型如何被要求棄答與輸出框。[(ref: main §3.3)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **論文未交代** — 門檻 τ_acc 如何設定（正文只說明偏移 a 的選擇方式），以及 Train-dev 從哪裡切出。[(ref: main §2.4, §3.3)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **論文未交代** — Train／Eval／Test 是以影像還是病人為單位切分，以及三聯組背後有多少張不重複的影像或多少位病人。[(ref: main §3.1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **論文未交代** — 病灶移除所用的重建演算法細節；正文只說明以周圍非病灶區域重建病灶，做法沿用作者先前的預印本。[(ref: main §2.1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **論文未交代** — 程式碼、模型權重與三聯組資料是否釋出；Data Availability 只列出原始資料來源。[(ref: main Data Availability)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

## 資料與實驗

下表整理論文 §3.1 與 Data Availability 的資料規模。[(ref: main §3.1, Data Availability)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

| 項目 | 內容 |
|---|---|
| 影像來源 | CBIS-DDSM、MIAS、VinDr-Mammo（經 MammoVQA 取得），涵蓋數位化 screen-film 與 full-field digital 影像 |
| 題型 | Pathology（Benign／Malignant）與 Abnormality（九類異常的多標籤子集） |
| 單位 | 三聯組（x_O、x_R、x_T），共 7,358 個 |
| 切分 | Train 5,044／Eval 736／Test 1,578 三聯組 |
| 測試題組成 | 622 題 Pathology、956 題 Abnormality |
| 影像編輯品質檢查 | 一位放射科醫師檢視 50 個隨機三聯組 |
| 新收資料 | 無；只使用既有、去識別化的公開資料 |

下表由本書庫整理自論文 §3.4 正文，對應論文 Table 1（測試集；所有數值為百分比或百分點）。「—」表示正文沒有明列該格數值；B0 的數值正文未討論。GPT-5.6 與 Gemini-3.5-flash 的 ASG、CF-H、JR、GA 依正文「GPT-5.6 and Gemini-3.5-flash」的列舉順序對應，作者另以 JR ÷ GA 算出的比例（約 18% 與 6%）與此對應一致。[(ref: main §3.4, Table 1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

| Method | Cov | Sel-Acc | CCR | GA | Target-removal abstention | ASG | CF-H | GCF-H | JR |
|---|---|---|---|---|---|---|---|---|---|
| B1（answer SFT） | 100（full coverage） | 56.08 | 56.08 | 0.00 | — | 0 | 0 | 0 | 0 |
| B2（+ evidence boxes） | 100（full coverage） | 55.64 | — | 5.58 | — | 0 | 0 | 0 | 0 |
| B3（+ abstention, single generator） | 1.58 | 76.00 | 1.20 | — | — | — | — | — | — |
| Same-backbone baselines，最佳值 | — | — | — | — | — | ≤ 1.14 | — | — | ≤ 0.06 |
| CARE-MVLM w/o selector | 100.00 | 59.19 | 59.19 | 11.09 | 0.00 | — | — | — | — |
| **CARE-MVLM** | 85.93 | 59.00 | 50.70 | 10.39 | 47.97 | 21.48 | 47.35 | 16.57 | 4.75 |
| GPT-5.6 | — | — | — | 21.67 | — | 8.24 | 27.37 | 20.17 | 3.87 |
| Gemini-3.5-flash | — | — | — | 18.63 | — | 2.34 | 13.88 | 11.38 | 1.08 |

下表整理論文 §3.5 的兩組消融，信賴區間為 Eval 集上 2,000 次 bootstrap 的 pointwise 95% CI；兩組各有自己的參照執行，所以參照值不同。[(ref: main §3.2, §3.5)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

| Ablation | Metric | Reference → ablated | Paired difference（95% CI） |
|---|---|---|---|
| 移除 answer conditioning | GCF-H | 17.00 → 14.90 | −2.10（−3.74, −0.49） |
| 移除 answer conditioning | CF-H | 不變（答案與 selector 決策固定） | — |
| 移除 selector 的 pairwise 與 contrastive 項 | CF-H | 48.41 → 45.26 | −3.15（−5.32, −1.11） |
| 移除 selector 的 pairwise 與 contrastive 項 | GCF-H | 17.37 → 16.76 | −0.61（−1.17, −0.06） |

## 結果

- **只做答案或框的監督，模型不會因病灶消失而棄答** — B1 與 B2 在全覆蓋下的 Sel-Acc 為 56.08% 與 55.64%，但移除病灶後都不棄答，四個反事實指標全為零；加入框監督讓 GA 從 B1 的 0.00% 升到 B2 的 5.58%。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **把棄答塞進同一個 generator 會變成幾乎全部棄答** — B3 的 Sel-Acc 76.00% 是各方法最高，但只回答 1.58% 的題目，CCR 掉到 1.20%（B1 為 56.08%）。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **獨立 selector 帶來對病灶敏感的棄答** — 開啟 selector 後，target removal 棄答率從 0.00% 升到 47.97%；代價是原始視圖的 coverage 從 100.00% 降到 85.93%、CCR 從 59.19% 降到 50.70%，Sel-Acc 幾乎不變（59.00% 對 59.19%），GA 從 11.09% 降到 10.39%。ASG 為 21.48 個百分點，同骨幹基線最多 1.14；random removal 下的預測框只有 1.58% 有至少一半落在被編輯區域內。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **和商用 VLM 比，棄答較強、定位較弱** — 相對 GPT-5.6 與 Gemini-3.5-flash，CARE-MVLM 的 Sel-Acc 與 CCR 較高，ASG（21.48 對 8.24、2.34）與 CF-H（47.35 對 27.37、13.88）較高，JR 點估計最高（4.75% 對 3.87%、1.08%）；但 GA 較低（10.39% 對 21.67%、18.63%），GCF-H 16.57 低於 GPT-5.6 的 20.17、高於 Gemini-3.5-flash 的 11.38。這些比較都只有點估計，沒有信賴區間或顯著性檢定。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **答對又框對之後，其餘條件成立的比例** — 作者以 JR ÷ GA 計算，在原始視圖已答對且定位正確的案例中，x_R 仍答對且 x_T 棄答同時成立的比例約為 CARE-MVLM 46%、GPT-5.6 18%、Gemini-3.5-flash 6%。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **影像編輯本身的品質** — 放射科醫師檢視 50 個隨機三聯組：target removal 在 92% 完全移除病灶，random removal 在 94% 保留了有診斷意義的證據；76% 沒有會改變判讀的瑕疵，10% 有與編輯相關的不對稱，另 14% 有其他編輯瑕疵。[(ref: main §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- **消融** — 拿掉 answer conditioning 讓 GCF-H 下降 2.10（95% CI −3.74 至 −0.49）；拿掉 selector 的 pairwise 與 contrastive 項讓 CF-H 下降 3.15（95% CI −5.32 至 −1.11）。[(ref: main §3.5)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

作者的結論是：在同骨幹基線與兩個商用 VLM 中，CARE-MVLM 有最強的病灶敏感棄答與最高的 Joint Reliability，但 Joint Reliability 的絕對值仍低，證據定位是主要的改進目標。[(ref: main §4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)

## 限制

- 作者列出的限制：Joint Reliability 的絕對值仍低，證據定位是主要待改進處；未來需要評估更多 VLM，以及比人工抹除更自然的「證據不存在」情境。[(ref: main §4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 作者列出的限制：病灶移除的編輯瑕疵可能依位置與組織而在不同視圖間有差異；放射科醫師檢查的 50 個三聯組中，24% 有不對稱或其他編輯瑕疵。[(ref: main §2.1, §3.4)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 論文未提供：主要比較（含與商用 VLM 的比較）的信賴區間或顯著性檢定；訓練只報單一 seed。GPT-5.6 與 Gemini-3.5-flash 的 prompt 與棄答指示未公開，比較結果與商用模型被要求的輸出格式綁在一起。[(ref: main §3.2, §3.3)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 論文未提供：切分單位與不重複影像／病人數；同一張影像能衍生多個題目，若切分不是以影像或病人為單位，測試集可能與訓練集共用影像。這一點論文沒有交代，本文無法判斷。[(ref: main §3.1)](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)
- 本書庫補充：「病灶被抹掉就該棄答」是作者設計的反事實測試，臨床上的「證據不足」多半是病灶不明顯、影像品質或視野問題，而不是病灶被乾淨地移除；ASG 量到的是對這種人工編輯的敏感度，能否轉移到自然發生的證據不足，論文沒有評估。
- 本書庫補充：selector 的偏移 a 是依 Train-dev 上的 JR 選定，換言之 coverage 與棄答之間的取捨點是為 JR 調出來的；在不同的部署門檻下，CCR 與棄答率會有不同的組合，論文只報告了一個操作點。

## 與書庫其他文章的關係

MammoClaw 讓凍結的 MLLM 透過確定性工具與演化出的技能讀乳房攝影，只評估答案的 macro-F1；本篇在同一個影像領域另外量測證據框是否對應病灶、以及病灶被移除後會不會棄答，補上 MammoClaw 沒有檢查的「答案有沒有依據」: [工具給齊了，凍結的 MLLM 就會讀乳房攝影嗎？MammoClaw 用失敗軌跡演化出的技能補上「怎麼用」](2026-10-01-mammoclaw-skill-evolving-mammography-agent.md)

OCT 影像依賴稽核在推論端固定理由、替換影像，量測影像對決策的實際貢獻；本篇則把「移除影像證據」做成訓練與評估用的反事實視圖，並以 random removal 對照排除「只是對編輯起反應」，兩篇從稽核端與訓練端處理同一個「答案是否真的依賴影像證據」的問題: [抽掉影像、留下理由：VLM 在 anti-VEGF 治療決策裡，OCT 到底出了多少力？](2026-09-23-vlm-oct-image-dependence-audit.md)

## 實務的啟發

本篇的定位是一套可借用的評估設計，以及一個在單一操作點、只有點估計下看起來有效的訓練做法；它不是可直接部署的棄答機制。

第一，三聯組評估本身值得借用。若要檢查自家影像 VLM 的棄答或「不確定」輸出是否真的與證據有關，可以比照 x_R／x_T 的設計：同時做「移除目標病灶」與「在無關區域做相同編輯」，再看兩者的棄答率差（ASG），而不只看整體棄答率。論文中 B3 的 Sel-Acc 最高但只回答 1.58% 的題目，說明只看已回答題目的正確率會誤導，CCR 這類把覆蓋率算進去的指標應一起報告。

第二，「答對」「框對」「該棄答時棄答」三者分開量測時都可能看起來不錯，同時要求時卻很低：本篇最好的 JR 只有 4.75%，而 GA 最高的反而是 GPT-5.6。導入任何宣稱「可解釋」或「會棄答」的乳房攝影 VLM 前，應在本地資料上用同一個案例同時檢查這幾個條件，而不是分別看各自的平均。

第三，若要沿用獨立 selector 的做法，需要先補齊論文沒有交代的部分：棄答門檻如何設定、切分是否以病人為單位、以及在自然發生的證據不足（例如緻密乳房或影像品質不佳）下棄答是否仍有意義。本書庫認為，在這些問題有答案之前，CARE-MVLM 的數字應被讀成「這個方向可行」的訊號，而非可移植的效能。

## References

- `main`：[CARE-MVLM: Counterfactual Abstention and Region-Grounded Evidence in Mammography Vision-Language Models（medRxiv v1 全文）](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1.full)；本文使用 §1 Introduction、§2.1–2.4 Methods、§3.1 Data、§3.2 Evaluation Metrics、§3.3 Models and Training、§3.4 Results、§3.5 Ablation Study、§4 Conclusion、Data Availability，以及 Fig. 1 與 Table 1 的圖表說明。
- `abs`：[medRxiv v1 摘要頁](https://www.medrxiv.org/content/10.64898/2026.09.23.26363835v1)。
- `doi`：[10.64898/2026.09.23.26363835](https://doi.org/10.64898/2026.09.23.26363835)。
- `data`：[MammoVQA（論文列出）](https://github.com/PiggyJerry/MammoVQA)；[CBIS-DDSM（TCIA，論文列出）](https://www.cancerimagingarchive.net/collection/cbis-ddsm/)；[University of Cambridge repository 項目（論文列出）](https://www.repository.cam.ac.uk/items/b6a97f0c-3b9b-40ad-8f18-3d121eef1459)。

[Home](../) · [AI Papers](./)
