---
parent: Industry Watch
nav_order: 3
title: "分子讀得準、化合物選不準：OpenAI MedChemBench 解析"
category: industry-watch
date: 2026-11-24
tags: [OpenAI, MedChemBench, medicinal-chemistry, drug-discovery, benchmark, multimodal, SMILES, RDKit, SAR, ADME, PRMT5, RAS-ON, GPT-6-Astra, GPT-6.2-Astra, rubric, LLM-as-judge, research-workflow]
catalog_id: "openai:medchembench-2026-11-20"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.2"
source:
  orgs:
    - "OpenAI"
  event: "OpenAI 發布 MedChemBench，一套取自 117 篇已發表論文與專利的 99 題 medicinal chemistry 回溯式多模態評測，並公布十一個 GPT 型號在四個給分成分上的成績"
  event_date: "2026-11-20"
  official_url: "https://openai.com/index/introducing-medchembench/"
  single_source: false
  single_org: true
related_articles:
  - path: "2026-11-16-openai-biobasicsbench-wet-lab-agents.md"
    relation: "同一家公司四天前後發布的兩套自家科學評測，揭露程度相反：該則的題目與評分細節只有公告一頁，本則另附了一份署名論文，使成績的分母、信賴區間與評分方式可逐項回查"
  - path: "2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md"
    relation: "該則示範的是代理程式串接既有化學工具、可反覆計算與改寫提案，本則的受測條件剛好是它的反面——單回合、無工具、無回饋，而本則論文把代理式軌道列為未來工作"
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "兩則都把藥物開發當成前沿模型的主戰場，但量的東西不同：該則數的是六個合作組織實際做出的成果，本則量的是模型在已完成的歷史藥物專案上答得多像"
refs:
  mcb:
    title: "Can AI help scientists identify promising drug candidates?（OpenAI 官方公告，2026-11-20）"
    url: "https://openai.com/index/introducing-medchembench/"
  paper:
    title: "MedChemBench: Evaluating complex multimodal reasoning in medicinal chemistry（OpenAI 官方論文 PDF，署期 2026-11-09）"
    url: "https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf"
---

[Home](../) · [Industry Watch](./)

# 分子讀得準、化合物選不準：OpenAI MedChemBench 解析

## 來源

