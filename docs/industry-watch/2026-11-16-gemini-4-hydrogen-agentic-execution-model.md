---
parent: Industry Watch
nav_order: 5
title: "非旗艦卻超過自家 Argon：Gemini 4 Hydrogen 解析"
category: industry-watch
date: 2026-11-16
tags: [Google, Google-DeepMind, Gemini-4, Gemini-4-Hydrogen, Orchestrator, Google-Antigravity, frontier-model, model-launch, pricing, context-window, agentic-workflow, benchmark, HealthBench-Pro, biosecurity, false-refusal, research-workflow]
catalog_id: "google:gemini-4-hydrogen-launch-2026-11-12"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.1"
source:
  orgs:
    - "Google"
    - "Google DeepMind"
  event: "Google 發布 Gemini 4 Hydrogen，定位為與前沿模型 Carbon／Argon 分工的快速執行層，整個一百萬 token 脈絡視窗採單一費率，並在 Google Antigravity 同步推出可於單一任務中切換模型的 Orchestrator"
  event_date: "2026-11-12"
  official_url: "https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/"
  single_source: false
  single_org: true
related_articles:
  - path: "2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md"
    relation: "該則是研究機構對代理式工作流程推論成本的預測，本則是供應商對同一個成本問題給出的產品答案：Hydrogen 以較低單價承接執行端、Orchestrator 在單一任務中切換模型以省下前沿模型的額度，官方自報平均少用 24% quota"
  - path: "2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md"
    relation: "該則示範的藥物設計代理流程就跑在 Google Antigravity 上，而本則在同一個環境裡改變了模型指派方式：Orchestrator 讓 Carbon 負責規劃、Hydrogen 負責執行，那類多步驟科研流程的成本與延遲結構因此改變"
  - path: "2026-10-07-openai-gpt-6-1-sol-launch.md"
    relation: "兩則都是以價格與速度為主軸的非旗艦型號發布，揭露方式剛好相反：該則給了相對價格卻在科學那一欄落後自家旗艦，本則給了絕對單價並宣稱指數分數反而高過自家前沿的 Argon"
refs:
  launch:
    title: "Introducing Gemini 4 Hydrogen（Google 官方部落格，2026-11-12）"
    url: "https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/"
  antigravity:
    title: "Gemini 4 Hydrogen and Orchestrator（Google Antigravity 官方部落格，2026-11-12）"
    url: "https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity"
  modelcard:
    title: "Gemini 4 Hydrogen Model Card（PDF，公告所指向的文件；本文未引用其內容）"
    url: "https://storage.googleapis.com/deepmind-media/Model-Cards/Gemini-4-Hydrogen-Model-Card.pdf"
---

[Home](../) · [Industry Watch](./)

# 非旗艦卻超過自家 Argon：Gemini 4 Hydrogen 解析

## 來源

- 組織／產品：Google／Google DeepMind — Gemini 4 Hydrogen；同族另有前沿模型 Gemini 4 Carbon 與 Gemini 4 Argon。
- 事件：發布 Gemini 4 Hydrogen，公布計價、四段 thinking level、一組評測數字與安全評估，並在 Google Antigravity 同步推出 Orchestrator。
- 日期：2026-11-12（公告頁可見日期 `Nov 12, 2026`，JSON-LD `datePublished` 為 `2026-11-12T18:00:00+00:00`；該頁另標 `Last updated November 13, 2026`，`dateModified` 為 `2026-11-13T18:27:54.873135+00:00`）
- 官方入口：[Introducing Gemini 4 Hydrogen](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/)
- 其他官方頁面：[Gemini 4 Hydrogen and Orchestrator](https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity)（Google Antigravity 官方部落格，同日），本文用它核對 Orchestrator 的運作方式與取用層級。
- **同一家公司的兩個官方頁，無獨立第三方驗證**：本文引用的所有分數、速度與成本比例都由 Google 自行發布或由其合作夥伴提供，相關的限定條件集中列在後段的證據邊界一節。

