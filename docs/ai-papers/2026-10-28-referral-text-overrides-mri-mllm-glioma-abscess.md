---
catalog_id: "doi:10.64898/2026.10.17.26365809"
editors:
  - "Clare"
refs:
  main:
    title: "Clinical referral text overrides MRI evidence in multimodal large language models: glioma versus brain abscess"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full"
  abs:
    title: "medRxiv abstract page: 10.64898/2026.10.17.26365809v1"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1"
  supp:
    title: "Supplemental Information (Supplementary Tables 1–3, Supplementary Figures 1–5)"
    url: "https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 轉診單上一句話，就決定多模態 LLM 怎麼讀 MRI？膠質瘤 vs 腦膿瘍：四個模型的 text-driven span 0.79–1.00，叫它忽略文字也只有一個模型降到 0.04

## 來源

- 團隊：德國 University Hospital Cologne（University of Cologne 醫學院）Institute for Diagnostic and Interventional Radiology；作者依序為 Nedim C. Beste、Fabian Bauer、Nicolás Lopez、Thomas Schömig、Michael Schönfeld、David Zopfs、Lukas Goertz、Thorsten Persigehl、Christoph Kabbasch、Marc Schlamann、David Maintz、Roman J. Gertz、Nils Weitzer、Jonathan Kottlors。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1)
- 論文：*Clinical referral text overrides MRI evidence in multimodal large language models: glioma versus brain abscess*，medRxiv v1 預印本，2026-10-19 張貼，未經同儕審查；授權 CC BY-NC-ND 4.0。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1)
- 識別碼：DOI [10.64898/2026.10.17.26365809](https://doi.org/10.64898/2026.10.17.26365809)；未見期刊版本。
- 全文：[medRxiv 全文 HTML v1](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)；[補充資料 PDF](https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf)（轉診文字與 system prompt 的英譯、讀者表現表）。
- 程式與資料：作者表示資料可向作者合理申請，未見公開程式碼或資料庫連結；德文原始轉診文字同樣需向通訊作者索取。[(ref: main Data Availability)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)[(ref: supp Table 1)](https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf)
- 研究性質：單一中心回顧性的受控輸入實驗，不是 pilot 也不是方法論文；核心設計（同一張影像搭配五種轉診文字、三種指令、每個條件重複 20 次）已完整執行，共 72,000 筆模型回答，並報告 SE 與 mixed-effects 檢定。樣本只有 60 例、一個鑑別診斷、每例一張切面。[(ref: main Methods, Limitations)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)
- 證據邊界：本文數值以 medRxiv v1 全文 HTML 的正文與補充資料 Table 1–3 為準；Table 1（病人特徵）的完整表格與補充 Figure 1–5 的圖面數值未納入本文引述，相關數字只取正文與補充表格明列者。

**編輯：** Clare

作者把同一張無法單靠影像確定的 MRI 切面，配上從「明顯感染」到「明顯腫瘤」五種寫法的轉診文字送進四個多模態 LLM，發現轉診文字在兩個極端之間能把模型答「腫瘤」的比例拉動 0.79–1.00，而確診腫瘤與確診膿瘍之間的答案差異平均只有 0.01–0.25；在 system prompt 要求模型忽略文字後，只有 Gemini 的文字效應降到接近零。[(ref: main Abstract, Results)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

## 流程

![研究設計示意圖。最上方標題為 Study design: the same MRI slice is sent with different referral texts and instructions。六個圓角方塊：左上藍色方塊「1 Cases (single center)」寫 60 MRI exams: 30 glioma, 30 brain abscess、University Hospital Cologne, 2014-2026、One axial contrast-enhanced T1 slice、DWI and other sequences withheld、Reference: histopathology (glioma); microbiology / clinical course (abscess)；左下紫色方塊「2 Referral text (German)」寫 5 levels, same age / sex / symptoms，列出 explicit inflammatory、subtle inflammatory、neutral、subtle tumor、explicit tumor，以及 Ablations: image without text; neutral text without image；中間上方綠色方塊「4 Multimodal LLMs (API)」列出 GPT-4o、Claude Sonnet 5、Gemini 3.5 Flash、Qwen 3.6 (27B)，以及 Forced choice: TUMOR / NON-TUMOR、20 repeats per condition、60 x 5 x 3 x 20 x 4 = 72,000 answers；中間下方橘色方塊「3 System-prompt instruction」寫 none、prioritize the image、ignore the text (image only)；右上灰色方塊「5 Human reference」寫 2 board-certified radiologists、Same slices, image only, no text、Blinded, random order、120 readings；右下黃色方塊「6 Outcomes」寫 Tumor-call frequency per case、Text-driven span: explicit tumor minus explicit inflammatory, mean of 60 cases、Confirmed-diagnosis separation、Subtle-text share; consistency。五支深灰色實線箭頭：藍色方塊指向綠色方塊、紫色方塊斜向上指向綠色方塊、橘色方塊向上指向綠色方塊、綠色方塊斜向下指向黃色方塊、灰色方塊向下指向黃色方塊。底部灰色斜體字為 Schematic redrawn by EFAI-RD from the paper's Methods and supplementary tables; design counts only, no result values.](assets/referral-text-mri-mllm-design.png)

圖：本書庫依論文 Methods 與補充 Table 1–2 的文字重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的研究流程圖為 Figure 1）。五支實線箭頭表示病例影像、轉診文字與指令一起送進模型，模型回答與兩位放射科醫師的判讀再一起進入結果指標。[(ref: main Methods, Fig 1)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F1)[(ref: supp Table 1–2)](https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf)

## 背景／問題

作者的出發點是：放射科醫師判讀影像時本來就會看轉診單上的臨床資訊，多模態 LLM 若進入臨床流程，也很可能同時收到影像與這段文字；模型如何在兩者之間取捨，作者把它定位為安全問題，並引用文獻說明權重失當可能導致不必要或延誤的治療。[(ref: main Introduction)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full) 作者指出，既有評估多半只在單一輸入上量準確度；最接近的先前研究以刻意帶偏的提示降低了 LLM 在放射科考題上的準確率，但沒有回答一般、非對抗性的臨床文字在真實病例上會造成多大影響、需要多少字眼才會生效，以及模型在沒有暗示性文字時本來偏向哪一邊。[(ref: main Introduction)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

作者選擇膠質瘤（glioma）與腦膿瘍（brain abscess）作為鑑別對：兩者在對比增強 T1 影像上都可呈環狀強化，但治療完全不同，通常靠擴散加權影像（DWI）區分；作者刻意不提供 DWI，讓影像本身保持模稜兩可，才能量測模型如何在文字與影像之間分配權重。[(ref: main Introduction)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full) 也就是說，這是一個為了放大文字效應而設計的情境，不是模擬一般臨床判讀的完整檢查。

## 方法摘要

**病例。** University Hospital Cologne 2014–2026 年間隨機選取的 60 例（膠質瘤 30、腦膿瘍 30），每例只取一張 3 T、1 mm 對比增強 T1 的代表性軸切面；膠質瘤以組織病理為準，腦膿瘍以微生物學及／或臨床病程為準。[(ref: main Methods «Study design and patients»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

**輸入條件。** 五種德文轉診文字沿著「明顯感染 → 輕微感染 → 中性 → 輕微腫瘤 → 明顯腫瘤」排列，病人年齡、性別與症狀固定，只改變診斷線索；另有「只給影像、不給文字」與「只給中性文字、不給影像」兩個 ablation。system prompt 再分三種：不加權重指令、要求優先看影像、要求忽略文字。[(ref: main Methods «Clinical text conditions», «Prompt instructions»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

**模型與問法。** GPT-4o、Claude Sonnet 5、Gemini 3.5 Flash、Qwen 3.6（27B，經 Groq）以 API 查詢，每次獨立、無狀態；模型只能回答 TUMOR 或 NON-TUMOR，不能棄答；每個條件重複 20 次，共 72,000 筆回答。查詢期間為 2026 年 5–8 月。[(ref: main Methods «Models and querying»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

**人類對照與指標。** 兩位放射科專科醫師在不看任何文字的情況下獨立判讀同一批切面（120 次判讀）。主要指標 text-driven span 定義為每例在「明顯腫瘤」與「明顯感染」兩種文字下答腫瘤比例的差，再對 60 例取平均。[(ref: main Methods «Human reader reference», «Outcomes and statistical analysis»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

## 方法詳解

**轉診文字的內容。** 補充 Table 1 的英譯顯示，五種文字都描述一位 54 歲、頭痛合併進行性偏癱的病人。明顯感染版有高燒、寒顫、免疫抑制、近期鼻竇炎與 39.2 °C、CRP 明顯升高、白血球明顯增多；輕微感染版為輕微發燒、控制不佳的糖尿病、近期牙齒感染、37.9 °C 與 CRP 輕度升高；中性版的病程、感染源與檢驗皆為未知；輕微腫瘤版為約五週的緩慢進展、一次局部癲癇、無發燒且發炎指標正常；明顯腫瘤版為約三個月的緩慢進展、人格改變、反覆局部癲癇、發炎指標完全正常。文字由三位放射科醫師反覆修訂而成。[(ref: supp Table 1)](https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf)[(ref: main Methods «Clinical text conditions»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

**System prompt 與三種指令。** 所有條件共用的基本指令把模型設定為臨床放射分類器，看一張對比增強 T1 軸切面（可能附帶臨床病史），判斷病灶是腫瘤或非腫瘤，輸出限定為單一 token TUMOR 或 NON-TUMOR。「優先看影像」指令要求影像所見明顯優先於臨床病史；「忽略文字」指令要求只根據影像決定、完全忽略病史。作者刻意使用定性措辭而非數值權重，理由是 transformer 不會依數值比例做明確的加權組合。[(ref: supp Table 2)](https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf)

**解碼設定。** 正文寫 GPT-4o、Gemini、Qwen 的 temperature 為 0.7，Claude 用 provider 預設值，top-p 皆為預設；輸出上限 GPT-4o 與 Claude 為 20 token、Gemini 500、Qwen 800，以容納 reasoning token。只保留最終標籤，兩類都不符者記為 unclear 並排除。[(ref: main Methods «Models and querying»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

**其他指標與統計。** subtle-text share 是「輕微文字」已達到的變化占「明顯文字」變化的比例，分腫瘤側與感染側計算；consistency 是答腫瘤比例偏離 0.5 的絕對值，在多數決答對與答錯的情況間比較。統計以 mixed-effects logistic regression（每例 random intercept，文字層級、指令及交互作用為固定效應）並以 Holm 校正兩兩比較；比例用 Wilson 95% CI，一致性用 Cohen's κ；由於人類對照只有兩位讀者，模型與讀者的比較只做描述。[(ref: main Methods «Outcomes and statistical analysis»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

- **論文未交代** — 每例代表性切面如何挑選；正文只說每例取一張代表性軸切面。
- **論文未交代** — 兩個 ablation（只給影像、只給中性文字但無影像）的結果；Methods 列出這兩個條件，但正文 Results 與補充表格都沒有報告數值，查詢次數也未說明。
- **論文未交代** — 模型的準確度、敏感度與特異度如何從 20 次重複彙整（逐次計算或依多數決）；Methods 只列出指標名稱，沒有公式，各模型的敏感度也只給 0.57–0.71 的範圍。
- **論文未交代** — 「confirmed-diagnosis separation」在 Methods 沒有正式定義，Results 中的描述為確診腫瘤與確診膿瘍兩組答腫瘤比例的差。
- **論文未交代** — 解碼設定前後不一致：正文寫三個模型 temperature 0.7，補充資料則寫在可設定處使用 provider 預設的取樣設定，並提到其中一個模型為 preview 版本但未指明是哪一個。
- **論文未交代** — 正文的 span 與中性文字結果未逐句標明屬於哪一種指令條件；與 Figure 5 中「無指令」一欄的數值相同，本文據此視為無指令條件的結果。

## 資料與實驗

### 資料

| 項目 | 數量／內容 | 說明 |
|---|---|---|
| 病例 | 60 例（膠質瘤 30、腦膿瘍 30） | 2014–2026 年單一中心隨機選取 |
| 年齡 | 平均 55.8 ± 16.4 歲（25–87） | 膠質瘤組平均 59.4 歲、膿瘍組 52.1 歲 |
| 女性 | 29／60（48%） | 膠質瘤組 14、膿瘍組 15 |
| 影像 | 每例 1 張 3 T、1 mm 對比增強 T1 軸切面 | DWI 與其他序列刻意不提供 |
| 參考標準 | 膠質瘤：組織病理；膿瘍：微生物學及／或臨床病程 | 參考標準不明確、明顯假影、病灶區曾手術或放療者排除 |
| 模型回答 | 60 例 × 5 文字 × 3 指令 × 20 次 × 4 模型 = 72,000 | 另有兩個 ablation，次數未說明 |
| 人類判讀 | 2 位放射科專科醫師 × 60 例 = 120 次 | 只看影像、不看文字、互相盲化 |

[(ref: main Methods, Results «Study cohort»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

### 實驗：中性文字下的基準傾向與兩位讀者（論文 Results «Human reader reference and answers with neutral text»、Figure 2）

| 判讀者 | 答腫瘤比例 | 特異度（膿瘍） | 準確度 |
|---|---|---|---|
| Claude Sonnet 5 | 67% | 0.38 | 0.54 |
| Qwen 3.6 | 59% | 0.53 | 0.62 |
| GPT-4o | 54% | 0.48 | 0.52 |
| Gemini 3.5 Flash | 45% | 0.78 | 0.73 |
| 讀者 NR1（無文字） | 52% | 0.77 (0.59–0.88) | 0.78 (0.66–0.87) |
| 讀者 NR2（無文字） | 60% | 0.63 (0.46–0.78) | 0.73 (0.61–0.83) |

模型列為中性文字條件；讀者列括號為補充 Table 3 的 95% CI，讀者敏感度為 0.80 與 0.83，對參考標準的 κ 為 0.57 與 0.47，兩位讀者彼此一致 45／60 例、κ 0.50（0.28–0.72）。作者把準確度定位為背景資訊，而非性能宣稱。[(ref: main Results, Fig 2)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F2)[(ref: supp Table 3)](https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf)

### 實驗：文字效應與指令（論文 Results «Effect of the clinical text conditions»、«Subtle versus explicit text»、«Effect of prompt instructions»、Figure 3–5）

| 模型 | Text-driven span（無指令，SE） | Confirmed-diagnosis separation | Subtle-text share（腫瘤側／感染側） | Span：優先看影像 | Span：忽略文字 |
|---|---|---|---|---|---|
| GPT-4o | 1.00 (0.00) | 0.01 | 98%／100% | 0.87 | 0.58 |
| Claude Sonnet 5 | 0.97 (0.02) | 0.03 | 83%／100% | 0.75 | 0.48 |
| Qwen 3.6 | 0.86 (0.03) | 0.10 | 92%／98% | 0.82 | 0.70 |
| Gemini 3.5 Flash | 0.79 (0.04) | 0.25（最大 0.46） | 31%／99% | 0.31 | 0.04 |

四個模型的 span 皆 p < 0.001。span 1.00（SE 0.00）表示幾乎每一例都隨文字從全答「非腫瘤」翻成全答「腫瘤」；separation 為確診腫瘤與確診膿瘍兩組答腫瘤比例的平均差。指令條件下的 CI 與 p 值未在正文列出，Figure 5 的誤差線為 ±1 SE。[(ref: main Results, Fig 3)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F3)[(ref: main Fig 4)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F4)[(ref: main Fig 5)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F5)

## 結果

- **文字決定答案** — 在兩種明顯文字之間，GPT-4o 的 span 為 1.00、Claude 0.97、Qwen 0.86、Gemini 0.79；相對地，同一模型對確診腫瘤與確診膿瘍的回答平均只差 0.01、0.03、0.10 與 0.25。作者的解讀是一行臨床文字就能在很大程度上獨立於影像決定答案。[(ref: main Results, Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F3)
- **輕微措辭就夠** — 輕微腫瘤文字已達到明顯腫瘤文字效應的 98%（GPT-4o）、83%（Claude）、92%（Qwen），感染側三者為 98%–100%；只有 Gemini 在腫瘤側呈漸進反應（31%）。[(ref: main Results, Fig 4)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F4)
- **沒有暗示時，各模型的預設傾向不同** — 中性文字下四個模型答腫瘤的比例為 45%–67%，兩位讀者為 52% 與 60%；模型準確度 0.52–0.73，讀者 0.78 與 0.73。作者認為模型間的差異反映的是各自的預設行為，而不是共同、合理的先驗。不過讀者沒有看文字、模型看了中性文字，兩者條件不同。[(ref: main Results, Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F2)
- **指令的效果因模型而異** — 「優先看影像」把 span 降到 0.31（Gemini）至 0.87（GPT-4o）；「忽略文字」把 Gemini 從 0.79 降到 0.04，GPT-4o 降到 0.58、Claude 0.48、Qwen 0.70，Qwen 對兩種指令的反應都最小。在忽略文字指令下，Gemini 對確診腫瘤答腫瘤 54%–66%、對確診膿瘍 18%–23%。[(ref: main Results, Fig 5)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F5)
- **重複一致不代表答對** — 多數決答錯時與答對時的一致性幾乎相同（答錯 vs 答對：GPT-4o 0.465 vs 0.474、Claude 0.488 vs 0.497、Gemini 0.456 vs 0.474、Qwen 0.419 vs 0.453）；作者據此指出，重複查詢的一致性不能當成信心訊號。[(ref: main Results «Consistency», Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

## 限制

**作者自述的限制。** 只測一個鑑別對、一個序列的一張切面、單一機構 60 例，結果能否推到其他診斷、模態或完整檢查未知；作者也說明，刻意保持影像模稜兩可是設計所需，影像明確時文字效應可能被掩蓋。病例組成刻意平衡，不反映臨床盛行率，也沒有分析各模型偏向腫瘤的原因。解碼設定無法完全一致，商用模型會隨時間更新，結果只適用於測試的版本。讀者沒有收到文字而模型收到中性文字，模型與讀者的差異只能描述，讀者自己受文字影響的程度沒有量測。強迫二選一、不能棄答，不確定性只能從重複間的變異推斷。[(ref: main Discussion «Limitations»)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

**本書庫的觀察。**

- **量到的是「文字壓過影像」的上限情境** — 不給 DWI、只給一張切面，影像本身就難以判斷（兩位讀者 κ 只有 0.50），文字在這種條件下占上風是可預期的方向；這篇的價值在於量出幅度與模型間差異，而不是顯示一般臨床判讀中文字都會壓過影像。
- **ablation 缺席讓「影像用了多少」只能間接推估** — 只給影像與只給文字兩個條件的結果沒有報告，影像的獨立貢獻只能從 confirmed-diagnosis separation 間接看出；若要把這套設計當成評估工具，這兩個數字是最該補上的。
- **轉診文字不只有措辭差異** — 明顯與輕微版本同時改變了發燒、CRP、白血球、病程與癲癇等具體臨床資訊，這些本來就是合理的鑑別線索；span 量到的是「模型多依賴臨床資訊」，至於多依賴才算過度，論文沒有給出人類讀者在同樣文字下的對照。
- **人類讀者也會受病史影響** — 作者在 Discussion 引用的系統性回顧指出，提供臨床病史多半改善人類讀者表現；因此「模型會參考文字」本身不是缺陷，問題在於確診診斷幾乎不改變模型答案。[(ref: main Discussion)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

## 與書庫其他文章的關係

兩篇都量測影像以外的文字如何改變模型判讀：口腔顎顏面放射研究把錯誤診斷與權威身分寫進提問，本篇則用不帶欺騙意圖、只改變臨床線索的轉診文字，並以同一張影像在五個文字層級間的變化量化文字效應: [說是專科醫師的意見，LLM 就跟著改診斷？五個模型在 200 個口腔顎顏面放射情境下的 sycophancy 測試](2026-10-13-llm-sycophancy-oral-maxillofacial-radiology.md)

ModaLens 固定報告與問題、只交換影像來量測醫療 VLM 是否仍看影像，本篇反過來固定影像、只改轉診文字，量的是同一個「文字與影像誰說了算」問題的另一面: [ModaLens：有報告可讀時，醫療 VLM 還會看影像嗎？](2026-09-17-modalens-image-sensitivity.md)

mTICI 研究以只有報告、只有影像、兩者皆有三種條件顯示 GPT-5 的一致性主要來自手術報告，本篇則在同一張影像上逐級改寫轉診文字，顯示文字不只是補充、而是能直接決定多模態 LLM 的答案: [有手術報告時，GPT-5 的 mTICI 分級追得上醫師；只給 DSA 影像，一致性從 0.87 掉到 0.35：取栓後再灌流分級的多模態模型比較](2026-10-19-lmm-mtici-thrombectomy-dsa-grading.md)

## 實務的啟發

- **可借用的評估設計** — 固定影像、把臨床文字分成明顯／輕微／中性的雙向階梯，再以 span 與 subtle-text share 量化，是部署前檢查「模型對臨床脈絡有多敏感」的具體作法；建議同時跑只給影像與只給文字的 ablation，並讓人類讀者在相同文字條件下判讀，才能區分「合理參考病史」與「過度依賴文字」。
- **待驗證的警訊** — 在這個刻意模稜兩可的設定裡，四個模型的確診診斷幾乎不改變答案、輕微措辭就能翻轉結果；這是單一中心 60 例、單一鑑別對的結果，是否適用於完整檢查或其他疾病需要另外驗證，但足以說明只報告平衡資料集上的準確度可能看不到這個問題。
- **不要把 prompt 指令當成防護** — 「忽略文字」只在一個模型上讓文字效應接近零，在其他三個模型上仍保留 0.48–0.70；任何以 system prompt 限制模型參考臨床資訊的做法，都需要針對所用模型與任務實測。[(ref: main Results, Fig 5)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F5)
- **一致性不是信心** — 多數決答錯與答對時的重複一致性幾乎相同，用「問多次答案都一樣」來篩選可信回答，在這類任務上沒有依據。
- **證據強度** — 它支持「在這四個模型版本與這個設定下，轉診文字對答案的影響遠大於確診診斷」；不足以支持特定模型在臨床上安全或不安全，作者也只主張臨床使用前需要依模型與任務做測試。[(ref: main Conclusion)](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full)

## References

- **main** — Beste NC, Bauer F, Lopez N, Schömig T, Schönfeld M, Zopfs D, Goertz L, Persigehl T, Kabbasch C, Schlamann M, Maintz D, Gertz RJ, Weitzer N, Kottlors J. *Clinical referral text overrides MRI evidence in multimodal large language models: glioma versus brain abscess*. medRxiv v1 (2026). DOI: <https://doi.org/10.64898/2026.10.17.26365809>。全文 HTML：<https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full>。文內引用位置：Abstract、Introduction、Materials and methods（«Study design and patients»、«Clinical text conditions»、«Models and querying»、«Prompt instructions»、«Human reader reference»、«Outcomes and statistical analysis»）、Results（«Study cohort»、«Human reader reference and answers with neutral text»、«Effect of the clinical text conditions»、«Subtle versus explicit text»、«Effect of prompt instructions»、«Consistency»）、Discussion、Limitations、Conclusion、Data Availability；圖：<https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F1>、[#F2](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F2)、[#F3](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F3)、[#F4](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F4)、[#F5](https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1.full#F5)。
- **abs** — medRxiv abstract page：<https://www.medrxiv.org/content/10.64898/2026.10.17.26365809v1>。
- **supp** — Supplemental Information（Supplementary Table 1：轉診文字英譯；Table 2：system prompt 與加權指令；Table 3：讀者表現）：<https://www.medrxiv.org/content/medrxiv/early/2026/10/19/2026.10.17.26365809/DC1/embed/media-1.pdf>。

[Home](../) · [AI Papers](./)
