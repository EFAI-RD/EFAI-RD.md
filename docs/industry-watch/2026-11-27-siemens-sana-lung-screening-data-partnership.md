---
parent: Industry Watch
nav_order: 1
title: "不只影像還要報告與標註：Siemens 與 Sana 肺癌篩檢合作解析"
category: industry-watch
date: 2026-11-27
tags: [Siemens-Healthineers, Sana-Kliniken, Sana-Data-Solutions, lung-cancer-screening, low-dose-CT, training-data, annotations, radiology-report, data-sovereignty, G-BA, Germany, real-world-evaluation, double-reading]
catalog_id: "siemens-healthineers:sana-kliniken-ai-data-partnership-2026-11-17"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.2"
source:
  orgs:
    - "Siemens Healthineers"
    - "Sana Kliniken AG"
  event: "Siemens Healthineers 與 Sana Kliniken 簽訂合作協議，由子公司 Sana Data Solutions 在受控資料環境內提供德國的策展健康資料供 Siemens 訓練 AI，第一個共同專案為肺癌篩檢演算法"
  event_date: "2026-11-17"
  official_url: "https://www.siemens-healthineers.com/press/releases/sana"
  single_source: true
  single_org: false
related_articles:
  - path: "2026-11-11-ge-healthcare-magnus-neuro-alliance.md"
    relation: "兩則都是大廠把多家醫療機構圈成一個研究供給網，拿到的東西卻不同：該則聯盟換到的是九家機構圍繞一台研究用機器的使用與交流意向，本則協議換到的是一家醫院集團的影像、標註與放射報告，以及事後在同一批院所內評估的場域"
  - path: "2026-11-19-ge-healthcare-photonova-spectra-pcct-collaborations.md"
    relation: "該則的光子計數 CT 已取得美國 510(k) 許可，七家機構是在許可之後才展開結構化評估；本則連受評的軟體都還沒有，醫療機構供應的是訓練階段的輸入。同樣是大廠與醫療機構的結構化合作，分別落在法規後與訓練前"
  - path: "2026-11-26-ge-healthcare-inteleorchestrator-clarity-reporting.md"
    relation: "該則的報告草稿功能把放射報告當成產出端的目標，本則的協議則把放射報告列為要交付給廠商的訓練輸入之一。同一種文件在兩則裡分別站在模型的輸出端與輸入端"
refs:
  shs:
    title: "Siemens Healthineers and Sana Kliniken collaborate on AI solutions for healthcare（Siemens Healthineers 官方新聞稿頁，Published on November 17, 2026）"
    url: "https://www.siemens-healthineers.com/press/releases/sana"
  sana:
    title: "Siemens Healthineers und Sana arbeiten gemeinsam an KI-Lösungen für die Gesundheitsversorgung（Sana Kliniken AG 新聞室，Ismaning，17 November 2026，同一份聯合新聞稿的德文版）"
    url: "https://www.sana.de/newsroom/siemens-healthineers-und-sana-arbeiten-gemeinsam-an-ki-loesungen-fuer-die-gesundheitsversorgung/"
  gba:
    title: "Lungenkrebs-Früherkennung für Raucherinnen und Raucher（Gemeinsamer Bundesausschuss 主題頁，含給付資格與雙重判讀流程）"
    url: "https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/"
  gba_beschluss:
    title: "Krebsfrüherkennungs-Richtlinie: Einführung der Lungenkrebsfrüherkennung mittels Niedrigdosis-Computertomographie bei Rauchern（G-BA 決議頁，Beschlussdatum 18.06.2025）"
    url: "https://www.g-ba.de/beschluesse/7301/"
---

[Home](../) · [Industry Watch](./)

# 不只影像還要報告與標註：Siemens 與 Sana 肺癌篩檢合作解析

## 來源

