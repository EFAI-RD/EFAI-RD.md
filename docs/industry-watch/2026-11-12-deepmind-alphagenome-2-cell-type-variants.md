---
parent: Industry Watch
nav_order: 1
title: "AlphaGenome 2：變異效應預測從組織平均走到細胞類型"
category: industry-watch
date: 2026-11-12
updated: 2026-11-12
tags: [Google-DeepMind, AlphaGenome, genomics, variant-effect-prediction, single-cell, GWAS, regulatory-variant, cell-type-specificity, rare-disease, research-use-only, Antigravity]
catalog_id: "google-deepmind:alphagenome-2-launch-2026-11-11"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.1"
source:
  orgs:
    - "Google DeepMind"
  event: "Google DeepMind 發布 AlphaGenome 2，把 DNA 變異效應預測的解析度從組織平均推進到單一細胞類型，並開放非商業研究以 API 取用"
  event_date: "2026-11-11"
  official_url: "https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/"
  single_source: true
  single_org: true
related_articles:
  - path: "2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md"
    relation: "本則公告結尾預告 AlphaGenome 2 Skills 將進入 Google Antigravity，與該則是同一條路線的兩端：該則示範的是代理式平台怎麼串起既有的化學工具，本則是即將被串進去的專用科學模型本身"
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "該則提到 Antigravity 可接的三十多個生命科學資料庫中包含 1PB 的 AlphaGenome Atlas，而那個 Atlas 正是本則模型的前一代對全基因體預先算出的產物；兩則合看可見同一條「模型 → 預算好的資產 → 接進代理式平台」的建置順序"
  - path: "2026-11-05-google-health-ai-evaluation-framework.md"
    relation: "同一家公司相隔一週的兩則發布，一則談健康 AI 該用哪些方法評估、門檻由各團隊自訂，一則是實際發布的模型與它所公布的評估範圍；並讀可以看出該框架所談的 accuracy／safety／usefulness 三個領域，在一則研究用模型的發布裡各自被交代到什麼程度"
refs:
  blog:
    title: "AlphaGenome 2: Deciphering how cells read DNA to better understand disease（Google DeepMind 官方部落格，2026-11-11）"
    url: "https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/"
  ag1:
    title: "AlphaGenome: AI for better understanding the genome（Google DeepMind 官方部落格，2025-06-25）"
    url: "https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/"
  ets2:
    title: "A disease-associated gene desert directs macrophage inflammation through ETS2（Nature 630(8016): 447–456，2024-06-05）"
    url: "https://www.nature.com/articles/s41586-024-07501-1"
  paper:
    title: "AlphaGenome 2 技術文件 PDF（由 Google 自有 storage.googleapis.com 託管）"
    url: "https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/alphagenome-2.pdf"
  api:
    title: "AlphaGenome API 文件站（取用入口）"
    url: "https://www.alphagenomedocs.com/"
---

[Home](../) · [Industry Watch](./)

# AlphaGenome 2：變異效應預測從組織平均走到細胞類型

## 來源

- 組織：Google DeepMind
- 事件：發布 AlphaGenome 2，把 DNA 變異效應預測的解析度從組織平均推進到單一細胞類型與細胞狀態
- 日期：2026-11-11（頁面可見 November 11, 2026，`meta` 的 `article:published_time` 為 `2026-11-11T15:00:00+00:00`，兩者一致）
- 官方入口：<https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/>
- **單源，待交叉驗證**：關於 AlphaGenome 2 的所有宣稱與數值均只出自這一則官方公告。本文另引的 Nature 論文屬獨立第三方，但它佐證的是公告所重現的那個既有發現，不是模型本身的效能。

**編輯：** Clarence

Google DeepMind 於 2026-11-11 發布 AlphaGenome 2，一個預測 DNA 序列及其變異如何影響特定人類細胞類型的模型 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。相對於 2025 年的初版，這一版最主要的改動是把細胞類型從「平行輸出的其中一欄」改成「輸入的一部分」：模型一次只針對一個指定的組織、細胞類型或細胞狀態作預測，而那個條件可以直接由研究者自己的單細胞實驗現場產生。對醫學研究端而言，這一步要解決的是變異判讀長年的痛點 —— 候選變異不缺，缺的是「它在哪一種細胞上起作用」。模型即日起開放非商業研究以 API 取用，商業研究為私下預覽；官方並載明僅供研究用途、未經臨床或診斷用途驗證。

## 背景

