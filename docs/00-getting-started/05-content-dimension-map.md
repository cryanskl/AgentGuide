# Content Dimension Map：内容维度补充地图

> 本文回答一个问题：**除了补齐已知的占位文档，AgentGuide 还能从哪些维度补充资料？**
>
> 它是 [仓库补洞地图](./04-repo-gap-map.md) 的续篇：gap-map 记录"哪些文件是占位"，本文记录"哪些维度整体缺失"。结论来自一次对全仓库 7 个板块的系统盘点，加上 5 个视角（技术趋势、读者画像、内容形态、求职市场、对标竞品）的交叉分析。

## 现状一句话

仓库的"厚"高度集中在五处：**面试题库**（34 个文件，含 824KB 面经整合）、**学习路线**（6 份 roadmap）、**上下文工程**（5 篇）、**评测体系**（3 篇大文档）、**Post-training**（346KB）。可补充的维度分为六类——其中优先级最高的一类不是"加新资料"，而是**把已经承诺、但实际不存在的东西补上**。

---

## 维度〇：先还债——承诺了但不存在的内容

这些不是新维度，是信任问题，读者点进去会直接落空：

| 问题 | 现状 | 建议 |
|:---|:---|:---|
| 可运行代码整体缺位 | README 快速开始引导运行 `examples/quickstart_agent.py` 和 `quickstart_rag_agent.py`，但 examples/ 下没有任何 `.py` 文件；8 个"简历级项目"共 30 处"即将推出"；projects/01-03 蓝图零代码；全仓库无 notebook | 先写出两个 quickstart 脚本（150-200 行、只依赖一个 API key、按 `trace-schema.json` 输出 JSONL）；projects/01-03 各交付蓝图里自定义的 M1 里程碑最小 demo |
| 14 篇 ~200 字节占位 stub 被当正式链接引用 | LangChain、多 Agent 框架、MCP、RAG 全链路、Transformer、Agent RL、手撕框架等——恰好是求职者最常被考的框架实操层 | 按 gap-map 的 P0/P1 顺序补齐；已被 README/路线图链接的优先 |
| LICENSE 缺失 | badge 宣称"完全开源"、FAQ Q5 让读者"详见 LICENSE"，文件不存在 | 补 LICENSE（可参考 JavaGuide：内容 CC BY-NC-SA 4.0 + 代码 MIT 双许可），同步修正 FAQ 表述 |
| 链接与元信息硬伤 | README 3 处链接文件名写错会 404；FAQ Q3 链到 208 字节 stub（真实内容在 07-career-transition）；CONTRIBUTING 留有占位邮箱和指向错误仓库的链接 | 一次性修复，并在 CI 加死链检查防止回归 |

---

## 维度一：技术内容——2025-2026 版图上的空白

对照当前技术格局，缺失或只有 stub 的方向（按岗位热度排序）。注意：上下文工程、评测、Post-training、Memory 已经很厚，不在此列。

