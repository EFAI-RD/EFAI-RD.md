---
catalog_id: "doi:10.1038/s44401-026-00114-y"
editors:
  - "Clare"
refs:
  main:
    title: "A multi-site benchmarking framework for scalable extraction of geriatric care constructs from electronic health records"
    url: "https://www.nature.com/articles/s44401-026-00114-y"
status: published
skill_version: "write-ai-paper@2.8"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 規則引擎、GPT-4o 與微調小模型，誰讀得懂病歷裡的老年照護？四家院所、41 個構念的基準

## 來源

- 團隊：UTHealth Houston McWilliams School of Biomedical Informatics 主導，聯合 Mayo Clinic、Memorial Hermann Health System、UTMB、University of Pittsburgh、Beth Israel Deaconess Medical Center、Hebrew SeniorLife／Harvard Medical School、MD Anderson 等機構；共二十六位作者，第一作者 Sunyang Fu，通訊作者 Hongfang Liu。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)
- 論文：*A multi-site benchmarking framework for scalable extraction of geriatric care constructs from electronic health records*，刊於 *npj Health Systems* 3(1):93，2026-09-16 出版。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)
- 識別碼：[DOI: 10.1038/s44401-026-00114-y](https://doi.org/10.1038/s44401-026-00114-y)；PMID 42749862；PMCID PMC13582951。
- 全文：[npj Health Systems 官方 HTML 全文](https://www.nature.com/articles/s44401-026-00114-y)，開放取用，授權為 CC BY。
- 取用說明：本次以出版社 HTML 全文逐節核對；文中表與圖的 ref 指向該頁的 `#Tab1`、`#Tab2`、`#Fig1`–`#Fig5` 錨點。

**編輯：** Clare

這篇論文把「從病歷自由文字抽取老年照護構念」做成一個跨四家院所、41 個概念的公開基準，然後讓規則引擎、通用 LLM 與微調小模型在同一把尺上比，結論是三者各有各的破法。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

## 流程

![左圖為三種方法在 41 個構念上的 macro F1 與 micro F1 對比：GPT-4o 0.56／0.87、MedAgingIE 0.55／0.92、Qwen2-7B-Instruct 0.30／0.81，三者的 macro 與 micro 之間都有巨大落差；右圖為 macro precision 與 macro recall 的對比，GPT-4o 為 0.47／0.83 的高召回低精確，MedAgingIE 為 0.75／0.49 的高精確低召回，恰好互為鏡像，Qwen2-7B-Instruct 則是 0.26／0.50](assets/llm-geriatric-ehr-multisite-benchmark.png)

圖：本書庫依論文 Fig. 2 報告的 macro／micro 平均值重畫，數值逐格取自該圖，未加入任何本文推論。左圖呈現 macro 與 micro 的落差，右圖呈現兩個領先方法在 precision 與 recall 上的反向配置。[(ref: main Fig. 2)](https://www.nature.com/articles/s44401-026-00114-y#Fig2)

## 背景／問題

老年醫學的照護規劃高度依賴一組結構化評估：Comprehensive Geriatric Assessment（CGA，全面性老年評估）以及以 Mentation、Mobility、Medication、What Matters 為軸的 4Ms 框架。這些構念在臨床上決定了照護方向，但在電子病歷（electronic health record，EHR）裡多半只存在於敘事式的自由文字中，沒有對應的結構化欄位可以直接查詢。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

因此要把這些構念拿來做族群層級的研究或品質監測，就得先做資訊抽取。問題是，過去的抽取工作多半綁在單一機構的資料與單一方法上，既難以判斷方法之間的高下，也難以判斷結論換一家醫院還成不成立。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

這篇論文要補的就是這個缺口：建立一個跨院所、涵蓋 41 個 CGA／4Ms 構念的標註資料集與評估框架，並在同一套資料上同時比較三種典型技術路線——符號式規則、生成式通用模型、以及指令微調的開源小模型。[(ref: main Table 2)](https://www.nature.com/articles/s44401-026-00114-y#Tab2)

## 方法摘要

資料面，研究者從四家性質互異的院所各取 100 位 65 歲以上病人的臨床紀錄，合計 400 份，由臨床團隊逐句標註，產出 49,195 句的黃金標準集。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y) [(ref: main Table 1)](https://www.nature.com/articles/s44401-026-00114-y#Tab1)

任務被定義成句子層級的分類：判斷每一句是否提及 41 個構念中的某一個。構念分屬四個領域，分別是 Goals of Care and Advanced Care Planning、Socioeconomic Status、Cognitive and Behavioral Status，以及 Mobility and Functional Status。[(ref: main Table 2)](https://www.nature.com/articles/s44401-026-00114-y#Tab2)

方法面，三條路線放在同一套測試集上比：GPT-4o 走 in-context learning，MedAgingIE 是以 LLM 輔助建規則、但最終由決定性規則引擎判斷的混合式系統，Qwen2-7B-Instruct 則是以 LoRA 做指令微調的開源模型。[(ref: main Fig. 5)](https://www.nature.com/articles/s44401-026-00114-y#Fig5)

## 方法詳解

**四個站點的取樣。** UTPhysicians（UTP）代表門診與專科紀錄，Memorial Hermann Health System（MHHS）代表住院紀錄，Harris County Psychiatric Center（HCPC）代表精神科住院紀錄，Beth Israel Deaconess Medical Center 則以公開的 MIMIC 重症紀錄代表。前兩者同時供訓練與測試，後兩者僅供測試。取樣刻意偏向較長、概念密度較高的紀錄，以提高罕見構念的覆蓋率。[(ref: main Table 1)](https://www.nature.com/articles/s44401-026-00114-y#Tab1)

**標註與一致性。** 標註團隊由一位老年科醫師、一位資深臨床資料摘錄員與兩位醫學生組成，由資深老年科醫師與臨床資訊學者督導，流程以 TRUST 框架為基礎分階段精修 schema。第一階段以 25 份隨機文件衡量偽陽性與偽陰性，第二階段以 120 份分層抽樣文件確保每個概念至少出現三次。以各標註者對多數決的 F1 衡量標註者間一致性（inter-annotator agreement，IAA），兩階段平均分別為 0.845 與 0.919；歧異由督導者共識裁決。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

**GPT-4o。** 以結構化提示搭配 3-shot 範例，提示中包含任務說明、類別定義、輸出限制與格式規則；提示經與領域專家諮詢後反覆精修。研究者另評估過 GPT-4.1、O1 與 O4-mini，最後基於效能與成本的平衡選用 GPT-4o。[(ref: main Fig. 5)](https://www.nature.com/articles/s44401-026-00114-y#Fig5)

**MedAgingIE。** 這是本研究自建的混合式系統：以既有的老化領域 NLP 模型為原型，由 GPT-4o 擔任「智慧層」協助同義詞擴充、錯誤分析與規則生成，但最終判斷交給決定性的規則引擎，而非生成式推論。規則與本體都是人類可讀、可稽核的形式，並在訓練資料上反覆精修至最佳。[(ref: main Fig. 5)](https://www.nature.com/articles/s44401-026-00114-y#Fig5)

**Qwen2-7B-Instruct。** 以 LoRA（Low-Rank Adaptation）做參數高效微調，把句子分類到 41 個預定義類別。訓練資料為 52,253 則臨床片段，以 distant supervision 從 2012–2022 年的 EHR 取得銀標準標註，採 80／20 訓練驗證切分、負正比 3:1、20 個 epoch、學習率 1 × 10⁻⁴。[(ref: main Fig. 5)](https://www.nature.com/articles/s44401-026-00114-y#Fig5)

**評估設計。** 同時報告 micro 與 macro 平均：micro 把所有實例的 TP／FP／FN 彙總，因此由高頻概念主導；macro 對 41 個概念各自計算再等權平均，因此罕見概念與常見概念等價。統計檢定採句子層級的配對 bootstrap 重抽（1,000 次）、95% 信賴區間，並以 Bonferroni 校正多重比較。[(ref: main Fig. 3)](https://www.nature.com/articles/s44401-026-00114-y#Fig3)

## 資料與實驗

下表是本書庫依論文 Table 1 整理的四個站點設計。四家院所的照護型態刻意拉開，且其中只有一家的資料是公開的。[(ref: main Table 1)](https://www.nature.com/articles/s44401-026-00114-y#Tab1)

| 站點 | 照護型態 | 樣本 | 紀錄特性 | 用途 |
|---|---|---|---|---|
| UTPhysicians（UTP） | 門診／專科 | 100 位 ≥65 歲病人 | 門診紀錄、功能評估 | 訓練＋測試 |
| Memorial Hermann（MHHS） | 住院 | 100 位 ≥65 歲病人 | 密集的住院文件 | 訓練＋測試 |
| Harris County Psychiatric Center（HCPC） | 精神科住院 | 100 位 ≥65 歲病人 | 偏重行為與認知 | 僅測試 |
| Beth Israel Deaconess（MIMIC） | 重症 | 100 位 ≥65 歲病人 | 詳細護理與 ICU 紀錄 | 僅測試（公開資料） |

黃金標準集合計 400 份臨床紀錄、49,195 個完整標註句；Qwen2 的微調另使用 52,253 則以 distant supervision 取得的銀標準片段。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

41 個構念分屬四個領域，數量分布如下。[(ref: main Table 2)](https://www.nature.com/articles/s44401-026-00114-y#Tab2)

| 領域 | 構念數 | 代表項目 |
|---|---:|---|
| Goals of Care and Advanced Care Planning | 4 | 預立醫療指示、維生治療限制、安寧、緩和醫療 |
| Socioeconomic Status | 5 | 經濟壓力、糧食與居住不安全、社會家庭支持、就業、保險 |
| Cognitive and Behavioral Status | 14 | 譫妄、意識狀態改變、認知障礙、憂鬱、焦慮、躁動、幻覺、妄想等 |
| Mobility and Functional Status | 18 | 跌倒、身體活動、日常生活活動（沐浴／穿衣／進食／如廁／移位等）、工具性日常生活活動 |

下表重製論文 Fig. 2 報告的整體效能，是本研究的主要結果。[(ref: main Fig. 2)](https://www.nature.com/articles/s44401-026-00114-y#Fig2)

| 方法 | macro precision | macro recall | macro F1 | micro F1 |
|---|---:|---:|---:|---:|
| GPT-4o（in-context learning） | 0.47 | 0.83 | 0.56 | 0.87 |
| MedAgingIE（規則＋LLM 混合） | 0.75 | 0.49 | 0.55 | 0.92 |
| Qwen2-7B-Instruct（LoRA 微調） | 0.26 | 0.50 | 0.30 | 0.81 |

論文另以 Fig. 3 報告各站點的 micro F1 與信賴區間，以 Fig. 1 報告四個站點的標註分布熱圖，以 Fig. 4 以 Sankey 圖呈現三種方法的錯誤型態流向。這些圖以圖形方式呈現，論文正文未逐格列出對應數值，本文因此不轉述其個別數字。[(ref: main Fig. 1)](https://www.nature.com/articles/s44401-026-00114-y#Fig1) [(ref: main Fig. 3)](https://www.nature.com/articles/s44401-026-00114-y#Fig3) [(ref: main Fig. 4)](https://www.nature.com/articles/s44401-026-00114-y#Fig4)

## 結果

- **micro 與 macro 的落差是本研究最一致的訊號** — 三種方法的 micro F1 都在 0.81 以上，但 macro F1 最高只有 0.56。換句話說，高頻概念抽得不錯，而 41 個概念等權之後成績立刻塌下來。[(ref: main Fig. 2)](https://www.nature.com/articles/s44401-026-00114-y#Fig2)
- **整體 micro F1 由混合式系統領先** — MedAgingIE 0.92，其次 GPT-4o 0.87，最後 Qwen2-7B-Instruct 0.81。[(ref: main Fig. 2)](https://www.nature.com/articles/s44401-026-00114-y#Fig2)
- **兩個領先方法的 macro F1 幾乎打平，但走法相反** — GPT-4o 是 precision 0.47、recall 0.83 的高召回配置，MedAgingIE 是 precision 0.75、recall 0.49 的高精確配置，macro F1 分別為 0.56 與 0.55。[(ref: main Fig. 2)](https://www.nature.com/articles/s44401-026-00114-y#Fig2)
- **概念之間的離散度很大** — 論文指出各概念 F1 分布廣泛，安寧、經濟壓力、大小便控制等明確定義的概念表現穩定，而譫妄、思考紊亂、躁動、用藥管理等則普遍偏弱；作者據此表示現有方法都還沒有完整處理這批概念的語意與脈絡需求。[(ref: main Fig. 2)](https://www.nature.com/articles/s44401-026-00114-y#Fig2)
- **公開資料上的成績明顯高於院內資料** — 論文寫明「所有方法在公開資料集上的表現都顯著高於私有 EHR 資料」，並提出三種可能：去識別化帶來的相對同質性、廣為研究的語料可能造成的資料洩漏，以及只用公開資料評估會高估泛化能力。[(ref: main Fig. 3)](https://www.nature.com/articles/s44401-026-00114-y#Fig3)
- **生成式方法的跨院變異大於符號式方法** — 論文表示生成式路線在不同機構之間的效能變異較大，符號式模型相對穩定。[(ref: main Fig. 3)](https://www.nature.com/articles/s44401-026-00114-y#Fig3)
- **錯誤型態隨技術路線而不同** — 生成式方法（GPT-4o、Qwen2）的典型錯誤是概念混淆、遺漏與完全幻覺；規則式的 MedAgingIE 則是隱含推論、指引判定、否定與排除類的錯誤，整體呈現保守抽取的風格。[(ref: main Fig. 4)](https://www.nature.com/articles/s44401-026-00114-y#Fig4)
- **標註品質本身是可查核的** — 兩階段 IAA 平均為 0.845 與 0.919，歧異由資深老年科醫師與臨床資訊學者共識裁決。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)
- **跨站點的概念重疊只是中等** — 論文報告 41 個概念中有 20 個在四個站點都出現、39 個至少出現在兩個站點，站點之間的 pairwise Jaccard similarity 介於 0.571 到 0.795。[(ref: main Fig. 1)](https://www.nature.com/articles/s44401-026-00114-y#Fig1)

## 限制

論文自列三項限制。第一，取樣刻意偏向較長、概念密度較高的紀錄，這提高了罕見概念的覆蓋率，但可能限制外部效度。第二，即使經過多站點精修，標註 schema 仍可能帶有機構偏誤，未必能完整推廣到未見過的照護場景或文件書寫風格。第三，句子層級、單一標籤的任務設定本身是一個結構性限制，因為臨床文字經常在一句裡疊加多個概念，也經常跨句相依。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

倫理方面，研究經 UT Physicians、Memorial Hermann Health System 與 Harris County Psychiatric Center 的 IRB 與倫理委員會核准（IRB#: HSC-MS-25-1090、HSC-SBMI-23-0765、HSC-SBMI-24-0403、HSC-SBMI-17-0354）。資料可得性聲明為本研究未產生或分析新的資料集。[(ref: main)](https://www.nature.com/articles/s44401-026-00114-y)

以下幾點是本書庫對照全文與圖表後的觀察，不是論文的結論：

- **百分比與分母對不起來** — 論文寫「41 個概念中有 20 個（44.4%）在四站皆現、39 個（86.7%）至少出現在兩站」。以 41 為分母，20 應為 48.8%、39 應為 95.1%；而 44.4% 與 86.7% 恰好都對應分母 45。引用這兩個比例前值得先回頭確認分母。[(ref: main Fig. 1)](https://www.nature.com/articles/s44401-026-00114-y#Fig1)
- **macro F1 才是這個任務該看的數字** — micro F1 0.92 讀起來像可以上線，macro F1 0.55 讀起來像還早。差別來自加權：老年照護真正想抓的往往就是低頻但高風險的那幾個（譫妄、躁動、用藥管理），而它們正是被 micro 平均稀釋掉、也正是各方法表現最弱的一群。
- **precision 與 recall 的反向配置意味著這是一個選擇題，不是排名題** — 若用途是族群層級的篩選與後續人工複核，GPT-4o 的高召回比較合用；若用途是直接進入報表或品質指標，MedAgingIE 的高精確比較安全。把兩者用單一 F1 排名，會掩蓋掉這個實際上更重要的分歧。
- **公開資料成績較高這件事，作者已經自己點名了資料洩漏的可能** — 這在方法論上比多零點幾的 F1 更值得記住：只在 MIMIC 上驗證的抽取模型，其報告數字可能同時受惠於去識別化的同質性與語料的高曝光度。本書庫認為這支持一個實務原則——院內導入前務必在院內資料重測。
- **混合式系統的「可稽核」是一個容易被低估的規格** — MedAgingIE 的最終判斷來自決定性規則引擎，規則與本體是人類可讀的。當抽取結果要支撐品質指標或研究族群定義時，能逐條指出「為什麼這句被判為譫妄」的價值，通常高於幾個百分點的 F1。
- **微調小模型落後，但條件並不對等** — Qwen2-7B-Instruct 的訓練標註來自 distant supervision 的銀標準，而非黃金標準。它的 0.30 macro F1 說明的是「這個資料條件下的 LoRA 微調」表現，不足以推論「7B 級開源模型做不到這個任務」。

## 與書庫其他文章的關係

MedicalBench 量的是 LLM 在病歷裡抽取隱性醫學概念的能力，本篇則把同一件事放到四家院所、41 個老年照護構念上，並加上規則式與微調式的對照組: [MedicalBench：讓 LLM 指出病歷證據，隱性概念抽取真的更準嗎？](2026-09-17-medicalbench-concept-extraction.md)

nMAS 把心衰竭特徵從病歷抽出來供下游使用，本篇則回答上游那一步能做到多準，以及不同技術路線的誤差型態差在哪裡: [Tracing the Heart：用多代理管線追蹤心衰竭特徵的證據來源](2026-09-15-tracing-the-heart.md)

胸片結核篩檢的稽核顯示換一個評估條件結論就未必成立，本篇則在四家院所之間看到同一件事的文字版本，且作者明確點名公開資料可能高估泛化: [稽核胸片結核篩檢的醫療 VLM：換一個評估條件，哪一種結論還站得住？](2026-09-21-cxr-tb-vlm-portability-audit.md)

醫療 LLM 評估落差那篇談的是研究設計層面的嚴謹度，本篇則提供一個具體示範：同一批模型在 micro 與 macro 兩種平均下，可以得到截然不同的可用性判斷: [醫療 LLM 評估落差：研究更嚴謹，為何證據反而更舊？](2026-09-17-medical-llm-evaluation-gap.md)

## 實務的啟發

第一，驗收資訊抽取時，micro 與 macro 兩個平均都要求，而且要先講清楚哪一個才對應用途。本篇最直接的教訓是同一組模型在兩種平均下的差距可以大到 0.36（0.92 對 0.56）。只報一個數字的驗收報告，等於讓供應商挑對自己有利的那一個。

第二，把 precision 與 recall 的配置當成需求規格來寫，而不是等模型交付後再看。高召回配置適合「先撈出來再人工複核」的族群篩選，高精確配置適合「直接進報表」的品質指標。本篇兩個領先方法的 macro F1 只差 0.01，但一個是 0.47／0.83、另一個是 0.75／0.49，選錯邊的成本遠大於那 0.01。

第三，公開資料上的成績不要當成院內成績的預估值。本篇四個站點裡表現最好的正是公開的 MIMIC，而作者自己把資料洩漏列為可能原因之一。院內導入的驗收基準應該建立在院內自己的標註資料上，哪怕規模小很多。

第四，別預設規則式方法已經被淘汰。本篇的混合式系統在整體 micro F1 上領先兩個生成式對手，跨院變異也較小，而且保有逐條可稽核的性質。比較務實的讀法是：用 LLM 來加速建規則與做錯誤分析，把最終判斷留給可檢查的引擎。

最後，標註成本不是可以省掉的項目。本篇的 49,195 句黃金標準、兩階段 IAA 0.845 與 0.919、以及共識裁決流程，是讓上面所有比較能夠成立的前提。少了這一層，任何「哪個模型比較好」的結論都無從驗證。

## References

- `main`：[npj Health Systems 官方 HTML 全文](https://www.nature.com/articles/s44401-026-00114-y)；本文使用其 [Table 1 研究場域與族群](https://www.nature.com/articles/s44401-026-00114-y#Tab1)、[Table 2 CGA 任務定義](https://www.nature.com/articles/s44401-026-00114-y#Tab2)、[Fig. 1 四站標註分布](https://www.nature.com/articles/s44401-026-00114-y#Fig1)、[Fig. 2 三方法效能](https://www.nature.com/articles/s44401-026-00114-y#Fig2)、[Fig. 3 跨站點效能](https://www.nature.com/articles/s44401-026-00114-y#Fig3)、[Fig. 4 錯誤型態 Sankey 圖](https://www.nature.com/articles/s44401-026-00114-y#Fig4) 與 [Fig. 5 模型開發與驗證流程](https://www.nature.com/articles/s44401-026-00114-y#Fig5)，以及 Introduction、Results、Discussion 與 Method 各節內文。
- `doi`：[10.1038/s44401-026-00114-y](https://doi.org/10.1038/s44401-026-00114-y)。

[Home](../) · [AI Papers](./)
