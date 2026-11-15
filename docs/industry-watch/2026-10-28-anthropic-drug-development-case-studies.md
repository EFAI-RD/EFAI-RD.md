---
parent: Industry Watch
nav_exclude: true
title: "Anthropic 公布六個藥物開發組織接入 Claude 的早期成果"
category: industry-watch
date: 2026-10-28
updated: 2026-11-12
tags: [Anthropic, Claude, drug-development, antibody-engineering, BigHat-Biosciences, Divergence-Labs, Enveda, Generate-Biomedicines, Mithril-Medicine, lead-optimization, regulatory-documents, preclinical, evaluation-metrics]
catalog_id: "anthropic:early-progress-drug-development-2026-10-27"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.1"
source:
  orgs:
    - "Anthropic"
    - "BigHat Biosciences"
    - "Divergence Labs"
    - "Enveda"
    - "Generate Biomedicines"
    - "The Column Group"
    - "Bristol Myers Squibb"
  event: "發布公告 Early progress on accelerating drug development with Claude，彙整六個藥物開發合作案與一項自有研究計畫的早期結果"
  event_date: "2026-10-27"
  official_url: "https://www.anthropic.com/research/early-progress-drug-development"
related_articles:
  - path: "2026-10-22-openai-distributed-agents-perturb-seq-atlas.md"
    relation: "兩則是前沿模型供應商在六天內先後發布的生命科學成果公告，落差型態卻不同：該則是公告與它所連結的預印本在同一個數字上互相矛盾，本則的數字則全部正確，問題出在被挑出來的那一個不是被提名的那一個，以及量尺本身在專案中途被換過；兩則並讀可以看出「回去對數字」這個動作除了核對數值，還得核對那個數值描述的是哪一個對象、用哪一把尺量的"
  - path: "2026-10-20-google-amie-lancet-primary-care-feasibility.md"
    relation: "該則的 90% 是前七名清單的命中率、排第一名的只有 56%，兩個數字都在 Google 自家的技術部落格裡；本則的「結塊慢 100 倍以上」與「6 到 9 倍」同樣分屬兩層官方文件，而本則多了一層 —— 詳細版不是另一個頁面，而是同一頁上要點開才看得到的面板，六段利益揭露也只存在於那些面板裡"
  - path: "2026-10-19-ge-healthcare-end-tidal-control-michigan-study.md"
    relation: "該則是本書庫目前最接近完整部署評估的樣本，它事先寫明三個假設、並在其中一個未達自訂門檻時照實報出；本則恰好是相反的作法，技術報告自述最終規格是在看過結果之後才設定的，而按原規格最後一輪 113 個 scFv 設計沒有一個以實測解離常數通過，兩則並讀可以看出「終點什麼時候定」這件事如何決定一份成果該被當成驗證還是當成探索"
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "兩則是前沿模型供應商相隔十二天發布的生命科學成果公告，而該則比本則更早一步 —— 本則至少有六份技術報告可以把公告裡的每一個數字逐項回查，該則除了一個資料庫編號之外沒有任何可回查的量測，所有成果都停在 wet-lab validation 之前；兩則並讀可以看出同一類公告在「可查核物存不存在」這一軸上的兩個位置"
  - path: "2026-10-30-anthropic-ai-for-science-foundations-expansion.md"
    relation: "同一家公司相隔一天的兩則公告，分屬成果側與取用側，而兩則的可核對物都不在正文：本則的樣本數與利益揭露藏在同頁面板裡，該則的夥伴總數與正文三份名單對不起來，模型層級限制則寫在兩個月前的另一頁"
  - path: "2026-11-02-microsoft-mai-dxo-sdbench-sequential-diagnosis.md"
    relation: "兩則的核心都是「訂標準的人與被評分的系統出自同一方」：本則的成功規格依技術報告自述是在看過結果之後才定下的；該則則是 benchmark、Gatekeeper、Judge 與受測系統 MAI-DxO 由同一個團隊設計，論文的利益揭露列出全體作者皆為 Microsoft 員工並持有股權。差別在於該則把整套評分程式碼開源了，讓外部至少能檢視那把尺怎麼刻"
  - path: "2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md"
    relation: "兩則是前沿模型供應商相隔七天發布的藥物開發成果，可回查的深度不同：本則同日釋出六份技術報告，公告裡的數字能逐項對照回原始報告；該則以工作流程示範為主，代理程式側未公布模型指標。兩則並讀可以看出「廠商自報」在證據密度上的落差"
