---
parent: Industry Watch
nav_exclude: true
title: "Anthropic 把免費 Claude 額度擴大到基金會與研究機構"
category: industry-watch
date: 2026-10-30
updated: 2026-11-12
tags: [Anthropic, AI-for-Science, research-credits, life-sciences, genomics, computational-pathology, rare-disease, Model-Hardware-Standard, dual-use, model-access, research-workflow]
catalog_id: "anthropic:ai-for-science-expands-foundations-research-institutions-2026-10-28"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.1"
source:
  orgs:
    - "Anthropic"
  event: "AI for Science 計畫擴大至科學基金會、研究機構與研究計畫（AI for Science expands to foundations and research institutions）"
  event_date: "2026-10-28"
  official_url: "https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions"
related_articles:
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "同一家公司相隔一天的兩則公告，分屬成果側與取用側，而兩則的可核對物都不在正文：該則的樣本數與利益揭露藏在同頁要點開的面板裡，本則的夥伴總數與正文三份名單對不起來，決定研究者能用到哪一級模型的那段限制則寫在兩個月前的另一頁"
  - path: "2026-10-08-medgemma-global-deployment-claims.md"
    relation: "兩則都是大廠公布自己支持了哪些單位：該則是五個醫療落地合作，本則是擴大到基金會與研究機構的免費額度計畫。兩則並讀可以看出把公告的名單逐條點清，是閱讀這類發布最基本也最有用的一個動作"
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "該則的三種加速說法分屬三個官方位置、沒有一個附得出絕對數值，本則的「數月變數小時」與「數週變數小時」是同一種寫法，差別在本則連被加速的工作是哪一項都沒有指明"
refs:
  main:
    title: "Anthropic：AI for Science expands to foundations and research institutions（官方公告，2026-10-28）"
    url: "https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions"
  scientists:
    title: "Anthropic：Expanding our support for scientists（官方公告，2026-08-27）"
    url: "https://www.anthropic.com/news/expanding-support-for-scientists"
  fable:
    title: "Anthropic：Improving Fable 5's biology safeguards（官方公告，2026-08-07）"
    url: "https://www.anthropic.com/news/improving-fable-5-s-biology-safeguards"
  mhs:
    title: "Anthropic：Previewing the Model Hardware Standard（官方公告，2026-08-27）"
    url: "https://www.anthropic.com/news/model-hardware-standard-research-preview"
  program:
    title: "Anthropic：Introducing Anthropic's AI for Science Program（官方公告，2025-05-05）"
    url: "https://www.anthropic.com/news/ai-for-science-program"
---

[Home](../) · [Industry Watch](./)

# Anthropic 把免費 Claude 額度擴大到基金會與研究機構

## 來源

- 組織：Anthropic
- 事件：AI for Science 計畫擴大至科學基金會、研究機構與特定研究計畫（原標題 `AI for Science expands to foundations and research institutions`）
- 日期：2026-10-28（頁面 `time` 標籤 `datetime="2026-10-28"` 顯示 `Oct 28, 2026`；同頁 JSON-LD 的 `datePublished` 為 `2026-10-28T00:00:00.000Z`、`dateModified` 為 `2026-10-29T04:43:29.000Z`，未推斷）
- 官方入口：<https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions>
- 另有四個同一計畫的官方頁作為脈絡：2025-05-05 的計畫發布頁、2026-08-07 的 Claude Fable 5 生物安全機制更新、2026-08-27 的科學家支援擴大公告、2026-08-27 的 Model Hardware Standard research preview
- 五個頁面同屬 Anthropic，**單源（單一組織），待交叉驗證**。本則沒有第三方查核、沒有同儕審查文獻，計畫成效也沒有任何外部可驗證的量測

**編輯：** Clarence

