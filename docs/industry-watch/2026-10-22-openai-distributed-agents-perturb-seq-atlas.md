---
title: "OpenAI 公布以 AI 代理群解讀全腦 Perturb-seq 圖譜：公告寫「引用逾 700 篇」，它所連結的論文寫的是「711 倍」"
category: industry-watch
date: 2026-10-22
updated: 2026-10-22
tags: [OpenAI, PerturbAI, Scripps-Research, GPT-Rosalind, multi-agent, Perturb-seq, CRISPR, research-workflow, literature-grounding, preprint, hypothesis-generation]
catalog_id: "openai:distributed-agents-brain-perturb-seq-atlas-2026-10-21"
editors:
  - "Clarence"
status: published
evidence_reviewed: true
source:
  orgs:
    - "OpenAI"
    - "PerturbAI"
    - "Scripps Research"
  event: "發布公告 Using thousands of AI agents to uncover new leads in biological data，說明以分散式 AI 代理解讀一份全腦 Perturb-seq 圖譜，並連結同組作者的 bioRxiv 預印本"
  event_date: "2026-10-21"
  official_url: "https://openai.com/index/scaling-ai-research-for-complex-biological-data/"
related_articles:
  - path: "2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md"
    relation: "該則預測每個 agentic workflow 的推論成本到 2028 年增加逾五倍，理由是更複雜的工作流程用掉遠多於聊天機器人的 token，但全文沒有給任何絕對量；本則正好提供了一組被量出來的絕對量 —— 1,946 個代理、39,185 次論文閱讀、16,445 筆保留引用，而且論文把「單一代理」與「分散代理」在同樣模型與工具下直接對跑，是少見把成本與成效放在同一張表上的公開材料"
  - path: "2026-10-20-google-amie-lancet-primary-care-feasibility.md"
    relation: "兩則是同一種改寫手法的兩個樣本：官方部落格給出一個百分比，而它的分母只存在於被連結的論文裡；該則的 90% 實為前七名清單命中率，本則的 75% 實為 20 組配對報告、每組三位評審共 60 次判斷中的 45 次，兩則並讀可以看出「官方頁有連結到論文」與「官方頁保留了限定條件」是兩回事"
  - path: "../ai-basics/multi-agent-llm.md"
    relation: "該篇說明 ReAct 迴圈、工具呼叫與多代理協作的機制，而本則的架構恰好是其中最單純的一種拓撲 —— 一個擾動配一個代理、代理之間不對話，合成留到最後一層；把兩篇並讀可以看出「多代理」的效益未必來自互相辯論，也可能只來自不讓單一上下文被塞爆"
refs:
  pr:
    title: "OpenAI：Using thousands of AI agents to uncover new leads in biological data（官方公告）"
    url: "https://openai.com/index/scaling-ai-research-for-complex-biological-data/"
  paper:
    title: "Sun et al.：Distributed AI agents enable comprehensive discovery of biological insights at scale（bioRxiv 預印本，doi:10.64898/2026.10.15.759436）"
    url: "https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1"
  paperfull:
    title: "同上，全文版（Results、Discussion 與圖說）"
    url: "https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full"
  atlas:
    title: "被解讀的原始資料集：Shi et al., Genome-scale functional mapping of the mammalian whole brain with in vivo Perturb-seq（bioRxiv 2026.03.16.711480，Posted March 18, 2026）"
    url: "https://www.biorxiv.org/content/10.64898/2026.03.16.711480v1"
  code:
    title: "公告所稱可取用的 reasoning atlas 程式碼庫（GitHub，jinlabneurogenomics/distributed_agent）"
    url: "https://github.com/jinlabneurogenomics/distributed_agent"
  data:
    title: "公告所連結的資料集（Hugging Face，perturbai/wholebrain_crispr_atlas）"
    url: "https://huggingface.co/datasets/perturbai/wholebrain_crispr_atlas"