**編輯：** Clarence

Google 在 2026-11-12 發布 Gemini 4 Hydrogen [(ref: launch)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/)。公告把它定位成與前沿模型分工的一層：Gemini 4 Carbon 與 Gemini 4 Argon 負責「deep, long-horizon reasoning」，Hydrogen 則是「built for rapid execution across diverse agentic workflows」，承接寫程式、跑測試、驗證修改這類需要高頻反覆執行的段落。整個一百萬 token 的脈絡視窗採單一費率，每百萬 input token 1.50 美元、每百萬 output token 7.50 美元。同日 Google Antigravity 另發一頁，宣布新的 Orchestrator 選項會在同一段任務的進行中，於 Carbon 與 Hydrogen 之間雙向切換 [(ref: antigravity)](https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity)。對醫療與研究工作流程來說，這則發布有兩個直接相關之處：一是長脈絡的單一費率，決定長病歷、長文獻、長紀錄批次處理的成本可預測性；二是公告在安全一節寫明，新的防護更能分辨真正的生物安全風險與正當的醫學或科學問題，並以 HealthBench Pro 上低於 0.4% 的誤擋率作為指標。

## 背景

- **2026-11-12 稍早的同一週** — Antigravity 頁寫「Earlier this week, we introduced Gemini 4 Carbon alongside `/swarm`」，把前沿模型 Carbon 與多工作區平行代理功能的發布定在本則之前幾天 [(ref: antigravity)](https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity)。本則的 Orchestrator 正是把那個前沿模型與新的執行層配成一對，因此兩者屬於同一條產品線上前後相接的兩步，而非各自獨立的公告。
- **2026-11-12** — Google 發布 Gemini 4 Hydrogen（本則事件），同日 Antigravity 發布 Gemini 4 Hydrogen and Orchestrator。
- **2026-11-13** — 公告頁標示最後更新日為 November 13, 2026；本文的所有數值取自 2026-11-16 讀到的該頁原始文字。

公告把 Hydrogen 的主要對照基準設在 Gemini 3.8 Flash（原文寫 `teams migrating from Gemini 3.8 Flash`），因此本則多數的速度與成本比較是對 3.8 Flash，而非對 Carbon 或 Argon。

本則無配圖。公告頁的圖片與示範影片為 Google 自有素材，不重製。

## 這個模型的定位與分工（事實）

- **與前沿模型的分工** — 公告寫明 Carbon 與 Argon 是「our frontier models」，擅長最難問題上的長程推理；Hydrogen 則「built for rapid execution across diverse agentic workflows」，可單獨使用，也可作為多模型工作流程中的「high-efficiency execution engine」[(ref: launch)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/)。
- **四段 thinking level** — low、medium、high（預設）與新增的 xhigh。公告稱這四段在品質、延遲與成本之間提供「smooth, predictable progression」。
- **脈絡視窗** — 原生一百萬 token 輸入，輸出最多一百萬 token。
- **平行代理的角色分派** — 公告描述的用法是 Carbon 擔任 coordinator，Hydrogen 擔任 worker 與 verifier，在彼此隔離的工作區中同時建置與測試。

## 計價（事實）

- **單一費率涵蓋整個視窗** — 公告寫 Hydrogen「priced flat across its entire 1 million-token context window」，每百萬 input token 1.50 美元、每百萬 output token 7.50 美元 [(ref: launch)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/)。output 單價為 input 單價的五倍（7.50 ÷ 1.50，由本文代為計算）。
- **沒有分級加價** — 這裡的 flat 指的是不隨脈絡長度跳階，公告未列出任何長脈絡加價級距。公告未提供 Gemini 3.8 Flash、Carbon 或 Argon 的單價可供並列。

## Orchestrator：同一任務內切換模型（事實）

