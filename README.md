<div align="center">

# MO Ming · Bosch Algorithm Internship

**把 AI 放进真实工程流程里**  
LLM Applications · RAG · Agentic AI · Internal Digital Products

**🏆 BOSCH BBM AI DAY · 第二名（2nd Place）**  
**2026 Bosch China AI Day · Top 4 Most Impressive Topics**

[![2026 Bosch China AI Day](assets/00-bosch-ai-day.jpg)](assets/00-bosch-ai-day.jpg)

*2026 Bosch China AI Day 颁奖现场 · BBM AI Day 第二名*  
📷 图中**从右数第 2 位**（白 T 恤、戴眼镜）就是我

</div>

---

## 先认识一下

我是 **MO Ming**，在博世中国 **XC/QMS-CN** 做算法实习。

这张照片拍摄于 **2026 Bosch China AI Day** 的颁奖现场。我参与的项目在 **BOSCH BBM AI DAY** 中获得 **第二名（2nd Place）**，并入选 **2026 Bosch China AI Day Top 4 Most Impressive Topics**。照片里，从右数第 2 位、穿白色 T 恤、戴眼镜的人就是我。

这段实习里，我主要在做一件事：

> **让大模型从“会回答”，变成“能被信任地放进工程流程里”。**

从内部应用的统一入口，到能追溯证据的审核助手；从 CAN 故障日志分析、刷件 AI 预审，到 Early-D 合同自动填写——这些系统面向的不是演示，而是真实业务流程中的“找得到、用得上、可治理”。

> **关于这个仓库**  
> 因博世内部数据合规要求，我不能上传源代码、原始业务数据或内部文档。这里用产品界面截图记录我参与设计、开发的系统，重点展示问题定义、产品思路与工程能力。截图中的同事邮箱、客户与联系人信息已打码，界面内容仅作能力展示。

---

## 项目地图

| # | 项目 | 解决的问题 | 关键词 |
|---|------|------------|--------|
| 01 | **Digital Platform** | 内部工具分散、重复建设、缺少统一治理 | App Store · 权限 · 审批流 · 资产目录 |
| 02 | **CodexConcern** | 审核证据分散，结论难以追溯 | RAG · 引用溯源 · 审核知识库 |
| 03 | **Failure Log Analysis** | CAN 日志门槛高，故障定位依赖人工翻找 | DBC · ASC/BLF · 信号分析 |
| 04 | **Q-Model Farm** | 模型调用成本和用量像“黑盒” | LiteLLM · Token 计量 · 成本归因 |
| 05 | **Reflash Space** | 刷件审核依赖人工逐条判断 | AI 预审 · Human-in-the-loop · 审计留痕 |
| 06 | **Early-D Contract Assistant** | 合同字段重复填写、模板映射容易出错 | 文档自动化 · 字段映射 · PDF 导出 |

---

## 01 · Digital Platform

### 内部数字化应用的“App Store”

[![Digital Platform](assets/01-digital-platform.png)](assets/01-digital-platform.png)

把散落在不同团队、不同目录里的脚本、看板、AI 工具，收进一个统一的数字化应用入口。它解决的不是“再做一个工具”，而是**让已有的数字资产被看见、被复用、被治理**。

**界面里能看到的产品能力：**

- **应用目录与标签体系**：按 Development、After-sales Ops、Project Mgmt、Reflash Ops、Compliance Ops 等场景分类，支持搜索和一键打开。
- **项目全生命周期**：Dashboard、Projects、Approvals、Toolflow，把“提出需求 → 审批 → 开发 → 发布”串起来。
- **权限与角色**：Users、Roles & Permissions、Workflow Config，让不同团队看到不同的应用和操作范围。
- **资产治理**：IT Assets、Asset Catalog、App Access Analytics，回答“有哪些资产、谁在用、用得怎么样”。

**我的关注点：** 不是堆功能，而是设计一套让内部工具**可发现、可申请、可复用、可审计**的产品结构。

`Internal Platform` · `App Catalog` · `RBAC` · `Workflow` · `Usage Analytics`

---

## 02 · CodexConcern

### 一个“先找证据，再下结论”的审核助手

[![CodexConcern](assets/02-codexconcern.png)](assets/02-codexconcern.png)

面向工程审核 / concern 场景的对话式助手：把项目文件、审核知识和历史记录变成可检索的证据库，再用大模型帮助审核人员快速定位相关材料。

它最重要的设计不是“回答得多流畅”，而是**回答是否站得住**。界面中的回答会明确区分：

