---
parent: Industry Watch
nav_order: 1
title: "AlphaGenome 2 的近兩倍，只出自一個免疫細胞資料集"
category: industry-watch
date: 2026-11-12
updated: 2026-11-12
tags: [Google-DeepMind, AlphaGenome, genomics, variant-effect-prediction, single-cell, GWAS, regulatory-variant, cell-type-specificity, rare-disease, research-use-only, Antigravity]
catalog_id: "google-deepmind:alphagenome-2-launch-2026-11-11"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.0"
source:
  orgs:
    - "Google DeepMind"
  event: "Google DeepMind 發布 AlphaGenome 2，一個以細胞類型為條件的 DNA 序列模型，宣稱辨識出的影響基因表現變異數量接近前代的兩倍"
  event_date: "2026-11-11"
  official_url: "https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/"
  single_source: true
  single_org: true
related_articles:
  - path: "2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md"
    relation: "同一家公司相隔六天的兩則科學發布，唯一的案例研究都是一個在示範開始前就已經公開發表的答案：該則的 crizotinib→lorlatinib 被公告自己標為 well-known case，本則的 IBD／ETS2 結論出自 2024-06-05 的 Nature 論文、早於 AlphaGenome 初版上線十二個月"
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "該則文中被當成 Antigravity 可接的三十多個生命科學資料庫之一、只佔一行的 AlphaGenome Atlas，在本則成了被發布的主體；而兩則的可核對程度正好相反——該則全文沒有任何一個效能量測，本則有四個百分比，但四個全部來自同一個免疫細胞資料集"
  - path: "2026-11-05-google-health-ai-evaluation-framework.md"
    relation: "該則的白皮書主張健康 AI 的評估要同時涵蓋 accuracy、safety 與 usefulness 三個領域，本則是同一家公司把一個直接談疾病的模型發布出來時實際給了什麼——只有 accuracy 那一類的四個百分比，safety 與 usefulness 兩個領域在整篇公告裡沒有對應的任何數值，而頁尾寫明本模型未經臨床或診斷用途驗證"
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

# AlphaGenome 2 的近兩倍，只出自一個免疫細胞資料集

## 來源

- 組織：Google DeepMind
- 事件：發布 AlphaGenome 2，一個以細胞類型為條件（conditional）的 DNA 序列模型，宣稱辨識出的影響基因表現變異數量接近前代的兩倍
- 日期：2026-11-11（頁面可見日期為 November 11, 2026，頁面 `meta` 的 `article:published_time` 為 `2026-11-11T15:00:00+00:00`，兩者一致）
- 官方入口：<https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/>
- **單源，待交叉驗證**：關於 AlphaGenome 2 本身的所有宣稱與數值，均只出自 Google DeepMind 這一則公告。本文另引用的 Nature 論文屬獨立第三方，但它所佐證的是公告所重現的那個既有發現，不是 AlphaGenome 2 的效能。

**編輯：** Clarence

Google DeepMind 於 2026-11-11 發布 AlphaGenome 2，一個預測 DNA 序列變異如何影響特定人類細胞類型的模型 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。標題寫的是 `to better understand disease`，摘要句宣稱它辨識出的影響基因表現變異數量接近前一個 state-of-the-art 模型的兩倍。逐段核對這篇長度 15,580 字元的公告後，全文出現的百分比共四個——30%、16%、43%、23%——四個全部來自同一個資料集的同一項比較；公告列出的其餘五項能力宣稱，一個數值都沒有附。而頁面最後一行寫明，AlphaGenome 與 AlphaGenome 2 僅供研究使用，未經臨床或診斷用途的驗證或核准。

## 背景

