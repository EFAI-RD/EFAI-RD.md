---
catalog_id: "doi:10.64898/2026.10.21.26365949"
editors:
  - "Clare"
refs:
  main:
    title: "Image-Based Dietary Assessment Using Multimodal Large Language Models: Performance, Limitations, and Clinical Applicability in Diabetes"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 拍一張餐點照片就能算碳水嗎？八個多模態 LLM 在 SNAPMe 1,680 張餐前照片上：最好的 GPT-4o mini 碳水 MAE 13.3 g、只有 57% 的餐落在 ±10 g 內，作者判定還不能拿來算胰島素

## 來源

- 團隊：University of Bergen（挪威）臨床科學系、Stanford University School of Medicine 遺傳學系與內科、Diabetes Technology Society 與 Sutter Mills Peninsula Medical Center，共 13 位作者；第一作者 Lila Gravellier，通訊作者 Helge Ræder、Michael P. Snyder、Tao Wang。[(ref: main author block)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- 論文：*Image-Based Dietary Assessment Using Multimodal Large Language Models: Performance, Limitations, and Clinical Applicability in Diabetes*，medRxiv 預印本 v1，2026-10-24 公開，未經同儕審查，授權 CC BY-NC-ND 4.0。[(ref: main)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1)
- 識別碼：DOI [10.64898/2026.10.21.26365949](https://doi.org/10.64898/2026.10.21.26365949)。
- 全文：[medRxiv 全文 HTML](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)、[PDF](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full.pdf)。
- 資料與程式：SNAPMe 原始照片可由 USDA Ag Data Commons 取得，作者提供所用照片 ID 的 metadata；作者稱評估框架 SeeFood benchmark 將開源，但要到正式發表時才釋出。[(ref: main Data and code availability)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- 研究性質：完整的回溯性 benchmark，不是 pilot；不訓練任何模型，評估對象是透過 API 呼叫的現成多模態 LLM，主要比較附參與者層級 bootstrap 95% CI；研究中沒有營養師或既有飲食 App 在同一批照片上的對照。[(ref: main Methods, §2.3.4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- 證據邊界：本文數值以 medRxiv v1 全文正文為準；Table 2 的完整儲存格、補充材料（prompt 全文 SM6、Table S1–S4、MAPE 公式）未納入引述。正文未把另兩個 finalist 的部分數值對應到模型時，本文只列數值、不指派模型。

**編輯：** Clare

作者把八個多模態 LLM 拿來看餐前照片、估計營養素與飲食品質，在公開資料集 SNAPMe 的 1,680 張照片上，表現最好的 GPT-4o mini 各營養素的 MAPE 仍都超過 50%、碳水化合物 MAE 13.3 g（95% CI 12.4–14.3），作者據此認為目前的模型還不足以用於糖尿病的精準管理，例如胰島素劑量計算。[(ref: main Abstract, §3.2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

## 流程

![以影像評估飲食的研究設計示意圖。由左到右三個圓角方塊，以兩支實線箭頭相連，圖頂標題為「Image-based dietary assessment with multimodal LLMs: study design」。左側藍框「1. Data」列出 SNAPMe（公開、美國）95 位參與者、275 個參與者日、1,680 張餐前照片、1.5 x 1.5 吋紙製尺寸標記、參考值為自填 ASA24 回顧（非秤重），ASA24 portion set 為 100 種食物 x 5 種份量（1x–5x）、只用於份量敏感度，以及三項任務：餐點營養素與熱量（MAPE）、食物品項辨識（Dice）、日層級飲食品質（HEI-2020 RMSE）。中間綠框「2. Phase 1: screening」列出 80 張照片子集（15 位參與者的第一個記錄日）、8 個經 API 呼叫的多模態 LLM（4 商用、4 開源）乘以兩種 prompt（no-CoT JSON／structured CoT）共 16 組、temperature 0.0、每張照片跑 3 次、營養素取中位數、品項 3 次中出現 2 次才保留，每家供應商取最佳組合成為 3 個 finalist。右側橘框「3. Phase 2: full evaluation」列出 3 個皆用 CoT 的 finalist（GPT-4o mini、Gemini 2.5 Flash-Lite、Llama 4 Maverick）在全部 1,680 張照片上評估、參與者層級 bootstrap 95% CI（2,000 次重抽），以及最佳模型的深入分析：餐別、份量、尺寸標記條件、可見度與品項數、HEI 各分項。圖底為斜體說明「Design schematic redrawn from the paper's Methods text; contains no result values.」](assets/mllm-dietary-assessment-design.png)

圖：本書庫依論文 Methods 的文字重繪的研究設計示意圖，只含設計層級的計數與設定，不含結果數值，未複製論文原圖（論文 Figure 1 為研究設計與兩階段 benchmark 流程）。[(ref: main Figure 1, §2.2–§2.3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F1)

## 背景／問題

作者的出發點是：飲食記錄是糖尿病自我管理的基礎，第 1 型糖尿病中依記錄準確計算碳水與血糖在目標範圍內的時間有關，第 2 型糖尿病與糖尿病前期中持續自我監測與 HbA1c 和體重下降有關；但手動記錄負擔重、依從性會隨時間下降。這幾點作者都附有引用文獻（refs 1–6）。[(ref: main Introduction)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

「拍照交給多模態 LLM 就能減輕記錄負擔」則是作者要檢驗的對象，而不是前提：本文的問題是，現成的通用模型從一張餐點照片估出來的營養素、品項與飲食品質，與參與者自填的飲食回顧差多少，這個差距在糖尿病照護的哪些用途上還可以接受。論文沒有直接量測使用者負擔或依從性。

## 方法摘要

**三項任務。** 作者把影像飲食評估拆成三個層級：(1) 每餐的熱量與營養素估計（熱量、碳水化合物、蛋白質、脂肪、纖維），主要指標為 MAPE（mean absolute percentage error）；(2) 每餐的食物品項辨識，主要指標為 Sørensen–Dice coefficient；(3) 每日的飲食品質，以 HEI-2020（Healthy Eating Index，0–100 分）總分的 RMSE 為主。[(ref: main §2.1, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T1)

**資料。** 主資料集 SNAPMe 來自 95 位美國參與者，共 1,680 張餐前照片、275 個參與者日；參與者拍照並填寫 ASA24 飲食回顧，參考營養值來自這份自填回顧，不是秤重；每張照片都附一張 1.5 × 1.5 吋的黑白紙製尺寸標記。另一個 ASA24 portion dataset 從 167 種有五種份量（1×–5×）影像的食物中隨機抽 100 種，只用於份量敏感度分析。[(ref: main §2.2.1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full) [(ref: main §2.2.2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#sec-10)

**模型與 prompt。** 八個透過 OpenAI、Google AI 或 TogetherAI API 呼叫的多模態 LLM：GPT-4o mini、GPT-5.2、Gemini 3 Pro Preview、Gemini 2.5 Flash-Lite、Qwen3-VL-8B-Instruct、Qwen3-VL-32B-Instruct、Llama-4-Maverick-17B-128E-Instruct-FP8、Gemma-3n-E4B-it。每個模型都跑兩種 prompt：直接輸出 JSON、不給推理指引的 no-CoT，以及依序要求辨識食材、估計份量與營養素、彙總到餐、估計 HEI 變項、最後自我一致性檢查的 structured CoT。[(ref: main §2.3.1–§2.3.2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

**兩階段評估。** Phase 1 在 80 張照片的子集（隨機 15 位參與者的第一個記錄日）上跑 8 個模型 × 2 種 prompt 共 16 組，每家供應商取最佳組合成為 finalist；Phase 2 在完整 SNAPMe 上評估三個 finalist，再對最佳模型做餐別、份量、尺寸標記、可見度與品項數的深入分析（論文 Results 把這部分稱為 Phase 3）。[(ref: main §2.3.4, §3.1–§3.3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

## 方法詳解

**執行設定。** prompt 放在 system role、照片作為 user content；可設定時 temperature 為 0.0；每個「照片 × 模型」組合跑三次，營養數值取三次的中位數，食物品項只保留三次中至少出現兩次的項目。輸出為 JSON，包含食材與整餐層級的營養估計及 HEI 相關的份量變項，不適用的數值欄填 0。[(ref: main §2.3.2–§2.3.3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

**指標細節。** MAPE 是排名所用的主要指標；參考值低於 1 g 或 1 kcal 時另有 near-zero 規則（論文 Table 3 的例子中，參考值為 0 時 APE 記為 NA）。次要指標包括 MAE、RMSE、平均與中位數 signed bias、碳水估計落在 ±10 g 內的餐點比例與 Pearson r。Dice 在品項名稱正規化後，以寬鬆的一對一配對計算（例如預測的 "rice" 可配對參考的 "brown rice"）。HEI-2020 依 NCI 指引，由模型預測的食物群份量、營養素與熱量計算。[(ref: main §2.1, Table 3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T3)

**統計。** 以參與者為單位做 2,000 次 bootstrap 重抽（抽到的參與者保留其全部照片或參與者日）求 95% CI；finalist 之間的比較取配對差的 bootstrap CI，每個指標做兩次比較的 Bonferroni 校正（97.5% CI）；prompt 比較與次要比較用配對 Wilcoxon signed-rank test。[(ref: main §2.4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

**深入分析的設計。** 份量敏感度用 ASA24 portion dataset 看預測值是否隨 1×–5× 份量成比例增加；尺寸標記分析比較無標記、真實大小、人為放大與人為縮小四種條件；可見度分析比較所有品項皆可見與有品項被遮住的餐點（各 43 餐）；品項數分析看 Dice 隨每餐品項數的變化。[(ref: main §2.4.1–§2.4.5)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

- **論文未交代** — prompt 全文與 MAPE 的計算公式只在補充材料（SM6、Supplementary Methods），正文沒有；near-zero 規則在正文只說明門檻，未說明這些餐點如何計分。
- **論文未交代** — 模型輸出無法解析或呼叫失敗時如何處理、發生幾次，正文沒有報告；各模型的存取日期也未列出。
- **論文未交代** — Dice 在預測或參考品項清單為空時如何計算；HEI 分析使用 272 個有效參與者日（Figure 3 圖說），少掉的 3 個參與者日排除原因未說明。
- **論文未交代** — Phase 1 的 16 組完整數值只在補充 Table S2；Gemini 3 Pro 在子集上的營養素 MAPE 最低，正文說明 Google 的 finalist 改選 Gemini 2.5 Flash-Lite 是因為它在 Dice 與 HEI 上較好，但沒有給出兩者的完整對照數值。
- **論文未交代** — 評估框架 SeeFood benchmark 的程式碼要到正式發表才釋出，目前無法重跑。

## 資料與實驗

下表整理兩個資料集與兩個評估階段的規模，取自論文 §2.2、§2.3.4 與 Figure 3 圖說（HEI 有效參與者日數）。[(ref: main §2.2, §2.3.4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full) [(ref: main Figure 3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F3)

| 資料／階段 | 規模 | 參考標準 | 用途 |
|---|---|---|---|
| SNAPMe（完整） | 95 位參與者、275 個參與者日、1,680 張餐前照片 | 參與者自填 ASA24 飲食回顧（非秤重） | Phase 2 三個 finalist 的評估與最佳模型的深入分析 |
| SNAPMe Phase 1 子集 | 80 張照片（隨機 15 位參與者的第一個記錄日） | 同上 | 8 個模型 × 2 種 prompt 篩選 finalist |
| ASA24 portion dataset | 100 種食物（從 167 種有五種份量影像的食物中隨機抽出）× 1×–5× 份量 | ASA24 影像庫的份量設定 | 只用於份量敏感度分析 |
| HEI-2020 分析 | 272 個有效參與者日 | 由 ASA24 回顧計算的 HEI-2020 | 日層級飲食品質 |

下表為 Phase 2 三個 finalist（皆用 CoT）在完整 SNAPMe 上的主要數值，取自 §3.2 正文與 Table 2 對應的敘述；方括號為 95% CI。正文把碳水 MAPE 的 92.5% 與 111.6%、碳水 MAE 的 14.8 g 與 15.8 g、HEI RMSE 的 12.27 與 12.65 列為「另兩個模型」的數值，未逐一對應，本表不指派。[(ref: main §3.2, Table 2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T2)

| 指標 | GPT-4o mini | Gemini 2.5 Flash-Lite | Llama 4 Maverick |
|---|---|---|---|
| 碳水化合物 MAPE | 73.4% | 92.5% 或 111.6% | 92.5% 或 111.6% |
| 碳水化合物 MAE | 13.3 g [12.4–14.3] | 14.8 g 或 15.8 g | 14.8 g 或 15.8 g |
| 碳水估計落在 ±10 g 內的餐點 | 57% | — | — |
| 熱量平均 bias | −61 kcal [−74 至 −50] | +30 kcal [17 至 43] | 平均低估（正文未給數值） |
| 碳水平均 bias | −5.0 g [−6.4 至 −3.7] | +4.7 g [3.2 至 6.3] | 平均低估（正文未給數值） |
| 蛋白質平均 bias | — | +1.3 g [0.7 至 1.9] | 平均低估（正文未給數值） |
| HEI-2020 RMSE（分） | 12.54 | 12.27 或 12.65 | 12.27 或 12.65 |

下表為最佳模型 GPT-4o mini 依餐別的熱量 MAPE，取自 §3.3.1。[(ref: main §3.3.1, Figure 4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F4)

| 餐別 | 熱量 MAPE |
|---|---|
| 晚餐 | 43.4% |
| 午餐 | 58.9% |
| 早餐 | 88.8% |
| 點心 | 94.3% |
| 只有飲料 | 312.3% |

## 結果

- **Phase 1：沒有任何組合把單一營養素的 MAPE 壓到 43% 以下** — 16 組的平均營養素 MAPE 介於 57.6% 到 99.3%，最低的是 Gemini 3 Pro（57.6%）。[(ref: main §3.1.1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- **CoT 幫到的主要是品項辨識** — CoT 對熱量、蛋白質、脂肪與 HEI-2020 在任何模型上都沒有顯著改善；有四個模型的 Dice 顯著提高，Llama 4 Maverick 的受益最廣（品項辨識、碳水、纖維與平均 MAPE）。[(ref: main §3.1.1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- **較新、較大的模型不一定較好** — GPT-5.2 在營養素 MAPE、Dice 與 HEI RMSE 三個面向都輸給 GPT-4o mini。[(ref: main §3.1.1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- **Phase 2：GPT-4o mini 各項 MAPE 最低，但只有碳水與纖維的差距有統計支持** — 碳水 MAPE 73.4%，另兩個 finalist 為 92.5% 與 111.6%；摘要報告的整體 MAPE 範圍為 52%–90%，討論段說明 GPT-4o mini 每一項都超過 50%。[(ref: main Abstract, §3.2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T2)
- **系統性偏差方向因模型而異** — GPT-4o mini 平均低估熱量（−61 kcal）與碳水（−5.0 g），Gemini 2.5 Flash-Lite 平均高估熱量（+30 kcal）、碳水（+4.7 g）與蛋白質（+1.3 g）；各模型的中位數誤差接近 0，作者指出平均偏差主要由少數大誤差造成。[(ref: main §3.2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T2)
- **相關性中等** — GPT-4o mini 的熱量與營養素 Pearson r 為 0.53–0.75；三個模型中脂肪最弱（r 0.49–0.58），蛋白質最強（r 0.73–0.76）。[(ref: main §3.2, Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)
- **品項辨識兩極化** — 三個模型約 30%–34% 的餐點品項完全辨識正確（Dice = 1），約 21%–23% 完全沒對上（Dice = 0），模型之間的 Dice 差距不顯著。[(ref: main §3.2, Figure 3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F3)
- **HEI-2020 誤差以 0 為中心** — 三個模型的 RMSE 為 12.27–12.65 分，與參考 HEI 的相關 r 0.61–0.65。[(ref: main §3.2, Figure 3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F3)
- **飲料是最大的漏洞** — GPT-4o mini 的熱量 MAPE 在晚餐 43.4%，只有飲料的餐達 312.3%，飲料的熱量 MAE 為 48.6 kcal、碳水 MAE 7.5 g；作者指出溶在飲料裡的糖或蜂蜜在照片上看不到。[(ref: main §3.3.1)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F4)
- **份量越大越低估** — 估計值會隨份量增加，但在 4× 與 5× 份量時，預測的熱量倍率中位數停在約 2–3 倍，大約只有真實倍率的一半。[(ref: main §3.3.2)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F4)
- **尺寸標記沒有幫助** — 無標記、真實大小、人為放大、人為縮小四種條件下，各營養素的誤差都沒有顯著變化。[(ref: main §3.3.3)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F4)
- **看得到才認得出，但認得出不代表算得準** — 所有品項皆可見的餐點 Dice 0.74，有品項被遮住時 0.45（各 43 餐，p < 0.001）；1–4 個品項時 Dice 約 0.6–0.7，13 個以上低於 0.3。在 4 個品項的 141 餐中，Dice 與五種營養素誤差都沒有顯著相關（r −0.035 至 −0.162）。[(ref: main §3.3.4)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F4)
- **作者的臨床判斷** — 碳水 MAE 13.3 g 超過作者引用的 ±10 g 門檻（超過此範圍胰島素劑量可能受影響），約 43% 的餐點落在範圍外且高估低估都有；作者結論是目前的多模態 LLM 不適合用於胰島素劑量或無監督的臨床使用，可能的低風險用途（研究用回顧的輔助、諮詢時的食物群質性回饋、追蹤飲食變化）仍待驗證。[(ref: main Discussion, Conclusion)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

## 限制

**作者自述的限制。** 資料只來自美國，參考值是自填飲食回顧、本身也有誤差；Phase 1 只用 80 張照片篩選，可能影響哪些模型進入 Phase 2；MAPE 在參考值接近 0 時會被放大，Dice 對每個品項一視同仁、不考慮營養上的重要性；所有模型共用同一個 prompt，沒有針對個別模型最佳化，也沒有提供用餐時間、病史或飲食限制等脈絡；只評估單次估計的準確度，沒有評估追蹤個人飲食變化的能力；模型排名反映評估當時可用的版本。作者另在後續方向（§4.6）指出需要人類（例如營養師）基線的比較。[(ref: main §4.5–§4.6)](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full)

**本書庫的觀察。**

- **參考標準與模型誤差混在一起** — 參考值來自參與者自填的 ASA24 回顧，論文量到的 MAPE 是「模型估計」與「自填回顧」的差，不是與真實攝取量的差；在沒有秤重參考的情況下，無法分出多少誤差屬於模型。
- **沒有同條件的人類對照** — 討論中提到的專家熱量估計 MAPE 約 55% 來自另一個 20 張照片的資料集，與本文的 SNAPMe 不可直接比較；「模型是否已接近人類估計」本文無法回答。
- **finalist 的選擇規則影響結論範圍** — 每家供應商只取一個 finalist，且 Google 的 finalist 不是子集上 MAPE 最低的 Gemini 3 Pro；完整資料上的排名只涵蓋這三個組合，不能外推成八個模型的排名。
- **另兩個 finalist 的數值在正文中未對應到模型** — 碳水 MAPE、MAE 與 HEI RMSE 只有 GPT-4o mini 的數值可以確定歸屬，比較 Gemini 2.5 Flash-Lite 與 Llama 4 Maverick 時需要回到 Table 2 原表。

## 與書庫其他文章的關係

膀胱鏡那篇同樣把未經醫療訓練的通用多模態 LLM 經 API 套在臨床照片上，並比較不同 prompt 策略與棄答門檻；本篇把場景換到參與者自己拍的餐點照片，比較 8 個模型與 CoT／no-CoT 兩種 prompt，並發現較新的 GPT-5.2 不如 GPT-4o mini: [膀胱鏡影像交給通用多模態 LLM：提示詞與棄答門檻能換到多少可靠度？](2026-09-21-mllm-cystoscopy-bladder-triage.md)

## 實務的啟發

- **可借用的量測方法** — 評估影像飲食估計時，除了 MAPE，同時報告「落在臨床門檻內的比例」（本篇的 ±10 g 碳水）與 signed bias 的方向；本篇最佳模型的平均 MAPE 與 MAE 看起來差距不大，但 43% 的餐點超出門檻、且不同模型系統性偏向相反方向，只看平均誤差會漏掉這些資訊。
- **可借用的量測方法** — 把飲料、份量倍率、遮擋與品項數拆開分析；本篇在這幾個面向上找到明確的失效模式（只有飲料的餐 MAPE 312.3%、大份量只估到約一半、有遮擋時 Dice 從 0.74 掉到 0.45），比整體 MAPE 更能指出模型在哪裡不能用。
- **待驗證的警訊** — 照片裡的尺寸標記沒有改善營養估計，品項辨識正確也與營養素誤差無顯著相關；若產品設計依賴「放一個參考物」或「先認對食物」來提升份量估計，本篇的結果不支持這個假設，需要在自己的資料上驗證。
- **待驗證的警訊** — CoT 主要改善品項辨識而非營養數值；在這類任務上，不能預設加入推理步驟就會讓數值估計更準。
- **證據強度** — 單一美國公開資料集、參考值為自填回顧、無人類基線、prompt 未個別最佳化的回溯性 benchmark 預印本；它支持「在 SNAPMe 上，這幾個現成多模態 LLM 從單張照片估計營養素的誤差仍大，不足以支撐胰島素劑量計算」，不足以支持任何一個模型可直接用於臨床飲食評估，也不足以判定低風險用途已經可行。

## References

- **main** — Gravellier L, Zhang C, Wu Y, Parameswaran V, Scheideman A, Shao M, Zhang E, Perelman D, Gardner C, Klonoff DC, Ræder H, Snyder MP, Wang T. *Image-Based Dietary Assessment Using Multimodal Large Language Models: Performance, Limitations, and Clinical Applicability in Diabetes*. medRxiv. 2026. DOI: 10.64898/2026.10.21.26365949（v1 預印本）。摘要頁：<https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1>；全文 HTML：<https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full>；PDF：<https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full.pdf>。文內引用位置：author block、Abstract、Introduction、§2.1–§2.4、§3.1–§3.3、Discussion、Limitations、Conclusion、Data and code availability；深鏈 [§2.2.2](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#sec-10)、[Table 1](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T1)、[Table 2](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T2)、[Table 3](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#T3)、[Figure 1](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F1)、[Figure 3](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F3)、[Figure 4](https://www.medrxiv.org/content/10.64898/2026.10.21.26365949v1.full#F4)。
- **doi** — <https://doi.org/10.64898/2026.10.21.26365949>。

[Home](../) · [AI Papers](./)
