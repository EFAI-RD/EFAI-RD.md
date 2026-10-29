---
title: "Anthropic 公布 Claude 參與的六個藥物開發合作案：公告說抗體「結塊慢 100 倍以上」，技術報告寫明那是單一個孔的讀數，而判定成功的規格是看過結果之後才定的"
category: industry-watch
date: 2026-10-28
updated: 2026-10-28
tags: [Anthropic, Claude, drug-development, antibody-engineering, BigHat-Biosciences, Divergence-Labs, Enveda, Generate-Biomedicines, Mithril-Medicine, lead-optimization, regulatory-documents, preclinical, evaluation-metrics]
catalog_id: "anthropic:early-progress-drug-development-2026-10-27"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
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
refs:
  pr:
    title: "Anthropic：Early progress on accelerating drug development with Claude（官方公告；六段案例詳述為同頁可展開面板）"
    url: "https://www.anthropic.com/research/early-progress-drug-development"
  bighat:
    title: "Stanton S, Solomon A, Delaney E, Montgomery M, Acker T, Henrici R, Eid C, Abrams E, Greenside P：Reasoning in the loop: antibody lead optimization by probing mechanism and measurement（BigHat Biosciences 技術報告，31 頁；第一作者單位為 Anthropic）"
    url: "https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026"
---

[Home](../) · [Industry Watch](./)

# Anthropic 公布 Claude 參與的六個藥物開發合作案：公告說抗體「結塊慢 100 倍以上」，技術報告寫明那是單一個孔的讀數，而判定成功的規格是看過結果之後才定的

## 來源

- 組織：Anthropic；合作方 BigHat Biosciences、Divergence Labs、Enveda、Generate Biomedicines、The Column Group、Bristol Myers Squibb
- 事件：發布公告 `Early progress on accelerating drug development with Claude`，彙整六個藥物開發合作案與一項自有研究計畫的早期結果
- 日期：2026-10-27
- 官方入口：<https://www.anthropic.com/research/early-progress-drug-development>
- 本則為**單源（單一組織主導），待交叉驗證**。公告連出六份技術報告，其中 BigHat 那一份可完整取用並逐項回查，但它不是獨立佐證 —— 該報告第一作者的掛名單位是 Anthropic，而同頁面板的揭露寫明 `Anthropic paid BigHat for carrying out the laboratory work described here` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)

**編輯：** Clarence

Anthropic 在 2026-10-27 公布其生命科學團隊過去數月的合作成果：六個藥物開發組織（BigHat Biosciences、Bristol Myers Squibb、Divergence Labs、Enveda、Generate Biomedicines、The Column Group）各自把 Claude 接進自己的研發流程，另有一項由 Anthropic 收購而來的自有計畫。公告同時表明這些工作 `so far it is mostly preclinical`，亦即多數尚未進入人體試驗階段 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

公告正文約 1,850 字，只出現三個百分比與兩個倍數。把這五個數字逐一回到同頁可展開的案例面板與公開的技術報告之後，數值本身沒有一個錯；落差集中在三件事上 —— 被挑出來的那個數字常常不是被提名的那個分子、幾個分母在正文裡不存在，以及最關鍵的一項：BigHat 那一組用來判定「成功」的量尺，是專案進行到一半由被評估的模型自己提議換掉的。

## 背景

這一則需要分三層讀，而三層的詳細程度差距很大。