| 优先级 | 方向 | 现状 | 为什么值得做 |
|:---:|:---|:---|:---|
| P0 | **Agentic RL**（RLVR、多轮工具调用 RL、环境工程） | `21-agent-reinforcement-learning.md` 是 209 字节 stub | 算法岗最热招聘方向；仓库自己的《AI可入方向》报告就把它列为 HC 热门；Post-training 大文档停在单轮偏好对齐，没讲 agent 场景的多轮 rollout、可验证奖励。可配一个用 verl/TRL 跑通 GRPO 训练 tool use 的小实验 |
| P0 | **Coding Agent 专题**（SWE-bench 拆解、repo map、编辑工具设计、测试反馈闭环） | 只有 Claude Code 使用指南和源码 playbook，无原理正文 | 落地最成功、岗位最多的 agent 品类；可借"从零写一个 mini coding agent"教程同时兑现 `22-build-your-agent-framework` stub |
| P0 | **Multi-Agent 框架 + A2A/ACP 协议** | `06-multi-agent-frameworks.md`、`07-agentscope.md` 双 stub；gap-map 规划的对比对象（Swarm、Magentic-One）已过时 | 2025 年格局已洗牌（AutoGen 并入 Microsoft Agent Framework、OpenAI Agents SDK 取代 Swarm、A2A 捐给 Linux 基金会），需按 2026 版图重写；A2A 中文深度材料稀缺 |
| P1 | **MCP 深水区 + Skills 生态** | `14-mcp-protocol.md` 仅 5KB 概览；Skills 只有面试向 playbook | spec 已大幅演进（Streamable HTTP、elicitation、官方 registry）；"自己写一个 MCP server"是门槛最低的简历项目；顺手补 MCP 安全（tool poisoning、confused deputy） |
| P1 | **Agent 安全攻防扩容** | 正文"安全"标签出现 43 次，深度供给只有一篇 5.3KB；`agent_security/` 论文目录仅 1 份 PDF 无 README | 已成独立岗位方向；可给 projects/01-03 各配一组注入攻击用例 + 防御验收标准，产出简历可写的安全消融 |
| P1 | **Deep Research / Agentic Search 系统** | 只有面试 playbook；README 承诺的"深度研究 Agent"项目是期货 | 最出圈的产品形态；在 Paper Agent 蓝图基础上加多源并行检索与报告合成，是最容易出简历成果的进阶项目 |
| P1 | **AgentOps 可观测性**（tracing 标准、线上失败归因 SOP、成本护栏） | 有零件（trace schema、可靠性六件套）没有成篇；`02-high-availability-rag.md` 是 stub | 行业共识已从"搭起来"转向"稳定运行"；这是开发岗面试"上线后怎么运维"一题的完整答案来源 |
| P2 | **Computer Use / GUI Agent 原理** | 只有 projects/03 的工程蓝图，无技术原理文档 | 截图坐标 vs 可访问性树 vs DOM 三条路线取舍、GUI grounding 训练、OSWorld/WebArena 评测，是蓝图落地绕不开的选型依据 |
| P2 | **Voice Agent 与实时交互** | 近乎零覆盖，但 industry_reports 里已收了 22 页 AI 陪聊行业报告 | 商业化最快的赛道之一，竞争相对不卷；级联 vs 端到端、打断/双工/首响延迟是该方向面试核心考点 |
| P2 | **端侧 Agent 与小模型** | 完全空白；模型笔记全讲旗舰大模型 | 对手机厂/芯片厂 AI 岗读者是空白市场；可在算法岗 14 阶段路线的"垂直分支"下挂一条，复用具身智能分支的体例 |

---

## 维度二：读者画像——现在只服务一种人

现有内容几乎只服务"有 CS/AI 背景、全职备战校招的求职者"。被漏掉的群体与学习阶段：

| 优先级 | 缺失的读者层 | 现状证据 | 落地建议 |
|:---:|:---|:---|:---|
| P0 | **读者分流导航**（成本最低、杠杆最高） | 6 份路线周数口径不一（8 周 / 9 周 / 8-15 周 / 多年期），`05-roadmaps/` 连 README 都没有；`04-interview/` 34 个文件无索引 | 写一张"你是谁 → 读哪份"决策页（README 分流卡 + 05-roadmaps/README + 04-interview/README），不用写任何新教程 |
| P0 | **零基础/非科班前置层（Stage -1）** | FAQ 对零基础只有一句话；7 天计划 Day 1 已假设会 Python、会命令行 | 前置知识自测页（Python/Git/数学/英文四项）+ 只补 Agent 岗最小集的 8 周补课路线，终点对齐 7 天计划的 Day 1 |
| P0 | **非算法技术岗平移路径** | `07-career-transition.md` 名为转行，实为圈内人选方向指南 | 技能映射专篇：Java/Go 后端→Agent infra、前端→Web Agent、测试→评测工程师、数据工程→RAG pipeline；每条给"可迁移 + 必补"清单，基于开发岗 8 周计划做 delta 裁剪而非重写 |
| P1 | **在校生科研线 + 实习跳板** | 顶会产出被路线图要求但没人教怎么走到那一步；毕设指南是 stub；`external/ai-research-ebook`（整本科研工作流电子书）游离在体系外无人能发现 | 读研三年时间线、可发论文选题地图（复用已有论文导读）、"论文复现→workshop 投稿"最小闭环（顺手兑现毕设 stub）、实习获取指南 |
| P1 | **在职碎片时间版** | 全部路线都是全日制口径（每日计划） | 给三份主力路线各出"在职换算表"（周数 ×2.5，标注可砍/必留）+ 8-10 个"单个周末 8 小时"冲刺包，不重写内容 |
| P1 | **拿 Offer 之后** | 叙事在拿 Offer 处戛然而止，读者上岸即流失 | "新人 30/60/90 天"指南、Agent 工程师 L1-L5 能力自评表（借用 what-is-agent 的分级思路）、在职者每周 5 小时持续学习计划 |
| P2 | **出海/英文求职** | 全仓库仅 2 处偶然提到海外/remote | 英文简历 bullet 对照版、核心术语中英速查表、海外面试差异（behavioral/system design 英文表达）、目标市场地图 |
| P2 | **AI 产品经理旁支** | 零承接，但能盘活两块死资产 | 用 industry_reports 的 4 份行业报告写导读；把 projects/05-06 的 Dify/Coze/n8n 链接堆重编为 PM 作品集教程 |