refs:
  pr:
    title: "Anthropic：Early progress on accelerating drug development with Claude（官方公告；六段案例詳述為同頁可展開面板）"
    url: "https://www.anthropic.com/research/early-progress-drug-development"
  bighat:
    title: "Stanton S, Solomon A, Delaney E, Montgomery M, Acker T, Henrici R, Eid C, Abrams E, Greenside P：Reasoning in the loop: antibody lead optimization by probing mechanism and measurement（BigHat Biosciences 技術報告，31 頁；第一作者單位為 Anthropic）"
    url: "https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026"
---

[Home](../) · [Industry Watch](./)

# Anthropic 公布六個藥物開發組織接入 Claude 的早期成果

## 來源

- 組織：Anthropic；合作方 BigHat Biosciences、Divergence Labs、Enveda、Generate Biomedicines、The Column Group、Bristol Myers Squibb
- 事件：發布公告 `Early progress on accelerating drug development with Claude`，彙整六個藥物開發合作案與一項自有研究計畫的早期結果
- 日期：2026-10-27
- 官方入口：<https://www.anthropic.com/research/early-progress-drug-development>
- 本則為**單源（單一組織主導），待交叉驗證**。公告連出六份技術報告，其中 BigHat 那一份可完整取用並逐項回查，但它不是獨立佐證 —— 該報告第一作者的掛名單位是 Anthropic，而同頁面板的揭露寫明 `Anthropic paid BigHat for carrying out the laboratory work described here` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)

**編輯：** Clarence

Anthropic 在 2026-10-27 公布其生命科學團隊過去數月的合作成果：六個藥物開發組織（BigHat Biosciences、Bristol Myers Squibb、Divergence Labs、Enveda、Generate Biomedicines、The Column Group）各自把 Claude 接進研發流程的不同環節 —— 從抗體的設計與量測循環、大量設計的生成與篩選，到法規文件覆核、文獻判讀與臨床試驗規劃 —— 另有一項由 Anthropic 收購而來的自有計畫已做到小鼠。公告同時表明這些工作 `so far it is mostly preclinical`，亦即多數尚未進入人體試驗階段 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

對藥物開發與生技研究的工作流程而言，本則的可用資訊在於它把「模型接在哪一段、補上或取代了哪一個動作」寫成六個可分辨的位置，而不是一句整體加速：有兩案把模型放在濕式實驗的設計—量測循環裡（其中一案甚至動到量測指標本身），一案放在設計的大量生成與結構篩選，一案放在品質與法規文件的覆核與撰寫，一案放在標的—疾病配對的文獻判讀，一案放在臨床試驗規劃。這六個位置對應的是藥物開發鏈上難度與可驗收程度都不同的工作。

這一則的可回查程度在同類公告中相對高，值得先說明：六份技術報告隨公告釋出，同頁六個可展開面板另載有樣本數、限制聲明與利益揭露，其中 BigHat 那一份 31 頁的技術報告可完整取用、公告的每一個數字都能逐項對照回去。本文即以該報告與各案面板逐項核對公告正文，核對結果本身沒有一個數值是錯的；公告寫法與詳細層之間的落差，連同本則的單源與利益結構，一併收在後段的〈證據邊界（事實）〉。

## 背景

- **2026 年 7 月** — Anthropic 收購一人公司 Mithril Medicine，將其兩個計畫納為自有研發計畫；本則的小鼠結果出自這條線 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **2026-10-27** — 公告 `Early progress on accelerating drug development with Claude` 上線。頁面 `<time datetime="2026-10-27">` 顯示 `Oct 27, 2026`，JSON-LD `datePublished` 與 `meta article:published_time` 同為 2026-10-27，三處一致 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **同日** — 六份技術報告隨公告釋出，分別託管於各合作方自己的網站或 Anthropic 的內容伺服器，皆非同儕審查出版品。

