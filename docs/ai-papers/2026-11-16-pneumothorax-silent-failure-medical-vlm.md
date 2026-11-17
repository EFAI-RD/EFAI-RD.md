---
parent: AI Papers
nav_order: 4
title: "胸片 VLM 稽核：兩個模型對 432 例氣胸全答「沒有」"
catalog_id: "arxiv:2611.14975"
editors:
  - "Clare"
refs:
  main:
    title: "Aggregate Accuracy Hides Diagnosis-Specific Failure in Medical Vision-Language Models"
    url: "https://arxiv.org/html/2611.14975v1"
  abs:
    title: "arXiv abstract page: 2611.14975v1"
    url: "https://arxiv.org/abs/2611.14975v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 胸片 VLM 稽核：兩個模型對 432 例氣胸全答「沒有」

## 來源

- 團隊：Shreya Ajay Kale 與 Angad Ripudaman Singh Bajwa，兩位皆標示為獨立研究者（Independent Researcher），共同第一作者；論文未列機構與經費來源。[(ref: main author block)](https://arxiv.org/html/2611.14975v1)
- 論文：*Aggregate Accuracy Hides Diagnosis-Specific Failure in Medical Vision-Language Models*，arXiv:2611.14975v1（eess.IV；另列 cs.CL、cs.CV、cs.LG），2026-11-11 提交，目前只有 v1；arXiv 頁註記已被 NeurIPS 2026 Workshop on Medical Reasoning with Vision Language Foundation Models（Med-Reasoner）接受；授權為 arXiv 非專屬散布授權。[(ref: abstract)](https://arxiv.org/abs/2611.14975v1)
- 識別碼：arXiv [2611.14975](https://arxiv.org/abs/2611.14975v1)；DOI [10.48550/arXiv.2611.14975](https://doi.org/10.48550/arXiv.2611.14975)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.14975v1)、[PDF v1](https://arxiv.org/pdf/2611.14975v1)。
- 程式與資料：兩個資料集與五個模型都是公開的；作者不釋出程式，也不釋出評估題目清單與產生腳本，只在正文寫明抽樣格子、提示詞與解碼設定，供讀者自行重建。[(ref: main Checklist)](https://arxiv.org/html/2611.14975v1#Sx1)
- 研究性質：對公開模型的推論稽核（audit），workshop 論文，不訓練任何模型；不是 pilot，核心分析（6,048 題主評估、四種提示、解析度與規模檢查、SIIM-ACR 外部重現、logit 與 linear probe）都已實際執行並有數字。[(ref: main §3)](https://arxiv.org/html/2611.14975v1#S3) [(ref: main §4)](https://arxiv.org/html/2611.14975v1#S4)
- 證據邊界：本文數值以 arXiv v1 HTML 版的正文、Table 1–5 與文末 checklist 為準；作者提到的人口學差異檢定只以文字摘要結果，論文沒有列出對應數值表，本文不另行引述。[(ref: main §5)](https://arxiv.org/html/2611.14975v1#S5)

**編輯：** Clare

作者在 6,048 題性別、年齡、徵象與標籤都平衡的胸片是非題上稽核五個開放醫療 VLM，發現 HuatuoGPT-Vision-7B 與 Qwen2.5-VL-7B 對 432 張氣胸陽性影像一張都沒答「有」，同一批影像 Lingshu-7B 抓到 67%、MedGemma-4B 抓到 38%。[(ref: main Table 2)](https://arxiv.org/html/2611.14975v1#S4.T2)

## 流程

![左右兩欄圖。左欄由上而下四個淺藍底、深藍實線的圓角框，以三支向下箭頭相連：「1. Prevalence-matched audit (ChestX-ray14)：2 sexes x 3 age bands x 7 findings x 2 labels = 84 cells; 72 images per cell -> 6,048 yes/no items」、「2. Five open VLMs, deterministic decoding：MedGemma-4B, Lingshu-7B, HuatuoGPT-Vision-7B, Qwen2.5-VL-7B, MedVLM-R1; vLLM, temperature 0」、「3. Rule out alternatives：4 prompt formats, native 1024px, single-label cases, Qwen2.5-VL-72B / MedGemma-27B, SIIM-ACR masks」、「4. Read logits and hidden states：first-token P(Yes), margin, ECE; linear probe on decision-token hidden state」；左下角小字「Redrawn by EFAI-RD from arXiv:2611.14975v1 Sections 3.1-4.6」。右欄為長條圖，標題「Tables 2-3: pneumothorax recall」，縱軸為「Pneumothorax recall (default prompt)」，刻度 0.0–1.0；橫軸四個模型依序為 Lingshu-7B、MedGemma-4B、HuatuoGPT-7B、Qwen2.5-VL-7B，每組左為灰色 ChestX-ray14 (432 positives)、右為橘色 SIIM-ACR (432 positives)，長條上方標示數值：Lingshu-7B 0.671、0.861；MedGemma-4B 0.377、0.470；HuatuoGPT-7B 0.000、0.000；Qwen2.5-VL-7B 0.000、0.000。](assets/pneumothorax-silent-failure-audit-and-recall.png)

*圖：本書庫依論文 §3.1–4.6 重繪的四段稽核流程（左），以及預設提示下四個模型在 ChestX-ray14 與 SIIM-ACR 各 432 張氣胸陽性影像上的 recall（右）。數值來自 [Table 2](https://arxiv.org/html/2611.14975v1#S4.T2) 與 [Table 3](https://arxiv.org/html/2611.14975v1#S4.T3)；MedVLM-R1 因幾乎全答「no」未列入。*

## 背景／問題

作者的出發點是：醫療 VLM 多半以跨徵象平均的準確率互相比較，而平均數可能把某一個診斷的完全失效藏起來。這是作者對現行評估習慣的描述，論文沒有另外統計有多少基準只報平均分數；平均數會掩蓋弱勢子集，則有 hidden stratification 等既有研究可循。[(ref: main §1)](https://arxiv.org/html/2611.14975v1#S1) [(ref: main §2)](https://arxiv.org/html/2611.14975v1#S2)

作者認為這種失效在輸出上難以察覺：模型可以描述氣胸的放射徵象（例如塌陷肺邊緣的 pleural line），接著說它不存在，既不拒答也不保留，讀起來就是一句有把握的陰性判讀。[(ref: main §1)](https://arxiv.org/html/2611.14975v1#S1) 本篇要問的是：一個整體分數不差的醫療 VLM，會不會整個漏掉某個診斷；如果會，原因是提示、解析度、標籤雜訊、模型規模，還是模型根本「看不到」。[(ref: main §1)](https://arxiv.org/html/2611.14975v1#S1)

## 方法摘要

- **Prevalence-matched audit** — 從 ChestX-ray14 以 2 種性別 × 3 個年齡帶 × 7 種徵象 × 有／無，組成 84 格、每格 72 張，共 6,048 題是非題；每種徵象各 432 張陽性、432 張陰性。[(ref: main §3.1)](https://arxiv.org/html/2611.14975v1#S3.SS1)
- **五個開放模型** — MedGemma-4B、Lingshu-7B、HuatuoGPT-Vision-7B、Qwen2.5-VL-7B 與 MedVLM-R1，以 vLLM、temperature 0 推論；Lingshu 與 HuatuoGPT-Vision 都是 Qwen2.5-VL-7B 的醫療微調版，可在同一主幹上比較。[(ref: main §3.4)](https://arxiv.org/html/2611.14975v1#S3.SS4)
- **四種影像條件** — 原圖、換成標籤相反的另一位病人（swap）、輕微擾動（augmented）與灰色空白圖，用來算 grounding。[(ref: main §3.3)](https://arxiv.org/html/2611.14975v1#S3.SS3)
- **排除其他解釋** — 四種提示格式、原生 1024 像素、只有單一標籤的影像、7B→72B 的規模檢查，以及有放射科醫師像素遮罩的 SIIM-ACR 外部重現。[(ref: main §4.2)](https://arxiv.org/html/2611.14975v1#S4.SS2) [(ref: main §4.3)](https://arxiv.org/html/2611.14975v1#S4.SS3) [(ref: main §4.4)](https://arxiv.org/html/2611.14975v1#S4.SS4)
- **讀模型內部** — 由第一個回答 token 的 Yes／No 機率算信心、margin 與 ECE，並以 linear probe 檢查決策 token 的 hidden state 能否解碼出氣胸。[(ref: main §4.5)](https://arxiv.org/html/2611.14975v1#S4.SS5) [(ref: main §4.6)](https://arxiv.org/html/2611.14975v1#S4.SS6)

## 方法詳解

- **題目建構** — ChestX-ray14 共 112,120 張正面胸片、30,805 位病人；去掉 16 筆不合理年齡、保留 AP 與 PA。年齡帶為 0–40、40–60、60+（原 60–80 與 80+ 合併）；七種徵象是能填滿每個人口學格子的那些，pneumonia 因 80 歲以上男性只有 5 張陽性而剔除。6,048 題來自 4,054 位病人。[(ref: main §3.1)](https://arxiv.org/html/2611.14975v1#S3.SS1)
- **攝影姿勢平衡** — AP 比例在性別間差 3.1 個百分點、年齡帶間差 5.8 個百分點，作者據此認為姿勢不太能解釋人口學結果。[(ref: main §3.1)](https://arxiv.org/html/2611.14975v1#S3.SS1)
- **預設提示** — 每張影像配一題單一徵象的是非題：「Is there evidence of {finding} on this chest X-ray? Answer yes or no, then briefly explain your reasoning. Start your reply with either ‘Yes’ or ‘No’.」原圖縮放至 512×512 並轉 RGB。[(ref: main §3.3)](https://arxiv.org/html/2611.14975v1#S3.SS3)
- **影像條件** — swap 換成同一徵象、標籤相反、AP／PA 相同的另一位病人；augmented 為 ±2° 旋轉、±5% 亮度、JPEG 品質 85；blank 為灰色均勻影像，所有模型都答「no」，因此不納入 grounding。所有變體以固定 seed 產生一次並快取，各模型拿到相同輸入。[(ref: main §3.3)](https://arxiv.org/html/2611.14975v1#S3.SS3)
- **推論設定** — temperature 0、固定 seed，輸出上限 200 token（MedVLM-R1 為 400）；checklist 註明 vLLM 0.27.1。[(ref: main §3.4)](https://arxiv.org/html/2611.14975v1#S3.SS4) [(ref: main Checklist)](https://arxiv.org/html/2611.14975v1#Sx1)
- **指標** — 每種徵象報 recall、specificity 與兩者平均的 balanced accuracy（一律答 yes 或一律答 no 都是 0.500）。grounding = P(flip | swap) − P(flip | augment)，以真實標籤為條件計算；模型從不翻轉時 grounding 無定義。[(ref: main §3.5)](https://arxiv.org/html/2611.14975v1#S3.SS5)
- **SIIM-ACR 外部重現** — 12,047 張 1024×1024 胸片、附放射科醫師逐像素的氣胸遮罩；作者抽 60 例核對標籤與遮罩一致，再抽 432 張陽性、432 張陰性，陽性依遮罩面積分成三組各 144 張（最大組佔影像 1.2–7.2%）。此資料集沒有年齡、性別與姿勢欄位，只用來重現氣胸結果。[(ref: main §3.2)](https://arxiv.org/html/2611.14975v1#S3.SS2)
- **信心分析** — 從第一個 token 的 top-20 logprob 取 Yes／No 機率（合併大小寫），正規化為 P(Yes)，margin = log P_Yes − log P_No；另以 margin 排序 864 例算 AUROC。[(ref: main §4.5)](https://arxiv.org/html/2611.14975v1#S4.SS5)
- **Linear probe** — 以 logistic regression 對決策 token 的 hidden state 預測氣胸有無，依病人分組做 5 折交叉驗證，報告最後一層的 AUC 與病人層級 bootstrap 95% CI；也對每一層跑同樣的 probe。[(ref: main §4.6)](https://arxiv.org/html/2611.14975v1#S4.SS6)
- **論文未交代** — 另外三種提示（bare question、forced one-word answer、clinical persona）的完整措辭；probe 的正則化與特徵前處理設定。[(ref: main §4.2)](https://arxiv.org/html/2611.14975v1#S4.SS2) [(ref: main §4.6)](https://arxiv.org/html/2611.14975v1#S4.SS6)
- **論文未交代** — 胸管（drain）有無是由 MedGemma 與 Qwen 判讀，沒有人工標註；drain-free 子集（n=92）因此也是模型標註。[(ref: main §4.3)](https://arxiv.org/html/2611.14975v1#S4.SS3) [(ref: main Table 5)](https://arxiv.org/html/2611.14975v1#S4.T5)
- **論文未交代** — 程式、題目清單與產生腳本都不釋出；人口學檢定只寫結論（校正多重比較後無性別或年齡差異）與方法（2,000 次 bootstrap、對 16 個檢定做 Benjamini–Hochberg、80% 檢定力下最小可偵測差異 0.051），沒有逐組數值。[(ref: main §5)](https://arxiv.org/html/2611.14975v1#S5) [(ref: main Checklist)](https://arxiv.org/html/2611.14975v1#Sx1)

## 資料與實驗

### 資料

| 項目 | ChestX-ray14（主評估） | SIIM-ACR Pneumothorax（外部重現） |
|---|---|---|
| 標籤來源 | 由放射報告以 NLP 抽取，非逐張影像核對 | 放射科醫師逐像素繪製的氣胸遮罩 |
| 評估題數 | 6,048 題（84 格 × 72 張），來自 4,054 位病人 | 864 張（432 陽性、432 陰性） |
| 徵象 | Atelectasis、Cardiomegaly、Effusion、Infiltration、Mass、Nodule、Pneumothorax | 只有 Pneumothorax |
| 人口學平衡 | 性別 × 三個年齡帶，各格徵象與標籤分布相同 | 無年齡、性別與姿勢欄位 |
| 備註 | 部分氣胸陽性影像為引流後、仍見胸管 | 遮罩面積中位數只佔影像 0.8% |
| 授權 | CC0 | Kaggle 競賽資料條款 |

[(ref: main §2)](https://arxiv.org/html/2611.14975v1#S2) [(ref: main §3.1)](https://arxiv.org/html/2611.14975v1#S3.SS1) [(ref: main §3.2)](https://arxiv.org/html/2611.14975v1#S3.SS2) [(ref: main §4.3)](https://arxiv.org/html/2611.14975v1#S4.SS3) [(ref: main Checklist)](https://arxiv.org/html/2611.14975v1#Sx1)

### 實驗

預設提示下 6,048 題的整體表現，節錄自 Table 1（機率水準為 0.500；Tokens 為平均回答長度）：

| Model | Yes rate | Accuracy | Grounding | Tokens |
|---|---|---|---|---|
| MedGemma-4B | 0.423 | 0.698 | 0.418 | 37.6 |
| Lingshu-7B | 0.488 | 0.620 | 0.457 | 39.9 |
| HuatuoGPT-7B | 0.147 | 0.534 | 0.091 | 54.6 |
| Qwen2.5-VL-7B | 0.089 | 0.518 | 0.075 | 62.6 |
| MedVLM-R1 | 0.014 | 0.502 | — | 02.0 |

[(ref: main Table 1)](https://arxiv.org/html/2611.14975v1#S4.T1)

每種徵象 432 張陽性影像的 recall，節錄自 Table 2：

| Finding | MedGemma | Lingshu | HuatuoGPT | Qwen |
|---|---|---|---|---|
| Atelectasis | 0.947 | 0.632 | 0.484 | 0.019 |
| Cardiomegaly | 0.738 | 0.512 | 0.123 | 0.292 |
| Effusion | 0.787 | 0.701 | 0.007 | 0.000 |
| Infiltration | 0.604 | 0.586 | 0.641 | 0.400 |
| Mass | 0.461 | 0.616 | 0.007 | 0.030 |
| Nodule | 0.433 | 0.539 | 0.002 | 0.012 |
| Pneumothorax | 0.377 | 0.671 | 0.000 | 0.000 |

[(ref: main Table 2)](https://arxiv.org/html/2611.14975v1#S4.T2)

SIIM-ACR 的氣胸重現，節錄自 Table 3（432 陽性、432 陰性；Small／Mid／Large 為依遮罩面積分的三組，各 144 張）：

| Model | Recall | FP | Bal. acc. | Small | Mid | Large | Grounding |
|---|---|---|---|---|---|---|---|
| Lingshu-7B | 0.861 | 0.250 | 0.806 | 0.847 | 0.903 | 0.833 | 0.613 |
| MedGemma-4B | 0.470 | 0.049 | 0.711 | 0.396 | 0.465 | 0.549 | 0.396 |
| HuatuoGPT-7B | 0.000 | 0.000 | 0.500 | 0.000 | 0.000 | 0.000 | — |
| Qwen2.5-VL-7B | 0.000 | 0.000 | 0.500 | 0.000 | 0.000 | 0.000 | — |
| MedVLM-R1 | 0.000 | 0.000 | 0.500 | 0.000 | 0.000 | 0.000 | — |

[(ref: main Table 3)](https://arxiv.org/html/2611.14975v1#S4.T3)

氣胸的決策信心，節錄自 Table 4（P(Yes)⁺ 與 Margin⁺ 只算 432 張陽性；其餘欄用全部 864 例）：

| Model | P(Yes)⁺ | Margin⁺ | Margin-AUROC | Mean conf. | Accuracy | ECE |
|---|---|---|---|---|---|---|
| MedGemma-4B | 0.368 | −3.19 | 0.795 | 0.992 | 0.663 | 0.329 |
| Lingshu-7B | 0.715 | +1.41 | 0.841 | 0.841 | 0.767 | 0.074 |
| HuatuoGPT-7B | 0.253 | −1.10 | 0.641 | 0.759 | 0.500 | 0.259 |
| Qwen2.5-VL-7B | 0.026 | −3.91 | 0.586 | 0.976 | 0.500 | 0.476 |

[(ref: main Table 4)](https://arxiv.org/html/2611.14975v1#S4.T4)

決策 token hidden state 的氣胸 linear probe AUC，節錄自 Table 5（最後一層、病人分組 5 折；方括號為病人層級 bootstrap 95% CI；Drain-free 為 ChestX-ray14 中無胸管的陽性，n=92；Nodule 為同模型對照）：

| Model | ChestX-ray14 | Drain-free | SIIM-ACR | Nodule |
|---|---|---|---|---|
| MedGemma-4B | 0.819 [.791, .848] | 0.631 | 0.891 [.869, .912]† | 0.684 |
| Lingshu-7B | 0.786 [.752, .817] | 0.598 | 0.851 [.826, .876] | 0.619 |
| HuatuoGPT-7B | 0.613 [.574, .650] | 0.411 | 0.746 [.713, .778] | 0.543 |
| Qwen2.5-VL-7B | 0.545 [.507, .583] | 0.421 | 0.716 [.683, .751] | 0.549 |

† MedGemma 主幹不同，SIIM-ACR 的 AUC 不能直接和 Qwen 系列比較。[(ref: main Table 5)](https://arxiv.org/html/2611.14975v1#S4.T5)

## 結果

- **整體分數最高的模型也有盲點** — MedGemma-4B 整體準確率 0.698 居首，但 atelectasis 的 0.947 recall 只配上 0.317 specificity，等於把約 68% 的陰性判成有病，該徵象 balanced accuracy 只有 0.632；Lingshu 是唯一七種徵象 balanced accuracy 都高於 0.590 的模型。[(ref: main §4.1)](https://arxiv.org/html/2611.14975v1#S4.SS1)
- **失效集中在特定徵象** — Qwen2.5-VL-7B 對 effusion 與 pneumothorax 都是 0/432，HuatuoGPT-Vision-7B 的 pneumothorax 0、effusion 3、mass 3、nodule 1；但兩者在 infiltration 分別抓到 40% 與 64%，所以不是全面失明。[(ref: main §4.1)](https://arxiv.org/html/2611.14975v1#S4.SS1)
- **換提示救不回來** — 四種提示下，Qwen 的氣胸 recall 都是 0.000（四種提示合計 1,728 次陽性提問沒有一次答「有」）；HuatuoGPT 在 forced 提示下 nodule recall 79.2%、effusion 69.4%，氣胸只有 6.2%，氣胸的 balanced accuracy 在四種提示下都落在 0.500–0.512。[(ref: main §4.2)](https://arxiv.org/html/2611.14975v1#S4.SS2)
- **解析度、多標籤與規模都不是主因** — 原生 1024 像素下 Qwen 仍是 0/100；210 張只有氣胸標籤的影像，Qwen 與 HuatuoGPT 一張未抓，MedGemma 與 Lingshu 抓到 35.2% 與 60.0%；兩個失效模型辨認「這是胸片」「有肋骨」都是 100%。Qwen2.5-VL 從 7B 放大到 72B（AWQ 4-bit），氣胸 recall 只從 0.000 升到 0.044（19/432），但 72B 的 cardiomegaly 偵測為 0.631、整體 balanced accuracy 0.560，作者據此認為 72B 本身並未故障；MedGemma 從 4B 到 27B 則由 0.377 升到 0.565。[(ref: main §4.3)](https://arxiv.org/html/2611.14975v1#S4.SS3)
- **換成醫師遮罩仍重現** — 在 SIIM-ACR 上，HuatuoGPT、Qwen 與 MedVLM-R1 對 432 例確認氣胸都是 0，連面積最大的 144 例也是 0；Lingshu 與 MedGemma 為 0.861 與 0.470，MedGemma 的 recall 隨病灶變大由 0.396 升到 0.549。[(ref: main §4.4)](https://arxiv.org/html/2611.14975v1#S4.SS4)
- **有把握地答錯，而非猶豫** — Qwen 在氣胸陽性上的 P(Yes) 只有 0.026、margin −3.91，是七種徵象中最低；它對答案的平均信心 97.6%，準確率卻只有 50.0%（ECE 0.476）。但以 margin 排序時 AUROC 為 0.586，高於機率水準：分數裡仍有訊號，只是門檻永遠落在「No」。[(ref: main §4.5)](https://arxiv.org/html/2611.14975v1#S4.SS5)
- **內部表徵解得出氣胸** — 在 SIIM-ACR 上，兩個 recall 約為 0 的模型 probe AUC 仍有 0.716（Qwen）與 0.746（HuatuoGPT）；逐層 probe 顯示失效模型的氣胸訊號在早期層最明顯（Qwen 為第 1 層）、往輸出逐漸消退，可運作的模型則在後段層最強。作者解讀為「表徵較弱，加上在輸出端被壓下」。[(ref: main §4.6)](https://arxiv.org/html/2611.14975v1#S4.SS6)
- **胸管只部分解釋 probe** — ChestX-ray14 的氣胸陽性中，MedGemma 與 Qwen 對 150 張陽性判出胸管的比例為 54.0% 與 52.7%；只看無胸管的陽性時 probe AUC 全面下降（Lingshu 0.786→0.598），但把胸管方向從特徵中投影掉，AUC 最多只變 0.067。作者因此以 SIIM-ACR 為決定性測試。[(ref: main §4.3)](https://arxiv.org/html/2611.14975v1#S4.SS3) [(ref: main §4.6)](https://arxiv.org/html/2611.14975v1#S4.SS6)
- **輸出文字看不出問題** — 作者抽看 10 例陽性，10 例都以「No」開頭，並給出「lung fields are well-expanded」之類具體的解剖描述，沒有拒答或保留語氣。[(ref: main §4.2)](https://arxiv.org/html/2611.14975v1#S4.SS2) [(ref: main Figure 1)](https://arxiv.org/html/2611.14975v1#S4.F1)

## 限制

- **標籤雜訊** — ChestX-ray14 的標籤由報告以 NLP 抽取；SIIM-ACR 只涵蓋氣胸、沒有人口學欄位，因此每種徵象與人口學的結論只建立在 ChestX-ray14 上。部分 ChestX-ray14 氣胸陽性是引流後影像，會影響絕對 recall，但作者指出同一批影像上模型之間的差距仍在。[(ref: main §4.3)](https://arxiv.org/html/2611.14975v1#S4.SS3) [(ref: main §5)](https://arxiv.org/html/2611.14975v1#S5)
- **只問是非題** — 研究沒有讓模型寫自由格式報告；信心與 probe 分析只做氣胸一種徵象。[(ref: main §5)](https://arxiv.org/html/2611.14975v1#S5)
- **Probe 的意義有限** — probe 只證明資訊可從 hidden state 解碼，不證明模型在決策時使用它；作者找到訊號在哪裡消退，但沒有找到原因，也沒有測試在輸出端介入能否救回偵測。[(ref: main §5)](https://arxiv.org/html/2611.14975v1#S5) [(ref: main §6)](https://arxiv.org/html/2611.14975v1#S6)
- **可運作的模型也不可靠** — 作者自己指出視覺對照顯示 MedGemma 與 Lingshu 並非處處可靠；MedGemma 的氣胸平均信心 99.2% 而準確率 66.3%（ECE 0.329）。[(ref: main §4.5)](https://arxiv.org/html/2611.14975v1#S4.SS5) [(ref: main §5)](https://arxiv.org/html/2611.14975v1#S5)
- **重現與揭露** — 程式與題目清單不釋出；三種替代提示的措辭、probe 設定未完整列出；胸管標註來自模型；人口學檢定沒有數值表；MedVLM-R1 因輸出退化（98.6% 答 no、沒有產生推理軌跡）被排除在逐徵象分析之外。[(ref: main §4.1)](https://arxiv.org/html/2611.14975v1#S4.SS1) [(ref: main Checklist)](https://arxiv.org/html/2611.14975v1#Sx1)
- **本書庫的判讀** — 結果說明的是「這五個公開 checkpoint 在這套是非題協定下」的行為，作者也提醒絕對 recall 不應讀成臨床表現；Qwen2.5-VL-7B 是未經醫療微調的通用模型，HuatuoGPT-Vision 只測了一個 checkpoint，不宜推論到同名系列的其他版本。[(ref: main §3.4)](https://arxiv.org/html/2611.14975v1#S3.SS4) [(ref: main Checklist)](https://arxiv.org/html/2611.14975v1#Sx1)

## 與書庫其他文章的關係

Lingshu 原論文以醫療 VQA 平均分數呈現能力，本篇則在同一個 Qwen2.5-VL-7B 主幹上逐徵象比較，Lingshu-7B 在兩個資料集抓到 67% 與 86% 的氣胸，而未微調主幹與 HuatuoGPT-Vision 一例未抓: [Lingshu 靠合成資料拉高醫療 VQA，強化學習那一步沒加分](2026-09-15-lingshu-medical-vlm.md)

ModaLens 以交換影像與 yes/no logit margin 量測 MedGemma 在有報告時是否仍看影像，本篇用同類的換病人影像與 margin 分析，問的是模型會不會整個漏掉單一徵象: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎](2026-09-17-modalens-image-sensitivity.md)

胸片結核稽核改換提示詞、負類與閾值，檢查醫療 VLM 的結論是否站得住；本篇同樣換提示與解析度，發現氣胸失效在四種提示下都沒有改變: [換一個評估條件，胸片結核 VLM 的結論還剩幾條站得住](2026-09-21-cxr-tb-vlm-portability-audit.md)

本篇在胸片是非題上發現兩個模型對氣胸陽性一律答「沒有」；乳房攝影一致性稽核同樣測 MedGemma-4B 與 Lingshu-7B，改在選擇題中加入 NOTA 選項，發現影像被拿掉後 MedGemma 仍以約 95 分信心給出 BI-RADS 類別: [拿掉乳房攝影影像，MedGemma 仍以約 95 分信心給 BI-RADS](2026-11-16-mammography-vlm-cross-signal-coherence.md)

## 實務的啟發

1. **評估醫療 VLM 時，逐徵象報 recall 與 specificity。** 作者的主要建議是在平衡的病例上逐一列出每個徵象的表現；Table 2 顯示，整體分數無法區分「每個徵象都普通」和「某個徵象完全為零」。[(ref: main §6)](https://arxiv.org/html/2611.14975v1#S6)
2. **把「一律答 no」當成需要排除的基線。** 在一半陽性的題組上，balanced accuracy 正好 0.500、yes rate 遠低於 0.5 就是警訊；Table 1 的 yes rate 一欄已經透露 Qwen 與 HuatuoGPT 的問題。[(ref: main Table 1)](https://arxiv.org/html/2611.14975v1#S4.T1)
3. **不要以解釋文字的流暢度判斷答案可信。** 失效模型會描述正確的徵象再否認它；本書庫認為，若院內評估包含醫師讀模型理由，應另外以真陽性病例確認模型實際的偵測率。[(ref: main §4.2)](https://arxiv.org/html/2611.14975v1#S4.SS2)
4. **選型時對高風險徵象做外部重現。** 本篇用有醫師遮罩的 SIIM-ACR 排除標籤雜訊，並同時檢查提示與規模；這套排除程序可借用，但「在輸出端介入就能救回偵測」仍是作者待驗證的假設，不是已證實的修正方法。[(ref: main §4.4)](https://arxiv.org/html/2611.14975v1#S4.SS4) [(ref: main §6)](https://arxiv.org/html/2611.14975v1#S6)

## References

- `main` — Kale SA, Bajwa ARS. *Aggregate Accuracy Hides Diagnosis-Specific Failure in Medical Vision-Language Models*. arXiv:2611.14975v1, 2026. [https://arxiv.org/html/2611.14975v1](https://arxiv.org/html/2611.14975v1)
  - 深鏈：[author block](https://arxiv.org/html/2611.14975v1)、[§1](https://arxiv.org/html/2611.14975v1#S1)、[§2](https://arxiv.org/html/2611.14975v1#S2)、[§3](https://arxiv.org/html/2611.14975v1#S3)、[§3.1](https://arxiv.org/html/2611.14975v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.14975v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.14975v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.14975v1#S3.SS4)、[§3.5](https://arxiv.org/html/2611.14975v1#S3.SS5)、[§4](https://arxiv.org/html/2611.14975v1#S4)、[§4.1](https://arxiv.org/html/2611.14975v1#S4.SS1)、[Figure 1](https://arxiv.org/html/2611.14975v1#S4.F1)、[Table 1](https://arxiv.org/html/2611.14975v1#S4.T1)、[Table 2](https://arxiv.org/html/2611.14975v1#S4.T2)、[§4.2](https://arxiv.org/html/2611.14975v1#S4.SS2)、[§4.3](https://arxiv.org/html/2611.14975v1#S4.SS3)、[§4.4](https://arxiv.org/html/2611.14975v1#S4.SS4)、[Table 3](https://arxiv.org/html/2611.14975v1#S4.T3)、[§4.5](https://arxiv.org/html/2611.14975v1#S4.SS5)、[Table 4](https://arxiv.org/html/2611.14975v1#S4.T4)、[§4.6](https://arxiv.org/html/2611.14975v1#S4.SS6)、[Table 5](https://arxiv.org/html/2611.14975v1#S4.T5)、[§5](https://arxiv.org/html/2611.14975v1#S5)、[§6](https://arxiv.org/html/2611.14975v1#S6)、[Checklist](https://arxiv.org/html/2611.14975v1#Sx1)
- `abstract` — arXiv abstract page, 2611.14975v1. [https://arxiv.org/abs/2611.14975v1](https://arxiv.org/abs/2611.14975v1)
- PDF v1：[https://arxiv.org/pdf/2611.14975v1](https://arxiv.org/pdf/2611.14975v1)
- DOI：[https://doi.org/10.48550/arXiv.2611.14975](https://doi.org/10.48550/arXiv.2611.14975)

[Home](../) · [AI Papers](./)
