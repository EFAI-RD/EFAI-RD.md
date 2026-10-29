---
catalog_id: "doi:10.1186/s13244-026-02421-2"
editors:
  - "Clare"
refs:
  main:
    title: "Large language model assistance for report-based carotid plaque AHA classification: a multi-reader study"
    url: "https://link.springer.com/article/10.1186/s13244-026-02421-2"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 把 AHA 分型規則寫進 prompt，8B 本地模型從 38.9% 升到 81.5%：頸動脈斑塊 MRI 報告的 LLM 輔助判讀，四位放射科醫師對文字參考標準的一致率從 69% 升到 85%（8B）與 90%（671B DeepSeek-R1）

## 來源

- 團隊：上海交通大學醫學院附屬上海市第六人民醫院放射科、東華大學資訊與智慧科學學院、同濟大學醫學院附屬上海市東方醫院放射科、淮安市第一人民醫院放射科共 13 位作者；第一作者 Mengfei Wang 與 Yixiao Tang（共同第一作者），通訊作者 Ruipeng Zhang、Xiaoer Wei、Dan Wang、Yuehua Li。[(ref: main author list)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- 論文：*Large language model assistance for report-based carotid plaque AHA classification: a multi-reader study*，Insights into Imaging 第 17 卷、文章編號 264（2026）；2026-03-24 投稿、2026-09-04 接受，授權 CC BY 4.0。[(ref: main)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- 識別碼：DOI [10.1186/s13244-026-02421-2](https://doi.org/10.1186/s13244-026-02421-2)。本篇無 arXiv 預印本。
- 全文：[Springer 全文頁](https://link.springer.com/article/10.1186/s13244-026-02421-2)、[PDF](https://link.springer.com/content/pdf/10.1186/s13244-026-02421-2.pdf)。
- 資料與程式：資料集因隱私限制不公開，可向通訊作者申請；網頁應用、prompt 與部署範本公開於 [GitHub CGP-Plaque](https://github.com/Becomingw/CGP-Plaque)，但不含統計評估流程。[(ref: main Data and Code availability)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- 研究性質：三中心回顧性研究，不是 pilot；方法實際執行在 433 位病人、866 條頸動脈的中文報告上，另有四位放射科醫師的 report-only reader study。參考標準是由報告文字推得的共識分型，不是影像或病理答案；研究沒有事先計算樣本數。[(ref: main Materials and methods, Discussion)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- 證據邊界：本文數值以全文正文與 Table 1–3 為準；補充資料（Table S1–S4，含十個模型的完整清單與逐模型結果、完整 prompt）未納入本文引述，Fig. 5 中只以圖呈現的逐模型數值也未引述。

**編輯：** Clare

作者把頸動脈高解析 MRI（high-resolution MRI，HRMRI）的中文報告交給 LLM 依 modified AHA 分型，發現把分型準則寫進 prompt 後，本地 8B 模型 Qwen3-8B 對文字參考標準的六類一致率從 38.91% 升到 81.52%，四位只看報告的放射科醫師在 AI 輔助下的一致率也從 69.38% 升到 85.31%（Qwen3-8B）與 90.00%（DeepSeek-R1）。[(ref: main Abstract, Results)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

## 流程

![頸動脈斑塊報告分型研究設計示意圖。四個圓角方塊由左到右排成一列，彼此以三支實線箭頭依序相連。藍色方塊「1 Cohort and reference」：3 centers, Jan 2023 - Sep 2024；Carotid HRMRI reports (Chinese text)；762 screened -> 433 patients = 866 vessels (Center A 376, B 28, C 29)；Prompt development: 50 other patients；Reference: text-based consensus (2 readers + senior expert)；Six classes: Normal/I-II, III, IV-V, VI, VII, VIII。綠色方塊「2 Prompting」：Naive prompting (NP)；Criteria-guided prompting (CGP): modified AHA criteria, signal tables, differential rules in the prompt；Step a: map signal descriptions to plaque components (L / R)；Step b: hierarchical exclusion -> one type per vessel。橘色方塊「3 Standalone evaluation」：866 vessels；Rule-based text extraction baseline；10 LLMs, NP vs CGP, incl. Qwen3-8B, DeepSeek-R1 (671B), MedGemma, Gemini 2.5 Pro；Temperature 0.1；Six-class agreement, Type VI sensitivity, AUC; clustered bootstrap；CRFS 1-5 on reasoning text。紫色方塊「4 Report-only reader study」：200 patients / 400 vessels (stratified random sample)；4 radiologists: 2 junior (4-5 y), 2 senior (7-9 y)；Session 1: no AI；Then Qwen3-8B and DeepSeek-R1 (balanced order, 6-week washout)；GEE + Holm; McNemar per reader。](assets/llm-carotid-plaque-study-design.png)

圖：本書庫依論文 Materials and methods 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的整體流程圖為 Fig. 2）。[(ref: main Materials and methods, Fig. 2)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

## 背景／問題

modified AHA 分型依斑塊的組成與表面完整性把頸動脈斑塊分成多個型別，作者引用文獻指出它是標準化的風險分層框架，辨識易損斑塊（例如斑塊內出血）有助於預防腦血管事件，其中 Type VI 斑塊的缺血風險顯著較高，但標準化的實際應用仍有限。[(ref: main Introduction)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

作者另引用文獻指出，放射科醫師對單一影像發現的一致性不錯，對綜合後的結論一致性較差，而把多序列訊號描述「翻譯」成斑塊型別的這一步依賴經驗。論文據此提出：在報告文字這一層介入，用 LLM 協助套用分型準則。「AHA 分型的認知負擔很重」「報告層級的做法取決於報告的完整與一致」「此前沒有研究系統性評估 LLM 輔助報告層級 AHA 推論」三句論文沒有附引用，本文只當成作者的動機陳述與研究缺口。[(ref: main Introduction)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

## 方法摘要

**任務。** 輸入一份頸動脈 HRMRI 報告的文字，為左右兩側血管各給一個 modified AHA 型別，共六類：Normal/Type I–II、III、IV–V、VI、VII、VIII。[(ref: main Materials and methods, Table 1)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**兩種 prompt。** Naive prompting（NP）只要求分型；criteria-guided prompting（CGP）把 modified AHA 準則、訊號特徵表與鑑別規則寫進 prompt，要求模型先把左右側的訊號描述對應到斑塊成分，再依階層式準則排除不適用的型別，最後為每條血管給出一個型別。[(ref: main AI classification framework and prompting strategy)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**兩個實驗。** 一是 standalone 評估：rule-based 文字抽取基線與十個 LLM 在 NP 與 CGP 下分別對 866 條血管分型。二是 report-only reader study：四位放射科醫師先不用 AI 判讀，再分別在 Qwen3-8B 與 DeepSeek-R1 輔助下判讀同一批報告。[(ref: main Materials and methods, Fig. 2)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**指標。** 主要終點是對文字參考標準的六類一致率（vessel level，左右側各算一筆；patient level 為兩側都對），關鍵次要終點是 Type VI 的偵測敏感度；另報告 quadratic-weighted κ、macro F1、判讀時間，以及 1–5 分的 Clinical Reasoning Fidelity Score（CRFS），用來評 AI 寫出的推理文字。[(ref: main Materials and methods, Table 2)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

## 方法詳解

**病例。** 三個中心 2023 年 1 月至 2024 年 9 月連續接受頸動脈 HRMRI 的病人共 762 位，排除曾接受頸動脈介入、影像嚴重偽影、嚴重全身性疾病、雙側皆無斑塊與重複紀錄者，最後 433 位、866 條血管；Center A 占 376 位。掃描儀涵蓋 Siemens Healthineers、Philips、GE Healthcare 與 United Imaging，報告全為中文。另取 Center A 的 50 位病人、與主要世代不重疊，用來開發 prompt。[(ref: main Study design and ethics statement, Fig. 1)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**參考標準。** 一位五年以上經驗的放射科醫師抽出並去識別化報告中的斑塊形態描述；兩位讀者獨立分型（血管層級一致 96.42%，Cohen's κ = 0.95），不一致者先共識討論，仍不一致再交由 20 年經驗的資深專家判定。作者把它定義為「從報告文字能推得的最合理分型」，衡量的是文字到標籤的對應一致性，不是影像或病理上的正確性。[(ref: main Reference standard establishment)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**模型。** Qwen3-8B 是主要受測的輕量本地模型，DeepSeek-R1（671B）作為上界對照，rule-based 文字抽取作為下界基線；其餘探索性對照包括開源通用模型、醫療微調的 MedGemma 與經 API 使用的 Gemini 2.5 Pro，完整清單在補充資料 Table S2。推論設定為 temperature 0.1、max_tokens 8192，本地模型在 GPU 叢集上執行。[(ref: main AI classification framework and prompting strategy)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**Reader study。** 以分層隨機抽樣取 200 位病人（400 條血管）；四位放射科醫師中兩位資淺（4–5 年）、兩位資深（7–9 年），都沒有神經血管影像次專科訓練，只看去識別化的報告文字、不看影像。先做無 AI 判讀，之後以平衡順序做 Qwen3-8B 與 DeepSeek-R1 輔助判讀，兩個 AI 條件之間間隔 6 週 washout。另由三位 10–20 年經驗的資深放射科醫師在不知模型、prompt 與參考標籤的情況下評 CRFS：第一階段三人共評 200 例，第二階段由一人評 150 位病人（300 條血管）的 AI 推理文字。[(ref: main Report-based human–AI collaboration study and clinical reasoning fidelity)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**統計。** 個別讀者的配對比較用 exact McNemar；組別比較用以病人為群集的 logistic GEE，視需要調整左右側與讀者，Holm 校正多重比較；standalone 的 95% CI 以病人層級群集 bootstrap 1,000 次計算；另做事後的檢定力分析與 session 順序的 GEE。[(ref: main Statistical analysis)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

- **論文未交代** — AI 輔助時讀者看到的是什麼：只有型別，還是連同模型的推理文字；正文提到讀者檢視 AI 推理，但沒有描述呈現介面。
- **論文未交代** — 無 AI 判讀與第一個 AI 輔助條件之間是否有 washout；正文只寫兩個 AI 條件之間間隔 6 週。
- **論文未交代** — 分層抽樣所依據的變項（Table 1 註只說為了讓罕見型別有足夠代表）、各排除原因的人數（只在流程圖中）、rule-based 基線的建構方式、判讀時間的量測方式，以及 DAUS 量表的定義與評分者。
- **論文未交代** — 十個模型中有六個只在補充資料列名；各模型的版本識別碼與查詢日期正文未給；standalone 只有 Qwen3-8B 報告了三次重複執行的穩定性。

## 資料與實驗

下表摘錄論文 Table 1 的分中心與子集組成，型別欄為血管數（括號內為百分比）；全世代合計 433 位、平均年齡 65.9 ± 13.4 歲、男性 248 位。[(ref: main Table 1, Baseline cohort characteristics)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

| 子集 | 病人數 | 年齡 mean (SD) | 男性 n (%) | Normal/I–II | III | IV–V | VI | VII | VIII |
|---|---|---|---|---|---|---|---|---|---|
| Center A | 376 | 66.1 (13.71) | 217 (57.71) | 241 (32.05) | 23 (3.06) | 150 (19.95) | 221 (29.39) | 34 (4.52) | 83 (11.04) |
| Center B | 28 | 63.44 (11.31) | 13 (46.43) | 8 (14.29) | 4 (7.14) | 19 (33.93) | 25 (44.64) | 0 (0.00) | 0 (0.00) |
| Center C | 29 | 66.52 (10.86) | 18 (62.07) | 21 (36.21) | 1 (1.72) | 10 (17.24) | 19 (32.76) | 1 (1.72) | 6 (10.34) |
| CRFS study | 150 | 56 (13.91) | 88 (58.67) | 89 (29.67) | 9 (3.00) | 59 (19.67) | 88 (29.33) | 13 (4.33) | 38 (12.67) |
| Reader study | 200 | 55 (12.53) | 102 (51.00) | 120 (30.00) | 9 (2.25) | 65 (16.25) | 133 (33.25) | 16 (4.00) | 57 (14.25) |

下表摘錄論文 Table 2 與 Table 3 的 reader study 結果（vessel level，400 條血管，資淺與資深各兩位）；± 依論文原樣列出。[(ref: main Table 2, Table 3)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

| 指標 | 組別 | No AI | Qwen3-8B | DeepSeek-R1 |
|---|---|---|---|---|
| 六類一致率 (%) | Junior | 61.75 ± 1.00 | 83.12 ± 0.63 | 87.75 ± 0.50 |
| 六類一致率 (%) | Senior | 77.00 ± 1.75 | 87.50 ± 0.75 | 92.25 ± 1.50 |
| 六類一致率 (%) | Overall | 69.38 ± 7.76 | 85.31 ± 2.29 | 90.00 ± 2.51 |
| Quadratic-weighted κ | Junior | 0.041 | 0.603 | 0.714 |
| Quadratic-weighted κ | Senior | 0.421 | 0.722 | 0.836 |
| Quadratic-weighted κ | Overall | 0.231 ± 0.234 | 0.663 ± 0.072 | 0.775 ± 0.064 |
| Macro F1 | Overall | 0.572 ± 0.128 | 0.796 ± 0.046 | 0.855 ± 0.046 |
| Type VI 敏感度 (%) | Junior | 60.9 | 83.8 | 88.7 |
| Type VI 敏感度 (%) | Senior | 70.7 | 83.5 | 88.7 |
| 資深減資淺的一致率差 (pp) | — | 15.25 | 4.38 | 4.50 |
| 資深減資淺的 κ 差 | — | 0.380 | 0.119 | 0.122 |

下表整理正文報告的 standalone 結果（vessel level，866 條血管，括號內為病人群集 bootstrap 95% CI）；其餘模型的逐一數值只在 Fig. 5 與補充資料 Table S4。[(ref: main Standalone AI performance evaluation, Fig. 5)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

| 方法 | Prompt | 六類一致率 (%) | 其他正文報告的數值 |
|---|---|---|---|
| Rule-based 文字抽取 | — | 50.92 | — |
| Qwen3-8B | NP | 38.91 | Type VI 敏感度 0.4% |
| Qwen3-8B | CGP | 81.52 (78.87–84.06) | Type VI 敏感度 80.1%；分中心 82.05／69.64／86.21% |
| Gemini 2.5 Pro | CGP | 84.30 | — |
| DeepSeek-R1 | CGP | 87.41 (85.10–89.61) | Type VI AUC 0.950；分中心 87.90／73.21／94.83% |

## 結果

- **AI 輔助提高讀者對文字參考標準的一致率** — 合併四位讀者從 69.38% 升到 85.31%（Qwen3-8B）與 90.00%（DeepSeek-R1）；個別讀者從 60.75–78.75% 升到 82.50–88.25% 與 87.25–93.75%。資淺組與資深組的組別比較 Holm 校正後 p 皆 < 0.001。[(ref: main Report-based reader study, Table 2)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **病人層級的落差更大** — 兩側都分對的比例，資淺組 41.0% → 71.0% → 78.8%，資深組 59.8% → 80.2% → 87.8%。[(ref: main Report-based reader study)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **資淺與資深的差距縮小** — 一致率差從 15.25 個百分點縮到 4.38 與 4.50，Type VI 敏感度差從 9.80 個百分點變成 −0.30 與 0.00。[(ref: main Table 3)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **主要錯誤型態** — 無 AI 時最常見的錯誤是把 Type VI 判成 IV–V，資淺組 88 筆、資深組 58 筆；DeepSeek-R1 輔助下資淺組降到 21 筆（少 76.1%）。[(ref: main Report-based reader study, Fig. 4)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **AI 也帶進錯誤** — 資淺組 800 筆血管判讀中，有 33 筆（4.1%）無 AI 時正確、有 AI 時改錯，多在過渡型別：IV–V 改成 VI 12 筆、I–II 改成 III 6 筆、VI 改成 IV–V 4 筆；資深組也有類似情形。[(ref: main Report-based reader study)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **時間** — 每例判讀時間無 AI 35.6 秒、Qwen3-8B 輔助 31.9 秒、DeepSeek-R1 輔助 60.0 秒。[(ref: main Report-based reader study, Fig. 3)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **Prompt 比模型大小影響更大** — Qwen3-8B 在 NP 下 38.91%，低於 rule-based 基線 50.92%；改用 CGP 後 81.52%，與 DeepSeek-R1（CGP 87.41%）差 5.89 個百分點。作者據此主張明確寫出準則、而不只是模型規模，是表現的主要決定因素。[(ref: main Standalone AI performance evaluation, Discussion)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **跨中心差異** — CGP 下各模型的一致率在 Center A 為 73–88%、Center B 52–73%、Center C 74–95%；Center B、C 只有 56 與 58 條血管，作者視為描述性結果。[(ref: main Standalone AI performance evaluation)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **穩定性與推理文字** — Qwen3-8B 三次重複執行的 Fleiss' κ 在 CGP 為 0.91、NP 為 0.85；CRFS 第一階段評分者間 ICC(1,2) = 0.917，Qwen3-8B 改用 CGP 後 ≤ 2 分的比例從 43.6% 降到 17.6%、≥ 4 分從 34.5% 升到 72.0%。[(ref: main Standalone AI performance evaluation)](https://link.springer.com/article/10.1186/s13244-026-02421-2)
- **Session 順序** — 事後 GEE 中兩個 AI session 的一致率 88.12% 與 87.19%（p = 0.325），模型與順序的交互作用 p = 0.437。[(ref: main Report-based reader study)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

## 限制

**作者自述的限制。** 參考標準由報告文字共識推得、reader study 只看報告，結果反映的是文字到標籤的對應，不是影像層級的準確度或臨床結局；讀者設計沒有隨機化，無 AI 條件永遠在先，學習效應可能放大 AI 的效益，疲勞效應則可能掩蓋效益，左右側與重複觀察也不完全獨立；報告全為中文，世代以 Center A 為主（376/433），外部樣本有限，雙語分析用的是翻譯後的報告；沒有事先計算樣本數、只有四位讀者；CRFS 第二階段只有一位評分者；AI 在邊界病例會帶進錯誤，輸出不應當成自動決策。作者呼籲在更廣泛臨床使用前做前瞻、多讀者多病例、以影像為終點的驗證。[(ref: main Discussion)](https://link.springer.com/article/10.1186/s13244-026-02421-2)

**本書庫的觀察。**

- **「準確度」其實是「與文字共識一致」** — 參考標準與讀者、模型看的是同一份報告文字，衡量的是把報告描述對應到型別的一致性。報告本身若描述不完整或寫錯，三方會一起錯，這個設計測不出來。
- **六類一致率與 κ 的落差沒有解釋** — 無 AI 時資淺組一致率 61.75%，quadratic-weighted κ 卻只有 0.041；合併讀者 69.38% 對應 κ 0.231。論文沒有討論這個落差，讀者在不同型別之間的錯誤分布只能從 Fig. 4 的 Sankey 圖看出一部分。
- **子集的年齡與全世代差很多** — Reader study 子集平均 55 歲、CRFS 子集 56 歲，全世代與各中心則在 63–67 歲之間；以分層隨機抽樣而言這個差距偏大，論文沒有說明。另外 CRFS 子集的型別欄加總為 296 條血管，與 150 位病人的 300 條不符。
- **DeepSeek-R1 的增益伴隨時間成本** — 一致率最高的條件，每例判讀時間也從 35.6 秒增加到 60.0 秒；Qwen3-8B 則一致率較低、但時間略短。這是兩種不同的取捨，不是單一方向的改善。
- **順序效應只檢查了一半** — 事後 GEE 比較的是兩個 AI session 之間的順序；無 AI 判讀永遠在先，它與 AI 條件之間的學習效應沒有被估計。

## 與書庫其他文章的關係

兩篇都把醫學影像的文字描述交給 LLM、再與既有的規則式分類方法比較；該研究用手術病理當答案，本篇用文字共識當答案，因此本篇的一致率不能和該研究的診斷準確度直接相比: [把超音波描述交給 ChatGPT 判良惡性：300 顆附件腫塊，和 IOTA 規則、ADNEX 與專家差多少？](2026-09-22-chatgpt-adnexal-mass-ultrasound-triage.md)

兩篇都在中文放射報告上把 LLM 與不同經驗的人類讀者放在同一批文字前比較；該研究讓模型挑出報告裡的錯誤，本篇則假設報告正確、讓模型協助把描述對應到分型，報告本身的錯誤正是本篇設計測不到的部分: [中文放射科報告的真實錯誤：八個 LLM 與八位人類讀者，誰抓得出來？](2026-09-22-llm-chinese-radiology-report-error-detection.md)

本篇把 AHA 分型規則寫進 prompt、仍由 LLM 自己套規則，該研究則把醫療計算器的規則寫成程式、LLM 只負責從病歷填入參數，兩篇並讀可對照「規則放在 prompt」與「規則放在程式」兩種把臨床規則交給 LLM 的做法: [算分交給程式、LLM 只抽參數：GPT-5.5 先把 55 個醫療計算器寫成驗證過的 Python 工具，Qwen3-8B 負責從病歷填表，MedCalc-Bench Verified 上 86.73%，剩下的錯多半出在讀病歷](2026-10-20-tool-augmented-llm-medical-calculation.md)

兩篇都讓 LLM 從放射報告文字套用分型規則、參考標準也都是醫師依同一份文字判定；本篇把 AHA 準則寫進 prompt 並與只下指令的 prompt 對照，該研究只用不含規則的零樣本 prompt 比較三種網頁版模型設定，錯誤集中在 CAD-RADS 4B 與 5 這類需要組合多條規則的類別，正好是本篇 criteria-guided prompting 可以檢驗的情境: [三個聊天介面零樣本讀 CCTA 報告分 CAD-RADS：DeepSeek-R1 與 ChatGPT-5 約八成、ChatGPT-4o 54%，900 份高風險報告被降到 3 以下的比例 2.6%–14.1%](2026-10-22-llm-cad-rads-ccta-report-classification.md)

## 實務的啟發

- **可借用的量測方法** — 把「準則寫進 prompt」與「只下指令」並列比較，再加一個 rule-based 基線，可以分開估計 prompt 設計與模型規模各自的貢獻。本篇 Qwen3-8B 在 NP 下低於規則基線、CGP 下高出 30 個百分點，若只報 CGP 的結果，就看不出這個落差。
- **可借用的報告方式** — 除了整體一致率，同時報告「無 AI 時正確、有 AI 後改錯」的筆數與型別（本篇資淺組 4.1%），以及每例判讀時間。這兩項是評估輔助工具時常被省略、但直接影響臨床可用性的數字。
- **待驗證的方向** — 若要在本地部署小模型協助報告分型，本篇支持「把分型準則明確寫進 prompt」值得在地驗證；但目前的證據只到「與文字共識一致」，Center B 只有 52–73% 的結果也提醒換一個中心、換一種報告寫法時需要重新驗證。
- **證據強度** — 三中心回顧性研究、以單一中心為主、四位讀者、非隨機的判讀順序、文字參考標準；它支持「準則導向 prompt 能提高報告文字到 AHA 型別的對應一致性」，不足以支持影像層級的診斷準確度或臨床結局的改善。

## References

- **main** — Wang M, Tang Y, Yang Y, Tu Y, Cao Z, Ling R, Sun K, Ma J, Zhang Z, Zhang R, Wei X, Wang D, Li Y. *Large language model assistance for report-based carotid plaque AHA classification: a multi-reader study*. Insights into Imaging 17:264 (2026). DOI: 10.1186/s13244-026-02421-2. 全文頁：<https://link.springer.com/article/10.1186/s13244-026-02421-2>。文內引用位置：author list、Abstract、Introduction、Materials and methods（Study design and ethics statement、Reference standard establishment、AI classification framework and prompting strategy、Report-based human–AI collaboration study and clinical reasoning fidelity、Statistical analysis）、Results（Baseline cohort characteristics、Report-based reader study、Standalone AI performance evaluation）、Discussion、Data and Code availability、Table 1、Table 2、Table 3、Fig. 1–5。
- **pdf** — PDF 版：<https://link.springer.com/content/pdf/10.1186/s13244-026-02421-2.pdf>。
- **doi** — <https://doi.org/10.1186/s13244-026-02421-2>。
- **code** — CGP-Plaque（MIT 授權）：<https://github.com/Becomingw/CGP-Plaque>。

[Home](../) · [AI Papers](./)
