---
parent: AI Papers
nav_order: 4
title: "語言替病理 VLM 加了什麼？拿掉切片，答對率只掉 0.4 個百分點"
catalog_id: "arxiv:2610.26805"
editors:
  - "Clare"
refs:
  main:
    title: "What Language Adds, and at What Cost: Four Controlled Probes of Pathology Vision-Language Models"
    url: "https://arxiv.org/abs/2610.26805v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 語言替病理 VLM 加了什麼？拿掉切片，答對率只掉 0.4 個百分點

## 來源

- 團隊：Wenhao Zhang、Yi Ping、Zirui Wang、Sheng Li（University of Virginia School of Data Science）與 Zhongliang Zhou（Merck & Co., Inc.）；arXiv 作者欄列這 5 位。論文的利益衝突聲明指出部分作者為 Merck Sharp & Dohme LLC 員工、可能持有 Merck 股票。[(ref: main title block)](https://arxiv.org/html/2610.26805v1) [(ref: main Competing interests)](https://arxiv.org/html/2610.26805v1#Sx3)
- 論文：*What Language Adds, and at What Cost: Four Controlled Probes of Pathology Vision-Language Models*，arXiv:2610.26805v1（cs.CV；另列 q-bio.QM），2026-10-19 提交，目前只有 v1；授權為 CC BY 4.0；預印本，未經同儕審查。[(ref: abstract)](https://arxiv.org/abs/2610.26805v1)
- 識別碼：arXiv [2610.26805](https://arxiv.org/abs/2610.26805v1)；DOI [10.48550/arXiv.2610.26805](https://doi.org/10.48550/arXiv.2610.26805)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2610.26805v1)、[PDF v1](https://arxiv.org/pdf/2610.26805v1)。
- 程式與資料：所有資料（TCGA 切片與臨床終點、SlideChat 公開釋出的報告文字與 VQA 題目）與模型權重都是公開釋出；論文沒有提供這四組實驗的程式碼，只附一份病理 VLM 清單的 GitHub 連結。[(ref: main Data and code availability)](https://arxiv.org/html/2610.26805v1#Sx1)
- 研究性質：獨立稽核（evaluation），不是新模型；作者重用已釋出的權重與公開資料，每次只改變一個輸入，沒有訓練或微調任何模型。不是 pilot：存活分析 1,633 位病人、分型 930＋718 張切片、VQA 1,227 題，全部附 1,000 次 bootstrap 的 95% 信賴區間。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3)
- 證據邊界：本文數值只引用論文正文與摘要寫出的數字；論文的結果主要畫在 Fig. 1–2，沒有數值結果表，圖上各組的點估計本文不從圖面讀數引述。論文另有數處引用作者「companion review（51 個病理 VLM）」，該文獻在參考文獻中沒有出處連結，本文對這部分只轉述、不當成已查證的事實。[(ref: main §1)](https://arxiv.org/html/2610.26805v1#S1) [(ref: main Fig. 1)](https://arxiv.org/html/2610.26805v1#S4.F1) [(ref: main Fig. 2)](https://arxiv.org/html/2610.26805v1#S4.F2)

**編輯：** Clare

作者用四組「一次只改一個輸入」的控制實驗檢驗病理 VLM 的語言成分：病理報告文字確實帶有切片以外的預後訊號，但推論時的 prompt 沒有比監督式線性探測更準，切片層級的問答幾乎不看切片，換個說法又會讓 8–23% 的答案改變。[(ref: main Abstract)](https://arxiv.org/html/2610.26805v1)

## 流程

![四組控制實驗的設計示意圖，標題為 Four controlled probes of pathology VLMs (one input varied at a time)。最上方灰色長方框「Shared harness」寫著：Released checkpoints and public data, used without modification; no model is trained or fine-tuned；Representation frozen, predictor and evaluation split held fixed；Encoder probes: patient- and tissue-source-site-disjoint five-fold splits。灰框以四支向下箭頭連到並排的四個方框。左起第一個淺藍色框「Probe 1 Survival」：TCGA-BRCA / -LUAD / -COAD；n = 1,633 (394 PFI, 345 OS events)；Frozen TITAN slide embedding + frozen PubMedBERT report embedding -> L2-penalised linear Cox model；Arms: A vision; B + full report; B' + stage-redacted report; C stage + grade; T_full, T_red text；Metric: pooled out-of-fold Harrell's C-index。第二個淺綠色框「Probe 2 Subtyping」：TCGA NSCLC (N = 930)；TCGA RCC (N = 718)；Encoders: CONCH v1, CONCH v1.5, TITAN (language-aligned); Prov-GigaPath (pure vision) -> L2-penalised logistic head；Within CONCH v1: zero-shot (top-k or mean pooling) vs. supervised linear probes；Metric: balanced accuracy。第三個淺橘色框「Probe 3 Grounding」：SlideBench-VQA (TCGA)；1,227 multiple-choice items；SlideChat, WSI-LLaVA; text-only Qwen2.5-7B-Instruct, Qwen3-8B；P0 unperturbed vs. slide removed, features zeroed, mismatched slide, options shifted, correct option -> "none of the above"；Metric: accuracy。第四個淡紫色框「Probe 4 Wording」：SlideBench-VQA (TCGA + BCNB) matched multiple-choice subset；SlideChat, Qwen3-VL, InternVL3, text-only Qwen3；Canonical item vs. banks of paraphrases, prompt reframings (framing sentence / persona line), and both；Metrics: accuracy change, answer-flip rate, consistency。四個框各以一支向下箭頭連到最下方白色長方框「Statistics」：95% confidence intervals from 1,000 bootstrap resamples at a fixed seed (cases in Probes 1-2, questions in Probes 3-4); an effect is called significant when its interval excludes zero。](assets/pathology-vlm-four-probes-design.png)

圖：本書庫依論文 §3 的文字重繪的實驗設計示意圖，只含設定與樣本數，不含結果數值，未複製論文原圖（論文 Fig. 1–2 為結果圖）。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3)

## 背景／問題

病理 VLM 把組織影像編碼器接上文字編碼器或大型語言模型，讓同一個系統可以依 prompt 分類、檢索相似病例、回答自由文字問題或起草報告。作者提出的問題是：語言到底讓病理 AI 變得更好，還是只是更有說服力？因為純視覺模型在一些窄任務上已經相當準，而自由文字可能寫出組織上沒有的發現、流暢的理由可能被當成證據，答案又可能隨問法改變。[(ref: main §1)](https://arxiv.org/html/2610.26805v1#S1)

作者主張既有的發表結果無法回答這個問題，理由有三：幾乎每個系統都由開發團隊在自選的測試集與協定上評估；最常用的 patch 層級基準（PathMMU、PathVQA、Quilt-VQA）的影像取自文獻、教科書、教學影片與社群媒體，這些來源也會出現在預訓練語料裡，題目又多由半自動或語言模型輔助產生；切片層級基準多半與被評估助理的指令微調資料共用 TCGA 來源。第一點的依據是作者自己對 51 個病理 VLM 的 companion review，論文沒有提供該文的出處，本文只能把它記為作者的判斷。[(ref: main §1)](https://arxiv.org/html/2610.26805v1#S1) [(ref: main §2)](https://arxiv.org/html/2610.26805v1#S2)

為此作者把證據分三級：多個系統在同一協定下的獨立再評估（tier 1）、第三方對單一系統的重現（tier 2）、系統對自己的報告數字（tier 3），並把自己的四組實驗定位為 tier 1 證據。[(ref: main §2)](https://arxiv.org/html/2610.26805v1#S2)

## 方法摘要

**共同設計。** 四組實驗都凍結表徵、固定預測器與評估切分，每次只改變一個輸入；模型都是公開釋出的權重、不做修改，對話式助理用原作者的推論程式執行。編碼器實驗用病人與 tissue source site 都不重疊的五折切分，避免站點特徵跨折洩漏；VQA 實驗則是對已釋出題目的純推論。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3)

**四個問題。**

- **Probe 1 survival** — 報告文字能否在切片之外增加預後訊號，而且這個增益是不是只是報告裡寫的腫瘤分期？
- **Probe 2 subtyping** — 語言對齊的編碼器在分型上是否較好？推論時用 prompt 做 zero-shot，是否比在同樣特徵上訓練一個監督式線性分類器更準？
- **Probe 3 grounding** — 切片層級的 VQA 答案是否依賴切片本身？
- **Probe 4 wording** — 語意相同的改寫會不會改變答案？

[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3)

**統計。** 所有區間都是固定 seed、1,000 次 bootstrap 的 95% 信賴區間：Probe 1–2 以病例重抽、Probe 3–4 以題目重抽；區間不含 0 才稱為顯著。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3)

最後，作者把實驗沒涵蓋的兩類主張（agentic navigation 與 MIL 中的 few-shot language prior）依 companion review 收錄的文獻數字分級評估，本身不重新跑。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3) [(ref: main §4.5)](https://arxiv.org/html/2610.26805v1#S4.SS5)

## 方法詳解

**Probe 1 — 存活。** TCGA-BRCA、-LUAD、-COAD 的切片配上 TCGA Clinical Data Resource 的 progression-free interval（PFI）與 overall survival（OS）。報告文字取自 SlideChat 公開釋出的 SlideInstruct／SlideBench-Caption 報告衍生文字，並濾掉追蹤與結局相關的句子。凍結的 PubMedBERT 報告嵌入與凍結的 TITAN 切片嵌入串接後，配一個 L2 懲罰的線性 Cox 模型。六個組別只差在輸入：

| Arm | 輸入 |
|---|---|
| A | 切片嵌入（vision） |
| B | 切片＋完整報告 |
| B′ | 切片＋去除分期敘述的報告（stage-redacted） |
| C | 結構化分期與分級 |
| T_full | 只有完整報告文字 |
| T_red | 只有去除分期的報告文字 |

以 pooled out-of-fold Harrell's C-index 比較四個對比：clean language increment（B′ − A）、staging leakage（B − B′）、text-channel leakage（T_full − T_red）與 text versus vision（T_red − A）。[(ref: main §3 Probe 1)](https://arxiv.org/html/2610.26805v1#S3)

**Probe 2 — 分型。** TCGA NSCLC（LUAD vs. LUSC）與 RCC（KIRC、KIRP、KICH）切片分別由三個語言對齊的編碼器（CONCH v1、CONCH v1.5 與建立在其上的 TITAN 切片編碼器）與純視覺的 Prov-GigaPath 編碼成每張切片一個向量，再配 L2 懲罰的多項 logistic 分類頭，以 balanced accuracy 評分。在 CONCH v1 內部，另比較 zero-shot 分類（對 tile 做 top-k 或 mean pooling）與同一組特徵上的監督式線性探測。[(ref: main §3 Probe 2)](https://arxiv.org/html/2610.26805v1#S3)

**Probe 3 — 是否看切片。** SlideChat 與 WSI-LLaVA，加上兩個只吃文字的模型 Qwen2.5-7B-Instruct（SlideChat 的語言骨幹）與 Qwen3-8B，回答 SlideBench-VQA(TCGA) 中切片能在本地重新編碼（CLAM 切 tile、CONCH 特徵）的 1,227 題選擇題。相對於未擾動條件（P0），分別拿掉切片、把特徵歸零、換成不相符的切片、循環移動選項位置，或把正確選項換成「none of the above」（NOTA）。答案由同一個確定性 parser 讀取；永遠選最常見字母的基準為 40.7%。[(ref: main §3 Probe 3)](https://arxiv.org/html/2610.26805v1#S3)

**Probe 4 — 換個說法。** SlideChat、Qwen3-VL、InternVL3 與只吃文字的 Qwen3 回答 SlideBench-VQA（TCGA 與 BCNB）的一個配對選擇題子集。切片、題目內容與正確答案固定，每題以原始問法，以及語意相同的改寫（paraphrase）、改變框架句或加一行 persona 的 prompt reframing、兩者兼具三組題庫提出；報告準確率變化（原始減擾動）、答案翻轉比例，以及各題庫內的答案一致性。[(ref: main §3 Probe 4)](https://arxiv.org/html/2610.26805v1#S3)

**運算。** 線性分類頭與 bootstrap 在 CPU 上執行；zero-shot 與多模態推論最多用兩張 NVIDIA H200 NVL GPU、bf16。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3)

- **論文未交代** — Probe 4 子集的題數、改寫與 reframing 題庫如何產生（人工或模型）及每題幾個版本，以及「consistency」的計算公式。
- **論文未交代** — Probe 2 zero-shot 的 prompt 模板與 top-k 的 k 值；Probe 1–2 線性模型的懲罰強度與選擇方式；報告去除分期敘述的具體規則。
- **論文未交代** — 四組實驗的程式碼沒有公開；各組別的 C-index 與 balanced accuracy 點估計只畫在圖上，正文只給對比差值。

## 資料與實驗

**資料。** 四組實驗使用的資料如下，全部為公開、去識別化資料，沒有收集新的人體資料。[(ref: main §3)](https://arxiv.org/html/2610.26805v1#S3) [(ref: main Data and code availability)](https://arxiv.org/html/2610.26805v1#Sx1)

| Probe | 資料 | 規模 | 模型 | 主要指標 |
|---|---|---|---|---|
| 1 Survival | TCGA-BRCA／-LUAD／-COAD 切片＋臨床終點；SlideChat 釋出的報告衍生文字 | pooled n = 1,633（394 個 PFI 事件、345 個 OS 事件） | TITAN（切片）、PubMedBERT（報告）＋線性 Cox | pooled out-of-fold Harrell's C-index |
| 2 Subtyping | TCGA NSCLC（LUAD／LUSC）、RCC（KIRC／KIRP／KICH） | N = 930、N = 718 | CONCH v1、CONCH v1.5、TITAN、Prov-GigaPath＋logistic head | balanced accuracy |
| 3 Grounding | SlideBench-VQA(TCGA) 選擇題 | 1,227 題 | SlideChat、WSI-LLaVA、Qwen2.5-7B-Instruct、Qwen3-8B | accuracy |
| 4 Wording | SlideBench-VQA（TCGA＋BCNB）配對選擇題子集 | 論文未列題數 | SlideChat、Qwen3-VL、InternVL3、Qwen3 | accuracy 變化、翻轉比例、consistency |

**病理 VLM 常用的公開基準。** 下表摘錄論文 Table 1（數量依各基準來源報告；Gran. 為粒度：G1 patch、G2 region of interest、G3 全切片；NR 為來源未報告；WSI-Bench 的數量含訓練集）。作者據此指出：多數比較依賴的三個 patch 層級基準有資料污染風險，切片層級基準則常與被評估助理的訓練資料同源於 TCGA。[(ref: main Table 1)](https://arxiv.org/html/2610.26805v1#S2.T1)

| Benchmark | Items | Questions | Gran. | Task type |
|---|---|---|---|---|
| PathMMU | 24,067 | 33,428 | G1 | MCQ diagnostic reasoning |
| PathVQA | 4,998 | 32,799 | G1 | Open- and closed-ended VQA |
| Quilt-VQA | 985 | 1,283 | G1 | Open- and closed-ended VQA |
| PathQABench-Public | TCGA subset | Expert-curated | G1/G2 | Diagnostic MCQ |
| PathMMU-HR2 | NR | 1,668 | G2 | VQA on 16,000² px regions |
| WSI-VQA | 977 WSIs | 8,672 | G3 | Slide-level VQA |
| WSI-Bench | 9,850 WSIs | 179,569 | G3 | VQA (3 × 11 task grid) |
| SlideBench-VQA (TCGA) | 732 patients | 7,827 | G3 | VQA (13 tasks) |
| SlideBench-VQA (BCNB) | 1,058 patients | 7,274 | G3 | VQA (zero-shot) |
| PathText | 9,009 pairs | — | G3 | WSI-to-text report generation |
| REG2025 | 10,494 pairs | — | G3 | Report generation, 7 organs |
| HEST-Bench | ST-paired WSIs | — | G2/G3 | Gene-expression prediction |
| PathGLS | NR | — | G1/G3 | Reference-free factuality |

**實驗結果的呈現方式。** 論文沒有數值結果表，四組實驗的結果畫在 Fig. 1（Probe 1–2）與 Fig. 2（Probe 3–4 與文獻自報數字），正文只寫出關鍵差值。下表整理正文與摘要明寫的數字，未在正文出現的圖上數值不列。[(ref: main Fig. 1)](https://arxiv.org/html/2610.26805v1#S4.F1) [(ref: main Fig. 2)](https://arxiv.org/html/2610.26805v1#S4.F2)

| Probe | 比較 | 正文報告的結果 |
|---|---|---|
| 1 | B′ − A（clean language increment） | 六個癌別×終點組合皆為正且顯著；pooled PFI +0.019、OS +0.016 C-index |
| 1 | B − B′、T_full − T_red（兩個 leakage 對比） | 皆為 null |
| 1 | T_red vs. A；arm C | 只有去分期報告至少與切片嵌入一樣具預後力；結構化分期與分級（C）最弱 |
| 2 | 三個語言對齊編碼器 vs. Prov-GigaPath（同一監督式探測） | 兩項任務皆較高 |
| 2 | CONCH v1 mean-pooled zero-shot − 線性探測 | NSCLC −0.020、RCC −0.019 balanced accuracy，皆不顯著 |
| 3 | SlideChat 有切片 vs. 拿掉切片 | 74.82% vs. 74.41%；拿掉與換錯切片的差皆與 0 無法區分 |
| 3 | Qwen2.5-7B（只有文字）；最常見字母基準 | 43.52%；40.7% |
| 4 | 只做改寫 | 四個系統準確率變化皆不顯著；8–23% 的題目答案改變 |
| 4 | 改寫＋reframing | 25% 的題目答案改變，consistency 降到 0.57 |

[(ref: main §4.1)](https://arxiv.org/html/2610.26805v1#S4.SS1) [(ref: main §4.2)](https://arxiv.org/html/2610.26805v1#S4.SS2) [(ref: main §4.3)](https://arxiv.org/html/2610.26805v1#S4.SS3) [(ref: main §4.4)](https://arxiv.org/html/2610.26805v1#S4.SS4)

## 結果

- **報告文字帶來切片以外的預後訊號** — 把去分期報告的凍結嵌入加到切片嵌入上，C-index 在六個癌別×終點組合都顯著上升，pooled 為 PFI +0.019、OS +0.016；兩個 leakage 對比都是 null，只用去分期報告就至少和切片嵌入一樣具預後力，結構化分期與分級反而最弱。作者的解讀是增益不是在重述分期，而是報告中與切片互補的資訊，而且是由凍結的文字編碼器、而不是 VLM 取得的；作者也提醒去分期後，腫瘤大小這類與分期相關的發現仍留在報告裡。[(ref: main §4.1)](https://arxiv.org/html/2610.26805v1#S4.SS1)
- **語言的貢獻在預訓練特徵，不在推論時的 prompt** — 在相同的監督式探測下，三個語言對齊編碼器在兩項分型任務都勝過 Prov-GigaPath；但作者強調這些編碼器在骨幹、資料、維度與聚合方式上都不同，差距不能歸因於語言。真正隔離 prompt 的是 CONCH v1 內部比較：特徵與 pooling 固定時，zero-shot 與線性探測的差（NSCLC −0.020、RCC −0.019）都不顯著；top-k zero-shot 分數較高，但在共用 pooling 後差距消失，作者認為那是 instance selection 的效果。[(ref: main §4.2)](https://arxiv.org/html/2610.26805v1#S4.SS2)
- **切片層級 VQA 幾乎不依賴切片** — SlideChat 有切片答對 74.82%，拿掉切片 74.41%，拿掉與換錯切片的差都與 0 無法區分，連分級與分期題也一樣；WSI-LLaVA 少了幾個百分點，差距顯著。SlideChat 的語言骨幹 Qwen2.5-7B 不看切片只答對 43.52%，接近 40.7% 的最常見字母基準，作者據此推算約 31 個百分點來自指令微調資料的規律，而不是切片。兩個助理反而對答案格式敏感：移動選項位置顯著降低準確率，把正確選項換成 NOTA 會讓 SlideChat 跌破字母基準。[(ref: main §4.3)](https://arxiv.org/html/2610.26805v1#S4.SS3)
- **換個說法，準確率不變但答案會變** — 只做改寫時四個系統的準確率變化都不顯著，但 8–23% 的題目答案改變；改寫加 reframing 時 25% 的題目答案改變、consistency 降到 0.57。最穩定的 SlideChat 在只改框架句時也改了四分之一的答案；加一行 persona 讓 Qwen3-VL 的準確率顯著改變，是整組實驗中唯一區間不含 0 的準確率變化。[(ref: main §4.4)](https://arxiv.org/html/2610.26805v1#S4.SS4)
- **自報的增益還無法歸因於語言** — 這部分是作者對文獻數字的分級，不是重新實驗：CPathAgent 在 PathMMU-HR2 報告 88.6%，比單次作答的 Gemini-2.5-Pro 高 15.4 點，但在切片層級平均只領先 ABMIL 2.9 點、在 CPTAC-Lung 落後 TITAN（88.1% vs. 91.9%），而 Gemini-2.5-Pro 被提示以同樣方式瀏覽時也從 73.2% 升到 76.4%；MIL 中的 few-shot language prior（ViLa-MIL、VLEER、GMAT）報告較小而一致的增益，例如 ViLa-MIL 以 16-shot 對 CLAM-MB 多 1.7 與 5.9 AUC 點。這些數字都來自提出方法的論文本身：navigation 沒有區間或 seed，無法拆開兩個成分；language prior 沒有獨立或控制洩漏的重現，作者評為 weakly supported。[(ref: main §4.5)](https://arxiv.org/html/2610.26805v1#S4.SS5)

## 限制

作者自述的限制：[(ref: main §5 Limitations)](https://arxiv.org/html/2610.26805v1#S5)

- **範圍有限** — 只測 TCGA 衍生資料上的公開權重：兩個切片層級助理、三個語言對齊編碼器與一個純視覺編碼器；reasoning-tuned、agentic 與 MIL 系統沒有直接實驗。
- **Probe 1 的 null 可能另有解釋** — 若凍結的文字編碼器本身對分期敘述不敏感，leakage 對比也會是 null；沒有「切片＋結構化分期分級」的組別；報告文字是經過處理的釋出版本。
- **Probe 2 的跨編碼器比較有混淆** — zero-shot 與監督式分類頭只在 mean pooling 下比較，沒有 attention-based MIL 這類學習式 instance selection。
- **Probe 3–4 只用選擇題** — 自由文字生成可能有不同表現；navigation 與 few-shot 的分級只依文獻自報數字。

本書庫另外注意到：

- **TCGA 內部、沒有外部資料** — 四組實驗都在 TCGA 與其衍生的 SlideBench 上，作者自己就指出切片層級基準與助理的訓練資料同源；這讓 Probe 3 的「不看切片也答得對」更像是在量訓練資料的規律，換到不同來源的切片與題目時，差距大小可能不同。[(ref: main §2)](https://arxiv.org/html/2610.26805v1#S2)
- **部分論點依賴未公開的 companion review** — 「幾乎每個系統都自評」「51 個系統沒有一個報告校準後的信心」等敘述來自作者另一篇沒有出處的回顧，本文無法核對。[(ref: main §5)](https://arxiv.org/html/2610.26805v1#S5)
- **利益衝突** — 部分作者為 Merck 員工；本篇不評估任何 Merck 產品，但讀者可自行納入判斷。[(ref: main Competing interests)](https://arxiv.org/html/2610.26805v1#Sx3)
- **重現資訊不足** — 程式碼未公開，Probe 4 的題庫產生方式與題數、zero-shot prompt 等細節未交代（見方法詳解）。

## 與書庫其他文章的關係

CONCH 論文以 zero-shot 分類展示病理圖文預訓練的遷移能力，本篇在 CONCH v1 的同一組特徵上把 zero-shot 與監督式線性探測放在相同 pooling 下比較，兩者差距不顯著，說明語言的價值主要留在特徵裡、不在推論時的 prompt: [CONCH：零樣本病理分類很強，多類腦瘤就露出邊界](2026-09-15-conch-pathology-vlm.md)

REG 2025 從報告生成端指出病理 VLM 的榜單分數抓不到數值幻覺，本篇則從問答端補上另一個評估盲點：切片層級 VQA 的分數可以幾乎不依賴切片，而 REG2025 本身也列在本篇整理的公開基準表中: [REG 2025：報告生成分數上去了，腫瘤比例與分級仍會失真](2026-09-16-reg-2025-pathology-report-generation.md)

ModaLens 在胸片加報告的情境下交換影像來量測醫療 VLM 是否仍看影像，本篇把同一類「拿掉或換掉影像」的對照搬到病理全切片問答，並加上選項位移、NOTA 與改寫三種格式對照: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎](2026-09-17-modalens-image-sensitivity.md)

MedVTok 以 VQA 準確率比較不同視覺 tokenizer、差距約 1 個百分點，本篇則顯示切片層級 VQA 拿掉切片後答對率幾乎不變，兩篇合讀提醒 VQA 分數差距未必全部來自影像表徵: [MedVTok：影像任務平均領先，接上 LLM 的 VQA 只多 1.1 分](2026-11-05-medvtok-unified-medical-visual-tokenizer.md)

## 實務的啟發

- **可借用的量測方法：作者提出的最低對照組** — 評估病理 VLM 時，作者建議至少報告：切片條件 VQA 的 text-only、換錯切片、選項位移與 NOTA 組別並附多數答案基準；改寫與 reframing 下的翻轉比例與一致性；主張文字改善預後時的去分期與只有文字組別；主張 prompt 有用時的同編碼器比較；每個主要比較的信賴區間與 seed；以及六項運算資訊。這些對照每一項的成本都不高，可直接加進內部評估流程。[(ref: main §5 Minimum controls)](https://arxiv.org/html/2610.26805v1#S5)
- **待驗證的警訊：選擇題準確率不代表模型讀了切片** — 本篇的結果是 SlideChat 在 TCGA 衍生題目上不看切片也答得一樣好；在自己的題目上，先跑一次「拿掉影像」與「只用語言骨幹」的對照，再決定要不要相信一個 VQA 分數。[(ref: main §4.3)](https://arxiv.org/html/2610.26805v1#S4.SS3)
- **分類任務不一定需要 prompt** — 在 CONCH v1 上 zero-shot 與線性探測差距不顯著，作者因此認為有標註資料時可以用監督式分類器取代 prompt，避開 prompt 敏感度；這是兩個 TCGA 分型任務的結果，換任務時仍需重測。[(ref: main §4.2)](https://arxiv.org/html/2610.26805v1#S4.SS2)
- **報告文字是值得保留的輸入** — 存活預測的增益來自凍結的文字編碼器而非 VLM，幅度為 C-index +0.016–0.019；這支持在預後模型中把報告文字當成獨立輸入，但增益不大，且尚未在 TCGA 以外驗證。[(ref: main §4.1)](https://arxiv.org/html/2610.26805v1#S4.SS1)

## References

- **main** — Zhang W, Zhou Z, Ping Y, Wang Z, Li S. *What Language Adds, and at What Cost: Four Controlled Probes of Pathology Vision-Language Models*. arXiv:2610.26805v1, 2026. [abstract](https://arxiv.org/abs/2610.26805v1)；[HTML v1](https://arxiv.org/html/2610.26805v1)；[PDF v1](https://arxiv.org/pdf/2610.26805v1)；DOI [10.48550/arXiv.2610.26805](https://doi.org/10.48550/arXiv.2610.26805)
  - 深鏈：[§1](https://arxiv.org/html/2610.26805v1#S1)、[§2](https://arxiv.org/html/2610.26805v1#S2)、[Table 1](https://arxiv.org/html/2610.26805v1#S2.T1)、[§3](https://arxiv.org/html/2610.26805v1#S3)、[Fig. 1](https://arxiv.org/html/2610.26805v1#S4.F1)、[§4.1](https://arxiv.org/html/2610.26805v1#S4.SS1)、[§4.2](https://arxiv.org/html/2610.26805v1#S4.SS2)、[Fig. 2](https://arxiv.org/html/2610.26805v1#S4.F2)、[§4.3](https://arxiv.org/html/2610.26805v1#S4.SS3)、[§4.4](https://arxiv.org/html/2610.26805v1#S4.SS4)、[§4.5](https://arxiv.org/html/2610.26805v1#S4.SS5)、[§5](https://arxiv.org/html/2610.26805v1#S5)、[Data and code availability](https://arxiv.org/html/2610.26805v1#Sx1)、[Competing interests](https://arxiv.org/html/2610.26805v1#Sx3)

[Home](../) · [AI Papers](./)
