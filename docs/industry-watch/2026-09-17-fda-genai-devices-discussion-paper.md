---
title: "FDA 徵求 GenAI 醫材監管意見：討論文件≠指引"
category: industry-watch
date: 2026-09-17
updated: 2026-09-17
tags: [FDA, GenAI, SaMD, CDRH, DHCoE, regulation, discussion-paper]
catalog_id: "fda:genai-devices-discussion-paper-2026-08-18"
editors:
  - "Curitis"
source:
  orgs:
    - "U.S. Food and Drug Administration (FDA)"
  event: "Discussion paper and request for feedback on generative AI-enabled medical devices (docket FDA-2026-N-7874)"
  event_date: "2026-08-18"
  official_url: "https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices"
related_articles:
  - path: "./2026-09-15-fda-cardio-ml-notification.md"
    relation: "same FDA CDRH SaMD track; Class II final order vs GenAI discussion paper"
  - path: "../ai-basics/multi-agent-llm.md"
    relation: "paper defines agentic AI and seeks extra evaluation considerations"
  - path: "../ai-papers/2026-09-17-medical-llm-evaluation-gap.md"
    relation: "research evidence gap for agentic medical LLM vs emerging regulatory framing"
refs:
  press:
    title: "FDA Seeks Public Feedback to Inform Regulatory Approach for Generative AI-Enabled Medical Devices"
    url: "https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices"
  hub:
    title: "Considerations for the Regulation of Generative AI-Enabled Medical Devices: Discussion Paper and Request for Feedback"
    url: "https://www.fda.gov/medical-devices/digital-health-center-excellence/considerations-regulation-generative-ai-enabled-medical-devices-discussion-paper-and-request"
  pdf:
    title: "Discussion paper PDF (FDA media/194242)"
    url: "https://www.fda.gov/media/194242/download"
  dhac_exec:
    title: "DHAC Executive Summary: Total Product Lifecycle Considerations for Generative AI-Enabled Devices"
    url: "https://www.fda.gov/media/182871/download"
  dhac_meeting:
    title: "November 20-21, 2024 Digital Health Advisory Committee Meeting Announcement"
    url: "https://www.fda.gov/advisory-committees/advisory-committee-calendar/november-20-21-2024-digital-health-advisory-committee-meeting-announcement-11202024"
  pccp:
    title: "Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions"
    url: "https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial-intelligence"
status: published
skill_version: "write-industry-watch@2.7"
evidence_reviewed: true
---

**導覽：** [Home](../) · [Industry Watch](./)

# FDA 徵求 GenAI 醫材監管意見：討論文件≠指引

## 來源

