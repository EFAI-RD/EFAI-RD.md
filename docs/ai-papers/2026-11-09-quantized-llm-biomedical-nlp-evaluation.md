---
parent: AI Papers
nav_order: 4
title: "生醫 LLM 量化：4-bit 省約 68% 記憶體，8-bit 反而最慢"
catalog_id: "doi:10.1038/s44401-026-00152-6"
editors:
  - "Clare"
refs:
  main:
    title: "Quantized large language models in biomedical natural language processing: evaluation and recommendation"
    url: "https://www.nature.com/articles/s44401-026-00152-6"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 生醫 LLM 量化：4-bit 省約 68% 記憶體，8-bit 反而最慢

## 來源

- 團隊：University of Minnesota（Minneapolis）Department of Surgery 的 Division of Computational Health Sciences、Department of Electrical and Computer Engineering 與 School of Nursing，共 10 位作者；第一作者 Zaifu Zhan，通訊作者 Rui Zhang。[(ref: main author information)](https://www.nature.com/articles/s44401-026-00152-6)
- 論文：*Quantized large language models in biomedical natural language processing: evaluation and recommendation*，npj Health Systems 3, 104（2026），2026-04-06 投稿、2026-08-24 接受、2026-11-04 線上刊出，open access，授權 CC BY 4.0。[(ref: main)](https://www.nature.com/articles/s44401-026-00152-6) [(ref: main PDF p.8)](https://www.nature.com/articles/s44401-026-00152-6.pdf#page=8)
- 識別碼：DOI [10.1038/s44401-026-00152-6](https://doi.org/10.1038/s44401-026-00152-6)。
- 全文：[出版社全文頁](https://www.nature.com/articles/s44401-026-00152-6)、[PDF](https://www.nature.com/articles/s44401-026-00152-6.pdf)。
- 資料與程式：程式碼公開於 [GitHub](https://github.com/Learner4everrr/Benchmark_quantization)，資料集依循先前的生醫 LLM 基準研究、置於 [Zenodo](https://doi.org/10.5281/zenodo.14025500)。[(ref: main PDF p.8, Data availability; Code availability)](https://www.nature.com/articles/s44401-026-00152-6.pdf#page=8)
- 研究性質：完整的離線基準評估，不是 pilot；所有量化設定都實際執行，以同一模型的全精度版本為對照，涵蓋 12 個 LLM、8 個公開資料集（測試規模 315–16,943 筆）。論文表格只給點估計，沒有印出信賴區間；Methods 提到以 nonparametric bootstrap 檢查輸出層級的變異，Fig. 2 的誤差線則是跨資料集的 SD。未在臨床資料上前瞻驗證。[(ref: main Methods; Table 6; Fig. 2)](https://www.nature.com/articles/s44401-026-00152-6#Tab6)
- 證據邊界：本文數值以 PDF 版的 Table 1–6 與正文為準；Fig. 3–6 的長條與曲線數值、Fig. 7 的建議圖內容沒有以文字提供，本文只引用論文正文對這些圖的文字描述。

**編輯：** Clare

作者在 4 項生醫 NLP 任務、8 個資料集上比較 12 個 LLM 的全精度、8-bit 與 4-bit（BitsAndBytes）版本：4-bit 平均只用全精度約 32% 的峰值 GPU 記憶體、各任務平均分數變化在 0.015 以內，8-bit 卻省得較少、延遲是全精度的 2.2–2.9 倍，且分數變化較大，例如 Llama-3.3-70B 的 MedQA 準確率從 0.732 掉到 0.555。[(ref: main Table 1; Table 2)](https://www.nature.com/articles/s44401-026-00152-6#Tab2)

## 流程

![量化 LLM 生醫 NLP 評估的研究設計示意圖。共五個圓角方塊，排成三欄：左上藍色方塊「1. Eight benchmark datasets」列出四類任務與資料集大小——Multi-label classification 的 HoC (315)、LitCovid (2500)，NER 的 BC5CDR-chemical (4797)、NCBI-disease (940)，Relation extraction 的 ChemProt (16,943)、DDI2013 (5761)，QA 的 MedQA-USMLE (1273)、PubMedQA (500)，以及指標 macro F1／entity-level F1／accuracy；左下紫色方塊「2. Twelve LLMs」列出四個通用模型（Llama-3.3-70B、Qwen2.5-72B、Phi-4、DeepSeek-LLM-67B）、四個領域模型（ClinicalCamel-70B、Llama3-Med42-70B、HuatuoGPT-o1-70B、Meditron-70B）與 Qwen2.5 3B／7B／14B／32B／72B 的規模比較；中上綠色方塊「3a. Main matrix (Transformers)」列出 4 張 NVIDIA A100 40 GB 上的 BitsAndBytes、Full precision 對 W8A16（預設 8-bit）對 W4A16（NF4、fp16 compute、double quantization），以及 instruction prompt、few-shot（0/1/5/10）與 Qwen2.5-72B 的 CoT／self-consistency；中下綠色方塊「3b. Serving check (vLLM)」列出 AWQ／GPTQ／FP8 checkpoint、Qwen2.5-7B 與 32B、DDI2013／HoC／MedQA／NCBI Disease 四個資料集、batched offline inference 量測分數與 tok/s，並註明記憶體不與 3a 比較；右側一個縱跨全高的橘色方塊「4. Measured outputs」列出任務分數、峰值 GPU 記憶體（GB）、CUDA 同步計時的延遲、生成 token 吞吐量、以任務專用 parser 判定的 invalid-output 與 repetition rate、相對全精度的任務層級比值，以及相對 instruction prompt 的 token 與延遲比值。共四條實線箭頭：藍色方塊指向 3a、紫色方塊指向 3a、3a 指向橘色方塊、3b 指向橘色方塊；3b 沒有來自左欄的箭頭](assets/quantized-llm-biomedical-nlp-design.png)

圖：本書庫依論文 Methods 與 Table 6 的文字重繪的研究設計示意圖，只含設計層級的資訊與資料集大小，不含結果數值，未複製論文原圖（論文 Fig. 1 為一般 LLM 與量化版本的比較示意，Fig. 7 為使用建議）。[(ref: main Methods; Table 6; Fig. 1)](https://www.nature.com/articles/s44401-026-00152-6#Fig1)

## 背景／問題

作者的出發點是：病人資料的保密與資安要求限制了雲端 LLM 的使用，醫療場域常需要在本地推論，而 70B 等級的模型需要大量 GPU 記憶體；量化（把權重從 16-bit 壓到 8-bit 或 4-bit）是降低記憶體的常見手段，但它在生醫 NLP 任務上的影響，作者認為還「largely unexplored」。這些動機在 Introduction 都附有文獻引用（運算需求、隱私與雲端資安、在較弱硬體上執行量化模型等），本研究本身沒有量測本地部署的隱私效益。[(ref: main Introduction)](https://www.nature.com/articles/s44401-026-00152-6)

因此本文把「醫院需要本地部署」視為作者引用文獻支持的情境，論文實際檢驗的是另一件事：在固定的資料集與硬體上，量化會讓分數、峰值記憶體、延遲與輸出有效性各改變多少。[(ref: main Introduction; Methods)](https://www.nature.com/articles/s44401-026-00152-6)

## 方法摘要

**任務與資料。** 依先前的生醫 LLM 基準研究（Chen 等，Nat Commun 2025）挑選 4 類任務、8 個公開資料集：multi-label classification（HoC、LitCovid）、named entity recognition（BC5CDR-chemical、NCBI-disease）、relation extraction（ChemProt、DDI2013）與 question answering（MedQA-USMLE、PubMedQA）。指標為 macro F1（分類、關係抽取）、entity-level F1（NER）與 accuracy（QA）。[(ref: main Methods, Datasets; Table 6)](https://www.nature.com/articles/s44401-026-00152-6#Tab6)

**模型。** 通用模型 Llama-3.3-70B、Qwen2.5-72B、Phi-4、DeepSeek-LLM-67B；生醫領域模型 ClinicalCamel-70B、Llama3-Med42-70B、HuatuoGPT-o1-70B、Meditron-70B；另以 Qwen2.5 3B、7B、14B、32B、72B 看模型大小的效應，合計 12 個不同模型。[(ref: main Methods, LLMs)](https://www.nature.com/articles/s44401-026-00152-6)

**量化設定。** 主實驗在 Hugging Face Transformers 上以 BitsAndBytes 載入：W8A16 使用預設 8-bit 設定；W4A16 使用 NF4、float16 compute type 與 double quantization。另以 vLLM 對 Qwen2.5-7B／32B 測 AWQ、GPTQ、FP8 三種預先量化的 checkpoint，作為 serving 情境的補充。[(ref: main Methods, Quantization setup; Table 4)](https://www.nature.com/articles/s44401-026-00152-6#Tab4)

**量測項目。** 每個「模型 × 資料集 × 精度」組合記錄任務分數、峰值 GPU 記憶體（GB）、延遲（秒）與生成 token 吞吐量，並以任務專用 parser 標記無效輸出與重複輸出。[(ref: main Methods, Latency, output validity, and statistical analysis; Table 1)](https://www.nature.com/articles/s44401-026-00152-6#Tab1)

## 方法詳解

**提示方式。** 主實驗用 instruction prompt（描述任務、輸出格式與輸入）。另在 Qwen2.5-72B 上比較 0、1、5、10 個範例的 few-shot，以及 chain-of-thought（CoT）與 self-consistency 兩種提示。[(ref: main Methods, Prompt methods; Fig. 5; Fig. 6)](https://www.nature.com/articles/s44401-026-00152-6#Fig5)

**生成長度與其他參數。** 輸出長度依任務調整：分類任務約 50 個 token、NER 最多 200 個 token；其餘參數沿用 Hugging Face 的預設值。[(ref: main Methods, Experimental settings)](https://www.nature.com/articles/s44401-026-00152-6)

**硬體與計時。** 主要在 4 張 NVIDIA A100（各 40 GB）上執行。Transformers 實驗在生成前後做 CUDA 同步來量延遲，吞吐量以生成 token 總數除以實際經過時間；vLLM 以 batched offline inference 執行。作者說明 vLLM 會預先保留記憶體，與 PyTorch 的峰值配置不能直接比較，所以 vLLM 結果只報分數與吞吐量。[(ref: main Methods, Experimental settings; Latency, output validity, and statistical analysis; Table 4)](https://www.nature.com/articles/s44401-026-00152-6#Tab4)

**輸出有效性。** 在計算指標之前，以任務專用 parser 把空白或無法解析的輸出標為 invalid，並以輕量的重複掃描標記 repetition。[(ref: main Methods; Table 3)](https://www.nature.com/articles/s44401-026-00152-6#Tab3)

- **論文未交代** — 每個模型與量化版本使用的 Hugging Face checkpoint ID，以及 AWQ、GPTQ、FP8 checkpoint 的來源與校準資料。
- **論文未交代** — 函式庫版本（transformers、bitsandbytes、vLLM、CUDA）、每次執行用幾張 GPU 與如何切分模型。
- **論文未交代** — 完整 prompt 模板、解碼方式（greedy 或 sampling、溫度、top-p）、self-consistency 的取樣次數，以及「約 50」「最多 200」以外的生成長度上限。
- **論文未交代** — 延遲量測的 batch size 與重複次數、各結果是否為單次執行，以及 bootstrap 的重抽次數與信賴水準；表格沒有印出任何信賴區間。
- **論文未交代** — invalid 與 repetition 的判定門檻；Table 2 的 Δ 與比值由哪些模型組合彙總（論文只說取自原始實驗矩陣）。

## 資料與實驗

下表摘錄論文 Table 6 的資料集與指標。[(ref: main Table 6)](https://www.nature.com/articles/s44401-026-00152-6#Tab6)

| Task | Dataset | Size | Metric |
|---|---|---|---|
| Multi-label classification | HoC | 315 | Macro F1 |
| Multi-label classification | LitCovid | 2500 | Macro F1 |
| Named entity recognition | BC5CDR-chemical | 4797 | Entity-level F1 |
| Named entity recognition | NCBI-disease | 940 | Entity-level F1 |
| Relation extraction | ChemProt | 16,943 | Macro F1 |
| Relation extraction | DDI2013 | 5761 | Macro F1 |
| Question answering | MedQA-USMLE | 1273 | Accuracy |
| Question answering | PubMedQA | 500 | Accuracy |

下表為論文 Table 1：四個通用模型在全精度、W8A16、W4A16 下的峰值記憶體（Mem，GB）、延遲（Late，秒）與分數（Score，依資料集為 F1 或 accuracy）。[(ref: main Table 1)](https://www.nature.com/articles/s44401-026-00152-6#Tab1)

| Dataset / Metric | Model | FP Mem | FP Late | FP Score | W8A16 Mem | W8A16 Late | W8A16 Score | W4A16 Mem | W4A16 Late | W4A16 Score |
|---|---|---|---|---|---|---|---|---|---|---|
| HoC / Macro F1 | DeepSeek-LLM-67B | 126.5 | 4.57 | 0.391 | 65.61 | 10.4 | 0.404 | 36.87 | 6.84 | 0.377 |
| HoC / Macro F1 | Llama-3.3-70B | 132.37 | 3.74 | 0.45 | 68.85 | 11.4 | 0.343 | 39.38 | 4.87 | 0.419 |
| HoC / Macro F1 | Phi-4 | 28.41 | 1.05 | 0.459 | 16.08 | 2.27 | 0.458 | 10.72 | 1.45 | 0.487 |
| HoC / Macro F1 | Qwen2.5-72B | 136.41 | 2.75 | 0.576 | 72.58 | 6.83 | 0.581 | 41.0 | 3.48 | 0.573 |
| LitCovid / Macro F1 | DeepSeek-LLM-67B | 127.15 | 1.96 | 0.444 | 66.37 | 4.73 | 0.452 | 37.41 | 2.36 | 0.456 |
| LitCovid / Macro F1 | Llama-3.3-70B | 133.08 | 1.47 | 0.481 | 69.7 | 3.55 | 0.41 | 39.95 | 2.0 | 0.452 |
| LitCovid / Macro F1 | Phi-4 | 29.2 | 0.47 | 0.461 | 16.91 | 1.02 | 0.462 | 11.36 | 0.67 | 0.465 |
| LitCovid / Macro F1 | Qwen2.5-72B | 137.13 | 1.27 | 0.546 | 73.46 | 2.97 | 0.548 | 41.6 | 1.67 | 0.553 |
| BC5CDR-chemical / Entity F1 | DeepSeek-LLM-67B | 125.97 | 6.48 | 0.547 | 64.92 | 16.58 | 0.547 | 36.41 | 8.95 | 0.552 |
| BC5CDR-chemical / Entity F1 | Llama-3.3-70B | 131.87 | 6.52 | 0.734 | 68.21 | 15.77 | 0.668 | 38.94 | 7.15 | 0.7 |
| BC5CDR-chemical / Entity F1 | Phi-4 | 27.78 | 1.97 | 0.656 | 15.23 | 4.66 | 0.663 | 10.23 | 2.82 | 0.653 |
| BC5CDR-chemical / Entity F1 | Qwen2.5-72B | 135.87 | 6.8 | 0.842 | 71.62 | 17.79 | 0.828 | 40.56 | 7.73 | 0.833 |
| NCBI Disease / Entity F1 | DeepSeek-LLM-67B | 125.89 | 6.22 | 0.279 | 64.82 | 15.95 | 0.275 | 36.34 | 9.09 | 0.282 |
| NCBI Disease / Entity F1 | Llama-3.3-70B | 131.77 | 6.52 | 0.469 | 68.12 | 17.31 | 0.488 | 38.88 | 7.56 | 0.486 |
| NCBI Disease / Entity F1 | Phi-4 | 27.68 | 1.96 | 0.332 | 15.1 | 4.74 | 0.336 | 10.16 | 2.93 | 0.372 |
| NCBI Disease / Entity F1 | Qwen2.5-72B | 135.78 | 6.94 | 0.413 | 71.49 | 18.76 | 0.402 | 40.49 | 7.86 | 0.357 |
| ChemProt / Macro F1 | DeepSeek-LLM-67B | 126.43 | 1.01 | 0.324 | 65.54 | 2.52 | 0.334 | 36.81 | 1.52 | 0.294 |
| ChemProt / Macro F1 | Llama-3.3-70B | 132.3 | 0.82 | 0.249 | 68.73 | 1.64 | 0.181 | 39.3 | 1.09 | 0.243 |
| ChemProt / Macro F1 | Phi-4 | 28.27 | 0.37 | 0.336 | 15.82 | 0.62 | 0.338 | 10.62 | 0.37 | 0.305 |
| ChemProt / Macro F1 | Qwen2.5-72B | 136.33 | 0.74 | 0.435 | 72.53 | 1.67 | 0.427 | 40.95 | 1.03 | 0.446 |
| DDI2013 / Macro F1 | DeepSeek-LLM-67B | 126.19 | 0.87 | 0.464 | 65.29 | 2.03 | 0.452 | 36.65 | 1.3 | 0.432 |
| DDI2013 / Macro F1 | Llama-3.3-70B | 132.03 | 0.83 | 0.524 | 68.48 | 1.51 | 0.45 | 39.14 | 1.12 | 0.51 |
| DDI2013 / Macro F1 | Phi-4 | 28.03 | 0.25 | 0.56 | 15.59 | 0.5 | 0.562 | 10.43 | 0.38 | 0.557 |
| DDI2013 / Macro F1 | Qwen2.5-72B | 136.09 | 0.82 | 0.552 | 72.24 | 1.86 | 0.55 | 40.78 | 1.18 | 0.553 |
| MedQA / Accuracy | DeepSeek-LLM-67B | 126.75 | 0.75 | 0.441 | 65.89 | 1.77 | 0.445 | 37.08 | 1.07 | 0.416 |
| MedQA / Accuracy | Llama-3.3-70B | 132.63 | 0.5 | 0.732 | 69.15 | 0.88 | 0.555 | 39.58 | 0.77 | 0.705 |
| MedQA / Accuracy | Phi-4 | 28.67 | 0.25 | 0.648 | 16.29 | 0.53 | 0.64 | 10.94 | 0.39 | 0.628 |
| MedQA / Accuracy | Qwen2.5-72B | 136.7 | 0.45 | 0.71 | 72.76 | 0.92 | 0.709 | 41.26 | 0.73 | 0.704 |
| PubMedQA / Accuracy | DeepSeek-LLM-67B | 126.44 | 0.7 | 0.166 | 65.5 | 1.58 | 0.146 | 36.82 | 1.1 | 0.118 |
| PubMedQA / Accuracy | Llama-3.3-70B | 132.34 | 0.63 | 0.706 | 68.78 | 1.07 | 0.758 | 39.33 | 0.89 | 0.756 |
| PubMedQA / Accuracy | Phi-4 | 28.31 | 0.2 | 0.61 | 15.87 | 0.4 | 0.532 | 10.66 | 0.34 | 0.602 |
| PubMedQA / Accuracy | Qwen2.5-72B | 136.37 | 0.48 | 0.616 | 72.46 | 0.92 | 0.614 | 40.97 | 0.8 | 0.628 |

下表為論文 Table 2：BitsAndBytes 量化相對全精度的任務層級變化（MLC = multi-label classification，RE = relation extraction）；Δ 為分數變化，記憶體與延遲為相對全精度的比值，記憶體比值越低代表省得越多。[(ref: main Table 2)](https://www.nature.com/articles/s44401-026-00152-6#Tab2)

| Task | Quant. | Mean Δ | Median Δ | Mem. ratio | Lat. ratio |
|---|---|---|---|---|---|
| MLC | 4bit | −0.011 | −0.010 | 0.320 | 1.312 |
| MLC | 8bit | −0.032 | −0.001 | 0.544 | 2.647 |
| NER | 4bit | −0.015 | −0.010 | 0.316 | 1.338 |
| NER | 8bit | −0.054 | −0.008 | 0.534 | 2.864 |
| QA | 4bit | −0.001 | −0.011 | 0.325 | 1.541 |
| QA | 8bit | −0.020 | −0.004 | 0.542 | 2.235 |
| RE | 4bit | −0.009 | −0.007 | 0.318 | 1.420 |
| RE | 8bit | −0.017 | −0.002 | 0.540 | 2.431 |

下表為論文 Table 3：主實驗矩陣的平均無效輸出率與重複率。[(ref: main Table 3)](https://www.nature.com/articles/s44401-026-00152-6#Tab3)

| Quantization | Invalid output rate | Repetition rate |
|---|---|---|
| Full precision | 11.3% | 0.18% |
| 8bit | 13.9% | 0.23% |
| 4bit | 12.0% | 0.21% |

下表為論文 Table 4：vLLM 上三種預先量化 checkpoint 的分數與生成 token 吞吐量（tok/s）；DDI2013、HoC 為 macro F1，NCBI Disease 為 entity F1，MedQA 為 accuracy。[(ref: main Table 4)](https://www.nature.com/articles/s44401-026-00152-6#Tab4)

| Dataset | Model | AWQ score | AWQ tok/s | GPTQ score | GPTQ tok/s | FP8 score | FP8 tok/s |
|---|---|---|---|---|---|---|---|
| DDI2013 | Qwen2.5-32B | 0.535 | 2717.0 | 0.542 | 2900.7 | 0.536 | 1873.5 |
| DDI2013 | Qwen2.5-7B | 0.483 | 11,671.1 | 0.487 | 12,148.6 | 0.505 | 11,397.7 |
| HoC | Qwen2.5-32B | 0.350 | 2329.6 | 0.524 | 2427.7 | 0.403 | 1238.9 |
| HoC | Qwen2.5-7B | 0.451 | 8538.3 | 0.456 | 8803.4 | 0.457 | 7915.6 |
| MedQA | Qwen2.5-32B | 0.665 | 2707.0 | 0.653 | 2856.6 | 0.673 | 2381.2 |
| MedQA | Qwen2.5-7B | 0.518 | 11,302.2 | 0.504 | 11,849.5 | 0.543 | 11,015.1 |
| NCBI Disease | Qwen2.5-32B | 0.395 | 1352.4 | 0.360 | 1265.3 | 0.367 | 181.8 |
| NCBI Disease | Qwen2.5-7B | 0.283 | 3991.9 | 0.296 | 4154.5 | 0.337 | 3487.1 |

下表為論文 Table 5：Qwen2.5-72B 改用 CoT 或 self-consistency 時，相對 instruction prompt 的分數變化、延遲比值與生成 token 比值。[(ref: main Table 5)](https://www.nature.com/articles/s44401-026-00152-6#Tab5)

| Dataset | Prompt | Quant. | Score delta | Latency ratio | Token ratio |
|---|---|---|---|---|---|
| HoC | CoT | 4bit | 0.023 | 12.7 | 10.2 |
| HoC | CoT | 8bit | 0.001 | 17.4 | 11.4 |
| HoC | CoT | Full precision | 0.003 | 16.1 | 11.1 |
| HoC | Self-consistency | 4bit | 0.045 | 12.9 | 10.3 |
| HoC | Self-consistency | 8bit | 0.034 | 17.2 | 11.4 |
| HoC | Self-consistency | Full precision | 0.022 | 16.3 | 11.2 |
| MedQA | CoT | 4bit | 0.006 | 76.8 | 28.8 |
| MedQA | CoT | 8bit | 0.046 | 142.7 | 26.5 |
| MedQA | CoT | Full precision | 0.035 | 109.6 | 26.3 |
| MedQA | Self-consistency | 4bit | 0.076 | 75.9 | 28.5 |
| MedQA | Self-consistency | 8bit | 0.056 | 144.9 | 26.6 |
| MedQA | Self-consistency | Full precision | 0.055 | 110.0 | 26.4 |

## 結果

- **4-bit 省最多記憶體、平均分數變化小** — 四類任務的 4-bit 記憶體比值為 0.316–0.325（約省 68%），平均分數變化 −0.001 到 −0.015；在 Table 1 中，DeepSeek-LLM-67B 與 Llama-3.3-70B 的 4-bit 峰值記憶體為 36.34–39.95 GB，Qwen2.5-72B 為 40.49–41.6 GB。[(ref: main Table 1; Table 2)](https://www.nature.com/articles/s44401-026-00152-6#Tab2)
- **8-bit 反而最慢，平均掉分也較多** — 8-bit 記憶體比值 0.534–0.544，延遲比值 2.235–2.864，4-bit 為 1.312–1.541；8-bit 的平均分數變化 −0.017 到 −0.054，中位數則只有 −0.001 到 −0.008，表示少數組合掉得特別多。作者的文字描述是：在 Transformers／BitsAndBytes 設定下，量化會增加延遲。[(ref: main Results; Table 2)](https://www.nature.com/articles/s44401-026-00152-6#Tab2)
- **大幅掉分集中在少數組合** — Llama-3.3-70B 在 8-bit 下 MedQA 從 0.732 降到 0.555、HoC 從 0.45 降到 0.343、ChemProt 從 0.249 降到 0.181，同一模型的 4-bit 則為 0.705、0.419、0.243；Qwen2.5-72B 在 8 個資料集上三種精度的差距多在 0.02 以內，只有 NCBI Disease 的 4-bit 從 0.413 降到 0.357。[(ref: main Table 1)](https://www.nature.com/articles/s44401-026-00152-6#Tab1)
- **全精度也有一成以上無效輸出** — 無效輸出率全精度 11.3%、8-bit 13.9%、4-bit 12.0%，重複率 0.18%–0.23%；作者據此建議部署時要監測輸出有效性，而不是只看量化前後的分數。[(ref: main Results; Table 3)](https://www.nature.com/articles/s44401-026-00152-6#Tab3)
- **領域模型在 8-bit 下更容易出問題** — 作者以文字描述 Fig. 3：四個 70B 生醫模型的記憶體都明顯下降，DDI2013 與 HoC 受影響很小、尤其是 4-bit；HuatuoGPT-o1-70B 與 Llama3-Med42-70B 在部分 8-bit 設定下出現重複且無意義的輸出、分數大幅下降，作者歸因於指令遵循能力較弱，而不是生醫知識流失。論文沒有以文字列出這些長條的數值。[(ref: main Results; Fig. 3; Discussion)](https://www.nature.com/articles/s44401-026-00152-6#Fig3)
- **vLLM 上沒有一種方法通吃** — 同為 Qwen2.5-32B 的 HoC，AWQ 0.350、GPTQ 0.524、FP8 0.403；NCBI Disease 的 FP8 吞吐量只有 181.8 tok/s，AWQ 與 GPTQ 為 1352.4 與 1265.3 tok/s。[(ref: main Results; Table 4)](https://www.nature.com/articles/s44401-026-00152-6#Tab4)
- **模型大小** — 在 Qwen2.5 3B–72B 上，記憶體大致隨參數量線性增加；NCBI 與 HoC 在 14B 就接近平台，DDI 與 MedQA 則持續隨規模提升，量化與全精度的曲線大致重疊（論文正文描述，未列數值）。[(ref: main Results; Fig. 4)](https://www.nature.com/articles/s44401-026-00152-6#Fig4)
- **提示策略的代價大於量化** — Qwen2.5-72B 在 MedQA 改用 CoT 或 self-consistency，分數增加 0.006–0.076，延遲卻是 instruction prompt 的 75.9–144.9 倍、生成 token 是 26.3–28.8 倍；作者指出此時瓶頸從權重轉到生成長度與 KV cache。few-shot 範例越多，峰值記憶體也隨提示長度增加。[(ref: main Results; Table 5; Fig. 5; Fig. 6)](https://www.nature.com/articles/s44401-026-00152-6#Tab5)

## 限制

**作者自述的限制。** 所有實驗只在 NVIDIA A100 上跑，沒有量測 RTX 等消費級 GPU 的吞吐量、延遲、kernel 行為與耗電；vLLM 預先保留記憶體，無法與 PyTorch 的峰值配置直接比較；資料集都是公開基準，可能出現在部分模型的預訓練或指令微調資料中，所以絕對分數要保守解讀、不能當成臨床泛化的證據；評估是離線的，不是前瞻臨床驗證；測試的量化方法只涵蓋快速演變生態系的一部分，KV-cache 量化留待未來。[(ref: main Discussion)](https://www.nature.com/articles/s44401-026-00152-6)

**本書庫的觀察。**

- **「生醫 NLP」幾乎都是文獻任務** — 8 個資料集中 7 個來自生醫文獻（摘要分類、化學／疾病實體、藥物交互作用、PubMedQA），MedQA 是醫師執照考題；沒有病歷、放射報告等臨床文本。量化對臨床筆記抽取的影響，本篇無法直接回答。
- **不確定性看不到** — 表格只有點估計，Methods 提到 bootstrap 卻沒有印出區間，也沒有說明是否單次執行；Table 1 中 0.01–0.03 的差距（例如 Phi-4 在 HoC 的 4-bit 0.487 高於全精度 0.459）不應解讀成量化「改善」分數。
- **「省記憶體」不等於「能塞進一張卡」** — 論文用 4 張 40 GB A100，沒有說明每次執行用了幾張；Qwen2.5-72B 的 4-bit 峰值為 40.49–41.6 GB，超過單張 40 GB。論文也沒有在消費級 GPU 上驗證。
- **延遲結論綁在 BitsAndBytes** — 8-bit 最慢是 Transformers／BitsAndBytes 這條路徑的結果；vLLM 部分只報吞吐量，兩種執行環境不能互相換算。
- **Table 2 的彙總方式不透明** — 論文只說數值取自原始實驗矩陣，沒有寫明納入哪些模型；讀者若用 Table 1 的四個通用模型自行平均，會得到不完全相同的數字。
- **領域模型的結果只有圖** — 8-bit 下「重複且無意義的輸出」是作者對 Fig. 3 的描述，沒有文字數值，也沒有逐模型的無效輸出率。

## 與書庫其他文章的關係

西語精神科病歷那篇在病歷文字上直接使用 4-bit 量化（Ollama）的 11 個開源 LLM 做概念偵測與 LoRA 微調，但沒有和全精度比較；本篇則在生醫文獻基準上系統比較全精度、8-bit 與 4-bit，補上「量化本身會讓分數與延遲改變多少」這一層，兩篇合起來看可以分清楚表現差異來自量化還是來自提示與微調: [西語精神科病歷的 109 個症狀：微調後才追平規則式 tNLP](2026-10-30-llm-psychiatric-concepts-spanish-ehr.md)

## 實務的啟發

- **可借用的做法** — 若要在院內 GPU 上跑 70B 等級的開源模型，4-bit NF4 是本篇中記憶體與分數折衷最好的設定（約省 68% 峰值記憶體、平均掉分在 0.015 以內）；但這是生醫文獻基準與 A100 上的結果，換到臨床文本或其他硬體前要在自己的任務上複驗。
- **待驗證的警訊** — 不要預設 8-bit 比 4-bit 「保守、安全」。本篇在 BitsAndBytes 下 8-bit 更慢、平均掉分更多，且 Llama-3.3-70B 在 MedQA 掉了約 18 個百分點；選定量化設定時應逐模型、逐任務實測。
- **可借用的量測方法** — 評估量化時同時記錄分數、峰值記憶體、延遲與無效輸出率；本篇全精度就有 11.3% 的無效輸出，只比較量化前後的分數會漏掉輸出格式的問題。
- **可借用的量測方法** — 若計畫加上 CoT 或 self-consistency，先量生成 token 與延遲；本篇在 MedQA 上換來 0.006–0.076 的分數增加，延遲卻增加數十到上百倍，成本可能遠大於量化省下的部分。
- **證據強度** — 12 個模型、8 個公開資料集、離線評估、沒有信賴區間、只用 A100；它支持「4-bit 量化在生醫文獻 NLP 基準上通常能大幅省記憶體且平均掉分小，但效果依模型、任務與執行環境而異」，不足以支持量化模型可直接用於臨床決策。

## References

- **main** — Zhan Z, Zhou S, Zeng M, Song Y, Yu K, Song M, Chen X, Wang J, Hou Y, Zhang R. *Quantized large language models in biomedical natural language processing: evaluation and recommendation*. npj Health Systems. 2026;3:104. DOI: 10.1038/s44401-026-00152-6. 全文：<https://www.nature.com/articles/s44401-026-00152-6>。文內引用位置：author information、Introduction、Results（Quantized LLMs on MLC, NER, RE, QA tasks；Performance of domain-specific quantized LLMs across biomedical NLP tasks；Additional quantization methods with vLLM serving；Quantized LLMs with different size；Quantized LLMs with few-shot learning；Prompting strategies on quantized LLMs）、Discussion、Methods（Datasets、LLMs、Quantization setup、Prompt methods、Experimental settings、Latency, output validity, and statistical analysis）、Data availability、Code availability；深鏈 [Table 1](https://www.nature.com/articles/s44401-026-00152-6#Tab1)、[Table 2](https://www.nature.com/articles/s44401-026-00152-6#Tab2)、[Table 3](https://www.nature.com/articles/s44401-026-00152-6#Tab3)、[Table 4](https://www.nature.com/articles/s44401-026-00152-6#Tab4)、[Table 5](https://www.nature.com/articles/s44401-026-00152-6#Tab5)、[Table 6](https://www.nature.com/articles/s44401-026-00152-6#Tab6)、[Fig. 1](https://www.nature.com/articles/s44401-026-00152-6#Fig1)、[Fig. 2](https://www.nature.com/articles/s44401-026-00152-6#Fig2)、[Fig. 3](https://www.nature.com/articles/s44401-026-00152-6#Fig3)、[Fig. 4](https://www.nature.com/articles/s44401-026-00152-6#Fig4)、[Fig. 5](https://www.nature.com/articles/s44401-026-00152-6#Fig5)、[Fig. 6](https://www.nature.com/articles/s44401-026-00152-6#Fig6)。
- **PDF** — <https://www.nature.com/articles/s44401-026-00152-6.pdf>（p.8 投稿／接受日期、Data availability、Code availability）。
- **doi** — <https://doi.org/10.1038/s44401-026-00152-6>。
- **code** — <https://github.com/Learner4everrr/Benchmark_quantization>。
- **data** — <https://doi.org/10.5281/zenodo.14025500>。

[Home](../) · [AI Papers](./)
