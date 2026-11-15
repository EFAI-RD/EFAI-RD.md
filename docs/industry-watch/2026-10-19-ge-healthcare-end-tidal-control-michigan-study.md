---
parent: Industry Watch
nav_exclude: true
title: "ETC 自動調控麻醉氣體：密西根大學 12,818 例回溯研究"
category: industry-watch
date: 2026-10-19
updated: 2026-11-12
tags: [GE-HealthCare, University-of-Michigan, End-tidal-Control, anesthesia, clinical-workflow, closed-loop-automation, real-world-evidence, adoption, sustainability, retrospective-study]
catalog_id: "ge-healthcare:end-tidal-control-michigan-study-2026-10-16"
editors:
  - "Clarence"
source:
  orgs:
    - "GE HealthCare"
    - "University of Michigan"
  event: "發布新聞稿宣傳一篇在 A&A Practice 刊出的密西根大學回溯性觀察研究，稱 End-tidal Control 軟體的使用與吸入麻醉新鮮氣體流量下降 62.3%、sevoflurane 用量下降 39.3% 相關"
  event_date: "2026-10-16"
  official_url: "https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow"
related_articles:
  - path: "2026-10-15-ge-healthcare-mgb-genai-radiation-therapy.md"
    relation: "同一家公司相隔三天的兩則發布，都在談工作流程的量化改善，但證據層級不同：該則的放療合作仍在探索階段，本則有一篇開放取用的同儕審查論文可供逐項回查。兩則引用的關鍵數字都帶有原文的限定條件，轉述時都需要回到原處確認"
  - path: "2026-10-13-siemens-accela-radiotherapy-launch.md"
    relation: "兩則都缺少讀者自行設定驗收門檻所需的那個數字，但缺法相反，該則給了九個全為上下限、沒有典型值也沒有對照機型的規格，本則給的 62.3% 恰恰就是論文算出來的典型值，只是新聞稿沒說它是模型對一位虛構病人的推算"
  - path: "2026-10-08-medgemma-global-deployment-claims.md"
    relation: "兩則都在回答「落地之後能量到什麼」：該則的五個合作案以部署階段與使用場景描述進展，本則則用電子病歷與麻醉機既有的使用紀錄，把採用率、逐位臨床人員的使用分布與變異來源拆解出來。兩則並讀可以看出落地評估的粒度差異，往往取決於現場有沒有既存的量測資料"
  - path: "2026-10-20-google-amie-lancet-primary-care-feasibility.md"
    relation: "兩則都是廠商宣傳一篇數值本身正確的論文，而被省略的限定條件種類不同，本則省略的是「這兩個百分比是論文為一位虛構典型病人以調整後模型推算的差異」，該則省略的是「90% 指的是七項鑑別診斷清單之內命中、排第一名只有 56%」"
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "本則是本書庫目前最接近完整部署評估的樣本，事先寫明三個假設、並在其中一個未達自訂門檻時照實報出；該則恰好是相反的作法，技術報告自述最終規格是在看過結果之後才設定的，而按原規格最後一輪 113 個 scFv 設計沒有一個以實測解離常數通過，兩則並讀可以看出「終點什麼時候定」這件事如何決定一份成果該被當成驗證還是當成探索"
refs:
  pr:
    title: "GE HealthCare：Research conducted at University of Michigan published in Anesthesia & Analgesia Practice demonstrates GE HealthCare End-tidal Control software may help to reduce fresh gas flow（官方新聞稿）"
    url: "https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow"
  paper:
    title: "McBride J 等：Utilization and Estimation of Environmental Impact of End-Tidal Control in a Multisite Academic Health System: A Retrospective Observational Cross-Sectional Study（A&A Practice，開放取用全文）"
    url: "https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of"
status: published
skill_version: "write-industry-watch@3.1"
evidence_reviewed: true
---

[Home](../) · [Industry Watch](./)

# ETC 自動調控麻醉氣體：密西根大學 12,818 例回溯研究

## 來源

