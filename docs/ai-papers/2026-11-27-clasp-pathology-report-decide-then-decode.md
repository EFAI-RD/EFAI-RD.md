---
parent: AI Papers
nav_order: 2
title: "病理報告生成：挑同院舊報告，BLEU-4 就逼近已發表方法"
catalog_id: "arxiv:2611.28576"
editors:
  - "Clare"
refs:
  main:
    title: "CLASP: Deciding Structure and Claims Before Decoding for Whole-Slide Pathology Report Generation"
    url: "https://arxiv.org/html/2611.28576v1"
  abs:
    title: "arXiv abstract page: 2611.28576v1"
    url: "https://arxiv.org/abs/2611.28576v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 病理報告生成：挑同院舊報告，BLEU-4 就逼近已發表方法

## 來源

- 團隊：Ziaullah Khan、Rashadul Islam Sumon、Md Ariful Islam Mozumder、Moon-Il Joo、Hee-Cheol Kim（韓國 Inje University，Digital Anti-aging Healthcare），以及 Duc-Son Pham（澳洲 Curtin University of Technology，Computing）。[(ref: main)](https://arxiv.org/html/2611.28576v1) [(ref: abstract)](https://arxiv.org/abs/2611.28576v1)
- 論文：*CLASP: Deciding Structure and Claims Before Decoding for Whole-Slide Pathology Report Generation*，arXiv:2611.28576v1（cs.CV；交叉列於 cs.AI、cs.CL），2026-11-21 提交，目前只有 v1；未註記發表場合；授權為 arXiv 非專屬散布授權 1.0。[(ref: abstract)](https://arxiv.org/abs/2611.28576v1)
- 識別碼：arXiv [2611.28576](https://arxiv.org/abs/2611.28576v1)；DOI [10.48550/arXiv.2611.28576](https://doi.org/10.48550/arXiv.2611.28576)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.28576v1)、[PDF v1](https://arxiv.org/pdf/2611.28576v1)。
- 程式與資料：摘要寫明程式與模型放在一個匿名程式庫（anonymous.4open.science 上的 CVPR-2027-FFB8），本文未核對其內容；資料為公開的 TCGA-BRCA／TCGA-LUAD 切片與 PathText 報告，切片特徵用公開釋出的 UNI2-h tile embeddings。[(ref: abstract)](https://arxiv.org/abs/2611.28576v1) [(ref: main §4.1)](https://arxiv.org/html/2611.28576v1#S4.SS1)
- 研究性質：方法研究加上基準分析，模型實際訓練與推論，不是 pilot；主結果為三個隨機種子的平均與標準差，並以病人層級 paired bootstrap 檢定。測試集只有 92（乳癌）與 44（肺腺癌）位病人；臨床正確性由 Llama-3.1-8B-Instruct 讀報告後對照 TCGA 臨床紀錄評分，沒有病理師評估。論文的 LLM 使用聲明寫明以 Claude（經 Claude Code）協助程式、分析與撰稿。[(ref: main §4.2)](https://arxiv.org/html/2611.28576v1#S4.SS2) [(ref: main §5)](https://arxiv.org/html/2611.28576v1#S5) [(ref: main LLM Usage Statement)](https://arxiv.org/html/2611.28576v1#Sx1)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、表 1 與附錄表 S1–S24 為準；論文圖 4 的病例影像與附錄圖 S1、S2 只引用正文寫出的數值。

**編輯：** Clare

在乳癌全切片病理報告的標準基準 PathText-BRCA 上，作者發現不做任何學習、只從查詢切片所屬醫院（由病例代碼得知）隨機挑 30 份訓練報告取共識，BLEU-4 就有 0.135，與已發表的 BiGen 相同；他們據此提出 CLASP，在寫第一個字之前先決定報告的句子結構、長度與要寫的發現，35M 參數的模型 BLEU-4 0.1425，但對照 TCGA 臨床紀錄的矛盾率反而上升，要把切片看不出的荷爾蒙受體狀態整段拿掉才降到 0.130。[(ref: main §3.1)](https://arxiv.org/html/2611.28576v1#S3.SS1) [(ref: main Table 1)](https://arxiv.org/html/2611.28576v1#S4.T1) [(ref: main §4.4)](https://arxiv.org/html/2611.28576v1#S4.SS4)

## 流程

![左右兩個面板。左側面板標題「(a) CLASP: decide once per slide, then decode」：最上方灰色框「WSI tile embeddings (UNI2-h) -> Slide Knowledge Encoder (SKE)」，以三支箭頭分別連到並排的三個框，右上角斜體註記「three decisions made before the first word」；三個框由左至右為淺橘色「ESP」（sentence plan + length from 10 / 5 most image-similar training reports）、淺藍色「CCD」（findings from calibrated slide posteriors (one global threshold)）、淺綠色「CSP」（put each finding into the planned sentence type that states it most often）。三個框各以箭頭連到下方粉紫色框「PCD (3-layer decoder): reads plan, claims, placement; trained with cross-entropy, then SAST」，再以一支向下箭頭連到最下方白色框「Optional explicit abstention: drop receptor-status sentence types and claims, delete any generated sentence of those types」。右側上方長條圖標題「(b) PathText-BRCA test BLEU-4 (Table 1, 92 patients)」，縱軸 Test BLEU-4，六根直條由左至右：灰色「LLM, no visual input (7B)」0.0790、灰色「TITAN + LLM (7B)」0.0780、淺藍「CLASP-Base」0.1106、橘色「Hospital consensus (no learning)」0.1315、淺藍「CLASP-Base + length control」0.1378、深藍「CLASP」0.1425。右側下方長條圖標題「(c) Contradictions with TCGA clinical records (Table 1; references: Sec. 4.4)」，縱軸 Contradiction rate (lower is better)，六根直條由左至右：白色「Reference reports」0.052、淺藍「CLASP-Base」0.169、淺藍「CLASP CE」0.185、深藍「CLASP」0.232、綠色「CLASP, receptors withheld」0.130、橘色「Hospital consensus」0.267。右下角灰色小字註明重繪來源。](assets/clasp-decide-then-decode-bleu-contradiction.png)

*圖：本書庫依論文 [§3](https://arxiv.org/html/2611.28576v1#S3)、[圖 3](https://arxiv.org/html/2611.28576v1#S3.F3) 與 [§3.8](https://arxiv.org/html/2611.28576v1#S3.SS8) 重繪的流程示意（左），右側兩張長條圖的數值取自論文[表 1](https://arxiv.org/html/2611.28576v1#S4.T1)「Run under our protocol」區塊（有多個種子者為三種子平均）；參考報告的矛盾率取自 [§4.4](https://arxiv.org/html/2611.28576v1#S4.SS4)。左圖三個彩色框是解碼前做的三個決定，最下方白框為可選的 explicit abstention；右圖橘色直條是不經學習的 hospital consensus，深藍直條是 CLASP 主模型。*

## 背景／問題

全切片影像（whole-slide image，WSI）通常被表示成上萬個 tile 的特徵，病理報告則是依報告醫院格式寫成、平均約 149 個 token 的結構化文字。PathText-BRCA 是這個任務的標準基準，把 TCGA-BRCA 診斷切片配上清理過的病理報告；過去的進展多來自給解碼器更好的證據：multiple-instance 編碼器、階層式切片表示、檢索報告句子與重新排序的知識，以及切片層級多模態 LLM。[(ref: main §1)](https://arxiv.org/html/2611.28576v1#S1) [(ref: main §2)](https://arxiv.org/html/2611.28576v1#S2)

作者的切入點是：這些方法都把「報告多長、怎麼分段、寫哪些發現、寫在哪一句」留給 beam search 逐字決定，而這些報告層級的選擇主導了基準分數。論文以自己的分析支撐這個前提，而不只是引用：[(ref: main §3.1)](https://arxiv.org/html/2611.28576v1#S3.SS1)

- **切片洩漏醫院** — 在平均 UNI2-h tile 特徵上做線性探測，能辨認 92.4% 測試切片的來源醫院（多數類只有 15.2%）；最像的那份訓練報告在 82.6% 的測試病例來自同一家醫院。同院報告兩兩之間的句子 BLEU-4 是異院的 2.4–2.6 倍。[(ref: main §3.1)](https://arxiv.org/html/2611.28576v1#S3.SS1) [(ref: main Appendix A)](https://arxiv.org/html/2611.28576v1#A1)
- **格式比內容值分** — 從查詢病例所屬醫院隨機抽 30 份報告取共識，測試 BLEU-4 0.135，等於 BiGen 已發表的分數；改挑 30 份真實發現最相符的報告反而只有 0.113。這裡的「所屬醫院」由 TCGA 病例代碼直接讀出，是分析用的 oracle，不是模型可用的資訊。[(ref: main Figure 2)](https://arxiv.org/html/2611.28576v1#S3.F2) [(ref: main Table S1)](https://arxiv.org/html/2611.28576v1#A1.T1)
- **檢索到的報告長度對、內容錯** — 最像的 8 份訓練報告平均 144 token（參考 149），但其中的發現陳述只有 38.7% 對查詢病例成立。[(ref: main Appendix A)](https://arxiv.org/html/2611.28576v1#A1)
- **生成器寫太短、只寫常見發現** — 不含任何決定的 CLASP-Base 平均只寫 109 token；它寫出的發現 micro-F1 0.432，和「每份報告都寫最常見的四個發現」的 0.403 差不多，還低於它自己的切片分類器（0.499）。[(ref: main §3.1)](https://arxiv.org/html/2611.28576v1#S3.SS1)

因此論文要回答的是：與其期待解碼器自己決定這些事，能不能在解碼前就明確決定？

## 方法摘要

- **Slide Knowledge Encoder（SKE）** — 把 UNI2-h tile 特徵轉成「帶有發現資訊」的證據：tile 先查詢 20 個最常見發現的詞向量，再讓發現回頭聚集支持它的 tile，並與發現圖（finding graph）和檢索報告做 knowledge attention。[(ref: main §3.3)](https://arxiv.org/html/2611.28576v1#S3.SS3)
- **Exemplar Structure Prior（ESP）** — 句子結構與長度取自影像最相似的訓練報告：從 10 份最相似報告的句型序列取 medoid 當 sentence plan，長度取 5 份最相似報告的平均。[(ref: main §3.4)](https://arxiv.org/html/2611.28576v1#S3.SS4)
- **Calibrated Claim Decision（CCD）** — 要寫哪些發現只由切片決定：切片層級多標籤分類器的 class weighting 以解析方式還原成校準後的後驗機率，再用一個在驗證集選定的全域門檻決定 claim。[(ref: main §3.5)](https://arxiv.org/html/2611.28576v1#S3.SS5)
- **Claim-to-Sentence Placement（CSP）** — 每個 claim 放進 plan 中「最常陳述該發現的句型」的那一句。[(ref: main §3.6)](https://arxiv.org/html/2611.28576v1#S3.SS6)
- **Plan-Conditioned Decoder（PCD）與 SAST** — 三層 Transformer 解碼器在每一步讀取剩餘句數、目前句型、剩餘 token 數與 claim；先以 cross-entropy 訓練，再以 Structure-Anchored Sequence Training（SAST）在測試時的決定下取樣、以 BLEU-4＋METEOR＋ROUGE-L 為 reward 做序列層級訓練。[(ref: main §3.3)](https://arxiv.org/html/2611.28576v1#S3.SS3) [(ref: main §3.7)](https://arxiv.org/html/2611.28576v1#S3.SS7)
- **Explicit abstention** — 對切片無法判定的變項（此處是以免疫組織化學測定的受體狀態），從 plan 移除對應句型、撤回對應 claim，並在解碼後刪除被分到這些句型的句子；不需訓練或調參。[(ref: main §3.8)](https://arxiv.org/html/2611.28576v1#S3.SS8)
- **評估** — 基準詞面指標（BLEU-1–4、METEOR、ROUGE-L、CIDEr），加上一個獨立的臨床評估：用 Llama-3.1-8B-Instruct 對每份報告回答七個變項的選擇題（含「未陳述」選項），對照 TCGA-BRCA 臨床紀錄算 macro-F1 與 contradiction rate（報告陳述的值與紀錄相反的病人比例）；另報 PathReportEval 的 CRQS、REG 2025 分數與 BERTScore。[(ref: main §4.1)](https://arxiv.org/html/2611.28576v1#S4.SS1) [(ref: main Appendix E)](https://arxiv.org/html/2611.28576v1#A5)

## 方法詳解

- **句型怎麼來** — 訓練報告的句子以 TF-IDF（unigram 與 bigram、min df 3、SVD 64 維、ℓ2 正規化）做 k-means 分成 C = 24 種句型；plan 之間的距離是除以較長 plan 長度的 edit distance。[(ref: main Appendix N)](https://arxiv.org/html/2611.28576v1#A14)
- **發現詞彙與發現圖** — 20 個 topic 是訓練報告中最常見的發現，由一個帶否定處理的規則式抽取器（46 個乳房病理發現的同義詞樣式）得到；發現圖依五個組織區塊（invasive tumour、ducts and lobules、benign parenchyma、axillary lymph nodes、surgical margins）兩兩相連，加一個連到全部發現的 global node，共 69 條無向邊。[(ref: main Appendix H)](https://arxiv.org/html/2611.28576v1#A8) [(ref: main Table S15)](https://arxiv.org/html/2611.28576v1#A8.T15)
- **校準的作法** — 以 w_j = n⁻/n⁺ 加權正例的 BCE，其最小值的 logit 等於 logit p_j + log w_j，所以減去 log w_j 就還原後驗機率，不必另外擬合校準器。三個種子各自的分類器選出門檻 τ = 0.17、0.19、0.27；驗證集上每份報告平均 5.7 個 claim（參考報告 3.9 個），作者說明這是 F1 最佳規則為了召回稀有發現而接受偽陽性。[(ref: main §3.5)](https://arxiv.org/html/2611.28576v1#S3.SS5) [(ref: main Appendix G)](https://arxiv.org/html/2611.28576v1#A7)
- **訓練三階段** — 先單獨訓練 tile 投影與發現圖（多標籤分類，之後凍結作為 CCD 的模型）；再以 cross-entropy 在「參考報告自己的結構與發現」條件下訓練 SKE 與 PCD；最後 SAST 以 5 個樣本、leave-one-out baseline 在測試時的決定下微調。沒有結構錨點的序列訓練在初步實驗中讓報告長到 181–187 token、驗證 BLEU-4 下滑；加上錨點後維持在 139–141 token。[(ref: main §3.7)](https://arxiv.org/html/2611.28576v1#S3.SS7) [(ref: main Appendix M)](https://arxiv.org/html/2611.28576v1#A13)
- **規模與成本** — CLASP 35.1M 參數（含凍結的 2.4M 切片分類器），三個決定增加 5.6M 參數與約 3% 計算；在一張 RTX A5000 上每張切片推論 1.6 秒、峰值 0.51 GiB；訓練每個種子 1–2 小時，加 SAST 66–95 分鐘。[(ref: main Table S14)](https://arxiv.org/html/2611.28576v1#A8.T14) [(ref: main §4.2)](https://arxiv.org/html/2611.28576v1#S4.SS2)
- **比較協定** — 所有模型都以驗證 BLEU-4 選 checkpoint、測試集只解碼一次；重訓的 MI-Gen 與 HistGen 只跑一個種子，CLASP 與 LLM 基線各三個種子。作者指出 WsiCaption、BiGen、HistGen 的公開訓練程式在每次驗證時也會對測試集評分並記錄最佳測試分數；他們在一次 CLASP-Base 重跑中記錄 18 個驗證回合的測試 BLEU-4，範圍 0.079–0.121，和已發表方法之間的差距同一量級。[(ref: main §4.2)](https://arxiv.org/html/2611.28576v1#S4.SS2) [(ref: main Appendix J)](https://arxiv.org/html/2611.28576v1#A10)
- **切片層級 LLM 基線為何重訓** — 公開的 SlideChat 訓練資料含 92 位測試病人中 75 位的報告，WSI-LLaVA 的 WSI-Bench 訓練集包含全部 92 位，因此作者不評估釋出的權重，而是在相同 792 份訓練報告上重訓：微調 HistoGPT-1B，以及以 Qwen2.5-7B-Instruct＋LoRA 為解碼器的 SlideChat 架構、TITAN＋LLM 與不給影像的 LLM。[(ref: main Appendix K)](https://arxiv.org/html/2611.28576v1#A11) [(ref: main Table S17)](https://arxiv.org/html/2611.28576v1#A11.T17)
- **論文未交代** — 程式放在匿名程式庫，本文未核對內容；臨床評估的讀者是 Llama-3.1-8B，作者只以參考報告驗證讀者（變項有陳述時與紀錄一致 76–95%），沒有病理師判讀生成報告；20 個 silver 發現標籤與 CE-F1 來自同一個規則式抽取器，作者明說 CE-F1 不獨立，只用於元件間比較；RANGER 與 BiGen 無法重訓，與已發表數字的比較跨了不同測試集（93 對 92 位）與特徵；BERTScore 在 CLASP 最低（0.117），作者歸因於結構條件化產生較多三字以內的句子片段。[(ref: main Appendix C)](https://arxiv.org/html/2611.28576v1#A3) [(ref: main Appendix E)](https://arxiv.org/html/2611.28576v1#A5) [(ref: main Appendix B)](https://arxiv.org/html/2611.28576v1#A2)

## 資料與實驗

### 資料

| 資料 | 內容 | 病人數（train／val／test） | 用途 |
|---|---|---|---|
| PathText-BRCA | TCGA-BRCA 診斷切片＋清理過的病理報告；BiGen 的病人層級切分，每人一張切片；有 UNI2-h 特徵者 969／977 | 792／85／92 | 主實驗 |
| PathText-LUAD | TCGA-LUAD 第一張診斷切片＋PathText 報告；33 個來源醫院，與 BRCA 的 38 個不重疊 | 380／42／44 | 跨器官、跨醫院泛化 |
| TCGA-BRCA 臨床紀錄 | 組織型態、ER、PR、HER2、淋巴結、切緣、腫瘤大小；只用於評估 | 每變項 75–92 位測試病人 | 獨立臨床評估 |

BRCA 報告平均 token 數：訓練 139.7、驗證 149.4、測試 149.2；切片平均 12,016 個 tile，上限 10,000 個。[(ref: main §4.1)](https://arxiv.org/html/2611.28576v1#S4.SS1) [(ref: main Table S23)](https://arxiv.org/html/2611.28576v1#A14.T23) [(ref: main Appendix I)](https://arxiv.org/html/2611.28576v1#A9) [(ref: main Table S5)](https://arxiv.org/html/2611.28576v1#A3.T5)

### 實驗：PathText-BRCA 測試集，相同協定下的比較（論文表 1 下半，平均值）

| Method | B-1 | B-4 | MTR | R-L | CIDEr | F1 | Contr.↓ | CRQS |
|---|---|---|---|---|---|---|---|---|
| MI-Gen | 0.406 | 0.1265 | 0.157 | 0.295 | 0.076 | 0.259 | 0.108 | 0.259 |
| HistGen | 0.293 | 0.0866 | 0.130 | 0.273 | 0.049 | 0.201 | 0.161 | 0.236 |
| HistoGPT-1B | 0.312 | 0.0823 | 0.136 | 0.267 | 0.052 | 0.265 | 0.191 | 0.157 |
| SlideChat arch. (7B) | 0.327 | 0.0791 | 0.137 | 0.248 | 0.029 | 0.209 | 0.197 | 0.185 |
| TITAN + LLM (7B) | 0.340 | 0.0780 | 0.140 | 0.251 | 0.039 | 0.175 | 0.152 | 0.207 |
| + Clasp decisions as text | 0.405 | 0.0878 | 0.161 | 0.260 | 0.076 | 0.324 | 0.210 | 0.248 |
| LLM without visual input (7B) | 0.327 | 0.0790 | 0.136 | 0.246 | 0.054 | 0.233 | 0.291 | 0.188 |
| Most similar training report | 0.439 | 0.1068 | 0.182 | 0.281 | 0.062 | 0.305 | 0.163 | 0.232 |
| Consensus of 30 similar | 0.445 | 0.1201 | 0.185 | 0.286 | 0.088 | 0.327 | 0.227 | 0.245 |
| Hospital consensus | 0.468 | 0.1315 | 0.199 | 0.302 | 0.084 | 0.337 | 0.267 | 0.229 |
| Clasp-Base | 0.363 | 0.1106 | 0.150 | 0.287 | 0.112 | 0.293 | 0.169 | 0.266 |
| Clasp-Base + length control | 0.453 | 0.1378 | 0.176 | 0.288 | 0.104 | 0.330 | 0.189 | 0.260 |
| Clasp-Base + Esp | 0.452 | 0.1416 | 0.174 | 0.293 | 0.126 | 0.314 | 0.170 | 0.244 |
| + Ccd | 0.448 | 0.1350 | 0.173 | 0.287 | 0.121 | 0.289 | 0.180 | 0.245 |
| + Csp = Clasp CE | 0.447 | 0.1383 | 0.172 | 0.289 | 0.126 | 0.313 | 0.185 | 0.280 |
| + Sast = Clasp | 0.450 | 0.1425 | 0.174 | 0.301 | 0.113 | 0.328 | 0.232 | 0.269 |
| Clasp-EMA (validation-selected) | 0.454 | 0.1445 | 0.175 | 0.303 | 0.121 | 0.279 | 0.209 | 0.267 |
| Clasp, receptor status withheld | 0.405 | 0.1265 | 0.162 | 0.298 | 0.073 | 0.222 | 0.130 | n/a |

B-1／B-4：BLEU-1／BLEU-4；MTR：METEOR；R-L：ROUGE-L；F1 與 Contr.：七個 TCGA 臨床變項的 macro-F1 與 contradiction rate。表中省略論文的 BLEU-2／BLEU-3 欄、各列標準差與顯著性標記；MI-Gen、HistGen 為單一種子，檢索列為確定性結果，其餘為三種子平均。論文表 1 上半另列已發表方法的單次結果（不同測試集，例如 BiGen B-4 0.135、RANGER 0.1435）。[(ref: main Table 1)](https://arxiv.org/html/2611.28576v1#S4.T1)

### 實驗：與已發表最佳結果（RANGER，引用值）比較（論文表 S4）

| Metric | RANGER | Clasp（三種子） | Clasp 95% 區間 | 種子 ≥ RANGER | p |
|---|---|---|---|---|---|
| BLEU-1 | 0.4598 | 0.450 ± 0.007 | [0.418, 0.469] | 0/3 | 0.14 |
| BLEU-2 | 0.3044 | 0.310 ± 0.003 | [0.286, 0.325] | 3/3 | 0.08 |
| BLEU-3 | 0.2036 | 0.214 ± 0.003 | [0.195, 0.228] | 3/3 | 0.02 |
| BLEU-4 | 0.1435 | 0.1425 ± 0.0026 | [0.1280, 0.1535] | 1/3 | 0.57 |
| METEOR | 0.1883 | 0.174 ± 0.002 | [0.165, 0.182] | 0/3 | 0.00 |
| ROUGE-L | 0.3038 | 0.301 ± 0.004 | [0.290, 0.311] | 1/3 | 0.27 |

區間只涵蓋 CLASP 自己的病人抽樣不確定性；RANGER 的引用值沒有報告自己的變異。[(ref: main Table S4)](https://arxiv.org/html/2611.28576v1#A2.T4)

### 實驗：Explicit abstention（論文表 S8，測試集三種子平均）

| 設定 | B-4 | MTR | R-L | Len | F1 | Contr.↓ | ER 陳述／矛盾 | PR 陳述／矛盾 | Nodes 陳述／矛盾 |
|---|---|---|---|---|---|---|---|---|---|
| Clasp-Base | 0.1106 | 0.150 | 0.287 | 109 | 0.293 | 0.169 | 0.38 / 0.18 | 0.38 / 0.18 | 0.68 / 0.34 |
| Clasp CE | 0.1383 | 0.172 | 0.289 | 143 | 0.313 | 0.185 | 0.48 / 0.28 | 0.50 / 0.26 | 0.88 / 0.35 |
| Clasp | 0.1425 | 0.174 | 0.301 | 143 | 0.328 | 0.232 | 0.67 / 0.34 | 0.67 / 0.36 | 0.95 / 0.46 |
| abstain: receptors | 0.1265 | 0.162 | 0.298 | 122 | 0.222 | 0.130 | 0.06 / 0.04 | 0.05 / 0.02 | 0.92 / 0.48 |
| abstain: receptors, nodes | 0.1022 | 0.143 | 0.294 | 95 | 0.187 | 0.116 | 0.07 / 0.06 | 0.03 / 0.03 | 0.69 / 0.39 |

Len 為每份報告 token 數；ER、PR、Nodes 兩個數字為「陳述該變項的報告比例／矛盾率」。[(ref: main Table S8)](https://arxiv.org/html/2611.28576v1#A4.T8)

### 實驗：釋出的切片層級 LLM 看過多少測試報告（論文表 S17）

| Model | File | Patients | Train (792) | Val (85) | Test (92) |
|---|---|---|---|---|---|
| SlideChat | SlideInstruction, stage-1 captions | 3294 | 602 | 65 | 75 |
| SlideChat | SlideInstruction, stage-2 VQA | 3294 | 602 | 65 | 75 |
| SlideChat | SlideBench-Caption (its test set) | 1547 | 147 | 14 | 11 |
| WSI-LLaVA | WSI-Bench, train | 8383 | 790 | 85 | 92 |
| WSI-LLaVA | WSI-Bench, test | 727 | 161 | 15 | 16 |

[(ref: main Table S17)](https://arxiv.org/html/2611.28576v1#A11.T17)

### 實驗：PathText-LUAD 泛化（論文表 S16，44 位測試病人）

| Method | B-1 | B-4 | MTR | R-L | CIDEr | F1 of stated findings |
|---|---|---|---|---|---|---|
| Most similar training report | 0.430 | 0.095 | 0.196 | 0.284 | 0.143 | 0.449 |
| Consensus of 30 similar | 0.412 | 0.091 | 0.170 | 0.270 | 0.088 | 0.458 |
| Clasp-Base | 0.363 ± 0.021 | 0.097 ± 0.007 | 0.141 ± 0.006 | 0.286 ± 0.002 | 0.086 ± 0.031 | 0.479 ± 0.030 |
| Clasp CE | 0.418 ± 0.002 | 0.115 ± 0.002 | 0.149 ± 0.002 | 0.286 ± 0.007 | 0.123 ± 0.010 | 0.417 ± 0.046 |
| Clasp | 0.434 ± 0.007 | 0.128 ± 0.004 | 0.152 ± 0.001 | 0.297 ± 0.007 | 0.116 ± 0.007 | 0.469 ± 0.039 |

肺癌沒有做臨床紀錄評估，因為該評估讀的是乳癌專屬變項。[(ref: main Table S16)](https://arxiv.org/html/2611.28576v1#A9.T16)

## 結果

- **相同協定下 BLEU 最高，但多半來自長度** — CLASP 的 BLEU-4 0.1425 顯著高於每個重訓的生成器、每個切片層級 LLM 與每個檢索對照；相對 CLASP-Base，報告從 109 拉長到 143 token、BLEU-4 從 0.111 升到 0.1425（p < 0.001）。但只把 CLASP-Base 的結束 token 擋到 ESP 長度之前（length control）就有 0.1378，與 CLASP 的差距 +0.005 不顯著；作者自己的結論是「就 BLEU 而言，大部分是長度」。[(ref: main §4.3)](https://arxiv.org/html/2611.28576v1#S4.SS3)
- **不經學習的醫院共識拿到最高 BLEU-1 與 METEOR** — 以預測的來源醫院取共識報告，BLEU-1 0.468、METEOR 0.199 都是表中最高；作者解讀為偏召回的指標獎勵醫院的報告格式。[(ref: main §4.3)](https://arxiv.org/html/2611.28576v1#S4.SS3) [(ref: main Table 1)](https://arxiv.org/html/2611.28576v1#S4.T1)
- **7B 切片 LLM 學到的是「典型報告」** — 在 792 份報告上重訓的切片層級 LLM BLEU-4 0.078–0.082，低於 MI-Gen 與每個檢索對照；不給影像的 LLM 對全部 92 位病人寫出同一份報告，BLEU-4 0.079，與看得到切片的 LLM 相當；SlideChat 架構與 TITAN＋LLM 對 92 位病人只寫出 17–74 種不同報告。[(ref: main §4.3)](https://arxiv.org/html/2611.28576v1#S4.SS3) [(ref: main Table S18)](https://arxiv.org/html/2611.28576v1#A11.T18)
- **決定能改變內容，不只長度** — 相對 length control，CLASP 的 BLEU-3、ROUGE-L（+0.013）與關鍵字重疊較高、hallucination rate 較低（0.439 對 0.476）。不經解碼器、只把 CCD／CSP 的決定以規則套到檢索報告（刪掉未被 claim 的發現句、插入缺的 claim），陳述發現的 micro-F1 從 0.393 升到 0.500、臨床 macro-F1 從 0.306 升到 0.335，增益集中在切片看得到的組織型態（macro-F1 0.35 → 0.49）。[(ref: main §4.3)](https://arxiv.org/html/2611.28576v1#S4.SS3) [(ref: main Table S10)](https://arxiv.org/html/2611.28576v1#A6.T10) [(ref: main Table S11)](https://arxiv.org/html/2611.28576v1#A6.T11)
- **為 n-gram 最佳化會增加矛盾** — CLASP 的臨床 macro-F1 0.328 高於 CLASP-Base 的 0.293（p = 0.009），但 contradiction rate 從 CLASP CE 的 0.185 升到 0.232，增量 +0.047（95% CI 0.021–0.072）來自 SAST：它讓模型在 95% 的報告寫淋巴結狀態（參考報告 80%）、67% 寫受體狀態（參考 35–39%），而切片預測淋巴結轉移的 AUC 只有 0.69。CLASP 在 92 份測試報告中有 67 份同時寫了左右兩側乳房（參考 12 份），因為寫兩側總能命中參考的側別。[(ref: main §4.4)](https://arxiv.org/html/2611.28576v1#S4.SS4) [(ref: main Appendix C)](https://arxiv.org/html/2611.28576v1#A3)
- **拿掉受體狀態，矛盾降到 0.130** — explicit abstention 把 contradiction rate 從 0.232 降到 0.130（差異 95% CI −0.121 到 −0.082），比 CLASP-Base 少 23%，BLEU-4 0.1265 仍高於 CLASP-Base；代價是正確的受體陳述也沒了（macro-F1 0.222），且仍高於很少寫受體的 MI-Gen（0.108）。即使 plan 中沒有受體句型，解碼器仍約每份報告寫一句受體，要靠解碼後刪除才擋得住；淋巴結狀態也會寫在其他句型裡，整句刪除只把它的矛盾率從 0.46 降到 0.39。[(ref: main §4.4)](https://arxiv.org/html/2611.28576v1#S4.SS4) [(ref: main Appendix D)](https://arxiv.org/html/2611.28576v1#A4)
- **決定可以交給 7B LLM** — 把 CLASP 的 plan、每句的發現與長度以文字放進 TITAN＋LLM 的 prompt，陳述發現的 macro-F1 從 0.13 升到 0.32、臨床 macro-F1 從 0.175 升到 0.324；改給 5 份最相似報告的原文，臨床 macro-F1 也到 0.310（與給決定的差異不顯著），但發現與組織型態較差。兩種作法的矛盾率都上升（0.210、0.193）。[(ref: main §4.5)](https://arxiv.org/html/2611.28576v1#S4.SS5) [(ref: main Table S19)](https://arxiv.org/html/2611.28576v1#A11.T19)
- **元件消融** — ESP 帶來重疊分數的主要增益（BLEU-4 0.111 → 0.142）；CCD＋CSP 讓 CRQS 0.244 → 0.280（p = 0.018），BLEU-4 不變；只給 claim 集合而不放進句子（CCD 無 CSP）時 BLEU-4 降到 0.135、臨床 macro-F1 降到 0.289。[(ref: main §4.5)](https://arxiv.org/html/2611.28576v1#S4.SS5)
- **與已發表結果持平** — 與 RANGER 引用值相比，BLEU-2、BLEU-3 三個種子都較高（BLEU-3 p = 0.02），BLEU-1、BLEU-4、ROUGE-L 持平，METEOR 低 0.015；依事先登錄規則選出的 EMA 變體 BLEU-4 0.1445，但臨床 macro-F1 降到 0.279。[(ref: main §4.3)](https://arxiv.org/html/2611.28576v1#S4.SS3) [(ref: main Appendix L)](https://arxiv.org/html/2611.28576v1#A12)
- **肺腺癌泛化** — 在與 BRCA 醫院不重疊的 PathText-LUAD 上沿用所有設定，BLEU-4 從 CLASP-Base 的 0.097 升到 0.128（+0.031，95% CI 0.022–0.038），陳述發現的 F1 不變（−0.010，CI −0.051 到 0.031）。[(ref: main §4.3)](https://arxiv.org/html/2611.28576v1#S4.SS3) [(ref: main Appendix I)](https://arxiv.org/html/2611.28576v1#A9)

## 限制

- **測試集小、只有一個基準家族** — 作者自陳只評估同一基準家族的兩個器官，測試集為 92 與 44 位病人；論文表 S4 中 BLEU-4 的病人 bootstrap 區間寬達 0.128–0.154，涵蓋 BiGen 與 RANGER 的引用值。[(ref: main §5)](https://arxiv.org/html/2611.28576v1#S5) [(ref: main Table S4)](https://arxiv.org/html/2611.28576v1#A2.T4)
- **臨床評估不是病理師** — 「與臨床紀錄一致」由 8B LLM 讀報告後作答，讀者本身對參考報告的一致率只有 76–95%；參考報告自己的 macro-F1 只有 0.515，是這個評估的上限。TCGA 紀錄是摘錄後的結構化資料，與自由文字報告不一致的部分無法分給讀者錯誤或紀錄差異。[(ref: main Appendix C)](https://arxiv.org/html/2611.28576v1#A3) [(ref: main Table S6)](https://arxiv.org/html/2611.28576v1#A3.T6)
- **主指標仍是 BLEU** — checkpoint 選擇、SAST 的 reward 與主要比較都以 BLEU 類指標為準，而論文自己顯示這些指標偏好醫院格式與長度、且 SAST 會增加矛盾；EMA 變體 BLEU-4 更高、臨床 macro-F1 更低，顯示兩類目標在這個資料上會互相拉扯。[(ref: main §4.2)](https://arxiv.org/html/2611.28576v1#S4.SS2) [(ref: main Appendix L)](https://arxiv.org/html/2611.28576v1#A12)
- **基線不完整** — RANGER 與 BiGen 無法在相同協定下重訓，MI-Gen 與 HistGen 只跑一個種子；SCOUT 的公開切分把 75 位本研究測試病人放在訓練集，作者沒有重訓。[(ref: main §5)](https://arxiv.org/html/2611.28576v1#S5) [(ref: main Appendix J)](https://arxiv.org/html/2611.28576v1#A10)
- **abstention 只是句子層級** — 變項如果寫在別的句型裡就擋不住（淋巴結），作者認為完整的放棄陳述需要陳述層級的實作；要放棄哪些變項由臨床定義人工指定。[(ref: main Appendix D)](https://arxiv.org/html/2611.28576v1#A4)
- **發現標籤是 silver** — 切片分類器的 20 個訓練標籤由規則式抽取器從報告抽出，沒有病理師核對；作者在未來方向中列出 pathologist-verified findings。[(ref: main Appendix H)](https://arxiv.org/html/2611.28576v1#A8) [(ref: main §5)](https://arxiv.org/html/2611.28576v1#S5)

## 與書庫其他文章的關係

REG 2025 從競賽結果指出病理報告生成的榜單分數抓不到數值與分級失真；CLASP 在 PathText-BRCA 上進一步量出 BLEU 主要獎勵醫院格式與報告長度，並把 REG 2025 的排名分數列為附錄評估之一: [REG 2025：報告生成分數上去了，腫瘤比例與分級仍會失真](2026-09-16-reg-2025-pathology-report-generation.md)

DeCAD 讓 CT 報告模型在寫報告前先輸出陽性發現清單，CLASP 在病理全切片上更進一步，在解碼前同時決定句子結構、長度、發現與每個發現放在哪一句；兩篇都顯示「先決定要寫什麼」能提高以標籤計的報告正確性: [CT 報告模型問得出卻寫不出：先列發現再寫，F1 15.9→39.0](2026-11-26-decad-ct-diagnosis-to-report-gap.md)

該研究在問答端發現 SlideChat 拿掉切片後答對率幾乎不變，CLASP 則在報告端發現不給影像的 7B LLM 對所有病人寫同一份報告、BLEU-4 仍與看得到切片的 LLM 相當，並查出 SlideChat 與 WSI-LLaVA 的訓練資料含 PathText-BRCA 的測試報告: [語言替病理 VLM 加了什麼？拿掉切片，答對率只掉 0.4 個百分點](2026-11-04-pathology-vlm-language-controlled-probes.md)

PathXAI 以「全答存在」的常數控制顯示病理報告的 finding F1 會被輕易超過，CLASP 則以「每份報告都寫最常見四個發現」與不經學習的醫院共識報告做同類控制，兩篇都說明病理報告的自動分數需要不靠影像的對照組: [PathXAI：公開集 finding F1 48.8，全答「有」得 86.3](2026-11-10-pathxai-segmentation-guided-pathology-report.md)

## 實務的啟發

- **評估病理報告生成時先放三個不學習的對照** — 同院報告共識、最相似訓練報告，以及「每份都寫最常見發現」；在 PathText-BRCA 上，前者的 BLEU-4 已與已發表方法相當，後者的發現 F1 與受訓模型差不多。沒有贏過這些對照的分數，很難解讀成模型讀懂了切片。[(ref: main §3.1)](https://arxiv.org/html/2611.28576v1#S3.SS1) [(ref: main Table 1)](https://arxiv.org/html/2611.28576v1#S4.T1)
- **使用公開切片 LLM 的分數前先查測試集重疊** — 論文顯示 SlideChat 與 WSI-LLaVA 的訓練資料已含 PathText-BRCA 大部分或全部測試病人的報告；以 TCGA 衍生資料評估的任何模型，都應先以病人代碼比對訓練資料。[(ref: main Table S17)](https://arxiv.org/html/2611.28576v1#A11.T17)
- **可借用的設計** — 把結構、長度與發現在解碼前明確決定，讓這些決定可以檢查、覆寫，並能以文字交給較大的 LLM 解碼器；但本研究只在 92 位測試病人上、以 LLM 讀者評分，屬待更大規模與病理師評估驗證的作法。[(ref: main §4.5)](https://arxiv.org/html/2611.28576v1#S4.SS5)
- **待驗證的警訊** — 以 BLEU 類 reward 做序列訓練，會讓模型更常寫出切片無法支持的受體與淋巴結狀態，甚至同時寫兩側乳房以命中參考；若要對切片無法判定的變項放棄陳述，只在 plan 裡移除還不夠，必須在輸出端強制執行。[(ref: main §4.4)](https://arxiv.org/html/2611.28576v1#S4.SS4) [(ref: main Appendix D)](https://arxiv.org/html/2611.28576v1#A4)

## References

- `main` — Ziaullah Khan, Rashadul Islam Sumon, Md Ariful Islam Mozumder, Duc-Son Pham, Moon-Il Joo, Hee-Cheol Kim. *CLASP: Deciding Structure and Claims Before Decoding for Whole-Slide Pathology Report Generation*. arXiv:2611.28576v1, 2026. HTML：https://arxiv.org/html/2611.28576v1 ；用到的深鏈：[§1](https://arxiv.org/html/2611.28576v1#S1)、[§2](https://arxiv.org/html/2611.28576v1#S2)、[§3](https://arxiv.org/html/2611.28576v1#S3)、[§3.1](https://arxiv.org/html/2611.28576v1#S3.SS1)、[Figure 2](https://arxiv.org/html/2611.28576v1#S3.F2)、[Figure 3](https://arxiv.org/html/2611.28576v1#S3.F3)、[§3.3](https://arxiv.org/html/2611.28576v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.28576v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.28576v1#S3.SS5)、[§3.6](https://arxiv.org/html/2611.28576v1#S3.SS6)、[§3.7](https://arxiv.org/html/2611.28576v1#S3.SS7)、[§3.8](https://arxiv.org/html/2611.28576v1#S3.SS8)、[§4.1](https://arxiv.org/html/2611.28576v1#S4.SS1)、[§4.2](https://arxiv.org/html/2611.28576v1#S4.SS2)、[Table 1](https://arxiv.org/html/2611.28576v1#S4.T1)、[§4.3](https://arxiv.org/html/2611.28576v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.28576v1#S4.SS4)、[§4.5](https://arxiv.org/html/2611.28576v1#S4.SS5)、[§5](https://arxiv.org/html/2611.28576v1#S5)、[LLM Usage Statement](https://arxiv.org/html/2611.28576v1#Sx1)、[Appendix A](https://arxiv.org/html/2611.28576v1#A1)、[Table S1](https://arxiv.org/html/2611.28576v1#A1.T1)、[Appendix B](https://arxiv.org/html/2611.28576v1#A2)、[Table S4](https://arxiv.org/html/2611.28576v1#A2.T4)、[Appendix C](https://arxiv.org/html/2611.28576v1#A3)、[Table S5](https://arxiv.org/html/2611.28576v1#A3.T5)、[Table S6](https://arxiv.org/html/2611.28576v1#A3.T6)、[Appendix D](https://arxiv.org/html/2611.28576v1#A4)、[Table S8](https://arxiv.org/html/2611.28576v1#A4.T8)、[Appendix E](https://arxiv.org/html/2611.28576v1#A5)、[Table S10](https://arxiv.org/html/2611.28576v1#A6.T10)、[Table S11](https://arxiv.org/html/2611.28576v1#A6.T11)、[Appendix G](https://arxiv.org/html/2611.28576v1#A7)、[Appendix H](https://arxiv.org/html/2611.28576v1#A8)、[Table S14](https://arxiv.org/html/2611.28576v1#A8.T14)、[Table S15](https://arxiv.org/html/2611.28576v1#A8.T15)、[Appendix I](https://arxiv.org/html/2611.28576v1#A9)、[Table S16](https://arxiv.org/html/2611.28576v1#A9.T16)、[Appendix J](https://arxiv.org/html/2611.28576v1#A10)、[Appendix K](https://arxiv.org/html/2611.28576v1#A11)、[Table S17](https://arxiv.org/html/2611.28576v1#A11.T17)、[Table S18](https://arxiv.org/html/2611.28576v1#A11.T18)、[Table S19](https://arxiv.org/html/2611.28576v1#A11.T19)、[Appendix L](https://arxiv.org/html/2611.28576v1#A12)、[Appendix M](https://arxiv.org/html/2611.28576v1#A13)、[Appendix N](https://arxiv.org/html/2611.28576v1#A14)、[Table S23](https://arxiv.org/html/2611.28576v1#A14.T23)
- `abstract` — arXiv abstract page, 2611.28576v1：https://arxiv.org/abs/2611.28576v1 （PDF：https://arxiv.org/pdf/2611.28576v1 ；DOI：https://doi.org/10.48550/arXiv.2611.28576）

[Home](../) · [AI Papers](./)