- 哪些结论已经有文件证据；
- 哪些只是基于经验的推测，需要进一步打开 PDF 确认；
- 当证据不足时，直接说“我现在不能替它下结论”，并询问是否继续解析。

这种“**证据优先、允许不知道**”的交互，比一个看起来很自信的答案更适合审核场景。

**其他能力：**

- 按项目 / concern 发起检索与多轮追问；
- **批量审核**：选定目录后预览待审条目、已审跳过数量和预计耗时，确认后串行执行，并在页面顶部显示进度；
- 展示命中的项目文件和“查了哪些资料”；
- 维护审核知识库、审核历史与会话记录；
- 把“判定规则”沉淀成可复用的审核知识。

`RAG` · `Citation / Evidence` · `Batch Audit` · `Audit Knowledge Base` · `Conversational Search`

---

## 03 · Failure Log Analysis

### 把 CAN 故障日志分析做成可复用的产品

[![Failure Log Analysis](assets/03-failure-log-analysis.png)](assets/03-failure-log-analysis.png)

分析一份 CAN 故障日志，通常需要同时处理两类文件：描述报文和字节布局的 **DBC 信号定义文件**，以及记录总线通信的 **ASC 文本 / BLF 二进制日志**。过去这类工作往往依赖个人脚本和经验，门槛高、复用难。

[![Failure Log signal view](assets/03b-failure-log-signals.png)](assets/03b-failure-log-signals.png)

*信号视图：多信号叠加、时间轴缩放，以及联动面板 / 单独视图*

[![Failure Log AI report](assets/03c-failure-log-ai-report.png)](assets/03c-failure-log-ai-report.png)

*AI 诊断报告：结论摘要、解析范围与支持结论的报文证据*

这个系统把流程产品化：

- **文件配对**：左侧共享仓库按客户 / 项目组织，DBC 与日志可以本地上传或直接选择；
- **信号解码与可视化**：基于 DBC 把原始报文还原成可读信号，支持多信号叠加、时间轴定位和联动查看；
- **AI 辅助分析**：在信号视图之上提供 AI Analysis（Beta），生成包含结论、证据、时间基准和解析完整性的诊断报告；
- **共享协作**：项目、文件、日志集中管理，减少“文件在谁电脑上”的沟通成本。

**价值：** 把一次性的排障脚本，变成团队可以反复使用的分析工具。

`CAN Bus` · `DBC Parsing` · `ASC / BLF` · `Signal Visualization` · `AI-assisted Diagnosis`

---

## 04 · Q-Model Farm

### 让大模型用量和成本变得可见、可解释

[![Q-Model Farm](assets/04-q-model-farm.png)](assets/04-q-model-farm.png)

当越来越多团队开始调用大模型，新的问题出现了：**这个月花了多少？花在哪个模型、哪个用例、哪个团队？** Q-Model Farm 把 LiteLLM 网关的用量数据做成了一套可运营的看板。

**界面里展示的能力：**

- **总览**：本月总成本、Token 用量、输入 / 输出占比；
- **趋势**：按天看成本与 Token 变化，按月做对比；
- **成本归因**：按模型、按用例拆分，定位真正的成本来源；
- **服务能力**：Q-Safe Secure Hosting、Q-Fast Instant Issuance、Q-Smart Usage Visibility；
- **用量治理**：让预算、配额和模型选择有数据依据，而不是拍脑袋。

**价值：** 把“模型账单”从财务结果，变成团队可以日常优化的工程指标。

`LiteLLM` · `Token Metering` · `Cost Attribution` · `Usage Dashboard` · `Secure Hosting`

---

## 05 · Reflash Space

### AI 做初筛，人做最终判断

[![Reflash Space](assets/05-reflash-space.png)](assets/05-reflash-space.png)

刷件（Reflash）记录审核需要逐条核对信息。记录量大、规则细，完全依赖人工既慢又容易不一致。Reflash Space 的 AI 审核模块把这件事拆成“**AI 预审 + 人工复核**”：

- 输入 E-Workflow 记录 ID 或完整链接即可发起审核；
- 对记录给出 **通过 / 需人工介入 / 不通过 / 冲突** 四类结果，并展示关键版本、料号、CoverSheet、XFLASH 等核对依据；
- 支持按记录 ID、名称搜索，按结论筛选；
- 保留历史记录、耗时和人工裁决入口；
- 测试阶段明确提示：**结论仅供参考，不影响正式回填流程，结果与人工裁决单独存档，不写入正式统计**。

