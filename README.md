<div align="center">

# MO Ming · Bosch Algorithm Internship

**AI Agents · RAG · Internal AI Products**

**🏆 BOSCH BBM AI DAY · 第二名（2nd Place）**<br>
**2026 Bosch China AI Day · Top 4 Most Impressive Topics**

[![2026 Bosch China AI Day](assets/00-bosch-ai-day.jpg)](assets/00-bosch-ai-day.jpg)

*2026 Bosch China AI Day 颁奖现场 · BBM AI Day 第二名*<br>
📷 图中**从右数第 2 位**（白 T 恤、戴眼镜）就是我

</div>

---

## 关于我

我是 **MO Ming**，在博世中国做算法实习。

这段实习里，我参与了多个内部 AI 产品，主要精力在三个项目：**工程文档审核、CAN 日志诊断、刷件审批自动化**。下面按“业务是什么、我做了什么、效果如何”介绍。

> **关于这个仓库**  
> 因博世内部数据合规要求，我不能上传源代码、原始业务数据或内部文档。这里用产品界面截图介绍我参与的项目；截图中的同事邮箱、客户名称与联系人信息已打码，客户和具体项目名称已做匿名化处理。

---

## 项目一览

前三个是主要项目，后三个是同一时期参与的平台型项目。

| 项目 | 我的角色 | 业务 |
|------|----------|------|
| **01 CodexConcern** | 独立设计与开发 | 判断历史 Codex Concern 是否适用于新项目 |
| **02 Fault Log Analysis** | 主导后端与 AI 分析模块 | 从 CAN / CAN-FD 日志中定位整车故障 |
| **03 Reflash Space** | 核心开发（协作），主导 AI 审核工程化 | 打通刷件执行清单与审批系统，自动巡检 + AI 复核 |
| **04 Digital Platform** | 参与 | 内部数字化应用的统一入口 |
| **05 Q-Model Farm** | 参与 | 大模型用量与成本的可视化治理 |
| **06 Early-D Contract Assistant** | 参与 | 合同字段到文档的自动映射与 PDF 导出 |

---

## 01 · CodexConcern

**独立设计与开发** · Python · FastAPI · Vue 3 · OpenAI Agents SDK

[![CodexConcern](assets/02-codexconcern.png)](assets/02-codexconcern.png)

*批量审核：先预览待审条目、跳过数量与预计耗时，再确认执行*

**业务**

ADAS 雷达项目会不断收到历史平台的 Codex Concern，类似“问题预警单”。项目方需要判断：这个机制在我们项目里存不存在？参数是多少？如果不适用，依据是什么？

人工判断一条 Concern，通常要翻功能定义、设计文档、参数标定、测试用例、失效后果等多类资料；而且 Concern 和项目文档的术语经常对不上，按字面搜索很容易 0 命中。

**我做了什么**

- 独立设计并实现一套 AI 审核系统：把审核拆成策略、结构化、检索、机制定位、参数补齐、裁决几个步骤；机械步骤用代码，语义判断交给 LLM。
- 让 Agent 自主换检索词、换目录、读原文，并对引用的证据做逐字校验；同时补全检索范围，从 1,458 篇扩展到 3,192 篇。
- 对接质量业务方，组织试用并按反馈迭代；保留人工复核与留档，保证每条结论都能追溯。

**效果**

- 支持一次批量审核 80 条；已沉淀 81 条留档裁决（34 条适用 / 46 条不适用）。
- 单条审核约 4 分钟，输出“适用性 + 置信度 + 证据”的可追溯结果。

---

## 02 · Fault Log Analysis

**主导后端与 AI 分析模块** · Python · FastAPI · LangGraph · Vue 3 · ECharts · Docker

| 文件配对 | 信号视图 | AI 诊断报告 |
|:---:|:---:|:---:|
| [![文件配对](assets/03-failure-log-analysis.png)](assets/03-failure-log-analysis.png) | [![信号视图](assets/03b-failure-log-signals.png)](assets/03b-failure-log-signals.png) | [![AI 诊断报告](assets/03c-failure-log-ai-report.png)](assets/03c-failure-log-ai-report.png) |

*上传 DBC + ASC / BLF 日志，查看多信号联动，最后生成可追溯的诊断报告*

**业务**

ADAS 整车在路测或售后出现功能异常时，工程师需要从 CAN / CAN-FD 总线日志中定位问题。一份典型日志约 47.7 万帧，用 CANalyzer 逐条比对是小时级工作，而且高度依赖工程师经验。

**我做了什么**

- 主导后端与 AI 分析模块：设计 8 节点 LangGraph 工作流，让 LLM 负责选择和解释；所有时间、帧数、信号值都来自 11 个确定性工具，避免模型“算错数”。
- 参与 FastAPI + Vue 3 + ECharts 平台开发，把上传、解析、信号查看、诊断报告串成完整流程。
- 加入数据质量预检、DBC 错配检测和报告证据链，避免“解析成功但数值错误”。

