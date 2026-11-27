---
parent: AI Papers
nav_exclude: true
title: "CT 報告修訂規則庫：有影像證據 CE-F1 多 11.5，只看草稿學不到"
catalog_id: "arxiv:2611.28281"
editors:
  - "Clare"
refs:
  main:
    title: "Learning a Rule Bank to Revise 3D CT Reports with Independent Evidence"
    url: "https://arxiv.org/html/2611.28281v1"
  abs:
    title: "arXiv abstract page: 2611.28281v1"
    url: "https://arxiv.org/abs/2611.28281v1"
status: published
skill_version: "write-ai-paper@3.0"
evidence_reviewed: true
---

[Home](../) · [AI Papers](./)

# CT 報告修訂規則庫：有影像證據 CE-F1 多 11.5，只看草稿學不到

## 來源

- 團隊：Renjie Liang、Mengxian Lyu、Zijian Xu、Boxin Zhao、Yang Yang、Jinqian Pan、Zhengkang Fan、Mei Liu、Yonghui Wu、Jie Xu，University of Florida（Gainesville, FL）。[(ref: main author block)](https://arxiv.org/html/2611.28281v1) [(ref: abstract)](https://arxiv.org/abs/2611.28281v1)
- 論文：*Learning a Rule Bank to Revise 3D CT Reports with Independent Evidence*，arXiv:2611.28281v1（cs.CV；cross-list cs.AI），2026-11-20 提交，目前只有 v1；未註記發表場合；授權為 CC BY 4.0。[(ref: abstract)](https://arxiv.org/abs/2611.28281v1)
- 識別碼：arXiv [2611.28281](https://arxiv.org/abs/2611.28281v1)；DOI [10.48550/arXiv.2611.28281](https://doi.org/10.48550/arXiv.2611.28281)。
- 全文：[arXiv HTML v1](https://arxiv.org/html/2611.28281v1)、[PDF v1](https://arxiv.org/pdf/2611.28281v1)。
- 程式：論文寫明程式公開於 GitHub [`renjie-liang/CT-RuleBank`](https://github.com/renjie-liang/CT-RuleBank)；本文未檢視其內容。資料為公開的 CT-RATE。[(ref: main Abstract)](https://arxiv.org/html/2611.28281v1#abstract1) [(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1)
- 研究性質：方法研究，規則學習與報告修訂都實際執行，不是 pilot 規模；測試集為 1,564 份 CT，附病人層級 bootstrap 95% 信賴區間與五個草稿取樣 seed 的重複。作者明說測試用的 CT-RATE 驗證集在方法開發期間被檢視過（量測定義、編輯操作與新增句措辭都在含該集的探索分析中定案），因此測試結果不是完全未見資料上的評估；逐條編輯的品質由 LLM 依參考報告判讀，沒有放射科醫師逐例審閱。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1) [(ref: main §5)](https://arxiv.org/html/2611.28281v1#S5)
- 證據邊界：本文數值以 arXiv v1 HTML 版的表 1–7、附錄表 8–15 與正文為準；論文圖 3（逐條編輯的參考報告一致性）只引用正文寫出的比例。

**編輯：** Clare

讓 LLM 代理從 3,000 份開發集案例的修訂結果學出一套「什麼影像證據出現時才改哪一句」的可執行規則，SelfCue-KD 的胸部 CT 報告 CE-F1 從 46.2 升到 57.7，已經很強的 NV-Reason-CT 只多 0.9；同一套學習流程若只能用草稿本身的訊號、不給新的影像證據，CE-F1 幾乎沒有變化。[(ref: main Table 1)](https://arxiv.org/html/2611.28281v1#S3.T1) [(ref: main Table 3)](https://arxiv.org/html/2611.28281v1#S4.T3)

## 流程

![左右兩個面板。左側面板標題「(a) 學規則（開發集）與用規則（推論）」：最左欄由上而下三個實線圓角框——灰色「3D 胸部 CT」、淺橘色「Report model SelfCue-KD 或 NV-Reason-CT → 草稿 r0」、淺藍色「Independent evidence ① 3 個分類器機率平均（FlexiCT／HLIP／ASAP 特徵）② TotalSegmentator v2＋HU 量測」；CT 框向下箭頭指向 report model 框，另有一條左側弧形箭頭指向證據框。中欄兩個淺紫色框：上方「Learning agent（gpt-oss-120b）提出候選規則：目標發現、編輯類型、證據值與方向 ↓ 程式搜尋門檻（11 個百分位）並套用到開發集草稿」，下方「Admission（程式）改動 ≥ 20／3,000 份草稿；GREEN 檢查；新增需 CE-F1 上升且對參考標籤 precision ≥ 50% ↓ LLM 醫學合理性審查」，兩框之間向下箭頭，另有一條標「結果回饋下一輪」的弧形箭頭由下方框回到上方框；左欄兩框各有箭頭指向中欄，其中一支標「開發集草稿」。中欄最下方淺綠色框「Rule bank（每個 report model 各一套）SelfCue-KD 30 條；NV-Reason-CT 13 條」，一條標「固定規則庫」的折線箭頭向右再向上指向右欄。右欄由上而下：灰色框「推論輸入：測試集草稿 r0＋證據」、淺橘色框「Editor agent（推論）程式先找出適用的規則，LLM 依規則提出局部編輯，程式檢查後套用；未編輯的句子原樣保留」、白色框「修訂報告 r1＋revision trace（觸發規則與所用證據值）」，以向下箭頭相連。右側面板標題「(b) 規則庫可用的證據來源 vs. CE-F1」，縱軸「CE-F1（18 種異常 macro，CT-RATE 測試 1,564 例）」刻度 40–70，五組直條由左至右為「草稿」「只用草稿訊號學規則」「只用量測」「只用分類器」「兩種證據」，每組左邊橘色為 SelfCue-KD（46.2、46.2、50.9、54.5、57.7），右邊藍色為 NV-Reason-CT（63.0、63.1、63.4、63.8、63.9），每根直條上方標數值。](assets/ct-rulebank-flow-and-evidence-ablation.png)

*圖：本書庫依論文圖 1 與 [§3](https://arxiv.org/html/2611.28281v1#S3) 重繪的流程（左），規則條數取自 [Appendix C.2](https://arxiv.org/html/2611.28281v1#A3.SS2)、admission 條件取自 [Appendix A.2](https://arxiv.org/html/2611.28281v1#A1.SS2) 與 [Appendix B.1](https://arxiv.org/html/2611.28281v1#A2.SS1)；右側數值取自論文表 3，每種證據設定各自重新學一套規則庫。左圖淺紫色兩框是學習階段、淺綠色框是學好的規則庫、右欄淺橘框是推論時的 editor agent；右圖橘色直條為 SelfCue-KD、藍色直條為 NV-Reason-CT。「只用草稿訊號學規則」為通過醫學合理性審查後保留的規則結果。[(ref: main Figure 1)](https://arxiv.org/html/2611.28281v1#S0.F1) [(ref: main Table 3)](https://arxiv.org/html/2611.28281v1#S4.T3)*

## 背景／問題

作者引用先前研究指出，從 3D 胸部 CT 生成報告的視覺語言模型可能漏寫異常，或寫錯依賴精確量測的發現；本研究自己的資料也顯示這一點：SelfCue-KD 草稿在 18 種 CT-RATE 異常上的 macro recall 只有 43.4%（被修訂的報告子集）。[(ref: main §1)](https://arxiv.org/html/2611.28281v1#S1) [(ref: main Table 2)](https://arxiv.org/html/2611.28281v1#S4.T2)

修訂草稿有兩種常見做法，作者各自點出問題：只讓 LLM 讀草稿自行挑錯，並沒有對影像多一次觀察，而引用文獻顯示沒有外部回饋的自我修正並不可靠；把工具得到的影像證據交給 LLM 綜合（論文以 MedScribe 為例），則是把「證據與草稿衝突時聽誰的」留給 LLM 隱性判斷。分類器會判錯、分割會影響量測，同一個量測值對不同病人的診斷意義也不同，所以證據與草稿不一致時不一定該改。[(ref: main §1)](https://arxiv.org/html/2611.28281v1#S1)

論文要回答的是：**能否從開發集案例的修訂成敗中，替每個報告模型學出一套明確、可檢查的規則，規定哪些影像證據在什麼條件下才觸發哪一種局部修改。**作者同時主張這套規則應該依報告模型而異，因為對某個模型有用的修正，對另一個模型可能是多餘或有害的。[(ref: main §1)](https://arxiv.org/html/2611.28281v1#S1)

## 方法摘要

- **任務設定** — 報告模型 G 由 CT 產生草稿 r0；另以與 G 無關的影像分析得到 independent evidence e；系統輸出修訂報告 r1 = Revise(r0, e; B_G)，其中 B_G 是為 G 學出的 rule bank。報告模型本身不重新訓練。[(ref: main §3.1)](https://arxiv.org/html/2611.28281v1#S3.SS1)
- **兩種 independent evidence** — 分類器預測：兩個報告模型都用 COLIPRI 系的視覺編碼器，因此另以 FlexiCT、HLIP、ASAP 三個分別預訓練的編碼器特徵訓練分類器，對每種異常取三者機率平均。影像量測：由 TotalSegmentator v2 遮罩與 Hounsfield unit（HU）計算 15 項數值或類別，例如升主動脈直徑、肝臟衰減值、心胸比、冠狀動脈鈣化體積、積液側別與植入裝置類型。[(ref: main §3.2)](https://arxiv.org/html/2611.28281v1#S3.SS2) [(ref: main Table 8)](https://arxiv.org/html/2611.28281v1#A0.T8)
- **一條規則長什麼樣** — 指定目標發現、編輯類型（新增、移除、補量測值、改屬性）、哪些草稿符合條件，以及可選的「某個證據值高於／低於門檻」條件；每條規則另附編輯指示與證據關係說明。[(ref: main §3.3)](https://arxiv.org/html/2611.28281v1#S3.SS3) [(ref: main Appendix C.2)](https://arxiv.org/html/2611.28281v1#A3.SS2)
- **學規則** — 從空的規則庫開始；learning agent（LLM）每輪提出候選規則，程式在學習案例上搜尋門檻並實際套用，比較修訂前後對參考報告的結果，把改動數量、對異常偵測與報告品質的影響回饋給 agent。規則庫對每個「目標發現 × 編輯類型」只保留最好的一條；學完後 agent 再審查證據與發現的關係是否有醫學依據，刪掉不合理的規則。概念上借用 ExpeL、ReasoningBank 等 experience bank，但把經驗寫成可執行的條件而不是提示詞裡的文字心得。[(ref: main §3.3)](https://arxiv.org/html/2611.28281v1#S3.SS3) [(ref: main §2.2)](https://arxiv.org/html/2611.28281v1#S2.SS2)
- **用規則** — 推論時由程式檢查哪些規則適用；editor agent（LLM）依適用規則提出局部編輯；程式檢查後套用，未編輯的句子原樣保留，每個改動連到觸發它的規則與所用的證據值；editor agent 也可以不改。[(ref: main §3.4)](https://arxiv.org/html/2611.28281v1#S3.SS4)
- **指標** — CE-F1：以 RadBERT 從報告抽出 18 種 CT-RATE 異常標籤後的 macro F1；另有 CRG、GREEN（對參考報告計算臨床錯誤）、CT-FineBench（以問答檢查發現與屬性）與 BLEU、ROUGE-L、METEOR。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1)

## 方法詳解

- **admission 條件** — 規則必須在 3,000 份開發草稿中改動至少 20 份（依學習案例數等比例調整）；要通過以 GREEN 計算的報告品質檢查（新增 18 種標籤內異常時，被改報告的 GREEN 平均變化需 ≥ −1.0 分，其他編輯需不為負）；標籤內的新增與移除必須讓 CE-F1 上升，新增另需對參考標籤 precision ≥ 50%；標籤外的目標，新增時需在至少 60% 被改報告的參考報告中出現，移除時至多 40%。[(ref: main Appendix A.2)](https://arxiv.org/html/2611.28281v1#A1.SS2) [(ref: main Appendix B.1)](https://arxiv.org/html/2611.28281v1#A2.SS1)
- **學習設定** — 每次學習跑 20 輪、每輪最多 20 個新提案；每個條件只比較一個證據值與一個門檻，門檻從符合條件案例的 11 個百分位中搜尋。開發評估採五個病人層級 fold（四個學、一個評），最終規則庫用全部開發案例重學後才跑測試。learning agent、主要 editor agent 與醫學合理性審查都是 gpt-oss-120b；editor 以 temperature 0 執行，無法套用時最多以 temperature 0.7 重試兩次。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1) [(ref: main Appendix B.1)](https://arxiv.org/html/2611.28281v1#A2.SS1)
- **醫學合理性審查只看關係** — 審查只拿到目標、編輯、證據描述與比較方向，判斷這個證據與發現的關係是否合理，不評估數值門檻本身，也不逐一審查實際產生的修訂；直接使用積液側別或裝置類型的編輯免審。[(ref: main Appendix A.2)](https://arxiv.org/html/2611.28281v1#A1.SS2)
- **量測的處理** — 例如肺動脈直徑套用以開發集參考量測擬合的固定 −3.8 mm 校正；肝臟衰減取侵蝕兩個 voxel 後的中位 HU；萃取失敗的量測視為缺值，缺值不滿足任何條件。主動脈分割品質旗標只記錄供檢視，不用來過濾證據；沒有逐例修正遮罩。[(ref: main Appendix A.1)](https://arxiv.org/html/2611.28281v1#A1.SS1)
- **編輯的執行約束** — editor agent 收到編號的草稿句子、相關證據值與每條適用規則的一段指示，回傳連結到規則的編輯（改寫、刪除或新增句子）；程式檢查規則與句子編號後才套用，重複句只留一次。18 種標籤內異常的「是否符合條件」以 RadBERT 對草稿的判讀決定。[(ref: main Appendix A.3)](https://arxiv.org/html/2611.28281v1#A1.SS3)
- **NV-Reason-CT 的開發草稿** — 開發草稿是以 3° 旋轉的輸入產生，讓錯誤程度較接近測試情境；測試草稿不旋轉。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1)
- **論文未交代** — learning agent、editor agent 與醫學合理性審查的完整 prompt 沒有寫在論文裡；最終規則庫（SelfCue-KD 30 條、NV-Reason-CT 13 條）只示範三條，且省略各條的開發集表現；以 Claude Sonnet 5.5 作 editor 的對照透過 Claude Code 執行，取樣設定不在作者控制內；開發集內部有兩個步驟（條件簡化檢查、肺動脈校正）用到所有 fold 的資料，作者以重跑確認 CE-F1 不變，但校正改由學習 fold 擬合後對規則選擇的完整影響未量測。[(ref: main Appendix B.1)](https://arxiv.org/html/2611.28281v1#A2.SS1) [(ref: main Appendix B.3)](https://arxiv.org/html/2611.28281v1#A2.SS3) [(ref: main Appendix C.2)](https://arxiv.org/html/2611.28281v1#A3.SS2)

## 資料與實驗

### 資料

| 用途 | 來源 | 規模 | 說明 |
|---|---|---|---|
| 測試 | CT-RATE 官方 validation split | 1,564 份 CT／1,304 位病人 | 非顯影 3D 胸部 CT 配放射報告；18 種異常標籤 |
| 規則學習（開發） | CT-RATE training split 保留一部分 | 3,000 份 CT／2,490 位病人 | 排除於 SelfCue-KD 訓練之外 |
| 分類器訓練 | CT-RATE training split | 21,765 份擬合＋2,363 份 early stopping | 開發集分數以五個病人層級 fold 交叉產生 |
| 量測涵蓋率計算 | CT-RATE 全部 | 25,692 份（訓練 21,128、開發 3,000、測試 1,564） | 各量測可用率 99.15%–100% |

作者說明保留開發集的理由：報告模型在訓練看過的 CT 上錯誤較少，留給規則學習的錯誤也較少。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1) [(ref: main Appendix A.1)](https://arxiv.org/html/2611.28281v1#A1.SS1) [(ref: main Appendix B.1)](https://arxiv.org/html/2611.28281v1#A2.SS1) [(ref: main Table 8)](https://arxiv.org/html/2611.28281v1#A0.T8)

### 實驗：主結果（論文表 1，本研究的兩個報告模型）

| Model | CE-F1 | CRG | GREEN | CT-FineBench | BLEU-1 | BLEU-4 | ROUGE-L | METEOR |
|---|---|---|---|---|---|---|---|---|
| SelfCue-KD † | 46.2 | 43.9 | 50.5 | 26.2 | 43.6 | 21.7 | 34.9 | 21.2 |
| SelfCue-KD + RuleBank | 57.7 (↑11.5) | 51.9 (↑8.0) | 49.8 (↓0.7) | 41.4 (↑15.2) | 45.6 | 22.4 | 34.6 | 21.7 |
| NV-Reason-CT † | 63.0 | 54.0 | 45.8 | 44.9 | 36.6 | 12.5 | 21.9 | 17.4 |
| NV-Reason-CT + RuleBank | 63.9 (↑0.9) | 54.9 (↑1.0) | 45.9 (↑0.2) | 44.7 (↓0.2) | 36.7 | 12.5 | 21.9 | 17.4 |

† 為作者在自己的評估協定下重跑的基線。論文表 1 另列 CT-CHAT、CLarGen、MedScribe、RadAgent 等文獻數值，多數欄位缺值，評估設定也不一定相同，本文不轉載。CE-F1 增益的 95% 信賴區間：SelfCue-KD 10.48–12.57、NV-Reason-CT 0.49–1.29。[(ref: main Table 1)](https://arxiv.org/html/2611.28281v1#S3.T1) [(ref: main §4.2)](https://arxiv.org/html/2611.28281v1#S4.SS2)

### 實驗：證據來源（論文表 3）

| Setting | CE-F1 | CRG | GREEN | CT-FineBench |
|---|---|---|---|---|
| *SelfCue-KD* | | | | |
| Draft | 46.2 | 43.9 | 50.5 | 26.2 |
| Draft-only learning | 46.2 | 43.9 | 50.4 | 26.3 |
| Classifier evidence | 54.5 | 50.8 | 50.1 | 39.6 |
| Measurement evidence | 50.9 | 45.4 | 50.6 | 28.9 |
| Both evidence sources | 57.7 | 51.9 | 49.8 | 41.4 |
| *NV-Reason-CT* | | | | |
| Draft | 63.0 | 54.0 | 45.8 | 44.9 |
| Draft-only learning | 63.1 | 54.1 | 45.8 | 44.9 |
| Classifier evidence | 63.8 | 54.8 | 45.9 | 44.6 |
| Measurement evidence | 63.4 | 54.3 | 45.7 | 45.0 |
| Both evidence sources | 63.9 | 54.9 | 45.9 | 44.7 |

[(ref: main Table 3)](https://arxiv.org/html/2611.28281v1#S4.T3)

### 實驗：修訂策略（論文表 4，同一批草稿）

| Revision strategy | CE-F1 | CRG | GREEN | CT-FineBench |
|---|---|---|---|---|
| *SelfCue-KD* | | | | |
| Draft | 46.2 | 43.9 | 50.5 | 26.2 |
| Direct LLM revision | 52.5 | 49.1 | 43.8 | 42.4 |
| Classifier-driven | 58.9 | 53.7 | 48.9 | 44.0 |
| Fixed clinical rubric | 44.4 | 43.5 | 49.3 | 28.3 |
| Rule Bank | 57.7 | 51.9 | 49.8 | 41.4 |
| *NV-Reason-CT* | | | | |
| Draft | 63.0 | 54.0 | 45.8 | 44.9 |
| Direct LLM revision | 57.1 | 54.1 | 39.2 | 51.4 |
| Classifier-driven | 60.1 | 54.8 | 42.9 | 45.5 |
| Fixed clinical rubric | 61.2 | 53.1 | 45.0 | 46.4 |
| Rule Bank | 63.9 | 54.9 | 45.9 | 44.7 |

Direct LLM revision 仿 MedScribe 的最終綜合階段，使用相同的 editor 與證據；Classifier-driven 使用以開發集校準的分類器門檻；Fixed clinical rubric 使用文獻量測切點（例如升主動脈 ≥ 40 mm、肝臟中位衰減 ≤ 40 HU、心胸比 ≥ 0.50）。[(ref: main Table 4)](https://arxiv.org/html/2611.28281v1#S4.T4) [(ref: main Table 12)](https://arxiv.org/html/2611.28281v1#A5.T12)

### 實驗：precision 門檻（論文表 5）

| Min. precision (%) | SelfCue-KD Changed (%) | Δ CE-F1 | Δ GREEN | NV-Reason-CT Changed (%) | Δ CE-F1 | Δ GREEN |
|---|---|---|---|---|---|---|
| 30 | 86.0 | +12.21 | −1.69 | 51.3 | +1.07 | −0.65 |
| 40 | 86.2 | +11.79 | −1.18 | 42.5 | +1.14 | −0.26 |
| 50 | 85.0 | +11.50 | −0.69 | 25.9 | +0.89 | +0.17 |
| 60 | 60.1 | +8.81 | 0.00 | 19.9 | +0.55 | +0.11 |
| 70 | 49.1 | +6.02 | +0.08 | 20.0 | +0.42 | +0.11 |

預設值為 50%。[(ref: main Table 5)](https://arxiv.org/html/2611.28281v1#S4.T5)

## 結果

- **改了多少、改在哪** — 規則庫修改了 85.0% 的 SelfCue-KD 草稿與 25.9% 的 NV-Reason-CT 草稿；在被改的 NV-Reason-CT 報告上 CE-F1 多 2.3。兩個模型都是 macro recall 上升（SelfCue-KD 43.4 → 60.1、NV-Reason-CT 59.7 → 64.5），macro precision 變化小（+0.8、−0.7）。[(ref: main §4.2)](https://arxiv.org/html/2611.28281v1#S4.SS2) [(ref: main Table 2)](https://arxiv.org/html/2611.28281v1#S4.T2)
- **偵測增加，也帶進假陽性** — 被改的 SelfCue-KD 報告中，GREEN 的漏寫發現從每份 3.32 降到 3.01，錯誤發現從 1.22 增加到 1.71；以 RadBERT 標籤計，真陽性多 1,148、假陽性多 873。整體 GREEN 微降（95% 信賴區間 −1.38 至 −0.03）；NV-Reason-CT 的整體 GREEN 區間為 −0.22 至 0.57。[(ref: main §4.2)](https://arxiv.org/html/2611.28281v1#S4.SS2) [(ref: main Table 10)](https://arxiv.org/html/2611.28281v1#A3.T10)
- **沒有新的影像觀察就學不到** — 只用草稿衍生訊號（報告長度、異常數、RadBERT 分數）學規則時，學出 8 條（SelfCue-KD）與 5 條（NV-Reason-CT），合理性審查後只剩 1 條與 2 條，CE-F1 幾乎不變；即使不做審查，增益也只有 0.21 與 0.33。被刪的例子包括以報告長度推肺擴張不全、以草稿的食道裂孔疝分數推肺結節。[(ref: main §4.3)](https://arxiv.org/html/2611.28281v1#S4.SS3) [(ref: main Appendix D.1)](https://arxiv.org/html/2611.28281v1#A4.SS1)
- **兩種證據互補** — 單用分類器或單用量測都有增益，兩者合用最高；量測還能處理 18 種標籤以外的發現，例如以肝臟衰減的規則讓脂肪肝的 F1 在 SelfCue-KD 從 34.5 升到 56.4、在 NV-Reason-CT 從 0.0 升到 51.0（脂肪肝標籤由 gpt-oss-120b 以同一個是／否 prompt 從參考報告、草稿與修訂報告抽出）。[(ref: main §4.3)](https://arxiv.org/html/2611.28281v1#S4.SS3)
- **分類器本身不比強模型準，仍有幫助** — 三個分類器的平均 CE-F1 為 59.73，低於 NV-Reason-CT 草稿的 63.03，但 recall 較高（68.86 對 59.93）；規則庫仍讓 NV-Reason-CT 提升到 63.91。[(ref: main Table 11)](https://arxiv.org/html/2611.28281v1#A4.T11)
- **規則比直接交給 LLM 穩** — Direct LLM revision 讓 SelfCue-KD 的 GREEN 從 50.5 掉到 43.8，讓 NV-Reason-CT 的 CE-F1 從 63.0 掉到 57.1；Classifier-driven 在 SelfCue-KD 的 CE-F1 最高（58.9），但兩個模型的 GREEN 都下降，NV-Reason-CT 的 CE-F1 也下降；固定的臨床切點在兩個模型上 CE-F1 都下降。作者的解讀是：證據來源本身不決定修訂是否有益，取決於規則是否配合報告模型原本的強項與錯誤。[(ref: main §4.4)](https://arxiv.org/html/2611.28281v1#S4.SS4)
- **precision 門檻是調整旋鈕** — 門檻從 50% 提高到 70%，SelfCue-KD 被改的比例從 85.0% 降到 49.1%，CE-F1 增益從 11.5 降到 6.0，GREEN 回到草稿水準。[(ref: main §4.4)](https://arxiv.org/html/2611.28281v1#S4.SS4) [(ref: main Table 5)](https://arxiv.org/html/2611.28281v1#S4.T5)
- **重複性** — 五個草稿取樣 seed 各自重學規則庫，CE-F1 每次都上升：SelfCue-KD +10.67 ± 0.80、NV-Reason-CT +0.72 ± 0.33（範圍 0.14–0.93）；GREEN 平均變化接近 0。換用 Claude Sonnet 5.5 作 learning 或 editor agent，第 10 輪時的 CRG 與 CT-FineBench 相近。[(ref: main Table 6)](https://arxiv.org/html/2611.28281v1#S4.T6) [(ref: main Table 13)](https://arxiv.org/html/2611.28281v1#A5.T13) [(ref: main Table 14)](https://arxiv.org/html/2611.28281v1#A5.T14)
- **補上量測值** — 修訂後含量測數值的報告比例，SelfCue-KD 從 18.9% 到 31.3%、NV-Reason-CT 從 0.3% 到 2.9%，共新增 558 個血管直徑，全部與提供的量測值一致（四捨五入後）。在有參考報告直徑可比的升主動脈子集，平均絕對誤差為 2.3 mm（62 例）與 2.4 mm（23 例）。SelfCue-KD 的修訂同時移除了 127 個原有數值。[(ref: main Table 7)](https://arxiv.org/html/2611.28281v1#S4.T7) [(ref: main Appendix E.4)](https://arxiv.org/html/2611.28281v1#A5.SS4)
- **逐條編輯的品質** — 以 Claude Sonnet 5.5 依參考報告判讀每個編輯（不看影像）：得到支持或部分支持的編輯多於被參考報告否定的；以量測補細節的編輯被否定比例為 0.3%（SelfCue-KD）與 2.4%（NV-Reason-CT）；依分類器移除發現的編輯在 NV-Reason-CT 有 45.6% 與參考報告矛盾。[(ref: main §4.5)](https://arxiv.org/html/2611.28281v1#S4.SS5) [(ref: main Appendix F)](https://arxiv.org/html/2611.28281v1#A6)

## 限制

- **測試集在開發時被看過** — 量測定義、編輯操作與新增句措辭是在包含測試集的探索分析中發展的，作者明說結果反映的是「開發過程中檢視過的公開基準」上的評估；門檻與規則納入則只用開發案例決定。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1)
- **沒有放射科醫師評估** — 編輯品質由 LLM 依在放射科醫師指導下設計的 prompt 判讀，判讀本身不是醫師做的，且不看影像；參考報告沒提到的編輯無法驗證，部分支持的編輯仍可能有錯誤細節。[(ref: main §5)](https://arxiv.org/html/2611.28281v1#S5) [(ref: main §4.5)](https://arxiv.org/html/2611.28281v1#S4.SS5)
- **評估範圍** — 只在 CT-RATE（非顯影胸部 CT）上評估兩個報告模型；CE-F1 依賴 RadBERT 對 18 種異常的抽取，標籤外的發現另以 LLM 抽取。對最強的 NV-Reason-CT，增益只有 0.9 點，且 CT-FineBench 的位置與分布屬性分數下降，作者提醒某些修訂可能改善一些屬性、同時損害其他屬性。[(ref: main §4.1)](https://arxiv.org/html/2611.28281v1#S4.SS1) [(ref: main Appendix C.1)](https://arxiv.org/html/2611.28281v1#A3.SS1)
- **證據品質** — 規則只控制雜訊證據如何被使用，不改善證據本身；解剖遮罩對病灶的資訊有限，agent 只拿到證據數值、看不到影像，無法自行複查邊界案例。新增的升主動脈直徑與參考報告差 2.3–2.4 mm，作者引用的專用量測方法對人工標註的誤差約 1.09 mm。[(ref: main §5)](https://arxiv.org/html/2611.28281v1#S5) [(ref: main §4.4)](https://arxiv.org/html/2611.28281v1#S4.SS4)

## 與書庫其他文章的關係

EviGround-CT 在 CT 報告寫完後用 3D 驗證器逐句找影像證據，只負責查核；本篇同樣在報告寫完後才引入獨立的影像證據，但直接依學到的規則改寫草稿，並為每個改動留下觸發規則與證據值: [EviGround-CT：CT 報告逐句送去定位查核，參考遮罩並不完整](2026-10-30-eviground-ct-sentence-grounding-report-verification.md)

DLoss 在訓練時改損失函數、讓 CT 報告模型少寫沒有根據的診斷詞，本篇則完全不重新訓練報告模型，改在生成之後以影像證據修訂草稿，兩篇分別代表「訓練時約束」與「生成後修訂」，也都以 GREEN 評估: [DLoss：訓練時分開施壓該寫與不該寫的診斷詞，GREEN 多 4 分](2026-11-02-dloss-diagnostic-loss-ct-report-generation.md)

兩篇都把影像分類器的分數當作報告之外的證據；Rad-Linter 讓微調小模型判斷胸片報告與分數是否一致、只發出旗標，本篇則在胸部 CT 上用學到的門檻規則決定何時依分數與量測修改報告，並顯示直接讓 LLM 依證據改寫反而降低報告品質: [胸片報告對照分類器分數：1.5B 模型 98.5%，規則 80.5%](2026-11-23-rad-linter-cxr-report-score-consistency.md)

本篇在報告寫完後以獨立影像證據修訂草稿，DeCAD 則在生成時就先讓模型自己寫出陽性發現清單；兩篇都在 CT-RATE 上以 RadBERT 抽出 18 類異常的 macro-F1 評估，增益都以 recall 上升最明顯: [CT 報告模型問得出卻寫不出：先列發現再寫，F1 15.9→39.0](2026-11-26-decad-ct-diagnosis-to-report-gap.md)

本篇證明只看草稿文字學不到該改什麼、必須有獨立的影像證據，該則的產業產品恰好把輸入限定為醫師口述與既有文字、不含任何影像端證據，也因此沒有宣稱任何判讀能力: [不碰判讀只做文書：InteleOrchestrator Clarity 拆解](../industry-watch/2026-11-26-ge-healthcare-inteleorchestrator-clarity-reporting.md)

## 實務的啟發

- **可借用的設計** — 「規則由 LLM 提案、由程式在開發集上驗證與套用、改動可追溯到規則與證據值」的分工，讓修訂行為可以被檢查與審核；對於想用影像工具補強既有報告模型、但不想重訓模型的團隊，這是一個可複製的架構骨架。增益大小則依報告模型而異，本研究在強模型上只多 0.9 點。[(ref: main §3.4)](https://arxiv.org/html/2611.28281v1#S3.SS4) [(ref: main Table 1)](https://arxiv.org/html/2611.28281v1#S3.T1)
- **評估時一定要放「只給草稿」與「直接交給 LLM」兩個對照** — 本研究的 draft-only 對照顯示增益來自新的影像觀察而非重寫本身；direct LLM 對照顯示同樣的證據交給 LLM 自由使用會傷害報告品質。任何報告修訂或後處理方法，都可以用這兩個對照確認增益來源。[(ref: main §4.3)](https://arxiv.org/html/2611.28281v1#S4.SS3) [(ref: main §4.4)](https://arxiv.org/html/2611.28281v1#S4.SS4)
- **待驗證的警訊** — CE-F1 上升主要來自 recall，同時假陽性與 GREEN 的錯誤發現也增加；依分類器「移除」發現的編輯在強模型上近半與參考報告矛盾。在放射科醫師逐例審閱修訂、並在未於開發時檢視過的資料上評估之前，不應把這些數字讀成臨床報告品質的提升。[(ref: main Table 10)](https://arxiv.org/html/2611.28281v1#A3.T10) [(ref: main §4.5)](https://arxiv.org/html/2611.28281v1#S4.SS5)
- **precision 門檻是部署時要決定的取捨** — 門檻越低改得越多、偵測增益越大、參考報告品質越差；這個參數應該依使用情境（例如給醫師看的建議稿或自動定稿）在本地資料上重新選定。[(ref: main Table 5)](https://arxiv.org/html/2611.28281v1#S4.T5)

## References

- `main` — Renjie Liang, Mengxian Lyu, Zijian Xu, Boxin Zhao, Yang Yang, Jinqian Pan, Zhengkang Fan, Mei Liu, Yonghui Wu, Jie Xu. *Learning a Rule Bank to Revise 3D CT Reports with Independent Evidence*. arXiv:2611.28281v1, 2026. HTML：https://arxiv.org/html/2611.28281v1 ；用到的深鏈：[author block](https://arxiv.org/html/2611.28281v1)、[Abstract](https://arxiv.org/html/2611.28281v1#abstract1)、[Figure 1](https://arxiv.org/html/2611.28281v1#S0.F1)、[§1](https://arxiv.org/html/2611.28281v1#S1)、[§2.2](https://arxiv.org/html/2611.28281v1#S2.SS2)、[§3](https://arxiv.org/html/2611.28281v1#S3)、[Table 1](https://arxiv.org/html/2611.28281v1#S3.T1)、[§3.1](https://arxiv.org/html/2611.28281v1#S3.SS1)、[§3.2](https://arxiv.org/html/2611.28281v1#S3.SS2)、[§3.3](https://arxiv.org/html/2611.28281v1#S3.SS3)、[§3.4](https://arxiv.org/html/2611.28281v1#S3.SS4)、[§4.1](https://arxiv.org/html/2611.28281v1#S4.SS1)、[§4.2](https://arxiv.org/html/2611.28281v1#S4.SS2)、[Table 2](https://arxiv.org/html/2611.28281v1#S4.T2)、[§4.3](https://arxiv.org/html/2611.28281v1#S4.SS3)、[Table 3](https://arxiv.org/html/2611.28281v1#S4.T3)、[§4.4](https://arxiv.org/html/2611.28281v1#S4.SS4)、[Table 4](https://arxiv.org/html/2611.28281v1#S4.T4)、[Table 5](https://arxiv.org/html/2611.28281v1#S4.T5)、[Table 6](https://arxiv.org/html/2611.28281v1#S4.T6)、[Table 7](https://arxiv.org/html/2611.28281v1#S4.T7)、[§4.5](https://arxiv.org/html/2611.28281v1#S4.SS5)、[§5](https://arxiv.org/html/2611.28281v1#S5)、[Table 8](https://arxiv.org/html/2611.28281v1#A0.T8)、[Appendix A.1](https://arxiv.org/html/2611.28281v1#A1.SS1)、[Appendix A.2](https://arxiv.org/html/2611.28281v1#A1.SS2)、[Appendix A.3](https://arxiv.org/html/2611.28281v1#A1.SS3)、[Appendix B.1](https://arxiv.org/html/2611.28281v1#A2.SS1)、[Appendix B.3](https://arxiv.org/html/2611.28281v1#A2.SS3)、[Appendix C.1](https://arxiv.org/html/2611.28281v1#A3.SS1)、[Table 10](https://arxiv.org/html/2611.28281v1#A3.T10)、[Appendix C.2](https://arxiv.org/html/2611.28281v1#A3.SS2)、[Appendix D.1](https://arxiv.org/html/2611.28281v1#A4.SS1)、[Table 11](https://arxiv.org/html/2611.28281v1#A4.T11)、[Table 12](https://arxiv.org/html/2611.28281v1#A5.T12)、[Table 13](https://arxiv.org/html/2611.28281v1#A5.T13)、[Table 14](https://arxiv.org/html/2611.28281v1#A5.T14)、[Appendix E.4](https://arxiv.org/html/2611.28281v1#A5.SS4)、[Appendix F](https://arxiv.org/html/2611.28281v1#A6)
- `abstract` — arXiv abstract page, 2611.28281v1：https://arxiv.org/abs/2611.28281v1 （PDF：https://arxiv.org/pdf/2611.28281v1 ；DOI：https://doi.org/10.48550/arXiv.2611.28281）

[Home](../) · [AI Papers](./)
