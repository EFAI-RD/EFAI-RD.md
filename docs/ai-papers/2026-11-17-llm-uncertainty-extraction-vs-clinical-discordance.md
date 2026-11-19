---
parent: AI Papers
nav_order: 5
title: "LLM 不確定性抓得出讀錯報告，抓不出 CCTA 與心導管落差"
catalog_id: "arxiv:2611.10502"
editors:
  - "Clare"
refs:
  main:
    title: "Distinguishing Extraction Failures and Clinical Discordance with LLM Uncertainty on Radiology Reports"
    url: "https://arxiv.org/html/2611.10502v1"
  abs:
    title: "arXiv abstract page: 2611.10502v1"
    url: "https://arxiv.org/abs/2611.10502v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# LLM 不確定性抓得出讀錯報告，抓不出 CCTA 與心導管落差

## 來源

- 團隊：University of California, San Diego 的 Department of Radiology 與 Halıcıoğlu Data Science Institute，作者依序為 Jerjes Aguirre-Chavez、Shant Malkasian、Roshun Sankaran、Brendan Crabb、Albert Hsiao；論文標示兩位作者同等貢獻。[(ref: main author block)](https://arxiv.org/html/2611.10502v1)
- 論文：*Distinguishing Extraction Failures and Clinical Discordance with LLM Uncertainty on Radiology Reports*，arXiv:2611.10502v1（cs.CL），2026-11-07 提交，目前只有 v1；arXiv 頁註記為 ML4H 2026 spotlight presentation，收錄於 Proceedings of Machine Learning Research 346；授權 CC BY 4.0。[(ref: abstract)](https://arxiv.org/abs/2611.10502v1)
- 識別碼：arXiv [2611.10502](https://arxiv.org/abs/2611.10502v1)；DOI [10.48550/arXiv.2611.10502](https://doi.org/10.48550/arXiv.2611.10502)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.10502v1)、[PDF v1](https://arxiv.org/pdf/2611.10502v1)。
- 程式與資料：作者以匿名程式庫釋出統計分析程式（建隊列、迴歸、鑑別與校準、鎖定量測與切點），不含抽取系統，也不含資料，因此無法從頭重跑；prompt 收在附錄 E.4–E.5。論文未列經費與利益衝突聲明。[(ref: main Appendix C)](https://arxiv.org/html/2611.10502v1#A3) [(ref: main Appendix E.3)](https://arxiv.org/html/2611.10502v1#A5.SS3)
- 研究性質：單一機構回顧性分析，不是 pilot；Llama-3.3-70B 實際在院內硬體上以 few-shot 抽取 CCTA 報告，主要分析涵蓋 253 位與 729 位病人，並附病人層級 bootstrap 95% CI 與 optimism correction。不確定性量測是在同一批 P2 資料上挑選、再用同一個切點套到其他族群。[(ref: main §2.1)](https://arxiv.org/html/2611.10502v1#S2.SS1) [(ref: main §2.4)](https://arxiv.org/html/2611.10502v1#S2.SS4) [(ref: main Appendix B)](https://arxiv.org/html/2611.10502v1#A2)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文與附錄 E.7 表格為準；只以圖呈現的 ICA 抽取準確率（96 份 ICA 報告）、十種量測的逐一圖示與校準曲線未納入本文引述。

**編輯：** Clare

作者用 CCTA 報告的冠狀動脈狹窄抽取檢驗：Llama-3.3-70B 抽取時的 token 不確定性，能幫忙找出它和放射科醫師讀法不同的血管（AUC 0.805→0.862），卻幾乎無助於找出 CCTA 與後續心導管（ICA）結果不一致的血管（0.618→0.625）。[(ref: main Table E.7)](https://arxiv.org/html/2611.10502v1#A5.SS7.tab3)

## 流程

![左右兩欄圖。左欄為流程圖：上排三個淺藍底、深藍實線圓角框，由左至右為「External radiologist rereads CCTA report (1 of 3 readers; 270 studies)」、「CCTA LLM Llama-3.3-70B, few-shot stenosis per vessel (6-point scale)」、「ICA LLM reads later ICA report (within 0-90 days)」；四支向下箭頭連到中排兩個淺橘底、橘褐色實線框：左「Extraction Failure (P2) CCTA LLM != radiologist exact 6-point match 1,077 vessels / 253 patients」，右「Clinical Discordance (P3) CCTA LLM vs ICA LLM disagree on obstructive CAD 1,641 vessels / 729 patients」；下方一個淺藍底、深藍實線寬框以兩支向上箭頭連到中排兩框，內容為「Uncertainty during CCTA extraction: 10 measures (token margin / perplexity + self-rated confidence / ambiguity) Stenosis Margin selected on P2, median cutoff locked; GEE logistic regression + AUC over CAD-phenotype baseline」；左下角小字「Redrawn by EFAI-RD from arXiv:2611.10502v1 Sections 2-2.6」。右欄為長條圖，標題「Table E.7: discrimination with vs without uncertainty」，縱軸「AUC (apparent)」刻度 0.50–0.90；兩組長條，左為灰色「CAD-phenotype baseline」、右為橘色「Baseline + Stenosis Margin」：Extraction Failure (P2) 為 0.805 與 0.862，軸標註 ΔAUC +0.057, P=0.001；Clinical Discordance (P3) 為 0.618 與 0.625，軸標註 ΔAUC +0.007, P=0.245。](assets/llm-uncertainty-extraction-vs-discordance.png)

*圖：本書庫依論文 §2–2.6 重繪的三方量測與兩種失敗定義（左），以及加入 Stenosis Margin 前後的 AUC（右，未經 optimism correction 的原始值）。數值來自附錄 [Table E.7](https://arxiv.org/html/2611.10502v1#A5.SS7.tab3) 與 [§2.2 族群表](https://arxiv.org/html/2611.10502v1#S2.SS2.tab1)。*

## 背景／問題

作者引用文獻指出，從非結構化報告大規模抽取標籤常是開發臨床工具的第一步，而 LLM 抽取難免出錯，錯誤會傳到後續分析。[(ref: main §1)](https://arxiv.org/html/2611.10502v1#S1) 作者的論點是：當 LLM 抽出的資料和另一個參考（例如後續檢查）對不上時，研究者分不清是 LLM 讀錯了報告，還是兩種檢查本來就不一致；作者認為區分這兩種來源很關鍵，但這是作者的立場，論文沒有另外引用證據說明混淆兩者的實際後果。[(ref: main §1)](https://arxiv.org/html/2611.10502v1#S1)

CCTA 是很適合的測試場景：作者引用的研究指出，CCTA 陰性時把握度高（sensitivity 95%、NPV 98%），陽性時 specificity 79%、PPV 51%，且約 25% 的病人在 CCTA 與 ICA 間對阻塞性 CAD 的判定不一致，主要來自 CCTA 高估狹窄。[(ref: main §1)](https://arxiv.org/html/2611.10502v1#S1) 因此 CCTA 與 ICA 對不上，多半不是抽取問題。本篇要問的是：LLM 在抽取時的不確定性，能不能分辨這兩種失敗。

## 方法摘要

- **三方量測** — 同一條血管有三個狹窄程度：CCTA LLM 從 CCTA 報告抽出的結果、外部放射科醫師重讀同一份報告給的結果，以及 ICA LLM 從後續心導管報告抽出的結果。[(ref: main §2)](https://arxiv.org/html/2611.10502v1#S2)
- **兩種失敗** — Extraction Failure：CCTA LLM 與放射科醫師在六級狹窄量表上不完全相同；Clinical Discordance：CCTA LLM 與 ICA LLM 對「是否為阻塞性 CAD」判定不同。[(ref: main §2.4)](https://arxiv.org/html/2611.10502v1#S2.SS4) [(ref: main §2.5)](https://arxiv.org/html/2611.10502v1#S2.SS5)
- **十種不確定性量測** — token 層級的 margin 與 perplexity（分別算在狹窄類別、findings 段落、自評欄位上），加上模型自評的 confidence 與 ambiguity；挑出在 P2 增加最多 AUC 的 Stenosis Margin，並以其在 P2 的中位數作為高／低不確定性的固定切點。[(ref: main §2)](https://arxiv.org/html/2611.10502v1#S2) [(ref: main Appendix A.1)](https://arxiv.org/html/2611.10502v1#A1.SS1)
- **統計** — 以病人為群集的 GEE logistic regression（單變項與校正 CAD phenotype 兩種），並比較 CAD-phenotype baseline 加入量測前後的 AUC。[(ref: main §2.4)](https://arxiv.org/html/2611.10502v1#S2.SS4)
- **交叉分析** — 在三種量測都有的 P4（138 條血管）上，把兩種失敗交叉成四格表，看兩者是否同時發生。[(ref: main §2.6)](https://arxiv.org/html/2611.10502v1#S2.SS6)

## 方法詳解

- **隊列** — 經 IRB 核准、豁免知情同意的單一機構回顧性隊列，7,847 位病人各一份 CCTA 報告；排除 CCTA 前做過 ICA（255 人）與已有支架或繞道手術（302 人），847 人在 CCTA 後 0–90 天內做了 ICA。另有 270 份研究由三位外部放射科醫師之一重讀；兩群重疊 72 人，合計 1,045 位病人。[(ref: main §2.1)](https://arxiv.org/html/2611.10502v1#S2.SS1) [(ref: main Table E.7 cohort)](https://arxiv.org/html/2611.10502v1#A5.SS7.tab1)
- **抽取設定** — Llama-3.3-70B-Instruct（unsloth 版本）以 vLLM 在院內四張 GPU 上執行，few-shot、不微調，報告文字不出院內環境。每條血管各發一個 prompt，抽出最多 18 個冠狀動脈節段，再取各節段最大值作為血管等級，六級量表為 0%、1–24%、25–49%、50–69%、70–99%、100%；每位病人最多五條血管（LM、LAD、RI、LCX、RCA）。[(ref: main §2.1)](https://arxiv.org/html/2611.10502v1#S2.SS1) [(ref: main Appendix B)](https://arxiv.org/html/2611.10502v1#A2) [(ref: main Appendix E.2)](https://arxiv.org/html/2611.10502v1#A5.SS2)
- **輸出格式** — CCTA prompt 要求以 YAML 輸出各節段的狹窄類別（可填 NR），並在同一次呼叫中給 0–1 的 CONFIDENCE 與 AMBIGUITY；ICA prompt 輸出各血管的最大狹窄百分比或 none。[(ref: main Appendix E.4)](https://arxiv.org/html/2611.10502v1#A5.SS4) [(ref: main Appendix E.5)](https://arxiv.org/html/2611.10502v1#A5.SS5)
- **Stenosis Margin** — 在決定血管等級的那些節段上，取「最不確定位置的前兩名 token 機率差」的最小值；margin 與 self-confidence 取負號、perplexity 取對數，所有量測都轉成「越高越不確定」並在各分析族群內標準化。[(ref: main Appendix A.1)](https://arxiv.org/html/2611.10502v1#A1.SS1)
- **阻塞性定義** — LM ≥50%，LAD、LCX、RCA、RI ≥70%。ICA 報告沒寫出百分比的血管不當成 0%，而是排除，這條規則刪掉 3,370 條中的 1,729 條。[(ref: main §2.5)](https://arxiv.org/html/2611.10502v1#S2.SS5)
- **校正模型** — CAD-phenotype baseline 包含 CCTA 狹窄程度、log2(CACS+1)（未報告者另加指標）與血管別；作者的理由是不確定性會隨疾病負擔上升，必須排除「只是反映嚴重度」的路徑。十種量測以 Holm step-down 校正多重比較。[(ref: main §2.4)](https://arxiv.org/html/2611.10502v1#S2.SS4)
- **鑑別與校準** — 以 2,000 次病人層級 bootstrap 算 AUC 與差值的 CI，並以 Brier score 與十分位校準曲線報告校準；因為在同一資料上配適與評估，另以 Efron–Gong 法（400 次）做 optimism correction。[(ref: main §2.4)](https://arxiv.org/html/2611.10502v1#S2.SS4)
- **模型選擇** — 選模時比較 Llama 3.3 70B、MedGemma 27B、Qwen 3.5 9B 與一個正規表示式（regex）解析器，以 quadratic weighted κ 對照放射科醫師與 ICA；這一步用的是較新的匯出資料（8,253 份 CCTA），血管族群與主要分析不同。[(ref: main §2.3)](https://arxiv.org/html/2611.10502v1#S2.SS3)
- **論文未交代** — 解碼設定（temperature、top-p、最大長度、seed）、vLLM 版本與數值精度、regex 解析器的規則、Stenosis Margin 切點的實際數值，以及 few-shot 範例全文（CCTA prompt 13 例、ICA prompt 5 例在 HTML 中以括號省略）。[(ref: main Appendix B)](https://arxiv.org/html/2611.10502v1#A2) [(ref: main Appendix E.4)](https://arxiv.org/html/2611.10502v1#A5.SS4)
- **論文未交代** — 研究期間；ICA 參考值本身由 LLM 抽取，對 96 份 ICA 報告的準確率只以圖呈現；270 份重讀是人工挑選而非隨機，每份只由一位放射科醫師讀、沒有仲裁。[(ref: main §2)](https://arxiv.org/html/2611.10502v1#S2) [(ref: main Appendix D)](https://arxiv.org/html/2611.10502v1#A4)

## 資料與實驗

### 資料

| 族群 | 內容 | 分析 | 參考 | 血管數 | 病人數 |
|---|---|---|---|---|---|
| P1 | 所有抽出的血管 | — | — | 5,225 | 1,045 |
| P2 | CCTA＋外部放射科醫師 | Extraction Failure | 外部放射科醫師 | 1,077 | 253 |
| P3 | CCTA＋ICA | Clinical Discordance | ICA | 1,641 | 729 |
| P4 | CCTA＋外部放射科醫師＋ICA | 兩者交叉 | 兩者 | 138 | 57 |

[(ref: main §2.2 table)](https://arxiv.org/html/2611.10502v1#S2.SS2.tab1)

### 實驗

選模比較：各方法對放射科醫師參考的 quadratic weighted κ（regex 對照的獨立比較；Δκ 為 regex 減該方法）：

| Method | Quadratic weighted κ | Regex − method, Δκ | Holm-adjusted P |
|---|---|---|---|
| Regex | 0.946 (0.925–0.964) | — | — |
| Llama 3.3 70B | 0.974 (0.966–0.981) | −0.028 (−0.050 to −0.009) | 0.003 |
| MedGemma 27B | 0.963 (0.949–0.974) | −0.017 (−0.040 to 0.004) | 0.21 |
| Qwen 3.5 9B | 0.957 (0.940–0.971) | −0.011 (−0.034 to 0.012) | 0.36 |

[(ref: main §3.1 table)](https://arxiv.org/html/2611.10502v1#S3.SS1.tab1)

同樣以 ICA 為參考時，κ 降到 Regex 0.335、Llama 3.3 70B 0.454、MedGemma 27B 0.450、Qwen 3.5 9B 0.411，三個 LLM 對 regex 的差異 Holm P 皆為 0.003。[(ref: main Table E.7 ICA reference)](https://arxiv.org/html/2611.10502v1#A5.SS7.tab7)

兩種失敗的校正後 odds ratio（每增加 1 SD 不確定性），節錄自附錄 Table E.7：

| Measure | Extraction Failure 校正 OR (95% CI) | Holm P | Clinical Discordance 校正 OR (95% CI) | Holm P |
|---|---|---|---|---|
| Stenosis Margin | 4.15 (2.57–6.69) | < 0.001 | 1.22 (1.04–1.43) | 0.118 |
| Stenosis Perplexity | 1.29 (1.12–1.48) | 0.002 | 1.02 (0.91–1.15) | 1.0 |
| Self-Confidence | 1.62 (1.25–2.09) | 0.002 | 1.16 (1.03–1.31) | 0.118 |
| Self-Ambiguity | 1.44 (1.17–1.77) | 0.003 | 1.19 (1.07–1.33) | 0.018 |
| Ambiguity Margin | 1.66 (1.15–2.39) | 0.027 | 1.25 (1.10–1.43) | 0.009 |
| Confidence Margin | 0.92 (0.64–1.33) | 1.000 | 1.04 (0.91–1.17) | 1.0 |

[(ref: main Table E.7 regression)](https://arxiv.org/html/2611.10502v1#A5.SS7.tab2)

加入不確定性前後的鑑別力，節錄自附錄 Table E.7（AUC 與 ΔAUC 括號內為 95% CI）：

| Model | AUC (95% CI) | ΔAUC vs baseline (95% CI) | Bootstrap P | Brier score | Optimism-corrected AUC |
|---|---|---|---|---|---|
| P2 Baseline | 0.805 (0.763–0.842) | — | — | 0.0788 | 0.783 |
| P2 Stenosis Margin alone | 0.580 (0.530–0.628) | — | — | 0.0917 | — |
| P2 Baseline + Stenosis Margin | 0.862 (0.828–0.892) | +0.0571 (+0.0290, +0.0872) | 0.001 | 0.0702 | 0.845 |
| P3 Baseline | 0.618 (0.588–0.649) | — | — | 0.1968 | 0.602 |
| P3 Baseline + Stenosis Margin | 0.625 (0.595–0.655) | +0.0067 (−0.0042, +0.0175) | 0.245 | 0.1961 | 0.608 |
| P3 Baseline + Self-Ambiguity | 0.630 (0.601–0.661) | +0.0119 (+0.0002, +0.0239) | 0.049 | 0.1955 | 0.614 |

[(ref: main Table E.7 discrimination)](https://arxiv.org/html/2611.10502v1#A5.SS7.tab3)

## 結果

- **抽取本身很準** — P2 中 CCTA LLM 與放射科醫師完全一致 967／1,077 條血管（89.8%，κ = 0.97）；110 個錯誤中 103 個只差一級，差兩級以上只有 7 條（0.65%）。[(ref: main §3.2)](https://arxiv.org/html/2611.10502v1#S3.SS2)
- **不確定性對抽取錯誤有訊號** — 校正 CAD phenotype 後有五種量測通過 Holm 校正，Stenosis Margin 的 OR 4.15；加入後 AUC 由 0.805 升至 0.862（ΔAUC +0.057，P = 0.001），optimism correction 後為 0.783 對 0.845。Stenosis Margin 單獨使用時 AUC 只有 0.580，要和 CAD phenotype 合併才有用。[(ref: main §3.2)](https://arxiv.org/html/2611.10502v1#S3.SS2)
- **單變項與校正後方向不同** — Stenosis Margin 的單變項 OR 對抽取錯誤為 1.10（Holm P 0.508），對臨床不一致甚至是 0.87；校正後才分別變成 4.15 與 1.22。[(ref: main Table E.7 regression)](https://arxiv.org/html/2611.10502v1#A5.SS7.tab2)
- **對臨床不一致幾乎沒有增益** — P3 中 476／1,641 條血管（29.0%）CCTA 與 ICA 對阻塞性判定不同，順序量表完全一致只有 43.4%（κ = 0.45）；校正後只有 Ambiguity Margin（1.25）與 Self-Ambiguity（1.19）通過 Holm，加入 Stenosis Margin 的 ΔAUC +0.007（P = 0.245）。作者說明唯一區間不含 0 的 Self-Ambiguity（+0.012，P = 0.049）只是名目顯著。[(ref: main §3.3)](https://arxiv.org/html/2611.10502v1#S3.SS3)
- **高把握的錯誤分布不同** — 以固定切點區分後，抽取錯誤 69／110（62.7%）落在高不確定性一側（正確者為 48.5%），「有把握又錯」只有 41 條（P2 的 3.8%）；臨床不一致者高不確定性比例 43.7%、一致者 46.3%，「有把握又不一致」有 268 條（P3 的 16.3%）。[(ref: main §3.4)](https://arxiv.org/html/2611.10502v1#S3.SS4)
- **兩種失敗幾乎不重疊** — P4 的 42 條臨床不一致血管中 38 條（90%）抽取正確，16 個抽取錯誤只有 4 個同時不一致；觀察到 4 條、獨立時預期 4.87 條，Fisher OR 0.74（P = 0.776）。[(ref: main §3.5)](https://arxiv.org/html/2611.10502v1#S3.SS5)
- **錯的報告長相不同** — P2 中抽錯的血管所讀段落較長（中位數 187→244 字元）、阻塞性比例較高（16.3%→25.5%）、鈣化分數較高（中位數 0→64）；P3 中臨床不一致只有阻塞性比例不同（48.4%→42.2%），段落長度與鈣化無顯著差異。[(ref: main §3.5)](https://arxiv.org/html/2611.10502v1#S3.SS5)

## 限制

- **P3 是被篩過的族群** — 只有 ICA 量化過的血管才進入 P3，健康血管最容易沒被量化，因此 29.0% 不一致率與 0.618 的 baseline AUC 只描述這個偏向有病的子族群（作者自述）。[(ref: main Appendix D)](https://arxiv.org/html/2611.10502v1#A4)
- **參考標準較弱** — 270 份重讀為人工挑選，每份只有一位醫師、無仲裁，抽取錯誤與讀者間差異分不開；ICA 參考值也是 LLM 抽的（作者自述）。[(ref: main Appendix D)](https://arxiv.org/html/2611.10502v1#A4) [(ref: main §2)](https://arxiv.org/html/2611.10502v1#S2)
- **兩個任務本身不同** — 抽取錯誤用六級完全一致、臨床不一致用二元阻塞性門檻，族群也不同，所以增益差異同時反映任務差異，不只是失敗類型（作者自述）。[(ref: main Appendix D)](https://arxiv.org/html/2611.10502v1#A4)
- **交叉分析檢定力有限** — P4 只有 138 條血管，只能排除強關聯，無法排除弱關聯（作者自述）。[(ref: main §3.5)](https://arxiv.org/html/2611.10502v1#S3.SS5)
- **選擇與評估同一資料** — Stenosis Margin 是依 P2 的 AUC 增益挑出，再在 P2 報告其 OR 與 AUC；optimism correction 只處理配適樂觀，沒有處理在十種量測中挑最好的那一步。這是本書庫的解讀。[(ref: main §2.4)](https://arxiv.org/html/2611.10502v1#S2.SS4)
- **可攜性** — 單一機構、單一開放權重模型、只有 few-shot；Stenosis Margin 需要 token 機率，託管 API 通常不提供（作者自述）。[(ref: main Appendix D)](https://arxiv.org/html/2611.10502v1#A4) [(ref: main §4)](https://arxiv.org/html/2611.10502v1#S4)

## 與書庫其他文章的關係

兩篇都讓 LLM 讀 CCTA 報告文字、參考標準都由放射科醫師依同一份文字判定；CAD-RADS 那篇看整份報告分級時的升降級方向，本篇則把狹窄抽到血管層級，再用 token 不確定性分辨「讀錯報告」與「CCTA 和心導管本來就不一致」: [零樣本分 CAD-RADS：高風險報告被降級的比例 2.6%–14.1%](2026-10-22-llm-cad-rads-ccta-report-classification.md)

兩篇都在檢查醫療 LLM 的信心訊號何時可信；guardrail 那篇顯示生醫微調後模型在證據被抽掉時更少棄答、信心也跟著上升，本篇則在真實報告抽取上顯示 token 層級不確定性只對讀錯報告有用，對來源資料本身的不一致幾乎沒有增益: [生醫微調 LLM：證據被抽掉時，25 對有 21 對更少棄答](2026-11-11-guardrail-erosion-biomedical-llm-abstention.md)

兩篇都在問 LLM 讀病歷文字時，錯誤到底來自模型還是來自病歷本身；本篇用 token 不確定性分辨「讀錯 CCTA 報告」與「檢查本來就不一致」，note bloat 那篇則反過來在病歷中刻意注入 AI 摘要與未證實的鑑別診斷，看下游 LLM 會不會把它帶進出院摘要: [病歷埋入未證實鑑別診斷，下游 LLM 摘要沿用最高 31%](2026-11-17-llm-note-bloat-diagnostic-overcall.md)

## 實務的啟發

- **先拆分失敗來源再談資料品質** — 作者這套「抽取者 vs 重讀者 vs 下游參考」三方量測，是可借用的量測方法：用 LLM 建研究資料集時，至少留一小批人工重讀，才能把下游不一致中屬於抽取錯誤的部分分出來。
- **token 不確定性可當人工覆核的排序依據，但要和臨床特徵一起用** — 本研究中它單獨使用時 AUC 只有 0.580，和 CCTA 狹窄程度、鈣化分數合併後才有增益；而且這個結果來自單一機構、在同一資料上選出的量測，換到別的報告格式或模型前仍待驗證。
- **不要把低不確定性當作「資料可信」** — P3 中有 16.3% 的血管是 LLM 很有把握、卻和心導管不一致；這類差異來自影像本身與判讀，抽取端的信心看不到。
- **部署限制要提早評估** — Stenosis Margin 需要 token 機率，若流程改用不提供 logprob 的託管 API，這個訊號就無法取得；自評 confidence／ambiguity 雖可取得，但在本研究中對抽取錯誤的增益較小。

## References

- **main** — Aguirre-Chavez J, Malkasian S, Sankaran R, Crabb B, Hsiao A. *Distinguishing Extraction Failures and Clinical Discordance with LLM Uncertainty on Radiology Reports*. arXiv:2611.10502v1, 2026（ML4H 2026, PMLR 346）. HTML: https://arxiv.org/html/2611.10502v1 ；deep links used: [§1](https://arxiv.org/html/2611.10502v1#S1)、[§2](https://arxiv.org/html/2611.10502v1#S2)、[§2.1](https://arxiv.org/html/2611.10502v1#S2.SS1)、[§2.2 table](https://arxiv.org/html/2611.10502v1#S2.SS2.tab1)、[§2.3](https://arxiv.org/html/2611.10502v1#S2.SS3)、[§2.4](https://arxiv.org/html/2611.10502v1#S2.SS4)、[§2.5](https://arxiv.org/html/2611.10502v1#S2.SS5)、[§2.6](https://arxiv.org/html/2611.10502v1#S2.SS6)、[§3.1 table](https://arxiv.org/html/2611.10502v1#S3.SS1.tab1)、[§3.2](https://arxiv.org/html/2611.10502v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.10502v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.10502v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.10502v1#S3.SS5)、[§4](https://arxiv.org/html/2611.10502v1#S4)、[Appendix A.1](https://arxiv.org/html/2611.10502v1#A1.SS1)、[Appendix B](https://arxiv.org/html/2611.10502v1#A2)、[Appendix C](https://arxiv.org/html/2611.10502v1#A3)、[Appendix D](https://arxiv.org/html/2611.10502v1#A4)、[Appendix E.2](https://arxiv.org/html/2611.10502v1#A5.SS2)、[Appendix E.3](https://arxiv.org/html/2611.10502v1#A5.SS3)、[Appendix E.4](https://arxiv.org/html/2611.10502v1#A5.SS4)、[Appendix E.5](https://arxiv.org/html/2611.10502v1#A5.SS5)、[Table E.7 cohort](https://arxiv.org/html/2611.10502v1#A5.SS7.tab1)、[Table E.7 regression](https://arxiv.org/html/2611.10502v1#A5.SS7.tab2)、[Table E.7 discrimination](https://arxiv.org/html/2611.10502v1#A5.SS7.tab3)、[Table E.7 ICA reference](https://arxiv.org/html/2611.10502v1#A5.SS7.tab7)
- **abs** — arXiv abstract page: https://arxiv.org/abs/2611.10502v1 ；DOI: https://doi.org/10.48550/arXiv.2611.10502

[Home](../) · [AI Papers](./)
