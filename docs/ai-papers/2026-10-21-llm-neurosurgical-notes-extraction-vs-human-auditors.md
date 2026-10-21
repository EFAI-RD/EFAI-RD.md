---
catalog_id: "doi:10.3390/make8100328"
editors:
  - "Clare"
refs:
  main:
    title: "Large Language Models for Information Extraction from Neurosurgical Clinical Notes: A Benchmark Against Human Auditors"
    url: "https://www.mdpi.com/2504-4990/8/10/328"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 零樣本 LLM 讀德文神經外科病歷：最好的雲端模型在術前症狀與病程 F1 高過兩位初階稽核者，46 個術後併發症標籤上最好也只有 0.68

## 來源

- 團隊：Eberhard Karls University Tübingen 神經外科暨神經技術部（Department of Neurosurgery and Neurotechnology），共 6 位作者；第一作者暨通訊作者 Aldo Spolaore。[(ref: main author block)](https://www.mdpi.com/2504-4990/8/10/328)
- 論文：*Large Language Models for Information Extraction from Neurosurgical Clinical Notes: A Benchmark Against Human Auditors*，Machine Learning and Knowledge Extraction 2026;8(10):328，2026-10-11 線上刊出，開放取用（CC BY）。[(ref: main)](https://www.mdpi.com/2504-4990/8/10/328)
- 識別碼：DOI [10.3390/make8100328](https://doi.org/10.3390/make8100328)。
- 全文：[MDPI 全文頁](https://www.mdpi.com/2504-4990/8/10/328)。
- 資料與程式：病歷資料不公開，去識別化資料可依合理請求並經核准後向通訊作者索取；分析與介接程式碼在 [GitHub leoamedeo/LLMvsClinicians](https://github.com/leoamedeo/LLMvsClinicians)。[(ref: main Data Availability Statement)](https://www.mdpi.com/2504-4990/8/10/328)
- 研究性質：單一機構回顧性研究，不是 pilot；六個模型都實際跑過 211 位病人、每個設定 3 次執行，附病人層級 cluster bootstrap 95% CI；模型與稽核者的差異比較作者明說是探索性的。模型是 2025 年 2–4 月的版本快照。[(ref: main §2.4, §2.6)](https://www.mdpi.com/2504-4990/8/10/328)
- 證據邊界：本文的模型數值採用論文附錄 Table A7–A9 的三次執行平均與 Table A4 的合併計數，稽核者數值採用 §3.5 正文與 Table A1、A5 的混淆矩陣；Table 1 的信賴區間與 Table A14 的多重比較校正區間未納入本文引述。

**編輯：** Clare

作者在 Tübingen 單一中心 211 位微血管減壓術（microvascular decompression，MVD）病人、881 份以德文為主的病歷上，用零樣本 prompt 讓四個雲端 LLM 與兩個本地 70B 模型抽取 15 個是／否變項，對照一位醫學生與一位神經外科初階住院醫師的人工稽核：術前症狀與病程兩個領域，最好的雲端模型平均 F1 為 0.953 與 0.951，高於兩位稽核者的 0.87–0.90；但只有 46 個陽性標籤的術後併發症領域，最好的模型 F1 為 0.678，兩個本地模型都低於 0.40。[(ref: main Abstract; Tables A7–A9)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A7)

## 流程

![零樣本 LLM 抽取神經外科病歷對照人工稽核的研究設計示意圖。由左到右四欄：最左藍色方塊「1. Cohort and notes」列出 Tuebingen（Tübingen）單一中心、Microvascular decompression、2010–2022，224 位找到、211 位納入（2 位非 MVD、11 位缺至少 3 個月追蹤而排除），881 份去識別化、以德文為主的筆記（每位平均 4.17 份），每位病人的筆記依時間順序串接；藍色方塊以兩條實線箭頭分別指向第二欄上方綠色方塊「2a. Cloud LLMs (API)」（GPT-4o、o3-mini、Claude Sonnet 3.5、Gemini 2.0 Flash）與下方綠色方塊「2b. Local LLMs (Ollama, 70B)」（Llama 3.3、DeepSeek-R1）；兩個綠色方塊下方的文字註明六個模型使用相同的零樣本領域 prompt、先推理再以 Yes/No 條列作答、可設定時 temperature 0、每位病人每個領域跑 3 次。兩個綠色方塊各以一條實線箭頭指向第三欄灰色方塊「4. Evaluation」：15 個二元變項、3 個領域各 5 個（術前症狀、術後併發症、病程），指標為 accuracy、sensitivity、specificity、F1、kappa（每次執行合併 5 個變項計算、取 3 次平均），病人層級 cluster bootstrap CI，以及跨次執行的一致性。最右一欄上方橘色方塊「3a. Human auditors」（HA1 醫學生、HA2 神經外科初階住院醫師，各做一次獨立審閱且看不到 LLM 輸出）與下方橘色方塊「3b. Reference standard」（2 位臨床醫師獨立標註，分歧以共識解決，在檢視 LLM 輸出前完成）各以一條實線箭頭向左指向灰色方塊](assets/neurosurgical-notes-llm-extraction-design.png)

圖：本書庫依論文 §2 Materials and Methods 與 Figure 1 的文字重繪的研究設計示意圖，只含設計層級的計數與設定，不含結果數值，未複製論文原圖（論文 Figure 1 為病人篩選流程，Figure 2 為零樣本抽取管線與 prompt 組成）。[(ref: main §2; Figure 1; Figure 2)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f001)

## 背景／問題

回顧性臨床研究多半要靠人工翻閱病歷做 chart abstraction。作者引用文獻指出這項工作耗時、且不同摘錄者之間結果不一致；傳統 NLP 則需要針對任務寫規則或準備標註資料。[(ref: main §1 Introduction)](https://www.mdpi.com/2504-4990/8/10/328)

作者因此在一個具體情境下比較：不給任何範例、只用領域 prompt 的 LLM，從神經外科病歷判斷 15 個研究變項時，能不能達到人工稽核者的水準；雲端商用模型與可在院內本地執行的開放權重模型差多少；同一個模型重跑三次答案是否穩定。作者另主張檢索增強或微調會增加運算、延遲與資料工程負擔，所以長上下文零樣本 prompting「可能是較實際的替代」——這一句是作者的推論，論文沒有引用證據，也沒有在本研究裡比較 RAG 或微調。[(ref: main §1 Introduction)](https://www.mdpi.com/2504-4990/8/10/328)

## 方法摘要

**任務。** 病人層級的 15 個二元變項，分三個領域各 5 個：術前症狀（trigeminal pain、facial numbness、lacrimation、vertigo、facial spasm）、術後併發症（CSF leak、infection、facial palsy、facial numbness、hearing loss）、病程（第一次手術後改善、第一次手術後無痛、第一次手術後復發、第二次手術、thermocoagulation）。[(ref: main §2.3)](https://www.mdpi.com/2504-4990/8/10/328)

**六個模型。**

- **雲端 API** — GPT-4o（gpt-4o-2024-08-06）、o3-mini（o3-mini-2025-01-31）、Claude Sonnet 3.5（claude-3-5-sonnet-20241022）、Gemini 2.0 Flash（gemini-2.0-flash-exp）。[(ref: main §2.4)](https://www.mdpi.com/2504-4990/8/10/328)
- **本地（Ollama 0.5.8，NVIDIA RTX A6000）** — Llama 3.3 70B、DeepSeek-R1 70B。[(ref: main §2.4)](https://www.mdpi.com/2504-4990/8/10/328)

**Prompting。** 每個領域一個零樣本 prompt，不給範例，要求模型先寫推理或簡短臨床摘要，再以條列輸出每個變項的 Yes／No；可設定的模型 temperature 設 0。每位病人、每個模型、每個領域跑 3 次。[(ref: main §2.4; Appendix B.2–B.5)](https://www.mdpi.com/2504-4990/8/10/328#app2-make-08-00328)

**比較對象。** 參考標準由一位神經外科住院醫師與一位資深神經外科醫師獨立標註、共識裁決；另有兩位人工稽核者（HA1 醫學生、HA2 神經外科初階住院醫師）各自獨立審閱一次，作為「人工摘錄」的對照。[(ref: main §2.5)](https://www.mdpi.com/2504-4990/8/10/328)

**指標。** Accuracy、sensitivity、specificity、F1 與 Cohen's κ；併發症另報 PPV、NPV。95% CI 以病人為單位做 100,000 次 cluster bootstrap。[(ref: main §2.6)](https://www.mdpi.com/2504-4990/8/10/328)

## 方法詳解

**病人與病歷。** 2010–2022 年找到 224 位病人，排除 2 位非 MVD 手術、11 位沒有至少 3 個月追蹤紀錄者，剩 211 位。適應症約 83% 為三叉神經痛、13% 為半面痙攣，其餘為舌咽神經痛與前庭陣發症。881 份筆記（每位平均 4.17 份），以 GPT-2 編碼計每位病人平均 2,602 個 token。[(ref: main §2.1, §3.1; Figure 1)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f001)

**去識別化與輸入。** 雲端處理前做半自動去識別化，並由人逐份檢查。每位病人的筆記依時間順序串成一份輸入；可設定的模型 context 上限設為 32,768 token。[(ref: main §2.2, §2.4; Appendix B.1)](https://www.mdpi.com/2504-4990/8/10/328#app2-make-08-00328)

**標籤規則。** 病歷沒有記載的發現編為 No；模型回答 Not provided 時，在二元分析中也編為 No。作者特別說明，參考標準裡的 No 代表「病歷沒有確立這個發現」，不等於臨床上確認沒有。[(ref: main §2.3)](https://www.mdpi.com/2504-4990/8/10/328)

**Prompt 開發。** 只在術前症狀領域、用另外 11 位不納入評估的病人試了四版 prompt（初版、加臨床角色、加「未提及即編 No」、加「先推理」），以人工閱讀原始病歷做質性檢查，不對照參考標籤；定稿後才檢視 211 位評估病人的輸出，再把同一結構改寫給另兩個領域。[(ref: main Appendix B.1; Figure A1)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f0A1)

**輸出解析。** 以規則比對變項名稱與 Yes／No（含德文 Ja／Nein），無法解析的回答由人工轉錄，不修正其臨床內容。[(ref: main Appendix B.1)](https://www.mdpi.com/2504-4990/8/10/328#app2-make-08-00328)

**指標的彙總方式。** 每次執行把同一領域 5 個變項的 1,055 個病人–變項標籤合併成一個混淆矩陣計算指標，再取 3 次執行的算術平均；例如 GPT-4o 術前症狀第 1 次執行為 TP 268、FN 20、FP 3、TN 764。另一組「合併計數」指標（Table A4）是把 3 次執行的混淆計數相加後計算，與三次平均的數值不一定相同。[(ref: main §2.6; Table A1)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A1)

**統計比較。** 模型與稽核者的 F1 差以病人層級配對 bootstrap 估計，並對 36 組比較（6 模型 × 2 稽核者 × 3 領域）做 Bonferroni 校正；作者明說這些比較是探索性的。一致性定義為同一病人–變項三次執行答案完全相同的比例，作者提醒它衡量的是可重複性、不是正確性。[(ref: main §2.6; Figure 4)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f004)

- **論文未交代** — o3-mini 與 DeepSeek-R1 沒有設定輸出長度上限或 reasoning effort，所有模型都沒有設定 seed 與其他取樣參數；推理型與非推理型模型的設定因此不完全對等。
- **論文未交代** — 病人的年齡、性別與追蹤時間長度；只報告排除條件與適應症比例。
- **論文未交代** — 沒有規則式或傳統 NLP 的對照組，也沒有 RAG、few-shot 或微調的對照，無法判斷零樣本是否真的比這些做法「更實際」。
- **論文未交代** — 處理時間、API 成本與人工去識別化花費的工時；論文只說逐份人工檢查會增加工作量。
- **論文未交代** — 兩位稽核者只各做一次審閱、且資歷較淺，論文沒有經驗豐富的專業摘錄者作為對照。

## 資料與實驗

下表整理三個領域的變項與參考標準陽性數（每個領域 211 位病人 × 5 個變項 = 1,055 個標籤）。[(ref: main §2.3; Tables A1–A5; Figure 3)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f003)

| 領域 | 5 個變項 | 陽性標籤 / 總標籤 |
|---|---|---|
| 術前症狀 | trigeminal pain、facial numbness、lacrimation、vertigo、facial spasm | 288 / 1,055 |
| 術後併發症 | CSF leak（5 位）、infection（1 位）、facial palsy（8 位）、facial numbness（24 位）、hearing loss（8 位） | 46 / 1,055 |
| 病程 | 第一次手術後改善、無痛、復發、第二次手術、thermocoagulation | 466 / 1,055 |

下表摘錄三個領域的 F1。模型為三次執行的平均（括號內為 SD），取自論文 Table A7–A9；稽核者為單次審閱，取自 §3.5 正文。[(ref: main Tables A7–A9; §3.5)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A8)

| 模型／稽核者 | 部署 | 術前症狀 F1 | 術後併發症 F1 | 病程 F1 |
|---|---|---|---|---|
| GPT-4o | 雲端 | 0.953 (0.005) | 0.678 (0.021) | 0.929 (0.004) |
| o3-mini | 雲端 | 0.908 (0.012) | 0.645 (0.019) | 0.919 (0.007) |
| Gemini 2.0 Flash | 雲端 | 0.926 (0.008) | 0.659 (0.038) | 0.855 (0.004) |
| Claude Sonnet 3.5 | 雲端 | 0.921 (0.003) | 0.617 (0.017) | 0.951 (0.004) |
| Llama 3.3 | 本地 70B | 0.861 (0.002) | 0.352 (0.049) | 0.696 (0.011) |
| DeepSeek-R1 | 本地 70B | 0.855 (0.006) | 0.390 (0.073) | 0.600 (0.012) |
| HA1（醫學生） | 人工 | 0.898 | 0.549 | 0.882 |
| HA2（初階住院醫師） | 人工 | 0.896 | 0.417 | 0.870 |

下表摘錄術後併發症領域的 sensitivity 與 specificity（三次執行平均），可以看出 F1 背後的取捨。[(ref: main Table A8)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A8)

| 模型 | Sensitivity | Specificity | κ |
|---|---|---|---|
| GPT-4o | 0.841 | 0.971 | 0.660 |
| o3-mini | 0.870 | 0.962 | 0.625 |
| Gemini 2.0 Flash | 0.804 | 0.971 | 0.640 |
| Claude Sonnet 3.5 | 0.543 | 0.990 | 0.602 |
| Llama 3.3 | 0.261 | 0.988 | 0.333 |
| DeepSeek-R1 | 0.370 | 0.976 | 0.364 |

下表摘錄論文 Table A4 兩種併發症的合併計數指標（三次執行的混淆計數相加後計算）。[(ref: main Table A4)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A4)

| 併發症 | 模型 | Recall | PPV | F1 |
|---|---|---|---|---|
| Facial palsy（8 位） | GPT-4o | 0.958 | 0.885 | 0.920 |
| Facial palsy（8 位） | Gemini 2.0 Flash | 0.958 | 0.958 | 0.958 |
| Facial palsy（8 位） | Llama 3.3 | 0.417 | 0.714 | 0.526 |
| Facial numbness（24 位） | GPT-4o | 0.819 | 0.488 | 0.611 |
| Facial numbness（24 位） | o3-mini | 0.903 | 0.455 | 0.605 |
| Facial numbness（24 位） | Claude Sonnet 3.5 | 0.403 | 0.690 | 0.509 |
| Facial numbness（24 位） | Llama 3.3 | 0.222 | 0.593 | 0.323 |

## 結果

- **術前症狀與病程** — 四個雲端模型在術前症狀的 F1 為 0.908–0.953（GPT-4o 最高），病程為 0.855–0.951（Claude Sonnet 3.5 最高、Gemini 2.0 Flash 最低）；兩位稽核者分別為 0.898／0.896 與 0.882／0.870。[(ref: main Tables A7, A9; §3.5)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A9)
- **與稽核者的探索性比較** — 校正後，GPT-4o 在術前症狀（F1 差 +0.055、+0.057）與病程（+0.047、+0.059）高於兩位稽核者，Claude Sonnet 3.5 在病程高於兩位（+0.069、+0.081），o3-mini 在病程高於 HA2（+0.048）；術後併發症所有校正後區間都包含 0。作者明說這些結果不足以宣稱與人工審閱等效或不劣於人工。[(ref: main §3.5, §4)](https://www.mdpi.com/2504-4990/8/10/328)
- **術後併發症是共同的弱點** — 46 個陽性標籤下，雲端模型 F1 0.617–0.678，GPT-4o sensitivity 0.841 但約七成假陽性來自 facial numbness；作者推測模型難以分辨術前就有的麻木與術後新出現的缺損。兩位稽核者在這個領域的 sensitivity 也只有 54.3% 與 32.6%，兩人之間的 κ 為 0.433（95% CI 0.279–0.571）。[(ref: main §3.5, §4 Discussion; Table A8)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A8)
- **雲端對本地** — 三個領域裡，四個雲端模型的平均 F1 都高於兩個本地模型；差距在術前症狀最小（本地最佳 0.861 對雲端最低 0.908），在併發症與病程較大。作者把本地模型規模受硬體限制列為「可能的解釋」，並指出推理導向與模型身分互相混淆，無法分開歸因。[(ref: main §3.3, §4; Tables A7–A9)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A7)
- **重跑三次的穩定性** — 三次答案完全相同的病人–變項比例：Claude Sonnet 3.5 98.86%、GPT-4o 97.73%、o3-mini 96.59%、Gemini 2.0 Flash 94.76%、Llama 3.3 94.22%、DeepSeek-R1 90.46%。即使 temperature 設 0，也沒有模型做到完全一致；DeepSeek-R1 的併發症 F1 三次分別為 0.315、0.395、0.460。[(ref: main §3.4; Figure 4; Table A8)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f004)
- **極罕見事件無法評估** — Infection 只有 1 位陽性病人，六個模型中有四個的合併 recall 為 0。[(ref: main Table A4)](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A4)

## 限制

**作者自述的限制。** 單一機構、以德文為主的筆記與專科隊列；模型是特定時間的版本快照，更新或改設定都可能改變結果；推理導向與模型身分互相混淆；人工對照只有一位醫學生與一位初階住院醫師；只評 15 個二元變項，沒有評估模型寫出的推理文字；罕見事件的 sensitivity 估計不穩定；每個模型只跑 3 次；需要前瞻、多中心驗證；即使已去識別化，雲端處理仍有隱私與治理上的疑慮。[(ref: main §4)](https://www.mdpi.com/2504-4990/8/10/328)

**本書庫的觀察。**

- **「勝過人工」的對照組偏弱** — 比較對象是單次審閱的醫學生與初階住院醫師，而參考標準本身由兩位臨床醫師共識產生；模型高於這兩位，不代表高於經驗豐富的專業摘錄者，論文也明確不這樣主張。
- **No 的意義是「病歷沒寫」** — 未記載編為 No、Not provided 也編為 No，因此這裡的 specificity 衡量的是「沒有在病歷裡找出不存在的紀錄」，不是確認臨床上沒有該症狀；換到記錄習慣不同的醫院，陽性與陰性的分界會跟著變。
- **併發症的數字是在很少的陽性病人上估的** — 46 個陽性標籤分散在 5 種併發症、其中 infection 只有 1 位，Table A4 的 recall 每一格只由 3 到 72 個陽性計數（三次執行合併）組成，單一病人就能讓數值大幅移動。
- **Prompt 只在術前症狀上調過** — 另外兩個領域沿用同一結構，併發症領域的表現較差，可能部分來自 prompt 沒有針對「術前已有 vs 術後新發」做區分；論文沒有測試這個假設。
- **模型版本已過時** — 推論在 2025 年 2–4 月完成，用的是當時的模型快照（含 gemini-2.0-flash-exp 這類實驗版識別碼）；數值適合用來看「任務難度落在哪裡」，不適合直接當成今日模型的效能估計。

## 與書庫其他文章的關係

NSCLC 轉移擷取那篇在單一機構的英文腫瘤病歷上比較微調 GatorTron 與兩個本地零樣本開放權重模型，本篇則在德文神經外科病歷上比較四個雲端模型與兩個本地 70B 模型並加上人工稽核者，兩篇都顯示零樣本病歷抽取在罕見、低盛行率的標籤上最不穩定: [癌症登記缺了 54% 的轉移欄位，病歷補得回來嗎？NSCLC 病歷上，零樣本 MedGemma、Llama 3.1 與微調 GatorTron 的比較](2026-10-19-llm-nsclc-metastasis-extraction-clinical-notes.md)

老年照護構念基準在四家院所比較規則引擎、GPT-4o 與微調小模型，本篇則在單一中心把 GPT-4o 等零樣本模型放到人工稽核者旁邊比較，兩篇合起來看，前者回答「換院所之後哪種方法還站得住」，後者回答「和實際做摘錄的人相比差在哪裡」: [規則引擎、GPT-4o 與微調小模型，誰讀得懂病歷裡的老年照護？四家院所、41 個構念的基準](2026-09-24-llm-geriatric-ehr-multisite-benchmark.md)

## 實務的啟發

- **可借用的設計** — 把「人工稽核者」和「參考標準」分成兩組人：參考標準由較資深的人共識產生，另找實際會做摘錄的人員單獨審閱一次，模型與這些人用同一套參考比較。這比只報模型對參考標準的 F1 更能回答「交給模型會不會比現在的人工流程差」。
- **可借用的量測方法** — 每個設定至少重跑數次並報告「完全一致的比例」與各次的數值範圍；本篇即使 temperature 設 0，一致率仍在 90–99%，DeepSeek-R1 的併發症 F1 三次相差 0.145，單次執行的數字可能誤導。
- **待驗證的警訊** — 術後併發症這類罕見、需要區分「術前已有」與「術後新發」的變項，是零樣本模型與初階人員共同的弱點；在自己的資料上導入前，應針對這類變項單獨抽樣檢查，而不是只看整體 F1。
- **證據強度** — 單一中心、德文、211 位病人、2025 年初的模型快照，模型與人的比較是探索性的；它支持「在這類結構清楚的研究變項上，零樣本雲端 LLM 可達到或高於初階人工稽核者的表現」，不足以支持取代經驗豐富的摘錄者，也不能直接推論到其他語言、科別或目前版本的模型。

## References

- **main** — Spolaore A, Scholl J, Gkampenis A, Machetanz K, Tatagiba M, Naros G. *Large Language Models for Information Extraction from Neurosurgical Clinical Notes: A Benchmark Against Human Auditors*. Machine Learning and Knowledge Extraction. 2026;8(10):328. DOI: 10.3390/make8100328. 全文：<https://www.mdpi.com/2504-4990/8/10/328>。文內引用位置：author block、Abstract、§1 Introduction、§2.1–§2.6、§3.1–§3.5、§4 Discussion、Data Availability Statement、Appendix B.1–B.5；深鏈 [Figure 1](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f001)、[Figure 3](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f003)、[Figure 4](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f004)、[Figure A1](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-f0A1)、[Table A1](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A1)、[Table A4](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A4)、[Table A7](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A7)、[Table A8](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A8)、[Table A9](https://www.mdpi.com/2504-4990/8/10/328#make-08-00328-t0A9)、[Appendix B](https://www.mdpi.com/2504-4990/8/10/328#app2-make-08-00328)。
- **doi** — <https://doi.org/10.3390/make8100328>。
- **code** — <https://github.com/leoamedeo/LLMvsClinicians>（論文 Data Availability Statement 所列；本文未引用其內容）。

[Home](../) · [AI Papers](./)