---

[Home](../) · [Industry Watch](./)

# OpenAI 公布以 AI 代理群解讀全腦 Perturb-seq 圖譜：公告寫「引用逾 700 篇」，它所連結的論文寫的是「711 倍」

## 來源

- 組織：OpenAI、PerturbAI、Scripps Research
- 事件：發布公告 `Using thousands of AI agents to uncover new leads in biological data`，說明以分散式 AI 代理解讀一份全腦 Perturb-seq 圖譜
- 日期：2026-10-21（頁面可見標示）
- 官方入口：<https://openai.com/index/scaling-ai-research-for-complex-biological-data/>
- 本則**非單源**：公告連結的 bioRxiv 預印本可完整取用並逐項回查。但兩者並非互相獨立的佐證 —— 預印本的作者群包含六位 OpenAI 員工與兩位 PerturbAI 員工，其中兩位是 PerturbAI 共同創辦人，而被解讀的那份原始圖譜也是同一個實驗室先前的研究 [(ref: paper)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1)

**編輯：** Clarence

OpenAI 在 2026-10-21 公布與 PerturbAI、Scripps Research 合作的一項工作：把一份涵蓋數百萬個小鼠腦細胞的全腦 Perturb-seq 圖譜（以 CRISPR 大規模擾動基因並逐細胞量測轉錄反應的資料集）拆成一個基因擾動配一個 AI 代理，讓代理各自分析資料、檢索文獻並提出解釋，再把報告合成為一份 reasoning atlas [(ref: pr)](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)。

公告頁全文只出現一個百分比，而三個被摘出來的量化說法回到它自己連結的預印本後，限定條件都在原處：「分散代理引用逾 700 篇參考文獻」在論文裡寫的是「比單一代理多 711 倍」（論文摘要另以 `100s times more` 佐證這是倍數而非筆數）；「人類專家偏好 75%」的分母是 20 組配對報告、每組三位評審共 60 次判斷；而公告開場用來起興的「阿茲海默症與帕金森氏症」，`Alzheimer` 一詞在預印本全文出現 0 次。

## 背景

這一則要讀懂，需要知道三份文件的先後與彼此關係 —— 它們都由同一批人產出，而公告只點名了其中一份。

