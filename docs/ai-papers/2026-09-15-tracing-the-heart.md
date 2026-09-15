---
title: "Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）"
category: ai-papers
date: 2026-09-15
updated: 2026-09-15
tags: [LLM, multi-agent, EHR, heart-failure, feature-engineering, evidence-linked]
catalog_id: "arxiv:2608.06366"
editors:
  - "Curitis"
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
related_articles:
  - path: "../ai-basics/multi-agent-llm.md"
    relation: "multi-agent lineage background"
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
  - path: "assets/nmas-pipeline-overview.png"
    caption: "nMAS 特徵工程流程摘要（EFAI-RD 重繪）"
    origin: efai
  - path: "assets/2608.06366-architecture.png"
    caption: "原文架構圖（arXiv HTML：architecture.png）"
    origin: paper
status: published
skill_version: "write-ai-paper@1.4"
evidence_reviewed: true
---

**導覽：** [Home](../) · [AI Papers](./)

# Tracing the Heart：證據可追溯的心衰竭特徵工程管線（nMAS）

## 來源

- **單位／團隊**：**Nimblemind** 主導，並與 Singapore University of Technology and Design、UIUC、FIU、UCLA、Rutgers 等機構合作
- **論文**：*Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering*
- **識別**：[arXiv:2608.06366](https://arxiv.org/abs/2608.06366) · [HTML 全文](https://arxiv.org/html/2608.06366) · 投稿 ML4H 2026

**編輯：** Curitis

一句話：作者提出 **nMAS**（Nimblemind Multi-Agent System），用「臨床 rubric + 可追溯證據鏈」自動做心衰竭（heart failure, HF）EHR 特徵工程，並在 500 筆 dummy 資料上示範可審計、可提升表型分型預測。

## 流程

![nMAS 流程摘要（EFAI-RD 重繪）](assets/nmas-pipeline-overview.png)

*圖 1：nMAS 特徵工程流程摘要（EFAI-RD 重繪）。*

![原文 nMAS 架構圖](assets/2608.06366-architecture.png)

*圖 2：原文架構圖，取自 arXiv HTML [`architecture.png`](https://arxiv.org/html/2608.06366v1/architecture.png)；方法見 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。*

## 背景／問題

臨床機器學習前，常要把異質 EHR 清成病人層級變數；作者引用資料科學家約有 **39–45%** 工時花在載入與清理，而非分析 [(ref: main §1)](https://arxiv.org/html/2608.06366#S1)。心衰竭尤其棘手：診斷、用藥、檢驗、影像與行為史分散在多表，且表型依賴指引中的射血分率（ejection fraction, EF）門檻等明確定義 [(ref: main §1)](https://arxiv.org/html/2608.06366#S1) [(ref: main §2)](https://arxiv.org/html/2608.06366#S2)。既有規則式或 LLM 管線多半只能部分自動化，**可維護性與證據可追溯性**不足 [(ref: main Abstract)](https://arxiv.org/html/2608.06366#abstract1)。

## 方法摘要

nMAS 是 **evidence-linked、rubric-grounded** 的多代理管線 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)：

1. **Achievability Agent**：檢查來源是否撐得起目標特徵；缺輸入則標 unsupported [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
2. **Stage 1**：九表標準化 → 去重 → 時間彙總 → 一病人一列 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
3. **Stage 2**：版本化臨床 rubric 產出複合特徵 + structured evidence trace [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
4. **LLM auditor**（Qwen 2.5-1.5B-Instruct）：白名單內有界校正 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。
5. Rubric 由小型 LLM 草案 + **心臟專科醫師全份審核**（2023 年起 22 篇文獻）[(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

## 方法詳解

以下對照圖 1／圖 2，展開 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4) 的特徵工程管線。

### 請求進入與可行性

流程以「EHR 匯出 + 版本化 rubric 目標特徵」為請求。**Achievability Agent** 先對每個目標特徵檢查必要輸入是否存在；撐不起來的特徵標成 unsupported，而不是用模型臆測補值 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。通過後，Query Parser 路由到對應 nMAS 管線。

### Stage 1：從九表到病人層級寬表

1. **標準化**：空白壓縮、空字串／`"nan"`→ null、病人 ID 大寫、EHR 時間轉 ISO [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。  
2. **去重**：各表用臨床有意義的事件鍵去重 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。  
3. **時間彙總**：每張來源表先壓到病人層，再 merge 成唯一病人列 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。  
4. **EF 解析**：區間字串拆成低／高／中點，再算最低、最高、最近 EF [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。  
5. **缺失策略**：連續測量保留 missing、**不填 0** [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

臨床推理層會把文字／代碼轉成可解釋旗標；HF 表型以 ICD 衍生值為主，並在與診斷名衝突時掛 conflict flag [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

### Stage 2：Rubric 複合特徵與證據軌跡

Rubric 定義條件、給分與證據階層；七類分數加總後上限 100，再映到 high（≥55）／medium（25–54）／low（&lt;25）[(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。**HF 表型**採 EF 門檻或 ICD 路徑，**不插補 EF** [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

### LLM Auditor 與品管

本機 Qwen 2.5-1.5B-Instruct 僅改白名單欄位；另有 harness 查表型互斥、rubric 合規與 provenance [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)。

## 資料與實驗

### 資料

評估使用 **500** 筆 dummy HF 病人紀錄（單機構、去識別）[(ref: main §3)](https://arxiv.org/html/2608.06366#S3) [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。

**表 A — 世代特徵** [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)

| 項目 | 數值 |
|------|------|
| 總病人數 | 500 |
| 男性 | 256 (51.2%) |
| 女性 | 243 (48.6%) |
| 未註明性別 | 1 (0.2%) |
| 平均 BMI（n=266） | 29.99 |
| 慢性腎病 | 227 (45.4%) |
| 糖尿病 | 208 (41.6%) |
| 冠狀動脈疾病 | 202 (40.4%) |
| 心房顫動 | 175 (35.0%) |
| 有數值 EF | 15 (3.0%) |
| 有 BNP／NT-proBNP | 154 (30.8%) |
| 有 Troponin | 429 (85.8%) |

**表 B — 九張 EHR 來源表** [(ref: main §3)](https://arxiv.org/html/2608.06366#S3)

| 來源表 | 說明 | 欄位舉例 |
|--------|------|----------|
| PatientBase | 人口學與主要診斷 | ID、年齡、性別、種族、BMI、血壓、ICD、診斷名 |
| OtherDiagnosis | 其他 ICD 診斷 | ICD-10、診斷名、日期 |
| Medications | 縱向用藥 | 藥名、藥理／治療分類、開立日 |
| EchoProcs | 心臟超音波處置 | 處置碼／名、開立日 |
| Surgery | 手術 | 術式、日期、醫院／科別 |
| LabsComponents | 院內檢驗 | 項目、結果日、單位、異常旗標 |
| LabsExternal | 外院檢驗 | 項目、數值、單位、採檢時間 |
| EjectionFraction | EF 紀錄 | EF 值／區間、紀錄時間 |
| SocialHx | 社會史 | 菸、酒、非法藥物使用 |

### 實驗

次要評估：XGBoost；任務為 HFrEF／HFpEF 各自 vs phenotype-unknown；比較 baseline（清洗合併變數）與加入複合特徵；5-fold × 10 shuffle [(ref: main §4)](https://arxiv.org/html/2608.06366#S4) [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。

**表 C — 分型預測績效（mean ± SD）** [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)

| Task | Features | Accuracy | AUROC | F1 |
|------|----------|----------|-------|-----|
| HFrEF | Baseline | 0.776 ± 0.065 | 0.895 ± 0.046 | 0.776 ± 0.063 |
| HFrEF | Aggregated | 0.896 ± 0.049 | 0.963 ± 0.028 | 0.894 ± 0.052 |
| HFpEF | Baseline | 0.752 ± 0.056 | 0.870 ± 0.042 | 0.758 ± 0.058 |
| HFpEF | Aggregated | 0.809 ± 0.061 | 0.910 ± 0.040 | 0.812 ± 0.059 |

**表 D — LLM 建構效度（正規化分數 %）** [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)

| Feature Category | Normalized Score (%) |
|------------------|----------------------|
| Blood Comorbidities | 93.8 |
| Cardiovascular Risk | 93.4 |
| Brain Comorbidities | 91.3 |
| Kidney Comorbidities | 90.6 |
| Behavioral Risk | 89.5 |
| Lung Comorbidities | 88.5 |
| Metabolic Comorbidities | 85.5 |
| Disease Severity | 74.6 |
| Demographic Vulnerability | 63.1 |
| Gap Features | 60.6 |
| Care Recommendations | 38.5 |
| Overall | 81.5 |

完整八類 rubric 給分表見原文附錄 Table 1 [(ref: main §4)](https://arxiv.org/html/2608.06366#S4)；去重鍵與彙總量見附錄來源表說明。

## 結果

- Stage 1：**500** 列、**132** 結構化欄；Stage 2：**70** 個 rubric 欄 [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- 加入彙總特徵後 AUROC：HFrEF **0.895 → 0.963**；HFpEF **0.870 → 0.910**（見表 C）[(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。
- 建構效度整體 **81.5%**（見表 D）[(ref: main Abstract)](https://arxiv.org/html/2608.06366#abstract1)。
- 等權／隨機權重 ablation 變差，支持 rubric 權重 [(ref: main §5)](https://arxiv.org/html/2608.06366#S5)。

## 限制

單機構、**dummy**、n=500；任務是 HF 表型分型（非 vs 非 HF 對照）；可能有特徵—標籤證據重疊；未做前瞻臨床效益等 [(ref: main §6)](https://arxiv.org/html/2608.06366#S6)。

## 與書庫其他文章的關係

一句話敘述關係: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md) 提供閱讀 nMAS「專責代理＋有界稽核」時所需的多代理譜系背景。

## 實務的啟發

1. 特徵輸出應能指回來源欄與評分規則，方便稽核與複現。
2. LLM 宜框在 rubric 起草／有界稽核；執行評分可偏 deterministic。
3. 誠實標示 dummy／單中心；落地仍需外部驗證。

## References

- **main** — Shimgekar et al. *Tracing the Heart: An Evidence-Linked Pipeline for Heart-Failure Feature Engineering*.  
  [HTML](https://arxiv.org/html/2608.06366) · [abs](https://arxiv.org/abs/2608.06366)  
  [`#abstract1`](https://arxiv.org/html/2608.06366#abstract1) · [`#S1`](https://arxiv.org/html/2608.06366#S1) · [`#S3`](https://arxiv.org/html/2608.06366#S3) · [`#S4`](https://arxiv.org/html/2608.06366#S4) · [`#S4.fig1`](https://arxiv.org/html/2608.06366#S4.fig1) · [`#S5`](https://arxiv.org/html/2608.06366#S5) · [`#S6`](https://arxiv.org/html/2608.06366#S6)

**導覽：** [Home](../) · [AI Papers](./)
