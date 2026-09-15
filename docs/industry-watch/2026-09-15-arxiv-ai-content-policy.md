---
title: "arXiv 收緊 AI 生成內容政策：幻覺引用等可致一年禁投"
category: industry-watch
date: 2026-09-15
updated: 2026-09-15
tags: [arXiv, generative-AI, research-integrity, citations, moderation]
catalog_id: "arxiv:genai-unchecked-llm-penalty-2026-05"
editors:
  - "Curitis"
source:
  orgs:
    - "arXiv"
  event: "Clarified penalties for unchecked LLM-generated content (hallucinated refs / meta-comments)"
  event_date: "2026-05-15"
  official_url: "https://info.arxiv.org/help/moderation/index.html"
related_articles:
  - path: "../ai-basics/multi-agent-llm.md"
    relation: "LLM tooling responsibility background"
refs:
  arxiv_moderation_ai:
    title: "arXiv moderation — Policy for authors’ use of generative AI language tools"
    url: "https://info.arxiv.org/help/moderation/index.html"
  arxiv_blog_2023:
    title: "arXiv announces new policy on ChatGPT and similar tools"
    url: "https://blog.arxiv.org/2023/01/31/arxiv-announces-new-policy-on-chatgpt-and-similar-tools/"
  nature_2026:
    title: "Researchers who use hallucinated references to face arXiv ban"
    url: "https://www.nature.com/articles/d41586-026-01595-5"
  techcrunch_2026:
    title: "Research repository ArXiv will ban authors for a year if they let AI do all the work"
    url: "https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/"
  verge_2026:
    title: "ArXiv will ban researchers who upload papers full of AI slop"
    url: "https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers"
  ars_2026:
    title: "Send the arXiv AI-generated slop, get a yearlong vacation from submissions"
    url: "https://arstechnica.com/science/2026/05/preprint-server-arxiv-will-ban-submitters-of-ai-generated-hallucinations/"
status: published
skill_version: "write-industry-watch@2.2"
evidence_reviewed: true
---

**導覽：** [Home](../) · [Industry Watch](./)

# arXiv 收緊 AI 生成內容政策：幻覺引用等可致一年禁投

## 來源

