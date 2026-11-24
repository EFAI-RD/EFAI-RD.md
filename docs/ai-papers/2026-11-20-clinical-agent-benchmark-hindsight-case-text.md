---
parent: AI Papers
nav_order: 3
title: "診斷代理基準的後見之明：LLM 讀病例摘要比讀檢傷資料多答對 14 點"
catalog_id: "arxiv:2611.22241"
editors:
  - "Clare"
refs:
  main:
    title: "Where Does Hindsight Enter Clinical Agent Benchmarks? An Audit of Simulators and Case Construction"
    url: "https://arxiv.org/html/2611.22241v1"
  abs:
    title: "arXiv abstract page: 2611.22241v1"
    url: "https://arxiv.org/abs/2611.22241v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# 診斷代理基準的後見之明：LLM 讀病例摘要比讀檢傷資料多答對 14 點

## 來源

- 團隊：作者依序為 Meilu Zhu（The University of Hong Kong, Department of Electrical and Computer Engineering）、Xiaohan Li（The University of Hong Kong, Faculty of Dentistry, Department of Restorative Dental Sciences）、Axiu Mao（City University of Hong Kong, Department of Infectious Diseases and Public Health；通訊作者）。[(ref: main author block)](https://arxiv.org/html/2611.22241v1)
- 論文：*Where Does Hindsight Enter Clinical Agent Benchmarks? An Audit of Simulators and Case Construction*，arXiv:2611.22241v1（cs.CL），2026-11-17 提交，目前只有 v1；arXiv 頁未註記發表場合；授權為 arXiv 非專屬散布授權（nonexclusive-distrib 1.0）。[(ref: abstract)](https://arxiv.org/abs/2611.22241v1)
- 識別碼：arXiv [2611.22241](https://arxiv.org/abs/2611.22241v1)；DOI [10.48550/arXiv.2611.22241](https://doi.org/10.48550/arXiv.2611.22241)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.22241v1)、[PDF v1](https://arxiv.org/pdf/2611.22241v1)。
- 程式與資料：資料為 PhysioNet credentialed 存取的 MIMIC-IV v3.1、MIMIC-IV-Note v2.2 與 MIMIC-IV-ED；所有模型在本地伺服器執行，不釋出病人層級文字或生成紀錄。論文寫明程式碼與彙總結果「將會釋出」，正文未附 repo 連結；各項預先登錄的檢定規則與修訂紀錄存於 OSF。[(ref: main Ethics Statement)](https://arxiv.org/html/2611.22241v1#Sx2) [(ref: main Appendix C)](https://arxiv.org/html/2611.22241v1#A3) [(ref: main Appendix A)](https://arxiv.org/html/2611.22241v1#A1)
- 研究性質：稽核（audit）研究，不是新模型。模擬器、LLM 診斷與互動代理都實際執行；樣本為 27,489 次急診住院，分析附病人層級 bootstrap 95% 區間。全文最主要的發現（病例文字通道）是在預先登錄的模擬器檢定全部未達標後以探索性分析找到，再以預先登錄的規則在 validation split 上複製；作者稱兩個 split 同屬一個 pilot cohort，因此這是同一隊列中保留病人的複製，不是獨立的確認性研究。[(ref: main §3)](https://arxiv.org/html/2611.22241v1#S3) [(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2) [(ref: main §6)](https://arxiv.org/html/2611.22241v1#S6)
- 證據邊界：本文數值以 arXiv v1 HTML 版的表 1–4、表 6、表 9 與正文為準；只以圖呈現的逐模型與逐類別結果（圖 2、圖 4–6）未納入本文引述。

**編輯：** Clare

作者把 LLM 診斷代理基準常見的兩個建構步驟拆開量測：告訴檢驗模擬器最終診斷幾乎沒有讓模擬結果更好猜，但同一次急診住院若改給基準式病例摘要而不是檢傷時可得的資訊，四個 LLM 的零樣本診斷準確率從 25.4% 升到 39.7%，而且刪掉診斷名稱後差距不變。[(ref: main Table 2)](https://arxiv.org/html/2611.22241v1#S5.T2) [(ref: main Table 3)](https://arxiv.org/html/2611.22241v1#S5.T3)

## 流程

![左右兩欄圖。左欄標題「Three hindsight channels (MIMIC-IV, 27,489 emergency admissions)」。最上排兩個實線圓角框：左為灰底深灰框「Discharge summary (written after the diagnosis) + final diagnosis D」，右為淺綠底綠框「ED triage record (at arrival) + pre-admission history」。中排兩框：左為淺藍底藍框「Simulator writes unrecorded lab results (profile: history H, +/- D)」，右為淺橘底橘框「Agent-facing case text V1 LLM summary / V2 history vs V3 presentation-time view」。灰框有兩支深灰箭頭分別指向中排兩框，綠框以一支綠色箭頭指向橘框。中排兩框各以向下箭頭連到最下排白底框：藍框寫「(1) Diagnosis line to simulator: <= 1.4 pp」「(2) Retrospective history: +0.014 to +0.059 p_true」「Prompted gatekeepers keep 16-62% of real lab signal (trained world models 70-84%)」；橘框寫「(3) Case text, top-1 gain over V3」「4 zero-shot LLMs +14.2 pp (V1), +19.8 pp (V2)」「6 interactive agents +7.2 pp (V1), +12.5 pp (V2)」「Upper bound on hindsight」。右欄為分組長條圖，標題「Same 1,053 test admissions, four views of the case」，縱軸「Top-1 accuracy over 50 CCSR groups (%)」刻度 0–50，四組橫軸為 V1 benchmark summary、V2 discharge history、V3 presentation-time、V4 sex + chief complaint；橘色長條為「Mean of 4 zero-shot LLMs (Table 2)」39.7／45.3／25.4／25.2，藍色長條為「Mean of 6 interactive agents (Table 9)」37.9／43.2／30.7，V4 沒有藍色長條，位置以灰色直排小字「not run」標示。左下角小字「Redrawn by EFAI-RD from arXiv:2611.22241v1 Figure 1, Tables 2, 4 and 9」。](assets/clinical-agent-benchmark-hindsight-channels.png)

*圖：本書庫依論文圖 1 的三通道架構重繪（左），並以表 2 與表 9 的平均 top-1 準確率畫出同一批 1,053 次住院在四種病例寫法下的結果（右）。左欄的模擬器數字來自 [§1](https://arxiv.org/html/2611.22241v1#S1) 與 [表 4](https://arxiv.org/html/2611.22241v1#S5.T4)；互動代理沒有跑 V4。*

## 背景／問題

作者引用多篇工作指出，LLM 代理正被當作「逐步診斷者」來評估：讀一段病人簡介、開檢查、收到結果、給出診斷，而這些基準的分數被用來比較模型，甚至用來主張代理接近臨床可用。[(ref: main §1)](https://arxiv.org/html/2611.22241v1#S1) 這些基準只能用回溯性電子病歷建構，作者歸納出大多數基準共用的兩個步驟：代理讀的病例常由 LLM 從出院摘要改寫而來，而出院摘要是在診斷確定後才寫的；代理開了但實際沒做的檢查，則由一個模擬器回答（微調的 world model，或用提示詞驅動的 gatekeeper LLM），模擬器通常拿得到完整病歷、包括最終診斷。[(ref: main §1)](https://arxiv.org/html/2611.22241v1#S1)

兩個步驟都可能把「只有知道答案才會有的資訊」帶進代理看得到的地方，論文稱之為 hindsight。作者指出現有基準的防線集中在第二步、而且集中在最顯眼的形式：要求模擬器不要說出答案、濾掉寫出診斷名稱的病例文字。這些防線是否擋住了主要來源，論文認為過去沒有被量過。[(ref: main §1)](https://arxiv.org/html/2611.22241v1#S1)

## 方法摘要

- **三個通道** — 以最終診斷 D、出院摘要中體檢段之前的回溯病史 H、以及只含性別與主訴的呈現時資訊 P 定義三種模擬器輸入：S+ =（H, D）是一般基準設定，S− = H，S0 = P。S+ 對 S− 隔離「診斷那一行」（通道 1），S− 對 S0 隔離回溯脈絡（通道 2）；代理讀的病例文字另成通道 3。[(ref: main §3)](https://arxiv.org/html/2611.22241v1#S3)
- **只用真實資料訓練的 judge** — 模擬器通道的洩漏，以一個只在真實訓練資料上訓練的 judge 能多容易從（真實或模擬的）檢驗值猜出 D 來衡量。主要 judge（num）是對 300 個最常見檢驗項目的數值、異常旗標與缺值做 multinomial logistic regression；另有 gradient-boosted judge、文字＋數值 judge 與本地 LLM judge 作對照。所有結果都先遮掉診斷關鍵字。[(ref: main §3)](https://arxiv.org/html/2611.22241v1#S3)
- **指標** — p_true 為 judge 給正確類別的機率（五次模擬取平均），另報 top-1／top-5；signal retention =（模擬結果平均 p_true − c）/（真實結果平均 p_true − c），c = 1/50；typicalization 為「對該診斷屬非典型的真實結果被模擬器改成典型狀態」的比例。不確定性一律以病人層級 bootstrap 95% percentile interval 表示。[(ref: main §3)](https://arxiv.org/html/2611.22241v1#S3)
- **病例文字通道** — 同一次住院寫成四種 view：V1 依 DiagGym 指令由 LLM 寫的到院前摘要（通過 DiagGym 的洩漏過濾才保留）、V2 出院摘要中的病史、V3 由 MIMIC-IV-ED 檢傷紀錄（主訴、生命徵象、疼痛分數、檢傷級數）加上出院摘要裡描述入院前狀態的段落（過敏、過去病史、家族史）重建的呈現時版本、V4 性別＋主訴。本地 LLM 讀其中一種 view，在 50 個 CCSR 診斷群組中排序。[(ref: main §4)](https://arxiv.org/html/2611.22241v1#S4)
- **預先登錄** — 每次執行前把假說、主要指標、決策規則與失敗後的動作寫進有時間戳的版本化 protocol，事後不改；登錄是依序、內部進行的，每個檢定在前一個結果出來後才設計。[(ref: main §3)](https://arxiv.org/html/2611.22241v1#S3)

## 方法詳解

- **隊列建構** — 主診斷對應到 AHRQ CCSR 類別（ICD-9 經 CMS GEMs 轉換），保留出院摘要同時有病史、體檢與出院診斷段的急診或緊急住院（264,058 筆）；排除外傷（INJ）與精神行為（MBD）類別、轉院與術後住院；每位病人一次住院，取最常見的 50 類、每類最多 600 例，依病人 8:1:1 切分。入院體檢由本地 Qwen2.5-7B-Instruct 結構化（解析成功率 98.6%），剔除只有出院體檢或判定入院前已知診斷者，得 27,489 例。[(ref: main §4)](https://arxiv.org/html/2611.22241v1#S4)
- **與 DiagGym 的差異** — DiagGym 未釋出病例建構程式，作者依其論文描述實作，差異包括：體檢結構化與「入院前已知診斷」過濾改用本地 Qwen2.5-7B-Instruct（原為 DeepSeek-V3）、以 CCSR 分組並只留急診／緊急住院、自訓模擬器改為 Qwen2.5-3B＋LoRA、檢驗項目保留單一分析物層級（每例 54.0 項，對 28.4 項）。[(ref: main Appendix B)](https://arxiv.org/html/2611.22241v1#A2)
- **模擬器** — FT-3B 為 Qwen2.5-3B-Instruct＋LoRA（r = 64、α = 128、diagnosis dropout 0.5，同一模型可當 S+ 或 S−）；GK-14B、GK-32B（加給每項檢驗最常見的單位）、GK-72B 為 AWQ 量化的 Qwen2.5 Instruct，以 SDBench 式 gatekeeper 提示；另有 DiagGym 7B 公開權重與 Phi-4。每項結果在溫度 1.0 下抽 5 次，分 sequential（以先前真實結果為條件）與 independent（只看 profile）兩種。預先登錄的檢定只用 FT-3B、GK-14B 與 GK-32B，其餘為描述性複製。[(ref: main §4)](https://arxiv.org/html/2611.22241v1#S4) [(ref: main Table 6)](https://arxiv.org/html/2611.22241v1#A3.T6)
- **LLM 診斷** — Qwen2.5-7B、-14B-AWQ、-32B-AWQ 與 Phi-4 在溫度 0 下讀單一 view，事後加入 Llama-3.1-8B-Instruct 作第三個模型家族；變體包括在所有 view 刪除診斷詞、換一種提示詞措辭、以及 V3n（用寫 V1 的同一模型與指令把 V3 改寫成敘事體，作格式對照）。每個 view 另訓練一個 TF-IDF＋logistic regression 分類器作非 LLM 參考。作者明言 50 群組的零樣本 top-1 是「文字帶了多少診斷資訊」的探針，不是臨床能力的量測。[(ref: main §4)](https://arxiv.org/html/2611.22241v1#S4)
- **代理** — 預先登錄的端到端檢定（A′2）用 Qwen2.5-14B-Instruct-AWQ 代理，只看性別與主訴，可開最多五組檢驗（血球、生化、肝功能、乳酸、尿液），結果來自真實紀錄重播或 GK-14B 模擬，限 721 例五組檢驗都有紀錄者。探索性的互動代理分析另用六個本地模型（7B–72B、三個家族）讀 V1、V2 或 V3，可在七種動作中最多提出 8 個請求（含第一份影像報告與入院體檢），沒有紀錄的檢查回覆「not done」。[(ref: main §4)](https://arxiv.org/html/2611.22241v1#S4) [(ref: main Appendix H)](https://arxiv.org/html/2611.22241v1#A8)
- **統計與運算** — 病人層級配對 bootstrap，預先登錄的檢定與 LLM 診斷 B = 10,000，其他描述性分析 B = 2,000；A′1–A′3 為單尾、Holm 校正的一族，E1 另有自己的 Holm 校正。全部實驗在一台四張 RTX 4090（24 GB）的伺服器上完成，成功的工作約用 155 GPU-hours。[(ref: main Table 6)](https://arxiv.org/html/2611.22241v1#A3.T6) [(ref: main Appendix L)](https://arxiv.org/html/2611.22241v1#A12)
- **論文未交代** — 程式碼尚未釋出，正文沒有 repo 連結；OSF 上的登錄文件以 view-only 連結提供，本文未核對其內容。
- **論文未交代** — 多個控制都以「刪除診斷詞」進行，但論文沒有說明診斷詞清單如何建立（來源詞表、是否涵蓋縮寫與同義詞）；Appendix G 只列出摘要分類器權重最高的詞例。[(ref: main §3)](https://arxiv.org/html/2611.22241v1#S3)

## 資料與實驗

**資料**

| 項目 | 內容 |
|---|---|
| 來源 | MIMIC-IV v3.1、MIMIC-IV-Note v2.2、MIMIC-IV-ED（美國單一中心） |
| 納入 | 急診或緊急住院，出院摘要含病史／體檢／出院診斷段；排除 INJ、MBD、轉院、術後 |
| 隊列 | 27,489 例（train 21,994／validation 2,748／test 2,747），50 個 CCSR 類別，每類最多 600 例 |
| 模擬器分析 | 460 個 test 病例（每類約 10 例） |
| 病例文字分析 | 1,053 個 test 病例（有 ED 檢傷紀錄且摘要通過洩漏過濾）；E1 複製用 1,091 個 validation 病例 |
| A′2 代理檢定 | 721 個五組檢驗皆有紀錄的 test 病例 |
| 檢查時間窗 | 入院前後 24 小時，各項目取第一次 |

[(ref: main §4)](https://arxiv.org/html/2611.22241v1#S4) [(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2)

**實驗：病例文字讓診斷變容易多少（論文表 2 節錄）**

| 模型 | V1 | V2 | V3 | V4 | V1−V3 | V2−V3 |
|---|---|---|---|---|---|---|
| Qwen2.5-7B | 37.5 | 42.8 | 23.1 | 23.2 | +14.4 | +19.8 |
| Qwen2.5-14B | 39.3 | 45.1 | 24.4 | 24.5 | +14.9 | +20.7 |
| Qwen2.5-32B | 40.0 | 46.0 | 27.5 | 25.8 | +12.4 | +18.4 |
| Phi-4 | 41.9 | 47.2 | 26.7 | 27.3 | +15.2 | +20.5 |
| Llama-3.1-8B（事後加入，不計入平均） | 34.4 | 39.8 | 17.7 | 18.9 | +16.7 | +22.1 |
| 平均（四個模型） | 39.7 | 45.3 | 25.4 | 25.2 | +14.2 | +19.8 |
| 刪除診斷詞（四模型平均） | 36.1 | 41.7 | 21.4 | 20.1 | +14.8 | +20.3 |
| 14B，換一種提示詞 | 29.1 | 26.2 | 19.1 | 22.1 | +10.0 | +7.1 |
| E1，validation 複製 | 36.2 | 43.1 | 25.0 | 23.5 | +11.1 | +18.1 |
| 文字分類器 | 48.1 | 55.1 | 33.1 | 35.0 | +14.9 | +21.9 |

單位為 50 個 CCSR 群組的零樣本 top-1 準確率（%），差值為百分點，由未四捨五入的準確率計算；論文註明每個模型的病人層級 bootstrap 95% 區間約 ±3 個百分點、四模型平均約 ±2.3 個百分點（皆 p < 0.001）。[(ref: main Table 2)](https://arxiv.org/html/2611.22241v1#S5.T2)

**實驗：所有預先登錄的檢定（論文表 3 節錄）**

| 檢定 | 設定 | 主要指標 | Δ [95% CI] | 達標？ |
|---|---|---|---|---|
| D1 | FT-3B，sequential | clf top-1，S+ − real | −0.080 [−0.113, −0.046] | 否 |
| A | GK-14B，sequential | clf top-1，S+ − S− | +0.007 [−0.004, +0.017] | 否 |
| A2 | GK-14B，independent | num p_true，S+ − real；S+ − S0 | −0.143 [−0.172, −0.114]；+0.017 [+0.007, +0.027] | 否 |
| A′1 | 摘要 vs 主訴 | 文字 clf p_true，摘要 − 主訴 | +0.002 [−0.008, +0.013]，p = 0.320 | 否 |
| A′2 | 代理，GK-14B | top-1，S+ − S0 | +0.000 [−0.015, +0.015]，p = 0.538 | 否 |
| A′3 | GK-32B＋單位，independent | num p_true，S+ − real | −0.117 [−0.146, −0.089]，p ≈ 1 | 否 |
| E1 | LLM 診斷，validation | top-1，V1 − V3；V2 − V3 | +0.111 [+0.089, +0.132]；+0.181 [+0.158, +0.203]（皆 p < 0.001） | 是 |

top-1 差值以比例表示（0.010 = 1 個百分點）；A′ 一族為單尾、Holm 校正、α = 0.05。[(ref: main Table 3)](https://arxiv.org/html/2611.22241v1#S5.T3) [(ref: main Table 5)](https://arxiv.org/html/2611.22241v1#A1.T5)

## 結果

- **告訴模擬器診斷，效果可忽略** — 在所有設定中，S+ 的模擬結果都比真實結果更難猜；診斷那一行最多增加 1.35 個百分點（FT-3B，S+ − S− top-1 [+0.30, +2.39]），對 gatekeeper 則量不到（GK-14B p_true −0.0005 [−0.007, +0.007]）。作者以同一批 judge 能偵測到回溯脈絡的痕跡與 gatekeeper 的稀釋，說明這個 null 不是 judge 不靈敏。[(ref: main §5.3)](https://arxiv.org/html/2611.22241v1#S5.SS3)
- **Prompted gatekeeper 會稀釋訊號** — 以 values-only 線性 judge 計，independent 生成的 gatekeeper 結果只保留真實訊號的 16–32%（boosted judge 為 43–62%），訓練過的 world model DiagGym 為 72%；sequential 生成時，訓練模型保留 77–84%、GK-14B 為 25%。從 GK-32B 到 GK-72B 保留率沒有再上升；未量化的 BF16 版 GK-14B 保留 19%，與量化版的 16% 相近。[(ref: main §5.4)](https://arxiv.org/html/2611.22241v1#S5.SS4) [(ref: main Table 4)](https://arxiv.org/html/2611.22241v1#S5.T4)
- **回溯脈絡留下小而一致的痕跡** — S+ − S0 在每個模擬器都為正（p_true +0.014 到 +0.059，DiagGym 最大）；由於 S+ 與 S− 無法區分，作者判斷痕跡來自回溯病史而非診斷那一行。這些對比為次要分析。[(ref: main §5.4)](https://arxiv.org/html/2611.22241v1#S5.SS4)
- **回溯病史本身就帶答案** — 在 validation split 的 2,748 例上，只讀回溯病史 H 的文字分類器 top-1 為 55.9%，高於讀全部真實檢查結果的 judge（40.0%），刪除診斷詞後仍為 55.8%；52% 的病史提到診斷詞。通過洩漏過濾的 DiagGym 式摘要中仍有 46.9% 含診斷詞，分類器 top-1 從主訴的 35.7% 升到 49.1%（+13.4 個百分點 [+10.9, +15.9]）。[(ref: main §5.1)](https://arxiv.org/html/2611.22241v1#S5.SS1) [(ref: main Table 1)](https://arxiv.org/html/2611.22241v1#S5.T1)
- **登錄的主要指標選錯，作者照實報告** — 同一個摘要對主訴的比較，在預先登錄的 A′1 主要指標 p_true 上沒有差異（+0.002，p = 0.32），原因是比較了兩個校準不同的分類器；作者依規則把 A′1 報為不支持，準確率差異列為次要。[(ref: main §5.1)](https://arxiv.org/html/2611.22241v1#S5.SS1)
- **病例文字是最大的通道** — 四個 LLM 讀摘要比讀 V3 多答對 14.2 個百分點（95% CI [12.0, 16.5]），讀出院病史多 19.8 個百分點（[17.5, 22.2]）；預先登錄的 E1 在不重疊的 validation 病人上複製成功（+11.1 與 +18.1 個百分點）。把 V3 改寫成敘事體只讓準確率升 1.5 個百分點，V1 − V3n 仍為 +13.2 個百分點；刪除所有 view 的診斷詞後差距不變。[(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2)
- **訊號在名稱過濾抓不到的字詞裡** — 刪除診斷詞、檢查、治療、住院經過或病史類詞再重訓分類器，各類別單獨刪除時 top-1 變化都不到 1 個百分點；五類一起刪仍有 0.499，比主訴高 14 個百分點。權重最高的是症狀描述、同義詞與縮寫，例如 melena 對應腸胃道出血、flatus 對應腸阻塞。作者指出單看文字無法分辨這些字詞是到院時就被說出，還是知道答案的作者挑選寫進去的。[(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2)
- **檢傷結構化資訊幾乎沒有加分** — V3 對 V4 只多 0.2 個百分點（[−2.2, 2.8]）；換一種提示詞措辭時差距縮小但仍在（V1 為 +10.0 個百分點），49 個至少十例的類別中有 82% 出現差距。[(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2)
- **互動代理分數被抬高，排名幾乎不變** — 六個代理讀基準文字時全部得分較高，平均 V1 +7.2 個百分點 [5.6, 8.8]、V2 +12.5 個百分點 [10.8, 14.2]；V1 與 V3 的排名 Kendall τ = 0.87，唯一的對調是 Phi-4 與 Qwen2.5-32B。[(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2) [(ref: main Table 9)](https://arxiv.org/html/2611.22241v1#A8.T9)
- **登錄的代理檢定無法下結論** — 14B 代理用真實結果 top-1 20.7%、用任一 gatekeeper 19.3%，完全不給檢驗也有 19.6%，表示它幾乎沒用到檢驗。事後挑出八個通常靠這五組檢驗確診的類別（175 例）時，32B 代理確實用到結果，且 S+ − S0 top-1 +4.0 個百分點 [1.1, 7.4]；作者標明這是探索性、未做多重比較校正，且把診斷那一行與回溯 profile 混在一起。[(ref: main §5.3)](https://arxiv.org/html/2611.22241v1#S5.SS3)

## 限制

- **單一資料來源與本地模型** — 只用 MIMIC-IV（美國單一中心），所有模型都在本地推論；模擬器只涵蓋 Qwen2.5（含由其微調的 DiagGym）與 Phi-4 兩個家族，沒有 SDBench 所用 o4-mini gatekeeper 這類專有模型。作者提醒稀釋程度可能反映可在本地跑的開放模型的上限，不應外推到前沿模型。[(ref: main Limitations)](https://arxiv.org/html/2611.22241v1#Sx1) [(ref: main §5.4)](https://arxiv.org/html/2611.22241v1#S5.SS4)
- **差距是後見之明的上限，不是估計值** — MIMIC-IV 沒有急診醫師當下寫的紀錄，V3 缺少到院時的現病史；檢傷主訴比出院摘要中的主訴簡短、社會史被去識別、未納入用藥整合，因此 V3 可能低估了當下合法可得的資訊。差距中有多少是後見之明、多少是床邊本來問得到的病史，論文無法回答。[(ref: main Limitations)](https://arxiv.org/html/2611.22241v1#Sx1)
- **主要發現是探索性的** — 病例文字分析是在 pilot test split 上探索發現，再於同一隊列的 validation split 複製；只涵蓋約 60% 有 ED 檢傷紀錄的住院；LLM 差距大小對提示詞敏感，只測了一種替代提示詞。[(ref: main Limitations)](https://arxiv.org/html/2611.22241v1#Sx1)
- **量測依賴 judge** — boosted judge 找回的訊號約為線性 judge 的兩到三倍，因此稀釋只報區間；更強的 judge 可能偵測到本文沒抓到的模擬器洩漏。模擬器稽核只涵蓋檢驗套組，影像、病理與內視鏡報告是自由文字，知道診斷的 gatekeeper 可能在措辭中透露答案。[(ref: main Limitations)](https://arxiv.org/html/2611.22241v1#Sx1)
- **代理與登錄設計** — A′2 的代理偏弱（top-1 約 20–24%，檢驗最多只帶來 2 個百分點），只能開五組檢驗；登錄是內部、有時間戳、依序設計，不是事先存放於公開登錄處的單一計畫。[(ref: main Limitations)](https://arxiv.org/html/2611.22241v1#Sx1)
- **範圍** — 只研究 50 個常見急診類別，排除外傷與精神疾患；罕見疾病可能表現不同；以呈現時資訊建構的基準能否分出實力相近的代理尚未測試。[(ref: main Limitations)](https://arxiv.org/html/2611.22241v1#Sx1)

## 與書庫其他文章的關係

兩篇都指出下游 LLM 的表現被病歷文字本身的內容左右；note bloat 那篇在病歷中刻意埋入未證實的鑑別診斷，看 LLM 摘要是否沿用，本篇則量出由出院摘要改寫的病例文字讓 LLM 診斷比檢傷資訊多答對 14–20 個百分點: [病歷埋入未證實鑑別診斷，下游 LLM 摘要沿用最高 31%](2026-11-17-llm-note-bloat-diagnostic-overcall.md)

兩篇都在稽核醫療基準的分數是否被洩漏灌高；胸片＋EHR 那篇的洩漏來自 EHR 向量等同病人識別碼，本篇的主要來源則是由出院摘要建構的病例文字，而且刪掉診斷名稱也擋不住: [查表就追平最佳模型：胸片＋EHR 不平衡基準的病人洩漏](2026-11-06-cxr-ehr-imbalance-benchmark-patient-leakage.md)

本綜述從另一個角度質疑同一類基準：作者主張只以最終答案計分的臨床評估看不到推理過程中的錯誤，並整理多代理與工具型系統中早期錯誤沿流程放大的 hallucination cascade 證據；本篇則具體量出病例文字本身就能把診斷分數灌高: [臨床 LLM 安全綜述：符號否決層數字亮眼，多來自單一小型研究](2026-11-24-verifiable-logic-neuro-symbolic-review.md)

## 實務的啟發

- **可借用的量測方法** — 「同一次住院、不同病例寫法」的配對比較，加上只在真實資料上訓練的 judge 與 signal retention，可以直接拿來檢查自家或外部的診斷代理基準；作者把最低限度的建議寫成：在每個分數旁報告一個呈現時資訊的基線。[(ref: main Table 11)](https://arxiv.org/html/2611.22241v1#A11.T11)
- **待驗證的警訊** — 刪除診斷名稱不等於沒有洩漏；論文中症狀描述、同義詞與縮寫就足以維持差距。若用 LLM 從出院摘要或住院病程改寫評估病例，應預設分數偏高，直到有呈現時版本的對照為止。這個差距是上限，不是每個基準都會被抬高這麼多。
- **模擬器的選擇比它被告知什麼更值得檢查** — 在本研究的開放模型範圍內，prompted gatekeeper 產生的檢驗結果只保留部分真實訊號，而且在一個事後子集中可能抬高會用檢驗的代理分數；這部分是探索性結果，不應直接外推到專有模型，但在比較代理之前先確認代理真的有用到模擬結果，是低成本的檢查。[(ref: main §6)](https://arxiv.org/html/2611.22241v1#S6)
- **排名比絕對分數可靠** — 六個代理的排名在不同病例寫法下大致不變，因此基準較適合拿來比較模型相對強弱；把絕對準確率當成床邊表現的說法，在本文的證據下站不住。[(ref: main §5.2)](https://arxiv.org/html/2611.22241v1#S5.SS2)

## References

- `main` — Meilu Zhu, Xiaohan Li, Axiu Mao. *Where Does Hindsight Enter Clinical Agent Benchmarks? An Audit of Simulators and Case Construction*. arXiv:2611.22241v1, 2026. HTML：https://arxiv.org/html/2611.22241v1 ；用到的深鏈：[author block](https://arxiv.org/html/2611.22241v1)、[§1](https://arxiv.org/html/2611.22241v1#S1)、[§3](https://arxiv.org/html/2611.22241v1#S3)、[§4](https://arxiv.org/html/2611.22241v1#S4)、[§5.1](https://arxiv.org/html/2611.22241v1#S5.SS1)、[Table 1](https://arxiv.org/html/2611.22241v1#S5.T1)、[§5.2](https://arxiv.org/html/2611.22241v1#S5.SS2)、[Table 2](https://arxiv.org/html/2611.22241v1#S5.T2)、[§5.3](https://arxiv.org/html/2611.22241v1#S5.SS3)、[Table 3](https://arxiv.org/html/2611.22241v1#S5.T3)、[§5.4](https://arxiv.org/html/2611.22241v1#S5.SS4)、[Table 4](https://arxiv.org/html/2611.22241v1#S5.T4)、[§6](https://arxiv.org/html/2611.22241v1#S6)、[Limitations](https://arxiv.org/html/2611.22241v1#Sx1)、[Ethics Statement](https://arxiv.org/html/2611.22241v1#Sx2)、[Appendix A](https://arxiv.org/html/2611.22241v1#A1)、[Table 5](https://arxiv.org/html/2611.22241v1#A1.T5)、[Appendix B](https://arxiv.org/html/2611.22241v1#A2)、[Appendix C](https://arxiv.org/html/2611.22241v1#A3)、[Table 6](https://arxiv.org/html/2611.22241v1#A3.T6)、[Appendix H](https://arxiv.org/html/2611.22241v1#A8)、[Table 9](https://arxiv.org/html/2611.22241v1#A8.T9)、[Table 11](https://arxiv.org/html/2611.22241v1#A11.T11)、[Appendix L](https://arxiv.org/html/2611.22241v1#A12)
- `abstract` — arXiv abstract page, 2611.22241v1：https://arxiv.org/abs/2611.22241v1 （PDF：https://arxiv.org/pdf/2611.22241v1 ；DOI：https://doi.org/10.48550/arXiv.2611.22241）

[Home](../) · [AI Papers](./)