- **第一層：公告正文。** 2026-10-27 上線（頁面 `<time datetime="2026-10-27">` 顯示 `Oct 27, 2026`，JSON-LD `datePublished` 與 `meta article:published_time` 同為 2026-10-27，三處一致）。正文約 1,850 字，沒有註腳（`<sup>` 元素 0 個），沒有任何樣本數標記（`n =` 出現 0 次），也沒有任何一段利益揭露（`Disclosure` 一詞在正文出現 0 次）[(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **第二層：同一頁上的六個可展開面板。** 公告每段結尾的 `Read more` 不是連結，而是一個在原頁開啟對話框的按鈕；各案的完整敘述、樣本數、限制聲明與利益揭露都在這裡。六段揭露分三種強度：Generate、Divergence、Enveda、The Column Group 為 `Anthropic provides ... with Claude usage credits and engineering support`（Divergence 另加 `reimburses certain third-party computing costs`），BigHat 則是 `Anthropic paid BigHat for carrying out the laboratory work described here`。這些資訊沒有獨立網址，讀者若只讀正文或只讀轉述，不會知道它們存在 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **第三層：六份技術報告。** 分別託管於各合作方自己的網站或 Anthropic 的內容伺服器，皆非同儕審查出版品。本文逐項核對的是其中的 BigHat 報告 `Reasoning in the loop: antibody lead optimization by probing mechanism and measurement`（31 頁），其作者列為 Samuel Stanton（單位 1：Anthropic）與八位 BigHat 人員（單位 2）[(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。

## 事實（可核對）

以下左側為公告正文的說法，右側為同頁面板或技術報告在同一件事上的寫法。

- **BigHat／「bound more than 10x more tightly」** — 公告寫 `Compared with the originals, the best versions bound more than 10x more tightly, the cancer-targeting lead stayed in solution 18°C higher, and the lead for longer-lasting drugs clumped more than 100x more slowly` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。同頁面板對同兩個分子寫的是 `they bound six to nine times more tightly, held together at temperatures 8 to 18°C higher`，`more than tenfold` 一語在面板裡修飾的是另一組對象：`The tightest binders in both pilots improved more than tenfold`。技術報告給出確值：VHH 先導分子解離常數 1.15 nM 對親本 10.3 nM、scFv 0.63 nM 對 3.7 nM，摘要自述 `The VHH lead binds albumin about nine times more tightly`；而報告中達到 10 倍以上的是未被提名的設計（VHH 最緊者 0.85 nM，`12 times tighter than the parent`；scFv 一個基礎設計 `about 15 times tighter`）[(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。亦即「10 倍以上」與「被選為先導的兩個分子」是兩個不同的集合。

- **BigHat／「clumped more than 100x more slowly」** — 這是公告全文唯一的三位數倍數。`100-fold`、`100x` 與 `order of magnitude` 在 31 頁技術報告中全文命中 0 次，同頁面板也只寫 `the final VHH clumped far more slowly`。可對應的原始數值是聚集速率指標 `p k_agg`：`p k_agg is +2.00 on one identified well against −0.39`，兩者相差 2.39 個對數單位。技術報告在同一段緊接著自列兩項保留：`the aggregation value is one well, and the K_D margin, 0.14 log, is small` [(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。亦即這個倍數成立於單一個孔的讀數，而「單一個孔」這項限制在公告正文與面板中都不存在。

- **BigHat／量尺在專案中途被換掉** — 公告把這件事寫成一項優點：`Partway through, the team suspected the standard heat-stability and clumping metrics were misleading. Claude and the researcher reanalyzed the raw data, then proposed different metrics and a protocol change to test them` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。技術報告說明得更完整：原本儀器輸出的 apparent melting temperature（表觀熔點）與 aggregation onset（聚集起始溫度）被判定無法分辨好壞分子，於是在 VHH 上改用聚集速率、在 scFv 上改用 collapse temperature（溶液崩解溫度）。報告並寫明兩件公告沒有提的事：`we set the final specifications knowing the results`，以及按原規格 `none of the 113 final-round scFv designs passes with a measured K_D`（另有兩個若採計解離速率下限可通過，`each on one well`）[(ref: bighat)](https://www.bighatbio.com/bighat-anthropic-collaboration-report-10-27-2026)。同頁面板對 VHH 的對應敘述是 `No design in four rounds received a passing value that also cleared quality checks, including the final molecule` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **Generate Biomedicines／「more effective」** — 公告寫 `One design was about 70% shorter than the standard version, and in lab tests it was more effective: it allowed immune cells to make roughly 10 times as many receptors` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。同頁面板的摘要段寫的是 `The best design was about 70% shorter and no less effective`，並把 10 倍歸給 `one of the top designs`；面板後段的詳述則把兩者寫在同一個候選身上。`no less effective`（不遜於）與 `more effective`（更好）是兩個不同強度的宣稱，而這兩句出自同一頁。面板另寫明 `These are early laboratory results—Generate has not yet tested that the designs are safe or effective in patients`，以及首輪送驗的設計數為 186 個、整個專案歷時八個月 —— 三項皆不在正文 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **Divergence Labs／35,000 這個數字的位置** — 公告寫 `generated roughly 35,000 antibody designs in about a month to be narrowed down and tested. In those early tests, Divergence found "hits" for both arms: three designs that could bind to IgE, and 20 that could dislodge it` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。這個寫法容易被讀成 23 比 35,000。面板給出實際分母：35,000 個設計經結構預測模型篩選後，`kept only the highest scoring ones—no more than 96 per arm—to make and test in the lab`，實際進入濕式實驗的是 disruptor arm 91 個與 anchor arm 57 個；結果為 `20 of the 91 designs worked as intended` 與 anchor arm `three of them (around 5%)`。時間方面，面板寫的是 disruptor arm 約三週、anchor arm 約四週半，而非單一的「約一個月」；運算成本為 `around 2,750 hours of computing time spread across many Nvidia H100 GPUs`，正文未提 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **Enveda／11 個問題與 89%** — 公告寫 `Over tests on 1,061 pages of documentation, Claude caught all 11 issues that human reviewers had spotted—and flagged seven they'd missed. In the process, this method reduced human review time by 89%, from over 25 hours to less than three` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。面板把兩個數字拆開歸屬：11 個問題是 `Across its runs on these records`、`in at least one of its runs` 的聯集，而七個額外問題與 89% 來自 `one timed run`。時間的確值為人工 1,553 分鐘（25.9 小時）對系統加覆核 166 分鐘（2.8 小時）。面板另給出正文沒有的兩組數字與一項誤讀：系統計時那一輪共提出 42 條意見、其中 33 條（79%）不需處理，人工提出 96 條、其中 79 條（82%）不需處理；`the CDP did misread one entry, a struck-through handwritten correction`（未偵測到任何無中生有的發現）。評分者為 Enveda 自家品質部門一位未參與審查的成員，另一位成員覆核 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **Enveda／四小時對三個月** — 公告寫 `One took four hours, compared to about three months by hand` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。面板在同一組數字後補了一句正文沒有的限定：`Neither figure includes the three-week manual review process that every draft goes through`。此外，被比較的人工版本是該合作開始之前就已完成的草稿，而非同期對照 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **The Column Group／45 這個數字量的不是正確率** — 公告寫該公司的第一個 Claude skill `has been evaluated on 45 target-disease pairs`，未給結果 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。面板給出的結果是速度而非正確性：`has cut the process of finding and interpreting the relevant scientific literature from weeks to days`。面板沒有報出這 45 組評估中判斷正確的比例，也沒有說明對照標準是什麼 [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **Mithril Medicine／小鼠結果的樣本數** — 公告寫 `Mithril took a possible treatment for one form of muscular dystrophy from an idea to promising results in mice in less than 18 months`，並寫 `we expect a drug to be ready to start clinical trials in humans as soon as late 2028` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。面板給出樣本數：六週齡時的握力與三頭肌肌力比較為治療組 7 隻、未治療疾病組 4 隻、健康對照 12 隻；存活為治療組八隻死一隻、未治療組八隻死四隻、健康組 12 隻全活。面板並寫明受測的是 `tool molecules—early, unrefined versions`（非正式候選藥物）、`These are early results in mice, not human trials`，以及時程圖註 `Dates after 2026 are targets, not commitments` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

- **公告沒有宣稱的事** — 正文中 `FDA` 出現 0 次、`peer`（同儕）0 次、`approval`／`approved`（核准）0 次，`patient`（病人）僅 1 次。公告沒有宣稱任何一項成果已獲法規核准或經過同儕審查，並在結尾明確寫出 `All of this research is still at an early stage` 與 `so far it is mostly preclinical` [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。

## 本書庫解讀（評論）

以下為本書庫的判斷，非來源結論。

- **本則的落差型態與本書庫近期處理的幾則不同，值得單獨記下來。** 近期幾則廠商宣傳的問題是「限定條件被留在被連結的論文裡」—— 數字對，但分母在別處。本則的詳細版不在別的文件上，而在同一頁、同一段後面那顆 `Read more` 按鈕裡，而且那顆按鈕沒有自己的網址。這帶來一個實務後果：任何轉述、摘要或自動擷取這一頁的流程，預設拿到的都是沒有樣本數、沒有限制聲明、也沒有利益揭露的那一層。六段揭露全部只存在於面板中，這件事本身就值得記錄。

- **「量尺被換掉」是本則最該被記住的一件事，而它恰好是公告拿來當賣點的那一段。** 公告把 Claude 重新定義評估指標寫成跨出單純分子設計的一步，這個判斷在科學上站得住：技術報告的論證確實紮實 —— 它回到原始升溫曲線、建立物理模型、對濃度與升溫速率做出事前預測再跑實驗驗證，並誠實記下其中一項預測被推翻（`refuted`）。問題不在方法，而在最後那句成績怎麼報。當提出設計的模型同時也提出了評分標準，而最終規格又如技術報告自述是在看過結果之後設定的，那麼「兩個先導分子在三項性質上都優於親本」這句話的獨立性就被削弱了 —— 按原規格，最後一輪 113 個 scFv 設計沒有一個以實測解離常數通過。技術報告把這些全部寫出來了，公告沒有。

- **公告挑數字的方向一致地偏向同一邊。** 五個可核對的量化說法裡，三個挑的是範圍上緣或另一個集合的最佳值：「10 倍以上」對應的是未被提名的設計而非兩個先導分子（後者為 6 到 9 倍）、「18°C」是 8 到 18°C 區間的上緣、「100 倍以上」來自單一個孔。單獨看每一個都不算錯誤；放在一起看，這是一種系統性的挑法，而讀者無從從正文察覺，因為正文一個區間、一個樣本數都沒有給。

- **Enveda 那一案的揭露密度明顯高於其他幾案，反而凸顯了正文的取捨。** 面板主動報出系統誤讀了一筆劃線塗改的手寫更正、報出系統與人工各自有多少條意見其實不需處理（79% 對 82%）、報出四小時對三個月兩邊都不含三週人工覆核。這些都是會讓數字看起來沒那麼漂亮的資訊，合作方願意寫出來。正文把它們全部略去，留下的是「抓到全部 11 個、還多抓七個、省下 89% 時間」。

- **本則同時提供了一個正面樣本，不應該被上面幾段蓋過。** Mithril 那一案把小鼠實驗的每一組樣本數都標了出來（7／4／12 與 8／8／12），明寫受測的是 tool molecule 而非候選藥物，並在時程圖上標註 `Dates after 2026 are targets, not commitments`。以一份公司發布的材料而言，這樣的標示密度高於本書庫近兩個月收錄的多數同類公告。真正的問題是這些標示停在面板裡，沒有一個進到正文。

- **醫療橋接：這一則最該被醫療影像與臨床 AI 借走的，是「終點什麼時候定」這個問題。** 本則的核心缺陷不是造假，而是評分標準與被評分的系統出自同一方、且標準在看過結果後才定案。把這個形狀換到醫療場景，對應的是一組非常具體的情境：判讀模型的開發方同時定義了 reference standard（參考標準，即判定對錯的依據）、同時選定了要報的 operating point（工作點，即靈敏度與特異度的取捨位置）、或在看過測試集表現後才決定要報哪一個子族群。本書庫先前收錄的 GE HealthCare End-tidal Control 研究之所以可信，正是因為它事先寫明三個假設、並在其中一個未達自訂門檻時照實報出；本則則示範了相反的一端。實務上可以把它收斂成一個採購端問句：這份成果的成功標準是什麼時候寫下來的，以及寫的人和做的人是不是同一方。第二件可以借走的是 Enveda 那一案的形狀 —— 文件覆核是醫療機構裡體量最大、最像藥廠品保流程的工作（放射科報告的品質抽查、病歷編碼、臨床試驗的來源文件核對），而該案把「不需處理的意見有多少」報了出來，這正是任何輔助覆核工具在科室裡能不能存活的關鍵指標：抓到幾個問題決定它有沒有用，誤報幾條決定它會不會被關掉。

## 產業／生態影響

- **模型供應商開始直接持有藥物資產，而不只是賣工具。** Anthropic 在本則中揭露收購了一人公司 Mithril Medicine 並將其兩個計畫納為自有研發計畫，另與 The Column Group 共同設立新公司 Pleiades [(ref: pr)](https://www.anthropic.com/research/early-progress-drug-development)。對生技產業而言，這代表前沿模型供應商從上游供應者變成同時是合作方與競爭者；對醫療 AI 採購端而言，這類垂直整合會讓「模型供應商對某個臨床領域的成果宣稱」在未來更難被當作中立的技術評估。

- **評估的獨立性在這類合作中結構性地難以維持。** 本則六案全部由 Anthropic 提供運算額度與工程人力，其中一案由 Anthropic 直接支付實驗費用，BigHat 技術報告的第一作者掛名 Anthropic。這不是本則獨有的問題，而是「模型供應商深入參與真實研發流程」這個模式的必然結果 —— 要取得可用的案例，就得深入到足以影響結果的程度。可行的緩解不是要求供應商退出，而是要求成功標準在合作開始前就寫定並公開。

- **「AI 加速藥物開發」的證據等級目前仍集中在臨床前與文書作業兩端。** 本則六案中，真正有濕式實驗數據的三案（Generate、Divergence、BigHat）全部停在體外或細胞層級，Mithril 停在小鼠，BMS 一案只有流程描述與一段主管引述、無任何數字。證據密度最高的反而是 Enveda 的文件覆核 —— 它不涉及任何生物學宣稱，因此可以被完整量化。這個分布本身就說明了當下 AI 在藥物開發鏈上可被驗收的位置在哪裡。

- **技術報告與公司公告的詳細程度差距，正在變成一種穩定的結構。** 本則的技術報告品質相當高（事前預測、推翻自己的預測、逐項列出保留），而公告正文沒有樣本數、沒有揭露、沒有註腳。對於以公司公告為資訊來源的讀者，這個落差會直接影響他們對證據等級的判斷，而本則的詳細層還少了一個可獨立連結的網址。

## 與書庫其他文章的關係

兩則是前沿模型供應商在六天內先後發布的生命科學成果公告，落差型態卻不同：該則是公告與它所連結的預印本在同一個數字上互相矛盾，本則的數字則全部正確，問題出在被挑出來的那一個不是被提名的那一個，以及量尺本身在專案中途被換過；兩則並讀可以看出「回去對數字」這個動作除了核對數值，還得核對那個數值描述的是哪一個對象、用哪一把尺量的: [OpenAI 公布以 AI 代理群解讀全腦 Perturb-seq 圖譜：公告寫「引用逾 700 篇」，它所連結的論文寫的是「711 倍」](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md)

該則的 90% 是前七名清單的命中率、排第一名的只有 56%，兩個數字都在 Google 自家的技術部落格裡；本則的「結塊慢 100 倍以上」與「6 到 9 倍」同樣分屬兩層官方文件，而本則多了一層 —— 詳細版不是另一個頁面，而是同一頁上要點開才看得到的面板，六段利益揭露也只存在於那些面板裡: [Google 宣傳 AMIE 的 Lancet 研究：「鑑別診斷與醫師最終診斷相符 90%」是前七名清單的命中率，同一天更新的自家研究部落格寫著排第一名的只有 56%](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

該則是本書庫目前最接近完整部署評估的樣本，它事先寫明三個假設、並在其中一個未達自訂門檻時照實報出；本則恰好是相反的作法，技術報告自述最終規格是在看過結果之後才設定的，而按原規格最後一輪 113 個 scFv 設計沒有一個以實測解離常數通過，兩則並讀可以看出「終點什麼時候定」這件事如何決定一份成果該被當成驗證還是當成探索: [GE HealthCare 發布密西根大學 End-tidal Control 研究：新聞稿裡的 62.3% 是論文為「典型病人」建構的模型推算值，而出面肯定這項研究的 GE 高層是論文共同作者](2026-10-19-ge-healthcare-end-tidal-control-michigan-study.md)

兩則是前沿模型供應商相隔十二天發布的生命科學成果公告，而該則比本則更早一步 —— 本則至少有六份技術報告可以把公告裡的每一個數字逐項回查，該則除了一個資料庫編號之外沒有任何可回查的量測，所有成果都停在 wet-lab validation 之前；兩則並讀可以看出同一類公告在「可查核物存不存在」這一軸上的兩個位置: [Google DeepMind 示範用 Antigravity 搜尋抗菌胜肽：「數天變成一次對話」「in hours」「數小時變成數分鐘」三種加速說法分屬三個官方位置，沒有一個附得出絕對數值；而那個候選分子在 UniProt 的名稱，證據欄寫的是 Google:ProtNLM](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

## 實務的啟發

- **引用本則時，把倍數連同它修飾的對象一起帶。** 「bound more than 10x more tightly」描述的是兩個 pilot 中最緊的結合者，不是被提名的兩個先導分子（後者為 6 到 9 倍）；「clumped more than 100x more slowly」來自單一個孔，技術報告自己標了這項保留。若要引用 BigHat 這一案，建議直接引用技術報告的確值（解離常數 1.15 nM 對 10.3 nM、0.63 nM 對 3.7 nM），而不要引用公告的倍數。

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