- 2026-03-18，Scripps Research 的 Jin 實驗室貼出全腦 in vivo Perturb-seq 圖譜預印本 `Genome-scale functional mapping of the mammalian whole brain with in vivo Perturb-seq`，涵蓋近兩千個基因擾動，作者群與本次方法論預印本高度重疊 [(ref: atlas)](https://www.biorxiv.org/content/10.64898/2026.03.16.711480v1)。本次被 AI 代理解讀的就是這份資料，而論文在 Results 開頭自述 `We recently reported a whole-brain in vivo Perturb-seq study`，並說明即使有統計、基因體學與神經科學的專家團隊，資料中仍有大量生物學 `remained under-interpreted` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。亦即「人類分析」這一側的基準，是本次評估者自己先前的工作。
- 2026-10-16，方法論預印本貼上 bioRxiv：`Distributed AI agents enable comprehensive discovery of biological insights at scale`，頁面標示 `Posted October 16, 2026`，並載明 `This article is a preprint and has not been certified by peer review` [(ref: paper)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1)。
- 2026-10-21，OpenAI 公告頁上線（頁面可見標示 October 21, 2026；該頁沒有 JSON-LD、沒有日期 meta、也沒有指向本則的 `<time>` 標籤，日期即以頁面可見標示為準，未推斷）[(ref: pr)](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)。公告頁的「Read the paper」與「GPT-Rosalind」兩個連結指向同一份預印本，而公告正文從頭到尾沒有出現 `preprint` 或 `peer` 這兩個字。

## 事實（可核對）

以下左側為公告頁的說法，右側為它所連結的預印本在同一件事上的寫法。

- **代理數量** — 公告標題與內文用 `thousands of AI agents`；預印本 Results 寫的是 `We ran 1,946 AI agents independently and in parallel`，圖 1A 圖說同樣是 1,946 個擾動配 1,946 個代理 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。預印本摘要本身也用了 `thousands of parallel agents` 的概括寫法，因此這個取整並非公告獨有，但公開材料裡唯一的確切數字是 1,946。

- **文獻引用量** — 公告寫 `the single agent searched less of the literature, citing only 11 references at the largest workload, while the distributed agents cited more than 700 references`，並以同樣的「700 對 11」做成一句獨立的強調句 [(ref: pr)](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)。預印本在同一個實驗寫的是 `At 893 perturbations, the single agent cited 11 references, while the distributed agents retained 711x more references`，摘要則寫 `retrieving 100s times more references than single-agent mode` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。兩處都指向倍數讀法，而 711 倍乘上 11 約為七千八百餘筆。公告把一個倍數寫成了一個絕對筆數，使讀者看到的對比從 711 倍縮為約 64 倍。本文不主張哪一邊是筆誤，只陳述兩份文件在同一個數字上不一致。

- **專家偏好 75%** — 公告寫 `In blinded comparisons, human experts preferred distributed-agent reports over single-agent reports 75% of the time`，未給人數或次數 [(ref: pr)](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)。預印本：評估者為 30 位 doctoral-level biological experts，每人評六份報告；配對比較另行設計，`20 report pairs assessed by three experts each`，結果為 `distributed-agent interpretations were preferred in 45 of 60 judgments (75%), single-agent interpretations in 10 (16.7%), and five were ties (8.3%)` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。亦即 75% 的分母是 60 次判斷，而這 60 次來自 20 組報告，不是 60 組獨立比較。

- **「與人類專家一致」** — 公告寫 `Their assessments of novelty and scientific value also aligned with judgments from blinded human experts`，未給任何數值 [(ref: pr)](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)。預印本給的是 Spearman rho（等級相關係數）：novelty rho = 0.61（P = 2.7×10⁻⁴）、follow-up priority rho = 0.56、evidential support rho = 0.49 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。三個係數都落在中等相關的範圍。

- **文獻比對結果** — 公告沒有提及代理的判讀與既有文獻不合的比例。預印本：1,519 筆高信心發現中，`420 were flagged agree (27.6%), 636 inferred (41.9%), 101 disagree (6.6%), and 362 lacked retrieved precedent (23.8%)`；整體代理共讀了 39,185 篇論文、保留 16,445 筆引用，每個擾動約讀 19 篇、引 8 篇 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。預印本並自行加註 `'No literature' denotes a retrieval gap, not proof that no relevant study exists`。

- **預測保留集的表現** — 公告只寫代理 `predicted held-out perturbation effects`（見預印本摘要同句），沒有給任何準確率。預印本圖 3C 把 272 個保留擾動分成四類：`correctly predicted responses (n = 59), missed responses (n = 41), overcalled responses (n = 30), and correctly predicted non-responses (n = 142)` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。實際有反應的 100 個擾動中抓到 59 個，整體分類正確 201/272。

- **速度與對照** — 公告寫分析在 `just 32 minutes` 內完成，並稱 `The research team estimated that comparable human analysis ... would take months to a year`。預印本的對應句是 `Parallel execution completed the analysis in 32 minutes; illustrative human-effort estimates placed comparable serial analysis and literature review on the scale of months to a year` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。32 分鐘是量到的，`months to a year` 是示意性的估計，兩者不是同一種數字；公告用 `estimated` 保留了這一點，但開場的 `in minutes instead of months` 一句沒有。

- **兩則被舉例的發現** — 公告以 Tsc1／Tsc2 與 DCTN1 兩例說明代理找到的線索。回到預印本：Tsc 一例的原文是 `the Tsc2 perturbation yielding 83 significant DEGs in cerebellar GABAergic neurons`，Tsc1 幾無影響，統計門檻為 FDR < 0.1，而這一筆**正是被標為 no-literature flag 的發現**，預印本寫 `marks a potential knowledge gap as these relationships remain hypotheses for investigations`；DCTN1 一例在預印本的呈現是專家給的 follow-up priority 為 4.3/5，並以 `raises the possibility`、`could be further investigated` 描述 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。公告為這兩例各加上了一段疾病脈絡（結節性硬化症、Perry syndrome），而 `tuberous` 與 `TSC` 在預印本全文出現 0 次，`Perry syndrome` 僅出現 1 次且是在參考文獻 35 的篇名裡。

- **宣稱涵蓋到哪裡** — 公告開場問的是 `What if scientists could uncover new clues about Alzheimer's and Parkinson's in minutes instead of months?`，但 `Alzheimer` 在公告全文只出現這一次，在預印本全文出現 0 次；兩個被舉例的疾病關聯是結節性硬化症與 Perry syndrome，後者在公告中被描述為 `a neurodegenerative disease with Parkinson-like symptoms`。亦即帕金森氏症的連結是透過一個罕見症候群的症狀相似性，阿茲海默症則沒有對應的下文。

- **公告沒有宣稱的事** — 公告全文 `clinical`、`patient`、`FDA`、`validat`、`accuracy`、`sensitivity`、`specificity` 皆出現 0 次，也沒有註腳（`<sup>` 元素 0 個）。它沒有把這項工作說成臨床工具，也沒有宣稱任何假說已被驗證，並寫明 `Scientists remain at the center of discovery` [(ref: pr)](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)。

- **資料與程式碼** — 公告稱 reasoning atlas 已可取用，連結指向 GitHub 的 `jinlabneurogenomics/distributed_agent` [(ref: code)](https://github.com/jinlabneurogenomics/distributed_agent)，資料集連結指向 Hugging Face 的 `perturbai/wholebrain_crispr_atlas` [(ref: data)](https://huggingface.co/datasets/perturbai/wholebrain_crispr_atlas)。預印本採 CC-BY 4.0 授權。

- **模型與洩漏控制** — 預印本寫明使用 `GPT-Rosalind-5.5`，`whose stated knowledge cutoff was December 2025, preceding the release of the source manuscript in March 2026`，且原始論文與其結論在實驗中被扣住不給代理 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。公告只寫 `GPT-Rosalind`，未提版本、知識截止日或這項控制設計。

- **論文自列的限制** — 預印本 Discussion 寫 `matched comparisons are needed to determine how much of this scaling advantage generalizes`，以及 `Evaluation on independent datasets and prospective experiments will establish how well the framework generalizes and improves experimental prioritization, as biological interpretations remain challenging to assess systematically` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。這三句在公告頁沒有對應。

## 本書庫解讀（評論）

以下為本書庫的判斷，非來源結論。

- **這一則的落差型態與前幾則不同，值得單獨記下來。** 本書庫近期處理的幾則廠商宣傳，問題多半是「限定條件被留在原處」—— 數字本身對，但分母、對照組或受測對象被省略。本則除了同樣的省略（75%、32 分鐘、一致性）之外，還多了一處兩份文件**互相矛盾**的數字：公告的「逾 700 篇」與論文的「711 倍」不可能同時成立。這類矛盾比省略更容易被下游複述放大，因為它看起來是個具體、可引用的絕對數，不像倍數那樣會讓人追問被乘數。

- **被省略的那幾個數字，恰好是外部唯一能用來判斷門檻的東西。** 只說「與專家一致」而不說 rho ≈ 0.49 到 0.61，讀者無從判斷這是「可以直接採信代理排序」還是「排序只堪當粗篩」；只說「預測了保留集的擾動效應」而不說 100 個真實有反應的擾動抓到 59 個，讀者也無從判斷這個模組該放在工作流程的哪一段。這兩個數字都在公開的預印本裡，公告沒有寫錯，是沒有寫。

- **論文對自己的誠實程度，明顯高於公告。** `'No literature' denotes a retrieval gap, not proof that no relevant study exists`、`these relationships remain hypotheses for investigations`、`illustrative human-effort estimates`、以及 Discussion 那三句待驗證聲明，都是作者自己加的界線。值得注意的是被公告當成亮點的 Tsc1／Tsc2 發現，在論文裡的身分是一個**檢索不到文獻**的旗標；換句話說，「文獻裡沒有」被公告讀成了「代理發現了新東西」，而論文明確說這兩者不等價。

- **27.6% 的 `agree` 比例，可能才是這份工作最該被引用的數字。** 1,519 筆高信心發現裡，只有約四分之一能與既有文獻直接對上，41.9% 屬於推論，23.8% 檢索不到任何前例。這不是負面結果 —— 一個只會重述文獻的系統沒有用 —— 但它界定了下游該怎麼用：這是一台產生待驗證假說的機器，不是一台產生結論的機器，而 6.6% 的 `disagree` 提醒了代理的推論也會與文獻衝突。

- **評估的獨立性有邊界。** 被當作比較基準的「人類分析」來自同一個實驗室先前的圖譜論文，30 位評審的招募與利益關係在預印本可見資訊中未說明，而作者群中有六位 OpenAI 員工、兩位 PerturbAI 員工（含兩位共同創辦人）。這不使結果無效，但「代理重現了人類分析」這句話的強度，取決於那份人類分析是誰做的 —— 而公告沒有提。

- **醫療橋接：這套架構真正的醫療意義不在發現，而在它示範了一種可稽核的代理分工。** 醫療 AI 近一年快速從單次推論走向多步驟執行，而本則提供了一個罕見的公開樣本：每個代理只負責一個明確界定的單位（一個基因擾動），產出都掛著可追溯的文獻證據，最後再由一層合成排序成待辦佇列。把這個形狀換到醫療場景，等價於「一位病人一份檢查配一個代理、每條結論都要掛回它所依據的影像切面或檢驗值、再由排序層產生待覆核清單」。更關鍵的是，這份工作把「代理的排序」與「專家的評分」放在同一張表上比對（rho 與偏好次數），而這正是本書庫收錄的多數醫療代理論文最缺的一步 —— 多半只報終端準確率，不報人類會不會同意它的優先順序。本則同時也示範了相反的教訓：一份自列限制相當完整的研究，在轉成公司公告之後仍然掉了分母與對照；醫療端引用任何一則「AI 加速研究」的公司公告時，回到它所連結的論文對一次數字，是成本很低而回報很高的動作。

## 產業／生態影響

- **研究工作流程的瓶頸被重新定義。** 預印本把問題陳述為 `High-content perturbation screens shift the bottleneck from measuring phenotypes to interpreting them` [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。若這個判斷成立，大型生物資料集的價值將越來越取決於解讀層的工具，而非產生資料的能力本身 —— 這對手握大量既有資料而解讀人力有限的醫學中心同樣適用。

- **模型供應商開始以「科學代理」而非「聊天助理」定位自己。** 本則的 GPT-Rosalind 是以科學為名的模型線，公告的敘事主體是研究流程而非產品功能。對醫療 AI 採購端而言，這意味著未來評估對象可能不再是單一模型的分數，而是一整套代理編排的產出品質與可追溯性。

- **成本結構被攤在陽光下，但沒有被標價。** 1,946 個代理、39,185 次論文閱讀、16,445 筆引用是公開材料裡少見的絕對用量數字，然而公告與論文都沒有給這次執行的推論費用。這使本則成為「用量可見、單價不可見」的樣本。

- **預印本與公司公告的時間差值得留意。** 預印本 2026-10-16 貼出，公告 2026-10-21 發布，中間五天內沒有同儕審查程序能完成。公告未使用 `preprint` 一詞，而 bioRxiv 頁面首屏就寫著未經同儕審查認證。對於以公司公告為資訊來源的讀者，這個狀態標示的落差會直接影響他們對證據等級的判斷。

## 與書庫其他文章的關係

該則預測每個 agentic workflow 的推論成本到 2028 年增加逾五倍，理由是更複雜的工作流程用掉遠多於聊天機器人的 token，但全文沒有給任何絕對量；本則正好提供了一組被量出來的絕對量 —— 1,946 個代理、39,185 次論文閱讀、16,445 筆保留引用，而且論文把「單一代理」與「分散代理」在同樣模型與工具下直接對跑，是少見把成本與成效放在同一張表上的公開材料: [Gartner 預測 agentic workflow 的推論成本到 2028 年增加逾五倍，並提出 Inference Paradox](2026-10-21-gartner-inference-paradox-agentic-workflow-cost.md)

兩則是同一種改寫手法的兩個樣本：官方部落格給出一個百分比，而它的分母只存在於被連結的論文裡；該則的 90% 實為前七名清單命中率，本則的 75% 實為 20 組配對報告、每組三位評審共 60 次判斷中的 45 次，兩則並讀可以看出「官方頁有連結到論文」與「官方頁保留了限定條件」是兩回事: [Google 宣傳 AMIE 的 Lancet 研究：「鑑別診斷與醫師最終診斷相符 90%」是前七名清單的命中率，同一天更新的自家研究部落格寫著排第一名的只有 56%](2026-10-20-google-amie-lancet-primary-care-feasibility.md)

該篇說明 ReAct 迴圈、工具呼叫與多代理協作的機制，而本則的架構恰好是其中最單純的一種拓撲 —— 一個擾動配一個代理、代理之間不對話，合成留到最後一層；把兩篇並讀可以看出「多代理」的效益未必來自互相辯論，也可能只來自不讓單一上下文被塞爆: [LLM 多代理系統：從 ReAct 到可對話協作](../ai-basics/multi-agent-llm.md)

## 實務的啟發

- **引用本則時，把倍數與筆數分開。** 若要引用文獻覆蓋度的對比，建議直接引用預印本的 `711x more references`（基準為單一代理在 893 個擾動下的 11 筆），而不要引用公告的「逾 700 篇」—— 後者與它自己的出處不一致，且會讓對比看起來只有約 64 倍。

- **把「分母在哪裡」列為引用公司公告的固定檢查項。** 本則的 75%（45/60，來自 20 組配對）、前一則 Google AMIE 的 90%（前七名命中率）是同一類問題。實務上可以簡化成一個動作：公司公告裡的每一個百分比，都回到它連結的論文找出分子與分母，找不到就不要單獨引用那個百分比。

- **評估研究型 AI 工具時，問「它的 agree 比例是多少」。** 本則提供了一個可借用的指標組：代理產出中能與既有文獻直接對上的比例、屬於推論的比例、檢索不到前例的比例、以及與文獻衝突的比例。這四個數字合起來描述的是「這台機器產出的是結論還是假說」，而這決定了它該被放在工作流程的哪一段、需要多少人力覆核。

- **若要在醫療資料上複製這個架構，先確定每個代理的工作單位是可驗證的。** 本則之所以能把產出掛回證據，前提是「一個基因擾動」是一個邊界清楚、可獨立評分的單位。醫療場景裡對應的單位（一份報告、一個病灶、一次就診）邊界往往沒那麼乾淨，而單位切不乾淨，後面的排序與覆核佇列就無從驗收。

- **把「專家排序一致性」與準確率並列寫進驗收標準。** 本則用 Spearman rho 與配對偏好次數量了一件多數醫療代理研究沒量的事：臨床人員會不會同意這套系統的優先順序。一套排序正確但準確率普通的分流工具，和一套準確率高但排序與臨床直覺相反的工具，在科室裡的命運完全不同。

## 後續追蹤

- 預印本是否會進入同儕審查並刊出；若刊出，`711x` 與公告的「逾 700 篇」何者會被保留，是判斷這處不一致屬於筆誤或屬於轉述失真的直接指標 [(ref: paper)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1)。
- 預印本自列的待驗證項目 —— 在獨立資料集上的評估、前瞻性實驗、以及 matched comparisons —— 是否出現後續成果。這三項決定了本則能否從方法示範升級為可採信的流程工具 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。
- 代理提出的兩個假說（Tsc2 在 cerebellar GABAergic neurons 的選擇性效應、DCTN1 擾動與膽固醇合成的關聯）是否有實驗驗證發表。這是本則唯一能被真正驗收的終點。
- 是否出現以同一架構處理醫療資料的公開工作，以及它如何處理「工作單位切分」與「人類覆核佇列」這兩件事。
- 是否有第三方在相同資料集上重跑並報出不同結果。程式碼與資料集都已公開 [(ref: code)](https://github.com/jinlabneurogenomics/distributed_agent) [(ref: data)](https://huggingface.co/datasets/perturbai/wholebrain_crispr_atlas)，重現門檻低於多數同類宣稱。
- **引用本則時的提醒** — 這份工作的架構可以引用，公告頁的三個數字則請連同限定條件一起帶：「逾 700 篇」與出處的「711 倍」不一致，「75%」的分母是 20 組配對共 60 次判斷，「32 分鐘」的對照組 `months to a year` 是示意性估計而非量測值。另外，公告沒有寫的兩個數字 —— 保留集 100 個真實有反應的擾動中抓到 59 個、1,519 筆高信心發現中僅 27.6% 能與既有文獻直接對上 —— 才是判斷這套系統該被放在哪一段流程的依據 [(ref: paperfull)](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)。

## References

- `pr` — OpenAI，[Using thousands of AI agents to uncover new leads in biological data](https://openai.com/index/scaling-ai-research-for-complex-biological-data/)（官方公告，頁面可見標示 October 21, 2026；該頁無 JSON-LD、無日期 meta、無指向本則的 `<time>` 標籤）。底 URL：`https://openai.com/news/`
- `paper` — Sun A, Park JJ, DeTomaso D, Kim S, Liu A, Shringarpure S, Kim K, Thompson PC, Shi T, Wang Y, Mukamel EA, Zheng GXY, Jiao YJ, Jin X，[Distributed AI agents enable comprehensive discovery of biological insights at scale](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1)（bioRxiv 預印本，doi:10.64898/2026.10.15.759436，Posted October 16, 2026，CC-BY 4.0，未經同儕審查）。底 URL：`https://www.biorxiv.org/`
- `paperfull` — 同上，[全文版](https://www.biorxiv.org/content/10.64898/2026.10.15.759436v1.full)（本文引用的 Results、Discussion 與圖說文字出處）。底 URL：`https://www.biorxiv.org/`
- `atlas` — Shi T 等，[Genome-scale functional mapping of the mammalian whole brain with in vivo Perturb-seq](https://www.biorxiv.org/content/10.64898/2026.03.16.711480v1)（bioRxiv 2026.03.16.711480，Posted March 18, 2026；本次被解讀的原始資料集與其論文）。底 URL：`https://www.biorxiv.org/`
- `code` — [jinlabneurogenomics/distributed_agent](https://github.com/jinlabneurogenomics/distributed_agent)（公告所連結的 reasoning atlas 程式碼庫）。底 URL：`https://github.com/`
- `data` — [perturbai/wholebrain_crispr_atlas](https://huggingface.co/datasets/perturbai/wholebrain_crispr_atlas)（公告所連結的資料集）。底 URL：`https://huggingface.co/`

[Home](../) · [Industry Watch](./)