[![Reflash Space audit history](assets/05b-reflash-audit-history.png)](assets/05b-reflash-audit-history.png)

*历史记录：每次审核的结论、耗时、人工裁决与删除入口*

最后这一点很关键：AI 可以提效，但不能悄悄改变正式流程。**可解释、可回退、可审计**，才是内部 AI 产品能长期运行的前提。

`AI Review` · `Human-in-the-loop` · `Rule Configuration` · `Audit Trail`

---

## 06 · Early-D Contract Assistant

### 把合同填写变成“字段到文档”的自动映射

[![Early-D Contract Assistant](assets/06-earlyd-contract.png)](assets/06-earlyd-contract.png)

*界面中的客户与联系人信息已脱敏*

Early-D 样品合同 / 协议的准备涉及 BU、博世联系人、客户公司、技术 / 质量负责人等字段，以及固定的合同模板。这个工具把重复的手工填写变成**结构化录入 + 模板渲染**：

- **结构化表单**：选择 BU、联系人和客户信息，支持保存数据、导入数据与重试连接；
- **字段到文档映射**：把表单字段映射到合同模板的对应位置，实时生成预览；
- **一键导出**：确认预览后直接导出 PDF；
- **减少低级错误**：字段复用、模板统一，避免同一信息在多个文档中反复填写不一致。

**价值：** 把“找模板、填字段、反复核对”的文书工作，变成一条可复用的自动化流程。

`Document Automation` · `Field Mapping` · `Template Rendering` · `PDF Export`

---

## 我在这段实习里反复练习的几件事

### 1. 先定义“什么算好”，再选模型

审核场景的好，不是回答得像人，而是**结论有证据、边界说得清、错了能追回**。先把评价标准写清楚，模型选型和 Prompt 设计才有方向。

### 2. 证据链比“聪明”更重要

无论是 CodexConcern 的引用，还是 Failure Log Analysis 的信号来源，用户都需要知道：**这个结论是从哪来的？** 可追溯性决定了 AI 能否进入真正的工程决策。

### 3. 把人工兜底设计进流程

AI 预审、人工终审、单独存档、不写入正式统计——这些看似“保守”的设计，恰恰是内部系统能上线的前提。

### 4. 成本、权限、审计不是上线后再补的

从 Q-Model Farm 的 Token 计量，到 Digital Platform 的角色与审批，再到 Reflash Space 的审计记录，治理能力应该和产品一起长出来。

---

## 能力关键词

| 方向 | 关键词 |
|------|--------|
| **LLM 应用** | RAG、引用溯源、结构化输出、审核助手、AI 预审 |
| **平台工程** | Web 全栈、RBAC、审批流、应用目录、审计日志 |
| **数据与工程** | CAN DBC、ASC / BLF、日志解析、指标看板、成本归因 |
| **文档自动化** | 结构化表单、字段映射、合同模板渲染、PDF 导出 |
| **产品化** | 需求拆解、流程建模、原型设计、前后端联调、上线迭代 |

---

## English Snapshot

I'm **MO Ming**, an algorithm intern at **Bosch China (XC/QMS-CN)**. I build internal AI products that turn LLM capabilities into traceable, governable, and operable workflows.

At **BOSCH BBM AI Day**, my project won **2nd Place** and was selected among the **Top 4 Most Impressive Topics** at the 2026 Bosch China AI Day.

This repository is a screenshot-based portfolio. It covers an internal **Digital Platform / App Store**, a **RAG-based audit assistant (CodexConcern)**, **CAN bus failure-log analysis**, **LLM token & cost governance (Q-Model Farm)**, **AI-assisted reflash review (Reflash Space)**, and **Early-D contract automation**.

> Due to Bosch data-compliance requirements, no source code, business data, or internal documents are included. Colleague email addresses and customer/contact information in the screenshots have been redacted. The views expressed here are my own and do not represent Bosch.

---

## 说明 / Disclaimer

- 本仓库是**个人作品集**，不是博世官方仓库；文中观点仅代表个人。
- 不包含博世源代码、内部文档或客户数据文件；截图只展示产品界面与交互。
- 截图仅用于展示产品界面与个人参与的工作；部分功能处于 Beta / 测试阶段。
- 截图中的同事邮箱、客户名称与联系人信息已做打码 / 模糊处理；如仍有不应公开的信息，请通过 GitHub 联系我，我会尽快调整或撤下。
- “Bosch” 名称及相关商标归 Robert Bosch GmbH 所有。

<div align="center">

**Thanks for reading.**  
[GitHub @Moming0215](https://github.com/Moming0215)

</div>
