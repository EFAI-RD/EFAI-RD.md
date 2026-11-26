---
parent: AI Papers
nav_exclude: true
title: "胸片報告對照分類器分數：1.5B 模型 98.5%，規則 80.5%"
catalog_id: "arxiv:2611.26492"
editors:
  - "Clare"
refs:
  main:
    title: "Multimodal Error Detection in Chest X-ray Reports: A Large Language Model Reading Image Evidence"
    url: "https://arxiv.org/html/2611.26492v1"
  abs:
    title: "arXiv abstract page: 2611.26492v1"
    url: "https://arxiv.org/abs/2611.26492v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 胸片報告對照分類器分數：1.5B 模型 98.5%，規則 80.5%

## 來源

- 團隊：Yanda Cheng（Cornell University, Meinig School of Biomedical Engineering；通訊作者）、Bo Wen（University of Rochester, Department of Electrical and Computer Engineering）、Yuhao Lu（Cornell University, School of Electrical and Computer Engineering）。論文聲明無外部經費、無利益衝突。[(ref: main author block)](https://arxiv.org/html/2611.26492v1) [(ref: main Funding and Competing Interests)](https://arxiv.org/html/2611.26492v1#Sx3)
- 論文：*Multimodal Error Detection in Chest X-ray Reports: A Large Language Model Reading Image Evidence*，arXiv:2611.26492v1（cs.CL），2026-11-19 提交，目前只有 v1；arXiv 註記「34 pages, 4 figures, including supplementary material」，未註記發表場合；授權為 arXiv 非專屬散布授權（nonexclusive-distrib 1.0）。[(ref: abstract)](https://arxiv.org/abs/2611.26492v1)
- 識別碼：arXiv [2611.26492](https://arxiv.org/abs/2611.26492v1)；DOI [10.48550/arXiv.2611.26492](https://doi.org/10.48550/arXiv.2611.26492)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.26492v1)、[PDF v1](https://arxiv.org/pdf/2611.26492v1)。
- 程式與資料：資料為公開、去識別的 Indiana University Chest X-Ray Collection（OpenI）。論文寫明 quad 建構程式、每個 quad 的 OpenI 報告與影像識別碼、reference labeler 與 rule baseline、prompts、訓練與評估程式（含分析計畫修訂紀錄）與 LoRA adapters「將會釋出」於 GitHub `Nickcp39/rad_linter`。[(ref: main Data and Code Availability)](https://arxiv.org/html/2611.26492v1#Sx1)
- 研究性質：方法比較研究，核心模型實際訓練與執行，不是 pilot 規模。主要測試 131 個 quad（524 組報告－分數配對），模型結果為三個訓練 seed 的平均 ± SD，規則基線附 cluster bootstrap 95% 區間。比較的「正確答案」由規則式 labeler 與分數門檻自動產生，沒有放射科醫師判讀；量到的是「報告與分類器分數是否一致」，不是臨床上確認的報告錯誤。[(ref: main §3.4)](https://arxiv.org/html/2611.26492v1#S3.SS4) [(ref: main Table 1)](https://arxiv.org/html/2611.26492v1#S4.T1) [(ref: main §6)](https://arxiv.org/html/2611.26492v1#S6)
- 證據邊界：本文數值以 arXiv v1 HTML 版的表 1、表 4、表 5、圖 3、圖 4 與正文為準；逐病灶（per-pathology）的完整結果只引用正文給出的範圍。

**編輯：** Clare

同一份胸片報告、同一組影像分類器分數交給兩個查核器：以 LoRA 微調的 Qwen2.5-1.5B 判斷「報告與分數是否一致」的 item accuracy 為 98.5%，關鍵字＋否定詞規則為 80.5%，差距集中在需要讀懂「可能」「無」等措辭的配對；分數高而報告未提及或否定的 Omission 類，兩者打平。[(ref: main Table 1)](https://arxiv.org/html/2611.26492v1#S4.T1) [(ref: main §4.1)](https://arxiv.org/html/2611.26492v1#S4.SS1)

## 流程

![左右兩欄圖。左欄標題「(a) Counterfactual quad：兩份報告 × 兩組他人分數」，上方兩欄標頭為「High 分數向量 目標 Atelectasis ≥ 0.6」與「Low 分數向量 目標 Atelectasis ≤ 0.2」，左側兩列標頭為「報告 A「No atelectasis.」」與「報告 B「Atelectasis is present.」」；中間是 2×2 的四個圓角方格，左上淺橘色「Inconsistent Omission」、右上淺綠色「Consistent No_Error」、左下淺綠色「Consistent No_Error」、右下淺橘色「Inconsistent Contradiction」；下方小字「只看報告或只看分數：每個輸入在一致與不一致各出現一次，固定答案最多答對一半（item 50%、quad 0%）」。右欄為水平長條圖，標題「(b) 粗略線索探針在 hard 子集掉到 56.3%」，橫軸「Item accuracy（%），primary test」刻度 40–100，四組系統由上而下為 Rad-Linter（三次訓練平均）98.8／98.3、Rule baseline 82.1／78.9、Coarse probe 94.0／56.3、Zero-shot 54.5／50.8；每組上方淺藍長條為 Easy（報告 A 未肯定任何發現，n=268），下方深藍長條為 Hard（報告 A 肯定了另一個發現，n=256）；50% 處有一條灰色虛線，標「單一輸入 50%」。](assets/rad-linter-quad-and-shortcut-check.png)

*圖：本書庫依論文圖 2 的設計重繪 counterfactual quad（左，以門檻值取代論文示意圖中的具體分數），右側數值取自論文圖 4 與 [Appendix C.3](https://arxiv.org/html/2611.26492v1#A3.SS3)。左圖淺橘方格為兩個不一致配對、淺綠方格為兩個一致配對；右圖每個系統的上方淺藍長條是 easy 子集、下方深藍長條是 hard 子集，灰色虛線為單一輸入的 50% 參考線。Coarse probe 的 easy 數值是論文由整體與 hard 子集結果推得。[(ref: main Figure 2)](https://arxiv.org/html/2611.26492v1#S3.F2) [(ref: main Figure 4)](https://arxiv.org/html/2611.26492v1#A3.F4)*

## 背景／問題

作者引用文獻指出，胸片報告是其他醫師使用影像發現的依據，報告中的錯誤可能影響後續決策；而有些錯誤只看文字找不到，例如報告完全沒提到影像上有的積水，句子之間並不會互相矛盾。[(ref: main §1)](https://arxiv.org/html/2611.26492v1#S1) 既有的文字型查核（關鍵字規則、神經網路、以及讓 LLM 找出人工插入報告文字的錯誤）適合處理在報告內留下線索的錯誤；要檢查「報告說的」與「影像顯示的」是否一致，需要另一個證據來源。[(ref: main §2)](https://arxiv.org/html/2611.26492v1#S2)

論文要回答的問題比「能不能抓到報告錯誤」窄：**在影像證據固定不變的前提下，讓訓練過的語言模型讀報告，是否比規則讀報告更能判斷報告與分類器分數一致與否。**作者也說明他們較早一版用人工插入錯誤的評估，只給報告文字的模型 F1 就達 90.5，無法證明查核器真的有比對影像證據，因此改設計成兩個輸入缺一不可的測試。[(ref: main §3.4)](https://arxiv.org/html/2611.26492v1#S3.SS4) [(ref: main Appendix C)](https://arxiv.org/html/2611.26492v1#A3)

## 方法摘要

- **兩階段查核** — 固定的 TorchXRayVision DenseNet-121 對九個發現（Atelectasis、Consolidation、Pneumothorax、Edema、Effusion、Pneumonia、Cardiomegaly、Nodule、Mass）各給一個分數；語言模型讀「分數 JSON＋原始報告」，輸出 `has_error`、`error_type`、`finding` 三個欄位。語言模型看的是分數，不是影像像素。[(ref: main §3.2)](https://arxiv.org/html/2611.26492v1#S3.SS2)
- **錯誤類型的約定** — 分數 ≥ 0.6 為 high、≤ 0.2 為 low。high 配上未提及或明確否定的發現記為 Omission；high 配上不確定措辭記為 Hedging；low 配上肯定的發現記為 Contradiction；其餘為 No_Error。作者強調這是測試約定，不是臨床規則，No_Error 也不代表報告在臨床上正確。[(ref: main §3.1)](https://arxiv.org/html/2611.26492v1#S3.SS1) [(ref: main Table 2)](https://arxiv.org/html/2611.26492v1#A1.T2)
- **Rad-Linter** — Qwen2.5-1.5B-Instruct 以 LoRA 在 454 個 quad（1,816 組配對）上微調 30 個 epoch，三個 seed 重複。[(ref: main §3.2)](https://arxiv.org/html/2611.26492v1#S3.SS2)
- **Rule baseline** — 依 NegEx 式局部線索，在關鍵字前後 50 個字元內找否定或不確定詞，使用同樣的門檻與輸出欄位。它與產生參考答案的 reference labeler 是兩套不同的實作。[(ref: main §3.3)](https://arxiv.org/html/2611.26492v1#S3.SS3) [(ref: main Appendix B.2)](https://arxiv.org/html/2611.26492v1#A2.SS2)
- **Counterfactual quad** — 報告不改動，只換配對的分數：對一個目標發現，報告 A 不肯定它、報告 B 肯定它，再從同一 split 的其他病人取一組 high、一組 low 分數向量，兩兩配成四組（兩組一致、兩組不一致）。每份報告與每組分數都在一致與不一致中各出現一次，所以只用單一輸入最多答對一半。[(ref: main §3.4)](https://arxiv.org/html/2611.26492v1#S3.SS4)
- **指標** — item accuracy 是逐組配對判斷一致／不一致的正確率；quad accuracy 要求一個 quad 的四組全對。[(ref: main §3.5)](https://arxiv.org/html/2611.26492v1#S3.SS5)

## 方法詳解

- **資料切分** — OpenI 的 3,599 份報告（每位病人一份，Findings＋Impression 合併）依病人分成 2,520 位訓練、1,079 位測試，所有配對都在各自的 split 內建構。[(ref: main §3.4)](https://arxiv.org/html/2611.26492v1#S3.SS4)
- **參考答案怎麼來** — reference labeler（程式中稱 textlib）以句子切分、關鍵字比對與 NegEx／NegBio 式否定範圍規則，為每個發現給出 affirmed／uncertain／negated／not mentioned 四種狀態，再與分數門檻組合成答案。另以 Mistral-Small-24B-Instruct-2501 作 agreement labeler，在同一套約定下獨立讀報告；primary test 只收九個發現的三分類狀態全部一致的報告。兩者全九項一致的比例為 74.8%，在 914 份至少肯定或保留一個發現的報告中為 53.7%。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.26492v1#A2.SS1) [(ref: main Appendix B.3)](https://arxiv.org/html/2611.26492v1#A2.SS3)
- **quad 的限制條件** — 兩組分數向量在其他八個發現上必須與兩份報告都一致，只讓目標發現可能不一致；每份報告 A 與每組 low 向量只用於一個 quad，high 向量最多重複用於三個 quad，因 primary test 不足 120 個 quad 而放寬到五個。[(ref: main Appendix C.1)](https://arxiv.org/html/2611.26492v1#A3.SS1)
- **捷徑檢查** — 若報告 A 什麼都沒肯定，「沒有肯定任何發現」加上「某個分數偏高」就可能猜出不一致。為此建構時一半的 Omission 搜尋優先選「肯定了另一個發現」的報告 A，形成 64 個 hard quad；並訓練一個只看七個粗略特徵（是否有肯定的發現、肯定數、是否有保留語氣、最大／最小分數、高於與低於門檻的數量）的 gradient-boosted coarse probe。另有只看報告的 LoRA 模型、未微調只看報告的模型、只看分數的 logistic regression，以及兩個輸入都給但未微調的 zero-shot 模型。[(ref: main §3.5)](https://arxiv.org/html/2611.26492v1#S3.SS5) [(ref: main Table 3)](https://arxiv.org/html/2611.26492v1#A3.T3)
- **訓練設定** — LoRA rank 16、α 32、dropout 0.05，加在每個 block 的 query、key、value、output、gate、up、down 投影；AdamW、learning rate 1e-4、cosine schedule、3% warm-up、bfloat16、有效 batch size 32、最長 1,024 tokens；保留最後一個 epoch 的模型；測試時 greedy decoding、最多 256 個新 token，無法解析的輸出算錯。seed 為 42、43、44。[(ref: main Appendix D.1)](https://arxiv.org/html/2611.26492v1#A4.SS1)
- **不確定性** — 共用報告或分數向量的 quad 串成相關群組（primary test 28 組、second test 34 組），以群組為單位 bootstrap 1,000 次，比較系統時使用同一批重抽樣。[(ref: main Appendix C.2)](https://arxiv.org/html/2611.26492v1#A3.SS2)
- **論文未交代** — 程式、quad 識別碼與 LoRA adapters 在論文中寫為「將會釋出」，本文未能核對其內容；訓練 recipe 是在初始 recipe 已對兩個測試集各評估過一次後才修改（初始 recipe 的 primary test item accuracy 為 51–59%），修改時用 45 個訓練 quad 的 development split 比較；輸入 prompt 要求五個欄位，但最終訓練目標只有三個欄位，作者保留這個不一致的設定；訓練與測試報告之間是否有相同措辭沒有檢查（3,599 份報告只有 2,842 種相異文字）；coarse probe 是在較早的 303 個 quad 上訓練，沒有計算信賴區間。[(ref: main §6)](https://arxiv.org/html/2611.26492v1#S6) [(ref: main Appendix D.2)](https://arxiv.org/html/2611.26492v1#A4.SS2) [(ref: main Appendix D.3)](https://arxiv.org/html/2611.26492v1#A4.SS3)

## 資料與實驗

### 資料

| 集合 | 篩選 | quad | 配對（item） | 組成 |
|---|---|---|---|---|
| 訓練 | textlib 標籤，不要求兩個 labeler 一致 | 454 | 1,816 | — |
| Primary test（test_main） | 1,079 位保留病人，兩個 labeler 全九項一致 | 131 | 524 | Omission 114（未提及 58、否定 56）、Hedging 17、Contradiction 131、一致 262；Cardiomegaly 55、Atelectasis 44、Effusion 16、Pneumonia 6、Nodule 5、Mass 3、Consolidation 2 個 quad |
| Second test（test_all） | 同一批保留病人，不要求一致 | 181 | 724 | Hedging 40 個 quad；另行建構，不是 primary test 的擴充 |

兩個測試集都沒有 Pneumothorax 的 quad，primary test 也沒有 Edema。[(ref: main Appendix A)](https://arxiv.org/html/2611.26492v1#A1) [(ref: main Appendix C.1)](https://arxiv.org/html/2611.26492v1#A3.SS1)

### 實驗：主要比較（論文表 1）

| Checker | Item accuracy (%) | Quad accuracy (%) |
|---|---|---|
| *Primary test：131 quads, 524 items* | | |
| Rad-Linter | 98.5 ± 0.2 | 94.4 ± 0.4 |
| Rule baseline | 80.5 [75.0, 86.6] | 56.5 [36.7, 64.3] |
| *Without agreement filter：181 quads, 724 items* | | |
| Rad-Linter | 93.4 ± 0.6 | 81.4 ± 2.1 |
| Rule baseline | 75.3 [73.1, 82.9] | 47.0 [37.2, 57.5] |

Rad-Linter 為三個 seed 的 mean ± SD；規則基線為 cluster bootstrap 95% 區間，兩者描述不同來源的變異。[(ref: main Table 1)](https://arxiv.org/html/2611.26492v1#S4.T1)

### 實驗：對照系統（論文表 4，primary test）

| Row | Input | Item acc. (%) | Quad acc. (%) | Hard items (%) |
|---|---|---|---|---|
| M, Rad-Linter | scores + report | 98.5 ± 0.2 | 94.4 ± 0.4 | 98.3 |
| B1, rule baseline | scores + report | 80.5 [75.0, 86.6] | 56.5 [36.7, 64.3] | 78.9 |
| Z, zero-shot | scores + report | 52.7 [48.3, 53.7] | 0.0 [0.0, 0.0] | 50.8 |
| G, coarse probe | scores + rule-labeler states | 75.6 | 42.7 | 56.3 |
| T | report only | 50.0 ± 0.0 | 0.0 ± 0.0 | 50.0 |
| B2 | report only | 50.0 | 0.0 | 50.0 |
| S | scores only | 50.0 | 0.0 | 50.0 |

Hard items 為 64 個 hard quad 的 256 組配對；隨機猜測的 quad accuracy 為 6.25%。[(ref: main Table 4)](https://arxiv.org/html/2611.26492v1#A3.T4)

## 結果

- **主要差距** — primary test 上 item accuracy 差約 18 個百分點、quad accuracy 差約 38 個百分點，三個 seed 都成立；各 seed 的 item 差距配對 bootstrap 區間為 [+13.4, +25.0]，quad 差距的區間落在 [+33.1, +63.3] 之內。作者說明這是測試集內的不確定性，不代表在新臨床族群的表現。[(ref: main §4.1)](https://arxiv.org/html/2611.26492v1#S4.SS1)
- **漏報與誤報都較少** — Rad-Linter 標出 97.7% 的不一致配對（規則 85.5%），一致配對中 99.4% 未被標記（規則 75.6%），即每次執行約 1–2 個誤報。各病灶等權平均為 94.5% 對 81.5%。[(ref: main §4.1)](https://arxiv.org/html/2611.26492v1#S4.SS1)
- **差距在哪裡** — Omission 兩者幾乎相同（Rad-Linter 97.4%、規則 98.2%）；規則在 Hedging 為 64.7%、Contradiction 為 77.1%、「肯定＋high 分數」的一致配對為 69.5%，與 Rad-Linter 的差距分別為 +33.3、+20.9、+29.7 個百分點，「未肯定＋low 分數」的一致配對差 +17.8 個百分點。作者認為這符合「較可靠地解讀報告措辭」，但沒有以獨立標註的語言分析拆解是哪一種語言現象。[(ref: main Figure 3)](https://arxiv.org/html/2611.26492v1#S4.F3) [(ref: main Appendix C.4)](https://arxiv.org/html/2611.26492v1#A3.SS4)
- **捷徑檢查** — 單一輸入的系統都是 50%／0%，符合設計。coarse probe 整體 75.6%，在 268 個 easy 配對上達 94.0%，到 256 個 hard 配對掉到 56.3%；Rad-Linter 在 easy 與 hard 分別為 98.8% 與 98.3%。作者的結論是這七個粗略特徵解釋不了 Rad-Linter 的表現，但這項檢查不能排除所有捷徑。[(ref: main §4.2)](https://arxiv.org/html/2611.26492v1#S4.SS2)
- **微調是必要的** — 同一個 Qwen2.5-1.5B 不經微調只有 52.7%，沒有任何 quad 全對；它標記了 262 組不一致中的 224 組，但也標記了 262 組一致中的 210 組。[(ref: main §4.2)](https://arxiv.org/html/2611.26492v1#S4.SS2)
- **不限 labeler 一致時** — second test 上兩者都下降（Rad-Linter item 約 −5、quad 約 −13 個百分點），差距仍約 18 與 34 個百分點；zero-shot 為 50.8%。兩個測試集的報告篩選與 Hedging 比例都不同，作者沒有歸因下降的原因。[(ref: main §4.3)](https://arxiv.org/html/2611.26492v1#S4.SS3) [(ref: main Table 5)](https://arxiv.org/html/2611.26492v1#A3.T5)
- **逐病灶** — 規則從 Effusion 的 65.6% 到 Mass 的 91.7%；模型從 Pneumonia 的 93.1% 到 Cardiomegaly 與 Mass 的 100%，唯一例外是只有 8 組配對的 Consolidation 為 75.0%。樣本少的病灶估計精度有限。[(ref: main Appendix C.4)](https://arxiv.org/html/2611.26492v1#A3.SS4)

## 限制

- **參考答案是自動產生的** — reference labeler 與 agreement labeler 都沒有對照臨床醫師判讀驗證，而且 agreement labeler 被要求使用 reference labeler 的約定，兩者一致不構成臨床真值；沒有比較 CheXbert、RadGraph 等其他 labeler。影像分類器的訓練資料本身包含 OpenI；分數臨床上錯時，查核器「正確地跟隨分數」仍會被算對。[(ref: main §6)](https://arxiv.org/html/2611.26492v1#S6)
- **測試涵蓋範圍窄** — 131 個 quad 只分屬 28 個相關群組，其中 99 個是 Cardiomegaly 或 Atelectasis；四個病灶少於十個 quad，Hedging 只有 17 組配對，沒有 Pneumothorax；目標發現只測 high 與 low 分數，中間分數沒有測。配對是跨病人人為組合，不是每張影像配自己的報告。[(ref: main §6)](https://arxiv.org/html/2611.26492v1#S6)
- **比較與訓練選擇有限** — 只測一種模型大小與一種規則基線，更大的 zero-shot 模型或更強的規則系統可能結果不同；論文的結論也不代表勝過產生答案的 reference labeler 本身，或勝過一般規則方法。訓練 recipe 是在看過一次測試結果後修改的，最終結果不是所有訓練選擇都事先固定的評估。[(ref: main §5)](https://arxiv.org/html/2611.26492v1#S5) [(ref: main §6)](https://arxiv.org/html/2611.26492v1#S6)
- **臨床效益未測** — 只用一種影像模態與一個報告集，沒有測量醫師是否因此少犯錯、病人照護是否改善，也沒有分族群評估；胸片分類器在某些病人族群漏診較多，這會直接影響查核器的旗標。[(ref: main §6)](https://arxiv.org/html/2611.26492v1#S6)

## 與書庫其他文章的關係

兩篇都碰到「沒提到算不算沒有」這個約定；該篇顯示查核模型對未提及的 checklist 發現採不同解讀時，強化學習量到的增益就跟著變，本篇則把未提及與明確否定一起歸入 Omission，且在這一類上規則與微調模型打平，差距只出現在需要解讀措辭的配對: [「沒提到」算不算「沒有」？換一個查核模型，增益就跟著變](2026-10-23-unmentioned-findings-rl-cxr-report-checking.md)

該篇的 LLM 只審閱報告文字內部是否有錯，作者明說無法發現報告與影像不符；本篇則把影像分類器分數當作外部證據交給查核器，補的正是「文字對影像」這一層，但答案改由自動 labeler 與分數門檻產生，沒有放射科醫師判讀: [14 萬份中文報告挑錯：Qwen3 recall 0.96，醫師最高 0.67](2026-11-02-llm-radiology-report-error-qa-multicenter.md)

兩篇都把影像分類器分數當作報告之外的證據；本篇讓微調小模型判斷胸片報告與分數是否一致、只發出旗標，該篇則在胸部 CT 上用學到的門檻規則決定何時依分數與量測修改報告，並顯示直接讓 LLM 依證據改寫反而降低報告品質: [CT 報告修訂規則庫：有影像證據 CE-F1 多 11.5，只看草稿學不到](2026-11-25-ct-report-rulebank-independent-evidence.md)

## 實務的啟發

- **可借用的量測方法** — counterfactual quad 讓「只看一個輸入」的系統必然停在 50%，再加上 hard 子集與粗略特徵探針檢查捷徑；任何宣稱「比對了影像與報告」的查核器或報告評估指標，都可以用同樣的配對設計確認它真的用到了兩個輸入。[(ref: main §3.4)](https://arxiv.org/html/2611.26492v1#S3.SS4) [(ref: main §4.2)](https://arxiv.org/html/2611.26492v1#S4.SS2)
- **把影像證據與讀報告分開評估** — 兩階段設計讓分類器與報告閱讀器可以分別替換、分別驗證；本研究的證據只支持「在固定分數下，微調小模型比這一套規則更會讀報告措辭」。換分類器會改變分數分布，作者提醒門檻與查核器都要重新測試。[(ref: main §5)](https://arxiv.org/html/2611.26492v1#S5)
- **待驗證的警訊** — 98.5% 是對自動標籤的一致率，不是抓到真實報告錯誤的比率；在使用原始影像配原始報告、由放射科醫師判斷旗標是否為真錯誤之前，不應把這個數字讀成臨床查錯能力。作者自己列出的下一步正是這種研究。[(ref: main §5)](https://arxiv.org/html/2611.26492v1#S5)
- **未微調的小模型不能直接拿來用** — 同一個 1.5B 模型不微調時幾乎是什麼都標記；若要以小型本地模型做報告查核，需要任務專屬的訓練資料與一個不依賴單一輸入就能得分的測試集。[(ref: main §4.2)](https://arxiv.org/html/2611.26492v1#S4.SS2)

## References

- `main` — Yanda Cheng, Bo Wen, Yuhao Lu. *Multimodal Error Detection in Chest X-ray Reports: A Large Language Model Reading Image Evidence*. arXiv:2611.26492v1, 2026. HTML：https://arxiv.org/html/2611.26492v1 ；用到的深鏈：[author block](https://arxiv.org/html/2611.26492v1)、[§1](https://arxiv.org/html/2611.26492v1#S1)、[§2](https://arxiv.org/html/2611.26492v1#S2)、[§3.1](https://arxiv.org/html/2611.26492v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.26492v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.26492v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.26492v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.26492v1#S3.SS5)、[Figure 2](https://arxiv.org/html/2611.26492v1#S3.F2)、[§4.1](https://arxiv.org/html/2611.26492v1#S4.SS1)、[Table 1](https://arxiv.org/html/2611.26492v1#S4.T1)、[Figure 3](https://arxiv.org/html/2611.26492v1#S4.F3)、[§4.2](https://arxiv.org/html/2611.26492v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.26492v1#S4.SS3)、[§5](https://arxiv.org/html/2611.26492v1#S5)、[§6](https://arxiv.org/html/2611.26492v1#S6)、[Data and Code Availability](https://arxiv.org/html/2611.26492v1#Sx1)、[Funding and Competing Interests](https://arxiv.org/html/2611.26492v1#Sx3)、[Appendix A](https://arxiv.org/html/2611.26492v1#A1)、[Table 2](https://arxiv.org/html/2611.26492v1#A1.T2)、[Appendix B.1](https://arxiv.org/html/2611.26492v1#A2.SS1)、[Appendix B.2](https://arxiv.org/html/2611.26492v1#A2.SS2)、[Appendix B.3](https://arxiv.org/html/2611.26492v1#A2.SS3)、[Appendix C](https://arxiv.org/html/2611.26492v1#A3)、[Appendix C.1](https://arxiv.org/html/2611.26492v1#A3.SS1)、[Appendix C.2](https://arxiv.org/html/2611.26492v1#A3.SS2)、[Table 3](https://arxiv.org/html/2611.26492v1#A3.T3)、[Appendix C.3](https://arxiv.org/html/2611.26492v1#A3.SS3)、[Table 4](https://arxiv.org/html/2611.26492v1#A3.T4)、[Figure 4](https://arxiv.org/html/2611.26492v1#A3.F4)、[Appendix C.4](https://arxiv.org/html/2611.26492v1#A3.SS4)、[Table 5](https://arxiv.org/html/2611.26492v1#A3.T5)、[Appendix D.1](https://arxiv.org/html/2611.26492v1#A4.SS1)、[Appendix D.2](https://arxiv.org/html/2611.26492v1#A4.SS2)、[Appendix D.3](https://arxiv.org/html/2611.26492v1#A4.SS3)
- `abstract` — arXiv abstract page, 2611.26492v1：https://arxiv.org/abs/2611.26492v1 （PDF：https://arxiv.org/pdf/2611.26492v1 ；DOI：https://doi.org/10.48550/arXiv.2611.26492）

[Home](../) · [AI Papers](./)
