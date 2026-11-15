---
parent: Industry Watch
nav_order: 4
title: "Google 醫療人員 AI 認證：四門課、最多 5.0 CME 學分"
category: industry-watch
date: 2026-11-09
updated: 2026-11-12
tags: [Google, Grow-with-Google, Google-for-Health, AI-literacy, continuing-medical-education, CME, AMA-PRA-Category-1, ACCME, iiCME, AAMC, Coursera, clinician-training, non-clinical-tasks, Gemini]
catalog_id: "google:ai-for-healthcare-professionals-certificate-2026-10-29"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
skill_version: "write-industry-watch@3.1"
source:
  orgs:
    - "Google（Grow with Google）"
    - "International Institute for Continuing Medical Education（iiCME）"
  event: "Google 發布 Google AI for Healthcare Professionals Certificate，宣稱由 Google 的臨床醫師開發、經領先的學術與專業組織審閱，並提供最多 5.0 個 AMA PRA Category 1 Credits"
  event_date: "2026-10-29"
  official_url: "https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/"
  single_source: false
  single_org: true
related_articles:
  - path: "2026-11-05-google-health-ai-evaluation-framework.md"
    relation: "同一個官方部落格頻道相隔六天的兩則發布，把「誰來判斷模型輸出好不好」推給了相反的兩邊：該則的白皮書明寫量化門檻由各產品團隊在自家 phase-gate 自訂、不設通用數值切點，本則的課程則教臨床人員 evaluate model outputs with your clinical judgment，等於把同一個判斷責任交給第一線使用者，而兩則都沒有給出任何一個可操作的門檻"
  - path: "2026-10-08-medgemma-global-deployment-claims.md"
    relation: "同一家公司面向醫療的兩條路線：該則是把開放權重模型送進資源有限地區的落地合作，本則是給臨床人員的 AI 素養課程與繼續教育學分。兩則並讀可以看出 Google 在醫療 AI 上同時投入工具端與人員端"
  - path: "2026-10-20-google-amie-lancet-primary-care-feasibility.md"
    relation: "兩則的數字都只給了上限：該則的 90% 是前七名清單的命中率、排第一只有 56%，本則的 5.0 個繼續教育學分同樣是 maximum，而課程頁自己寫醫師只能按實際參與程度申報，公告轉述時兩句都只搬了前半"
refs:
  blog:
    title: "Equipping healthcare professionals with practical AI skills（Google 官方部落格，2026-10-29）"
    url: "https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/"
  program:
    title: "AI for Healthcare Professionals（Google 官方課程說明頁，grow.google）"
    url: "https://grow.google/healthcare-professionals/"
  coursera:
    title: "Google AI for Healthcare Professionals 專項課程（Coursera 課程頁，含 iiCME 繼續教育認證聲明）"
    url: "https://www.coursera.org/specializations/google-ai-for-healthcare-professionals"
---

[Home](../) · [Industry Watch](./)

# Google 醫療人員 AI 認證：四門課、最多 5.0 CME 學分

## 來源

