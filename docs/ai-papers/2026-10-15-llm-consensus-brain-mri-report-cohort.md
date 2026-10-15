---
catalog_id: "doi:10.64898/2026.10.06.26364312"
editors:
  - "Clare"
refs:
  main:
    title: "Large language model consensus for reliable research cohort construction from radiology reports: a retrospective cohort study"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 三個 LLM 都同意才自動貼標：6,718 份腦 MRI 報告分正常／異常，參考集零錯誤的代價是約一半報告退回人工

## 來源

- 團隊：Wushuang Rui（New York University 生物系）為第一作者，通訊作者為 Yiqiu Shen（NYU Center for Data Science；NYU Grossman School of Medicine 放射科；CAI2R）。其餘作者來自 NYU Center for Data Science、NYU Grossman School of Medicine 放射科、Bernard and Irene Schwartz Center for Biomedical Imaging、Center for Advanced Imaging Innovation and Research（CAI2R）與 University of Hawaii at Manoa 資訊與電腦科學系，全文共 10 位作者。[(ref: main author block)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- 論文：*Large language model consensus for reliable research cohort construction from radiology reports: a retrospective cohort study*，medRxiv 預印本 v1，2026-10-08 上線，授權 CC BY-NC-ND 4.0，未經同儕審查。[(ref: html)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full)
- 識別碼：DOI [10.64898/2026.10.06.26364312](https://doi.org/10.64898/2026.10.06.26364312)。
- 全文：[medRxiv 全文頁](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full)、[PDF v1](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)。
- 資料與程式：病歷資料因隱私與院內規範不公開；流程與分析程式碼公開於 [GitHub](https://github.com/WushuangRui/mri-report-llm-classification)。[(ref: main Data and code availability)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- 研究性質：單一機構回顧性研究，不是 pilot；核心流程（三個 LLM 各自分類、全體一致才自動貼標）有實作，在 680 份專家判讀參考集上評估並附 patient-level bootstrap 95% CI。分類只依報告文字，不看影像；參考集刻意加入較多正常報告，不代表全隊列的組成。[(ref: main Methods, Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- 證據邊界：本文數值以 PDF v1 的正文、Table 1 與 Table 2 為準；全隊列中「正常」與「異常」各自的報告數，論文只給合併的自動貼標比例，本文不另行推算。

**編輯：** Clare

作者讓三個 LLM 各自把腦 MRI 報告分成正常、只有非特異白質高訊號（WMH-only）或異常，只在三者全數同意正常或異常時才自動貼標；在 680 份專家參考集上，兩組三模型組合的自動貼標都沒有出錯，但只覆蓋 67%–71% 的參考報告、約 49%–52% 的全隊列報告，其餘留給人工。[(ref: main Abstract, Table 2)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

## 流程

![腦 MRI 報告多 LLM 一致性分類流程示意圖。上排由左到右三個方塊，以實線箭頭依序相連：藍色方塊為輸入（NYU Langone Health 門診影像中心 2014 年 10 月至 2020 年 10 月、6,718 份報告／5,856 位病人、以 regex 切成 indication、technique、findings、impression、other 五節）；綠色方塊為每個模型各自處理（同一個固定 prompt 與 JSON schema，先把報告轉成結構化 JSON、未提及欄位設為 null，再以零樣本輸出 1 normal／2 WMH-only／3 abnormal，temperature 0.2、每份報告跑一次）；橘色方塊為兩組三模型組合（Proprietary-inclusive：Qwen3-32B、Kimi-Linear-48B-A3B、GPT-5；Open-source：Qwen3-32B、Kimi-Linear-48B-A3B、DeepSeek-R1-Distill-Qwen-32B）。橘色方塊以斜向箭頭指向下排中間的紫色方塊 Unanimous-consensus rule（三者皆 normal 則自動貼為 NORMAL，三者皆 abnormal 則自動貼為 ABNORMAL，任一 WMH-only 或任何不一致則為 UNCERTAIN、退回人工判讀），紫色方塊再以箭頭指向右下灰色方塊 Evaluation（專家參考集 680 份：372 normal／90 WMH-only／218 abnormal；對照為單一 LLM、majority voting、ICD-10 二分；全隊列以 MRI 前後 10 天內的 active CNS ICD-10 診斷做一致性分析）。左下灰色方塊 Metrics 列出 assignment rate、assignment accuracy、normal／abnormal precision 與 recall、WMH-only deferral、2,000 次 patient-level bootstrap 的 95% CI，沒有箭頭連入或連出](assets/llm-consensus-brain-mri-report-workflow.png)

圖：本書庫依論文 Methods 與 Figure 1 圖說的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖。[(ref: main Methods, Figure 1)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

## 背景／問題

研究用的影像隊列常需要先把病人分成「影像正常」與「影像異常」。作者引用文獻指出，ICD-10 診斷碼反映的是症狀、病史或先前診斷，只能間接代表影像所見；放射報告較直接描述影像，但自由文字難以用規則或 bag-of-words 方法穩定分類；而把異常掃描誤當正常，會影響研究資料的有效性。[(ref: main Background)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

本研究的核心假設是「不同 LLM 在模稜兩可的報告上比較容易意見不一」，所以可以把不一致當成退回人工的訊號。這是作者提出的假設，背景段沒有引用文獻支持，結果段描述了不一致的報告組成，但沒有正式檢定這個假設。另一個設計前提是：只有非特異白質高訊號（WMH-only）的報告算不算「正常」，取決於研究問題，因此作者選擇一律不自動貼標；這一點作者有引用文獻討論。[(ref: main Background, Methods)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

## 方法摘要

**分類任務。** 每份腦 MRI 報告被分成三類：normal（腦實質無異常、結構符合年齡）、WMH-only（只有非特異白質病灶，或沒有急性或中風相關特徵的慢性缺血變化）、abnormal（WMH 以外的實質異常，例如梗塞、擴散受限、腫塊、出血、水腦，或有腦部手術、顱內治療史）。[(ref: main Methods, Listing 1)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**Multi-LLM consensus workflow。** 三個模型各自分類同一份報告；三者都說 normal 才貼正常，三者都說 abnormal 才貼異常；只要有一個模型說 WMH-only，或三者不一致，就列為 uncertain、留待人工判讀。作者組了兩組：proprietary-inclusive（Qwen3-32B、Kimi-Linear-48B-A3B、GPT-5）與 open-source（GPT-5 換成 DeepSeek-R1-Distill-Qwen-32B）。[(ref: main Methods, Figure 1)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**對照。** 單一 LLM（WMH-only 同樣列為 uncertain）、majority voting（有 WMH-only 就 uncertain，否則取多數），以及 ICD-10 二分（MRI 前後 10 天內有 active CNS 相關診斷即為異常，沒有 uncertain 類）。[(ref: main Methods)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**指標。** Assignment rate（被自動貼為正常或異常的比例）、assignment accuracy 與 error rate（自動貼標中與專家一致／不一致的比例）、normal／abnormal precision（貼正常／異常者中真的正常／異常的比例）、normal／abnormal recall（專家判為正常／異常的報告中，不經人工就被正確貼標的比例）、WMH-only deferral rate（專家判為 WMH-only 者中被列為 uncertain 的比例）。95% CI 以 2,000 次 patient-level bootstrap 計算。[(ref: main Methods, Statistical analysis)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

## 方法詳解

**報告前處理。** 以 regular expression 把報告切成 clinical indication、technique、findings、impression、other 五節；每個模型再用同一個固定 prompt 與 schema 把報告轉成結構化 JSON，報告沒寫的欄位設為 null，不做推論。分類時輸入的是 JSON，而且由做轉換的同一個模型負責分類。[(ref: main Methods, Report preprocessing)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**Prompt。** 單一固定的零樣本 prompt（Listing 1）包含五個部分：角色（臨床神經影像專家）、任務、三類的操作型定義、判斷與排除規則、只輸出一個數字的格式限制。排除清單分三組：良性顱內所見（如小型松果體囊腫、發育性靜脈異常、擴大的血管周圍間隙、與年齡相符的萎縮）、與顱內異常無關的顱外所見（如鼻竇或乳突黏膜增厚、頸椎所見），以及非病理性變異。規則另外要求只看腦實質、但腦膜瘤與垂體瘤等顱內非實質腫瘤仍算異常；老年人少量慢性微出血本身不算異常；報告各節權重相同，不特別偏重 Impression。[(ref: main Methods, Listing 1)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**推論設定。** 本地模型以 bfloat16、不量化，在 NVIDIA A100 上以 vLLM 執行，random seed 42；GPT-5 透過院內端點存取，未公開底層 snapshot、未設 seed。所有模型 temperature 0.2、top_p 1.0、最多輸出 512 tokens，每份報告每個模型只分類一次。[(ref: main Methods, Classification models and inference)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**專家參考集。** 共 680 份報告（675 位病人）：380 份來自先前內部專案、由一位醫學生標為正常並與一位放射科醫師複核；另 300 份為了涵蓋更多異常類型，依 DeepSeek-R1-32B 產生的 JSON 中病灶類別出現頻率，從前 300 個類別各取一份。由神經放射科專科醫師、放射科住院醫師與一位有 9 年神經影像經驗的博士後各自獨立判讀，不一致或邊界病例共同討論定案，判讀者看不到 LLM 輸出與 ICD-10 碼。[(ref: main Methods, Expert reference standard)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

- **論文未交代** — 三位判讀者獨立判讀時有多少份不一致、需要共同討論；先前專案的 380 份正常報告是否也經過三人判讀流程，Methods 只描述了原本的醫學生加放射科醫師流程。
- **論文未交代** — 結構化 JSON 轉換這一步單獨的正確率；每個模型分類用的是自己轉出的 JSON，轉換錯誤與分類錯誤在結果中無法分開。
- **論文未交代** — 同一模型重複執行時結果是否穩定（每份報告只跑一次，GPT-5 也未設 seed）；全隊列中自動貼為正常與異常各有多少份；uncertain 報告在非參考集中實際由誰、花多少時間判讀。

## 資料與實驗

下表摘錄論文 Table 1 的隊列特徵。[(ref: main Results, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

| 特徵 | 全隊列 | 非參考集 | 參考集 |
|---|---|---|---|
| 病人數 | 5,856 | 5,226 | 675 |
| MRI 檢查（報告）數 | 6,718 | 6,038 | 680 |
| 有 ≥2 次 MRI 的病人，n (%) | 694 (11.9%) | 654 (12.5%) | 5 (0.7%) |
| 女性，n (%) | 3,450 (58.9%) | 3,042 (58.2%) | 438 (64.9%) |
| 年齡，歲（mean ± SD） | 50.61 ± 20.55 | 50.95 ± 20.80 | 47.59 ± 17.95 |
| 有 active CNS ICD-10 診斷，n (%) | 2,223 (33.1%) | 2,105 (34.9%) | 118 (17.4%) |

參考集的專家標籤為 372 份 normal、90 份 WMH-only、218 份 abnormal。[(ref: main Results, Cohort characteristics)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

下表摘錄論文 Table 2 的參考集表現，括號內為 95% bootstrap CI；「錯誤數」為自動貼標中與專家不一致的報告數。[(ref: main Table 2)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

| 策略 | Assignment rate | Assignment accuracy | Normal precision | Abnormal precision | 錯誤數 | WMH-only deferral |
|---|---|---|---|---|---|---|
| ICD-10 二分 | 1.000 | 0.707 (0.672–0.740) | 0.658 (0.618–0.697) | 0.941 (0.896–0.982) | 199 (177–223) | 0.000 |
| Qwen3-32B | 0.831 (0.802–0.860) | 0.959 (0.942–0.975) | 0.948 (0.925–0.969) | 0.983 (0.962–1.000) | 23 (14–33) | 0.822 (0.739–0.898) |
| Kimi-Linear-48B-A3B | 0.804 (0.774–0.834) | 0.929 (0.907–0.949) | 0.985 (0.970–0.997) | 0.844 (0.794–0.891) | 39 (28–51) | 0.833 (0.750–0.904) |
| GPT-5 | 0.865 (0.839–0.891) | 0.971 (0.957–0.983) | 0.989 (0.977–0.997) | 0.941 (0.908–0.970) | 17 (10–25) | 0.867 (0.792–0.932) |
| DeepSeek-R1-32B | 0.818 (0.789–0.848) | 0.944 (0.924–0.962) | 0.936 (0.910–0.959) | 0.964 (0.933–0.988) | 31 (21–42) | 0.856 (0.781–0.926) |
| Majority voting（proprietary-inclusive） | 0.756 (0.723–0.789) | 0.990 (0.982–0.998) | 0.997 (0.991–1.000) | 0.976 (0.952–0.994) | 5 (1–9) | 0.989 (0.964–1.000) |
| Majority voting（open-source） | 0.729 (0.695–0.764) | 0.986 (0.975–0.996) | 0.988 (0.977–0.997) | 0.980 (0.955–1.000) | 7 (2–12) | 0.978 (0.944–1.000) |
| Consensus（proprietary-inclusive） | 0.707 (0.673–0.743) | 1.000 | 1.000 | 1.000 | 0 | 1.000 |
| Consensus（open-source） | 0.674 (0.639–0.708) | 1.000 | 1.000 | 1.000 | 0 | 1.000 |

## 結果

- **Consensus 的參考集表現** — 兩組都沒有錯誤自動貼標（0/481 與 0/458），WMH-only 報告 90 份全數退回；normal recall 為 85.8%（82.2–89.1）與 86.3%（82.8–89.6），abnormal recall 為 74.3%（68.6–80.0）與 62.8%（56.3–69.3）。[(ref: main Results, Table 2)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- **全隊列覆蓋** — 6,718 份報告中，proprietary-inclusive 組自動貼標 52.0%、open-source 組 48.6%，低於參考集的 70.7% 與 67.4%；作者說明參考集刻意加入較多正常報告，不用來估計母群體的覆蓋率。[(ref: main Results)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- **覆蓋率與錯誤的取捨** — 最佳單一模型（GPT-5／Qwen3-32B）覆蓋 86.5%／83.1%、錯誤率 2.9%／4.1%；majority voting 覆蓋 75.6%／72.9%、錯誤率 1.0%／1.4%；consensus 覆蓋 70.7%／67.4%、錯誤率 0%。majority voting 比 consensus 多貼標的那批報告，錯誤率為 15.2%（5/33）與 18.4%（7/38）。[(ref: main Results, Figure 5)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- **單一模型的錯誤被攔下** — Consensus 攔下 GPT-5 的全部 17 個錯誤（其中 12 個是專家判為 WMH-only 的報告）與 Qwen3-32B 的全部 23 個錯誤（16 個為 WMH-only）。[(ref: main Results, Figure 4)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- **Uncertain 群組的組成** — proprietary-inclusive 組有 199 份 uncertain：專家判為 normal 53、WMH-only 90、abnormal 56；open-source 組 222 份：51、90、81。專家 WMH-only 報告中約三分之二由「三模型一致說 WMH-only」退回，其餘約三分之一由模型不一致退回。[(ref: main Results, Figures 2–3)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- **全隊列 ICD-10 一致性** — 有 active CNS 相關 ICD-10 診斷的比例，在自動貼正常組為 1.6%、uncertain 組 29.7%／31.1%、自動貼異常組 51.3%／51.6%。被貼為正常卻有相關診斷的 17 份報告經人工檢視：13 份是臨床懷疑或排除診斷、該次 MRI 無對應異常，2 份為先前神經疾病、目前影像無表現，2 份的病灶在腦外或該次 MRI 看不到。[(ref: main Results, Figure 6)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)
- **ICD-10 二分作為對照** — 全數貼標但 assignment accuracy 只有 70.7%，normal precision 65.8%，共 199 個錯誤。[(ref: main Table 2)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

## 限制

**作者自述的限制。** 單一機構回顧性研究，跨院所、報告範本、MRI 協定、掃描儀與族群的可推廣性需要外部驗證；參考集刻意加入較多正常報告，不代表全隊列，可能沒有涵蓋罕見異常；300 份補充報告是依 DeepSeek-R1-32B 輸出的病灶類別挑選，可能影響病例組成；標籤來自報告而非影像，報告沒寫或沒強調的所見無法捕捉；單一的 abnormal 類不區分病因、嚴重度、分布或縱向變化；結果只代表一組模型、prompt 與部署設定，換版本、存取方式或報告格式都可能改變輸出。[(ref: main Discussion, Limitations)](https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf)

**本書庫的觀察。**

- **「零錯誤」的不確定性** — bootstrap 在零錯誤時給出 1.000–1.000 的區間，這是方法的退化結果，不代表真實錯誤率為零。以 rule of three 粗估（本書庫計算，非論文數值），481 份與 458 份零錯誤對應的 95% 錯誤率上限約為 0.6% 與 0.7%。
- **參考集與母群體不同** — 參考集有 active CNS ICD-10 診斷者只占 17.4%，全隊列為 33.1%；全隊列的自動貼標率也從約七成降到約五成。參考集上的零錯誤能否延伸到全隊列，論文沒有在非參考集上抽樣驗證。
- **參考集的挑選與受測模型有關** — 300 份補充報告依 DeepSeek-R1-32B 的輸出挑選，而 DeepSeek-R1-32B 又是 open-source 組的成員；作者已列為限制，但這可能讓參考集偏向該模型「看得懂」的病灶描述。
- **人工負擔沒有量化** — 全隊列約一半報告退回人工，論文沒有報告這些報告實際的判讀時間或人力，也沒有比較「全部人工判讀」與「consensus 加人工」的總成本。
- **三個模型不是獨立判讀者** — 兩組都共用 Qwen3-32B 與 Kimi-Linear-48B-A3B，且使用同一個 prompt；模型之間若有共同的誤讀，一致性不一定能攔下。論文的結果顯示參考集上沒有發生，但沒有檢驗這種相關錯誤的風險。

## 與書庫其他文章的關係

序列胸片報告研究把七個 LLM 逐一當成獨立判讀者比較準確率，本篇則把三個 LLM 是否一致本身當成自動貼標與退回人工的訊號，兩篇都只給模型報告文字、不給影像: [序列胸片報告的時序判讀：七個 LLM、五種提示詞，分得出「新出現」嗎？](2026-09-22-llm-temporal-change-cxr-reports.md)

膀胱鏡研究以棄答門檻在覆蓋率與可靠度之間選操作點，本篇用三模型一致與 WMH-only 一律退回做同一種取捨，換到參考集零錯誤、代價是約三成參考報告留給人工: [膀胱鏡影像交給通用多模態 LLM：提示詞與棄答門檻能換到多少可靠度？](2026-09-21-mllm-cystoscopy-bladder-triage.md)

RadKev 以單一 decision model 的答案機率做 coverage at 5% error，本篇則以三個 LLM 是否一致決定自動貼標或退回人工，兩篇處理的是同一種覆蓋率與錯誤率的取捨: [不生成文字、直接給每個選項機率：RadKev 把 decision model 專科化到放射科，15 項任務平均多 4.9 點，換到外院報告卻沒有進步](2026-10-15-radkev-radiology-decision-model.md)

## 實務的啟發

- **可借用的設計** — 建研究隊列時，把「多個 LLM 全數一致才自動貼標、其餘退回人工」當成篩選第一關，並把定義上本來就模稜兩可的類別（本篇的 WMH-only）明確設計成一律退回，而不是逼模型二選一。論文的參考集結果支持這種做法在這組資料上能把自動貼標錯誤壓到零，代價是覆蓋率下降。
- **可借用的量測方法** — 報告 consensus 類流程時，同時列出 assignment rate、各類 precision 與 recall，以及「多貼標的那一批」的錯誤率（本篇 majority voting 多貼的報告錯誤率約 15%–18%），比只報整體 accuracy 更能看出覆蓋率換到了什麼。
- **待驗證的警訊** — 參考集上的零錯誤來自單一機構、刻意組成的 680 份報告，且受測模型之一參與了參考集的挑選；換到另一家院所的報告範本或用語前，需要在當地非參考集上抽樣驗證自動貼標的錯誤率，並估計退回人工的實際工作量。
- **證據強度** — 這是單一機構的回顧性預印本，只依報告文字、不看影像；它支持「三模型一致規則在這組報告上能以較低覆蓋率換到很高的自動貼標精確度」，不足以支持直接取代人工判讀來建立研究隊列。

## References

- **main** — Rui W, Ma J, Stepanov V, et al. *Large language model consensus for reliable research cohort construction from radiology reports: a retrospective cohort study*. medRxiv, 2026. DOI: 10.64898/2026.10.06.26364312. PDF：<https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full.pdf>。文內引用位置：author block、Abstract、Background、Methods（Report preprocessing、Expert reference standard、Classification models and inference、Statistical analysis、Listing 1）、Results、Discussion、Limitations、Data and code availability、Table 1、Table 2、Figures 1–6。
- **html** — medRxiv 全文頁：<https://www.medrxiv.org/content/10.64898/2026.10.06.26364312v1.full>。
- **doi** — <https://doi.org/10.64898/2026.10.06.26364312>。
- **code** — 作者公開的流程與分析程式碼：<https://github.com/WushuangRui/mri-report-llm-classification>。

[Home](../) · [AI Papers](./)
