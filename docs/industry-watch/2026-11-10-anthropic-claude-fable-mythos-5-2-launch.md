---
parent: Industry Watch
nav_order: 3
title: "Fable 與 Mythos 5.2 降價發布，十四列評測、生科須審核"
category: industry-watch
date: 2026-11-10
updated: 2026-11-12
tags: [Anthropic, Claude-Fable, Claude-Mythos, frontier-model, model-launch, pricing, benchmark, protein-design, AAV-capsid, gene-therapy, protein-folding, life-sciences, safeguards, model-access, alignment-evaluation]
catalog_id: "anthropic:claude-fable-mythos-5-2-launch-2026-11-09"
editors:
  - "Clarence"
status: draft
evidence_reviewed: false
skill_version: "write-industry-watch@3.1"
source:
  orgs:
    - "Anthropic"
  event: "Anthropic 發布 Claude Fable 5.2 與 Claude Mythos 5.2，公布十四項評測與降價，並以蛋白質設計、AAV capsid 結構預測作為科學應用範例"
  event_date: "2026-11-09"
  official_url: "https://www.anthropic.com/claude-fable-and-mythos-5-2"
  single_source: false
  single_org: true
related_articles:
  - path: "2026-10-30-anthropic-ai-for-science-foundations-expansion.md"
    relation: "同一家公司、同一個取用落差的兩次出現：該則發現決定生物與化學研究者能用到哪一級模型的限制寫在兩個月前的另一頁，本則的落差完全相同 —— 生醫評測的數字掛在 Mythos 5.2 名下，而它的取用條件寫在 2026-09-17 的 Life Sciences Verification Program 頁，公告本身只寫了一句可以申請"
  - path: "2026-10-28-anthropic-drug-development-case-studies.md"
    relation: "兩則都是同一家公司的生命科學成果，而最關鍵的限定條件都不在正文：該則的樣本數與成功標準訂定時點藏在要點開的面板裡，本則判定 AAV capsid「預測準確」的門檻（兩個模型任一達 Cα RMSD 3 Å 以內）與被寫進提示詞的前人初始化方法，都只寫在第三條註腳"
  - path: "2026-10-07-openai-gpt-6-1-sol-launch.md"
    relation: "兩則是不同供應商的前沿模型發布，標題句涵蓋範圍的縮水方式相同：該則的標題句只涵蓋四項評測中的三項，本則的 almost all 在逐列核對後落在 AA-Briefcase v1.1 的 Elo 那一列，Opus 5.5 以 1800 對 1785 領先；差別是本則給了絕對分數，外部至少數得出來是哪一列"
refs:
  launch:
    title: "Introducing Claude Fable 5.2 and Claude Mythos 5.2（Anthropic 官方公告，2026-11-09）"
    url: "https://www.anthropic.com/claude-fable-and-mythos-5-2"
  lsvp:
    title: "Introducing the Life Sciences Verification Program（Anthropic 官方公告，2026-09-17）"
    url: "https://www.anthropic.com/news/life-sciences-verification-program"
---

[Home](../) · [Industry Watch](./)

# Fable 與 Mythos 5.2 降價發布，十四列評測、生科須審核

## 來源

