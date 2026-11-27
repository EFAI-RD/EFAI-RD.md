---
parent: AI Papers
nav_exclude: true
title: "ARIVE：胸片報告自動指標全拿第一，醫師評分與 Qwen3.5 打平"
catalog_id: "arxiv:2611.14018"
editors:
  - "Clare"
refs:
  main:
    title: "Interleaving anatomical inspection and diagnostic reasoning for explainable radiology report generation"
    url: "https://arxiv.org/html/2611.14018v1"
  abs:
    title: "arXiv abstract page: 2611.14018v1"
    url: "https://arxiv.org/abs/2611.14018v1"
  code:
    title: "DUTIR-BioNLP/ARIVE (GitHub)"
    url: "https://github.com/DUTIR-BioNLP/ARIVE"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# ARIVE：胸片報告自動指標全拿第一，醫師評分與 Qwen3.5 打平

## 來源

- 團隊：大連理工大學計算機科學與技術學院（Chentao Huang、Zhijun Wang、Yunxiang Li、Yuanyuan Sun、Jian Wang、Hongfei Lin、Ling Luo），以及大連醫科大學附屬第二醫院核醫科（Runlong Lin，負責臨床評估）。[(ref: main author block)](https://arxiv.org/html/2611.14018v1) [(ref: main Author contributions)](https://arxiv.org/html/2611.14018v1#Sx4)
- 論文：*Interleaving anatomical inspection and diagnostic reasoning for explainable radiology report generation*，arXiv:2611.14018v1（cs.CV；cs.AI），2026-11-10 提交，目前只有 v1，arXiv 頁未註記 venue；授權為 arXiv 非專屬散布授權。[(ref: abstract)](https://arxiv.org/abs/2611.14018v1)
- 識別碼：arXiv [2611.14018](https://arxiv.org/abs/2611.14018v1)；DOI [10.48550/arXiv.2611.14018](https://doi.org/10.48550/arXiv.2611.14018)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.14018v1)、[PDF v1](https://arxiv.org/pdf/2611.14018v1)。
- 程式與資料：MCoT 資料建構、訓練與推論程式公開於 [DUTIR-BioNLP/ARIVE](https://github.com/DUTIR-BioNLP/ARIVE)（Apache-2.0）；MIMIC-CXR 與 Chest ImaGenome 需在 PhysioNet 完成資格審核才能取得。經費來自國家自然科學基金與中央高校基本科研業務費，作者聲明無利益衝突。[(ref: main Code availability)](https://arxiv.org/html/2611.14018v1#Sx2) [(ref: main Data availability)](https://arxiv.org/html/2611.14018v1#Sx1) [(ref: main Funding)](https://arxiv.org/html/2611.14018v1#Sx3)
- 研究性質：完整的方法研究，不是 pilot；核心方法已實作並在 MIMIC-CXR（2,463 個測試樣本、285 位病人）與 MIMIC-ABN 上對六個模型比較，附病人群集 bootstrap 95% CI 與單尾檢定。醫師評估只由一位放射科醫師（即上述共同作者）在 100 例上完成，作者稱 MCoT 輔助審閱的結果為「初步證據」。[(ref: main Table S3)](https://arxiv.org/html/2611.14018v1#A2.T3) [(ref: main §4.9)](https://arxiv.org/html/2611.14018v1#S4.SS9) [(ref: main §2.4.3)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS3)
- 證據邊界：本文數值以 arXiv v1 HTML 版正文、Table 1–3 與附錄 Table S3、S8 為準；只以圖呈現的逐項 CheXbert F1（Fig. 2a）、Chest ImaGenome Gold 逐區域定位分數（Fig. 2g，正文點名的右上肺區除外）與 GREEN 的 CI（Fig. 2c、2f）未納入本文引述，案例圖（Fig. 5、6）只做文字摘要。

**編輯：** Clare

ARIVE 讓 4.85B 的胸片報告模型邊推理邊「調閱」解剖區域影像，在 MIMIC-CXR 七項自動臨床指標全拿第一，但一位放射科醫師盲評時，它的平均分（3.47）與 397B 的 Qwen3.5（3.51）幾乎相同，而且拆解實驗顯示主要增益出現在最後的強化學習階段，不在多模態推理鏈本身。[(ref: main Table 1)](https://arxiv.org/html/2611.14018v1#S2.T1) [(ref: main §2.4.1)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1) [(ref: main Table 2)](https://arxiv.org/html/2611.14018v1#S2.T2)

## 流程

![左右兩部分的圖。左半部為流程圖，五個圓角框：左上淺藍底、深藍實線框「1. MCoT data (159,416) MIMIC-CXR report -> GPT-OSS-120B rewrite with radiologist-style template + Chest ImaGenome boxes (29 regions)」，以向右箭頭連到右上淺藍底、深藍實線框「2a. SFT on MCoT Qwen3-VL-4B + anatomical visual module (4.85B total)」；其下以向下箭頭連到右中淺橘底、橘褐色實線框「2b. ACCO (GRPO), 4 rewards」，列出 R_BBOX region IoU、R_CXB^rea reasoning CheXbert、R_CXB^ans report CheXbert、R_RG RadGraph 與 inverse-frequency weights；再以向左箭頭連到左中淺藍底、深藍實線框「3. Inference」，內容為 global view、request region box、crop encoded and inserted in context、interpret、next region，最後產生 final Findings report；左中框以向下箭頭連到底部淺藍底、深藍實線寬框「Evaluation」，列出 MIMIC-CXR／MIMIC-ABN 測試集對 6 個比較模型（CheXbert F1、SRR-BERT、RadGraph、GREEN）、Chest ImaGenome Gold grounding，以及一位放射科醫師的 100 例報告評分、100 例 MCoT 評分與同 100 份 ARIVE 報告有無 MCoT 的審閱。左下角小字「Redrawn by EFAI-RD from arXiv:2611.14018v1 Fig. 1, Sections 2.4, 4.3-4.6」。右半部為分組長條圖，標題「Training-stage ablation on MIMIC-CXR (Table 2, Fig. 2f)」，縱軸「score (MIMIC-CXR test set)」刻度由 0.28 到 0.46；四組橫軸類別依序為 SFT (report only)、SFT w/ CoT (text only)、SFT w/ MCoT、ARIVE (MCoT + ACCO)，每組左為灰色 CheXbert macro F1 (14 obs.)、右為橘色 GREEN，數值依序為 0.412／0.335、0.412／0.314、0.410／0.320、0.437／0.360。](assets/arive-mcot-acco-ablation.png)

*圖：本書庫依論文 Fig. 1 與 §2.4、§4.3–4.6 重繪的 ARIVE 訓練與評估流程（左），以及 MIMIC-CXR 上四種訓練設定的 14 項 CheXbert macro F1 與 GREEN（右，縱軸由 0.28 起算）。數值來自 [Table 2](https://arxiv.org/html/2611.14018v1#S2.T2) 與 [§2.3.1](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS1)、[§2.3.2](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS2) 正文。*

## 背景／問題

作者引用的專家評估指出，自動產生的放射報告可能含有相當比例的錯誤，而多模態模型即使答對，其影像判讀與推理也可能有缺陷；作者據此主張「可解釋性」應是自動報告的核心要求，也就是讓每個發現的影像證據可以檢視、推理過程可以追溯。這是作者的立場；「可追溯的推理能幫臨床醫師找出錯誤」這一點，論文只提供了下文單一讀者的初步證據。[(ref: main §1)](https://arxiv.org/html/2611.14018v1#S1)

既有做法各補一塊：attention 視覺化、檢索相似病例、以圖結構引導生成，或像 MAIRA-2 那樣把發現連到定位框。作者指出的缺口是：純文字 chain-of-thought（CoT）讓推理變得可讀，卻不保證每一步都有對應的影像證據；推理越長，後段越依賴前文而不是影像（作者引用的 visual forgetting 文獻）。ARIVE 要回答的是：如果在推理過程中反覆「調閱」特定解剖區域的影像，報告的臨床正確性與可審閱性會不會改善。[(ref: main §1)](https://arxiv.org/html/2611.14018v1#S1)

## 方法摘要

- **Multimodal chain-of-thought（MCoT）資料** — 用放射科醫師式的判讀順序模板，請 GPT-OSS-120B 把 MIMIC-CXR 報告改寫成逐步推理，再把 Chest ImaGenome 29 個解剖區域的定位框插進與報告相關的步驟，得到 159,416 條訓練軌跡。[(ref: main §4.3)](https://arxiv.org/html/2611.14018v1#S4.SS3)
- **邊看邊推理** — 推理時模型先看整張影像，再輸出某個解剖區域的框；系統把該區域裁切、經 anatomical visual module 編碼後插回上下文，模型讀完再決定下一個區域或結束，最後寫出 Findings 報告。[(ref: main §4.4)](https://arxiv.org/html/2611.14018v1#S4.SS4)
- **兩階段訓練** — 先以 MCoT 做 supervised fine-tuning（SFT），再用 Anatomical and Clinical-Content Optimization（ACCO）：以 GRPO 同時最佳化四個 reward——區域定位、推理文字的 CheXbert、最終報告的 CheXbert 與 RadGraph，並以 inverse-frequency 權重加重少見區域與少見發現。[(ref: main §4.5)](https://arxiv.org/html/2611.14018v1#S4.SS5)
- **評估** — 自動指標（CheXbert F1、F1-SRR-BERT、RadGraph F1、GREEN 與 NLG 指標）對六個比較模型；Chest ImaGenome Gold 子集評估定位；一位放射科醫師盲評報告與 MCoT，並做「有無 MCoT」的配對審閱。[(ref: main §2.1)](https://arxiv.org/html/2611.14018v1#S2.SS1) [(ref: main §2.4)](https://arxiv.org/html/2611.14018v1#S2.SS4)

## 方法詳解

- **資料前處理** — 只用 Findings 段作為參考報告；只保留正面（AP／PA）影像、排除側面；依官方切分，訓練集再限縮到 Chest ImaGenome Silver 有標註的研究。定位評估用 Gold 子集：MIMIC-CXR 636 例（444 位病人）、MIMIC-ABN 142 例（120 位病人），脊椎與腹部因 Gold 無框而不計。[(ref: main §4.2)](https://arxiv.org/html/2611.14018v1#S4.SS2)
- **MCoT 建構** — 判讀順序取自 NV-Reason-CXR 釋出的放射科醫師推理軌跡：管路、氣道、雙肺、縱膈與肺門、心臟、上腹、骨骼，最後總結。改寫 prompt 要求保留全部診斷資訊；插框 prompt 只在報告提到、且屬於 29 個區域之一的步驟加框，其餘步驟維持純文字。每條軌跡平均 399.98 個字的推理文字、5.75 次區域定位。prompt 收在 Table S9–S10。[(ref: main §4.3)](https://arxiv.org/html/2611.14018v1#S4.SS3) [(ref: main Table S9)](https://arxiv.org/html/2611.14018v1#A5.T9)
- **輸入** — 當前影像、最近一次前次影像與其報告（若有），以及當次檢查的 Indication；影像縮放為 224×224。報告生成 prompt 見 Table S11–S12。[(ref: main §4.5.1)](https://arxiv.org/html/2611.14018v1#S4.SS5.SSS1) [(ref: main §4.6)](https://arxiv.org/html/2611.14018v1#S4.SS6)
- **架構** — 主幹為 Qwen3-VL-Instruct-4B；anatomical visual module 複製主幹的 vision encoder 與 visual merger 並以主幹參數初始化，總參數 4.85B。SFT 的 loss 只算文字 token，插入的區域影像嵌入只當上下文。[(ref: main §4.6)](https://arxiv.org/html/2611.14018v1#S4.SS6) [(ref: main §4.5.1)](https://arxiv.org/html/2611.14018v1#S4.SS5.SSS1) [(ref: main Table S8)](https://arxiv.org/html/2611.14018v1#A4.T8)
- **ACCO 的 reward** — 定位 reward 是加權 IoU，再對多出的框扣分（λ = 0.05）；兩個 CheXbert reward 是以 inverse-frequency 權重計算的 14 項發現 F1，其中推理文字用的是作者在 MCoT 資料上微調的「reasoning CheXbert」（held-out micro／macro F1 0.918／0.906）；RadGraph reward 為 Simple、Partial、Complete 三種分數的平均。四個 reward 在群組內各自標準化後平均成 advantage。[(ref: main §4.5.2)](https://arxiv.org/html/2611.14018v1#S4.SS5.SSS2) [(ref: main Table S7)](https://arxiv.org/html/2611.14018v1#A3.T7)
- **超參數** — SFT 以 AdamW、學習率 1×10⁻⁵、batch 64 在 MIMIC-CXR 訓練 6 epoch，MIMIC-ABN 模型由此接續 3 epoch；ACCO 只更新 LLM、1 epoch、學習率 1×10⁻⁶、batch 32、group size 5、KL 係數 0.01，inverse-frequency 指數 α_reg = 0.25、α_obs = 0.5。作者說明這些值是在算力預算內依經驗挑選。[(ref: main §4.6)](https://arxiv.org/html/2611.14018v1#S4.SS6)
- **比較條件** — Qwen3.5-397B-A17B（reasoning mode）、MedGemma-1.5、MAIRA-2、Libra、MLRG、PriorRG，使用公開 checkpoint，輸入內容與 ARIVE 相同；MAIRA-2 與 Libra 依原訓練流程在 MIMIC-ABN 上再訓練。檢定為單尾：CheXbert、SRR-BERT 用病人群集配對 permutation，RadGraph、GREEN 用配對 Wilcoxon；CI 由 10,000 次病人群集 bootstrap 求得。[(ref: main §4.7)](https://arxiv.org/html/2611.14018v1#S4.SS7) [(ref: main §4.9)](https://arxiv.org/html/2611.14018v1#S4.SS9)
- **醫師評估** — 報告評分：100 個隨機案例（71 位病人），來源隱藏，附當前影像、Indication 與前次影像／報告，1（不可用）到 5（可直接使用）。MCoT 評分：另抽 100 例（80 位病人），四個面向各 1–5 分。配對審閱：同 100 份 ARIVE 報告先只看影像審一次，間隔兩週再附上 MCoT 審一次，記錄判定有臨床顯著錯誤的報告與審閱時間。[(ref: main §2.4.1)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1) [(ref: main §2.4.2)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS2) [(ref: main §2.4.3)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS3)
- **論文未交代** — ARIVE 推論採 sampling，但 temperature、top-p 與 seed 未列；Qwen3.5 的解碼設定與推論時間未列；只有單次訓練，沒有多 seed 結果（CI 只反映測試樣本抽樣）；ACCO 實際使用的訓練樣本數與算力未列。[(ref: main Table S8)](https://arxiv.org/html/2611.14018v1#A4.T8) [(ref: main §4.6)](https://arxiv.org/html/2611.14018v1#S4.SS6)
- **論文未交代** — 用來比對觀察項與推理–報告一致性的 DeepSeek-V4.1-Flash 抽取沒有準確度驗證；放射科醫師的年資未列；配對審閱固定先「無 MCoT」再「有 MCoT」，沒有交叉順序，也沒有第二位讀者或一致性係數。[(ref: main §2.4.1)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1) [(ref: main §2.4.3)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS3)

## 資料與實驗

### 資料

| 資料集 | 統計 | 訓練 | 驗證 | 測試 |
|---|---|---|---|---|
| MIMIC-CXR | 樣本 | 159,416 | 1,286 | 2,463 |
| MIMIC-CXR | 研究 | 142,946 | 1,151 | 2,211 |
| MIMIC-CXR | 病人 | 57,729 | 448 | 285 |
| MIMIC-ABN | 樣本 | 34,259 | 302 | 432 |
| MIMIC-ABN | 研究 | 34,152 | 263 | 378 |
| MIMIC-ABN | 病人 | 23,039 | 181 | 134 |

*正面影像過濾並將訓練集限縮到 Chest ImaGenome Silver 後的數量。[(ref: main Table S3)](https://arxiv.org/html/2611.14018v1#A2.T3)*

### 實驗：與六個模型比較（MIMIC-CXR）

| 模型 | CheXbert F1 mic-5 | CheXbert F1 mac-5 | CheXbert F1 mic-14 | CheXbert F1 mac-14 | F1-SRR-BERT | RadGraph F1 |
|---|---|---|---|---|---|---|
| Qwen3.5-397B-A17B | 0.567** | 0.519** | 0.535** | 0.428 | 0.498** | 0.200** |
| MedGemma-1.5 | 0.596** | 0.534** | 0.556** | 0.409** | 0.491** | 0.219** |
| MAIRA-2 | 0.563** | 0.491** | 0.526** | 0.407** | 0.491** | 0.214** |
| Libra | 0.583** | 0.519** | 0.537** | 0.395** | 0.489** | 0.228** |
| MLRG | 0.559** | 0.491** | 0.520** | 0.363** | 0.492** | 0.241** |
| PriorRG | 0.575** | 0.508** | 0.537** | 0.391** | 0.511 | 0.270** |
| ARIVE | 0.652 | 0.555 | 0.603 | 0.437 | 0.515 | 0.271 |

*節錄 Table 1 的 MIMIC-CXR 部分（各欄 95% CI 省略）。mic／mac 為 micro／macro 平均，5／14 為發現數。\*\* 表示 ARIVE 單尾檢定顯著較高（p < 0.01）；未標者不顯著。ARIVE 的 GREEN 為 0.360，次高的 PriorRG 為 0.352。[(ref: main Table 1)](https://arxiv.org/html/2611.14018v1#S2.T1) [(ref: main §2.2)](https://arxiv.org/html/2611.14018v1#S2.SS2)*

### 實驗：訓練階段拆解（MIMIC-CXR）

| 訓練設定 | CheXbert F1 mic-5 | CheXbert F1 mac-14 | F1-SRR-BERT | RadGraph F1 | GREEN |
|---|---|---|---|---|---|
| SFT（只學報告） | 0.576** | 0.412** | 0.503* | 0.243** | 0.335 |
| SFT w/ CoT（純文字推理） | 0.590** | 0.412** | 0.487** | 0.227** | 0.314 |
| SFT w/ MCoT | 0.601** | 0.410** | 0.501** | 0.236** | 0.320 |
| ARIVE（MCoT＋ACCO） | 0.652 | 0.437 | 0.515 | 0.271 | 0.360 |

*節錄 Table 2 的 MIMIC-CXR 部分，GREEN 取自正文（§2.3.1、§2.3.2）。\* p < 0.05、\*\* p < 0.01（ARIVE 較高）。[(ref: main Table 2)](https://arxiv.org/html/2611.14018v1#S2.T2) [(ref: main §2.3.1)](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS1) [(ref: main §2.3.2)](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS2)*

### 實驗：放射科醫師評估

| 評估 | 項目 | 結果 |
|---|---|---|
| 報告盲評（100 例，1–5 分） | 平均分 | 參考報告 3.88、Qwen3.5 3.51、ARIVE 3.47、PriorRG 3.31 |
| 報告盲評 | 4–5 分（至多小修）比例 | 參考報告 81%、Qwen3.5 56%、ARIVE 50%、PriorRG 40% |
| 報告盲評 | 配對比較 ARIVE 高／低／同 | 對 PriorRG 30／19／51；對 Qwen3.5 31／34／35 |
| MCoT 評分（另 100 例） | 平均分（95% CI） | diagnostic traceability 4.90（4.84–4.96）、clinical factual correctness 4.87（4.79–4.94）、expression quality 4.67（4.58–4.76）、anatomical localization accuracy 4.30（4.14–4.46） |
| 有無 MCoT 的配對審閱 | 判定有錯的報告 | 8／100 → 11／100（前 8 份皆再次被找出） |
| 有無 MCoT 的配對審閱 | 每份審閱時間中位數（IQR） | 24.5 s（18.0–36.4）→ 42.5 s（31.8–56.1） |

*[(ref: main §2.4.1)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1) [(ref: main §2.4.2)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS2) [(ref: main §2.4.3)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS3) [(ref: main Fig. 3)](https://arxiv.org/html/2611.14018v1#S2.F3) [(ref: main Fig. 4)](https://arxiv.org/html/2611.14018v1#S2.F4)*

## 結果

- **自動指標全拿第一，但主要指標對 Qwen3.5 不顯著** — MIMIC-CXR 七項臨床指標 ARIVE 都最高，42 組比較中 40 組 p < 0.01；兩個例外是主要指標 14 項 macro F1 對 Qwen3.5（0.437 對 0.428）與 F1-SRR-BERT 對 PriorRG（0.515 對 0.511）。MIMIC-ABN 上 14 項 macro F1 0.408 對 Qwen3.5 0.365，36 組中 32 組 p < 0.05。[(ref: main §2.2)](https://arxiv.org/html/2611.14018v1#S2.SS2) [(ref: main Table 1)](https://arxiv.org/html/2611.14018v1#S2.T1)
- **字面相似度沒有領先** — BLEU-4、METEOR、ROUGE-L 在兩個資料集上 ARIVE 都不是最高，作者解讀為模型重視臨床內容而非參考報告的措辭。[(ref: main §2.2)](https://arxiv.org/html/2611.14018v1#S2.SS2) [(ref: main Table S1)](https://arxiv.org/html/2611.14018v1#A1.T1)
- **多模態推理鏈本身的報告增益很小** — 純文字 CoT 讓 GREEN 由 0.335 降到 0.314；改成 MCoT 回升到 0.320，但 14 項 macro F1 仍是 0.410（SFT 為 0.412），RadGraph F1 與 GREEN 也仍低於只學報告的 SFT，要加上 ACCO 才超過。作者在討論中承認這一點。[(ref: main §2.3.1)](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS1) [(ref: main §3)](https://arxiv.org/html/2611.14018v1#S3)
- **MCoT 改善的是推理與報告的一致性** — 在 MIMIC-ABN 的 142 例 Gold 子集，MCoT 相對純文字 CoT 把推理階段 macro F1 由 0.310 提高到 0.413、推理–報告一致性 macro F1 由 0.728 提高到 0.894。[(ref: main Table 3)](https://arxiv.org/html/2611.14018v1#S2.T3)
- **ACCO 帶來主要增益，各 reward 互有取捨** — 加上 ACCO 後 14 項 macro F1 0.410→0.437、GREEN 0.320→0.360。拿掉報告端 CheXbert reward 時定位反而變好（mIoU 0.493 對 0.474），但 Gold 子集最終報告 micro F1 由 0.505 降到 0.463；作者據此指出定位品質不能代表報告正確。右上肺區的區域選擇 F1 由 MCoT 的 0.083 提高到 ARIVE 的 0.226。[(ref: main §2.3.2)](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS2) [(ref: main Table 3)](https://arxiv.org/html/2611.14018v1#S2.T3)
- **醫師評分與自動指標不一致** — ARIVE 每項自動指標都高於 Qwen3.5，醫師平均分卻是 3.47 對 3.51，配對比較 31 勝 34 負。用 LLM 抽觀察項比對後，ARIVE 涵蓋 71.3% 的參考觀察、所報觀察有 81.1% 獲參考支持；Qwen3.5 分別為 73.0% 與 57.3%，參考報告沒有的觀察 216 個對 ARIVE 的 66 個。作者推測參考式指標會懲罰這些額外觀察，但醫師看影像時可能接受其中一部分。[(ref: main §2.4.1)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1) [(ref: main §3)](https://arxiv.org/html/2611.14018v1#S3)
- **推理鏈可追溯，但定位分數較低** — 597 個報告主張中 572 個（95.8%）完全由推理支持、2 個（0.3%）相互矛盾；449 個推理中的陽性或不確定發現有 23 個（5.1%）沒寫進報告，其中 8 個是管路裝置。醫師把定位分數較低部分歸因於左肺與心臟的裁切範圍不完整。[(ref: main §2.4.2)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS2)
- **有 MCoT 時多抓到 3 份錯誤報告，審閱時間增加** — 判定有錯的報告由 8 份增為 11 份，審閱時間中位數由 24.5 秒增為 42.5 秒；作者稱之為初步證據。案例 2 也顯示，錯誤的「輕度心臟擴大」會從推理中的某一步一路傳到報告，作者提醒流暢的推理可能讓錯誤顯得更可信。[(ref: main §2.4.3)](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS3) [(ref: main §2.5.2)](https://arxiv.org/html/2611.14018v1#S2.SS5.SSS2)
- **成本** — ARIVE 4.85B 參數，在單張 A100 上產生推理鏈加報告平均 1.13 秒，與 MedGemma-1.5（1.30 秒）、MAIRA-2（1.20 秒）只出報告的時間相近，MLRG、PriorRG 較快。[(ref: main Table S8)](https://arxiv.org/html/2611.14018v1#A4.T8)

## 限制

- **單一機構資料** — 所有評估都來自 MIMIC-CXR 及其子集，跨院與不同報告風格的泛化未驗證；只用正面影像（作者自述）。[(ref: main §3)](https://arxiv.org/html/2611.14018v1#S3)
- **推理鏈是由報告反推的** — MCoT 由 LLM 從報告改寫而來，會繼承原報告的遺漏與機構寫作習慣，也可能有改寫錯誤，不能視為放射科醫師真實的思考過程（作者自述）。[(ref: main §3)](https://arxiv.org/html/2611.14018v1#S3)
- **部分解剖區域監督稀少** — 上、中肺區與肺尖合計只占約 2.8% 的定位框，ACCO 後定位仍明顯較弱；作者推測這可能與 Consolidation、Pneumothorax 的 CheXbert F1 偏低有關，但未證實（作者自述）。[(ref: main §3)](https://arxiv.org/html/2611.14018v1#S3) [(ref: main Table S4)](https://arxiv.org/html/2611.14018v1#A2.T4)
- **區域是預先定義的解剖框** — 不是病灶、切片或體積結構，延伸到其他影像模態需要新的空間標註與評估（作者自述）。[(ref: main §3)](https://arxiv.org/html/2611.14018v1#S3)
- **醫師評估規模小、讀者單一** — 報告評分、MCoT 評分與配對審閱都由同一位、且是共同作者的醫師完成，各 100 例；配對審閱的 8→11 沒有統計檢定，順序固定。這是本書庫依論文設計整理的限制。[(ref: main §2.4)](https://arxiv.org/html/2611.14018v1#S2.SS4) [(ref: main Author contributions)](https://arxiv.org/html/2611.14018v1#Sx4)
- **reward 與評估指標同源** — ACCO 直接以 CheXbert 與 RadGraph 當 reward，而主要比較也用 CheXbert F1 與 RadGraph F1，ACCO 後在這些指標上的增益部分反映「對指標最佳化」；未進 reward 的 GREEN 也上升（0.320→0.360），但醫師評分未顯示同幅領先。這是本書庫的解讀。[(ref: main §4.5.2)](https://arxiv.org/html/2611.14018v1#S4.SS5.SSS2) [(ref: main §2.3.2)](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS2)

## 與書庫其他文章的關係

MAIRA-2 是 ARIVE 的比較模型之一（MIMIC-CXR 14 項 macro F1 0.407 對 0.437）；兩篇都把報告連回胸片上的位置，MAIRA-2 是在輸出端讓每個發現附上定位框，ARIVE 則是在推理過程中裁切解剖區域、把影像證據插回上下文再寫報告: [MAIRA-2：胸片報告文字對了，定位不一定對](2026-09-15-maira-2-grounded-reporting.md)

兩篇都先以推理文字做監督微調、再用含 IoU reward 的 GRPO 強化學習；MedChain-R1 的 GRPO 在序列定位上只多 0.37 mIoU，ARIVE 的 ACCO 則是報告臨床指標增益的主要來源，但兩者任務與指標不同，不能直接比較幅度: [MedChain-R1：換上別題的推理，定位 mIoU 掉 12 點](2026-11-10-medchain-r1-sequential-grounding-rationale.md)

ARIVE 把 MedGemma-1.5 列為通用醫療 VLM 的比較對象：在 MIMIC-CXR 上它是三項 CheXbert 指標最強的比較模型（14 項 micro F1 0.556），ARIVE 以相近的參數量（4.85B 對 4.30B）高出 3.9–9.4%: [MedGemma 1.5：4B 吃下 3D 影像與全切片，代價一併公開](2026-09-16-medgemma-1-5.md)

本篇自動臨床指標全拿第一、醫師盲評卻與通用大模型打平，評估指標譜系文把它當成「自動指標第一不等於醫師偏好」的例子，並說明這些指標各自量的是什麼: [放射報告評估指標：從 BLEU 到 GREEN，三個新分數都拿同 50 例驗證](../ai-basics/radiology-report-generation-metrics.md)

## 實務的啟發

- **把「推理階段」和「reward 階段」分開評估** — ARIVE 的拆解顯示，多模態推理鏈主要改善推理與報告的一致性，報告臨床指標的增益多半來自 ACCO。評估類似方法時，應要求同時報告「只加推理監督」與「再加 RL」兩個版本，避免把 RL 的增益歸功於可解釋性設計。
- **reward 用到的指標，要另找獨立指標驗證** — 以 CheXbert／RadGraph 當 reward 時，這兩個指標的領先不能單獨當證據；GREEN、醫師盲評或外部資料集這類未進入訓練目標的評估，才是比較可信的檢驗。本研究中醫師盲評並未顯示 ARIVE 優於 Qwen3.5。
- **「可審閱」是一個待驗證的假設，不是已證實的效益** — 單一讀者 100 例中，附上推理鏈多找出 3 份錯誤報告，但審閱時間約增加七成，且錯誤推理同樣會被流暢地寫進報告。若要把推理鏈放進審閱流程，應先以多位讀者、交叉順序的設計量測找錯率與時間成本。
- **定位分數不等於報告正確** — 拿掉報告端 reward 後定位更好、報告更差；只看 grounding 指標挑模型可能挑錯方向，這一點可借用為評估報告生成模型時的檢查項。

## References

- **main** — Huang C, Lin R, Wang Z, Li Y, Sun Y, Wang J, Lin H, Luo L. *Interleaving anatomical inspection and diagnostic reasoning for explainable radiology report generation*. arXiv:2611.14018v1, 2026. HTML: https://arxiv.org/html/2611.14018v1 ；deep links used: [§1](https://arxiv.org/html/2611.14018v1#S1)、[§2.1](https://arxiv.org/html/2611.14018v1#S2.SS1)、[§2.2](https://arxiv.org/html/2611.14018v1#S2.SS2)、[Table 1](https://arxiv.org/html/2611.14018v1#S2.T1)、[§2.3.1](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS1)、[Table 2](https://arxiv.org/html/2611.14018v1#S2.T2)、[§2.3.2](https://arxiv.org/html/2611.14018v1#S2.SS3.SSS2)、[Table 3](https://arxiv.org/html/2611.14018v1#S2.T3)、[§2.4](https://arxiv.org/html/2611.14018v1#S2.SS4)、[§2.4.1](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS1)、[Fig. 3](https://arxiv.org/html/2611.14018v1#S2.F3)、[§2.4.2](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS2)、[Fig. 4](https://arxiv.org/html/2611.14018v1#S2.F4)、[§2.4.3](https://arxiv.org/html/2611.14018v1#S2.SS4.SSS3)、[§2.5.2](https://arxiv.org/html/2611.14018v1#S2.SS5.SSS2)、[§3](https://arxiv.org/html/2611.14018v1#S3)、[§4.2](https://arxiv.org/html/2611.14018v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.14018v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.14018v1#S4.SS4)、[§4.5](https://arxiv.org/html/2611.14018v1#S4.SS5)、[§4.5.1](https://arxiv.org/html/2611.14018v1#S4.SS5.SSS1)、[§4.5.2](https://arxiv.org/html/2611.14018v1#S4.SS5.SSS2)、[§4.6](https://arxiv.org/html/2611.14018v1#S4.SS6)、[§4.7](https://arxiv.org/html/2611.14018v1#S4.SS7)、[§4.9](https://arxiv.org/html/2611.14018v1#S4.SS9)、[Data availability](https://arxiv.org/html/2611.14018v1#Sx1)、[Code availability](https://arxiv.org/html/2611.14018v1#Sx2)、[Funding](https://arxiv.org/html/2611.14018v1#Sx3)、[Author contributions](https://arxiv.org/html/2611.14018v1#Sx4)、[Table S1](https://arxiv.org/html/2611.14018v1#A1.T1)、[Table S3](https://arxiv.org/html/2611.14018v1#A2.T3)、[Table S4](https://arxiv.org/html/2611.14018v1#A2.T4)、[Table S7](https://arxiv.org/html/2611.14018v1#A3.T7)、[Table S8](https://arxiv.org/html/2611.14018v1#A4.T8)、[Table S9](https://arxiv.org/html/2611.14018v1#A5.T9)
- **abs** — arXiv abstract page: https://arxiv.org/abs/2611.14018v1 ；DOI: https://doi.org/10.48550/arXiv.2611.14018
- **code** — DUTIR-BioNLP/ARIVE: https://github.com/DUTIR-BioNLP/ARIVE

[Home](../) · [AI Papers](./)