- 組織：Siemens Healthineers（DAX: SHL）與 Sana Kliniken AG（含子公司 Sana Data Solutions GmbH）
- 事件：雙方簽訂合作協議開發 AI 軟體解決方案，由 Sana Data Solutions 在受控資料環境內提供德國的策展健康資料，第一個共同專案為肺癌篩檢演算法
- 日期：2026-11-17（Siemens Healthineers 頁面可見標示為 Published on November 17, 2026；Sana 新聞室頁面的發稿行為 Ismaning，17 November 2026）
- 官方入口：<https://www.siemens-healthineers.com/press/releases/sana>
- **單源，待交叉驗證**：Siemens Healthineers 與 Sana 兩個網址登的是**同一份聯合新聞稿**（頁面自標 Joint Press Release），一為英文、一為德文，內容逐段對應。兩個組織各自發布不等於兩個獨立來源，關於本次合作的一切敘述目前只有這一份文本支持。本文另引用的德國聯邦共同委員會（Gemeinsamer Bundesausschuss，G-BA）頁面是獨立的主管機關文件，但它描述的是德國肺癌篩檢的法定制度，與本次合作無關，不能用來佐證合作本身的任何內容。

**編輯：** Clarence

Siemens Healthineers 與德國醫院集團 Sana Kliniken 於 2026-11-17 共同發布新聞稿，宣布簽訂開發 AI 軟體解決方案的合作協議 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。協議的核心不是一項產品，而是一條資料供給路線：Sana Kliniken AG 的子公司 Sana Data Solutions GmbH 將在一個 `secure, controlled data environment`（安全、受控的資料環境）內提供來自德國的策展健康資料，作為訓練 AI 工具與開發對應軟體的其中一塊基礎。第一個共同專案是肺癌篩檢的 AI 演算法，由 Sana Kliniken 與其所屬放射科機構提供去識別化資料交由 Siemens Healthineers 訓練；要交付的資料不只是影像，公告明列為臨床與病理資料集，`including images, annotations and radiology reports`，後續再加上病人脈絡、檢查結果與檢查順序。雙方並規劃第二步，在 Sana 自家醫院與所屬放射科診所的日常臨床工作中評估做出來的軟體。

## 背景

