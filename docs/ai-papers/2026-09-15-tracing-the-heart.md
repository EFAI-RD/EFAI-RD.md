---
title: "Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）"
category: ai-papers
date: 2026-09-15
updated: 2026-09-15
tags: [LLM, multi-agent, EHR, heart-failure, feature-engineering, evidence-linked]
catalog_id: "arxiv:2608.06366"
source:
  orgs:
    - "Nimblemind"
    - "Singapore University of Technology and Design"
    - "University of Illinois Urbana-Champaign"
    - "Florida International University"
    - "University of California Los Angeles"
    - "Rutgers University / Rutgers Health"
  paper_title: "Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering"
  venue: "arXiv preprint；投稿 ML4H 2026"
  url: "https://arxiv.org/abs/2608.06366"
  html_url: "https://arxiv.org/html/2608.06366"
related_articles: []
refs:
  main:
    title: "Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering"
    url: "https://arxiv.org/html/2608.06366"
    abs_url: "https://arxiv.org/abs/2608.06366"
    anchors:
      abstract: "#abstract1"
      s1: "#S1"
      s2: "#S2"
      s3: "#S3"
      s4: "#S4"
      s4_fig: "#S4.fig1"
      s5: "#S5"
      s6: "#S6"
figures:
  - path: "assets/nmas-pipeline-overview.svg"
    caption: "nMAS 特徵工程流程摘要（EFAI-RD 重繪）"
    origin: efai
  - path: "assets/2608.06366-architecture.png"
    caption: "原文架構圖（arXiv HTML：architecture.png）"
    origin: paper
status: published
skill_version: "write-ai-paper@1.1"
evidence_reviewed: true
---

# Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）

## 來源

- **單位／團隊**：**Nimblemind** 主導、與 Singapore University of Technology and Design、UIUC、FIU、UCLA、Rutgers 等機構合作（見原文作者單位）
- **論文**：*Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering*
- **識別**：[arXiv:2608.06366](https://arxiv.org/abs/2608.06366) · [HTML 全文](https://arxiv.org/html/2608.06366) · 投稿 ML4H 2026

一句話：作者提出 **nMAS**（Nimblemind Multi-Agent System），用「臨床 rubric + 可追溯證據鏈」自動做心衰竭（heart failure, HF）EHR 特徵工程，並在 500 筆 dummy 資料上示範可審計、可提升表型分型預測。

## 圖／流程

![nMAS 流程摘要（EFAI-RD 重繪）](assets/nmas-pipeline-overview.svg)

*圖 1：nMAS 特徵工程流程摘要（EFAI-RD 重繪；細節以原文為準）。*

![原文 nMAS 架構圖](assets/2608.06366-architecture.png)

*圖 2：原文架構圖，取自 arXiv HTML [`architecture.png`](https://arxiv.org/html/2608.06366v1/architecture.png)；對應方法流程見 [(ref: main §4 圖)](https://arxiv.org/html/2608.06366#S4.fig1)。*

## 背景／問題

臨床機器學習前，常要把異質 EHR 清成病人層級變數；作者引用資料科學家約有 **39–45%** 工時花在載入與清理，而非分析 [(ref: main §1)](https://arxiv.org/html/2608.06366#S1)。心衰竭尤其棘手：診斷、用藥、檢驗、影像與行為史分散在多表，且表型依賴指引中的射血分率（ejection fraction, EF）門檻等明確定義 [(ref: main §1)](https://arxiv.org/html/2608.06366#S1) [(ref: main §2)](https://arxiv.org/html/2608.06366#S2)。既有規則式或 LLM 管線多半只能部分自動化，**可維護性與證據可追溯性**不足 [(ref: main Abstract)](https://arxiv.org/html/2608.06366#abstract1)。

## 方法摘要

nMAS 是 **evidence-linked、rubric-grounded** 的多代理管線 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)：

1. **Achievability Agent**：先檢查來源資料是否撐得起目標特徵；缺輸入則標 unsupported，不硬猜 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
2. **Stage 1**：九張 EHR 表標準化、去重、時間彙總後併成「一病人一列」結構化表 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
3. **Stage 2**：依版本化臨床評分 rubric 產生高階複合特徵；每項附 **structured evidence trace**（成分、分數、來源欄、輸入是否存在）[(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
4. **LLM auditor**（文中為 Qwen 2.5-1.5B-Instruct）：在白名單欄位內做有界校正，保護證據軌跡欄位 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
5. Rubric 由小型 LLM 彙整指引文獻草案，再經**心臟專科醫師全份審核**；定稿含 **2023 年起 22 篇**參考文獻 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

重點設計：缺失值保持缺失（不把缺 EF 填 0）；表型優先用數值 EF，否則用 ICD／診斷碼，**不插補 EF** [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

## 資料與實驗

- **500** 筆 dummy HF 病人紀錄，來自九張結構化 EHR 表 [(ref: main §3)](https://arxiv.org/html/2608.06366#S3)。
- 數值 EF 僅 **3.0%**（15/500）病人有，多數表型需診斷名／碼後援 [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- 下游次要評估：XGBoost 做 HFrEF vs phenotype-unknown、HFpEF vs phenotype-unknown；比較 baseline vs 加入複合特徵；5-fold × 10 shuffle [(ref: main §4)](https://arxiv.org/html/2608.06366#S4) [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。

## 結果

- Stage 1：正好 **500** 列、**132** 個結構化欄位 [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- Stage 2：**70** 個 rubric 評分／彙總欄位，全部列經 LLM auditor [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- 加入彙總特徵後，平均 AUROC：HFrEF **0.895 → 0.963**；HFpEF **0.870 → 0.910** [(ref: main Abstract)](https://arxiv.org/html/2608.06366#abstract1) [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- 獨立 LLM（Claude Opus 4.8）建構效度：整體約 **81.5%** 滿分 [(ref: main Abstract)](https://arxiv.org/html/2608.06366#abstract1) [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- Ablation：等權／隨機權重明顯變差，支持 rubric 權重而非只靠特徵數量 [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。

## 限制

單機構、**dummy** 世代、樣本 500；任務是 HF **表型分型**（對 phenotype-unknown），不是對非 HF 對照的疾病偵測；部分特徵可能與標籤證據重疊；未做前瞻臨床效益等 [(ref: main §6)](https://arxiv.org/html/2608.06366#S6)。

## 與書庫舊文的關係

書庫目前尚無直接相關定稿文章；本篇可觸發後續 `ai-basics`（evidence-linked feature engineering、rubric-grounded agent）。

## 對 EFAI／實務的啟發

1. **Evidence-linked** 要能指回來源欄與評分規則——與本庫「可點 ref → 原文段落」同一精神。
2. LLM 角色框在 **rubric 起草／有界稽核**，執行評分偏 deterministic。
3. 評估誠實標示 dummy／單中心；落地仍需外部驗證。

## References

- **main** — Shimgekar et al. *Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering*.  
  [HTML（可深鏈）](https://arxiv.org/html/2608.06366) · [abs](https://arxiv.org/abs/2608.06366)  
  Anchors：[`#abstract1`](https://arxiv.org/html/2608.06366#abstract1) · [`#S1`](https://arxiv.org/html/2608.06366#S1) · [`#S3`](https://arxiv.org/html/2608.06366#S3) · [`#S4`](https://arxiv.org/html/2608.06366#S4) · [`#S4.fig1`](https://arxiv.org/html/2608.06366#S4.fig1) · [`#S5`](https://arxiv.org/html/2608.06366#S5) · [`#S6`](https://arxiv.org/html/2608.06366#S6)
