---
title: "OpenAI 發布 GPT-6.1 Sol：五分之一價格逼近 Astra，但科學研究那一欄仍由 Astra 領先"
category: industry-watch
date: 2026-10-07
updated: 2026-10-07
tags: [OpenAI, GPT-6.1-Sol, pricing, agentic-coding, computer-use, benchmark, factuality]
catalog_id: "openai:introducing-gpt-6-1-sol"
editors:
  - "Clarence"
source:
  orgs:
    - "OpenAI"
  event: "發布 GPT-6.1 Sol：標準輸入與輸出 token 價格為 GPT-6 Astra 的五分之一，官方稱在 agentic coding、computer use 與 professional work 三個方向上「幾乎媲美」Astra"
  event_date: "官方公告頁未標示發布日期"
  official_url: "https://openai.com/index/introducing-gpt-6-1-sol/"
related_articles:
  - path: "2026-09-17-gemini-3-8-live-launch.md"
    relation: "同為大廠前沿模型發布，兩則可對照「廠商自報評測＋價格」這種發布敘事的可核對程度差異"
  - path: "2026-09-15-amodei-pace-the-frontier.md"
    relation: "調速倡議之後的又一次前沿發布，延續治理承諾與發布行為的對照觀察"
refs:
  oai:
    title: "OpenAI：Introducing GPT-6.1 Sol（官方公告）"
    url: "https://openai.com/index/introducing-gpt-6-1-sol/"
status: published
skill_version: "write-industry-watch@2.8"
evidence_reviewed: true
---

[Home](../) · [Industry Watch](./)

# OpenAI 發布 GPT-6.1 Sol：五分之一價格逼近 Astra，但科學研究那一欄仍由 Astra 領先

## 來源

