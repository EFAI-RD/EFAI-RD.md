---
parent: AI Papers
nav_order: 4
title: "病歷埋入未證實鑑別診斷，下游 LLM 摘要沿用最高 31%"
catalog_id: "arxiv:2611.10601"
editors:
  - "Clare"
refs:
  main:
    title: "AI in the Clinical Documentation Loop: Effects of LLM-Induced Note Bloat and Diagnostic Overcall on Downstream LLMs"
    url: "https://arxiv.org/html/2611.10601v1"
  abs:
    title: "arXiv abstract page: 2611.10601v1"
    url: "https://arxiv.org/abs/2611.10601v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 病歷埋入未證實鑑別診斷，下游 LLM 摘要沿用最高 31%

## 來源

- 團隊：作者依序為 Jinghui Liu、Anthony Nguyen、Taylan Gurgenci；論文作者欄列出的單位為 Australian e-Health Research Centre, CSIRO、Mater Research Institute – University of Queensland，以及 Griffith University 的 School of Medicine and Dentistry。[(ref: main author block)](https://arxiv.org/html/2611.10601v1)
- 論文：*AI in the Clinical Documentation Loop: Effects of LLM-Induced Note Bloat and Diagnostic Overcall on Downstream LLMs*，arXiv:2611.10601v1（cs.CL；cs.AI），2026-11-07 提交，目前只有 v1；arXiv 頁註記為 ML4H 2026 Findings；授權 CC BY 4.0。[(ref: abstract)](https://arxiv.org/abs/2611.10601v1)
- 識別碼：arXiv [2611.10601](https://arxiv.org/abs/2611.10601v1)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.10601v1)、[PDF v1](https://arxiv.org/pdf/2611.10601v1)。
- 程式與資料：資料為公開的 MIMIC-III；論文附錄列出全部 reader、生成與評估 prompt 以及解碼設定，但未見程式碼或衍生資料的釋出連結。經費聲明為 Mater Foundation 的 Betty McGrath Seeding Grant 支持 Gurgenci 的研究時間。[(ref: main Appendix G)](https://arxiv.org/html/2611.10601v1#A7) [(ref: main Appendix C.1)](https://arxiv.org/html/2611.10601v1#A3.SS1) [(ref: main §5)](https://arxiv.org/html/2611.10601v1#S5)
- 研究性質：作者自稱 preliminary study（ML4H Findings 短文），但不是只有概念驗證：兩種 artifact 都實際生成並由七個 reader 模型讀取，主要分析涵蓋 300 個住院紀錄，附 2,000 次 bootstrap 95% 區間；臨床醫師覆核只有 24 對摘要，作者在附錄稱為 pilot。所有 AI 內容都是在 MIMIC-III 上人工插入的模擬，不是真實醫院中已累積的 AI 紀錄。[(ref: main §1)](https://arxiv.org/html/2611.10601v1#S1) [(ref: main §3.3)](https://arxiv.org/html/2611.10601v1#S3.SS3) [(ref: main Appendix F)](https://arxiv.org/html/2611.10601v1#A6)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文表 1 與附錄表 3–6 為準；只以圖呈現的劑量—反應曲線（圖 2、圖 3）未納入本文引述。

**編輯：** Clare

作者在 MIMIC-III 病歷中插入 AI 摘要、或把一個未證實的鑑別診斷寫進一段筆記，再讓七個開放權重 LLM 寫出院摘要：AI 摘要讓下游摘要穩定但小幅變差，被埋入的鑑別診斷則依 reader 不同有 2.5%–31.2% 被帶進摘要，而文件層級的品質指標幾乎看不出來。[(ref: main Table 3)](https://arxiv.org/html/2611.10601v1#A5.T3) [(ref: main Appendix E.4)](https://arxiv.org/html/2611.10601v1#A5.SS4)

## 流程

![左右兩欄圖。左欄為流程圖：最上方一個灰底、深灰實線圓角框寫「MIMIC-III: 300 admissions (one per patient) all notes charted before discharge」，兩支箭頭分向左下的藍色標題「Bloat (insert notes)」與右下的橘色標題「Distortion (edit one passage)」。左側淺藍底、深藍實線框列出「Dose d = 0.05-0.50 of final record」「AI-red: AI summary of preceding notes」「H-red: copied problem-list text / snippets」「F-red: templated boilerplate」「R-red: AI rephrase of copied notes」「(same slots, matched length)」；右側淺橘底、橘褐色實線框列出「Target diagnosis absent from record」「(ICD co-occurrence: related / unrelated)」「Control: neutral AI rephrase of passage」「Distorted: same rephrase + hedged unconfirmed differential (overcall)」。兩框各以向下箭頭連到中央灰底框「Reader LLM writes Brief Hospital Course (BHC) main: Gemma-4-26B-A4B; 6 further readers, 4 families generator: Qwen3.8-27B (alt. Nemotron-3.5-Lightning)」，再分出兩支箭頭到最下排：左為淺藍底框「Score vs clinician-written BHC ROUGE-L, BERTScore, LLM-judged quality (1-5), supported-claim share」，右為淺橘底框「Paired evaluator (control vs distorted): confirmed / possible / absent Induced propagation = mentioned only in distorted summary」；左下角小字「Redrawn by EFAI-RD from arXiv:2611.10601v1 Sections 3.1-3.4, Appendices B-D」。右欄為分組長條圖，標題「Table 3: overcall propagation by reader (overcalls written by Qwen3.8-27B; Qwen evaluator)」，縱軸「Induced propagation (%)」刻度 0–35，六組 reader 各有橘色「Related targets」與藍灰色「Unrelated targets」兩根長條：Gemma-4-12B 10.2／6.0、Gemma-4-26B-A4B (main) 24.6／16.1、Gemma-4-31B 31.2／23.9、Nemotron-3.5-Lightning 5.8／2.5、Llama-3.3-70B 9.7／7.3、Llama-4-Scout-17B-16E 6.2／6.5。](assets/llm-note-bloat-overcall-design-and-propagation.png)

*圖：本書庫依論文 §3.1–3.4 與附錄 B–D 重繪的兩種 artifact 實驗設計（左），以及六個 reader 對 Qwen3.8-27B 寫入的 overcall 的 induced propagation（右）。右欄數值來自附錄 [Table 3](https://arxiv.org/html/2611.10601v1#A5.T3)；Qwen3.8-27B 讀自己生成的筆記時只評相似度，因此不在右欄。*

## 背景／問題

作者引用文獻指出，AI scribe、自動摘要與出院衛教生成已廣泛可得，部分已大規模導入。[(ref: main §1)](https://arxiv.org/html/2611.10601v1#S1) 由此作者推論：病歷會同時被 AI 寫入與讀取，後續的 AI 會讀到前一輪 AI 寫進去的內容。這個「AI 讀 AI 寫的病歷」迴圈在真實醫院中有多普遍，論文沒有提供量測證據，屬於作者的研究前提；作者也承認 MIMIC-III 早於 LLM 文件工具，裡面沒有真實的 AI 內容。[(ref: main §5)](https://arxiv.org/html/2611.10601v1#S5)

作者要問的是：病歷裡已經存在的 AI 內容，會不會改變下游 LLM 讀同一份病歷後的輸出？論文區分兩種 artifact。第一種是 note bloat：AI 摘要不斷累積，改變病歷的長度與內容來源。第二種是 distortion：不是捏造事實，而是微妙地改變臨床發現的語境；作者以 diagnostic overcall（把臨床醫師原本不會寫的、未證實的鑑別診斷寫進病歷）作為代表。[(ref: main §1)](https://arxiv.org/html/2611.10601v1#S1)

## 方法摘要

- **下游任務** — reader LLM 依時間順序讀入出院前的所有筆記（含時間戳與筆記類型），寫出出院摘要中的 Brief Hospital Course（BHC），以臨床醫師寫的 BHC 作為參考。[(ref: main §3.1)](https://arxiv.org/html/2611.10601v1#S3.SS1)
- **Note bloat** — 在病歷中插入冗餘筆記，插入量以 dose（插入文字佔最終病歷的比例）0.05–0.50 共七級控制；比較 AI-red（AI 摘要前面的筆記）、兩種 H-red（複製人寫的 problem-list 段落或隨機段落）與 F-red（樣板文字），四者插入位置相同、長度相配；另以 R-red（AI 用自己的話改寫複製段落、內容不變）分開「AI 措辭」與「AI 內容」。[(ref: main §3.2)](https://arxiv.org/html/2611.10601v1#S3.SS2)
- **Diagnostic overcall** — 挑一個病歷中沒有的目標診斷，先讓 generator 中性改寫一段筆記作為 control，再在同一段改寫中加入 hedged、未證實的鑑別診斷作為 distorted；兩份病歷只差這個 overcall，AI 措辭在兩邊都存在。目標依 ICD 共現分成與主診斷 related 與 unrelated 兩類。[(ref: main §3.2)](https://arxiv.org/html/2611.10601v1#S3.SS2)
- **評估** — bloat 以 ROUGE-L、BERTScore、LLM judge 的 1–5 分品質評分與 supported-claim share 衡量；overcall 由 LLM evaluator 成對比較 control 與 distorted 兩份摘要，標記目標診斷為 confirmed、possible 或 absent，並定義 induced propagation：只在 distorted 摘要中出現（possible 或 confirmed）的比例。[(ref: main §3.3)](https://arxiv.org/html/2611.10601v1#S3.SS3)
- **模型** — generator 為 Qwen3.8-27B（另以 Nemotron-3.5-Lightning-30B-A3B 檢驗對 generator 的依賴），主要 reader 為 Gemma-4-26B-A4B，另有六個 reader 跨四個模型家族；全部以 vLLM 在本地執行。[(ref: main §3.4)](https://arxiv.org/html/2611.10601v1#S3.SS4)

## 方法詳解

- **隊列** — MIMIC-III 中每次住院的輸入為出院摘要之前的所有筆記（出院摘要本身排除，因其 BHC 是參考答案）。納入條件為至少 5 份先前筆記、至少 3 份敘述性筆記（Physician、Nursing、Nursing/other）、先前筆記估計不超過 32,000 tokens、主診斷屬循環、呼吸或感染章節，且至少 3 個 hedged findings；完全相同的筆記先去重，部分 copy-forward 保留。符合結構條件的 8,472 次住院中，以固定種子抽出 800 次篩 hedged findings，620 次符合，再抽出 300 次、每位病人一次。[(ref: main Appendix A)](https://arxiv.org/html/2611.10601v1#A1)
- **插入方式** — 原病歷 W 字、目標 dose d 時插入預算為 dW/(1−d)，切成約 200 字一份的筆記，放在相鄰筆記之間的隨機位置；AI-red 只摘要其插入位置之前的原始筆記，看不到先前插入的 AI 筆記。AI-red 的 prompt 以相同機率要求寫成「私人工作筆記」或「正式交班筆記」。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.10601v1#A2.SS1) [(ref: main Appendix G.2)](https://arxiv.org/html/2611.10601v1#A7.SS2)
- **R-red 的改寫幅度** — 2,100 個病歷版本（300 次住院 × 7 個 dose）中的 8,412 份筆記全部改寫，無遺漏或截斷；改寫與原筆記的 word-level unigram F1 中位數 0.65（第 10–90 百分位 0.48–0.81），長度中位數為原文 1.13 倍。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.10601v1#A2.SS1)
- **Overcall 目標的選法** — 段落取自 Physician 或 Nursing 筆記中 25–400 字的段落；候選診斷取自 DIAGNOSES_ICD，必須不在該次住院的編碼與病歷文字中、整體盛行率 1–10%。related 需至少 10 次共同住院、條件盛行率 ≥ 0.10 且 lift ≥ 2；unrelated 需條件盛行率 ≤ 0.02 且 lift ≤ 0.5。[(ref: main Appendix B.2)](https://arxiv.org/html/2611.10601v1#A2.SS2)
- **Evaluator 的約束** — Qwen3.8-27B 兼任 evaluator，但不評自己寫的摘要；overcall 另以 GPT-OSS-120B 作第二位 evaluator。成對評估時兩份摘要順序隨機，判為 confirmed 或 possible 時必須附上摘要中點名該診斷（ICD 名稱或同義詞）的逐字引文，並以程式檢查；兩個 evaluator 都先通過 50 對合成資料的校準。claim verification 先把摘要拆成最多 60 個 atomic claims，再逐一對照參考 BHC 標為 supported、contradicted 或 not_addressed。[(ref: main §3.4)](https://arxiv.org/html/2611.10601v1#S3.SS4) [(ref: main Appendix D)](https://arxiv.org/html/2611.10601v1#A4)
- **解碼設定** — Qwen generator 與 evaluator 為 temperature 0.7、top-p 0.8、top-k 20、presence penalty 1.5、seed 0；Gemma reader 為 temperature 1.0、top-p 0.95、top-k 64；Llama reader 為 temperature 0.6、top-p 0.9；Nemotron 為 temperature 1.0、top-p 0.95。reader 最大輸出 1,536 tokens，prompt 不指定摘要長度。[(ref: main Appendix C.1)](https://arxiv.org/html/2611.10601v1#A3.SS1) [(ref: main Appendix G.1)](https://arxiv.org/html/2611.10601v1#A7.SS1)
- **統計** — 所有比較都在同一次住院內配對；報告平均值與 2,000 次固定種子 percentile bootstrap 的 95% 區間，表 1 的主要 reader 三列另做 Bonferroni 校正。[(ref: main §3.3)](https://arxiv.org/html/2611.10601v1#S3.SS3) [(ref: main Table 1)](https://arxiv.org/html/2611.10601v1#S3.T1)
- **論文未交代** — 每份病歷是否只生成一份摘要、正文所稱「單一摘要 run-to-run variation」如何量測；dose 0.50 時樣本數由 300 降為 274（Qwen）與 258–259（Nemotron）、overcall 配對數為 171–179 與 243–252 的排除原因；以及程式碼與衍生資料是否釋出。[(ref: main §4.1)](https://arxiv.org/html/2611.10601v1#S4.SS1) [(ref: main Table 3)](https://arxiv.org/html/2611.10601v1#A5.T3) [(ref: main Table 4)](https://arxiv.org/html/2611.10601v1#A5.T4)

## 資料與實驗

### 資料

| 項目 | 內容 |
|---|---|
| 資料來源 | MIMIC-III（progress notes 與出院摘要） |
| 篩選 | 8,472 次住院符合結構條件 → 800 次篩 hedged findings → 620 次符合 → 抽 300 次 |
| 單位 | 每位病人 1 次住院，共 300 次 |
| 主診斷章節 | circulatory、respiratory、infectious |
| Bloat 版本 | 7 個 dose（0.05–0.50）× 4 種設定；R-red 只在 0.10、0.25、0.50 |
| Overcall 配對 | 每個 reader 約 171–179 對 related、243–252 對 unrelated |
| 臨床醫師覆核 | 24 對主要 reader 摘要（依 target type 與 evaluator 判定分層，各 6 對） |

[(ref: main Appendix A)](https://arxiv.org/html/2611.10601v1#A1) [(ref: main §3.2)](https://arxiv.org/html/2611.10601v1#S3.SS2) [(ref: main Table 3)](https://arxiv.org/html/2611.10601v1#A5.T3) [(ref: main Appendix F)](https://arxiv.org/html/2611.10601v1#A6)

### 實驗

Diagnostic overcall 的 induced propagation（表 1；除註明外，overcall 由 Qwen3.8-27B 寫入、評估主要 reader Gemma-4-26B-A4B 的摘要；括號為對主要 reader 三列做 Bonferroni 校正的 95% 區間）：

| | Related | Unrelated |
|---|---|---|
| Main reader | 24.6 [16.8, 32.4] | 16.1 [10.9, 22.2] |
| GPT-OSS evaluator | 23.8 [16.8, 31.4] | 15.6 [10.2, 21.1] |
| Nemotron generator | 10.2 [5.1, 15.8] | 8.3 [4.4, 12.7] |
| Five other readers | 5.8–31.2 | 2.5–23.9 |
| Clinician review：evaluator agreement | 22/24（κ = 0.83） | |
| Clinician review：genuine overcalls | 6/12 | 8/12 |

[(ref: main Table 1)](https://arxiv.org/html/2611.10601v1#S3.T1)

兩種效應依 reader 與 generator 分列（表 3 節錄；bloat 為 dose 0.25 時 AI-red 減 problem-list H-red，單位 pp；propagation 單位 %；Hardened 為 related／unrelated 中被寫成 confirmed 的比例；Rated accuracy 為該 reader 讀原始病歷時的 judge 評分，1–5）：

| Reader | ΔROUGE-L | Δsupported share | Related | Unrelated | Hardened | Rated accuracy |
|---|---|---|---|---|---|---|
| Gemma-4-12B | −0.76 | −3.03 | 10.2 | 6.0 | 0.0 / 0.4 | 2.35 |
| Gemma-4-26B-A4B (main) | −0.66 | −3.71 | 24.6 | 16.1 | 0.0 / 0.0 | 2.66 |
| Gemma-4-31B | −0.68 | −2.87 | 31.2 | 23.9 | 0.6 / 0.0 | 2.72 |
| Nemotron-3.5-Lightning | −0.98 | −4.97 | 5.8 | 2.5 | 0.0 / 0.0 | 1.92 |
| Llama-3.3-70B | −0.75 | −2.19 | 9.7 | 7.3 | 0.0 / 0.0 | 2.28 |
| Llama-4-Scout-17B-16E | −1.13 | −2.90 | 6.2 | 6.5 | 0.0 / 0.0 | 2.48 |
| Qwen3.8-27B (own notes) | −0.66 | – | – | – | – | – |
| Gemma-4-26B-A4B (main), Nemotron-written artifacts | −0.57 | −2.72 | 10.2 | 8.3 | 0.6 / 0.4 | 2.66 |

[(ref: main Table 3)](https://arxiv.org/html/2611.10601v1#A5.T3)

主要 reader 上 AI-red 減 problem-list H-red，依 dose 與 generator 分列（表 4；* 表示 95% 區間不含 0）：

| Measure (AI-red − H-red) | Qwen 0.10 | Qwen 0.25 | Qwen 0.50 | Nemotron 0.10 | Nemotron 0.25 | Nemotron 0.50 |
|---|---|---|---|---|---|---|
| ROUGE-L (pp) | −0.35* | −0.66* | −0.93* | −0.45* | −0.57* | −1.22* |
| Summary length (pp of reference) | +6.1* | +13.0* | +17.2* | +4.8* | +5.5* | +15.6* |
| Claims per summary | +2.0* | +4.1* | +5.4* | +1.4* | +2.7* | +5.1* |
| Supported-claim share (pp) | −1.2* | −3.7* | −3.5* | −0.9* | −2.7* | −4.5* |
| Contradicted-claim share (pp) | −0.1 | −0.3 | +0.6* | 0.0 | 0.0 | −0.2 |
| Rated accuracy (1–5) | +0.11 | −0.11 | −0.37* | +0.02 | −0.10 | −0.32* |

[(ref: main Table 4)](https://arxiv.org/html/2611.10601v1#A5.T4)

## 結果

- **AI 摘要讓下游摘要變差，且隨 dose 增加** — 在相同插入長度與位置下，AI-red 的下游 BHC 在文字相似度、judge 品質與 supported claims 上都比複製人寫文字差，H-red 與 F-red 則大致接近原始病歷的輸出。dose 0.5 時，AI-red 的 judge 準確度評分比 snippet H-red 低 0.47 分（95% CI 0.34–0.59）、比 F-red 低 0.43 分（0.31–0.55）。[(ref: main §4.1)](https://arxiv.org/html/2611.10601v1#S4.SS1)
- **效應小但一致** — 作者說明這個效應約為單一摘要 run-to-run variation 的一半；dose 0.25 時七個 reader 的 ROUGE-L 都下降（−0.66 到 −1.13 pp），換成 Nemotron 寫的筆記也下降（−0.57 pp）。[(ref: main §4.1)](https://arxiv.org/html/2611.10601v1#S4.SS1)
- **變差來自內容，不是 AI 措辭** — R-red 相對它改寫的複製筆記，ROUGE-L 變化在 dose 0.10、0.25、0.50 分別為 −0.07、−0.07、0.00 pp，區間都含 0；AI-red 相對 R-red 仍低 0.28、0.59、0.92 pp。AI 筆記讓摘要變長、多出參考 BHC 沒有的 claims，supported share 下降，contradicted share 幾乎不變。[(ref: main §4.1)](https://arxiv.org/html/2611.10601v1#S4.SS1) [(ref: main Table 4)](https://arxiv.org/html/2611.10601v1#A5.T4) [(ref: main Table 5)](https://arxiv.org/html/2611.10601v1#A5.T5)
- **讀自己的筆記沒有保護作用** — Qwen3.8-27B 讀自己生成的筆記時，AI-red 相對原始病歷的 ROUGE-L 下降 0.42、0.76、1.04 pp，主要 reader 為 0.46、0.74、0.97 pp。[(ref: main Appendix E.1)](https://arxiv.org/html/2611.10601v1#A5.SS1)
- **Overcall 會被帶進摘要，但多半仍寫成「可能」** — 主要 reader 的 induced propagation 為 related 24.6%、unrelated 16.1%，Bonferroni 校正後皆顯著大於 0；寫成 confirmed 的最多 0.6%。related 高於 unrelated，但差異不顯著。換 GPT-OSS evaluator 結果相近（23.8%、15.6%）。[(ref: main §4.2)](https://arxiv.org/html/2611.10601v1#S4.SS2) [(ref: main Table 1)](https://arxiv.org/html/2611.10601v1#S3.T1)
- **Reader 間差好幾倍** — judge 評分最高的兩個 reader（Gemma-4-26B-A4B 2.66、Gemma-4-31B 2.72）propagation 最高，評分最低的 Nemotron-3.5-Lightning（1.92）最低；作者認為可能與 reader 能力有關，但只是觀察。[(ref: main Appendix E.1)](https://arxiv.org/html/2611.10601v1#A5.SS1)
- **短的 overcall 較少被帶過去** — Nemotron 寫的 overcall 中位數只多 5–6 字（Qwen 為 16 字），主要 reader 的 propagation 約為 Qwen 版的一半；多 1–6 字的編輯只有 6.6% 被帶過去，多 7–12 字時兩個 generator 相近（13.5% 與 14.3%）。作者說明子群很小，只當作提示。[(ref: main Appendix E.1)](https://arxiv.org/html/2611.10601v1#A5.SS1)
- **文件層級指標看不出來** — 對有 overcall 的摘要與其 control 比較 ROUGE-L、BERTScore 與三項 judge 評分，全部 reader 與設定共 70 個對比中只有 2 個區間不含 0，且都是很小的 ROUGE-L 差異（−0.28、−0.25 pp）。[(ref: main Appendix E.4)](https://arxiv.org/html/2611.10601v1#A5.SS4)
- **臨床醫師覆核** — 一位共同作者臨床醫師在盲化下看 24 對摘要，與 evaluator 對 induced propagation 一致 22/24（91.7%，95% CI 74–98%，κ = 0.83），evaluator 找到醫師判定的全部 10 個 propagation，且都寫成 possible；但醫師只認為 14/24 個注入是真正的 overcall，其中 7 個被帶過去，5 個被評為可能引發不必要檢查或改變處置。[(ref: main §4.3)](https://arxiv.org/html/2611.10601v1#S4.SS3) [(ref: main Appendix F)](https://arxiv.org/html/2611.10601v1#A6)

## 限制

- **AI 內容是模擬的** — MIMIC-III 早於 LLM 文件工具，插入的 AI 內容是合成的，無法重現現行醫院中真實 AI 內容的組成；作者也指出尚未模擬多輪累積（作者自述）。[(ref: main §5)](https://arxiv.org/html/2611.10601v1#S5)
- **Overcall 目標依賴 ICD** — 缺席檢查只比對 ICD 名稱與同義詞，以別名或縮寫記載的狀況可能被誤判為不存在；臨床醫師只認定 24 個中 14 個是真正 overcall。95.3%（related）與 94.6%（unrelated）的 Qwen 編輯逐字使用 ICD 名稱，與臨床寫法不同（作者自述）。[(ref: main Appendix B.2)](https://arxiv.org/html/2611.10601v1#A2.SS2)
- **規模與模型範圍** — 300 次住院、七個本地開放權重 reader，未納入前沿閉源模型（作者自述需經合規管道）。[(ref: main §5)](https://arxiv.org/html/2611.10601v1#S5)
- **評估幾乎全由 LLM 完成** — bloat 的品質與 claim 判定只由 Qwen3.8-27B 評分，且同一個模型也是 artifact 的 generator；人類覆核只有一位共同作者、24 對、只針對 overcall。這是本書庫的解讀。[(ref: main §3.4)](https://arxiv.org/html/2611.10601v1#S3.SS4) [(ref: main Appendix F)](https://arxiv.org/html/2611.10601v1#A6)
- **reader 的絕對品質不高** — 讀原始病歷時 judge 準確度評分只有 1.92–2.72（1–5 分），bloat 的效應是在這個基線上的小幅變化（作者自己也稱之為 modest but consistent）；這個差距在臨床上是否有感，論文沒有評估。這是本書庫的解讀。[(ref: main Table 3)](https://arxiv.org/html/2611.10601v1#A5.T3)

## 與書庫其他文章的關係

兩篇都在問 LLM 讀病歷文字時，錯誤到底來自模型還是來自病歷本身；不確定性那篇讓 LLM 從 CCTA 報告抽取狹窄並分辨「讀錯報告」與「檢查本來就不一致」，本篇則反過來在病歷中刻意注入 AI 內容，看下游 LLM 會不會把它帶進出院摘要: [LLM 不確定性抓得出讀錯報告，抓不出 CCTA 與心導管落差](2026-11-17-llm-uncertainty-extraction-vs-clinical-discordance.md)

兩篇都在檢查醫療 LLM 面對不可靠上下文時的行為；guardrail 那篇顯示生醫微調模型在證據被抽掉時更少棄答，本篇則顯示 reader 會把病歷中 hedged、未證實的鑑別診斷保留進摘要，而一般品質指標看不出差異: [生醫微調 LLM：證據被抽掉時，25 對有 21 對更少棄答](2026-11-11-guardrail-erosion-biomedical-llm-abstention.md)

## 實務的啟發

- **可借用的量測方法** — 「同位置、等長度的 AI 筆記 vs 複製筆記 vs 樣板」與「只差一個 overcall 的配對病歷」這兩種控制設計，可以直接拿來檢查自家下游 LLM 對病歷中 AI 內容的敏感度；但本研究的 AI 內容是模擬的，真實病歷中的效應大小仍待驗證。
- **不要只看文件層級指標** — 本研究中 overcall 被帶進摘要時，ROUGE-L、BERTScore 與 judge 評分幾乎不變；若要監測這類錯誤，需要針對特定診斷的成對檢查，而不是整體摘要分數。
- **病歷中的 AI 內容值得標記來源** — 作者的結論是需要監測病歷中的 AI 生成內容，並在後續 AI 處理時納入考量；本研究顯示 AI 摘要即使內容忠於原文，仍會讓下游摘要變長、多出參考沒有的 claims，這是一個待驗證的警訊，而非已證實的臨床危害。
- **較強的 reader 不一定較安全** — 本研究中 judge 評分最高的兩個 Gemma reader propagation 也最高；選模時若只看摘要品質，可能同時選到最會沿用病歷中未證實診斷的模型。這只是七個模型上的觀察。

## References

- **main** — Liu J, Nguyen A, Gurgenci T. *AI in the Clinical Documentation Loop: Effects of LLM-Induced Note Bloat and Diagnostic Overcall on Downstream LLMs*. arXiv:2611.10601v1, 2026（ML4H 2026 Findings）. HTML: https://arxiv.org/html/2611.10601v1 ；deep links used: [§1](https://arxiv.org/html/2611.10601v1#S1)、[§3.1](https://arxiv.org/html/2611.10601v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.10601v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.10601v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.10601v1#S3.SS4)、[Table 1](https://arxiv.org/html/2611.10601v1#S3.T1)、[§4.1](https://arxiv.org/html/2611.10601v1#S4.SS1)、[§4.2](https://arxiv.org/html/2611.10601v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.10601v1#S4.SS3)、[§5](https://arxiv.org/html/2611.10601v1#S5)、[Appendix A](https://arxiv.org/html/2611.10601v1#A1)、[Appendix B.1](https://arxiv.org/html/2611.10601v1#A2.SS1)、[Appendix B.2](https://arxiv.org/html/2611.10601v1#A2.SS2)、[Appendix C.1](https://arxiv.org/html/2611.10601v1#A3.SS1)、[Appendix D](https://arxiv.org/html/2611.10601v1#A4)、[Appendix E.1](https://arxiv.org/html/2611.10601v1#A5.SS1)、[Table 3](https://arxiv.org/html/2611.10601v1#A5.T3)、[Table 4](https://arxiv.org/html/2611.10601v1#A5.T4)、[Table 5](https://arxiv.org/html/2611.10601v1#A5.T5)、[Appendix E.4](https://arxiv.org/html/2611.10601v1#A5.SS4)、[Appendix F](https://arxiv.org/html/2611.10601v1#A6)、[Appendix G](https://arxiv.org/html/2611.10601v1#A7)、[Appendix G.1](https://arxiv.org/html/2611.10601v1#A7.SS1)、[Appendix G.2](https://arxiv.org/html/2611.10601v1#A7.SS2)
- **abs** — arXiv abstract page: https://arxiv.org/abs/2611.10601v1

[Home](../) · [AI Papers](./)