---

## 维度三：内容形态——同样的知识，换个形态

约 95% 的内容是长文 markdown + 外链。很多空白是**形态转换**而非新写作，成本低、杠杆高：

| 优先级 | 形态 | 现状 | 落地建议 |
|:---:|:---|:---|:---|
| P0 | **带答案的自测层** | 绝大多数题库是"题目+标签"无答案（824KB 题库约 7600 行题目零答案），而完整答案已存在于 10 本 playbook 中 | 从 playbook 抽问答对做 Anki 闪卡包 + 按路线 Stage 做 checkpoint 自测卷（题目+简答+深读链接）；为高频题分批补"30 秒参考答案" |
| P0 | **一页纸速查表（cheatsheet）** | 速查内容全部内嵌在超长文档里（346KB / 96KB / 824KB），面试前夜没法用 | 后训练一页纸（SFT/PPO/DPO/GRPO 对照）、评测矩阵一页纸、上下文工程一页纸（顺带充当 5 篇重叠文档的统一入口）、MCP vs A2A vs ACP 协议对照、安全上线 checklist 打印版 |
| P1 | **决策树与图解** | docs/ 下零 mermaid 图；86 处图片全部依赖外部图床（微信 qpic 21 处防盗链高危、picui 11 处），是必然劣化的维护炸弹 | 把外链图片收编进 `assets/images/`；用 mermaid 画"要不要上 Agent"、框架选型、RAG 架构升级三棵决策树（GitHub 原生渲染）；CONTRIBUTING 加"禁止外链图床"规范 |
| P1 | **结构化数据资产** | 约 60 份 PDF 不在 `data/resources.json` 索引内"裸奔"；1500+ 题锁在 prose 里无法筛选；14 阶段指南背后的 6635 条 JD 数据只留下叙述没留下数据 | PDF 收入索引或补目录 README；发布 `questions.jsonl`（question/category/difficulty/company_tags）；公开 JD 数据的脱敏聚合 CSV——这是独家传播素材 |
| P1 | **模板库补全** | examples/ 自己的交付标准要求 `spec.md`、`eval_report.md`，但这两样连模板都没有；tool-card 模板有嵌套代码围栏渲染 bug | 补 spec / eval-report / 简历 bullet / system prompt / 失败归因五个模板，examples/ 即成完整项目脚手架产品线 |
| P2 | **术语表 + 概念索引** | 无集中术语表；RoPE/GQA/RMSNorm 在三篇模型笔记中各讲一遍（`03-transformer.md` 反而是 stub） | 建 `docs/glossary.md`：中英术语 + 3 句定义 + "面试一句话版本" + 指向仓库内最深文档的链接 |
| P2 | **时间线与动态层** | 无任何时间线/更新栏目；FAQ 承诺"每周 2-3 篇"却无承载 | Agent 技术大事记（可先顶替 `02-agent-history` stub）+ 月度求职情报 digest + 根目录 CHANGELOG |

---

## 维度四：求职链路纵深——答题之外的环节

题库解决"面试怎么答"，但链路的前端（市场情报、选公司、投递）和后端（Offer 决策、入职）都是空白：

| 优先级 | 环节 | 现状 | 落地建议 |
|:---:|:---|:---|:---|
| P0 | **JD 市场情报产品化** | 14 阶段指南自述基于 6635 条真实岗位要求生成，但市场分析本身没有以读者可读的形式呈现；《AI可入方向》HC 情报以裸 PDF 躺着 | 《从 6635 条 JD 看 Agent 岗位要求全景》（词频榜、算法岗 vs 开发岗差异、门槛分布）+《如何拆解一份 Agent 岗 JD》教程 + industry_reports 补 README 导读 |
| P0 | **公司图谱** | 面经案例几乎全部匿名成"某大厂"，读者不知道该投谁 | 按赛道（大厂大模型部门 / AI Coding / Agent 平台 / 具身 / 出海）列出谁在招、业务方向、技术栈、面试轮次；每家链回题库对应标签的面经 |
| P1 | **薪资行情与 Offer 决策** | 谈薪指南教读者说"我了解到行业平均是 XXX"，但没有任何一篇告诉读者 XXX 是多少；FAQ 的"应届 30-50 万"无依据 | 总包结构与职级对照科普（引用可验证公开来源）+ 多 Offer 加权决策表 + 口头 offer 到三方的流程科普 + 脱敏真实 Offer 案例集 |
| P1 | **作品集最后一公里** | 路线图反复要求"作品集"交付物，但没有一篇讲 GitHub 主页、demo 部署、个人站怎么做 | 面试官视角的 GitHub 主页 checklist、HF Spaces/Vercel demo 三条路线、"简历数字 → 仓库内 eval 脚本自证"的互证关系 |
| P1 | **Mock Interview 剧本 + AI 陪练** | 题库是"弹药"不是"实弹演习"，没有一份完整 60 分钟面试的流程级预演 | 算法岗 60 分钟全真剧本（含 5 层追问树 + 评分 rubric）+ "用 Claude/GPT 当面试官"的 prompt 套件（能直接吃仓库题库，本身就是 dogfooding 展示项目） |
| P2 | **挂经与失败复盘库** | 只收"考了什么"，不收"为什么挂"；心态文仅 3.7KB | 挂经结构化模板向社群征集 + 高频挂点统计（每个挂点链接补救章节）+《简历石沉大海排查手册》 |
| P2 | **投递渠道与内推** | README 社群承诺"内推"，但没有内容教内推和 networking 本身 | 渠道全景对比、内推话术模板与跟进节奏、"开源贡献换 visibility"路径（衔接 projects/04 的 25+ 项目导航） |
| P2 | **求职全年历** | 求职攻略是纯秋招向，无全年时间地图 | 按月标注提前批/秋招/春招/实习窗口，并与 8/9 周路线图倒排对齐 |