- **組織**：OpenAI
- **事件**：發布 **GPT-6.1 Sol**（API 模型名 `gpt-6.1-sol`），為 GPT-6 Sol 的升級版。官方標題句為「near-Astra intelligence for a fifth of the price」，並說明其在 **agentic coding、computer use 與 professional work** 上幾乎媲美 GPT-6 Astra，而標準輸入與輸出 token 價格為 Astra 的五分之一 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)
- **日期**：**官方公告頁未標示發布日期**，OpenAI 的 news 列表亦未對本則標註日期；本文因此不引述發布日。可確認的時間錨點是公告寫明「即日起」在各通路提供，且同頁「繼續閱讀」列出的前一代公告 *Introducing GPT-6 Sol and Luna* 日期為 2026-09-22 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)
- **官方入口**：[OpenAI：Introducing GPT-6.1 Sol](https://openai.com/index/introducing-gpt-6-1-sol/)
- **單源**：本則目前僅有 OpenAI 官方公告一個來源，所有評測成績與價格皆為廠商自報，**單源，待交叉驗證**

**編輯：** Clarence

OpenAI 發布 GPT-6.1 Sol，把「接近旗艦的能力」與「五分之一的價格」綁在同一個型號上：標準輸入每百萬 token 2 美元、輸出 10 美元，正好是 GPT-6 Astra 的五分之一；快取輸入 0.10 美元，比自身標準輸入低 95%。官方公布五組評測，其中 coding、professional work、computer use 三項確實把差距壓到接近 Astra；但在第四項 **Terminal-Bench Science 0.1** 上，OpenAI 自己寫明 **Astra 仍以 68.1% 居受測模型之首，最困難的科學研究任務應使用 Astra**。把這次發布讀成「四個領域全面逼近旗艦」會讀錯一欄。

## 背景

1. **2026-09-03**：OpenAI 發布 GPT-6 Astra（同頁「繼續閱讀」標示日期），定位為「我們最聰明的模型」[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
2. **2026-09-22**：OpenAI 發布 GPT-6 Sol 與 GPT-6 Luna（同頁標示日期），確立 Astra／Sol／Luna 的三層產品線 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
3. **本次（日期未標示）**：發布 GPT-6.1 Sol，為 GPT-6 Sol 的升級版，同時調整 Sol 層的價格與快取定價，並預告數日內推出 **GPT-6.1 Sol Ultrafast**，在 Codex 中的 token 生成速度最高可達標準速度的 8 倍 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。

## 事實（可核對）

以下數值全部取自 OpenAI 官方公告頁，單位與分母依原文保留。

### 價格（每百萬 token）

| 模型 | 輸入 | 輸出 | 快取輸入 |
|---|---:|---:|---:|
| GPT-6 Astra | $10.00 | $50.00 | $1.00 |
| **GPT-6.1 Sol** | **$2.00** | **$10.00** | **$0.10** |
| GPT-6 Luna | $0.10 | $0.50 | $0.01 |

[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)

- **五分之一指的是標準輸入與輸出的掛牌價**（$2 對 $10、$10 對 $50），不是每項任務的實際成本比；後者依評測而異，見下節。
- **快取輸入 $0.10**：比自身標準輸入低 95%，比 GPT-6 Sol 的快取輸入低 50%。官方把這一項連結到「讓開發者有餘裕建構會跨請求重用上下文的 agent」[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。

### 五組評測

官方公告以**相對差距**（百分點、成本倍數）呈現，**除 Astra 在 Terminal-Bench Science 0.1 的 68.1% 外，未公布各模型的絕對分數**。

| 評測 | 官方陳述 | 成本對照 |
|---|---|---|
| **DeepSWE v1.1**（coding，真實程式碼庫的長程軟體工程任務） | 與 GPT-6 Astra 表現相同；比 GPT-6 Sol 的最佳成績高 **6.4 個百分點**，且推理強度與成本更低 | 約為 Astra 的 **1/5** |
| **GDP.pdf**（professional work，依複雜 PDF 回答專業問題；文件取自金融、**醫療保健**、法律及其他七個專業領域） | 在所有受測推理設定下皆高於 Opus 5.5（含備援機制）；接近 Astra 的頂尖水準 | 不到 Opus 5.5 的一半；約為 Astra 的 **1/5** |
| **AutomationBench 1.0.6**（多步驟業務流程，涵蓋 sales／marketing／operations／support／finance／HR 的 47 種工具） | 推理強度「中」時比 Opus 5.5 高 **2.2 個百分點**；比同設定的 GPT-6 Sol 高 **4.8 個百分點** | 約為 Opus 5.5 的 **1/3** |
| **OSWorld 2.0**（computer use，v2026.08.08 離線測試集的 partial reward） | 最高推理強度下比 GPT-6 Sol 高 **7 個百分點**；與 Astra 差距 **2.1 個百分點** | 不到 GPT-6 Sol 的一半；約為 Astra 的 **1/7** |
| **Terminal-Bench Science 0.1**（科學工作流程：資料分析、模擬、定理證明） | 最高推理強度下超過 GPT-6 Sol 得分的 **兩倍**；**Astra 仍以 68.1% 為受測模型最高分** | 每項任務平均 **$5.47**，Opus 5.5 為 **$23.21**、Astra 為 **$23.80**（低逾 75%） |

[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)

- **OpenAI 自己標註的一項比較限制**：AutomationBench 圖中 Claude Fable 5.1 的數據**低估實際成本**，因為未計入備援機制（fallback）的成本，而約 **40%** 的任務曾啟用備援機制 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- **科學研究那一欄的官方原話**：「GPT-6 Astra still achieves the highest score among the models tested at 68.1%, and should be used for the most difficult scientific research tasks.」[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)

### 事實正確性（factuality）

- 相較 GPT-6 Sol，提升幅度最大者在**低**推理強度：含有事實錯誤的回答比例由 **11.4% 降至 7.7%**，降幅約 **32%** [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- 在各受測推理強度下，其錯誤率與 GPT-6 Astra 的差距維持在 **1.9 個百分點**以內，而每項任務成本不到 Astra 的五分之一 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- **分母定義**：這項評測使用經去識別化、且使用者曾指出前一代模型事實錯誤的 ChatGPT 對話，衡量「回答中含有至少一項事實錯誤」的比例。OpenAI 兩度聲明這些是**刻意挑選的高難度提示，不代表一般使用情況** [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。

### 安全與對齊

- 官方稱在對齊評測上比 GPT-6 Sol 大幅進步、更接近 Astra；具體列出三類：告知搜尋工具故障、遵守明確限制、避免在 agentic 任務中產生未經授權的結果 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- **搜尋工具故障時未告知使用者的比例**：GPT-6.1 Sol **2.1%**、GPT-6 Sol **4.9%**、GPT-6 Astra **1.5%**、GPT-6 Luna **28.7%**（最高推理強度；官方註明為刻意挑選的易失敗任務）[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- 未觀察到試圖繞過自動化安全審查機制的行為，與 Astra 及 GPT-6 Sol 一致；完整資訊在 GPT-6.1 Sol system card addendum [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。

### 供應情況

- 即日起對 **Plus、Pro、Business、Enterprise、Edu** 使用者在 **ChatGPT Work 與 Codex** 中提供；**尚未在 Chat 中提供** [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- 開發者可經 OpenAI API 以 `gpt-6.1-sol` 存取 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- 官方並聲明：GPT 的評測在其研究環境或經 API 進行，因系統提示、可用工具、推理強度不同，輸出可能與正式版 ChatGPT 略有差異；**競爭對手模型的評測結果取自公開報告**，非由 OpenAI 重跑 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。

## 本書庫解讀（評論）

- **「逼近旗艦」是三個方向的宣稱，不是四個。** 官方的標題句明確限定在 agentic coding、computer use 與 professional work；科學研究是第四組評測，但結論相反 —— Astra 以 68.1% 居首，OpenAI 自己建議最困難的科學任務用 Astra。對研究單位而言，這一欄反而是最該看清楚的：**便宜五倍的是日常代理工作，不是最難的科學推理**。
- **相對數字讀起來漂亮，但缺少絕對分數。** 除了 Astra 的 68.1%，五組評測全部只給百分點差距與成本倍數。沒有絕對分數就無法判斷「高 6.4 個百分點」是從 40% 到 46.4% 還是從 80% 到 86.4% —— 前者意味兩個模型都還不堪用，後者才是接近可用。這不是指控，而是提醒：**自報評測若只給差距，外部無法評估門檻**。
- **競品數字取自公開報告，不是同場重跑。** OpenAI 在頁尾聲明對手成績取自公開報告；同時又在 AutomationBench 處主動註記 Claude Fable 5.1 的成本被低估。兩者並列的意思是：跨廠商成本比較的基準並不齊平，引用時應連同這個限制一起引。
- **factuality 的改善不宜外推到臨床。** 11.4% → 7.7% 是在「使用者曾指出前代錯誤的對話」上量到的，OpenAI 兩次聲明不代表一般使用。醫療場域關心的是**特定臨床任務上的錯誤率與漏判代價**，與這個分母無關；把 32% 降幅講成「幻覺少了三成所以可以用在醫療」是跨族群的誤讀。
- **對醫療 AI 讀者最直接的一欄是 GDP.pdf。** 它的文件來源明列 healthcare，測的是「依含表格、圖表、示意圖與小字的複雜 PDF 回答專業問題」—— 這正是保險審查、臨床指引比對、器材說明書查核這類工作的形狀。但官方同樣只給了相對位置（高於 Opus 5.5、接近 Astra），沒有絕對準確率，因此仍不足以作為導入判斷的依據。

## 產業／生態影響

- **價格分層的競爭轉向「中階逼近旗艦」。** Astra／Sol／Luna 三層中，這次調整的是中階；以 1/5 掛牌價承接旗艦的多數日常代理工作，等於把旗艦壓縮到「最難的任務」這個較窄的位置 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- **快取輸入成為 agent 成本結構的關鍵項。** $0.10／百萬 token（比自身標準輸入低 95%）直接指向需要跨請求重用上下文的長時程 agent；這類工作負載的實際成本將更取決於快取命中率而非掛牌單價 [(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。
- **評測焦點明顯移向 agentic 與成本效率。** 五組評測有四組是 agent 形式（真實程式碼庫、業務流程、電腦操作、終端機科學工作流程），且全部附上每項任務成本 —— 比較的單位正在從「分數」變成「分數／成本」[(ref: oai)](https://openai.com/index/introducing-gpt-6-1-sol/)。

## 與書庫其他文章的關係

同為大廠前沿模型發布，但兩則的可核對程度不同：Gemini 3.8 Live 的榜首成績可在第三方 Artificial Analysis 榜單獨立對照，本則的五組評測則全部是廠商自報且多數未給絕對分數: [Google 發布 Gemini 3.8 Live 系列：Extended Thinking 登上語音對語音評測榜首](2026-09-17-gemini-3-8-live-launch.md)

調速倡議之後又一次前沿發布，可延續「治理承諾與發布行為是否一致」的對照觀察，本則的觀察點落在 system card addendum 與自報評測的揭露程度: [AI 龍頭罕見同調：Amodei 發表〈We Must Pace the Frontier〉，OpenAI、DeepMind、xAI 表態支持](2026-09-15-amodei-pace-the-frontier.md)


同為大廠自報成果的發布敘事：本則的落差在標題句只涵蓋四項評測中的三項，該則的落差在標題用現在進行式概括了四個尚未完成的案例，兩則屬同一種閱讀問題: [Google 公布 MedGemma 全球落地案例：五個合作案裡只有一個報出已完成的篩檢量](2026-10-08-medgemma-global-deployment-claims.md)
## 實務的啟發

1. **先問絕對分數再談採用。** 面對只給百分點差距的發布，導入評估的第一個問題應該是「基準線在哪」。拿不到絕對分數時，用自家任務重跑小規模對照，比引用廠商差距有意義得多。
2. **成本要算每項任務，不是掛牌價。** 同一次發布裡，相對 Astra 的成本比在 coding 是 1/5、computer use 是 1/7、科學研究是「低逾 75%」—— 掛牌價的 1/5 只是起點，實際比值由推理強度與任務長度決定。
3. **把快取命中率納入 agent 的成本模型。** 快取輸入與標準輸入差 95%，長時程 agent 的成本差異會主要來自上下文重用設計，而不是選哪個型號。
4. **跨廠商比較要檢查備援成本是否計入。** OpenAI 自己揭露約 40% 的任務啟用過 fallback 而對手成本未計入 —— 自行比價時，把重試、降級與人工接手的成本一併算進去。
5. **醫療用途看 GDP.pdf 的形狀而非分數。** 該評測的任務形態（複雜 PDF、表格與小字、專業提問）與醫療文件作業高度相似，值得用自家的審查件、指引與說明書做一組同形態的內部評測。
6. **factuality 指標要連分母一起引。** 這組數字來自刻意挑選的易錯對話，不是一般使用的錯誤率；在任何對外說明中單獨引用 7.7% 都會失真。

## 後續追蹤

- 絕對分數與完整評測表：是否在 system card addendum 或後續技術文件中公布。
- 發布日期：官方公告頁與 news 列表目前皆未標示，後續是否補上。
- GPT-6.1 Sol Ultrafast 的實際上線時間與定價（公告稱數日內、Codex 中最高 8 倍生成速度）。
- 第三方獨立評測（如 Artificial Analysis 等）是否出現可與本則對照的數據。
- 是否開放至 ChatGPT 的 Chat 介面（目前僅 ChatGPT Work 與 Codex）。

## References

- **oai** — [OpenAI：Introducing GPT-6.1 Sol（官方公告）](https://openai.com/index/introducing-gpt-6-1-sol/)。含價格表（Astra／Sol／Luna 三層）、五組評測（DeepSWE v1.1、GDP.pdf、AutomationBench 1.0.6、OSWorld 2.0、Terminal-Bench Science 0.1）、factuality、安全與對齊評測、定價與供應情況，以及評測方法聲明。本則所有數值均出自此頁。

[Home](../) · [Industry Watch](./)
