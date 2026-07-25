# 判决层框架 (Verdict Layer Framework)

**[🇺🇸 English](README.md) | 🇨🇳 简体中文**


> **翻译状态 / Translation status:** 本文档翻译于 **2026-07-25**，此后不再同步更新。
> 英文版本为唯一权威版本，如有出入以英文为准。
> *Translated 2026-07-25 and frozen. The English document is canonical; where the
> two differ, the English text governs.*

一个**以测量为先**的框架，关注**对 AI 生成变更的信任 (trust)**——一套用于判断工程组织可以安全接纳哪些 AI 变更的模式与标准。

## 重新定义问题

这个领域大多在测量一个维度——**能力 (capability)**：*智能体能否解决任务？*（解决率、通过率）。这是**模型**的属性。但它并不是工程组织在代码进入主干之前必须回答的问题。

> **能力问的是：「智能体能否解决任务？」**
> **信任问的是：「组织能否安全地接纳这个变更？」**

**信任是工程*过程*的属性，而非模型的属性。** 本框架关注的正是后一个维度。

为了不让「信任」一词滑回模糊的「治理」，我们给它一个可测量的定义：

> **信任 = 一个被自动接纳的 AI 变更，实际符合既定需求的概率**（以独立裁决器上的 `1 − 误受率 (false-accept rate)` 来度量）。

## 为什么需要第二个维度

智能体为自己的变更编写的测试是**自我指涉的**——无论修复正确还是自信地出错，它都会通过。随着 AI 自主性上升，人工审查不再是完整的检查，而退化为一种**抽样**。于是，单个被悄悄接纳的错误变更，其代价的增长速度，快于生成代码本身的成本。这正是一个**独立的接纳决策**体现价值之处。

这个决策是**三态的，而非二态**——一个「能回答就回答，否则上报」、懂得自己何时无法判断的系统：

> **接受 (accept) · 复核 (review) · 拒绝 (reject)**

## 状态——以诚实为构造前提

这是一项进行中的研究工作。一个隐藏自身局限的信任项目，已经背叛了它自己的论点，所以局限先行：

- 标题性的数字来自一次**冻结的、独立的留出集 (held-out) 评测**，已于 2026-07-05 完成，依照一份在结果存在之前即已发布的[预注册计分契约](https://github.com/kolesnikov-arch/patchward/blob/main/PREREGISTRATION_zh.md)：在 50 个留出任务上，同一个模型**无门控时静默交付 17/50 个错误修复，有门控时为 0/50**——完整结果、置信区间、公开的代价与可复现工件见 **[patchward — 留出集结果](https://github.com/kolesnikov-arch/patchward/blob/main/RESULTS_zh.md)**。开发过程中的观察仍然只是观察，不构成证据。
- 目前仅在一个公开的软件工程基准上验证，而**非**生产环境的 CI。
- 在得出任何结论前，请先阅读 **[当前范围与局限](CURRENT_SCOPE_AND_LIMITATIONS_zh.md)**。

## 这是什么

用于构建「面向 AI 生成变更的独立信任/接纳层」的抽象模式与标准。它们**不是**产品（没有可安装的代码），**不是**创业企划，也**不是**特定于实现的（工具名、阶段名、提示词和内部逻辑都被刻意省略）。

公开的是**方法与证明**；实现本身不是发布的对象。当结果就绪时，「可复现」意味着两件事：*核验我们已发布的评测产物*，以及*用该方法测量你自己的信任*——而**绝非***复现我们的控制器*。

## 目录

| 文档 | 涵盖内容 |
|----------|---------------|
| [判决层宣言](MANIFESTO_zh.md) | 推理过程：以独立验证取代自我报告 |
| [当前范围与局限](CURRENT_SCOPE_AND_LIMITATIONS_zh.md) | 这项工作**尚未**证明什么 |
| [术语表](GLOSSARY_zh.md) | 信任维度上每个术语的定义 |
| [交互式模拟](https://github.com/kolesnikov-arch/patchward/tree/main/sim) | 三态判决逻辑的交互式演练（已迁入 patchward 仓库，英文） |

> 这是理论层，刻意保持精简。早先那些不服务于信任论点的架构模式草稿已被移除；其历史仍保留在 git 中。

## 目标受众

- 正在权衡如何安全接纳 AI 生成变更的 CTO / 工程副总裁
- 设计 AI 交付接纳控制的平台与赋能团队
- 想要一个可测量属性、而非幻灯片的工程领导者

## 作者

**Dmitriy Kolesnikov.**
**联系方式:** [kolesnikov.arch@gmail.com](mailto:kolesnikov.arch@gmail.com)  ·
[LinkedIn](https://www.linkedin.com/in/dmitriy-kolesnikov-631b67169) ·
[X @kolesnikov_arc](https://x.com/kolesnikov_arc)

## 许可与使用

依据 **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** 发布。你可以阅读、研究、引用，并将这些蓝图用于组织内部治理。商业使用、转售、咨询、衍生的商业产品或培训课程，需通过上述联系方式获得书面许可。详见 [LICENSE](LICENSE)。
