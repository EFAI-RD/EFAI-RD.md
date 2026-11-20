---
parent: AI Papers
nav_exclude: true
title: "放射選擇題：五個多模態 LLM 都認得模態，病灶偵測只有 68–88%"
catalog_id: "doi:10.2196/98849"
editors:
  - "Clare"
refs:
  main:
    title: "Diagnostic Accuracy and Fine-Grained Image-Interpretation Performance of Multimodal Large Language Models on Bilingual Radiology Questions: Cross-Sectional Benchmark Study"
    url: "https://www.jmir.org/2026/1/e98849"
  doi:
    title: "DOI landing page: 10.2196/98849"
    url: "https://doi.org/10.2196/98849"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 放射選擇題：五個多模態 LLM 都認得模態，病灶偵測只有 68–88%

## 來源

- 團隊：華中科技大學同濟醫學院附屬協和醫院超聲醫學科（Union Hospital, Tongji Medical College, Huazhong University of Science and Technology）、湖北省醫學影像臨床醫學研究中心與湖北省分子影像重點實驗室；作者 Yijie Liu、Xin Zhang（共同第一作者）、Jia Xu、Manxin Huang、Yinting Xiong 與 Wenqian Wu（通訊作者）。[(ref: main author block)](https://www.jmir.org/2026/1/e98849)
- 論文：*Diagnostic Accuracy and Fine-Grained Image-Interpretation Performance of Multimodal Large Language Models on Bilingual Radiology Questions: Cross-Sectional Benchmark Study*，J Med Internet Res 2026;28:e98849，2026-11-11 出版；期刊頁標示 preprint 首次公開於 2026-04-20。[(ref: main)](https://www.jmir.org/2026/1/e98849)
- 識別碼：DOI [10.2196/98849](https://doi.org/10.2196/98849)；Europe PMC 標示為開放取用全文（PMCID PMC13754182）。
- 全文：[JMIR 期刊全文頁](https://www.jmir.org/2026/1/e98849)。
- 程式與資料：作者表示資料可向通訊作者合理索取；論文未提及程式碼釋出。作者聲明無外部經費、無利益衝突。[(ref: main Data Availability)](https://www.jmir.org/2026/1/e98849)
- 研究性質：橫斷面 benchmark 研究，不訓練模型；五個模型在 298 題上實際作答，核心分析（答案準確率、分層比較、198 題影像題的四維度推理判讀）皆已執行並附 95% CI；不是 pilot，但每題看起來只跑一次。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849)
- 證據邊界：本文數值以期刊出版版正文與 Table 1–5 為準；成對差異的 Newcombe 信賴區間、Cohen kappa、模型設定與題目出處明細放在 [Multimedia Appendix 1](https://www.jmir.org/2026/1/e98849#app1)，本文未納入引述；授權條款未納入本文引述。

**編輯：** Clare

作者用 298 題中英文放射科選擇題零樣本（zero-shot）測試五個多模態 LLM，Gemini 3 Pro 答對 89.9%，五個模型的文字題準確率都高於影像題；再拆解 198 題影像題的推理文字，模態與解剖辨識幾乎全對（99.0–100.0%），病灶偵測卻只有 68.2–88.4%。[(ref: main Table 2)](https://www.jmir.org/2026/1/e98849#table2) [(ref: main Table 5)](https://www.jmir.org/2026/1/e98849#table5)

## 流程

![左右兩欄圖。左欄由上而下四個淺藍底、深藍實線的圓角框，以三支向下箭頭相連：「1. Question pool (N=298 MCQs)：Chinese qualification exams 160; NEJM Image Challenge 71; Radiopaedia 54; BMJ EMJ 7; Asian NM Board 6; Image-based 198 / text-based 100; 2 radiologists screened」、「2. Five multimodal LLMs, zero-shot：Gemini 3 Pro, Doubao, GPT-5.2, Yuanbao (web, Dec 2025-Jan 2026); Llama 4 Maverick (Together AI endpoint, Sep 2026); New conversation per question; prompt in question's language」、「3. Final-answer accuracy：Overall, by language, question type, modality, anatomical system; Cochran Q -> exact McNemar (Holm); Wilson 95% CI」、「4. Visual reasoning (198 image items)：Modality / anatomy / lesion detection / lesion localization judged from reasoning text; 2 radiologists by consensus」；左下角小字「Redrawn by EFAI-RD from Liu Y, Zhang X, et al. J Med Internet Res 2026;28:e98849 (Methods; Tables 1, 2, 5)」。右欄為分組長條圖，標題「Table 5: visual reasoning dimensions」，縱軸「Accuracy on 198 image-based items (%)」，刻度 50–100；橫軸五個模型依序為 Gemini 3 Pro、Doubao、GPT-5.2、Llama 4 Maverick、Yuanbao，每組左為灰色 Anatomical recognition、中為藍色 Lesion localization、右為橘色 Lesion detection，長條上方標示數值：Gemini 3 Pro 100.0、95.5、88.4；Doubao 99.5、86.4、80.3；GPT-5.2 100.0、89.9、76.8；Llama 4 Maverick 99.0、86.9、71.7；Yuanbao 100.0、84.8、68.2；圖例在長條圖下方。](assets/mllm-bilingual-radiology-mcq-flow-and-visual-reasoning.png)

*圖：本書庫依論文 Methods 重繪的題庫、模型與兩層評分流程（左），以及 198 題影像題上三個推理維度的準確率（右，縱軸自 50% 起）。題數來自 [Table 1](https://www.jmir.org/2026/1/e98849#table1)，維度數值來自 [Table 5](https://www.jmir.org/2026/1/e98849#table5)；模態辨識（99.0–100.0%）未畫出。*

## 背景／問題

作者引用兩篇先前研究指出，GPT-4 系列多模態模型在放射科題目上，帶影像的題目表現低於純文字題：一篇測 ChatGPT-4o 在影像、臨床資料與選項不同組合下的表現，一篇測 GPT-4 with vision 在 ACR 住院醫師考試的文字題與影像題。[(ref: main Introduction)](https://www.jmir.org/2026/1/e98849) 這個「影像題較難」的前提有引用證據支持，本研究也在自己的題庫上重現了它。

作者要補的缺口有兩個：一是只看最後答案對錯，看不出模型是在辨認模態、認出解剖部位、找到病灶，還是在定位病灶的哪一步出錯；二是想在同一題庫上同時比較中文題與英文題，以及國際模型與中國平台（Doubao、Yuanbao）。[(ref: main Introduction)](https://www.jmir.org/2026/1/e98849) 本篇要回答的是：多模態 LLM 在放射科選擇題上的準確率，會因語言、題型、模態與解剖系統差多少；影像題答錯時，問題出在視覺判讀鏈的哪一段。

## 方法摘要

- **雙語題庫** — 298 題放射科單選題，中文 160 題來自中國衛生專業技術資格考試（放射、核醫、超聲的副高級），英文 138 題來自 NEJM Image Challenge、BMJ Emergency Medicine Journal Image Challenge、Asian Nuclear Medicine Board 樣題與 Radiopaedia 題目；198 題附影像、100 題純文字。[(ref: main Table 1)](https://www.jmir.org/2026/1/e98849#table1)
- **五個模型** — Gemini 3 Pro（Pro mode）、Doubao（Deep Thinking）、GPT-5.2（Auto mode）、Yuanbao（DeepSeek-R1＋Deep Thinking）透過官方網頁介面作答；Llama 4 Maverick 17B 128E Instruct 透過 Together AI 的固定端點以 API 作答。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849)
- **零樣本作答** — 以題目原語言提問，影像題上傳圖片並附題幹、選項與指示；網頁系統每題開新對話，使用預設參數。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849) [(ref: main Figure 2)](https://www.jmir.org/2026/1/e98849#figure2)
- **兩層評分** — 主要指標為最後答案的二元準確率；影像題另由兩位放射科醫師讀模型的推理文字，判定 modality recognition、anatomical recognition、lesion detection、lesion localization 四個二元維度。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849)
- **統計** — 五個模型整體以 Cochran Q 檢定，顯著才做 two-sided exact McNemar 事後比較並以 Holm-Bonferroni 校正；準確率附 Wilson 95% CI，同一模型內跨語言、題型、模態與系統以卡方檢定比較。[(ref: main Statistical Analysis)](https://www.jmir.org/2026/1/e98849)

## 方法詳解

- **題目篩選** — 兩位執業超過 5 年的放射科醫師獨立篩選與審閱全部題目：題幹完整、至少四個選項且只有一個確定答案；影像題須為單一模態、清晰可診斷。排除非放射影像（例如大體病理）、影片或動態影像，以及混合模態的題目；輸入前也檢查題目與影像沒有病人識別資訊。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849)
- **分類標註** — 每題標上模態（CT、X 光、MRI、超音波、核醫）與解剖系統（神經、呼吸、心血管、消化、泌尿生殖、肌肉骨骼），作為分層分析的依據。[(ref: main Table 1)](https://www.jmir.org/2026/1/e98849#table1)
- **模型挑選與時間** — 四個商用系統依 2025 年 11 月時的視覺能力與市場地位挑選，不具影像輸入的模型排除；四者在 2025-12-14 至 2026-01-31 間測試。Llama 4 Maverick 在 2026 年 9 月另以獨立 API 請求測試，作者把它當作可重現的開放權重錨點。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849)
- **提示** — 正文給出的提示範例只有一句要求選出正確答案的指令，另以 Figure 2 截圖示範 Gemini 3 Pro 回答一題英文影像題與一題英文文字題。[(ref: main Figure 2)](https://www.jmir.org/2026/1/e98849#figure2)
- **四維度判讀** — 四個維度都由推理文字判定，不是讓模型畫框或輸出座標；兩位放射科醫師共同審閱、取得共識後只記錄共識結果。為檢查一致性，另由兩位醫師各自盲評隨機抽出的 40 題影像題（約 198 題的 20%）在五個模型上的 200 份回答。[(ref: main Methods)](https://www.jmir.org/2026/1/e98849)
- **完整性** — 298 題在五個模型上都得到有效回答，沒有缺漏或補值。[(ref: main Statistical Analysis)](https://www.jmir.org/2026/1/e98849)
- **論文未交代** — 標準答案如何確定（沿用題源答案，或另經醫師核對）。
- **論文未交代** — 每題重跑次數；正文只說每題獨立作答、每題開新對話，沒有描述重複作答或取平均。
- **論文未交代** — 網頁系統的 temperature 等解碼設定（只寫使用預設參數）；Llama 4 Maverick 的解碼設定正文未列，作者指向附錄 Table S3。
- **論文未交代** — 完整提示文字與中文提示的措辭，正文只有一句英文範例。

## 資料與實驗

### 資料

| 分類 | 子類 | 題數 (%) |
|---|---|---|
| 題型 | 影像題 | 198 (66.4) |
| 題型 | 文字題 | 100 (33.6) |
| 語言 | 中文 | 160 (53.7) |
| 語言 | 英文 | 138 (46.3) |
| 模態 | CT | 71 (23.8) |
| 模態 | X 光（radiography） | 65 (21.8) |
| 模態 | MRI | 60 (20.1) |
| 模態 | 超音波 | 53 (17.8) |
| 模態 | 核醫（NM） | 49 (16.4) |
| 解剖系統 | 神經 | 56 (18.8) |
| 解剖系統 | 消化 | 61 (20.5) |
| 解剖系統 | 心血管 | 49 (16.4) |
| 解剖系統 | 呼吸 | 49 (16.4) |
| 解剖系統 | 肌肉骨骼 | 44 (14.8) |
| 解剖系統 | 泌尿生殖 | 39 (13.1) |
| 來源 | 中國衛生專業技術資格考試 | 160 (53.7) |
| 來源 | NEJM Image Challenge | 71 (23.8) |
| 來源 | Radiopaedia MCQs | 54 (18.1) |
| 來源 | BMJ EMJ Image Challenge | 7 (2.4) |
| 來源 | Asian Nuclear Medicine Board 樣題 | 6 (2.0) |

*資料：[Table 1](https://www.jmir.org/2026/1/e98849#table1)，N=298。*

### 實驗

**答案準確率（%，括號為 Wilson 95% CI）** [(ref: main Table 2)](https://www.jmir.org/2026/1/e98849#table2)

| 子群（N） | Yuanbao | Doubao | GPT-5.2 | Gemini 3 Pro | Llama 4 Maverick | 整體 P |
|---|---|---|---|---|---|---|
| 中文（160） | 66.9 (59.3–73.7) | 76.9 (69.8–82.7) | 68.1 (60.6–74.8) | 86.9 (80.8–91.3) | 66.9 (59.3–73.7) | <.001 |
| 英文（138） | 79.0 (71.4–85.0) | 81.2 (73.8–86.8) | 89.9 (83.7–93.9) | 93.5 (88.1–96.5) | 79.0 (71.4–85.0) | <.001 |
| 影像題（198） | 63.6 (56.7–70.0) | 74.7 (68.3–80.3) | 71.7 (65.1–77.5) | 85.9 (80.3–90.0) | 66.2 (59.3–72.4) | <.001 |
| 文字題（100） | 90.0 (82.6–94.5) | 87.0 (79.0–92.2) | 91.0 (83.8–95.2) | 98.0 (93.0–99.4) | 85.0 (76.7–90.7) | .002 |
| 全部（298） | 72.5 (67.2–77.2) | 78.9 (73.9–83.1) | 78.2 (73.2–82.5) | 89.9 (86.0–92.9) | 72.5 (67.2–77.2) | <.001 |

**影像題推理四維度準確率（%，n=198，括號為 Wilson 95% CI）** [(ref: main Table 5)](https://www.jmir.org/2026/1/e98849#table5)

| 維度 | Yuanbao | Doubao | GPT-5.2 | Gemini 3 Pro | Llama 4 Maverick | P |
|---|---|---|---|---|---|---|
| Modality recognition | 100.0 (98.1–100.0) | 99.5 (97.2–99.9) | 100.0 (98.1–100.0) | 100.0 (98.1–100.0) | 99.5 (97.2–99.9) | .56 |
| Anatomical recognition | 100.0 (98.1–100.0) | 99.5 (97.2–99.9) | 100.0 (98.1–100.0) | 100.0 (98.1–100.0) | 99.0 (96.4–99.7) | .25 |
| Lesion detection | 68.2 (61.4–74.3) | 80.3 (74.2–85.2) | 76.8 (70.4–82.1) | 88.4 (83.2–92.1) | 71.7 (65.1–77.5) | <.001 |
| Lesion localization | 84.8 (79.2–89.2) | 86.4 (80.9–90.5) | 89.9 (84.9–93.4) | 95.5 (91.6–97.6) | 86.9 (81.5–90.9) | <.001 |

依模態（[Table 3](https://www.jmir.org/2026/1/e98849#table3)）與解剖系統（[Table 4](https://www.jmir.org/2026/1/e98849#table4)）的分層結果在下一節以文字摘錄。

## 結果

- **整體** — Gemini 3 Pro 答對 268/298（89.9%，95% CI 86.0–92.9%），顯著高於 Doubao 235/298（78.9%）、GPT-5.2 233/298（78.2%）、Yuanbao 與 Llama 4 Maverick 各 216/298（72.5%），四者兩兩之間沒有顯著差異。[(ref: main Table 2)](https://www.jmir.org/2026/1/e98849#table2)
- **文字題高於影像題** — 五個模型都是文字題較高，模型內比較皆顯著（Yuanbao、GPT-5.2、Llama 4 Maverick P<.001，Gemini 3 Pro P=.002，Doubao P=.02）；Gemini 3 Pro 為 98.0% 對 85.9%，Yuanbao 為 90.0% 對 63.6%。[(ref: main Table 2)](https://www.jmir.org/2026/1/e98849#table2)
- **英文題較高的有三個** — GPT-5.2（P<.001）、Llama 4 Maverick 與 Yuanbao（皆 P=.03）英文題顯著較高；GPT-5.2 中文 68.1%、英文 89.9%。中文題上 Gemini 3 Pro 與 Doubao 沒有顯著差異（86.9% 對 76.9%）。[(ref: main Table 2)](https://www.jmir.org/2026/1/e98849#table2)
- **模態** — 各模型在各模態的準確率落在 66.2–91.7%；影像題 CT 子集 Gemini 3 Pro 44/51、Yuanbao 29/51（P<.001），X 光影像題 Doubao 與 Gemini 3 Pro 各 38/44、Llama 4 Maverick 26/44（皆 P=.04）。文字題按模態分層後，五個模型之間都沒有顯著差異。[(ref: main Table 3)](https://www.jmir.org/2026/1/e98849#table3)
- **解剖系統** — 各模型在各系統落在 65.3–95.9%；呼吸系統 Gemini 3 Pro 47/49（95.9%），Yuanbao 35/49（71.4%）、Llama 4 Maverick 34/49（69.4%）。同一模型跨模態、跨系統的卡方檢定都不顯著（例如 Gemini 3 Pro 跨模態 P=.96）。[(ref: main Table 4)](https://www.jmir.org/2026/1/e98849#table4)
- **影像判讀鏈** — 模態與解剖辨識五個模型都在 99.0–100.0%，模型間無差異（P=.56、.25）；到病灶偵測降為 68.2–88.4%，定位為 84.8–95.5%，兩者模型間都有顯著差異（P<.001）。Gemini 3 Pro 偵測 175/198，Yuanbao 135/198。[(ref: main Table 5)](https://www.jmir.org/2026/1/e98849#table5)
- **評分一致性** — 兩位醫師在 40 題、200 份回答上的四維度觀察一致率為 97.5–99.5%，PABAK 0.95–0.99。[(ref: main Results)](https://www.jmir.org/2026/1/e98849)

## 限制

作者列出的限制：

- **樣本** — 298 題，部分模態與解剖系統子群很小，精確度與外推性有限。
- **污染** — 題目來自歷年考題與公開教學資源，無法排除進入過模型訓練資料；抽查時部分公開題目可在網路上找到逐字或近乎逐字的版本，各模型接觸程度可能不同。
- **影像的獨立貢獻** — 影像題也含文字題幹，研究沒有做拿掉影像的輸入消融，無法分離影像本身的貢獻。
- **提示** — 只用標準化零樣本提示，未評估最佳化提示。
- **時間點** — 四個網頁系統會被廠商更新，Llama 4 Maverick 於 2026 年 9 月才測（其他四個在 2025-12 至 2026-01），結果是有時間戳的 benchmark。[(ref: main Limitations)](https://www.jmir.org/2026/1/e98849)

本書庫另外注意到：

- **四維度只讀推理文字** — 病灶偵測與定位是醫師從模型自述判定，不是對照影像上的框或座標；模型寫對位置不等於它在影像上看到了同一處。
- **沒有人類對照** — 放射科醫師只負責篩題與評分，沒有作答基準，論文無法說明這些準確率相對於住院醫師或專科醫師的位置。
- **正文與表格不一致** — Discussion 寫呼吸系統是校正後唯一仍有成對差異的子群，但 Table 3 對 CT、X 光與超音波也標示了經 Holm 校正後仍顯著的 Gemini 3 Pro 比較，讀者應以表格為準。[(ref: main Table 3)](https://www.jmir.org/2026/1/e98849#table3)
- **網頁介面作答** — 四個商用系統的推理模式與預設參數由平台決定，同名模型日後重測未必得到相同結果。

## 與書庫其他文章的關係

氣胸稽核在 prevalence-matched 是非題上發現兩個開放醫療 VLM 對 432 張氣胸陽性全答「沒有」；本篇改用中英文放射選擇題測五個通用多模態 LLM，從推理文字看到模態與解剖幾乎全對、病灶偵測才開始掉分，兩篇都指出整體分數會遮住病灶層級的失效: [胸片 VLM 稽核：兩個模型對 432 例氣胸全答「沒有」](2026-11-16-pneumothorax-silent-failure-medical-vlm.md)

轉診文字研究固定 MRI、逐級改寫文字，量到多模態 LLM 的答案主要跟著文字走；本篇的影像題同樣附有題幹文字、也沒有做拿掉影像的消融，因此影像題與文字題的差距不能直接解讀成模型「看懂影像」的程度: [轉診單一句話就改變 MRI 判讀，叫模型忽略只有一個做得到](2026-10-28-referral-text-overrides-mri-mllm-glioma-abscess.md)

## 實務的啟發

- **拆解判讀鏈是可借用的量測方法** — 把影像題的對錯拆成模態、解剖、病灶偵測、病灶定位四段，比單看最後答案更能指出模型卡在哪一步；做多模態模型內部評估時，可以沿用這種分段記錄，但最好同時要求模型輸出可對照影像的位置，而不只靠自述。
- **語言要分開報** — 同一模型中英文題可差到 20 個百分點以上（GPT-5.2 為 68.1% 對 89.9%），以英文 benchmark 選型後要用於中文臨床情境，需另做中文題的驗證。
- **影像題低於文字題是待驗證的警訊** — 本研究沒有拿掉影像的消融、題目可能已在訓練資料中，且沒有人類基準；這些分數只能當作考試型題目上的相對比較，不能推論到臨床判讀表現。作者自己也認為臨床導入前需要獨立的臨床驗證。[(ref: main Conclusions)](https://www.jmir.org/2026/1/e98849)

## References

- `main` — Liu Y, Zhang X, Xu J, Huang M, Xiong Y, Wu W. *Diagnostic Accuracy and Fine-Grained Image-Interpretation Performance of Multimodal Large Language Models on Bilingual Radiology Questions: Cross-Sectional Benchmark Study*. J Med Internet Res. 2026;28:e98849. [https://www.jmir.org/2026/1/e98849](https://www.jmir.org/2026/1/e98849)
  - 深鏈：[Table 1](https://www.jmir.org/2026/1/e98849#table1)、[Table 2](https://www.jmir.org/2026/1/e98849#table2)、[Table 3](https://www.jmir.org/2026/1/e98849#table3)、[Table 4](https://www.jmir.org/2026/1/e98849#table4)、[Table 5](https://www.jmir.org/2026/1/e98849#table5)、[Figure 1](https://www.jmir.org/2026/1/e98849#figure1)、[Figure 2](https://www.jmir.org/2026/1/e98849#figure2)、[Multimedia Appendix 1](https://www.jmir.org/2026/1/e98849#app1)
- `doi` — DOI landing page. [https://doi.org/10.2196/98849](https://doi.org/10.2196/98849)

[Home](../) · [AI Papers](./)
