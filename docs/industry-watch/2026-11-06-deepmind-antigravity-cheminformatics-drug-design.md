---
parent: Industry Watch
nav_order: 5
title: "DeepMind 藥物設計示範：答案在代理程式動手前就寫好了"
category: industry-watch
date: 2026-11-06
updated: 2026-11-06
tags: [Google-DeepMind, Google-Antigravity, cheminformatics, drug-discovery, RDKit, ChEMBL, PubChem, matched-molecular-pair, macrocycle, crizotinib, lorlatinib, scaffold-split, agentic-workflow, retrospective-validation]
catalog_id: "google-deepmind:antigravity-cheminformatics-walkthrough-2026-11-03"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.0"
source:
  orgs:
    - "Google DeepMind"
  event: "發布技術示範文章 Agentic cheminformatics with Google Antigravity，發表 Antigravity 的 Cheminformatics Skills，並以 crizotinib 與 lorlatinib 這組已知的剛性化案例示範一次藥物設計迭代"
  event_date: "2026-11-03"
  official_url: "https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/"
related_articles:
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "同一產品線相隔十九天的第二篇科學示範，而兩則的證據缺口換了位置沒有補上 —— 該則的加速宣稱只寫在網頁中繼資料裡、正文沒量過時間，本則把「一小時」寫進了正文第二段，量測方式、樣本數與基準流程仍然三項皆無"
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "兩則是前沿模型供應商相隔七天發布的藥物開發成果，可回查程度差一整級 —— 該則的爭點在於一個倍數出自單一個孔、成功標準事後才定，至少有孔數與成功標準可供爭論；本則連一個代理程式端的數值都沒有產生，無從爭起"
  - path: "2026-11-05-google-health-ai-evaluation-framework.md"
    relation: "同一家公司相隔一天的兩則發布恰好構成對照 —— 該則主張健康 AI 的評估要同時涵蓋 closed-question benchmarks、autoraters 與 expert human review 三種方法，本則的示範正是那套框架所指的第一種評估的反面：模型被建起來、被宣稱在 held-out set 上驗證過，卻沒有公布任何一個評估數值"
refs:
  pr:
    title: "Google DeepMind：Agentic cheminformatics with Google Antigravity（官方部落格，2026-11-03）"
    url: "https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/"
  amp:
    title: "Google DeepMind：Accelerating the search for antimicrobial peptides with Google Antigravity（官方部落格，2026-10-15）"
    url: "https://deepmind.google/blog/accelerating-antimicrobial-discovery/"
  antigravity:
    title: "Google Antigravity：Why choose Google Antigravity for science（官方產品頁）"
    url: "https://antigravity.google/use-cases/science?hl=en"
  pubchem_criz:
    title: "PubChem：crizotinib（CID 11626560）計算屬性，RotatableBondCount"
    url: "https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/crizotinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON"
  pubchem_lorl:
    title: "PubChem：lorlatinib（CID 71731823）計算屬性，RotatableBondCount"
    url: "https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/lorlatinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON"
---

[Home](../) · [Industry Watch](./)

# DeepMind 藥物設計示範：答案在代理程式動手前就寫好了

## 來源

- 組織：Google DeepMind（產品為 Google Antigravity；文中涉及的 RDKit 由開源社群維護，ChEMBL 由 EMBL-EBI 維運，PubChem 由美國國家生物技術資訊中心（National Center for Biotechnology Information, NCBI）維運）
- 事件：發布技術示範文章 `Agentic cheminformatics with Google Antigravity`，同時發表 Antigravity 的 `Cheminformatics Skills`
- 日期：2026-11-03（頁面可見 `November 3, 2026`，`meta article:published_time` 與 JSON-LD `datePublished` 皆為 `2026-11-03T15:00:00+00:00`；`dateModified` 為 `2026-11-04T09:22:30.548258+00:00`）
- 官方入口：<https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/>
- 作者署名：Zoi Tsangalidou、Ruijie (Kelly) Zhang、Sukhdeep Singh、Michael V. LeVine
- 本則**事件本身為單源（Google 單一組織），待交叉驗證** —— 公告與其所連結的 Antigravity 產品頁同屬 Google，沒有第三方聲明。但公告唯一的兩個化學量值已回查 PubChem 的官方計算屬性，該資料庫由 NCBI 維運，屬公告以外的來源 [(ref: pubchem_criz)](https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/crizotinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON)

**編輯：** Clarence

