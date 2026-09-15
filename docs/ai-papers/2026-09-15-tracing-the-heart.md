---
title: "Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）"
category: ai-papers
date: 2026-09-15
updated: 2026-09-15
tags: [LLM, multi-agent, EHR, heart-failure, feature-engineering, evidence-linked]
catalog_id: "arxiv:2608.06366"
related_articles: []
refs:
  main:
    title: "Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering"
    url: "https://arxiv.org/abs/2608.06366"
    locator: "Abstract; §3–§6"
status: published
skill_version: "write-ai-paper@1.0"
evidence_reviewed: true
---

# Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）

一句話：這篇提出 **nMAS**（Nimblemind Multi-Agent System），用「臨床 rubric + 可追溯證據鏈」自動做心衰竭（heart failure, HF）EHR 特徵工程，並在 500 筆 dummy 資料上示範可審計、可提升表現型分型預測。

## 背景／問題

臨床機器學習前，常要把異質 EHR 清成病人層級變數；作者引用資料科學家約有 **39–45%** 工時花在載入與清理，而非分析 (ref: main §1)。心衰竭尤其棘手：診斷、用藥、檢驗、影像與行為史分散在多表，且表型依賴指引中的射血分率（ejection fraction, EF）門檻等明確定義 (ref: main §1–§2)。既有規則式或 LLM 管線多半只能部分自動化，**可維護性與證據可追溯性**不足 (ref: main Abstract)。

## 方法摘要

nMAS 是 **evidence-linked、rubric-grounded** 的多代理管線 (ref: main §4)：

1. **Achievability Agent**：先檢查來源資料是否撐得起目標特徵；缺輸入則標 unsupported，不硬猜 (ref: main §4)。
2. **Stage 1**：九張 EHR 表標準化、去重、時間彙總後併成「一病人一列」結構化表 (ref: main §4)。
3. **Stage 2**：依版本化臨床評分 rubric 產生高階複合特徵；每項附 **structured evidence trace**（成分、分數、來源欄、輸入是否存在）(ref: main §4)。
4. **LLM auditor**（文中為 Qwen 2.5-1.5B-Instruct）：在白名單欄位內做有界校正，保護 `_json`／`_explanation` 等證據軌跡欄位 (ref: main §4)。
5. Rubric 由小型 LLM 彙整指引文獻草案，再經**心臟專科醫師全份審核**；定稿含 **2023 年起 22 篇**參考文獻，並連到各評分元件 (ref: main §4)。

重點設計選擇：缺失值保持缺失（例如不把缺 EF 填 0）；表型優先用數值 EF，否則用 ICD／診斷碼，**不插補 EF** (ref: main §4)。

## 資料與實驗

- **500** 筆 dummy HF 病人紀錄，來自九張結構化 EHR 表（人口學、診斷、用藥、超音波／手術、檢驗、EF flowsheet、社會史等）(ref: main §3, §5)。
- 數值 EF 僅 **3.0%**（15/500）病人有，多數表型需診斷名／碼後援 (ref: main §5 Table)。
- 下游次要評估：XGBoost 做 HFrEF vs phenotype-unknown、HFpEF vs phenotype-unknown；比較「僅清洗合併變數」vs「再加上複合特徵」；5-fold × 10 shuffle (ref: main §4–§5)。

## 結果

- Stage 1：正好 **500** 列、**132** 個結構化欄位、無重複列 (ref: main §5)。
- Stage 2：**70** 個 rubric 評分／彙總欄位，且全部列經 LLM auditor (ref: main §5)。
- 加入彙總特徵後，held-out 平均 AUROC：HFrEF **0.895 → 0.963**；HFpEF **0.870 → 0.910** (ref: main Abstract; §5 Table)。
- 獨立 LLM（Claude Opus 4.8）建構效度評分：整體正規化約 **81.5%** 滿分 (ref: main Abstract; §5)。
- Ablation：等權／隨機權重明顯變差，支持「rubric 權重」而非「只靠特徵數量」 (ref: main §5)。

## 限制

作者明列：單機構、**dummy** 世代、樣本 500；任務是 HF **表型分型**（對 phenotype-unknown），不是對非 HF 對照的疾病偵測；部分特徵可能與標籤證據重疊；未做前瞻臨床效益；regex／機構用語可能漏抓；臨床審查涵蓋 rubric 與代表輸出，非全世代逐筆 (ref: main §6)。

## 與書庫舊文的關係

書庫目前尚無直接相關定稿文章；本篇可作為後續 `ai-basics`（例如 evidence-linked feature engineering、rubric-grounded agent）的觸發來源。

## 對 EFAI／實務的啟發

1. **Evidence-linked** 不只是引用論文：特徵輸出要能指回來源欄與評分規則——與本庫「`(ref: xxx)` + URL」同一精神，可遷移到 EHR 特徵產線。
2. LLM 角色被框在 **rubric 起草／有界稽核**，執行評分偏 **deterministic**，降低「模型自由發揮臨床結論」的風險。
3. 評估誠實標示 dummy／單中心與表型任務定義；落地前仍需外部驗證與真實資料治理。

## References

- **main** — Shimgekar et al. *Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering*. arXiv:2608.06366 (submitted to ML4H 2026).  
  https://arxiv.org/abs/2608.06366  
  （HTML：https://arxiv.org/html/2608.06366 ）  
  Locator：Abstract（工作量 39–45%、AUROC、81.5%、nMAS 摘要）；§1（問題設定）；§3（500 病人、九表）；§4（管線、rubric、auditor、EF 規則）；§5（132／70 欄、EF 3.0%、結果表）；§6（限制）。
