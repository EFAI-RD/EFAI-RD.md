---
parent: AI Basics
nav_order: 1
title: "放射報告評估指標：從 BLEU 到 GREEN，三個新分數都拿同 50 例驗證"
category: ai-basics
date: 2026-11-27
catalog_id: "topic:radiology-report-metrics"
editors:
  - "Clara"
refs:
  bleu:
    title: "Bleu: a Method for Automatic Evaluation of Machine Translation"
    url: "https://aclanthology.org/P02-1040/"
  rouge:
    title: "ROUGE: A Package for Automatic Evaluation of Summaries"
    url: "https://aclanthology.org/W04-1013/"
  bertscore:
    title: "BERTScore: Evaluating Text Generation with BERT"
    url: "https://arxiv.org/abs/1904.09675"
  chexpert:
    title: "CheXpert: A Large Chest Radiograph Dataset with Uncertainty Labels and Expert Comparison"
    url: "https://arxiv.org/abs/1901.07031"
  clinically_accurate:
    title: "Clinically Accurate Chest X-Ray Report Generation"
    url: "https://arxiv.org/html/1904.02633v2"
  chexbert:
    title: "CheXbert: Combining Automatic Labelers and Expert Annotations for Accurate Radiology Report Labeling Using BERT"
    url: "https://arxiv.org/html/2004.09167v3"
  radgraph:
    title: "RadGraph: Extracting Clinical Entities and Relations from Radiology Reports"
    url: "https://arxiv.org/abs/2106.14463"
  radgraph_reward:
    title: "Improving the Factual Correctness of Radiology Report Generation with Semantic Rewards"
    url: "https://arxiv.org/html/2210.12186v1"
  radcliq:
    title: "Evaluating progress in automatic chest X-ray radiology report generation"
    url: "https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/"
    doi: "10.1016/j.patter.2023.100802"
  green:
    title: "GREEN: Generative Radiology Report Evaluation and Error Notation"
    url: "https://arxiv.org/html/2405.03595v2"
  ratescore:
    title: "RaTEScore: A Metric for Radiology Report Generation"
    url: "https://arxiv.org/html/2406.16845v2"
  radfact:
    title: "MAIRA-2: Grounded Radiology Report Generation (RadFact section)"
    url: "https://arxiv.org/html/2406.04449v2"
  rexrank:
    title: "ReXrank: A Public Leaderboard for AI-Powered Radiology Report Generation"
    url: "https://arxiv.org/html/2411.15122v2"
status: published
skill_version: "write-ai-basic@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Basics](./)

# 放射報告評估指標：從 BLEU 到 GREEN，三個新分數都拿同 50 例驗證

## 來源

