---
parent: AI Papers
nav_order: 2
title: "病理多視野診斷：選項輪換十次全對，開放 MLLM 最高 17.9%"
catalog_id: "arxiv:2611.15325"
editors:
  - "Clare"
refs:
  main:
    title: "CaseScope: A Multi-Field Benchmark for Case-Level Pathology Diagnosis with Multimodal LLMs"
    url: "https://arxiv.org/abs/2611.15325"
  html:
    title: "CaseScope (arXiv HTML v1)"
    url: "https://arxiv.org/html/2611.15325v1"
  code:
    title: "CaseScope evaluation code (GitHub)"
    url: "https://github.com/Wenchuan-Zhang/CaseScope"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 病理多視野診斷：選項輪換十次全對，開放 MLLM 最高 17.9%

## 來源

- 團隊：四川大學華西醫院病理科與臨床病理研究所、四川大學計算機學院、中國醫科大學附屬盛京醫院病理科、武漢大學人民醫院病理科；作者 Wenchuan Zhang、Chengyang Zhang、Fengling Li（共同第一作者）、Ting Yin、Chen Shu、Jie Chen、Shuwan Zhang、Xiaoyan Wu、Zhang Zhang、Yuhao Yi（通訊作者）、Jiancheng Lv、Hong Bu。[(ref: main author block)](https://arxiv.org/html/2611.15325v1)
- 論文：*CaseScope: A Multi-Field Benchmark for Case-Level Pathology Diagnosis with Multimodal LLMs*，arXiv 預印本，2026-11-11 提交（v1），分類 cs.CV。[(ref: main)](https://arxiv.org/abs/2611.15325)
- 識別碼：arXiv [2611.15325](https://arxiv.org/abs/2611.15325)；DOI [10.48550/arXiv.2611.15325](https://doi.org/10.48550/arXiv.2611.15325)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.15325v1)。
- 程式：評估程式碼公開於 [GitHub](https://github.com/Wenchuan-Zhang/CaseScope)（MIT License）；論文未明寫病理影像本身是否公開。
- 研究性質：完整的 benchmark 研究，不訓練模型；32 個多模態大型語言模型（multimodal large language model，MLLM）實際作答，主表附 case-level bootstrap 95% 信賴區間，另有 8 位讀者的人類對照；不是 pilot，但每個模型在每種選項順序下只以 greedy decoding 跑一次。[(ref: main §4)](https://arxiv.org/html/2611.15325v1#S4) [(ref: main §5.1)](https://arxiv.org/html/2611.15325v1#S5.SS1)
- 證據邊界：本文數值以 arXiv v1 正文、Table 2、Table 3 與補充材料 Table S5 為準；完整 28 個開放模型的逐模型數值與信賴區間在 Table S6／S7，本文未逐列引述。

**編輯：** Clare

作者把一份住院醫師教學圖庫與 88 本已出版圖譜改造成「同一病灶多個 H&E 視野」的病理診斷 benchmark，測 28 個開放與 4 個專有 MLLM：十選一診斷單次作答時開放模型最高 50.6%，但要求十種選項順序都答對後只剩 17.9%（最佳專有模型 78.3% → 61.7%），而且在教學個案上，拿掉一行檢體部位比少給幾個視野更影響答案。[(ref: main Abstract)](https://arxiv.org/abs/2611.15325) [(ref: main Table 3)](https://arxiv.org/html/2611.15325v1#S5.T3)

## 流程

![左右兩欄圖。左欄由上而下四個淺藍底、深藍實線的圓角框，以三支向下箭頭相連：「1. Two sources：Teaching: residency library, 436 cases, 2,448 H&E fields (median 5); Atlas: 88 published atlases, 800 cases, 2,664 fields (median 3); 843 entities, 18 organ systems」、「2. Curation：De-duplication; field order low -> high power (76 fixed); WHO-aligned ontology; LLM pre-review flags 64 cases, pathologist re-examines flagged cases」、「3. Six tasks, 4,679 items：A1 open diagnosis (HDS); A2 10-way MCQ; B behaviour; C grading; R1 finding T/F; G1 finding location (Atlas); CircularEval: correct under every option rotation」、「4. 32 MLLMs：28 open (general, medical, pathology) + 4 proprietary; open: vLLM, greedy; field-set and site ablations (open); reader study: 8 readers (residents, attendings), 120 cases」；左下角小字「Redrawn by EFAI-RD from Zhang W, et al. arXiv:2611.15325v1 (Sec. 3-5, Sec. S9; Tables 2-3)」。右欄為分組長條圖，標題「Table 3: A2 single-pass vs. circular accuracy」，縱軸「CaseScope-Teaching, ten-way diagnosis (%)」，刻度 0–100；一條灰色直線把左側「Proprietary」四組與右側「Open (selected from Table 3)」四組分開；每組左為灰色 Single-pass accuracy (A2v)、右為橘色 All 10 rotations correct (A2, CircularEval)，長條上方標示數值：Claude Sonnet 5.5 78.3、61.7；GPT-5.6-sol 67.4、49.3；Claude Haiku 5.5 61.0、39.0；GPT-5.6-luna 57.3、31.9；Qwen3.5-9B 50.6、17.9；ScaleReasoner-R1 41.8、10.8；Hulu-Med-7B 41.2、13.3；Patho-R1-7B 36.2、7.1；10% 處有一條深灰色虛線，右端標「chance 10%」；圖例在長條圖下方。](assets/casescope-pipeline-and-circular-accuracy.png)

*圖：本書庫依論文 §3–§5 與 Sec. S9 重繪的資料建構、任務與評估流程（左），以及 CaseScope-Teaching 十選一診斷的單次準確率與十種選項順序全對比例（右）。數值來自 [Table 3](https://arxiv.org/html/2611.15325v1#S5.T3)，開放模型只挑出表中四個；其餘 24 個開放模型的數值在 Table S6。*

## 背景／問題

作者描述的病理判讀方式是：先在低倍看組織架構（邊界、浸潤、生長模式），再到高倍看細胞學（核大小、染色質、分裂），在不同視野之間來回直到證據一致；住院醫師的訓練與考試也是給同一病灶由低到高倍的多張視野。[(ref: main §1)](https://arxiv.org/html/2611.15325v1#S1) 這是作者對實務的描述，論文沒有另外引用研究量化它。

作者引用既有文獻指出，現有病理 VQA benchmark 多半只問一張圖，全切片（whole-slide image，WSI）benchmark 多在測切片編碼器或導航代理，少數跨尺度 benchmark 只取單一公開 cohort（TCGA）癌症切片的巢狀區域，題目由 LLM 生成。[(ref: main §1)](https://arxiv.org/html/2611.15325v1#S1) [(ref: main Table 1)](https://arxiv.org/html/2611.15325v1#S2.T1) 本篇要回答的是：給 MLLM 已經挑好的多張視野（因此失敗不能歸咎於找錯區域），它能不能整合成一個穩定的診斷；它的答案究竟靠影像、靠多出來的視野，還是靠題目裡的檢體部位。

## 方法摘要

- **兩個來源** — CaseScope-Teaching 來自住院醫師教學圖庫，436 例、2,448 張 H&E 視野（每例中位數 5 張，最多給模型 8 張）；CaseScope-Atlas 來自 88 本已出版病理圖譜，800 例、2,664 張視野（中位數 3）。兩者合計 843 個 entity、18 個器官系統。[(ref: main §1)](https://arxiv.org/html/2611.15325v1#S1) [(ref: main §3.6)](https://arxiv.org/html/2611.15325v1#S3.SS6)
- **六個任務** — A1 開放式診斷、A2 十選一診斷、B 生物行為分流（非腫瘤／良性／中間型／惡性）、C 分級、R1 形態學敘述的是非判斷、G1 找出某個描述出現在哪張視野（僅 Atlas）；兩個來源合計 4,679 題。[(ref: main Table 2)](https://arxiv.org/html/2611.15325v1#S4.T2)
- **難的干擾選項** — A2 的九個干擾選項依 ontology 優先序抽取，每個 entity 的經典鑑別對象（classic look-alike）只要規則允許就一定放進去；同義詞、上下位、同形態不同部位與 H&E 分不開的配對則排除。[(ref: main §4)](https://arxiv.org/html/2611.15325v1#S4) [(ref: main Sec. S8)](https://arxiv.org/html/2611.15325v1#S8)
- **CircularEval** — 每道選擇題依選項輪換重問（A2 十次、B 四次、C 二到四次、G1 每張視野一次），所有輪換都答對才算對；同時報單次（vanilla）準確率。[(ref: main §4)](https://arxiv.org/html/2611.15325v1#S4)
- **輸入消融與人類對照** — 對開放模型重跑 A2：只給最高倍視野，或拿掉一行檢體部位；R1 另讓每個模型只讀文字作答，量影像帶來的增益。另有 8 位讀者（住院醫師第 1–3 年與主治醫師各 2 位）在 120 例上作答。[(ref: main §5.3)](https://arxiv.org/html/2611.15325v1#S5.SS3) [(ref: main Sec. S9)](https://arxiv.org/html/2611.15325v1#S9)

## 方法詳解

- **教學圖庫的重建** — 原始圖庫 3,291 個檔案只有 2,586 個不同檔案，因為同一例常被歸在多個器官系統、名稱也不同；作者以檔案雜湊、感知雜湊與病理 CLIP 相似度（再以像素層級確認）找出所有複本，剩 2,512 張不同影像、合併成 453 例，排除非 H&E 影像、保留至少兩張 H&E 視野的 436 例。[(ref: main §3.2)](https://arxiv.org/html/2611.15325v1#S3.SS2)
- **視野順序** — 每題都告訴模型視野由低倍到高倍排列；作者以零樣本病理 CLIP 的倍率分數加上原始拍攝順序排序，再由一位病理醫師逐例檢查，改正 76 例（17%）。[(ref: main §3.2)](https://arxiv.org/html/2611.15325v1#S3.SS2)
- **標籤 ontology** — 圖庫標籤混用不同 WHO 版本與命名，作者對應到 407 個與 WHO Classification of Tumours 第 5 版對齊的 canonical entity（非腫瘤疾病用教科書術語），每個 entity 記錄同義詞、behaviour、lineage、family，以及是否單靠 H&E 可診斷（Y／P／N）。436 例中 400 例在提示中給檢體部位。[(ref: main §3.3)](https://arxiv.org/html/2611.15325v1#S3.SS3)
- **標籤品質控制** — 教學個案的標籤是圖庫老師歸檔時的診斷；一個多模態 LLM agent（DeepSeek-V4.1-Flash）預先審閱每一例與每道 A2 題，標出 64 例（14.7%）與 7 題，但不改任何東西；一位主治以上病理醫師逐一複核被標出的個案與題目，其餘 372 例沿用圖庫標籤。[(ref: main §3.4)](https://arxiv.org/html/2611.15325v1#S3.SS4) [(ref: main Sec. S9)](https://arxiv.org/html/2611.15325v1#S9)
- **Atlas 標籤** — 每例由兩個開放 LLM（Qwen2.5-32B、Qwen3.5-9B）從圖說對應到 ontology，兩者一致才收；再由 LLM 閱讀圖說、標籤與部位，替換 126 例、修正 128 例的部位或名稱，最後由病理醫師確認標籤。387 例是共用同一圖說的同一病灶，413 例是同一章節內同一 entity 的連續圖（提示會說明是哪一種）。[(ref: main §3.6)](https://arxiv.org/html/2611.15325v1#S3.SS6)
- **A1 評分** — 模型以 JSON 回傳一個診斷、兩個鑑別診斷與信心值；hierarchical diagnostic score（HDS）對參考 entity、同義詞或可接受替代給 1 分，同 family 其他 entity 給 0.5 分，其餘 0 分；每題取開放權重 LLM judge（Qwen2.5-32B-Instruct, AWQ）與確定性 ontology 比對兩者中的較高分。對 297 份回答的病理醫師盲評，完全一致 80.5%、quadratic-weighted κ 0.76（judge 單獨 0.73），平均分 0.32 對 0.49，作者據此說 A1 分數偏嚴。[(ref: main §4)](https://arxiv.org/html/2611.15325v1#S4) [(ref: main Sec. S9)](https://arxiv.org/html/2611.15325v1#S9)
- **R1 的敘述從哪來** — 195 例（全部 194 個單靠 H&E 可診斷的個案加上一例示範）各有低倍與高倍兩題、每題四句敘述，兩真兩假：真句是該 entity 的必要條件，假句是鑑別對象的定義特徵。敘述由 LLM（DeepSeek-V4.1-Flash）依標籤與 WHO 準則生成、病理醫師審閱；因此真假值由專家標籤推得，不是由逐張影像標註得來。[(ref: main §4)](https://arxiv.org/html/2611.15325v1#S4)
- **推論設定** — 開放模型以 vLLM、greedy decoding、最多 1,024 個新 token（推理模型 4,096）；單圖模型（LLaVA-Med、Quilt-LLaVA、PathGen-LLaVA）收到拼成一張的編號拼貼。推理模型在上限內還沒答完時，作者附上停止思考的指令強制作答，這在八個模型的預設執行中共 14,623 份回答，Qwen3.5-9B 佔其回答的 34.7%。[(ref: main §5.1)](https://arxiv.org/html/2611.15325v1#S5.SS1) [(ref: main Sec. S10)](https://arxiv.org/html/2611.15325v1#S10)
- **提示** — 單一使用者回合、無 system prompt，每張視野前標 `Image i:`，最後接題目、選項與作答指令；各任務的完整提示列在補充材料。[(ref: main Sec. S6)](https://arxiv.org/html/2611.15325v1#S6a)
- **論文未交代** — 病理影像與題目檔是否公開及其授權；正文只寫評估程式碼公開，提示一節提到「released task files」但未說明影像如何取得。
- **論文未交代** — 四個專有模型的 API 版本、推理設定與解碼參數；推論設定的描述集中在開放模型。
- **論文未交代** — 病理醫師審閱 R1 敘述時改了多少句；也沒有說明教學圖庫使用的倫理審查或資料使用許可。
- **論文未交代** — 重複執行：每個模型在每種選項順序下只跑一次 greedy decoding，主表的信賴區間來自重抽個案，不反映模型輸出本身的變異。

## 資料與實驗

### 資料

| 項目 | CaseScope-Teaching | CaseScope-Atlas |
|---|---|---|
| 來源 | 住院醫師教學圖庫（四位病理醫師自同一 WSI 選視野） | 88 本已出版病理圖譜 |
| 個案數 | 436 | 800 |
| H&E 視野數（中位數） | 2,448（5） | 2,664（3） |
| 惡性／中間型／良性／非腫瘤 | 165／61／96／114 | 293／107／190／210 |
| 標籤來源 | 圖庫歸檔診斷對應 ontology；LLM 預審標出的 64 例由病理醫師複核 | 兩個 LLM 從圖說對應且須一致，病理醫師確認 |
| A1 開放式診斷 | 436 | 800 |
| A2 十選一（chance 10%） | 436 | 800 |
| B 行為分流，四選一（25%） | 380 | 762 |
| C 分級，二到四選一（1/n） | 44 | – |
| R1 敘述是非（50%） | 390 | 195 |
| G1 找視野，二到八選一（1/n） | – | 436 |
| 題數合計 | 1,686 | 2,993 |

*資料：個案組成見 [§3.5](https://arxiv.org/html/2611.15325v1#S3.SS5) 與 [§3.6](https://arxiv.org/html/2611.15325v1#S3.SS6)；任務題數為選項輪換前的題數，見 [Table 2](https://arxiv.org/html/2611.15325v1#S4.T2)。*

### 實驗

**CaseScope-Teaching 主要結果（%，節錄）** [(ref: main Table 3)](https://arxiv.org/html/2611.15325v1#S5.T3)

| 模型 | A1 | A2 | A2v | B | Miss ↓ | C | C κ | R1 | Δimg |
|---|---|---|---|---|---|---|---|---|---|
| Random choice | – | 0.0 | 10.1 | 0.5 | 49.7 | 11.4 | 0.08 | – | – |
| Claude Sonnet 5.5 | 64.2 | 61.7 | 78.3 | 75.5 | 11.4 | 79.5 | 0.81 | 93.2 | +10.2∗ |
| Claude Haiku 5.5 | 43.9 | 39.0 | 61.0 | 57.4 | 10.3 | 54.5 | 0.55 | 83.2 | +19.5∗ |
| GPT-5.6-sol | 43.5 | 49.3 | 67.4 | 55.5 | 19.4 | 61.4 | 0.64 | 92.9 | +12.6∗ |
| GPT-5.6-luna | 33.5 | 31.9 | 57.3 | 51.1 | 33.6 | 56.8 | 0.61 | 87.1 | +15.4∗ |
| Qwen3.5-9B | 29.7 | 17.9 | 50.6 | 31.8 | 45.1 | 36.4 | 0.42 | 81.5 | +16.3∗ |
| InternVL3.5-8B | 18.3 | 11.0 | 34.7 | 30.5 | 15.0 | 27.3 | 0.16 | 66.5 | +3.4∗ |
| Lingshu-7B | 21.0 | 5.7 | 33.6 | 34.2 | 35.4 | 36.4 | 0.32 | 57.8 | +2.4∗ |
| MedGemma-1.5-4B | 11.5 | 2.5 | 21.5 | 18.9 | 15.2 | 20.5 | 0.15 | 51.7 | +0.6 |
| Hulu-Med-7B | 17.3 | 13.3 | 41.2 | 33.4 | 19.7 | 13.6 | 0.28 | 63.3 | +4.9∗ |
| Quilt-LLaVA-7B† | 3.8 | 1.6 | 17.7 | 1.1 | 40.0 | 2.3 | −0.08 | 49.4 | +3.4∗ |
| Patho-R1-7B | 34.7 | 7.1 | 36.2 | 33.2 | 11.1 | 29.5 | 0.28 | 36.1 | +8.5∗ |
| ScaleReasoner-R1 | 32.5 | 10.8 | 41.8 | 34.5 | 6.1 | 25.0 | 0.33 | 29.2 | −2.0 |

*A1 為 HDS；A2、B、C 為 CircularEval，A2v 為單次準確率；Miss 為 critical miss rate（惡性或原位病灶被判為良性或非腫瘤）；C κ 為 quadratic weighted κ；Δimg 為 R1 有影像減無影像（∗ 表 95% 配對 bootstrap 區間不含 0）；† 為單圖模型、收到視野拼貼。論文註明 95% 半寬在 Teaching 最多 4.8 個百分點。本表只節錄 Table 3 的 13 列與 Teaching 欄位，Atlas 欄位見原表。*

**人類讀者與模型在同一 120 例上的比較（%）** [(ref: main Table S5)](https://arxiv.org/html/2611.15325v1#S9.T5)

| 讀者／模型 | A2 個別讀者 1 / 2 | A2 | A1 exact |
|---|---|---|---|
| 住院醫師第 1 年 | 56.7 / 63.3 | 60.0 | 40.0 |
| 住院醫師第 2 年 | 66.7 / 70.8 | 68.8 | 52.5 |
| 住院醫師第 3 年 | 75.8 / 80.0 | 77.9 | 65.0 |
| 主治醫師 | 84.2 / 88.3 | 86.3 | 77.5 |
| Claude Sonnet 5.5 | – | 77.5 | 67.5 |
| Claude Haiku 5.5 | – | 61.7 | 46.7 |
| GPT-5.6-sol | – | 75.8 | 42.5 |
| GPT-5.6-luna | – | 62.5 | 39.2 |
| Qwen3.5-9B | – | 53.3 | 27.5 |
| Patho-R1-7B | – | 37.5 | 36.7 |

*A2 為單次作答準確率（模型只用第 0 種選項順序，與讀者看到的相同）；A1 為完全命中的診斷準確率。讀者先寫開放式診斷，才看到十個選項。*

## 結果

- **單次作答高估穩定性** — Teaching 上十選一單次準確率，開放模型 9.8–50.6%、專有模型 57.3–78.3%；要求十種選項順序都答對後，分別剩 0.0–17.9% 與 31.9–61.7%。28 個開放模型中，十次輪換都給出同一個診斷的個案只有 0.2–21.8%。[(ref: main §5.2)](https://arxiv.org/html/2611.15325v1#S5.SS2)
- **開放式診斷同樣有落差** — A1 的 HDS 開放模型 3.8–34.7、專有模型 33.5–64.2；完全說中 entity 的比例為 2.1–30.0% 與 30.3–60.6%，開放模型有 21.6–54.1% 的答案連 behaviour 都錯。開放模型中 A1 領先的是病理推理模型（Patho-R1-7B 34.7、ScaleReasoner-R1 32.5），但它們在 A2 輪換後並沒有比通用模型穩定。[(ref: main §5.2)](https://arxiv.org/html/2611.15325v1#S5.SS2)
- **分流兩個方向都會錯** — 開放模型把惡性或原位病灶判成良性或非腫瘤的比例為 3.3–52.4%（專有 10.3–33.6%）；最低的 Qwen2-VL-7B 只漏 3.3%，原因是它把 89.9% 的良性與非腫瘤個案判為惡性或交界性。[(ref: main §5.2)](https://arxiv.org/html/2611.15325v1#S5.SS2)
- **錯答偏向經典鑑別對象** — 178 例的干擾選項中含經典鑑別對象；開放模型答錯時有 26.6% 選中它（各模型 18.5–37.7%），若平均分散到干擾選項應為 14.7%；專有模型為 33.2–45.1%。[(ref: main §5.4)](https://arxiv.org/html/2611.15325v1#S5.SS4)
- **教學個案上檢體部位比視野重要** — 開放模型只給最高倍視野時，A2 輪換準確率變動 −7.1 到 +2.1 點（6 個顯著下降、1 個顯著上升）；拿掉一行檢體部位則 28 個中 25 個下降，最多降 9.4 點。[(ref: main §5.3)](https://arxiv.org/html/2611.15325v1#S5.SS3) [(ref: main Figure 4)](https://arxiv.org/html/2611.15325v1#S5.F4)
- **形態學敘述多半接近猜** — R1 開放模型判對的敘述中位數 62.0%（最高 81.5%，chance 50%），一題四句全對的比例沒有超過 54.4%；影像相對純文字只帶來中位數 +3.4 點（最高 +16.3）。專有模型判對 83.2–93.2%，影像帶來 +10.2 到 +19.5 點，純文字已有 63.7–83.0%。[(ref: main §5.2)](https://arxiv.org/html/2611.15325v1#S5.SS2) [(ref: main §5.3)](https://arxiv.org/html/2611.15325v1#S5.SS3)
- **Atlas 重現排名、不重現水準** — 兩個來源的 A2 排名 Spearman ρ 0.83（95% CI 0.59–0.96，32 個模型），A1 為 0.80，只看開放模型則 0.74。在兩邊都有的 347 個 entity 上，專有模型 Atlas 比 Teaching 低 13.0 點（A2）與 11.5 點（A1），開放模型 +0.9 與 −1.1；critical miss 在 Atlas 更高（專有平均 32.2% 對 18.6%）。[(ref: main §5.5)](https://arxiv.org/html/2611.15325v1#S5.SS5)
- **Atlas 上視野與部位一樣重要** — 只看三張以上視野的個案，最高倍視野單獨給時 A2 變動 −2.2 點（Atlas）對 −1.0 點（Teaching），拿掉部位為 −2.9 對 −4.7；作者因此說「部位比視野重要」只在教學個案上成立。[(ref: main §5.5)](https://arxiv.org/html/2611.15325v1#S5.SS5)
- **人類對照** — 同一 120 例上，主治醫師單次十選一平均 86.3%、第 3 年住院醫師 77.9%；最佳模型 Claude Sonnet 5.5 為 77.5%，開放模型 Qwen3.5-9B 為 53.3%。[(ref: main Table S5)](https://arxiv.org/html/2611.15325v1#S9.T5)

## 限制

作者列出的限制：

- **挑過的視野** — 教學個案與圖譜的視野都是為了示範某個 entity 而挑，比病理醫師在未經挑選的切片上要找的區域容易；CaseScope 量的是教科書層級的跨視野推理，作者稱之為臨床使用的必要但非充分條件。
- **每個 entity 多半只有一例** — 因此結果按器官系統、behaviour 與任務報告，不報逐 entity 的表現。
- **協定本身** — 視野順序固定且已告知，沒有測模型自己挑視野；只給 H&E 與部位；R1 的真假由標籤（Teaching）或圖說（Atlas）推得，不是由影像區域標註。
- **污染** — 在 228,899 張公開病理影像中沒有找到近似重複，但整張影像比對抓不到被裁切後刊出的版本。[(ref: main §6)](https://arxiv.org/html/2611.15325v1#S6) [(ref: main Sec. S11)](https://arxiv.org/html/2611.15325v1#S11)

本書庫另外注意到：

- **標籤只有部分經人工複核** — 教學個案的 372 例沿用圖庫歸檔診斷，只有 LLM 預審標出的 64 例由一位病理醫師複核；Atlas 標籤由 LLM 從圖說對應、病理醫師確認。標籤錯誤的比例沒有獨立估計。
- **人類對照規模小** — 每個年資組只有 2 位讀者、120 例、單次作答；表中只有點估計，模型也只用了一種選項順序，人類與模型之間的差距沒有以輪換準確率比較。
- **最強開放模型有三成多是被強制作答** — Qwen3.5-9B 有 34.7% 的回答是在 token 上限內推理未完、被附上停止思考指令後才作答；它的分數部分取決於這個預算設定。
- **兩個來源的差異拆不開** — 作者也說明 Atlas 與 Teaching 在影像翻拍品質與干擾選項池上不同，專有模型在 Atlas 上掉分的原因無法分離。[(ref: main §5.5)](https://arxiv.org/html/2611.15325v1#S5.SS5)

## 與書庫其他文章的關係

該研究以拿掉切片檢驗病理 VLM 在切片層級問答是否真的看圖，本篇改在多視野個案上只留最高倍視野或拿掉一行檢體部位，發現教學個案上部位比其餘視野更影響答案，兩篇都指出病理 VLM 的答案相當程度靠文字線索: [語言替病理 VLM 加了什麼？拿掉切片，答對率只掉 0.4 個百分點](2026-11-04-pathology-vlm-language-controlled-probes.md)

Lingshu 原論文以醫療 VQA 平均分數呈現能力，本篇把 Lingshu-7B 放進病理多視野十選一診斷，單次準確率 33.6%、十種選項順序全對只有 5.7%: [Lingshu 靠合成資料拉高醫療 VQA，強化學習那一步沒加分](2026-09-15-lingshu-medical-vlm.md)

乳房攝影一致性稽核以打亂選項發現 40–99% 的答案會改變，本篇以 CircularEval 要求十種選項順序都答對，把同一種選項順序敏感度直接寫進主指標: [拿掉乳房攝影影像，MedGemma 仍以約 95 分信心給 BI-RADS](2026-11-16-mammography-vlm-cross-signal-coherence.md)

## 實務的啟發

- **選擇題評估加上選項輪換是可借用的量測方法** — 本研究中單次準確率與十次輪換全對之間，開放模型可差到 30 個百分點以上（Qwen3.5-9B 為 50.6% 對 17.9%）；內部評估病理或其他醫療 MLLM 時，只報單次準確率會高估模型的穩定性。
- **把文字線索與影像分開量** — 拿掉檢體部位、只留部分視野、R1 純文字作答這三種對照成本不高，卻能看出答案靠的是哪一部分輸入；這是可沿用的檢查清單，不是本研究已證實的部署準則。
- **分數不能直接當成臨床表現** — CaseScope 的視野是挑好的教學影像，標籤只部分經人工複核，人類對照每組只有兩位讀者；最佳專有模型在 120 例上接近第 3 年住院醫師的點估計，但這只是教科書層級、單次作答的比較，不代表在未經挑選切片上的診斷能力。

## References

- `main` — Zhang W, Zhang C, Li F, Yin T, Shu C, Chen J, Zhang S, Wu X, Zhang Z, Yi Y, Lv J, Bu H. *CaseScope: A Multi-Field Benchmark for Case-Level Pathology Diagnosis with Multimodal LLMs*. arXiv:2611.15325v1, 2026. [https://arxiv.org/abs/2611.15325](https://arxiv.org/abs/2611.15325)
  - 深鏈：[§1](https://arxiv.org/html/2611.15325v1#S1)、[Table 1](https://arxiv.org/html/2611.15325v1#S2.T1)、[§3.2](https://arxiv.org/html/2611.15325v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.15325v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.15325v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.15325v1#S3.SS5)、[§3.6](https://arxiv.org/html/2611.15325v1#S3.SS6)、[§4](https://arxiv.org/html/2611.15325v1#S4)、[Table 2](https://arxiv.org/html/2611.15325v1#S4.T2)、[§5.1](https://arxiv.org/html/2611.15325v1#S5.SS1)、[§5.2](https://arxiv.org/html/2611.15325v1#S5.SS2)、[Table 3](https://arxiv.org/html/2611.15325v1#S5.T3)、[Figure 4](https://arxiv.org/html/2611.15325v1#S5.F4)、[§5.3](https://arxiv.org/html/2611.15325v1#S5.SS3)、[§5.4](https://arxiv.org/html/2611.15325v1#S5.SS4)、[§5.5](https://arxiv.org/html/2611.15325v1#S5.SS5)、[§6](https://arxiv.org/html/2611.15325v1#S6)、[Sec. S6](https://arxiv.org/html/2611.15325v1#S6a)、[Sec. S8](https://arxiv.org/html/2611.15325v1#S8)、[Sec. S9](https://arxiv.org/html/2611.15325v1#S9)、[Table S5](https://arxiv.org/html/2611.15325v1#S9.T5)、[Sec. S10](https://arxiv.org/html/2611.15325v1#S10)、[Sec. S11](https://arxiv.org/html/2611.15325v1#S11)
- `html` — arXiv HTML v1 全文. [https://arxiv.org/html/2611.15325v1](https://arxiv.org/html/2611.15325v1)
- `code` — CaseScope evaluation code. [https://github.com/Wenchuan-Zhang/CaseScope](https://github.com/Wenchuan-Zhang/CaseScope)

[Home](../) · [AI Papers](./)
