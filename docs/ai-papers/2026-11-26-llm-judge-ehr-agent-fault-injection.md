---
parent: AI Papers
nav_order: 4
title: "LLM judge 審 EHR 代理：只看最終答案，正確紀錄也誤報 56%"
catalog_id: "arxiv:2611.33012"
editors:
  - "Clare"
refs:
  main:
    title: "Can LLM Judges Catch Unsafe Clinical Actions? A Fault-Injection Study"
    url: "https://arxiv.org/html/2611.33012v1"
  abs:
    title: "arXiv abstract page: 2611.33012v1"
    url: "https://arxiv.org/abs/2611.33012v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# LLM judge 審 EHR 代理：只看最終答案，正確紀錄也誤報 56%

## 來源

- 團隊：單一作者 Neda Ghafouri（University of Central Florida, Computer Science Department, Orlando）。[(ref: abstract)](https://arxiv.org/abs/2611.33012v1) [(ref: PDF v1)](https://arxiv.org/pdf/2611.33012v1)
- 論文：*Can LLM Judges Catch Unsafe Clinical Actions? A Fault-Injection Study*，arXiv:2611.33012v1（cs.AI；交叉列 cs.CL），2026-11-24 提交，目前只有 v1；arXiv 頁未註記發表場合；授權為 arXiv 非專屬散布授權（nonexclusive-distrib 1.0）。[(ref: abstract)](https://arxiv.org/abs/2611.33012v1)
- 識別碼：arXiv [2611.33012](https://arxiv.org/abs/2611.33012v1)；DOI [10.48550/arXiv.2611.33012](https://doi.org/10.48550/arXiv.2611.33012)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.33012v1)、[PDF v1](https://arxiv.org/pdf/2611.33012v1)。
- 程式與資料：論文寫明 fault injector、step checker、judge harness 與分析程式以 MIT 授權放在 GitHub（neda86/clinical-judge）；本文撰寫時該網址無法公開存取，因此 judge 的完整提示詞與檢查規則無法對照程式核實。環境為公開的 MedAgentBench（HAPI FHIR 伺服器、100 位去識別病人）。[(ref: main Code and Data Availability)](https://arxiv.org/html/2611.33012v1#Sx2) [(ref: main §IV-A)](https://arxiv.org/html/2611.33012v1#S4.SS1)
- 研究性質：評估方法稽核，不提出新模型。錯誤是人為注入的（mutation testing 式），六個開放權重 judge 都實際執行，共 32,112 個判定，主要結果附以任務為單位 bootstrap 的 95% 區間與預先設定的假說檢定；作者在方法段稱本研究為 pilot（其中一個假說 H5 的條件未納入）。嚴重度由作者自訂規則指派、未經臨床人員覆核，全文未提到臨床人員參與。[(ref: main §V)](https://arxiv.org/html/2611.33012v1#S5) [(ref: main §VI)](https://arxiv.org/html/2611.33012v1#S6) [(ref: main §IV-D)](https://arxiv.org/html/2611.33012v1#S4.SS4)
- 證據邊界：本文數值以 arXiv v1 HTML 版的表 I–VII 與正文為準；只以圖呈現的逐錯誤類型、逐 judge 數值（圖 4、圖 5）只引用正文有寫出的部分。

**編輯：** Clare

作者把一個錯誤注入已驗證正確的 EHR 代理軌跡，再讓 LLM judge 分別審正確版與錯誤版：只給 judge 看最終答案時，它分不出不改變答案的錯誤（paired discrimination −0.01），卻把 56% 的正確軌跡判為不安全；給了實際的 EHR 回應後，同類錯誤的 discrimination 升到約 0.8、誤報降到 6–8%。[(ref: main Table III)](https://arxiv.org/html/2611.33012v1#S7.T3)

## 流程

![左右兩欄圖。左欄標題「What the judge sees (instruction I2 fixed; Table III)」，為分組直條圖，四組橫軸依序為「V1–I2 final answer」「V2–I2 + tool calls」「V3n–I2 + EHR responses」「V3–I2 + agent reasoning」；每組三根直條：橘色「Δ, answer unchanged」−0.01／0.46／0.81／0.81，藍色「Δ, answer changed」0.00／0.16／0.68／0.59，灰色「False alarm on correct runs (÷100)」標值 54%／39%／7%／6%；縱軸「Paired discrimination Δ (bars 1–2) / false-alarm rate (bar 3)」，刻度 0.0–1.0，y = 0 處有黑色水平線。右欄標題「Injected faults detected (%), Table VI」，為綠色深淺熱圖，欄位由左至右為 Grader、Checker、Judges、Majority，九列依序為 F1 Wrong patient (60)、F2 Dose magnitude (18)、F3 Unit swap (60)、F4 Ignored observation (60)、F5 Skipped precondition (38)、F6 Hallucinated observation (60)、F7 False completion (60)、F8 Wrong code (60)、All faults (416)，格內數值同論文表 VI，最後一列與上方以黑色橫線分隔；熱圖下方文字「Checker + judge majority combined: 97% of all 416 faults」。左下角灰色小字「Redrawn by EFAI-RD from arXiv:2611.33012v1 Tables III and VI (MedAgentBench, six open-weight judges)」。](assets/llm-judge-ehr-fault-injection-views-and-detectors.png)

*圖：本書庫依論文表 III（左，固定 instruction I2、逐步增加 judge 看得到的證據）與表 VI（右，三種評估方式對八類注入錯誤的偵出率）重繪。左欄灰色直條是正確軌跡被誤判為不安全的比例，標值為百分比、柱高為比例；導言的 56% 來自同表 V1–I1 列。[(ref: main Table III)](https://arxiv.org/html/2611.33012v1#S7.T3) [(ref: main Table VI)](https://arxiv.org/html/2611.33012v1#S7.T6)*

## 背景／問題

作者引用多篇工作指出，臨床 LLM 代理已開始透過 FHIR 介面在 EHR 中查檢驗值、記錄生命徵象、開藥物與檢查醫囑，而評估這類代理越來越常交給第二個模型——LLM judge——讀代理的軌跡判斷是否正確且安全；judge 也被拿來當訓練訊號，例如 Doctor-R1 以含安全維度的逐輪 judge 獎勵訓練臨床代理。[(ref: main §I)](https://arxiv.org/html/2611.33012v1#S1)

作者要回答的是：一個代理可能跳過必要的檢驗確認、卻給出同樣的最終答案，這種錯誤在只看答案的 judge 眼中是看不見的。哪些 EHR 動作錯誤 judge 最容易漏、它是否較能辨認潛在傷害較大的錯誤、給它實際的 EHR 回應或代理自己的推理會不會幫忙，作者認為先前的臨床 judge 研究多針對臨床文字與生成回答，沒有針對結構化的 EHR 工具呼叫回答過。[(ref: main §I)](https://arxiv.org/html/2611.33012v1#S1) [(ref: main §II)](https://arxiv.org/html/2611.33012v1#S2)

## 方法摘要

- **Paired fault injection** — 借用軟體工程的 mutation testing：從通過基準 grader 與更嚴格 step checker 的正確軌跡（parent）複製出只含一個已知錯誤的 mutant，錯誤類型與位置都已知。[(ref: main §I)](https://arxiv.org/html/2611.33012v1#S1)
- **Paired discrimination（Δ）** — 對每類錯誤的 n 組 parent–mutant，Δ =（只有 mutant 被判不安全的組數 − 只有 parent 被判不安全的組數）/ n，等於 judge 對 mutant 與 parent 判為不安全的機率差；單看 recall 會獎勵「什麼都判不安全」的 judge，Δ 只計入由錯誤本身引起的判定。[(ref: main Eq. 1)](https://arxiv.org/html/2611.33012v1#S3.E1)
- **View-blind 錯誤** — 若錯誤不改變 judge 看到的內容，任何只依輸入判斷的 judge 期望 Δ 為 0；因此不改變最終答案的錯誤，原理上就無法被只看答案的 judge 偵出。[(ref: main §III)](https://arxiv.org/html/2611.33012v1#S3)
- **八類錯誤與嚴重度** — F1 錯病人、F2 劑量十倍、F3 單位對調、F4 忽略觀察值、F5 跳過前置檢驗、F6 虛報觀察值、F7 假完成、F8 錯代碼，另有 C0 無害編輯對照；嚴重度 S0–S3 依參考 NCC MERP 用藥錯誤分類的預設規則指派。[(ref: main Table I)](https://arxiv.org/html/2611.33012v1#S4.T1) [(ref: main Table II)](https://arxiv.org/html/2611.33012v1#S4.T2)
- **Views × instructions** — 四種 view：V1 只有任務與最終答案、V2 加上工具呼叫、V3n 再加實際 EHR 回應、V3 再加代理推理；三種 instruction：I1 整體評估、I2 逐步檢查、I3 臨床安全 checklist。[(ref: main §V)](https://arxiv.org/html/2611.33012v1#S5)

## 方法詳解

- **環境** — MedAgentBench 含 300 個醫師撰寫、十類的任務，跑在 HAPI FHIR 伺服器上（100 位去識別病人、785,207 筆 FHIR 紀錄），代理有九個 FHIR 函式、最多八輪。原基準只有三個任務需要開藥，作者仿照既有兩類用藥任務的措辭另加 15 個補鎂、補鉀任務，grader 不變，主要比較也另報只用原 300 題的結果。伺服器接受 POST 但不儲存，因此 judge 評的是「提出的醫囑」而非已執行的動作；被修改的 GET 會在新伺服器上重跑以取得實際回應。[(ref: main §IV-A)](https://arxiv.org/html/2611.33012v1#S4.SS1)
- **Clean parents** — gpt-oss 120B 與 Qwen3 32B 兩個代理各跑全部 315 題兩次（greedy 與溫度 0.7），共 1,260 次；基準 grader 分別接受 48% 與 45%。只有同時通過 grader 與 step checker 的才當 parent；checker 檢查病人身分、開立前是否查過必要檢驗、劑量、回報數值是否有 EHR 回應支持、宣稱與實際送出的醫囑是否一致。代理跑不出合適軌跡時改用由參考解答腳本產生的軌跡；34 個用藥 parent 中 32 個是腳本產生的。最終 193 個 parent（137 個代理、56 個腳本）。[(ref: main §IV-B)](https://arxiv.org/html/2611.33012v1#S4.SS2)
- **注入程序** — 每個 mutant 只改一個步驟；若最終答案提到受影響的數值（例如劑量），答案也同步改寫，讓答案與修改後的動作一致。替換用的病人識別碼與臨床代碼都取自資料集內的有效值，劑量錯誤一律為十倍增減。另有 60 個 C0 對照（重排 GET／POST 欄位或在數字後加 0），全部通過 grader 與 checker。[(ref: main §IV-E)](https://arxiv.org/html/2611.33012v1#S4.SS5)
- **Judges** — Qwen3 8B、Qwen3 32B、gpt-oss 20B、gpt-oss 120B、Gemma 3 27B 與醫療微調的 MedGemma 27B（與 Gemma 3 27B 同尺寸可直接對照）。八個條件：V1、V2、V3 各配 I1 與 I2，加上 V3–I3 與 V3n–I2。每個判定回傳不安全旗標、信心、疑似出錯步驟與錯誤類型；669 條軌跡（193 parent＋416 mutant＋60 對照）× 8 條件 × 6 judge = 32,112 個判定，另抽 10% 重判測一致性。[(ref: main §V)](https://arxiv.org/html/2611.33012v1#S5)
- **統計** — 95% 區間以 162 個任務為單位重抽 10,000 次（同任務軌跡綁在一起）。預先設定的假說 H1、H2、H4、H6 做 Holm 校正，H3、H7 為探索性；等價與非優越性檢定的 margin 為 0.05。[(ref: main §VI)](https://arxiv.org/html/2611.33012v1#S6)
- **論文未交代** — judge 的實際提示詞、I1–I3 的完整文字與 I3 checklist 內容沒有列在正文或附錄；judge 的解碼設定（溫度、取樣）也未說明。論文所附程式網址目前無法存取，無法從程式補足。
- **論文未交代** — step checker 只以文字描述檢查項目，沒有列出具體規則；表 VI 中 checker 對單位對調只偵出 30%、對錯代碼 0%，論文沒有說明是哪些規則沒有涵蓋。[(ref: main Table VI)](https://arxiv.org/html/2611.33012v1#S7.T6)
- **論文未交代** — 表 VI 的「Judges」與「Majority」欄是在哪個 view／instruction 條件下計算、Judges 欄如何跨六個 judge 彙總，表註與正文沒有寫明；表 III 的 critical miss 與 false alarm 欄也未標單位（表 V 同類欄位註明為百分比）。[(ref: main Table III)](https://arxiv.org/html/2611.33012v1#S7.T3) [(ref: main Table V)](https://arxiv.org/html/2611.33012v1#S7.T5)
- **論文未交代** — 10% 重判樣本如何抽取未說明；另外 15 個新增任務與 56 個腳本軌跡的內容沒有逐一公開於正文。

## 資料與實驗

**資料**

| 項目 | 內容 |
|---|---|
| 環境 | MedAgentBench：300 個醫師撰寫任務（十類）＋作者新增 15 個補鎂／補鉀任務；HAPI FHIR，100 位去識別病人、785,207 筆紀錄 |
| 代理執行 | gpt-oss 120B、Qwen3 32B 各 315 題 × 2（greedy、T = 0.7），共 1,260 次 |
| Clean parents | 193 條（137 條代理軌跡、56 條腳本軌跡）；信賴區間以 162 個任務為重抽單位 |
| 錯誤軌跡 | 416 條 mutant（八類，每條一個錯誤）；S3 嚴重度 12 條 |
| 對照 | 60 條無害編輯（C0） |
| 判定 | 669 條軌跡 × 8 條件 × 6 judge = 32,112 個判定 |

[(ref: main §IV-A)](https://arxiv.org/html/2611.33012v1#S4.SS1) [(ref: main §IV-B)](https://arxiv.org/html/2611.33012v1#S4.SS2) [(ref: main §IV-D)](https://arxiv.org/html/2611.33012v1#S4.SS4) [(ref: main §V)](https://arxiv.org/html/2611.33012v1#S5)

**錯誤類型（論文表 I）**

| ID | 錯誤 | 編輯方式 | n | 答案不變 % | 嚴重度 |
|---|---|---|---|---|---|
| F1 | Wrong patient | GET 或 POST 改用另一位真實病人的 MRN；被改的 GET 重跑 | 60 | 50 | S1–S3 |
| F2 | Dose magnitude | 鉀或鎂劑量乘或除以 10 | 18 | 100 | S2–S3 |
| F3 | Unit swap | 劑量或記錄值數字不變、單位改變（mEq → mg） | 60 | 100 | S1–S2 |
| F4 | Ignored observation | 檢驗值高於門檻仍開立，或低於門檻卻未開立 | 60 | 100 | S0–S3 |
| F5 | Skipped precondition | 刪除開立前必須的檢驗 GET，醫囑保留 | 38 | 100 | S1–S2 |
| F6 | Hallucinated observation | 推理或答案引用與工具回應矛盾的數值 | 60 | 0 | S1–S2 |
| F7 | False completion | 刪除必要的 POST，答案仍稱已完成 | 60 | 72 | S1–S3 |
| F8 | Wrong code | 改成另一個有效的 LOINC、NDC 或 SNOMED 代碼 | 60 | 100 | S1–S3 |
| C0 | Harmless edit | 重排欄位或在回報數字後加 0 | 60 | – | none |

[(ref: main Table I)](https://arxiv.org/html/2611.33012v1#S4.T1)

**實驗：judge 看到多少證據（論文表 III）**

| 條件 | Δ（答案不變） | Δ（答案改變） | Crit. miss | False alarm |
|---|---|---|---|---|
| V1–I1 | −0.01 [−0.03, 0.00] | 0.01 [−0.05, 0.06] | 11 [3, 21] | 56 [51, 61] |
| V1–I2 | −0.01 [−0.03, 0.01] | 0.00 [−0.06, 0.05] | 21 [12, 31] | 54 [49, 59] |
| V2–I1 | 0.49 [0.41, 0.57] | 0.10 [0.05, 0.15] | 0 [0, 0] | 44 [39, 50] |
| V2–I2 | 0.46 [0.38, 0.54] | 0.16 [0.11, 0.21] | 0 [0, 0] | 39 [34, 44] |
| V3n–I2 | 0.81 [0.75, 0.86] | 0.68 [0.62, 0.73] | 3 [0, 8] | 7 [5, 9] |
| V3–I1 | 0.80 [0.74, 0.86] | 0.69 [0.64, 0.74] | 8 [4, 13] | 8 [6, 11] |
| V3–I2 | 0.81 [0.75, 0.86] | 0.59 [0.53, 0.64] | 6 [1, 11] | 6 [4, 9] |
| V3–I3 | 0.83 [0.78, 0.88] | 0.65 [0.60, 0.70] | 3 [0, 7] | 6 [4, 8] |

Crit. miss 為未偵出的 S3 錯誤，False alarm 為正確軌跡被判為不安全；兩欄表 III 未標單位。方括號為 95% 區間。[(ref: main Table III)](https://arxiv.org/html/2611.33012v1#S7.T3)

**實驗：六個 judge（論文表 V，V3–I2）**

| Judge | Δ V1–I1 | Δ V3–I2 | Sensitivity | False alarm | Critical miss | Paired AUROC | ECE |
|---|---|---|---|---|---|---|---|
| Qwen3 8B（reasoning） | −0.04 | 0.67 [0.58, 0.76] | 87 | 13 | 0 [0, 0] | 0.86 | 0.10 |
| Qwen3 32B（reasoning） | 0.04 | 0.81 [0.76, 0.87] | 89 | 5 | 0 [0, 0] | 0.93 | 0.07 |
| gpt-oss 20B（reasoning） | −0.01 | 0.69 [0.63, 0.75] | 71 | 1 | 0 [0, 0] | 0.81 | 0.19 |
| gpt-oss 120B（reasoning） | −0.04 | 0.77 [0.67, 0.86] | 96 | 14 | 0 [0, 0] | 0.93 | 0.03 |
| Gemma 3 27B | 0.02 | 0.81 [0.76, 0.86] | 85 | 3 | 0 [0, 0] | 0.94 | 0.09 |
| MedGemma 27B（醫療微調） | −0.02 | 0.73 [0.68, 0.79] | 78 | 3 | 33 [8, 67] | 0.89 | 0.15 |

Sensitivity、False alarm、Critical miss 為百分比；信心相關指標使用與判定方向對齊的分數。[(ref: main Table V)](https://arxiv.org/html/2611.33012v1#S7.T5)

**實驗：三種評估方式的偵出率（論文表 VI，%）**

| 錯誤 | n | Grader | Checker | Judges | Majority |
|---|---|---|---|---|---|
| F1 Wrong patient | 60 | 100 | 100 | 98 | 100 |
| F2 Dose magnitude | 18 | 100 | 100 | 93 | 100 |
| F3 Unit swap | 60 | 100 | 30 | 99 | 100 |
| F4 Ignored observation | 60 | 100 | 100 | 78 | 85 |
| F5 Skipped precondition | 38 | 0 | 100 | 95 | 95 |
| F6 Hallucinated observation | 60 | 100 | 70 | 49 | 35 |
| F7 False completion | 60 | 100 | 100 | 80 | 90 |
| F8 Wrong code | 60 | 100 | 0 | 95 | 100 |
| All faults | 416 | 91 | 71 | 84 | 87 |

Grader 為 MedAgentBench 原本的評分器（使用參考答案），Checker 為作者的規則式 step checker。[(ref: main Table VI)](https://arxiv.org/html/2611.33012v1#S7.T6)

## 結果

- **只看答案的 judge 等於沒在分辨** — V1–I1 對不改變答案的錯誤 Δ = −0.01 [−0.03, 0.00]（H1），同時把 56% 的正確軌跡判為不安全；作者據此指出「抓到很多錯誤軌跡」不代表能把錯誤和正確分開。[(ref: main §VII-A)](https://arxiv.org/html/2611.33012v1#S7.SS1) [(ref: main Table IV)](https://arxiv.org/html/2611.33012v1#S7.T4)
- **EHR 回應是關鍵證據** — 加上工具呼叫後 discrimination 上升，再加上實際 EHR 回應又比只有動作時多 0.39；對虛報觀察值（F6），EHR 回應讓 Δ 增加 0.64 [0.57, 0.71]（H4），因為沒有回應就沒有東西可以對照。完整軌跡（V3–I2）整體 Δ = 0.75 [0.70, 0.80]，只用原 300 題時為 0.72 [0.67, 0.78]。[(ref: main §VII-A)](https://arxiv.org/html/2611.33012v1#S7.SS1)
- **代理的推理沒有幫忙** — 加入代理推理後整體 discrimination 沒有提升，F6 的偵測反而下降 0.18；在固定證據下改 instruction，Δ 差異最多 0.10；C0 對照幾乎沒有改變 discrimination。[(ref: main §VII-A)](https://arxiv.org/html/2611.33012v1#S7.SS1)
- **錯值比漏步驟好抓，與假說相反** — V3–I2 下病人識別、劑量、單位與代碼錯誤 Δ 為 0.83–0.93，漏步驟與錯用證據類為 0.45–0.74；預先設定的 H2 預期方向相反（F1–F3 減 F5、F7 為 +0.22 [0.14, 0.29]，Holm 校正 p = 1.000）。F6 在完整軌跡下仍只有 Δ = 0.45。[(ref: main §VII-B)](https://arxiv.org/html/2611.33012v1#S7.SS2) [(ref: main Table IV)](https://arxiv.org/html/2611.33012v1#S7.T4)
- **看見矛盾卻仍判安全** — 被多數 judge 漏掉的 18 個 S2–S3 錯誤全部屬於 F6；探索性檢視 40 個「安全」判定時，有 9 個的說明承認回報數值與 EHR 紀錄矛盾，卻仍判為安全。[(ref: main §VII-B)](https://arxiv.org/html/2611.33012v1#S7.SS2)
- **醫療微調沒有比較好** — V3–I2 下漏掉 S3 十倍過量的 4 個判定全部來自 MedGemma 27B（九個十倍過量中漏四個）；MedGemma 對 Gemma 3 的 Δ 差為 −0.08 [−0.14, −0.02]（H6）。Gemma 3 27B 與 Qwen3 32B 最高（Δ = 0.81）；同家族內較大模型較好。S3 錯誤只有 12 個，作者提醒不宜由此推論傷害程度與 judge 可靠度的一般關係。[(ref: main §VII-B)](https://arxiv.org/html/2611.33012v1#S7.SS2) [(ref: main §VII-C)](https://arxiv.org/html/2611.33012v1#S7.SS3)
- **多個 judge 合議提升有限** — 六個 judge 合併時 Δ 約 0.85，對最強單一 judge 的 0.81，作者解釋為彼此的錯誤大多重疊；「judge 偏好自家模型軌跡」在控制錯誤類型後消失（H7，探索性）。[(ref: main §VII-C)](https://arxiv.org/html/2611.33012v1#S7.SS3) [(ref: main §VIII)](https://arxiv.org/html/2611.33012v1#S8)
- **一致但信心不可靠** — 重判一致率 93.4%，偵出錯誤的類型分類 macro-F1 0.76；但許多 judge 在判「安全」時給高信心，儘管提示要求報告「不安全」的機率。若真實錯誤盛行率為 1%，最強 judge 的警示只有 25% 是真錯誤，5% 時為 63%。[(ref: main §VII-C)](https://arxiv.org/html/2611.33012v1#S7.SS3)
- **三種評估方式互補** — 原 grader 偵出 91% 的注入錯誤，但 38 條刻意跳過檢驗的軌跡全部放行；checker 偵出 71%，judge 多數決 87%；checker 加 judge 多數決達 97% [95, 98]，且不需參考答案。每個注入錯誤至少被三種方式之一抓到。[(ref: main §VII-D)](https://arxiv.org/html/2611.33012v1#S7.SS4)
- **未注入的真實執行也有漏網** — grader 接受的 587 次執行中，checker 標出 9 次（1.5%），都是代理正確地不開立醫囑、卻沒有查證明這個決定所需的檢驗；全部 1,260 次執行中 25% 至少觸發一條 checker 規則。[(ref: main §VII-E)](https://arxiv.org/html/2611.33012v1#S7.SS5) [(ref: main Table VII)](https://arxiv.org/html/2611.33012v1#S7.T7)

## 限制

- **單一模擬環境、任務短** — 只用一個模擬 EHR 環境與相對短的臨床任務，伺服器不保存 POST，judge 評的是提出的醫囑而非已執行的動作；作者認為可能無法代表更複雜的臨床流程。[(ref: main §IX)](https://arxiv.org/html/2611.33012v1#S9) [(ref: main §IV-A)](https://arxiv.org/html/2611.33012v1#S4.SS1)
- **人為單一錯誤、嚴重度未經臨床覆核** — 每條軌跡只注入一個錯誤，自然發生的錯誤與錯誤組合未研究；嚴重度是依預設規則指派的潛在傷害，作者明言未經臨床專家審閱。[(ref: main §IX)](https://arxiv.org/html/2611.33012v1#S9) [(ref: main §IV-D)](https://arxiv.org/html/2611.33012v1#S4.SS4)
- **用藥 parent 多為腳本產生** — 34 個用藥 parent 中 32 個由參考解答腳本產生，用藥類錯誤（F2 等）主要建立在腳本軌跡上，與真實代理軌跡的寫法可能不同；S3 錯誤只有 12 個。[(ref: main §IV-B)](https://arxiv.org/html/2611.33012v1#S4.SS2) [(ref: main §IV-D)](https://arxiv.org/html/2611.33012v1#S4.SS4)
- **重現細節不足** — judge 提示詞、checker 規則與解碼設定未列於論文，所附程式網址目前無法存取；表 VI 的 judge 欄計算條件未說明（見方法詳解）。
- **範圍** — 只測六個開放權重 judge，沒有專有模型；作者自稱 pilot，H5 的條件未納入。[(ref: main §V)](https://arxiv.org/html/2611.33012v1#S5) [(ref: main §VI)](https://arxiv.org/html/2611.33012v1#S6)

## 與書庫其他文章的關係

兩篇都在檢查臨床代理基準的分數能不能信；後見之明那篇稽核基準建構時病例文字與模擬器帶進答案，本篇則稽核事後評分的 LLM judge，發現只看最終答案時它分不出錯誤軌跡: [診斷代理基準的後見之明：LLM 讀病例摘要比讀檢傷資料多答對 14 點](2026-11-20-clinical-agent-benchmark-hindsight-case-text.md)

HealthAdminBench 把部分子項交給 LLM judge 計分並以人類一致率背書，本篇則在 EHR 代理上以注入錯誤顯示 judge 的可靠度取決於它看得到多少證據，且最好和規則式檢查並用: [HealthAdminBench：子項 78.4%，整件工作只做完 36.3%](2026-11-17-healthadminbench-computer-use-agents-admin.md)

## 實務的啟發

- **可借用的量測方法** — 「同一條軌跡、正確版與只差一個錯誤的版本」配對，加上 Δ 與無害編輯對照，是低成本檢查自家 LLM judge 的做法：它直接把「什麼都判不安全」的 judge 與真正分得出錯誤的 judge 分開。單報偵出率或 recall 會掩蓋這個差別。
- **待驗證的警訊** — 在本研究的環境中，只給 judge 最終答案或代理的自述，等於讓它看不到最危險的一類錯誤；若要用 judge 評 EHR 代理，至少應提供實際 EHR 回應。這是單一模擬環境、人為注入錯誤的結果，換到真實 EHR 與長流程時仍需重測。
- **醫療微調的 judge 不應預設較安全** — MedGemma 27B 在本研究中比同尺寸的通用模型差，且在完整軌跡條件下是唯一漏掉十倍過量的 judge；選 judge 時應以自己的錯誤類型實測，而不是看模型標籤。S3 樣本很少，這點應視為需要再驗證的訊號。
- **規則檢查與 judge 互補** — 本研究中原 grader 放行全部「跳過檢驗」的軌跡、checker 抓不到錯代碼、judge 抓不好虛報數值，三者合併才接近全數偵出；評估流程的設計問題比挑選單一 judge 更值得先處理。作者的 checker 規則未公開，實際採用時需要自行建立。

## References

- `main` — Neda Ghafouri. *Can LLM Judges Catch Unsafe Clinical Actions? A Fault-Injection Study*. arXiv:2611.33012v1, 2026. HTML：https://arxiv.org/html/2611.33012v1 ；用到的深鏈：[§I](https://arxiv.org/html/2611.33012v1#S1)、[§II](https://arxiv.org/html/2611.33012v1#S2)、[§III](https://arxiv.org/html/2611.33012v1#S3)、[Eq. 1](https://arxiv.org/html/2611.33012v1#S3.E1)、[§IV-A](https://arxiv.org/html/2611.33012v1#S4.SS1)、[§IV-B](https://arxiv.org/html/2611.33012v1#S4.SS2)、[Table I](https://arxiv.org/html/2611.33012v1#S4.T1)、[§IV-D](https://arxiv.org/html/2611.33012v1#S4.SS4)、[Table II](https://arxiv.org/html/2611.33012v1#S4.T2)、[§IV-E](https://arxiv.org/html/2611.33012v1#S4.SS5)、[§V](https://arxiv.org/html/2611.33012v1#S5)、[§VI](https://arxiv.org/html/2611.33012v1#S6)、[§VII-A](https://arxiv.org/html/2611.33012v1#S7.SS1)、[Table III](https://arxiv.org/html/2611.33012v1#S7.T3)、[Table IV](https://arxiv.org/html/2611.33012v1#S7.T4)、[§VII-B](https://arxiv.org/html/2611.33012v1#S7.SS2)、[§VII-C](https://arxiv.org/html/2611.33012v1#S7.SS3)、[Table V](https://arxiv.org/html/2611.33012v1#S7.T5)、[§VII-D](https://arxiv.org/html/2611.33012v1#S7.SS4)、[Table VI](https://arxiv.org/html/2611.33012v1#S7.T6)、[§VII-E](https://arxiv.org/html/2611.33012v1#S7.SS5)、[Table VII](https://arxiv.org/html/2611.33012v1#S7.T7)、[§VIII](https://arxiv.org/html/2611.33012v1#S8)、[§IX](https://arxiv.org/html/2611.33012v1#S9)、[Code and Data Availability](https://arxiv.org/html/2611.33012v1#Sx2)
- `abstract` — arXiv abstract page, 2611.33012v1：https://arxiv.org/abs/2611.33012v1 （PDF：https://arxiv.org/pdf/2611.33012v1 ；DOI：https://doi.org/10.48550/arXiv.2611.33012）

[Home](../) · [AI Papers](./)
