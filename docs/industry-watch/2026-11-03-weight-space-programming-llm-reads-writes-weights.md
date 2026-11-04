---
parent: Industry Watch
nav_order: 1
title: "LLM 直接改權重，數學從 7.9% 到 48.1% —— 但它只是不再迴圈"
category: industry-watch
date: 2026-11-03
updated: 2026-11-03
tags: [MIT-CSAIL, weight-space-programming, GPT-6-Astra, mechanistic-interpretability, model-editing, Qwen3.5, Gemma-3, MATH-500, IFEval, sycophancy, reasoning-loops, gradient-free, research-blog]
catalog_id: "mit-csail:weight-space-programming-blog-2026-11-02"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.0"
source:
  orgs:
    - "MIT CSAIL"
  event: "研究部落格 Sparks of Weight-Space Programming: LLMs can natively read & write neural network weights 發布，並釋出全部實驗 logs"
  event_date: "2026-11-02"
  official_url: "https://rikiyat.github.io/blog/weight-space-programming/"
  single_source: true
related_articles:
  - path: "2026-10-07-openai-gpt-6-1-sol-launch.md"
    relation: "兩則談的是同一個模型 GPT-6 Astra，揭露姿態卻完全相反：該則記錄 OpenAI 自家公告除了 Terminal-Bench Science 的 68.1% 之外不公布任何絕對分數，外部無法設定門檻；本則是四位外部研究者把 Astra 的每一次輸入、輸出、推理摘要與評估腳本整包放上 GitHub，連失敗的那個實驗也留在裡面"
  - path: "../ai-papers/2026-10-05-clinical-concept-centers-llm.md"
    relation: "兩者對神經網路做的是同一類手術，而誰拿刀不同：該研究以 sparse autoencoder 解出 ICD 章節的概念方向並在 11 個開源模型上做因果介入，方向由既定演算法算出；本則的 Experiment 8 是讓一個通用語言模型自己讀權重、自己指認那條造成迴圈的方向，再從兩層 MLP 的各 64 個輸出欄位把它減掉"
  - path: "2026-09-17-fda-genai-devices-discussion-paper.md"
    relation: "該則整理 FDA 對生成式 AI 醫材提出的監管問題，其中一項是上市後變更要如何追溯；本則示範的修改方式剛好把那個問題推到極端 —— 改動 0.016% 的權重、沒有訓練迴圈、沒有資料集、沒有梯度，傳統上用來證明一次變更做了什麼的那些紀錄全都不存在"
refs:
  post:
    title: "Takehi R., Teoh J., Zhang A., Khattab O., Sparks of Weight-Space Programming: LLMs can natively read & write neural network weights（官方部落格，2026-11-02）"
    url: "https://rikiyat.github.io/blog/weight-space-programming/"
  logs:
    title: "RikiyaT/lm_understand-logs（作者釋出的全部實驗 logs，GitHub）"
    url: "https://github.com/RikiyaT/lm_understand-logs"
  hfmodel:
    title: "RikiyaT/Qwen3.5-0.8B-weight-space-programming（Experiment 8 編輯後模型，Hugging Face，Apache-2.0）"
    url: "https://huggingface.co/RikiyaT/Qwen3.5-0.8B-weight-space-programming"
---

[Home](../) · [Industry Watch](./)

# LLM 直接改權重，數學從 7.9% 到 48.1% —— 但它只是不再迴圈

## 來源

