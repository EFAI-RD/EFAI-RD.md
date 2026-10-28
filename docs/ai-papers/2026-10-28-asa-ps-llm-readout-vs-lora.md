---
catalog_id: "doi:10.64898/2026.10.20.26366028"
editors:
  - "Clare"
refs:
  main:
    title: "Non-generative readout with few-label calibration versus LoRA fine-tuning of a large language model for ASA physical status classification: accuracy, speed, cost and label efficiency in three data sources"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 不生成理由、只讀 A–D 選項的機率：Qwen3.5-9B 分 ASA 身體狀態，比生成式提示快約 64 倍，再用 1,000 個在地標籤調三個門檻，κ 只比 LoRA 低約 0.02，標籤再多 LoRA 仍會拉開

## 來源

- 團隊：新疆醫科大學（Xinjiang Medical University）與新疆維吾爾自治區人民醫院（People's Hospital of Xinjiang Uygur Autonomous Region，烏魯木齊），共 5 位作者；第一作者 Yutong Shi，通訊作者 Guiping Xu。[(ref: main author block)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)
- 論文：*Non-generative readout with few-label calibration versus LoRA fine-tuning of a large language model for ASA physical status classification: accuracy, speed, cost and label efficiency in three data sources*，medRxiv 預印本 v1，2026-10-22 公開，未經同儕審查，授權 CC BY-NC-ND 4.0。[(ref: main)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1)
- 識別碼：DOI [10.64898/2026.10.20.26366028](https://doi.org/10.64898/2026.10.20.26366028)。
- 全文：[medRxiv 全文 HTML](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)、[PDF](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf)。
- 資料與程式：院內資料含病人資訊、不公開；MOVER 需向提供者簽資料使用協議；VitalDB 公開。作者表示分析腳本、各設定的 prompt 全文與 OpenJev 修補檔放在補充材料。[(ref: main PDF Data availability)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=25)
- 研究性質：完整的回溯性比較研究，不是 pilot；所有比較方法都有實作，主要比較附病人層級 cluster bootstrap 95% CI，依 TRIPOD-LLM 報告，但沒有預先註冊，且有數項分析是在看到主要結果後才加入（作者在 §2.10 逐項列出）。[(ref: main §2.1, §2.10)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-24)
- 證據邊界：本文數值以 medRxiv v1 全文正文為準；Table 1–4 的完整儲存格與補充材料（prompt 全文、補充對照組的完整結果）未納入引述，表內數值取自正文對應段落。

**編輯：** Clare

在三個資料來源上，作者把 Qwen3.5-9B 用四種方式拿來分術前 ASA 身體狀態（ASA physical status，ASA-PS）：只讀選項字母機率的 non-generative readout 比先寫理由再作答的生成式提示 quadratic-weighted κ 高約 0.22–0.23、每例快約 64 倍；再用 1,000 個在地標籤擬合三個門檻，κ 達 0.534，比同樣 1,000 個標籤做 LoRA 低約 0.02，但標籤增加到數千時 LoRA 會再拉開 0.04–0.06。[(ref: main Abstract, §3.2–§3.4)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-27)

## 流程

![ASA-PS 分類的研究設計示意圖。由左到右三個圓角方塊，以兩支實線箭頭相連。左側藍色方塊「1. Data: three sources」列出院內醫院（腹部／骨盆手術）開發集 2021–2024 n = 4,326 與時間外部驗證集 2025–2026 n = 2,753、MOVER（UC Irvine）57,473 台手術與評估子集 n = 4,000（生成式組只用前 2,000）、VitalDB（首爾大學醫院）訓練 4,357／測試 1,885，參考標準為麻醉紀錄中登載的 ASA 等級（不重新標註），輸入 T1 為結構化術前變項的共用英文模板、T2 為 T1 加術前診斷文字。中間綠色方塊「2. Qwen3.5-9B: four compared arms」列出 (a) generative zero-shot（最多 3 句理由加答案、最多 140 個新 token）、(b) non-generative readout（對選項字母 A–D 的 logits 取 softmax、一次前向傳遞、不生成 token）、(c) readout 加 few-label cutpoint calibration（E = sum k * p_k，在 k 個在地標籤上擬合 3 個 cutpoint 使 quadratic-weighted kappa 最大、不更新模型參數）、(d) task LoRA（QLoRA、4-bit NF4、rank 16、alpha 32、1 epoch、n = 100／300／1,000／all、3 seeds）。中間下方灰色方塊「Supplementary arms」列出 OpenJev、XGBoost、kNN-8 few-shot 與 27B 規模檢查，沒有箭頭連入或連出。右側橘色方塊「3. Outcomes」列出主要指標 quadratic-weighted kappa（相對登載的 ASA 等級、病人層級 cluster bootstrap 95% CI、B = 1,000）、假說 H1–H3（H2 的不劣性 margin 為 0.05）、次要指標與速度成本。圖底為斜體說明「Design schematic redrawn from the paper's Methods text; contains no result values.」](assets/asa-ps-readout-vs-lora-design.png)

圖：本書庫依論文 Methods 的文字重繪的研究設計示意圖，只含設計層級的計數與設定，不含結果數值，未複製論文原圖（論文 Figure 1 為研究設計與資料流，Figure 2 為納入、排除與切分流程）。[(ref: main Figure 1, Figure 2, §2.2–§2.5)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F1)

## 背景／問題

ASA-PS 是麻醉前評估常用的四級（本文合併 V 級後）病人整體健康分級，同一位病人由不同麻醉科醫師評定時並不總是一致；作者引用的文獻中，麻醉科醫師彼此之間的 weighted κ 約 0.62–0.85。[(ref: main §4.2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)

作者要回答的是部署層面的取捨，而不是 LLM 能否「懂」ASA：同一個開放權重的 9B 模型，(1) 讓它生成理由再作答、(2) 只讀它對四個選項字母的機率、(3) 讀機率之後再用少量在地標籤調門檻、(4) 用在地標籤做 LoRA，四者在 κ、速度、訓練成本與所需標籤數上各差多少。作者把三個方向寫成預先設定的假說（H1 readout 優於生成式、H2 校準後 readout 不劣於同標籤量的 LoRA、H3 全量 LoRA 優於校準後 readout），但研究整體沒有預先註冊。「生成式提示太慢、太貴」在本文不是被假定的前提，而是作者自己量測的結果之一（§3.3）。[(ref: main §2.8, §3.3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)

## 方法摘要

**任務。** 只用術前資訊，把每一台手術分成 ASA I、II、III、IV–V 四類；V 級併入 IV。參考標準是各院麻醉紀錄中登載的 ASA 等級，沒有人工重新標註。[(ref: main §2.3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-13)

**資料。**

- **院內醫院** — 腹部／骨盆手術 7,079 台；2021–2024 為開發集（4,326 台），2025–2026 為時間外部驗證集（2,753 台、2,640 位病人）。[(ref: main §2.2, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T1)
- **MOVER** — UC Irvine 的手術室資料庫，57,473 台成人手術（38,245 位病人，2017–2023），以病人為單位 80／20 切分，評估用 4,000 台的子集（2,606 位病人）。[(ref: main §2.2, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T1)
- **VitalDB** — 首爾大學醫院公開資料，6,242 台（5,961 位病人），以病人為單位切成訓練 4,357 台、測試 1,885 台，作為第二院所的重複驗證。[(ref: main §2.2, §3.6)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)

**輸入。** T1 是把人口學、BMI、生命徵象、共病、檢驗值與預定術式等結構化術前變項填進共用英文模板，缺值寫成 "unknown"；T2 是 T1 加術前診斷文字。院內的 T2 是原始中文門診紀錄、遮掉其中的 ASA 字樣；MOVER 的 T2 是沒有日期的診斷史、可能含術後診斷，因此只作探索性分析。[(ref: main §2.3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-13)

**四個比較組（皆以 Qwen3.5-9B 為底）。**

- **Generative zero-shot** — 先寫最多三句理由再給答案，greedy decoding、最多 140 個新 token，解析最後答案；prompt 不列出選項。
- **Non-generative readout** — 把四類寫成選項 A–D，在最後一個位置對四個選項字母的 logits 取 softmax，一次前向傳遞、不生成任何文字。
- **Few-label cutpoint calibration** — 以 readout 的四類機率算期望分數 E = Σ k·p_k，再用 k 個在地標籤以 coordinate search 擬合三個 cutpoint，使 quadratic-weighted κ 最大；不更新任何模型參數。
- **Task LoRA** — QLoRA 微調，在 100、300、1,000 個與全部在地標籤上訓練。

另有補充對照：OpenJev（作者描述為一個與託管 decision model Jev 請求格式相容的開放實作）、XGBoost、retrieval-based kNN-8 few-shot，以及 27B 規模的檢查。[(ref: main §2.4)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=6)

**指標。** 主要指標為相對登載 ASA 等級的 quadratic-weighted κ，附病人層級 cluster bootstrap 95% CI（B = 1,000）；次要指標為 accuracy、adjacent accuracy（差一級以內算對）、差兩級以上錯誤的比例、macro one-vs-rest AUC、expected calibration error（ECE）與 Brier score。H2 的不劣性 margin 為 0.05，另報 0.03 與 0.10 的結果。[(ref: main §2.8)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=9)

## 方法詳解

**Readout 的計算。** Readout 的 prompt 由角色說明、輸入模板與選項清單組成，取最後一個位置在 A、B、C、D 四個字母上的 logits 做 softmax，得到四類機率。主分析固定使用自然順序（A–D 依序為 ASA I 到 IV–V），作者說明這個順序在看到任何結果前就已決定；六種選項順序的平均只在 §3.9 的穩健性分析中出現。[(ref: main §2.4, §3.9)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-41)

**校準標籤從哪裡來。** 三個來源各從開發／訓練集隨機抽 1,000 台（seed 11）作為校準標籤池；畫標籤數曲線時，從池中抽 k = 25、50、100、200、500、1,000 個標籤，各重複 100 次（VitalDB 為 60–100 次）。[(ref: main §2.5)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)

**LoRA 設定。** 4-bit NF4 的 QLoRA，rank 16、α 32、dropout 0.05，套在所有 attention 與 feed-forward 的 linear 層；AdamW，learning rate 1×10⁻⁴（one-cycle cosine）、effective batch 16、1 個 epoch，以選項字母 logits 上的 cross-entropy 訓練；seed 為 20261017、11、12。院內 LoRA 的訓練池是 2021–2024 開發集；MOVER 另訓練 3,000 與 12,000 個標籤的版本。[(ref: main §2.4)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=6)

**精度與硬體。** 主分析中 readout 與生成式組以 fp16 執行，LoRA 以 4-bit NF4 執行；4-bit 的 readout 只出現在敏感度分析。速度在單張改裝 RTX 2080 Ti（設定為 22 GB）上以 batch size 1 量測。[(ref: main §2.6, §3.9)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-41)

**生成式組的抽樣。** 生成式組只跑子集：院內驗證集隨機抽 1,000 台（999 台可解析），MOVER 取評估子集的前 2,000 台（1,978 台可解析）。作者另以單一研究者檢查生成理由與結構化欄位是否矛盾，只看前 400 個字元，因此估計值是下限。[(ref: main §2.7, §3.2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-21)

**Natural-language guidance。** 作者另外測試在 prompt 中加入描述在地評分習慣的文字段落（不訓練、不用標籤），看它如何改變 readout 預測的類別分布與 κ。[(ref: main §2.4, §3.7, Figure 6)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F6)

- **論文未交代** — MOVER 以 12,000 個標籤訓練的 LoRA 用了幾個 seed：Methods 寫三個 seed，Table 4 的註記卻寫單一 seed 20261017。
- **論文未交代** — kNN-8 few-shot 在 Methods 中被列為補充對照，但結果段沒有報告它的 κ；XGBoost 在結果段也只報告院內數值。
- **論文未交代** — 生成式組只要求「先寫理由再作答」，沒有只輸出答案的生成式基線，因此 64 倍的速度差與 κ 差有多少來自理由的長度、有多少來自生成本身，無法從本文分開。
- **論文未交代** — 各設定的 prompt 全文與分析腳本只在補充材料，正文沒有完整 prompt。

## 資料與實驗

下表整理三個資料來源的規模與 ASA 分布，取自論文 §2.2 與 Table 1 對應的正文敘述；MOVER 正文只給出 III 與 IV–V 的比例。[(ref: main §2.2, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T1)

| 資料來源 | 規模 | 評估集 | ASA I / II / III / IV–V |
|---|---|---|---|
| 院內醫院（腹部／骨盆手術） | 7,079 台；開發 2021–2024 4,326 台 | 時間外部驗證 2025–2026，2,753 台（2,640 位病人） | 1.3% / 46.0% / 50.0% / 2.6% |
| MOVER（UC Irvine，2017–2023） | 57,473 台（38,245 位病人），病人層級 80／20 切分 | 4,000 台子集（2,606 位病人）；生成式組用前 2,000 台 | III 51.2%、IV–V 12.2%（I、II 未於正文列出） |
| VitalDB（首爾大學醫院） | 6,242 台（5,961 位病人）；訓練 4,357 台 | 測試 1,885 台（1,788 位病人） | 測試集 28.3% / 58.8% / 11.7% / 1.2% |

下表為主要比較的 κ 配對差（A − B）與 95% cluster bootstrap CI，對應論文 Table 3 的正文數值。[(ref: main §3.2, §3.4, Table 3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T3)

| 假說 | 比較 | 資料 | Δκ（95% CI） |
|---|---|---|---|
| H1 | readout − generative zero-shot | 院內 1,000 台子集 | +0.234（0.201 至 0.264） |
| H1 | readout − generative zero-shot | MOVER 2,000 台子集 | +0.224（0.199 至 0.247） |
| H2 | 校準 readout（1,000 標籤）− LoRA@1,000，預先指定 seed 20261017 | 院內驗證集 | −0.019（−0.042 至 +0.005） |
| H2 | 校準 readout（1,000 標籤）− LoRA@1,000，三 seed 平均 | 院內驗證集 | −0.025（−0.046 至 −0.003） |
| H3 | LoRA（全部標籤）− 校準 readout，三 seed 平均 | 院內驗證集 | +0.027（+0.006 至 +0.048） |

下表為院內驗證集上 κ 隨標籤數的變化（LoRA 為三 seed 平均），取自 §3.4 正文。[(ref: main §3.4, Figure 3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F3)

| 方法 | 0 標籤 | 100 | 300 | 1,000 | 全部（4,326） |
|---|---|---|---|---|---|
| Readout（未校準） | 0.443 | — | — | — | — |
| Readout＋cutpoint 校準 | — | 0.526 | — | 0.534（0.508–0.559） | — |
| Task LoRA | — | 0.423 | 0.542 | 0.559 | 0.561 |
| XGBoost | — | 0.431 | 0.467 | 0.521 | 0.549 |

下表為院內驗證集的 accuracy 與相鄰類別錯誤（cutpoint 以最大化 κ 擬合，LoRA 為 n = 1,000 的三 seed 平均），對應論文 Table 4 的正文數值。[(ref: main §4.3, Table 4)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T4)

| 指標 | Zero-shot readout | 校準 readout（1,000 標籤） | LoRA（1,000 標籤） |
|---|---|---|---|
| Accuracy | 0.563 | 0.666 | 0.746 |
| Adjacent accuracy | 0.984 | 0.991 | 0.999 |
| 差兩級以上的錯誤 | 1.6% | 0.9% | 0.1% |

下表為速度與成本，取自 §3.3 與 Table 2 對應的正文；硬體為單張改裝 RTX 2080 Ti、batch size 1，LoRA 訓練為 9B、4-bit。[(ref: main §3.3, Table 2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T2)

| 項目 | Readout | Generative zero-shot | LoRA |
|---|---|---|---|
| 每例延遲中位數（p95） | 111 ms（118 ms） | 7,067 ms（9,105 ms） | 179 ms（4-bit） |
| 推估 10,000 台手術的時間 | 約 18.5 分鐘 | 約 19.6 小時 | — |
| 訓練／校準時間 | 校準：k = 100 約 11 秒、k = 1,000 約 2 分鐘，cutpoint 擬合 < 1 秒 | 不需要 | n = 1,000 約 6.7 分鐘、n = 3,000 約 20 分鐘、n = 12,000 約 81 分鐘（另加 3–4 分鐘載入） |

## 結果

- **Readout 勝過生成式提示（H1）** — 院內 1,000 台子集上 readout 與生成式的 κ 為 0.460 對 0.227，MOVER 2,000 台子集為 0.473 對 0.249，兩處的差距 CI 都不含 0；生成式組平均每例生成約 89 個 token。[(ref: main §3.2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-27)
- **少量標籤時，調門檻比 LoRA 好用** — 院內只有 100 個標籤時，校準 readout 的 κ 為 0.526、LoRA 為 0.423；兩條曲線約在 270 個標籤交叉，MOVER 約在 1,000–1,800 個標籤交叉。LoRA 在 accuracy 上較早領先。[(ref: main §3.4, §4.3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=22)
- **H2 只在預先指定的分析中成立** — 預先指定 seed 的差距 −0.019，CI 下界 −0.042 未越過 −0.05；三 seed 平均 −0.025（−0.046 至 −0.003）與同標籤 seed 11 的 −0.028（−0.051 至 −0.003）則貼近或觸及 margin。作者在結論中把不劣性寫成「有條件的」，取決於實作、輸入、選項順序、標籤抽樣與 LoRA seed。[(ref: main §3.4, §4.7)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=25)
- **標籤多時 LoRA 仍會拉開（H3）** — 院內全量 LoRA 比校準 readout 高 0.027（+0.006 至 +0.048）；MOVER 上校準 readout 為 0.524，LoRA 在 3,000 與 12,000 個標籤時分別高 0.039（0.019 至 0.058）與 0.059（0.040 至 0.080）。[(ref: main §3.4, Table 3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T3)
- **校準修的是門檻，不是鑑別力** — 100 個標籤的校準把院內 κ 從 0.443 拉到 0.526，但 macro AUC 維持 0.794，LoRA 的 macro AUC 為 0.846–0.857；作者據此把 readout 的差距拆成門檻／先驗與鑑別力兩部分。[(ref: main §4.2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)
- **第二院所 VitalDB** — 在 T2 輸入的探索性分析中，校準 readout 與 LoRA@1,000 都是 0.567，差距 0.000（−0.023 至 +0.025）。[(ref: main §3.6, Figure 5)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F5)
- **換一個 decision model 實作就不成立** — OpenJev 在院內 T1 未校準 κ 為 0.314、校準後 0.502，對 LoRA@1,000 的差距 −0.051（−0.080 至 −0.022），H2 不成立。[(ref: main §3.5)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-37)
- **選項順序的影響很大** — 未校準 readout 在六種選項順序下，院內 κ 從 0.142 到 0.505、MOVER 從 0.222 到 0.473。[(ref: main §3.9, §4.2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-41)
- **輸入文字的效果多半來自語言對齊** — 院內加入診斷文字（T2）讓未校準 readout 從 0.443 升到 0.505；但把 T1 翻成中文、配中文 prompt 也達 0.512（macro AUC 0.821，T2 為 0.833），作者認為增益大多來自語言與 prompt 的對齊而非診斷內容，並稱此拆解為初步結果。[(ref: main §3.5, §4.2)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-37)
- **機率校準方向不一致** — readout 與 LoRA 的原始 ECE 在院內為 0.030 對 0.040，在 MOVER 反過來為 0.092 對 0.051。[(ref: main §3.8)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full)
- **其他** — 27B 模型沒有穩定改善零樣本表現（readout +0.015、OpenJev −0.057）；fp16 與 4-bit LoRA 的 κ 差 −0.008（−0.021 至 +0.006）；生成理由與結構化欄位矛盾的比例約 2%（95% CI 約 1%–3%），為下限估計。[(ref: main §3.8, §3.9, §4.2, §4.3)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=22)

## 限制

**作者自述的限制。** 參考標準是登載的 ASA 等級，包含評分者差異與院所習慣，κ 的上限未知，也沒有獨立的人工評分；不劣性是在 κ 上檢定，而 cutpoint 正是為最大化 κ 而擬合，LoRA 在 exact agreement 上較好；H2 的結果隨標籤池、LoRA seed 與實作而變，且只有三個訓練池；研究為回溯性、未預先註冊，數項分析在主要結果後才加入；readout 用 fp16、LoRA 用 4-bit，fp16 LoRA 只在院內 n = 1,000 跑過一次；多數 LoRA 點只有三個 seed，27B LoRA 只有一個；生成式組要求寫理由，沒有只輸出答案的基線；矛盾檢查只涵蓋結構化欄位與前 400 個字元；速度只在單張改裝 RTX 2080 Ti、batch size 1 下量測，只有一個基礎模型家族，VitalDB 的 ASA 分布與其他來源差異很大，MOVER 的 T2 可能含術後診斷。作者明言結論只適用於有在地門檻、標籤有雜訊的封閉集合文字分類，不涵蓋開放式生成、多模態輸入或完全沒有標籤的院所。[(ref: main PDF §4.6)](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=24)

**本書庫的觀察。**

- **指標選擇偏向校準法** — cutpoint 是在校準集上直接最大化 quadratic-weighted κ，而 H2 也用 κ 判定；在 accuracy 上，同樣 1,000 個標籤的 LoRA（0.746）比校準 readout（0.666）高 8 個百分點。若下游用途需要的是準確的單一等級（例如排程或計費規則），本文的「不劣」結論不能直接套用。
- **參考標準本身就是被模仿的對象** — 登載的 ASA 等級帶有院所評分習慣，LoRA 的優勢有多少是學到 ASA 的臨床判斷、有多少是學到該院的登載習慣，作者自己也說無法分開；本文的 κ 0.5 左右不能與麻醉科醫師之間的一致性直接比較，作者也明確不主張達到人類水準。
- **單一順序的零樣本分數不可靠** — 光是改變 A–D 的對應順序，院內未校準 κ 就能從 0.142 變到 0.505；任何用選項字母機率做零樣本分類的研究，若只報一種順序，數字的參考價值有限。
- **同一題的不劣性結論依賴實作** — 同樣的校準法換成 OpenJev 就不成立，代表「decision model 加少量標籤可取代 LoRA」不是對這類方法的一般結論，而是 Qwen3.5-9B readout 在這幾組資料上的結果。

## 與書庫其他文章的關係

RadKev 把「一次前向傳遞給出每個選項機率」的 decision model 拿去做放射科專科化並比較延遲，本篇則在麻醉 ASA 分級上直接比較這種 readout、生成式提示與 LoRA 的 κ、延遲與標籤成本，兩篇都顯示 decision model 的速度優勢明確、但準確度結論依賴實作與資料: [不生成文字、直接給每個選項機率：RadKev 把 decision model 專科化到放射科，15 項任務平均多 4.9 點，換到外院報告卻沒有進步](2026-10-15-radkev-radiology-decision-model.md)

病歷時間關係抽取那篇比較 prompting 與 QLoRA 等調適方式在資料充足與每類一例時的差距，本篇則把同一個問題延伸到「需要多少在地標籤 LoRA 才划算」，在 ASA 分級上找到約 270 個標籤的交叉點: [病歷時間關係抽取該怎麼調模型？i2b2 2012 上只調 query／value 的 QLoRA 讓 LLaMA3.1-8B 達 89.15% micro-F1，但每類只給一例時沒有一種做法超過 60%](2026-10-20-llm-clinical-temporal-relation-extraction-adaptation.md)

## 實務的啟發

- **可借用的做法** — 答案可以列舉的病歷分類任務，先試「讀選項字母機率＋少量在地標籤調門檻」作為不需訓練的起點；本篇在院內只用 100 個標籤就從 0.443 升到 0.526，且不必為每家院所訓練與保存 adapter。這是單一基礎模型、三個資料來源的結果，換任務或換模型前需要複驗。
- **可借用的量測方法** — 比較 prompting 與微調時，畫出 κ（或主要指標）對在地標籤數的曲線並標出交叉點，同時報 exact accuracy；本篇的 κ 曲線約在 270 個標籤交叉，但 LoRA 在 accuracy 上更早領先，只看單一指標會選錯方法。
- **可借用的量測方法** — 用選項字母機率做零樣本分類時，把選項順序當成必報的敏感度分析；本篇六種順序之間的 κ 差距比 readout 與 LoRA 之間的差距大得多。
- **待驗證的警訊** — 參考標準是登載的 ASA 等級時，任何方法學到的都包含院所的登載習慣；若要拿來做跨院比較或品質稽核，需要另建獨立的人工評分集。
- **證據強度** — 回溯性、未預先註冊、單一基礎模型、參考標準為登載值的預印本；它支持「在這三組資料上，Qwen3.5-9B 的選項機率 readout 比生成式提示快很多且 κ 較高，少量標籤校準後在 κ 上接近同標籤量的 LoRA」，不足以支持這套做法可直接用於臨床 ASA 評定，或可普遍取代微調。

## References

- **main** — Shi Y, Wang Y, Simayi A, Qu L, Xu G. *Non-generative readout with few-label calibration versus LoRA fine-tuning of a large language model for ASA physical status classification: accuracy, speed, cost and label efficiency in three data sources*. medRxiv. 2026. DOI: 10.64898/2026.10.20.26366028（v1 預印本）。摘要頁：<https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1>；全文 HTML：<https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full>；PDF：<https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf>。文內引用位置：author block、Abstract、§2.1–§2.8、§2.10、§3.2–§3.9、§4.2–§4.3、§4.6–§4.7、Data availability；深鏈 [§2.3](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-13)、[§2.7](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-21)、[§2.10](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-24)、[§3.2](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-27)、[§3.5](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-37)、[§3.9](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#sec-41)、[Table 1](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T1)、[Table 2](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T2)、[Table 3](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T3)、[Table 4](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#T4)、[Figure 1](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F1)、[Figure 3](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F3)、[Figure 5](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F5)、[Figure 6](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full#F6)、[PDF p.6 §2.4](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=6)、[PDF p.9 §2.8](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=9)、[PDF p.22 §4.3](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=22)、[PDF p.24 §4.6](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=24)、[PDF p.25 §4.7 與 Data availability](https://www.medrxiv.org/content/10.64898/2026.10.20.26366028v1.full.pdf#page=25)。
- **doi** — <https://doi.org/10.64898/2026.10.20.26366028>。

[Home](../) · [AI Papers](./)