- **與靜態 router 的差別** — Antigravity 頁把業界常見作法描述為「static model router」：從第一個提示猜測任務難度，然後把整個任務交給足以完成它的最便宜模型；該頁指出這種作法在長時間執行的代理任務上會失效，因為不同階段需要的複雜度不同，而且常常是任務進行中才發現 [(ref: antigravity)](https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity)。
- **雙向切換的實際流程** — 該頁舉的例子是：Carbon 先以唯讀階段探索相依關係、釐清模糊處並訂出帶有明確重新規劃觸發條件的計畫；Hydrogen 接手寫修改、更新套件、跑測試；Hydrogen 遇到阻礙時再交還 Carbon 檢視狀態、修正計畫並恢復執行。
- **官方自報的效益** — 兩頁都寫 Orchestrator 達到「near-Carbon task success rates」，平均少用 24% quota、快 19% 完成。兩頁對這組數字所用的評測版本寫法不同，見證據邊界一節。
- **SDK 的明確指派** — Antigravity 頁另提供以 Antigravity SDK 直接指定各角色模型的作法，示範是一套開源 issue 分流系統：Hydrogen 代理負責分流、搜尋程式庫、提出釐清問題與依 PR 留言快速調整介面，Carbon 代理負責較大的重構、新功能與安全檢查。
- **Orchestrator 的取用層級** — Antigravity 頁寫 Orchestrator 以 `Orchestrator (Carbon)` 與 `Orchestrator (Argon)` 兩種形式提供給 Google AI Ultra 訂戶，付費 Google AI Pro 訂戶只拿得到 `Orchestrator (Argon)`；企業則透過 Gemini for business 取用。

## 評測分數（事實）

以下數字全部出自 Google 自己的兩個頁面 [(ref: launch)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/) [(ref: antigravity)](https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity)。

| 項目 | Hydrogen | 對照 | 公告寫法 |
|---|---|---|---|
| Artificial Analysis Intelligence Index（預設 high） | 51 | Argon 50 | `surpasses Argon` |
| Artificial Analysis Intelligence Index（xhigh） | 54 | — | `reaching 54 at its highest xhigh thinking setting` |
| Terminal-Bench 4.1 | 57% | Gemini 3.8 Flash 18.2% | `more than tripling` |
| HLE-Diamond | 58.8% | — | `leads its class` |
| Vals Tax Agent Bench | 52.3% | — | `ranks #1 overall` |
| Vals Legal Research Bench | 55.8% | — | `ties for #1` |
| Multimodal Knowledge Agent（MKA） | 53.4% | — | `outperforms other models` |
| Agents' Last Exam v1.1 | 71.6% | — | 同上句 |
| Agent Arena | 第 5 名 | — | `ranks #5` |
| AutomationBench-AA | 未給分數 | — | `leads its class` |
| SWE-sweep | 未給分數 | — | `outperforms similar-tier models` |

- **相對於 Gemini 3.8 Flash 的三項改善** — 公告寫在預設 high 設定下完成任務快 2.5 倍、Terminal-Bench 4.1 分數「more than tripling」（57% 對 18.2%，相除約為 3.13 倍，由本文代為計算），以及捏造宣稱（`fabricated claims`）減少超過五倍。
- **合作夥伴的早期測試** — 公告寫在複雜圖結構、SQL 與資料密集的企業工作流程上，合作夥伴看到 Hydrogen 比 3.8 Flash 快 2 到 2.8 倍，token 用量少 12% 到 23%。
- **Google Sheets 內的一項** — 公告寫在 Sheets canvas 中產出比先前模型快超過 30%。

## 安全評估與醫學問題的誤擋（事實）

