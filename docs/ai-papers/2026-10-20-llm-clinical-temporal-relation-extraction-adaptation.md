---
catalog_id: "doi:10.2196/89957"
editors:
  - "Clare"
refs:
  main:
    title: "Optimizing Clinical Temporal Relation Extraction With Large Language Models: Comparative Analysis"
    url: "https://medinform.jmir.org/2026/1/e89957"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 病歷時間關係抽取該怎麼調模型？i2b2 2012 上只調 query／value 的 QLoRA 讓 LLaMA3.1-8B 達 89.15% micro-F1，但每類只給一例時沒有一種做法超過 60%

## 來源

- 團隊：The University of Texas Health Science Center at Houston（McWilliams School of Biomedical Informatics）與 Mayo Clinic in Florida（Department of Artificial Intelligence and Informatics），共 8 位作者；第一作者 Jianping He，通訊作者 Cui Tao。[(ref: main author block)](https://medinform.jmir.org/2026/1/e89957)
- 論文：*Optimizing Clinical Temporal Relation Extraction With Large Language Models: Comparative Analysis*，JMIR Medical Informatics 2026;14:e89957，2026-10-15 正式刊出（預印本 2025-12-19 首次公開），授權 CC BY 4.0。[(ref: main)](https://medinform.jmir.org/2026/1/e89957)
- 識別碼：DOI [10.2196/89957](https://doi.org/10.2196/89957)。
- 全文：[JMIR Medical Informatics 全文頁](https://medinform.jmir.org/2026/1/e89957)。
- 資料與程式：2012 i2b2 temporal relations 語料需簽 data use agreement 取得；外部驗證用的 MACCROBAT 公開於 Figshare；論文未提供程式碼連結。[(ref: main Data Availability)](https://medinform.jmir.org/2026/1/e89957)
- 研究性質：完整的方法比較研究，不是 pilot；所有調適策略都有實作，在 i2b2 2012 測試集 27,736 筆時間關係上評估，每個設定跑 3 個 seed 並報告 mean (SD)；沒有信賴區間或顯著性檢定。外部驗證只用單一 seed 的 checkpoint。[(ref: main Methods, Experimental Settings; Table 4)](https://medinform.jmir.org/2026/1/e89957#table4)
- 證據邊界：本文數值以出版社全文頁的正文與 Table 1–14 為準；論文 Multimedia Appendix 1（逐 seed 結果、逐類指標與訓練時間的 XLSX）與 decoder 的 system message 原文未納入引述。

**編輯：** Clare

作者在 2012 i2b2 出院摘要的時間關係抽取（clinical temporal relation extraction，CTRE）上，把兩個 encoder（GatorTron-Base、GatorTron-Large）與兩個 decoder（LLaMA3.1-8B、MeLLaMA-13B）放進 standard fine-tuning、hard-prompting、soft-prompting 與 QLoRA 四種調適策略比較：資料充足時，只在 query 與 value 投影層加 QLoRA 的 LLaMA3.1-8B 以 89.15% micro-F1 最高，但每個關係類別只給一個訓練例時，最好的設定也只有 58.17%，而在外部的 MACCROBAT 病例報告上，最佳模型降到約 62%。[(ref: main Abstract; Table 4; Table 12; Table 14)](https://medinform.jmir.org/2026/1/e89957#table4)

## 流程

![病歷時間關係抽取調適策略比較的研究設計示意圖。由左到右三欄：左欄藍色方塊「1. Data and input」列出 2012 i2b2 temporal relations corpus 的 310 份出院摘要（train 190，以 9:1 再分訓練與驗證；test 120）、DocTimeRel 與 TLINK、8 種原始關係合併為 BEFORE／AFTER／OVERLAP、關係數 train 33,543／test 27,736、輸入為涵蓋兩個論元的最小連續句段並以 [@Subject$] 與 [@Object$] 標記、data-rich 用完整訓練集而 1-shot 每種關係只取一例且驗證與測試集不變；藍色方塊以兩條實線箭頭分別指向中欄上方綠色方塊「2a. Full-parameter (GatorTron-Base only)」（standard fine-tuning 以 [CLS] 接分類頭；hard-prompting 模板 "Subject [MASK] [MASK] Object"，label words 為 happened before／happened overlap／happened after；不量化）與中欄下方綠色方塊「2b. Parameter-efficient (quantized)」（encoder：GatorTron-Base 345M、GatorTron-Large 8.9B；decoder：LLaMA3.1-8B、MeLLaMA-13B，decoder 輸入外包 System Message + "Text:" + input + question；soft-prompting 長度 32／64、backbone 凍結；QLoRA rank 16、alpha 32、dropout 0.1，qv 只調 query 與 value 投影、all 調所有 linear 層）。兩個綠色方塊各以一條實線箭頭指向右欄橘色方塊「3. Evaluation」：每個設定 3 次執行（seeds 1234／42／47）報 mean (SD)；指標 micro-F1（主要）、macro-F1、weighted-F1；內部測試為 i2b2 測試集 27,736 筆關係（data-rich 與 1-shot）；外部驗證為 MACCROBAT（PubMed Central 病例報告）的 1,000 筆平衡子集（333 BEFORE／334 AFTER／333 OVERLAP），直接套用 i2b2 訓練的 checkpoint](assets/ctre-llm-adaptation-strategies.png)

圖：本書庫依論文 Methods 與 Table 1–3 的文字重繪的研究設計示意圖，只含設計層級的計數與設定，不含結果數值，未複製論文原圖（論文 Figure 1、Figure 2 為四種調適策略的架構示意，Figure 3 為 decoder 的 prompt 格式）。[(ref: main Methods; Figure 1; Figure 2)](https://medinform.jmir.org/2026/1/e89957#figure1)

## 背景／問題

時間關係抽取要從病歷自由文字判斷事件與時間表達、或事件與文件撰寫時間之間的先後，用來重建病人時間線；作者指出這類標註的標註者間一致性偏低，因此需要在少量訓練資料下也能維持表現的系統。[(ref: main Introduction)](https://medinform.jmir.org/2026/1/e89957)

作者認為的缺口是：既有研究對 GatorTron 試過 prompt tuning，但沒有評估 LoRA 類的 parameter-efficient fine-tuning（PEFT），也沒有在 i2b2 2012 上做基準；decoder 模型在相關 shared task 多半只做 zero-shot，或沒有納入 LLaMA 3.1 這類較新的模型。作者引用的是 LLM 在一般 NLP 與臨床實體任務上的成果，並未引用 CTRE 專屬的證據；「LLM 加上適當調適能改善 CTRE」在本文是被檢驗的問題，不是已知事實。[(ref: main Introduction)](https://medinform.jmir.org/2026/1/e89957)

## 方法摘要

**任務。** 給定一對論元（事件、時間表達，或文件撰寫時間），判斷兩者關係屬於 BEFORE、AFTER 或 OVERLAP。i2b2 原有 8 種關係依下列方式合併：BEFORE 含 BEFORE、ENDED_BY、BEFORE_OVERLAP；AFTER 含 AFTER、BEGUN_BY；OVERLAP 含 SIMULTANEOUS、OVERLAP、DURING。[(ref: main Methods, Data Preprocessing)](https://medinform.jmir.org/2026/1/e89957)

**模型。** 兩個醫療 encoder：GatorTron-Base（345M）與 GatorTron-Large（8.9B）；一個通用 decoder：LLaMA3.1-8B；一個醫療 decoder：MeLLaMA-13B（LLaMA 2 的持續預訓練版本）。[(ref: main Methods, LLMs Used; Table 2)](https://medinform.jmir.org/2026/1/e89957#table2)

**四種調適策略。**

- **Standard fine-tuning** — 全參數更新，以分類頭輸出三類；只用在 GatorTron-Base。[(ref: main Methods, Standard Fine-Tuning; Table 3)](https://medinform.jmir.org/2026/1/e89957#table3)
- **Hard-prompting** — 在輸入後接 "Subject [MASK] [MASK] Object" 模板，讓 masked LM 在遮罩位置預測 label words（happened before／overlap／after）；全參數，只用在 GatorTron-Base。[(ref: main Methods, Hard-Prompting)](https://medinform.jmir.org/2026/1/e89957)
- **Soft-prompting** — 在輸入嵌入前接長度 32 或 64 的可訓練 prompt embeddings，backbone 凍結；四個模型都測。[(ref: main Methods, Soft-Prompting)](https://medinform.jmir.org/2026/1/e89957)
- **QLoRA** — 在量化模型上加 LoRA 模組（rank 16、alpha 32、dropout 0.1），分成只調 query 與 value 投影層的 QLoRA (qv)，以及調所有 linear 層的 QLoRA (all)；四個模型都測。[(ref: main Methods, LoRA; Table 3)](https://medinform.jmir.org/2026/1/e89957#table3)

**資料情境與指標。** Data-rich 用完整訓練集；1-shot 每種關係只取一個訓練例，驗證集與測試集與 data-rich 相同。主要指標為 micro-F1，另報 macro-F1（三類等權，對樣本最少的 AFTER 類敏感）與 weighted-F1。[(ref: main Methods, Experimental Settings)](https://medinform.jmir.org/2026/1/e89957)

## 方法詳解

**輸入怎麼切。** 兩個論元在同一句時，以該句為上下文；跨句時，保留兩個論元所在句之間的完整句段，也就是涵蓋兩者的最小連續句段。論元前後以 [@Subject$] 與 [@Object$] 標記，所有策略都保留這些標記。[(ref: main Methods, Data Preprocessing)](https://medinform.jmir.org/2026/1/e89957)

**Decoder 也用分類頭。** Decoder 的輸入包成「System Message + "Text: " + 原始輸入 + "The temporal relationship between the subject and object is? <Answer>"」，但輸出仍由分類頭給出三類，不是生成標籤文字；論文 Figure 2 標示 soft-prompting 與 LoRA 兩種設定下分類頭都可訓練。[(ref: main Methods, Fine-Tuning Overview; Figure 2; Figure 3)](https://medinform.jmir.org/2026/1/e89957#figure3)

**量化與否。** 依論文 Table 3 註腳，soft-prompting 與 LoRA 等 PEFT 策略搭配量化模型；standard fine-tuning 與 hard-prompting 為全參數訓練，不量化。[(ref: main Table 3)](https://medinform.jmir.org/2026/1/e89957#table3)

**訓練設定。** Learning rate 在 encoder 為 1e-4、decoder 為 2e-4；data-rich 最多訓練 10 個 epoch、未收斂則延長到 20，few-shot 最多 20、延長到 30，early stopping patience 皆為 3。最大輸入長度 encoder 為 512 token、decoder 為 4,096 token；batch size 與 gradient accumulation 依模型與策略不同（例如 decoder QLoRA 為 batch 4、accumulation 4）。每個設定以 seeds 1234、42、47 各跑一次，硬體為 H100。[(ref: main Methods, Experimental Settings)](https://medinform.jmir.org/2026/1/e89957)

**可訓練參數對齊的比較。** 為了不只比模型大小，作者把可訓練參數相近的設定分組比較：Group A 約 7M–13M（LLaMA3.1-8B 與 MeLLaMA-13B、GatorTron-Large 的 QLoRA (qv)，以及 GatorTron-Base 的 QLoRA (all)），Group B 約 42M–62M（三個較大模型的 QLoRA (all)）。[(ref: main Table 5)](https://medinform.jmir.org/2026/1/e89957#table5)

**外部驗證。** 把 i2b2 上表現最好的 checkpoint 直接套用到 MACCROBAT（200 篇 PubMed Central 病例報告），不再訓練；評估用的是 1,000 筆三類平衡的子集。[(ref: main Methods, External Validation; Table 14)](https://medinform.jmir.org/2026/1/e89957#table14)

- **論文未交代** — decoder 使用的 system message 原文；正文只說它「提供詳細指示」。
- **論文未交代** — 1-shot 訓練例的抽樣方式（隨機或其他、三個 seed 是否抽不同的例子），以及「每種關係」指的是合併後的 3 類或原始的 8 類。
- **論文未交代** — MACCROBAT 的關係如何對應到 BEFORE／AFTER／OVERLAP，以及 1,000 筆平衡子集如何抽樣；外部驗證只用 seed 42 的 checkpoint，沒有 SD。
- **論文未交代** — optimizer、warmup 與 weight decay；訓練集 33,543 筆中 DocTimeRel 與 TLINK 的比例（測試集有 13,317 筆為 section time 關係）。
- **論文未交代** — 程式碼；也沒有對各設定之間的差異做顯著性檢定或信賴區間，作者並提醒各模型的 batch 設定因記憶體限制而不同，跨模型比較需保守解讀。

## 資料與實驗

下表摘錄論文 Table 1 的 i2b2 2012 語料統計（合併為三類後）。[(ref: main Table 1)](https://medinform.jmir.org/2026/1/e89957#table1)

| 項目 | 訓練集 | 測試集 |
|---|---|---|
| 出院摘要（份） | 190 | 120 |
| 事件 | 16,468 | 13,594 |
| 時間表達 | 2,366 | 1,820 |
| 時間關係 | 33,543 | 27,736 |
| BEFORE | 17,513 | 15,113 |
| AFTER | 3,207 | 2,729 |
| OVERLAP | 12,823 | 9,894 |

外部驗證的 MACCROBAT 子集為 1,000 筆：BEFORE 333、AFTER 334、OVERLAP 333。[(ref: main Methods, External Validation)](https://medinform.jmir.org/2026/1/e89957)

下表摘錄論文 Table 5：data-rich 情境下可訓練參數相近的設定比較，數值為 3 次執行的 mean (SD)，單位 %。[(ref: main Table 5)](https://medinform.jmir.org/2026/1/e89957#table5)

| 組別 | 模型與策略 | 可訓練參數 | Micro-F1 | Macro-F1 | Weighted-F1 |
|---|---|---|---|---|---|
| Group A | LLaMA3.1-8b QLoRA (qv) | 7M | 89.15 (0.30) | 84.44 (0.33) | 89.08 (0.30) |
| Group A | MeLLaMA-13b QLoRA (qv) | 13M | 88.04 (2.15) | 82.69 (3.42) | 87.97 (2.21) |
| Group A | GatorTron-Large QLoRA (qv) | 13M | 87.33 (0.19) | 81.00 (0.60) | 87.11 (0.32) |
| Group A | GatorTron-Base QLoRA (all) | 7M | 87.62 (0.24) | 81.76 (0.30) | 87.50 (0.21) |
| Group B | LLaMA3.1-8b QLoRA (all) | 42M | 88.30 (1.18) | 83.39 (1.30) | 88.33 (1.03) |
| Group B | MeLLaMA-13b QLoRA (all) | 62M | 88.94 (0.28) | 84.10 (0.55) | 88.87 (0.32) |
| Group B | GatorTron-Large QLoRA (all) | 58M | 87.31 (0.27) | 81.15 (0.22) | 87.17 (0.25) |

下表摘錄論文 Table 6 與 Table 7：GatorTron-Base 的全參數策略，以及四個模型的 soft-prompting（data-rich），mean (SD)，單位 %。Table 7 中第二到第四個模型區塊的列名在全文頁未標出，此處依論文 Table 2 的模型順序與可訓練參數量（隨模型 feature dimension 遞增）對應。[(ref: main Table 6; Table 7)](https://medinform.jmir.org/2026/1/e89957#table7)

| 模型 | 策略 | 可訓練參數 | Micro-F1 | Macro-F1 | Weighted-F1 |
|---|---|---|---|---|---|
| GatorTron-Base | Standard fine-tuning | 345M | 86.86 (0.44) | 80.49 (0.65) | 86.68 (0.44) |
| GatorTron-Base | Hard-prompting | 345M | 86.10 (0.61) | 80.17 (1.04) | 86.00 (0.63) |
| GatorTron-Base | Soft-prompting 32 | 36K | 71.07 (0.15) | 49.24 (0.13) | 67.62 (0.15) |
| GatorTron-Base | Soft-prompting 64 | 69K | 72.88 (0.60) | 50.60 (0.43) | 69.40 (0.57) |
| GatorTron-Large | Soft-prompting 32 | 125K | 71.65 (0.46) | 49.63 (0.38) | 68.17 (0.48) |
| GatorTron-Large | Soft-prompting 64 | 240K | 70.63 (1.06) | 48.67 (0.93) | 67.00 (1.16) |
| LLaMA3.1-8B | Soft-prompting 32 | 143K | 49.32 (0.30) | 35.35 (1.49) | 44.43 (0.40) |
| LLaMA3.1-8B | Soft-prompting 64 | 274K | 49.31 (0.18) | 35.86 (1.91) | 44.39 (0.69) |
| MeLLaMA-13B | Soft-prompting 32 | 179K | 49.47 (0.42) | 35.67 (2.10) | 44.23 (1.21) |
| MeLLaMA-13B | Soft-prompting 64 | 343K | 50.01 (0.71) | 36.15 (0.85) | 45.19 (1.15) |

下表摘錄論文 Table 10–13 的 1-shot 情境（每種關係一個訓練例），micro-F1 的 mean (SD)，單位 %；soft-prompting 列只列各模型較佳的 prompt 長度；GatorTron-Base 的 QLoRA (qv) 只出現在 Table 10，論文未報告其 macro-F1。[(ref: main Table 10; Table 11; Table 12; Table 13)](https://medinform.jmir.org/2026/1/e89957#table10)

| 模型 | 策略 | Micro-F1 | Macro-F1 |
|---|---|---|---|
| GatorTron-Base | Hard-prompting | 58.17 (4.22) | 34.29 (8.01) |
| GatorTron-Large | Soft-prompting 64 | 56.25 (3.54) | 32.43 (7.01) |
| LLaMA3.1-8B | QLoRA (all) | 55.99 (2.56) | 28.42 (8.36) |
| GatorTron-Base | Standard fine-tuning | 54.08 (0.71) | 23.84 (0.58) |
| LLaMA3.1-8B | QLoRA (qv) | 51.96 (2.01) | 28.94 (5.77) |
| MeLLaMA-13B | QLoRA (all) | 48.18 (10.04) | 21.92 (2.66) |
| GatorTron-Base | Soft-prompting 64 | 47.81 (8.14) | 24.75 (3.93) |
| GatorTron-Base | QLoRA (all) | 45.75 (11.80) | 23.62 (5.30) |
| GatorTron-Base | QLoRA (qv) | 45.70 (11.69) | 未報告 |
| MeLLaMA-13B | QLoRA (qv) | 44.81 (7.85) | 23.94 (4.19) |
| GatorTron-Large | QLoRA (qv) | 41.42 (9.94) | 23.15 (4.15) |
| GatorTron-Large | QLoRA (all) | 39.42 (11.58) | 23.94 (5.36) |
| LLaMA3.1-8B | Soft-prompting 32 | 34.86 (5.40) | 25.18 (2.93) |
| MeLLaMA-13B | Soft-prompting 64 | 33.9 (4.65) | 24.75 (2.70) |

下表摘錄論文 Table 14：在 MACCROBAT 1,000 筆平衡子集的外部驗證，單一 checkpoint，單位 %。[(ref: main Table 14)](https://medinform.jmir.org/2026/1/e89957#table14)

| 模型 | 策略 | Micro-F1 | Macro-F1 | Weighted-F1 |
|---|---|---|---|---|
| LLaMA3.1-8B | QLoRA (all) | 62.40 | 61.59 | 61.58 |
| LLaMA3.1-8B | QLoRA (qv) | 61.60 | 60.43 | 60.42 |
| MeLLaMA-13B | QLoRA (all) | 56.80 | 54.37 | 54.35 |
| MeLLaMA-13B | QLoRA (qv) | 49.80 | 46.56 | 46.55 |
| GatorTron-Base | QLoRA (all) | 59.80 | 57.76 | 57.74 |
| GatorTron-Base | QLoRA (qv) | 61.00 | 59.58 | 59.57 |
| GatorTron-Large | QLoRA (all) | 56.90 | 54.24 | 54.22 |
| GatorTron-Large | QLoRA (qv) | 57.30 | 53.90 | 53.88 |
| GatorTron-Base | Standard fine-tuning | 48.20 | 44.31 | 44.30 |
| GatorTron-Base | Hard-prompting | 51.40 | 48.05 | 48.03 |

## 結果

- **資料充足時，QLoRA 讓 decoder 小幅領先** — LLaMA3.1-8B 的 QLoRA (qv) 以 89.15% micro-F1 最高，MeLLaMA-13B 的 QLoRA (all) 為 88.94%；四個模型的 QLoRA 最佳設定落在 87.33%–89.15%，都高於 GatorTron-Base 的 standard fine-tuning（86.86%）。幾組差距小於一個 SD（例如 LLaMA3.1-8B 的 QLoRA (all) 為 88.30%，SD 1.18），論文未做顯著性檢定。[(ref: main Table 4; Table 5; Table 6)](https://medinform.jmir.org/2026/1/e89957#table4)
- **只調 query／value 夠用** — 在同一模型上，QLoRA (qv) 與 QLoRA (all) 的差距都在 1 個百分點以內，而 qv 的可訓練參數只有 all 的數分之一（LLaMA3.1-8B 為 7M 對 42M）；作者據此把 QLoRA (qv) 定位為計算成本較低、表現有競爭力的選項。[(ref: main Table 4; Table 5; Conclusions)](https://medinform.jmir.org/2026/1/e89957#table5)
- **可訓練參數最少時，encoder 反而較好** — Soft-prompting 只訓練數萬到數十萬個參數，GatorTron 兩個模型約 71%–73% micro-F1，兩個 decoder 只有約 49%–50%。[(ref: main Table 7)](https://medinform.jmir.org/2026/1/e89957#table7)
- **錯在 BEFORE 與 OVERLAP 之間，AFTER 最弱** — 論文對 data-rich 最佳設定的一次執行（seed 47）做錯誤分析，27,736 筆中錯 2,940 筆；最常見的混淆是 BEFORE 與 OVERLAP 互判（904 筆 BEFORE 判成 OVERLAP、623 筆反向），AFTER 類 F1 為 72.78%、recall 69.22%，遠低於 BEFORE 的 93.05% 與 OVERLAP 的 88.25%。[(ref: main Results, Error Analysis; Table 8; Table 9)](https://medinform.jmir.org/2026/1/e89957#table9)
- **每類一例時沒有穩定的贏家** — 1-shot 下 GatorTron-Base 的 hard-prompting 最高（58.17%），比同模型的 standard fine-tuning 高約 4.1 個百分點；但多數設定的 SD 在 4–12 個百分點之間，例如 GatorTron-Base QLoRA (all) 為 45.75%（SD 11.80），排序並不穩。作者也指出 hard-prompting 的好處沒有在所有設定中一致出現。[(ref: main Table 10; Table 12; Table 13; Conclusions)](https://medinform.jmir.org/2026/1/e89957#table12)
- **換到病例報告就掉 25 個百分點以上** — 在 MACCROBAT 上，LLaMA3.1-8B QLoRA (all) 最高，為 62.40% micro-F1，與 i2b2 上同設定的 88.30% 相比低約 26 個百分點；GatorTron-Base 的 standard fine-tuning 只有 48.20%。作者說明這是初步的外部驗證。[(ref: main Results, External Validation Results; Table 14)](https://medinform.jmir.org/2026/1/e89957#table14)
- **與先前研究的比較** — 作者引用先前在同一預定義測試集上最高 82.04% micro-F1 的研究，並說明另一篇報告 85.7% 的研究使用自訂 80/10/10 切分，不能直接比較；作者沒有宣稱新的 state of the art。[(ref: main Discussion)](https://medinform.jmir.org/2026/1/e89957)

## 限制

**作者自述的限制。** 只用 i2b2 2012 一個語料做主要評估、MACCROBAT 做初步外部驗證，文件類型、事件密度與標註指引不同都可能改變表現與排名；採三類關係方案，更細的關係分類會增加歧義並影響 macro-F1 與少數類；decoder 受參數規模限制，更大或經指令微調的臨床 LLM 可能呈現不同模式；soft-prompting 只測了長度 32 與 64，沒有評估 prefix tuning 等其他 PEFT 方法；hard-prompting 的表現可能取決於模板設計；各模型的 batch 設定不同，跨模型比較需保守解讀。[(ref: main Discussion, Limitations)](https://medinform.jmir.org/2026/1/e89957)

**本書庫的觀察。**

- **差距多半落在 SD 之內** — data-rich 下 QLoRA 各設定的 micro-F1 只差 1–2 個百分點，3 次執行的 SD 最高到 2.15，論文沒有檢定；「LLaMA3.1-8B QLoRA (qv) 最佳」比較適合讀成「四個模型加 QLoRA 都在同一個表現帶」，而不是穩定的排名。
- **外部驗證是單一 checkpoint 的單一數字** — MACCROBAT 結果只用 seed 42 的模型、沒有 SD，抽樣與標籤對應方式也未說明；從 i2b2 到病例報告的 25 個百分點以上落差有多少來自文件類型、多少來自標籤對應，無法從論文分開。
- **AFTER 類是瓶頸，但 micro-F1 看不太出來** — AFTER 只占測試關係約 10%（2,729／27,736），最佳設定在這一類的 F1 只有 72.78%；以 micro-F1 為主要指標時，這個弱點被 BEFORE 的大量樣本稀釋，macro-F1 84.69% 比較能反映。
- **Decoder 沒有用生成式輸出** — 本文的 decoder 也是接分類頭做三類分類，結果不能直接推論到用 prompt 讓 LLM 生成答案的做法；soft-prompting 下 decoder 的低分，也可能與這種用法有關，論文未分開檢驗。

## 與書庫其他文章的關係

NSCLC 轉移擷取在真實腫瘤病歷上比較微調 GatorTron-base 與兩個零樣本 LLM，本篇則在 i2b2 時間關係任務上把 GatorTron 與 decoder 放進同一組微調與 PEFT 策略比較，兩篇合起來看可以區分「模型選擇」與「調適方式」各自對病歷抽取表現的影響: [癌症登記缺了 54% 的轉移欄位，病歷補得回來嗎？NSCLC 病歷上，零樣本 MedGemma、Llama 3.1 與微調 GatorTron 的比較](2026-10-19-llm-nsclc-metastasis-extraction-clinical-notes.md)

假釋／緩刑偵測那篇顯示在合成資料上分數很高的 encoder 換到真實病歷會大幅崩落，本篇在 MACCROBAT 外部驗證上也看到各設定從 i2b2 上約 86%–89% 掉到 48%–62%，兩篇都提醒病歷抽取模型的內部測試分數不能直接當成跨資料來源的表現: [一筆真實標註都不用：GPT-4o-mini 生成的 7,579 句訓練資料，換到 293 份 VA 病歷偵測假釋／緩刑，Llama 守在 81–87% macro-F1，encoder 跌到 30%](2026-10-20-llm-synthetic-data-parole-probation-detection.md)

ASA 分級那篇同樣比較 prompting 與 QLoRA，但把問題改成「需要多少在地標籤 LoRA 才划算」，並加入不訓練、只用標籤調門檻的做法，在院內資料上找到約 270 個標籤的交叉點，可補上本篇 data-rich 與 1-shot 兩端之間的中間地帶: [不生成理由、只讀 A–D 選項的機率：Qwen3.5-9B 分 ASA 身體狀態，比生成式提示快約 64 倍，再用 1,000 個在地標籤調三個門檻，κ 只比 LoRA 低約 0.02，標籤再多 LoRA 仍會拉開](2026-10-28-asa-ps-llm-readout-vs-lora.md)

## 實務的啟發

- **可借用的做法** — 有充足標註資料、又要控制運算成本時，可以先試只在 query 與 value 投影層加 QLoRA；本篇在 i2b2 上它與調所有 linear 層的版本差距都在 1 個百分點以內，可訓練參數少很多。這是單一語料、單一任務的結果，換任務前需要複驗。
- **可借用的量測方法** — 比較不同大小的模型時，像本篇的 Table 5 一樣把可訓練參數相近的設定放在同一組，並同時報 micro-F1 與 macro-F1；只看 micro-F1 會掩蓋少數類（本篇的 AFTER）的弱點。
- **待驗證的警訊** — 標註極少時，本篇沒有任何策略超過 60% micro-F1，而且 seed 之間的 SD 常達 5–12 個百分點；若要在少量標註下開發時間關係抽取，結論應以多次重複的平均與變異為準，不要用單次結果挑方法。
- **待驗證的警訊** — 外部病例報告上的表現只有約 48%–62%，代表在 i2b2 出院摘要上調好的模型不能直接搬到其他文件類型；部署前要在目標院所的文件上另建測試集。
- **證據強度** — 單一主語料、3 個 seed、無顯著性檢定與信賴區間、外部驗證為單一 checkpoint；它支持「資料充足時 QLoRA 能讓 8B–13B 模型在 i2b2 時間關係上達到約 88%–89% micro-F1」，不足以支持任何單一模型或策略在臨床時間線重建上已可直接使用。

## References

- **main** — He J, Sun Z, Rasmy L, Yu E, Zhi D, Li H, Li J, Tao C. *Optimizing Clinical Temporal Relation Extraction With Large Language Models: Comparative Analysis*. JMIR Medical Informatics. 2026;14:e89957. DOI: 10.2196/89957. 全文：<https://medinform.jmir.org/2026/1/e89957>。文內引用位置：author block、Abstract、Introduction、Methods（Data Preprocessing、LLMs Used、Fine-Tuning Overview、Standard Fine-Tuning、Hard-Prompting、Soft-Prompting、LoRA、Experimental Settings、External Validation）、Results（Error Analysis、External Validation Results）、Discussion、Limitations、Conclusions、Data Availability；深鏈 [Table 1](https://medinform.jmir.org/2026/1/e89957#table1)、[Table 2](https://medinform.jmir.org/2026/1/e89957#table2)、[Table 3](https://medinform.jmir.org/2026/1/e89957#table3)、[Table 4](https://medinform.jmir.org/2026/1/e89957#table4)、[Table 5](https://medinform.jmir.org/2026/1/e89957#table5)、[Table 7](https://medinform.jmir.org/2026/1/e89957#table7)、[Table 9](https://medinform.jmir.org/2026/1/e89957#table9)、[Table 10](https://medinform.jmir.org/2026/1/e89957#table10)、[Table 12](https://medinform.jmir.org/2026/1/e89957#table12)、[Table 14](https://medinform.jmir.org/2026/1/e89957#table14)、[Figure 1](https://medinform.jmir.org/2026/1/e89957#figure1)、[Figure 3](https://medinform.jmir.org/2026/1/e89957#figure3)。
- **doi** — <https://doi.org/10.2196/89957>。

[Home](../) · [AI Papers](./)