- **初版 AlphaGenome 於 2025-06-25 上線。** 公告把它定位為 `a new, unifying DNA sequence model that advances regulatory variant-effect prediction`，當時即以 API 形式提供 [(ref: ag1)](https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/)。本則公告寫 `Last year, we launched AlphaGenome`，與該頁日期相符。
- **中間一步是把預測結果整包算好。** 本則公告寫 `We expanded its reach with AlphaGenome Atlas, a platform containing predictions for all 9 billion possible single-letter changes in the human genome`，即對人類基因體所有可能的單鹼基變異預先算好、做成可查詢的平台 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **本則要處理的限制是「組織平均」。** 公告寫初版把一段一百萬字母的 DNA 序列一次平行預測出數千個實驗的性質（`fixed parallel outputs of bulk tissues and cell lines`），而這種作法把模型容量攤薄，難以區分性質相近的細胞類型。這就是本版改成條件式架構的理由。
- **技術主張只有一個，其餘由它推導。** 公告把跨模態補值、免重新訓練即可適應新單細胞資料、以及預先算好的全基因體關聯研究（genome-wide association study，GWAS）變異評分，都說成條件化架構的衍生結果。
- **下一步已被預告。** 公告結尾寫 `And soon, we will release AlphaGenome 2 Skills in Google Antigravity`，即這個模型將接上該公司的代理式開發平台。公告未給時程。

## 模型改了什麼（事實）

- **從平行輸出改為條件式預測** — AlphaGenome 2 是 conditional model：在一百萬字母的 DNA 序列之外，另把一個目標生物條件（公告定義為 `a tissue, cell type or state`）在架構的每一層都當成輸入，一次只預測一個條件。公告的說法是，這讓模型得以學會「同一段 DNA 在不同細胞類型中被讀取的方式有何不同」 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **條件有兩種來源** — 可取自一份細胞類型的 reference catalog，也可由研究者自己的單細胞實驗經 cell encoder 即時產生。後者是這一版對外部使用者意義最大的一項：不必等官方把某個細胞類型納入目錄。
- **新增一項讀出** — 預測項目包含初版就有的 gene expression、histone modifications 與 chromatin accessibility，另新增 DNA methylation，公告稱後者是 `a widely requested readout`。
- **訓練資料** — 公告正文寫 `We trained AlphaGenome 2 on both bulk and single-cell data from human and mouse samples, including over 107 million individual cell profiles`，即同時使用 bulk 與單細胞資料、涵蓋人與小鼠樣本。摘要句另寫為 `more than 100 million individual cell profiles across 68 tissues`。

## 能做什麼（事實）

- **跨模態補值（cross-modality imputation）** — 模型把細胞的生物狀態與其輸出分離，因此研究者若只輸入一項量測（例如單細胞基因活性），模型可預測未量測的其他性質（例如 chromatin accessibility）。公告把用途說成協助決定下一步該做哪些實驗 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **免重新訓練即可吃新的細胞狀態** — 研究者可上傳僅數十個細胞的單細胞 RNA 定序（single-cell RNA sequencing，scRNA-seq）快照，壓縮成一個 cell state representation 後用以條件化模型。公告稱在這種情況下 AlphaGenome 2 `can match or outperform models trained or fine-tuned directly on those datasets`。
- **預先算好的 GWAS 變異評分** — 公告稱已對數百種人類細胞與組織條件預先計算 trait-associated variants 的預測，使研究者不必自行跑大規模運算，並指出兩項用途：
  - **enhancer 與基因的連結延伸到真實人體細胞**。公告指出實驗性的 CRISPR 篩選多半使用實驗室培養的細胞株，因此人體內特定細胞的調控連線圖長年缺乏；AlphaGenome 2 把 enhancer–gene mapping 延伸到 primary human cell types，公告舉的例子是支持並保護神經元的腦部星狀膠細胞（astrocytes）。
  - **指出 GWAS 區段中的因果變異與其作用細胞**。公告寫在從身高到第二型糖尿病的多項複雜性狀上，預先算好的變異評分有助於指出最可能涉入的變異與細胞類型；在模型有把握時，也會預測該變異是調高或調低基因活性。

## 效能與案例（事實）