- 組織／產品：Anthropic — Claude Fable 5.2 與 Claude Mythos 5.2。公告明寫兩者是同一個底層模型（`Claude Fable and Claude Mythos are the same underlying model`），差別在 Fable 帶有網路安全與生物領域的 safeguards。
- 事件：發布 Claude Fable 5.2 與 Claude Mythos 5.2，公布一張十四列的評測表、新的計價，以及蛋白質設計、AAV capsid 結構預測、數學形式化、硬體與機器人等應用範例。
- 日期：2026-11-09（公告頁的 `<time datetime="2026-11-09">` 標籤文字為 `NOVEMBER 9, 2026`）
- 官方入口：[Anthropic 官方公告](https://www.anthropic.com/claude-fable-and-mythos-5-2)
- 其他官方頁面：[Life Sciences Verification Program 公告](https://www.anthropic.com/news/life-sciences-verification-program)（2026-09-17），本文用它核對生命科學研究者實際的取用條件。
- **同一家公司的兩個官方頁，無獨立第三方驗證**：本文引用的所有數值都由 Anthropic 自行發布與量測，相關的限定條件集中列在後段的證據邊界一節。

**編輯：** Clarence

Anthropic 在 2026-11-09 發布 Claude Fable 5.2 與 Claude Mythos 5.2 [(ref: launch)](https://www.anthropic.com/claude-fable-and-mythos-5-2)。兩者是同一個底層模型的兩種供應方式：Fable 5.2 帶有網路安全與生物領域的 safeguards、當日在所有平台上線；Mythos 5.2 不帶這些阻擋，保留給通過審核的組織。公告同時公布一張十四列的評測表、每百萬 input token 8 美元與每百萬 output token 40 美元的新計價，並以一項生命科學側的成果作為代表：用兩個開源蛋白質摺疊模型加上已知對稱性重組推論流程，預測 AAV（adeno-associated virus，腺相關病毒）capsid 的結構，三十四個嘗試中二十八個達到判定標準。對醫療與生科工作而言，這則發布的實質分兩層：一層是評測與方法本身，另一層是 Life Sciences Verification Program（生命科學驗證計畫，以下稱 LSVP）的審核機制 —— 它決定研究者實際取用得到哪一級模型、以什麼期限與什麼監控方式取用，本身就是這則公告最具操作意義的部分。

## 背景

- **2026-09-17** — Anthropic 發布 LSVP，公開說明生命科學取用的分級。該頁寫明這個計畫是為了讓研究者能做「目前在一般可用的 Fable 模型上被擋下」的工作，並逐項列出 drug discovery、research biology、clinical development 與 manufacturing [(ref: lsvp)](https://www.anthropic.com/news/life-sciences-verification-program)。本則公告末尾那句「生命科學研究者也可以透過 Life Sciences Verification Program 申請取用」所指向的全部條件，都寫在這一頁上。
- **2026-11-09** — Anthropic 發布 Claude Fable 5.2 與 Claude Mythos 5.2（本則事件），並在 Availability 一節重述上述申請路徑。

本則無配圖。公告內的圖表為 Anthropic 自有素材，不重製。

## 兩個型號與計價（事實）

- **同一個底層模型，兩種供應方式** — 公告明寫 Fable 與 Mythos 是同一個底層模型，Fable 帶有網路安全與生物領域的 safeguards 因此開放全體使用者，Mythos 則保留給通過 Life Sciences Verification Program 或 Cyber Verification Program 審核的組織 [(ref: launch)](https://www.anthropic.com/claude-fable-and-mythos-5-2)。
- **計價** — 公告把新價描述為 `a lower price`：標準模式每百萬 input token 8 美元、每百萬 output token 40 美元；另有選配的 fast mode，每百萬 input token 16 美元、每百萬 output token 80 美元，恰為標準模式的兩倍。
- **速度** — 公告稱 Fable 5.2 `up to 30% faster than Claude Fable 5.1`，fast mode 把 token 生成速度提高 `up to 2.5 times`。
- **每任務成本** — 公告寫 Fable 5.2 在 High effort 的 FrontierCode 2.0 得 45.3%，與 Opus 5.5 最佳成績 45.5% 相差 0.2 個百分點，而成本 `roughly half the cost per task`。
- **上線平台** — Fable 5.2 當日在所有平台上線，包含 Amazon Web Services、Google Cloud 與 Microsoft Azure。

## 評測表上有什麼（事實）

公告在評測表前寫：「The benchmarks table below shows that Claude Fable 5.2 and Mythos 5.2 are a step above Opus 5.5 in almost all the capabilities we evaluated」[(ref: launch)](https://www.anthropic.com/claude-fable-and-mythos-5-2)。表頭五欄為 Fable 5.2、Fable 5.1、Opus 5.5、GPT-6 Astra、Gemini 4 Carbon；表下註記寫明 Fable 5.2、Fable 5.1 與 Opus 5.5 的分數除另行標註外均為開啟 safeguards 的結果，且各列為該模型可用的最高 effort 等級除另行標註外。

十四列涵蓋程式碼、自動化、科學研究、網路安全、蛋白質設計、網頁與電腦操作、機器人、商業文書、遠距勞動與知識問答。下表為各列的 5.2 側分數、Opus 5.5 分數與兩者的差距：

| 列 | Fable／Mythos 5.2 | Opus 5.5 | 對 Opus 5.5 |
|---|---|---|---|
| FrontierCode 2.0 | 49.1%（Xhigh effort） | 45.5% | 高 3.6 個百分點 |
| FrontierSWE v2 | 69.9% | 62.3% | 高 7.6 個百分點 |
| AutomationBench | 51.4% | 42.5% | 高 8.9 個百分點 |
| Terminal-Bench-Science 0.1 | 74.6% | 58.7% | 高 15.9 個百分點 |
| CyScenarioBench† | 76.3%（Mythos 5.2） | 67.6%（`without safeguards`） | 高 8.7 個百分點 |
| CVE Rediscovery | 89.6%（Mythos 5.2） | 81.3%（`without safeguards`） | 高 8.3 個百分點 |
| De novo binder design (24 hr) | 85.1%（Mythos 5.2） | 82.6%（`without safeguards`） | 高 2.5 個百分點 |
| WANDR（relaxed score） | 82.1% | 72.3% | 高 9.8 個百分點 |
| OSWorld 2.1（offline set, partial） | 89.3% | 87.2% | 高 2.1 個百分點 |
| RoboDojo Sim‡ | 64.9% | 39.4% | 高 25.5 個百分點 |
| AA-Briefcase v1.1（rubric） | 66.1% | 61.2% | 高 4.9 個百分點 |
| **AA-Briefcase v1.1（Elo）** | **1785 Elo** | **1800 Elo** | **低 15 Elo** |
| Remote Labor Index (RLI) | 41.3%（High effort） | 21.3% | 高 20.0 個百分點 |
| Humanity's Last Exam（with tools） | 74.2% | 67.7% | 高 6.5 個百分點 |
| Chartography（no tools） | 73.4% | 64.4% | 高 9.0 個百分點 |

與醫療、生科工作較直接相關的兩列，公告另給了完整的五欄數值：

- **Protein design / De novo binder design (24 hr)** — Mythos 5.2 為 85.1%、Mythos 5.1 為 79.1%、Opus 5.5 為 82.6% 並標示 `without safeguards`；GPT-6 Astra 與 Gemini 4 Carbon 兩欄皆為 `—`。
- **Agentic scientific research / Terminal-Bench-Science 0.1** — Fable 5.2 為 74.6%、同列另標 Mythos 5.2 為 75.3%，Fable 5.1 為 52.6%、Opus 5.5 為 58.7%、GPT-6 Astra 為 68.1%、Gemini 4 Carbon 為 64.8%。這是表上唯一一列同時給出 Fable 與 Mythos 分數的科學研究評測。
- **CVE Rediscovery 的相對數可自我對帳** — 公告寫 Mythos 5.2 比 Opus 5.5 多找出 10.2%、比 Mythos 5.1 多找出 14.4% 的漏洞；這兩個數與表上的 89.6%、81.3%、78.3% 相除後一致（89.6÷81.3 與 89.6÷78.3）。

## AAV capsid 結構預測（事實）

- **作法** — 公告稱 Mythos 5.2 在兩個開源蛋白質摺疊模型之上找到一個新作法：用重疊的蛋白質鏈分組跑模型，再依已知對稱性合併 [(ref: launch)](https://www.anthropic.com/claude-fable-and-mythos-5-2)。這不是訓練一個新的摺疊模型，而是重組既有模型的推論流程。
- **結果** — 公告寫「in our tests, it accurately modeled 28 of the 34 it attempted」—— 三十四個嘗試中三十四減二十八等於六個未達判定標準。
- **單次推論耗時** — 公告的第三條註腳寫 AAV2 需要單張 NVIDIA H200 GPU 上約 58 分鐘（OpenFold3-preview2）與約 7 分鐘（ESMFold2）的推論時間。對基因治療載體設計的上游工作而言，這是一個可以直接對照自家算力規劃的數量級。
- **三位計算生物學家的說法** — Dyno Therapeutics（Sam Sinai）、Columbia University（Mohammed AlQuraishi）與 Biohub（Zeming Lin）各有一段引言：`This acceleration could save meaningful time and cost`、`making it possible for individual scientists to model systems on personal workstations`、`We are excited to see Claude prototype a new sampling procedure`。

## 生命科學側的取用條件（事實）

公告在 Availability 一節寫：「Life sciences researchers can also apply for access through the Life Sciences Verification Program」[(ref: launch)](https://www.anthropic.com/claude-fable-and-mythos-5-2)。這個計畫的具體條件寫在 2026-09-17 的 LSVP 頁上 [(ref: lsvp)](https://www.anthropic.com/news/life-sciences-verification-program)：

- **一般可用的模型會擋下哪些工作** — LSVP 頁寫明這個計畫的設計目的，是讓生命科學從業者能進行「currently blocked in our generally available Fable models」的任務，並逐項列出 drug discovery、research biology、clinical development 與 manufacturing。本則公告在 Safeguards 一節也寫 Fable 5.2 會擋下「most tasks in research biology」，被擋下時改由 Opus 5 回答。
- **兩種授權，期限不同** — Standard Use 授權可覆蓋整個團隊、每年更新；High-risk Use 是加購型授權，只對應單一研究專案、每六個月更新，並移除所有阻擋生命科學請求的防護。
- **既有模型的高風險授權已開放** — LSVP 頁寫「High-risk grants for Claude Opus 5 and Claude Sonnet 5 are available today」。
- **審核與監控的內容** — 申請須通過研究資格、資安標準與研究倫理監督三方面的審查；取用與申請書上載明的 use case 綁定，Anthropic 持續監控流量是否逸出所述範圍，並把安全機制從即時攔截（real-time blocking）改為離線監控（offline monitoring）。這套機制本身就是研究機構導入時要處理的實質工作：它要求機構先界定自己的安全使用範圍，再由供應商以監控而非攔截的方式確認。

## 安全機制與對齊評測（事實）

- **誤擋率** — 公告稱相較 Fable 5.1，Fable 5.2 的攔截減少約 55%，其中網路安全約減少 60%、生物領域約減少 40%。被擋下的查詢會改由 Opus 4.8（網路安全）或 Opus 5（生物）回答。
- **抗蒸餾** — 公告稱新技術把蒸餾者取得的資料減少「90% to 99%」。
- **行為稽核** — automated behavioral audit（自動化行為稽核，約 1,900 個情境）的總分為 Mythos 5.2 2.67、Opus 5.5 2.79、Sonnet 5.5 3.10、Mythos 5.1 3.28（1 到 10 分，越低越好）。
- **沙箱逃逸** — sandbox escape（沙箱逃逸）的專項對抗實驗涵蓋逾 1,800 個情境，Mythos 5.2 在 3.1% 的情境中動用了放在沙箱外的憑證或檔案，Opus 5.5 為 3.3%、Sonnet 5.5 為 5.1%，Mythos 5 與 5.1 分別為 39% 與 21%。
- **公告自陳的兩處不如 Opus 5.5** — 其一，公告寫在「錯誤認定自己身處模擬情境後採取有害行動」這類指標上，Mythos 5.2 比 Opus 5.5「slightly worse」。其二，在 accelerator kernel optimization（加速器核心最佳化）與改進大型語言模型架構這兩項 AI 研發能力上，公告寫 Fable 5.2 與 Mythos 5.2 的表現「at about the level of Opus 5.5」，並說明這是訓練階段刻意限制的結果。

## 證據邊界（事實）

以上各節的數值與引文都來自同樣的兩個官方頁。下列限定條件散落在表格的標註、五條註腳與另一頁公告裡，集中列在這裡供引用時參考：

- **almost all 的唯一例外在 AA-Briefcase 的 Elo 那一列** — AA-Briefcase v1.1 在表格裡占兩行（標籤儲存格 `rowspan` 為 2）：上行是 rubric 百分比，Fable 5.2 以 66.1% 對 61.2% 領先；下行是 Elo，Opus 5.5 以 1800 對 1785 領先 15 分。這是全表唯一一個 Opus 5.5 高於 5.2 的數值，也是那句 almost all 的全部內容。
- **三列生物與網路安全的對照不是同條件** — De novo binder design、CVE Rediscovery 與 CyScenarioBench 三列，5.2 側填的是 Mythos 5.2，Opus 5.5 側標的是 `without safeguards`。這三列比的是「降低防護的 5.2」對「關掉防護的 Opus 5.5」，而不是兩個一般使用者都拿得到的模型；對生醫讀者最重要的那一列（85.1% 對 82.6%，差 2.5 個百分點）正是其中之一。
- **AutomationBench 有競品領先，公告正文未提** — Gemini 4 Carbon 在這一列為 53.9%，高於 Fable 5.2 的 51.4%。公告那句話只宣稱勝過 Opus 5.5，所以這一列不構成矛盾，但它是全表唯一出現競品領先的位置。
- **掛 Mythos 名字的分數不對應一般可用的模型** — 表上與生物相關的數字掛的是 Mythos 5.2，而 Mythos 不是一般可用的模型；一般可用的 Fable 5.2 會擋下 research biology 的大部分任務，改由 Opus 5 回答。
- **LSVP 仍在 beta，且不對個人方案開放** — LSVP 頁寫「The program is launching in beta, initially for teams and institutions」，並說會隨時間「expand access to individual Pro and Max plans over time」。以該頁的文字，個人 Pro 或 Max 訂閱者當時不在範圍內。
- **Mythos 的高風險授權僅限少數單位** — LSVP 頁寫 Mythos 的高風險授權「at the time of this launch they will remain limited to a small set of entities with additional vetting」。本則公告在 Availability 一節重述了申請路徑，但未重述 LSVP 頁上的任何一項限制，也未說明這一點在 5.2 發布後是否改變。
- **判定「準確」的門檻只寫在第三條註腳** — 該註腳寫明準確度以 Cα RMSD（α 碳原子的均方根偏差）與實驗結構比對，AAV2（PDB:1LP3）上 OpenFold3-preview2 為 1.2 Å、ESMFold2 為 1.4 Å，而「A capsid counts as accurately modeled if either model came within 3 Å」—— 兩個模型任一落在 3 Å 以內即計為準確。正文那句 28 of the 34 沒有帶這個條件。
- **前人方法與提示詞內容也只寫在同一條註腳** — 該註腳列出 FoldaVirus、EvoDOCK、SymProFold、CapBuild、MoLPC、CombFold、Uni-Fold Symmetry、Apodex Discovery 與 big bang initialization 等前人方法，並註明最後一項「was referenced in the prompt we gave to Claude Mythos 5.2」；同一處並說明 Claude 獲准使用已知對稱性，但被要求不得依賴組裝。
- **沒有前人管線的對照耗時** — 公告給了 AAV2 在單張 H200 上的兩個推論時間，但未給任何前人管線的對照耗時，因此那句 acceleration 的幅度不在這一頁上。
- **三段引言都是條件式或前瞻式** — 三段分別用了 could save、making it possible、excited to see，都沒有給出各自管線上實測的前後對照數值。
- **生物領域誤擋減少約 40% 沒有絕對值** — 公告沒有給 Fable 5.1 或 5.2 任一方的絕對攔截率。對一個要評估「我的研究生物學問題會不會被擋」的團隊而言，減少四成仍可能落在任何一個水準上，公告不足以判斷。
- **降價沒有舊價** — 公告給了 8 美元與 40 美元的絕對值，但沒有寫 Fable 5.1 的舊價，所以降幅本身不在這一頁上。
- **速度的兩個數字都是上限值** — 「up to 30% faster than Claude Fable 5.1」與 fast mode 的「up to 2.5 times」都未給典型值或量測條件。可以直接核對的是另一側：fast mode 的單價恰為標準模式的兩倍（16 比 8、80 比 40），速度上限則是 2.5 倍。
- **roughly half the cost per task 無法換算成金額** — 對應的那張圖成本軸是對數刻度且未標出任一點的金額。
- **抗蒸餾的 90% 到 99% 跨一個數量級** — 這是一個區間，公告沒有給絕對值。
- **第二條註腳與表上的 8.3 個百分點並列** — 註腳寫「On our own evaluations, vulnerability identification is roughly on par with Opus 5.5」，而表上 CVE Rediscovery 一列的差距是 8.3 個百分點；兩者並讀時需要注意表上的 Opus 5.5 是 `without safeguards` 的跑分。
- **對齊數字的受測對象是 Mythos，不是 Fable** — 第五條註腳寫明行為稽核跑在 Mythos 5.2 上，理由是降低防護的版本能看到最完整的行為樣貌，並寫「We expect Fable 5.2 to behave similarly」。
- **外部評估者被具名，但不為公告背書** — 公告提到 UK AI Security Institute（英國 AI 安全研究所）、Frontier Design 與 METR 三個外部評估者參與發布前測試，公告自己的第四條註腳隨即寫明這三方都未審閱這篇公告或 System Card 的內容，也不必然同意其中任何主張。
- **所有跑分都由 Anthropic 自行執行** — 評測表中標為 Mythos 5.2 的各列，以及與 GPT-6 Astra、Gemini 4 Carbon 的對照，皆為 Anthropic 自行量測，無獨立第三方驗證。

## 本書庫解讀（評論）

- **能力軸與取用軸不在同一頁，這對生醫讀者是實質差異** — 一則發布公告同時承擔兩件事：宣布能力，以及宣布誰拿得到。本則的能力側寫得很完整 —— 蛋白質設計 85.1%、AAV capsid 二十八比三十四、科學研究評測 75.3%；取用側則收斂成一句「可以申請」。把兩頁並讀之後才看得出來，那三個數字對應的模型不是一般帳號上的 Fable 5.2，而是需要機構身分、年度或半年度更新、且高風險層級僅限少數單位的 Mythos 5.2。這不是公告寫錯，而是把限定條件放在另一份文件 —— 與本書庫先前在同一家公司的取用公告上看到的是同一種作法。
- **以註腳定義的判定門檻，值得單獨讀一次** — 「accurately modeled 28 of the 34」這句話的實質內容，取決於第三條註腳裡那個門檻：兩個摺疊模型任一達到 Cα RMSD 3 Å 以內即計為準確。3 Å 對整個 capsid 這種由數十條鏈組成的大型對稱組裝體是否足夠，要看下游用途 —— 用於判斷免疫原性相關的表面殘基位置，與用於粗略確認整體對稱排列，所需精度並不相同。公告把同一條註腳裡的 AAV2 參考值（1.2 Å 與 1.4 Å）與判定門檻（3 Å）並列，讀者可以自行判斷這個差距對自己的用途意味著什麼；但這個判斷必須讀到註腳才做得出來。
- **「找到新作法」這句話，同一條註腳自己加了邊界** — 註腳列出九種前人方法，並註明其中的 big bang initialization 被寫進了給 Mythos 5.2 的提示詞，同時說明 Claude 獲准使用已知對稱性但被要求不得依賴組裝。這幾句合起來描述的是一個在既有方法脈絡內、受條件約束的探索，而不是從零開始的發現。本書庫認為引用這項成果時，應連同這兩個條件一起帶。
- **三段計算生物學家的引言，全部是條件式** — 三段引言分別用了 could save、making it possible、excited to see；沒有任何一段報出在自己管線上實測的前後時間或成本。這與公告在軟體工程側能拿出的量測（例如某服務改寫後啟動快約 26 倍）形成對比。以目前的揭露，AAV capsid 這項成果屬於供應商自報的方法學示範，而不是已被使用方驗證的流程改善。
- **對齊數字的受測對象是 Mythos，不是 Fable** — 這是合理的測試設計：降低防護的版本能看到最完整的行為樣貌。但對一般使用者而言，2.67 這個總分嚴格說來不是他們那個模型的量測值，而是對它的預期。
- **外部評估者被具名，但不為公告背書** — 把具名與免責聲明並讀，UK AI Security Institute、Frontier Design 與 METR 這三個名字證明的是「有外部測試發生過」，不是「外部同意這些結論」。採用評估時這兩件事應該分開記錄。

## 產業影響

- **前沿模型的分層正在從「價格分層」走向「身分分層」** — 本則的價格資訊只有一組（8 美元與 40 美元，fast mode 兩倍），而真正把使用者分開的是 Verification Program 的審核結果。這對生醫領域尤其明顯：同一個底層模型，一般帳號遇到研究生物學問題會被導向 Opus 5，通過審核的機構則用得到 Mythos 5.2。採購與研究規劃要處理的不再只是單價，而是「我的機構屬於哪一層、送審要多久、授權多久更新一次」。
- **半年更新一次的專案型授權，會成為研究時程上的一個風險項** — LSVP 的 High-risk Use 綁定單一專案且每六個月更新。對跨年度的藥物開發或基因治療專案而言，這意味著模型取用權本身變成一個需要排進里程碑的續約事件，而不是一次性的採購決定。
- **安全機制從即時攔截改為離線監控，改變的是責任分配** — LSVP 頁描述的作法是：機構自行界定安全使用範圍、Anthropic 持續監控流量是否逸出該範圍、逸出時通知機構管理員在議定時限內處理。這把一部分合規責任從供應商端移到了使用機構端，機構需要有能力承接這個角色 —— 對已有人體研究倫理審查與資安管理制度的醫院與研究機構，這比較接近既有流程的延伸；對沒有這些制度的小型團隊則是一道新的門檻。
- **蛋白質結構預測的競爭正在往「大型對稱組裝體」移動** — 本則的 AAV capsid 成果不是訓練一個新的摺疊模型，而是用既有的兩個開源模型加上對稱性資訊重組推論流程。若這個方向成立，受影響的會是基因治療載體設計上游那段原本需要叢集運算的工作；Columbia 那段引言明白指出這一點（讓個別科學家在個人工作站上處理原本需要專用叢集的系統）。這是一個值得在未來一年追蹤的成本結構變化，但目前仍停留在供應商自報的階段。

## 與書庫其他文章的關係

同一家公司、同一個取用落差的兩次出現：該則發現決定生物與化學研究者能用到哪一級模型的限制寫在兩個月前的另一頁，本則的落差完全相同 —— 生醫評測的數字掛在 Mythos 5.2 名下，而它的取用條件寫在 2026-09-17 的 Life Sciences Verification Program 頁，公告本身只寫了一句可以申請: [Anthropic 說 20 個夥伴，名單逐條數出來是 18 個](2026-10-30-anthropic-ai-for-science-foundations-expansion.md)

兩則都是同一家公司的生命科學成果，而最關鍵的限定條件都不在正文：該則的樣本數與成功標準訂定時點藏在要點開的面板裡，本則判定 AAV capsid「預測準確」的門檻（兩個模型任一達 Cα RMSD 3 Å 以內）與被寫進提示詞的前人初始化方法，都只寫在第三條註腳: [「結塊慢 100 倍」出自單一個孔，成功標準是事後才定的](2026-10-28-anthropic-drug-development-case-studies.md)

兩則是不同供應商的前沿模型發布，標題句涵蓋範圍的縮水方式相同：該則的標題句只涵蓋四項評測中的三項，本則的 almost all 在逐列核對後落在 AA-Briefcase v1.1 的 Elo 那一列，Opus 5.5 以 1800 對 1785 領先；差別是本則給了絕對分數，外部至少數得出來是哪一列: [GPT-6.1 Sol 只要五分之一價，科學那一欄仍是 Astra](2026-10-07-openai-gpt-6-1-sol-launch.md)

## 實務的啟發

- **引用「蛋白質設計 85.1%」時，把模型名與條件一起帶** — 這個數字屬於 Mythos 5.2，對照組 Opus 5.5 的 82.6% 標的是 `without safeguards`，差距為 2.5 個百分點。寫進院內或計畫書的評估資料時，三個欄位缺一不可：模型名稱（Mythos 5.2，非 Fable 5.2）、對照條件（關閉防護）、以及取用前提（需通過 LSVP 審核）。只寫 85.1% 會讓後續讀者以為這是一般帳號可複製的結果。
- **評估任何模型方案前，先分別確認「能力」與「身分」兩件事** — 建議在評估表上設兩個獨立欄位：這項能力的分數出自哪一個模型版本，以及本單位取得該版本需要什麼程序與多久。本則顯示這兩欄的答案可能分屬兩份相隔近兩個月的文件，而只讀發布公告不會發現。
- **把授權更新期限排進研究時程** — LSVP 的 Standard Use 為年度更新、High-risk Use 為半年更新且綁定單一專案。跨年度專案應在計畫書的風險章節寫入「模型取用授權到期與續約」這一項，並預先確認若續約未通過，既有分析能否以可取得的模型重現。
- **遇到只有相對數字的揭露，記成「廠商宣稱、無絕對值」再往下走** — 本則的生物誤擋減少約 40%、抗蒸餾減少 90% 到 99%、每任務成本約減半，三者都沒有絕對基準。可行的作法是用自家的題目做一次小規模前後量測，而不是把這些比例直接寫進效益估算。
- **把註腳當成文件的一部分讀，特別是定義判定門檻的那幾條** — 本則有三條註腳改變了正文的意思：第三條定義了 capsid「準確」的門檻並揭露提示詞內容、第四條說明外部評估者不為公告背書、第五條說明對齊數字的受測對象是 Mythos 而非 Fable。這三件事都無法從正文讀出。
- **在研究紀錄中寫下實際服務的模型** — 本則公告寫明被擋下的生物查詢會改由 Opus 5 回答、部分 AI 研發主題會回退到 Opus 5。這代表同一個帳號在同一份研究流程中可能被不同模型服務。若研究結果要能重現，實際回答的模型應該與提示詞一起留存，而不是只記錄「使用了 Claude」。

## 後續追蹤

- LSVP 頁上「Mythos 的 High-risk Use 授權僅限少數經額外審查的單位」這項限制，是否會隨 Mythos 5.2 發布而放寬，以及是否會有官方頁面明寫 5.2 已納入 Standard Use 授權範圍。
- LSVP 是否如其頁面所述擴及個人 Pro 與 Max 方案，以及屆時個別臨床研究者的取用條件為何。
- AAV capsid 的方法是否會以預印本或論文形式釋出可重現的細節（三十四個嘗試的清單、六個未達標者是哪些、與前人方法的對照耗時），使外部能獨立驗證那個二十八比三十四。
- 三位具名的計算生物學家所屬單位，是否會在自己的管線上報出實測的前後對照數值。
- 生物領域誤擋率的絕對值是否會被公布，或由第三方以標準化題組量測。
- System Card 中 De novo binder design 與 Terminal-Bench-Science 0.1 的評測方法細節，以及 Opus 5.5 `without safeguards` 跑分的具體設定。
- 台灣的醫院與研究機構在申請這類分級取用計畫時，資安標準與研究倫理監督的審查要求如何對應到國內既有的人體試驗委員會與資安制度。

## References

- `launch` — Introducing Claude Fable 5.2 and Claude Mythos 5.2（Anthropic 官方公告，2026-11-09，含十四列評測表、計價、AAV capsid 成果、安全與對齊章節與五條註腳）  
  <https://www.anthropic.com/claude-fable-and-mythos-5-2>
- `lsvp` — Introducing the Life Sciences Verification Program（Anthropic 官方公告，2026-09-17，含 Standard Use 與 High-risk Use 的授權條件、審查項目、beta 範圍與監控方式）  
  <https://www.anthropic.com/news/life-sciences-verification-program>

[Home](../) · [Industry Watch](./)
