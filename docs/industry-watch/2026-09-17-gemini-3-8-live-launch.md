---
title: "Google 發布 Gemini 3.8 Live 系列：Extended Thinking 登上語音對語音評測榜首"
category: industry-watch
date: 2026-09-17
updated: 2026-09-17
tags: [Google, Gemini, voice-agent, speech-to-speech, benchmark, SynthID]
catalog_id: "google:gemini-3.8-live-launch-2026-09-15"
editors:
  - "Clare"
source:
  orgs:
    - "Google（Gemini Audio Team）"
  event: "發布 Gemini 3.8 Live 與 Gemini 3.8 Live Extended Thinking；後者以 82.6 分登上 Artificial Analysis Speech-to-Speech Index 首位"
  event_date: "2026-09-15"
  official_url: "https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/"
related_articles:
  - path: "2026-09-15-amodei-pace-the-frontier.md"
    relation: "9/12 各家（含 Google DeepMind）表態支持調速前沿，9/15 Google 照常發布新前沿語音模型的治理對照"
refs:
  goog:
    title: "Google 官方公告：Introducing Gemini 3.8 Live and 3.8 Live Extended Thinking（2026-09-15）"
    url: "https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/"
  aa:
    title: "Artificial Analysis：Speech to Speech Leaderboard"
    url: "https://artificialanalysis.ai/speech-to-speech"
  sa:
    title: "SiliconANGLE：Google's new speech model Gemini 3.8 Live supports real-time reasoning（2026-09-15）"
    url: "https://siliconangle.com/2026/09/15/googles-new-speech-model-gemini-3-8-live-supports-real-time-reasoning/"
status: published
skill_version: "write-industry-watch@2.7"
evidence_reviewed: true
---

**導覽：** [Home](../) · [Industry Watch](./)

# Google 發布 Gemini 3.8 Live 系列：Extended Thinking 登上語音對語音評測榜首

## 來源

- **組織**：Google（Gemini Audio Team）
- **事件**：發布兩款即時語音對話模型——**Gemini 3.8 Live**（面向規模與成本效率）與 **Gemini 3.8 Live Extended Thinking**（面向高複雜度任務）；後者在第三方評測機構 Artificial Analysis 的 Speech-to-Speech Quality Index 以 **82.6 分**居首位
- **日期**：**2026-09-15**
- **官方入口**：[Google 官方公告](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)

**編輯：** Clare

Google 在 2026 年 9 月 15 日發布兩款「即時語音對話」（live dialogue）模型：Gemini 3.8 Live 與 Gemini 3.8 Live Extended Thinking。兩者的共同賣點是**邊說邊做**——在對話持續進行的同時於背景執行工具與 API 呼叫，以及跨 97 種語言的對話中自動偵測與切換。Extended Thinking 版本並以 82.6 分登上 Artificial Analysis 的語音對語音品質指標榜首，領先 OpenAI 與 xAI 的旗艦語音模型。值得注意的時間點是：就在三天前，包括 Google DeepMind 執行長在內的多位 AI 領袖才公開表態支持「調速前沿」。

## 流程

