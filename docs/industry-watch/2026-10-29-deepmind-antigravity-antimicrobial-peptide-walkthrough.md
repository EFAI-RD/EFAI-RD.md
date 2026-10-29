---
title: "Google DeepMind 示範用 Antigravity 搜尋抗菌胜肽：「數天變成一次對話」「in hours」「數小時變成數分鐘」三種加速說法分屬三個官方位置，沒有一個附得出絕對數值；而那個候選分子在 UniProt 的名稱，證據欄寫的是 Google:ProtNLM"
category: industry-watch
date: 2026-10-29
updated: 2026-10-29
tags: [Google-DeepMind, Google-Antigravity, ProtNLM, AlphaFold, UniProt, antimicrobial-peptides, bacteriocin, antimicrobial-resistance, drug-discovery, agentic-workflow, automatic-annotation, data-provenance]
catalog_id: "google-deepmind:antigravity-antimicrobial-peptide-walkthrough-2026-10-15"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.0"
source:
  orgs:
    - "Google DeepMind"
  event: "發布技術示範文章 Accelerating the search for antimicrobial peptides with Google Antigravity，說明研究者如何在 Antigravity 中以代理程式從 UniProt 挑出一個抗菌胜肽候選分子，並發表內建的 Biomolecular Structure Viewer"
  event_date: "2026-10-15"
  official_url: "https://deepmind.google/blog/accelerating-antimicrobial-discovery/"
related_articles:
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "兩則是前沿模型供應商相隔十二天發布的生命科學成果公告，而本則比該則更早一步 —— 該則至少有六份技術報告可以把公告數字逐項回查，本則除了一個資料庫編號之外沒有任何可回查的量測，全部成果都停在 wet-lab validation 之前"
  - path: "2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md"
    relation: "該則預測 agentic workflow 的推論成本到 2028 年增加逾五倍卻沒有給任何絕對量，本則則是同一種寫法出現在效益側 —— 三個官方位置給了三種加速說法，分母與基準全部缺席，兩則並讀可以看出成本與效益在缺少絕對值時同樣無法進入任何採購試算"
  - path: "2026-10-20-google-amie-lancet-primary-care-feasibility.md"
    relation: "同一家公司相隔七天的兩則發布，可回查程度相差一整個層級 —— 該則有同儕審查論文、開放預印本與試驗登錄可以逐項對照，問題只出在哪個百分比被挑出來放進標題；本則連一篇預印本都沒有，正文的 peer、paper、arXiv、DOI 命中數皆為零"
refs:
  pr:
    title: "Google DeepMind：Accelerating the search for antimicrobial peptides with Google Antigravity（官方部落格，2026-10-15）"
    url: "https://deepmind.google/blog/accelerating-antimicrobial-discovery/"
  uniprot:
    title: "UniProtKB：A0A0U0D591 · Lactococcin 972 family bacteriocin（Streptococcus pseudopneumoniae，官方資料庫條目）"
    url: "https://www.uniprot.org/uniprotkb/A0A0U0D591/entry"
  protnlm:
    title: "UniProt：Automatic annotation using ProtNLM（官方說明頁）"
    url: "https://www.uniprot.org/help/ProtNLM"
  antigravity:
    title: "Google Antigravity：Why choose Google Antigravity for science（官方產品頁）"
    url: "https://antigravity.google/use-cases/science"
  amr:
    title: "Public Health England：Health matters: antimicrobial resistance（GOV.UK 官方指引）"
    url: "https://www.gov.uk/government/publications/health-matters-antimicrobial-resistance/health-matters-antimicrobial-resistance"
---

[Home](../) · [Industry Watch](./)

# Google DeepMind 示範用 Antigravity 搜尋抗菌胜肽：「數天變成一次對話」「in hours」「數小時變成數分鐘」三種加速說法分屬三個官方位置，沒有一個附得出絕對數值；而那個候選分子在 UniProt 的名稱，證據欄寫的是 Google:ProtNLM

## 來源

