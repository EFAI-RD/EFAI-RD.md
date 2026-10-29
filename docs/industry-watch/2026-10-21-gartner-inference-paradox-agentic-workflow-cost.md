---
title: "Gartner 預測「每個」agentic workflow 的推論成本到 2028 年增加逾五倍，並提出 Inference Paradox；新聞稿全文沒有起算基準"
category: industry-watch
date: 2026-10-21
updated: 2026-10-22
tags: [Gartner, inference-cost, agentic-AI, AI-agent, token-economics, Inference-Paradox, unit-economics, FinOps, forecast, cost-management]
catalog_id: "gartner:inference-paradox-agentic-workflow-fivefold-2026-08-17"
editors:
  - "Clarence"
source:
  orgs:
    - "Gartner"
  event: "發布新聞稿預測每個 agentic workflow 的 AI 推論成本到 2028 年將增加逾五倍，並提出 Inference Paradox 一詞"
  event_date: "2026-08-17"
  official_url: "https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028"
related_articles:
  - path: "2026-10-07-openai-gpt-6-1-sol-launch.md"
    relation: "該則是本則所描述現象的供給側樣本，掛牌價降到五分之一而每任務成本比依評測落在 1/5 到 1/7 不等，正好示範了單價與單位工作成本是兩條不同的曲線，而本則主張的就是前者下降不保證後者下降"
  - path: "../ai-basics/multi-agent-llm.md"
    relation: "該篇說明 ReAct 迴圈、工具呼叫與多代理協作的機制，而這些機制正是本則所說「更複雜的工作流程用掉遠多於聊天機器人的 token」的技術來源，兩篇並讀可以把一句成本預測還原成可指認的架構選擇"
  - path: "../ai-papers/2026-10-06-voxelsage-liver-ct-tool-agent.md"
    relation: "Gartner 在本則開出的處方是 inference-tiering、routing 與 orchestration，而該篇的醫療代理正是這個處方的具體樣貌，量測交給確定性程式、大型語言模型只負責調度"
  - path: "2026-10-22-openai-distributed-agents-perturb-seq-atlas.md"
    relation: "該則提供了本則缺少的絕對量 —— 1,946 個代理、39,185 次論文閱讀、16,445 筆保留引用 —— 並把單一代理與分散代理在同樣模型、提示與工具下直接對跑，是少見把 token 用量與產出品質放在同一張表上的公開材料"
  - path: "2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md"
    relation: "本則預測 agentic workflow 的推論成本到 2028 年增加逾五倍，卻沒有給任何絕對量、也沒有基準年；該則是同一種寫法出現在效益側 —— 三個官方位置給出三種加速說法，而被壓縮前後的實測值一律缺席。兩則並讀可以看出成本與效益在缺少絕對值時的對稱性：都無法被否證，也都無法進入任何採購試算"
refs:
  pr:
    title: "Gartner：Gartner Predicts AI Inference Costs Per Agentic Workflow Will Increase More Than Fivefold Through 2028（官方新聞稿）"
    url: "https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028"
  trends:
    title: "Gartner：Gartner Identifies the Top Strategic Technology Trends for 2027（官方新聞稿，2026-10-20）"
    url: "https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027"
  day2:
    title: "Gartner：Gartner IT Symposium/Xpo 2026 Orlando — Day 2 Highlights（官方會議紀要，2026-10-20）"
    url: "https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-it-symposium-xpo-2026-orlando-day-2-highlights"
status: published
skill_version: "write-industry-watch@3.0"
evidence_reviewed: true
---

[Home](../) · [Industry Watch](./)

# Gartner 預測「每個」agentic workflow 的推論成本到 2028 年增加逾五倍，並提出 Inference Paradox；新聞稿全文沒有起算基準

## 來源