1. **2026-09-12（背景）**：Anthropic 執行長 Dario Amodei 發表〈We Must Pace the Frontier〉，OpenAI、Google DeepMind、xAI 負責人表態支持放緩前沿 AI 開發（本庫已有專文：[AI 龍頭罕見同調](2026-09-15-amodei-pace-the-frontier.md)）。這是本次發布落地時的治理輿論環境——「調速」主張明言不等於停止發布，本則正是檢驗這句話的第一個實例。
2. **2026-09-15**：Google 於官方部落格發布兩款模型，公布各項評測成績、97 語言自動切換、背景工具執行、SynthID 浮水印與各通路上線時程 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。
3. **2026-09-15（同日）**：第三方評測機構 Artificial Analysis（下稱 AA）的 Speech-to-Speech Index 榜單顯示 Gemini 3.8 Live Extended Thinking (High) 以 82.6 分居首，領先第二名 GPT-Live-1（Astra, medium）的 81.5 與第三名 Grok Voice Think Fast 2.0 High 的 81.3 [(ref: aa)](https://artificialanalysis.ai/speech-to-speech)；科技媒體同日報導並補充 API 定價細節 [(ref: sa)](https://siliconangle.com/2026/09/15/googles-new-speech-model-gemini-3-8-live-supports-real-time-reasoning/)。
4. **2026-09-15 起（上線）**：開發者可經 Gemini API 與 Google AI Studio 使用；企業版在 Gemini Enterprise 私密預覽；一般使用者端 3.8 Live 進入 Search Live，Extended Thinking 進入 Gemini Live 與 Workspace（Docs、Gmail、Keep，依訂閱方案）[(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。

## 事實（可核對）

- **兩款模型的定位**：3.8 Live 面向規模與成本效率，結合對話智慧、流暢對話與即時視覺理解（visual grounding，即模型能參照鏡頭／畫面內容回應）；Extended Thinking 面向高複雜度任務，能**邊推理邊說話**，以「我查一下……」之類的口頭提示自然銜接多步驟背景任務 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。
- **評測成績（Google 公布、AA 榜單可獨立對照）**：Extended Thinking 在 Artificial Analysis Speech-to-Speech Quality Index 得 **82.6（第 1 名）**——該指標是語音推理、代理任務、人類偏好與任務成功率的加權平均 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/) [(ref: aa)](https://artificialanalysis.ai/speech-to-speech)；另有 τ-Voice **68.6%**、Sierra τ-Voice-banking **35.1%**、Big Bench Audio **97.7%** [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。3.8 Live 在 AA 同榜為 **76.0（第 5 名）**，並在人類偏好的 Speech Agent Arena 排第 2 [(ref: aa)](https://artificialanalysis.ai/speech-to-speech) [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。
- **97 種語言**：官方公告將「自動偵測並於對話中切換 97 種支援語言」寫在 3.8 Live 的段落；SiliconANGLE 報導則稱兩款模型皆支援 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/) [(ref: sa)](https://siliconangle.com/2026/09/15/googles-new-speech-model-gemini-3-8-live-supports-real-time-reasoning/)。
- **EVA-Bench**：Google 稱兩款模型在 ServiceNow 的語音代理評測 EVA-Bench 上推進了準確率與對話品質的取捨前緣（Pareto frontier），並註明該測試是在 Gemini Enterprise Agent Platform 的 Live API 上執行 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。
- **SynthID 浮水印**：所有 AI 生成音訊皆嵌入不可聽聞的 SynthID 浮水印，供事後偵測 AI 生成內容 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。
- **API 定價**（單源，待交叉驗證）：SiliconANGLE 報導 3.8 Live 音訊輸入約每分鐘 0.005 美元、輸出約每分鐘 0.018 美元；Extended Thinking 另計推理 token 與影像／文件輸入 [(ref: sa)](https://siliconangle.com/2026/09/15/googles-new-speech-model-gemini-3-8-live-supports-real-time-reasoning/)。
- **生態夥伴**：Agora、Fishjam、LangChain、LiveKit、Pipecat、Vercel、Vision Agents 等平台經 Gemini Live API 支援開發；Google 並點名 Salesforce、Genspark、Lumeris 等合作企業 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。

## 本書庫解讀（評論）

- **「榜首」要拆開讀。** 82.6 是可由第三方網站獨立對照的成績，不是純廠商宣稱，這點值得肯定；但領先第二名僅 1.1 分，而分項裡的 Sierra τ-Voice-banking（模擬銀行客服情境的任務成功率）只有 35.1%——把「綜合指標第一」直接翻譯成「語音代理可以上線接客了」是過度推論。在受監管、錯誤代價高的領域（金融、醫療），任務級成功率才是門檻指標。
- **對醫療 AI 讀者的橋接**：語音代理（voice agent，指以語音互動並能在背景呼叫工具的 AI 代理）常被期待用於掛號、衛教回覆、慢性病追蹤電話等場景。97 語言自動切換與即時視覺理解確實降低了多語系醫療場域的門檻，但銀行情境 35.1% 的任務成功率提醒我們：**從展示到受監管場景部署之間，還隔著任務級驗證這一關**——這與本庫先前整理的「研究指標 ≠ 上市門檻」是同一件事。另外，SynthID 讓 AI 生成語音可被事後辨識，對醫病通話紀錄的可稽核性是有意義的基礎設施。
- **治理對照**：9 月 12 日 Google DeepMind 執行長才公開支持「調速前沿」，9 月 15 日 Google 照常發布新前沿語音模型——這不必然矛盾（該倡議明言 pacing 不等於停止發布），但它把觀察點變得很具體：後續值得看的是這類發布的安全說明與 model card 是否出現承諾中的第三方查核痕跡，而不是發布節奏本身。

## 產業／生態影響

- 語音代理基礎設施（LiveKit、Pipecat 等串流平台）成為大廠模型的標準發行通路，開發者的切換成本進一步下降 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)。
- 語音模型競爭焦點從「聽得懂、說得順」移到**邊說邊做**（背景工具執行＋進度口述）與按分鐘計價的成本結構 [(ref: goog)](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/) [(ref: sa)](https://siliconangle.com/2026/09/15/googles-new-speech-model-gemini-3-8-live-supports-real-time-reasoning/)。
- AA 榜單前三名分屬 Google、OpenAI、xAI，差距在 1.3 分內，語音對語音的榜首位置預期將高頻輪替 [(ref: aa)](https://artificialanalysis.ai/speech-to-speech)。

## 與書庫其他文章的關係

一句話敘述關係: [AI 龍頭罕見同調：Amodei 發表〈We Must Pace the Frontier〉，OpenAI、DeepMind、xAI 表態支持](2026-09-15-amodei-pace-the-frontier.md) 記錄 9/12 的調速倡議；本則是倡議之後第一個大廠前沿模型發布的實例，可作治理承諾與發布行為的對照觀察。

## 實務的啟發

1. 選語音模型看**分項**而非總分：語音推理、代理任務成功率、對話動態（插話／輪替處理）與延遲各自對應不同場景，AA 的分項圖比單一指標有用。
2. 受監管場景（醫療、金融）先做**任務級評測**再談上線：拿自己場景的真實任務腳本測成功率，35.1% 與 97.7% 之間的落差就是「展示」與「部署」的距離。
3. 留意語音浮水印：SynthID 之類的機制讓「這段話是 AI 說的」可被驗證，設計通話紀錄與稽核流程時可以主動利用。

## 後續追蹤

- API 定價的官方文件交叉驗證（目前僅 SiliconANGLE 單源）。
- AA 榜單變動：OpenAI／xAI 是否短期內反超。
- Gemini Enterprise 從私密預覽到正式開放的時程，以及是否出現醫療場景導入案例。
- 對照 9/12 調速承諾：後續發布的 model card 是否出現第三方查核（embedded evaluators）相關記載。

## References

- **goog** — [Google：Introducing Gemini 3.8 Live and 3.8 Live Extended Thinking（2026-09-15）](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-8-live-gemini-3-8-live-extended-thinking/)
- **aa** — [Artificial Analysis：Speech to Speech Leaderboard](https://artificialanalysis.ai/speech-to-speech)
- **sa** — [SiliconANGLE：Google's new speech model Gemini 3.8 Live supports real-time reasoning（2026-09-15）](https://siliconangle.com/2026/09/15/googles-new-speech-model-gemini-3-8-live-supports-real-time-reasoning/)

**導覽：** [Home](../) · [Industry Watch](./)
