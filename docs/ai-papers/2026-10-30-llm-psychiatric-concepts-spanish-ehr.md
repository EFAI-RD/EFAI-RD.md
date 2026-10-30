---
catalog_id: "doi:10.2196/93328"
editors:
  - "Clare"
refs:
  main:
    title: "Generative Large Language Models for Psychiatric Concept Detection in Spanish-Language Electronic Health Records: Development and Evaluation Study"
    url: "https://www.jmir.org/2026/1/e93328"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 西語精神科病歷裡的 109 個症狀概念，開源 LLM 抓得到嗎？11 個模型零樣本 macro-F1 只有 0.20–0.60，LoRA 微調後 0.75–0.86 才與規則式 tNLP 打平；只用合成資料訓練的 Mistral-small-psych 為 0.79，換到另一家醫院 0.73

## 來源

- 團隊：University of California, Los Angeles（UCLA）Semel Institute 神經行為遺傳中心與放射科學系、哥倫比亞 Universidad de Antioquia 精神醫學研究群（GIPSI）、Universidad de Caldas，共 10 位作者；第一作者 Clara Frydman-Gani，通訊作者 Loes M Olde Loohuis。[(ref: main author block)](https://www.jmir.org/2026/1/e93328)
- 論文：*Generative Large Language Models for Psychiatric Concept Detection in Spanish-Language Electronic Health Records: Development and Evaluation Study*，J Med Internet Res 2026;28:e93328，2026-10-26 正式刊出（預印本 2026-02-12 首次公開），授權 CC BY 4.0。[(ref: main)](https://www.jmir.org/2026/1/e93328) [(ref: main PDF p.18)](https://www.jmir.org/2026/1/e93328/PDF#page=18)
- 識別碼：DOI [10.2196/93328](https://doi.org/10.2196/93328)。
- 全文：[JMIR 全文頁](https://www.jmir.org/2026/1/e93328)、[PDF](https://www.jmir.org/2026/1/e93328/PDF)。
- 資料與程式：合成資料集與推論、微調、評估程式碼公開於 [GitHub](https://github.com/clarafrydman/LLMs_for_psychiatric_phenotyping)，Mistral-small-psych 模型公開於 [Hugging Face](https://huggingface.co/loeslab/mistral_small_psych)，規則式 tNLP 的 pattern 另有 [GitHub](https://github.com/clarafrydman/Spanish_Psych_Phenotyping)；含病人筆記的完整標註資料不公開。[(ref: main PDF p.15, Data Availability)](https://www.jmir.org/2026/1/e93328/PDF#page=15)
- 研究性質：完整的開發與評估研究，不是 pilot；所有模型都有實作，在院內 358 份與外院 309 份測試文件上評估，對照既有的規則式 tNLP，以 Wilcoxon signed-rank 檢定加 FDR 校正比較。只報告跨概念的 SD，沒有信賴區間或重複執行。兩家醫院都在哥倫比亞、都是精神科場域。[(ref: main Methods, Statistical Analysis; Table 3)](https://www.jmir.org/2026/1/e93328#table3)
- 證據邊界：本文數值以出版社全文頁的正文與 Table 1–4 為準；完整 prompt（Note S2）、few-shot 範例挑選（Note S3）、微調細節（Note S4）與合成資料細節（Note S5）在 Multimedia Appendix 2，概念清單與逐概念結果在 Multimedia Appendix 1，本文未納入引述。

**編輯：** Clare

作者在哥倫比亞兩家精神科醫院的西語病歷上，比較 11 個可在本機執行的開源生成式 LLM 以零樣本、few-shot 與 LoRA 微調偵測 109 個精神症狀概念：零樣本 macro-F1 為 0.20–0.60、few-shot 最高 0.74，微調後為 0.75–0.86，與先前以同一批訓練資料建立的規則式 tNLP（論文報告 0.85）大致相當；只用合成句子訓練的 Mistral-small-psych 為 0.79，在外院測試集上為 0.73。[(ref: main Abstract, Table 3, Table 4)](https://www.jmir.org/2026/1/e93328#table3)

## 流程

![西語精神科病歷概念偵測的研究設計示意圖。共五個圓角方塊，排成三欄：左上藍色方塊「1. Real Spanish EHR (CSJDM)」列出 Manizales 的精神科醫院、2,000 份文件／1,821 位病人、由一位精神科醫師與一位臨床心理師標註 136 個概念、開發集 1,642 份（訓練 1,477＋驗證 165）、測試 358 份（依概念分層）；左下紫色方塊「2. Synthetic data」列出 Llama3-70B 依審閱過的標註片段寫出臨床風格句子（T = 0.8，somatic／other 句 T = 0.99）、3,740 句組成 1,223 份文件（每份 1–6 句）、以 tNLP 弱標註把標註實例從 3,440 增加到 5,427；中上綠色方塊「3a. 11 open LLMs (local, 4-bit, T = 0)」列出 11 個模型名稱，以及零樣本（每個文件–概念配對一個 yes／no 提問）、few-shot（每個概念最多 5 個範例）、LoRA 微調（1–4 epochs，輸出概念與標註片段）；中下綠色方塊「3b. Mistral-small-psych」列出 Mistral-Small 加 LoRA 9 epochs、只用合成文件訓練，以及所有設定的對照基線為以 CSJDM 訓練資料建立的 pattern-based tNLP；右側一個縱跨全高的橘色方塊「4. Evaluation」列出院內 CSJDM 測試 358 份文件（109 個概念，tNLP 比較用 88 個）、外院 HOMO 測試 309 份文件（Hospital Mental de Antioquia，1,828 位病人，不用於訓練，跨院表用 97 個概念）、文件層級逐概念的二元判定、precision／recall／macro-F1／micro-F1，以及以 per-concept F1 做、經 FDR 校正、對 tNLP 的 Wilcoxon signed-rank 檢定。共四條實線箭頭：藍色方塊指向 3a、紫色方塊指向 3b、3a 與 3b 各指向橘色方塊](assets/llm-psychiatric-concepts-spanish-ehr-design.png)

圖：本書庫依論文 Methods 與 Table 2 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文 Figure 1 為概念範例與研究設計，Figure 4 為 Mistral-small-psych 的建立流程與跨院比較）。[(ref: main Methods; Figure 1; Figure 4)](https://www.jmir.org/2026/1/e93328#figure1)

## 背景／問題

作者的出發點是：精神症狀這類跨診斷的表現多半只寫在病歷的自由文字裡，要拿來做表型研究就得先從文字中抽出來；而既有的臨床 NLP 工具與評估大多以英文為主，西語病歷的精神症狀抽取缺少可分享的模型。先前研究（De La Hoz 等）已在同一家醫院建立規則式的 traditional NLP（tNLP）方法，本研究想知道開源生成式 LLM 能不能做到同等或更好，以及能否做出一個不碰病人資料、可以公開分享的模型。[(ref: main Introduction)](https://www.jmir.org/2026/1/e93328)

「LLM 可以取代規則方法」在本文不是前提，而是被檢驗的問題；文中規則式 tNLP 是實際跑過的對照組。「以合成資料訓練的模型可以公開分享且不暴露病人資料」則是作者的設計目標，論文用同一批模型在真實標註上微調的結果作為比較基準。[(ref: main Introduction; Methods, Fine-Tuning on Synthetic Data)](https://www.jmir.org/2026/1/e93328)

## 方法摘要

**任務。** 給一份臨床文件，判斷 136 個預先定義的精神症狀概念中，哪些出現在文件裡；評估以文件層級、逐概念的二元判定計分。[(ref: main Methods, Model Performance Metrics)](https://www.jmir.org/2026/1/e93328)

**資料。**

- **CSJDM（開發與院內測試）** — Clínica San Juan de Dios Manizales，2,000 份文件、1,821 位病人，取自 intake、急診與門診筆記中症狀描述較多的段落；由一位精神科醫師與一位臨床心理師標註 136 個概念。開發集 1,642 份（訓練 1,477、驗證 165），測試 358 份，切分時讓每個概念至少 20% 的實例落在測試集。[(ref: main Methods, Real EHR Data and Concept Annotation; Table 2)](https://www.jmir.org/2026/1/e93328#table2)
- **HOMO（外院測試）** — Hospital Mental de Antioquia，標註 2,000 份文件、1,828 位病人，其中 309 份作為測試，不用於訓練或調超參數。[(ref: main Table 2; Methods, Cross-Hospital Transportability Evaluation)](https://www.jmir.org/2026/1/e93328#table2)
- **評估概念數** — 在訓練與測試集都至少有 3 個實例的 109 個概念用於主要評估；跨院比較用兩個測試集都符合條件的 97 個；與 tNLP 比較用 88 個。[(ref: main Methods; Table 3; Table 4)](https://www.jmir.org/2026/1/e93328#table4)

**模型。** 11 個開源指令模型，以 Ollama 0.3.14 在本機 4-bit 量化執行、溫度 0：Llama3-8B／70B-Instruct、Qwen2.5-7B／14B／32B-Instruct、Mistral-7B-Instruct-v0.3、Mistral-Nemo-Instruct-2407、Mistral-Small-24B-Instruct-2501、Mixtral-8x7B-Instruct-v0.1、Aya-23-8B／35B。[(ref: main Table 1; Methods, Setting)](https://www.jmir.org/2026/1/e93328#table1)

**三種用法與一個合成資料模型。**

- **Zero-shot** — 每個文件–概念配對單獨提問，要求回答概念是否出現。[(ref: main Methods, Zero-Shot Prompting)](https://www.jmir.org/2026/1/e93328)
- **Few-shot** — 每個概念最多 5 個標註範例，從該概念最常見的 10 種不同標註中隨機抽，所有模型與文件共用同一組範例。[(ref: main Methods, Few-Shot Prompting)](https://www.jmir.org/2026/1/e93328)
- **Fine-tuned** — 以 LoRA 在 CSJDM 訓練集上做 multilabel、文件層級的指令微調，模型輸出偵測到的概念與對應的文字片段。[(ref: main Methods, Fine-Tuning on CSJDM Data)](https://www.jmir.org/2026/1/e93328)
- **Mistral-small-psych** — 只用合成文件微調的 Mistral-Small，作者把它當成可公開分享的模型釋出。[(ref: main Methods, Fine-Tuning on Synthetic Data; Figure 4)](https://www.jmir.org/2026/1/e93328#figure4)

**對照與指標。** 對照組為先前研究（De La Hoz 等）以同一批 CSJDM 訓練資料建立的 pattern-based tNLP。指標為 precision、recall、macro-F1（各概念 F1 的平均）與 micro-F1（跨概念合併 TP、FP、FN 後計算）；模型間比較以各概念 F1 做 Wilcoxon signed-rank 檢定，並做 false discovery rate（FDR）校正。[(ref: main Methods, Model Performance Metrics; Comparison to tNLP Method; Statistical Analysis)](https://www.jmir.org/2026/1/e93328)

## 方法詳解

**回答怎麼解析。** Zero-shot 與 few-shot 只接受二元回答，無法解析成是／否的回答一律算陰性。微調模型輸出自由文字的概念名稱與片段，評估時再對應回預先定義的概念清單；清單以外的標籤不計。[(ref: main Methods, Response Parsing; Discussion)](https://www.jmir.org/2026/1/e93328)

**微調設定。** LoRA 套在 4-bit 量化的基礎模型上，以 Unsloth 或 Axolotl 訓練，每個模型從同一個超參數空間挑出 1–4 個 epoch；硬體為 AWS G5 執行個體上的 1 張或 4 張 NVIDIA A10G（各 24 GB）。[(ref: main Methods, Fine-Tuning on CSJDM Data; Setting)](https://www.jmir.org/2026/1/e93328)

**合成資料怎麼做。** 作者把人工審閱過的簡短標註片段交給 Llama3-70B，生成臨床風格的句子（概念句溫度 0.8，與精神症狀無關的身體或其他描述句溫度 0.99）；品質檢查後取 3,440 句概念句加 300 句其他句，共 3,740 句，打散後每 1–6 句組成一份「文件」，得 1,223 份（平均 83.72 tokens，SD 51.91）。接著用 tNLP 對這些合成文件做弱標註，把標註實例從 3,440 個增加到 5,427 個，再以 Mistral-Small 為基礎模型微調 9 個 epoch（單張 A10G 約 4 小時），得到 Mistral-small-psych。[(ref: main Methods, Synthetic Data; Fine-Tuning on Synthetic Data)](https://www.jmir.org/2026/1/e93328)

**合成資料量的敏感度分析。** 從合成文件各抽 250、500、750、1,000 份、每種大小 3 個隨機子集重新訓練，觀察表現隨資料量的變化。[(ref: main Methods, Synthetic Training Set Size Sensitivity Analysis)](https://www.jmir.org/2026/1/e93328)

- **論文未交代** — 完整 prompt 的內容與語言、是否在 prompt 中提供概念定義；正文只說 prompt 在 Note S2。
- **論文未交代** — LoRA 的 rank、alpha、learning rate、batch size，以及「同一個超參數空間」的範圍；正文只給 epoch 數，細節在 Note S4。
- **論文未交代** — 標註者間一致性 Cohen κ 的數值；正文說有在訓練集計算，並用它與模型表現做相關分析，但沒有列出 κ 本身。
- **論文未交代** — 微調模型的自由文字輸出對應回概念清單的具體規則，以及片段（span）是否納入計分。
- **論文未交代** — 文件的時間範圍；HOMO 的筆記類型；tNLP 報告的 macro-F1 0.85 是在 109 個概念還是 88 個概念上計算。
- **論文未交代** — 合成句子的品質檢查準則，以及生成時所用標註片段是否只取自訓練集。

## 資料與實驗

下表摘錄論文 Table 2 的兩個資料集。[(ref: main Table 2)](https://www.jmir.org/2026/1/e93328#table2)

| 項目 | CSJDM | HOMO |
|---|---|---|
| 標註文件數 | 2,000 | 2,000 |
| 開發集文件數 | 1,642 | 未使用 |
| 測試集文件數 | 358 | 309 |
| 納入的筆記段落 | Chief complaint、thought content、analysis、current illness、objective | Chief complaint、thought content、analysis、affect、sensory-perception |
| 病人數 | 1,821 | 1,828 |

下表摘錄論文 Table 3：CSJDM 測試集（109 個概念）上的 macro-F1（括號內為跨概念 SD）與 micro-F1。Mistral-small-psych 只有微調結果。[(ref: main Table 3)](https://www.jmir.org/2026/1/e93328#table3)

| 模型 | Zero-shot macro-F1 | Zero-shot micro-F1 | Few-shot macro-F1 | Few-shot micro-F1 | Fine-tuned macro-F1 | Fine-tuned micro-F1 |
|---|---|---|---|---|---|---|
| Llama3-70B | 0.53 (0.24) | 0.58 | 0.56 (0.24) | 0.60 | 0.79 (0.18) | 0.81 |
| Llama3-8B | 0.39 (0.23) | 0.45 | 0.52 (0.22) | 0.60 | 0.82 (0.18) | 0.84 |
| Qwen2.5-14B | 0.57 (0.23) | 0.59 | 0.67 (0.20) | 0.72 | 0.82 (0.19) | 0.84 |
| Qwen2.5-32B | 0.53 (0.26) | 0.53 | 0.67 (0.22) | 0.70 | 0.86 (0.16) | 0.87 |
| Qwen2.5-7B | 0.53 (0.25) | 0.62 | 0.69 (0.23) | 0.74 | 0.79 (0.22) | 0.81 |
| Aya-35B | 0.27 (0.20) | 0.30 | 0.38 (0.22) | 0.43 | 0.86 (0.14) | 0.87 |
| Aya-8B | 0.20 (0.18) | 0.24 | 0.20 (0.18) | 0.23 | 0.83 (0.16) | 0.84 |
| Mixtral-8x7B | 0.35 (0.24) | 0.42 | 0.55 (0.22) | 0.60 | 0.82 (0.17) | 0.84 |
| Mistral-7B | 0.21 (0.19) | 0.25 | 0.30 (0.21) | 0.37 | 0.75 (0.25) | 0.77 |
| Mistral-nemo | 0.46 (0.23) | 0.56 | 0.37 (0.19) | 0.45 | 0.85 (0.16) | 0.86 |
| Mistral-small | 0.60 (0.23) | 0.64 | 0.74 (0.19) | 0.78 | 0.86 (0.16) | 0.88 |
| Mistral-small-psych | — | — | — | — | 0.79 (0.15) | 0.85 |

下表摘錄論文 Table 4：微調模型在院內（CSJDM）與外院（HOMO）測試集上的表現，限兩個測試集都符合條件的 97 個概念；macro-F1 括號內為跨概念 SD。[(ref: main Table 4)](https://www.jmir.org/2026/1/e93328#table4)

| 模型 | CSJDM precision | CSJDM recall | CSJDM macro-F1 | CSJDM micro-F1 | HOMO precision | HOMO recall | HOMO macro-F1 | HOMO micro-F1 |
|---|---|---|---|---|---|---|---|---|
| Llama3-70B | 0.90 | 0.76 | 0.81 (0.16) | 0.89 | 0.84 | 0.74 | 0.77 (0.21) | 0.86 |
| Llama3-8B | 0.90 | 0.79 | 0.83 (0.18) | 0.90 | 0.85 | 0.64 | 0.70 (0.24) | 0.81 |
| Qwen2.5-14B | 0.89 | 0.80 | 0.82 (0.19) | 0.91 | 0.87 | 0.74 | 0.77 (0.20) | 0.86 |
| Qwen2.5-32B | 0.89 | 0.86 | 0.87 (0.15) | 0.93 | 0.86 | 0.76 | 0.79 (0.19) | 0.87 |
| Qwen2.5-7B | 0.89 | 0.76 | 0.81 (0.20) | 0.88 | 0.82 | 0.58 | 0.65 (0.23) | 0.76 |
| Aya-35B | 0.90 | 0.85 | 0.86 (0.13) | 0.92 | 0.87 | 0.81 | 0.83 (0.14) | 0.88 |
| Aya-8B | 0.88 | 0.82 | 0.83 (0.16) | 0.91 | 0.81 | 0.72 | 0.74 (0.20) | 0.84 |
| Mistral-7B | 0.83 | 0.75 | 0.77 (0.22) | 0.88 | 0.77 | 0.57 | 0.63 (0.26) | 0.77 |
| Mistral-nemo | 0.91 | 0.83 | 0.85 (0.16) | 0.92 | 0.87 | 0.72 | 0.77 (0.20) | 0.85 |
| Mistral-small | 0.90 | 0.85 | 0.86 (0.16) | 0.92 | 0.85 | 0.79 | 0.81 (0.23) | 0.89 |
| Mixtral-8x7B | 0.88 | 0.81 | 0.83 (0.17) | 0.91 | 0.86 | 0.80 | 0.81 (0.14) | 0.87 |
| Mistral-small-psych | 0.84 | 0.79 | 0.81 (0.15) | 0.85 | 0.83 | 0.68 | 0.73 (0.17) | 0.79 |

## 結果

- **只靠提示遠遠不夠** — 零樣本 macro-F1 介於 0.20（Aya-8B）到 0.60（Mistral-small），few-shot 最高 0.74（Mistral-small）；作者報告 tNLP 在零樣本與 few-shot 設定下顯著優於所有 LLM。錯誤以偽陽性為主，例如零樣本 Mistral-7B 的 precision 只有 0.14、recall 0.88。[(ref: main Results; Table 3)](https://www.jmir.org/2026/1/e93328#table3)
- **微調後與規則方法打平** — 微調後 macro-F1 為 0.75–0.86，Aya-35B、Mistral-small、Qwen2.5-32B 並列最高 0.86；論文報告 tNLP 為 0.85。微調後 tNLP 只顯著勝過 Llama3-70B（校正後 P=.01），其餘模型與 tNLP 沒有顯著差異。[(ref: main Results; Table 3)](https://www.jmir.org/2026/1/e93328#table3)
- **概念層級各有勝負** — 有 9 個概念 tNLP 勝過所有微調 LLM，10 個概念所有微調 LLM 都勝過 tNLP；作者報告共有 100 個概念至少有一個微調 LLM 或 tNLP 的 F1 超過 0.8。[(ref: main Results)](https://www.jmir.org/2026/1/e93328)
- **哪些概念難** — 微調模型的逐概念表現與訓練頻率（Spearman ρ=0.32–0.55）及標註者間一致性（ρ=0.46–0.61）相關。表現差的多是範圍廣或用詞多變的概念，例如 "other addictions"、"adverse effects"、"poor response to psychotropic medications"；"hypothymia" 雖然訓練頻率低，所有模型 F1 都在 0.89 以上。[(ref: main Results; Figure 3)](https://www.jmir.org/2026/1/e93328#figure3)
- **換一家醫院** — 在 97 個概念上，微調模型在 HOMO 的 macro-F1 為 0.63–0.83；Mixtral-8x7B 只降 0.02（0.83→0.81），Qwen2.5-7B 降 0.16（0.81→0.65）。從 Table 4 看，多數模型的 recall 降幅大於 precision（例如 Qwen2.5-7B recall 0.76→0.58、precision 0.89→0.82），但 Llama3-70B 與 Mixtral-8x7B 的 recall 幾乎沒有下降。[(ref: main Results; Table 4)](https://www.jmir.org/2026/1/e93328#table4)
- **合成資料模型** — Mistral-small-psych 在 109 個概念上 macro-F1 0.79、micro-F1 0.85，在 97 個概念上院內 0.81、外院 0.73；同一個基礎模型以真實標註微調為 0.86 與 0.81。只用合成句子、不加 tNLP 弱標註時 macro-F1 只有 0.49。[(ref: main Results; Table 3; Table 4)](https://www.jmir.org/2026/1/e93328#table4)
- **合成資料量** — 抽 750 份合成文件訓練時平均 F1 約 0.78，已接近用全部合成資料的結果；同一大小的子集之間平均 F1 差異在 0.01 以內。[(ref: main Results, Synthetic Training Set Size Sensitivity Analysis)](https://www.jmir.org/2026/1/e93328)
- **執行成本** — 每 100 份文件的推論時間，Aya-35B 為 85.62 秒、Llama3-70B 為 81.11 秒；Llama3-70B 耗電 12.2 Wh，約為 Llama3-8B 的 7 倍。[(ref: main Results, Inference Runtime, Electricity Consumption, and Cost)](https://www.jmir.org/2026/1/e93328)

## 限制

**作者自述的限制。** 表現依賴特定院所的標註語料，可能受資料漂移、書寫習慣、病人族群與流程改變影響，需要定期重新評估；輸出的文字片段有助檢查，但不能說明模型的決策過程，也不保證抽出的概念在臨床上正確；只評估 decoder-only 的生成式模型，沒有和 BERT 這類 encoder 比較；兩個測試集都來自哥倫比亞的精神科醫院，西語臨床用語在不同國家差異大，且兩院納入的筆記段落不同，推論到其他西語地區要保守。[(ref: main Discussion, Limitations)](https://www.jmir.org/2026/1/e93328)

**本書庫的觀察。**

- **同一模型的數字在不同表不一樣** — Mistral-small-psych 在 Table 3 為 0.79、在 Table 4 院內為 0.81，Llama3-70B 為 0.79 與 0.81；兩表的概念集合不同（109 對 97），可以解釋差異，但讀者比較不同段落的數字時要先確認是哪一組概念。
- **tNLP 的比較基準不完全對齊** — tNLP 是在同一批 CSJDM 訓練資料上手工建立的 pattern，論文報告的 0.85 沒有標明概念集合，跨院比較表（Table 4）也沒有 tNLP 的外院結果；「微調 LLM 與 tNLP 打平」只在院內成立，無法得知 tNLP 換一家醫院會掉多少。
- **合成資料並沒有脫離真實標註** — 合成句子是從人工審閱過的真實標註片段生成，訓練標籤又由在真實資料上建立的 tNLP 補強；不加 tNLP 弱標註只有 0.49。Mistral-small-psych 證明的是「不必釋出病人原文也能分享模型」，不是「不需要專家標註」。
- **不確定性只有跨概念 SD** — 溫度 0、單次執行，SD 反映的是概念之間的差異，不是抽樣或訓練隨機性；模型之間 0.01–0.03 的 macro-F1 差距不應解讀成排名。
- **零樣本的偽陽性與解析規則有關** — 每個文件–概念配對獨立提問，每份文件要對每個概念各問一次；作者把無法解析的回答算成陰性，零樣本的低 precision 是在這個設計下觀察到的，換成一次列出全部概念的提問方式結果可能不同。

## 與書庫其他文章的關係

假釋／緩刑偵測那篇只用 GPT-4o-mini 生成的合成句子訓練、再拿真實 VA 病歷測試，本篇的 Mistral-small-psych 也只用合成文件微調，但合成句子源自真實標註片段、並以規則式 tNLP 補標，且有同一基礎模型以真實標註微調的結果可直接對照，兩篇合起來看可以比較兩種「不釋出病人資料」的合成資料做法各自付出的代價: [一筆真實標註都不用：GPT-4o-mini 生成的 7,579 句合成資料（訓練集 5,305 句），換到 293 份 VA 病歷偵測假釋／緩刑，Llama 3.3-70B 以合成範例 few-shot 達 87% macro-F1、微調的 Llama 3.1-8B 達 81%，encoder 跌到 30%](2026-10-20-llm-synthetic-data-parole-probation-detection.md)

時間關係抽取那篇在 i2b2 上比較 standard fine-tuning、hard-／soft-prompting 與 QLoRA 等需要訓練的調適策略，並看到每類只給一例時沒有一種做法超過 60%；本篇則比較不訓練的零樣本／few-shot 提示與 LoRA 微調，兩篇都顯示病歷抽取的表現高度依賴調適方式與標註量，也都在換資料來源後看到表現下降: [病歷時間關係抽取該怎麼調模型？i2b2 2012 上只調 query／value 的 QLoRA 讓 LLaMA3.1-8B 達 89.15% micro-F1，但每類只給一例時沒有一種做法超過 60%](2026-10-20-llm-clinical-temporal-relation-extraction-adaptation.md)

## 實務的啟發

- **可借用的做法** — 病歷概念抽取若已有一定量的在地標註，LoRA 微調中型開源模型比零樣本或 few-shot 提示可靠得多；本篇在同一批 109 個概念上，從 0.20–0.74 拉到 0.75–0.86。這是單一國家、精神科場域的結果，換語言或科別前需要複驗。
- **可借用的量測方法** — 同時報告院內與外院結果，並把 precision 與 recall 分開看；本篇多數模型跨院時 recall 掉得比 precision 多，只看院內 F1 會低估模型在新院所漏抓的程度。
- **可借用的做法** — 想公開分享模型又不能釋出病歷時，可以參考「從審閱過的標註片段生成句子＋以既有規則補標＋微調」的流程；但本篇顯示少了規則補標只有 0.49，這條路仍依賴在真實資料上建立的標註與規則。
- **待驗證的警訊** — 規則方法在院內與微調 LLM 打平，論文卻沒有它的外院結果；在選擇規則或 LLM 時，應先在目標院所的資料上同時測兩者，而不是依本篇院內的數字決定。
- **證據強度** — 兩家院所、358＋309 份測試文件、單次執行、只有跨概念 SD；它支持「微調後的開源 LLM 在西語精神科病歷上可達到與既有規則方法相當的概念偵測水準，且多數模型換院後只中度下降」，不足以支持直接用於臨床決策或其他語言、科別。

## References

- **main** — Frydman-Gani C, Arias A, Perez-Vallejo M, Londoño Martínez JD, Valencia-Echeverry J, Castano Ramírez M, Bui AAT, Freimer NB, Lopez-Jaramillo C, Olde Loohuis LM. *Generative Large Language Models for Psychiatric Concept Detection in Spanish-Language Electronic Health Records: Development and Evaluation Study*. J Med Internet Res. 2026;28:e93328. DOI: 10.2196/93328. 全文：<https://www.jmir.org/2026/1/e93328>。文內引用位置：author block、Abstract、Introduction、Methods（Setting、Real EHR Data and Concept Annotation、Synthetic Data、Zero-Shot Prompting、Few-Shot Prompting、Fine-Tuning on CSJDM Data、Fine-Tuning on Synthetic Data、Response Parsing、Model Performance Metrics、Comparison to tNLP Method、Cross-Hospital Transportability Evaluation、Statistical Analysis、Synthetic Training Set Size Sensitivity Analysis）、Results、Discussion（Limitations）；深鏈 [Table 1](https://www.jmir.org/2026/1/e93328#table1)、[Table 2](https://www.jmir.org/2026/1/e93328#table2)、[Table 3](https://www.jmir.org/2026/1/e93328#table3)、[Table 4](https://www.jmir.org/2026/1/e93328#table4)、[Figure 1](https://www.jmir.org/2026/1/e93328#figure1)、[Figure 3](https://www.jmir.org/2026/1/e93328#figure3)、[Figure 4](https://www.jmir.org/2026/1/e93328#figure4)。
- **PDF** — <https://www.jmir.org/2026/1/e93328/PDF>（p.15 Data Availability、p.18 授權聲明）。
- **doi** — <https://doi.org/10.2196/93328>。
- **code** — <https://github.com/clarafrydman/LLMs_for_psychiatric_phenotyping>。
- **model** — <https://huggingface.co/loeslab/mistral_small_psych>。
- **tNLP patterns** — <https://github.com/clarafrydman/Spanish_Psych_Phenotyping>。

[Home](../) · [AI Papers](./)