Anthropic 在 2026-10-28 宣布把 AI for Science 計畫從個別研究者擴大到科學基金會、研究機構與特定研究計畫，並逐條列出合作對象 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。這個計畫提供免費的 Claude credits 給研究者，自 2025-05-05 啟動。對醫療端的讀者而言，本則有三層直接相關的資訊：名單裡有相當比例是基因體學與疾病生物學的重鎮（Wellcome Sanger Institute、The Francis Crick Institute、Gladstone Institutes、Broad Institute 的 gnomAD、Johns Hopkins 的 AstroPath、澳洲的 Centre for Population Genomics）；取得資源的途徑從研究者逐案申請，擴成了經由基金會、學會與機構轉發；而生物與化學研究者實際能用到的模型層級，由另一份兩個月前的文件決定，仍停在 Opus-class。

## 背景

這則公告是一條延續約十八個月的計畫線的最新一步，而它前面幾步決定了這次擴編的實際意義，不是無關的參考文獻：

- **2025-05-05** — Anthropic 發布 AI for Science 計畫。當時的用詞是 `free API credits`，並寫明 `with a particular focus on biology and life sciences applications` [(ref: program)](https://www.anthropic.com/news/ai-for-science-program)。這是本則「擴大」的起點，也是後面範圍變化的基準。
- **2026-08-07** — Anthropic 更新 Claude Fable 5 的生物安全機制（biology safeguards），並在同一頁寫明：Fable 對它判定為 dual-use 的請求（頁面列舉 virology、toxicology、molecular design）仍會退回 Opus 5，因此 `it isn't yet usable for professional biology research and drug development` [(ref: fable)](https://www.anthropic.com/news/improving-fable-5-s-biology-safeguards)。這一段是本則名單上那些生醫機構實際會碰到的邊界。
- **2026-08-27** — Anthropic 宣布科學家支援擴大，開放 10,000 個席次，並在同一頁重述上述限制：`researchers working in biology and chemistry will still be limited to our Opus-class models` [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。同一頁也首次給出 AI for Science 的金額上限。
- **2026-08-27** — 同一天，Anthropic 公布 Model Hardware Standard（MHS）的 research preview，並寫明它源自與 HHMI Janelia Research Campus 的合作 [(ref: mhs)](https://www.anthropic.com/news/model-hardware-standard-research-preview)。本則公告把 Janelia 這段合作當成「過去一年開始擴大」的例子回述。
- **2026-10-28** — 本則公告。把對象從個別研究者擴大到基金會與機構，逐條列出合作單位 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。

## 這個計畫提供什麼（事實）

- **資源形式** — 本則公告的用詞是 `free Claude credits`。2025 年的發布頁用的是 `free API credits`，並寫明重點在生物與生命科學 [(ref: program)](https://www.anthropic.com/news/ai-for-science-program)。
- **每個計畫的額度上限** — `up to $50,000 in credits per project`，寫在 2026-08-27 的頁面，不在本則公告裡 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。
- **研究者個人的取用管道** — 同一頁宣布 team plan for scientists 開放 10,000 個席次：standard 席次免費，premium 席次每月 15 美元且用量上限為 5 倍，期間一年。Claude Science 於 2026 年六月推出 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。
- **申請入口就是公告內文的連結** — 本則公告內文只有三個對外連結，分別指向 AI for Science 計畫頁、科學家 team plan 頁與 MHS 頁；前兩者即是研究者自行申請的入口（頁尾另有一張指向 2026-08-27 公告的相關文章卡）[(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- **目前規模** — 公告寫 `supported hundreds of projects across biology, medicine, physics, chemistry, climate science, and mathematics`，只有量級，沒有數目 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- **領域範圍已從生命科學擴出去** — 2026-08-27 的頁面寫 `To date, we've largely supported scientists using Claude for biological sciences`，並宣布擴及其他領域 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)；本則名單橫跨天文（Space Telescope Science Institute）、地球系統（Columbia 的 LEAP）與數學（Tau Ceti），生醫不再是唯一重心 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。

## 這次擴編點名了哪些對象（事實）

公告正文有三個小節，各帶一份清單 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)：

| 小節（原文標題） | 清單內容 |
|---|---|
| `Science funders and societies` | Alfred P. Sloan Foundation（1934 年創立）、Simons Foundation（含 Flatiron Institute）、Schmidt Sciences（2024 年創立）、Open Source for Science Fund（Renaissance Philanthropy 旗下）、US National Science Foundation（公告稱其為 `$9 billion` 聯邦機構、1950 年設立、約占美國大專院校基礎研究聯邦經費 25%）、CAS（American Chemical Society 旗下，維護 CAS REGISTRY） |
| `Institutions` | Space Telescope Science Institute（由 AURA 管理，Hubble／JWST／Roman）、Wellcome Sanger Institute、The Francis Crick Institute（公告稱其有逾 100 個研究群組）、Imperial College London 生命科學系、EMBL（六個據點，EMBL-EBI 託管 Ensembl、Protein Data Bank in Europe、Europe PMC）、Gladstone Institutes |
| `Research projects and initiatives` | FlyWire（Princeton，連結體）、LEAP（Columbia，NSF 中心）、AstroPath（Johns Hopkins）、gnomAD（Broad Institute）、Tau Ceti（Lean 數學形式化）、Centre for Population Genomics（澳洲） |

三份清單之中只有第三份被標為新，引導句為 `The new projects are:`。正文另以敘述提到兩個組織：HHMI Janelia Research Campus（共同開發 Model Hardware Standard）與 Allen Institute；兩段都出現在 `Over the past year, we've started to expand this work` 之後，寫法是回述既有合作（`we partnered with`、`We also support`）[(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。

公告另一個小節標題為 `What's next`。

## 名單中與醫療直接相關的單位（事實）

[(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)

- **Wellcome Sanger Institute** — 基因體學。
- **The Francis Crick Institute** — 公告稱其有逾 100 個研究群組。
- **Imperial College London 生命科學系**。
- **EMBL** — 六個據點；EMBL-EBI 託管 Ensembl、Protein Data Bank in Europe 與 Europe PMC 等開放資源。
- **Gladstone Institutes**。
- **AstroPath**（Johns Hopkins）— 隸屬 Mark Foundation Center for Advanced Genomics and Imaging 與 Bloomberg~Kimmel Institute for Cancer Immunotherapy，公告描述是把天文巡天的校正方法用於腫瘤的逐細胞影像，使 `measurements consistent across slides and labs`。
- **gnomAD**（Broad Institute）— 公告稱匯集逾 800,000 人的 DNA 資料，供罕見疾病的發現與診斷。
- **Centre for Population Genomics**（澳洲）— Garvan Institute of Medical Research 與 Murdoch Children's Research Institute 的聯合計畫，做罕見疾病診斷工具。

## 研究者實際能用到哪一級模型（事實）

這一層不寫在本則公告裡，但它決定上述機構拿到額度之後能做什麼：

- **生物與化學仍限 Opus-class** — 2026-08-27 頁面原文為 `For now, researchers working in biology and chemistry will still be limited to our Opus-class models. Claude Fable models will continue to block professional biology and drug development queries because of their potential dual-use risks.` [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)
- **Fable 擋下的是哪一類請求** — 2026-08-07 頁面寫 Fable 對它判定為 dual-use 的請求（virology、toxicology、molecular design）仍會退回 Opus 5，因此 `it isn't yet usable for professional biology research and drug development`。同頁另寫 `Healthcare professionals will be able to receive more support from Fable 5 on clinical tasks.`，舉的日常例子是 interpreting lab results 與 understanding symptoms [(ref: fable)](https://www.anthropic.com/news/improving-fable-5-s-biology-safeguards)。
- **Mythos-class 另走一條路** — Anthropic 說明正與美國政府合作建立讓生命科學專業人員使用 Mythos-class 模型的取用計畫，`We have now enrolled our first participants`，參與條件與時程未公布 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。
- **Fable 5 這次更新的幅度** — 2026-08-07 頁面寫這次更新把生物相關的 fallback 減少 `by about 85% across our product surfaces`，前綴為 `In our testing`；頁面唯一的註腳給出各產品表面不分原因的總 fallback 降幅：Claude.ai 約 67%、Cowork 約 55%、Claude Code 約 17%、Claude Platform 約 7% [(ref: fable)](https://www.anthropic.com/news/improving-fable-5-s-biology-safeguards)。

## 這些合作要產出什麼（事實）

- **開放產出** — 公告說這些合作多半會產出開放資料集、開源軟體、開放標準與共用函式庫 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- **Model Hardware Standard** — 本則公告寫 `MHS is currently in research preview`；MHS 自己的頁面進一步寫明它只開放給第一批科學實驗室與先進製造業者，源自與 HHMI Janelia Research Campus 的合作，且仍在 `ahead of making the standard open source` 的階段，亦即尚未開源 [(ref: mhs)](https://www.anthropic.com/news/model-hardware-standard-research-preview)。
- **MHS 要解決的工作** — MHS 頁寫實驗室或製造場域的整合工作原本需要 `weeks, if not months`，MHS 把它降為 `hours or minutes` [(ref: mhs)](https://www.anthropic.com/news/model-hardware-standard-research-preview)。
- **Allen Institute** — 公告寫 `turning months of manual analysis into hours` [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。

## 證據邊界（事實）

本則是計畫擴編公告，可核對的範圍有明確的邊界，列在這裡供引用時參考：

- **開頭的 20 與名單逐條數出來的 18 對不起來。** 公告第一段寫 `We're highlighting 20 scientific foundations, institutions, and research groups from around the world that we've partnered with in an expansion of our AI for Science program`；這個句子逐字出現在正文、頁面的 meta description、`og:description` 與 JSON-LD 的 `description`，`20` 在正文中只出現這一次。而三份名單的 `li` 元素逐條計數為 6+6+6=18，是對頁面原始碼逐一計數的結果，不是概估。公告沒有說明另外兩個是誰 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- **18 個夥伴名稱在公告中都不是連結。** 公告內文的三個對外連結指向 AI for Science 計畫頁、科學家 team plan 頁與 MHS 頁，讀者無法從這則公告點進任何一個夥伴的官方頁去確認合作內容 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- **決定模型層級的那段限制不在這則公告裡。** `researchers working in biology and chemistry will still be limited to our Opus-class models` 與 Claude Fable 對 dual-use 請求的 fallback，寫在兩個月前的 2026-08-27 與 2026-08-07 兩頁；本則 2026-10-28 公告沒有重述，本書庫在查核時也未在本則公告、AI for Science 計畫頁或 MHS 頁找到修訂這項限制的敘述 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。
- **計畫擴編本身沒有任何成效數值。** 全文唯一的成效描述是 Allen Institute 的 `turning months of manual analysis into hours`：沒有說是哪一項分析、原本幾個月、現在幾小時，也沒有說這是已完成的結果還是預期。同一種寫法出現在 MHS 頁的 `weeks, if not months` 降為 `hours or minutes`，同樣沒有任何量測值。計畫規模則只有 `hundreds of projects` 這種量級描述 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- **金額不在這則公告裡。** 本則只寫 `free Claude credits`，全文唯一的金額 `$9 billion` 用來形容 US National Science Foundation 這個機構本身的規模，不是這次投入的資源；每計畫最高 50,000 美元 credits 與 10,000 個席次都寫在 2026-08-27 的頁面 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。
- **Fable 的生物安全機制數值全是相對值，而且兩組量的不是同一件事。** 85% 是生物相關 fallback 的降幅，註腳的 67%／55%／17%／7% 是各產品表面不分原因的總 fallback 降幅，不能相互換算，頁面也沒有給出任何一項的絕對次數 [(ref: fable)](https://www.anthropic.com/news/improving-fable-5-s-biology-safeguards)。
- **MHS 尚未開源。** 公告寫它在 research preview，MHS 頁寫明仍在 `ahead of making the standard open source` 的階段 [(ref: mhs)](https://www.anthropic.com/news/model-hardware-standard-research-preview)。
- **五個頁面同屬一家公司。** 本則與其脈絡頁的所有數字 —— 85%、67%、55%、17%、7%、數月變數小時、數週變數小時 —— 都是 Anthropic 自報，皆標為自家測試，沒有第三方查核，也沒有同儕審查文獻。

## 本書庫解讀（評論）

以下為本書庫的判讀，不是來源的結論。

- **20 與 18 的差額本身不是重點，「無法確認」才是。** 這個差額有幾種無害的解釋：可能把回述的 HHMI Janelia 與 Allen Institute 算進去，可能把 Centre for Population Genomics 的兩個母機構分開計，也可能把 AstroPath 所屬的兩個中心分開計。問題在於公告沒有提供任何一種解釋，而 18 個夥伴名稱全都不是連結，外部讀者沒有任何途徑可以把這份名單對齊成 20。對一則以逐條點名為主要內容的公告而言，清單與它自己的總數對不起來，是讀者唯一能做的核對動作當場失效。

- **把限制與擴編寫在不同頁面，效果等同於不寫。** Opus-class 限制與 Claude Fable 對 dual-use 請求的 fallback，是這份名單上生醫機構最可能先撞到的邊界：Sanger 的基因體學、Crick 的疾病生物學、Gladstone 的感染症與癌症研究、gnomAD 的變異判讀，都落在 2026-08-07 頁面列舉的 virology、toxicology、molecular design 附近或其延伸。一則在 10 月宣布擴大取用的公告，不重述 8 月寫下的取用邊界，讀者除非主動回查兩個月前的另一頁，否則會把「擴大取用」讀成「擴大到最新模型」。這不是事實錯誤，是編排造成的理解落差。

- **「數月變數小時」這類句子在採購與研究規劃上的價值是零。** 本則的 Allen Institute 與 MHS 頁的整合工作都採這種寫法。缺的不是精確度而是分母：沒有說明是哪一項工作、原本的基準量是多少、量測條件為何，外部就無法判斷這個比值適不適用於自己的流程，也無法判斷它是已完成的觀察還是設計目標。本書庫先前在 Gartner 的成本預測一則記錄過同樣形狀的問題 —— 只給倍數不給絕對量，結論既無法被否證，也無法進入任何試算。

- **醫療橋接之一：AstroPath 點到的正是醫療影像 AI 最難的那一項。** 跨玻片與跨實驗室的量測一致性，就是計算病理模型換一家醫院就失效的主因（染色批次、掃描機型、切片流程造成的系統性偏移）。一筆運算額度不會解決這個問題，但這個計畫至少把資源投在正確的問題上，值得後續追蹤它是否產出可供外部使用的校正方法或資料集 —— 公告說這些合作多半會產出開放資料集、開源軟體與開放標準，這一項能否兌現，比夥伴數目重要得多。

- **醫療橋接之二：模型層級限制是研究規劃的實際變數，不是法遵細節。** 對任何要把前沿模型納入影像判讀、基因變異註解或臨床文件流程的團隊，「我們拿到的是哪一級模型、什麼樣的查詢會被降級、降級之後輸出會不會改變」是會直接影響可重現性的問題：同一個 prompt 在不同時間落到不同模型，產出的差異無法歸因於方法。公告提到的 Mythos-class 取用計畫仍在第一批參與者階段，時程未公布。研究設計若預期用到前沿模型處理生物相關內容，目前應把降級視為常態而非例外，並在方法學上記錄實際服務的模型。

- **把額度交給既有的科研經費網路轉發，是這次擴編真正改變的事。** 對象從個別研究者換成基金會、學會與機構之後，資源的分配規則也跟著換手：決定誰拿到額度的不再只有供應商的審查，而是這些單位原本的分配機制。這對研究機構是一條新的供應線，但其規則目前不公開。

## 產業影響

- **運算額度正在成為科研基礎設施的一條新供應線。** 本則的特徵是對象從個別研究者換成了基金會與機構：Sloan、Simons、Schmidt Sciences、Renaissance Philanthropy 的 Open Source for Science Fund、美國國家科學基金會（US National Science Foundation）與美國化學學會（American Chemical Society）旗下的 CAS，都是本來就在分配研究資源的單位。把額度交給它們轉發，意味著模型供應商的資源開始沿著既有的科研經費網路流動，而不是逐案審查。對研究機構而言，這是一條新的、與傳統經費來源並行的供應線，其分配規則目前不公開。

- **模型層級與研究領域的交叉管制已經是結構性的。** 生物與化學研究者被限制在 Opus-class、Fable 對 dual-use 請求退回 Opus 5、Mythos-class 需另走政府合作的取用計畫 —— 這三層加起來的效果是：風險最高的領域也是取用最新能力最慢的領域，而醫療 AI 的許多題目正好落在這一區。這並非單一廠商的選擇，而是生物安全考量下可預期的通則；值得注意的是它對研究進度的影響尚無任何公開量化。

- **開放產出是這類計畫能否被外部檢驗的唯一著力點。** 公告說這些合作多半會產出開放資料集、開源軟體、開放標準與共用函式庫。這是整則公告中唯一可被第三方日後查證的承諾 —— 夥伴數目與加速倍數都不是。MHS 目前處於 research preview 且尚未開源，正好是這項承諾的第一個測試點。

- **對台灣的學術研究單位而言，這條路徑目前是間接的。** 本次點名的轉發者集中在美國、英國與歐洲的基金會與機構，公告沒有提到亞太地區的對應窗口；名單上唯一的亞太機構是澳洲的 Centre for Population Genomics，而它是以研究計畫而非轉發者的身分列入。

## 與書庫其他文章的關係

同一家公司相隔一天的兩則公告，分屬成果側與取用側，而兩則的可核對物都不在正文：該則的樣本數與六段利益揭露藏在同頁要點開的面板裡，本則的夥伴總數與正文三份名單對不起來，決定研究者實際能用到哪一級模型的那段限制則寫在兩個月前的另一頁；兩則並讀可以看出同一家公司在同一週內，把關鍵限定條件放在正文以外的兩種不同作法: [Anthropic 公布六個藥物開發組織接入 Claude 的早期成果](2026-10-28-anthropic-drug-development-case-studies.md)

兩則都是大廠公布自己支持了哪些單位：該則是五個醫療落地合作，本則是擴大到基金會與研究機構的免費額度計畫。兩則並讀可以看出把公告的名單逐條點清，是閱讀這類發布最基本也最有用的一個動作: [MedGemma：開放權重醫療模型，四國五個落地合作案](2026-10-08-medgemma-global-deployment-claims.md)

該則的三種加速說法分屬三個官方位置、沒有一個附得出絕對數值；本則的「數月變數小時」與「數週變數小時」是同一種寫法，差別在本則連被加速的工作是哪一項都沒有指明。兩則並讀可以看出相對倍數在缺少分母時，不論出現在效益側或成本側都同樣無法使用: [DeepMind 抗菌胜肽示範：代理程式從資料庫走到實驗計畫](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

同一家公司、同一個取用落差的兩次出現：本則發現決定生物與化學研究者能用到哪一級模型的限制寫在兩個月前的另一頁，該則的落差完全相同 —— 生醫評測的數字掛在 Mythos 5.2 名下，而它的取用條件寫在 2026-09-17 的 Life Sciences Verification Program 頁，公告本身只寫了一句可以申請: [Fable 與 Mythos 5.2 降價發布，十四列評測、生科須審核](2026-11-10-anthropic-claude-fable-mythos-5-2-launch.md)

## 實務的啟發

- **讀到「我們支持了 N 個單位」時，先把名單數一遍。** 這是成本最低的核對動作，本則就是靠它發現 20 與 18 的差距。清單與總數不一致不必然代表誇大，但它會告訴你這份文件在發布前沒有被逐條核對過，後面的敘述也該用同樣的態度讀。

- **評估任何模型取用方案時，把「哪一級模型」與「什麼情況下會被降級」列為必問項。** 本則顯示這兩件事可能根本不寫在取用公告裡，而寫在兩個月前的安全機制頁。對研究與臨床流程而言，中途被降級到另一個模型會讓同一份方法學產生無法歸因的輸出差異，這一項應在方案評估階段就問清楚，並在研究記錄中寫下實際服務的模型。

- **把「免費額度」與「可用能力」分開登記。** 本則給的是額度，而生物與化學領域的能力上限由另一份文件決定。採購或申請時若只記錄額度金額，會高估這筆資源的實際價值；兩欄分開登記比較不會在後續規劃時混淆。

- **申請前先確認入口與條件寫在哪一頁。** 本則的額度上限（每計畫最高 50,000 美元 credits）、席次數與席次價格都不在公告本文，而在 2026-08-27 的頁面；申請入口則是公告內文的兩個連結。把這幾項抄進同一張表再送件，可以省掉一輪往返。

- **廠商自報的加速倍數，缺分母就不要寫進規劃文件。** 本則與其脈絡頁出現的每一個加速說法都沒有絕對量測。可行的作法是把它們記錄為「廠商宣稱、無絕對值」，並在自家環境做一次小規模的前後量測再決定是否納入估算。

- **對開放產出的承諾設一個回查時間點。** 公告說這些合作多半會產出開放資料集、開源軟體與開放標準，這是整則公告中唯一能被外部查證的項目。MHS 尚未開源，是最具體的一個觀察對象。

## 後續追蹤

- Anthropic 是否補充說明 20 與 18 的差額對應哪兩個組織，或修正該句敘述。目前三份名單合計 18 項，而公告正文、meta description 與 JSON-LD 三處都寫 20 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- `researchers working in biology and chemistry will still be limited to our Opus-class models` 這項限制是否被正式修訂，以及與美國政府合作的 Mythos-class 取用計畫是否公布參與條件與時程。目前只知道已納入第一批參與者 [(ref: scientists)](https://www.anthropic.com/news/expanding-support-for-scientists)。
- Model Hardware Standard 是否如公告所述開源，以及 research preview 階段是否產出安全評估或最佳實務文件 [(ref: mhs)](https://www.anthropic.com/news/model-hardware-standard-research-preview)。
- 這些合作是否實際產出公告承諾的開放資料集、開源軟體、開放標準與共用函式庫，特別是 AstroPath 的跨玻片／跨實驗室校正方法是否以可供外部使用的形式釋出 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。
- 基金會與學會轉發這批額度的分配規則是否公開，以及是否出現同儕審查文獻在方法學段落揭露使用了這批資源。
- Anthropic 是否公布 AI for Science 計畫的任何絕對量測 —— 支援的計畫數目前只有「hundreds of projects」這種量級描述，各項加速宣稱則都沒有基準值 [(ref: main)](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)。

## References

- `main` — Anthropic，[AI for Science expands to foundations and research institutions](https://www.anthropic.com/news/ai-for-science-expands-foundations-research-institutions)（官方公告，頁面 `time` 標籤 `datetime="2026-10-28"`、JSON-LD `datePublished` `2026-10-28T00:00:00.000Z`、`dateModified` `2026-10-29T04:43:29.000Z`；三份名單小節為 `Science funders and societies`、`Institutions`、`Research projects and initiatives`）。底 URL：`https://www.anthropic.com/news`
- `scientists` — Anthropic，[Expanding our support for scientists](https://www.anthropic.com/news/expanding-support-for-scientists)（官方公告，頁面 `time` 標籤 `datetime="2026-08-27"`；含 10,000 席次、premium 每月 15 美元與 5 倍用量上限、每計畫最高 50,000 美元 credits，以及 Opus-class 限制與 Mythos-class 取用計畫）。底 URL：`https://www.anthropic.com/news`
- `fable` — Anthropic，[Improving Fable 5's biology safeguards](https://www.anthropic.com/news/improving-fable-5-s-biology-safeguards)（官方公告，頁面 `time` 標籤 `datetime="2026-08-07"`；生物相關 fallback 降幅約 85%，註腳 1 列出各表面總 fallback 降幅 67%／55%／17%／7%）。底 URL：`https://www.anthropic.com/news`
- `mhs` — Anthropic，[Previewing the Model Hardware Standard](https://www.anthropic.com/news/model-hardware-standard-research-preview)（官方公告，頁面 `time` 標籤 `datetime="2026-08-27"`；research preview，與 HHMI Janelia Research Campus 共同開發，尚未開源）。底 URL：`https://www.anthropic.com/news`
- `program` — Anthropic，[Introducing Anthropic's AI for Science Program](https://www.anthropic.com/news/ai-for-science-program)（官方公告，頁面 `time` 標籤 `datetime="2025-05-05"`；原用詞為 `free API credits`，重點在生物與生命科學）。底 URL：`https://www.anthropic.com/news`

[Home](../) · [Industry Watch](./)