- 組織：Google DeepMind（產品為 Google Antigravity；文中涉及的 UniProt 由 UniProt consortium 維運，AlphaFold Protein Structure Database 由 DeepMind 與 EMBL-EBI 共同維運）
- 事件：發布技術示範文章 `Accelerating the search for antimicrobial peptides with Google Antigravity`，並發表內建於 Antigravity 的 `Biomolecular Structure Viewer`
- 日期：2026-10-15（頁面可見 `October 15, 2026`，`meta article:published_time` 與 JSON-LD `datePublished` 皆為 `2026-10-15T16:00:00+00:00`，三處一致）
- 官方入口：<https://deepmind.google/blog/accelerating-antimicrobial-discovery/>
- 作者署名：Pengfei Tian、Maxwell L. Bileschi、Zoi Tsangalidou、Sukhdeep Singh、Lucy J. Colwell
- 本則**事件本身為單源（Google 單一組織），待交叉驗證** —— 公告與其所連結的產品頁同屬 Google，沒有第三方聲明。但文中關於該候選分子的硬事實已回查 UniProt 官方條目與 UniProt 官方說明頁，這兩者由 UniProt consortium 維運，屬公告以外的來源 [(ref: uniprot)](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)

**編輯：** Clarence

Google DeepMind 在 2026-10-15 發布一篇技術示範：研究者在 Antigravity（該公司的代理式開發平台）裡設定一個生物學目標 —— 在 *Streptococcus pseudopneumoniae* 中尋找新的抗菌胜肽 —— 由代理程式跨資料庫查詢、比對結構、讀基因體鄰域、整理文獻，最後產出一份實驗計畫。文章同時發表 `Biomolecular Structure Viewer`，一個嵌進 Antigravity 的 3D 結構檢視器 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。

公告正文約 1,390 字。把它逐詞掃過之後，有兩件事值得先講清楚。