- **代理行為面** — 公告稱 Hydrogen 把代理任務中的 overreach（逾越授權範圍）降低最多 81%、under-service（做得不足）降低最多 79%，並把工具使用與程式碼評估中的 misaligned actions 與 task shortcutting 降低 12 倍；面對不可能或被阻擋的任務時，繞過權限邊界的機率最多降為二分之一，內部 agent honesty evaluation 的誠實率為 94% [(ref: launch)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/)。
- **推理可讀性** — 公告稱在超過 200,000 個受稽核的回合中保有 99.9% 的 chain-of-thought legibility，且 deceptive reasoning edits 為零。
- **提示注入** — 公告稱在 Gray Swan IPI benchmark 上對 indirect prompt injection 的韌性提高超過 2.3 倍。
- **醫學與科學問題的誤擋** — 公告寫更新後的防護「much more precise at distinguishing between real biosecurity risks and legitimate medical or scientific questions」，並把 HealthBench Pro 上的 false refusals 控制在 0.4% 以下。這是全篇公告唯一一處同時出現 `medical` 與 `biosecurity` 的句子（兩詞全文命中各 1 次）。
- **一段生技側的合作夥伴說法** — LatchBio 的 Biologics Development 團隊（Joshua Badshah、Dillon Flood）在公告中寫：Hydrogen 是他們 Antibody Development benchmark 的 toxicology and safety 一節中最準確的模型，通過 67% 的嘗試，對比非 Gemini 模型最佳的 37%（相差 30 個百分點，由本文代為計算），並且是最快的 Gemini 模型，每項任務約 13 分鐘；該段並描述它「reasoned like a cautious safety reviewer」，在病人風險高時選擇保守假設。

## 取用與上線範圍（事實）

- **公告的範圍句** — 公告寫 Hydrogen 把 Gemini 4 帶給所有人，涵蓋 Google AI Studio 的所有層級、Gemini API、Gemini for business、Gemini 應用程式、Google Search，以及 Google Antigravity 中付費的 Google AI Pro 與 Ultra 訂戶 [(ref: launch)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/)。
- **免費層的實際條件寫在註腳** — 公告唯一一條註腳寫：在 Gemini 應用程式中，免費使用者是透過 auto model selection 在系統判斷適合時才用到 Gemini 4 Hydrogen，而非自行從模型選單指定。
- **Search 的變動** — 公告稱 Hydrogen 大幅升級 Search，包括更能理解自然語序與含錯字的複雜提問、更視覺化的回應，以及擴大 query fan-out 技術所連出的連結範圍。

## 證據邊界（事實）

上列數值全部來自 Google 自己的兩個官方頁面。下列限定條件集中列在這裡，供引用時一併帶上：

