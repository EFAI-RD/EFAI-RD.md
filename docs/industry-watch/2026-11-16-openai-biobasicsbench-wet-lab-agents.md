---
parent: Industry Watch
nav_order: 4
title: "例行實驗判讀只拿 66.7%：OpenAI BioBasicsBench 拆解"
category: industry-watch
date: 2026-11-16
tags: [OpenAI, BioBasicsBench, Ligo, benchmark, wet-lab, life-sciences, agentic-workflow, multimodal, GPT-6-Astra, GPT-6.1-Sol, rubric-scoring, research-workflow, biosafety, biosecurity, evaluation]
catalog_id: "openai:biobasicsbench-wet-lab-benchmark-2026-11-06"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.2"
source:
  orgs:
    - "OpenAI"
    - "Ligo"
  event: "OpenAI 發布 BioBasicsBench，與生技公司 Ligo 共同建立的 100 題濕實驗室評測，量測代理程式判讀原始實驗證據的能力，並公布七個自家模型在 xhigh 推理設定下的平均得分與 95% 信賴區間"
  event_date: "2026-11-06"
  official_url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/"
  single_source: true
  single_org: true
related_articles:
  - path: "2026-10-22-openai-distributed-agents-perturb-seq-atlas.md"
    relation: "兩則都是 OpenAI 把代理程式放進生物研究，但落在流程的兩端：該則讓代理去讀一份已發表的全腦 Perturb-seq 圖譜並產出假說，本則量的是代理能不能讀懂還沒整理成圖表的膠片、培養皿與儀器輸出"
  - path: "2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md"
    relation: "兩則都在談代理程式進入實驗科學，揭露形式剛好相反：該則是一場沒有任何分數的示範流程，本則是一組有逐條評分標準與 95% 信賴區間、卻沒有人類基準的分數"
  - path: "2026-10-07-openai-gpt-6-1-sol-launch.md"
    relation: "同一家公司對同一個型號的兩種揭露方式：該則記錄 GPT-6.1 Sol 發布時除 Terminal-Bench Science 的 68.1% 外不給絕對分數，本則把同一個型號放進 BioBasicsBench，給了 62.0% 與 55.6–68.4% 的 95% 信賴區間"
refs:
  main:
    title: "Measuring how AI agents handle everyday wet-lab science（OpenAI 官方公告，2026-11-06）"
    url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/"
  inside:
    title: "Inside BioBasicsBench（同一公告的題庫組成與評分一節）"
    url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#inside-biobasicsbench"
  results:
    title: "Results（同一公告的成績一節）"
    url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#results"
  improve:
    title: "GPT-6 Astra improvements from GPT-5.6 Sol（同一公告的進步案例一節）"
    url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#gpt-6-astra-improvements-from-gpt-56-sol"
  shortfall:
    title: "Where models still fall short（同一公告的失誤案例一節）"
    url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#where-models-still-fall-short"
  outlook:
    title: "Building toward reliable lab assistance（同一公告的結語一節）"
    url: "https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#building-toward-reliable-lab-assistance"
---

[Home](../) · [Industry Watch](./)

# 例行實驗判讀只拿 66.7%：OpenAI BioBasicsBench 拆解

## 來源

- 組織／產品：OpenAI — BioBasicsBench；共同開發方為生技公司 Ligo，公告描述為「a biotech company focused on enzyme design」。
- 事件：發布 BioBasicsBench，公布題庫組成、出題與評分流程、七個自家模型的成績，以及六個逐例說明的對錯案例。
- 日期：2026-11-06（公告頁頁首可見 `November 6, 2026`，OpenAI 新聞列表頁同樣標 2026 年 11 月 6 日）
- 官方入口：[Measuring how AI agents handle everyday wet-lab science](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/)
- **單源，待交叉驗證**：本文引用的題庫組成、評分方式與全部分數都只出自這一頁。Ligo 是共同開發方而非獨立驗證者，公告中沒有指向 Ligo 的連結，也沒有 Ligo 自身的對應聲明可供比對。

**編輯：** Clarence