- **2025-06-18：G-BA 決議把低劑量電腦斷層（Niedrigdosis-Computertomographie，低劑量 CT）肺癌篩檢納入癌症篩檢指引。** 決議頁載明 Beschlussdatum 為 18.06.2025、Inkrafttreten（生效）為 05.09.2025，並於 BAnz AT 04.09.2025 B3 公告 [(ref: gba_beschluss)](https://www.g-ba.de/beschluesse/7301/)。
- **2026 年 4 月起成為法定健保給付項目。** G-BA 主題頁寫 `Seit April 2026` 起，年齡 50 至 75 歲、現在或曾經重度吸菸者可獲得低劑量 CT 肺癌早期篩檢的給付；其放射防護法上的依據是 Lungenkrebs-Früherkennungs-Verordnung，G-BA 再據此在 Krebsfrüherkennungs-Richtlinie 中規範法定保險人的給付請求權 [(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。這一段是本則題目的制度背景：德國的肺癌篩檢在本次合作公告之前，已經是一個有法定資格條件、法定流程與給付的常規業務，而不是一個待開闢的研究場景。
- **2026-11-17：本則聯合新聞稿發布。** 頁面標示為 Joint Press Release by Siemens Healthineers and Sana Kliniken，德文版發稿地為 Sana Kliniken AG 總部所在地 Ismaning [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)[(ref: sana)](https://www.sana.de/newsroom/siemens-healthineers-und-sana-arbeiten-gemeinsam-an-ki-loesungen-fuer-die-gesundheitsversorgung/)。

本則無配圖。兩家公司新聞稿頁面上的圖像為其自有素材，不重製；本則正文沒有任何成組數值可供自繪圖表。

## 這份協議的內容（事實）

- **協議標的是資料與開發，不是一項已存在的產品。** 公告第一句寫雙方 `have entered into an agreement to collaborate on the development of AI-powered solutions`，由 Sana Data Solutions GmbH 為該專案提供來自德國的策展健康資料，資料的角色被寫成 `one component in training AI-powered tools and developing corresponding software solutions`，也就是訓練用材料的其中一塊，而非唯一來源 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。
- **合作想建立的是一個 real-world testing environment。** 公告寫這段夥伴關係 `is intended to create a real-world testing environment in which medically relevant software products can be developed and clinically evaluated more quickly while complying with regulatory requirements`，即在符合法規要求的前提下，讓醫療相關軟體產品能更快被開發與臨床驗證 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。
- **具名發言者兩位。** Siemens Healthineers 中歐與西歐區負責人 Stefan Schaller 的引言主張資料驅動的創新需要貼近照護現場並有明確規則；Sana Data Solutions GmbH 總經理 Michael Hübner 的引言則把關鍵因素列為 `clear governance, precisely defined purposes and uncompromising protection of patients and their data`，即明確治理、精確界定的使用目的，以及對病人與其資料的保護 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。
- **歐洲資料主權是公告自陳的動機之一。** 公告寫 `Until now, projects of this kind have often relied on data from outside Europe`，並稱此合作強化德國作為創新據點的地位、促進歐洲資料主權（European data sovereignty）[(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。這是一句關於此類專案的一般性陳述，公告並未指明過去哪些專案、也未指明是否包含 Siemens Healthineers 自己的專案。

## 第一個題目與資料內容（事實）

- **第一個共同專案是肺癌篩檢演算法。** 公告寫 `As part of an initial joint project, AI-powered algorithms for lung cancer screening are to be developed`，並寫由 Sana Kliniken 及其所屬放射科機構（affiliated radiology facilities）提供去識別化（anonymized）資料，供 Siemens Healthineers 訓練演算法 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。
- **交付的資料分兩階段，且不限於影像。** 公告寫提供的資料將包含臨床與病理資料集，`including images, annotations and radiology reports`（影像、標註與放射報告），`and later also patient context, results and examination sequences`（後續再加上病人脈絡、檢查結果與檢查順序）[(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。對模型訓練而言，標註與放射報告屬於監督訊號與文字輸出的來源，與單純的像素資料不是同一類輸入。
- **第二步是在自家院所內評估。** 公告寫 `In a second step, the partners aim to evaluate the AI-powered software solutions developed in the day-to-day clinical and practice settings of Sana Kliniken and its affiliated radiology practices`，即在 Sana 醫院與所屬放射科診所的日常臨床與門診場域評估所開發的軟體 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。提供訓練資料者與後續評估場域是同一個機構網絡。
- **雙方自陳的期待有三項。** 更快且更好的診斷能力、由此而來的更個人化治療建議，以及在醫院與診所的真實條件下更早測試 AI 工具與工作流程 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。三項皆以 expect 書寫，無任何已達成的結果。
- **資安與資料保護以概括語句帶過。** 公告寫 `Comprehensive security concepts will ensure compliance with high standards of data protection and data security`，未指名任何具體標準、認證、稽核機制或法律依據 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。

## 德國肺癌篩檢的法定流程（事實）

這一節的內容出自 G-BA，與本次合作無關，但它界定了上述資料與未來軟體所要進入的業務形態。

- **給付資格有明確門檻。** 法定健保被保險人、年齡 50 至 75 歲、重度吸菸達至少 25 年且至少 15 個「包年」（Packungsjahre）。一個包年等於每天抽一包菸（20 支）持續一年；期間的戒菸中斷不得長於 10 年 [(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。
- **入口在非放射科醫師手上。** 參與此篩檢的內科、一般醫學或職業醫學醫師負責確認資格，並與被保險人進行關於低劑量 CT 利弊的資訊告知會談；符合條件者取得轉介，前往有篩檢許可的放射科診所 [(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。
- **制度要求雙重判讀，而且是在第一位判讀者判定異常之後才啟動。** 檢查由取得篩檢許可的放射科醫師執行初次判讀（Erstbefundung）。若判定為無異常（unauffälliger Befund），下一次篩檢請求權在 12 個月後。若判定為需追蹤（kontrollbedürftig）或需釐清（abklärungsbedürftig），初判者必須把該次低劑量 CT 影像傳送給參與此篩檢的第二判讀者（Zweitbefunder）[(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。
- **第二判讀獨立進行，再與初判者合議。** Zweitbefunder 獨立於 Erstbefunder 評估同一批影像，之後兩人交換意見形成共同判定。共同判定為需追蹤者，兩人給出下次檢查時點的共同建議（小於 12 個月）；共同判定為需釐清者，即存在具體疾病懷疑，必須立即啟動後續措施，由初判者儘速與被保險人討論下一步 [(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。

## 證據邊界（事實）

本則目前只有一份文本，且該文本刻意停在協議層級，可核對的範圍因此很窄。相關限制集中列在這裡供引用時參考。

- **兩個官方網址不構成交叉驗證。** Siemens Healthineers 的英文頁與 Sana 的德文頁是同一份聯合新聞稿的兩個語言版本，段落結構與內容逐段對應。本文對合作內容的每一項敘述，實際上都只回得到這一份文本 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)[(ref: sana)](https://www.sana.de/newsroom/siemens-healthineers-und-sana-arbeiten-gemeinsam-an-ki-loesungen-fuer-die-gesundheitsversorgung/)。
- **公告正文沒有任何一個數字。** 把英文頁自三行重點（Development of AI-powered software solutions…／Pilot phase for lung cancer screening launched／Advancing European data sovereignty）起至正文結束的這段文本逐字清點，共 3,251 個字元，其中阿拉伯數字出現 0 次（清點由本文執行）。也就是說，資料筆數、病人數、檢查數、時程、里程碑、金額、分潤或任何一方的投入規模，全部不在公告之內 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。頁面上出現的數字全部位於兩家公司的制式簡介段落：Sana 方為 50 家醫院、66 家醫療照護中心公司（MVZ）約 550 個醫師席位、逾 60 家醫材供應與預防保健據點、2025 年約 43,000 名員工與 41 億歐元營收、1976 年創立、由 24 家私人健康保險公司持有，並註明資訊狀態為 2025 年 12 月；Siemens Healthineers 方為截至 2026-09-30 的會計年度約 75,000 名員工與約 236 億歐元營收、業務遍及逾 180 國。這些是公司規模，不是本次合作的規模。
- **重點行寫「已啟動」，正文寫「將要開發」。** 英文頁的第二行重點是 `Pilot phase for lung cancer screening launched`，而正文對應段落寫的是 `algorithms for lung cancer screening are to be developed`。德文版同樣呈現這組落差：重點行為 `Pilotphase bei Lungenkrebsscreening gestartet`，正文為 `sollen KI-gestützte Algorithmen für das Lungenkrebsscreening entwickelt werden` [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)[(ref: sana)](https://www.sana.de/newsroom/siemens-healthineers-und-sana-arbeiten-gemeinsam-an-ki-loesungen-fuer-die-gesundheitsversorgung/)。兩種語言一致，表示這不是翻譯造成的差異；但公告未說明所謂 pilot phase 已啟動的是哪一部分，也未給啟動日期。
- **「策展」與「去識別化」是兩個不同的描述，各自出現在不同段落。** 總述段寫 Sana Data Solutions 提供 `curated health data`，肺癌篩檢專案段寫 Sana Kliniken 與所屬放射科機構提供 `anonymized data`。公告未說明兩者是否為同一批資料，也未說明去識別化的作法或標準 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。
- **法規與驗證用語只出現一次，且是概括語。** 公告正文中 regulatory 一詞僅出現於 `while complying with regulatory requirements` 這一處；FDA、CE、MDR、cleared、clearance、study、trial、validation、accuracy 等字詞的命中皆為 0（清點由本文執行，範圍同上）[(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。公告因此未說明未來軟體打算走哪一條醫療器材法規路徑、預期的風險分級，或第二步的「評估」屬於哪一種性質的評估。
- **第二步只寫 aim to，沒有時程。** 公告對臨床場域評估的寫法是 `the partners aim to evaluate`，沒有起訖時間、沒有納入院所數、沒有終點指標 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。
- **「提供資料的機構」與「評估軟體的機構」是同一批。** 這是公告明寫的安排，而非本文推論：訓練資料來自 Sana Kliniken 與其所屬放射科機構，第二步的評估場域也是 Sana Kliniken 與其所屬放射科診所 [(ref: shs)](https://www.siemens-healthineers.com/press/releases/sana)。公告未說明評估時將如何處理訓練資料與評估場域重疊所帶來的影響。
- **本文未取得的文件。** 公告未提供協議全文、資料使用條款、倫理審查或資料保護影響評估的任何文件連結，本文亦未自其他管道取得，因此上述所有限制只能以公告自身的文字為準。

## 本書庫解讀（評論）

- **這則公告真正交易的是資料與場域，不是技術。** 把可核對的內容抽出來，成立的事實只有三件：雙方簽了協議、Sana 會在受控環境內提供資料、第一個題目是肺癌篩檢。沒有模型、沒有規格、沒有效能。對產業觀察而言，值得記下的不是「Siemens 又做了一個 AI」，而是一家設備商用合作協議的形式，取得了一個醫院集團的影像、標註與報告，外加同一批院所作為日後的評估場域。在醫療影像 AI 這個領域，這兩樣東西的取得難度通常高於模型本身。
- **要到放射報告與標註，和只要到影像，是兩種不同量級的事。** 影像可以回溯匯出；標註與放射報告則牽涉判讀者的時間、報告系統的結構化程度，以及去識別化時最難處理的自由文字。公告把這三者並列為第一批交付內容，等於把監督訊號與文字輸出的來源一次納入。若後續再加上公告所寫的病人脈絡、檢查結果與檢查順序，可訓練的任務就不只是結節偵測，還可能延伸到報告生成與追蹤建議。這是本則最值得追問的一段，而公告對此沒有給出任何量的描述。
- **挑肺癌篩檢當第一個題目，在德國有制度上的理由。** 德國的低劑量 CT 肺癌篩檢自 2026 年 4 月起成為法定給付，有明確的資格門檻與法定流程 [(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。一個剛開始運轉的法定篩檢計畫，意味著檢查量會持續累積、判讀行為被規則約束、資料結構相對一致 —— 這些都是訓練資料品質的有利條件。本書庫認為這是合理的推論方向，但要強調：公告本身完全沒有提到 G-BA、沒有提到這個篩檢計畫的法定地位，也沒有說明 Sana 的資料是否來自該計畫。兩件事放在一起看是本文的解讀，不是公告的主張。
- **德國制度已內建的雙重判讀，是這類模型最現實的落點問題。** 依 G-BA 的規範，異常影像必須由第二判讀者獨立評估、再與初判者合議 [(ref: gba)](https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/)。也就是說，這個工作流程裡已經有一個設計好的「第二意見」位置，而且它的輸出是人與人的合議，不是單一判讀。任何想進入這個流程的模型，都必須先回答它要站在哪一格：是幫初判者排序與標示、是作為第二判讀的輔助、還是只做量測與追蹤比對。這三種定位對應的法規風險分級與驗證要求並不相同。公告未觸及這一題。
- **「歐洲資料主權」在這則裡是動機陳述，不是可驗證的事實。** 公告寫此類專案過去常依賴歐洲以外的資料，但沒有給出任何依據，也沒有說明這次的資料會存放在哪裡、由誰持有、使用目的如何界定與終止。Hübner 的引言把治理、目的界定與資料保護列為關鍵因素，這是正確的方向；但公告提供的是對這些原則的宣示，不是這些原則的具體內容。評估這類合作時，宣示與條款不能互相替代。
- **重點行與正文的時態落差值得在轉述時守住。** 只讀重點行的人會得到「肺癌篩檢試辦已經開始」，讀完正文的人得到的是「演算法將要被開發」。這兩種說法在半年後回看會導向不同的進度判斷。在內部技術雷達上，本則應記為「已簽協議、資料供給安排已定、演算法尚未開發完成」。

## 產業影響

- **對醫療影像 AI 的資料端而言**，本則的意義在於供給側的形狀：一家設備商以協議取得單一醫院集團的縱向資料，而不是向多個來源零散採購或依賴公開資料集。這種安排的好處是資料結構一致、可追加欄位、並有同一批院所可供後續評估；代價則是族群與作業慣例集中於一個集團，外部化（external validation）必須另外安排。公告沒有提到任何外部驗證計畫。
- **對歐洲的臨床資料市場而言**，Sana 把資料業務放在一家獨立子公司（Sana Data Solutions GmbH）這件事本身是一個訊號：醫院集團正在把資料供給當成一條可簽約、可治理、可重複的業務線，而不是個案式的研究合作。對其他正在評估類似安排的醫療機構而言，這是一個可參照的組織形態。
- **對設備商的競爭態勢而言**，本書庫近一個月記錄的多則大廠公告，多半是圍繞一台機器或一項已取得許可的功能組建多機構網絡；本則則把網絡建在訓練階段之前。若這種「先談資料、後談產品」的安排成為常態，臨床資料的取得條件會比演算法更早決定誰能做出什麼。
- **對台灣的醫療機構而言**，本則可直接對照的是資料供給的治理形態而非技術內容。以單一院所或體系為單位與廠商簽訂長期資料協議時，本則公告沒有回答的那幾題 —— 資料存放地、使用目的範圍、二次利用與終止條件、評估階段的角色衝突 —— 正是合約階段必須先寫清楚的部分。

## 與書庫其他文章的關係

兩則都是大廠把多家醫療機構圈成一個研究供給網，拿到的東西卻不同：該則聯盟換到的是九家機構圍繞一台研究用機器的使用與交流意向，本則協議換到的是一家醫院集團的影像、標註與放射報告，以及事後在同一批院所內評估的場域: [不談 AI 拼硬體梯度：GE 籌組九機構 MAGNUS 神經影像聯盟解析](2026-11-11-ge-healthcare-magnus-neuro-alliance.md)

該則的光子計數 CT 已取得美國 510(k) 許可，七家機構是在許可之後才展開結構化評估；本則連受評的軟體都還沒有，醫療機構供應的是訓練階段的輸入。同樣是大廠與醫療機構的結構化合作，分別落在法規後與訓練前: [先過審再收證據：GE Photonova Spectra 七機構評估解析](2026-11-19-ge-healthcare-photonova-spectra-pcct-collaborations.md)

該則的報告草稿功能把放射報告當成產出端的目標，本則的協議則把放射報告列為要交付給廠商的訓練輸入之一。同一種文件在兩則裡分別站在模型的輸出端與輸入端: [不碰判讀只做文書：InteleOrchestrator Clarity 拆解](2026-11-26-ge-healthcare-inteleorchestrator-clarity-reporting.md)

## 實務的啟發

- **轉述本則時，把動詞與階段一起記下。** 公告寫的是簽訂協議與「將要開發」，不是「已推出肺癌篩檢 AI」。在技術雷達或競品追蹤表上，本則應記為協議階段，並在同一行註明：無產品名、無法規路徑、無時程。只記下「Siemens 與 Sana 合作肺癌篩檢 AI」，半年後回看會高估進度。
- **評估資料合作案時，先問資料的四個維度再談模型。** 本則公告把影像、標註、放射報告列為第一批交付內容，是一個好的檢查清單起點：資料型態（影像／標註／文字／結構化欄位）、時間範圍與筆數、去識別化作法與殘餘風險、以及後續可追加的欄位。本則四項皆未揭露量的資訊，若本單位要簽類似協議，這四項應該在意向書階段就寫進去。
- **訓練資料來源與評估場域重疊時，要在計畫書裡先處理。** 本則的訓練資料與第二步評估都來自同一個醫院集團。這在實務上常見且有其效率，但評估結果的可外推性會受限。規劃院內 AI 導入研究時，建議預先區分「開發資料集」「院內評估資料集」與「外部驗證資料集」三層，並寫明三者的來源與時間切點。
- **若模型要進入法定篩檢流程，先確認它要站在流程的哪一格。** 德國的低劑量 CT 肺癌篩檢有法定的初判與第二判讀安排。導入任何輔助工具之前，應先界定它是影響初判、影響第二判讀、還是只在合議之後做量測與追蹤。不同的位置對應不同的驗證設計與責任歸屬，這件事應在採購或研究設計階段就定案，而不是等工具上線後再討論。
- **把報告與標註當成受保護資產看待。** 放射報告是自由文字，去識別化的難度高於影像標頭；標註則代表判讀者的時間投入。醫療機構若要提供這兩類資料，建議在合約中分別約定其使用目的、是否可用於與本專案無關的模型訓練，以及專案結束後的處置方式，而不是用一條概括的「研究用途」涵蓋。
- **「符合法規要求」這句話不能當成合規佐證。** 本則公告以 `while complying with regulatory requirements` 一語帶過，未指名任何法規、標準或機制。在內部審查文件中引用廠商材料時，應要求對方指出具體條文或標準編號；概括語句不具備可稽核性。

## 後續追蹤

- 本次合作是否會出現協議全文、資料使用條款、資料保護影響評估或倫理審查文件的公開版本。
- 肺癌篩檢專案的資料規模：筆數、時間範圍、納入的 Sana 院所數，以及標註的產生方式與一致性安排。
- 公告所稱已啟動的 pilot phase 具體指哪一部分、起始時點為何，以及重點行與正文的時態落差是否會被更正。
- 開發中的演算法未來的醫療器材法規路徑與風險分級，以及是否會進入歐盟醫療器材法規（Medical Device Regulation，MDR）2017/745 的符合性評鑑程序。
- 第二步在 Sana 院所的評估屬於何種性質（內部驗證、前瞻性臨床評估或上市後觀察），以及是否會有登錄編號與公開的終點指標。
- 是否會安排 Sana 體系之外的外部驗證，以及資料與評估場域重疊的問題將如何在發表時揭露。
- 公告所稱 `curated health data` 與肺癌篩檢專案所稱 `anonymized data` 是否為同一批資料，以及去識別化採用的標準。
- 德國肺癌篩檢計畫自 2026 年 4 月開辦後的實際檢查量與第二判讀發動比例，將決定這類工具的需求規模；G-BA 或相關機構是否會公布這些統計。
- 台灣的醫療機構若要比照設立資料供給子公司或簽訂長期資料協議，個人資料保護法與人體研究相關規範下的可行形態為何。

## References

- `shs` — Siemens Healthineers and Sana Kliniken collaborate on AI solutions for healthcare（Siemens Healthineers 官方新聞稿頁，頁面可見標示 Published on November 17, 2026，自標 Joint Press Release by Siemens Healthineers and Sana Kliniken；含三行重點、兩段具名引言與兩家公司制式簡介）  
  <https://www.siemens-healthineers.com/press/releases/sana>
- `sana` — Siemens Healthineers und Sana arbeiten gemeinsam an KI-Lösungen für die Gesundheitsversorgung（Sana Kliniken AG 新聞室，發稿行 Ismaning，17 November 2026；同一份聯合新聞稿的德文版）  
  <https://www.sana.de/newsroom/siemens-healthineers-und-sana-arbeiten-gemeinsam-an-ki-loesungen-fuer-die-gesundheitsversorgung/>
- `gba` — Lungenkrebs-Früherkennung für Raucherinnen und Raucher（Gemeinsamer Bundesausschuss 主題頁；含「Seit April 2026」的給付起點、年齡與包年門檻，以及 Erstbefundung／Zweitbefundung 的法定流程）  
  <https://www.g-ba.de/themen/methodenbewertung/erwachsene/krebsfrueherkennung/lungenkrebs-screening/>
- `gba_beschluss` — Krebsfrüherkennungs-Richtlinie: Einführung der Lungenkrebsfrüherkennung mittels Niedrigdosis-Computertomographie bei Rauchern（G-BA 決議頁；Beschlussdatum 18.06.2025、Inkrafttreten 05.09.2025、BAnz AT 04.09.2025 B3）  
  <https://www.g-ba.de/beschluesse/7301/>

[Home](../) · [Industry Watch](./)
