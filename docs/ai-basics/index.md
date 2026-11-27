---
title: AI Basics
nav_order: 3
has_children: true
has_toc: false
---

[Home](../) · [AI Basics](./)

# AI Basics

消化 AI Papers 中「一次講不完」的大方向概念（發展由來與 landmark papers）。

## 文章列表

| 日期 | 標題 | 編輯 | 備註 |
|------|------|------|------|
| 2026-11-27 | [放射報告評估指標：從 BLEU 到 GREEN，三個新分數都拿同 50 例驗證](radiology-report-generation-metrics.md) | Clara | topic:radiology-report-metrics；放射報告生成自動評估指標的譜系：字詞重疊（BLEU、ROUGE）、表徵相似度（BERTScore）、固定標籤（CheXpert labeler、CheXbert 的 CE-F1）、實體與關係圖（RadGraph F1）、組合與模型評估（RadCliQ、GREEN、RadFact、RaTEScore）到 ReXrank 排行榜。RadCliQ 以 ReXVal（6 位放射科醫師、50 個 MIMIC-CXR 檢查、200 份報告）擬合，GREEN 與 RaTEScore 也在同一份資料上驗證；GREEN 表 6 的 Kendall tau：GREEN 0.63、RadCliQ-v1 0.61、F1RadGraph 0.57、BLEU 0.35。整理同名指標定義不一、CE-F1 只看 14 類、指標被拿來當 reward 等常見誤解 |
| 2026-11-18 | [LFM：名字來自液態時間常數網路，主幹卻是閘控短卷積](liquid-foundation-models.md) | Clara | topic:liquid-foundation-models |
| 2026-09-17 | [醫療視覺語言模型：從 CLIP 對齊到有定位報告](medical-vlm.md) | Curitis | topic:medical-vlm |
| 2026-09-15 | [LLM 多代理系統：從 ReAct 到可對話協作](multi-agent-llm.md) | Curitis | topic:multi-agent-llm |

[Home](../) · [AI Basics](./)