Google DeepMind 在 2026-11-03 發布一篇技術示範：研究者在 Antigravity（該公司的代理式開發環境）裡安裝新的 `Cheminformatics Skills`，由代理程式從文獻中抽取化合物、做 matched molecular pair analysis（MMPA，配對分子分析）、訓練活性預測模型，最後提出新的剛性化巨環（macrocycle）分子與合成路線。公告摘要句寫的是，這整段工作 `in just an hour` 完成，而同樣的流程 `typically takes multiple days for a single iteration` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

這篇文章值得記錄的不是它宣稱了什麼，而是它的示範結構：被拿來驗證代理程式的那個化學問題，答案在代理程式開始工作之前就已經寫在同一篇文章裡，而且被作者標示為 `well-known`。

## 背景

這則公告不是監管動作，也不是臨床產品上市，而是同一條產品線上的第二篇科學工作流程示範。要讀出它的位置，需要把兩條線排清楚：產品線的時間線，以及被選來示範的那個化學問題本身。

**產品線的時間線**

- **2026-10-15** — Google DeepMind 發布第一篇 Antigravity 科學示範 `Accelerating the search for antimicrobial peptides with Google Antigravity`，由代理程式在 UniProt 中篩選抗菌胜肽候選。本書庫已處理該則（見〈與書庫其他文章的關係〉）[(ref: amp)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- **2026-11-03 15:00 UTC** — 本則公告發布，主題自蛋白質換到小分子，並首次發表 `Cheminformatics Skills` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **2026-11-04 09:22 UTC** — 頁面最後修改時間（`dateModified`），較發布晚約十八小時 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **公告發布後的產品頁現況** — Antigravity 的科學用途頁已列出 `Accelerating cheminformatics` 區塊，並說明 Science 外掛可自應用程式內的 Customizations marketplace 一鍵安裝 [(ref: antigravity)](https://antigravity.google/use-cases/science?hl=en)。

**被選來示範的化學問題**

公告選的技術叫 rigidification（剛性化）。依公告的說明：藥物分子常以可旋轉鍵（rotatable bond）連接多個次結構，使分子在溶液中呈現多種構形；要與標靶結合時必須鎖定成單一活性構形，失去的運動自由度會付出熵的代價，削弱結合親和力。醫藥化學家因此加入新的鍵把次結構綁在一起，公告稱之為 `paying the entropic cost in advance` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

公告接著寫明：`Here, we will focus on a well-known case of successful rigidification.` 這個案例是 crizotinib 與 lorlatinib —— 依公告敘述，前者是用於某些非小細胞肺癌（non-small cell lung carcinoma, NSCLC）的第一代小分子酪胺酸激酶抑制劑（tyrosine kinase inhibitor, TKI），後者是第三代 TKI，結構相似但在末端環化，把有效的可旋轉鍵數降為零，因而有較高效價 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

也就是說，在代理程式被要求去搜尋文獻、做 MMPA、訓練模型之前，公告已經先用兩段文字告訴讀者：環化會降低可旋轉鍵數並提高效價，而且這在這個分子對上是已知的成功案例。後面代理程式做出來的 MMPA 結論與此一致 —— 公告對該結論的用詞是 `as expected` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

本則**沒有配圖**。公告頁內的截圖、互動式檢視器畫面與影片為 Google 自有素材，不在此重製。

## 事實（可核對）

以下區分**公告宣稱**、**公告正文的語彙邊界**，以及**回查 PubChem 官方計算屬性所得**。

### 公告自報的內容

- **摘要宣稱** — `Using real-world lung cancer treatments, an agent searches through thousands of compounds, performs matched molecular pair analysis, and proposes novel rigidified macrocycles with synthetic routes in just an hour.` 同段開頭寫既有流程 `typically takes multiple days for a single iteration`；文末再寫一次 `Not long ago, the workflow demonstrated here would have taken multiple days and required significant computational expertise` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **技術基礎** — 公告寫 `Grounded in RDKit, the foundational open source cheminformatics toolkit developed over two decades by a global community of contributors, alongside connectors to curated resources from ChEMBL and PubChem, the skills encode domain best practices directly into the agent's workflow.` 分工方式為語言模型負責流程編排、資料庫導航與科學推理，確定性的化學工具負責分子計算 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **檢索與整理** — 圖說寫 `Within minutes, the agent retrieves thousands of compounds, filters out irrelevant molecules (such as buffers and solvents), and documents their sources in a report.`，報告中並指出取得的巨環多數被預測可穿透腦部，公告說明這對易轉移至腦部的目標肺癌是重要性質。化合物數目只寫 `thousands`，未給確切數 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **MMPA 結論** — `The results of the analysis show that cyclization reduces the number of rotatable bonds while generally increasing potency, as expected.` 公告並寫 `The agent had also independently suggested this analysis, as we expect the dataset to include many informative pairs.` 亦即該分析是作者預期會有收穫、而代理程式也提出的同一項 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **模型與驗證** — `The agent also built a large number of potency models using varying feature sets and model architectures, and validated them on a held-out set.` 模型數只寫 `a large number`，held-out set 的規模、切分方式與任何一個評估數值皆未出現 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **切分方式的兩種說法** — 正文說代理程式在有時序資訊時「常」採 chronological split（以較舊化合物訓練、預測較新者），必要時改用 scaffold split；而實際示範的圖說寫的是 `across four different experimental read outs, using a scaffold split to better gauge out-of-distribution performance`。公告未說明這次為何落在後者 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **設計產出** — 代理程式提出新的巨環設計、醫藥化學理由與合成路線，並以前一輪訓練的模型預測各設計的效價；產出可匯出至業界標準化學軟體，或接 AlphaFold 與分子動力學模擬做後續分析。沒有任何一項設計的預測值被寫出來 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **公告自陳的限制** — `Sparse data, inter-lab assay noise, and narrow dynamic ranges limit the predictive precision of even the most powerful models; computational designs are testable hypotheses, not finished drugs.` 以及 `every proposed design must be synthesized and validated experimentally` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- **免費方案** — `we're offering 10,000 scientists the highest usage tier in Google Antigravity free of charge for 6 months (onboarded on a rolling basis), subject to eligibility, capacity, and selection` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。同一方案在產品頁上的寫法是 `We're giving 10,000 scientists our highest usage tier in Google Antigravity and our most advanced Gemini 4 Argon model, free of charge.` —— 人數相同，但產品頁全頁沒有出現 `6 months`，也沒有出現任何期限 [(ref: antigravity)](https://antigravity.google/use-cases/science?hl=en)。

### 公告正文沒有包含什麼

把公告正文（`<main>` 區塊）逐詞掃過，下列詞彙的命中數為零：`%`、`accuracy`、`AUC`、`RMSE`、`metric`、`peer`、`arXiv`、`DOI`、`preprint`、`code`、`github`、`clinical`、`patient`、`trial`、`FDA`、`regulat`。該區塊內的 `sup` 元素為 0 個，亦即全文沒有註腳 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

以阿拉伯數字寫出的量，全文只有四處：發布日期的 `3` 與 `2026`、關聯文章區塊的年份，以及免費方案的 `10,000` 與 `6`。亦即**整篇文章裡，沒有任何一個阿拉伯數字是在描述代理程式做出來的東西**。化學量值則以英文數詞寫出：`five`（crizotinib 的可旋轉鍵）、`zero`（lorlatinib）、`four different experimental read outs`（圖說）、RDKit 的 `two decades`、化學結構的 `millions` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

`<main>` 內共 20 個連結、去重後 13 個：4 個為社群分享與郵件分享連結，其餘指向 Antigravity 產品頁、兩個 Wikipedia 條目（IUPAC 命名法、Markush structure）、RDKit 官網、ChEMBL、PubChem、一份 Google 表單（免費方案申請）與兩篇同站文章。**沒有任何連結指向論文、預印本、程式碼或資料集** [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

### 回查 PubChem 所得

公告唯一的兩個化學量值可以逐項回查。PubChem 的 `Rotatable Bond Count` 是該資料庫公開的計算屬性（由 Cactvs 產生），不是實驗量測：

| 項目 | 公告寫法 | PubChem 計算屬性 |
|---|---|---|
| crizotinib | `there are five major rotatable bonds` | CID `11626560`，`RotatableBondCount` = **5**，分子式 `C21H22Cl2FN5O` |
| lorlatinib | `cyclized at its end to reduce the effective number of rotatable bonds to zero` | CID `71731823`，`RotatableBondCount` = **0**，分子式 `C21H19FN6O2` |

兩項皆與公告一致 [(ref: pubchem_criz)](https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/crizotinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON) [(ref: pubchem_lorl)](https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/lorlatinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON)。

這張表要說的不是公告寫錯了，而是相反：**公告裡唯一能被外部逐項核對的兩個數字，描述的是兩個早已上市的分子，不是代理程式**。而且核對它們所用的資料庫，正是公告自述 `Cheminformatics Skills` 所連接的資源之一。

### 宣稱涵蓋到哪裡

逐項核對後，公告的三類陳述可以分開：

- **成立且可外部核對** — crizotinib 五個可旋轉鍵、lorlatinib 零個；兩者的結構關係與剛性化的方向。
- **成立但只能依公告自述** — 代理程式檢索了數千個化合物、做了 MMPA、訓練了多個模型、提出了新設計與合成路線。這些是流程敘述，沒有可供外部重跑或比對的產物。
- **未成立或無從判斷** — 「一小時 vs 數天」的加速幅度（沒有量測方式、沒有被加速的基準流程定義、沒有人數與樣本數）；模型「在 held-out set 上驗證過」的驗證結果（沒有任何評估數值）；新設計的品質（沒有合成、沒有實驗，公告自己也說明了這一點）。

## 本書庫解讀（評論）

以下為本書庫的判讀，不是來源結論。

- **這是一次回溯示範（retrospective demonstration），而公告的結構讓它不容易被看出來。** 示範的標準做法是先設問、再讓系統作答、最後與獨立的正確答案比對。本則的順序是：先用兩段文字說明 crizotinib 到 lorlatinib 的剛性化是 `well-known case`、方向是環化降低可旋轉鍵並提高效價，然後讓代理程式去同一批文獻裡做 MMPA，得到同方向的結論，並標為 `as expected`。公告沒有寫錯任何一句，但一個由公告自己標為 `well-known`、且在同一篇文章前段就已向讀者說明方向的結論，被代理程式重新導出時，能證明的是工具鏈接得通，不是它能發現新知識。

- **「一小時 vs 數天」缺的是基準流程的定義，而不只是數字。** 即使拿掉「沒有實測」這一點，這個比較仍然無法使用：被壓縮的「數天」是指一位計算化學家從零開始建管線，還是一個已有內部工具的團隊跑一次既有流程？「一小時」包含不包含安裝外掛、設定資料庫連線、以及人在旁邊審視與重下指令的時間？公告的兩處寫法（`typically takes multiple days for a single iteration`、`would have taken multiple days and required significant computational expertise`）都把主體寫得很寬，寬到任何一種讀法都成立。本書庫在同一產品線的前一則已記錄過同一種寫法出現在網頁中繼資料裡；本則把它移進了正文，但三項必要資訊（改造前後同一任務的實測時間、樣本數、量測方式）一項都沒有補上。

- **「validated on a held-out set」是全篇最值得追問的一句。** 公告同時說代理程式建了「大量」模型、用不同特徵集與架構做了 benchmark、並在 held-out set 上驗證。這些詞都是評估語彙，但沒有任何一個隨附的數值 —— 沒有 R²、沒有 RMSE、沒有排序相關係數，連「最好的模型比最差的好多少」都沒有。公告選用 scaffold split 的理由寫得很清楚 —— `to better gauge out-of-distribution performance`，亦即刻意讓評估落在訓練時未見過的分子骨架上。選了較嚴格的評估設定卻一個結果都不公布，讀者無從分辨這是「表現夠好但省略」還是「表現不足以放進公告」。

- **切分方式的兩種說法沒有被交代。** 正文說有時序資訊時「常」採 chronological split，示範用的卻是 scaffold split。兩者都是合理選擇，但對於一篇以「技能把領域最佳實務編進代理程式工作流程」為賣點的文章，示範本身落在非預設路徑而未說明原因，削弱了「最佳實務已被編碼」這個宣稱的說服力。

- **公告的限制段寫得比多數同類公告誠實，值得單獨記錄。** `computational designs are testable hypotheses, not finished drugs`、`every proposed design must be synthesized and validated experimentally`、以及對資料稀疏、跨實驗室檢定雜訊與動態範圍過窄的點名，都是正確且具體的。問題不在這一段，而在於它與摘要句之間的落差：摘要句用 `in just an hour` 作為賣點，限制段則說明產出只是待驗證的假說。兩段都在同一頁上，但只有前者會進到轉述裡。

- **醫療橋接（一）：在答案已知的案例上做示範，等於在醫學影像裡拿教科書病例做讀片者研究。** 醫學影像 AI 的日常評估也有同一個陷阱 —— 以公開資料集中標註明確、文獻中已被反覆討論的典型病例展示模型，結論通常成立，卻無法說明模型在未見過的、分佈外的病例上會怎麼表現。本則提供的檢查方式很直接：看示範所用案例的正確答案是不是在示範開始前就已經公開，以及是否存在於系統的訓練資料中。如果兩者皆是，該示範能支持的結論僅止於「流程可以跑通」。

- **醫療橋接（二）：「省下幾天」這類宣稱在科室導入評估上與本則同構。** 影像後處理、報告生成與排程工具的廠商宣稱常是同一句型。要據此估人力或投資回收，需要的是改造前後在相同案例組成下的實測週轉時間、樣本數與量測方式三項。本則示範了缺少這三項時會發生什麼：同一段文字可以同時支持「省下數天」與「省下一次迭代」兩種差距極大的讀法，而兩者都無法被否證。

## 產業／生態影響

- **代理式平台的科學外掛正在從蛋白質擴到小分子。** 自 2026-10-15 的抗菌胜肽示範到本則的小分子示範，相隔十九天，覆蓋面自 UniProt 與 AlphaFold 擴及 RDKit、ChEMBL 與 PubChem [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/) [(ref: amp)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。對使用這些公共資料庫的團隊而言，這意味著資料庫欄位的品質與出處標示會直接影響代理式工作流程的輸出，而不只影響人工查詢。

- **確定性工具與語言模型的分工是這條產品線明確的設計選擇。** 公告把化學計算交給 RDKit 這類確定性工具，語言模型只做編排、導航與推理 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。這個分工值得記錄：它把「分子結構被改錯一個原子就是另一個化合物」這類不容錯的步驟留在可驗證的程式裡。同樣的分工在醫學影像上對應到「量測與幾何運算交給確定性演算法、語言模型只負責串接與敘述」，是可以直接借用的架構原則。

- **同一免費方案在兩個官方位置的寫法不一致。** 公告寫 `free of charge for 6 months`、`onboarded on a rolling basis`、`subject to eligibility, capacity, and selection`；產品頁寫 `free of charge`，全頁無任何期限字樣 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/) [(ref: antigravity)](https://antigravity.google/use-cases/science?hl=en)。申請者若只讀產品頁，不會知道方案有六個月期限與篩選條件。這類跨頁面的條件落差在評估任何廠商免費方案時都值得先查一次。

- **這條產品線至今沒有產出可供第三方重現的成果物。** 兩篇示範都沒有論文、預印本、程式碼或資料集連結 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/) [(ref: amp)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。若免費方案如期開放給一萬名科學家，短期內會有相當數量的分析與候選分子以同一套工具產生；在沒有任何公開基準的情況下，這批產出的品質分佈將無從估計。

## 與書庫其他文章的關係

同一產品線相隔十九天的第二篇科學示範，而兩則的證據缺口只是換了位置、沒有補上 —— 該則的加速宣稱只寫在網頁中繼資料與產品頁上、正文一次都沒量過時間；本則把「一小時」正式寫進了正文第二段，但量測方式、樣本數與被壓縮的基準流程定義仍然三項皆無。兩則並讀可以看出同一種宣稱如何在版本之間變得更醒目而非更可查: [DeepMind 說把數天縮成一次對話，全文沒量過任何一段時間](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

兩則是前沿模型供應商相隔七天發布的藥物開發成果，可回查程度差一整級：該則的爭點在於一個倍數出自單一個孔、成功標準是事後才定的，至少有孔數與成功標準可供爭論；本則在代理程式那一側沒有產生任何數值，連可以爭論的對象都不存在。把兩則並讀可以看出「廠商自報」也分成可被挑錯與無從挑起兩種: [「結塊慢 100 倍」出自單一個孔，成功標準是事後才定的](2026-10-28-anthropic-drug-development-case-studies.md)

同一家公司相隔一天的兩則發布恰好構成對照：該則主張健康 AI 的評估要同時涵蓋 closed-question benchmarks、autoraters 與 expert human review 三種方法，並把量化門檻留給各團隊自訂；本則的示範則是那套框架所指的第一種評估的反面 —— 模型被建起來、被宣稱在 held-out set 上驗證過，卻沒有公布任何一個評估數值。兩則並讀可以看出「有評估框架」與「公布評估結果」是兩件事: [Google 公開健康 AI 評估框架，及格線留給各家自己訂](2026-11-05-google-health-ai-evaluation-framework.md)

## 實務的啟發

- **評估任何 AI 工具的示範時，先查示範案例的正確答案是什麼時候公開的。** 本則的檢查只要兩步：公告自己寫了 `well-known case` [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)，而兩個分子的結構與可旋轉鍵數在公開資料庫中可以直接查到 [(ref: pubchem_lorl)](https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/lorlatinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON)。一個在示範之前就已公開的答案，無法區分「系統推導出結論」與「系統複述結論」。內部評估新工具時，把「案例答案的公開日期」固定記成一欄，成本極低而且能擋掉大部分看起來很有說服力的示範。

- **看到「在 held-out set 上驗證」就追問三件事：切分方式、集合大小、評估數值。** 本則三項全缺，卻同時使用了 benchmark、validated、out-of-distribution 這組詞。這是可以直接寫進內部採購問卷的三個欄位；廠商若能答出前兩項卻不給第三項，本身就是一個資訊。

- **把「省下幾天」記為「未提供量測」，不要記為效益。** 需要的是改造前後同一任務的實測時間、樣本數與量測方式。本則示範了缺少這三項時，同一句話可以同時支持差距極大的多種讀法。

- **借用「確定性工具 + 語言模型編排」這個分工，並明確劃出不容錯的步驟。** 本則把分子計算交給 RDKit、把編排交給模型。醫學影像的對應作法是把量測、幾何運算、單位換算與座標轉換留在確定性程式裡，讓語言模型只負責串接、查詢與敘述；哪些步驟屬於「錯一個值就是另一個病例」，應該在設計階段就列出來。

- **採用廠商免費或優惠方案前，把同一方案在所有官方頁面上的條件並排看一次。** 本則的免費方案在公告與產品頁上的期限寫法不同（一處寫六個月，一處無期限）。這類落差不必然是刻意，但只讀其中一頁就足以對承諾產生誤解。

## 後續追蹤

- `Cheminformatics Skills` 是否出現任何帶絕對數值的評估報告 —— 例如模型在 scaffold split 上的具體指標、或同一任務在導入前後的實測時間與人數。目前公告與產品頁皆無 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/) [(ref: antigravity)](https://antigravity.google/use-cases/science?hl=en)。
- 公告中代理程式提出的那些巨環設計是否被實際合成並測定活性。公告自述每一個設計都必須經合成與實驗驗證，但未給任何時程 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- 這條產品線是否開始產出同儕審查論文、預印本或可執行的程式碼。至今兩篇示範的連結中皆無 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/) [(ref: amp)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- 是否出現以答案未知的案例（而非 `well-known case`）進行的示範，亦即前瞻性的設計與驗證 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。
- 面向一萬名科學家的免費方案實際開放規模、篩選條件，以及產品頁是否補上六個月期限 [(ref: antigravity)](https://antigravity.google/use-cases/science?hl=en)。
- 第三方是否以公開工具重現同一條 MMPA 與活性預測流程，並公布可比較的數值 [(ref: pr)](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)。

## References

- `pr` — Google DeepMind，[Agentic cheminformatics with Google Antigravity](https://deepmind.google/blog/agentic-cheminformatics-with-google-antigravity/)（官方部落格，頁面可見 `November 3, 2026`；`meta article:published_time` 與 JSON-LD `datePublished` 皆為 `2026-11-03T15:00:00+00:00`，`dateModified` 為 `2026-11-04T09:22:30.548258+00:00`；作者 Zoi Tsangalidou、Ruijie (Kelly) Zhang、Sukhdeep Singh、Michael V. LeVine）。底 URL：`https://deepmind.google/blog/`
- `amp` — Google DeepMind，[Accelerating the search for antimicrobial peptides with Google Antigravity](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)（官方部落格，2026-10-15，同一產品線的前一篇科學示範）。底 URL：`https://deepmind.google/blog/`
- `antigravity` — Google，[Why choose Google Antigravity for science](https://antigravity.google/use-cases/science?hl=en)（官方產品頁；本文引述以英文版 `?hl=en` 為準）。底 URL：`https://antigravity.google/`
- `pubchem_criz` — NCBI PubChem，[crizotinib（CID 11626560）計算屬性](https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/crizotinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON)（PUG REST 屬性查詢；`RotatableBondCount` 為 PubChem 公開的計算屬性，非實驗量測）。底 URL：`https://pubchem.ncbi.nlm.nih.gov/compound/11626560`
- `pubchem_lorl` — NCBI PubChem，[lorlatinib（CID 71731823）計算屬性](https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/lorlatinib/property/MolecularFormula,RotatableBondCount,SMILES,IUPACName/JSON)（PUG REST 屬性查詢；同上）。底 URL：`https://pubchem.ncbi.nlm.nih.gov/compound/71731823`

[Home](../) · [Industry Watch](./)