- 組織／產品：Google（Grow with Google）— Google AI for Healthcare Professionals Certificate。課程由 Coursera 託管；繼續教育學分由 International Institute for Continuing Medical Education（iiCME，國際繼續醫學教育協會）與 Google LLC 以 joint providership（共同提供）的形式提供。
- 事件：Google 推出一張針對醫療專業人員的 AI 認證，四門線上自學課程，範圍限定在非臨床任務，完成後可申請最多 5.0 個 AMA PRA Category 1 Credits™（美國醫學會 American Medical Association 的第一類繼續醫學教育學分）。
- 日期：2026-10-29（公告頁可見文字為 `Oct 29, 2026`；`article:published_time` 為 `2026-10-29`，`published_time` 與 JSON-LD `datePublished` 皆為 `2026-10-29T13:00:00+00:00`，三處一致）
- 官方入口：[Google 官方部落格公告](https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/)
- 其他官方頁面：[課程說明頁](https://grow.google/healthcare-professionals/)（grow.google）與 [Coursera 專項課程頁](https://www.coursera.org/specializations/google-ai-for-healthcare-professionals)（含 iiCME 的繼續教育認證聲明）
- **內容同源，待獨立驗證**：三個頁面的實質內容都由 Google 提供，Coursera 僅為託管平台；全文唯一不出自 Google 的敘述，是 Coursera 頁上那段 iiCME 的認證聲明。

**編輯：** Clarence

Google 在 2026-10-29 由 Chief Health Officer（首席健康長）Michael Howell 具名發出一篇標示 `3 min read` 的部落格，推出 Google AI for Healthcare Professionals Certificate [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/)。這是一套託管在 Coursera 的四門線上自學課程，內容限定在非臨床的行政任務、病人溝通與專業進修，課程頁並明文寫出它不涵蓋臨床診斷、醫療決策與治療建議；完成後可申請最多 5.0 個 AMA PRA Category 1 Credits™，由經 ACCME 認可的 iiCME 與 Google 共同提供，學分資格自 2026-10-29 起算、2029-10-29 到期。公告具名四所已經把這張認證開給自家師生或護理學生的學校。對台灣的臨床人員進修與院內教育訓練規劃而言，這張認證本身不能直接換成國內學分，可用的是它的結構：課程邊界怎麼寫、時數與學分如何對應、認證由誰授予、利益揭露放在哪裡。三個官方頁面之間另有數處敘述不一致，集中收在後段的證據邊界一節。

## 背景

- **2026-10-29** — Google 官方部落格發出公告（本則事件）。同一天，Coursera 頁面上的 iiCME 聲明記載這份 enduring material activity（長效型教材活動）的有效期自 `October 29, 2026` 起算 [(ref: coursera)](https://www.coursera.org/specializations/google-ai-for-healthcare-professionals)，與公告同日，可確認兩者指向同一次發布。
- **2029-10-29** — 同一段聲明記載的有效期終止日。也就是說，這張認證的學分資格有一個三年的明確到期日。
- **取頁當日（2026-11-09）** — Coursera 頁面顯示 3,448 人已註冊、評分 4.8 來自 12 則評論，等級標示為「初級 等級」，課程標示「最近已更新！十月 2026」。這三個數字會隨時間變動，本文只記錄取頁當下的值。

公告用兩項外部統計說明這套課程要解的問題：一份 National Nursing Workforce Survey 指 `nearly one in three registered nurses planned to leave or retire due to unsustainable workloads`，連向《Journal of Nursing Regulation》的一篇文章；以及 `nine out of 10 doctors say they want dedicated training in how to use AI effectively`，連向 American Medical Association 的一份醫師態度報告 PDF [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/)。這兩份文件的原始數值未納入本文引述，本文只記錄公告引用了它們。

課程與認證之間的分工也屬於本則的脈絡：Google 是內容製作方與 joint provider 之一，iiCME 是經 Accreditation Council for Continuing Medical Education（ACCME，美國繼續醫學教育評鑑委員會）認可、實際授予學分的一方，Coursera 則是收費與託管平台。

本則無配圖。三個官方頁面上的課程縮圖、講師照與產品截圖均為 Google 與 Coursera 自有素材，不重製。

## 這張認證是什麼（事實）

- **形式與門檻** — 四門線上課程，self-paced（自學、可自訂進度），Coursera 的等級標示為「初級 等級」。grow.google 的常見問答把它描述為 `four courses (approximately one hour each)`，公告與 Coursera 的課程描述則寫這套課程 `designed to be completed in less than five hours`／`In under 5 hours` [(ref: program)](https://grow.google/healthcare-professionals/)。
- **開發者** — 公告寫這張認證 `Built by clinicians at Google`，並列出開發者的專科背景為 `backgrounds spanning internal medicine, pediatrics, critical care medicine, emergency medicine, and public health`。公告本身由 Chief Health Officer Michael Howell 具名發出 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/)。
- **教學工具** — grow.google 列出的工具為 `GEMINI`、`GEMINI NOTEBOOK`、`GEMINI FOR WORK`，都是 Google 自家產品；同時三個頁面都把這套技能描述為可跨工具使用，Coursera 的常見問答用詞是 `product-agnostic`（不綁定特定產品）[(ref: program)](https://grow.google/healthcare-professionals/)。
- **收費** — grow.google 寫 `In the U.S. and Canada, the program is available on Coursera through a monthly subscription of $49 per month, allowing you to finish at your own pace. Prices may vary by country.`；Coursera 頁的註冊按鈕文字則是「免費註冊」，其結構化資料的 `offers` 類別為 `Subscription` [(ref: coursera)](https://www.coursera.org/specializations/google-ai-for-healthcare-professionals)。

## 四門課涵蓋到哪裡、不涵蓋哪裡（事實）

四門課依序為 AI Fundamentals for Healthcare Professionals、Strengthen Patient Communication with AI、Optimize Healthcare Administrative Tasks with AI、Advance Healthcare Professional Development with AI。Coursera 的課程清單逐課標示第 1 門 2 小時、第 2、3、4 門各 1 小時 [(ref: coursera)](https://www.coursera.org/specializations/google-ai-for-healthcare-professionals)。

- **涵蓋範圍** — grow.google 的常見問答寫 `The certificate is strictly designed for non-clinical administrative tasks, patient communication, and professional development.`，三項，與四門課名對得上 [(ref: program)](https://grow.google/healthcare-professionals/)。
- **排除範圍** — 同一則問答以 `No.` 開頭，接著寫 `It does not cover clinical diagnosis, medical decision-making, or treatment recommendations.` 這是三個官方頁面上對課程邊界最明確的一句。
- **公告的範圍句較窄** — 公告寫 `the program offers flexible, self-paced lessons that focus on non-clinical administrative tasks. It is designed to be completed in less than five hours`，只列了課程頁三項中的一項。
- **課綱依據** — 公告寫 `the curriculum draws on draft versions of the Association of American Medical Colleges (AAMC) Artificial Intelligence Competencies Across the Learning Curriculum (which was under development at the time of the initial course design, but reflected the overall direction of the final competencies)`，即課綱參考的是 AAMC 能力指標的草案版本。

## 採用的學校與課綱審閱者（事實）

- **四所具名的學校都是採用方** — 公告具名 NYU Grossman School of Medicine、University of Alabama at Birmingham、Touro University，句子動詞是 `are offering it to their faculty, residents, and medical students`（開給自家教師、住院醫師與醫學生）；另具名 Purdue University School of Nursing，句子說它屬於 `leading nursing institutions` 中提供這張認證的一員 [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/)。
- **公告收錄的審閱意見** — 公告在 `Clinical and medical education professionals who reviewed the curriculum` 這個標題之後，放了一段引言，署名為 Anoop Muniyappa, M.D., Director of AI in MedEd, UCSF。
- **摘要句的定位** — 公告的摘要句把這張認證概括為 `Built by clinicians at Google and reviewed by leading academic and professional organizations`。

## 學分怎麼算（事實）

- **授予方與形式** — 學分由 iiCME 與 Google LLC 以 joint providership 共同提供，iiCME 為 ACCME 認可機構，課程形式登記為 enduring material（長效型教材），有效期聲明原文為 `This enduring material activity is valid from October 29, 2026 through October 29, 2029.` [(ref: coursera)](https://www.coursera.org/specializations/google-ai-for-healthcare-professionals)
- **學分數與申報條件** — iiCME 聲明原文為 `The iiCME designates the enduring format for this educational activity for a maximum of 5.0 AMA PRA Category 1 Credits™. Physicians should only claim credit commensurate with the extent of their participation in the activity.` 也就是 5.0 是上限，實際可申報的數量以參與程度為準。
- **公告的對應句** — `The Google AI for Healthcare Professionals Certificate offers an opportunity to build these skills, while earning up to 5.0 AMA PRA Category 1 Credits™` [(ref: blog)](https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/)。
- **財務揭露** — Coursera 頁的揭露聲明寫 `All faculty, planners, reviewers, or staff report no relationships to disclose`，引號內的自述是未持有與 `ineligible companies` 的財務關係。

## 證據邊界（事實）

以下各項是本則在三個官方頁面之間核對出的落差與限制，列在這裡供引用時參考：

- **「經領先組織審閱」沒有任何一個組織被具名。** 公告摘要句為 `Built by clinicians at Google and reviewed by leading academic and professional organizations`；grow.google 課程頁上 `reviewed by leading` 出現 3 次（`reviewed by leading healthcare organizations`）[(ref: program)](https://grow.google/healthcare-professionals/)。同一頁逐詞計數，`NYU`、`Purdue`、`UCSF`、`Touro`、`Alabama` 的命中數皆為 0；頁面出現的 `AAMC` 兩次都在「課綱參考了 AAMC 的能力指標草案」這個語境，不是審閱者。三個官方頁面合計，沒有任何一個組織被指為審閱者。
- **公告具名的四所學校，動詞都是採用。** 三所學校的句子動詞是 `are offering it to their faculty, residents, and medical students`，Purdue University School of Nursing 的句子是提供這張認證的一員。四處都是採用，沒有一處是審閱。
- **唯一具名的審閱意見來自個人。** `Clinical and medical education professionals who reviewed the curriculum` 之後只有一段引言，署名 Anoop Muniyappa, M.D., Director of AI in MedEd, UCSF。這是一位個人，不是一個以組織名義出具的審閱結論。
- **課程時數有三種說法。** grow.google 的常見問答寫 `four courses (approximately one hour each)`，約四小時；公告與 Coursera 的課程描述都寫 `In under 5 hours`；Coursera 的課程清單則逐課標示第 1 門 2 小時、第 2、3、4 門各 1 小時，加總為 5 小時，而同一頁的摘要徽章顯示「4 小時 完成」。
- **公告只搬了學分上限，沒有搬申報條件。** iiCME 聲明的兩句是 `a maximum of 5.0 AMA PRA Category 1 Credits™` 與 `Physicians should only claim credit commensurate with the extent of their participation in the activity.`；公告寫的是 `up to 5.0 AMA PRA Category 1 Credits™`，後面那句條件不在公告裡。
- **公告的範圍句只覆蓋課程頁三項中的一項。** 公告寫課程 `focus on non-clinical administrative tasks`；以課名論，行政任務是四門課中的第 3 門一門，而 grow.google 的常見問答自己給的範圍是三項（non-clinical administrative tasks、patient communication、professional development）。
- **課綱依據是草案，而「草案與定稿方向一致」是 Google 自評。** 公告的括號句寫 draft versions `reflected the overall direction of the final competencies`，沒有附上定稿版本的連結，也沒有逐項比對。
- **公告沒有出現的詞。** 公告正文共 5,395 字元，逐詞計數後 `$`、`price`、`cost`、`Coursera`、`iiCME`、`ACCME` 的命中數皆為 0。價格、託管平台與實際授予學分的認證機構，公告一個字都沒提。
- **開發者專科背景在同一頁有兩份不同清單。** grow.google 一處寫 `backgrounds spanning internal medicine, pediatrics, critical care medicine, emergency medicine, and public health`（五項，與公告一致），另一處寫 `backgrounds in internal medicine, pediatrics, emergency medicine, and intensive care`（四項，public health 不在其中，critical care medicine 改寫為 intensive care）。
- **課名在兩頁之間也有出入。** 第 3 門課在 grow.google 的課程區塊寫作 `Optimize Healthcare Administration Tasks with AI`，而同頁常見問答與 Coursera 都寫 `Optimize Healthcare Administrative Tasks with AI`；第 4 門課在 Coursera 帶有結尾的 `with AI`，在 grow.google 的課程區塊沒有。
- **價格只寫在課程頁，而兩種取用敘述未被說明如何併存。** grow.google 寫美加地區每月 49 美元訂閱、各國價格可能不同；Coursera 頁的註冊按鈕文字是「免費註冊」，其結構化資料的 `offers` 類別為 `Subscription`；兩者如何併存，頁面未說明。
- **利益揭露用的詞，頁面上沒有定義。** Coursera 頁的財務揭露聲明寫 `All faculty, planners, reviewers, or staff report no relationships to disclose`，引號內的自述是未持有與 `ineligible companies` 的財務關係。joint provider 之一的 Google LLC 正是課程所教工具的製造商；`ineligible companies` 這個詞的定義不在三個頁面的任何一頁上。
- **三個頁面同源。** 實質內容都由 Google 提供，Coursera 僅為託管平台，唯一不出自 Google 的敘述是 iiCME 的認證聲明。公告引用的兩項外部統計（一份護理人力調查與一份 American Medical Association 的醫師態度報告），其原始數值未納入本文引述。
- **學分的三年有效期只寫在 Coursera 頁。** `This enduring material activity is valid from October 29, 2026 through October 29, 2029.` 這段出自 Coursera 頁的 iiCME 聲明，公告沒有提到到期日這件事。
- **Coursera 頁上的三個數字會變動。** 3,448 人已註冊、評分 4.8、12 則評論，為 2026-11-09 取頁當下的值。

## 本書庫解讀（評論）

- **把可核對的部分抽出來，這是一張範圍收得很緊的入門課。** 四門課、約五小時、無先備知識要求、線上自學、三年有效期、明文排除臨床診斷與醫療決策。這些條件加起來，它要解的是「全院人員對 AI 的基本認識」這一層，不是臨床決策支援的使用訓練。把它放在院內訓練地圖的入門格，位置是清楚的。
- **「經領先組織審閱」目前是一句不可核對的話。** 這不是說審閱沒有發生，而是說三個官方頁面都沒有提供任何可以讓外部確認的線索：沒有組織名稱、沒有審閱範圍、沒有審閱時間、沒有審閱結論的任何形式。相對地，公告願意具名的是四所採用這張認證的學校——採用與審閱是兩件事，而被放進摘要句、最具分量的那個形容詞落在後者。
- **課綱依據是 AAMC 能力指標的草案，而「草案與定稿方向一致」是自評。** 公告的坦白值得肯定：它主動寫明當時用的是 draft versions。但它緊接著用一句括號宣稱草案反映了最終能力指標的整體方向，這句話沒有附上定稿版本的連結，也沒有逐項比對。對要把這張認證納入院內訓練的人來說，這一句決定了課綱是否仍與現行能力指標對得上，而它目前只有 Google 的說法。
- **時數與學分的落差需要使用者自己承擔。** AMA PRA Category 1 Credits™ 是以參與時數為基礎的制度，而這套課程在三個官方頁面上分別被描述為約四小時、未滿五小時、逐課加總五小時。iiCME 的聲明已經先一步寫明「只能按實際參與程度申報」，等於把界定責任交回給申報者；公告轉述時只留下 `up to 5.0`。申報醫師若照上限填，風險由自己承擔。
- **「為醫療人員設計」與「不涵蓋臨床」兩句話要同時讀。** 課程頁的 `No.` 寫得清楚，這是一個負責任的範圍界定，而不是缺陷。值得指出的是公告的敘事重心：它談的是把時間還給病人、談病床邊的專注與照護的喜悅，而實際交付的是四門關於行政、衛教素材與個人進修的課。兩者不矛盾，但讀者若只看公告的敘事，容易把這張認證理解成一張「臨床 AI 使用」的憑證。
- **揭露聲明的涵蓋範圍，讀者無法在這三頁上判斷。** 一份由工具製造商共同提供、內容即為該製造商自家產品的繼續教育課程，其財務揭露聲明使用了 `ineligible companies` 這個詞而未加定義。要判斷這份揭露涵蓋到哪裡，讀者必須另行查閱 ACCME 對該詞的界定——這正是把判斷成本轉嫁給使用者的典型形式。本書庫不主張這份揭露不實，只指出它在這三個頁面上不可自證。
- **價格不在公告裡。** 課程頁寫美加地區每月 49 美元訂閱、各國價格可能不同，而公告全文沒有任何價格字樣。這對一篇以「減輕醫療人員負擔」為題的公告而言，是一個會影響讀者決策的欄位。

## 產業影響

- **對醫療機構的 AI 素養訓練規劃而言**，這張認證提供的是一份現成且門檻極低的入門教材：不需要先備知識、四門課、線上自學、附帶繼續教育學分。附學分是這類教材最容易通過院內審核的屬性，也是本則最值得台灣端注意的設計——國內醫事人員繼續教育有自己的學分體系，AMA PRA Category 1 Credits™ 並不互通，因此直接照搬的價值有限，可照搬的是結構。
- **對自建院內教材的單位而言**，本則抓到的幾個欄位剛好是最容易留白的幾個：審閱者是否具名、總時數與學分如何對應、課綱依據的版本與日期、講師與工具供應商的利益關係。這四項在本則都出現了不同程度的留白，而它們恰好是日後被稽核時最先被問到的四項。
- **對臨床人員個人進修而言**，這張認證在履歷上能支撐的是「具備非臨床場景的生成式 AI 操作素養」，不是臨床 AI 的使用資格。課程頁自己用 `No.` 把這條線畫出來了，轉述時不應該抹掉。
- **對這類教材的供應鏈形態而言**，本則呈現的分工是：模型供應商出內容、第三方認證機構出學分、通用學習平台出通路。這條鏈上沒有任何一方單獨對「這套教材是否適合臨床情境」負責，而醫療機構採購時通常只看到最前端的品牌。

## 與書庫其他文章的關係

同一個官方部落格頻道相隔六天的兩則發布，把「誰來判斷模型輸出好不好」推給了相反的兩邊：該則的白皮書明寫量化門檻由各產品團隊在自家 phase-gate 自訂、不設通用數值切點，本則的課程則教臨床人員 evaluate model outputs with your clinical judgment，等於把同一個判斷責任交給第一線使用者，而兩則都沒有給出任何一個可操作的門檻: [Google 健康 AI 評估框架：三個領域、三種方法、17 個維度](2026-11-05-google-health-ai-evaluation-framework.md)

同一家公司面向醫療的兩條路線：該則是把開放權重模型送進資源有限地區的落地合作，本則是給臨床人員的 AI 素養課程與繼續教育學分。兩則並讀可以看出 Google 在醫療 AI 上同時投入工具端與人員端: [MedGemma：開放權重醫療模型，四國五個落地合作案](2026-10-08-medgemma-global-deployment-claims.md)

兩則的數字都只給了上限：該則的 90% 是前七名清單的命中率、排第一只有 56%，本則的 5.0 個繼續教育學分同樣是 maximum，而課程頁自己寫醫師只能按實際參與程度申報，公告轉述時兩句都只搬了前半: [AMIE 看診前先問病史：98 人的 Lancet 可行性研究](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

## 實務的啟發

- **把它放進院內訓練地圖之前，先確認它補的是哪一格。** 本則課程的邊界句 `It does not cover clinical diagnosis, medical decision-making, or treatment recommendations` 已經把位置界定清楚：它是通識層，不是臨床應用層。院內若同時需要兩層，這張認證只能解決其中一層，另一層仍需自建或另尋教材。
- **把課程的排除項抄進院內教材說明。** 上述那一句比它的四條學習目標更值得被轉達給受訓人員。院內推廣 AI 素養訓練時，最容易產生的誤解不是「學了什麼」，而是「以為學完就可以用在哪裡」。
- **繼續教育學分要分開看「上限」與「申報條件」。** 看到 `up to N credits` 時，往下找授予機構的那段聲明，裡面通常會寫申報條件（本則是 `commensurate with the extent of their participation`）。把上限寫進院內公告而漏掉條件，風險會落在實際申報的醫師身上。
- **把「經某某審閱」當成一個待填欄位，而不是一個形容詞。** 評估任何外部 AI 訓練教材時，直接向供應方索取三件事：審閱組織的名稱、審閱涵蓋的課綱版本與日期、審閱結論的形式（是否出具書面意見）。拿不到這三項，就把這句話從採用理由中移除，而不是打折採信。
- **工具廠商自製的訓練教材，先確認它教的是概念還是產品。** 本則三個頁面都把技能描述為可跨工具使用，而實際使用的工具是同一家的三個產品。判斷方式很直接：把課程目標逐條拿掉產品名，看還剩下多少可遷移的內容；剩不下來的部分，就要同時規劃院內實際採用工具的對應訓練。
- **自建院內 AI 訓練時，把課綱依據的版本與日期設成必填。** 本則的課綱參考的是 AAMC 能力指標的草案，這件事公告有寫；若院內教材不記錄依據版本，幾年後連「當時依據什麼」都無從回答。

## 後續追蹤

- 是否會有任何一個「審閱組織」被具名，或在後續的課程頁更新中補上審閱範圍與日期。
- AAMC 的 Artificial Intelligence Competencies Across the Learning Curriculum 定稿版本與課綱所依據的草案之間，是否會出現由 Google 或第三方做的逐項比對。
- 三個官方頁面上的課程時數說法（約四小時／未滿五小時／逐課加總五小時）是否會被統一，以及統一後與 5.0 學分上限的對應關係。
- 這張認證是否會延伸出涵蓋臨床決策的後續課程；若有，其審閱與驗證標準是否會比本則嚴格。
- 其他前沿模型供應商是否跟進推出附帶繼續教育學分的醫療 AI 訓練，以及是否出現由醫學會或醫學院主導、而非由模型供應商主導的對照版本。
- 台灣的醫事人員繼續教育主管單位或醫學會，是否就廠商自製 AI 訓練教材的採認提出說明。

## References

- `blog` — Equipping healthcare professionals with practical AI skills（Google 官方部落格，作者 Michael Howell, Chief Health Officer，2026-10-29）  
  <https://blog.google/innovation-and-ai/technology/health/google-ai-for-healthcare-professionals-certificate/>
- `program` — AI for Healthcare Professionals（Google 官方課程說明頁，含課程清單、常見問答、價格與認證說明）  
  <https://grow.google/healthcare-professionals/>
- `coursera` — Google AI for Healthcare Professionals 專項課程（Coursera 課程頁，含四門課的逐課時數、iiCME 與 ACCME 認證聲明、學分上限與申報條件、有效期與財務揭露聲明）  
  <https://www.coursera.org/specializations/google-ai-for-healthcare-professionals>

[Home](../) · [Industry Watch](./)