**效果**

- 47.7 万帧日志全链路约 1 分钟；缓存命中约 0.2 秒，内存从约 2 GB 降到几十 MB。
- 工程师从逐条比对转为复核诊断报告，输出可追溯的中文报告。

---

## 03 · Reflash Space

**核心开发（与同事协作）· 主导 AI 审核模块的工程化** · FastAPI · Vue 3 · Microsoft Graph · SQLite · Docker · LLM

| 发起审核 | 历史记录 |
|:---:|:---:|
| [![发起审核](assets/05-reflash-space.png)](assets/05-reflash-space.png) | [![历史记录](assets/05b-reflash-audit-history.png)](assets/05b-reflash-audit-history.png) |

*输入审批记录 ID 或链接发起审核；历史页保留结论、耗时与人工裁决*

**业务**

客户或博世侧改了软件版本后，需要把一批 ECU 产品重新刷写，并登记在 E-Workflow 审批系统中。执行清单在 SharePoint 在线 Excel，审批记录在 E-Workflow，两边没有关联字段，只能靠料号人工对齐。

全量记录约 1,440 条，人工巡检工作量大、判断口径不一致，结果也没有留痕。

**我做了什么**

- 参与搭建自动化中间层：定时拉取审批记录，按料号匹配，自动回填版本号并标色（绿 = 已完成 / 黄 = 进行中 / 红 = 无有效记录），异常邮件告警。
- 主导 AI 审核模块的工程化：脚本规则 + LLM 独立复核 + 冲突仲裁 + 人工裁决，覆盖 5 大类检查项；AI 不可用时降级可见，不静默放行。
- 设计人工裁决留痕与内容指纹复用，让审核员不必重复确认已经处理过的节点。

**效果**

- 覆盖 1,440 条记录（1,215 条有效），每小时自动巡检，人只处理红 / 黄异常。
- AI 单案耗时从 30–90 秒降到 8–17 秒，裁决条数不变；结果可追溯、可回放。

---

## 其他参与项目

| Digital Platform | Q-Model Farm | Early-D Contract Assistant |
|:---:|:---:|:---:|
| [![Digital Platform](assets/01-digital-platform.png)](assets/01-digital-platform.png) | [![Q-Model Farm](assets/04-q-model-farm.png)](assets/04-q-model-farm.png) | [![Early-D](assets/06-earlyd-contract.png)](assets/06-earlyd-contract.png) |
| 内部应用统一入口 | 模型用量与成本 | 合同字段自动映射 |

**04 · Digital Platform** — 参与内部数字化应用平台。提供 App Store 式应用目录、标签与搜索、审批入口、角色权限、IT 资产目录和访问分析，让分散的内部工具有一个可发现、可申请、可复用的入口。

**05 · Q-Model Farm** — 参与大模型用量与成本治理。基于 LiteLLM 网关做用量追踪：按天 / 月查看成本和 Token 变化，按模型和用例拆解，并提供 Q-Safe 安全托管、Q-Fast 即时开通、Q-Smart 用量可见三项服务。

**06 · Early-D Contract Assistant** — 参与合同填写自动化。把 BU、联系人、客户公司、技术 / 质量负责人等字段做成结构化表单，映射到合同模板，生成预览并一键导出 PDF，减少“找模板、填字段、反复核对”的文书工作。

---

## 技术栈

| 方向 | 技术 |
|------|------|
| **AI / Agent** | OpenAI Agents SDK、LangGraph、RAG、LiteLLM、Prompt Engineering |
| **后端 / 数据** | Python、FastAPI、PostgreSQL、SQLite |
| **前端 / 部署** | Vue 3、ECharts、Docker Compose、nginx |
| **集成** | Microsoft Graph、SharePoint、E-Workflow |

---

## English Snapshot

I'm **MO Ming**, an AI master's student and former algorithm intern at **Bosch China**. I build internal AI products that turn document review, CAN log diagnosis, and reflash approval into traceable, human-in-the-loop workflows.

At **BOSCH BBM AI Day**, my project won **2nd Place** and was selected among the **Top 4 Most Impressive Topics** at the 2026 Bosch China AI Day.

---

## 说明 / Disclaimer

- 本仓库是**个人作品集**，不是博世官方仓库；文中观点仅代表个人。
- 不包含博世源代码、内部文档或客户数据文件；截图只展示产品界面与交互。
- 截图中的同事邮箱、客户名称与联系人信息已做打码 / 模糊处理；客户与具体项目名称已匿名化。如仍有不应公开的信息，请通过 GitHub 联系我，我会尽快调整或撤下。
- “Bosch” 名称及相关商标归 Robert Bosch GmbH 所有。

<div align="center">

**Thanks for reading.**<br>
[GitHub @Moming0215](https://github.com/Moming0215)

</div>