- **組織** — **Gartner**（美國市場研究與顧問公司，NYSE: IT）。新聞稿由 Gartner for High Tech Leaders and Providers 發布，具名分析師為 `Will Sommer`，職銜 `Sr. Director Analyst` [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **事件** — Gartner 發布新聞稿，預測**每個 agentic workflow（代理式工作流程）的 AI 推論成本（inference cost，模型在服務請求時實際產生運算的成本）到 2028 年將增加逾五倍**，並提出 `Inference Paradox`（推論悖論）一詞描述「單位經濟改善反而推高 AI 總成本」的現象 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **日期** — **2026-08-17**。頁面發稿行為 `STAMFORD, Conn., August 17, 2026`；頁內 JSON-LD 結構化資料的 `datePublished` 為 `2026-08-17T03:30:00Z`。同一段 JSON-LD 的 `dateModified` 為 `2026-08-14T11:37:27Z`，**早於** `datePublished` 三天；頁面沒有 `<time>` 標籤，也沒有任何日期相關的 meta 欄位。本文採用頁面發稿行與 `datePublished` 一致的 2026-08-17，未推斷 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **官方入口** — [Gartner Predicts AI Inference Costs Per Agentic Workflow Will Increase More Than Fivefold Through 2028](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)
- **來源狀態** — **單源（單一組織），待交叉驗證**。本文另引用兩個 Gartner 官方頁面作為同一主張在兩個月後的延續（2026-10-20 的 2027 年技術趨勢新聞稿與 IT Symposium/Xpo Day 2 會議紀要），但三者同屬 Gartner，不構成獨立佐證 [(ref: trends)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027) [(ref: day2)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-it-symposium-xpo-2026-orlando-day-2-highlights)。支撐本則數字的研究本身為客戶付費內容（新聞稿寫明 `Gartner clients can read more in The Inference Paradox: Inference Tiering Is Critical to Protect Margins`），**本文未取得、未引用其內容**，因此方法、樣本與估算方式皆無法由外部檢驗 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。

**編輯：** Clarence

Gartner 在 2026-08-17 發布新聞稿，給出一個很容易被轉述成一句話的預測：AI 代理的成本會在 2028 年前漲五倍，即使 token 價格在跌。逐項回到原始頁面核對後，這句話的方向沒有錯，但三個限定條件在轉述時最容易掉：它量的是**推論成本**（不是代理的總持有成本），分母是**每一個 agentic workflow**（不是企業的 AI 總支出），而時間寫的是 `through 2028`（到 2028 年為止的一段期間），不是 2028 年當年。更關鍵的是**全文從頭到尾沒有給起算基準** —— 沒有基準年、沒有單一 workflow 現在要花多少錢、沒有任何金額；全頁 `$` 出現 0 次，正文百分比出現 0 次，也沒有任何註腳。因此「逾五倍」是一個**只有倍數、沒有被乘數**的數字，外部無法據以推算任何絕對值，也無法判斷自家的成本曲線是否落在這個預測裡。另有一處極易混淆：新聞稿後半還有第二個「五倍」—— `increases provider inference costs by at least five times` —— 但那是**今天**把任務從聊天機器人換成代理式推論模型的橫向比較，與標題那個**跨時間**的五倍是兩個不同的量，而新聞稿沒有在任何一處區分它們。

## 背景

1. **這一天在本案中的位置** — 2026-08-17 是新聞稿發布日，也是 `Inference Paradox` 這個說法首次出現在 Gartner 公開頁面的日子。新聞稿結尾預告 `Additional analysis on the economics of AI will be presented during Gartner IT Symposium/Xpo`，並列出該年度五場會議的日期與地點，其中 Orlando 場為 2026-10-19 至 10-22 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。這條線在兩個月後確實延續了下去（見下一點），因此本則不是孤立的單篇預測，而是一條論述的起點。
2. **兩個月後的同一條線** — 在 2026-10-20 的 Orlando 會議紀要中，Distinguished VP Analyst `Mary Mesaglio` 的講次要點寫著 `The AI value gap is really an AI risk gap. Cost is the biggest tactical risk to scaling AI.`（AI 的價值落差其實是風險落差；成本是規模化 AI 最大的戰術風險） [(ref: day2)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-it-symposium-xpo-2026-orlando-day-2-highlights)。同日的 2027 年技術趨勢新聞稿則把 `excessive token consumption`（過量的 token 消耗）列為缺少 context layer 時的營運風險之一，並預測 `by 2027, organizations that prioritize semantics in AI-ready data will increase agentic AI accuracy by up to 80% and reduce costs by up to 60%` [(ref: trends)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027)。亦即八月的成本預測在十月被提升為 CIO 層級議題，但後者給的兩個數字同樣是 `up to`（最多）形式的上限值。
3. **這篇是寫給誰看的** — 新聞稿歸屬於 **Gartner for High Tech Leaders and Providers**，正文反覆以 `product leaders`（產品主管）為對象，並把問題定義為 `a new margin challenge`（新的毛利挑戰） [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。亦即它的原始讀者是**賣 AI 產品的科技供應商**，關心的是自家產品的毛利；企業採購端（例如醫院資訊部門）是這條成本鏈的下游，會以價格形式承受，但不是這篇的設定讀者。這一點影響怎麼讀它的建議。
4. **為什麼單價下降不等於支出下降** — 新聞稿給的機制是三條同時發生的趨勢：基礎模型的成本經濟快速改善；效率改善反而讓更強、**也更貴**的模型得以投入更高價值的應用；而更複雜的工作流程用掉的 token 遠多於單純的聊天機器人互動 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。三者相乘的結果是單位成本在降、單位工作量在漲，而後者漲得更快。
5. **本書庫為何收錄一則非醫療的預測** — 本書庫記錄的醫療 AI 研究正在大量從「單次推論出一個答案」轉向多步驟的工具代理，而這類系統的成本結構恰好就是本則描述的那一種。評論段會把這件事接回醫療影像與研究工作流程的實際意義。

## 事實（可核對）

### 新聞稿寫了什麼

- **標題與主張** — 標題為 `Gartner Predicts AI Inference Costs Per Agentic Workflow Will Increase More Than Fivefold Through 2028`，導言重述為 `AI inference costs per agentic workflow will increase more than fivefold through 2028 according to Gartner, Inc.`。三個限定詞都在標題裡：`inference costs`（推論成本）、`per agentic workflow`（每一個代理式工作流程）、`through 2028`（到 2028 年為止） [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **副標題即是結論** — `Product Leaders Are Facing the Inference Paradox: Better Unit Economics Is Escalating the Overall Cost of AI Without Providing a Clear Pathway to Commensurate and Predictable Value`。`Inference Paradox` 在正文中另有一次完整定義，用字相同 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **沒有起算基準** — 全文沒有基準年、沒有單一 workflow 的現行成本、沒有任何金額。以頁面可見文字逐詞計數：`$` 符號 **0 次**、`baseline` **0 次**、`today`（作為時間基準）**0 次**；正文沒有任何百分比（整頁唯一一個 `%` 出現在側欄「Latest releases」清單中另一則新聞稿的標題裡）。頁面 `<sup>` 元素 **0 個**，亦即全文沒有註腳 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **「逾五倍」是下限而非點估計** — 用字為 `more than fivefold`，沒有上界、沒有區間、沒有分布，也沒有說明這個倍數是中位數、平均值或情境上限 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **沒有定義 agentic workflow** — 新聞稿未說明一個 workflow 包含幾個步驟、呼叫幾次模型、使用哪一類模型，也沒有區分產業或地區 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **三條驅動趨勢（原文轉述）** — `Foundational model cost economics are rapidly improving.`；`Improved AI efficiency is unlocking the deployment of more powerful, and more expensive, models to enable higher-value, more sophisticated AI applications.`；`More sophisticated AI workflows use far more tokens than simple chatbot interactions, driving higher overall inference costs.` [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)
- **單價下降這件事沒有被量化** — 新聞稿只寫 `falling model prices`、`cost economics are rapidly improving`，以及 `tokens are becoming more cost-efficient, but not as quickly as AI capabilities and the costs associated with those capabilities are increasing`。**降幅是多少、在什麼期間降、以什麼為基準，全文都沒有寫** [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **分析師引述三則** — `Product leaders cannot rely on more efficient token economics to rationalize AI costs.`；`Each successive generation of AI capability will necessitate more, and often more expensive, tokens. There is no reliable, economical one-size-fits-all model on the horizon.`；`Defaulting to generic autonomous intelligence will result in unbounded costs orders of magnitude higher than those of optimized product ecosystems.` 三則皆出自 Will Sommer [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **開出的處方** — `highly optimized inference-tiering, routing and orchestration`（推論分層、路由與調度），用以 `calibrate complex tasks relative to more cost-efficient intelligence`；或者要求先進 AI 帶來 `exponentially higher returns relative to basic models`。新聞稿自述兩條路都 `eminently possible but will require significant effort` [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **支撐研究不公開** — 全文唯一指向方法的句子是 `Gartner clients can read more in The Inference Paradox: Inference Tiering Is Critical to Protect Margins`，為客戶付費內容 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。

### 兩個「五倍」量的不是同一件事

- **第一個五倍（標題）** — `increase more than fivefold through 2028`。這是**跨時間**的變化：同一個對象（每個 agentic workflow 的推論成本）在一段期間內的倍增 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **第二個五倍（正文後段）** — `Compared to a basic chatbot interaction, routing a task to an agentic reasoning model increases provider inference costs by at least five times, and often much more as task complexity grows.` 這是**同一時點的橫向比較**：把任務從基本聊天機器人互動換成代理式推論模型，成本至少五倍；而且量的是 `provider inference costs`（服務提供方的推論成本），與第一個五倍的對象並不相同 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **新聞稿沒有區分兩者** — 全文沒有任何一句說明這兩個「五倍」是不同的量，也沒有說明兩者是否相乘、是否重疊，或第二個是否就是第一個的成因之一。以頁面逐詞計數，`fivefold` 出現 2 次、`five times` 出現 1 次、`5x` 0 次 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。

### 唯一的圖沒有任何數字

- **圖說與出處** — 圖標題為 `Figure 1: AI Complexity Outpaces Falling Token Costs`，下方標示 `Source: Gartner (August 2026)` [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **圖面內容** — 本文在瀏覽器中檢視該圖（`inferenceparadox2026.png`，1149 × 593 像素）後確認：縱軸標示為 `Total Inference Cost`，**沒有刻度值也沒有單位**；橫軸**完全沒有標籤**，也沒有刻度。圖上有三條自原點附近向右上方延伸的直線，由陡至緩依序標為 `2025 AI Technology Cost Curve`、`2026 AI Technology Cost Curve`、`Optimal AI Technology Cost Curve`；另有兩個圓點分別標 `2025` 與 `2026`，以一小段虛線相連，虛線旁標 `Rate of Innovation` [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **這張圖能與不能支撐什麼** — 它是一張純示意圖：能表達「較新的技術曲線較平緩、但實際落點仍往右上移動」這個概念，**無法支撐任何倍數**。標題所稱的「逾五倍」不出現在圖上，圖上也沒有任何可供外部核對的數值 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。
- **圖的替代文字是未填的樣板** — 該圖在頁面上的 `alt` 屬性為字串 `[Image Alt Text for SEO]`，頁內 JSON-LD 的 `ImageObject.description` 亦為同一字串，且 `height` 欄位填 `0`。這是 Gartner 自家頁面未填妥的樣板佔位，與本則主張無關，但影響該圖對螢幕閱讀器使用者的可及性 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。

### 兩個月後的延續

- **成本被提升為 CIO 層級議題** — Mary Mesaglio 在 Orlando 的講次要點：`The AI value gap is really an AI risk gap. Cost is the biggest tactical risk to scaling AI.`；同一組要點另寫 `AI agents are experiencing a reality check, where the goldilocks zone of implementation is where reliability and security meet autonomy.` [(ref: day2)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-it-symposium-xpo-2026-orlando-day-2-highlights)
- **token 消耗被寫進技術趨勢** — Gene Alvarez 在 2027 年技術趨勢中指出，缺少專屬的 context layer 時，組織會面臨 `overprivileged agents, compliance failures, low trust and excessive token consumption` 等營運風險；同節並預測 `by 2027, organizations that prioritize semantics in AI-ready data will increase agentic AI accuracy by up to 80% and reduce costs by up to 60%` [(ref: trends)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027)。
- **十月這兩個數字同樣是上限值** — `up to 80%` 與 `up to 60%` 皆為上界，新聞稿未給典型值、未給分母、未說明以什麼為對照 [(ref: trends)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027)。

## 本書庫解讀（評論）

- **只有倍數、沒有被乘數的預測，無法被任何人拿去驗收** — 這是本則最實際的限制。「逾五倍」若要能用，必須知道從什麼起算：是 2025 年的某個基準、2026 年發稿當下，還是客戶自己的現況？新聞稿三者都沒給。結果是任何一家組織都無法回答「我們算不算符合這個預測」，也無法在 2028 年回頭判定這個預測對了還是錯了。一個在定義上就無法被證偽的數字，傳播力很強，可驗收性是零。本書庫先前記錄過數則「只給相對數字」的公告（見關聯段），本則是其中最純粹的一個 —— 它連一個絕對數都沒有。
- **兩個五倍放在同一頁，是這則最容易出錯的地方** — 標題的五倍是跨時間的（到 2028 年），後段的五倍是跨架構的（聊天機器人換成代理式推論模型，今天就成立）。兩者碰巧同為「五」，但量的對象、時間跨度與承擔方都不同。轉述時若把兩句合併，很容易得到「換成代理會貴五倍、而且到 2028 年還會再貴五倍」這種新聞稿沒有說過的複合結論，也可能反過來把標題那個需要三年才發生的變化，誤讀成今天換架構就會發生的事。要避免這個錯誤，最低成本的做法是：**看到倍數，先問它的分母和時間軸**。
- **「即使 token 價格下降」這半句在新聞稿裡是質性的** — 新聞稿明確說了單價在降、說了降得不夠快，但**沒有給任何降幅數字**。這一點值得特別標出來，因為這半句在轉述時常被補上一個具體百分比。就本則官方頁面而言，單價下降的速度是未量化的；本文不替它補數字。
- **機制說得比數字好** — 撇開數字不談，新聞稿的三條驅動趨勢是站得住的因果描述：單價下降 → 更貴更強的模型變得可用 → 工作流程變複雜 → token 用量成長快過單價下降。這條鏈不需要那個五倍也成立，而且它可以被任何一家組織用自己的帳單驗證。本書庫認為這篇的價值在機制，不在倍數。
- **這是寫給供應商的毛利建議，轉到採購端要換算** — 新聞稿把問題定義為產品主管的 margin challenge，處方是 inference-tiering、routing 與 orchestration。這些是**供給側**降低自家成本的手段。對醫院或研究單位這種需求側讀者，同一份分析的意思要翻譯一次：你買到的 AI 功能價格，取決於供應商有沒有做這些最佳化；而當供應商把成本壓力轉為用量計價時，**你的帳單會隨你的工作流程複雜度浮動，而不是隨模型掛牌價浮動**。
- **醫療橋接** — 本書庫收錄的醫療 AI 系統，正在大量從「一次推論得到一個答案」轉向本則所說的 `multistep execution`。影像判讀的工具代理會先分割、再量測、再比對先前檢查、再生成敘述；報告生成的代理會逐段自我檢查；多代理系統更會讓數個模型彼此質詢。這些架構在論文裡是以準確率提升被記錄的，但它們在部署端的意義是**每一份檢查的 token 用量不再由模型單價決定，而由它想幾輪、調幾次工具決定**。這帶來三個具體後果。第一，**成本必須以「每一份檢查／每一份報告」計價來評估**，而不是以每百萬 token 的掛牌價評估 —— 後者正是本則說的那條會誤導人的曲線。第二，**論文裡的推論次數就是成本規格**，應與準確率並列閱讀；一個多兩個百分點但多跑五輪的設計，在真實科室可能是賠本的。第三，Gartner 開出的 tiering 與 orchestration，在醫療情境已有現成樣貌：把確定性的量測交給傳統程式、只讓模型負責調度與敘述，既是本書庫記錄過的工程作法，也正好是成本上最便宜的那條路。換句話說，這則預測對醫療 AI 的提醒不是「代理會變貴所以別做」，而是**把推論預算當成系統設計的一個欄位，和準確率寫在一起**。
- **Gartner 自己的後續沒有補上基準** — 兩個月後的 Orlando 會議把成本拉高到「規模化 AI 最大的戰術風險」，但同一批公開材料給的仍是 `up to 80%`、`up to 60%` 這種上限值。亦即從八月到十月，這條論述的**可驗收性沒有改善**，改善的是它的受眾層級。

## 產業／生態影響

- **單位價格戰與總支出成長可以同時發生，而且兩邊都會被拿來行銷** — 模型供應商會以掛牌價下降為賣點，顧問公司會以總支出上升為警示，兩種說法可以同時為真。對讀者而言，真正的判準不是相信哪一邊，而是**確認對方講的是哪一個分母**：每百萬 token、每一次請求、每一個工作流程，還是整個組織的年度支出。本則把這四者中的第三個挑出來談，而這恰好是最少被公布的一個。
- **用量計價正在把成本風險從供應商移到使用者** — 當定價從席次授權轉為依消耗量計費，使用者的帳單就會隨自家工作流程的複雜度浮動，而複雜度多半是由供應商的產品決策（模型世代、推論輪數、預設代理行為）決定的。這是一種**使用者承擔、供應商決定**的成本結構，值得在採購合約階段就要求可預測性條款或用量上限。
- **「成本」正在被重新歸類為風險而非財務項目** — Gartner 十月把成本講成 `the biggest tactical risk to scaling AI` [(ref: day2)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-it-symposium-xpo-2026-orlando-day-2-highlights)。這個歸類的實務後果是：成本控制會從財務部門的事，變成架構與治理的事，也就是會進到技術選型與驗收標準裡。對醫療機構而言，這意味著 AI 採購的評估表上應該要有推論預算這一欄。
- **預測的可驗收性應該成為顧問內容的品質訊號** — 一則帶倍數但無基準的預測，和一則給出基準年與絕對值的預測，對讀者的價值差距極大。本書庫的立場是：**把「有沒有給被乘數」當成判斷分析品質的固定一問**，這不需要任何專業背景就能執行，而且對廠商與顧問一體適用。

## 與書庫其他文章的關係

兩則合起來正好是同一個現象的兩端：該則是供給側的樣本，掛牌價降到五分之一，但每任務成本比依評測落在 1/5 到 1/7 不等，顯示單價與單位工作成本從來不是同一條曲線；本則則從需求側主張，單價下降反而會讓更貴的工作流程變得可行，使總推論成本不降反升 —— 兩則並讀可以看出「價格變便宜了」這句話在缺少分母時有多不可靠: [OpenAI 發布 GPT-6.1 Sol：五分之一價格逼近 Astra，但科學研究那一欄仍由 Astra 領先](2026-10-07-openai-gpt-6-1-sol-launch.md)

該篇說明 ReAct 迴圈、工具呼叫與多代理協作的運作方式，而這些機制正是本則所說「更複雜的工作流程用掉遠多於聊天機器人的 token」在技術上的具體來源；把兩篇並讀，本則那句成本預測就可以被還原成一組可指認的架構選擇 —— 要不要讓模型自我質詢、要跑幾輪、要讓幾個代理互相對話: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md)

Gartner 在本則開出的處方是 inference-tiering、routing 與 orchestration，而該篇的醫療工具代理正是這個處方在醫療影像上的具體樣貌：量測交給確定性程式、大型語言模型只負責調度，從成本角度看這正是把最貴的那一段從推論移出去；該篇同時提醒這種設計的證據仍停在系統測試與模擬器，亦即成本與效益都還沒有在真實科室被量過: [量測交給程式、LLM 只負責調度：VoxelSage 的肝腫瘤 CT 工具代理，證據停在系統測試與模擬器](../ai-papers/2026-10-06-voxelsage-liver-ct-tool-agent.md)

本則主張 agentic workflow 的推論成本將隨工作流程複雜度上升，卻沒有給任何絕對量；該則提供了一組被量出來的絕對量 —— 1,946 個代理、39,185 次論文閱讀、16,445 筆保留引用 —— 並把單一代理與分散代理在同樣模型、提示與工具下直接對跑，是少見把 token 用量與產出品質放在同一張表上的公開材料，可以當作本則那句預測的具體下界: [OpenAI 公布以 AI 代理群解讀全腦 Perturb-seq 圖譜：公告寫「引用逾 700 篇」，它所連結的論文寫的是「711 倍」](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md)

本則預測 agentic workflow 的推論成本到 2028 年增加逾五倍，卻沒有給任何絕對量、也沒有基準年；該則是同一種寫法出現在效益側 —— 三個官方位置給出三種加速說法，而被壓縮前後的實測值一律缺席。兩則並讀可以看出成本與效益在缺少絕對值時的對稱性：都無法被否證，也都無法進入任何採購試算: [Google DeepMind 示範用 Antigravity 搜尋抗菌胜肽：「數天變成一次對話」「in hours」「數小時變成數分鐘」三種加速說法分屬三個官方位置，沒有一個附得出絕對數值；而那個候選分子在 UniProt 的名稱，證據欄寫的是 Google:ProtNLM](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md)

## 實務的啟發

- **看到倍數，先找被乘數** — 本則提供了一個乾淨的練習：「逾五倍」若找不到起算基準，它就只能當成方向性判斷，不能進財務模型、不能寫進採購簡報的數字欄。問法很簡單：「從多少開始算？哪一年？」
- **分清楚跨時間的倍數與跨架構的倍數** — 本則同一頁上就有兩種。換架構的成本差距今天就會發生，時間軸上的成長則需要數年且取決於你會不會採用更複雜的設計。兩者該放進不同的決策。
- **用「每一份產出」當成本單位，而不是每百萬 token** — 對醫院與研究單位，有意義的單位是每一份檢查、每一份報告、每一次問答的成本。這個數字可以從現有帳單與用量紀錄直接算出來，不需要等任何人公布預測。
- **把推論預算寫進模型驗收標準** — 建議在評估任何醫療 AI 工具時，與準確率並列記錄：單次工作流程的平均推論輪數、平均 token 用量、以及尖峰與中位數的差距。這三個數字決定了規模化後的帳單形狀。
- **在合約裡處理用量計價的不可預測性** — 若供應商採消耗量計費，值得要求用量上限、超額告警、以及模型世代更換時的成本變動通知。本則的核心機制正是「更強的新模型會讓每次工作用掉更多 token」，而換代通常由供應商決定。
- **先做分層，再談自主** — 新聞稿那句 `Defaulting to generic autonomous intelligence will result in unbounded costs` 可以直接當成設計原則：預設讓最強的模型處理所有步驟是成本最高的做法；把簡單步驟下放給便宜模型或傳統程式，是成本與可稽核性同時改善的一步。

## 後續追蹤

- Gartner 是否會在後續公開材料中補上起算基準（基準年或每個 workflow 的現行成本）。若補上，本則的預測就從方向性判斷變成可驗收的指標，值得回頭對照。
- 2026-10-21 之後的 Gartner IT Symposium/Xpo 仍有 Orlando 以外四場（Yokohama、Barcelona、Kochi 等） [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)；新聞稿預告會在這些場次進一步談 AI 經濟學，可追蹤是否出現帶基準的版本。
- 支撐本則的研究 `The Inference Paradox: Inference Tiering Is Critical to Protect Margins` 為客戶付費內容，本文未取得。若日後有公開摘要或方法說明，可補充核對其樣本與估算方式。
- `by 2027, organizations that prioritize semantics in AI-ready data will increase agentic AI accuracy by up to 80% and reduce costs by up to 60%` [(ref: trends)](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027) 這組上限值是否會出現典型值或對照基準，是觀察 Gartner 公開材料可驗收性的另一個指標。
- 醫療端值得追蹤的是：是否開始出現把「每份檢查的推論成本」與準確率並列報告的醫療 AI 研究。目前本書庫收錄的論文幾乎都只報準確率。
- **引用本則時的提醒** — 這則預測的機制可以用，數字不行。新聞稿全文沒有給起算基準 —— 沒有基準年、沒有單一 workflow 的現行成本、全頁 `$` 出現 0 次 —— 因此「逾五倍」是一個只有倍數、沒有被乘數的數字，無法進財務模型，也無法在 2028 年回頭判定它對了還是錯了；而全文的兩個「五倍」量的是完全不同的兩件事，標題那個是跨時間的（到 2028 年為止），後段那個是跨架構的（今天把聊天機器人換成代理式推論模型）。引用本則時請連同這兩點一起帶，不要單獨引用「五倍」 [(ref: pr)](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)。

## References

- `pr` — Gartner，[Gartner Predicts AI Inference Costs Per Agentic Workflow Will Increase More Than Fivefold Through 2028](https://www.gartner.com/en/newsroom/press-releases/2026-08-17-gartner-predicts-ai-inference-costs-per-agentic-workflow-will-increase-more-than-fivefold-through-2028)（官方新聞稿，發稿行 STAMFORD, Conn., August 17, 2026；JSON-LD `datePublished` 2026-08-17T03:30:00Z）。底 URL：`https://www.gartner.com/en/newsroom/press-releases/`
- `trends` — Gartner，[Gartner Identifies the Top Strategic Technology Trends for 2027](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-identifies-the-top-strategic-technology-trends-for-2027)（官方新聞稿，發稿行 ORLANDO, Fla., October 20, 2026；JSON-LD `datePublished` 2026-10-20T11:00:00Z）。底 URL：`https://www.gartner.com/en/newsroom/press-releases/`
- `day2` — Gartner，[Gartner IT Symposium/Xpo 2026 Orlando: Day 2 Highlights](https://www.gartner.com/en/newsroom/press-releases/2026-10-20-gartner-it-symposium-xpo-2026-orlando-day-2-highlights)（官方會議紀要，發稿行 ORLANDO, Fla., October 20, 2026；頁面無 NewsArticle JSON-LD，日期以發稿行為準）。底 URL：`https://www.gartner.com/en/newsroom/press-releases/`

[Home](../) · [Industry Watch](./)