- **免疫細胞資料集上的變異辨識** — 公告給出的量化結果來自 TenK10K，一個涵蓋 28 種 primary immune cell types 的大型單細胞圖譜。原文為：`On the TenK10K dataset, a large single-cell map of 28 primary immune cell types, AlphaGenome 2 reliably identified nearly twice as many causal variants (30% vs. 16%) and directional gene effects (43% vs. 23%) as the original AlphaGenome fine-tuned on single-cell data and other specialized tools.` [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)

  | 指標 | AlphaGenome 2 | 對照組 |
  |---|---|---|
  | causal variants | 30% | 16% |
  | directional gene effects | 43% | 23% |

  對照組依公告原文為「在單細胞資料上微調過的初版 AlphaGenome，以及其他專用工具」。熱圖圖說對同一組對照的寫法是 `AG1 fine tuned on single cell data predictions`。
- **細胞類型間的表現差異** — 公告寫在訓練資料之外的基因體區段上，AlphaGenome 2 能解釋顯著更多的「同一組織內不同細胞類型之間的基因表現差異」，並能追蹤連續變化，舉的例子是人類血液幹細胞成熟為紅血球與各免疫譜系的過程。此項未附數值。
- **發炎性腸道疾病的回溯案例** — 公告引用一項既有研究：一個位於遠端調控開關上的變異透過過度活化腸道巨噬細胞中的 ETS2 基因而驅動發炎性腸道疾病（inflammatory bowel disease，IBD）。AlphaGenome 2 以計算方式重現了這個結論，指出該因果變異並顯示它選擇性地只在腸道巨噬細胞中放大 ETS2，對其他細胞類型與基因影響不大。該研究為 Nature 第 630 卷第 8016 期第 447–456 頁，線上日期 2024-06-05 [(ref: ets2)](https://www.nature.com/articles/s41586-024-07501-1)。
- **疫苗活化狀態下的變異效應** — 公告另舉一例：給模型一份它沒見過的 COVID-19 mRNA 疫苗研究單細胞資料，模型區分出被疫苗活化的免疫 T 細胞與靜止的 T 細胞，並顯示一個與重症 COVID-19 相關的變異在細胞處於活化狀態時對基因活性的干擾更強 —— 公告稱這是在未活化細胞上會被忽略的效應。此項未附數值，公告亦未連結該份研究。

## 取用條件與法規狀態（事實）

- **兩級取用** — 公告寫 AlphaGenome 2 與其表現條件化的互動式 Colab 教學 `are available today for non-commercial research via the AlphaGenome API and in private preview for commercial research`，即非商業研究可即刻取用，商業研究為私下預覽 [(ref: api)](https://www.alphagenomedocs.com/)。公告未說明 private preview 的申請條件、審核方式或時程。
- **僅供研究用途** — 公告在致謝之前寫明 `Please note that AlphaGenome and AlphaGenome 2 are intended for research use only and have not been validated or approved for clinical or diagnostic purposes.`，這句話同時涵蓋初版與二版 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **社群徵集** — 公告邀請社群回報使用案例，寫明 `Get in touch via this form by 30 November`，入選者可能獲得額外額度與點數。
- **兩段外部引言** — Human Cell Atlas 聯盟共同創辦人、劍橋大學幹細胞醫學教授 Sarah Teichmann 稱本模型令人振奮之處在於 `adapts directly to new single-cell data without retraining`；Genomics Limited 執行長 Peter Donnelly 稱它 `represents an impressive advance in the field`，並寫 `We look forward to incorporating it in our Mystra platform`。

## 證據邊界（事實）

本則為單一組織的單一公告，下列幾點限制了外部可核對的範圍，列在這裡供引用時參考：

- **量化結果只有一組，且未給分母。** 全篇出現的百分比就是 30%／16% 與 43%／23% 這四個，全部來自 TenK10K 這一個免疫細胞資料集。公告未說明這些百分比的分母，該節的標題用了 `variant recall` 一詞但給數字的句子並未定義它。因此外部無法判斷未被辨識出的部分是什麼性質，也無法推算這個水準在實務流程中夠不夠用。
- **其餘能力宣稱沒有對應數值。** 細胞類型特異性（`significantly more`）、免重訓泛化（`match or outperform`）、enhancer–gene mapping 的延伸、以及 GWAS 變異評分的效果，公告都以定性詞描述。
- **對照組在摘要與正文的寫法不同。** 摘要句寫 `our previous state-of-the-art model`，正文與圖說寫的則是「在單細胞資料上微調過的初版」加上未具名的 `other specialized tools`。引用時宜採正文的寫法。
- **兩個疾病案例都不是前瞻預測。** IBD／ETS2 的結論公開發表於 2024-06-05，早於初版 AlphaGenome 上線（2025-06-25）約十二個月；公告用的動詞是 `reproduced`。COVID-19 那一例未附來源連結。公告未提出任何由 AlphaGenome 2 先指出、而後經實驗證實的新案例。
- **訓練資料的兩種說法略有出入。** 摘要寫 `more than 100 million … across 68 tissues`，正文寫 `over 107 million …` 並註明含小鼠樣本；`68 tissues` 僅出現於摘要。
- **技術文件未經同儕審查。** 公告的 `Read the paper` 指向 Google 自有 storage 上的一份 PDF，而非 arXiv、bioRxiv 或期刊 [(ref: paper)](https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/alphagenome-2.pdf)。本文所有數值取自公告頁本身，未引用該 PDF 內容。
- **兩段外部引言皆非獨立評估。** Teichmann 同時列名於同一頁的致謝名單；Donnelly 來自表明將採用此模型的公司。

## 本書庫解讀（評論）

- **這一版真正改變的是提問的單位。** 從「這個變異在肝臟會怎樣」變成「這個變異在肝臟的哪一種細胞會怎樣」。對罕見疾病與複雜性狀的判讀而言，這正是長年卡住的地方：候選變異從來不缺，缺的是指認作用細胞的依據。把細胞類型從輸出欄位改成輸入條件，是直接對著這個缺口設計的。
- **「自己上傳幾十個細胞就能用」比效能數字更值得注意。** 多數此類模型的實用瓶頸不在準確度，而在「我關心的那個細胞狀態不在人家的目錄裡」。若免重訓條件化真的可行，使用門檻會從「等官方支援」降到「拿自己手上的 scRNA-seq 資料來跑」。公告對這一項沒有給數值，但它是本則最可能改變實際工作流程的設計。
- **以免疫細胞的結果外推到其他組織要保守。** 免疫細胞容易大量取得、刺激反應明確、既有單細胞圖譜最完整，調控變異的效應相對好測。公告強調的應用卻跨到腦部星狀膠細胞、腸道巨噬細胞與第二型糖尿病。目前只有免疫細胞那一組有數字。
- **回溯重現與前瞻預測是兩種強度的證據。** IBD／ETS2 的重現能說明模型在一個已知答案上不會失準，這本身有意義；但它無法排除選擇效應 —— 外部不會知道有多少同樣知名的案例被試過而沒有重現出來。真正的檢驗要等由模型先指出、再被實驗證實的案例出現。
- **「僅供研究用途」這一行限定的是責任，不是使用熱度。** 一個免費開放給非商業研究、而且已預先算好數百種細胞條件的平台，在實務上會很快出現在研究者的變異判讀流程裡。這一行的意義在於：由它產生的詮釋在進入臨床報告之前，仍須走完既有的驗證路徑。

## 產業影響

- **對基因體醫學與罕見疾病判讀而言**，本則提供的是一個免費、已預算好的候選變異排序來源，可用來縮小功能驗證的實驗清單。在分母與非免疫細胞類型的效能公布之前，它的定位是產生假說的工具，而非判讀依據。
- **對單細胞研究社群而言**，跨模態補值與免重訓條件化改變的是實驗規劃順序：先用少量細胞跑出預測、據此決定下一批要量測什麼，而不是先把所有模態都做完。這一點若成立，影響的是研究經費的配置方式。
- **對醫學研究資訊基礎設施而言**，由 AlphaGenome 到 AlphaGenome Atlas 再到 AlphaGenome 2、並預告接進 Antigravity，呈現的是同一條建置路線：先出模型，再把搜尋空間整包算好成為可查詢資產，再接進代理式平台。採用方值得注意的是這三層由同一家供應商提供。
- **對台灣的醫學中心與生技公司而言**，非商業研究可直接以 API 取用是實質的門檻降低。但「非商業」與「商業」的界線在產學合作與衍生新創的情境下常不清楚，這會影響研究成果能否沿用到後續開發，進入計畫前宜先釐清取用條款。

## 與書庫其他文章的關係

本則公告結尾預告 AlphaGenome 2 Skills 將進入 Google Antigravity，與該則是同一條路線的兩端：該則示範的是代理式平台怎麼串起既有的化學工具，本則是即將被串進去的專用科學模型本身: [DeepMind 化學資訊學 Skills：代理程式跑完一輪藥物設計](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md)

該則提到 Antigravity 可接的三十多個生命科學資料庫中包含 1PB 的 AlphaGenome Atlas，而那個 Atlas 正是本則模型的前一代對全基因體預先算出的產物；兩則合看可見同一條「模型 → 預算好的資產 → 接進代理式平台」的建置順序: [DeepMind 抗菌胜肽示範：代理程式從資料庫走到實驗計畫](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

同一家公司相隔一週的兩則發布，一則談健康 AI 該用哪些方法評估、門檻由各團隊自訂，一則是實際發布的模型與它所公布的評估範圍；並讀可以看出該框架所談的 accuracy／safety／usefulness 三個領域，在一則研究用模型的發布裡各自被交代到什麼程度: [Google 健康 AI 評估框架：三個領域、三種方法、17 個維度](2026-11-05-google-health-ai-evaluation-framework.md)

## 實務的啟發

- **把細胞類型當成變異判讀表單的第一級欄位。** 本則的技術主張若成立，實務意義是「同一變異在不同細胞類型上效應不同」從定性變成可排序。即使暫不採用此模型，在院內判讀表單中增設「預期作用細胞類型」一欄，本身就能改善功能驗證實驗的設計順序。
- **評估這類工具時，固定問四個欄位。** 召回率、分母、偽陽性率、評估所用的細胞類型。本則公告能填上第一欄與第四欄，另外兩欄空白。把這四欄做成固定格式，可以避免只憑一個百分比決定工具在流程中的位置。
- **引用效能時連對照組一起寫。** 建議寫法是「在 TenK10K 免疫細胞資料集上，相對於在單細胞資料上微調過的初版 AlphaGenome，因果變異辨識由 16% 提升至 30%」。
- **內部技術雷達把案例標成 retrospective 或 prospective。** 本則兩個疾病案例皆屬前者。這個欄位能避免把「重現了已知結論」記成「發現了新事」。
- **研究用途的限定要寫進計畫書。** 若院內研究要使用它的變異評分，計畫書宜預先寫明工具的法規狀態，以及由它產生的詮釋在進入臨床報告前須經哪些獨立驗證。
- **產學合作前先書面確認「非商業研究」的界線。** 非商業可直接以 API 取用、商業僅限 private preview，這條界線會影響衍生成果的後續運用。

## 後續追蹤

- 30%／16% 與 43%／23% 的分母、偽陽性率，以及這些門檻對應的操作點。
- 除 TenK10K 之外，非免疫細胞類型（腦部、心肌、腸道等）上的對應效能數值。
- 公告中 `other specialized tools` 所指為何，以及它們在同一評估上的分數。
- 是否會出現由 AlphaGenome 2 事前指出、而後經實驗證實的新變異案例。
- 技術文件是否會投往預印本平台或期刊並接受同儕審查。
- 商業研究 private preview 的申請條件、審核標準與開放時程。
- 預告的 AlphaGenome 2 Skills 何時進入 Antigravity，屆時可取用範圍是否與 API 相同。
- 台灣的基因檢測實驗室若採用此類模型做候選變異排序，在實驗室自行開發檢測（laboratory developed tests，LDTs）的品質管理要求下須補足哪些驗證文件。

## References

- `blog` — AlphaGenome 2: Deciphering how cells read DNA to better understand disease（Google DeepMind 官方部落格，2026-11-11，含架構說明、訓練資料、TenK10K 效能、兩個疾病案例、取用條件、兩段外部引言與研究用途限定句）  
  <https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/>
- `ag1` — AlphaGenome: AI for better understanding the genome（Google DeepMind 官方部落格，2025-06-25；為本則公告 `Last year, we launched AlphaGenome` 所指的初版發布頁）  
  <https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/>
- `ets2` — A disease-associated gene desert directs macrophage inflammation through ETS2（Nature 第 630 卷第 8016 期第 447–456 頁，線上日期 2024-06-05，DOI 10.1038/s41586-024-07501-1；為本則公告 IBD 案例所引的研究）  
  <https://www.nature.com/articles/s41586-024-07501-1>
- `paper` — AlphaGenome 2 技術文件 PDF（由 Google 自有 storage.googleapis.com 託管，非期刊或預印本平台；本文未引用其內容）  
  <https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/alphagenome-2.pdf>
- `api` — AlphaGenome API 文件站（公告所給的取用入口）  
  <https://www.alphagenomedocs.com/>

[Home](../) · [Industry Watch](./)