- **組織**：美國 FDA（Food and Drug Administration）；由 **CDRH**（Center for Devices and Radiological Health，器械與放射健康中心）下的 **DHCoE**（Digital Health Center of Excellence，數位健康卓越中心）主導
- **事件**：發布 *Considerations for the Regulation of Generative AI-Enabled Medical Devices* **討論文件（discussion paper）** 並公開徵求意見；文件明文**不是**草案或最終指引，也**不**提出或實施政策變更
- **日期**：新聞稿 **2026-08-18**；意見截止 **2026-10-19**（docket **FDA-2026-N-7874**，Regulations.gov）
- **官方入口**：[FDA 新聞稿](https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices) · [DHCoE 討論文件頁](https://www.fda.gov/medical-devices/digital-health-center-excellence/considerations-regulation-generative-ai-enabled-medical-devices-discussion-paper-and-request) · [討論文件 PDF](https://www.fda.gov/media/194242/download)

**編輯：** Curitis

FDA 在 2026 年 8 月就「生成式 AI（GenAI）賦能的醫療器材」公開徵求意見：重點是風險評估、上市前評估、上市後監測，以及基礎模型／代理式系統等議題。這份討論文件是**早期意見蒐集**，不是已生效的法規要求；讀新聞標題時，勿把它當成已定稿的 guidance。

## 流程

1. **2024-11-20～21**：CDRH 召開 **Digital Health Advisory Committee（DHAC，數位健康諮詢委員會）** 公開會議，主題為 GenAI 賦能裝置的 **total product life cycle（TPLC，產品全生命週期）** 考量；會前 Executive Summary 已點出風險分級與有效科學證據兩大挑戰。此會議與摘要是本案討論文件的**直接前身**，不是旁枝背景 [(ref: dhac_meeting)](https://www.fda.gov/advisory-committees/advisory-committee-calendar/november-20-21-2024-digital-health-advisory-committee-meeting-announcement-11202024) [(ref: dhac_exec)](https://www.fda.gov/media/182871/download) [(ref: pdf)](https://www.fda.gov/media/194242/download)。
2. **2026-08-18**：FDA 發布討論文件與新聞稿，由 DHCoE 主導，就 GenAI 賦能醫材的監管考量公開徵求利害關係人意見 [(ref: press)](https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices) [(ref: hub)](https://www.fda.gov/medical-devices/digital-health-center-excellence/considerations-regulation-generative-ai-enabled-medical-devices-discussion-paper-and-request)。
3. **至 2026-10-19**：意見提交至 Regulations.gov docket **FDA-2026-N-7874**；文件允許只回答部分問題 [(ref: press)](https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices) [(ref: hub)](https://www.fda.gov/medical-devices/digital-health-center-excellence/considerations-regulation-generative-ai-enabled-medical-devices-discussion-paper-and-request)。

## 事實（可核對）

- **文件定位**：僅供討論；**不**代表草案或最終指引；**不**提出或實施 CDRH 對 GenAI 賦能裝置的政策變更；**不**傳達擬議／最終的監管期望（含未來上市申請應附證據）；**不**處理討論中的做法是否落在既有法定權限內 [(ref: pdf)](https://www.fda.gov/media/194242/download) [(ref: hub)](https://www.fda.gov/medical-devices/digital-health-center-excellence/considerations-regulation-generative-ai-enabled-medical-devices-discussion-paper-and-request)。
- **監管對象**：FDA **不**「監管 GenAI 本身」，而是監管符合《聯邦食品、藥品與化粧品法》（FD&C Act）裝置定義的產品（含 GenAI 賦能裝置）；採風險基礎、並強調 TPLC [(ref: pdf)](https://www.fda.gov/media/194242/download)。
- **GenAI 裝置特性（文件描述）**：可能接受開放式輸入、執行多子任務、對相似輸入產出**可變輸出**；可能透過底層模型、提示、檢索、護欄、編排邏輯或介面等持續演進；常建於第三方 **foundation model（基礎模型）**，訓練資料／架構／評估透明度不一 [(ref: pdf)](https://www.fda.gov/media/194242/download)。
- **風險：雙軸啟發式**：一軸是裝置活動（從非指示性資訊 → 行動導向資訊 → 採取行動／自主程度）；另一軸是依賴錯誤輸出的**危害後果嚴重度**；風險大致由左下往右上升高。文件另討論病患端 vs 醫療專業人員（HCP）端、全科 vs 專科、多輪對話中功能漂移、以及急診升級的**低升級／過升級**雙向誤差 [(ref: pdf)](https://www.fda.gov/media/194242/download) [(ref: press)](https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices)。
- **上市前：能力導向（competency-based）評估構想**：高階靈感來自醫師訓練／認證，但需適配醫材法規；評估對象是**最終面向使用者的裝置配置**，不是單獨的基礎模型。構想含（1）**裝置基準測試（device benchmarking）**——安全、臨床熟練度、可泛化性，以及僅適用於代理式裝置的能力；（2）**臨床確認（clinical confirmation）**——未必每案都要前瞻臨床試驗，可依風險選用回溯評估、影子部署、標準化病患互動、臨床醫師裁決、前瞻研究等 [(ref: pdf)](https://www.fda.gov/media/194242/download)。
- **上市後監測與變更**：文件討論是否可用更強的上市後監測換取較大的上市前不確定性；例示含定期重做基準測試、樣本式臨床醫師審查、效能退化／漂移監測。變更可能含贊助者主動更新、裝置設計為持續學習的**模型演進**，以及**第三方基礎模型**發起的變更；**Predetermined Change Control Plan（PCCP，預定變更控制計畫）**被提及為可能機制之一，並指向既有 AI 裝置 PCCP 指引 [(ref: pdf)](https://www.fda.gov/media/194242/download) [(ref: pccp)](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial-intelligence)。
- **其他議題**：徵求對自願性 **Foundation Model Device Master File（MAF，裝置主檔）** 的可行性意見；並定義 **agentic AI systems（代理式 AI 系統）** 為可自主規劃／執行多步驟任務、使用外部工具或跨步驟採取行動的 GenAI 賦能系統，詢問是否需額外評估考量 [(ref: pdf)](https://www.fda.gov/media/194242/download)。
- **意見截止**：2026-10-19；docket **FDA-2026-N-7874** [(ref: press)](https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices)。

## 本書庫解讀（評論）

- **對產品／法規讀者**：這是**意見蒐集框架**，不是「現在就要照這套交案」。把討論文件的雙軸風險或能力導向評估寫進標示／行銷，容易被誤讀成已生效期望；正確對齊點是：意見截止前可針對自己產品架構回答問題，同時仍遵守既有裝置路徑與既有 AI 相關指引（例如 PCCP）。
- **對研究筆記讀者**：學術管線裡的 LLM／代理評測（基準、離線 benchmark）與「若該功能落入裝置定義後，FDA 正在討論的上市前／上市後證據」不是同一關。差在：研究可只報準確率；討論文件則把**範圍外拒絕、急診升級雙向誤差、影子部署、第三方模型變更**等放到同一張風險—證據桌上。
- **代理式系統**：文件把 agentic 能力單獨列為基準測試元素，並點出多步驟行動、工具使用、人為覆核機會減少等額外風險。這與書庫裡多代理／agentic 研究成長快、但前瞻證據相對稀少的觀察可對讀——一邊是研究供給結構，一邊是監管端開始點名的評估維度。

## 產業／法規生態影響

- 製造商與基礎模型供應商可能被捲入同一對話：前者要證明**裝置**安全有效；後者若採自願 MAF，可能影響多家下游申請的審查資訊基礎——但仍**不**等於模型本身獲准用於任一預期用途。
- 依賴第三方模型 API 的產品，需提早設計「模型版本變更如何偵測、評估、是否觸發新申請／PCCP」的合約與技術機制；文件已把這類變更列為明確問題。
- 意見截止（2026-10-19）前的產業回覆，可能影響後續是否出現草案指引或新證據期望；在那之前，不宜把討論文件當 checklist 對外承諾合規。

## 與書庫其他文章的關係

一句話敘述關係: [FDA 將心血管 ML 通知軟體定為 Class II：通報≠診斷](./2026-09-15-fda-cardio-ml-notification.md) 同屬 CDRH 對 AI／ML 醫材的成文或準則脈絡；該則是已編入 21 CFR 的 Class II **最終命令**，本則是 GenAI 裝置的**討論文件／徵求意見**，尚未成為指引或規則。

一句話敘述關係: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md) 說明多代理／工具編排概念；本則補上 FDA 對 agentic GenAI 賦能裝置是否需額外評估的官方徵求問題。

一句話敘述關係: [醫療 LLM 評估落差：研究更嚴謹，為何證據反而更舊？](../ai-papers/2026-09-17-medical-llm-evaluation-gap.md) 從文獻地圖顯示 agentic／multi-agent 醫療研究成長快、trial-grade 證據相對稀少；本則對應監管端開始把代理式能力與上市後監測寫進討論框架。

一句話敘述關係: [FDA 駁回放射科 AI 免 510(k) 請願：既有 clearance 不是後續產品的通行證](./2026-09-18-fda-radiology-cad-510k-exemption-denied.md) 本則徵求 GenAI 醫材監管意見、探索未來框架，該則則是 FDA 在具體請願上守住現行 510(k) 關卡的定案。

## 實務的啟發

1. 先確認產品是否落入**裝置定義**與哪一類軟體功能；文件一再強調 FDA 不監管「GenAI 技術本身」。
2. 寫**預期用途（intended use）**與輸出語氣時，對齊雙軸思維：是非指示性資訊、行動導向建議，還是直接採取診斷／處方等行動——並區分病患端與 HCP 端。
3. 驗證計畫預留：基準測試元素（含範圍外拒絕、升級雙向誤差）、臨床確認路徑（含影子部署等），以及第三方模型變更的監測／PCCP 選項——即使目前仍屬討論階段，這些問題已寫進官方徵求清單。
4. 讀 PDF 免責與新聞稿截止日；二手標題常省略「discussion paper ≠ guidance」。

## 後續追蹤

- Docket FDA-2026-N-7874 截止後，FDA 是否彙整回覆或發布後續草案指引。
- 自願 Foundation Model MAF 是否出現可操作的提交慣例或產業試點。
- PCCP 概念如何被進一步適配「無法完全預先指定」的 GenAI 變更與第三方模型更新。

## References

- **press** — [FDA 新聞稿：Seeks Public Feedback… Generative AI-Enabled Medical Devices（2026-08-18）](https://www.fda.gov/news-events/press-announcements/fda-seeks-public-feedback-inform-regulatory-approach-generative-ai-enabled-medical-devices)
- **hub** — [DHCoE：Discussion Paper and Request for Feedback 入口頁](https://www.fda.gov/medical-devices/digital-health-center-excellence/considerations-regulation-generative-ai-enabled-medical-devices-discussion-paper-and-request)
- **pdf** — [討論文件 PDF（fda.gov/media/194242）](https://www.fda.gov/media/194242/download)
- **dhac_exec** — [DHAC Executive Summary：TPLC Considerations for Generative AI-Enabled Devices](https://www.fda.gov/media/182871/download)
- **dhac_meeting** — [2024-11-20～21 DHAC 會議公告](https://www.fda.gov/advisory-committees/advisory-committee-calendar/november-20-21-2024-digital-health-advisory-committee-meeting-announcement-11202024)
- **pccp** — [FDA guidance：PCCP for AI-Enabled Device Software Functions](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/marketing-submission-recommendations-predetermined-change-control-plan-artificial-intelligence)

**導覽：** [Home](../) · [Industry Watch](./)
