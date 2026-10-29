---
catalog_id: "doi:10.64898/2026.10.23.26366376"
editors:
  - "Clare"
refs:
  main:
    title: "Scoring the NIH Stroke Scale from bedside exam transcripts: a synthetic benchmark of a decision model and a large language model"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf"
  abs:
    title: "medRxiv abstract page: 10.64898/2026.10.23.26366376v1"
    url: "https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 從床邊檢查逐字稿直接打 NIHSS：112 個合成中風案例上，LLM 項目準確率 99.0%、decision model Jev 94.4% 但快約 40 倍；病例、逐字稿與答案卷都由 LLM 產生，人工審查尚未完成

## 來源

- 團隊：Wayne State University School of Medicine／Detroit Medical Center 神經科（Detroit, Michigan）。PDF 首頁作者依序為 Noor Abdulla、Waleed Abood，medRxiv 摘要頁則列為 Waleed Abood、Noor Abdulla；依作者貢獻聲明，研究設計、決策與撰稿由 Waleed Abood 負責。[(ref: main p.1, p.20)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=1) [(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1)
- 論文：*Scoring the NIH Stroke Scale from bedside exam transcripts: a synthetic benchmark of a decision model and a large language model*，medRxiv v1 預印本，2026-10-26 張貼，未經同儕審查；授權 CC BY-ND 4.0。[(ref: abs)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1)
- 識別碼：DOI [10.64898/2026.10.23.26366376](https://doi.org/10.64898/2026.10.23.26366376)；未見期刊版本。
- 全文：[medRxiv PDF v1](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf)（21 頁）。
- 程式與資料：評分表、逐字稿、prompt、完整模型回應與分析腳本可向通訊作者申請，作者預定在人工審查完成後公開於 GitHub（`waleedabood/nihss-transcript-benchmark`）。[(ref: main p.20)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=20)
- 研究性質：完整執行的合成資料 benchmark，不是真實病人研究；兩個評分引擎都實際跑過全部 112 份逐字稿，主要指標附 Wilson 95% CI 與配對檢定。病例、答案卷（score form）與逐字稿都由 Claude Opus 5.5 生成，答案卷只經另一個 LLM（Claude Fable 5.1）核對，預先指定的人工審查尚未納入這一版。[(ref: main p.3–6)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=3)
- 證據邊界：本文數值以 v1 PDF 的正文與 Table 1–5 為準，頁碼依 PDF 頁尾的「Page X of 21」；Figure 4 的逐項準確率只引用正文明列的項目，prompt 全文與模型回應不在論文中、未納入本文引述。

**編輯：** Clare

作者用 LLM 生成 112 個中風急診病例的 NIHSS 答案卷與對應的床邊檢查逐字稿，讓託管的 decision model Jev 與 LLM gpt-6-luna 只看逐字稿逐項打分：LLM 的項目準確率 99.0%、Jev 94.4%，Jev 每份檢查的延遲中位數 0.15 秒、LLM 5.78 秒；但答案卷本身由 LLM 寫成、尚未經人工確認，這是一份「在乾淨合成文字上的上限」而非臨床準確度。[(ref: main p.11–12, Table 3)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=12)

## 流程

![研究設計示意圖。最上方標題為 Study design: synthetic NIHSS benchmark from bedside exam transcripts。上排由左到右四個圓角方塊，以三支深灰色實線箭頭相連：藍色方塊「1 Case design」寫 43 presentation types (69 references)、Main set: 100 cases, 31 syndrome rows、Stress set: 12 cases (special scoring rules)；紫色方塊「2 Answer key」寫 Claude Opus 5.5 writes 15-item NIHSS score form + vignette + reasons、Automated form check (flags only, no edits)；綠色方塊「3 Transcript」寫 Claude Opus 5.5, T = 1.0、speech-to-text style、no score or item named、Narrated 62 / telegraphic 50；橘色方塊「4 Scoring engines」寫 Input: transcript only、Jev (jev-1.13.0): choice + confidence、gpt-6-luna (LLM): JSON choice + self-reported confidence。下排三個方塊：灰底實線框「Key check」寫 Claude Fable 5.1 scores forms and transcripts blind to the key；白底灰色虛線框「Human review (pending)」寫 2 NIHSS-certified raters、44 prespecified transcripts、not in this version；青色方塊「5 Outcomes」寫 Item accuracy vs key (112 x 15 = 1,680 items)、Exact total, latency, cost、Post hoc: examiner-only lines; confidence hybrid。三支灰色虛線箭頭分別由紫色方塊指向 Key check、由綠色方塊指向 Key check、由綠色方塊指向 Human review；一支深灰色實線箭頭由橘色方塊向下指向青色方塊。左下角斜體說明為 Schematic redrawn from the paper's Methods; design counts only, no result values.](assets/nihss-transcript-benchmark-design.png)

圖：本書庫依論文 Methods 文字與 Table 1 重繪的研究設計示意圖，只含設計層級的計數，不含結果數值，未複製論文原圖（論文的研究流程圖為 Figure 1）。上排四個方塊以實線箭頭表示病例、答案卷、逐字稿到評分引擎的生成順序；灰色虛線箭頭表示答案卷的核對路徑，其中白底虛線框的人工審查在這一版尚未執行。[(ref: main p.3–6)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=3)

## 背景／問題

NIH Stroke Scale（NIHSS）有 15 個項目，評分需要正式訓練；作者引用的認證研究顯示，人類評分者之間的 item-level κ 落差很大，Lyden 等人在 8,214 位評分者中為 0.15（limb ataxia）到 0.81（level-of-consciousness commands），Anderson 等人的新版動畫認證系統為 0.25–0.90。[(ref: main p.2)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=2) 既有的 LLM 研究多半是從病歷「抽出已寫下的分數」，作者引用的 Lott 等人在 312 份出院摘要上報告 88.5% 的項目準確率。[(ref: main p.2)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=2)

作者的出發點是 ambient AI scribe 正在被導入以減輕文書負擔，並表示就其所知還沒有研究直接從檢查對話本身打 NIHSS。[(ref: main p.2–3)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=2) 「從對話自動打分能改善急性中風照護」這個前提，論文沒有提供證據，也不在評估範圍；本篇回答的是較窄的問題：在劇本化、無語音辨識錯誤的逐字稿上，兩種引擎能否重現一份預先寫好的答案卷。

## 方法摘要

**病例。** 作者先整理 43 種中風表現的族群頻率與典型 NIHSS 項目組合（69 篇參考文獻，排除 stroke mimics），再依比例配出 100 個主集病例（缺血 66、TIA 20、腦內出血 12、其他出血 2）與 12 個壓力測試病例，後者專門檢驗昏迷、插管、截肢、locked-in、全失語等特殊計分規則。[(ref: main p.3–4, Table 1)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=3)

**答案卷與逐字稿。** Claude Opus 5.5 依症候群、病灶側與目標總分寫出 15 項評分表、病例描述與每個異常項的理由，作為答案卷；再為每份答案卷寫一份語音轉文字風格的逐字稿（溫度 1.0），逐字稿中不出現分數或項目名稱。主集逐字稿隨機分為 narrated（檢查者口述所見）與 telegraphic（簡短、所見需由對話推斷）各 50 份，壓力測試病例全為 narrated。[(ref: main p.3–4)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=3)

**評分引擎。** Jev 是 TypeSafe 提供的 decision model（主分析版本 jev-1.13.0），把每個項目當成選擇題回答並給出所選答案的 confidence；gpt-6-luna 是 OpenAI 的 LLM，以項目評分準則提示、輸出含答案與自評 confidence 的 JSON。兩者都只看逐字稿。[(ref: main p.6)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=6)

**評估。** 主要指標是 1,680 個項目（112 × 15）對答案卷的準確率，附 Wilson 95% CI，配對比較用 McNemar；次要指標包含總分完全相符、總分誤差、逐項準確率、依檢查者風格分層、延遲與每 1,000 次檢查的成本。[(ref: main p.6)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=6)

## 方法詳解

**答案卷的自動檢查。** 程式會標出總分不符、偏離目標總分超過 2 分、非法值、違反昏迷規則、側別矛盾、右側病灶卻有失語、缺少理由等問題，但只標記、不修改分數。[(ref: main p.3–4)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=4)

**逐字稿的寫法。** 含時間戳記、說話者標籤與急診背景噪音描述；所有逐字稿都有一位護理師與一位家屬或旁人，112 份中 109 份出現廣播、呼叫器或警報。構音障礙以拼音式文字呈現，52 個構音障礙病例中有 48 個檢查者也口頭提到；就診月份固定為 2026 年 10 月；建構病例、逐字稿與答案卷時沒有使用任何 OpenAI 模型。[(ref: main p.4, p.8)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=4)

**答案卷的核對。** 由同公司的另一個模型 Claude Fable 5.1 核對兩次：把病例描述改寫成去除分數的純所見後重新打分，與答案卷一致 99.6%（1674／1680，κ 0.99）；直接盲評逐字稿，一致 99.2%（1666／1680，κ 0.98），15 項全對的逐字稿 narrated 58／62、telegraphic 41／50。[(ref: main p.5)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=5)

**預定但未執行的人工審查。** 兩位 NIHSS 認證評分者在不看答案卷下為 44 份預先指定的逐字稿打分並評真實度 1–5 分（含全部 13 份模型核對不一致者、其餘 11 個壓力測試病例與 20 份隨機抽樣主集），由資深神經科醫師裁決；結果將在修訂版報告。[(ref: main p.6)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=6)

**統計。** 病例層級以 Wilcoxon signed-rank 比較每份逐字稿的準確率，並以 10,000 次病例層級 bootstrap 估計準確率差的 95% CI。[(ref: main p.6)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=6)

**事後分析。** 只保留檢查者台詞的 examiner-only 分析（6,366 行保留 3,715 行，以 jev-1.14.0 與相同 prompt 重跑）與以 Jev confidence 分流的 hybrid 模擬，論文都明言不是預先規劃。[(ref: main p.7, p.17)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=7)

- **論文未交代** — 兩個引擎的 prompt 與項目評分準則全文（作者說沿用一個未發表的 pilot，可向作者索取），以及產生病例與逐字稿的 prompt 全文。
- **論文未交代** — gpt-6-luna 的取樣溫度與 API 設定；每個項目分開呼叫還是整份逐字稿一次呼叫。
- **論文未交代** — Jev 的架構、訓練資料與開放程度；作者聲明與 TypeSafe 無財務關係，但沒有描述模型本身。
- **論文未交代** — 研究是否預先註冊；主分析用的 jev-1.13.0 已無法選用，作者自承主結果無法完全重跑。[(ref: main p.7, p.19)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=19)

## 資料與實驗

### 資料

| 項目 | 數量 | 說明 |
|---|---|---|
| 主集病例 | 100 | 缺血 66（MCA／ACA 皮質分支 23、lacunar 17、後循環 15、大範圍 MCA 11）、TIA 20、腦內出血 12、其他出血 2 |
| 壓力測試病例 | 12 | 雙側失明、插管、截肢、昏迷規則、locked-in、全失語、雙肢 ataxia 等 |
| 主集 NIHSS 總分分布 | 0／1–4／5–15／16–20／≥21 = 15／38／34／4／9 | 20 個 TIA 中 14 個總分為 0 |
| 檢查者風格 | narrated 62／telegraphic 50 | 主集各 50；壓力測試 12 份皆為 narrated |
| 逐字稿字數，中位數（範圍） | narrated 805（613–986）；telegraphic 556（451–670）；全部 689（451–986） | 模擬檢查時間中位數 3:36（2:33–4:56） |
| 評分單位 | 1,680 個項目 | 112 份逐字稿 × 15 項 |

[(ref: main p.3, p.7–9, Table 1–2)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=8)

### 實驗：112 份逐字稿的準確率、速度與成本（論文 Table 3）

| 指標 | Jev | gpt-6-luna |
|---|---|---|
| 項目準確率，%（95% CI） | 94.4（93.2–95.4） | 99.0（98.4–99.4） |
| 總分完全相符，n／112 | 63 | 101 |
| 總分差 1 分（偏高／偏低） | 27（21／6） | 10（3／7） |
| 總分差 2 分（偏高／偏低） | 18（10／8） | 1（0／1） |
| 總分差 ≥ 3 分 | 4（最大 7） | 0 |
| 總分在 ±1 分內 | 90 | 111 |
| 平均總分絕對誤差（分） | 0.72 | 0.11 |
| 延遲中位數／第 95 百分位（秒） | 0.15／0.29 | 5.78／11.77 |
| 每 1,000 次檢查成本（USD） | 0.23 | 0.67 |

[(ref: main p.11–12, Table 3)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=12)

### 實驗：Jev 錯誤集中的四個項目（論文 Table 4）

| 項目 | Jev 錯誤數（／112） | 方向 | 其中 telegraphic | 主要型態 |
|---|---|---|---|---|
| 9 Language | 16 | 15 偏高、1 not assessed | 12 | 15 個高估中 13 個是構音障礙病人：把口齒不清當成失語 |
| 11 Extinction and neglect | 14 | 14 偏高 | 13 | 14 個都有視野缺損：把視野缺損當成 extinction |
| 1b LOC questions | 11 | 7 偏低、4 偏高 | 7 | 接受近似錯誤的答案（例如「Octember」） |
| 3 Visual fields | 10 | 7 not assessed、2 偏低、1 偏高 | 4 | 有做視野檢查卻沒有辨認出來（例如 blink to threat） |

[(ref: main p.14, Table 4)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=14)

### 實驗：只保留檢查者台詞（事後分析，論文 Table 5）

| 檢查者風格 | Jev，完整逐字稿 | Jev，examiner-only | gpt-6-luna，完整逐字稿 | gpt-6-luna，examiner-only |
|---|---|---|---|---|
| Narrated（n = 62） | 97.3% | 96.9% | 100% | 98.8% |
| Telegraphic（n = 50） | 90.9% | 79.5% | 97.7% | 80.0% |
| 全部（n = 112） | 94.5% | 89.1% | 99.0% | 90.4% |

examiner-only 分析以 jev-1.14.0 執行；Table 5「Jev，完整逐字稿」全部列的 94.5% 與論文報告的 jev-1.14.0 完整逐字稿準確率相同，主分析的 jev-1.13.0 為 94.4%。[(ref: main p.7, p.17–18, Table 5)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=18)

## 結果

- **主要結果** — 項目準確率 LLM 99.0%、Jev 94.4%（McNemar p < 0.001）；配對項目中只有 Jev 答對的 10 項、只有 LLM 答對的 87 項。病例層級 LLM 較好 47 份、Jev 較好 3 份、平手 62 份，準確率差 4.6 個百分點（95% CI 3.2–6.1）。兩個引擎都沒有任何一份逐字稿執行失敗。[(ref: main p.11–12)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=11)
- **錯誤方向** — Jev 總分錯時多半偏高（33 比 16 份）；它對 8 個逐字稿中其實有檢查的項目回答 not assessed，LLM 沒有這種情況。[(ref: main p.12)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=12)
- **逐項** — Jev 最低的是 language 85.7%、extinction and neglect 87.5%、LOC questions 90.2%、visual fields 91.1%；LLM 每項至少 94.6%（最低為 LOC questions），sensory 兩者 112 例全對。[(ref: main p.13–14)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=13)
- **檢查者風格** — 主集中 telegraphic 讓 Jev 下降 7.1 個百分點（98.0% → 90.9%）、LLM 下降 2.3 個百分點（100% → 97.7%）；總分完全相符 Jev 38／50 → 20／50，LLM 50／50 → 39／50。壓力測試集 LLM 180／180 項全對，Jev 169 項（93.9%）。[(ref: main p.16)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=16)
- **只看檢查者台詞** — narrated 時兩者仍高（Jev 96.9%、LLM 98.8%），telegraphic 時都掉到約 80%；降幅最大的是需要病人回答的 LOC questions（Jev 90.2% → 62.5%、LLM 94.6% → 60.7%）。這個條件下 LLM 的優勢不再顯著（McNemar χ² 2.63，p = 0.10）。[(ref: main p.17–18)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=17)
- **Confidence 與 hybrid** — Jev 答對時平均 confidence 0.91、答錯 0.53；LLM 自評為 0.97 與 0.78。把 Jev confidence 低於 0.70 的項目（14.8%）轉給 LLM，可涵蓋 Jev 94 個錯誤中的 81 個（86%）；用已收集的 LLM 答案事後模擬的 hybrid 準確率 98.8%（1659／1680），略低於 LLM 單獨的 99.0%，實際串接尚未執行。[(ref: main p.16–17)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=17)

## 限制

**作者自述的限制。** 病例、評分表與逐字稿全由 LLM 生成，LLM 寫的文字可能對 LLM 引擎有利；答案卷只由與生成者同公司的模型核對，尚無人工審查；沒有音訊，逐字稿是沒有語音辨識錯誤、交談重疊與噪音的乾淨文字；拼音式的口齒不清在真實語音轉文字中不會保留，Jev 的部分 language 錯誤可能與文字寫法有關；只有兩種檢查者風格、一個 LLM、一個 decision model、每個引擎只跑一次、就診月份固定；jev-1.13.0 已無法選用；examiner-only 與 hybrid 為事後分析；排除 stroke mimics，研究測的是評分而不是診斷。[(ref: main p.19–20)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=19)

**本書庫的觀察。**

- **參考標準與受測對象同屬 LLM** — 答案卷是 Claude Opus 5.5 依目標總分「寫出來」的，逐字稿再由同一模型依答案卷寫成，等於先決定答案、再寫出支持答案的對話；核對者 Claude Fable 5.1 只看逐字稿就有 99.2% 一致。99.0% 這個數字比較接近「逐字稿把答案寫得多清楚」，而不是臨床上從真實檢查打分的難度。
- **數字的分母要對齊** — Jev 的 narrated 準確率在正文與 Discussion 寫 98.0%（主集 50 份的比較），在 Table 5 是 97.3%（n = 62，含 12 份壓力測試），而 Table 5 的全部列數值與 jev-1.14.0 相同；引用時要說明是哪個分母與版本。
- **與人類評分者的 κ 不能直接比** — 作者自己也指出，對固定答案卷的一致率與評分者之間的 κ 是不同量測；文中引用的人類 κ 0.15–0.90 只是背景，不是本研究的對照組。[(ref: main p.18–19)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=18)

## 與書庫其他文章的關係

RadKev 那篇把託管的 Jev 當成放射科選擇題的比較對象之一，本篇則在 NIHSS 逐字稿上把 Jev 與 LLM 正面對照，兩篇都看到 decision model 延遲遠低於 LLM、準確率結論則依任務與資料而變: [不生成文字、直接給每個選項機率：RadKev 把 decision model 專科化到放射科，15 項任務平均多 4.9 點，換到外院報告卻沒有進步](2026-10-15-radkev-radiology-decision-model.md)

ASA 分級那篇在真實術前資料上比較「讀選項機率」的 readout 與生成式提示的 κ、延遲與標籤成本，本篇則在合成逐字稿上比較 decision model 與生成式 LLM 的準確率、延遲與每千次成本，並多了一個以 confidence 分流的 hybrid 模擬: [不生成理由、只讀 A–D 選項的機率：Qwen3.5-9B 分 ASA 身體狀態，比生成式提示快約 64 倍，再用 1,000 個在地標籤調三個門檻，κ 只比 LoRA 低約 0.02，標籤再多 LoRA 仍會拉開](2026-10-28-asa-ps-llm-readout-vs-lora.md)

## 實務的啟發

- **可借用的評估設計** — 把逐字稿分成 narrated 與 telegraphic、再做 examiner-only 的刪減，是拆解「模型是在讀醫師的口述，還是在理解對話」的有效作法；本篇的結果顯示，需要病人回答的項目（例如 LOC questions）在只收檢查者麥克風時會大幅失準。
- **可借用的錯誤分析** — Table 4 把 Jev 的錯誤歸成可命名的型態（構音障礙當失語、視野缺損當 extinction），比只報總準確率更能指出要改哪一題的問法；作者認為可以只改提問方式而不重訓，但這一點論文沒有測試。
- **待驗證的方向** — confidence 低於門檻就轉給 LLM 的 hybrid 只是用既有答案事後模擬，準確率也沒有超過 LLM 單獨使用；要談成本與延遲的取捨，需要實際串接並在真實錄音上測試。
- **證據強度** — 它支持「在乾淨、劇本化、由 LLM 生成的逐字稿上，兩個引擎都能重現 LLM 寫的答案卷，LLM 較準、decision model 較快較便宜」；不足以支持任何一個引擎能在真實急診錄音上取代 NIHSS 認證評分者，作者也把下一步定為真實錄音與人工評分者。[(ref: main p.20)](https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf#page=20)

## References

- **main** — Abdulla N, Abood W. *Scoring the NIH Stroke Scale from bedside exam transcripts: a synthetic benchmark of a decision model and a large language model*. medRxiv v1 (2026). DOI: <https://doi.org/10.64898/2026.10.23.26366376>。全文 PDF：<https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1.full.pdf>。文內引用位置：p.1（作者與單位）、p.2–3（Introduction）、p.3–7（Methods）、p.7–18（Results、Table 1–5）、p.18–20（Discussion、Limitations、Declarations）。
- **abs** — medRxiv abstract page：<https://www.medrxiv.org/content/10.64898/2026.10.23.26366376v1>。

[Home](../) · [AI Papers](./)
