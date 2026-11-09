---
parent: AI Papers
nav_order: 5
title: "配上不相符的胸片，照片幻覺從 25–37.5% 升到 45–57.5%"
catalog_id: "arxiv:2611.06631"
editors:
  - "Clare"
refs:
  main:
    title: "Trick-or-Treat: Adversarial Evaluation of Multimodal Medical Reasoning with Synthetic Images"
    url: "https://arxiv.org/html/2611.06631v1"
  abs:
    title: "arXiv abstract page: 2611.06631v1"
    url: "https://arxiv.org/abs/2611.06631v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 配上不相符的胸片，照片幻覺從 25–37.5% 升到 45–57.5%

## 來源

- 團隊：Oishi Banerjee、Eujin Lee、Sung Eun Kim、Alexandra N. Willauer、Christine Y. Zhou、Zhizhou Yang、Pranav Rajpurkar，共 7 位作者；全員隸屬 Harvard Medical School Department of Biomedical Informatics，另有作者分屬 Cornell University Department of Computer Science、Massachusetts General Hospital（Division of Gastroenterology、Department of Surgery）與 University of Cincinnati（Division of Pulmonary, Critical Care, and Sleep Medicine）。[(ref: main author block)](https://arxiv.org/html/2611.06631v1)
- 論文：*Trick-or-Treat: Adversarial Evaluation of Multimodal Medical Reasoning with Synthetic Images*，arXiv:2611.06631v1（cs.CV；另列 cs.AI），2026-11-04 提交，目前只有 v1；授權為 CC BY 4.0；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2611.06631v1)
- 識別碼：arXiv [2611.06631](https://arxiv.org/abs/2611.06631v1)；DOI [10.48550/arXiv.2611.06631](https://doi.org/10.48550/arXiv.2611.06631)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.06631v1)、[PDF v1](https://arxiv.org/pdf/2611.06631v1)。
- 程式與資料：論文沒有提供程式碼或基準資料的釋出連結，也沒有列出全部 40 種疾病與各張照片的 ground-truth caption；胸片取自公開資料集 ReXGradient。[(ref: main §3.2)](https://arxiv.org/html/2611.06631v1#S3.SS2)
- 研究性質：評估基準（benchmark）與失效模式稽核，不是新模型或新方法；作者在摘要中稱之為以合成影像做對抗式多模態評估的 proof of concept。規模為 40 種疾病、40 張真實胸片與 80 張合成臨床照片，每個比率附 Clopper–Pearson 95% 信賴區間，設定間差異以 exact McNemar 檢定。[(ref: abstract)](https://arxiv.org/abs/2611.06631v1) [(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1) [(ref: main §5.2)](https://arxiv.org/html/2611.06631v1#S5.SS2)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、Table 1 與 Appendix A 為準；論文未量測診斷是否正確，本文也不推論診斷層級的結果。

**編輯：** Clare

作者把真實胸片和兩張只差一個發現的合成臨床照片配對，發現三個前沿 VLM 在照片與胸片「指向不同診斷」時，描述照片時捏造出具臨床意義異常的比例從單看照片的 25–37.5% 升到 45–57.5%，而且捏造的方向傾向配合胸片暗示的診斷。[(ref: abstract)](https://arxiv.org/abs/2611.06631v1) [(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1)

## 流程

![三段圖。上方標題「A. Trick-or-Treat 基準與評估流程」，由左到右為實線圓角框：淺藍色「40 張真實胸片（ReXGradient，成人 AP/PA）每張對應 1 種疾病」以兩支箭頭分別連到淺紅色「Matched 照片：合成，呈現同一疾病的外觀徵象」與淺綠色「Mismatched 照片：合成，同一人換成替代發現」；兩張照片各以箭頭同時連到淺藍色「Photo only：只給照片」與「Photo + radiograph：照片與胸片一起給」兩框；兩框再以箭頭連到最右淺藍色「3 個前沿模型作答 → 只抽出 PHOTO_FINDINGS → Claude Sonnet 5.5 依 rubric 判 FP / FN」；框下註「每個模型 × 每種設定：40 張 matched 與 40 張 mismatched 照片」。下方左為「B. Matched 照片」、右為「C. Mismatched 照片」兩張長條圖，縱軸為照片 false positive 率（%，刻度 0–80），橫軸為 Claude Fable 5.1、GPT-6 Astra、Gemini 4 Argon，每個模型左側灰色長條為 Photo only、右側橘色長條為 Photo + radiograph，長條上有黑色誤差線並標數值。B 圖數值：25 與 17.5、12.5 與 2.5、10 與 7.5；C 圖數值：25 與 45、37.5 與 57.5、35 與 45。最下方小字註明誤差線為論文 Table 1 的 Clopper–Pearson 95% CI。](assets/trick-or-treat-design-and-fp-rates.png)

圖：本書庫依論文 §3–§4、Appendix A 與 Table 1 重繪。上方流程只含設計與資料量；下方長條為 Table 1 的照片 false positive 率與 95% CI，未複製論文原圖（論文 Fig. 1、Fig. 4 為病例範例，Fig. 2 為單一疾病的建構示意，Fig. 3 為錯誤率圖）。[(ref: main §3)](https://arxiv.org/html/2611.06631v1#S3) [(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1) [(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1)

## 背景／問題

作者的出發點是：讀多種醫療影像的 VLM，必須能分辨兩種模態何時共同指向同一診斷、何時沒有。他們舉的例子是一張提示病毒性肺炎的胸片，配上水痘的結痂水疱照片時應想到 varicella pneumonia，配上普通痘痘的照片時則不應跳到同一個診斷。[(ref: main §1)](https://arxiv.org/html/2611.06631v1#S1)

「模型難以整合多模態」這個前提，作者以既有研究支持：先前研究顯示相互衝突的文字線索會降低影像判讀準確度；已有的多影像模態基準則多半改用放射科教學病例，或從醫院特地收集多種眼科影像。作者認為這類做法受限於既有病例庫或高成本的資料收集，影像數量與可問的問題都被綁住，因此很難做「只改一個發現」的受控比較。[(ref: main §1)](https://arxiv.org/html/2611.06631v1#S1) [(ref: main §2.2)](https://arxiv.org/html/2611.06631v1#S2.SS2)

本篇要回答的不是「模型能不能診斷」，而是更窄的一個問題：同一張臨床照片，旁邊多一張胸片之後，模型對照片本身的描述會不會變，變的方向是否被胸片牽著走。

## 方法摘要

**配對設計。** 每種疾病挑一張真實胸片，搭配兩張合成臨床照片：matched 照片呈現支持同一診斷的外觀徵象，mismatched 照片則是同一個人、同一部位、外觀相近但不指向該診斷的替代發現（例如 crusted chickenpox vesicles 換成 pimples、cyanosis 換成紫色指甲油）。作者強調 mismatched 照片的發現可以和胸片發現在同一位病人身上並存，只是不構成一個統一診斷。[(ref: main §3.1)](https://arxiv.org/html/2611.06631v1#S3.SS1) [(ref: main §3.3)](https://arxiv.org/html/2611.06631v1#S3.SS3)

**兩種設定。** 每張照片在兩種設定下各問一次：photo + radiograph（照片與胸片一起給，要求分別描述兩張影像並說明合起來可能提示什麼）與 photo only（只給照片）。[(ref: main §4.1)](https://arxiv.org/html/2611.06631v1#S4.SS1)

**量什麼。** 只評分模型對「照片」的描述：false positive（FP）是描述了照片裡沒有的、具臨床意義的異常；false negative（FN）是漏掉照片裡有的、具臨床意義的異常；normal variant 與臨床上不重要的偶發特徵不計。評分由 LLM judge 依 rubric 進行，不評估診斷是否正確。[(ref: main §4.2)](https://arxiv.org/html/2611.06631v1#S4.SS2)

## 方法詳解

**胸片來源。** 胸片取自 ReXGradient，只保留 AP 或 PA 視角；因為模型的內容安全過濾較常拒絕兒童影像，只用 18 歲以上病人。作者以疾病相關關鍵字（例如 pulmonary Kaposi sarcoma 用 "flame-shaped"）查詢報告後設資料找候選，再對照報告確認發現相容，最後由臨床醫師逐張確認與目標疾病相容；acromegaly 與 osteogenesis imperfecta 兩例裁切掉不相容的肩臂發現。[(ref: main §3.2)](https://arxiv.org/html/2611.06631v1#S3.SS2)

**照片生成。** 用 gemini-3-pro-image 文字生成影像模型，採 human-in-the-loop：依回饋改寫 prompt、提供來自研究或教學來源（非商用授權）的參考影像、把部分成功的生成結果附上修改意見再生成，或指定要修改的座標。同一疾病的兩張照片由其中一張衍生另一張、或由同一張底圖各自生成，因此是同一個人。照片人物的年齡與性別依胸片後設資料配對；由於胸片資料集幾乎沒有族裔標註，族裔依近似 2020 年美國人口比例的可重現抽樣指定。[(ref: main §3.3)](https://arxiv.org/html/2611.06631v1#S3.SS3)

**臨床審查。** 每組配對經多輪臨床醫師審查：matched 照片的徵象是否忠實、mismatched 照片的替代發現是否合適、與胸片是否相容；不合適就把意見帶進下一輪生成。每題最終版本由 1–3 位肺科、骨科或內科的 board-certified 醫師核准。[(ref: main §3.3)](https://arxiv.org/html/2611.06631v1#S3.SS3)

**模型與呼叫參數。** 三個模型經原廠 API 呼叫：GPT-6 Astra（Azure OpenAI deployment gpt-6-astra）、Gemini 4 Argon（Google Vertex AI 上的 gemini-4-argon）、Claude Fable 5.1（claude-fable-5-1，Anthropic Messages API）。全部使用各家預設取樣設定，沒有設定 temperature、top-p 或 seed；最大輸出長度 GPT-6 Astra 為 4,000 tokens、Gemini 4 Argon 用預設、Claude Fable 5.1 雙影像請求 12,000、單照片請求 6,000。影像以 base64 PNG 傳送，最長邊超過 1,568 像素時縮到 1,568。[(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1)

**Prompt。** 兩種設定的 prompt 全文列在 Appendix A：雙影像版要求以 CXR_FINDINGS、PHOTO_FINDINGS、SUGGESTIVE_OF 三個標籤分行回答，並告知兩張影像來自同一位病人；單照片版只有 PHOTO_FINDINGS 與 SUGGESTIVE_OF。[(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1)

**Extract-then-judge。** 先抽出 PHOTO_FINDINGS 段落、丟掉胸片描述與 SUGGESTIVE_OF 的診斷假設，因此回答其他地方寫出的診斷不會被算成照片發現。Judge 為 claude-sonnet-5-5（最大輸出 500 tokens、預設取樣），拿抽出的文字對照該照片的 ground-truth caption，依同一份 rubric 輸出 FALSE_POSITIVE、FALSE_NEGATIVE 兩個 YES／NO 與一行理由；同一回答可以同時是 FP 與 FN。[(ref: main §4.2)](https://arxiv.org/html/2611.06631v1#S4.SS2) [(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1)

**統計。** 每個比率以 40 張照片為分母、附 exact（Clopper–Pearson）95% CI；同一批照片在兩種設定間的差異以 exact McNemar 檢定，分別報告單一模型與三模型合併的結果。[(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1) [(ref: main §5.2)](https://arxiv.org/html/2611.06631v1#S5.SS2)

- **論文未交代** — LLM judge 的判定沒有和臨床醫師的判讀比對過一致性；作者在討論中把納入臨床醫師判斷列為未來工作。[(ref: main §6)](https://arxiv.org/html/2611.06631v1#S6)
- **論文未交代** — 40 種疾病的完整清單、每張照片的 ground-truth caption、所用胸片在 ReXGradient 中的識別碼，以及基準資料與程式碼是否釋出。
- **論文未交代** — 每張照片在每種設定下只問一次、使用預設取樣，論文沒有報告重複詢問時答案的變異。

## 資料與實驗

### 資料

| 項目 | 內容 | ref |
|---|---|---|
| 疾病數 | 40 種，含急性表現（traumatic hemothorax、pulmonary contusion、varicella pneumonia 等）與慢性／全身性疾病（systemic sclerosis、acromegaly、Marfan syndrome 等） | [(ref: main §3.1)](https://arxiv.org/html/2611.06631v1#S3.SS1) |
| 胸片 | 40 張真實胸片，來自 ReXGradient；AP 或 PA 視角；病人皆 18 歲以上 | [(ref: main §1)](https://arxiv.org/html/2611.06631v1#S1) [(ref: main §3.2)](https://arxiv.org/html/2611.06631v1#S3.SS2) |
| 胸片病人特徵 | 50% 標註為男性；平均年齡 45 歲（SD 18） | [(ref: main §3.2)](https://arxiv.org/html/2611.06631v1#S3.SS2) |
| 臨床照片 | 80 張合成照片（每種疾病 matched、mismatched 各 1 張，同一人物）；gemini-3-pro-image 生成，臨床醫師多輪審查 | [(ref: main §1)](https://arxiv.org/html/2611.06631v1#S1) [(ref: main §3.3)](https://arxiv.org/html/2611.06631v1#S3.SS3) |
| 照片人物族裔分布 | White 55%、Black 17.5%、Hispanic/Latino 20.0%、Asian 7.5% | [(ref: main §3.3)](https://arxiv.org/html/2611.06631v1#S3.SS3) |
| 受測模型 | GPT-6 Astra、Gemini 4 Argon、Claude Fable 5.1 | [(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1) |
| 設定 | photo only、photo + radiograph；每模型每設定 40 張 matched 與 40 張 mismatched 照片 | [(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1) |
| Judge | Claude Sonnet 5.5，extract-then-judge，rubric 判 FP／FN | [(ref: main §4.2)](https://arxiv.org/html/2611.06631v1#S4.SS2) |

### 實驗

下表為論文 Table 1 全文：各模型、照片類型與設定下的每張照片錯誤率（%），括號為 Clopper–Pearson 95% CI；FP 為描述了照片沒有的具臨床意義異常，FN 為漏掉照片有的具臨床意義異常，Any 為至少一個 FP 或 FN。[(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1)

| Model | Setting | Matched FP | Matched FN | Matched Any | Mismatched FP | Mismatched FN | Mismatched Any |
|---|---|---|---|---|---|---|---|
| Claude Fable 5.1 | Photo only | 25.0 (12.7–41.2) | 27.5 (14.6–43.9) | 30.0 (16.6–46.5) | 25.0 (12.7–41.2) | 2.5 (0.1–13.2) | 27.5 (14.6–43.9) |
| Claude Fable 5.1 | Photo + radiograph | 17.5 (7.3–32.8) | 12.5 (4.2–26.8) | 20.0 (9.1–35.6) | 45.0 (29.3–61.5) | 2.5 (0.1–13.2) | 47.5 (31.5–63.9) |
| GPT-6 Astra | Photo only | 12.5 (4.2–26.8) | 10.0 (2.8–23.7) | 15.0 (5.7–29.8) | 37.5 (22.7–54.2) | 2.5 (0.1–13.2) | 40.0 (24.9–56.7) |
| GPT-6 Astra | Photo + radiograph | 2.5 (0.1–13.2) | 2.5 (0.1–13.2) | 2.5 (0.1–13.2) | 57.5 (40.9–73.0) | 0.0 (0.0–8.8) | 57.5 (40.9–73.0) |
| Gemini 4 Argon | Photo only | 10.0 (2.8–23.7) | 7.5 (1.6–20.4) | 12.5 (4.2–26.8) | 35.0 (20.6–51.7) | 2.5 (0.1–13.2) | 37.5 (22.7–54.2) |
| Gemini 4 Argon | Photo + radiograph | 7.5 (1.6–20.4) | 2.5 (0.1–13.2) | 10.0 (2.8–23.7) | 45.0 (29.3–61.5) | 5.0 (0.6–16.9) | 47.5 (31.5–63.9) |

設定間差異的 exact McNemar 檢定（論文 §5.2 文字報告）：

| 比較 | 範圍 | p |
|---|---|---|
| Matched 照片 FP，photo only → photo + radiograph（下降） | 三模型合併 | 0.08 |
| Matched 照片 FN，photo only → photo + radiograph（下降） | 三模型合併 | 0.003 |
| Mismatched 照片 FP，photo only → photo + radiograph（上升） | GPT-6 Astra | 0.02 |
| Mismatched 照片 FP，photo only → photo + radiograph（上升） | Claude Fable 5.1 | 0.02 |
| Mismatched 照片 FP，photo only → photo + radiograph（上升） | Gemini 4 Argon | 0.22 |
| Mismatched 照片 FP，photo only → photo + radiograph（上升） | 三模型合併 | < 0.001 |
| Mismatched 照片 FN | 三模型合併 | 1.0 |

[(ref: main §5.2)](https://arxiv.org/html/2611.06631v1#S5.SS2)

## 結果

- **單看照片就會出錯** — photo only 設定下，三個模型在 matched 照片上的 FN 都是各自最高（Claude Fable 5.1 27.5%、GPT-6 Astra 10%、Gemini 4 Argon 7.5%），mismatched 照片的 FN 只有 2.5%；mismatched 照片多半是正常或良性變異，FP 為 GPT-6 Astra 37.5%、Gemini 4 Argon 35%、Claude Fable 5.1 25%，作者描述模型傾向在沒有異常時捏造重要異常。[(ref: main §5.1)](https://arxiv.org/html/2611.06631v1#S5.SS1)
- **Matched 胸片有幫助** — 加入指向同一診斷的胸片後，三個模型的 FP 與 FN 都下降；FN 下降在合併檢定下達顯著（p = 0.003），FP 下降合併後未達顯著（p = 0.08）。[(ref: main §5.2)](https://arxiv.org/html/2611.06631v1#S5.SS2)
- **Mismatched 胸片讓照片 FP 上升** — 同一批 mismatched 照片配上胸片後，FP 由 37.5% 升到 57.5%（GPT-6 Astra）、35% 升到 45%（Gemini 4 Argon）、25% 升到 45%（Claude Fable 5.1）；GPT-6 Astra 與 Claude Fable 5.1 個別顯著（p = 0.02），Gemini 4 Argon 個別不顯著（p = 0.22），三模型合併 p < 0.001；FN 幾乎沒有變化（合併 p = 1.0）。[(ref: main §5.2)](https://arxiv.org/html/2611.06631v1#S5.SS2) [(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1)
- **錯誤的方向** — 作者質性檢視 mismatched 配對，觀察到胸片特別容易誘發「支持與胸片相符診斷」的照片幻覺；論文 Fig. 1 的例子是 GPT-6 Astra 單看照片時正確描述良性的 port-wine stain，配上提示外傷的胸片後把同一塊胎記讀成 flank ecchymosis。這一段是質性觀察，論文沒有量化幻覺與胸片診斷的一致比例。[(ref: main Fig. 1)](https://arxiv.org/html/2611.06631v1#S1.F1) [(ref: main §5.2)](https://arxiv.org/html/2611.06631v1#S5.SS2) [(ref: main Fig. 4)](https://arxiv.org/html/2611.06631v1#S5.F4)

## 限制

作者自述的限制：[(ref: main §6)](https://arxiv.org/html/2611.06631v1#S6)

- 只合成臨床照片、胸片用真實影像；未來可合成胸片或擴到其他模態。
- 合成照片都通過臨床醫師審查，但仍可能有人眼看不出的生成瑕疵或錯誤。
- 只評估照片描述的品質，judge 只用 Claude Sonnet 5.5；胸片描述品質、整體診斷準確度與臨床醫師判斷都未納入。
- 沒有量測下游結果；abstention、超參數選擇與 multi-agent 做法能否緩解問題，尚未評估。

本書庫補充的閱讀限制：

- **樣本量** — 每個比率只有 40 張照片，比率落在 25–60% 時 CI 寬度約 30 個百分點（例如 Claude Fable 5.1 mismatched photo + radiograph FP 45.0%，CI 29.3–61.5%），模型之間的排名不宜過度解讀。[(ref: main Table 1)](https://arxiv.org/html/2611.06631v1#S3.T1)
- **評分者與受測者的關係** — 受測模型之一（Claude Fable 5.1）與 judge（Claude Sonnet 5.5）屬同一廠商，照片生成器（gemini-3-pro-image）與受測模型之一（Gemini 4 Argon）也屬同一廠商；論文沒有討論這是否影響評分或難度，也沒有人工判讀可以對照。[(ref: main §3.3)](https://arxiv.org/html/2611.06631v1#S3.SS3) [(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1)
- **提示語的作用** — 雙影像 prompt 明說兩張影像「來自同一位病人」並要求說明合起來提示什麼；論文沒有測試拿掉這兩點時效應是否仍在，因此結果是這個 prompt 設計下的觀察。[(ref: main Appendix A)](https://arxiv.org/html/2611.06631v1#A1)
- **只看照片端** — 論文刻意只計照片描述的錯誤；mismatched 配對本身可能相容於多種診斷，所以無法從本篇得知最終診斷建議錯了多少。[(ref: main §4.2)](https://arxiv.org/html/2611.06631v1#S4.SS2)

## 與書庫其他文章的關係

兩篇都量測「另一個輸入」如何改寫模型對影像的判讀：轉診文字研究固定 MRI、逐級改寫轉診單文字，本篇則把干擾來源換成第二種影像，固定臨床照片、只改變旁邊胸片是否指向同一診斷，觀察照片描述本身被帶偏: [轉診單一句話就改變 MRI 判讀，叫模型忽略只有一個做得到](2026-10-28-referral-text-overrides-mri-mllm-glioma-abscess.md)

ModaLens 固定報告與問題、交換影像來量測醫療 VLM 是否仍看影像，本篇則讓兩種影像都在場，量的是一種影像是否會讓模型「看見」另一種影像裡不存在的發現: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎](2026-09-17-modalens-image-sensitivity.md)

## 實務的啟發

以下為本書庫的解讀，不是論文的結論。本篇規模小、評分仰賴單一 LLM judge，適合當成「可借用的量測方法」與「待驗證的警訊」，而不是對特定模型的定論。

- **可借用的量測方法** — 用同一人物、只改一個發現的配對影像，加上「單一模態」與「多模態」兩種設定的配對比較，能把「第二個輸入改變了第一個輸入的描述」這件事和一般的判讀錯誤分開。評估多模態系統時，可以把 photo only 這類單模態基線當成必備對照，而不只看合在一起的最終答案。
- **只評分中間描述** — 論文以 extract-then-judge 只評分 PHOTO_FINDINGS，避開「多種診斷都可能成立」時無法評分最終診斷的問題。需要評估多模態推理的團隊，可以考慮先要求模型分段輸出各模態的發現，再分別評分。
- **待驗證的警訊** — 在本篇的設定裡，第二張影像指向的診斷會讓模型在第一張影像上報告不存在的異常；如果系統會把多種影像或「同一位病人」的脈絡一起餵給模型，值得在自己的資料上用類似的配對設計檢查是否也有這種現象，再決定是否需要逐模態獨立判讀或要求模型標示各發現的來源影像。這不等於在臨床上已證實會造成錯誤處置，論文也沒有量測下游結果。

## References

- `main` — Banerjee O, Lee E, Kim SE, Willauer AN, Zhou CY, Yang Z, Rajpurkar P. *Trick-or-Treat: Adversarial Evaluation of Multimodal Medical Reasoning with Synthetic Images*. arXiv:2611.06631v1, 2026. [https://arxiv.org/html/2611.06631v1](https://arxiv.org/html/2611.06631v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.06631v1)、[§1](https://arxiv.org/html/2611.06631v1#S1)、[Fig. 1](https://arxiv.org/html/2611.06631v1#S1.F1)、[§2.2](https://arxiv.org/html/2611.06631v1#S2.SS2)、[§3](https://arxiv.org/html/2611.06631v1#S3)、[§3.1](https://arxiv.org/html/2611.06631v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.06631v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.06631v1#S3.SS3)、[Table 1](https://arxiv.org/html/2611.06631v1#S3.T1)、[§4.1](https://arxiv.org/html/2611.06631v1#S4.SS1)、[§4.2](https://arxiv.org/html/2611.06631v1#S4.SS2)、[§5.1](https://arxiv.org/html/2611.06631v1#S5.SS1)、[§5.2](https://arxiv.org/html/2611.06631v1#S5.SS2)、[Fig. 4](https://arxiv.org/html/2611.06631v1#S5.F4)、[§6](https://arxiv.org/html/2611.06631v1#S6)、[Appendix A](https://arxiv.org/html/2611.06631v1#A1)
- `abstract` — arXiv abstract page, 2611.06631v1. [https://arxiv.org/abs/2611.06631v1](https://arxiv.org/abs/2611.06631v1)
- PDF v1：[https://arxiv.org/pdf/2611.06631v1](https://arxiv.org/pdf/2611.06631v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.06631](https://doi.org/10.48550/arXiv.2611.06631)

[Home](../) · [AI Papers](./)