第一，這篇文章的賣點是加速，但它沒有量過任何一段時間。正文裡 `hours` 出現 0 次，`days` 出現 1 次，而那一次是「turning days of fragmented database triage into a single collaborative session」—— 舊流程「數天」沒有量測來源，新流程「一次協作對話」也沒有時長。同一頁的 `meta description` 與 `og:description`（亦即搜尋結果與社群預覽會顯示的那一段）寫的卻是 `...prioritize novel antimicrobial peptides **in hours**`，而 `hours` 這個詞在正文中一次都沒有出現。產品頁上這件事又換了第三種寫法：`condensing hours of manual structural analysis into minutes` [(ref: antigravity)](https://antigravity.google/use-cases/science)。三個官方位置、三種說法，沒有一個給得出被壓縮前後的實測值。

第二，被當成成果展示的那個候選分子，是 UniProt 編號 `A0A0U0D591`。回查該條目之後，它的名稱 `Lactococcin 972 family bacteriocin` 在 UniProt 的證據欄位上寫的是 `Automatic Annotation (ECO:0008006) Google:ProtNLM` —— 也就是說，代理程式在資料庫裡「找到一個 bacteriocin」時所讀到的那個名稱，正是 Google 自家模型先前寫進去的 [(ref: uniprot)](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)。公告本身並未隱瞞 ProtNLM 是 Google 開發的，但它沒有說明這個特定候選分子的名稱來源，而這決定了整條證據鏈該怎麼讀。

## 背景

這則公告不是一項監管動作或產品上市，而是一篇把既有資產串起來的技術示範。要理解它的範圍，需要先把四個時間點排清楚，因為它們分屬不同主體、而公告把它們寫成同一件事的不同步驟。

- **2016-02-17** — UniProt 條目 `A0A0U0D591` 首次公開，序列版本 1，此後序列從未更新。該序列來自 *Streptococcus pseudopneumoniae* 菌株 Spain2270 的全基因體散彈定序（whole genome shotgun, WGS）計畫，開放閱讀框編號 `D6867_00595`。條目至今掛著一則 UniProt 的 `Caution`：`The sequence shown here is derived from an EMBL/GenBank/DDBJ whole genome shotgun (WGS) entry which is preliminary data` [(ref: uniprot)](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)。
- **UniProt release 2022_04 起** — UniProt 開始把 ProtNLM 預測的蛋白質名稱填進原本名為 `uncharacterized protein` 的 TrEMBL 條目。UniProt 官方說明頁寫明 ProtNLM 是「developed by collaborators at Google DeepMind」，並指出這類標註可由 `Automatic Annotation (ECO:0008006) Google:ProtNLM` 這個證據標籤辨識，也可以用搜尋語法 `source:google` 篩出 [(ref: protnlm)](https://www.uniprot.org/help/ProtNLM)。
- **2026-09-02** — 該條目最近一次標註更新（版本 48）。條目唯一引用的文獻是一筆 2018 年 9 月的資料庫提交紀錄，沒有任何期刊論文 [(ref: uniprot)](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)。
- **2026-10-15** — Google DeepMind 發布本則公告，把這個條目描述為代理程式從數百萬筆資料中篩出的候選，並表示它與同一管線產出的其他數個候選已進入 wet-lab validation [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。

換句話說，這條序列在公開資料庫裡已經存在十年又八個月；公告描述的工作是在既有條目上做檢索、結構比對與文獻整理，不是定序或合成出一個新分子。公告沒有寫錯，但它用 `uncover`、`discovery`、`previously uncharacterized` 這組詞描述這段過程，讀者若不回查條目，容易把它讀成一個分子被發現。

## 事實（可核對）

以下區分**公告宣稱**與**回查 UniProt 官方條目所得**。

### 公告自報的內容

- **目標與範圍** — 研究者設定的目標是 `find and computationally validate novel AMPs in Streptococcus pseudopneumoniae`（AMP 即 antimicrobial peptide，抗菌胜肽）；公告自述這次對話聚焦於 `a narrow amino acid window` [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- **六張投影片的工作流程** — 依序為資料庫篩選、以 EMBL-EBI 的 NCBI-BLAST 服務對 Swiss-Prot 查新穎性、取 AlphaFold 預測結構做遠源同源比對、讀基因體鄰域、整理文獻形成機制假說、產出實驗計畫 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- **基因體鄰域** — 公告稱該候選位於一個緊密耦合的 operon 上游，距離一個 ABC transporter permease 僅 6 個鹼基對，鄰近另有一個已標註的 bacteriocin 與一個 XRE 轉錄調控因子。本文未獨立核對這項基因體排列，僅記為公告宣稱 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- **機制與活性為預測** — 公告寫的是 `existing evidence suggests a mechanism of action targeting bacterial cell division, and a predicted potency spectrum spanning several drug-resistant pathogens`。這是從文獻推得的假說，不是量測 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- **尚未驗證** — 公告自己寫明 `it still requires wet lab validation`，並說候選已進入 wet-lab validation，`where experimental results will provide the ultimate test of the agent's analysis` [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- **唯一的量化風險陳述** — `could result in an estimated 10 million annual deaths globally by 2050`，連結指向 GOV.UK 的 `Health matters: antimicrobial resistance`。該頁由 Public Health England 發布，頁面可見的發布日為 `Published 10 December 2015`，內文寫的是「an estimated 10 million deaths every year globally by 2050」以及「a cost of £66 trillion in lost productivity」 [(ref: amr)](https://www.gov.uk/government/publications/health-matters-antimicrobial-resistance/health-matters-antimicrobial-resistance)。

### 正文逐詞計數（說明這篇文章沒有包含什麼）

正文約 1,390 字，`<main>` 區塊內有 0 個 `sup` 元素，亦即全文沒有註腳。下列詞彙在正文中的命中數為零：`hours`、`%`、`peer`、`paper`、`arXiv`、`DOI`、`clinical`、`patient`、`benchmark`、`accuracy`、`baseline`、`control`、`MIC`（minimum inhibitory concentration，最小抑菌濃度）、`in vivo`、`validated`。出現的是 `predict` 10 次、`predicted` 4 次、`candidate` 12 次、`validation` 4 次、`wet-lab` 4 次 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。`<main>` 內的連結共 7 個，其中 2 個是同一個 Antigravity 導流連結；其餘指向 GOV.UK、UniProt 首頁、UniProt 的 ProtNLM 說明頁、該候選條目與 AlphaFold 資料庫。**沒有任何連結指向論文、預印本、程式碼或資料**。

### 回查 UniProt 條目所得

| 欄位 | 條目實際內容 |
|---|---|
| 條目狀態 | `UniProtKB unreviewed (TrEMBL)`（TrEMBL 為 UniProtKB 未經人工審閱的部分，相對於人工審閱的 Swiss-Prot） |
| Protein existence | `4: Predicted`（UniProt 五級證據中倒數第二級） |
| Annotation score | 1（滿分 5） |
| 名稱證據 | `Automatic Annotation (ECO:0008006) Google:ProtNLM` |
| 長度／分子量 | 97 個胺基酸／10,408 Da |
| 首次公開／序列最後更新 | 皆為 2016-02-17（序列版本 1） |
| 標註最後更新／條目版本 | 2026-09-02／版本 48 |
| 文獻 | 僅一筆 2018 年 9 月的資料庫提交，無期刊論文 |
| Caution | 序列源自 WGS 條目，屬 preliminary data |

公告提到的 97 個胺基酸、Lactococcin 972 家族、*S. pseudopneumoniae* 三項與條目一致 [(ref: uniprot)](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)。

### 「novel」這個詞涵蓋到哪裡

公告的原句有明確限定：`confirm this peptide has no meaningful sequence homolog among manually reviewed proteins`。這句話沒有寫錯，但 `manually reviewed` 指的是 Swiss-Prot。以 UniProt 官方 API 查詢當下的規模：

- 已審閱（Swiss-Prot）條目：**575,748**
- 未審閱（TrEMBL）條目：**149,430,635**

亦即這項新穎性檢查的比對範圍約為 UniProtKB 的 0.38%。把範圍放大到全庫之後，同樣以 UniProt API 查得：

- 與該候選同屬一個 UniRef50 叢集（50% 序列相同度）的條目：**6** 筆；UniRef90 與 UniRef100 叢集則各只有 **1** 筆，表示庫中沒有近乎相同的序列
- 蛋白質名稱為 `Lactococcin 972 family bacteriocin` 的條目：**929** 筆，其中已審閱者：**0** 筆
- 其中屬於 *S. pseudopneumoniae*（taxonomy id 257758）者：**3** 筆

所以「在人工審閱的子集中沒有有意義的同源序列」成立；「在整個 UniProtKB 中沒有相似序列」則不成立 —— 同家族名稱底下有 929 筆，50% 相同度層級有 6 筆。公告沒有宣稱後者，但標題與摘要用的是不帶限定的 `novel`。

### ProtNLM 的兩個版本，與圖說裡被換掉的那個 2

UniProt 官方說明頁把 ProtNLM 與 ProtNLM2 分得很清楚 [(ref: protnlm)](https://www.uniprot.org/help/ProtNLM)：

- **ProtNLM（已整合進條目）** — 只預測蛋白質名稱，模型分數門檻 0.2。全庫以 `source:google` 可篩出 **12,993,526** 筆帶有 ProtNLM 預測名稱的條目，其中已審閱者 **0** 筆。
- **ProtNLM2（未整合，平行儲存）** — 預測範圍擴及 function comments、subcellular locations、keywords 與 Gene Ontology（GO）terms，門檻降為 0.05，但加掛一套稱為 `Evidencer` 的後處理：以字串比對、`phmmer` 序列相似度（bit score > 25）或 `TM-align` 結構相似度等條件尋找佐證，無法佐證者不顯示。試行版涵蓋約 26,000 筆條目，於 UniProt 2026_02 釋出。

這個區分對本則很關鍵：`A0A0U0D591` 的名稱是**整合進條目**的那一種，走的是 ProtNLM 第一版、只過 0.2 分數門檻的路徑，**沒有**經過 ProtNLM2 的 `Evidencer` 佐證流程。

而公告的第一張圖說是這樣寫的：`Overview of the ProtNLM pipeline translating raw amino acid sequences into natural-language biological annotations for unreviewed UniProtKB/TrEMBL entries. The functional annotation scope of the system covers protein names, function comments, subcellular locations, and GO terms, in addition to keywords.` 把它與 UniProt 說明頁對照，這段文字是該頁兩張圖的圖說接起來的：第一句逐字相同；第二句在 UniProt 頁上原文為 `The functional annotation scope of **ProtNLM2**, covering...`，公告把 `ProtNLM2` 換成了 `the system`。結果是，公告用來描述「ProtNLM 管線」能力範圍的那句話，在 UniProt 的原始語境裡描述的是另一個版本 —— 而那個版本的輸出並沒有被整合進本則候選分子所在的條目。

UniProt 在同一頁也寫著：`machine learning AI models do make errors. We invite users to carefully evaluate these predictions` [(ref: protnlm)](https://www.uniprot.org/help/ProtNLM)。

## 本書庫解讀（評論）

以下為本書庫的判讀，不是來源結論。

- **整條鏈上只有一步來自 Google 以外。** 候選的名稱來自 ProtNLM（Google DeepMind 開發），結構取自 AlphaFold Protein Structure Database（DeepMind 與 EMBL-EBI 共同維運），執行環境是 Antigravity（Google）。唯一完全外部的步驟是透過 EMBL-EBI 的 NCBI-BLAST 服務對 Swiss-Prot 做序列比對。公告寫「structural evidence corroborates ProtNLM's prediction」是誠實的描述，但讀者需要知道：被佐證的那個預測與做佐證的那個結構預測，出自同一個組織的兩個模型。這不使結論無效，它只是把「獨立佐證」的強度降了一級，而公告沒有把這一級標出來。

- **三種加速說法的共同問題是沒有分母。** 「數天變成一次協作對話」「in hours」「數小時變成數分鐘」—— 誰的數天、哪一段的數小時、由誰在什麼條件下量的，三處都沒有寫。這類相對陳述在閱讀時幾乎沒有成本，在採購或資源規劃時卻完全不能用：要估一個團隊導入後省下多少人時，需要的是改造前後同一項任務的實測時間與人數，而不是兩個量綱不明的副詞。本書庫先前在成本側記錄過同一種寫法（見〈與書庫其他文章的關係〉的 Gartner 一則）；本則是同一種寫法出現在效益側。

- **「資料庫欄位是誰寫的」已經是一個必須查的問題。** 全庫有 12,993,526 筆條目的蛋白質名稱由 ProtNLM 寫入，其中沒有一筆經過人工審閱。值得肯定的是 UniProt 把這件事做成了可查詢的欄位 —— `Automatic Annotation (ECO:0008006) Google:ProtNLM` 這個標籤加上 `source:google` 搜尋語法，讓任何人都能把模型產生的標註篩出來或排除掉。這是出處標示的好範例。問題不在 UniProt，而在下游：當一篇公告以這些欄位為起點展示成果時，出處資訊並不會跟著被複述。

- **醫療橋接（一）：取用公開資料庫時要先問欄位的出處。** 這一點直接對應醫療影像 AI 的日常。放射科報告經規則式或語言模型抽取而來的標籤（例如以文本標註器從報告產出的影像層級標籤）、由模型預測再回填的結構化欄位、自動分割產生的體積數值 —— 這些在資料集裡與人工判讀的欄位長得一模一樣。本則提醒的作法是：在把任何公開資料庫欄位當成 reference standard 之前，先找它的出處欄位；找不到出處欄位的資料集，等於無法排除「用模型的輸出訓練並評估下一個模型」。UniProt 提供了這個欄位，多數醫療影像資料集沒有。

- **醫療橋接（二）：相對加速宣稱在臨床工作流程上同樣無法落地。** 「把判讀時間縮短」「把報告產出從數小時縮為數分鐘」是取像端與報告端廠商最常見的宣稱句型，與本則三處說法同構。科室要據此排班、估人力或計算投資回收，需要的是改造前後在相同病例組成下的實測週轉時間、樣本數與量測方式。本則示範了這類宣稱在缺少絕對值時可以同時存在三個版本而彼此不衝突 —— 因為三者都無法被否證。

- **這篇文章本身的定位是產品示範，不是研究成果。** 公告沒有宣稱任何已驗證的抗菌活性，也沒有宣稱任何核准；它的結論句是候選已進入 wet-lab validation。把它當成產品能力的示範來讀是恰當的；把它當成一個抗菌胜肽被發現來讀則超出了公告自己的主張。

## 產業／生態影響

- **代理式平台正在把生命科學資料庫當成一級介面。** 產品頁宣稱 Antigravity 可對 `more than 30 major life-science databases` 立即上手，包括 `1PB AlphaGenome Atlas`、UniProt、PubChem 與 ChEMBL，並提供可安裝的 Science 外掛 [(ref: antigravity)](https://antigravity.google/use-cases/science)。這意味著資料庫的欄位品質與出處標示，會直接決定代理式工作流程的輸出品質 —— 而不是只影響人工查詢。

- **免費方案的規模值得記錄。** 產品頁寫明將提供 `10,000 scientists` 最高用量級別與 Gemini 4 Argon 模型，免費 [(ref: antigravity)](https://antigravity.google/use-cases/science)。若實際落地，短期內會有相當數量的候選分子與分析流程以同一套工具產生；這對後續的重複性評估既是機會也是風險。

- **模型標註回灌資料庫的循環已經成形。** ProtNLM 以 UniProtKB 的快照訓練，再把預測名稱寫回 UniProtKB 的未審閱部分，目前涵蓋約 1,299 萬筆。UniProt 以 `Evidencer` 這類佐證機制與明確的出處標籤在控制這個循環，而這套機制目前只套用在未整合進條目的 ProtNLM2 預測上。這個治理設計對所有要把模型輸出寫回公共資料資產的領域（包括醫學影像的公開標註集）都有參考價值。

- **產品頁的語彙邊界很清楚。** 該頁逐詞計數中 `clinical`、`patient`、`medical`、`diagnos`、`regulat`、`FDA` 命中皆為 0 [(ref: antigravity)](https://antigravity.google/use-cases/science)。亦即 Google 在這條產品線上把定位放在研究工作流程，而非臨床或受監管用途。閱讀時不宜把它往臨床方向外推。

## 與書庫其他文章的關係

兩則是前沿模型供應商相隔十二天發布的生命科學成果公告，而本則比該則更早一步 —— 該則至少有六份技術報告可以把公告裡的每一個數字逐項回查，本則除了一個資料庫編號之外沒有任何可回查的量測，所有成果都停在 wet-lab validation 之前；兩則並讀可以看出同一類公告在「可查核物存不存在」這一軸上的兩個位置: [Anthropic 公布 Claude 參與的六個藥物開發合作案：公告說抗體「結塊慢 100 倍以上」，技術報告寫明那是單一個孔的讀數，而判定成功的規格是看過結果之後才定的](2026-10-28-anthropic-drug-development-case-studies.md)

該則預測 agentic workflow 的推論成本到 2028 年增加逾五倍，卻沒有給任何絕對量、也沒有基準年；本則是同一種寫法出現在效益側 —— 三個官方位置給出三種加速說法，而被壓縮前後的實測值一律缺席。兩則並讀可以看出成本與效益在缺少絕對值時的對稱性：都無法被否證，也都無法進入任何採購試算: [Gartner 預測「每個」agentic workflow 的推論成本到 2028 年增加逾五倍，並提出 Inference Paradox；新聞稿全文沒有起算基準](2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md)

同一家公司相隔七天的兩則發布，可回查程度相差一整個層級：該則有同儕審查論文、開放預印本與試驗登錄可以逐項對照，爭點只在哪一個百分比被挑進標題；本則的正文裡 `peer`、`paper`、`arXiv`、`DOI` 命中數全部為零，唯一能回查的對象是一個公開資料庫條目。把兩則並讀可以看出「同一家公司的官方發布」不是一種均質的證據等級: [Google 宣傳 AMIE 的 Lancet 研究：「鑑別診斷與醫師最終診斷相符 90%」是前七名清單的命中率，同一天更新的自家研究部落格寫著排第一名的只有 56%](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

## 實務的啟發

- **引用公開資料庫的任一欄位之前，先把它的出處欄位一起抄下來。** UniProt 的作法可以直接照搬成內部規範：每一筆被引用的標註都記錄其證據標籤（本則為 `Automatic Annotation (ECO:0008006) Google:ProtNLM`）與條目狀態（本則為 `unreviewed (TrEMBL)`、Protein existence `4: Predicted`、Annotation score 1/5）。這三項資訊在條目頁上都是公開的，抄錄成本接近零，而少了它們就無法判斷一筆標註該被當成事實還是當成待驗證的預測。

- **看到「新穎」「首見」「無同源」這類詞時，先找它的比對範圍。** 本則的 `no meaningful sequence homolog` 是對 575,748 筆已審閱條目成立，而全庫有 149,430,635 筆。範圍一換，同家族名稱底下還有 929 筆。這個檢查適用於所有宣稱新穎性的材料：問的不是「有沒有比對過」，而是「比對的母體是什麼、佔全體多少」。

- **對任何加速宣稱，要求改造前後的實測值、樣本數與量測方式三項。** 本則示範了缺少這三項時會發生什麼：同一件事可以在三個官方位置寫成三種互不相同的說法而不互相矛盾。採購或導入評估時，把「數天變成數分鐘」這類句子直接記為「未提供量測」，而不是記為一項效益。

- **區分「模型提出的假說」與「已量測的結果」，並讓這個區分進到文件裡。** 本則所有生物學結論都是預測：功能來自語言模型、結構來自結構預測、機制與活性譜來自文獻推論。公告自己標示得很清楚，但這些詞在轉述時最容易脫落。內部整理時建議固定分欄登記 —— 預測、佐證方式、是否有濕式實驗結果。

- **若團隊計畫把模型輸出寫回內部的共用資料資產，先設計出處標籤與佐證門檻。** UniProt 的組合值得參考：可查詢的證據標籤、明確的模型分數門檻（ProtNLM 名稱為 0.2、ProtNLM2 為 0.05）、以及一套在顯示前要求外部佐證的後處理流程，而未達佐證條件者不顯示。醫療影像的內部標註庫若要納入模型預測，同一組機制可以直接對應。

## 後續追蹤

- 該候選分子的濕式實驗結果是否公布，以及是否出現最小抑菌濃度等可量測的活性數值。公告僅稱已進入 wet-lab validation，未給時程 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- 這條管線是否產出同儕審查論文或預印本。目前公告正文沒有任何指向論文、資料或程式碼的連結 [(ref: pr)](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)。
- UniProt 條目 `A0A0U0D591` 的狀態是否因後續實驗而改變 —— 特別是 Protein existence 是否自 `4: Predicted` 升級，以及名稱的證據標籤是否自 `Google:ProtNLM` 改為人工審閱 [(ref: uniprot)](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)。
- ProtNLM2 的 `Evidencer` 是否擴大適用、或其預測是否開始整合進條目本身。目前試行版約 26,000 筆、平行儲存且不整合 [(ref: protnlm)](https://www.uniprot.org/help/ProtNLM)。
- Antigravity 的科學工作流程是否出現任何帶絕對數值的效能報告 —— 例如同一項任務在導入前後的實測時間與人數。三個官方位置目前皆無 [(ref: antigravity)](https://antigravity.google/use-cases/science)。
- 面向 10,000 名科學家的免費方案實際開放規模與條件，以及是否出現第三方對同一管線的重現嘗試 [(ref: antigravity)](https://antigravity.google/use-cases/science)。

## References

- `pr` — Google DeepMind，[Accelerating the search for antimicrobial peptides with Google Antigravity](https://deepmind.google/blog/accelerating-antimicrobial-discovery/)（官方部落格，頁面可見 `October 15, 2026`；`meta article:published_time` 與 JSON-LD `datePublished` 皆為 `2026-10-15T16:00:00+00:00`，`dateModified` 為 `2026-10-16T10:06:05.549502+00:00`）。底 URL：`https://deepmind.google/discover/blog/`
- `uniprot` — UniProt consortium，[A0A0U0D591 · Lactococcin 972 family bacteriocin](https://www.uniprot.org/uniprotkb/A0A0U0D591/entry)（UniProtKB 官方條目，`unreviewed (TrEMBL)`；條目版本 48，標註最後更新 2026-09-02）。底 URL：`https://www.uniprot.org/`
- `protnlm` — UniProt consortium，[Automatic annotation using ProtNLM](https://www.uniprot.org/help/ProtNLM)（UniProt 官方說明頁，含證據標籤格式、模型分數門檻與 Evidencer 佐證條件）。底 URL：`https://www.uniprot.org/help`
- `antigravity` — Google，[Why choose Google Antigravity for science](https://antigravity.google/use-cases/science)（官方產品頁；本文引述以英文版 `?hl=en` 為準）。底 URL：`https://antigravity.google/`
- `amr` — Public Health England，[Health matters: antimicrobial resistance](https://www.gov.uk/government/publications/health-matters-antimicrobial-resistance/health-matters-antimicrobial-resistance)（GOV.UK 官方指引，頁面可見 `Published 10 December 2015`）。底 URL：`https://www.gov.uk/`

[Home](../) · [Industry Watch](./)
