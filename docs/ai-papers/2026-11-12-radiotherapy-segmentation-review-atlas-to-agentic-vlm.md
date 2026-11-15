---
parent: AI Papers
nav_order: 1
title: "放療勾畫綜述：VLM 對 nnU-Net 勝負未定，論點改押 CTV"
catalog_id: "arxiv:2611.12085"
editors:
  - "Clare"
refs:
  main:
    title: "Next-Generation Segmentation in Radiotherapy: A Narrative Review from Atlas-Based Methods to Agentic Vision–Language Models"
    url: "https://arxiv.org/abs/2611.12085v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 放療勾畫綜述：VLM 對 nnU-Net 勝負未定，論點改押 CTV

## 來源

- 團隊：Technical University of Munich（TUM Klinikum rechts der Isar 放射腫瘤科、Chair for AI in Healthcare and Medicine）、Universitat de Barcelona BCN-AIM 與 German Consortium for Translational Cancer Research（DKTK）慕尼黑站，6 位作者 Josef A. Buchner（通訊作者）、Richard Osuala、Ayhan Can Erdur、Melissa C. Olufs、Stephanie E. Combs、Jan C. Peeken。[(ref: main title block)](https://arxiv.org/html/2611.12085v1)
- 論文：*Next-Generation Segmentation in Radiotherapy: A Narrative Review from Atlas-Based Methods to Agentic Vision–Language Models*，arXiv:2611.12085v1（eess.IV；physics.med-ph），2026-11-09 提交，目前只有 v1；授權為 arXiv 非專屬散布授權。[(ref: abstract)](https://arxiv.org/abs/2611.12085v1)
- 識別碼：arXiv [2611.12085](https://arxiv.org/abs/2611.12085v1)；DOI [10.48550/arXiv.2611.12085](https://doi.org/10.48550/arXiv.2611.12085)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.12085v1)、[PDF v1](https://arxiv.org/pdf/2611.12085v1)。
- 研究性質：**敘述性綜述（narrative review）**，不是方法或實驗論文。作者明寫沒有做 PRISMA 系統性檢索，文獻以各世代的代表作為錨點、再由作者群依專業判斷挑選「里程碑」；沒有新方法、沒有自己的資料集或量化實驗。文中唯一的自家測試（VoxTell 在院內腦轉移資料上不理解外擴邊界）只有文字描述，沒有數字。[(ref: main §1.1)](https://arxiv.org/html/2611.12085v1#S1.SS1) [(ref: main §6.3)](https://arxiv.org/html/2611.12085v1#S6.SS3)
- 利益揭露：研究經費來自 ERC 與 Else Kröner-Fresenius Foundation；兩位資深作者揭露與 Brainlab、AstraZeneca 等多家廠商的顧問或酬勞關係，其中一位持有 Mevidence GmbH 股份，作者稱與本稿無關。[(ref: main Funding Statement)](https://arxiv.org/html/2611.12085v1#Sx1) [(ref: main Conflict of Interest)](https://arxiv.org/html/2611.12085v1#Sx2)
- 證據邊界：本文引用的數字都是綜述轉述其他研究的結果，以 arXiv v1 的轉述為準，本書庫未逐篇回查原始研究；文中標出綜述引用的文獻編號，方便讀者追查。

**編輯：** Clare

這篇綜述把放療勾畫從 atlas、任務專用 CNN、promptable foundation model 一路整理到視覺語言模型（VLM）與尚未實現的 agentic 系統，並坦白承認：就作者轉述的研究來看，VLM 在影像看得到的結構上還不能說勝過任務專用的 nnU-Net，它真正的賣點被作者押在影像看不到、必須依指引推論的臨床靶區（CTV）上，而目前還沒有任何模型被證明能從指引文字畫出這類靶區。[(ref: main Abstract)](https://arxiv.org/html/2611.12085v1) [(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1) [(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)

## 流程

![綜述內容的結構示意圖，分上下兩排。上排標題為 (a) Methodological generations covered by the review (examples from its Table 1)，五個不同底色的方塊由左到右以實線箭頭相連：灰色「Atlas-based」（Multi-atlas (2006)；Deformable registration + label fusion；Fails with large anatomical deviation；First commercial tools (Elekta ABAS, 2008)）→ 淺藍色「Task-specific CNN」（U-Net, nnU-Net (2021)；TotalSegmentator (2023, 104 CT classes)；Fixed label set；Mostly OAR; some GTV；Clinical workhorse (Mirada DLCExpert, 2018)）→ 淺綠色「Promptable FM」（UniverSeg, MedSAM, SAM-Med3D, nnInteractive；Spatial or example prompts；Class-agnostic；Suited to GTV refinement；Cannot express CTV concepts）→ 淺橘色「Vision-language」（CLIP-Driven Universal, SegVol, BiomedParse, VoxTell；LLMSeg, Radformer: clinical text -> CTV/GTV；No margin concept, guidelines learned implicitly）→ 淺紫色「Agentic (proposed)」（LLM controller + tools；RAG over contouring guidelines；Prompts a 3D VLM；Oncologist approves, refines by text；No system shown yet）。下排標題為 (b) Evaluation dimensions the review argues for beyond DSC，四個白底方塊、彼此無箭頭：「Geometric」（Volumetric DSC；Surface: HD95, MSD；Surface DSC / NSD；Treat all boundary errors as equally important）、「Effort and dose」（Added path length (APL)；Correction time, blinded acceptability；Dosimetric impact (DVH)；Online adaptive timing）、「Prompt adherence」（Counterfactual prompts (e.g. nodal stage, laterality)；Language ablation (with vs. without text)；Semantic invariance (paraphrases agree)）、「Agent and outcome」（Trajectory-level checks of intermediate steps；Graceful degradation；Embedding-space and outcome-linked analysis (hypothesis)）](assets/rt-segmentation-generations-and-evaluation.png)

圖：本書庫依綜述 §2–§8 與 Table 1 的文字重繪的結構示意圖，只含綜述提到的模型名稱、年份與評估概念，未複製論文原圖（論文 Figure 1 為各世代的時間軸，Figure 5 為作者構想的 agentic 勾畫流程，Figure 6 為嵌入空間評估的示意）。[(ref: main Figure 1)](https://arxiv.org/html/2611.12085v1#S1.F1) [(ref: main Figure 5)](https://arxiv.org/html/2611.12085v1#S7.F5) [(ref: main Figure 6)](https://arxiv.org/html/2611.12085v1#S8.F6)

## 背景／問題

綜述的分析框架是放療的三種勾畫任務：危及器官（OAR）主要由影像對比定義；腫瘤體積（GTV）看得到、但邊界常模糊且因人而異；臨床靶區（CTV）在影像上看不到，必須從腫瘤生物學、淋巴引流、分期、病理與手術史推論。作者引用文獻指出 CTV 的觀察者間變異大於 OAR，ESTRO 與 RTOG 等機構因此訂定勾畫指引，而遵循指引可降低變異。[(ref: main §1)](https://arxiv.org/html/2611.12085v1#S1)

作者據此提出全篇的主軸：每一代方法都解決了前一代的部分限制、又帶來新的限制，而越往後的世代越試圖納入「使用者意圖」與臨床文字。作者也直說研究與臨床之間仍有大落差：臨床上用的仍以 atlas 與商用任務專用深度學習工具為主。[(ref: main Abstract)](https://arxiv.org/html/2611.12085v1) [(ref: main §9)](https://arxiv.org/html/2611.12085v1#S9)

作者自稱本篇與 NRG Oncology 對商用深度學習勾畫工具的評估（ref [12]）及另一篇 CNN 勾畫綜述（ref [13]）互補，並主張兩點放療特有的貢獻：一是把勾畫指引當成可更新的外部知識庫、以檢索增強生成（RAG）餵給 agent 的勾畫流程構想；二是一套超越幾何重疊的語言條件模型評估方式。這兩點都是提案，沒有實作或驗證。[(ref: main §1)](https://arxiv.org/html/2611.12085v1#S1)

## 方法摘要

本篇沒有方法，以下整理的是綜述本身的論證結構。

**文獻怎麼選。** 以 U-Net、nnU-Net、SAM、CLIP 等各世代的奠基論文為錨點，往回追其引用、往後追延伸到醫療或放療的工作，再以 PubMed、Google Scholar、arXiv 關鍵字補充；沒有日期限制，但著重 2015 年後、尤其 2023 年後的研究。「里程碑」由作者群依概念新穎性、對後續研究的影響與放療相關性共同判斷，作者承認這反映自身專業與觀點。[(ref: main §1.1)](https://arxiv.org/html/2611.12085v1#S1.SS1)

**五個世代。**

- **Atlas-based** — 以形變配準把專家標註傳到新病人；大型腫瘤或術後變形會讓配準失敗；Elekta ABAS 於 2008 年取得 FDA 510(k)。[(ref: main §2)](https://arxiv.org/html/2611.12085v1#S2)
- **任務專用 CNN** — U-Net 與 nnU-Net 是目前放療勾畫的主力；TotalSegmentator 以 nnU-Net 分割 104 個 CT 解剖結構，但不含 GTV、CTV；Mirada DLCExpert 於 2018 年成為第一個取得 FDA 510(k) 的深度學習勾畫工具。這一代主要用在 OAR，CTV 很少被純視覺模型處理。[(ref: main §3.2)](https://arxiv.org/html/2611.12085v1#S3.SS2)
- **Promptable foundation model** — SAM 把「以提示指定要分什麼」形式化；醫療版本有 MedSAM（2D、逐層框選）、MedSAM 2（把切片當影片幀）、SAM-Med3D（原生 3D、128³ 裁切）、nnInteractive（點、框、塗鴉、套索並可反覆修正）。作者認為空間提示適合 GTV，但無法表達 CTV 這類由指引定義的概念。[(ref: main §4.2)](https://arxiv.org/html/2611.12085v1#S4.SS2) [(ref: main §5)](https://arxiv.org/html/2611.12085v1#S5) [(ref: main §5.2)](https://arxiv.org/html/2611.12085v1#S5.SS2)
- **Vision–language model** — 語言從訓練時的類別先驗（CLIP-Driven Universal）、推論時的類別名稱提示（SegVol）、2D 自由文字定位（BiomedParse）走到原生 3D 的自由文字分割（VoxTell）；針對 CTV 的 LLMSeg 以 LLM 編碼分期、側別等結構化臨床資料，Radformer 則用 GPT-4 摘要病歷、PubMed-BERT 編碼後在多層融合。[(ref: main §6.2)](https://arxiv.org/html/2611.12085v1#S6.SS2) [(ref: main §6.3)](https://arxiv.org/html/2611.12085v1#S6.SS3) [(ref: main §6.4)](https://arxiv.org/html/2611.12085v1#S6.SS4)
- **Agentic（構想）** — 以 LLM 為控制器呼叫分割、配準、報告解析與指引檢索等專門工具。放療中目前的概念驗證是做治療計畫的 GPT-RadPlan，不是勾畫；作者提出的 agentic CTV 流程尚未有人實作。[(ref: main §7.1)](https://arxiv.org/html/2611.12085v1#S7.SS1) [(ref: main §7.2)](https://arxiv.org/html/2611.12085v1#S7.SS2) [(ref: main §7.3)](https://arxiv.org/html/2611.12085v1#S7.SS3)

**評估主張。** 作者把「VLM 比任務專用基線好」拆成四個宣稱：分割品質、介面彈性、跨任務／部位／模態的泛化、不確定性量化，並逐一檢視證據（見〈結果〉）。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)

## 方法詳解

**作者構想的 agentic CTV 流程。** 系統讀入計畫 CT 與病歷，以 RAG 從指引知識庫取出與本次適應症相關的段落，轉成給 3D VLM 的分割提示，產出候選 CTV；放射腫瘤科醫師核准，或以文字、空間提示修正並反覆迭代。作者認為這能解決 LLMSeg、Radformer 的共同問題：指引在訓練時被隱含學進權重，指引更新就得重新訓練。[(ref: main §7.3)](https://arxiv.org/html/2611.12085v1#S7.SS3) [(ref: main Figure 5)](https://arxiv.org/html/2611.12085v1#S7.F5) [(ref: main §6.4)](https://arxiv.org/html/2611.12085v1#S6.SS4)

**作者自己列的失效模式。** 這一段是綜述裡最具體的部分：

- **檢索** — 可能取回過時、不完整或不適用於本地的指引段落，讓輪廓在無聲中依錯誤標準畫出。[(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **理由** — LLM 可能給出檢索來源不支持、但說得很順的理由，反而讓錯誤輪廓顯得可信。[(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **指令遵循** — 綜述轉述 ref [80]：VoxTell 在 NSCLC GTV 上的輸出主要取決於提示中的解剖位置，幾乎不受組織學或分期影響；對 GTV 合理，但代表像淋巴結分期這類應該改變靶區的屬性可能被默默忽略。[(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **錯誤串接與歸責** — 模組串接時，早期錯誤可能被放大或被後段錯誤抵銷，最終看似合理的輪廓無法反映中間步驟是否正確，也讓品管與責任歸屬變得困難。[(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **能力缺口** — 作者寫明，目前的分割 VLM 沒有可靠理解放療專屬概念（如體積外擴），也還沒有模型被證明能從指引文字畫出淋巴引流分區這類子體積；RAG 用在放療勾畫指引這種高度結構化語言上則尚未被研究。[(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)

**作者提出的評估方式。** 對語言條件分割，作者建議三種提示遵循測試：counterfactual prompt evaluation（改分期、換側別或加入高風險子體積，看輸出是否往預期方向、以預期幅度改變）、language ablation（有無文字條件的表現差，衡量有多少表現來自提示）、semantic invariance testing（同義改寫的提示應給出幾何上一致的結果）。對 agentic 系統，建議評估中間步驟的 trajectory-level 正確性與 graceful degradation（遇到分布外輸入時是否標示不確定並交回醫師）。[(ref: main §8.4)](https://arxiv.org/html/2611.12085v1#S8.SS4)

- **論文未交代** — 作者自家 VoxTell 測試的病例數、提示內容與任何量化結果；文中只有「Dice 與專家模型相當，但不懂外擴邊界」的文字描述。[(ref: main §6.3)](https://arxiv.org/html/2611.12085v1#S6.SS3)
- **論文未交代** — 三種提示遵循測試的具體判定門檻（例如輸出要改變多少才算「預期幅度」），以及 agent 中間步驟要如何取得參考答案。[(ref: main §8.4)](https://arxiv.org/html/2611.12085v1#S8.SS4)
- **論文未交代** — 收錄或排除文獻的明確條件以外的篩選紀錄（篩過多少篇、為何排除），這是敘述性綜述的形式限制，作者已自承。[(ref: main §1.1)](https://arxiv.org/html/2611.12085v1#S1.SS1)

## 資料與實驗

本篇沒有自己的資料與實驗。下表整理綜述轉述的量化證據，數字皆為其他研究的結果，括號為綜述引用的文獻編號。[(ref: main §5)](https://arxiv.org/html/2611.12085v1#S5) [(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1) [(ref: main §8.2)](https://arxiv.org/html/2611.12085v1#S8.SS2)

| 比較 | 資料／任務 | 綜述轉述的結果 | 綜述位置 |
|---|---|---|---|
| UniverSeg vs. 任務專用 nnU-Net（[24]） | 留出任務 | mean DSC 0.72 vs. 0.84 | §4.2 |
| 現成 MedSAM vs. nnU-Net（[61]） | 骨盆 MRI OAR | 膀胱差 0.15、直腸差 0.08 mean DSC；不連續的雙側結構差 0.37–0.64 | §5、§8.1 |
| nnInteractive、MedSAM 2、SAM 2（[62]） | MRI-Linac 五個腫瘤部位 GTV，多機構 | 所有提示設定平均的 median DSC 0.75、0.70、0.54；未納入全自動的任務專用基線 | §5.2、§8.1 |
| Text-prompted universal model vs. 各資料集 nnU-Net（[91]） | 72 個公開資料集 | 相當，但未超過 | §8.1 |
| 零樣本 VoxTell vs. 微調 nnU-Net（[80]） | 93 例 NSCLC 放療 | mean DSC 0.61 vs. 0.69，統計上無差異；其他零樣本 VLM ≤ 0.25 | §8.1 |
| 文字修正 VoxTell vs. T1c nnU-Net（[92]） | 膠質瘤子區域 | 內部測試 0.80 vs. 0.79；跨資料集 0.55 vs. 0.49，但未加指令的 VoxTell 已 0.53，正確指令只再多 0.02–0.05 | §8.1 |
| Radformer 有無語言特徵（[32]） | RADCURE 頭頸癌 GTV，597 例留出測試 | mean DSC 0.70 → 0.76；單一機構、無外部驗證 | §6.4 |
| VoxTell vs. SegVol（[33]） | 肺立體定位放療 GTV，報告原文作提示 | DSC 約 0.5，明顯高於 SegVol | §6.3 |
| 幾何指標 vs. 修正時間（[96]） | 20 位肺癌病人的胸腔 OAR | 與絕對修正時間相關：APL R=0.87、surface DSC R=−0.69、HD R=0.64、volumetric DSC R=−0.32 | §8.2 |

**綜述的 Table 1：代表性方法比較。** 下表重製論文 Table 1（作者註明 SAM／SAM 2、TransUNet、UNETR、MedSAM 2、BiomedParse-V 在正文討論、表中省略）。[(ref: main Table 1)](https://arxiv.org/html/2611.12085v1#S1.T1)

| Model | Year | Modality | Input Dim. | Interaction | Role of Language | Label Space | Main Limitation |
|---|---|---|---|---|---|---|---|
| Multi-Atlas Segm. | 2006 | CT, MRI | Native 3D | Automatic | — | Fixed (atlas labels) | Registration fails with large anatomical deviations |
| nnU-Net | 2021 | Any | Auto-config. (2D, 3D, cascade) | Automatic | — | Fixed (per task) | Task-specific training; limited long-range context |
| TotalSegmentator | 2023 | CT | Native 3D | Automatic | — | Fixed (104 classes) | CT only; fixed label set; no CTV support |
| UniverSeg | 2023 | Multi-mod. medical (16 mod.) | 2D (128²) | In-context (support set of image–label pairs) | — | Defined by support set | 2D binary only; quality depends on support set |
| MedSAM | 2024 | Multi-mod. medical | 2D (slice-by-slice) | Interactive (bound. boxes) | — | Class-agnostic | 2D only; per-slice bounding boxes required |
| SAM-Med3D | 2025 | Multi-mod. medical | Native 3D (crop) | Interactive (vol. points) | — | Class-agnostic | Small crop size (128³); sliding-window inference |
| nnInteractive | 2025 | CT, MRI, PET | Native 3D | Interactive, iterative (points, boxes, scribbles, lasso) | — | User prompt-defined spatial label set | No semantic prompting; spatial prompts only |
| CLIP-Driven Univ. | 2023 | CT | Native 3D | Automatic | Label embedd. as semantic regularizer | Fixed (CLIP-enhanced) | No text prompting; fixed class set at inference |
| SegVol | 2024 | CT (partial MRI) | Native 3D | Interactive (points, boxes + text) | Semantic prompts via frozen CLIP (category names) | Semi-open (>200 cat.) | Frozen CLIP encoder limits medical vocabulary |
| BiomedParse | 2025 | Multi-mod. (9 mod.) | 2D only | Automatic (text-prompted) | Free-form text–region grounding | Open-vocabulary | 2D only; no volumetric context |
| LLMSeg | 2024 | CT + clin. metadata | Native 3D | Automatic | Structured clinical context (stage, laterality) via LLM | Fixed (CTV targets) | Structured input only; retraining for guideline updates |
| Radformer | 2025 | CT + clin. record | Native 3D (crop) | Automatic | Unstructured record summarized by GPT-4, embedded via PubMed-BERT; fused at each encoder stage | Fixed (GTV) | GTV only; single-institution data, no external validation |
| VoxTell | 2025 | Multi-mod. medical | Native 3D | Automatic (text-prompted) | Free-form clinical text drives segmentation directly | Open-vocabulary | Lacks RT-specific concepts (e.g., vol. margins) |

## 結果

綜述的「結果」是作者對四個常見宣稱的判斷：

- **介面彈性：有支持** — 作者認為文獻與架構分析支持 VLM 在介面彈性上的優勢，泛化性部分支持。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)
- **分割品質：證據未定** — 依〈資料與實驗〉表中的轉述，VLM 在 OAR 與 GTV 上大致與 nnU-Net 相當或略低；膠質瘤跨資料集的優勢在沒有文字指令時就已存在，作者因此說這個優勢「不是指令引導修正所特有」，也無法區分來自大規模預訓練、文字條件，還是預訓練時看過公開測試資料。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)
- **不確定性量化：幾乎沒測過** — 作者認為語言引導模型在這一項上大多尚未被檢驗；已有的例子是用 Monte Carlo dropout 為術後攝護腺 CTV 產生 95% 信心帶的非語言模型。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1) [(ref: main §6.5)](https://arxiv.org/html/2611.12085v1#S6.SS5)
- **論點改押在 CTV** — 作者明寫，目前支持這類模型的理由不是在看得到的結構上超越 nnU-Net，而是能不重新訓練就分割任意或未見過的結構，以及處理影像模型無法表達、由指引定義的 CTV。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)
- **證據基礎本身有問題** — 同一測試集的比較很少、多由模型開發者自評；多機構研究常只比較 promptable 模型之間、沒有全自動任務專用基線；多數研究只看解剖結構或 GTV、只報幾何指標，且可能與公開預訓練資料重疊。作者因此主張建立一個不在任何公開訓練語料中的放療基準，固定切分、統一參考標準、分開全自動與提示兩條賽道。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)
- **幾何指標不等於臨床影響** — 綜述轉述 HaN-Seg challenge 的分析（ref [98]）：參賽深度學習演算法的幾何準確度與劑量學符合度之間沒有明確相關；作者建議把劑量學評估列為基準測試的必要條件。[(ref: main §8.2)](https://arxiv.org/html/2611.12085v1#S8.SS2)
- **臨床現況** — 綜述轉述一份德語區放療科問卷（ref [112]）：65.7% 已在臨床常規使用 AI 自動勾畫軟體；作者判斷臨床上仍以 atlas 與商用任務專用工具為主，promptable、VLM、agentic 方法多停在概念驗證。[(ref: main §9)](https://arxiv.org/html/2611.12085v1#S9)

## 限制

作者自承的限制：敘述性綜述、非系統性檢索，文獻選擇反映作者群的專業與觀點；VLM 與 agentic 系統的跨機構泛化尚未在臨床部署所需的規模上建立，前瞻驗證資料稀少；基礎模型的法規框架不明，CE 等認證下任何修改都可能需要重新評估，與 agentic 系統「不重訓即可更新」的設計互相牴觸。[(ref: main §1.1)](https://arxiv.org/html/2611.12085v1#S1.SS1) [(ref: main §9)](https://arxiv.org/html/2611.12085v1#S9)

本書庫另外注意到：

- **「里程碑」與作者群的研究重疊** — 綜述引用的 agentic 神經影像系統（ref [75]）、CNN 勾畫綜述（ref [13]）與提示式分割基準（ref [81]）都有本篇作者參與；作者已在 §1.1 承認選文反映自身觀點，讀者在看「代表性方法」時宜留意這一點。[(ref: main §1.1)](https://arxiv.org/html/2611.12085v1#S1.SS1) [(ref: main §7.1)](https://arxiv.org/html/2611.12085v1#S7.SS1) [(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **自家 VoxTell 測試沒有數字** — 「VoxTell 不懂外擴邊界」是本篇多處論證（§6.3、§6.4、§7.4.1）的依據，但只有文字描述；作者另以 ref [81] 的基準支持這一點。這個結論目前只能當作待量化的觀察。[(ref: main §6.3)](https://arxiv.org/html/2611.12085v1#S6.SS3) [(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **多篇被轉述的研究仍是預印本** — 例如 NSCLC 的 VoxTell 對照（ref [80]）、膠質瘤文字修正（ref [92]）與 VoxTell 本身（ref [33]）在參考文獻中都列為 arXiv 預印本，綜述轉述的數字尚未經同儕審查。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)
- **嵌入空間與結果連結是假說** — §8.3 提出以 VLM 輪廓嵌入預測預後、甚至以結果最佳化靶區定義，作者自己標為 hypothesis，並指出需要尚不存在的大型縱向資料與對治療選擇偏差的控制。[(ref: main §8.3)](https://arxiv.org/html/2611.12085v1#S8.SS3)

## 與書庫其他文章的關係

DbC 的作者把 SegVol、SAT 與 VoxTell 這幾個本篇整理的文字提示分割模型當成基線，在肝臟 CT 上微調後比較；本篇則從放療角度指出這些模型理解臨床概念（如外擴邊界）的限制，兩篇並讀可看到同一批模型在診斷與放療兩種用途上的評估: [DbC：先認徵象再組肝病診斷，未見疾病定位六勝、AP 三輸](2026-11-11-diagnosis-by-composition-liver-ct-findings.md)

VoxelSage 是「LLM 呼叫專門工具」的一個實作，把肝腫瘤量測交給程式執行；本篇 §7 構想的 agentic 勾畫系統採同樣的控制器加工具架構，並列出檢索錯誤、理由不實與錯誤串接等失效模式: [VoxelSage：肝腫瘤量測交給程式，成效數字來自二維模擬器](2026-10-06-voxelsage-liver-ct-tool-agent.md)

GE HealthCare 與 Mass General Brigham 的公告要在放療工作流程軟體上探索以自然語言彙整病歷、影像與治療計畫的工具，但生成式 AI 部分沒有任何成效數字；本篇從研究面提出放療 agent 應如何評估，包括中間步驟正確性與失效時是否交回醫師: [GE 擴大研究合作，探索放療工作流程的生成式 AI](../industry-watch/2026-10-15-ge-healthcare-mgb-genai-radiation-therapy.md)

## 實務的啟發

- **可借用的評估清單：三種提示遵循測試** — 若團隊要評估任何吃臨床文字的分割或報告模型，counterfactual prompt、language ablation、semantic invariance 三種測試不需要新資料就能做，能直接回答「模型有沒有在用文字」；這是作者的建議，尚無研究依此建立標準，判定門檻需要自己定。[(ref: main §8.4)](https://arxiv.org/html/2611.12085v1#S8.SS4)
- **待驗證的警訊：Dice 好不代表有聽懂提示** — 作者指出，即使模型完全忽略文字、只靠影像先驗，DSC 仍可能滿分；轉述的 NSCLC 研究也顯示分期與組織學幾乎不影響輸出。在 CTV 這類應依臨床屬性改變的靶區上，只報 DSC 的研究不足以支持「會用臨床資訊」的說法。[(ref: main §8.4)](https://arxiv.org/html/2611.12085v1#S8.SS4) [(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)
- **比較時要放回任務專用基線** — 綜述歸納的證據缺口（缺同一測試集、缺全自動基線、可能與預訓練資料重疊）可直接當作審閱 VLM 分割論文的檢查項目。[(ref: main §8.1)](https://arxiv.org/html/2611.12085v1#S8.SS1)
- **agentic 勾畫目前只是構想** — 本篇沒有實作任何系統；作者自己也認為稽核紀錄、不確定性呈現、可追溯到指引原文與醫師強制驗證應是臨床使用的前提，且嚴格審閱會吃掉部分效率增益。它可以當設計參考，不能當成可行性的證據。[(ref: main §7.4.1)](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)

## References

- **main** — Buchner JA, Osuala R, Erdur AC, Olufs MC, Combs SE, Peeken JC. *Next-Generation Segmentation in Radiotherapy: A Narrative Review from Atlas-Based Methods to Agentic Vision–Language Models*. arXiv:2611.12085v1, 2026. [abstract](https://arxiv.org/abs/2611.12085v1)；[HTML v1](https://arxiv.org/html/2611.12085v1)；[PDF v1](https://arxiv.org/pdf/2611.12085v1)；DOI [10.48550/arXiv.2611.12085](https://doi.org/10.48550/arXiv.2611.12085)
  - 深鏈：[Funding Statement](https://arxiv.org/html/2611.12085v1#Sx1)、[Conflict of Interest](https://arxiv.org/html/2611.12085v1#Sx2)、[§1](https://arxiv.org/html/2611.12085v1#S1)、[Figure 1](https://arxiv.org/html/2611.12085v1#S1.F1)、[Table 1](https://arxiv.org/html/2611.12085v1#S1.T1)、[§1.1](https://arxiv.org/html/2611.12085v1#S1.SS1)、[§2](https://arxiv.org/html/2611.12085v1#S2)、[§3.2](https://arxiv.org/html/2611.12085v1#S3.SS2)、[§4.2](https://arxiv.org/html/2611.12085v1#S4.SS2)、[§5](https://arxiv.org/html/2611.12085v1#S5)、[§5.2](https://arxiv.org/html/2611.12085v1#S5.SS2)、[§6.2](https://arxiv.org/html/2611.12085v1#S6.SS2)、[§6.3](https://arxiv.org/html/2611.12085v1#S6.SS3)、[§6.4](https://arxiv.org/html/2611.12085v1#S6.SS4)、[§6.5](https://arxiv.org/html/2611.12085v1#S6.SS5)、[§7.1](https://arxiv.org/html/2611.12085v1#S7.SS1)、[§7.2](https://arxiv.org/html/2611.12085v1#S7.SS2)、[§7.3](https://arxiv.org/html/2611.12085v1#S7.SS3)、[Figure 5](https://arxiv.org/html/2611.12085v1#S7.F5)、[§7.4.1](https://arxiv.org/html/2611.12085v1#S7.SS4.SSS1)、[§8.1](https://arxiv.org/html/2611.12085v1#S8.SS1)、[§8.2](https://arxiv.org/html/2611.12085v1#S8.SS2)、[§8.3](https://arxiv.org/html/2611.12085v1#S8.SS3)、[Figure 6](https://arxiv.org/html/2611.12085v1#S8.F6)、[§8.4](https://arxiv.org/html/2611.12085v1#S8.SS4)、[§9](https://arxiv.org/html/2611.12085v1#S9)

[Home](../) · [AI Papers](./)
