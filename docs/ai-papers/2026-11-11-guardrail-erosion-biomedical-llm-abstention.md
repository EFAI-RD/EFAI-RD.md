---
parent: AI Papers
nav_order: 2
title: "生醫微調 LLM：證據被抽掉時，25 對有 21 對更少棄答"
catalog_id: "arxiv:2611.08780"
editors:
  - "Clare"
refs:
  main:
    title: "Guardrail Erosion in Domain Fine-Tuned Large Language Models: A Paired Audit of Knowledge-Centric Abstention in Biomedical LLMs"
    url: "https://arxiv.org/html/2611.08780v1"
  abs:
    title: "arXiv abstract page: 2611.08780v1"
    url: "https://arxiv.org/abs/2611.08780v1"
  pdf:
    title: "arXiv PDF v1: 2611.08780v1"
    url: "https://arxiv.org/pdf/2611.08780v1"
  code:
    title: "Anonymized reproduction repository (Anonymous GitHub)"
    url: "https://anonymous.4open.science/r/guardrail-erosion-paper-8D9F"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 生醫微調 LLM：證據被抽掉時，25 對有 21 對更少棄答

## 來源

- 團隊：Stephen Peng、Vineet Jagadeesan Nair、Noah Broestl、Anne Friederike Kleppe、Steven Mills、Adi Zolotov，共 6 位作者，前三位為共同第一作者；單位為 BCG X AI Science Institute（Boston Consulting Group），Noah Broestl 另屬 University of Cambridge 的 Centre for Human-Inspired Artificial Intelligence。[(ref: pdf p.1)](https://arxiv.org/pdf/2611.08780v1#page=1)
- 論文：*Guardrail Erosion in Domain Fine-Tuned Large Language Models: A Paired Audit of Knowledge-Centric Abstention in Biomedical LLMs*，arXiv:2611.08780v1（cs.CL；cross-list cs.AI），2026-11-05 提交，目前只有 v1；授權為 CC BY-NC-SA 4.0；arXiv 頁註記將收錄於 ML4H 2026（PMLR volume 346）。[(ref: abstract)](https://arxiv.org/abs/2611.08780v1)
- 識別碼：arXiv [2611.08780](https://arxiv.org/abs/2611.08780v1)；DOI [10.48550/arXiv.2611.08780](https://doi.org/10.48550/arXiv.2611.08780)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.08780v1)、[PDF v1](https://arxiv.org/pdf/2611.08780v1)。
- 程式與資料：只用公開的 MedAbstain、ClinDet-Bench 與公開模型權重，無人體受試者；重現程式放在匿名化的程式庫（Anonymous GitHub），此類連結不保證長期可用。[(ref: pdf p.1)](https://arxiv.org/pdf/2611.08780v1#page=1) [(ref: code)](https://anonymous.4open.science/r/guardrail-erosion-paper-8D9F)
- 研究性質：觀察性稽核（observational audit），不是方法論文、也不是 pilot；作者沒有自己微調模型，而是把 25 個已公開的生醫微調模型各自和它的 base checkpoint 配對，在同一套提示下評估。[(ref: main §2.1)](https://arxiv.org/html/2611.08780v1#S2.SS1) [(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、附錄 A.2、A.4、A.6–A.9 與 Table 1–4 為準；論文的 Figure 1–16 只引用圖說與正文報告的統計量，未從圖上讀取逐對數值。

**編輯：** Clare

作者把 25 個公開的生醫微調 LLM 和各自的 base checkpoint 配對，在 MedAbstain 中「關鍵證據被抽掉、且提供棄答選項」的題目上，棄答率的中位數由 8.3% 降到 4.2%，25 對中有 21 對下降；但下降幅度與方向在各對之間差異很大，另一個基準 ClinDet-Bench 只呈現同方向、未達顯著的變化。[(ref: main §3.1)](https://arxiv.org/html/2611.08780v1#S3.SS1)

## 流程

![左右兩欄圖。左欄標題「Paired audit design (arXiv:2611.08780v1, Sec. 2)」，五個圓角框：上排兩個淺藍色框，左為「1 11 base checkpoints」（Llama-2 7B/13B/70B, Llama-3 8B, Llama-3 8B/70B-Instruct, Llama-3.1 8B/70B-Instruct, Llama-3.1 70B, Gemma-3 4B/27B-PT），右為「2 25 biomedical fine-tunes」（CPT, SFT, RL, DPO, QLoRA, MERGE；e.g. Med42, OpenBioLLM, HuatuoGPT-o1, Aloe-Beta, Meerkat, MedGemma；Each paired with its own base）；中排兩個淺橘色框，左為「3 Same completion prompt」（MedAbstain: 1,007 items x 4 variants, NA / A / NAP / AP (A, AP add abstain)；ClinDet-Bench: 94 scenarios, Met / Not met / Unable to determine；Greedy, temperature 0, 2,048 tokens），右為「4 Four dimensions, per pair」（Capability: accuracy (MA NA, CD Complete)；Caution: abstention on MA AP, CD Incomplete-Undeterminable；Calibration: ECE10, AUROC；All as fine-tune minus base；Commitment: max-choice prob., entropy）；下排一個橫跨兩欄的淺綠色框「5 Cohort inference (pair = unit)」（Wilcoxon signed-rank + BH over 15 tests; two-stage bootstrap over base checkpoints (p_cluster); robust = same direction, q_BH < 0.05 and p_cluster < 0.05）。框之間有五個實線箭頭：1 向右指 2、1 向下指 3、2 向下指 4、3 向右指 4、4 向下指 5。左下灰色小字「Redrawn by EFAI-RD from arXiv:2611.08780v1 Sec. 2, App. A.2 and Tables 3-4」。右欄為水平長條圖，標題「Table 1: nine pairs with an Instruct base」與「Median: completion -1.89, native chat -2.88」，橫軸「Change in MA AP appropriate abstention (pp, fine-tune minus base)」由 −25 到 5，每個模型兩根長條，藍色為「Completion prompt (primary)」、橘色為「Native chat template」，長條旁標數值：Aloe-Beta-70B −0.70／+0.10、Aloe-Beta-8B −8.44／−3.38、HuatuoGPT-o1-70B −0.89／+3.28、HuatuoGPT-o1-8B −1.89／−0.60、Med42-v2-70B −3.48／−3.18、Med42-v2-8B −21.25／−10.43、Meerkat-8B −5.66／−13.01、OpenBioLLM-70B −1.49／−2.18、Palmyra-Med-70B-32K +0.79／−2.88。](assets/guardrail-erosion-design-and-table1.png)

*圖：本書庫依論文 [§2](https://arxiv.org/html/2611.08780v1#S2)、[附錄 A.2](https://arxiv.org/html/2611.08780v1#A1.SS2) 與 [Table 3](https://arxiv.org/html/2611.08780v1#A1.T3)、[Table 4](https://arxiv.org/html/2611.08780v1#A1.T4) 重繪的配對稽核設計（左）；右欄為 [Table 1](https://arxiv.org/html/2611.08780v1#A1.T1) 中 base 為 Instruct 版的 9 對，分別在共同 completion prompt 與各模型原生 chat template 下，MA AP 適當棄答率的變化（百分點）。*

## 背景／問題

作者的出發點是：微調會改變模型權重，可能帶來難以預期的行為變化。論文引用的既有研究主要是「價值面」的拒答，例如只用 10 筆對抗性資料微調就能大幅削弱安全對齊，一般的實用型資料也會造成較小但不可忽略的退化；作者指出這些研究談的是 value-centric refusal，而不是「證據不足時要不要回答」。[(ref: main §1)](https://arxiv.org/html/2611.08780v1#S1)

論文因此把焦點放在 knowledge-centric abstention：可用證據不足以支持答案時，模型應該棄答或要求更多資訊；證據足夠時才回答。最接近的先前工作是 AbstentionBench，它在部分推理型微調看到棄答能力下降。生醫微調是否也會削弱這種「知道自己不知道」的行為、而且是否與準確率、校準一起移動，正是本篇想回答的問題，論文開頭沒有把它當成已知事實。[(ref: main §1)](https://arxiv.org/html/2611.08780v1#S1)

## 方法摘要

- **配對稽核** — 25 個公開的生醫微調模型，各自與其 base checkpoint 配對，base 共 11 個，涵蓋 Llama 2、Llama 3、Llama 3.1 與 Gemma-3；所有指標都以「微調版減 base」的配對差 Δ 表示。[(ref: main §2.1)](https://arxiv.org/html/2611.08780v1#S2.SS1) [(ref: main §2.2)](https://arxiv.org/html/2611.08780v1#S2.SS2)
- **兩個基準** — MedAbstain（MA）把同一題 MedQA 選擇題做成四個版本：原題或抽掉關鍵證據、有無棄答選項；ClinDet-Bench（CD）用 CHADS2 等臨床計分規則，問某項條件是 Met、Not met 還是 Unable to determine。[(ref: main A.6.1)](https://arxiv.org/html/2611.08780v1#A1.SS6.SSS1)
- **四個面向** — capability（有正確答案時的準確率）、caution（證據不足時是否棄答）、calibration（信心與正確率是否相符）與 commitment（選項機率分布有多集中）。[(ref: main §1)](https://arxiv.org/html/2611.08780v1#S1)
- **推論單位** — 每一對模型是一個樣本；以 Wilcoxon signed-rank 檢定、Benjamini–Hochberg（BH）多重比較校正，並因為 25 對只來自 11 個 base，另做以 base 為群集的兩階段 bootstrap。[(ref: main §2.3)](https://arxiv.org/html/2611.08780v1#S2.SS3)

## 方法詳解

- **模型挑選** — 條件為權重公開、base 血緣有揭露（Palmyra-Med 的 Llama-3 血緣為作者推斷）、訓練配方至少部分揭露，再兼顧參數規模與家族的涵蓋。25 個模型中 16 對的 base 是只做預訓練的 checkpoint，9 對的 base 是 Instruct 版。[(ref: main §2.1)](https://arxiv.org/html/2611.08780v1#S2.SS1) [(ref: main Table 4)](https://arxiv.org/html/2611.08780v1#A1.T4) [(ref: main A.2.2)](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS2)
- **MedAbstain 的四個版本** — No-Abstention（MA NA）、Abstention（MA A）、No-Abstention-Perturbed（MA NAP）、Abstention-Perturbed（MA AP）；每題 5 個選項，A 與 AP 另加一個棄答選項。使用公開的 MedQA-USMLE 半部，每個版本 1,007 題。證據抽除由 LLM 產生。[(ref: main A.6.1)](https://arxiv.org/html/2611.08780v1#A1.SS6.SSS1) [(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5)
- **ClinDet-Bench 的三類情境** — Complete 提供全部風險因子；Incomplete 遮掉部分因子，若遮掉的因子不論取什麼值結論都一樣即為 Determinable，否則為 Undeterminable。作者用公開程式庫 commit 1a05c63 的 94 個情境（32 Complete、30 Incomplete-Determinable、32 Incomplete-Undeterminable）；原論文報告 188 例，本研究評估的是較小的公開版。[(ref: main §2.1)](https://arxiv.org/html/2611.08780v1#S2.SS1) [(ref: main A.6.1)](https://arxiv.org/html/2611.08780v1#A1.SS6.SSS1)
- **提示與解碼** — 所有模型都用同一個純文字 completion 提示（題目、選項、以「Answer:」結尾），不套各模型的 chat template；greedy decoding、temperature 0、最多 2,048 個輸出 token。答案以由嚴到寬的 waterfall 規則解析，無法解析或前後矛盾的輸出記為答錯且未棄答。[(ref: main §2.1)](https://arxiv.org/html/2611.08780v1#S2.SS1) [(ref: main A.2)](https://arxiv.org/html/2611.08780v1#A1.SS2)
- **適當與過度棄答** — appropriate caution 量測 MA AP 與 CD Incomplete-Undeterminable 的棄答率；MA A 與 CD Incomplete-Determinable 的棄答則代表過度保守。兩者相減得到改編自 Youden's J 的 informedness：J = U(AP) − U(A)、J = U(Undet) − U(Det)，越大表示越會分辨何時該棄答。[(ref: main §2.2)](https://arxiv.org/html/2611.08780v1#S2.SS2)
- **覆蓋轉移分區** — 依 base 與微調版在 MA A 上是否棄答，把題目分成 always answered、newly answered、newly abstained、both abstained；newly answered accuracy gap 是微調版在「新回答的題」與「兩者都回答的題」上的準確率差。[(ref: main §2.2)](https://arxiv.org/html/2611.08780v1#S2.SS2)
- **機率指標** — 在第一個答案 token 的位置，把 top-20 token 中對應各選項的機率相加，再在選項之間重新正規化（choice-normalized）；據此計算 mean maximum-choice probability、normalized entropy（除以 log K，落在 0–1）、十個等寬 bin 的 ECE10，以及用信心區分對錯的 AUROC。另算「兩個模型都答錯的題」上的信心（shared-wrong confidence）。[(ref: main A.2)](https://arxiv.org/html/2611.08780v1#A1.SS2) [(ref: main A.8.8)](https://arxiv.org/html/2611.08780v1#A1.SS8.SSS8)
- **統計** — 對內用 exact McNemar、Fisher exact 與配對 item bootstrap；對整個隊列用雙尾 Wilcoxon signed-rank，BH 校正在 15 個預先指定的檢定（H1–H5）之間進行，機率指標另有 10 個檢定的次要族。作者定義的「穩健」需同時符合方向一致、q_BH < 0.05、p_cluster < 0.05。[(ref: main §2.3)](https://arxiv.org/html/2611.08780v1#S2.SS3)
- **算力** — ≤13B 模型用單張 NVIDIA L40S、27B–70B 用 8 張 H100 80GB，vLLM 0.26.0／0.27.1；全部約 38 L40S 與 28 H100 GPU-hours。[(ref: main A.2)](https://arxiv.org/html/2611.08780v1#A1.SS2)
- **論文未交代** — MedAbstain 棄答選項的實際文字，以及兩個推論 arm 共用的 random seed 數值，正文與附錄未列出。[(ref: main A.2)](https://arxiv.org/html/2611.08780v1#A1.SS2) [(ref: main A.2.2)](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS2)
- **論文未交代** — 附錄 A.2.2 寫 16 對預訓練 base 包含 Llama-1 與 Mistral-7B，但 Table 3 列出的 11 個 base 中沒有這兩者；論文未說明這個差異。[(ref: main A.2.2)](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS2) [(ref: main Table 3)](https://arxiv.org/html/2611.08780v1#A1.T3)
- **論文未交代** — 各模型的權重版本（revision／commit）只列到 Hugging Face repository 名稱；各個微調模型的訓練資料與超參數依公開揭露整理，作者說明揭露並不完整。[(ref: main Table 3)](https://arxiv.org/html/2611.08780v1#A1.T3) [(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5)

## 資料與實驗

### 資料

| 基準 | 版本／子集 | 題數 | 適當棄答的條件 | 用途 |
|---|---|---|---|---|
| MedAbstain（MA） | 公開 MedQA-USMLE 半部；NA、A、NAP、AP 四版 | 每版 1,007 題，5 個選項（A、AP 加棄答選項） | MA AP（證據被抽掉且可棄答） | capability（NA）、caution（AP）、過度保守（A）、calibration／commitment（NA） |
| ClinDet-Bench（CD） | 公開程式庫 commit 1a05c63 | 94 個情境：Complete 32、Incomplete-Determinable 30、Incomplete-Undeterminable 32 | 回答 Unable to determine 於 Incomplete-Undeterminable | capability／calibration（Complete）、caution（Undeterminable）、過度保守（Determinable） |

*資料：整理自 [§2.1](https://arxiv.org/html/2611.08780v1#S2.SS1) 與 [附錄 A.6.1](https://arxiv.org/html/2611.08780v1#A1.SS6.SSS1)。作者引用 MedAbstain 原作的人工驗證：49 題 AP 中有 38 題被判定應棄答。*

| Base 家族 | 微調模型（base checkpoint） | 對數 | MedQA 重疊旗標 |
|---|---|---|---|
| Llama-2 | Asclepius-Llama2-7B（Llama-2-7B）；Asclepius-Llama2-13B、Camel-Platypus2-13B、qCammel-13（Llama-2-13B）；Camel-Platypus2-70B、ClinicalCamel-70B、Med42-v1-70B、qCammel-70（Llama-2-70B） | 8 | ClinicalCamel-70B 為 yes；兩個 Asclepius 為 no；其餘 plaus. |
| Llama-3 | JSL-MedLlama-3-8B-v2、MMed-Llama-3-8B、MMed-Llama-3-8B-EnIns、OpenBioLLM-8B（Llama-3-8B）；Med42-v2-8B、Meerkat-8B（Llama-3-8B-Instruct）；OpenBioLLM-70B、Med42-v2-70B、Palmyra-Med-70B-32K（Llama-3-70B-Instruct，Palmyra 為推斷） | 9 | MMed-Llama-3-8B-EnIns 為 yes；其餘 plaus. |
| Llama-3.1 | Aloe-Beta-8B、HuatuoGPT-o1-8B（Llama-3.1-8B-Instruct）；Aloe-Beta-70B、HuatuoGPT-o1-70B（Llama-3.1-70B-Instruct）；MMed-Llama-3.1-70B、MMed-Llama-3.1-70B-MCQA（Llama-3.1-70B） | 6 | MMed-Llama-3.1-70B 為 plaus.，其餘 5 個為 yes |
| Gemma-3 | MedGemma-4B-IT（Gemma-3-4B-PT）；MedGemma-27B-Text-IT（Gemma-3-27B-PT） | 2 | plaus. |

*表：整理自 [Table 3](https://arxiv.org/html/2611.08780v1#A1.T3) 與 [Table 4](https://arxiv.org/html/2611.08780v1#A1.T4)。MA cont. 旗標：yes 為確認重用 MedQA／USMLE 衍生題目，plaus. 為可能但未確認，no 為無重疊；原表另列各模型的訓練配方（CPT、SFT、RL、DPO、QLoRA、MERGE）與階段數。*

### 實驗：隊列層級的主要結果（§3.1–3.5）

| 假設 | 結果（中位數，微調減 base） | p | q_BH | p_cluster | 作者判定 |
|---|---|---|---|---|---|
| H1 MA AP 適當棄答 | −3.48 pp（21 對下降、4 對上升；base 8.3% → 4.2%；clustered 95% CI −5.66 至 −0.79） | 0.0038 | 0.009 | 0.003 | 穩健 |
| H1 CD Incomplete-Undeterminable「Unable」 | −6.25 pp | 0.061 | 0.083 | 0.182 | 方向一致、未達顯著 |
| H2 MA informedness ΔJ | −0.60 pp | 0.034 | 0.052 | 0.100 | 校正後不顯著 |
| H2 CD informedness ΔJ | −2.71 pp | 0.158 | — | 0.195 | 無可靠變化 |
| H3 MA A newly answered accuracy gap | −14.98 pp（相對 −24.8%；clustered 95% CI −17.91 至 −8.36） | <0.0001 | 0.00009 | <0.001 | 穩健 |
| H3 newly abstained gap（base 準確率） | −11.47 pp | 0.014 | 0.023 | 0.051 | 未達群集門檻 |
| H4 MA NA normalized entropy | −0.191 | — | <0.001 | 0.001 | 穩健 |
| H4 MA NA mean maximum-choice probability | +0.127 | — | <0.001 | 0.002 | 穩健 |
| H4 MA NA shared-wrong confidence | +0.112 | — | <0.001 | 0.001 | 穩健 |
| H4 MA NA ECE10 | +0.040 | — | 0.009 | 0.040 | 穩健 |
| H4 CD Complete mean confidence | +0.185 | — | 0.018 | 0.035 | 穩健 |
| H4 CD Complete normalized entropy | −0.307 | — | 0.019 | 0.089 | 未達群集門檻 |
| H4 CD Complete shared-wrong confidence（23 對） | +0.225 | — | 0.019 | 0.094 | 未達群集門檻 |
| H4 CD Complete AUROC | +0.089 | — | 0.060 | 0.063 | 不顯著 |
| H5 capability 與 caution 相關 | MA r_P = −0.249；CD r_P = −0.538 | 0.210；0.008 | 0.225；0.028 | — | MA 不顯著、CD 顯著負相關 |

*表：整理自 [§3.1](https://arxiv.org/html/2611.08780v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.08780v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.08780v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.08780v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.08780v1#S3.SS5) 正文報告的統計量，論文正文沒有對應的彙總表；「—」為正文未報告。pp 為百分點；機率類指標無單位。*

### 實驗：原生 chat template 敏感度分析（Table 1）

| Adapted checkpoint | Base checkpoint | Completion | Native chat |
|---|---|---|---|
| Aloe-Beta-70B | Llama-3.1-70B-Instruct | −0.70 | +0.10 |
| Aloe-Beta-8B | Llama-3.1-8B-Instruct | −8.44 | −3.38 |
| HuatuoGPT-o1-70B | Llama-3.1-70B-Instruct | −0.89 | +3.28 |
| HuatuoGPT-o1-8B | Llama-3.1-8B-Instruct | −1.89 | −0.60 |
| Med42-v2-70B | Llama-3-70B-Instruct | −3.48 | −3.18 |
| Med42-v2-8B | Llama-3-8B-Instruct | −21.25 | −10.43 |
| Meerkat-8B | Llama-3-8B-Instruct | −5.66 | −13.01 |
| OpenBioLLM-70B | Llama-3-70B-Instruct | −1.49 | −2.18 |
| Palmyra-Med-70B-32K | Llama-3-70B-Instruct | +0.79 | −2.88 |
| Median | | −1.89 | −2.88 |

*表：[Table 1](https://arxiv.org/html/2611.08780v1#A1.T1)，MA AP 適當棄答率的配對變化（百分點），負值表示微調後較少適當棄答。只有 base 為 Instruct 版的 9 對可在兩側都套原生 chat template。*

## 結果

- **MedAbstain 上的適當棄答下降** — MA AP 棄答率的配對變化中位數 −3.48 個百分點，25 對中 21 對下降、4 對上升；base 與微調版的中位數為 8.3% 與 4.2%，對內相對降幅中位數 45.0%。經 BH 校正與 base 群集 bootstrap 後仍成立。[(ref: main §3.1)](https://arxiv.org/html/2611.08780v1#S3.SS1)
- **ClinDet-Bench 只有方向一致** — CD Incomplete-Undeterminable 回答「Unable to determine」的比例中位數下降 6.25 個百分點，但未通過校正與群集推論；作者明說穩健的結論只限於 MedAbstain。[(ref: main §3.1)](https://arxiv.org/html/2611.08780v1#S3.SS1)
- **少棄答不是因為更會分辨** — 如果微調讓模型更會分辨「可答」與「該棄答」，少棄答可能是好事；但 MA 與 CD 的 informedness 都沒有可靠的改善（中位數 −0.60 與 −2.71 個百分點）。作者指出 base 模型本來就對證據抽除反應很弱，解讀為微調沒有修正這個既有弱點，而不是已證實會讓它惡化。[(ref: main §3.2)](https://arxiv.org/html/2611.08780v1#S3.SS2)
- **新回答的題更容易錯** — 在 MA A 上，微調版「新回答」的題目準確率比「兩者都回答」的題目低 14.98 個百分點（相對 24.8%），是主要假設中最大且最穩健的效應。作者提醒，這個分區本身以 base 是否棄答為條件，新回答的題原本就預期較難；排除確認重疊模型與題數過少的分區後效應仍在。[(ref: main §3.3)](https://arxiv.org/html/2611.08780v1#S3.SS3) [(ref: main A.9.8)](https://arxiv.org/html/2611.08780v1#A1.SS9.SSS8)
- **能力本身未必變差** — 在必須作答的 MA NA 上，同樣分區內微調版與 base 的準確率差異都未通過校正，所以論文只能說「覆蓋改變的題目比較難」，不能說微調降低了這些題的知識。[(ref: main §3.3)](https://arxiv.org/html/2611.08780v1#S3.SS3)
- **信心更集中，錯題上也一樣** — MA NA 上 normalized entropy 降 0.191、最大選項機率升 0.127，兩者都答錯的題上信心也升 0.112；ECE10 升 0.040。AUROC 沒有可靠變化，表示信心變高，但用信心區分對錯的能力沒有跟著變好。CD Complete 上只有平均信心上升（+0.185）通過穩健門檻。[(ref: main §3.4)](https://arxiv.org/html/2611.08780v1#S3.SS4)
- **能力與謹慎不是固定的取捨** — MA 上 16 對準確率上升且棄答下降、1 對兩者都升、3 對準確率下降但棄答上升、5 對兩者都降，相關係數 −0.249 不顯著；CD 上為 −0.538 且顯著。兩個基準的對間異質性 I² 為 96.3% 與 93.4%，訓練配方、base 是否已對齊、訓練強度與參數量等調節變項在校正後都不顯著。[(ref: main §3.5)](https://arxiv.org/html/2611.08780v1#S3.SS5)
- **換成原生 chat template 方向不變** — 9 對 Instruct base 改用原生 chat template 後，MA AP 適當棄答 7 對下降、中位數 −2.88 個百分點（clustered 95% CI −10.43 至 +0.10，p = 0.074）；同 9 對在 completion 提示下為 −1.89、8 對下降。兩種格式的對內差異中位數 +0.79 個百分點、不顯著。作者也指出這 9 對只來自 Llama-3／3.1 Instruct 血緣，不代表整個隊列。[(ref: main A.2.2)](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS2)
- **其他敏感度分析** — 排除 7 對確認與 MedQA 重疊的模型後，18 對中 14 對下降，中位數 −3.92 個百分點；排除 4 個合併模型與血緣為推斷的 Palmyra 後，20 對中 17 對下降，中位數 −3.43。解析失敗集中在少數模型（Asclepius-Llama2-13B 29.1%、Asclepius-Llama2-7B 21.4%），排除後主要結果不變。[(ref: main A.9.8)](https://arxiv.org/html/2611.08780v1#A1.SS9.SSS8) [(ref: main A.2.1)](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS1)

## 限制

- **作者列出的基準限制** — MedAbstain 是選擇題，證據抽除由 LLM 產生，不是互動式臨床決策；原作的人工驗證只有 49 題，其中 38 題判定應棄答，所以 MA AP 不完全等於真實的臨床不確定。ClinDet-Bench 只有 94 例（Undeterminable 32 例），統計檢定力有限。兩個基準都沒有量測模型會不會轉介、追問資訊或升級處理，明確的棄答選項也未必能推廣到開放式生成。[(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5)
- **資料污染** — 許多受測模型的訓練或微調資料包含或可能包含 MedQA，而 MedAbstain 由 MedQA 衍生；作者說受限於公開揭露，無法做完全排除污染的分析。Table 4 中只有兩個 Asclepius 模型標為確認無重疊。[(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5) [(ref: main Table 4)](https://arxiv.org/html/2611.08780v1#A1.T4)
- **評估設定** — 只用一種 completion 提示與 greedy decoding；原生 chat template 只測 9 對，解碼設定與各發布者建議的 system prompt 未測。作者特別提到有的微調模型其建議 system prompt 要求「不確定時不要提供資訊」，這類設定可能直接影響棄答率。[(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5) [(ref: main A.2.2)](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS2)
- **機率指標的近似** — 信心只看 top-20 token、並在選項間重新正規化；以完整詞彙表重算 10 對（4–8B）後方向不變，但重新正規化讓 shared-error commitment 的變化中位數高估 0.7 點（最多 8.4 點）。[(ref: main A.4)](https://arxiv.org/html/2611.08780v1#A1.SS4)
- **觀察性設計** — 模型家族、base 是否已對齊、參數量、訓練資料與配方彼此混雜，只能描述現況，不能歸因；作者提出的三個可能機制（考試式資料強化「一律作答」、降低拒答的目標連帶壓低棄答、後訓練放大答案信心）都是待檢驗的假說。[(ref: main §4)](https://arxiv.org/html/2611.08780v1#S4) [(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5)
- **本書庫的解讀** — 棄答率的起點本來就很低：base 中位數只有 8.3%，而 MedAbstain 原作估計 AP 題約有 22% 在抽除證據後仍可回答（[附錄 A.6.1](https://arxiv.org/html/2611.08780v1#A1.SS6.SSS1)），換言之應棄答的比例遠高於模型實際棄答的比例。這篇量到的是「從很低降到更低」，比起把哪個模型當作「安全」，更適合用來說明單看準確率會漏掉什麼。

## 與書庫其他文章的關係

量化研究在 MedQA 等生醫文獻基準上比較 ClinicalCamel-70B、Llama3-Med42-70B、HuatuoGPT-o1-70B 等模型在不同精度下的分數與成本；本篇則把同一批生醫微調模型和各自的 base 配對，顯示這些模型在 MedQA 衍生題上的準確率之外，證據被抽掉時的棄答與信心也會隨微調改變: [生醫 LLM 量化：4-bit 省約 68% 記憶體，8-bit 反而最慢](2026-11-09-quantized-llm-biomedical-nlp-evaluation.md)

CARE-MVLM 在乳房攝影上把病灶抹掉，並以無關區域的同等編輯作對照，檢查 VLM 會不會改為棄答；本篇在文字題上用同樣「抽掉證據、看是否棄答」的邏輯，並以有無棄答選項的版本相減得到 informedness，兩篇都說明棄答率必須和證據是否真的被移除一起看: [把病灶抹掉，VLM 會改口說無法判斷嗎？四項同時成立只有 4.75%](2026-10-07-care-mvlm-mammography-counterfactual-abstention.md)

## 實務的啟發

1. **評估微調模型時，同時測它的 base。** 本篇所有效應都是配對差；只看單一模型的準確率，看不到「微調後少棄答、信心變高」這類變化。作者也把「配對評估、多面向報告」列為最有把握的建議。這是可直接借用的量測方法。[(ref: main §4)](https://arxiv.org/html/2611.08780v1#S4)
2. **在證據被抽掉的題目上量棄答，並一起報告過度保守。** 只看 AP 的棄答率，無法分辨模型是會判斷還是只是傾向保守；informedness（AP 減 A）把兩者分開。院內若要比較候選模型，可以照這個「有無證據 × 有無棄答選項」的四格設計建題。[(ref: main §2.2)](https://arxiv.org/html/2611.08780v1#S2.SS2)
3. **檢查模型「新回答」的那些題。** 微調後新回答的題目準確率中位數比其他題低約 15 個百分點；導入時抽查這些題，比只看整體準確率更能看出風險落在哪裡。[(ref: main §3.3)](https://arxiv.org/html/2611.08780v1#S3.SS3)
4. **不要用模型的信心值代替人工複核的門檻。** 微調後信心變高、連兩者都答錯的題也一樣，但區分對錯的 AUROC 沒有可靠改善；若流程打算以信心分數決定是否轉人工，這是需要在自家資料上先驗證的警訊。[(ref: main §3.4)](https://arxiv.org/html/2611.08780v1#S3.SS4)
5. **不要假設某種訓練配方比較安全。** 調節變項在校正後都不顯著、對間異質性超過 90%，結果應逐一模型稽核；同時記得本篇是觀察性稽核、單一提示、且有 MedQA 污染疑慮，數字不能直接搬到臨床部署的判斷。[(ref: main §3.5)](https://arxiv.org/html/2611.08780v1#S3.SS5) [(ref: main §5)](https://arxiv.org/html/2611.08780v1#S5)

## References

- `main` — Peng S, Nair VJ, Broestl N, Kleppe AF, Mills S, Zolotov A. *Guardrail Erosion in Domain Fine-Tuned Large Language Models: A Paired Audit of Knowledge-Centric Abstention in Biomedical LLMs*. arXiv:2611.08780v1, 2026（ML4H 2026, PMLR 346）. [https://arxiv.org/html/2611.08780v1](https://arxiv.org/html/2611.08780v1)
  - 深鏈：[§1](https://arxiv.org/html/2611.08780v1#S1)、[§2](https://arxiv.org/html/2611.08780v1#S2)、[§2.1](https://arxiv.org/html/2611.08780v1#S2.SS1)、[§2.2](https://arxiv.org/html/2611.08780v1#S2.SS2)、[§2.3](https://arxiv.org/html/2611.08780v1#S2.SS3)、[§3.1](https://arxiv.org/html/2611.08780v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.08780v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.08780v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.08780v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.08780v1#S3.SS5)、[§4](https://arxiv.org/html/2611.08780v1#S4)、[§5](https://arxiv.org/html/2611.08780v1#S5)、[A.2](https://arxiv.org/html/2611.08780v1#A1.SS2)、[A.2.1](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS1)、[A.2.2](https://arxiv.org/html/2611.08780v1#A1.SS2.SSS2)、[Table 1](https://arxiv.org/html/2611.08780v1#A1.T1)、[A.4](https://arxiv.org/html/2611.08780v1#A1.SS4)、[A.6.1](https://arxiv.org/html/2611.08780v1#A1.SS6.SSS1)、[Table 3](https://arxiv.org/html/2611.08780v1#A1.T3)、[Table 4](https://arxiv.org/html/2611.08780v1#A1.T4)、[A.8.8](https://arxiv.org/html/2611.08780v1#A1.SS8.SSS8)、[A.9.8](https://arxiv.org/html/2611.08780v1#A1.SS9.SSS8)
- `abstract` — arXiv abstract page, 2611.08780v1. [https://arxiv.org/abs/2611.08780v1](https://arxiv.org/abs/2611.08780v1)
- `pdf` — arXiv PDF v1（作者單位、Data and Code Availability 與倫理聲明見第 1 頁）. [https://arxiv.org/pdf/2611.08780v1](https://arxiv.org/pdf/2611.08780v1)
- `code` — Anonymized reproduction repository. [https://anonymous.4open.science/r/guardrail-erosion-paper-8D9F](https://anonymous.4open.science/r/guardrail-erosion-paper-8D9F)
- DOI：[https://doi.org/10.48550/arXiv.2611.08780](https://doi.org/10.48550/arXiv.2611.08780)

[Home](../) · [AI Papers](./)