- **組織**：arXiv（預印本庫）
- **事件**：澄清對「未核對 LLM 生成結果」的處罰——含幻覺引用、殘留對話／提示語等「無可辯駁證據」
- **日期**：約 2026-05-15 起由 CS 領域編輯負責人公開說明；媒體於 2026-05-16～19 跟進
- **官方入口**：[Content Moderation（含 generative AI 作者責任條款）](https://info.arxiv.org/help/moderation/index.html)
- **交叉報導**：[Nature](https://www.nature.com/articles/d41586-026-01595-5) · [TechCrunch](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/) · [The Verge](https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers) · [Ars Technica](https://arstechnica.com/science/2026/05/preprint-server-arxiv-will-ban-submitters-of-ai-generated-hallucinations/)

**編輯：** Curitis

2026 年 5 月，arXiv 方面公開澄清：若投稿出現「作者未檢查 LLM 生成結果」的硬證據（例如幻覺引用、未刪的模型對話殘句），作者可能面臨 **一年禁止投稿**，且之後須先經可靠同儕審查場域接受，才能再上 arXiv。

## 流程

1. **既有底線（官網）**：作者須對全文負責；生成式 AI 不得掛名作者；重大使用應依領域慣例揭露 [(ref: arxiv_moderation_ai)](https://info.arxiv.org/help/moderation/index.html) [(ref: arxiv_blog_2023)](https://blog.arxiv.org/2023/01/31/arxiv-announces-new-policy-on-chatgpt-and-similar-tools/)。
2. **處罰澄清（2026-05）**：CS 領域編輯負責人 Thomas Dietterich 於社群說明「無可辯駁證據 → 一年禁投 + 後續須先 peer-reviewed 接受」；多家媒體轉述同一組例證與流程 [(ref: techcrunch_2026)](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/) [(ref: verge_2026)](https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers) [(ref: nature_2026)](https://www.nature.com/articles/d41586-026-01595-5)。
3. **內部流程（媒體引述）**：主持人記錄問題 → Section Chair 確認後才處罰；可上訴 [(ref: techcrunch_2026)](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/) [(ref: verge_2026)](https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers)。

## 事實（可核對）

- arXiv 官網寫明：簽署為作者即對**全部內容**負責，無論內容如何生成；若生成式 AI 產出不當用語、抄襲、偏誤、錯誤、**不正確引用**或誤導內容並被納入文稿，責任在作者 [(ref: arxiv_moderation_ai)](https://info.arxiv.org/help/moderation/index.html)。
- 官網並要求依領域方法學慣例，**揭露**對文字生成式 AI 等複雜工具的重大使用；生成式 AI **不應**列為作者 [(ref: arxiv_moderation_ai)](https://info.arxiv.org/help/moderation/index.html)。
- 2026 年 5 月，媒體廣泛報導 arXiv 澄清處罰：投稿若含「作者未檢查 LLM 生成結果」的 **incontrovertible evidence**（例：hallucinated references；殘留如「here is a 200 word summary…」或「fill it in with the real numbers…」之類 meta-comments），處罰為 **1-year ban**，之後投稿須先被 reputable peer-reviewed venue 接受 [(ref: nature_2026)](https://www.nature.com/articles/d41586-026-01595-5) [(ref: techcrunch_2026)](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/) [(ref: verge_2026)](https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers)。
- 報導強調：**不是禁止使用 LLM**，而是禁止未核對就把生成結果貼進投稿 [(ref: techcrunch_2026)](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/)。
- TechCrunch／Verge 引述 Dietterich：此為 one-strike；須 moderator 記錄 + Section Chair 確認；可上訴 [(ref: techcrunch_2026)](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/) [(ref: verge_2026)](https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers)。

## 本書庫解讀（評論）

- **對醫療 AI 研究者**：本庫多篇筆記以 arXiv 為入口；幻覺引用與未刪提示語會直接傷害可信度，也觸及投稿資格風險。實務上應把「引用逐條點開驗證」當硬閘門，而非可選 polish。
- **政策邊界**：一年禁投的細節目前主要經編輯負責人公開說明與媒體交叉報導呈現；官網頁面仍以「作者責任／揭露／不得掛名 AI」為穩定條款。閱讀時宜同時看 [moderation 頁](https://info.arxiv.org/help/moderation/index.html) 與最新通告，勿把二手標題誇大成「全面禁用 AI 寫作」。
- **可執行性爭議**：外界有「受歡迎但難全面執法」的評論（例如高等教育媒體討論）；這屬評論層，不改變「有硬證據才重罰」的公開說法。

## 產業／學術生態影響

- 預印本仍是 CS／部分理工領域的主流通路；禁投一年會實質打斷曝光與社群回饋循環 [(ref: ars_2026)](https://arstechnica.com/science/2026/05/preprint-server-arxiv-will-ban-submitters-of-ai-generated-hallucinations/)。
- 與期刊／同儕審查端對 AI slop、假引用的壓力合流，預期會推高「可稽核寫作流程」（引用檢查、人審清單）的需求。

## 與書庫其他文章的關係

一句話敘述關係: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md) 討論 LLM 工具鏈與角色分工；本則補充預印本端對「未核對生成內容」的平台級後果。

## 實務的啟發

1. 投稿前強制：每筆引用可點開、作者／年份／題名一致；禁止保留聊天殘句。
2. 若使用生成式 AI 改寫或整理文獻，依領域慣例在方法／致謝揭露，且人為終審。
3. 共同作者掛名即共擔責任；掛名前確認自己核過引用與圖表數字。

## References

- **arxiv_moderation_ai** — [arXiv Content Moderation（generative AI 條款）](https://info.arxiv.org/help/moderation/index.html)
- **arxiv_blog_2023** — [arXiv announces new policy on ChatGPT and similar tools](https://blog.arxiv.org/2023/01/31/arxiv-announces-new-policy-on-chatgpt-and-similar-tools/)
- **nature_2026** — [Researchers who use hallucinated references to face arXiv ban](https://www.nature.com/articles/d41586-026-01595-5)
- **techcrunch_2026** — [TechCrunch 報導（2026-05-16）](https://techcrunch.com/2026/05/16/research-repository-arxiv-will-ban-authors-for-a-year-if-they-let-ai-do-all-the-work/)
- **verge_2026** — [The Verge 報導](https://www.theverge.com/science/931766/arxiv-ai-slop-ban-researchers)
- **ars_2026** — [Ars Technica 報導](https://arstechnica.com/science/2026/05/preprint-server-arxiv-will-ban-submitters-of-ai-generated-hallucinations/)

**導覽：** [Home](../) · [Industry Watch](./)
