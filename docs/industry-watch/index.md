---
title: Industry Watch
nav_order: 4
has_children: true
has_toc: false
---

[Home](../) · [Industry Watch](./)

# Industry Watch

國際大廠與台灣同業動向；亦涵蓋影響研究流通的平台／政策動態。

## 文章列表

| 日期 | 標題 | 編輯 | 備註 |
|------|------|------|------|
| 2026-11-17 | [API 到不了就改用點擊：OpenAI 醫療 computer use 解析](2026-11-17-openai-computer-use-agents-healthcare.md) | Clarence | 2026-11-16 官方公告，另有同日 ChatGPT for Healthcare 配套公告（同一家公司兩個官方頁，評估數字為單一組織自報）；代理程式以點擊、輸入與切換應用程式的方式操作既有醫療軟體，CVS Health 明言是為了完成 API 無法完全支援的步驟；適用範圍為事前授權、申覆、轉診、出院規劃與就診間追蹤聯繫；GPT-6 Astra 在 EHR 收件匣任務上，325 件受審任務 99% 被評為安全、646 次評估中 93% 被醫師評為 very helpful 或 extremely helpful（兩項分母不同，無對照組與人類基準，未通過案例未揭露）；HealthAdminBench 上官方自報 Astra 取得可得 rubric points 的 94.3%、Luna 91.8% 且每題 8.5 美分、便宜 98% —— 但該榜公開頁上 GPT-6／Astra／Luna 命中皆為 0，OpenAI 最新在榜型號為 GPT-5.4，且公告引用的是該站的 Subtask Score 而非頭條的 SCORE（預設檢視最高僅 36.3%）；依該站公布的逐筆資料加總，同一個 GPT-5.4 的 subtask 百分比在 Axtree 為 84.6%、Screenshot 為 43.5%，而公告未說明觀察模式與提示策略；四家具名機構中 CVS Health 與 Cigna Healthcare 已在生產環境、Abridge 的住院情境寫明為 planned、Ambience 示範的是遇病歷模稜兩可即停下詢問；全文 FDA、study、trial、peer、arXiv 命中皆為 0 |
| 2026-11-16 | [例行實驗判讀只拿 66.7%：OpenAI BioBasicsBench 拆解](2026-11-16-openai-biobasicsbench-wet-lab-agents.md) | Clarence | 2026-11-06 官方公告（單源，待交叉驗證；共同開發方 Ligo 為出題與審查方，非獨立驗證者，公告未附其連結或聲明）；BioBasicsBench 共 100 題，涵蓋 protein methods、imaging and cytometry、quantification and assays、nucleic acid methods、molecular cloning 五個領域，素材為膠片與轉漬、培養皿、顯微影像堆疊、定序檔、儀器螢幕翻拍等尚未整理成圖表的原始證據，輸入型態表九類合計 149（公告載明分類重疊）；出題者為科學家本人，每題附專家撰寫的逐條評分標準，經 Ligo 內部非作者、外部在職濕實驗室博士、最終內部三道審查；評了七個自家型號、37 組設定、每題五次，合計 18,500 筆結果（37×100×5，本文代為驗算相符）；xhigh 成績 GPT-6 Astra 66.7%（95% 信賴區間 60.3–73.1%、每題 4,704 token）、GPT-6.1 Sol 62.0%（55.6–68.4%、5,238）、GPT-5.6 Sol 43.8%（37.6–50.0%、9,099）、最舊的 GPT-5.2 31.2%（26.2–36.3%、27,620）—— 前兩位的區間大幅重疊，Astra 與 GPT-5.6 Sol 的區間不重疊；公告自寫 Higher benchmark scores do not yet mean models can make reliable judgments in the lab，並舉三個 Astra 失誤例：菌落 PCR 選第 4、6、7、8 泳道而參考答案為第 5、9、10、液泡對比只保留較暗那一種、單一示例盤菌落高估約 12%；全文 baseline 命中 0、human 僅出現在 humanity 一句，無人類基準；release／download／GitHub／arXiv 命中皆為 0，題庫未見釋出；clinical／medical／patient／FDA 命中皆為 0，頁面類型標為 Publication 卻無論文連結，作者欄位為 OpenAI；該頁無 JSON-LD 與 article:published_time，頁內 time 元素僅屬文末延伸閱讀卡片，日期以頁面可見文字與新聞列表頁互為佐證 |
| 2026-11-16 | [非旗艦卻超過自家 Argon：Gemini 4 Hydrogen 解析](2026-11-16-gemini-4-hydrogen-agentic-execution-model.md) | Clarence | 2026-11-12 官方部落格，另有同日 Google Antigravity 官方部落格（同一家公司兩個官方頁，無獨立第三方驗證）；定位為與前沿模型 Carbon／Argon 分工的快速執行層，整個一百萬 token 脈絡視窗單一費率，每百萬 input token 1.50 美元、output 7.50 美元；Artificial Analysis Intelligence Index 預設 high 為 51、高過 Argon 的 50，xhigh 為 54；Orchestrator 在單一任務中於 Carbon 與 Hydrogen 之間雙向切換，官方自報平均少用 24% quota、快 19% 完成 —— 同一組數字在公告頁標 Terminal-Bench 4.0、在 Antigravity 頁標 4.1；醫療接點兩處：HealthBench Pro 上正當醫學與科學問題的誤擋率「低於 0.4%」（上界，無分母無對照），以及 LatchBio 自建 Antibody Development benchmark 毒理與安全一節 67% 對 37%（合作夥伴自報） |
| 2026-11-12 | [不拚通用模型拚細胞條件：AlphaGenome 2 變異預測拆解](2026-11-12-deepmind-alphagenome-2-cell-type-variants.md) | Clarence | 2026-11-11 官方部落格（單源，待交叉驗證）；二版改為 conditional model，把組織／細胞類型／細胞狀態當成輸入條件，一次預測一個條件，條件可取自 reference catalog 或由使用者自己的 scRNA-seq 經 cell encoder 即時產生；讀出項目新增 DNA methylation；訓練含人與小鼠逾 1.07 億個 cell profiles。量化結果一組：TenK10K（28 種 primary immune cell types）causal variants 30% 對 16%、directional gene effects 43% 對 23%，對照組為在單細胞資料上微調過的初版加未具名的其他工具，公告未給分母。兩個疾病案例皆為回溯（IBD／ETS2 出自 2024-06-05 Nature 論文）。非商業研究可直接以 API 取用、商業為 private preview；官方載明僅供研究用途、未經臨床或診斷驗證 |
| 2026-11-11 | [不談 AI 拼硬體梯度：GE 籌組九機構 MAGNUS 神經影像聯盟解析](2026-11-11-ge-healthcare-magnus-neuro-alliance.md) | Clarence | 2026-11-10 官方新聞稿（單源，待交叉驗證）；頁面 HTML 標題與網址寫 establishes，頁面 H1 與正文寫的是 announces intent to establish；正文談臨床轉譯與臨床應用，註腳 1 寫 Not cleared or approved by the U.S. FDA or other global regulators、不可販售、僅供研究；新聞稿區塊 %、mT/m、slew、Tesla、510、CE mark 與獨立詞 AI 命中皆為 0，唯一機器規格是 3.0T；九家機構以 current and future users 合併表述 |
| 2026-11-10 | [要先過審核才拿得到生醫能力：Fable 與 Mythos 5.2 一探究竟](2026-11-10-anthropic-claude-fable-mythos-5-2-launch.md) | Clarence | 2026-11-09 官方公告，另有同公司 2026-09-17 的 Life Sciences Verification Program 頁（同一家公司兩個官方頁，無獨立第三方驗證）；蛋白質設計 85.1% 與 AAV capsid 二十八比三十四都屬於 Mythos 5.2，而一般可用的 Fable 5.2 會擋下大部分研究生物學任務改由 Opus 5 回答，取用須經 LSVP 審核且 Mythos 高風險授權僅限少數單位；公告「almost all 勝過 Opus 5.5」逐列核對後，唯一例外是 AA-Briefcase v1.1 的 Elo 1785 對 1800 |
| 2026-11-09 | [給臨床人員、可抵 CME 的四門課：Google 醫療 AI 認證重點整理](2026-11-09-google-ai-healthcare-professionals-certificate.md) | Clarence | 2026-10-29 官方部落格，另有 grow.google 課程頁與 Coursera 課程頁（內容同源，待獨立驗證）；「reviewed by leading academic and professional organizations」在三個官方頁面中無一具名任何組織，公告具名的四所學校都是採用方；課程時數三頁有三種說法（約四小時／未滿五小時／逐課加總五小時），而學分上限 5.0 附帶「按實際參與程度申報」的條件，公告只搬了上限 |
| 2026-11-06 | [代理程式串起既有化學工具：DeepMind 藥物設計 Skills 解剖](2026-11-06-deepmind-antigravity-cheminformatics-drug-design.md) | Clarence | 2026-11-03 官方部落格（單源，待交叉驗證）；示範案例由公告自己標為 well-known case，MMPA 結論被寫成 as expected，正文 %、accuracy、AUC、RMSE、peer、arXiv、DOI 命中皆為 0，唯一能外部核對的兩個數字是 crizotinib 的 5 與 lorlatinib 的 0 個可旋轉鍵 |
| 2026-11-06 | [掌上超音波加肺部導引與瓣膜提示：Vscan Air 510(k) 分析](2026-11-06-ge-healthcare-vscan-air-lung-guidance-autoas.md) | Clarence | 2026-11-03 官方新聞稿，另有 FDA 公開的兩份 510(k) summary（Lung Guidance K261042、AutoAS K254161）；新聞稿的 95.2% 對 96.8% 來自 63 位病人，FDA 摘要同時載明兩組差距為 −1.6 個百分點、95% 信賴區間 −18.7 到 15.5 |
| 2026-11-05 | [給了框架不給門檻：Google 健康 AI 評估三法十七維解讀](2026-11-05-google-health-ai-evaluation-framework.md) | Clarence | 2026-11-04 官方部落格，另有 arXiv:2611.05127 白皮書（2026-11-03）與 Gemini 4 Argon 安全報告；白皮書明寫不設通用數值切點、門檻由各團隊在各自 phase-gate 自訂，被連結的 Table 5.1 高風險情境 98.9 低於前代 Gemini 3.8 Flash 的 99.4 |
| 2026-11-03 | [48.1% 的關鍵實驗放寬過條件：LLM 直接改權重拆解](2026-11-03-weight-space-programming-llm-reads-writes-weights.md) | Clarence | 2026-11-02 作者自建站研究部落格（單源，無 arXiv／DOI、未經同儕審查，但釋出完整 logs 與編輯後模型）；Experiment 7 僅憑權重四次嘗試全部失敗，放寬為可看注意力圖樣後才成立 |
| 2026-11-03 | [歐盟可買、美國待審的吊掛介入機：Allia Celeo 一探究竟](2026-11-03-ge-healthcare-allia-celeo-interventional-launch.md) | Clarence | 2026-11-01 官方新聞稿（單源，待交叉驗證；官網無產品頁可比對）；Allia 平台繼落地式 Moveo 之後的第二台新機，改為天花板吊掛式，用於心導管室與介入放射手術房；相容工具分兩組——冠狀動脈與結構性心臟病（StentViz、3DStent、Valve ASSIST 2、Mac-Lab）該句寫 cleared 兩次，介入放射與腫瘤（Embo ASSIST AI、Vessel ASSIST、Needle ASSIST）該句未寫；服務端配 OnWatch Predict（24/7 遠端監控＋deep learning 預測非計畫性停機）；星號註腳寫 CE marked、510(k) pending、不得在美國銷售、可能並非所有地區供應。文章區 6,005 字元內 %／percent、study、trial、data、evidence 命中皆為 0，正文 designed to／with the goal of／aim to／intended to 合計 15 次 |
| 2026-11-02 | [把診斷評估改成逐步問診並計成本：SDBench 與 MAI-DxO 解析](2026-11-02-microsoft-mai-dxo-sdbench-sequential-diagnosis.md) | Clarence | 2026-10-22 官方公告，同日論文刊於 Science（FREE ACCESS）；「近四倍準確率」與「一半甚至三分之一成本」分屬四個運作點中的不同者，急診案例組沒有任何運作點符合後者 |
| 2026-10-30 | [基金會與研究機構可申請免費額度：Anthropic 擴編重點整理](2026-10-30-anthropic-ai-for-science-foundations-expansion.md) | Clarence | 2026-10-28 官方公告；三份名單的 li 元素逐一計數為 6+6+6=18，而正文、meta description 與 JSON-LD 三處都寫 20 |
| 2026-10-29 | [營收成長 7.2%、全年財測上修：GE 第三季財報分析](2026-10-29-ge-healthcare-q3-2026-results.md) | Clarence | 2026-10-28 官方新聞稿與同日 SEC Form 8-K；官網 11 張財務表格為點陣圖，數值以 Exhibit 99 的 HTML 表格核對 |
| 2026-10-29 | [代理程式從資料庫走到實驗計畫：DeepMind 抗菌胜肽解剖](2026-10-29-deepmind-antigravity-antimicrobial-peptide-walkthrough.md) | Clarence | 2026-10-15 官方部落格；正文 peer／paper／arXiv／DOI 命中皆為 0，候選分子名稱的 UniProt 證據標籤為 Automatic Annotation (ECO:0008006) Google:ProtNLM |
| 2026-10-29 | [4D SPECT/CT 交五家機構評估：StarGuide GX 一探究竟](2026-10-29-ge-healthcare-starguide-gx-theranostics-collaborations.md) | Clarence | 2026-10-20 官方新聞稿；與 2026-09-08 同產品公告逐字並排，四處措辭不同；美國站產品目錄無此機種 |
| 2026-10-29 | [顯示器裝上機身的行動式 C 臂：Cios Go ID 拆解](2026-10-29-siemens-cios-go-id-mobile-c-arm-dkou.md) | Clarence | 2026-10-20 官方新聞稿；產品頁 17 個上標中 16 個是「選配」，Evidence 區塊內容為假體影像與兩段證言 |
| 2026-10-28 | [藥物開發端的第一批成果：Anthropic 六個合作組織大公開](2026-10-28-anthropic-drug-development-case-studies.md) | Clarence | 2026-10-27 官方公告；樣本數與六段利益揭露只存在於同頁可展開面板 |
| 2026-10-22 | [一個代理讀一個基因：OpenAI 全腦擾動圖譜解讀拆解](2026-10-22-openai-distributed-agents-perturb-seq-atlas.md) | Clarence | 2026-10-21 官方公告；所依據的 bioRxiv 預印本未經同儕審查，75% 的分母是 20 組配對共 60 次判斷 |
| 2026-10-21 | [高階影像能力下放日常機種：LOGIQ Focus 超音波解析](2026-10-21-ge-healthcare-logiq-focus-ultrasound-launch.md) | Clarence | 2026-10-19 官方新聞稿；「快 26%」比的是自家前代機，同一研究對競品無時間差異 |
| 2026-10-21 | [代理式工作流程推論成本漲逾五倍：Gartner 2028 預測分析](2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md) | Clarence | 2026-08-17 官方新聞稿；全文無金額、無基準年，正文無百分比 |
| 2026-10-20 | [看診前先問病史的 98 人試驗：AMIE Lancet 可行性研究解讀](2026-10-20-google-amie-lancet-primary-care-feasibility.md) | Clarence | 2026-10-08 官方部落格；同日 The Lancet 線上刊出，試驗登錄 NCT06911398 |
| 2026-10-19 | [放射性藥物院內自製：MINItrace 加 Copper-64 解密](2026-10-19-ge-healthcare-minitrace-magni-ce-mark-copper-64.md) | Clarence | 2026-10-15 官方新聞稿；全頁無百分比、無註腳 |
| 2026-10-19 | [12,818 例回溯分析自動調控麻醉氣體：ETC 密西根研究分析](2026-10-19-ge-healthcare-end-tidal-control-michigan-study.md) | Clarence | 2026-10-16 官方新聞稿；論文開放取用，62.3% 為範例病人推算值 |
| 2026-10-15 | [合作先行、產品未到：GE 與 MGB 放療生成式 AI 一探究竟](2026-10-15-ge-healthcare-mgb-genai-radiation-therapy.md) | Clarence | 2026-09-23 官方新聞稿；生成式 AI 部分無任何數字 |
| 2026-10-14 | [四款機型當日停售：Siemens 退出一般影像超音波怎麼回事](2026-10-14-siemens-ultrasound-general-imaging-exit.md) | Clarence | 2026-10-12 官方公告；公告日即停售日，未給被退出業務的任何數字 |
| 2026-10-13 | [把自家代工廠買回來：GE 收購 SOFIE 與 FAPI-74 權利解析](2026-10-13-ge-healthcare-sofie-pet-radiopharma-acquisition.md) | Clarence | 2026-10-05 官方新聞稿；交易預計 2027 上半年完成 |
| 2026-10-13 | [影像到出束最快 90 秒：Siemens Accela 上市前搶先看](2026-10-13-siemens-accela-radiotherapy-launch.md) | Clarence | 2026-09-27 ASTRO 2026 發表；九個數值全為上下限 |
| 2026-10-08 | [開放權重醫療模型的四國五案：MedGemma 落地現況重點整理](2026-10-08-medgemma-global-deployment-claims.md) | Clarence | 2026-09-23 官方公告；五案一數字 |
| 2026-10-07 | [價格只要五分之一，但科學能力沒跟上：GPT-6.1 Sol 解剖](2026-10-07-openai-gpt-6-1-sol-launch.md) | Clarence | 官方公告未標日期；$2／$10 per M token |
| 2026-09-18 | [舊許可不是通行證：FDA 駁回放射科 CAD 510(k) 免審解讀](2026-09-18-fda-radiology-cad-510k-exemption-denied.md) | Clare | 09-17 最終命令；Harrison.ai 請願遭駁回 |
| 2026-09-17 | [一邊聽人說一邊跑工具：Gemini 3.8 Live 語音模型分析](2026-09-17-gemini-3-8-live-launch.md) | Clare | 09-15 官方公告；AA Index 82.6 |
| 2026-09-17 | [看方向可以、當合規依據不行：FDA GenAI 醫材討論文件解讀](2026-09-17-fda-genai-devices-discussion-paper.md) | Curitis | 2026-08-18 討論文件；意見至 10-19 |
| 2026-09-15 | [一封公開信讓全業表態：Amodei 前沿調速宣言一探究竟](2026-09-15-amodei-pace-the-frontier.md) | Clare | 09-12 原文；各方回應至 09-14 |
| 2026-09-15 | [AI 只能提醒不能下診斷：FDA 心血管 ML 軟體新條號解析](2026-09-15-fda-cardio-ml-notification.md) | Curitis | 21 CFR 870.2380 |
| 2026-09-15 | [幻覺引用沒抓掉可能禁投一年：arXiv AI 內容政策怎麼回事](2026-09-15-arxiv-ai-content-policy.md) | Curitis | 2026-05 處罰澄清 |

[Home](../) · [Industry Watch](./)
