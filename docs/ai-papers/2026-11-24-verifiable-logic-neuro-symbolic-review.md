---
parent: AI Papers
nav_order: 3
title: "臨床 LLM 安全綜述：符號否決層數字亮眼，多來自單一小型研究"
catalog_id: "arxiv:2611.25898"
editors:
  - "Clare"
refs:
  main:
    title: "Verifiable Logic in Medical LLMs: A Critical Review of Agentic Clinical Reasoning Optimization and Neuro-Symbolic Grounding"
    url: "https://arxiv.org/pdf/2611.25898v1"
  abs:
    title: "arXiv abstract page: 2611.25898v1"
    url: "https://arxiv.org/abs/2611.25898v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 臨床 LLM 安全綜述：符號否決層數字亮眼，多來自單一小型研究

## 來源

- 團隊：作者依序為 Youssef ElNahas（University of Prince Mugrin, Artificial Intelligence Department，沙烏地阿拉伯 Medina）、Adel Ammar（Prince Sultan University, Robotics and Internet of Things Laboratory，沙烏地阿拉伯 Riyadh；通訊作者）、Soumaya Chaffar（University of Prince Mugrin）、Wadii Boulila（Prince Sultan University）。[(ref: main p.1)](https://arxiv.org/pdf/2611.25898v1#page=1)
- 論文：*Verifiable Logic in Medical LLMs: A Critical Review of Agentic Clinical Reasoning Optimization and Neuro-Symbolic Grounding*，arXiv:2611.25898v1（cs.CL；交叉列於 cs.AI、cs.CY、cs.LG），2026-11-19 提交，目前只有 v1；PDF 頁尾註記為投稿 Elsevier 的預印本，未註記接受的 venue；授權 CC BY-NC-ND 4.0。[(ref: abstract)](https://arxiv.org/abs/2611.25898v1) [(ref: main p.1)](https://arxiv.org/pdf/2611.25898v1#page=1)
- 識別碼：arXiv [2611.25898](https://arxiv.org/abs/2611.25898v1)；DOI [10.48550/arXiv.2611.25898](https://doi.org/10.48550/arXiv.2611.25898)。
- 全文：[PDF v1](https://arxiv.org/pdf/2611.25898v1)（47 頁）。
- 資料與聲明：沒有產生新的一手資料；98 篇納入研究的清單列在 Supplementary Table S1，但 arXiv PDF v1 沒有附上這張表。作者聲明沒有特定經費、沒有利益衝突；並揭露以 Perplexity AI、Claude、DeepSeek、Grok、Kimi 協助文獻辨識，以 Claude 與 ChatGPT 檢查稿件與引用來源是否一致並建議措辭。[(ref: main p.36)](https://arxiv.org/pdf/2611.25898v1#page=36) [(ref: main p.37)](https://arxiv.org/pdf/2611.25898v1#page=37)
- 研究性質：作者自稱 critical narrative review。檢索與篩選依 PRISMA-ScR 的格式報告，但沒有預先登錄 protocol、以立意方式選樣，因此作者明說不是正式的 scoping review；全文沒有原始實驗。作者提出的整合框架是概念規格，各元件只在原研究中分開評估過，整合後未經臨床驗證。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=4) [(ref: main §6.3)](https://arxiv.org/pdf/2611.25898v1#page=33)
- 證據邊界：本文以 arXiv PDF v1 為準。文中各一手研究的數字都是綜述的轉述，本文沒有逐一回查原始論文；Table 3 的完整系統清單與 Figure 2 的年度分布未全數搬錄。

**編輯：** Clare

兩所沙烏地阿拉伯大學的作者從 98 篇 2024–2026 年的一手研究出發，主張臨床 LLM 的安全有很大一部分是系統架構問題，並提出在代理流程的關鍵邊界接上 PRM 逐步評分與符號驗證器（Prolog、知識圖譜、OWL 本體）的框架；但作者自己也寫明，符號否決層報告的大幅安全增益多來自單一、模擬或小樣本研究，彼此與神經網路基線不能直接比較，框架本身也還沒有被驗證。[(ref: abstract)](https://arxiv.org/abs/2611.25898v1) [(ref: main §6.2)](https://arxiv.org/pdf/2611.25898v1#page=29) [(ref: main §6.3)](https://arxiv.org/pdf/2611.25898v1#page=33)

## 流程

![左右兩欄圖，以灰色點線分隔。左欄標題「Evidence base (Section 2, Figure 1)」：三個淺藍底、深藍實線圓角框由上而下以黑色箭頭相連，依序為「140 records logged (prompt-based queries to 5 AI-assisted retrieval tools, 8 & 28 Apr 2026; hand-verified against indexed sources)」、「138 records screened (2 records under two RQs merged)」、粗體「98 primary studies included RQ1 29 · RQ2 23 · RQ3 24 · RQ4 22」；138 框下方另有一支灰色箭頭指向淺灰底、灰色實線框「40 excluded (scope, time window, overlap, insufficient detail)」。右欄標題「Proposed framework (Figure 6) — conceptual, not clinically validated」：「Clinical input」以箭頭接到「Agentic reasoning layer (ReAct / MAD / Orchestration)」，再往下接「Process monitor: PRM step-level scoring」；PRM 框右側有灰色箭頭指向淺灰框「Released unchecked (logged)」，灰框上方標「not activated」；PRM 框往下的箭頭旁標「activated: low step score or safety-critical flag」，指向「Symbolic router」框，框內列出 clinical stakes · knowledge structure · latency budget · coverage confidence；router 分出四支箭頭到四個淺藍框「Prolog / CLP protocol rules」「KG verifier claim triples」「OWL DL ontology axioms」「Executable rule engine」；四框下方以一條黑色橫線匯集，標斜體「Verification outcome」，再以箭頭分到三個框：淺綠底綠框「Pass release checked output」、淺橘底橘框「Fail correction and recheck」、淺灰底灰框「Uncovered / unresolved / timeout abstention or clinician escalation」；一條橘色虛線從 Fail 框左側繞回 Agentic reasoning layer，旁標橘字「revise and resubmit」；三個結果框都以箭頭指向最下方淺藍框「Clinician audit trail (every outcome logged)」。](assets/verifiable-logic-review-evidence-and-framework.png)

*圖：本書庫依論文 §2 的 Figure 1（左）與 §6.3 的 Figure 6、Table 4（右）重繪。左欄為文獻篩選流程與四個研究問題各自納入的研究數；右欄為作者提出的驗證框架：符號檢查只在 PRM 步驟分數低於部署時校準的門檻、或查詢被標為安全關鍵時啟動，其餘輸出不經符號檢查直接放行並記為 unchecked。原圖中「沒有任何驗證器涵蓋的查詢直接轉棄權或臨床醫師升級」的路徑，本圖併入右下灰框。數字來自 [Figure 1](https://arxiv.org/pdf/2611.25898v1#page=5)，架構來自 [Figure 6](https://arxiv.org/pdf/2611.25898v1#page=32) 與 [Table 4](https://arxiv.org/pdf/2611.25898v1#page=33)；作者明言此框架是尚未經臨床驗證的概念規格。*

## 背景／問題

作者的出發點是：臨床 LLM 通常只看最終答案對不對，但模型可能經由無效的推理得到流暢、看似合理的輸出，而靜態基準測不出來。這個前提在綜述第 3 節有引用研究支撐，例如作者轉述的 MedCheck 稽核指出，56 個醫療 LLM 基準中 89% 沒有測輸入穩健性、91% 沒有處理不確定性、88% 沒有處理資料污染風險；另一項類風濕性關節炎研究中，模型常答對診斷，給出的理由卻有時與預期臨床表現相反。[(ref: abstract)](https://arxiv.org/abs/2611.25898v1) [(ref: main §3.2)](https://arxiv.org/pdf/2611.25898v1#page=10) [(ref: main p.11)](https://arxiv.org/pdf/2611.25898v1#page=11)

作者接著指出兩支文獻各走各的：一支讓 LLM 自主使用工具、與其他代理協作（agentic clinical workflows），另一支用知識圖譜與醫學本體約束 LLM 輸出（neuro-symbolic grounding）。作者以 Table 1 比對六篇既有綜述，認為前者把知識圖譜當檢索資源而非驗證工具、後者多半停在單一 LLM 系統；「沒有先前綜述把兩者接成一個可驗證框架」是作者就其所知的說法。[(ref: main §1, Table 1)](https://arxiv.org/pdf/2611.25898v1#page=2)

綜述用四個研究問題組織全文：RQ1 臨床幻覺有哪些類型、為何以結果為準的評估測不出來；RQ2 代理架構如何透過錯誤級聯（cascade）製造並放大幻覺；RQ3 Process Reward Model（PRM）能驗證臨床推理到什麼程度；RQ4 神經符號架構比純神經方法多了哪些安全效益、在什麼條件下成立。[(ref: main §1)](https://arxiv.org/pdf/2611.25898v1#page=3)

## 方法摘要

- **設計** — critical narrative review，依 PRISMA-ScR 的結構報告檢索與篩選以求透明；沒有預先登錄 protocol，研究以「架構描述是否清楚、機制是否交代、與四個範式的關聯」立意選取，作者說這是以機制分析深度換取涵蓋完整度。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=4)
- **檢索** — 以結構化提示詞查詢五個 AI 輔助檢索工具（Perplexity AI、Claude、DeepSeek、Grok、Kimi），每個研究問題一組查詢；RQ1、RQ2 於 2026-04-08 送出，RQ3、RQ4 於 2026-04-28 送出，各組查詢字串列於正文。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=4)
- **篩選** — 所有結果人工核對是否存在、可取得、相關；在 IEEE Xplore、ACM Digital Library、PubMed、Google Scholar 等索引查不到的紀錄一律排除。登錄 140 筆，合併 2 筆跨研究問題重複後篩選 138 筆，排除 40 筆，納入 98 篇一手研究（RQ1 29、RQ2 23、RQ3 24、RQ4 22）。[(ref: main §2, Figure 1)](https://arxiv.org/pdf/2611.25898v1#page=5)
- **時間範圍** — 一手研究限 2024 年 4 月至 2026 年 4 月；既有綜述取 2023 年 1 月至 2026 年 4 月；ReAct、multi-agent debate、DeepProbLog、Scallop、Logic Tensor Networks 等較早的方法論前身例外納入。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=5)
- **歸類** — 每篇研究標上五種驗證型態之一與來源類型（P 同儕審查、PP 預印本、CF 概念框架），只在非臨床領域評估的系統另標 †；CF 不作為量化安全宣稱的主要證據。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=6)
- **框架** — 把第 4 節的三類代理失效對應到三個符號介入點，再以四個路由條件決定送哪一類驗證器（Figure 6、Table 4）。[(ref: main §6.3)](https://arxiv.org/pdf/2611.25898v1#page=31)

## 方法詳解

- **五種驗證型態** — 作者先固定「verifiable」的用法：Deductive verification（在指定推論系統下由前提形式蘊涵，例如 Prolog backward chaining；保證只相對於公理與輸入事實）；Ontology-based verification（以 HermiT、Pellet 等 description logic reasoner 在 OWL／RDF 本體上做 consistency check 或 entailment check，前者較弱）；Evidence-grounded verification（以指引、知識庫或結構化 EHR 佐證，沒有形式蘊涵保證但可稽核、可更新）；Probabilistic learned verification（訓練判別模型替步驟或輸出打分，保證是統計性的）；Structural process-level verification（chain-of-thought 監督等訓練目標的副產品，不算形式驗證）。[(ref: main §1)](https://arxiv.org/pdf/2611.25898v1#page=3) [(ref: main p.4)](https://arxiv.org/pdf/2611.25898v1#page=4)
- **四個要分開的性質** — factual provenance（擷取的事實是否真的在病歷裡）、consistency（是否與編碼知識矛盾）、entailment（編碼知識加上擷取事實是否蘊涵該主張）、clinical validity（對這位病人是否正確）。形式驗證器只能在其前提、編碼與推論程序之內建立 consistency 或 entailment，不檢查事實來源就不保證 provenance，編碼知識本身不正確或過時也不保證 clinical validity。[(ref: main §1)](https://arxiv.org/pdf/2611.25898v1#page=4)
- **排除條件** — 只報整體基準分數、不描述推理架構或失效機制的研究；只用結果準確率評估、未處理過程或架構因素的研究；與已納入系統高度重疊者；方法細節不足以獨立驗證者。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=6)
- **萃取欄位** — RQ1 記錯誤類型、臨床例子與失效的計算解釋；RQ2 記代理架構、可用工具與錯誤傳播位置；RQ3 記臨床任務、獎勵架構與步驟評估者；RQ4 記符號引擎或知識來源、驗證策略，以及安全增益與成本的取捨。跨範式的研究在各範式下都萃取，但在 Table 2 只計一次。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=6)
- **偏差緩解** — 作者列了三項：納入排除條件對每筆紀錄一致套用；刻意保留反面證據（神經符號方法的失效模式、PRM 的限制）；以 Table 1 與方法和範圍不同的既有綜述對照。作者也說這只能降低、不能消除立意選樣的偏差。[(ref: main p.7)](https://arxiv.org/pdf/2611.25898v1#page=7)
- **三個介入邊界** — 錯誤從事實擷取擴散時，在 extraction boundary 做 provenance check 與 derivation check（以 ProCDS 的 Prolog 推導為例，但作者指出它抓不到「錯得合理」的擷取值）；錯誤由代理間共識放大時，在 communication boundary 只讓知識圖譜記載或可推得的 claim triple 進入共識池（改編自 GraphEval，臨床用法未經測試）；錯誤源於工具選擇時，在 planning boundary 以決策樹／隨機森林 oracle 否決違反協定的工具呼叫（這些 oracle 只在一般推理基準評估過）。[(ref: main §6.3)](https://arxiv.org/pdf/2611.25898v1#page=31)
- **路由與五種情況** — 四個路由條件為 clinical stakes、knowledge structure、latency budget、coverage confidence。啟動條件是 PRM 步驟分數低於部署時校準的門檻或查詢被標為安全關鍵；未啟動的輸出直接放行並記為 unchecked；驗證通過則記錄後放行；被否決時若驗證器能定位出錯的事實或步驟、且在延遲預算內，退回代理層修正；沒有驗證器涵蓋、修正失敗或預算用完則結構化棄權。[(ref: main p.32)](https://arxiv.org/pdf/2611.25898v1#page=32) [(ref: main p.33)](https://arxiv.org/pdf/2611.25898v1#page=33)
- **作者列出的四種結構性失效** — ontology staleness（規則或本體編碼的是過時指引，產生形式有效但臨床錯誤的判定）；entity extraction failure（錯得合理的值仍能推導成功並悄悄通過）；guideline conflict（跨科照護的協定互相矛盾、約束無法同時滿足，現有架構都沒有仲裁機制）；latency exceedance（expressive OWL DL 推理與多跳知識圖譜驗證可能超出急診或加護病房的時間限制）。[(ref: main p.33)](https://arxiv.org/pdf/2611.25898v1#page=33)
- **論文未交代** — 五個 AI 檢索工具各自回傳多少紀錄、如何合併，以及工具的版本與設定；篩選由幾位作者執行、意見不一致時如何處理；是否對納入研究做正式的偏誤風險評估（正文只說從各研究取用其自述的結果與限制）；Table 2 的「dominant regime」如何判定；框架中 PRM 門檻要如何校準。98 篇納入研究的完整清單（Supplementary Table S1）不在 arXiv PDF v1 中。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=4) [(ref: main p.36)](https://arxiv.org/pdf/2611.25898v1#page=36)

## 資料與實驗

### 資料

| 項目 | 內容 |
|---|---|
| 綜述類型 | Critical narrative review；依 PRISMA-ScR 格式報告，無預先登錄 protocol，立意選樣 |
| 檢索工具 | Perplexity AI、Claude、DeepSeek、Grok、Kimi（每個研究問題一組查詢） |
| 檢索日期 | RQ1、RQ2：2026-04-08；RQ3、RQ4：2026-04-28 |
| 一手研究時間範圍 | 2024 年 4 月至 2026 年 4 月（方法論前身例外） |
| 紀錄流向 | 登錄 140 → 合併重複後 138 → 排除 40 → 納入 98 |
| 各研究問題納入數 | RQ1 29、RQ2 23、RQ3 24、RQ4 22 |
| 來源類型標記 | P 同儕審查、PP 預印本、CF 概念框架；† 只在非臨床領域評估 |
| 參考文獻 | 129 筆；2023–2026 年者 114 筆（2023：5、2024：15、2025：63、2026：31，2026 年僅計至檢索截止） |

[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=4) [(ref: main Figure 1)](https://arxiv.org/pdf/2611.25898v1#page=5) [(ref: main Figure 2)](https://arxiv.org/pdf/2611.25898v1#page=8)

納入研究依範式的特性，搬自論文 Table 2（上標：P 同儕審查、PP 預印本；† 只在非臨床領域評估）：

| Paradigm | n | Dominant Regime(s) | Dominant Metric Type | Representative Systems | Key Unresolved Gap |
|---|---|---|---|---|---|
| RQ1: Hallucination taxonomy | 29 | Not applicable (diagnostic, not verification-layer) | Hallucination or omission rate, F1 | mARC-QA (P), ShatterMed-QA (PP), MedHallu (PP), MedCaseReasoning (PP) | Few benchmarks test counterfactual demographic invariance or adversarial robustness |
| RQ2: Agentic cascade | 23 | Not applicable (architectural, not verification-layer) | Task success rate, cascade or error-propagation rate | EHRAgent (P), MedAgentBench (P), MedAgentAudit (PP), TrustEHRAgent (PP) | Calibration cliff: very low correct-answer yield under stringent reliability requirements |
| RQ3: PRM verification | 24 | Probabilistic learned, Structural process-level | Accuracy gain, F1, reasoning recall | Med-PRM (P), VPRM (PP), MedCEG (PP), MedS3 (P) | Evaluation infrastructure lags system development; calibration not integrated into PRM benchmarks |
| RQ4: Neuro-symbolic grounding | 22 | Deductive, Ontology-based, Evidence-grounded | Hallucination reduction (%), protocol adherence (%) | ProCDS (P), Ontology-grounded GraphRAG (P), GraphEval (P, †), Explanation-Refiner (P, †) | Specification soundness, veto precision/recall, and temporal specification decay are unaudited |

[(ref: main Table 2)](https://arxiv.org/pdf/2611.25898v1#page=7)

### 實驗

本篇是綜述，沒有原始實驗或作者自己量測的結果表。以下兩張表分別是作者提出的驗證器路由規則（論文 Table 4，全部是提議中的元件），以及綜述轉述、本文後面會用到的代表性數字。

驗證器路由條件，搬自論文 Table 4：

| Decision Domain | Verifier | Expected Latency | Primary Veto Condition |
|---|---|---|---|
| Formal protocol coverage (drug dosing, surgical eligibility) | Prolog / CLP | Medium (iterative re-extraction) | Conclusion not derivable from the protocol rules and extracted facts, or an extracted fact not traceable to the source record |
| Structured ontological domain (rare disease phenotype, infectious disease semantics) | OWL DL | Potentially high; profile- and ontology-dependent | Candidate claim inconsistent with, or (where required) not entailed by, the ontology axioms |
| Multi-hop relational claim (differential diagnosis, drug interaction) | KG Verifier | Medium | Claim triple neither recorded in the KG nor implied by composable relations, or entity absent from the graph |
| Fully enumerable safety-critical rule set (e.g., a hemodialysis dosing protocol) | Executable rule engine | Expected to be minimal (not measured) | Any output that departs from the encoded rule set (checked on every query) |
| Out-of-domain query (no formal coverage available) | Abstention | N/A | Default fallback for all unrouted queries |

[(ref: main Table 4)](https://arxiv.org/pdf/2611.25898v1#page=33)

綜述轉述的代表性數字（皆為各原研究在自身設定下的結果，作者強調彼此不能直接比較）：

| 研究（綜述中的名稱） | 範式 | 設定 | 綜述轉述的結果 | 頁 |
|---|---|---|---|---|
| MedCheck | RQ1 | 56 個醫療 LLM 基準 | 89% 無輸入穩健性測試、91% 忽略不確定性處理、88% 未處理資料污染 | [p.10](https://arxiv.org/pdf/2611.25898v1#page=10) |
| MedAgentBench | RQ2 | FHIR 虛擬 EHR，12 個模型、100 位病人檔案 | 最佳模型成功率 69.67% | [p.13](https://arxiv.org/pdf/2611.25898v1#page=13) |
| MedAgentAudit | RQ2 | 3,600 筆執行紀錄、14,400 個測試案例、6 個多代理架構 | 討論中重複最初觀點 98.42%；authority bias 由第一輪綜合 35.30% 升到第三輪 68.75% | [p.14](https://arxiv.org/pdf/2611.25898v1#page=14) |
| TrustEHRAgent | RQ2 | MIMIC-III、eICU | HCAcc@70%：44.23%／25.34%；HCAcc@90%：3.27%／2.24%；對照基線在 HCAcc@70% 已為 0.0 | [p.17](https://arxiv.org/pdf/2611.25898v1#page=17) |
| Med-PRM | RQ3 | 測試時以檢索證據替每步評分 | 基礎模型最多提升 13.50%；8B 模型在 MedQA 首次超過 80% | [p.19](https://arxiv.org/pdf/2611.25898v1#page=19) |
| DeepSeek-R1（Gupta et al.） | RQ3 | 零樣本慢性病分類 | 92% 案例給高信心，疾病層級判斷只有 76% 正確 | [p.22](https://arxiv.org/pdf/2611.25898v1#page=22) |
| ProCDS | RQ4 | 1,797 位病人真實病歷、14 條專家驗證規則（OSAHS 風險） | 資料完整時 99.5%；10% 紀錄遮蔽資訊時 85–95% | [p.24](https://arxiv.org/pdf/2611.25898v1#page=24) |
| AnemiaCare HD | RQ4 | 單一機構協定、600 個模擬情境 | 鬆散提示 32%（96/300）符合協定；確定性提示 100%（300/300） | [p.24](https://arxiv.org/pdf/2611.25898v1#page=24) |
| Ontology-grounded GraphRAG | RQ4 | 60 題臨床問題，埃及多家機構資料 | 準確率 98%（59/60），ChatGPT-4 37%、DeepSeek-R1 52%；幻覺率 1.7%，對照約 63% 與 48% | [p.25](https://arxiv.org/pdf/2611.25898v1#page=25) |
| Explanation-Refiner † | RQ4 | e-SNLI，GPT-4＋Isabelle/HOL | 邏輯有效解釋由 36% 升到 84% | [p.27](https://arxiv.org/pdf/2611.25898v1#page=27) |

## 結果

- **RQ1：四種幻覺子型** — 作者把臨床幻覺分成 shortcut learning 與 spurious correlations、context omission 與 adversarial fragility、miscalibration 與 overconfidence、multimodal 與 cross-domain fragility 四類，並解讀為同一個錯配的不同表現：生成目標最佳化的是 token likelihood 與人類偏好，臨床要的是完整性、校準過的不確定性與因果一致性；修好一類不會順帶修好其他類。[(ref: main §3.1)](https://arxiv.org/pdf/2611.25898v1#page=8) [(ref: main p.10)](https://arxiv.org/pdf/2611.25898v1#page=10)
- **RQ1：靜態指標測不到過程** — 綜述轉述的例子包括：在臨床小品文中植入單一捏造細節，幻覺率升到 50–82%，提示詞緩解只把平均由 66% 降到 44%；動態紅隊測試讓 94% 原本答對的 MedQA 題目崩潰；MedHallu 上偵測語意複雜捏造內容的 F1 低至 0.625。作者據此主張評估要轉向會擾動推理軌跡的動態、過程導向測試。[(ref: main p.9)](https://arxiv.org/pdf/2611.25898v1#page=9) [(ref: main p.11)](https://arxiv.org/pdf/2611.25898v1#page=11)
- **RQ2：hallucination cascade** — 作者把代理系統的新失效模式定義為：第 n 步的錯誤成為假前提，之後每一步都把它當作已驗證的事實，輸出愈來愈精緻、愈難辨認。綜述轉述的佐證包括 EHR-MCP 評估中，模型在抗生素紀錄缺漏時把提示詞裡的範例藥名當成已給藥、以真實結果的格式回報；以及在一般領域代理中觀察到捏造工具執行紀錄、只有密碼學執行紀錄能抓到。[(ref: main §4.2)](https://arxiv.org/pdf/2611.25898v1#page=15)
- **RQ2：共識會放大錯誤** — MedAgents 的錯誤分析中 77% 與領域知識有關、只有 8% 是推理鏈錯誤，而所有「專科代理」都由同一個基礎模型扮演；MedAgentAudit 量到代理在討論階段 98.42% 的時間只是重複最初觀點、42.73% 的案例沒有啟動符合角色的專科推理。作者的結論是，標準形式的多代理辯論並不能可靠地重現實證討論。[(ref: main §4.1)](https://arxiv.org/pdf/2611.25898v1#page=13) [(ref: main p.14)](https://arxiv.org/pdf/2611.25898v1#page=14)
- **RQ2：calibration cliff** — TrustEHRAgent 的 HCAcc@k% 是在至少 k% 已答題目正確的條件下可達到的最高整體準確率；要求 90% 可靠度時，最好的信心感知代理只答對約 2–3% 的全部查詢。作者把這解讀為代理的回報信心、訓練獎勵與實際正確率錯配的結構性後果，並明說「單靠調參不太可能消除」是假說。[(ref: main p.17)](https://arxiv.org/pdf/2611.25898v1#page=17) [(ref: main §7)](https://arxiv.org/pdf/2611.25898v1#page=35)
- **RQ3：PRM 有五種，保證各不相同** — discriminative step-level verifiers、rule-based deterministic verifiers、emergent process supervision、self-supervised path faithfulness、knowledge-graph-grounded supervision；作者強調知識圖譜路徑只代表兩個概念有關聯，不代表步驟有效。PRM 仍受訓練資料統計所限，且獎勵愈密集愈容易被 reward hacking；在精神科情境，推理軌跡可能通過所有自動檢查，卻因偏好附和而漏掉應有的治療性對質。[(ref: main §5.1)](https://arxiv.org/pdf/2611.25898v1#page=18) [(ref: main p.21)](https://arxiv.org/pdf/2611.25898v1#page=21)
- **RQ3：評估基礎設施落後** — MedPRMBench 以 14 種錯誤類型、四級嚴重度、6,500 題與 113,910 個標籤評估步驟層級的錯誤偵測；但作者指出 PRM 基準普遍沒有納入校準指標，而靜態基準會隨指引更新而過時。[(ref: main §5.2)](https://arxiv.org/pdf/2611.25898v1#page=22)
- **RQ4：符號否決層的數字與保留** — 作者整理 runtime symbolic veto（符號檢查器可在輸出前否決）的三種做法：logic-based protocol enforcement、ontology-grounded semantic verification、dynamic logic verification，並把只靠提示詞約束的 AnemiaCare HD 列為「確定性約束編碼」的近似。作者自己的評語是：這些都是單一研究、多為模擬或小樣本，與他處評估的神經網路基線不能直接比較，只顯示領域受限的符號約束能做到什麼，尚未證明對純神經架構有普遍的安全優勢；MedKGI 的 30% 增益是對話效率，不是安全。[(ref: main §6)](https://arxiv.org/pdf/2611.25898v1#page=23) [(ref: main §6.1)](https://arxiv.org/pdf/2611.25898v1#page=24) [(ref: main p.29)](https://arxiv.org/pdf/2611.25898v1#page=29)
- **RQ4：保證只相對於編碼內容** — ProCDS 的規則本身由 LLM 從指引擷取，錯誤仍可能經由事實擷取、規則編碼或規則涵蓋缺口進入；ontology 檢查的「接受」只代表沒找到矛盾；Explanation-Refiner 證明失敗可能是翻譯成邏輯出錯或 prover 的時間限制，不一定代表解釋無效。[(ref: main p.24)](https://arxiv.org/pdf/2611.25898v1#page=24) [(ref: main p.25)](https://arxiv.org/pdf/2611.25898v1#page=25) [(ref: main p.27)](https://arxiv.org/pdf/2611.25898v1#page=27)
- **RQ4：神經符號的評估缺口** — 作者指出臨床神經符號文獻的安全宣稱最強、評估基礎設施卻最弱：沒有研究稽核規格是否忠實形式化原始指引（specification soundness）、沒有 veto precision／recall、沒有涵蓋邊界指標、沒有量測指引更新造成的規格過時（temporal specification decay）。作者提議建立名為 NeuroSymBench 的版本化基準，檢查符號規格本身是否臨床正確且未過時。[(ref: main §6.4)](https://arxiv.org/pdf/2611.25898v1#page=34)
- **法規** — 作者認為 FDA AI/ML SaMD Action Plan、EU AI Act 2024/1689 與 MHRA 指引主要著重效能、風險管理與上市後監測；EU AI Act 對高風險系統另要求風險管理、技術文件、自動紀錄、透明度與人類監督（第 9–14 條）以及符合性評估（第 43 條），但三者都沒有要求對每個輸出的推理步驟做形式驗證，或在驗證失敗時棄權。作者另點出三個實務風險：「verified」標籤造成的 automation bias、符號驗證器漏報時的責任歸屬、以及推理延遲與證明軌跡在臨床介面的可讀性。[(ref: main §7)](https://arxiv.org/pdf/2611.25898v1#page=35) [(ref: main p.36)](https://arxiv.org/pdf/2611.25898v1#page=36)

## 限制

- **立意選樣與文獻範圍** — 作者自述立意抽樣會偏向機制交代清楚的架構，預印本的發現在同儕審查後未必能重現；兩批檢索日期（4 月 8 日與 28 日）造成小幅時間不對稱，之後發表的論文可能已處理文中指出的問題。[(ref: main §7)](https://arxiv.org/pdf/2611.25898v1#page=35)
- **框架未經驗證** — 整合架構只有元件在原研究中分開驗證過，作者明說其安全宣稱是架構性的、還不是實證的；部署前需要前瞻、端到端、跨族群的評估與法規審查。[(ref: main p.33)](https://arxiv.org/pdf/2611.25898v1#page=33) [(ref: main §7)](https://arxiv.org/pdf/2611.25898v1#page=35)
- **跨研究數字不可比** — 各研究的實驗設定、任務定義與幻覺操作型定義不同，作者說本綜述的綜合是結構性、架構性的，不是統合分析；多項驗證機制只在非臨床領域評估（†），臨床效益是推論。[(ref: main §7)](https://arxiv.org/pdf/2611.25898v1#page=35)
- **檢索以 LLM 工具為入口（本書庫的觀察）** — 作者有揭露並說明所有紀錄都人工對照索引來源核對過；但正文只列查詢字串，沒有交代各工具的版本、設定與各自回傳的紀錄數，這類工具的輸出也會隨時間變動，讀者難以重現同一個檢索結果。這一點是本書庫的解讀，不是作者列出的限制。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=4)
- **納入清單不在 PDF 內** — 作者說 98 篇研究列於 Supplementary Table S1，但 arXiv PDF v1 沒有這張表，讀者無法從 v1 核對完整的納入清單。[(ref: main p.36)](https://arxiv.org/pdf/2611.25898v1#page=36)
- **沒有描述偏誤風險評估** — 正文說各研究的結果與限制取自研究本身，並以來源類型（P／PP／CF）標記，但沒有描述對納入研究做正式的品質或偏誤風險評估。[(ref: main §2)](https://arxiv.org/pdf/2611.25898v1#page=6)

## 與書庫其他文章的關係

多代理基礎文整理 ReAct、角色分工與多代理對話的概念譜系；本綜述則彙整這些架構在臨床任務上的失效證據，例如作者轉述 MedAgentAudit 稽核到討論階段代理有 98.42% 的時間只是重複最初觀點: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md)

兩篇都在質疑臨床代理基準的分數能代表多少；本綜述主張只以最終答案計分的評估看不到推理過程中的錯誤，後見之明那篇則量出由出院摘要改寫的病例文字讓 LLM 診斷比檢傷資訊多答對 14–20 個百分點: [診斷代理基準的後見之明：LLM 讀病例摘要比讀檢傷資料多答對 14 點](2026-11-20-clinical-agent-benchmark-hindsight-case-text.md)

本綜述把「Degeneration of Thought」（模型一旦對答案有信心，後續自我反思就難以修正）列為代理錯誤級聯的成因之一，主張要靠外部可驗證的檢查打斷；VLM 代理那篇在急診 CT／MRI 多輪瀏覽中量到模型很早寫下的第一個假設多半不會被推翻，是這個現象在影像代理上的一組實測: [VLM 代理自己翻 CT／MRI：第一個假設錯，最後只有 12% 答對](2026-11-19-vlm-agent-ct-mri-navigation-first-hypothesis.md)

## 實務的啟發

- **檢視任何「verified」宣稱時，先問它驗證的是哪一個性質** — 作者把 factual provenance、consistency、entailment、clinical validity 分開的作法可以直接借用：一個推導成功的 Prolog 結論只說明它由輸入事實與規則推得，不代表擷取的事實正確，也不代表規則反映現行指引。
- **評估代理系統要看嚴格可靠度下的產出量** — HCAcc@k% 這類「在 k% 正確率要求下還能答多少」的指標是可借用的量測方法；綜述轉述的 TrustEHRAgent 結果只來自 MIMIC-III 與 eICU 上的單一研究，應視為待驗證的警訊，而不是一般代理的既定上限。
- **多代理辯論不等於獨立複核** — 若各代理由同一個基礎模型扮演，綜述轉述的稽核結果顯示討論多半只是重複最初觀點；要把多代理當作安全機制，至少要引入不同來源的外部證據，並實際量測討論是否改變答案。這些證據多為單一研究與預印本，需要在自己的任務上驗證。
- **導入符號驗證層前，先準備好量它的方法** — 作者指出的 veto precision／recall、涵蓋邊界與規格過時三項指標，目前沒有任何納入研究量測過；符號層若會把涵蓋範圍外的查詢靜默放行，宣稱的準確率就可能被高估。
- **框架是設計參考，不是可直接沿用的架構** — Figure 6 的路由設計整合了單獨評估過的元件，延遲、門檻校準與指引衝突的仲裁都還沒有解法；目前比較適合拿來檢查自己的系統在哪些邊界缺少驗證，而不是照著實作後宣稱更安全。

## References

- **main** — ElNahas Y, Ammar A, Chaffar S, Boulila W. *Verifiable Logic in Medical LLMs: A Critical Review of Agentic Clinical Reasoning Optimization and Neuro-Symbolic Grounding*. arXiv:2611.25898v1, 2026. PDF: https://arxiv.org/pdf/2611.25898v1 ；deep links used: [p.1](https://arxiv.org/pdf/2611.25898v1#page=1)、[p.2 Table 1](https://arxiv.org/pdf/2611.25898v1#page=2)、[p.3 §1](https://arxiv.org/pdf/2611.25898v1#page=3)、[p.4 §2](https://arxiv.org/pdf/2611.25898v1#page=4)、[p.5 Figure 1](https://arxiv.org/pdf/2611.25898v1#page=5)、[p.6](https://arxiv.org/pdf/2611.25898v1#page=6)、[p.7 Table 2](https://arxiv.org/pdf/2611.25898v1#page=7)、[p.8 §3.1, Figure 2](https://arxiv.org/pdf/2611.25898v1#page=8)、[p.9](https://arxiv.org/pdf/2611.25898v1#page=9)、[p.10 §3.2](https://arxiv.org/pdf/2611.25898v1#page=10)、[p.11](https://arxiv.org/pdf/2611.25898v1#page=11)、[p.13](https://arxiv.org/pdf/2611.25898v1#page=13)、[p.14](https://arxiv.org/pdf/2611.25898v1#page=14)、[p.15 §4.2](https://arxiv.org/pdf/2611.25898v1#page=15)、[p.17](https://arxiv.org/pdf/2611.25898v1#page=17)、[p.18 §5.1](https://arxiv.org/pdf/2611.25898v1#page=18)、[p.19](https://arxiv.org/pdf/2611.25898v1#page=19)、[p.21](https://arxiv.org/pdf/2611.25898v1#page=21)、[p.22 §5.2](https://arxiv.org/pdf/2611.25898v1#page=22)、[p.23 §6](https://arxiv.org/pdf/2611.25898v1#page=23)、[p.24 §6.1](https://arxiv.org/pdf/2611.25898v1#page=24)、[p.25](https://arxiv.org/pdf/2611.25898v1#page=25)、[p.27 §6.2](https://arxiv.org/pdf/2611.25898v1#page=27)、[p.29](https://arxiv.org/pdf/2611.25898v1#page=29)、[p.31 §6.3](https://arxiv.org/pdf/2611.25898v1#page=31)、[p.32 Figure 6](https://arxiv.org/pdf/2611.25898v1#page=32)、[p.33 Table 4](https://arxiv.org/pdf/2611.25898v1#page=33)、[p.34 §6.4](https://arxiv.org/pdf/2611.25898v1#page=34)、[p.35 §7](https://arxiv.org/pdf/2611.25898v1#page=35)、[p.36](https://arxiv.org/pdf/2611.25898v1#page=36)、[p.37](https://arxiv.org/pdf/2611.25898v1#page=37)
- **abs** — arXiv abstract page: https://arxiv.org/abs/2611.25898v1 ；DOI: https://doi.org/10.48550/arXiv.2611.25898

[Home](../) · [AI Papers](./)
