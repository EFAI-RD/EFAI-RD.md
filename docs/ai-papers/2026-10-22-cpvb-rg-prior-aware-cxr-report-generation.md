---
catalog_id: "arxiv:2610.28289"
editors:
  - "Clare"
refs:
  main:
    title: "CPVB-RG: Cross-Prior Visual Bridging for Prior-Aware Chest X-Ray Report Generation"
    url: "https://arxiv.org/abs/2610.28289"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# CPVB-RG：把前後兩張胸片的「變化」與「共同結構」分開處理再寫報告，82M 解碼器對最接近的 prior-aware 基線 PriorRG 在 F1RadGraph 多 0.0090、VLScore 多 0.0582

## 來源

- 團隊：Durham University 電腦科學系（Department of Computer Science）與 County Durham and Darlington NHS Foundation Trust 放射科；共 4 位作者：Sike Xiang、Shuang Chen、Julie Cox、Amir Atapour-Abarghouei（通訊作者）。[(ref: main p.1)](https://arxiv.org/pdf/2610.28289v1#page=1)
- 論文：*CPVB-RG: Cross-Prior Visual Bridging for Prior-Aware Chest X-Ray Report Generation*，arXiv v1，2026；arXiv 頁面註記已被 WACV 2027 接受，授權 CC BY 4.0。[(ref: abstract)](https://arxiv.org/abs/2610.28289)
- 識別碼：[arXiv:2610.28289](https://arxiv.org/abs/2610.28289)；[DOI: 10.48550/arXiv.2610.28289](https://doi.org/10.48550/arXiv.2610.28289)。
- 全文：[arXiv PDF v1](https://arxiv.org/pdf/2610.28289v1)。
- 研究性質：完整方法論文，核心模組已實作、訓練並在兩個公開資料集評估；另有 135 例臨床病例的放射科醫師判讀，作者自稱為初步結果。[(ref: main §4.4, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)
- 證據邊界：本文依 arXiv v1 正文（第 1 至 5 節、Table 1–6、Figure 1–5）撰寫。論文把資料集切分、指標完整定義、判讀流程與部分消融放在補充材料，補充材料未納入本文引述；以 WACV 正式版為準的讀者請留意版本差異。

**編輯：** Clare

CPVB-RG 在胸片報告生成中，把本次與前次影像的關係拆成「進展差異」與「共同空間結構」兩條 attention 分支，再接上臨床文字與一個 82M 參數的解碼器；在 MIMIC-CXR 的 ReXrank Findings 評估上，它對同樣使用前次影像與 82M 解碼器的 PriorRG 有統計顯著但幅度不大的提升。[(ref: main Abstract, p.1)](https://arxiv.org/pdf/2610.28289v1#page=1) [(ref: main §4.2, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)

## 流程

![CPVB-RG 架構圖：上方黃框為 Stage1 Pre-training alignment，前次與本次胸片經 Vision Encoder、Projection 並加上 V 與 T 嵌入，Indication／History 經 Text Encoder 與 Projection，兩者進入含 PGFA、兩個 CA 與 Anchors 的 CPVB 模組，輸出與 Findings 文字的編碼以 L_align 對齊；下方紫框為 Stage2 Downstream joint reasoning，同一路徑的 CPVB 輸出送入 LLM Decoder，以 L_CE 訓練生成報告](assets/cpvb-rg-overview-fig1.png)

圖：論文 Figure 1（CC BY 4.0），作者 Xiang、Chen、Cox、Atapour-Abarghouei。上方黃色圓角框是 Stage 1 預訓練對齊，右側球面示意以 𝓛align 把 CPVB 輸出與 Findings 文字的編碼對齊；下方紫色圓角框是 Stage 2 報告生成，黃色方塊 LLM Decoder 以 𝓛CE 訓練。兩個階段裡的淡紫色方塊都是 CPVB，內含一個綠色 PGFA、兩個粉紅色 CA 與一排 Anchors；右下深紅色虛線框是圖例。正文的主要實驗中，這個解碼器是 DistilGPT2；Stage 2 另有一個 Perceiver 模組（式 12），圖中沒有畫出。[(ref: main Figure 1, p.3)](https://arxiv.org/pdf/2610.28289v1#page=3) [(ref: main §3.2, p.4)](https://arxiv.org/pdf/2610.28289v1#page=4)

## 背景／問題

放射科醫師判讀追蹤胸片時，會拿本次與前次檢查比較，找出新出現、消退或惡化的發現；論文指出多數報告生成系統不是沒有使用前次檢查，就是把前後影像特徵直接融合，沒有區分「期間變化」與「兩次都一樣的解剖結構」。[(ref: main Abstract, p.1)](https://arxiv.org/pdf/2610.28289v1#page=1) [(ref: main §1, p.1)](https://arxiv.org/pdf/2610.28289v1#page=1)

論文的設計前提是：直接融合會讓穩定的解剖結構留在表徵裡，可能蓋掉微小但臨床上重要的變化。[(ref: main §1, p.1)](https://arxiv.org/pdf/2610.28289v1#page=1) 這個前提在論文中引用的是一篇多模態醫學影像癌症偵測的綜述，沒有直接量測「融合表徵會蓋掉變化」的證據；論文能支持的是自身的消融：把 attention map 相減改成相加，或改用 PriorRG 式的時序融合，各項指標都下降（見下方 Table 4）。本文因此把它讀成作者的設計假設，而不是已知事實。[(ref: main Table 4, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)

論文要回答的是：在模型大小與輸入條件接近的情況下，把前後影像的交互拆成兩條分支，並讓臨床文字參與，報告的語言與臨床指標會不會比既有 prior-aware 方法好。它沒有直接評估「報告中描述期間變化的句子是否正確」。

## 方法摘要

輸入是本次胸片、一張前次胸片，以及檢查原因與病史等臨床文字；前後影像共用一個視覺編碼器，臨床文字另有文字編碼器。兩者投影到同一維度後，由 Cross-Prior Visual Bridge（CPVB）融合。[(ref: main §3, p.2)](https://arxiv.org/pdf/2610.28289v1#page=2)

CPVB 內的 Progression-Guided Focus Attention（PGFA）用兩條 attention 分支處理前後影像：progression-difference 分支把前次的 key／value 從本次扣掉，shared-spatial 分支把兩次的 key 平均，最後用前者減去加權的後者。之後兩個 Cross-Attention 單元以可學習的 anchor token 把影像證據與臨床文字連起來。[(ref: main §3.1, p.3–4)](https://arxiv.org/pdf/2610.28289v1#page=3)

訓練分兩階段：Stage 1 以病人層級的 InfoNCE，把 CPVB 表徵對齊到參考報告的 Findings 文字；Stage 2 以 CPVB 與一個 Perceiver 的輸出作為條件，訓練 DistilGPT2 自回歸生成報告。Findings 文字只在 Stage 1 當作對比監督，推論時不會輸入。[(ref: main §3, p.2)](https://arxiv.org/pdf/2610.28289v1#page=2) [(ref: main §3.2, p.4–5)](https://arxiv.org/pdf/2610.28289v1#page=4)

## 方法詳解

- **前次影像的選擇** — 有效的前次檢查必須是同一病人、時間嚴格早於本次的胸片；有多張時取時間最接近的一張，不設最短間隔，同一攝影方位優先，否則保留現有方位並以 view-position embedding 標記。所有檢查同樣前處理，不依影像品質主觀排除。[(ref: main §3.1, p.3)](https://arxiv.org/pdf/2610.28289v1#page=3)
- **沒有前次影像時** — 把本次影像的 token 加上本次的 temporal embedding 後複製一份當作前次的佔位；作者說明此時兩條分支都只依賴本次檢查，PGFA 只是一個學到的本次影像精修，不提供任何縱向證據。IU X-Ray 的訓練與評估都在這個設定下進行。[(ref: main §3.1, p.3)](https://arxiv.org/pdf/2610.28289v1#page=3)
- **PGFA 的計算** — 前後影像 token 先以縮減因子 r 做平均池化；progression-difference 分支為 K_e = K_c − K_p、V_e = V_c − V_p，shared-spatial 分支為 K_s = (K_c + K_p)/2。兩組 attention map 為 A_e = softmax(Q_c K_eᵀ/√d_h) 與 A_s = softmax(Q_c K_sᵀ/√d_h)，輸出為 (A_e − λA_s)V_e，λ = sigmoid(α) 為可學習係數；再插值回原 token 數、殘差相加並做 layer normalization。PGFA 疊三層，只精修本次影像 token，前次 token 固定作為縱向引導。[(ref: main Eq. 1–8, p.3–4)](https://arxiv.org/pdf/2610.28289v1#page=3)
- **CPVB 的兩個 Cross-Attention 單元** — 第一個以 anchor token 為 query、對臨床文字 token 做 attention，得到文字條件化的 F_t；第二個以 F_t 為 query、從 PGFA 輸出擷取縱向影像證據 F_v；兩者串接後做 layer normalization 得到 CPVB 表徵 F_b。[(ref: main Eq. 9, p.4)](https://arxiv.org/pdf/2610.28289v1#page=4)
- **Stage 1 對齊** — 影像端取 F_b 的平均並正規化，文字端取 Findings 經文字編碼器的 CLS 表徵；patient-aware InfoNCE 把同一 minibatch 中同一病人的 Findings 都當正例，包含其他次就診的報告，不同病人為負例，正例權重正規化。[(ref: main Eq. 10–11, p.4)](https://arxiv.org/pdf/2610.28289v1#page=4)
- **Stage 2 生成** — 本次影像編碼器的多層特徵聚合成 F_j，CPVB 輸出作為 Perceiver 的 latent query 從 F_j 取補充證據 F_a；[F_b; F_a] 作為 DistilGPT2 cross-attention 的條件序列，以 token-level cross-entropy 訓練。[(ref: main Eq. 12–15, p.4–5)](https://arxiv.org/pdf/2610.28289v1#page=4)
- **實作設定** — 共同特徵維度 768；視覺編碼器以 RAD-DINO 初始化，文字編碼器以 CXR-BERT-General 初始化，解碼器為 DistilGPT2；CPVB 使用 128 個 anchor token，報告最長 100 token。Stage 1 最多 50 epoch、batch size 32，Stage 2 最多 50 epoch、batch size 16，兩階段皆用 AdamW、學習率 5 × 10⁻⁵，搭配學習率排程與 early stopping；單張 NVIDIA A100。[(ref: main §4.1, p.5–6)](https://arxiv.org/pdf/2610.28289v1#page=5)
- **論文未交代** — 正文沒有資料集的切分方式與各集大小（作者指向補充材料）；沒有 attention head 數、λ 的初始值、Perceiver 的設定與解碼策略（如 beam size）；CE 的 Precision／Recall／F1 是 micro 還是 macro 彙總未說明；CPVB-RG 的結果是否為單次訓練、有無多個 random seed 未說明，Table 1、2、4、5 都沒有標準差；正文沒有程式碼連結。[(ref: main §4.1, p.5–6)](https://arxiv.org/pdf/2610.28289v1#page=5)

## 資料與實驗

下表整理論文使用的資料與評估設定；兩個公開資料集的切分細節在補充材料，正文未提供。[(ref: main §4.1, p.5–6)](https://arxiv.org/pdf/2610.28289v1#page=5) [(ref: main §4.4, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)

| 資料／評估 | 角色 | 內容（論文所述） |
|---|---|---|
| MIMIC-CXR | 主要訓練與測試 | 公開胸片與報告配對資料；有前次檢查時使用前次影像 |
| IU X-Ray | 第二個公開基準 | 規模比 MIMIC-CXR 小很多；在無前次影像的設定下訓練與評估 |
| ReXrank MIMIC-CXR Findings protocol | F1RadGraph 與 VLScore 評估 | 所有方法使用相同測試案例、參考 Findings 與指標實作 |
| 135 例臨床胸片 | 放射科醫師判讀 | 去識別化，依 14 個臨床觀察類別分層隨機抽樣，不代表自然盛行率；一位醫師初評、兩位覆核 |
| CheXbert 14 類 | CE 指標 | Positive 與 uncertain 視為有，negative 與未提及視為無 |

下表重製論文 Table 1 的 MIMIC-CXR 部分，只保留近兩年的方法與 CPVB-RG（原表另列 2020–2023 年的 10 個方法）。表註寫「–」代表原始論文未報告該指標。[(ref: main Table 1, p.5)](https://arxiv.org/pdf/2610.28289v1#page=5)

| Methods | Year | BLEU-1 | BLEU-2 | BLEU-3 | BLEU-4 | ROUGE-L | METEOR |
|---|---|---|---|---|---|---|---|
| BootstrappingLLM | 2024 | 0.402 | 0.262 | 0.180 | 0.128 | 0.291 | 0.175 |
| CoFE | 2024 | – | – | – | 0.125 | 0.304 | 0.176 |
| MAN | 2024 | 0.396 | 0.244 | 0.162 | 0.115 | 0.274 | 0.151 |
| DCG | 2024 | 0.397 | 0.258 | 0.166 | 0.126 | 0.295 | 0.162 |
| Med-LMM | 2024 | – | – | – | 0.128 | 0.289 | 0.161 |
| MambaXray-VL | 2025 | 0.422 | 0.268 | 0.184 | 0.133 | 0.289 | 0.167 |
| MPO | 2025 | 0.416 | 0.269 | 0.191 | 0.139 | 0.309 | 0.162 |
| PriorRG | 2026 | 0.412 | 0.290 | 0.220 | 0.175 | 0.324 | 0.189 |
| CPVB-RG | ours | 0.428 | 0.295 | 0.223 | 0.176 | 0.328 | 0.196 |

在 IU X-Ray 上，CPVB-RG 的 BLEU-1 至 BLEU-4 為 0.552、0.394、0.281、0.211，ROUGE-L 0.423、METEOR 0.227，原表中 IU X-Ray 部分沒有 PriorRG。[(ref: main Table 1, p.5)](https://arxiv.org/pdf/2610.28289v1#page=5)

下表重製論文 Table 2：MIMIC-CXR 上的 clinical efficacy（CE），同樣只保留 2024 年後的方法（原表另列 2020–2023 年的 6 個方法）。[(ref: main Table 2, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)

| Methods | Year | P | R | F1 |
|---|---|---|---|---|
| BootstrappingLLM | 2024 | 0.465 | 0.482 | 0.473 |
| CoFE | 2024 | 0.489 | 0.370 | 0.405 |
| MAN | 2024 | 0.411 | 0.398 | 0.389 |
| DCG | 2024 | 0.441 | 0.414 | 0.404 |
| Med-LMM | 2024 | 0.412 | 0.373 | 0.395 |
| MambaXray-VL | 2025 | 0.371 | 0.321 | 0.340 |
| MPO | 2025 | 0.436 | 0.376 | 0.353 |
| PriorRG | 2026 | 0.541 | 0.485 | 0.511 |
| CPVB-RG | ours | 0.552 | 0.482 | 0.515 |

下表重製論文 Table 3：在 ReXrank MIMIC-CXR Findings protocol 下與近期系統的比較；Params 是語言骨幹或解碼器的參數量。[(ref: main Table 3, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)

| Method | Params ↓ | F1RadGraph ↑ | VLScore ↑ |
|---|---|---|---|
| PriorRG | 82M | 0.2757 | 0.6110 |
| CheXagent | 2.7B | 0.2530 | 0.6724 |
| UniRG-CXR | 8B | 0.3040 | 0.6747 |
| MAIRA-2 | 7B | 0.2647 | 0.6508 |
| CPVB-RG | 82M | 0.2847 | 0.6692 |

下表重製論文 Table 4：CPVB 與 PGFA 的細部消融。BLEU-4 與 CE F1 用標準 MIMIC-CXR 測試集，F1RadGraph 與 VLScore 用 ReXrank Findings protocol；PriorRG-Style Fusion 是把融合機制換成 PriorRG 的時序 attention，其他設定固定。[(ref: main Table 4, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)

| Variant | BLEU-4 ↑ | CE F1 ↑ | F1RadGraph ↑ | VLScore ↑ |
|---|---|---|---|---|
| PriorRG-Style Fusion | 0.1753 | 0.4892 | 0.2762 | 0.6578 |
| Single Cross-Attention | 0.1240 | 0.5128 | 0.2224 | 0.6448 |
| w/o PGFA | 0.1689 | 0.4739 | 0.2785 | 0.6603 |
| w/o Difference Branch | 0.1741 | 0.5122 | 0.2839 | 0.6673 |
| w/o Spatial Branch | 0.1745 | 0.5064 | 0.2767 | 0.6644 |
| Spatial Addition | 0.1729 | 0.5040 | 0.2783 | 0.6621 |
| Full CPVB-RG | 0.1760 | 0.5150 | 0.2847 | 0.6692 |

下表重製論文 Table 5：逐步加入輸入時的 MIMIC-CXR 結果。Order 為時間先後資訊，Text 為臨床文字。[(ref: main Table 5, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)

| Current | Prior | Order | Text | CPVB | BLEU-4 | CE F1 |
|---|---|---|---|---|---|---|
| ✓ | – | – | – | – | 0.152 | 0.311 |
| ✓ | ✓ | – | – | – | 0.149 | 0.298 |
| ✓ | ✓ | ✓ | – | – | 0.158 | 0.347 |
| ✓ | ✓ | ✓ | ✓ | – | 0.168 | 0.471 |
| ✓ | ✓ | ✓ | ✓ | ✓ | 0.176 | 0.515 |

下表重製論文 Table 6：135 例臨床胸片的報告層級判讀，單位為百分比；Overall correct 為完全正確與部分正確之和。[(ref: main Table 6, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)

| Category | Proportion (%) |
|---|---|
| Overall correct | 89.6 |
| Completely correct reports | 60.7 |
| Partially correct | 28.9 |
| Mixed & Missing | 5.93 |
| Completely incorrect | 4.44 |

## 結果

- **對 PriorRG 的增幅有統計顯著性，但不大** — 以 10,000 次病人層級的配對 bootstrap 與雙尾 bootstrap z 檢定，CPVB-RG 比 PriorRG 在 F1RadGraph 高 0.0090（95% CI 0.0048 至 0.0135，p < 0.0001），VLScore 高 0.0582（95% CI 0.0492 至 0.0673，p < 0.0001）。作者選 PriorRG 作為主要對照，是因為兩者都使用前次檢查與 82M 參數的解碼器，主要差別在前後影像交互的方式。[(ref: main §4.2, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)
- **CE 指標幾乎持平** — 相對 PriorRG，Precision 高 0.011、F1 高 0.004、Recall 低 0.003；作者的解讀是 F1 的提升來自臨床觀察的一致性，而不是每個 CE 分項都更好。CE 與 BLEU 等指標沒有報告顯著性檢定，BLEU-4 對 PriorRG 只多 0.001。[(ref: main §4.2, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6) [(ref: main Table 1, p.5)](https://arxiv.org/pdf/2610.28289v1#page=5)
- **小解碼器與大模型的對照** — 在 ReXrank Findings protocol 下，CPVB-RG 的 F1RadGraph 排第二，低於 8B 的 UniRG-CXR（0.3040），高於 7B 的 MAIRA-2 0.0200；VLScore 比 UniRG-CXR 低 0.0055，也低於 2.7B 的 CheXagent（0.6724）。[(ref: main Table 3, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)
- **前次影像本身不夠，要加上時間順序** — 只加入沒有順序資訊的前次影像，BLEU-4 從 0.152 降到 0.149、CE F1 從 0.311 降到 0.298；加入時間順序後升到 0.158 與 0.347；加入臨床文字後 CE F1 升到 0.471，是表中最大的一步；最後加入 CPVB 才到 0.176 與 0.515。[(ref: main Table 5, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)
- **消融支持相減的設計，但各項差距都在千分位到百分位** — 拿掉 PGFA 使 BLEU-4、CE F1、F1RadGraph、VLScore 分別降 0.0071、0.0411、0.0062、0.0089；把 attention map 相減改成相加，CE F1 降 0.0110；PriorRG-Style Fusion 的 BLEU-4 接近，但 CE F1、F1RadGraph、VLScore 分別低 0.0258、0.0085、0.0114。只保留一個 Cross-Attention 單元的下降最明顯，F1RadGraph 降到 0.2224。[(ref: main §4.3.3, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7) [(ref: main Table 4, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)
- **Stage 1 對 Recall 影響最大** — 不做 Stage 1 預訓練時，所有 NLG 與 CE 指標都下降，其中 Recall 從 0.482 降到 0.418、F1 從 0.515 降到 0.468，降幅大於 NLG 指標。[(ref: main Figure 4, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7) [(ref: main §4.3.1, p.6–7)](https://arxiv.org/pdf/2610.28289v1#page=6)
- **臨床病例的錯誤型態** — 135 例中 89.6% 被判為整體正確，其中完全正確 60.7%、只有輕微遺漏 28.9%；5.93% 含錯誤陳述或遺漏重要發現，4.44% 完全錯誤。論文舉的錯誤例子包括把心律調節器寫成 AICD 並加入參考報告沒有的細節，以及把多發雙側發炎性病灶寫成基底部融合性不透明影。[(ref: main §4.4, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8) [(ref: main Figure 5, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)

## 限制

- **臨床病例評估為初步結果（作者自述）** — 作者明言 135 例的結果受樣本數限制，只能用來分析模型的成功與殘留錯誤；未來工作列出不規則或缺失的前次影像，以及多機構驗證。[(ref: main §4.4, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8) [(ref: main §5, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)
- **本書庫補充：基線數值可能不是在相同條件下重跑** — Table 1 與 Table 2 的表註寫「–」表示原始論文未報告，顯示這些基線數值很可能取自各自的原始論文；不同論文的報告切分、前處理與指標實作可能不同。在相同測試案例與指標實作下比較的只有 Table 3 的 ReXrank 評估與 Table 4 的消融。[(ref: main Table 1, p.5)](https://arxiv.org/pdf/2610.28289v1#page=5) [(ref: main Table 3, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)
- **本書庫補充：沒有直接量測「期間變化」寫得對不對** — 論文的動機是區分新出現、消退與惡化的發現，但評估指標都是整份報告層級的 NLG、CE、F1RadGraph 與 VLScore，沒有針對時序比較語句的正確率；PGFA 是否真的抓到期間變化，只能從消融的整體分數間接推論。[(ref: main §4.1, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)
- **本書庫補充：IU X-Ray 結果與 prior-aware 設計無關** — IU X-Ray 在沒有前次影像的設定下訓練與評估，PGFA 退化為本次影像的精修；這部分的結果反映的是其他元件與訓練方式，不是縱向建模。[(ref: main §3.1, p.3)](https://arxiv.org/pdf/2610.28289v1#page=3)
- **本書庫補充：消融差距小且無變異估計** — Table 4 的多數差距在 0.001 至 0.02 之間，論文只對 PriorRG 的兩個 ReXrank 指標做了 bootstrap 檢定，消融與 CE 指標沒有 CI 或多 seed 結果，個別元件的貢獻能否穩定重現無法從正文判斷。[(ref: main Table 4, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)
- **本書庫補充：臨床判讀流程的資訊有限** — 135 例依 14 類分層抽樣而非依盛行率，一位醫師初評、兩位覆核，正文沒有讀者間一致性統計，也沒有說明病例來源機構與判讀標準細節（作者指向補充材料）；這組百分比不能解讀為臨床部署下的錯誤率。[(ref: main §4.4, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)

## 與書庫其他文章的關係

MAIRA-2 是本篇 Table 3 的 7B 對照之一，它把前次影像與前次報告一起餵給 LLM，本篇則只用前次影像加臨床文字、以 82M 解碼器在 F1RadGraph 上高出 0.0200: [MAIRA-2：胸腔 X 光報告的文字正確，定位也正確嗎？](2026-09-15-maira-2-grounded-reporting.md)

該研究只給 LLM 前後兩份報告文字、評分它分不分得出「新出現」，本篇則從影像端設計模組去分離期間變化，但沒有對時序比較語句另外評分，兩篇合起來看正好缺一個「影像端的時序判讀正確率」: [序列胸片報告的時序判讀：七個 LLM、五種提示詞，分得出「新出現」嗎？](2026-09-22-llm-temporal-change-cxr-reports.md)

本篇的縱向輸入限定為同一病人時間最接近的前次影像，該研究則顯示把別的病人的相似前例報告放進 prompt 時，通用 VLM 會把對方的發現抄進報告，兩者是「前例從哪裡來」的兩種極端: [一篇 pilot 的警訊：相似病例報告進了 prompt，胸片 VLM 會抄進別人的發現](2026-10-02-rag-induced-hallucination-cxr-report.md)

## 實務的啟發

這是一篇完整實作、有公開基準與顯著性檢定的方法論文，但相對最接近基線的增幅不大，也沒有直接評估時序語句；它比較適合當作「如何把前次影像接進小模型」的設計參考，而不是可以直接換上的報告生成器。

第一，Table 5 的輸入消融值得借用。只加入沒有順序資訊的前次影像，分數反而略降；加上時間順序與臨床文字後，CE F1 從 0.298 一路升到 0.471。若院內在試做 prior-aware 的報告生成，先確認時間順序與檢查原因有沒有被模型正確接收，可能比換融合模組更優先；這是本篇單一資料集上的觀察，需要在自己的資料上重測。[(ref: main Table 5, p.7)](https://arxiv.org/pdf/2610.28289v1#page=7)

第二，評估要有能看見時序錯誤的指標。本篇與多數報告生成論文一樣用整份報告層級的分數；如果系統的賣點是「看懂前後變化」，評估設計應該加上針對時序比較語句的檢查，例如抽出「較前增加／新出現／消退」等陳述，與參考報告或醫師判讀逐條比對。本書庫認為這是讀這類論文時應該追問的缺口。

第三，小解碼器在 ReXrank 上的位置值得追蹤，但不宜過度解讀。82M 解碼器在 F1RadGraph 上高於 7B 的 MAIRA-2，在 VLScore 上則仍低於 UniRG-CXR 與 CheXagent；不同系統的輸入條件（是否使用前次報告、側位影像）不同，排名不能直接換算成部署選擇。[(ref: main Table 3, p.6)](https://arxiv.org/pdf/2610.28289v1#page=6)

第四，臨床病例中的錯誤型態提醒了器材辨識的風險：模型把心律調節器寫成 AICD，並補上參考報告沒有的細節。這類錯誤在整份報告分數上不一定明顯，若要做臨床試用，器材與病灶分布的描述需要單獨抽查。[(ref: main §4.4, p.8)](https://arxiv.org/pdf/2610.28289v1#page=8)

## References

- `main`：[CPVB-RG: Cross-Prior Visual Bridging for Prior-Aware Chest X-Ray Report Generation，arXiv PDF v1](https://arxiv.org/pdf/2610.28289v1)；本文使用 [p.1 Abstract、§1 Introduction](https://arxiv.org/pdf/2610.28289v1#page=1)、[p.2 §2 Related Work、§3 Method](https://arxiv.org/pdf/2610.28289v1#page=2)、[p.3 Figure 1、§3.1、Eq. 1–4](https://arxiv.org/pdf/2610.28289v1#page=3)、[p.4 Figure 2–3、Eq. 5–13、§3.2](https://arxiv.org/pdf/2610.28289v1#page=4)、[p.5 Table 1、Eq. 14–15、§4.1](https://arxiv.org/pdf/2610.28289v1#page=5)、[p.6 §4.1–4.2、Table 2–3、§4.3.1](https://arxiv.org/pdf/2610.28289v1#page=6)、[p.7 Table 4–5、Figure 4、§4.3.2–4.3.3](https://arxiv.org/pdf/2610.28289v1#page=7)、[p.8 Figure 5、§4.4、Table 6、§5 Conclusion](https://arxiv.org/pdf/2610.28289v1#page=8)。
- `abstract`：[arXiv:2610.28289](https://arxiv.org/abs/2610.28289)。
- `doi`：[10.48550/arXiv.2610.28289](https://doi.org/10.48550/arXiv.2610.28289)。

[Home](../) · [AI Papers](./)