- **兩個官方頁對同一組數字標了不同的評測版本** — 同一句「Orchestrator 達到近似 Carbon 的任務成功率，平均少用 24% quota、快 19% 完成」，在 blog.google 的版本寫的是「On Terminal-Bench **4.0**」，在 Antigravity 的版本寫的是「On Terminal-Bench **4.1**」。兩頁的百分比完全相同，只有版本號不同；公告頁上「Terminal-Bench 4.0」的連結指向 tbench.ai 的 4.0 發布說明，而「Terminal-Bench 4.1」的連結指向 tbench.ai 首頁。外部無法從這兩頁判斷這組數字究竟跑在哪一版上。
- **near-Carbon 沒有數值** — 兩頁都未給 Carbon 在該評測上的分數，也未給 Orchestrator 的分數，因此「接近」的幅度不可核對；24% 與 19% 都是相對值，沒有任何絕對的 quota 量或完成時間作為基準。
- **指數領先幅度是 1 分，且未標示快照時間** — 51 對 50 的差距為 1 分、xhigh 的 54 比 Argon 高 4 分（由本文代為計算）。公告連到 artificialanalysis.ai 首頁，但未標明取數日期或版本，而該榜為持續更新的即時榜。
- **四項評測只給名次或等第，不給分數** — AutomationBench-AA 與 SWE-sweep 只寫「leads its class」「outperforms similar-tier models」；Agent Arena 只給第 5 名；「its class」在全文未被定義，因此「同級」包含哪些模型由公告自行認定。
- **多數百分比沒有分母** — 全文可抓到的百分比共 24 個，其中 HLE-Diamond 58.8%、Vals Tax Agent Bench 52.3%、Vals Legal Research Bench 55.8%、MKA 53.4%、Agents' Last Exam v1.1 71.6% 等，均未附題數、受測次數或信賴區間。
- **安全數字多為上限值或倍數** — overreach 的 81%、under-service 的 79% 都寫成 `up to`；12 倍與 2 倍同樣沒有絕對基準；94% 的誠實率來自「our internal agent honesty evaluation」，該評估未公開。
- **HealthBench Pro 的 0.4% 是上界，不是量測值** — 公告寫 `under 0.4%`，未給絕對次數、題數、受測模型設定，也未給 Gemini 3.8 Flash 或其他模型在同一題組上的誤擋率作為對照。對想判斷「我的臨床問題會不會被擋」的團隊而言，這一句只能說明方向，不足以當作門檻。
- **LatchBio 那組數字出自其內部評測** — Antibody Development benchmark 為該公司自建，公告未給題數、受測次數或方法說明，「best non-Gemini model」也未具名。這段文字刊登在供應商的公告中，屬於合作夥伴自報，而非獨立評估。
- **所有合作夥伴引言皆由供應商刊載** — 公告收錄 Cartwheel、Discovery Loop、LatchBio、STAN、Astrocade、Box、Pixelcut、Zingroll 八段使用者說法，全部出現在 Google 自己的頁面上，各自的評測條件未公開。
- **「available to everyone today」與註腳的條件不完全一致** — 小節標題寫的是今天起所有人都能用，而唯一一條註腳說明免費使用者只能透過 auto model selection 間接用到；兩者並讀才得到完整條件。
- **model card 的內容未納入本文** — 公告指向一份 Gemini 4 Hydrogen Model Card 的 PDF [(ref: modelcard)](https://storage.googleapis.com/deepmind-media/Model-Cards/Gemini-4-Hydrogen-Model-Card.pdf)。本文所有數值均取自上述兩個網頁，未引用該 PDF 的任何內容；安全與誤擋數字的方法細節因此仍屬未核對。
- **全文沒有醫療法規或臨床驗證的字樣** — `FDA`、`arXiv`、`peer review` 在公告中命中皆為 0。這是一則通用模型發布，不含任何醫療器材法規狀態的宣稱，HealthBench Pro 與 LatchBio 那兩處是全文僅有的醫學與生技接點。

## 本書庫解讀（評論）

- **把「分層」從價格分層改成任務階段分層，是這則發布真正的新東西** — 過去選模型是一次性決定：這個專案用哪一級。Orchestrator 描述的作法是在單一任務的進行中雙向切換 —— 規劃交給前沿模型，執行交給便宜的一層，卡住了再交還回去。對醫療與研究這種流程長、步驟異質的工作，這個結構比「再降一次價」更有意義：一段文獻回顧、一次影像前處理批次、一輪統計重跑，各自需要的推理深度本來就不同。但要注意這目前是供應商在自家環境（Google Antigravity）裡的實作，公開的效益數字只有相對值。
- **長脈絡單一費率對醫療文件處理是可預測性的改善，而不只是便宜** — 一百萬 token 的視窗內不跳階，意味著處理一份長病歷摘要與處理一份短出院摘要的單位成本相同。對要估算整批處理成本的單位來說，可預測性往往比單價本身更重要 —— 過去長脈絡加價級距會讓「處理多長的文件」成為成本函數中最難估的一項。不過公告沒給任何對照單價，所以「便宜多少」這件事本頁回答不了。
- **HealthBench Pro 的誤擋率值得注意，但目前只是一個方向** — 生物安全防護誤擋正當醫學問題，是臨床與生醫研究端實際遇過的摩擦：問一個關於毒理或病原的正當問題卻被拒答。公告把這件事放進發布說明本身，代表供應商把它當成可量化的產品指標，這在本書庫追蹤的同類公告中並不常見。但 `under 0.4%` 是上界而非量測值，沒有對照組、沒有題數，任何引用都應寫成「廠商自報、單源、無分母」。要判斷自家的題型會不會被擋，仍然只能自己跑一次小規模前後測。
- **兩個官方頁的評測版本不一致，是引用時的實際風險** — 24% 與 19% 這組數字會被當成「代理工作流程可省多少」的參考值四處轉引，而它在兩個官方頁上掛著不同的評測版本。這不是文字瑕疵：Terminal-Bench 4.0 與 4.1 是兩個不同的題組版本，分數不可互換。引用時應連同「官方兩頁版本標示不一致」一併記錄，或直接等待帶有版本號的第三方複現。
- **對照基準選在 3.8 Flash，決定了這些數字的可比性** — 2.5 倍、三倍多、少 12% 到 23% 的 token，全部是對 Gemini 3.8 Flash。對已經在用 Carbon 或 Argon 的團隊，這些數字不回答「降級到 Hydrogen 會失去什麼」；對從別家供應商評估的團隊，這些數字也不構成跨供應商比較。公告唯一的跨模型比較是對自家 Argon 的指數分數，差 1 分。

## 產業影響

- **代理式工作流程的成本競爭，正在從單價移到「一次任務用了哪些模型」** — 本則的兩個主要賣點（單一費率的長脈絡、任務內切換模型）都不是把單價再砍一刀，而是改變計費的形狀。若這個方向成立，採購評估要加一欄：不只是每百萬 token 多少錢，而是一次典型任務實際落在哪幾個模型上、各佔多少比例。本書庫先前整理過的推論成本預測，談的正是這個成本結構問題。
- **執行層模型的分數逼近前沿模型，會改變醫療與研究團隊的模型選擇邏輯** — 若一個定位在執行端的模型在公開指數上與自家前沿模型只差 1 分，那麼「用最強的模型」這個預設就不再自動成立，取而代之的是依任務階段指派。對院內與研究單位而言，這意味著模型治理文件要從「我們採用哪個模型」改寫成「哪一類任務用哪一層，誰決定切換」。
- **生物安全防護的誤擋率開始成為可比較的產品指標** — 把 HealthBench Pro 的誤擋率寫進發布公告，等於供應商承認這是採購方會問的問題。對醫療機構，這是一個可以寫進評估表的新欄位：供應商是否公布正當醫學問題的誤擋率、以什麼題組量測、有無對照。目前的揭露還不足以據此比較不同供應商，但欄位一旦存在，後續公告就有被要求填上的壓力。
- **Orchestrator 式的多模型調度若成為常態，重現性會變難** — 同一個提示在不同時間可能由不同模型的不同階段處理。研究用途上，這使「用了哪個模型」不再是一個單值答案。要讓分析可重現，紀錄的粒度必須從帳號層級細到單次任務的模型軌跡，而目前公開頁面並未說明這類軌跡是否可被使用者完整匯出。

## 與書庫其他文章的關係

該則是研究機構對代理式工作流程推論成本的預測，本則是供應商對同一個成本問題給出的產品答案：Hydrogen 以較低單價承接執行端、Orchestrator 在單一任務中切換模型以省下前沿模型的額度，官方自報平均少用 24% quota: [代理式工作流程推論成本漲逾五倍：Gartner 2028 預測分析](2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md)

該則示範的藥物設計代理流程就跑在 Google Antigravity 上，而本則在同一個環境裡改變了模型指派方式：Orchestrator 讓 Carbon 負責規劃、Hydrogen 負責執行，那類多步驟科研流程的成本與延遲結構因此改變: [代理程式串起既有化學工具：DeepMind 藥物設計 Skills 解剖](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md)

兩則都是以價格與速度為主軸的非旗艦型號發布，揭露方式剛好相反：該則給了相對價格卻在科學那一欄落後自家旗艦，本則給了絕對單價並宣稱指數分數反而高過自家前沿的 Argon: [價格只要五分之一，但科學能力沒跟上：GPT-6.1 Sol 解剖](2026-10-07-openai-gpt-6-1-sol-launch.md)

## 實務的啟發

- **引用 HealthBench Pro 的 0.4% 時，寫成上界而非量測值** — 完整的寫法是「Google 自報，正當醫學與科學問題在 HealthBench Pro 上的 false refusals（誤擋）低於 0.4%，無分母、無對照組、無獨立驗證」。若要據此決定是否導入，可行的替代作法是用本單位實際被擋過的問題整理成一份小題組，自行跑一次前後對照。
- **把 24% 與 19% 這組數字與評測版本一起記錄** — 由於兩個官方頁分別寫了 Terminal-Bench 4.0 與 4.1，任何內部簡報引用時都應註明「官方兩頁版本標示不一致」。不同版本的題組分數不可互換，省略版本號會讓後續讀者誤以為這是同一條可比較的基準。
- **評估長脈絡成本時，分開看「單價」與「計費形狀」** — 本則的單一費率改變的是成本可預測性。建議的作法是拿本單位最長與最短的兩類文件各跑一批，記錄實際 token 數與費用，再與現行方案比較；單看每百萬 token 的數字無法反映長文件在舊計費級距下的實際支出。
- **若要採用任務內切換模型，先決定紀錄粒度** — 導入 Orchestrator 這類機制前，應先確認使用者端能否取得每次任務的模型軌跡。研究用途上，若無法取得，等同於放棄該次分析的可重現性；可行的折衷是對需要重現的工作改以 Antigravity SDK 明確指派模型，而非交給自動調度。
- **把模型治理文件從「採用哪個模型」改寫成「哪一層負責哪一類任務」** — 本則顯示同一供應商內部已有明確的能力分層（前沿推理層與快速執行層）。院內或研究單位的 AI 使用規範若仍以單一模型名稱撰寫，會在供應商每次發布後失效；改以任務階段與風險等級描述，較能維持穩定。
- **區分「公告說所有人都能用」與註腳說的條件** — 本則的免費層實際上是透過 auto model selection 間接使用。評估可得性時，應以註腳與取用條件頁為準，並在內部文件註明不同訂閱層級實際拿得到什麼。

## 後續追蹤

- Terminal-Bench 的 4.0 與 4.1 標示不一致是否會被官方更正，以及 Orchestrator 那組 24%／19% 究竟跑在哪一版上。
- Artificial Analysis Intelligence Index 上 Hydrogen 與 Argon 的分數是否維持 51 對 50，以及該榜後續是否出現第三方帶日期的快照可供引用。
- HealthBench Pro 的誤擋率是否會有絕對次數、題數與對照模型的揭露，或由第三方以同一題組量測不同供應商。
- LatchBio 的 Antibody Development benchmark 是否會公開方法與題數，使那組 67% 對 37% 可被外部複現。
- Gemini 4 Hydrogen Model Card 中關於安全評估、誤擋與 chain-of-thought legibility 的方法細節。
- Orchestrator 的模型切換軌跡是否可由使用者完整匯出，以及是否有 API 層級的紀錄欄位。
- 台灣的醫院與研究機構在評估這類多模型自動調度時，如何對應既有的資訊系統驗證與研究紀錄保存要求。

## References

- `launch` — Introducing Gemini 4 Hydrogen（Google 官方部落格，2026-11-12，含定位、計價、thinking level、評測數字、安全評估、合作夥伴引言、取用範圍與一條註腳）  
  <https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/>
- `antigravity` — Gemini 4 Hydrogen and Orchestrator（Google Antigravity 官方部落格，2026-11-12，含 Orchestrator 的運作描述、SDK 指派方式與取用層級）  
  <https://antigravity.google/blog/gemini-4-hydrogen-in-google-antigravity>
- `modelcard` — Gemini 4 Hydrogen Model Card（PDF，公告所指向的文件；本文未引用其內容）  
  <https://storage.googleapis.com/deepmind-media/Model-Cards/Gemini-4-Hydrogen-Model-Card.pdf>

[Home](../) · [Industry Watch](./)
