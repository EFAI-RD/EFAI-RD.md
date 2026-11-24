---
parent: AI Papers
nav_order: 4
title: "VLM 代理自己翻 CT／MRI：第一個假設錯，最後只有 12% 答對"
catalog_id: "arxiv:2611.23480"
editors:
  - "Clare"
refs:
  main:
    title: "Diagnostic Accuracy and Navigation Behavior of Vision-Language Model Agents Reading Emergency CT and MRI Examinations"
    url: "https://arxiv.org/abs/2611.23480"
  pdf:
    title: "Diagnostic Accuracy and Navigation Behavior of Vision-Language Model Agents Reading Emergency CT and MRI Examinations (arXiv PDF v1)"
    url: "https://arxiv.org/pdf/2611.23480v1"
  code:
    title: "RadioAgent (GitHub; URL listed in paper)"
    url: "https://github.com/bastienLeGuellec/radioagent"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# VLM 代理自己翻 CT／MRI：第一個假設錯，最後只有 12% 答對

## 來源

- 團隊：法國 Lille University Hospital（神經放射科、腹部放射科、公共衛生部門）、德國 Charité Berlin、塞內加爾 Cheikh Anta Diop University Hospital、Pasteur Institute of Lille／Inserm／Université de Lille、德國 Technical University Munich Hospital；第一作者 Jonathan Lichtle 與 Aymen Meddeb（共同第一作者），通訊作者 Bastien Le Guellec，共 13 位作者。[(ref: main p.1)](https://arxiv.org/pdf/2611.23480v1#page=1)
- 論文：*Diagnostic Accuracy and Navigation Behavior of Vision-Language Model Agents Reading Emergency CT and MRI Examinations*，arXiv 預印本，2026-11-17 提交（v1），分類 cs.AI，授權 CC BY-NC-SA 4.0。[(ref: main)](https://arxiv.org/abs/2611.23480)
- 識別碼：arXiv [2611.23480](https://arxiv.org/abs/2611.23480)；DOI [10.48550/arXiv.2611.23480](https://doi.org/10.48550/arXiv.2611.23480)。
- 全文：[arXiv PDF v1](https://arxiv.org/pdf/2611.23480v1)（正文 13 頁，含附錄共 25 頁）。
- 程式：論文寫明代理環境與分析程式碼公開於 [GitHub](https://github.com/bastienLeGuellec/radioagent)；執行紀錄、評分與讀者紀錄須向通訊作者申請。本文未核對程式實作。[(ref: main Data Availability)](https://arxiv.org/pdf/2611.23480v1#page=11)
- 研究性質：完整執行的回溯性評估研究（不是 pilot），依 CLAIM 報告；六個 VLM 對 100 例公開教學病例各跑四種條件、每種兩次（4,800 次），另有九位放射科醫師讀其中 30 例，主要比較附病例群集的 GEE 與 bootstrap 95% 信賴區間。病例來自 Radiopaedia 教學圖庫而非臨床實務，答案由 LLM judge 評分。[(ref: main Materials and Methods)](https://arxiv.org/pdf/2611.23480v1#page=2)
- 證據邊界：本文數值以 arXiv v1 PDF 的正文、Table 1 與附錄表格為準；圖中長條只用正文或表格明寫的數字，各模型在四種條件下的完整數值只出現在 Fig 2c 的圖面上，本文未引用。

**編輯：** Clare

讓六個 VLM 代理像放射科醫師一樣逐張翻閱急診 CT 與 MRI，自由瀏覽時的整體準確率只有 32.6%，比一次送入全部切片還低；模型通常在只看了約一成切片時就提出第一個假設並一路守著，第一個假設錯了的執行中，最後答對的只有 12.4%。[(ref: main Abstract)](https://arxiv.org/pdf/2611.23480v1#page=1) [(ref: main First Hypothesis)](https://arxiv.org/pdf/2611.23480v1#page=8)

## 流程

![三個面板的圖。左側 A 標題「One turn of the navigating agent」，四個淺藍底、深藍實線圓角框由上而下以向下箭頭相連：「Receives: current slice + position + result of last command」、「Replies: check / adjust / plan」、「Working hypothesis + confidence (0-100)」、「Command: UP / DOWN / SWITCH series / DIAGNOSIS」；下方小字說明只有最近 3 張切片留在 context，以及四種條件。中間 B 為長條圖，標題「Pooled accuracy, 6 VLMs, 100 cases」，縱軸「Correct primary diagnosis (%)」，六根長條：Free navigation 32.6（深橘）、From key slice 37.9（淺橘）、All slices, one request 42.2（深藍）、Key slices, one request 42.5（淺藍）、Slice labels, no images 17.2（深灰）、Indication only 11.3（淺灰）；下方小字「Source: Table 1 and Table S4」。右側 C 為兩根長條，標題「Free navigation, 1196 runs」，縱軸「Final answer correct (%)」：綠色「First hypothesis right (n=311)」90.4、紅色「First hypothesis wrong (n=885)」12.4。左下角小字「Redrawn by EFAI-RD from Lichtle J, Meddeb A, et al. arXiv:2611.23480v1 (Fig 1, Table 1, Table S4, Fig 4). No case images reproduced.」](assets/vlm-agent-ct-mri-navigation-first-hypothesis.png)

*圖：本書庫依論文 [Fig 1](https://arxiv.org/pdf/2611.23480v1#page=4) 重繪的代理單輪流程（左，四個實線框以箭頭相連）；[Table 1](https://arxiv.org/pdf/2611.23480v1#page=6) 與 [Table S4](https://arxiv.org/pdf/2611.23480v1#page=23) 的四種讀片條件與兩種無影像對照之合併準確率（中，橘色為逐張瀏覽、藍色為一次送入、灰色為無影像）；以及自由瀏覽時第一個假設對或錯之後，最後答案正確的比例（右，綠色與紅色長條；[Fig 4c](https://arxiv.org/pdf/2611.23480v1#page=9)）。圖中不含任何病例影像。*

## 背景／問題

作者指出，VLM 的醫學影像評估幾乎都使用放射科醫師事先挑好的關鍵影像，跳過了實際判讀時「決定去哪裡看」的資訊蒐集過程；放射科醫師在體積資料中搜尋、辨識、修正並決定，這個過程本身也會出錯，例如 premature closure（還沒看到關鍵資訊就定案）與 anchoring（遇到矛盾證據仍不修正早期假設）。[(ref: main Introduction)](https://arxiv.org/pdf/2611.23480v1#page=2)

論文引用的既有工作顯示：在純文字臨床任務中，LLM 自己蒐集資訊時的診斷準確率低於一次給齊資訊，且會受資訊送達順序影響；也已有代理能在檢查中自主瀏覽影像。作者要問的是，VLM 代理在自己翻閱一整個 CT 或 MRI 檢查時，準確率是否受瀏覽方式影響，以及它的瀏覽行為會不會出現類似 premature closure 與 anchoring 的模式。「代理將進入放射科工作流程」是論文引用他人綜述的趨勢判斷，本研究本身並未評估部署情境。[(ref: main Introduction)](https://arxiv.org/pdf/2611.23480v1#page=2)

## 方法摘要

- **病例** — Radiopaedia 於 2025 年 3 月至 2026 年 8 月發布、可能出現在急診的 100 例 CT 與 MRI（73 例 CT、26 例 MRI、1 例 CT 加 DWI；其中 7 例正常），分為腹部 31、神經 30、胸腔 20、肌骨與外傷 19；模型與讀者只看到由病史改寫的一行臨床指示，看不到標題、診斷與討論。參考答案是病例發布時的診斷。[(ref: main Case Selection)](https://arxiv.org/pdf/2611.23480v1#page=2) [(ref: main Results)](https://arxiv.org/pdf/2611.23480v1#page=5)
- **代理環境** — 仿照放射科醫師的檢視器：每一輪代理收到目前切片、位置與上一個指令的結果，回覆 check、adjust、plan、working hypothesis（附 0–100 confidence）與一個指令（上／下一張、切換系列、作答）；只有最近三張切片留在 context。[(ref: main Agent Environment)](https://arxiv.org/pdf/2611.23480v1#page=3)
- **四種讀片條件** — free navigation（自選系列開始）、navigation from the key slice（從最有資訊的關鍵切片開始）、all slices in a single request（中位數 70 張一次送入）、key slices in a single request；每個模型每例每條件跑兩次。另有兩種無影像對照：只有切片標籤沒有影像、只有臨床指示。[(ref: main Reading Conditions)](https://arxiv.org/pdf/2611.23480v1#page=4)
- **模型** — 依 2026-08-25 的 LMArena 排名、在每百萬輸出 token 低於 2 美元的模型中，從六家開發者各選一個：Gemini 3.7 Flash、GPT-5.6 Luna、GLM-5.3 Flash、Qwen 3.7 Flash、MiniMax M3、MiMo v2.5。[(ref: main Models)](https://arxiv.org/pdf/2611.23480v1#page=3)
- **對照讀者與評分** — 九位放射科醫師以同一檢視器讀其中 30 例；所有答案由未參與受測的 Claude Sonnet 5 作為 LLM judge，判定主要診斷是否正確。[(ref: main Radiologist Readers)](https://arxiv.org/pdf/2611.23480v1#page=2) [(ref: main Grading of Answers)](https://arxiv.org/pdf/2611.23480v1#page=4)

## 方法詳解

- **病例篩選與關鍵切片** — 依系統與模態篩選 Radiopaedia 病例、不下關鍵字；一位住院醫師與一位放射科醫師（3 與 4 年經驗）選出急診可能遇到的病例並標出關鍵切片與最具資訊的一張，再由第三位放射科醫師（7 年）複核。參考診斷的確定度：certain 65 例、almost certain 30 例、probable 5 例。顯示視窗沿用病例作者的設定，讀者與模型都不能調整。[(ref: main Case Selection)](https://arxiv.org/pdf/2611.23480v1#page=2) [(ref: main Appendix S1)](https://arxiv.org/pdf/2611.23480v1#page=14)
- **放射科醫師讀者** — 來自四個機構的三位資深住院醫師與六位專科醫師（經驗中位數 7 年，3–10 年），使用顯示相同影像、視窗與臨床指示、允許相同逐張移動與切換系列的網頁檢視器，所有動作都有紀錄；行為分析只計到第一次儲存診斷為止。讀者沒有參與病例挑選、關鍵切片標註或評分。[(ref: main Radiologist Readers)](https://arxiv.org/pdf/2611.23480v1#page=2)
- **執行設定** — 全部透過 OpenRouter API、temperature 0、使用供應商預設的 reasoning 設定，隱藏的 reasoning token 不讀取。影像為 JPEG 品質 85、長邊最多 512 像素；一次送入時最多 400 張（Qwen 3.7 Flash 為 100 張），更大的檢查以等間距抽樣（9 次）。瀏覽步數上限為總切片數的 1.2 倍，到達上限的 297 次執行被要求直接作答；讓它們繼續到三倍切片數，準確率沒有改變。[(ref: main Agent Environment)](https://arxiv.org/pdf/2611.23480v1#page=3) [(ref: main Table A2.1)](https://arxiv.org/pdf/2611.23480v1#page=14) [(ref: main Table A2.3)](https://arxiv.org/pdf/2611.23480v1#page=15)
- **完整 prompt 與工具定義** — 瀏覽用 system prompt、JSON 回覆格式、tool schema、一次送入的 prompt、judge 與假設分段的 prompt，都在附錄 S2 逐字列出。[(ref: main Appendix S2)](https://arxiv.org/pdf/2611.23480v1#page=14)
- **評分** — judge 以「治療醫師會不會因此採取相同處置、是否為同一病理生理過程」判定主要診斷 correct／partial／incorrect，partial 計為錯；鑑別診斷不給分。在兩位放射科醫師獨立評分（分歧以共識解決）的 500 次執行上，judge 與共識的一致性（κ = 0.83）與單一放射科醫師相當（κ = 0.84、0.83），且優於另外三個候選 judge。放射科醫師讀者的答案另由兩位不知讀者身分的放射科醫師評分作為敏感度分析。[(ref: main Grading of Answers)](https://arxiv.org/pdf/2611.23480v1#page=4) [(ref: main S2.5)](https://arxiv.org/pdf/2611.23480v1#page=18)
- **行為指標** — 每次瀏覽記錄看過的切片比例、動作數、每看一張切片的動作數（不回頭為 1）、是否顯示過關鍵切片，以及關鍵切片的 dwell ratio（均勻掃過為 1）。Claude Sonnet 5 把每次執行的 working hypothesis 序列切成不同診斷段落，判定第一個假設與最後答案是否相同；在 100 次由兩位放射科醫師獨立切分的執行上，「第一個假設是否保留」的一致性 κ 為 0.67 與 0.78，兩位醫師之間為 0.63。[(ref: main Behavioral Measures)](https://arxiv.org/pdf/2611.23480v1#page=4)
- **統計** — 以執行為分析單位、同一病例的執行視為相關；條件比較用依病例群集、調整模型的 logistic GEE（omnibus Wald test 後 Holm 校正兩兩比較），95% CI 以病例（與放射科醫師比較時加上讀者）重抽 10,000 次 bootstrap。條件比較是主要分析，其餘為探索性分析。沒有可用答案的 18 次執行（供應商內容過濾）計為錯。[(ref: main Statistical Analysis)](https://arxiv.org/pdf/2611.23480v1#page=5)
- **論文未交代** — 另外三個候選 judge 的名稱與各自一致性、500 次評分樣本如何在 24 個模型×條件組合間分配，正文只寫「跨組合抽樣」。
- **論文未交代** — 每個模型實際使用的 reasoning 設定與隱藏 reasoning 長度；論文只寫「供應商預設」，不同模型之間可能差很多。
- **論文未交代** — 兩種無影像對照每例只跑一次、且在 2026 年 10 月執行，晚於主實驗的 8–9 月；正文未說明這個時間差是否影響比較。

## 資料與實驗

### 資料

| 項目 | 內容 | 規模 |
|---|---|---|
| 病例來源 | Radiopaedia 公開教學病例（2025-03 至 2026-08 發布） | 100 例：腹部 31、神經 30、胸腔 20、肌骨與外傷 19 |
| 模態 | CT 73、MRI 26、CT＋DWI 1；7 例正常 | 一次送入時每例中位數 70 張切片 |
| 參考診斷 | 病例發布時的診斷 | certain 65、almost certain 30、probable 5 |
| 模型執行 | 6 個 VLM × 100 例 × 4 條件 × 2 次 | 4,800 次；另有無影像對照 2 × 600 次 |
| 放射科醫師 | 9 位（3 位資深住院醫師、6 位專科醫師）讀 30 例 | 270 次判讀 |

[(ref: main Case Selection)](https://arxiv.org/pdf/2611.23480v1#page=2) [(ref: main Results)](https://arxiv.org/pdf/2611.23480v1#page=5) [(ref: main Table S4)](https://arxiv.org/pdf/2611.23480v1#page=23)

### 實驗：各讀片條件的準確率（Table 1）

| 讀片條件 | 正確數／總數 | 準確率 %（95% CI） | 比較（95% CI） | P |
|---|---|---|---|---|
| **全部 100 例，六個模型（每例兩次）** | | | | |
| Free navigation | 391/1200 | 32.6（26.7–38.8） | 參考 | — |
| Navigation from the key slice | 455/1200 | 37.9（31.8–44.4） | OR 1.27（1.11–1.46） | .003 |
| All slices, single request | 506/1200 | 42.2（35.7–48.8） | OR 1.52（1.34–1.73） | <.001 |
| Key slices, single request | 510/1200 | 42.5（36.2–48.9） | OR 1.54（1.29–1.85） | <.001 |
| **無影像對照，全部 100 例（每例一次）** | | | | |
| Slice labels, no images | 103/600 | 17.2（12.0–22.5） | OR 0.28（0.20–0.38）* | <.001 |
| Clinical indication only | 68/600 | 11.3（7.2–15.7） | OR 0.17（0.11–0.25）* | <.001 |
| **放射科醫師讀過的 30 例** | | | | |
| Radiologists | 208/270 | 77.0（65.9–87.0） | 參考 | — |
| Radiologists, graded by two radiologists | 223/270 | 82.6（71.1–91.9） | — | — |
| Free navigation | 108/360 | 30.0（19.2–41.1） | −47.0 點（−60.2 至 −33.9） | <.001 |
| Navigation from the key slice | 124/360 | 34.4（22.2–46.9） | −42.6 點（−55.7 至 −29.7） | <.001 |
| All slices, single request | 145/360 | 40.3（29.2–51.9） | −36.8 點（−48.8 至 −24.9） | <.001 |
| Key slices, single request | 163/360 | 45.3（33.6–57.2） | −31.8 點（−44.3 至 −18.8） | <.001 |

OR 相對於 free navigation（* 相對於 all slices, single request），來自依病例群集、調整模型的 logistic GEE，主要條件的 P 經 Holm 校正；與放射科醫師的差為百分點，P 來自 bootstrap。[(ref: main Table 1)](https://arxiv.org/pdf/2611.23480v1#page=6)

### 實驗：各模型有無瀏覽與無影像的準確率（Table S4，%）

| 模型 | Free navigation | All slices, single request | Slice labels, no images | Indication only |
|---|---|---|---|---|
| Gemini 3.7 Flash | 44.0 | 52.5 | 27.0 | 22.0 |
| GLM-5.3 Flash | 38.5 | 52.5 | 13.0 | 3.0 |
| Qwen 3.7 Flash | 34.5 | 34.5 | 16.0 | 17.0 |
| GPT-5.6 Luna | 30.5 | 41.5 | 9.0 | 6.0 |
| MiniMax M3 | 22.0 | 38.5 | 22.0 | 15.0 |
| MiMo v2.5 | 26.0 | 33.5 | 16.0 | 5.0 |

[(ref: main Table S4)](https://arxiv.org/pdf/2611.23480v1#page=23)

## 結果

- **自由瀏覽最差** — 合併六個模型，free navigation 32.6%、從關鍵切片開始 37.9%、一次送入全部切片 42.2%、只送關鍵切片 42.5%；從關鍵切片開始仍低於兩種一次送入（Holm P = .01 與 .03），兩種一次送入之間沒有差異（P = .86）。free navigation 在六個模型中有四個最差、一個並列最差，四個解剖領域的差距相近（P = .93）。在晚於最新已公布知識截止日之後發布的 34 例上，free navigation 仍最差（30.4% 對 41.9%）。[(ref: main Diagnostic Accuracy)](https://arxiv.org/pdf/2611.23480v1#page=5)
- **與放射科醫師差距大** — 在 30 例上，自由瀏覽的模型答對 30.0%，九位放射科醫師（同一 judge 評分）77.0%（P < .001）；四種條件都比放射科醫師低 31.8–42.6 個百分點。改由兩位放射科醫師評分時，放射科醫師為 82.6%；放射科醫師彼此的一致性為 Fleiss κ 0.22。[(ref: main Comparison with Radiologists)](https://arxiv.org/pdf/2611.23480v1#page=7) [(ref: main Comparison with Radiologists, cont.)](https://arxiv.org/pdf/2611.23480v1#page=8)
- **沒有影像也答對不少** — 只給切片標籤、不給影像時仍有 17.2% 正確，只給臨床指示時 11.3%；只給標籤的 600 個答案中，只有 5.5% 指出影像缺失。在沒有任何模型能不靠影像答對的 54 例上，自由瀏覽只答對 18.2%，其餘病例為 49.5%。[(ref: main No-Image Control)](https://arxiv.org/pdf/2611.23480v1#page=7) [(ref: main Table S4)](https://arxiv.org/pdf/2611.23480v1#page=23)
- **找得到關鍵切片，但沒看懂** — 95.7% 的自由瀏覽執行在作答前顯示過關鍵切片，答錯的執行中也有 95.3%；與放射科醫師在共同病例上的比例相當（98.1% 對 99.3%）。差別在停留：放射科醫師在關鍵切片上的 dwell ratio 中位數 1.27，模型 1.00（均勻掃過）。答錯但有指出異常的答案中，54.5% 把異常放在正確器官；不給影像時降到 39.9%。[(ref: main Exploration Patterns)](https://arxiv.org/pdf/2611.23480v1#page=8) [(ref: main Error Analysis)](https://arxiv.org/pdf/2611.23480v1#page=7)
- **瀏覽範圍** — 放射科醫師看過切片的中位數 77.9%；Gemini 3.7 Flash 較早停止（43.5%），其餘五個模型中位數看完 100%，且每個系列只單向掃一次（每看一張切片 1.00 個動作，放射科醫師 1.81）。[(ref: main Exploration Patterns)](https://arxiv.org/pdf/2611.23480v1#page=8)
- **第一個假設很早出現，而且很少改** — Gemini 以外的五個模型雖然最後看了中位數 98.1% 的切片，第一個假設在中位數 10.8% 的切片時就出現（各模型 7.8–16.7%）；在 1,196 次自由瀏覽中，第一個假設正確的只有 26.0%，卻有 63.1% 的執行把它當成最後答案。第一個假設對時最後答對 90.4%，錯時只有 12.4%（OR 29.0，17.6–47.7）；錯誤假設被保留的比例為 55.8%。[(ref: main First Hypothesis)](https://arxiv.org/pdf/2611.23480v1#page=8) [(ref: main First Hypothesis, cont.)](https://arxiv.org/pdf/2611.23480v1#page=9)
- **從關鍵切片開始，假設更早也更難改** — 第一個假設提前到中位數 3.2% 的切片，正確率 37.5%（對 26.0%），保留率 73.0%（對 63.1%）；錯誤假設的修正率表面上從 12.4% 降到 6.3%，但在兩種條件都先錯的 392 個模型×病例配對中沒有差異（5.3% 對 5.9%，P = .64）。把所有影像都留在 context，準確率（28.9% 對 30.0%）與假設保留率都沒有改變。[(ref: main First Hypothesis)](https://arxiv.org/pdf/2611.23480v1#page=9) [(ref: main Table S6)](https://arxiv.org/pdf/2611.23480v1#page=24)
- **信心與正確性脫鉤** — 最後答案的自述 confidence 中位數 90%，但只有 38.9% 正確；正確與錯誤答案的 confidence 幾乎相同（AUROC 0.59），Brier score 0.453，比固定給整體準確率的常數（0.238）還差，且每個模型、每個條件都如此。提出第一個假設後 confidence 不論對錯都上升，錯時從 35.6% 升到 85.1%，對時從 42.3% 升到 89.3%。[(ref: main Confidence)](https://arxiv.org/pdf/2611.23480v1#page=10)

## 限制

作者自述：

- 100 例來自線上教學圖庫而非臨床實務；部分病例早於三個有公布知識截止日之模型的截止日，但截止日前後發布的病例準確率沒有差異。[(ref: main Discussion)](https://arxiv.org/pdf/2611.23480v1#page=11)
- 受測模型在 benchmark 上有競爭力，但數千次多步執行的成本使作者無法測試各家最大的版本。[(ref: main Discussion)](https://arxiv.org/pdf/2611.23480v1#page=11)
- 一次送入全部切片同時移除了瀏覽、也改變了輸入並拿掉搜尋與停止的決策；只改起點的「從關鍵切片開始」只能分離出瀏覽效果的一部分。[(ref: main Discussion)](https://arxiv.org/pdf/2611.23480v1#page=11)
- 代理每一輪都必須寫出 working hypothesis，而它會留在 context 中，這個設計本身可能促成提早定案；且只評分主要診斷，不評鑑別診斷。[(ref: main Discussion)](https://arxiv.org/pdf/2611.23480v1#page=11)

本書庫另外注意到：

- **judge 與分段都靠同一個 LLM** — 正確性、錯誤位置與「第一個假設是否保留」都由 Claude Sonnet 5 判定；與放射科醫師的一致性在正確性上相當高（κ 0.83），在假設保留上則是 κ 0.67–0.78，「首個假設保留率」這類行為數字的不確定性比準確率大。
- **放射科醫師彼此一致性只有 fair** — Fleiss κ 0.22，作者把放射科醫師的準確率當成對照基準，但同一病例上醫師之間也常給出不同主要診斷。
- **低價模型與預設 reasoning** — 受測的是每百萬輸出 token 低於 2 美元的版本、使用預設 reasoning；結果不能直接外推到各家旗艦模型或刻意調高推理強度的設定。
- **尚未經同儕審查** — 目前為 arXiv v1 預印本；執行紀錄需向作者申請才能取得。

## 與書庫其他文章的關係

CT 標頭研究發現資訊在模型作答後才送到時，後到的來源常推翻原本判斷；本篇在多輪瀏覽中看到幾乎相反的現象：模型很早寫下的第一個假設，在之後看到更多切片時多半不會被推翻，兩篇一起提醒「證據送達順序」在多輪 VLM 流程中的影響方向取決於設計: [CT 品管 VLM：同一個錯誤標頭，晚一輪送到就推翻正確判斷](2026-11-19-ct-dicom-header-order-vlm-qc.md)

轉診文字研究固定 MRI、逐級改寫轉診文字，量到答案主要隨文字改變；本篇以只給切片標籤或只給臨床指示的無影像對照，量到六個 VLM 不看影像也能答對 11–17% 的急診病例，且多數不會指出影像缺失: [轉診單一句話就改變 MRI 判讀，叫模型忽略只有一個做得到](2026-10-28-referral-text-overrides-mri-mllm-glioma-abscess.md)

本篇量到 VLM 代理很早寫下的第一個假設多半不會被推翻；臨床 LLM 安全綜述則把這類「一旦對答案有信心，後續自我反思就難以修正」的現象（Degeneration of Thought）列為代理錯誤級聯的成因之一，並主張要靠外部可驗證的檢查打斷，而不是由同一個模型自我反思: [臨床 LLM 安全綜述：符號否決層數字亮眼，多來自單一小型研究](2026-11-24-verifiable-logic-neuro-symbolic-review.md)

## 實務的啟發

- **評估影像代理時，把「自己找影像」納入測試** — 本研究中只改變起點（自由瀏覽或從關鍵切片開始）就讓合併準確率從 32.6% 變成 37.9%，而一次送入挑好的關鍵切片又更高；用預選關鍵影像得到的分數，不能直接代表代理在整個檢查中自己瀏覽時的表現。作者的四種條件加兩種無影像對照，是可借用的量測設計。
- **追蹤假設軌跡，而不只看最後答案** — 第一個假設對錯幾乎決定了最後結果（90.4% 對 12.4%），而 95% 以上的執行其實都看過關鍵切片；若要改善，記錄每一輪的 working hypothesis 與修正次數，比只看最終準確率更能看出問題在「沒找到」還是「看到了卻沒改」。
- **不要把 VLM 自述的 confidence 當成可靠度** — 本研究中 confidence 中位數 90% 對應 38.9% 的正確率，且 Brier score 比常數猜測還差；在自己的資料上驗證之前，自述信心不宜用來決定是否需要人工複核。這些是在 100 例教學病例、六個低價模型上看到的警訊，不是已證實的普遍性質。

## References

- `main` — Lichtle J, Meddeb A, Birot A, et al. *Diagnostic Accuracy and Navigation Behavior of Vision-Language Model Agents Reading Emergency CT and MRI Examinations*. arXiv:2611.23480v1, 2026. [https://arxiv.org/abs/2611.23480](https://arxiv.org/abs/2611.23480)
  - 深鏈：[Abstract](https://arxiv.org/pdf/2611.23480v1#page=1)、[Introduction／Case Selection](https://arxiv.org/pdf/2611.23480v1#page=2)、[Models／Agent Environment](https://arxiv.org/pdf/2611.23480v1#page=3)、[Fig 1／Reading Conditions／Grading](https://arxiv.org/pdf/2611.23480v1#page=4)、[Statistical Analysis／Results](https://arxiv.org/pdf/2611.23480v1#page=5)、[Table 1](https://arxiv.org/pdf/2611.23480v1#page=6)、[No-Image Control／Error Analysis](https://arxiv.org/pdf/2611.23480v1#page=7)、[Exploration Patterns](https://arxiv.org/pdf/2611.23480v1#page=8)、[Fig 4](https://arxiv.org/pdf/2611.23480v1#page=9)、[Confidence／Discussion](https://arxiv.org/pdf/2611.23480v1#page=10)、[Limitations／Data Availability](https://arxiv.org/pdf/2611.23480v1#page=11)、[Appendix S1–S2](https://arxiv.org/pdf/2611.23480v1#page=14)、[Table A2.3](https://arxiv.org/pdf/2611.23480v1#page=15)、[S2.5](https://arxiv.org/pdf/2611.23480v1#page=18)、[Table S2–S4](https://arxiv.org/pdf/2611.23480v1#page=23)、[Table S5–S6](https://arxiv.org/pdf/2611.23480v1#page=24)
- `pdf` — arXiv PDF v1 全文. [https://arxiv.org/pdf/2611.23480v1](https://arxiv.org/pdf/2611.23480v1)
- `code` — RadioAgent（論文所列代理環境與分析程式碼網址）. [https://github.com/bastienLeGuellec/radioagent](https://github.com/bastienLeGuellec/radioagent)

[Home](../) · [AI Papers](./)
