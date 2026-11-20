---
parent: AI Papers
nav_order: 3
title: "CT 品管 VLM：同一個錯誤標頭，晚一輪送到就推翻正確判斷"
catalog_id: "arxiv:2611.18790"
editors:
  - "Clare"
refs:
  main:
    title: "Same Evidence, Different Verdicts: Delivery of CT Images and DICOM Metadata Changes VLM Quality-Control Decisions"
    url: "https://arxiv.org/abs/2611.18790"
  html:
    title: "Same Evidence, Different Verdicts (arXiv HTML v1)"
    url: "https://arxiv.org/html/2611.18790v1"
  code:
    title: "ct-vlm-delivery-order (GitHub; URL listed in paper)"
    url: "https://github.com/nav92061/ct-vlm-delivery-order"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# CT 品管 VLM：同一個錯誤標頭，晚一輪送到就推翻正確判斷

## 來源

- 團隊：University of Georgia School of Computing；單一作者 Nicolas Avelar。[(ref: main author block)](https://arxiv.org/html/2611.18790v1)
- 論文：*Same Evidence, Different Verdicts: Delivery of CT Images and DICOM Metadata Changes VLM Quality-Control Decisions*，arXiv 預印本，2026-11-13 提交（v1），分類 cs.CV；arXiv 註記為投稿 IEEE ISBI 2027，尚非已接受版本。[(ref: main)](https://arxiv.org/abs/2611.18790)
- 識別碼：arXiv [2611.18790](https://arxiv.org/abs/2611.18790)；DOI [10.48550/arXiv.2611.18790](https://doi.org/10.48550/arXiv.2611.18790)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.18790v1)（4 頁短文，2 張圖、1 張表）。
- 程式：論文寫明程式碼、prompt 與全部呼叫紀錄公開於 [GitHub](https://github.com/nav92061/ct-vlm-delivery-order)；本文未核對程式實作。[(ref: main Abstract)](https://arxiv.org/html/2611.18790v1)
- 研究性質：完整執行的評估研究（不是 pilot），九個 VLM 實際呼叫，主要比較附病人層級群集 bootstrap 95% 信賴區間；但只有 60 位病人、每個系列只看一張冠狀切面，標頭是合成的一行摘要。論文致謝寫明評估與分析程式碼、文字初稿由生成式 AI 助理（Claude）在作者指示下產生，作者審閱並負責全部內容。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2) [(ref: main §6)](https://arxiv.org/html/2611.18790v1#S6)
- 證據邊界：本文數值以 arXiv v1 的 Table 1 與正文為準；Fig. 1 右側與 Fig. 2 的長條只引用正文或 Table 1 明寫的數字。

**編輯：** Clare

同一組 CT 影像、同一個謊稱「系列完整」的 DICOM 標頭，與影像一起送進 prompt 時，Claude Haiku 5.5 只放行 2% 它已從影像抓到的缺陷；等模型先作答、標頭在第二輪才送到，放行率升到 91%，而且反過來也成立：哪個來源後到，模型就聽哪個。[(ref: main Abstract)](https://arxiv.org/html/2611.18790v1) [(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3)

## 流程

![左右兩部分的圖。左側標題「Four ways to deliver the same evidence」，下方四個淺藍底、深藍實線圓角框由上而下排列：「A. Image only：Coronal CT render of series A and B -> ADMIT / REFUSE」、「B. Image + false header, one prompt：Header says the pair is complete」、「C. Image first, false header in turn 2：Turn 1 = model's own refusal; turn 2 = header + 'Give your final decision'」、「D. Image + false header + warning, one prompt：'...if the image and the header disagree, trust the image'」；左下角小字「Redrawn by EFAI-RD from Avelar N. arXiv:2611.18790v1 (Fig. 1; Sec. 2)」。右側為分組長條圖，標題「False 'complete' header, aligned view (60 patients)」，縱軸「Detected defects then admitted (%)」，橫軸三個模型 Nemotron-3.5-VL、Claude Haiku 5.5、Claude Sonnet 5.5，每個模型三根長條：灰色「B. Together (one prompt)」43、2、0；橘色「C. After (turn 2)」100、91、21；綠色「C + warning sentence (turn 2)」1、1、0。底部小字「Source: Table 1 (rows A). Share of defects each model refused from the image alone that it admitted after the false header. Lower is better.」](assets/ct-dicom-header-order-vlm-qc.png)

*圖：本書庫依論文 Fig. 1 與 §2 重繪的四種送達方式（左），以及 [Table 1](https://arxiv.org/html/2611.18790v1#S2.T1) aligned view 列中，三個模型在「模型已從影像拒收的缺陷」上，因錯誤標頭而改為放行的比例（右）。*

## 背景／問題

肺癌篩檢會比較不同年度的低劑量 CT，以體積追蹤結節成長；這個比較假設每個系列都涵蓋它宣稱的解剖範圍。若系列在傳輸中被截斷、卻被當作完整系列放進追蹤，量測就會被悄悄帶偏。[(ref: main §1)](https://arxiv.org/html/2611.18790v1#S1)

作者的前提是：VLM 正被提議用來自動檢查臨床影像輸入，而檢查的時候，影像本身與 DICOM 標頭可能互相矛盾（例如標頭摘要來自計畫的掃描範圍，或在切片遺失、系列重新連結後沒有更新）。論文引用的既有工作多是 VLM 在 CT 影像品質評估與「視覺證據損壞」情境下的評估，而非 VLM 已在臨床擔任輸入檢查的部署證據，因此「VLM 被用作輸入檢查」應讀成作者設定的使用情境。[(ref: main §1)](https://arxiv.org/html/2611.18790v1#S1)

作者刻意不主張 VLM 適合做系列涵蓋範圍檢查：一個不需學習的像素規則就能做到 AUC 0.98–0.99。選涵蓋範圍當測試平台，是因為它的正確答案可以直接從掃描幾何算出來，每一個錯誤都沒有爭議；作者要問的是更一般的問題：模型看到的影像與 metadata 說法不一致時，它相信哪一個，以及答案會不會隨送達順序改變。[(ref: main §1)](https://arxiv.org/html/2611.18790v1#S1)

## 方法摘要

- **測試平台** — 從 NLST 取 60 對同一檢查的兩個重建系列，對系列 B 做截斷、內部缺口、z 位移三種缺陷，加上原始乾淨對，共 240 例；正確答案由每張切片的 Image Position (Patient) 算出。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **輸入** — 每個系列取中間冠狀切面，以 aligned（共用 z 軸、缺資料處為黑）或 native（各自依切片順序排列、只標自己的 z 值）兩種方式繪製；模型依明寫的規則回答一行 ADMIT／REFUSE 與理由。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **送達條件** — 只有標頭、只有影像、影像加正確標頭、影像加矛盾標頭（同一 prompt）；兩輪條件中，第一輪是模型自己的影像判斷，第二輪才送標頭；另有先送標頭、後送影像的反向順序。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **對照與緩解** — 只說「Please confirm」的中性追問、只有結論不含數值的標頭、以工具結果而非使用者訊息送達的標頭，以及一句「標頭可能錯，不一致時相信影像」的警告。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2) [(ref: main Table 1)](https://arxiv.org/html/2611.18790v1#S2.T1)
- **模型** — 九個 VLM：Llama-3.2-11B／90B-Vision、Gemma-4-31B、Nemotron-3.5-VL-120B、Muse-Glimmer-30B、MedGemma-1.5-4B、Qwen3-VL-8B、Claude Haiku 5.5、Claude Sonnet 5.5。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)

## 方法詳解

- **配對篩選** — 262 對 NLST 同檢查重建配對（NCI Imaging Data Commons，CC BY 4.0）中，取同一 frame of reference、z 範圍相同、切片厚度相同且 ≤ 2.5 mm 的 60 對，依廠牌分層（GE 24、Toshiba 19、Siemens 14、Philips 3）。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **缺陷幅度** — 截斷移除一端 10–35% 切片；內部缺口 5–20%；等長 z 位移 5–20%（A 與 B 各在不同端少切片，切片數相同但範圍錯開）。幅度逐對抽樣、seed 固定。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **矛盾標頭** — 缺陷例的錯誤標頭說「配對完整」；乾淨例的錯誤標頭說「有截斷」。標頭是管線從張數或範圍欄位推出的一行摘要，這類欄位可能過時。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **解碼設定** — NVIDIA API 上的五個模型 temperature 0；MedGemma 與 Qwen3-VL 開放權重、greedy、單張 A10G；兩個 Claude 模型不接受 temperature 設定，用預設取樣、每例一次（Haiku 關閉 extended thinking，Sonnet 用 low effort）。同一 prompt 中，Claude 的影像在文字之前，NVIDIA 模型則在文字之後。因解碼不同，比較只在同一模型內進行。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **指標** — SFR（silent failure rate，缺陷例被放行的比例）與 FRR（false refusal rate，可接受例被拒收的比例）分開報告，附 2,000 次病人群集 bootstrap 95% 信賴區間；Youden's J = 1 − SFR − FRR。順序比較只用「模型只看影像時已拒收、且兩種順序都解析得到答案」的缺陷，報告配對差的群集信賴區間。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **哪些模型進入順序分析** — 只用影像判斷能區分缺陷的 Nemotron、Gemma、Haiku、Sonnet。Gemma 的兩輪條件與 Llama-90B 的 native 條件因 API 吞吐量只跑了 15 位病人。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **事先寫定的協定** — 各條件使用相同的凍結 prompt、解析器與分析，每個條件的協定在第一次執行前寫定；像素規則的 3% 閾值也在執行前固定。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **真實不一致** — 另取主實驗沒用到、標頭算出 z-IoU < 0.95 的全部 24 對 NLST 配對（1 − IoU 中位數 0.13），不做任何編輯，跑只有影像、錯誤標頭（同一 prompt 與兩輪）、警告三種條件。[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2)
- **論文未交代** — 標頭摘要與「Bare」「Tool」條件的完整字串、送入模型的影像解析度與 z 標籤繪製細節；正文只描述格式並引用片段，作者表示完整 prompt 在程式庫中。
- **論文未交代** — Table 1 中 Bare、Tool、Hdr 1st 與 native 列多數比例的信賴區間；正文只對 aligned 主比較給出區間。
- **論文未交代** — 「原始標頭欄位」只在一個模型上測試，正文未寫是哪個模型與結果。

## 資料與實驗

### 資料

| 資料 | 用途 | 規模 | 正確答案 |
|---|---|---|---|
| NLST 同檢查重建配對（NCI Imaging Data Commons） | 合成測試平台 | 60 對（60 位病人）× 乾淨＋3 種缺陷 = 240 例，各有 aligned 與 native 兩種繪製 | 由每張切片位置算出的幾何涵蓋範圍 |
| NLST 真實不一致配對 | 外部檢查 | 24 對未編輯配對（1 − z-IoU 中位數 0.13） | 同上 |

[(ref: main §2)](https://arxiv.org/html/2611.18790v1#S2) [(ref: main §1)](https://arxiv.org/html/2611.18790v1#S1)

### 實驗：送達方式與放行率（Table 1）

數值為「模型只看影像時已偵測到的缺陷，在錯誤『完整』標頭之下改為放行」的百分比；FRR 為只看影像時的錯誤拒收率；Hdr 1st 為先只送錯誤標頭、第二輪才送影像時，影像推翻標頭所造成錯誤答案的比例。A／N = aligned／native。

| 模型 | 繪製 | FRR | Tog. | After | +Warn | Bare | Tool | Hdr 1st |
|---|---|---|---|---|---|---|---|---|
| Nemotron | A | 17 | 43 | 100 | 1 | 44 | 61 | – |
| | N | 4 | 97 | 100 | 0 | 30 | 99 | – |
| Haiku | A | 55 | 2 | 91 | 1 | 1 | 52 | 100 |
| | N | 38 | 35 | 99 | 9 | 5 | 96 | 99 |
| Sonnet | A | 33 | 0 | 21 | 0 | 0 | 71 | 98 |
| | N | 2 | 1 | 74 | 0 | 1 | 97 | 100 |

Tog.：標頭與影像同一 prompt；After：標頭在模型作答後送到；+Warn：After 加警告句；Bare：只有結論、不含數值的宣稱；Tool：標頭以工具結果送到。[(ref: main Table 1)](https://arxiv.org/html/2611.18790v1#S2.T1)

## 結果

- **同樣的證據，順序不同就不同判決** — aligned 繪製下，Haiku 在同一 prompt 中只放行 2%（95% CI 1–4）已偵測的缺陷，標頭晚一輪送到時為 91%（86–95），配對差 +88 個百分點（83–93）；Nemotron 43% 對 100%（+57，53–62）；Sonnet 0/178 對 21%（16–26）；Gemma 11% 對 64%（15 位病人）。只取乾淨配對已被正確放行的缺陷，模式相同。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3) [(ref: main Fig. 2)](https://arxiv.org/html/2611.18790v1#S2.F2)
- **雙向成立：後到的來源勝出** — 模型作答後，錯誤的「有截斷」標頭推翻了所有正確放行的乾淨配對（Nemotron 92/92、Haiku 64/64、Sonnet 99/99），正確標頭也幾乎推翻所有錯誤拒收（11/11、56/56、20/21）。順序反過來時，影像推翻了錯誤標頭造成之錯誤答案的 98–100%。同一 prompt 中，錯誤的「有截斷」標頭則讓三個模型拒收全部 120 個乾淨視圖：兩者同時在場時，只要任一方反對就拒收。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3)
- **不是一般的「被追問就改口」** — 中性的「Please confirm」在 1,072 個正確拒收中推翻 0 個，在 253 個正確放行中推翻 2 個；不含數值的「The pair is complete」很少推翻 Claude 的偵測，作者據此認為效果來自標頭裡的數值。標頭改以工具結果送到時，推翻率仍有 52–99%。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3) [(ref: main Table 1)](https://arxiv.org/html/2611.18790v1#S2.T1)
- **一句警告大幅降低，但有代價** — 「影像與標頭不一致時相信影像」讓同一 prompt 的推翻降到 ≤ 2%（Nemotron、Haiku、Sonnet；Gemma 5–8%），第二輪推翻降到 ≤ 9%；代價是標頭正確時錯誤拒收上升（Nemotron 0% → 12%），而且沒能阻止 Haiku 在乾淨配對上跟隨錯誤的「有截斷」標頭（95–96%）。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3)
- **只看影像的能力差異很大** — Nemotron、Gemma、Haiku、Sonnet 的 SFR ≤ 8%；Llama-3.2-11B 與 MedGemma-1.5 幾乎無法區分（SFR ≥ 96%）；Muse-Glimmer-30B 與 Qwen3-VL-8B 幾乎拒收所有可接受配對。即使在進入順序分析的模型中，Haiku aligned 的 FRR 也有 55%、Sonnet 33%。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3) [(ref: main Table 1)](https://arxiv.org/html/2611.18790v1#S2.T1)
- **真實不一致配對上模式相同** — 24 對未編輯配對中，aligned 下錯誤標頭在第二輪推翻的比例都高於同一 prompt：Haiku 21/23 對 5/23、Sonnet 10/21 對 0/21、Nemotron 23/23 對 19/23。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3)
- **缺陷在影像上看得到** — 只比較兩個面板資料範圍與強度剖面的像素規則，在 360 個合成缺陷視圖中漏掉 1 個、48 個真實缺陷視圖中漏掉 0 個（AUC 0.98–0.99）；穩健性檢查讓各比例移動 ≤ 3.3 個百分點。[(ref: main §3)](https://arxiv.org/html/2611.18790v1#S3)

## 限制

作者自述：

- 每個系列只看一張冠狀切面，不是整個體積；native 繪製下的 z 位移只能從 z 標籤推得，因此那一類衝突有一部分是文字對文字。[(ref: main §4)](https://arxiv.org/html/2611.18790v1#S4)
- 標頭是合成的一行摘要，原始欄位只在一個模型上測過；先標頭後影像的順序只測 Claude 模型；沒有 GPT 或 Gemini 模型。[(ref: main §4)](https://arxiv.org/html/2611.18790v1#S4)
- 研究量的是行為，不是機制；結果與「證據取代」相符，但並未驗證其原因。[(ref: main §4)](https://arxiv.org/html/2611.18790v1#S4)

本書庫另外注意到：

- **樣本與取樣** — 60 位病人、部分條件只有 15 位；兩個 Claude 模型使用預設取樣、每例只呼叫一次，同一案例重複呼叫的變異沒有量測。
- **兩組 API 的影像位置不同** — Claude 的影像在文字之前、NVIDIA 模型在文字之後；論文只做模型內比較，因此不能拿表中數字比較不同廠商模型誰比較穩。
- **作者與工具同源** — 論文自述評估程式與文字初稿由 Claude 產生，而 Claude 也是被評估的模型之一；作者表示所有模型使用同一組凍結 prompt 與分析，公開呼叫紀錄可供複核。
- **尚未經同儕審查** — 目前為投稿 ISBI 2027 的 4 頁預印本。

## 與書庫其他文章的關係

轉診文字研究把臨床線索與「忽略文字」指令放進同一 prompt，量到文字能改變 MRI 判讀；本篇則固定影像與錯誤標頭、只改變送達順序，發現同一資訊在模型作答後才送到時推翻率遠高於同時送達，而一句「不一致時相信影像」的警告能把第二輪推翻壓到 9% 以下: [轉診單一句話就改變 MRI 判讀，叫模型忽略只有一個做得到](2026-10-28-referral-text-overrides-mri-mllm-glioma-abscess.md)

皮膚科代理研究指出工具與推理讀同一張影像時工具輸出未必是獨立查核，本篇則補上另一種代理風險：metadata 以工具結果在模型作答後送到時，仍推翻了 52–99% 已正確偵測的缺陷: [先裁切再檢索，兩條路「錯得一樣」：交叉比對只抓得到 29%](2026-11-03-agentic-derm-vlm-fault-coupling.md)

低劑量 CT 品質研究顯示寫成文字的量測值會主導 MLLM 的品質評分，本篇在另一種 CT 輸入檢查（系列涵蓋範圍）上看到文字型 metadata 的影響，而且影響大小取決於它在對話中的送達位置: [低劑量 CT 品質評分：MLLM 讀量測值追平競賽冠軍，卻高估過度平滑影像](2026-11-18-ldct-iqa-measurement-aware-mllm.md)

VLM 代理瀏覽研究讓模型逐張翻閱整個 CT／MRI 檢查，發現很早寫下的第一個假設在之後看到更多切片時多半不被推翻；本篇則在兩輪對話中看到後到的 metadata 推翻原本判斷，兩篇一起顯示多輪 VLM 流程中證據順序的影響方向取決於設計: [VLM 代理自己翻 CT／MRI：第一個假設錯，最後只有 12% 答對](2026-11-19-vlm-agent-ct-mri-navigation-first-hypothesis.md)

## 實務的啟發

- **驗證 VLM 輸入檢查時，照管線實際的送達順序測** — 本研究中只看影像的測試完全看不出問題：模型在同一 prompt 下也多半保守處理，但同樣的標頭在作答後才送到時，Haiku 放行了 91% 已偵測的缺陷。作者提出的四步驗證（只有影像、同一 prompt 的矛盾 metadata、作答後才送到的矛盾 metadata、正確 metadata 與中性追問作對照），是可借用的量測方法。
- **SFR 與 FRR 分開看** — 進入順序分析的模型中，Haiku 只看影像時 aligned 錯誤拒收就有 55%；只報一個準確率或只報漏放率，會掩蓋這種「過度拒收」造成的工作量。
- **能在模型外做的檢查就不要交給模型** — 論文的像素規則與幾何計算就能判斷涵蓋範圍（AUC 0.98–0.99）；若一定要讓 VLM 看 metadata，警告句能壓低推翻率，但本研究也顯示它會提高錯誤拒收、且不能完全阻止錯誤的「有截斷」標頭。這些是待在自己的資料與模型上驗證的警訊，不是已證實的防護。

## References

- `main` — Avelar N. *Same Evidence, Different Verdicts: Delivery of CT Images and DICOM Metadata Changes VLM Quality-Control Decisions*. arXiv:2611.18790v1, 2026. [https://arxiv.org/abs/2611.18790](https://arxiv.org/abs/2611.18790)
  - 深鏈：[Fig. 1](https://arxiv.org/html/2611.18790v1#S0.F1)、[§1](https://arxiv.org/html/2611.18790v1#S1)、[§2](https://arxiv.org/html/2611.18790v1#S2)、[Fig. 2](https://arxiv.org/html/2611.18790v1#S2.F2)、[Table 1](https://arxiv.org/html/2611.18790v1#S2.T1)、[§3](https://arxiv.org/html/2611.18790v1#S3)、[§4](https://arxiv.org/html/2611.18790v1#S4)、[§6](https://arxiv.org/html/2611.18790v1#S6)
- `html` — arXiv HTML v1 全文. [https://arxiv.org/html/2611.18790v1](https://arxiv.org/html/2611.18790v1)
- `code` — ct-vlm-delivery-order（論文所列程式碼、prompt 與呼叫紀錄網址）. [https://github.com/nav92061/ct-vlm-delivery-order](https://github.com/nav92061/ct-vlm-delivery-order)

[Home](../) · [AI Papers](./)