---

## 维度五：栏目级与产品化——对标 JavaGuide 的结构性差距

| 优先级 | 栏目 | 差距 | 落地建议 |
|:---:|:---|:---|:---|
| P0 | **板块级导读页** | JavaGuide 每个一级栏目都有导读；本仓库 05-roadmaps、04-interview、01-theory、03-practice 均无，02-tech-stack 的 README 与实际文件脱节（3 处 404、346KB 的 post-training 未收录） | 每目录补 README；写目录结构 lint 脚本（README 必存在、编号无冲突、链接的文件必存在）挂进 CI |
| P1 | **一条可线性阅读的"AgentBook"主线** | 竞品（hello-agents、MS AI Agents for Beginners、HF Agents Course）都是编号章节的书；本仓库是"路线图 + 散装文档" | 规划 12-16 章主线，已有强内容可覆盖约一半章节；把三篇模型笔记（168KB，占 theory 板块 97% 篇幅）移入"模型深读"附录，顺手从中抽取重复内容合成缺失的 Transformer 章 |
| P1 | **在线阅读站** | 824KB 题库在 GitHub blob 页根本打不开；index.html 只是落地页 | 用 VitePress 或 Astro Starlight（external/ 已有 Astro 技术栈）建阅读站：侧边栏 + 全文搜索 + 大文件按一级标题拆分 |
| P1 | **贡献者体系** | 无 LICENSE、无 issue/PR 模板、承诺的贡献者墙不存在 | 补齐三件套；把 gap-map 的 P0/P1/P2 清单转成 good-first-issue + Project 看板——它本身就是现成的社区任务分发表，可用来众包还债 |
| P2 | **保鲜机制** | 无 CHANGELOG、文档无 last-reviewed 元数据；Agent 领域内容以月为单位过期 | CHANGELOG + "Agent 前沿月报"栏目 + frontmatter 加复核日期，超期文档打"可能过时"角标 |
| P2 | **社区问答沉淀** | 社群互动全部发生在仓库外，零沉淀；题库无持续供给机制 | 开 GitHub Discussions 分区 + 结构化面经投稿 issue 表单（审核后进题库）+ 匿名 Offer 数据众包页 |

---

## 如果只做五件事

1. **还债**：写出两个 quickstart 脚本 + 补 LICENSE + 修 README/FAQ/CONTRIBUTING 死链与占位信息（一周内可完成，全是信任问题）。
2. **补技术空白三大件**：Agentic RL、Coding Agent 专题、Multi-Agent + A2A/ACP（2026 版），三篇都能顺手兑现现有 stub。
3. **写导读**：05-roadmaps 和 04-interview 各一篇 README（读者分流，纯导航零新写作）。
4. **形态转换三件套**：playbook 抽答案做自测卷、大文档蒸馏 cheatsheet、6635 条 JD 数据公开成市场报告。
5. **projects/01-03 各交付 M1 里程碑代码**，兑现"clone 即跑"的自定标准。

## 与 gap-map 的关系

- 读 [04-repo-gap-map.md](./04-repo-gap-map.md)：了解**哪些具体文件**是占位、按什么顺序补。
- 读本文：了解**哪些整类维度**缺失、每类的优先级与落地点子。
- 两者的 P0 有交集（如 MCP、多 Agent 框架），交集处优先动手。
