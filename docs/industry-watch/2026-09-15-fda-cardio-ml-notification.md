---
title: "FDA 將心血管 ML 通知軟體定為 Class II：通報≠診斷"
category: industry-watch
date: 2026-09-15
updated: 2026-09-15
tags: [FDA, Class-II, cardiovascular, machine-learning, SaMD, regulation]
catalog_id: "fda:fr-2026-18612-cardio-ml-notification"
editors:
  - "Curitis"
source:
  orgs:
    - "U.S. Food and Drug Administration (FDA)"
  event: "Final order classifying cardiovascular machine learning-based notification software (21 CFR 870.2380)"
  event_date: "2026-09-11"
  official_url: "https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based"
related_articles:
  - path: "../ai-papers/2026-09-15-tracing-the-heart.md"
    relation: "cardiovascular AI context; research pipeline vs regulated notification software"
refs:
  fr_order:
    title: "Classification of the Cardiovascular Machine Learning-Based Notification Software"
    url: "https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based"
  fr_pdf:
    title: "Federal Register PDF 2026-18612"
    url: "https://www.govinfo.gov/content/pkg/FR-2026-09-11/pdf/2026-18612.pdf"
  ecfr:
    title: "21 CFR 870.2380"
    url: "https://www.ecfr.gov/current/title-21/section-870.2380"
status: published
skill_version: "write-industry-watch@2.3"
evidence_reviewed: true
---

**導覽：** [Home](../) · [Industry Watch](./)

# FDA 將心血管 ML 通知軟體定為 Class II：通報≠診斷

## 來源

- **組織**：美國 FDA（Food and Drug Administration）
- **事件**：最終命令（final order）將 *cardiovascular machine learning-based notification software* 編入 **Class II（special controls）**，並新增 [21 CFR 870.2380](https://www.ecfr.gov/current/title-21/section-870.2380)
- **日期**：命令生效 **2026-09-11**；分類自 **2023-08-03** 起已適用
- **官方入口**：[Federal Register 文件 2026-18612](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based) · [GovInfo PDF](https://www.govinfo.gov/content/pkg/FR-2026-09-11/pdf/2026-18612.pdf)

**編輯：** Curitis

FDA 在 2026 年 9 月把「用機器學習提示單一心血管疾患可能性、供後續轉介／檢查」的軟體類型正式寫進 Class II；重點是**通知／分流**，不是診斷級輸出。

## 流程

1. **2023-01-10**：Viz.ai, Inc. 就 **Viz HCM** 提出 De Novo 分類請求 [(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based)。
2. **2023-08-03**：FDA 以書面命令將該裝置類型列為 Class II（special controls）[(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based)。
3. **2026-09-11**：Federal Register 刊登最終命令，**成文法化**為 21 CFR 870.2380，並重申生效日與既有適用日 [(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based) [(ref: ecfr)](https://www.ecfr.gov/current/title-21/section-870.2380)。

## 事實（可核對）

- **識別（intended use 邊界）**：此類軟體以 ML 提示某心血管疾病／狀況的可能性，供進一步轉介或診斷追蹤；依**單一狀況**、一或多個**非侵入生理輸入**運作；作為後續檢查依據，**不提供 diagnostic quality output**；**不**用於辨識／偵測心律不整 [(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based) [(ref: ecfr)](https://www.ecfr.gov/current/title-21/section-870.2380)。
- **分類**：Class II（special controls）[(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based)。
- **為何走 De Novo／成文法**：FDA 認為一般控制不足，但可建立 special controls 以合理保證安全有效；De Novo 後該類型可作為後續 510(k) 的 predicate，降低重複走 De Novo／PMA 的負擔 [(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based)。
- **Special controls（摘要，非法規全文替代）**包括：臨床性能測試（真實世界、具代表性、與訓練集獨立、至少三個地理分散測試站點等）、軟體驗證／危害分析、人因評估（誤讀輸出風險）、以及標示要求（含性能摘要、限制族群、**不得以「沒有警示」排除追蹤**、不得取代完整臨床評估等）[(ref: fr_order)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based) [(ref: fr_pdf)](https://www.govinfo.gov/content/pkg/FR-2026-09-11/pdf/2026-18612.pdf)。

## 本書庫解讀（評論）

- **對醫療 AI 產品**：這條路徑清楚區分「風險分層／通知」與「診斷」；行銷若把 notification 說成診斷，會與成文識別衝突。
- **對研究筆記讀者**：學術管線（例如特徵工程、報告生成）≠ 已受規管的通知軟體；落地美國市場仍須對齊 intended use 與 special controls，不能只靠論文指標。
- **時間差**：分類自 2023-08 已適用，2026-09 的 FR 是把既有 De Novo 結果**編入 CFR**；解讀時勿誤成「2026 才第一次准許此類裝置」。

## 產業／法規生態影響

- 同類型心血管 ML 通知軟體可較明確走 **510(k) + special controls**，而不是每次 De Novo。
- 標示與臨床驗證門檻（多中心、族群／設備亞組、人因）會成為競品對標清單。

## 與書庫其他文章的關係

一句話敘述關係: [Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）](../ai-papers/2026-09-15-tracing-the-heart.md) 同屬心血管／心衰竭 AI 脈絡；本則補上美國對「ML 通知軟體」的成文分類與「通報≠診斷」邊界。

## 實務的啟發

1. 寫 intended use 時先問：輸出是「建議再查」還是「診斷結論」——本類型明文排除後者。
2. 驗證計畫預留：訓練／測試分離、多站點、亞組與硬體差異、以及標示警告（含陰性結果不可當排除）。
3. 讀 FR／eCFR 原文；二手新聞標題常省略「notification／非診斷」關鍵句。

## References

- **fr_order** — [Federal Register：Classification of Cardiovascular Machine Learning-Based Notification Software (2026-18612)](https://www.federalregister.gov/documents/2026/09/11/2026-18612/medical-devices-cardiovascular-devices-classification-of-the-cardiovascular-machine-learning-based)
- **fr_pdf** — [GovInfo PDF](https://www.govinfo.gov/content/pkg/FR-2026-09-11/pdf/2026-18612.pdf)
- **ecfr** — [21 CFR 870.2380](https://www.ecfr.gov/current/title-21/section-870.2380)

**導覽：** [Home](../) · [Industry Watch](./)