- 組織：MIT CSAIL（Rikiya Takehi*、Jayden Teoh*、Alex Zhang、Omar Khattab；`*` 為並列第一作者，標記依原頁）
- 事件：研究部落格 `Sparks of Weight-Space Programming: LLMs can natively read & write neural network weights` 發布，同時釋出全部實驗 logs
- 日期：2026-11-02（頁面可見文字 `November 2, 2026`；`citation_publication_date` 為 `2026/11/02`，`article:published_time` 為 `2026-11-02T00:00:00-08:00`，JSON-LD 型別為 `BlogPosting`）
- 官方入口：[rikiyat.github.io/blog/weight-space-programming](https://rikiyat.github.io/blog/weight-space-programming/)
- **單源，待交叉驗證**：這是作者自建站的部落格文章，**沒有 arXiv 編號、沒有 DOI、未經同儕審查**。所有數值由作者自行量測與報告，本文沒有第二個獨立來源可比對。作者釋出了完整 logs 與編輯後模型（見 `## References`），這讓宣稱**可被重現**，但重現尚未由外部完成。

**編輯：** Clarence

四位 MIT CSAIL 研究者提出 **Weight-Space Programming**：讓一個通用的前沿語言模型（全文使用 GPT-6 Astra）直接讀寫神經網路的權重數值本身 —— 不透過最佳化器、不用梯度下降、不寫訓練迴圈，只以自然語言的目標敘述，把權重當成可閱讀也可改寫的對象。八個實驗分成三類：從權重讀出網路學到什麼、修好一個壞掉的網路、從零寫出一個網路。

這篇值得記錄的地方有兩面。一面是結果本身在方法上確實新：先前的做法要嘛由專門訓練過的模型來讀權重，要嘛仍由訓練來寫權重，而這裡是一個未經特化的通用模型直接做。另一面是這篇的**揭露方式**：作者把失敗的實驗、反例、以及一段「這個方法做不到什麼」的附帶實驗都留在正文裡，而這些內容**沒有**出現在 TL;DR。本文逐項對照標題句涵蓋到哪裡、哪一項不成立。

## 背景

- **既有做法** — 權重由最佳化（Adam、Muon 這類符號式最佳化器）寫出，或由專門訓練來生成權重的網路寫出，或由形式化程式編譯而來。
- **近幾年** — 以語言模型最佳化「文字產物」已成常態：提示詞、程式、harness、訓練碼與超參數。作者指出這類做法的既有理由是「文字產物沒有別的原則性爬山方式」，而權重有梯度，所以權重一直留在符號式演算法的範圍內。
- **2026-11-02** — 本文主張這條界線正在消失：推理驅動的最佳化開始進入可微分神經網路本身。
- **logs 釋出** — 作者釋出的 `RikiyaT/lm_understand-logs` 為公開 repo，最後一次 push 為 2026-10-29（早於本文發布日），內容依作者說明包含送給 Astra 的全部輸入、模型回覆與推理摘要、執行過的程式與其輸出、讀寫的網路，以及每個數字背後的評估。

這條脈絡與本則標題事件的因果在於：正因為過去「人不能手改權重」被當成前提，一個通用模型若真能手改權重，衝擊的不只是最佳化的效率，而是可解釋性與稽核這兩件事原本依賴的工作方式。本文的評論段會回到這一點。

本則無配圖。原文的圖表與互動元件為作者自有素材，不重製。

## 事實（可核對）

以下數值全部取自官方部落格頁面本身 [(ref: post)](https://rikiyat.github.io/blog/weight-space-programming/)，表格為頁面原始文字逐欄抄錄。

### 八個實驗與各自的條件

| # | 問題 | 工具／前向傳遞 | 結果（依作者報告） |
|---|---|---|---|
| 1 | 這個網路被訓練來玩哪個遊戲 | 無工具 | 四個網路全對；Breakout 一例信心 99% |
| 2 | 這個 diffusion 模型會生成什麼圖形 | 無工具、不得前向傳遞 | 全對；但畫成外框，實際模型生成的是實心圖形 |
| 3 | 這個語言模型是用哪種語言訓練的 | 可用 Python 分析權重，不得執行網路 | 三個模型兩次嘗試全對；copying head 的指認與實測完全相符 |
| 4 | 修好一個卡在局部最小值的控車網路 | 無工具，單次嘗試 | 1,024 回合全部成功，改動 171,664 個權重中的 6,073 個（3.5%） |
| 5 | 從零寫出三個 MinAtar 遊戲的策略網路 | 無資料、無梯度、無工具、不得試玩 | 見下表 |
| 6 | 從零寫出 150 萬參數的圍棋網路 | Python sandbox；前向傳遞 0 至 50 次 | 0 次時對兩個較小的 PPO 網路勝率過半；50 次時勝過同尺寸、以 2,000 萬局訓練的 PPO |
| 7 | 兩個模型哪一個被訓練成諂媚 | 僅權重 → 後放寬為可看注意力圖樣 | **只看權重：四次嘗試全部失敗**；可看注意力圖樣後三組全對 |
| 8 | 讓 Qwen3.5-0.8B 數學更好 | Python session；前向傳遞 10／25／50 次 | 見下表 |

### Experiment 3 的信心值偏低

| 訓練語言 | Astra 的答案與信心（兩次嘗試） | Astra 指認的 copying head | 實測 ground truth |
|---|---|---|---|
| Python | Python (0.56)、Python (0.52) | 2.1, 3.1, 3.5 | 2.1, 3.1, 3.5 |
| Romaji | romaji (0.55)、romaji (0.62) | 3.3 | 3.3 |
| English | English (0.58)、English (0.48) | 3.1 | 3.1 |

答案全對，copying head 的指認與實測逐一相符且沒有多報。但自報信心落在 0.48 至 0.62 之間，六次中有兩次低於 0.55。作者沒有說明這個信心值的校準狀況。

### Experiment 5：對 100M 步的 PPO 全勝，對 500M 步的 PPO 三戰一勝

| 遊戲 | PPO，1 億步 | PPO，5 億步 | Astra，一次生成 |
|---|---|---|---|
| Breakout | 15.8 | 25.3 | **517.4** |
| Seaquest | 5.6 | 88.9 | 53.1 |
| Asterix | 25.8 | 55.2 | 53.2 |

TL;DR 的句子是「outplay networks trained with PPO for 100 million steps」，對照上表三個遊戲都成立。但同一張表的第三欄顯示，面對訓練 5 億步的 PPO，Astra 只在 Breakout 勝出（約 20 倍），Seaquest 得分為其 60%、Asterix 略低。**作者在正文把這件事明白寫出來**（「come close in Asterix, and reach 60% of its score in Seaquest」），只是 TL;DR 選用的是 1 億步那個比較基準。

### Experiment 7：只看權重時失敗，這一點沒有進 TL;DR

作者微調兩份相同的 Gemma 3 270M，一份訓練成答對、一份訓練成諂媚（永遠順著使用者提示的答案回答），並**凍結輸入 embedding 與輸出層**，避免靠輸入輸出分布走捷徑。原文的結論是：

> 只憑權重，Astra 無法判斷。四次嘗試中，它都在權重空間找出兩個模型的許多差異，卻無法把這些差異對應到行為差異。

放寬條件、允許它查看兩個模型在它自己撰寫的文字上的注意力圖樣（但不得看輸出）之後，三組配對全部指認正確，並定位到中間層：head 10.2 在諂媚模型中對使用者提議答案的注意力為 85.7%，誠實模型為 0.75%。

這是全文唯一一個**行為層級**的稽核實驗，也是唯一需要放寬條件才成立的實驗。文章標題與 TL;DR 的主張是「原生讀寫權重」，而這一項在「只看權重」的設定下是負面結果。

### Experiment 8：數字跳升只發生在最後一個預算點，而中間那一欄往回走

| Qwen3.5-0.8B | MATH-500 (%) | GSM8K (%) | IFEval (%) | 命中 token 上限 (%) |
|---|---|---|---|---|
| base | 7.9 | 13.8 | 21.0 | 93.0 |
| 編輯後，10 次前向傳遞 | 12.3 | 25.7 | 49.0 | 87.2 |
| 編輯後，25 次前向傳遞 | 14.1 | 25.1 | **39.9** | 86.4 |
| 編輯後，50 次前向傳遞 | **48.1** | 67.1 | 62.3 | 33.1 |

三件可直接讀出來的事：

- **跳升集中在最後一個預算點。** MATH-500 在 10 次與 25 次只從 7.9 動到 12.3 與 14.1，到 50 次才跳到 48.1。
- **IFEval 不是單調的。** 25 次（39.9%）比 10 次（49.0%）低了 9.1 個百分點。TL;DR 寫的「raising IFEval by 3x」對應的是 base 21.0 到 50 次的 62.3，而相鄰預算點往反方向走。
- **最後一欄說明了機制。** 命中 32,768 token 上限的比例從 93.0% 降到 33.1%。原文指出 base 模型前 96 次練習作答中有 85 次跑到 token 上限，Astra 把迴圈追到第 15 與第 19 層 MLP 寫出的**同一條方向**，並從每層的 64 個輸出欄位減掉這條方向，合計 131,072 個權重，佔模型 0.016%。

作者沒有報告重複次數或區間；Qwen 這張表沒有說明每題取樣幾次（相對地，後述 Gemma 那張表明確寫了平均 4 次取樣）。

### 作者自己放進去的反例：Gemma 3 270M 改不動

這是全文最重要的限定，位置在 Experiment 8 之後的「Additional experiment」：

| Gemma 3 270M | MATH-500 (%) |
|---|---|
| base | 6.8 |
| 編輯後，5 次前向傳遞 | 7.0 |
| 編輯後，10 次前向傳遞 | 7.6 |
| 編輯後，25 次前向傳遞 | 7.7 |
| 編輯後，50 次前向傳遞 | 7.0 |

Gemma 3 270M 很少迴圈（只有 8.5% 的作答達到 token 上限，Qwen 是 93%），而在它身上 Astra 改不動：讀到的是一般的推理錯誤（算錯、無效的代數步驟），沒有單一元件可以關掉，所有編輯都沒有讓 MATH-500 移動超過約一個百分點，連 Astra 自己都把這個幅度報成未確立。原文的結論句是：

> 編輯權重可以移除一個遮住能力的障礙，但無法加上模型本來沒有的能力。

換句話說，Experiment 8 那個 7.9% → 48.1% 的跳升，依作者自己的解釋是**讓模型把它本來就算得出來的題目做完**，不是讓它變得更會算。

### 可重現性：logs 與模型都查得到

- `RikiyaT/lm_understand-logs` 為公開 repo，最後 push 時間 2026-10-29，約 138 MB [(ref: logs)](https://github.com/RikiyaT/lm_understand-logs)。授權在 GitHub 的中繼資料中顯示為 `NOASSERTION`（即未被自動識別為標準授權條款）。
- Experiment 8 的編輯後模型公開於 Hugging Face，授權標示 Apache-2.0 [(ref: hfmodel)](https://huggingface.co/RikiyaT/Qwen3.5-0.8B-weight-space-programming)。作者致謝 Hugging Face 的 Ahsen Khaliq 依這些 logs 重建模型、重跑評估並做了線上示範 —— 依原文敘述，這是本文數值目前唯一一次外部重跑。

## 本書庫解讀（評論）

- **這篇的揭露品質高於它的標題。** 本書庫近期處理的多數案例，缺陷形態是標題句的涵蓋範圍大於正文能支撐的範圍，而限定條件被移到註腳或另一個頁面。這一篇的限定條件**全部留在正文**：對 5 億步 PPO 的兩場敗仗寫在表格旁邊，只看權重失敗的那段用的是「Unfortunately」，改不動 Gemma 的附帶實驗還額外寫了一句方法論上的否定結論。要挑剔的是 TL;DR 與標題：`natively read & write` 這個說法，在唯一一個行為層級的稽核任務上並不成立，而讀者多半只會讀 TL;DR。
- **「移除障礙」與「增加能力」的區分，是這篇真正的發現。** 把 Qwen 那 40 個百分點當成「LLM 能把模型改強」會讀錯。兩張表併看的結論很清楚：改得動的是 93% 作答跑到 token 上限的 Qwen，改不動的是只有 8.5% 達上限的 Gemma。這個方法目前的作用域，是**有單一元件可歸因的失效模式**，不是一般意義上的能力提升。作者把這一點寫成明文，值得記上一筆。
- **可稽核性的方向是雙向的，而本篇的證據偏向其中一邊。** 作者在展望裡提的第一項是 auditing without evaluation —— 不必跑推論就從權重發現後門或隱藏能力。但本文唯一真的去做行為稽核的 Experiment 7，恰恰是在「不跑模型」的條件下失敗的。目前已證成的是「從權重讀出**訓練任務**」（遊戲、圖形、語言），尚未證成的是「從權重讀出**行為傾向**」。這兩者在稽核上的價值差距很大。
- **對醫療 AI 的意義，集中在失效模式的移除而不是能力的取得。** 把上面那條界線搬到臨床場景：一個部署中的醫療語言模型若出現**有單一元件可歸因**的失效 —— 例如推理迴圈導致報告產不完、或諂媚傾向導致模型順著醫師提示的診斷走 —— 這類方法提供的是一條不必重新訓練、不必再動到病人資料的修補路徑，而且因為只改 0.016% 的權重，可以避開微調常見的災難性遺忘。但若要讓模型在某個科別「變得更準」，Gemma 那組數字就是現成的反證。順帶一提，Experiment 7 訓練出來的那個諂媚行為，在臨床上正是受關注的安全議題之一（模型順著使用者提出的答案走），而本篇的結果是：**光看權重偵測不到它**。
- **稽核與變更管理之間出現了一個新的空隙。** 一次權重編輯沒有訓練迴圈、沒有資料集、沒有梯度紀錄。傳統上用來描述一次模型變更做了什麼的那組文件 —— 訓練資料、超參數、訓練曲線 —— 在這種修改方式下全部不存在，留下的只有一段自然語言理由與一組改動過的張量。這對任何需要追溯變更的場域都是實際問題，不只醫材。

## 產業／生態影響

- **前沿模型的評估對象多了一類。** 過去衡量前沿模型多看程式、數學、agentic 任務。「讀寫權重」是一個全新的能力維度，而作者已經說明正在建立對應的 benchmark 與 harness。若這類評測成形，模型供應商之間會多一個可比較的軸，而這個軸與可解釋性研究直接相關。
- **可解釋性工具鏈可能被通用模型部分取代。** 本文 Experiment 3 的 copying head 指認，用的是 Elhage 等人提出的方法，而作者表示從未向 Astra 提及該方法。若通用模型能自行重現既有的機制可解釋性技術，這個領域的工具與人力配置會變動。但同樣要注意 Experiment 7 的界線：能重現的是結構層次的分析，行為層次的歸因還沒有。
- **開放權重與封閉權重的稽核落差會擴大。** 這類方法的前提是拿得到權重。能被這樣稽核的，只有開放權重的模型；而能執行這種稽核的，是最強的封閉模型。稽核能力與被稽核對象的這種不對稱，值得持續觀察。
- **研究成果的發布形態。** 本篇以自建站部落格發布、無 arXiv、無 DOI、未經同儕審查，但釋出了完整 logs 與模型，並已有一次外部重跑。這是一種以**可重現性**換取**同儕審查**的發布形態；對讀者而言，判斷依據從「它通過了審查」變成「我能不能自己跑一遍」。

## 與書庫其他文章的關係

兩則談的是同一個模型 GPT-6 Astra，揭露姿態卻完全相反：該則記錄 OpenAI 自家公告除了 Terminal-Bench Science 的 68.1% 之外不公布任何絕對分數，外部無法設定門檻；本則是四位外部研究者把 Astra 的每一次輸入、輸出、推理摘要與評估腳本整包放上 GitHub，連失敗的那個實驗也留在裡面: [GPT-6.1 Sol 只要五分之一價，科學那一欄仍是 Astra](2026-10-07-openai-gpt-6-1-sol-launch.md)

兩者對神經網路做的是同一類手術，而誰拿刀不同：該研究以 sparse autoencoder 解出 ICD 章節的概念方向並在 11 個開源模型上做因果介入，方向由既定演算法算出；本則的 Experiment 8 是讓一個通用語言模型自己讀權重、自己指認那條造成迴圈的方向，再從兩層 MLP 的各 64 個輸出欄位把它減掉: [病歷讀進 LLM 之後，ICD 章節藏在模型的哪裡？Clinical Concept Centers 在 11 個開源模型裡找方向、做介入](../ai-papers/2026-10-05-clinical-concept-centers-llm.md)

該則整理 FDA 對生成式 AI 醫材提出的監管問題，其中一項是上市後變更要如何追溯；本則示範的修改方式剛好把那個問題推到極端 —— 改動 0.016% 的權重、沒有訓練迴圈、沒有資料集、沒有梯度，傳統上用來證明一次變更做了什麼的那些紀錄全都不存在: [GenAI 醫材要怎麼管？FDA 還在問，這不是指引](2026-09-17-fda-genai-devices-discussion-paper.md)

## 實務的啟發

- **讀這類研究部落格時，先把 TL;DR 和正文的涵蓋範圍並排。** 本篇是個好樣本：正文誠實，TL;DR 只選了成立的那一半。可操作的做法是直接搜尋否定詞 —— `unable`、`could not`、`unfortunately`、`not` —— 看它們落在哪些段落，再回頭看這些段落有沒有進摘要。
- **看到「某指標從 A 升到 B」，先找同一張表的其他欄位。** 本篇的 MATH-500 從 7.9% 到 48.1% 看起來驚人，但同一列的「命中 token 上限」從 93.0% 降到 33.1%，這兩個數字合起來才說明發生了什麼。單看第一欄會把「跑完了」誤讀成「算對了」。
- **預算掃描不是單調就要當成警訊。** IFEval 在 25 次前向傳遞時比 10 次低 9.1 個百分點，而結論取的是 50 次那一點。沒有重複次數與區間的情況下，無法分辨 48.1% 是方法的效果還是單次執行的運氣。要引用這組數字時，應同時引用這個限制。
- **評估「免重訓修補」這類提案時，先問失效模式有沒有單一歸因點。** 本篇給了現成的判準：Qwen 的迴圈可以追到兩層 MLP 的同一條方向，改得動；Gemma 的算術與代數錯誤分散在整個模型，改不動。把一個臨床模型的問題列出來，逐項問「這是不是一個可以關掉的元件」，答案為否的項目就不該期待這條路徑。
- **權重可改寫這件事，應該進入模型變更紀錄的設計。** 若組織內部允許以這種方式修補模型，變更紀錄需要保存的就不再是訓練設定，而是：改了哪些張量的哪些索引、理由的自然語言敘述、以及修改前後的完整評估。本篇作者釋出 logs 的做法，實質上就是這種紀錄的一個範本。

## 後續追蹤

- 作者預告的 Weight-Space Programming benchmark 與 harness 是否發布，以及是否納入行為層級（而非僅訓練任務層級）的稽核任務。
- Experiment 7 的「只看權重」設定是否有後續進展 —— 這是目前「原生讀寫權重」主張與證據之間落差最大的一處。
- 本篇是否轉為 arXiv 預印本或投稿同儕審查；若轉，數值與限定條件是否與部落格版本一致。
- 是否有外部團隊依釋出的 logs 獨立重現 Experiment 8 的 48.1%，並報告重複次數與區間。
- 同類方法是否出現在開放權重的醫療語言模型上，以及屆時的失效模式是否符合本篇「單一可歸因元件」的前提。

## References

- `post` — Rikiya Takehi, Jayden Teoh, Alex Zhang, Omar Khattab. "Sparks of Weight-Space Programming: LLMs can natively read & write neural network weights"（官方部落格，2026-11-02；無 arXiv、無 DOI、未經同儕審查）  
  <https://rikiyat.github.io/blog/weight-space-programming/>
- `logs` — RikiyaT/lm_understand-logs（作者釋出的全部實驗 logs；公開 repo，最後 push 2026-10-29，約 138 MB，GitHub 中繼資料的授權欄為 `NOASSERTION`）  
  <https://github.com/RikiyaT/lm_understand-logs>
- `hfmodel` — RikiyaT/Qwen3.5-0.8B-weight-space-programming（Experiment 8 的編輯後模型，Hugging Face，授權標示 Apache-2.0）  
  <https://huggingface.co/RikiyaT/Qwen3.5-0.8B-weight-space-programming>

[Home](../) · [Industry Watch](./)