這份公告分三層，三層的詳細程度差距很大。第一層是正文，約 1,850 字（移除六個對話框面板後計為 11,753 字元、1,847 英文字），寫的是每一案做了什麼與最醒目的那個結果。第二層是每段結尾 `Read more` 開啟的同頁面板：各案的完整敘述、樣本數、限制聲明與利益揭露都在這裡，而這顆 `Read more` 不是連結而是在原頁開啟對話框的按鈕，面板沒有自己的網址。第三層是六份技術報告，本文逐項核對的是其中的 BigHat 報告 `Reasoning in the loop: antibody lead optimization by probing mechanism and measurement`（31 頁），作者列為 Samuel Stanton（單位 1：Anthropic）與八位 BigHat 人員（單位 2）[(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。

本則無配圖。公告頁的主視覺與各面板內的結果圖為 Anthropic 與各合作方自有素材，不重製；BigHat 技術報告的圖版權狀態未明示。

## 抗體先導優化：模型動到的是量測端（事實）

BigHat 這一案把 Claude 接在抗體先導優化（lead optimization）的設計—製造—量測循環裡，兩條平行試驗線分別是 VHH（單域抗體，公告稱為 `the lead for longer-lasting drugs`，技術報告摘要寫明其結合對象為 albumin）與 scFv（單鏈可變片段，公告稱為 `the cancer-targeting lead`）[(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development) [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。

- **被提名的兩個先導分子的實測值** — 技術報告給出確值：VHH 先導分子解離常數 1.15 nM 對親本 10.3 nM，scFv 0.63 nM 對 3.7 nM；報告摘要自述 `The VHH lead binds albumin about nine times more tightly`。同頁面板對這兩個分子的總結是 `they bound six to nine times more tightly, held together at temperatures 8 to 18°C higher`。溫度端的兩個確值為 scFv 的 collapse temperature 74.2 °C 對 56.3 °C、VHH 的 melting temperature 70.6 °C 對 62.2 °C [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。
- **專案中途換掉量測指標** — 這是本案在流程上最實質的一步。公告寫 `Partway through, the team suspected the standard heat-stability and clumping metrics were misleading. Claude and the researcher reanalyzed the raw data, then proposed different metrics and a protocol change to test them` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。技術報告說明得更完整：原本儀器輸出的 apparent melting temperature（表觀熔點）與 aggregation onset（聚集起始溫度）被判定無法分辨好壞分子，於是在 VHH 上改用聚集速率、在 scFv 上改用 collapse temperature（溶液崩解溫度）[(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。
- **換指標的論證方式** — 技術報告不是直接換了指標了事：它回到原始升溫曲線、建立物理模型、對濃度與升溫速率做出事前預測再跑實驗驗證，並記下其中一項預測被推翻（`refuted`）[(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。對研發流程而言，這一段示範的是模型介入的位置可以不只是「生成候選分子」，而是進到「這把尺量得準不準」這一層 —— 而這一層平常是由儀器預設輸出決定的。
- **聚集速率的原始讀數** — 新指標下的對應數值是 `p k_agg is +2.00 on one identified well against −0.39`，兩者相差 2.39 個對數單位（換算約 245 倍，由本文代為計算）。同頁面板的對應敘述是 `the final VHH clumped far more slowly` [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026) [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

## 設計的生成與篩選：Generate 與 Divergence（事實）

這兩案都把模型放在「大量產生設計、再靠運算篩到可做實驗的數量」這一段，差別在產出物與篩選漏斗的形狀。

- **Generate Biomedicines：把標準構件縮短約七成** — 公告寫 `One design was about 70% shorter than the standard version, and in lab tests it was more effective: it allowed immune cells to make roughly 10 times as many receptors` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。同頁面板補上正文沒有的三項：首輪送驗的設計數為 186 個、整個專案歷時八個月、`These are early laboratory results—Generate has not yet tested that the designs are safe or effective in patients`。面板摘要段對同一件事的寫法是 `The best design was about 70% shorter and no less effective`，並把 10 倍歸給 `one of the top designs` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **Divergence Labs：雙臂抗體的漏斗** — 這一案要同時做出兩條功能相反的抗體臂（anchor arm 與 disruptor arm，標的為 IgE）。公告寫 `generated roughly 35,000 antibody designs in about a month to be narrowed down and tested. In those early tests, Divergence found "hits" for both arms: three designs that could bind to IgE, and 20 that could dislodge it` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。面板給出漏斗的中間段：35,000 個設計經結構預測模型評分後 `kept only the highest scoring ones—no more than 96 per arm—to make and test in the lab`，實際進入濕式實驗的是 disruptor arm 91 個與 anchor arm 57 個，結果為 `20 of the 91 designs worked as intended` 與 anchor arm `three of them (around 5%)`。時間為 disruptor arm 約三週、anchor arm 約四週半；運算成本為 `around 2,750 hours of computing time spread across many Nvidia H100 GPUs` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

就工作流程而言，這兩案的共同形狀是模型產出的數量遠大於實驗端的吞吐量，真正決定成敗的是中間那層結構預測篩選把漏斗收到每臂不到一百個 —— 而這一層的門檻與評分方式，兩案都未在公告中展開。

## 法規與品質文件：Enveda 的覆核與撰寫（事實）

這一案不涉及任何生物學宣稱，模型接的是文件流程，因此是六案中可被完整量化的一案 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **文件覆核** — 公告寫 `Over tests on 1,061 pages of documentation, Claude caught all 11 issues that human reviewers had spotted—and flagged seven they'd missed. In the process, this method reduced human review time by 89%, from over 25 hours to less than three` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。面板給出時間的確值：人工 1,553 分鐘（25.9 小時）對系統加覆核 166 分鐘（2.8 小時）。
- **誤報與誤讀的數字** — 面板另報出正文沒有的兩組數字與一項誤讀：系統計時那一輪共提出 42 條意見、其中 33 條（79%）不需處理；人工提出 96 條、其中 79 條（82%）不需處理；`the CDP did misread one entry, a struck-through handwritten correction`，並未偵測到任何無中生有的發現 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **誰評分** — 評分者為 Enveda 自家品質部門一位未參與該次審查的成員，另一位成員覆核 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **文件撰寫** — 同一案的另一項產出是法規文件草稿，公告寫 `One took four hours, compared to about three months by hand`；面板在同一組數字後補 `Neither figure includes the three-week manual review process that every draft goes through` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

## 文獻判讀與試驗規劃：The Column Group 與 Bristol Myers Squibb（事實）

- **The Column Group：標的—疾病配對的文獻工作** — 公告寫該公司的第一個 Claude skill `has been evaluated on 45 target-disease pairs`（面板寫法為 `45 disease-target pairs`），面板給出的結果是速度：`has cut the process of finding and interpreting the relevant scientific literature from weeks to days` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。這一案另有一項公司層級的安排：Anthropic 與 The Column Group 共同設立新公司 Pleiades [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **Bristol Myers Squibb：臨床試驗規劃** — 這是六案中唯一觸及臨床階段的一案，接的是試驗規劃的評估工作。公告對這一案只有流程描述與一段主管引述，沒有任何數字 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

## Anthropic 自有計畫：Mithril 做到小鼠（事實）

- **時程與結果** — 公告寫 `Mithril took a possible treatment for one form of muscular dystrophy from an idea to promising results in mice in less than 18 months`，正文對效果的描述為握力約為未治療組的兩倍，並寫 `we expect a drug to be ready to start clinical trials in humans as soon as late 2028` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **樣本數** — 面板逐組給出：六週齡時的握力與三頭肌肌力比較為治療組 7 隻、未治療疾病組 4 隻、健康對照 12 隻；存活為治療組八隻死一隻、未治療組八隻死四隻、健康組 12 隻全活 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **受測物與階段標示** — 面板寫明受測的是 `tool molecules—early, unrefined versions`（非正式候選藥物）、`These are early results in mice, not human trials`，時程圖另有圖註 `Dates after 2026 are targets, not commitments` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

## 公告自己標明的階段（事實）

- 公告在結尾明確寫出 `All of this research is still at an early stage` 與 `so far it is mostly preclinical` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- 正文逐詞計數：`clinical` 11 次、`trial` 9 次、`preclinical` 1 次、`preprint` 1 次、`validat` 1 次、`patient` 1 次，而 `FDA` 0 次、`peer`（同儕）0 次、`approv`（核准）0 次。公告沒有宣稱任何一項成果已獲法規核准或經過同儕審查 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- 六案的階段分布：有濕式實驗數據的三案（BigHat、Generate、Divergence）停在體外或細胞層級，Mithril 停在小鼠，Enveda 為文書作業，Bristol Myers Squibb 為流程描述 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

## 證據邊界（事實）

本則為單源，且公告正文與詳細層之間存在多處落差。以下逐項列出，供引用時參考；數值本身沒有一個錯，問題在於正文選了哪一個數字、以及限定條件落在哪一層。

- **正文沒有樣本數、註腳與利益揭露。** 正文中 `<sup>` 元素 0 個、`n =` 出現 0 次、`Disclosure` 一詞出現 0 次 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **六段利益揭露只存在於面板，分三種強度。** Generate、Divergence、Enveda、The Column Group 為 `Anthropic provides ... with Claude usage credits and engineering support`（Divergence 另加 `reimburses certain third-party computing costs`），BigHat 則是 `Anthropic paid BigHat for carrying out the laboratory work described here`。面板沒有獨立網址，讀者若只讀正文或只讀轉述不會知道它們存在 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **正文的量化說法只有五個。** 約 1,850 字的正文中 `%` 出現 3 次、形如 `10x`／`100x` 的倍數 2 次 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **「bound more than 10x more tightly」修飾的不是被提名的兩個分子。** 公告原句為 `Compared with the originals, the best versions bound more than 10x more tightly, the cancer-targeting lead stayed in solution 18°C higher, and the lead for longer-lasting drugs clumped more than 100x more slowly`。同頁面板對同兩個分子寫的是 `they bound six to nine times more tightly`，而 `more than tenfold` 在面板裡修飾的是另一組對象：`The tightest binders in both pilots improved more than tenfold`。技術報告中達到 10 倍以上的是未被提名的設計（VHH 最緊者 0.85 nM，`12 times tighter than the parent`；scFv 一個基礎設計 `about 15 times tighter`）。亦即「10 倍以上」與「被選為先導的兩個分子」是兩個不同的集合 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development) [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。
- **「18°C」是區間上緣。** 面板寫的是 `8 to 18°C higher`，兩個確值分別為 scFv 的 17.9 °C 與 VHH 的 8.4 °C 差距 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development) [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。
- **「clumped more than 100x more slowly」出自單一個孔。** 這是公告全文唯一的三位數倍數。`100-fold`、`100x` 與 `order of magnitude` 在 31 頁技術報告中全文命中 0 次，同頁面板也只寫 `the final VHH clumped far more slowly`。可對應的原始數值是 `p k_agg is +2.00 on one identified well against −0.39`，而技術報告在同一段緊接著自列兩項保留：`the aggregation value is one well, and the K_D margin, 0.14 log, is small`。「單一個孔」這項限制在公告正文與面板中都不存在 [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026) [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **判定成功的規格依報告自述是在看過結果之後才設定的。** 技術報告寫明兩件公告沒有提的事：`we set the final specifications knowing the results`，以及按原規格 `none of the 113 final-round scFv designs passes with a measured K_D`（另有兩個若採計解離速率下限可通過，`each on one well`）。同頁面板對 VHH 的對應敘述是 `No design in four rounds received a passing value that also cleared quality checks, including the final molecule` [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026) [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **Generate 一案的宣稱強度在同一頁上不一致。** 正文寫 `more effective`（更好），面板摘要寫 `no less effective`（不遜於）；10 倍受體在面板摘要歸給 `one of the top designs`，面板後段的詳述則把兩者寫在同一個候選身上。186 個首輪設計、八個月、`has not yet tested that the designs are safe or effective in patients` 三項皆不在正文 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **Divergence 一案的分母在正文裡缺席。** 正文把 35,000 與 3＋20 寫在相鄰兩句，容易被讀成 23 比 35,000；實際進入濕式實驗的是每臂不超過 96 個、disruptor arm 91 個與 anchor arm 57 個。時間方面，面板寫的是約三週與約四週半，而非正文單一的「約一個月」；2,750 GPU 小時的運算成本未入正文 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **Enveda 的 11 與 89% 出自不同的聚合方式。** 面板把兩個數字拆開歸屬：11 個問題是 `Across its runs on these records`、`in at least one of its runs` 的聯集，而七個額外問題與 89% 來自 `one timed run`。42 條／33 條（79%）、96 條／79 條（82%）、誤讀一筆劃線塗改的手寫更正，以及評分者為自家品質部門成員，皆不在正文 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **四小時對三個月兩邊都不含人工覆核。** 面板的限定為 `Neither figure includes the three-week manual review process that every draft goes through`；此外被比較的人工版本是該合作開始之前就已完成的草稿，而非同期對照 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **The Column Group 的 45 組量的不是正確率。** 面板沒有報出這 45 組評估中判斷正確的比例，也沒有說明對照標準是什麼；給出的結果是速度（`from weeks to days`）[(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **Bristol Myers Squibb 一案沒有任何數字。** 公告對這一案只有流程描述與一段主管引述 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- **六案的資源與撰稿關係使其不構成獨立佐證。** 六案全部由 Anthropic 提供 Claude 使用額度與工程人力，其中 BigHat 一案由 Anthropic 直接支付實驗費用，BigHat 技術報告的第一作者掛名單位為 Anthropic；六份技術報告皆非同儕審查出版品 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development) [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。

## 本書庫解讀（評論）

以下為本書庫的判斷，非來源結論。

- **先把可回查程度這一點記下來：本則在同類公告中偏高的一端。** 六份技術報告同日釋出、六個面板載有樣本數與限制聲明、BigHat 那一份 31 頁報告讓公告的每個數字都能被逐項回查 —— 本書庫近兩個月收錄的同類公告中，多數連一個可供爭論的量都不存在。下面幾段對選數字與訂標準的批評，正是因為有這些可回查物才寫得出來；這個順序不應該被顛倒。
- **「量尺被換掉」是本則在方法上最值得學的一段，也是它最該被追問的一段。** 技術報告的論證紮實：回到原始升溫曲線、建立物理模型、對濃度與升溫速率做出事前預測再跑實驗驗證，並誠實記下其中一項預測被推翻。問題不在方法，而在最後那句成績怎麼報 —— 當提出設計的模型同時也提出了評分標準，而最終規格又如技術報告自述是在看過結果之後設定的，「兩個先導分子在三項性質上都優於親本」這句話的獨立性就被削弱了。技術報告把這些全部寫出來了，公告沒有。
- **公告挑數字的方向一致地偏向同一邊。** 五個可核對的量化說法裡，三個挑的是範圍上緣或另一個集合的最佳值：「10 倍以上」對應的是未被提名的設計（被提名者為 6 到 9 倍）、「18°C」是 8 到 18°C 區間的上緣、「100 倍以上」來自單一個孔。單獨看每一個都不算錯誤；放在一起看，這是一種系統性的挑法，而讀者無從從正文察覺，因為正文一個區間、一個樣本數都沒有給。
- **詳細版與正文的落差，在本則有一個特殊形狀：它不在別的文件上，而在同一頁的按鈕裡。** 面板沒有自己的網址，因此任何轉述、摘要或自動擷取這一頁的流程，預設拿到的都是沒有樣本數、沒有限制聲明、也沒有利益揭露的那一層。
- **Enveda 與 Mithril 兩案的揭露密度明顯高於其他案，反而凸顯了正文的取捨。** Enveda 面板主動報出系統誤讀了一筆手寫更正、報出兩邊各有多少條意見其實不需處理（79% 對 82%）、報出四小時對三個月兩邊都不含三週人工覆核；Mithril 面板把每一組小鼠樣本數都標出來（7／4／12 與 8／8／12）、明寫受測的是 tool molecule 而非候選藥物、並在時程圖上標註目標不等於承諾。以公司發布的材料而言，這樣的標示密度高於本書庫近兩個月收錄的多數同類公告 —— 真正的問題是它們全部停在面板裡。
- **醫療橋接：這一則最該被醫療影像與臨床 AI 借走的，是「終點什麼時候定」這個問題。** 把本則的形狀換到醫療場景，對應的是一組非常具體的情境：判讀模型的開發方同時定義了 reference standard（參考標準，即判定對錯的依據）、同時選定了要報的 operating point（工作點，即靈敏度與特異度的取捨位置）、或在看過測試集表現後才決定要報哪一個子族群。本書庫先前收錄的 GE HealthCare End-tidal Control 研究之所以可信，正是因為它事先寫明三個假設、並在其中一個未達自訂門檻時照實報出。實務上可以收斂成一個採購端問句：這份成果的成功標準是什麼時候寫下來的，以及寫的人和做的人是不是同一方。第二件可以借走的是 Enveda 那一案的形狀 —— 文件覆核是醫療機構裡體量最大、最像藥廠品保流程的工作（放射科報告的品質抽查、病歷編碼、臨床試驗的來源文件核對），而該案把「不需處理的意見有多少」報了出來，這正是任何輔助覆核工具在科室裡能不能存活的關鍵指標：抓到幾個問題決定它有沒有用，誤報幾條決定它會不會被關掉。

## 產業影響

- **模型供應商開始直接持有藥物資產，而不只是賣工具。** Anthropic 在本則中揭露收購了一人公司 Mithril Medicine 並將其兩個計畫納為自有研發計畫，另與 The Column Group 共同設立新公司 Pleiades [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。對生技產業而言，這代表前沿模型供應商從上游供應者變成同時是合作方與競爭者；對醫療 AI 採購端而言，這類垂直整合會讓「模型供應商對某個臨床領域的成果宣稱」在未來更難被當作中立的技術評估。
- **評估的獨立性在這類合作中結構性地難以維持。** 本則六案全部由 Anthropic 提供運算額度與工程人力，其中一案由 Anthropic 直接支付實驗費用，BigHat 技術報告的第一作者掛名 Anthropic。這不是本則獨有的問題，而是「模型供應商深入參與真實研發流程」這個模式的必然結果 —— 要取得可用的案例，就得深入到足以影響結果的程度。可行的緩解不是要求供應商退出，而是要求成功標準在合作開始前就寫定並公開。
- **「AI 加速藥物開發」目前可被驗收的位置，集中在臨床前與文書作業兩端。** 本則六案中，真正有濕式實驗數據的三案全部停在體外或細胞層級，Mithril 停在小鼠，BMS 一案只有流程描述與一段主管引述。證據密度最高的反而是 Enveda 的文件覆核 —— 它不涉及任何生物學宣稱，因此可以被完整量化。這個分布本身就說明了當下 AI 在藥物開發鏈上可被驗收的位置在哪裡。
- **技術報告與公司公告的詳細程度差距，正在變成一種穩定的結構。** 本則的技術報告品質相當高（事前預測、推翻自己的預測、逐項列出保留），而公告正文沒有樣本數、沒有揭露、沒有註腳。對於以公司公告為資訊來源的讀者，這個落差會直接影響他們對證據等級的判斷，而本則的詳細層還少了一個可獨立連結的網址。

## 與書庫其他文章的關係

兩則是前沿模型供應商在六天內先後發布的生命科學成果公告，落差型態卻不同：該則是公告與它所連結的預印本在同一個數字上互相矛盾，本則的數字則全部正確，問題出在被挑出來的那一個不是被提名的那一個，以及量尺本身在專案中途被換過；兩則並讀可以看出「回去對數字」這個動作除了核對數值，還得核對那個數值描述的是哪一個對象、用哪一把尺量的: [1,946 個 AI 代理各讀一個基因擾動，32 分鐘產出全腦圖譜解讀](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md)

該則的 90% 是前七名清單的命中率、排第一名的只有 56%，兩個數字都在 Google 自家的技術部落格裡；本則的「結塊慢 100 倍以上」與「6 到 9 倍」同樣分屬兩層官方文件，而本則多了一層 —— 詳細版不是另一個頁面，而是同一頁上要點開才看得到的面板，六段利益揭露也只存在於那些面板裡: [AMIE 看診前先問病史：98 人的 Lancet 可行性研究](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

該則是本書庫目前最接近完整部署評估的樣本，它事先寫明三個假設、並在其中一個未達自訂門檻時照實報出；本則恰好是相反的作法，技術報告自述最終規格是在看過結果之後才設定的，而按原規格最後一輪 113 個 scFv 設計沒有一個以實測解離常數通過，兩則並讀可以看出「終點什麼時候定」這件事如何決定一份成果該被當成驗證還是當成探索: [ETC 自動調控麻醉氣體：密西根大學 12,818 例回溯研究](2026-10-19-ge-healthcare-end-tidal-control-michigan-study.md)

兩則是前沿模型供應商相隔十二天發布的生命科學成果公告，而該則比本則更早一步 —— 本則至少有六份技術報告可以把公告裡的每一個數字逐項回查，該則除了一個資料庫編號之外沒有任何可回查的量測，所有成果都停在 wet-lab validation 之前；兩則並讀可以看出同一類公告在「可查核物存不存在」這一軸上的兩個位置: [DeepMind 抗菌胜肽示範：代理程式從資料庫走到實驗計畫](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

同一家公司相隔一天的兩則公告，分屬成果側與取用側，而兩則的可核對物都不在正文：本則的樣本數與六段利益揭露藏在同頁要點開的面板裡，該則的夥伴總數與正文三份名單對不起來，決定研究者實際能用到哪一級模型的那段限制則寫在兩個月前的另一頁；兩則並讀可以看出同一家公司在同一週內，把關鍵限定條件放在正文以外的兩種不同作法: [Anthropic 把免費 Claude 額度擴大到基金會與研究機構](2026-10-30-anthropic-ai-for-science-foundations-expansion.md)

兩則的核心都是「訂標準的人與被評分的系統出自同一方」：本則的成功規格依技術報告自述是在看過結果之後才定下的；該則則是 benchmark、Gatekeeper、Judge 與受測系統 MAI-DxO 由同一個團隊設計，論文的利益揭露列出全體作者皆為 Microsoft 員工並持有股權。差別在於該則把整套評分程式碼開源了，讓外部至少能檢視那把尺怎麼刻: [SDBench 與 MAI-DxO：把診斷評估改成逐步問診](2026-11-02-microsoft-mai-dxo-sdbench-sequential-diagnosis.md)

兩則是前沿模型供應商相隔七天發布的藥物開發成果，可回查的深度不同：本則同日釋出六份技術報告，公告裡的數字能逐項對照回原始報告；該則以工作流程示範為主，代理程式側未公布模型指標。兩則並讀可以看出「廠商自報」在證據密度上的落差: [DeepMind 化學資訊學 Skills：代理程式跑完一輪藥物設計](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md)

兩則都是同一家公司的生命科學成果，而最關鍵的限定條件都不在正文：本則的樣本數與成功標準訂定時點藏在要點開的面板裡，該則判定 AAV capsid「預測準確」的門檻（兩個模型任一達 Cα RMSD 3 Å 以內）與被寫進提示詞的前人初始化方法，都只寫在第三條註腳: [Fable 與 Mythos 5.2 降價發布，十四列評測、生科須審核](2026-11-10-anthropic-claude-fable-mythos-5-2-launch.md)

## 實務的啟發

- **要引用某一案時，先確認那一案接在流程的哪一段。** 本則六案跨越的範圍從抗體量測指標、設計生成與篩選、文件覆核與撰寫，到文獻判讀與試驗規劃，可驗收程度各不相同。把它們一起引用來支持「AI 加速新藥」這類整體宣稱，會把文書作業的成績混進生物學成績裡。
- **引用數字時，把倍數連同它修飾的對象一起帶。** 「bound more than 10x more tightly」描述的是兩個 pilot 中最緊的結合者，不是被提名的兩個先導分子（後者為 6 到 9 倍）；「clumped more than 100x more slowly」來自單一個孔，技術報告自己標了這項保留。若要引用 BigHat 這一案，建議直接引用技術報告的確值（解離常數 1.15 nM 對 10.3 nM、0.63 nM 對 3.7 nM），而不要引用公告的倍數。
- **把「成功標準何時寫定」列為評估任何 AI 成果的固定問句。** 本則提供了一個清楚的反面樣本：技術報告自述 `we set the final specifications knowing the results`，而按原規格最後一輪 113 個設計沒有一個以實測值通過。這個問句在醫療 AI 的對應形式是：參考標準、工作點、以及要報告的子族群，分別是在看到測試集結果之前還是之後決定的。
- **評估輔助覆核類工具時，問「不需處理的意見占多少」。** Enveda 那一案報出了這個數字（系統 33／42，人工 79／96），而這在多數同類宣稱中看不到。一套覆核工具在科室裡的存活，取決於真陽性與誤報兩個數字的比值，而不是單看它抓到了幾個問題；放射科報告品質抽查、病歷編碼稽核、臨床試驗來源文件核對都適用同一組指標。
- **讀這類公告時，先確認詳細版在哪裡、以及它有沒有網址。** 本則的樣本數、限制聲明與利益揭露全部只存在於同頁的可展開面板中，沒有獨立網址。這意味著書籤、轉述、摘要工具與任何自動擷取流程預設都拿不到這一層。實務上可以把它變成一個動作：遇到 `Read more` 或類似控制項，先點開再判斷這一則的證據密度。
- **區分「臨床前」與「藥物開發」這兩個詞的涵蓋範圍。** 公告標題說的是加速 drug development（藥物開發），而公告自己在結尾寫明 `so far it is mostly preclinical`。本則六案中唯一觸及臨床階段的是 BMS 的試驗規劃評估，而該案沒有任何數字。引用本則支持「AI 已在加速新藥上市」這類主張，會超出來源本身的涵蓋範圍。

## 後續追蹤

- 六份技術報告中是否有任一份進入同儕審查並刊出。BigHat 那一份若刊出，`we set the final specifications knowing the results` 這句自述與「兩個先導分子在三項性質上皆優於親本」的結論會如何被審稿處理，是判斷本則證據等級的直接指標 [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。
- BigHat 那一案的聚集速率結果是否有複孔重現。技術報告自列 `the aggregation value is one well`，這是「100 倍以上」能否成立的唯一待補項 [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。
- Divergence 的兩個抗體臂能否組成完整雙臂抗體，並在免疫細胞上證明可移除已結合的 IgE 而不觸發它意圖預防的免疫反應。這是該案面板自列的下一步，也是該路線唯一能被真正驗收的終點 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- Mithril 是否如其時程所述在 2027 年提名正式候選藥物、2028 年底前進入 LAMA2-CMD 人體試驗。公告已標明 2026 年之後的日期為目標而非承諾 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- 與 Bristol Myers Squibb 的臨床試驗規劃合作是否在 2027 年產出任何可核對的數字。該案是本則唯一觸及臨床階段者，目前只有流程描述與一段主管引述 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。
- 是否出現由非合作方執行的獨立評估。本則六案全部由模型供應商提供資源，其中一案由其直接支付實驗費用；在出現獨立複現之前，這些結果適合當作可行性示範而非效能證據。

## References

- `pr` — Anthropic，[Early progress on accelerating drug development with Claude](https://www.anthropic.com/research/early-progress-drug-development)（官方公告，2026-10-27；六段案例詳述為同頁可展開面板，無獨立網址）。底 URL：`https://www.anthropic.com/news`
- `bighat` — Stanton S, Solomon A, Delaney E, Montgomery M, Acker T, Henrici R, Eid C, Abrams E, Greenside P，[Reasoning in the loop: antibody lead optimization by probing mechanism and measurement](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)（BigHat Biosciences 技術報告 PDF，31 頁，非同儕審查；第一作者單位為 Anthropic）。底 URL：`https://www.bighatbio.com/`

[Home](../) · [Industry Watch](./)