- **組織** — **GE HealthCare**（新聞稿發布方）與 **University of Michigan**（研究執行機構）。新聞稿具名兩位發言人：GE HealthCare 的 Patient Care Solutions 事業部門醫務長、麻醉科醫師 John Beard, MD，以及密西根大學麻醉學副教授 Douglas A. Colquhoun, MB ChB, MSc, MPH [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)
- **事件** — GE HealthCare 宣布一篇評估其 **End-tidal Control**（ETC，吐氣末濃度控制）的研究在 *Anesthesia & Analgesia Practice*（*A&A Practice*）刊出，並摘出兩個百分比作為成效：**新鮮氣體流量（fresh gas flow，FGF）中位數下降 62.3%**、**sevoflurane 用量下降 39.3%** [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)
- **日期** — **2026-10-16**。新聞稿頁在標題下方以文字標示 `October 16, 2026`，正文發稿行為 `CHICAGO — October 16, 2026`。此頁沒有任何 JSON-LD 結構化資料、沒有 `<time>` 標籤、也沒有日期相關的 meta 欄位，本文的日期即以頁面上這兩處可見標示為準 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)
- **官方入口** — [Research conducted at University of Michigan published in Anesthesia & Analgesia Practice demonstrates GE HealthCare End-tidal Control software may help to reduce fresh gas flow](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)
- **第二來源** — 被宣傳的論文本身是**開放取用**，可逐項回查，因此本則**不是單源**。論文為 McBride J 等人，*A&A Practice* 20(9):e02256，2026 年 9 月，DOI `10.1213/XAA.0000000000002256` [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)

**編輯：** Clarence

