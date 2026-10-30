---
catalog_id: "doi:10.2196/104586"
editors:
  - "Clare"
refs:
  main:
    title: "Large Language Model–Generated Synthetic Data for Parole and Probation Detection in Clinical Notes: Development and Evaluation Study"
    url: "https://ai.jmir.org/2026/1/e104586"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 一筆真實標註都不用：GPT-4o-mini 生成的 7,579 句合成資料（訓練集 5,305 句），換到 293 份 VA 病歷偵測假釋／緩刑，Llama 3.3-70B 以合成範例 few-shot 達 87% macro-F1、微調的 Llama 3.1-8B 達 81%，encoder 跌到 30%

## 來源

- 團隊：University of Massachusetts Amherst、University of Massachusetts Lowell、美國退伍軍人事務部（US Department of Veterans Affairs，Bedford, MA 與 Washington, DC）、Yale University、The University of Texas at San Antonio Health Science Center，共 6 位作者；第一作者 Avijit Mitra，通訊作者 Jack Tsai。[(ref: main author block)](https://ai.jmir.org/2026/1/e104586)
- 論文：*Large Language Model–Generated Synthetic Data for Parole and Probation Detection in Clinical Notes: Development and Evaluation Study*，JMIR AI 2026;5:e104586，2026-10-19 正式刊出（預印本 2026-06-14 首次公開），授權 CC BY 4.0。[(ref: main)](https://ai.jmir.org/2026/1/e104586)
- 識別碼：DOI [10.2196/104586](https://doi.org/10.2196/104586)。
- 全文：[JMIR AI 全文頁](https://ai.jmir.org/2026/1/e104586)。
- 資料與程式：合成資料集 Synth-PPD 公開於 [Hugging Face](https://huggingface.co/datasets/bio-nlp-umass/Synth-PPD)，程式碼公開於 [GitHub](https://github.com/avipartho/parole_probation_detection_from_EHR)；真實病歷測試集 VA-PPD 受退伍軍人隱私法規限制，需經 VA 研究認證申請。[(ref: main Data Availability)](https://ai.jmir.org/2026/1/e104586)
- 研究性質：完整的開發與評估研究，不是 pilot；所有系統都有實作，在 1,517 句專家審閱的合成測試集與 293 份真實 VA 病歷上評估，報告跨 seed／fold 或重複執行的 SD 與 bootstrap 檢定 P 值，沒有報告信賴區間。單一醫療體系、單一真實測試集。[(ref: main Methods, Evaluation Protocol)](https://ai.jmir.org/2026/1/e104586)
- 證據邊界：本文數值以出版社全文頁的正文與 Table 1–3 為準；生成 prompt、模型參數與標註指引在論文的 Multimedia Appendix 1，本文未納入引述。

**編輯：** Clare

作者只用 GPT-4o-mini 生成、GPT-4.1 篩選的 7,579 句合成筆記（Synth-PPD）訓練或提供範例，不使用任何專家標註的真實病歷，再拿 293 份退伍軍人事務部（VA）真實病歷測試「目前在假釋／目前在緩刑／不明或皆非」三類偵測：以合成範例做 few-shot 提示的 Llama 3.3-70B-Instruct 達 87.22% macro-F1，在合成資料上微調的 Llama 3.1-8B 為 81.43%，最佳關鍵字規則為 77.55%，而在合成測試集上都有 95% 以上的 RoBERTa 類 encoder 在真實病歷只剩約 30%。[(ref: main Abstract, Table 2)](https://ai.jmir.org/2026/1/e104586)

## 流程

![Synth-PPD 假釋／緩刑偵測的研究設計示意圖。由左到右三欄：左欄藍色方塊「1. Synth-PPD (synthetic only)」列出 GPT-4o-mini few-shot 生成 10,014 筆附 label／presence／period 與 rationale 的筆記片段、ROUGE-L 去重（大於 0.7 移除）後 8,266 筆、GPT-4.1 以 LLM-as-a-judge 保留 Likert 3–4 分後 7,579 筆（平均 15.23 字）、70／10／20 分割為訓練 5,305、驗證 757、測試 1,517（測試集由 2 位人類專家審閱）、否定句（presence = no）占 25.1%；藍色方塊以兩條實線箭頭分別指向中欄上方綠色方塊「2a. Unsupervised LLM」（Llama 3.3-70B-Instruct；zero-shot、few-shot、COT、COT+few-shot；範例取自 Synth-PPD 訓練集的最低信心池，k = 15／30／60）與中欄中間綠色方塊「2b. Supervised, trained on Synth-PPD only」（10-fold CV 的 logistic regression、random forest、gradient boosting；3 seeds 的 RoBERTa-base、Clinical RoBERTa-base；prompt-based fine-tuning、3 seeds 的 Qwen2.5-7B、Llama 3.1-8B）；中欄最下方灰色方塊「Rule baselines」（majority class、keyword、keyword + negation）沒有箭頭從藍色方塊連入。中欄三個方塊各以一條實線箭頭指向右欄橘色方塊「3. Evaluation」：類別為 current parole、current probation、unclear or neither，主要指標 macro-F1；in domain 為 Synth-PPD 測試集 n = 1,517（expert-reviewed）；out of domain 為 VA-PPD 293 份 VA CDW 真實病歷（92 parole／84 probation／117 unclear or neither），切成 3 句一段、重疊 1 句的 5,341 段後彙總成病歷層級預測](assets/synth-ppd-parole-probation-workflow.png)

圖：本書庫依論文 Methods 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文 Figure 1 為資料收集流程，Figure 2–4 為非監督與監督設定的流程）。[(ref: main Methods, Figure 1)](https://ai.jmir.org/2026/1/e104586#figure1)

## 背景／問題

病人目前是否在假釋（parole，附條件提前出獄並受監督）或緩刑（probation，法院命令在社區受監督、以避免入監）會影響照護安排與服務銜接；作者引用的先前研究把這類身分與較高的疾病負擔、門診可近性下降，以及較高的心理健康與物質使用治療需求連在一起。這類資訊多半只寫在 intake 與 biopsychosocial 評估等敘述性筆記裡，很少有結構化欄位。[(ref: main Introduction)](https://ai.jmir.org/2026/1/e104586)

作者把 parole and probation detection（PPD）定位成比一般 social and behavioral determinants of health（SBDH）抽取更細的任務：要分辨肯定與否定的提及，也要分辨「目前」與「過去／未來」。他們想回答的是：在完全不用專家標註真實病歷的情況下，只靠 LLM 生成的合成資料，能不能訓練出可以轉移到真實病歷的偵測系統。作者引用先前把合成資料用在 SBDH、驅逐（eviction）偵測等任務的研究作為動機，並指出 PPD 的合成資料尚未被系統性研究；「合成資料可取代專家標註」在本文是被檢驗的命題，不是前提。[(ref: main Introduction)](https://ai.jmir.org/2026/1/e104586)

## 方法摘要

**任務。** 三類分類：目前在假釋、目前在緩刑、不明或皆非（presence = yes 且 period = current 才算前兩類）。[(ref: main Methods, Evaluation Protocol)](https://ai.jmir.org/2026/1/e104586)

**資料。**

- **Synth-PPD（訓練與 in-domain 測試）** — GPT-4o-mini 以 few-shot in-context learning 生成 10,014 筆筆記片段，每筆附 label（parole／probation／unclear）、presence（yes／no／unclear）、period（current／history／future／unclear）與 rationale；ROUGE-L 兩兩相似度大於 0.7 者移除，剩 8,266 筆；再由 GPT-4.1 獨立標註並以 4 分 Likert 量表評估與原標註的一致程度，保留 3–4 分，得 7,579 筆。[(ref: main Methods, Synthetic Dataset Construction)](https://ai.jmir.org/2026/1/e104586)
- **VA-PPD（out-of-domain 測試）** — 從 VHA Corporate Data Warehouse 取 293 份真實病歷，兩位專家獨立標註、裁決不一致；最終 92 份 parole、84 份 probation、117 份不明或皆非。[(ref: main Methods, Real-World Dataset Collection; Table 1)](https://ai.jmir.org/2026/1/e104586#table1)

**系統。** 所有需要訓練的模型只用 Synth-PPD，不碰任何真實病歷標註：

- **非監督 LLM** — Llama 3.3-70B-Instruct 的 zero-shot、few-shot、chain of thought（COT）與 COT+few-shot；範例從 Synth-PPD 訓練集挑。[(ref: main Methods, PPD Framework Design)](https://ai.jmir.org/2026/1/e104586)
- **監督式** — logistic regression、random forest、gradient boosting；RoBERTa-base 與 Clinical RoBERTa-base；以 prompt-based fine-tuning 微調的 Qwen2.5-7B 與 Llama 3.1-8B。[(ref: main Methods, Baselines and Experimental Settings)](https://ai.jmir.org/2026/1/e104586)
- **規則基線** — majority class、關鍵字（出現 "parole" 判 parole、出現 "probation" 判 probation）、關鍵字加否定規則。[(ref: main Methods, Baselines and Experimental Settings)](https://ai.jmir.org/2026/1/e104586)

**指標。** 主要指標為 macro-F1，另報 macro-precision 與 macro-recall；P 值以 bootstrap 檢定計算。[(ref: main Methods, Evaluation Protocol)](https://ai.jmir.org/2026/1/e104586)

## 方法詳解

**LLM-as-a-judge 的評分規則。** GPT-4.1 對每筆合成資料重新標註，與 GPT-4o-mini 的原標註比較：1 分為 presence 不符；2 分為 presence 相符但 label 與 period 都不符；3 分為 label 與 presence 相符、period 不符；4 分為三者皆符。領域專家判定 3、4 分可接受；3 分者的 period 改用 GPT-4.1 的標註。[(ref: main Methods, Synthetic Dataset Construction)](https://ai.jmir.org/2026/1/e104586)

**人工審閱只做在測試集。** 7,579 筆以 70／10／20 分成訓練 5,305、驗證 757、測試 1,517；只有測試集由兩位人類專家審閱並在必要時重新標註，作為 in-domain 評估的標準。作者報告 Synth-PPD 的標註者間一致率為 91%，人類審閱標籤與 LLM 生成標籤的一致率為 90.05%；一致率以兩位標註者同意的比例計算，不是 κ。[(ref: main Methods, Synthetic Dataset Construction)](https://ai.jmir.org/2026/1/e104586)

**VA-PPD 的抽樣與標註。** 至少一半的病歷是用一套既有的 SBDH 偵測系統找出提到法律問題的筆記，再加上 "parole" 與 "probation" 關鍵字過濾挑出；標註沿用 Synth-PPD 的指引，但採簡化方案、只保留 presence = yes 的例子。標註者間一致率 84.21%。[(ref: main Methods, Real-World Dataset Collection)](https://ai.jmir.org/2026/1/e104586)

**長病歷怎麼餵給模型。** 每份 VA-PPD 病歷切成 3 句一段、相鄰兩段重疊 1 句，共 5,341 段，段落層級的預測再彙總成病歷層級分類。[(ref: main Methods, Evaluation Protocol)](https://ai.jmir.org/2026/1/e104586)

**Few-shot 範例怎麼挑。** 模型先以 verbalization-based uncertainty estimation 為訓練集樣本輸出信心分數，範例從信心最低的一批中挑選；主結果用 30 個範例，另比較 15 與 60 個。[(ref: main Methods, PPD Framework Design; Table 3)](https://ai.jmir.org/2026/1/e104586#table3)

**監督式設定。** 任務寫成 multitask、multiple-choice 的問答，以 prompt-based fine-tuning 把 masked token 對應到答案選項；傳統機器學習用 stratified 10-fold cross-validation，其餘模型以 3 個 seed 微調，超參數在 Synth-PPD 驗證集上調整。軟體為 Python 3.12.2 與 PyTorch 2.2.2。[(ref: main Methods, Baselines and Experimental Settings)](https://ai.jmir.org/2026/1/e104586)

- **論文未交代** — 段落預測彙總成病歷層級分類的規則（例如任一段陽性即陽性，或 parole 與 probation 同時出現時的優先順序）。
- **論文未交代** — 非監督 Llama 3.3-70B-Instruct 的結果附有 SD，但正文沒有說明執行了幾次、每次之間改變的是什麼（範例抽樣、解碼隨機性或其他）；正文也沒有給溫度等解碼設定。
- **論文未交代** — 微調的超參數實際數值（learning rate、epoch、batch size、是否使用 LoRA）、關鍵字加否定規則的否定詞清單與視窗大小、傳統機器學習使用的特徵表示；作者表示 prompt 與模型參數在 Multimedia Appendix 1。
- **論文未交代** — VA-PPD 中另一半（非經 SBDH 系統與關鍵字挑出）病歷的抽樣方式、病歷的時間範圍與科別；bootstrap 檢定的重抽次數與比較組合。
- **論文未交代** — 沒有「用真實 VA 標註資料訓練」的對照組，因此無法得知合成資料與等量真實標註之間的差距。

## 資料與實驗

下表摘錄論文 Table 1 的兩個資料集。[(ref: main Table 1)](https://ai.jmir.org/2026/1/e104586#table1)

| 特徵 | Synth-PPD（n=7,579） | VA-PPD（n=293） |
|---|---|---|
| 來源 | GPT-4o-mini | VHA CDW 真實病歷 |
| 驗證者 | GPT-4.1 | 不適用 |
| 標註者 | GPT-4o-mini＋人工 | 人工 |
| 字數，mean (SD) | 15.23 (2.32) | 728.71 (629.01) |
| 字數，median (IQR) | 15 (14–17) | 557 (219–1052) |
| 句數，mean (SD) | 1 (0.01) | 36.17 (32.45) |
| Parole，n (%) | 1,589 (21) | 92 (31.4) |
| Probation，n (%) | 2,920 (38.5) | 84 (28.7) |
| 不明或皆非，n (%) | 3,070 (40.5) | 117 (39.9) |
| 否定（presence = no），n (%) | 1,900 (25.1) | 0 (0) |
| 標註 rationale | 有 | 無 |
| 取得方式 | 公開 | 不公開 |

下表摘錄論文 Table 2 的 macro-F1（%），非監督 LLM 與需要訓練的模型附 SD；所有需要訓練的模型都只用 Synth-PPD 訓練。[(ref: main Table 2)](https://ai.jmir.org/2026/1/e104586)

| 設定 | 系統 | In domain（Synth-PPD 測試集） | Out of domain（VA-PPD） |
|---|---|---|---|
| 規則 | Majority class baseline | 18.11 | 19.02 |
| 規則 | Keyword based | 50.61 | 76.51 |
| 規則 | Keyword+negation rules | 60.72 | 77.55 |
| 非監督 LLM（Llama 3.3-70B-Instruct） | Zero shot | 78.33 (0.10) | 80.10 (0.17) |
| 非監督 LLM（Llama 3.3-70B-Instruct） | Few shot | 90.33 (0.11) | 87.04 (0.16) |
| 非監督 LLM（Llama 3.3-70B-Instruct） | COT | 78.98 (0.60) | 80.40 (0.21) |
| 非監督 LLM（Llama 3.3-70B-Instruct） | COT+few shot | 91.72 (0.30) | 87.22 (1.20) |
| 傳統機器學習 | Logistic regression | 89.88 (0.29) | 55.70 (1.21) |
| 傳統機器學習 | Random forest | 88.72 (0.29) | 54.47 (5.38) |
| 傳統機器學習 | Gradient boosting | 89.86 (0.28) | 35.67 (2.95) |
| Transformer encoder | RoBERTa-base | 95.48 (0.32) | 29.85 (0.55) |
| Transformer encoder | Clinical RoBERTa-base | 96.03 (0.10) | 29.96 (1.17) |
| 監督式 LLM | Qwen2.5-7B | 95.91 (0.39) | 79.38 (2.66) |
| 監督式 LLM | Llama 3.1-8B | 96.07 (0.75) | 81.43 (1.16) |

下表摘錄論文 Table 3：VA-PPD 上 macro-F1（%）隨 few-shot 範例數與合成訓練資料量的變化，括號內為 SD。SFT-Synth-PPD-half／full 指用 50%／100% 的 Synth-PPD 訓練集微調。[(ref: main Table 3)](https://ai.jmir.org/2026/1/e104586#table3)

| 模型 | 設定 | Macro-precision | Macro-recall | Macro-F1 |
|---|---|---|---|---|
| Llama 3.3-70B-Instruct | Zero shot | 83.32 (0.14) | 83.35 (0.16) | 80.10 (0.17) |
| Llama 3.3-70B-Instruct | Few shot—k=15 | 84.55 (0.11) | 85.49 (0.13) | 83.10 (0.17) |
| Llama 3.3-70B-Instruct | Few shot—k=30 | 87.16 (0.14) | 88.43 (0.13) | 87.04 (0.16) |
| Llama 3.3-70B-Instruct | Few shot—k=60 | 86.02 (0.20) | 87.28 (0.22) | 85.90 (0.17) |
| Llama 3.3-70B-Instruct | COT | 83.62 (0.26) | 83.53 (0.07) | 80.40 (0.21) |
| Llama 3.3-70B-Instruct | COT+few shot—k=15 | 84.57 (0.36) | 85.49 (0.24) | 83.25 (0.30) |
| Llama 3.3-70B-Instruct | COT+few shot—k=30 | 87.02 (1.20) | 88.22 (1.14) | 87.22 (1.20) |
| Llama 3.3-70B-Instruct | COT+few shot—k=60 | 86.05 (0.68) | 87.24 (0.67) | 86.18 (0.75) |
| Qwen2.5-7B | SFT-Synth-PPD-half | 78.44 (3.13) | 77.83 (4.46) | 77.40 (4.51) |
| Qwen2.5-7B | SFT-Synth-PPD-full | 79.79 (2.29) | 79.69 (2.62) | 79.38 (2.66) |
| Llama 3.1-8B | SFT-Synth-PPD-half | 70.59 (1.19) | 63.28 (4.65) | 62.13 (5.18) |
| Llama 3.1-8B | SFT-Synth-PPD-full | 81.47 (1.05) | 81.82 (1.02) | 81.43 (1.16) |

## 結果

- **只用合成範例，非監督 LLM 最穩** — Llama 3.3-70B-Instruct 加 COT 與 30 個 Synth-PPD 範例在 VA-PPD 達 87.22% macro-F1，高於自身 zero-shot（80.10%）與最佳規則（77.55%），作者報告所有比較 P<.001；它也高於最佳的監督式模型 Llama 3.1-8B（81.43%，P<.001）。[(ref: main Abstract, Results; Table 2)](https://ai.jmir.org/2026/1/e104586)
- **合成資料微調的 8B 模型** — Llama 3.1-8B 在 VA-PPD 為 81.43%，高於最佳規則（P<.001）；比 zero-shot 的 Llama 3.3-70B-Instruct 高約 1.3 個百分點，但差異不顯著（P=.08）。[(ref: main Abstract, Results)](https://ai.jmir.org/2026/1/e104586)
- **In-domain 高分不代表能轉移** — 兩個 RoBERTa 類 encoder 在合成測試集上有 95.48% 與 96.03%，到 VA-PPD 只剩 29.85% 與 29.96%；三個傳統機器學習模型從約 89–90% 掉到 35.67%–55.70%。兩個監督式 LLM 從約 96% 掉到約 79–81%。[(ref: main Table 2)](https://ai.jmir.org/2026/1/e104586)
- **關鍵字規則在真實病歷反而比較好** — Keyword+negation rules 在 Synth-PPD 為 60.72%，在 VA-PPD 為 77.55%；作者歸因於 VA-PPD 沒有否定例、Synth-PPD 有 25.1% 是否定句。[(ref: main Discussion, Principal Findings; Table 1)](https://ai.jmir.org/2026/1/e104586#table1)
- **範例數有甜蜜點** — few-shot 從 15 增到 30 個時 VA-PPD macro-F1 上升，60 個時略降（無 COT：83.10%、87.04%、85.90%）。作者以 Figure 5 的混淆矩陣說明，在 COT 設定下加入 30 個範例後，parole precision 從 83.02% 升到 87.76%、probation precision 從 68.85% 升到 84.04%，主要是減少偽陽性。[(ref: main Results, Impact of Data Size; Table 3; Figure 5)](https://ai.jmir.org/2026/1/e104586#figure5)
- **合成資料量對小模型的影響不一致** — Llama 3.1-8B 用一半合成訓練資料時 VA-PPD 只有 62.13%（SD 5.18），用全部時 81.43%（P<.001）；Qwen2.5-7B 從 77.40% 到 79.38%，差異不顯著（P=.28）。[(ref: main Results, Impact of Data Size; Table 3)](https://ai.jmir.org/2026/1/e104586#table3)

## 限制

**作者自述的限制。** 真實世界驗證只有一個資料集、293 份 VA 病歷，難以推論到其他醫療體系、院所、科別或時期；VA-PPD 經 SBDH 篩選與關鍵字過濾建立，不一定代表所有臨床文件；Synth-PPD 可能帶有生成模型的偏誤，也未必涵蓋真實病歷的語言多樣性；只測了有限幾個 LLM；encoder 沒有做 domain adaptation，因此無法判斷其落差來自模型本身還是缺乏調適。作者也提醒假釋／緩刑資訊具汙名風險，誤判可能影響退伍軍人取得服務，任何臨床或研究使用前都需要明確的情境與防護。[(ref: main Discussion, Limitations; Principal Findings)](https://ai.jmir.org/2026/1/e104586)

**本書庫的觀察。**

- **合成句與真實病歷的形狀差很多** — Synth-PPD 平均 15.23 字、幾乎都是一句；VA-PPD 平均 728.71 字、36 句。模型在真實病歷上讀的是 3 句一段的切片，加上未說明的彙總規則；encoder 與傳統模型的崩落，可能有一部分來自這種長度與格式的落差，論文沒有分開檢驗。
- **真實測試集沒有測到否定** — VA-PPD 採只保留 presence = yes 的簡化標註方案，否定例為 0，所以「LLM 能分辨否定提及」這項能力只在合成測試集上被評估；關鍵字規則在 VA-PPD 的 77.55% 也因此偏樂觀，換到含否定句的真實病歷可能下降。
- **In-domain 標準與訓練資料出自同一個生成器** — 合成測試集與訓練集都由 GPT-4o-mini 生成、經 GPT-4.1 篩選，人工只審閱測試集；95% 以上的 in-domain 分數主要反映模型學會了合成句的分布，真正有參考價值的是 VA-PPD 的數字。
- **沒有真實資料訓練的對照** — 論文說明合成資料「可取代」專家標註，但沒有用等量 VA 標註資料訓練同一批模型做比較；目前的證據是「合成資料訓練出來的系統勝過關鍵字規則」，不是「合成資料等同真實標註」。
- **百分比的寫法混用** — 正文的提升幅度多為相對百分比（例如 Llama 3.1-8B 比最佳規則「高 5%」，實際是 81.43% 對 77.55%，約 3.9 個百分點；關鍵字加否定規則在 Synth-PPD「高 19.98%」，實際是 60.72% 對 50.61%，約 10.1 個百分點）。本文以表格的絕對數值為準。

## 與書庫其他文章的關係

NSCLC 轉移擷取比較的是零樣本開放權重 LLM 與以真實病歷標註微調的 GatorTron，本篇則完全不用真實標註、只用合成資料訓練或提供範例，兩篇合起來看，可以比較「省掉標註」的兩種做法在真實病歷上各自付出的代價: [癌症登記缺了 54% 的轉移欄位，病歷補得回來嗎？NSCLC 病歷上，零樣本 MedGemma、Llama 3.1 與微調 GatorTron 的比較](2026-10-19-llm-nsclc-metastasis-extraction-clinical-notes.md)

老年照護構念基準在四家院所以真實標註句比較規則引擎、GPT-4o 與微調小模型，本篇則在單一體系上比較規則、encoder 與 LLM 從合成資料轉移到真實病歷的能力，兩篇都顯示病歷抽取的方法排名會隨資料來源改變: [規則引擎、GPT-4o 與微調小模型，誰讀得懂病歷裡的老年照護？四家院所、41 個構念的基準](2026-09-24-llm-geriatric-ehr-multisite-benchmark.md)

時間關係抽取那篇在 i2b2 內部測試上各設定約 86%–89% micro-F1，換到 MACCROBAT 病例報告後掉到 48%–62%，本篇則看到合成資料上分數很高的 encoder 換到真實病歷大幅崩落，兩篇都提醒病歷抽取模型的內部測試分數不能直接當成跨資料來源的表現: [病歷時間關係抽取該怎麼調模型？i2b2 2012 上只調 query／value 的 QLoRA 讓 LLaMA3.1-8B 達 89.15% micro-F1，但每類只給一例時沒有一種做法超過 60%](2026-10-20-llm-clinical-temporal-relation-extraction-adaptation.md)

西語精神科概念偵測那篇的 Mistral-small-psych 也只用合成文件微調，但合成句子源自真實標註片段、並以規則式 tNLP 補標，且有同一基礎模型以真實標註微調的結果可直接對照，可補上本篇缺少的「合成資料對真實標註」比較: [西語精神科病歷裡的 109 個症狀概念，開源 LLM 抓得到嗎？11 個模型零樣本 macro-F1 只有 0.20–0.60，LoRA 微調後 0.75–0.86 才與規則式 tNLP 打平；只用合成資料訓練的 Mistral-small-psych 為 0.79，換到另一家醫院 0.73](2026-10-30-llm-psychiatric-concepts-spanish-ehr.md)

## 實務的啟發

- **可借用的量測方法** — 用合成資料開發病歷抽取模型時，同時報告 in-domain（合成測試集）與 out-of-domain（真實病歷）兩組分數；本篇 encoder 在兩者之間從 96% 掉到 30%，只看合成測試集會完全錯判模型的可用性。
- **可借用的做法** — 以合成資料做 LLM 的 few-shot 範例來源，而不是拿來微調小模型；本篇在 VA-PPD 上，Llama 3.3-70B-Instruct 加 30 個合成範例（87.22%）勝過用全部合成資料微調的 Llama 3.1-8B（81.43%）。這是單一任務、單一真實測試集的結果，換任務前需要複驗。
- **待驗證的警訊** — 真實測試集若是用關鍵字或既有系統挑出來、或標註方案只保留肯定提及，會系統性缺少某些難例（本篇是否定句），讓規則基線與模型都看起來比實際好；建立外部測試集時要檢查抽樣方式是否刪掉了任務的關鍵難點。
- **證據強度** — 單一醫療體系、293 份真實病歷、沒有真實資料訓練的對照與信賴區間；它支持「只用 LLM 合成資料，就能做出在這組 VA 病歷上勝過關鍵字規則的假釋／緩刑偵測系統」，不足以支持合成資料可取代專家標註，也不足以支持直接用於臨床或資格判斷。

## References

- **main** — Mitra A, Druhl E, Goodwin R, Yu H, Stimmel MA, Tsai J. *Large Language Model–Generated Synthetic Data for Parole and Probation Detection in Clinical Notes: Development and Evaluation Study*. JMIR AI. 2026;5:e104586. DOI: 10.2196/104586. 全文：<https://ai.jmir.org/2026/1/e104586>。文內引用位置：author block、Abstract、Introduction、Methods（Synthetic Dataset Construction、Real-World Dataset Collection、PPD Framework Design、Evaluation Protocol、Baselines and Experimental Settings）、Results（Overall Performance、Impact of Data Size）、Discussion（Principal Findings、Limitations）、Data Availability、Table 2；深鏈 [Figure 1](https://ai.jmir.org/2026/1/e104586#figure1)、[Figure 5](https://ai.jmir.org/2026/1/e104586#figure5)、[Table 1](https://ai.jmir.org/2026/1/e104586#table1)、[Table 3](https://ai.jmir.org/2026/1/e104586#table3)。
- **doi** — <https://doi.org/10.2196/104586>。
- **Synth-PPD** — <https://huggingface.co/datasets/bio-nlp-umass/Synth-PPD>。
- **code** — <https://github.com/avipartho/parole_probation_detection_from_EHR>。

[Home](../) · [AI Papers](./)