OpenAI 在 2026-11-06 發布 BioBasicsBench，一組與生技公司 Ligo 共同建立的濕實驗室評測 [(ref: main)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/)。它的 100 道題目不問生物學知識，而是把實驗台上的原始證據直接交給代理程式：膠片與轉漬影像、培養皿照片、顯微影像堆疊、定序讀段、儀器螢幕的翻拍，要求它判讀資料、找出錯誤，並在證據不足以支撐結論時說出來。公告給的成績是：在七個模型都有回報的最高推理設定 `xhigh` 之下，GPT-6 Astra 平均拿到可得分數的 66.7%，GPT-5.6 Sol 為 43.8% [(ref: results)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#results)。對醫療與研究工作流程而言，這則發布的意義不在哪個型號領先，而在它把「讀懂一張沒有被整理過的原始影像、並知道什麼時候不能下結論」這件事，變成一個有逐條評分標準、有信賴區間的可量測對象 —— 而這正是醫學影像判讀與臨床資料稽核最難自動檢查的那一段。

## 背景

公告自己說明了為什麼要另建題庫：日常的濕實驗室工作裡，充滿失敗的實驗、模糊的影像與互相矛盾的觀察，而既有評測是以「為了寫進論文而挑選過的圖表」為素材，會漏掉這種模糊性以及隨之而來的排錯過程 [(ref: main)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/)。因此 BioBasicsBench 改以科學家自己實驗產生的原始資料出題。

就本書庫追蹤的時間線而言，這一則落在 OpenAI 近一個月幾則「把模型放到實際任務上量測」的發布之後：2026-10-21 的全腦 Perturb-seq 圖譜重讀，是讓代理去分析一份已經整理好的公開資料集；2026-11-02 的 LifeVal 則把日常生活任務做成評測。BioBasicsBench 與前兩者的差別在素材的加工程度 —— 它要處理的是還沒有被清理、標註或畫成圖表的證據。公告結語也把這條線延伸到安全面，說追蹤這些能力同時有助於理解它們對 biosafety（生物安全）與 biosecurity（生物保安）的意涵 [(ref: outlook)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#building-toward-reliable-lab-assistance)。

## 題庫的組成（事實）

- **規模與領域** — 100 道題目，分布於五個例行濕實驗室領域：protein methods、imaging and cytometry、quantification and assays、nucleic acid methods、molecular cloning [(ref: inside)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#inside-biobasicsbench)。
- **題目要求** — 判讀原始實驗資料、辨識錯誤，以及辨認出證據不足以支撐某個結論。公告說明，誤讀一張影像或忽略對照組的問題，會讓科學家得到錯誤結論，並把時間花在回答不了原問題的實驗上。
- **難度範圍** — 從「讀出膠片上某段 DNA 的分子量」這種單純請求，到完整的 assay 分析；但公告強調全部都屬於濕實驗室科學家「應該能可靠完成」的例行工作。
- **輸入型態** — 公告以一張表列出每一類資料出現在幾道題目中：

| 資料型態 | 題數 | 公告列舉的內容 |
|---|---|---|
| Gels & blots | 31 | 瓊脂糖 DNA 膠、SDS-PAGE 膠、Western blot |
| Protocols, notes & specs | 27 | 實驗流程與標準作業程序、實驗記錄簿與執行紀錄、手寫筆記翻拍、型錄、儀器規格、已發表的方法 |
| Tables & instrument exports | 20 | CSV 與 Excel 匯出檔、泳道配置與庫存表、原始流式細胞術（FCS）檔 |
| Bench, apparatus & reagent photos | 18 | 實驗檯、電泳槽、試劑與培養管、一塊 PCR 盤、試管架、pH 試紙、濃縮管、冷凍櫃、液體處理工作台 |
| Microscopy | 14 | 原始明視野與螢光影像、多通道影像組、z-stack、縮時影片 |
| Instrument screens & plots | 13 | 流式細胞儀、顯微鏡、NanoDrop、盤式讀取儀與天平螢幕的翻拍；匯出的標準曲線、層析圖與圖表 |
| Sequencing files | 12 | 原始長讀長 FASTQ、FASTA 序列、GenBank 圖譜 |
| Protocol videos | 7 | 畫線接種、接菌、連續稀釋、SDS-PAGE 電泳槽與培養箱架設、天平秤重 |
| Agar plates & colonies | 7 | 轉形盤、藍白篩選盤、抗生素紙錠盤 |
| Reference sheets | 21 | 分子量標記對照表、質體圖譜、pH 對照表（輔助材料） |

公告在表下註明這些分類互相重疊，一道題可以含有好幾種資料，`Reference sheets` 屬輔助材料 [(ref: inside)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#inside-biobasicsbench)。本文代為加總前九類得 149，確實大於題數 100，與公告所述一致。

## 出題、審查與評分方式（事實）

- **出題** — 由科學家以自己實驗產生的資料出題，每題同時附一份專家撰寫的評分標準（grading rubric）。
- **三道審查** — 每題先經一位沒有參與出題的 Ligo 科學家內部審查，再經一位在濕實驗室工作、具博士學位的外部科學家審查，最後再做一次內部審查；審查者檢查題目敘述、實驗證據、評分標準、作者註記，以及一份已評分的模型作答。
- **作答形式** — 代理程式回傳結構化答案，內含被要求的結論、量測值或建議，必要時附支持推理。
- **評分方式** — 依評分標準逐條給分，因此能區分「結論正確」與「分析只對了一部分」。公告說明多數題目同時測好幾種能力，包括生物學知識、影像與其他資料的判讀、錯誤偵測與流程理解。
- **指標定義** — 成績以 mean reward 呈現，即平均每題得分佔該題可得分數的百分比；誤差範圍是 95% 信賴區間，以整題重抽樣計算，同一題的五次嘗試綁在一起 [(ref: results)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#results)。

## 七個模型的成績（事實）

公告評了七個模型：GPT-5.2、GPT-5.4、GPT-5.5、GPT-5.6 Sol、GPT-6.1 Sol、GPT-6 Luna、GPT-6 Astra，涵蓋 37 組「模型 × 推理強度」設定，每組設定對 100 道題各跑五次，合計 18,500 筆結果 [(ref: results)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#results)。本文代為驗算 37 × 100 × 5 = 18,500，與公告數字相符。

公告以表格給出 `xhigh` 設定下的成績：

| 模型 | 平均得分 | 95% 信賴區間 | 每題輸出 token |
|---|---|---|---|
| GPT-6 Astra | 66.7% | 60.3–73.1% | 4,704 |
| GPT-6.1 Sol | 62.0% | 55.6–68.4% | 5,238 |
| GPT-5.6 Sol | 43.8% | 37.6–50.0% | 9,099 |
| GPT-6 Luna | 38.3% | 32.3–44.5% | 13,120 |
| GPT-5.5 | 35.4% | 29.7–41.0% | 11,135 |
| GPT-5.4 | 33.2% | 28.3–38.4% | 13,717 |
| GPT-5.2 | 31.2% | 26.2–36.3% | 27,620 |

公告註明 `xhigh` 是七個模型都有回報的最高推理強度，每一列都含全部 100 題與每題五次嘗試；若某個模型另有更高的 max-effort 結果，只畫進上方的圖，不進這張表。

公告對這組數字的描述是：GPT-6 Astra 相對 GPT-5.6 Sol 有大幅改善，即使在低推理強度下亦然，並推測「更強的原生多模態能力」可能是日常濕實驗室判讀進步的關鍵。

本文代為比對同一張表的信賴區間，得到兩點公告沒有明說的事：GPT-6 Astra 的 60.3–73.1% 與 GPT-6.1 Sol 的 55.6–68.4% 大幅重疊，這兩列的先後不足以當成能力差距；而 GPT-6 Astra 與 GPT-5.6 Sol 的區間（60.3–73.1% 對 37.6–50.0%）則沒有重疊。另外，排名前兩位同時也是每題輸出 token 最少的兩個 —— GPT-6 Astra 的 4,704 約為 GPT-5.6 Sol 9,099 的一半，不到 GPT-5.2 的 27,620 的五分之一。

## 公告舉出的三個進步例（事實）

這一節的三個例子都是 GPT-6 Astra 相對 GPT-5.6 Sol 的改善 [(ref: improve)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#gpt-6-astra-improvements-from-gpt-56-sol)。

- **認出資料能說明與不能說明什麼** — 一題要判斷細胞死活。GPT-5.6 Sol 僅憑偵測死細胞用的染劑訊號就判定細胞已死；但該偵測器也會收到第二種染劑的光，兩個偵測窗在 525–540 nm 重疊（通道二為 SYTOX 標記的 470–540 nm，通道三為 FUN-1 green 的 525–580 nm），公告載明這個共用波段允許干擾、而干擾量未經量測，因此亮度本身不足以支撐該結論。GPT-6 Astra 指出這項模糊，並要求以更好的對照把兩個訊號分開。
- **多模態細節的辨識** — 一題要從 DNA 選殖實驗的照片下結論，而對照在這類實驗中是關鍵。GPT-5.6 Sol 看到陰性對照盤上沒有菌落，就以此為據下結論；GPT-6 Astra 注意到該盤管緣標籤寫的是 `LB Kan50`，指的是 kanamycin，與該實驗使用的 ampicillin 不是同一種抗生素，因而判定該盤不能當成可靠對照。
- **把實驗脈絡保持在腦中** — 一題給了一系列顯微影像，影像中的細胞時而清晰時而消失。GPT-5.6 Sol 去找細胞「消失」的生物學解釋；GPT-6 Astra 認出那是 z-stack，也就是在不同深度連續拍攝的影像序列。

## 公告舉出的三個失誤例（事實）

這一節的三個例子都仍發生在成績最高的 GPT-6 Astra 身上。公告在這一節開頭直接寫道：更高的評測分數還不代表模型能在實驗室裡做出可靠判斷 [(ref: shortfall)](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#where-models-still-fall-short)。

- **讓既有假設蓋過對照** — 一題是菌落 PCR 的結果判讀。GPT-6 Astra 能把菌落條帶分成兩群，卻假設「較大的 PCR 產物代表選殖成功」，據此提出第 4、6、7、8 泳道；參考答案依對照比對選的是第 5、9、10 泳道。公告說明視覺上的分群是對的，但兩群被賦予的實驗身分相對於參考答案是反的，照這個選法會純化到錯誤的質體。
- **排除與自己解釋相牴觸的資料** — 一題要描述細胞內液泡的外觀。GPT-6 Astra 結論是液泡普遍比周圍細胞暗，但同一張影像裡有些液泡看起來比較亮。公告說明兩種外觀都算數，因為改變顯微鏡對焦可以反轉對比，所以較暗的例子不足以成立通則。GPT-6 Astra 其實檢視過多個區域、也說過對比會隨對焦改變，最後卻只把較暗那一種寫進結論。
- **例行計數出錯** — 一題是菌落計數。GPT-6 Astra 的計數標記沒有可靠地對應到個別菌落：相鄰的菌落沒有分開、有可見菌落漏標、也有空白瓊脂被標成菌落；該盤的淨結果相對參考值高估約 12%。公告說明在鋪盤體積與稀釋倍數固定的前提下，菌落數高估會等比例放大 DNA 轉入細胞效率的估計值。

## 證據邊界（事實）

- **單一組織發布，共同開發方不是獨立驗證者** — 題庫組成、評分方式與全部分數都只出自 OpenAI 這一頁。Ligo 在全文出現三次，都是以共同開發方與出題／審查者的身分出現，頁面沒有指向 Ligo 的連結，也沒有它自己的對應聲明。
- **沒有人類基準** — 公告說題目都是濕實驗室科學家「應該能可靠完成」的工作，但沒有量測科學家在同一題庫上的得分。以頁面原始文字計數，全文 `baseline` 出現 0 次，`human` 只出現 1 次且是在「benefits all of humanity」這句使命宣言裡。外部因此無法判斷 66.7% 離「夠用」還有多遠，也無法據此設定任何驗收門檻。
- **題庫未見釋出** — 以同樣方式計數，全文 `release`、`download`、`GitHub`、`arXiv` 命中皆為 0，正文中的連結全部是頁內錨點或 OpenAI 自家分類頁。題目、評分標準與模型作答都沒有提供取得方式，外部無法複現這 18,500 筆結果。
- **頁面標為 Publication 但沒有論文** — 該頁的類型標示是 `Publication`，但全文 `paper` 只出現一次，而且是在描述既有評測以論文中的圖表為素材；沒有論文或技術報告連結，作者欄位寫的是 `OpenAI`，未具名任何研究者。
- **只評自家模型** — 七個受測模型全部是 OpenAI 自家型號，公告沒有納入任何其他供應商。這組數字可以看同一家公司的世代變化，不能當作跨廠商比較。
- **分領域成績未公布** — 公告說題目涵蓋五個領域，但只給全題庫的平均分，沒有給任一領域的分數，外部無法判斷弱項落在哪一類實驗。
- **12% 是單一盤的差距** — 菌落高估約 12% 是那一個示例盤相對參考值的結果，不是全題庫的統計量。
- **發布日期沒有結構化標記** — 該頁沒有 JSON-LD 結構化資料，也沒有 `article:published_time` 這類中繼標籤，頁內的 `<time>` 元素只屬於文末三張延伸閱讀卡片。本文的日期取自頁面可見文字與 OpenAI 新聞列表頁兩處互相佐證。
- **公告本身沒有任何臨床主張** — 以頁面原始文字計數，`clinical`、`medical`、`patient`、`FDA` 命中皆為 0。本文後段把這則發布接到醫療與研究工作流程，屬於本書庫的解讀，不是公告的主張。

## 本書庫解讀（評論）

這則發布值得看的地方不是分數，而是它把什麼變成了可量測的對象。過去一年大廠在科學領域的發布，多半是「代理程式串起既有工具、走完一條流程」的示範；BioBasicsBench 轉而去量一件更基礎、也更難的事 —— 在資料還沒有被清理、標註或畫成圖表之前，模型能不能從中讀出正確的事實，並且知道什麼時候證據不足以下結論。

對醫療影像與臨床資料的工作來說，這個轉向是直接相關的。公告舉的三個失誤，沒有一個是知識不足：第一個是讓既有假設蓋過對照組給出的證據，第二個是把與自己解釋相牴觸的觀察排除在結論之外，第三個是例行計數的視覺可靠度不足。這三類失效，恰好就是臨床判讀最難用後端指標稽核的型態 —— 結論看起來合理、推理過程讀起來通順，錯的是中間那一步對證據的取捨。把「要求更好的對照」與「說出證據不足」寫進評分標準，比只算一個準確率更接近醫療場域實際需要的稽核方式。

分數本身則要讀得保守。公告給了 95% 信賴區間，這在廠商自報的評測裡並不常見，值得肯定；但照這組區間看，排名前兩位之間的差距並沒有被區間分開，把 66.7% 與 62.0% 讀成能力排序會超出資料能支撐的範圍。真正穩的對照是跨世代那一組：GPT-6 Astra 與 GPT-5.6 Sol 的區間沒有重疊，而且前者用的每題輸出 token 約為後者的一半。對要把這類判讀放進長流程的單位來說，後面這件事比名次重要 —— 它意味著同一段工作的單位成本與延遲結構已經改變。

最關鍵的缺口是沒有人類基準。公告的題目設定是「濕實驗室科學家應該能可靠完成」，卻沒有量這些科學家實際能拿幾分。少了這條線，66.7% 既可能代表離可用很近，也可能代表離可用很遠，外部沒有辦法判斷。這與另一種常見的揭露問題同形：給了完整的評估框架卻不設數值切點，而這裡是給了數值卻沒有可對照的切點 —— 兩者對想設驗收門檻的採用方而言，結果一樣。

## 產業影響

評測的素材正在從「論文裡挑過的圖表」往「實驗台上的原始證據」移動。這個轉向如果持續，受影響的不只是模型排名，還有評測本身的生產方式：BioBasicsBench 的題目由合作企業的科學家用自己的實驗資料出題、由外部在職科學家審查，與近期幾家大廠「找領域夥伴共同建題庫」的做法是同一個形狀。它的好處是題目貼近真實工作，代價是題庫掌握在廠商與單一夥伴手上，外部無法複現，也無法確認題目難度的分布是否中性。

逐條評分標準這件事，對醫療器材與臨床 AI 的評估方法有參考價值。單一準確率無法分辨「結論對但理由錯」與「結論與理由都對」，而逐條給分可以 —— 這正是臨床稽核想要的資訊粒度。但在人類基準與題庫都未公開之前，這類廠商自建評測只能當成趨勢指標：它能說明同一供應商的世代變化，不足以支持採購決策或驗收條款。

另一個值得注意的訊號在結語：公告把「追蹤這些能力」同時說成理解 biosafety（生物安全）與 biosecurity（生物保安）意涵的一部分。同一組能力 —— 看懂原始實驗證據、判斷實驗哪裡出錯 —— 既是研究加速的來源，也是風險評估的對象，這一點在生命科學領域的模型治理討論中會愈來愈常出現。

## 與書庫其他文章的關係

兩則都是 OpenAI 把代理程式放進生物研究，但落在流程的兩端：該則讓代理去讀一份已發表的全腦 Perturb-seq 圖譜並產出假說，本則量的是代理能不能讀懂還沒整理成圖表的膠片、培養皿與儀器輸出；該則的 75% 有明確分母（20 組配對共 60 次判斷），本則的 66.7% 則沒有人類基準可對照: [一個代理讀一個基因：OpenAI 全腦擾動圖譜解讀拆解](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md)

兩則都在談代理程式進入實驗科學，揭露形式剛好相反：該則是一場沒有任何分數的示範流程，本則是一組有逐條評分標準與 95% 信賴區間、卻沒有人類基準的分數；合起來正好是「只有敘事」與「只有分數」的兩端: [代理程式串起既有化學工具：DeepMind 藥物設計 Skills 解剖](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md)

同一家公司對同一個型號的兩種揭露方式：該則記錄 GPT-6.1 Sol 發布時除 Terminal-Bench Science 的 68.1% 之外不公布任何絕對分數，本則把同一個型號放進 BioBasicsBench，給了 62.0% 與 55.6–68.4% 的 95% 信賴區間，並與其餘六個自家型號並列: [價格只要五分之一，但科學能力沒跟上：GPT-6.1 Sol 解剖](2026-10-07-openai-gpt-6-1-sol-launch.md)

## 實務的啟發

- **把「說出證據不足」寫進自家的評估表** — 本則最值得借用的不是題目，而是評分標準的設計：除了結論與數值，另外給「辨認出證據不支持該結論」的分數。單位若在評估醫學影像或檢驗資料的輔助判讀工具，可以在既有的準確率之外，另設一組「應該拒答而確實拒答」的題目，否則一個從不說不知道的模型在一般指標上會看起來更好。
- **要求供應商提供人類基準，而不是只要分數** — 本則的 66.7% 沒有可對照的人類成績，外部無法設門檻。採購或試用時的具體作法是：請供應商提供同一題組上由具資格人員作答的分數分布，若無，就以本單位自己的少量題組補做，再把兩者並列，不要直接拿廠商分數當驗收值。
- **評估長流程成本時把每題 token 一起看** — 本則表中排名前兩位同時也是每題輸出 token 最少的兩個，而最舊的型號用掉約六倍的 token 卻只拿到約一半的分數。若要把判讀步驟放進多步驟流程，建議以「每題 token × 題數」估算實際支出，而不是只比單價或只比分數。
- **內部驗證題庫用自己的失敗資料來出** — 本則的題目是科學家拿自己實驗的原始資料出的，包含失敗的實驗與模糊的影像。單位要建自己的小型驗證集時，比起挑選過的典型案例，更該刻意納入影像品質不佳、對照有問題、與結果互相矛盾的那些紀錄，因為那才是實際工作中模型最容易出錯的地方。

## 後續追蹤

- BioBasicsBench 的題目、評分標準與模型作答是否會釋出，使 18,500 筆結果可被外部複現。
- 是否會補上人類基準 —— 濕實驗室科學家在同一題庫上的得分分布，是判斷 66.7% 意義的前提。
- 五個領域（protein methods、imaging and cytometry、quantification and assays、nucleic acid methods、molecular cloning）是否會各自公布分數。
- 是否會有其他供應商的模型被放進同一題庫，或由第三方以同一題組量測跨廠商成績。
- 該頁標示為 `Publication` 卻無論文連結，後續是否會有技術報告或論文說明出題與評分方法。
- Ligo 是否會發布自己的說明，使這則從單一組織來源變成可交叉驗證。
- 醫學影像與檢驗領域是否會出現同形的題庫 —— 以未經整理的原始影像與儀器輸出出題、以逐條評分標準給分，並附上人類判讀者的基準。

## References

- `main` — Measuring how AI agents handle everyday wet-lab science（OpenAI 官方公告，2026-11-06，含題庫介紹、成績、六個案例與結語；作者欄位為 OpenAI，分類標示為 Publication 與 Life Sciences）  
  <https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/>
- `inside` — Inside BioBasicsBench（同一公告的題庫組成一節，含五個領域、輸入資料型態表與出題／審查／評分流程）  
  <https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#inside-biobasicsbench>
- `results` — Results（同一公告的成績一節，含七個模型、37 組設定、18,500 筆結果與 `xhigh` 成績表）  
  <https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#results>
- `improve` — GPT-6 Astra improvements from GPT-5.6 Sol（同一公告的進步案例一節，含染劑偵測窗重疊、抗生素標籤與 z-stack 三例）  
  <https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#gpt-6-astra-improvements-from-gpt-56-sol>
- `shortfall` — Where models still fall short（同一公告的失誤案例一節，含泳道選擇、液泡對比與菌落計數三例）  
  <https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#where-models-still-fall-short>
- `outlook` — Building toward reliable lab assistance（同一公告的結語一節，含對 biosafety 與 biosecurity 的敘述）  
  <https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/#building-toward-reliable-lab-assistance>

[Home](../) · [Industry Watch](./)