GE HealthCare 在 2026-10-16 發布新聞稿，宣傳一篇密西根大學主持、在 *A&A Practice* 刊出的回溯性觀察研究 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。本則在本書庫記錄的廠商公告中屬於**可回查程度最高的一類**，這一點值得先說清楚：被引用的論文是開放取用的，任何人都能打開全文；新聞稿寫出的每一個數值 —— 12,818 例、6,755 例（52.7%）、資料期間 2023-04-01 至 2024-09-30、62.3%、39.3% —— 都能在論文裡找到對應的位置，核對後數值本身正確，論文的結論段也確實寫著同樣的 62.3% 與 39.3% [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。研究本身的內容也相當罕見：它量的不是「這項技術有沒有效」，而是**這項技術鋪開到一整個學術醫療體系之後，臨床人員到底用不用它**，並把使用的變異拆解到人員層級。ETC 是一套依臨床人員設定的目標值自動調節新鮮氣體流量與吸入麻醉藥濃度的閉迴路軟體，直接關係到麻醉科的例行操作習慣與吸入麻醉藥的消耗量。新聞稿在轉述時遺落的幾項限定條件 —— 其中最重要的是那兩個百分比的身分 —— 集中收在後段的 `## 證據邊界（事實）`。

## 背景

1. **這一天在本案中的位置** — 2026-10-16 是**新聞稿發布日**，不是論文刊出日。論文的卷期標示為 *A&A Practice* 20(9):e02256、**2026 年 9 月**，亦即新聞稿是在論文所屬期別之後才發出的宣傳 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。研究的資料期間則更早：**2023-04-01 至 2024-09-30**，共 18 個月 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。
2. **ETC 是什麼，以及它為何不是 AI** — ETC 讓臨床人員設定吐氣末麻醉藥濃度與氧氣濃度的目標值，由機器自動調節氣體流量與揮發器輸出去維持該目標，屬於**閉迴路自動控制**，不是機器學習模型。新聞稿全文沒有任何一處把 ETC 稱為人工智慧；「AI」只出現在公司簡介的 `AI, cloud and software solutions` 一句 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。本書庫仍收錄此則的理由寫在評論段。
3. **為何關心新鮮氣體流量** — 吸入麻醉藥隨新鮮氣體流出，流量越低則藥物消耗、成本與溫室氣體排放越低；但低流量操作在技術上較難維持，吸入濃度與吐氣末濃度的落差會變大。論文把這段寫成 ETC 的立論基礎：自動化可能讓低流量麻醉在不增加操作負擔的情況下成為常態 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
4. **這不是第一份 ETC 證據，而是第一份大規模真實部署的盤點** — 論文自述先前證據多來自前瞻或受控的小規模研究，缺少大型學術醫療體系真實部署下的細部個案資訊。新聞稿註腳 `[v]` 引用的 McCabe 等人 2024 年隨機對照非劣性試驗即屬前者 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)；本研究要回答的是不同的問題 —— 當一項技術鋪開之後，**臨床人員到底用不用它** [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
5. **為何這一則值得本書庫記錄** — 這是本書庫目前收到最接近「一套成熟的真實世界部署評估應該長什麼樣」的樣本：有採用率、有逐位臨床人員的使用分布、有把變異拆解到人員層級的統計、有事先寫明並會被否定的假設、有完整的利益衝突揭露，而且全部公開可讀。

本則無可用的自製配圖。論文圖 1–4 的版權屬作者與出版方，官方新聞稿影像為 GE HealthCare 自有素材，均不重製；可用數值分屬 L/min、mL/h、kg CO2e/h、百分比與勝算比五種互異量綱，併成一張圖會暗示不存在的可比性。

## End-tidal Control 是什麼（事實）

- **運作方式** — 臨床人員設定吐氣末麻醉藥濃度與吸入氧氣濃度的目標值，機器自動調節新鮮氣體流量與揮發器輸出去維持該目標。這是閉迴路自動控制，不涉及機器學習模型 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **它要解決的操作問題** — 低流量麻醉能省藥、省錢、減少溫室氣體排放，但手動維持低流量需要持續監看與調整，而且吸入端與吐氣末端的濃度落差會隨流量下降而擴大。ETC 的立論是把這段調整交給機器，讓低流量成為預設而不是額外的操作負擔 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **搭載的機型** — 本研究限定於配備 ETC 的 GE **Aisys CS2** 麻醉機 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **適應症限定** — 新聞稿註腳 `[i]` 寫明 ETC 在美國的適應症為 18 歲以上 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。

## 這份回溯研究怎麼做（事實）

- **設計** — 回溯性觀察橫斷研究（retrospective observational cross-sectional study），論文標題為 `Utilization and Estimation of Environmental Impact of End-Tidal Control in a Multisite Academic Health System` [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **場域與期間** — University of Michigan Health – Ann Arbor 各院區，資料期間 2023-04-01 至 2024-09-30，共 18 個月 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **分母與篩選** — 論文評估了 **67,404 筆病例**，套用納入排除條件後剩 **12,818 筆**成人全身麻醉病例。排除項包含體外循環、心臟外科或心臟內科、吸入藥量不足 1 MAC（minimum alveolar concentration，最低肺泡濃度）小時、維持期不足 45 分鐘、非 GE Aisys CS2 機型、無氣管內管等 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **「使用 ETC」的定義** — 維持期內 ETC 開啟 **≥45 分鐘**。實際使用時中位數覆蓋維持期的 86.4%，中位數在維持期開始後 8 分鐘才啟用、結束前 10 分鐘即關閉 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **資料來源** — 來自 Multicenter Perioperative Outcomes Group（MPOG）這類麻醉領域的多中心周術期資料登錄系統，加上麻醉機自動回傳的機器參數 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **事先寫明的三個假設** — 論文在前言寫明：ETC 使用率 >30%、使用變異有 >50% 可由房內臨床人員解釋、FGF 與用量下降 30% [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **統計方法** — 以多層混合效果模型（multilevel mixed-effects model）調整病例與人員層級變項，並據此推算一位「範例病人」在使用與未使用 ETC 兩種情況下的數值；人員層級的變異以變異分割係數（variance partition coefficient，VPC）與中位勝算比（median odds ratio）呈現 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **審查與報告規範** — 研究計畫書與統計分析計畫由密西根大學麻醉學系的 Anesthesia Clinical Research Committee 事先審核通過；IRB 編號 `HUM00253860`；報告依 RECORD／STROBE 規範 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。

## 採用率與人員之間的差異（事實）

這是論文最具原創性的一段，也是新聞稿唯一正面引述的非數值發現。

- **整體採用率** — ETC 使用於 **6,755 筆病例（52.7%）**。在一家已經把設備鋪開、且所有人都受過同一份教育訓練的學術醫學中心，約有一半的病例沒有開啟它 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **變異來自誰** — 房內臨床人員（in-room anesthesia clinician）的 VPC 為 **38.5%**，主治麻醉醫師為 **3.9%**。換句話說，決定這台機器的功能有沒有被打開的，主要是實際站在手術室裡操作的那個人，而不是監督者 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **差異的規模** — 房內臨床人員的 median odds ratio 為 **4.10**，主治醫師為 **1.57**；意即兩位隨機抽出的房內臨床人員，在臨床條件相同的病例上使用 ETC 的勝算可相差逾四倍 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **使用分布** — 房內臨床人員中 **21.9% 在超過八成病例使用 ETC，48.0% 在不到五成病例使用**；主治醫師則為 3.5% 與 46.5% [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **新聞稿的對應寫法** — `variation in End-tidal Control use was significantly driven by the in-room anesthesia clinician`，並據此強調部署時工作流程、教育訓練與導入規劃的重要性 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。

## 氣體流量與吸入麻醉藥用量的測量結果（事實）

論文表 2 把結果分成三欄：未調整差異、調整後差異、以及 `Example patient (from adjusted model)`（依調整後模型推算的範例病人）。三欄的數字都列在下面 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。

- **未調整的觀察值** — FGF 中位數為使用 ETC 組 **0.67 L/min**、未使用組 **1.87 L/min**；平均 FGF 為 **1.54 L/min（SD 0.62）** 對 **2.68 L/min（SD 0.76）**。sevoflurane 未調整為 **7.63（SD 3.42）** 對 **14.24（SD 5.14）** mL／小時。
- **調整後的差異** — FGF 中位數 **−1.14 L/min（95% CI −1.16 至 −1.12）**，平均值 **−1.00 L/min（95% CI −1.03 至 −0.98）**；sevoflurane **−5.23 mL／小時（95% CI −5.34 至 −5.10）**；二氧化碳當量 **−1.06 kg／小時（95% CI −1.12 至 −0.99）**。
- **範例病人欄** — 中位 FGF **0.69 對 1.83 L/min**（−62.3%）；平均 FGF **1.31 對 2.31 L/min**（−43.3%）；sevoflurane **8.08 對 13.31 mL／小時**（−39.3%）；二氧化碳當量 **1.62 對 2.68 kg／小時**（−39.6%）。
- **範例病人的設定** — 由研究者指定：3.6 小時手術、45–64 歲、男性、耳鼻喉科、大手術、非門診、主治醫師搭配 CRNA（certified registered nurse anesthetist，麻醉護理師）、在 University Hospital 執行，MAC 0.9、未使用笑氣與 propofol。
- **臨床上的落點** — 低流量麻醉的臨床慣例門檻是每分鐘低於 1 公升。未調整的觀察值顯示使用 ETC 的那一組中位數 0.67 L/min 已落在該區間內，未使用的那一組 1.87 L/min 則離得相當遠。
- **這個降幅取決於導入前的習慣** — 論文討論段指出，McCabe 等人的隨機對照試驗（n = 210）依所選揮發性麻醉藥不同，報告的總用量下降為 **4% 至 34%**，低於本研究的 39.3%；論文自己給的解釋是該院原本的慣用流量約為 2 L/min，基準較高因此降幅較大 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。

## 利益揭露與經費來源（事實）

論文把三項揭露都寫得完整，可逐項核對 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。

- **作者與單位** — McBride J、Jewell ES、Zhao X、Pantis R、**Beard JW**、Shah N、Klumpner T、Hovord DG、Colquhoun DA。掛名單位只有兩個：`1` 為 Department of Anesthesiology, University of Michigan Medical School, Ann Arbor, Michigan；`2` 為 **GE HealthCare, Chicago, Illinois**。第五作者 John W. Beard 掛的是單位 2。
- **經費** — 資料萃取與分析由 GE HealthCare 部分出資給密西根大學；另有美國國家衛生研究院 National Heart, Lung, and Blood Institute 的 K08HL159327 補助（給 Colquhoun）。
- **利益衝突** — 論文揭露 Colquhoun、Hovord、Klumpner 三人有 GE HealthCare 支付給密西根大學的研究支持，其中 Hovord 另為 GE HealthCare 顧問；Colquhoun 另有 Merck Sharp & Dohme 與 Chiesi USA 支付給校方的其他研究支持；Klumpner 另有 BioIntellisense 的無關研究經費，並擔任 Epic Systems 成人麻醉次專科指導委員會（無給職）成員。
- **因此這篇論文的定位** — 一篇**有廠商參與、但經過同儕審查且完整揭露利益衝突**的研究，不是與廠商無關的獨立驗證。
- **新聞稿端的揭露** — 新聞稿註腳 `[iv]` 揭露「資料萃取與分析由 GE HealthCare 部分出資給密西根大學」；註腳 `[vii]` 寫明 Colquhoun 的意見僅代表個人、不代表密西根大學，並寫 `there can be no guarantee that others will achieve the same results`，理由是醫院規模、病例組成與人員經驗等變項不同 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。

## 證據邊界（事實）

- **62.3% 與 39.3% 是論文為一位虛構的「典型病人」以調整後模型推算的差異，不是兩組病例的觀察差距。** 這兩個數字出現在論文表 2 的第三欄 `Example patient (from adjusted model)`，對應的是上節所列那位由研究者指定條件的範例病人在使用與未使用 ETC 兩種情況下的推算值（中位 FGF 0.69 對 1.83 L/min、sevoflurane 8.08 對 13.31 mL／小時）。論文把這件事寫在表格標題與方法段，新聞稿則只留下百分比 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **新聞稿摘出的是四個可用百分比中最大的那一個。** 同一欄裡另有平均 FGF 的 −43.3% 與二氧化碳當量的 −39.6%，新聞稿都沒有摘 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **絕對值存在，但沒有進新聞稿。** 未調整的 0.67 對 1.87 L/min、調整後的 −1.14 L/min（95% CI −1.16 至 −1.12）都在論文裡；新聞稿對兩個百分比沒有給任何括號說明、沒有信賴區間、沒有對照組定義，也沒有絕對值 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **出面稱讚這項研究的 GE 高層本人是論文共同作者，新聞稿未提。** 新聞稿引述 John Beard 說這項研究 `adds important real-world evidence`；論文第五作者 John W. Beard 掛名單位為 GE HealthCare（Chicago, Illinois），是同一人 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **唯一揭露 GE 出資的那條註腳沒有內文錨點。** 以頁面 DOM 逐一檢視上標錨點後確認：內文實際出現的錨點為 `[i]`、`[ii]`、`[iii]`、`[i]`、`[v]`、`[vi]`、`[vii]`，七條註腳中**只有 `[iv]` 沒有任何內文錨點**，而 `[iv]` 正是揭露出資的那一條 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。
- **標題同時用了兩種強度相反的措辭。** 標題為 `Research conducted at University of Michigan ... demonstrates GE HealthCare End-tidal Control software may help to reduce fresh gas flow`，同一句裡同時出現 demonstrates（證明）與 may help to（可能有助於）；研究設計是回溯性觀察研究，論文全篇使用的是 associated with（與……相關） [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **三個事先假設裡，第二個未成立。** 使用率 52.7%（>30%，成立）、下降幅度超過 35%（>30%，成立），而房內臨床人員的 VPC 為 **38.5%**，低於作者自訂的 50% 門檻（**未成立**）。新聞稿引述了「變異由房內臨床人員主導」這個方向，但未提它低於作者自訂的門檻 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **兩組病例並不可比。** 使用 ETC 的病例麻醉時間較長（236 對 204 分鐘）、較常由住院醫師執行（主治搭住院醫師 39.7% 對 23.6%）、科別組成差異大（婦產科占 3.7% 對 16.1%）。論文報告的標準化差異在手術科別為 0.57、院內地點為 0.69，遠高於其自訂的 0.2 門檻。新聞稿未提及任何一項組間差異 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **篩選前的分母未進新聞稿。** 論文評估 67,404 筆、納入 12,818 筆，新聞稿只給 12,818（摘要列點寫為 nearly 13,000） [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **新聞稿提到卻留白的第三個結果。** 摘要列點寫 ETC 的使用與 `estimated CO2 equivalents`（二氧化碳當量）下降相關，Colquhoun 的引述另提到 `projected cost saving`，但新聞稿兩者都沒有給數字，儘管論文對前者有明確數值（1.62 對 2.68 kg CO2e／小時，調整後差異 −1.06 kg，95% CI −1.12 至 −0.99） [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow) [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **降幅大小取決於該機構導入前的既有操作習慣。** 論文自己的解釋是該院原本慣用流量約 2 L/min，基準較高因此降幅大於 McCabe 等人隨機對照試驗（n = 210）報告的 4% 至 34% [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **論文自列的限制。** 觀察性設計無法說明使用或不使用的動機；以照護時間最長者歸屬臨床人員可能造成錯誤分類偏誤；以 ≥45 分鐘定義使用同樣可能造成錯誤分類；可能存在使用上的適應症混淆（confounding by indication）；結果反映單一學術醫學中心的現況，可能無法類推到其他執業環境 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **與先前發表有重疊。** 本次分析包含先前一篇單一日間手術中心、六個月的先導分析中已報告過的 334 名病人 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。
- **新聞稿可見文字沒有書目資訊。** 論文標題、作者名單、卷期、DOI 均未出現在新聞稿可見文字中；期刊名以超連結指向全文，DOI 只存在於該連結的網址字串內 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。
- **註腳 `[ii]` 是以編號引用的非公開廠內報告。** `GE HealthCare Et Control Pivotal Study Report DOC2163005`，本文未引用其任何內容 [(ref: pr)](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)。
- **這篇論文不是與廠商無關的獨立驗證。** 共同作者之一掛名 GE HealthCare、資料萃取與分析由 GE HealthCare 部分出資，雖經同儕審查且完整揭露，但獨立性有其邊界 [(ref: paper)](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)。

## 本書庫解讀（評論）

- **可以完整回查，本身就是這則公告最值得記下的特性** — 本書庫處理過的廠商公告裡，佐證多半是以文件編號引用的非公開內部報告，或根本沒有佐證。本則不同：它指向一篇開放取用、可逐項回查的同儕審查論文，而且核對後數值本身沒有錯。即使轉述過程出現了下面幾處簡化，它仍然比「以編號引用廠內未公開報告」高出一個層級。對採購與評估方而言，值得記下的判準是：廠商的佐證是否能被你自己打開。
- **「數字正確」與「數字正確地被理解」是兩件事** — 62.3% 與 39.3% 逐字出現在論文結論段，問題在於論文把這兩個數字放在一個標明 `Example patient (from adjusted model)` 的欄位裡，而新聞稿把欄位名留在原處。讀者看到「62.3% reduction」會自然理解成「這批病例實際省了六成」，但它實際的意思是「對一位符合最常見類別組合的虛構病人，模型推算使用與不使用的差距是六成」。這類轉述不需要竄改任何數值就能改變含義，也因此特別難被一般讀者察覺 —— 要發現它，必須打開論文看表格標題。
- **絕對值存在卻沒被帶走，是本則最可惜的一點** — 論文給了絕對值（0.67 對 1.87 L/min），而且這組絕對值對讀者更有用，因為低流量麻醉的臨床慣例門檻是「低於 1 L/min」，有了絕對值才能判斷使用 ETC 的那組是否真的進入低流量區間（0.67 L/min，是），沒用的那組差多遠（1.87 L/min）。新聞稿捨絕對值而取百分比，讀者反而失去了判斷的依據。
- **出資揭露沒有錨點，不太可能是巧合** — 七條註腳裡有六條掛在內文句子上，唯獨揭露 GE 出資的 `[iv]` 沒有。它仍然印在頁面底部，因此不構成隱匿；但註腳的功能是把限定條件綁在被限定的那句話旁邊，一條沒有錨點的註腳等於把限定條件搬離了它該限定的位置。合理的做法是把 `[iv]` 掛在「announced the publication of research conducted at the University of Michigan」那一句上。
- **第二位發言人的身分缺了一句話** — 以 GE 高層身分評論自家產品的研究，本來就會被讀者打折扣，這沒有問題；問題是他同時是該論文的共同作者，而新聞稿沒有提。補上「本研究共同作者」七個字不會削弱這則公告，反而讓它更經得起查核 —— 論文自己就把這件事揭露得很完整（掛名單位、經費、利益衝突三處都寫了），新聞稿反而是揭露最少的那一環。
- **被否定的假設是這篇論文最有價值的部分，卻沒有被宣傳** — 作者事先寫下「房內臨床人員可解釋超過五成的使用變異」，結果是 38.5%，沒有達標。這種「寫下來、然後承認沒達到」的作法，正是本書庫在評估任何部署宣稱時最想看到的訊號。
- **醫療橋接** — ETC 不是 AI，但它與醫療 AI 共用同一個處境：一個裝在臨床現場、由人決定要不要開啟的輔助工具。本書庫收錄的醫療 AI 公告，絕大多數停在模型效能或合作宣布，而這篇論文做到了三件更後面的事。第一，**量到採用率**：52.7%，而不是「已部署於 N 家醫院」。第二，**把採用的變異拆解到人員層級**：房內臨床人員解釋 38.5%、主治醫師 3.9%，中位勝算比 4.10 對 1.57 —— 這直接回答了「要提高使用率該對誰下功夫」。第三，**承認組間不可比**：使用組的手術時間更長、科別組成不同，因此所有結論都寫成相關而非因果。如果把 ETC 換成任何一個影像判讀或報告生成模型，這三項正是目前最缺、而且技術上完全做得到的評估 —— 需要的只是把電子病歷裡既有的使用紀錄接出來，而不是再訓一個模型。
- **「誰在房間裡」比「工具有多好」更能決定結果** — 房內臨床人員之間四倍的使用勝算差距，發生在**同一家醫院、同一套機器、所有人都受過同一份教育訓練**的條件下。這個數字對醫療 AI 的意義很直接：一個在驗證集上表現良好的模型，實際產生的效益會先被「誰願意開啟它」這一層稀釋，而這一層的變異可能比模型版本之間的差異還大。目前的醫療 AI 評估幾乎不量這一層。

## 產業影響

- **對麻醉科的工作流程而言**，本則的實質訊息是：把低流量麻醉從「需要持續手動維持的技巧」改成「設定目標值後由機器維持」，確實與明顯較低的氣體流量與藥量相關；但在一家已經完成設備鋪設的醫學中心，採用率仍只有 52.7%，而且決定開不開的是房內那位實際操作者。導入規劃若只做設備與教育訓練，效益會停在一半。
- **對吸入麻醉藥用量與手術室碳足跡而言**，論文給的絕對值（FGF 中位數 0.67 對 1.87 L/min、二氧化碳當量 1.62 對 2.68 kg／小時）讓各院可以用自家導入前的既有流量去估算可能的效益區間 —— 而且因為降幅取決於基準，原本流量習慣越高的單位，可得的改善越大。
- **可查證的廠商宣傳正在變成一種可區分的品質訊號** — 這則新聞稿指向一篇開放取用、可逐項回查的同儕審查論文，這在本書庫記錄的公告中屬少數。
- **永續性正成為醫材行銷的新論述軸線** — 這則公告的核心賣點不是臨床結果，而是氣體用量與二氧化碳當量。手術室的吸入麻醉藥排放確實是醫院碳足跡的可量化項目，這條論述有其實質基礎；但以環境指標為賣點的宣稱同樣需要絕對值與基準，而本則恰好示範了只給百分比會發生什麼事。
- **真實世界部署資料的來源正在成形** — 「裝置自動記錄 + 既有登錄系統」的組合，是目前少數能在不額外收案的前提下量到真實使用行為的途徑，對醫療 AI 的上市後監測有直接的參考價值。
- **閉迴路自動化的法規位置與 AI 不同，但部署問題相同** — ETC 在美國以 18 歲以上為適應症，走的是傳統醫材路徑。但它證明了一件事：即使法規路徑完全清楚、效益也有同儕審查證據，採用率仍然只有一半。監管許可從來就不是部署的終點。

## 與書庫其他文章的關係

同一家公司相隔三天的兩則發布，都在談工作流程的量化改善，但證據層級不同：該則的放療合作仍在探索階段，本則有一篇開放取用的同儕審查論文可供逐項回查。兩則引用的關鍵數字都帶有原文的限定條件，轉述時都需要回到原處確認: [GE 擴大研究合作，探索放療工作流程的生成式 AI](2026-10-15-ge-healthcare-mgb-genai-radiation-therapy.md)

兩則都缺少讀者自行設定驗收門檻所需的那個數字，但缺法相反：該則給了九個全為上下限、沒有典型值也沒有對照機型的規格，本則給的 62.3% 恰恰就是論文算出來的典型值，只是新聞稿沒說它是模型對一位虛構病人的推算，而真正能用來對照臨床門檻的絕對值（0.67 對 1.87 L/min）留在論文裡: [Accela：以 NeoArc 動態弧形治療為核心的放療機](2026-10-13-siemens-accela-radiotherapy-launch.md)

兩則都在回答「落地之後能量到什麼」：該則的五個合作案以部署階段與使用場景描述進展，本則則用電子病歷與麻醉機既有的使用紀錄，把採用率、逐位臨床人員的使用分布與變異來源拆解出來。兩則並讀可以看出落地評估的粒度差異，往往取決於現場有沒有既存的量測資料: [MedGemma：開放權重醫療模型，四國五個落地合作案](2026-10-08-medgemma-global-deployment-claims.md)

同一家公司四天內的兩則公告，對證據的處理方式差距極大：本則整篇建立在一篇開放取用的同儕審查論文上，每個數字都能回到原文確認，落差只在轉述時遺落了限定條件；該則全頁沒有任何百分比、沒有任何註腳，也沒有一條可以打開的佐證，兩則合看可以看出「公告有沒有給出可查核物」這件事在同一家公司內部也不一致: [院內迴旋加速器取得 CE Mark，固態靶平台加 Copper-64](2026-10-19-ge-healthcare-minitrace-magni-ce-mark-copper-64.md)

兩則都是廠商宣傳一篇數值本身正確的論文，落差都出在限定條件被留在原處，而被省略的東西種類不同：本則省略的是「這兩個百分比是論文為一位虛構典型病人以調整後模型推算的差異」，該則省略的是「90% 指的是七項鑑別診斷清單之內命中，排第一名的只有 56%」；一個換掉了受測對象，一個換掉了清單長度，兩則並讀可以看出同一種改寫手法在不同量綱上的樣子: [AMIE 看診前先問病史：98 人的 Lancet 可行性研究](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

本則是本書庫目前最接近完整部署評估的樣本，事先寫明三個假設、並在其中一個未達自訂門檻時照實報出；該則恰好是相反的作法，技術報告自述最終規格是在看過結果之後才設定的，而按原規格最後一輪 113 個 scFv 設計沒有一個以實測解離常數通過，兩則並讀可以看出「終點什麼時候定」這件事如何決定一份成果該被當成驗證還是當成探索: [Anthropic 公布六個藥物開發組織接入 Claude 的早期成果](2026-10-28-anthropic-drug-development-case-studies.md)

## 實務的啟發

- **看到百分比先問它的欄位名** — 拿到任何「下降 X%」的宣稱，先找出這個百分比在原始論文的哪一欄。未調整差異、調整後差異、與範例病人推算值是三種不同的東西，彼此可以差很多（本則的 FGF 中位數差 62.3%、平均值差 43.3%，同一張表、同一批病例）。
- **要求絕對值，即使對方已經給了百分比** — 百分比的大小取決於基準。評估任何工具時，「你們導入前的基準是多少」與「導入後是多少」比降幅更有決定性。
- **把採用率寫進驗收條件** — 如果院內要導入一個臨床輔助工具（AI 或非 AI），本則提供了一組現成可抄的指標：使用率、使用時間占整段流程的比例、以及使用變異在人員層級的分割。這些都不需要額外收案，從既有紀錄就能算。
- **找出「房內那個人」是誰** — 本研究最實用的發現是變異主要來自實際操作者而非監督者。導入規劃若只對科主任或主治醫師做宣導，可能對準了解釋力只有 3.9% 的那一層。
- **讀廠商引用的論文時，先看作者單位與利益衝突揭露** — 本則的論文把三項揭露都寫得很完整，反而是新聞稿省略了。單位欄常常一眼就能看出廠商是否參與研究，這一步只要幾秒。
- **把「作者事先寫下的假設有沒有成立」當成讀研究的固定動作** — 一篇願意寫下門檻並承認未達標的論文，比一篇只報告成功結果的論文可信。本則的第二個假設未成立這件事，在新聞稿裡完全看不到。

## 後續追蹤

- 論文提到在技術鋪開至全院所有麻醉場所後，將進行促進採用與優化使用的後續研究；值得追蹤該研究是否會報告介入後的採用率變化，以及介入對象是否如本研究建議的鎖定房內臨床人員。
- 論文指出 ETC 中位數延後 8 分鐘啟用、提前 10 分鐘關閉，覆蓋維持期的 86.4%，並將此列為可優化空間；後續若有報告完整覆蓋下的效益數字，可與本則的 62.3% 對照。
- 本則的降幅受導入前既有流量習慣影響，若出現基準較低機構的同類研究，可用以檢驗 ETC 效益的可移轉性。
- 新聞稿註腳 `[ii]` 的 `GE HealthCare Et Control Pivotal Study Report DOC2163005` 為以編號引用的非公開廠內報告，本文未引用其任何內容；若日後公開可補充核對。
- GE HealthCare 是否會在後續引用同儕審查研究的公告中揭露自家人員的共同作者身分，值得作為該公司宣傳品質的觀察指標。

## References

- `pr` — GE HealthCare，[Research conducted at University of Michigan published in Anesthesia & Analgesia Practice demonstrates GE HealthCare End-tidal Control software may help to reduce fresh gas flow](https://www.gehealthcare.com/en-us/about/newsroom/press-releases/research-conducted-at-university-of-michigan-published-in-anesthesia-analgesia-practice-demonstrates-ge-healthcare-end-tidal-control-software-may-help-to-reduce-fresh-gas-flow)（官方新聞稿，頁面標示 October 16, 2026）。底 URL：`https://www.gehealthcare.com/en-us/about/newsroom/press-releases/`
- `paper` — McBride J、Jewell ES、Zhao X、Pantis R、Beard JW、Shah N、Klumpner T、Hovord DG、Colquhoun DA，[Utilization and Estimation of Environmental Impact of End-Tidal Control in a Multisite Academic Health System: A Retrospective Observational Cross-Sectional Study](https://journals.lww.com/aacr/fulltext/10.1213/xaa.0000000000002256~utilization-and-estimation-of-environmental-impact-of)，*A&A Practice* 20(9):e02256，2026 年 9 月，DOI `10.1213/XAA.0000000000002256`（開放取用）。底 URL：`https://journals.lww.com/aacr/`

[Home](../) · [Industry Watch](./)