- 組織／產品：OpenAI — MedChemBench（簡稱 MCB），一套針對 medicinal chemistry（藥物化學）推理能力的回溯式多模態評測。
- 事件：公布評測設計與十一個 GPT 型號的成績，並同步釋出一份署名論文。
- 日期：2026-11-20（公告頁標題下方可見文字為 `November 20, 2026`；該頁無 JSON-LD、無 `article:published_time`，頁內三個 `<time>` 元素全屬文末 Keep reading 卡片，故另以 openai.com 新聞列表頁標示的同一日期互為佐證，未推斷）
- 官方入口：[Can AI help scientists identify promising drug candidates?](https://openai.com/index/introducing-medchembench/)
- 官方論文：[MedChemBench: Evaluating complex multimodal reasoning in medicinal chemistry](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)（Jeremy Li、Andrew Ho、Suyash Shringarpure、Amelia Liu、Paul Humphries、Joy Jiao，單位皆為 OpenAI，署期 2026-11-09）。本文凡涉及題目組成、給分權重、分母與信賴區間者一律以這份論文原文為準。
- **評測與受測者同屬一個組織**：題庫由 OpenAI 建置、受測型號全為 GPT 家族、評分用的 judge（擔任評審的模型）亦為 GPT 型號，無獨立第三方複現，亦未納入其他廠商的模型。相關限定條件集中列在後段的證據邊界一節。

**編輯：** Clarence

OpenAI 發布 MedChemBench，把「AI 能不能幫忙做藥」這個問題改寫成一個可打分的形式：從 117 篇近期論文與專利裡抽出 99 道題，每道題給模型一段研究敘事、一批化合物的結構圖與既有實驗數據，然後要它做出一個藥物化學專案真的會遇到的決定——哪一顆化合物值得往下推、某個取代基換上去會讓活性往哪邊走、這三顆的細胞效價與代謝速率各是多少 [(ref: mcb)](https://openai.com/index/introducing-medchembench/)。成績的形狀比總分更值得看：最強的型號把分子結構讀成正確的 isomeric SMILES（帶立體化學資訊的分子字串表示法）這一項拿到 95.37%，但在「挑哪一顆」與「估多少」這兩項只有 50.42% 與 47.02% [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)。

## 背景

- **2026-11-09** — 論文 `MedChemBench: Evaluating complex multimodal reasoning in medicinal chemistry` 的署期。論文裡受測的是十一個型號，最高分為 GPT-6 Astra 在 max effort（推理強度設定的最高一檔）的 83.83%。
- **2026-11-20（本則事件）** — 公告頁上線，標題為提問句 `Can AI help scientists identify promising drug candidates?`，內文並列了論文裡沒有的一筆成績：GPT-6.2 Astra 在 xhigh 設定下的 84.5%。
- **本則與臨床無關的界線由論文自己畫出** — 論文寫明題目涵蓋 preclinical drug discovery（臨床前藥物探索），`clinical development is outside the benchmark's scope`。本則不含任何醫療器材法規狀態或臨床驗證的宣稱。

本則無配圖。公告頁與論文中的分子結構圖、效能散佈圖為 OpenAI 自有素材，不重製；本文可核對的數值已以文字與表格完整呈現。

## 這套評測在考什麼（事實）

每一題的輸入是文字與影像交錯的一包證據 [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)：

- 生物背景與治療目標、起始化合物或化學系列，以及一個促使團隊繼續改良的限制。
- 相關類似物的生化、細胞、ADME（吸收、分布、代謝、排泄）、藥物動力學、安全性或結構證據，形式包含分子結構圖、assay（檢定）結果表、圖表與 protein-ligand（蛋白質—配體）結合姿態圖。
- 最後是一個要模型做出的專案決定。

每一次作答都是單回合、不給工具、不給回饋、也不能追加實驗 [(ref: mcb)](https://openai.com/index/introducing-medchembench/#where-we-go-from-here)，輸出須為指定格式的 JSON；每個 model-effort 條件在每題保留十次作答 [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)。

## 七類題目與科學領域涵蓋（事實）

99 題依主要的實務問題分成七類，論文 Figure 1 標出各類題數（整數相加恰為 99，由本文代為計算）[(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)：

| 題類 | 題數 |
|---|---|
| Integrated lead selection（整合式先導化合物選擇） | 48 |
| SAR forecasting（structure-activity relationship，結構—活性關係預測） | 26 |
| ADME & delivery | 8 |
| Molecular design & enumeration | 6 |
| Safety & liabilities | 4 |
| Retrosynthesis（逆合成分析） | 4 |
| Assay biology & mechanism | 3 |

另依科學內容標註領域，同一題可屬多個領域，論文載明 99 題中有 85 題跨一個以上領域：potency and selectivity 75／99、ADME and exposure 54／99、structure-guided reasoning 51／99、cellular and translational pharmacology 39／99、molecular design 37／99、safety and liabilities 11／99、synthesis 5／99 [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)。

## 四個成分與給分權重（事實）

答案被拆成四個成分計分，每題總分正規化為 1、各題等權 [(ref: mcb)](https://openai.com/index/introducing-medchembench/#what-medchembench-grades)。論文給出這四個成分在 99 題上的平均分數佔比 [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)：

| 成分 | 平均佔可得分數 | 評分方式 | 適用題數 |
|---|---|---|---|
| Molecular structure（分子結構） | 37.49% | 以開源化學資訊學函式庫 RDKit 轉成 canonical isomeric SMILES 後與參考答案逐字比對，完全相同才給分，錯誤、無效或缺漏一律零分 | 92 |
| Scientific rationale（科學理據） | 35.78% | 由一個 medium reasoning effort 的 GPT-6 Astra judge 評分 | 91 |
| Ranking and candidate selection（排序與候選選擇） | 17.51% | 是否依題目列出的限制條件排序或選出化合物 | 86 |
| Numerical and categorical prediction（數值與類別預測） | 8.92% | 與來源文獻所報的量測值、計算值或類別標籤比對，數值依接近程度給部分分數 | 21 |

其餘 0.30% 為 technical checks（技術性檢查）。前兩項合計 73.27%、後兩項合計 26.43%（兩個合計值由本文代為計算）。適用題數取自論文 Figure 2 的 C–F 面板說明，該說明依序對應上表四列。

## 十一個型號的成績（事實）

論文評測的十一個型號為 GPT-5.2、GPT-5.4、GPT-5.5、GPT-5.6 Luna、GPT-5.6 Terra、GPT-5.6 Sol、GPT-6 Luna、GPT-6 Sol、GPT-6 Astra、GPT-6.1 Sol、GPT-6.1 Terra。每個型號跑遍當時可用的 reasoning effort 設定，共 61 個 model-effort 條件，每個條件在每題保留十次作答，合計 60,390 筆已評分回應；區間為 95% bootstrap 區間（以整題重抽樣估計的 95% 區間） [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)。

| 設定 | 成績 |
|---|---|
| 全評測最高分 | GPT-6 Astra 在 max effort 的 83.83%（81.27–86.20%），平均每次作答 22.9k 輸出 token |
| xhigh（十一個型號共有的最高設定）上界 | GPT-6 Astra 83.33%（80.71–85.71%），平均 14k 輸出 token |
| xhigh 下界 | GPT-6 Luna 35.02%（31.64–38.53%） |
| 其餘 max effort 成績 | GPT-6.1 Sol 82.89%、GPT-6.1 Terra 77.56%、GPT-6 Sol 69.07%、GPT-6 Luna 40.10%、GPT-5.6 Sol 59.77% |
| 測試期算力的效果 | 十一個型號提高 reasoning effort 後的平均分數增幅落在 8.97 至 33.26 個百分點之間 |

成分層級的差距比總分大得多。在 xhigh 設定下，分子結構一項的全距最寬：GPT-6 Astra 95.37%、GPT-6.1 Sol 93.70%、GPT-6.1 Terra 92.18%、GPT-6 Sol 65.85%、GPT-5.6 Sol 47.31%、GPT-5.5 28.70%、GPT-6 Luna 12.42%，其餘四個型號落在 8.74 至 17.00% 之間。另外三項在十一個型號間的全距則窄得多：科學理據 50.94–91.05%、排序與候選選擇 43.58–52.78%、數值預測 37.69–47.02%。GPT-6 Astra 在這三項的對應值為 91.05%、50.42%、47.02% [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)。

公告頁換算成一位小數後引用了其中幾筆，並加上論文沒有的一筆：xhigh 設定下 GPT-6.2 Astra 84.5%、GPT-6 Astra 83.3%、GPT-6.1 Sol 82.0%、GPT-6.1 Terra 75.1%、GPT-5.6 Sol 58.2%；max effort 的 83.8%；分子結構成分的 95.4% [(ref: mcb)](https://openai.com/index/introducing-medchembench/#medchembench-overall)。

## 被挑出來示範的兩道題（事實）

- **PRMT5 抑制劑的多性質預測** — 題目給三顆相關化合物的結構與先前實驗結果，要模型同時預測它們在細胞中抑制 PRMT5 所需的濃度、穿過細胞屏障的難易，以及在肝酵素 assay 中被分解的速度。被扣住不給模型看的後續實驗顯示了一個取捨：compound 23 在較低濃度就能抑制細胞中的 PRMT5，compound 24 則更容易穿過細胞屏障、在肝酵素 assay 中分解得更慢。提示中已經給過的量測值也必須照樣答對 [(ref: mcb)](https://openai.com/index/introducing-medchembench/#prediction-across-competing-properties)。
- **18 個原子的大環重建** — 題目取自導出 daraxonrasib 的那個研究專案，要模型把兩組取代基接到一個 macrocyclic RAS(ON) inhibitor（大環 RAS(ON) 抑制劑）骨架上，並保住大環的酯鍵與醯胺鍵、piperazic 的 N–N 鍵、雜芳香環的接點位置與指定的立體化學。在 xhigh 設定下，GPT-6 Astra 十次作答全部重建出正確的分子圖與立體化學；GPT-5.6 Sol 與 GPT-5.6 Luna 十次全錯。論文載明 GPT-5.6 Sol 那份示例答案有 67 個重原子（正確為 60）、大環只有 15 個環原子（正確為 18），GPT-5.6 Luna 那份則回傳兩個互不相連的片段 [(ref: paper)](https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf)。

## 證據邊界（事實）

上列成績全部出自 OpenAI 自建的題庫與自行執行的評測。下列限定條件集中列在這裡，供引用時一併帶上：

- **公告的頭條數字不在論文裡** — 公告以 GPT-6.2 Astra 的 84.5% 開場，但論文全文 `GPT-6.2` 命中為 0、`84.5` 命中為 0，其十一個型號在 xhigh 的上界是 83.33%、全評測最高是 max effort 的 83.83%。公告另一處把 xhigh 界定為「所有十一個型號共有的最高推理設定」，而 GPT-6.2 Astra 並不在那十一個之內。這一筆因此只有公告一個出處，分母、區間與 token 用量皆未公布；它與 GPT-6 Astra 的 83.3% 相差 1.2 個百分點（由本文代為計算）。
- **公告沒有提到 xhigh 的下界** — 公告列出的最低成績是 GPT-5.6 Sol 的 58.2%，論文的同一設定下界則是 GPT-6 Luna 的 35.02%。只讀公告會把型號間的實際落差看小。
- **科學理據由受測家族自己的型號評分** — 佔可得分數 35.78% 的科學理據一項，是由一個 medium reasoning effort 的 GPT-6 Astra judge 判定；GPT-6 Astra 同時是這份評測的最高分者。論文未提供人類藥物化學家與該 judge 的一致性數據。
- **題庫未見釋出** — 論文無 data availability 或 code availability 聲明，全文亦無 GitHub、repository 或 open-source 字樣；99 道題目、評分細則與 60,390 筆回應目前無法由外部取用或複現。
- **數值預測只在 21 題上量到** — 四個成分的適用題數為 92、91、86、21。被公告與論文同時點名為最弱的那一項，也是分母最小的那一項。
- **分數受比對方式左右** — 分子結構採 SMILES 逐字比對，不同但等價的畫法不給分；開放式的分子設計與合成題仍綁在參考答案上，論文自承這可能懲罰「不同但同樣合理」的設計，並把專家裁決列為後續工作。
- **污染未被排除** — 論文寫明 contamination 或 memorization 仍是潛在疑慮，明確來源識別碼帶來的平均效益很小，但「不足以排除訓練資料曾接觸過這些來源」。題目全部取自已發表的論文與專利。
- **接近飽和** — 論文自述這套評測在目前形式下已接近飽和，GPT-6 Astra 在 max effort 達 83.83%，未來版本必須加難才能繼續區分型號。
- **兩個型號在影像編碼修正前受測** — 論文載明 GPT-6 Sol 與 GPT-6 Luna 是在供應商 2026 年 9 月的影像編碼修正之前評測的，該修正對這兩個型號成績的影響未被量測。
- **公告的圖表範圍與論文不同** — 公告 Figure 2 的說明寫「GPT-5.6 以後的九個型號、51 個組合」，論文則是十一個型號、61 個 model-effort 條件；兩者差 10 個條件（由本文代為計算），對應被排除在該圖之外的 GPT-5.2 與 GPT-5.4。
- **回溯式設計的意義界線由論文自己寫明** — 數值預測類的題目量的是「與單一歷史案例在該案條件下的吻合程度」，公告亦寫明這些結果並不足以判定模型能不能發現新藥或改善實驗室決策。

## 本書庫解讀（評論）

- **這則發布真正的資訊不在總分，而在成分的權重表** — 83% 到 84% 這個數量級很容易被讀成「藥物化學已經做掉八成」。但把權重表攤開來看，分子結構與科學理據合計佔可得分數的 73.27%，而真正帶有決策形狀的那兩項——選哪一顆、估多少——合計只有 26.43%，而且最強的型號在這兩項各只拿到 50.42% 與 47.02%。換句話說，這個總分主要是在獎勵「把圖讀成分子、把理由講清楚」，而不是「做對決定」。願意把這張權重表印出來，是這份論文比多數廠商評測可信的地方；但引用它的人有義務一起帶上。
- **分子結構那一項的全距，量到的是一個會靜默出錯的能力** — 同一個 xhigh 設定下，分子結構分數從 12.42% 到 95.37%，是四個成分裡落差最大的。15 個環原子冒充 18 個環原子、67 個重原子冒充 60 個，這類錯誤不會回傳任何錯誤訊息，後面所有推理都會建立在一個根本不存在的分子上。對任何想把模型接進化學流程的人來說，這一項的意義不是「誰分數高」，而是「低分型號的輸出在結構層就不可信，而且看不出來」。
- **judge 與受測者同家族，是這份評測最該被獨立複製的一環** — 科學理據佔三分之一強的分數，判定者是 GPT-6 Astra，而 GPT-6 Astra 正是榜首。這不必然意味著偏誤，但在沒有人類藥物化學家一致性數據的情況下，外部無法區分「Astra 的理由寫得好」與「Astra 的理由寫得像 Astra 會接受的樣子」。分子結構那一項可以機械驗證，對錯沒有爭議；科學理據這一項則只能建立在對評審的信任上，兩者的可信程度不應被同一個總分混在一起。
- **接回醫療與研究工作流程：成分拆解這件事本身就可以照抄** — 本庫關注的醫學影像與報告生成，長期被同一個問題困住：一個總分同時混進了「看懂影像」「寫得像報告」「下對判斷」三種能力，分數上去了也說不出是哪一種上去。MedChemBench 的作法給了一個可直接移植的範例——先把答案拆成可機械驗證的部分（結構、數值）與只能由評審判定的部分（理據），公布各自的權重與適用題數，再分開報成績。對正在建立胸部 X 光報告評估的團隊而言，等價的拆法是把「病灶位置與側別是否正確」「量測值是否落在容許範圍」與「敘述是否符合臨床慣例」分開計分並公布權重；不這樣做，就會重現本則的情形：總分看起來很高，但真正要用的那一項只有一半。
- **單回合無工具的數字該當下限讀，不是上限** — 論文自己把代理式軌道（可檢索資料、可計算分子性質、可驗證結構、可多步修改提案）列為未來工作。這意味著目前這批數字量的是「模型腦中記得與推得出來的部分」，而實際部署時模型手上會有 RDKit、資料庫與同事。本庫的判讀是：選化合物那 50.42% 不應被當成「代理化學助手的能力天花板」，但分子結構那 95.37% 也不應被當成「結構處理已經解決」——單回合答對，和在長流程裡每一步都不出錯，是兩件事。

## 產業影響

- **自家評測的揭露標準被往上推了一格** — 這一輪同時給出署名論文、完整型號清單、61 個條件的分母、95% bootstrap 區間與給分權重表，比只在公告頁列幾個百分比的作法細得多。往後買方要求供應商補上「權重表與適用題數」時，手上多了一個同業已經做到的先例。
- **題庫不釋出，仍把這類數字鎖在供應商那一側** — 沒有公開題目與評分細則，外部就只能複述分數、無法複現，也無法把其他廠商的模型放上同一把尺。這與本庫近月追蹤到的其他發布一致：方法揭露愈來愈細，但可供第三方執行的那一份始終缺席。
- **藥物化學被明確劃進「模型可協助」的清單，臨床開發則被劃出去** — 論文把範圍限定在臨床前，並把臨床開發寫成界外。對製藥與生技買方而言，這等於供應商自己給出了一條採購邊界：這類模型目前被定位為先導化合物階段的推理助手，不是臨床決策工具。
- **評測接近飽和，下一輪會往代理式與前瞻式走** — 論文列出的後續方向是原始機器可讀 assay 資料、互動式三維結構、以及可檢索與可反覆修改的代理式軌道。這預告了下一代科學評測的形狀：從「單題答對率」轉向「多步流程裡的可靠度」。

## 與書庫其他文章的關係

同一家公司四天前後發布的兩套自家科學評測，揭露程度相反：該則的題目與評分細節只有公告一頁，本則另附了一份署名論文，使成績的分母、信賴區間與評分方式可逐項回查: [例行實驗判讀只拿 66.7%：OpenAI BioBasicsBench 拆解](2026-11-16-openai-biobasicsbench-wet-lab-agents.md)

該則示範的是代理程式串接既有化學工具、可反覆計算與改寫提案，本則的受測條件剛好是它的反面——單回合、無工具、無回饋，而本則論文把代理式軌道列為未來工作: [代理程式串起既有化學工具：DeepMind 藥物設計 Skills 解剖](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md)

兩則都把藥物開發當成前沿模型的主戰場，但量的東西不同：該則數的是六個合作組織實際做出的成果，本則量的是模型在已完成的歷史藥物專案上答得多像: [藥物開發端的第一批成果：Anthropic 六個合作組織大公開](2026-10-28-anthropic-drug-development-case-studies.md)

## 實務的啟發

- **比較任何評測分數之前，先問權重表與適用題數** — 本則顯示同一個總分底下，兩個成分佔七成三、另兩個佔二成六，而強弱恰好相反。採購或技術評估時建議把「每個成分佔總分多少、在幾題上量到、由誰評分」列為必填欄位；缺任何一項，兩家的分數都不可比。
- **把「讀得懂」與「做得對」拆成兩個指標再驗收** — 建議在自家評估裡至少分出可機械驗證的一軸（結構、數值、位置、側別）與需要評審判定的一軸（理據、敘述），分開報分。只報一個合併分數，等於把最弱的那一項藏在最強的那一項後面。
- **用模型當評審時，一併量人類一致性** — 若評估流程裡有 LLM-as-judge（以大型語言模型擔任評審），建議抽一個子集由領域專家重評，公布兩者的一致性；否則榜首與評審同家族時，外部無從判斷分數的來源。
- **針對「靜默錯誤」設一道前置檢查** — 分子結構那一項的教訓可以直接移植：在任何以模型輸出為輸入的流程前，先加一道結構或格式的機械驗證（化學用 RDKit 解析與正規化比對，影像報告用病灶位置、側別與量測單位的規則檢查），不通過就不要往下跑。
- **引用回溯式評測時寫明它量的是什麼** — 本則的數值預測量的是與單一歷史案例的吻合程度，不是預測新化合物的能力。內部報告若要引用，建議連同「回溯、單回合、無工具、題目取自已發表文獻」一起寫，避免讀者把它讀成前瞻性能力。

## 後續追蹤

- 99 道題目、評分細則與逐筆回應是否會公開，使外部得以複現並納入其他廠商的模型。
- GPT-6.2 Astra 的 84.5% 是否會以同樣的分母、區間與 token 用量進入更新版論文。
- 論文預告的代理式軌道是否實作，以及可檢索與可計算之後，選化合物與數值預測兩項會上升多少。
- 科學理據一項是否補上人類藥物化學家與 GPT judge 的一致性數據。
- 這套評測是否如論文所述加難，以及加難後型號間的全距變化。
- 製藥與生技端是否出現以這類成分化權重表為格式的採購規格。

## References

- `mcb` — Can AI help scientists identify promising drug candidates?（OpenAI 官方公告，2026-11-20，含評測定位、四個成分、PRMT5 與大環重建兩道示範題、公告版成績與作者自述的限制）  
  <https://openai.com/index/introducing-medchembench/>  
  深鏈：[評分成分](https://openai.com/index/introducing-medchembench/#what-medchembench-grades)、[多性質預測示範](https://openai.com/index/introducing-medchembench/#prediction-across-competing-properties)、[結構重建示範](https://openai.com/index/introducing-medchembench/#testing-spatial-reasoning-in-medicinal-chemistry)、[整體成績圖](https://openai.com/index/introducing-medchembench/#medchembench-overall)、[後續方向](https://openai.com/index/introducing-medchembench/#where-we-go-from-here)
- `paper` — MedChemBench: Evaluating complex multimodal reasoning in medicinal chemistry（OpenAI 官方論文 PDF，署期 2026-11-09，含七類題數、科學領域涵蓋、給分權重、十一個型號與 61 個條件的完整成績表 S1、成分全距、評分規則與限制章節）  
  <https://cdn.openai.com/pdf/09c4ec60-a32e-4652-837b-1811368a3bb0/medchembench-paper.pdf>

[Home](../) · [Industry Watch](./)