- **初版 AlphaGenome 於 2025-06-25 上線。** 該則公告把它定位為 `a new, unifying DNA sequence model that advances regulatory variant-effect prediction`，當時即以 API 形式提供 [(ref: ag1)](https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/)。本則公告寫 `Last year, we launched AlphaGenome`，與該頁日期相符。
- **中間一步是 AlphaGenome Atlas。** 本則公告寫 `We expanded its reach with AlphaGenome Atlas, a platform containing predictions for all 9 billion possible single-letter changes in the human genome`，也就是把初版模型的預測結果對整個人類基因體的單鹼基變異預先算好、做成可查詢的平台 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。本書庫先前記錄 Antigravity 可接的三十多個生命科學資料庫時，這個 1PB 的 Atlas 正是其中一項。
- **本則的改動在於模型吃進什麼。** 公告寫初版是把一段一百萬字母的 DNA 序列一次平行預測出數千個實驗的性質（`fixed parallel outputs of bulk tissues and cell lines`），AlphaGenome 2 則改為 conditional model：在序列之外，另把一個指定的生物條件（`a tissue, cell type or state`）當成輸入，一次只預測一個條件。公告的理由是平行作法把模型容量攤薄，難以區分性質相近的細胞類型 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **這一步的因果鏈是「條件化」帶出其餘三項宣稱。** 公告把 cross-modality imputation（跨模態補值）、免重新訓練即可適應新單細胞資料、以及預先算好的全基因體關聯研究（genome-wide association study，GWAS）變異評分，全部說成條件化架構的衍生結果。也就是本則真正的技術主張只有一個，其餘皆由它推導。
- **取用分兩級，且二版同日開放。** 公告寫 AlphaGenome 2 與其 Colab 教學 `are available today for non-commercial research via the AlphaGenome API and in private preview for commercial research`，即非商業研究可直接取用，商業研究僅限私下預覽 [(ref: api)](https://www.alphagenomedocs.com/)。
- **公告預告它將進入 Antigravity。** 結尾寫 `And soon, we will release AlphaGenome 2 Skills in Google Antigravity`，把這個模型接上本書庫已記錄兩則的那個代理式開發平台。這一項為未來式，公告未給時程。

## 公告寫了什麼（事實）

- **模型形態** — conditional model，在架構的每一層都吃進目標生物條件；條件可取自一份細胞類型的 reference catalog，也可由研究者自己的單細胞實驗經 cell encoder 即時產生 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **預測的讀出項目** — 與初版相同的 gene expression、histone modifications 與 chromatin accessibility，另新增 DNA methylation，公告稱後者是 `a widely requested readout`。
- **訓練資料** — 公告正文寫 `We trained AlphaGenome 2 on both bulk and single-cell data from human and mouse samples, including over 107 million individual cell profiles`。
- **跨模態補值** — 模型把細胞的生物狀態與其輸出分離，因此若研究者只輸入一項量測（例如單細胞基因活性），模型可預測未量測的其他性質（例如 chromatin accessibility），公告稱這有助於決定下一步要做哪些實驗。
- **免重新訓練的泛化** — 研究者可上傳僅數十個細胞的單細胞 RNA 定序（single-cell RNA sequencing，scRNA-seq）快照，壓縮成一個 cell state representation 後用以條件化模型；公告稱 AlphaGenome 2 `can match or outperform models trained or fine-tuned directly on those datasets`。
- **預先算好的 GWAS 變異評分** — 公告稱已對數百種人類細胞與組織條件預先計算 trait-associated variants 的預測，用以處理兩件事：把 enhancer（遠端調控開關）與基因的連結延伸到真實人體的 primary cell types，以及在 GWAS 標定的大段 DNA 中指出最可能的因果變異與其作用細胞。
- **徵集與期限** — 公告邀請社群回報使用案例，並寫明 `Get in touch via this form by 30 November`，入選者可能獲得額外額度與點數。

## 全文能核對的數值（事實）

把公告正文（`<main>` 元素，長度 15,580 字元）的數字逐一盤點，與模型效能有關的只有下面四個，而且是同一句話裡的同一組比較：

| 數值 | 出處與性質 |
|---|---|
| 30% 對 16% | 在 TenK10K 資料集上辨識出的 causal variants 比例，後者為對照 |
| 43% 對 23% | 同一資料集上的 directional gene effects 比例，後者為對照 |
| 107 million | 訓練所用的 individual cell profiles 數量，來自人與小鼠樣本 |
| 100 million、68 tissues | 摘要句的訓練資料說法，僅出現於摘要 |
| 9 billion | AlphaGenome Atlas 預先算過的人類基因體單鹼基變異總數，屬前一代產品 |
| 28 | TenK10K 資料集涵蓋的 primary immune cell types 數量 |
| 1-million-letter | 模型吃進的 DNA 序列長度 |

公告全文的百分比就是上表前兩列的四個，沒有第五個。這四個全部出自同一句：`On the TenK10K dataset, a large single-cell map of 28 primary immune cell types, AlphaGenome 2 reliably identified nearly twice as many causal variants (30% vs. 16%) and directional gene effects (43% vs. 23%) as the original AlphaGenome fine-tuned on single-cell data and other specialized tools.` [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)

兩點值得逐字留意：

- **「近兩倍」在算術上成立，但它描述的是這一組比較，不是整個模型。** 以公告自己的數字計算，30 ÷ 16 為 1.875、43 ÷ 23 約為 1.870，兩者都可稱 nearly twice。這項計算由本文代為執行，公告本身只寫 nearly twice。成立的範圍就是 TenK10K 這一個免疫細胞資料集。
- **這四個百分比沒有分母。** 公告沒有寫 30% 與 16% 是「多少個變異中的 30%」。該節的 H2 標題是 `State-of-the-art cell-type predictions and variant recall`，recall（召回率）一詞在全文只出現這一次，而且只出現在標題，給出數字的那一句並未說明這些百分比是什麼的百分比。外部因此無法判斷被遺漏的那 70% 是什麼、也無法推算這個門檻在實務上夠不夠用。

## 宣稱涵蓋到哪裡（事實）

公告在三個小節裡提出六項能力宣稱。逐項核對後，附有數值的只有一項：

| 公告的宣稱 | 原文用詞 | 是否附數值 |
|---|---|---|
| Improved cell type specificity | `explains significantly more of how gene expression differs across cell types` | 無 |
| Improved variant effect prediction | `nearly twice as many`（30% 對 16%、43% 對 23%） | 有，來自 TenK10K |
| Pinpointing disease-relevant variants | `reproduced this finding computationally` | 無 |
| 免重新訓練的泛化 | `can match or outperform models trained or fine-tuned directly on those datasets` | 無 |
| Mapping enhancer–gene links in real human cell types | `extends enhancer-gene mapping to primary human cell types` | 無 |
| Pinpointing causal GWAS variants and the cells where they act | `Across a number of complex traits, ranging from height to type 2 diabetes` | 無 |

公告的標題句與摘要句所涵蓋的，是上表第二列那一項；其餘五項的結論寫法是 significantly more、reproduced、match or outperform、extends、help pinpoint，沒有一項能被外部量化檢驗。公告也沒有說明為何只對其中一項公布數字。

## 比較基準是誰（事實）

同一件事在公告的三個位置有三種寫法，而三者的嚴格程度不同：

| 位置 | 實際文字 | 對照組是誰 |
|---|---|---|
| 摘要句 | compared to our previous `state-of-the-art model` | 未指名 |
| 效能那一句 | as `the original AlphaGenome fine-tuned on single-cell data and other specialized tools` | 初版加微調，外加未具名的其他工具 |
| 熱圖圖說 | `AG1 fine tuned on single cell data predictions` | 初版加微調 |

也就是摘要句的「前一個 state-of-the-art 模型」並不是未經處理的初版 AlphaGenome，而是在單細胞資料上微調過的初版。至於 `other specialized tools` 指的是哪些工具，公告全文未具名任何一個，也未給它們任何一個分數——這表示這句話裡被一起超越的對象，外部無從核對 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。

訓練資料的說法也分兩處：摘要句寫 `more than 100 million individual cell profiles across 68 tissues`，正文寫 `over 107 million individual cell profiles` 並註明來自 `human and mouse samples`。68 tissues 這個數字只出現在摘要那一次，而摘要那一句省略了訓練資料含小鼠樣本這件事，緊接著寫這個模型 `turns static cell atlases into a predictive engine for human genetics`。

## 唯一的疾病案例，答案早於模型（事實）

公告唯一具名的疾病案例是發炎性腸道疾病（inflammatory bowel disease，IBD）：

- **公告的寫法。** `A recent landmark study showed that a variant in a distant regulatory switch drives IBD by overactivating the ETS2 gene in gut immune cells (macrophages). Making predictions across various immune cell types in the gut, AlphaGenome 2 reproduced this finding computationally.` 公告接著寫模型 `singled out the causal variant` 並顯示它選擇性地只在腸道巨噬細胞中放大 ETS2 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **那篇 landmark study 的實際日期。** 公告的 `landmark study` 連到 Nature 的 *A disease-associated gene desert directs macrophage inflammation through ETS2*，該頁的 `prism.publicationDate` 與 `citation_online_date` 皆為 2024-06-05，刊於第 630 卷第 8016 期第 447–456 頁，DOI 為 `10.1038/s41586-024-07501-1` [(ref: ets2)](https://www.nature.com/articles/s41586-024-07501-1)。
- **因此這是一次回溯重現。** 該結論公開發表於 2024-06-05，早於初版 AlphaGenome 上線（2025-06-25）約十二個月，早於本則公告約十七個月。公告用的動詞是 reproduced，本身沒有寫錯；但這代表模型被要求指出的那個因果變異與那個基因，在模型跑之前就已經是公開文獻裡的已知答案。公告沒有提出任何一個由 AlphaGenome 2 先指出、而後被實驗證實的新案例。

公告另舉的 COVID-19 疫苗案例同樣沒有數值，而且與 IBD 案例不同的是，公告對那份 `COVID-19 mRNA vaccine study` 完全沒有附連結：該頁 `<main>` 之內沒有任何一個連結文字包含 COVID。

## 法規狀態與可取用範圍（事實）

- **頁尾的限定句。** 公告在致謝之前寫 `Please note that AlphaGenome and AlphaGenome 2 are intended for research use only and have not been validated or approved for clinical or diagnostic purposes.` 這句話同時涵蓋初版與二版 [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **標題與這句話談的是不同層次。** 標題寫 `to better understand disease`，正文反覆出現 disease-relevant、disease unfolds、disease states 等語彙，頁尾則把用途限定在研究。公告沒有說明從研究用模型走到診斷用途需要哪些步驟，也沒有提及任何主管機關的路徑或時程。
- **商業研究須另外排隊。** 非商業研究可透過 API 直接取用，商業研究僅開放 private preview。公告未說明 private preview 的申請條件、審核方式或排隊時間。
- **技術文件不在期刊或預印本平台。** 公告的 `Read the paper` 指向 `storage.googleapis.com` 上的一份 PDF，而非 arXiv、bioRxiv 或任何期刊 [(ref: paper)](https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/alphagenome-2.pdf)。本文的所有數值均取自公告頁本身的原始文字，未引用該 PDF 的內容。

## 兩段外部引言（事實）

公告引用兩位外部人士，兩段皆為評價性語句、不含數值：

- **Professor Sarah Teichmann**，公告標示為 Human Cell Atlas 聯盟共同創辦人、劍橋大學幹細胞醫學教授。她稱本模型令人振奮之處在於 `adapts directly to new single-cell data without retraining`。同一頁的致謝名單中亦列有 Sarah Teichmann [(ref: blog)](https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/)。
- **Peter Donnelly**，公告標示為 Genomics Limited 執行長。他稱 AlphaGenome 2 `represents an impressive advance in the field`，並寫 `We look forward to incorporating it in our Mystra platform`，即一家將採用此模型的公司對該模型的評價。

兩段引言都不是獨立評估：一位名列同一頁致謝，一位來自預計採用方。公告未引用任何未參與、亦不打算採用的第三方意見。

## 本書庫解讀（評論）

- **這是一則架構公告，附帶一個資料集的驗證。** 把可核對的內容抽出來，本則成立的事實是：模型改成 conditional 架構、新增 DNA methylation 讀出、訓練於逾 1.07 億個細胞輪廓、在一個免疫細胞資料集上的兩項指標接近前代微調版的兩倍。其餘五項能力宣稱目前只能視為待驗證。這不是說它們不成立，而是公告選擇不提供判斷依據。
- **免疫細胞與其他細胞類型之間不能直接外推。** TenK10K 涵蓋 28 種 primary immune cell types。免疫細胞的調控變異效應之所以相對好測，部分原因是它們容易大量取得、刺激反應明確、既有單細胞圖譜最完整。公告本身強調的應用卻跨到 brain astrocytes、gut macrophages、heart muscle cells 與 type 2 diabetes。從一個免疫細胞資料集的召回率，推不出這些組織上的同等表現，而公告沒有提供後者的任何數字。
- **沒有分母的召回率，無法進入任何工作流程的設計。** 30% 這個數字若指召回率，意味著七成的因果變異仍被漏掉。對一個要用來排序候選變異的工具而言，漏掉的比例與漏掉的是哪一類，決定了它該被放在流程的哪一段——是用來收斂名單，還是只能用來補充排序。公告沒有給分母、沒有給偽陽性率，這個判斷目前做不出來。
- **回溯重現已知答案，與事前預測未知答案，是兩種不同強度的證據。** 本書庫六天前記錄的同一家公司藥物設計示範，其案例被公告自己標為 well-known case；本則的 IBD／ETS2 結論同樣早於模型存在。回溯重現能排除模型完全無效，但無法排除選擇效應——公告不會告訴讀者，有多少個同樣知名的案例被試過而沒有重現出來。
- **「研究用」這一行限定的是責任歸屬，不是使用熱度。** 一個免費開放給非商業研究、且已預先算好數百種細胞條件的變異評分平台，在實務上會很快出現在研究者的變異判讀流程裡。研究用途的限定不會阻止這件事，但它確實意味著：由此產生的任何變異詮釋，在送進臨床報告之前都必須走回既有的驗證路徑。
- **對醫療端而言，本則真正的分量在輸入側而非輸出側。** 罕見疾病與複雜性狀的變異判讀，長年的瓶頸不是沒有候選變異，而是候選太多且無法指認作用細胞。若 AlphaGenome 2 的細胞類型條件化真的把「這個變異在哪一種細胞上起作用」變成可預測的量，受益的會是基因診斷的判讀排序與功能驗證實驗的設計順序。但這個「若」目前只由一個免疫細胞資料集支撐。

## 產業影響

- **對基因體醫學與罕見疾病判讀而言**，本則提供的是一個免費、已預算好的候選變異排序來源，可用於縮小功能驗證的實驗清單。但在公布分母與非免疫細胞類型的效能之前，它不應被當成判讀依據，只能當成產生假說的工具。
- **對醫學研究資訊基礎設施而言**，由 AlphaGenome 到 AlphaGenome Atlas 再到 AlphaGenome 2，呈現的是同一條路線：先出模型，再把整個搜尋空間預先算好做成可查詢資產，再把資產接進代理式平台。對採用方而言，值得注意的是這三層都由同一家供應商提供，且其中的 private preview 一層對商業使用設有門檻。
- **對台灣的醫學中心與生技公司而言**，非商業研究可直接以 API 取用是實質的門檻降低；但「非商業」與「商業」的界線在產學合作與衍生新創的情境下往往不清楚，這會直接影響研究成果能否沿用到後續的商業開發。進入任何以此模型為基礎的計畫前，應先釐清取用條款。
- **對轉述與二次引用而言**，本則的風險點在摘要句。「接近前一個 state-of-the-art 模型的兩倍」若被單獨摘出，讀者會以為對照組是初版 AlphaGenome；實際的對照組是在單細胞資料上微調過的初版，加上一批未具名的工具。

## 與書庫其他文章的關係

同一家公司相隔六天的兩則科學發布，唯一的案例研究都是一個在示範開始前就已經公開發表的答案：該則的 crizotinib→lorlatinib 被公告自己標為 well-known case，本則的 IBD／ETS2 結論出自 2024-06-05 的 Nature 論文、早於 AlphaGenome 初版上線十二個月: [DeepMind 藥物設計示範：答案在代理程式動手前就寫好了](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md)

該則文中被當成 Antigravity 可接的三十多個生命科學資料庫之一、只佔一行的 AlphaGenome Atlas，在本則成了被發布的主體；而兩則的可核對程度正好相反——該則全文沒有任何一個效能量測，本則有四個百分比，但四個全部來自同一個免疫細胞資料集: [DeepMind 說把數天縮成一次對話，全文沒量過任何一段時間](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

該則的白皮書主張健康 AI 的評估要同時涵蓋 accuracy、safety 與 usefulness 三個領域，本則是同一家公司把一個直接談疾病的模型發布出來時實際給了什麼——只有 accuracy 那一類的四個百分比，safety 與 usefulness 兩個領域在整篇公告裡沒有對應的任何數值，而頁尾寫明本模型未經臨床或診斷用途驗證: [Google 公開健康 AI 評估框架，及格線留給各家自己訂](2026-11-05-google-health-ai-evaluation-framework.md)

## 實務的啟發

- **引用這則消息時，把對照組一起寫進去。** 正確的寫法是「在 TenK10K 免疫細胞資料集上，相對於在單細胞資料上微調過的初版 AlphaGenome，因果變異辨識由 16% 提升至 30%」。只寫「接近兩倍」而不寫對照組與資料集，會讓半年後回看的人以為這是跨細胞類型的通用提升。
- **把這類模型放進變異判讀流程前，先問分母與偽陽性率。** 召回率單獨存在時無法定位工具該放在流程的哪一段。建議在評估表上固定四欄：召回率、分母、偽陽性率、評估所用的細胞類型。本則公告只能填上第一欄與第四欄。
- **區分「回溯重現」與「前瞻預測」兩種驗證，並分欄記錄。** 內部技術雷達在記錄此類模型時，建議把案例研究標註為 retrospective 或 prospective。本則的 IBD／ETS2 屬前者。這個欄位能避免把「模型重現了一個已知結論」讀成「模型發現了一件新事」。
- **研究用途的限定要寫進計畫書，而不只是記在心裡。** 本模型明寫 `research use only and have not been validated or approved for clinical or diagnostic purposes`。若院內研究要使用它的變異評分，計畫書應預先寫明工具的法規狀態，以及由它產生的詮釋在送進臨床報告前須經哪些獨立驗證。
- **產學合作前先確認「非商業研究」的界線。** 非商業研究可直接以 API 取用、商業研究僅限 private preview，這條界線會影響衍生成果的後續運用。建議在簽署合作前即向供應商書面確認本單位的使用情境落在哪一側。
- **把細胞類型當成變異判讀的第一級欄位。** 本則的技術主張若成立，實務上的意義是「同一個變異在不同細胞類型上的效應不同」這件事從定性變成可排序。即使暫不採用此模型，在院內的變異判讀表單中增設「預期作用細胞類型」一欄，本身就能改善功能驗證實驗的設計順序。

## 後續追蹤

- 30%／16% 與 43%／23% 的分母為何，以及偽陽性率與這些門檻所對應的操作點。
- 除 TenK10K 之外，是否會公布非免疫細胞類型（如腦部、心肌、腸道）上的對應效能數值。
- 公告中 `other specialized tools` 所指的是哪些工具，以及它們在同一評估上的分數。
- 是否會出現由 AlphaGenome 2 事前指出、而後經實驗證實的新變異案例，而非回溯重現既有發現。
- 技術文件是否會投往預印本平台或期刊並接受同儕審查。
- 商業研究的 private preview 申請條件、審核標準與開放時程。
- 預告的 AlphaGenome 2 Skills 何時進入 Antigravity，以及屆時可取用的範圍是否與 API 相同。
- 台灣的基因檢測實驗室若採用此類模型做候選變異排序，在實驗室自行開發檢測（laboratory developed tests，LDTs）的品質管理要求下須補足哪些驗證文件。

## References

- `blog` — AlphaGenome 2: Deciphering how cells read DNA to better understand disease（Google DeepMind 官方部落格，2026-11-11，含四項效能百分比、六項能力宣稱、兩段外部引言、致謝名單與研究用途限定句）  
  <https://deepmind.google/blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/>
- `ag1` — AlphaGenome: AI for better understanding the genome（Google DeepMind 官方部落格，2025-06-25；為本則公告 `Last year, we launched AlphaGenome` 所指的初版發布頁）  
  <https://deepmind.google/blog/alphagenome-ai-for-better-understanding-the-genome/>
- `ets2` — A disease-associated gene desert directs macrophage inflammation through ETS2（Nature 第 630 卷第 8016 期第 447–456 頁，線上日期 2024-06-05，DOI 10.1038/s41586-024-07501-1；為本則公告 `landmark study` 所指向的連結）  
  <https://www.nature.com/articles/s41586-024-07501-1>
- `paper` — AlphaGenome 2 技術文件 PDF（由 Google 自有 storage.googleapis.com 託管，非期刊或預印本平台；本文未引用其內容）  
  <https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphagenome-2-deciphering-how-cells-read-dna-to-better-understand-disease/alphagenome-2.pdf>
- `api` — AlphaGenome API 文件站（公告所給的取用入口）  
  <https://www.alphagenomedocs.com/>

[Home](../) · [Industry Watch](./)