- 本文定位：常青概念文，不是單篇論文筆記。整理放射報告生成（radiology report generation）常見的自動評估指標各自比對什麼、從哪裡來、與放射科醫師的判斷有多一致，以及讀論文時該怎麼看這些分數。
- 觸發的 papers：書庫的報告生成導讀幾乎都同時列 BLEU、CheXbert F1、RadGraph F1、GREEN 等分數，例如病理報告的 CLASP、胸片報告的 ARIVE、RadVLM 分節評估與 MAIRA-2；本篇補上它們共用的指標語言。
- 核心 landmark
  - [Bleu: a Method for Automatic Evaluation of Machine Translation](https://aclanthology.org/P02-1040/)（Papineni、Roukos、Ward、Zhu；ACL 2002）
  - [ROUGE: A Package for Automatic Evaluation of Summaries](https://aclanthology.org/W04-1013/)（Chin-Yew Lin；Text Summarization Branches Out，2004）
  - [BERTScore: Evaluating Text Generation with BERT](https://arxiv.org/abs/1904.09675)（Zhang、Kishore、Wu、Weinberger、Artzi；arXiv 2019，ICLR 2020）
  - [CheXpert](https://arxiv.org/abs/1901.07031)（Irvin 等；AAAI 2019）與 [CheXbert](https://arxiv.org/abs/2004.09167)（Smit 等；EMNLP 2020）
  - [Clinically Accurate Chest X-Ray Report Generation](https://arxiv.org/abs/1904.02633)（Liu 等；arXiv 2019）
  - [RadGraph](https://arxiv.org/abs/2106.14463)（Jain 等；NeurIPS 2021 Datasets and Benchmarks）與 [RadGraph reward](https://arxiv.org/abs/2210.12186)（Delbrouck 等；Findings of EMNLP 2022）
  - [Evaluating progress in automatic chest X-ray radiology report generation](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)（Yu 等；Patterns 4(9):100802，2023，DOI [10.1016/j.patter.2023.100802](https://doi.org/10.1016/j.patter.2023.100802)；提出 RadGraph F1 與 RadCliQ）
  - [GREEN](https://arxiv.org/abs/2405.03595)（Ostmeier 等；arXiv 2024）、[RaTEScore](https://arxiv.org/abs/2406.16845)（Zhao 等；EMNLP 2024）與 [MAIRA-2 的 RadFact](https://arxiv.org/abs/2406.04449)（Bannur 等；arXiv 2024）
  - [ReXrank](https://arxiv.org/abs/2411.15122)（Zhang 等；arXiv 2024，公開排行榜）
- 證據邊界：各指標的定義與與放射科醫師的一致性數字取自各 landmark 原文；GREEN、RaTEScore、ReXrank 與 RadGraph reward 以 arXiv HTML 最新版為準，RadCliQ 以 PMC 全文為準。本文只涵蓋胸片為主的英文報告文獻，CT、病理與其他語言的指標只在書庫導讀中出現。

**編輯：** Clara

放射報告的自動評估從比對字詞重疊（BLEU）走到抽取臨床標籤與實體（CheXbert、RadGraph），再到讓語言模型數錯誤（GREEN）；但 RadCliQ、GREEN 與 RaTEScore 對放射科醫師判斷的一致性，都量在同一份資料上：6 位放射科醫師為 50 個 MIMIC-CXR 測試檢查、200 份候選報告數出的錯誤（ReXVal）。[(ref: radcliq Results)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) [(ref: green §3.4.1)](https://arxiv.org/html/2405.03595v2#S3.SS4.SSS1) [(ref: ratescore §4.2)](https://arxiv.org/html/2406.16845v2#S4.SS2)

## 流程

![左右兩欄圖。左欄標題「(a) Lineage of report-generation metrics (by what is compared)」，五條橫列由上而下、每列左側以彩色粗體寫出比對方式：橘色「Word overlap」列有兩個橘框「BLEU 2002」（n-gram precision + brevity penalty）與「ROUGE 2004」（n-gram / LCS recall）；紫色「Embedding similarity」列有一個寬紫框「BERTScore 2019」（contextual token embeddings）；藍色「Fixed label set」列有「CheXpert labeler 2019」（rules: 14 observations pos / neg / uncertain）以小箭頭連到「CheXbert 2020」（BERT labeler; CE-F1, SembScore）；綠色「Entity & relation graph」列有「RadGraph 2021」（entities + relations (500 annotated reports)）以小箭頭連到「RadGraph reward 2022」（F1 as RL reward）再連到「RadGraph F1 2023」（metric (Yu et al.)）；紅色「Composite / model-based」列有四個框「RadCliQ 2023」（regression on 4 metrics）、「GREEN 2024」（LM counts 6 error types）、「RadFact 2024」（LLM entailment (+ grounding)）、「RaTEScore 2024」（entity NER + embeddings），框之間沒有箭頭。最下方黑色虛線框標「Shared yardstick」，內文為 ReXVal (Yu et al., 2023): 6 radiologists counted errors on 200 reports for 50 MIMIC-CXR test studies; used to fit RadCliQ and to validate GREEN and RaTEScore。右欄標題「(b) Agreement on ReXVal, 200 reports (GREEN paper, Table 6)」，橫條圖由上而下：QAFactEval 0.32、AlignScore 0.32、BLEU 0.35、BERTScore 0.49、ROUGE-L 0.56、F1RadGraph 0.57 為灰色；RadCliQ-v1* 0.61 為淺紅；GREEN 0.63 與 GREEN GPT-4 0.64 為深紅；Error count GREEN 0.79 為更深的紅；Inter-Expert 0.81 為近黑色；橫軸「Kendall's tau with radiologists' total error count」，下方註「* RadCliQ was fitted on 160 of these 200 reports」。](assets/radiology-report-metrics-lineage.png)

*圖：本書庫依各 landmark 原文自繪，未轉載原圖。左欄依「比對的是什麼」分列；只有同一列中有直接延續關係的方法以箭頭相連（CheXpert labeler → CheXbert；RadGraph 資料集 → RadGraph reward → RadGraph F1 指標），其餘框只按年份排列。右欄數值取自 [GREEN 表 6](https://arxiv.org/html/2405.03595v2#S4.T6)；RadCliQ-v1 是在同一批報告中的 160 份上擬合的（[RadCliQ 論文 Composite metric 一節](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)），所以它在這張表的分數不是獨立驗證。*

## 為何需要

一份放射報告的價值在於臨床事實是否正確：有沒有寫出該寫的發現、有沒有寫出不存在的發現、位置與嚴重度對不對。Yu 等人指出，多數報告生成研究沿用一般自然語言生成的指標，把報告當成一般文字；連為放射專門設計的指標，過去也不一定與放射科醫師一致，因此分數進步不一定代表臨床上有意義的進步。[(ref: radcliq Introduction)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)

人工閱讀又貴又慢：Yu 等人的研究動用 6 位放射科醫師，也只評了 50 個檢查、200 份候選報告；而且同一份報告在不同醫師之間常得到不同分數，作者把這列為主要限制。[(ref: radcliq Discussion)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) 自動指標要解決的就是「每次訓練、每個模型都能算」的問題，代價是它只能量到它設計要比對的那一部分。

## 核心概念

1. **Word overlap（字詞重疊）** — BLEU 計算候選文字與參考文字的 modified n-gram precision，取到長度 N 的幾何平均，再乘上以整個語料計算的 brevity penalty，避免候選寫太短也拿高分；它原本為機器翻譯設計。[(ref: bleu)](https://aclanthology.org/P02-1040/) ROUGE 則以 recall 為主，ROUGE-N 是 n-gram recall，ROUGE-L 用最長共同子序列，原本為摘要設計。[(ref: rouge)](https://aclanthology.org/W04-1013/)
2. **Embedding similarity（表徵相似度）** — BERTScore 不要求字面相同，而是用 contextual embeddings 計算候選與參考每個 token 的相似度；原論文以 363 個機器翻譯與影像描述系統的輸出評估，報告它比既有指標更貼近人類判斷。[(ref: bertscore)](https://arxiv.org/abs/1904.09675)
3. **Fixed label set（固定標籤集）** — 先用報告標註器把報告轉成固定標籤，再比對標籤。CheXpert labeler 以規則從報告抽出 14 個觀察的有無，並處理不確定與否定語句；CheXbert 改用 BERT，先學規則標註器的標籤、再以少量放射科醫師標註微調，對 13 個觀察輸出 blank／positive／negative／uncertain，加上 No Finding。[(ref: chexpert)](https://arxiv.org/abs/1901.07031) [(ref: chexbert §3.1)](https://arxiv.org/html/2004.09167v3#S3.SS1) 報告生成論文常說的 clinical efficacy（CE）F1，就是比對兩份報告的這些標籤；常見作法只把 positive 當陽性，negative、uncertain 與 blank 都算陰性。[(ref: radcliq Clinically aware performance metrics)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)
4. **Entity & relation graph（實體與關係圖）** — RadGraph 把報告轉成臨床實體（例如 observation、anatomy）與實體間的關係（Suggestive Of、Located At、Modify）。RadGraph F1 比對兩份報告抽出的實體與關係：實體的文字與類型都相同才算吻合，關係則要起訖實體與關係類型都相同，再取實體 F1 與關係 F1 的平均。[(ref: radgraph_reward §2.1)](https://arxiv.org/html/2210.12186v1#S2.SS1) [(ref: radcliq RadGraph metric-oracle)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)
5. **Composite metric（組合指標）** — RadCliQ 不提出新的比對方式，而是以帶限制的線性回歸，把 BLEU、BERTScore、CheXbert 向量相似度與 RadGraph F1 組合起來預測放射科醫師會數到的錯誤數，數值愈低愈好。[(ref: radcliq Composite metric RadCliQ)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)
6. **Model-based error counting（以模型數錯誤）** — GREEN 讓一個小型語言模型比對參考與候選報告，依六類錯誤（多寫的發現、漏寫的發現、位置錯、嚴重度錯、多提比較、漏提比較）分別數出臨床上重要與不重要的錯誤，再以「吻合發現數 ÷（吻合發現數 + 重要錯誤數）」得到 0 到 1 的分數，並附上每個錯誤的文字說明。[(ref: green §3.2)](https://arxiv.org/html/2405.03595v2#S3.SS2) RadFact 則用 LLM 判斷生成報告的每一句是否被參考報告蘊含（logical precision），反向得到 recall；若句子帶有影像位置，再檢查位置是否也被蘊含。[(ref: radfact)](https://arxiv.org/html/2406.04449v2#Sx2.SSx6)

## 發展譜系與 landmark

| 年份 | Landmark | 據原文的主要貢獻 |
|---|---|---|
| 2002 | [BLEU](https://aclanthology.org/P02-1040/) | modified n-gram precision 的幾何平均乘上 brevity penalty，為機器翻譯設計的自動指標。[(ref: bleu)](https://aclanthology.org/P02-1040/) |
| 2004 | [ROUGE](https://aclanthology.org/W04-1013/) | ROUGE-N、ROUGE-L 等以 recall 為主的摘要評估套件。[(ref: rouge)](https://aclanthology.org/W04-1013/) |
| 2019 | [CheXpert](https://arxiv.org/abs/1901.07031) | 224,316 張胸片、65,240 位病人的資料集，以及從報告抽出 14 個觀察、含不確定標籤的規則標註器。[(ref: chexpert)](https://arxiv.org/abs/1901.07031) |
| 2019 | [Clinically Accurate CXR Report Generation](https://arxiv.org/abs/1904.02633) | 以 CheXpert 標註器比對生成與參考報告在 14 個類別上的標註來評估臨床正確性，並把同一個標註器放進強化學習的 Clinically Coherent Reward。[(ref: clinically_accurate §4.2)](https://arxiv.org/html/1904.02633v2#S4.SS2) [(ref: clinically_accurate §3.3)](https://arxiv.org/html/1904.02633v2#S3.SS3) |
| 2019 | [BERTScore](https://arxiv.org/abs/1904.09675) | 以 contextual embeddings 計算 token 相似度，取代精確字面比對。[(ref: bertscore)](https://arxiv.org/abs/1904.09675) |
| 2020 | [CheXbert](https://arxiv.org/html/2004.09167v3) | BERT 報告標註器；14 個觀察的平均 F1 0.798，CheXpert 規則標註器 0.743，放射科醫師基準 0.805。[(ref: chexbert Table 1)](https://arxiv.org/html/2004.09167v3#S3.T1) |
| 2021 | [RadGraph](https://arxiv.org/abs/2106.14463) | 500 份 MIMIC-CXR 報告由放射科醫師標註 14,579 個實體、10,889 個關係，另以模型為 220,763 份報告自動標註。[(ref: radgraph)](https://arxiv.org/abs/2106.14463) |
| 2022 | [RadGraph reward](https://arxiv.org/html/2210.12186v1) | 把 RadGraph 實體與關係的 F1 設計成三種 reward（RG_E、RG_ER、RG_ER-bar），直接拿來訓練報告生成模型；作者報告事實正確性與完整性指標最多提升 14.2% 與 25.3%。[(ref: radgraph_reward §2.2)](https://arxiv.org/html/2210.12186v1#S2.SS2) [(ref: radgraph_reward abstract)](https://arxiv.org/abs/2210.12186) |
| 2023 | [RadGraph F1 與 RadCliQ](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) | 用「metric-oracle」（從訓練集檢索對某指標得分最高的報告）讓 6 位放射科醫師數錯；提出 RadGraph F1 作為指標，並以四個指標組合出 RadCliQ。[(ref: radcliq)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) |
| 2024 | [GREEN](https://arxiv.org/html/2405.03595v2) | 以 GPT-4 為 100,000 組參考／候選報告標註六類錯誤，再微調 7B 以下的開源模型來數錯並解釋。[(ref: green §3.1.1)](https://arxiv.org/html/2405.03595v2#S3.SS1.SSS1) |
| 2024 | [RaTEScore](https://arxiv.org/html/2406.16845v2) | 自建醫療 NER 資料與模型，把報告拆成實體後比較 embeddings，強調同義詞與否定語句；另提出 RaTE-Eval 基準。[(ref: ratescore abstract)](https://arxiv.org/abs/2406.16845) |
| 2024 | [RadFact（MAIRA-2）](https://arxiv.org/html/2406.04449v2#Sx2.SSx6) | 以 LLM 蘊含判斷評估逐句文字與定位，分出 logical、grounding、spatial precision／recall。[(ref: radfact)](https://arxiv.org/html/2406.04449v2#Sx2.SSx6) |
| 2024 | [ReXrank](https://arxiv.org/html/2411.15122v2) | 公開排行榜，同時算 BLEU-2、BERTScore、SembScore、RadGraph-F1、RadCliQ-v1、RaTEScore、GREEN、FineRadScore 八個指標，並以 1/RadCliQ-v1 排序。[(ref: rexrank §3.3)](https://arxiv.org/html/2411.15122v2#S3.SS3) |

### 同一份資料上的一致性

Yu 等人的 Kendall tau（候選報告分數對 6 位放射科醫師平均錯誤數，50 個檢查、200 份報告）：RadGraph F1 0.515、BERTScore 0.511、CheXbert 向量相似度 0.499、BLEU 0.462；以其中 160 份擬合 RadCliQ 後，在保留的 40 份上 RadCliQ 為 0.615（95% CI 0.450–0.749），單一指標為 0.414–0.537。RadCliQ 的係數為 BLEU 0.000、BERTScore −0.370、CheXbert −0.253、RadGraph F1 −0.377，也就是 BLEU 在組合中沒有權重。[(ref: radcliq Results)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)

GREEN 在同一份 200 份報告上報告 Kendall tau：GREEN 0.63、RadCliQ-v1 0.61、F1RadGraph 0.57、ROUGE-L 0.56、BERTScore 0.49、BLEU 0.35；若改用 GREEN 數出的錯誤總數，與醫師錯誤總數的 tau 為 0.79，表中 Inter-Expert 為 0.81。[(ref: green Table 6)](https://arxiv.org/html/2405.03595v2#S4.T6) RaTEScore 同樣在這份資料上報告 0.527，比較對象是 Yu 等人的數字，且作者說明為這份資料的長報告另外調整了權重矩陣。[(ref: ratescore §4.2)](https://arxiv.org/html/2406.16845v2#S4.SS2)

## 與醫療 AI 的連結

- **指標會被拿來當訓練目標** — CheXpert 標註器與 RadGraph F1 都被直接放進強化學習的 reward。[(ref: clinically_accurate §3.3)](https://arxiv.org/html/1904.02633v2#S3.SS3) [(ref: radgraph_reward §2.2)](https://arxiv.org/html/2210.12186v1#S2.SS2) 這時同一個指標再拿來評估，就同時是訓練目標與裁判，分數上升不一定代表報告更好。
- **檢索與共識基準常常很強** — Yu 等人發現，從訓練集檢索對某指標得分最高的報告，在多數指標上勝過當時的報告生成模型；他們也列出隨機檢索一份訓練報告的基準。[(ref: radcliq Discussion)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) 書庫的 CLASP 導讀也看到同樣現象：病理報告基準上，從同院隨機挑 30 份訓練報告取共識，BLEU-4 就有 0.135，與已發表方法相同。[(ref: CLASP §3.1)](https://arxiv.org/html/2611.28576v1#S3.SS1)
- **自動指標第一不等於醫師偏好** — 書庫的 ARIVE 導讀中，模型在 MIMIC-CXR 七項自動臨床指標全拿第一，一位放射科醫師盲評時平均分卻與大得多的通用模型幾乎相同（3.47 對 3.51）。[(ref: ARIVE Table 1)](https://arxiv.org/html/2611.14018v1#S2.T1) [(ref: ARIVE §2.4.1)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1)
- **排行榜把指標組合固定下來** — ReXrank 以 1/RadCliQ-v1 作為主要排序，並在 ReXGradient（10,000 個檢查）、MIMIC-CXR、IU X-ray、CheXpert Plus 上評估；排名因此繼承 RadCliQ 的擬合方式與權重。[(ref: rexrank Figure 2)](https://arxiv.org/html/2411.15122v2#S2.F2) [(ref: rexrank §3.3)](https://arxiv.org/html/2411.15122v2#S3.SS3) [(ref: rexrank abstract)](https://arxiv.org/abs/2411.15122)

## 常見誤解

- **「BLEU 高代表寫得對」** — Yu 等人的 metric-oracle 實驗中，以 BLEU 選出的報告每份平均多寫 0.807 個錯誤發現（含不重要錯誤），以 BERTScore 與 RadGraph F1 選出的分別為 0.477 與 0.427。字詞重疊獎勵的是寫法相似，不是發現正確。[(ref: radcliq Failure modes of metrics)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)
- **「同一個名字就是同一個分數」** — Yu 等人的 BLEU 是 BLEU-2，CLASP 等論文常報 BLEU-4；同樣在 ReXVal 的 200 份報告上，Yu 等人報告 BLEU 的 tau 為 0.462，GREEN 表 6 為 0.35，兩篇都沒有說明差異來源。[(ref: radcliq Textual-based metrics)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) [(ref: green Table 6)](https://arxiv.org/html/2405.03595v2#S4.T6) 「CheXbert 相似度」在 Yu 等人是 CheXbert 模型 CLS embedding 的 cosine，ReXrank 的 SembScore 則定義為 14 個病灶指示向量的 cosine。[(ref: radcliq Clinically aware performance metrics)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) [(ref: rexrank §3.3)](https://arxiv.org/html/2411.15122v2#S3.SS3) GREEN 論文正文寫 RadGraph 的 tau 為 0.47，表 6 為 0.57，本文採表格值。[(ref: green §4.3.1)](https://arxiv.org/html/2405.03595v2#S4.SS3.SSS1)
- **「CE-F1 涵蓋臨床正確性」** — 標籤式指標只看固定的 14 個觀察，位置、嚴重度與比較前片不在其中；常見作法還把 uncertain 一律算陰性。Yu 等人也觀察到以 CheXbert 相似度選出的報告位置錯誤比 BLEU 多（每份 0.227 對 0.113）。[(ref: radcliq Failure modes of metrics)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)
- **「與醫師一致性 0.6 已經很可靠」** — 這些數字來自 50 個檢查、只看 impression 節的胸片報告；RadCliQ 的保留集只有 40 份，95% CI 從 0.450 到 0.749。[(ref: radcliq Composite metric RadCliQ)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) RaTEScore 作者也指出 ReXVal 不論報告長短都直接加總錯誤數，一句話的報告和二十句的報告錯一次得到同樣分數。[(ref: ratescore §4.2)](https://arxiv.org/html/2406.16845v2#S4.SS2)
- **「LLM 數錯誤就沒有變異」** — GREEN 作者指出，即使以決定性解碼產生輸出，錯誤數量仍帶有一定隨機性，與專家之間對細項錯誤數的不一致相呼應；它與專家偏差最大的類別是位置錯誤。[(ref: green §7)](https://arxiv.org/html/2405.03595v2#S7) [(ref: green §4.3.1)](https://arxiv.org/html/2405.03595v2#S4.SS3.SSS1)

## 與書庫其他文章的關係

RadVLM 分節評估在胸片報告上同時算 RadGraph F1、BERTScore 與 CheXbert 相似度，發現 Impression 讀起來更順不代表 Findings 更正確；本篇說明這些指標各自比對什麼、與放射科醫師的一致性從何而來: [報告讀起來愈順，就寫得愈對嗎？RadVLM 的分節評估](../ai-papers/2026-09-22-radvlm-section-based-report-evaluation.md)

ARIVE 在七項自動臨床指標全拿第一、醫師盲評卻與通用大模型打平，是本篇「自動指標第一不等於醫師偏好」的實例: [ARIVE：胸片報告自動指標全拿第一，醫師評分與 Qwen3.5 打平](../ai-papers/2026-11-17-arive-anatomy-interleaved-cxr-report.md)

CLASP 在病理報告基準上顯示同院舊報告取共識就能讓 BLEU-4 追上已發表方法，對應本篇提到的檢索與共識基準問題: [病理報告生成：挑同院舊報告，BLEU-4 就逼近已發表方法](../ai-papers/2026-11-27-clasp-pathology-report-decide-then-decode.md)

MAIRA-2 提出 RadFact，以 LLM 蘊含判斷分開評估文字與定位，是本篇譜系中以模型評估的一支: [MAIRA-2：胸片報告文字對了，定位不一定對](../ai-papers/2026-09-15-maira-2-grounded-reporting.md)

醫療 VLM 譜系文整理模型如何從圖文對齊走到有定位的報告生成，本篇則整理這些報告產出後怎麼被打分: [醫療視覺語言模型：從 CLIP 對齊到有定位報告](medical-vlm.md)

## 實務的啟發

- **跨家族報分數** — 至少同時報一個字詞重疊、一個標籤或實體式、一個以模型數錯誤的指標，並寫清楚版本與實作（BLEU-n、CheXbert 相似度的定義、RadGraph 與 GREEN 的模型版本）；不同論文的同名分數不一定能直接相比。[(ref: radcliq Textual-based metrics)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/) [(ref: rexrank §3.3)](https://arxiv.org/html/2411.15122v2#S3.SS3)
- **加入檢索與共識基準** — 隨機檢索、最相似檢索或同院共識報告都很容易做，能看出模型的分數有多少只是「寫得像一般報告」。[(ref: radcliq Results)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/)
- **訓練目標與評估指標分開** — 若以 RadGraph F1、CheXbert 標籤或某個 LLM judge 當 reward，評估時應另外加上不同家族的指標與人工閱讀。[(ref: radgraph_reward §2.2)](https://arxiv.org/html/2210.12186v1#S2.SS2)
- **看錯誤類型，不只看總分** — 六類錯誤（多寫、漏寫、位置、嚴重度、比較前片的多提與漏提）各自對臨床的影響不同；GREEN 這類指標能輸出分項錯誤，比單一分數更能指出模型哪裡壞。[(ref: green §3.2)](https://arxiv.org/html/2405.03595v2#S3.SS2)
- **把「與醫師一致」當成有邊界的證據** — 現有的一致性數字主要來自 ReXVal 的 50 個胸片檢查；用在 CT、病理或中文報告時，需要自己的人工對照，不能直接沿用。[(ref: green §3.4.1)](https://arxiv.org/html/2405.03595v2#S3.SS4.SSS1)

## References

- `bleu` — Kishore Papineni, Salim Roukos, Todd Ward, Wei-Jing Zhu. *Bleu: a Method for Automatic Evaluation of Machine Translation*. ACL 2002：https://aclanthology.org/P02-1040/
- `rouge` — Chin-Yew Lin. *ROUGE: A Package for Automatic Evaluation of Summaries*. Text Summarization Branches Out, 2004：https://aclanthology.org/W04-1013/
- `bertscore` — Tianyi Zhang, Varsha Kishore, Felix Wu, Kilian Q. Weinberger, Yoav Artzi. *BERTScore: Evaluating Text Generation with BERT*. ICLR 2020：https://arxiv.org/abs/1904.09675
- `chexpert` — Jeremy Irvin et al. *CheXpert: A Large Chest Radiograph Dataset with Uncertainty Labels and Expert Comparison*. AAAI 2019：https://arxiv.org/abs/1901.07031
- `clinically_accurate` — Guanxiong Liu et al. *Clinically Accurate Chest X-Ray Report Generation*. arXiv 2019：https://arxiv.org/abs/1904.02633 ；深鏈：[§3.3](https://arxiv.org/html/1904.02633v2#S3.SS3)、[§4.2](https://arxiv.org/html/1904.02633v2#S4.SS2)
- `chexbert` — Akshay Smit et al. *CheXbert: Combining Automatic Labelers and Expert Annotations for Accurate Radiology Report Labeling Using BERT*. EMNLP 2020：https://arxiv.org/abs/2004.09167 ；深鏈：[§3.1](https://arxiv.org/html/2004.09167v3#S3.SS1)、[Table 1](https://arxiv.org/html/2004.09167v3#S3.T1)
- `radgraph` — Saahil Jain et al. *RadGraph: Extracting Clinical Entities and Relations from Radiology Reports*. NeurIPS 2021 Datasets and Benchmarks：https://arxiv.org/abs/2106.14463
- `radgraph_reward` — Jean-Benoit Delbrouck et al. *Improving the Factual Correctness of Radiology Report Generation with Semantic Rewards*. Findings of EMNLP 2022：https://arxiv.org/abs/2210.12186 ；深鏈：[§2.1](https://arxiv.org/html/2210.12186v1#S2.SS1)、[§2.2](https://arxiv.org/html/2210.12186v1#S2.SS2)
- `radcliq` — Feiyang Yu et al. *Evaluating progress in automatic chest X-ray radiology report generation*. Patterns 4(9):100802, 2023. PMC：https://pmc.ncbi.nlm.nih.gov/articles/PMC10499844/ ；DOI：https://doi.org/10.1016/j.patter.2023.100802
- `green` — Sophie Ostmeier et al. *GREEN: Generative Radiology Report Evaluation and Error Notation*. arXiv:2405.03595v2：https://arxiv.org/abs/2405.03595 ；深鏈：[§3.1.1](https://arxiv.org/html/2405.03595v2#S3.SS1.SSS1)、[§3.2](https://arxiv.org/html/2405.03595v2#S3.SS2)、[§3.4.1](https://arxiv.org/html/2405.03595v2#S3.SS4.SSS1)、[§4.3.1](https://arxiv.org/html/2405.03595v2#S4.SS3.SSS1)、[Table 6](https://arxiv.org/html/2405.03595v2#S4.T6)、[§7](https://arxiv.org/html/2405.03595v2#S7)
- `ratescore` — Weike Zhao et al. *RaTEScore: A Metric for Radiology Report Generation*. EMNLP 2024：https://arxiv.org/abs/2406.16845 ；深鏈：[§4.2](https://arxiv.org/html/2406.16845v2#S4.SS2)
- `radfact` — Shruthi Bannur et al. *MAIRA-2: Grounded Radiology Report Generation*（RadFact 一節）. arXiv:2406.04449v2：https://arxiv.org/html/2406.04449v2#Sx2.SSx6
- `rexrank` — Xiaoman Zhang et al. *ReXrank: A Public Leaderboard for AI-Powered Radiology Report Generation*. arXiv:2411.15122v2：https://arxiv.org/abs/2411.15122 ；深鏈：[Figure 2](https://arxiv.org/html/2411.15122v2#S2.F2)、[§3.3](https://arxiv.org/html/2411.15122v2#S3.SS3)
- 書庫例證的原始來源：CLASP [§3.1](https://arxiv.org/html/2611.28576v1#S3.SS1)；ARIVE [Table 1](https://arxiv.org/html/2611.14018v1#S2.T1)、[§2.4.1](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1)

[Home](../) · [AI Basics](./)
