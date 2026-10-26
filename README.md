# hybrid-LLMs

Hybrid LLM 推理系统研究资料库，整理 **Prefix Caching、FA / SWA / SSM（Mamba / GDN）异构缓存、内存分配、驱逐策略与复用实验**。仓库内的 HTML 可以独立在线阅读。

## 📚 HTML 报告索引

按**首次上传到本仓库的时间，从早到晚**排列（日期采用 UTC+8；同一天按 GitHub 首次提交顺序）。

| # | 首次上传 | 报告 | 主要内容 | GitHub 源文件 |
|---|---|---|---|---|
| 01 | 2026-10-15 | [Marconi：缓存机制与 FLOPs-aware 驱逐](https://wzhogqag.github.io/hybrid-LLMs/) | 讲解 Hybrid Prefix Radix Tree、SSM checkpoint 准入和淘汰、FLOPs / 内存成本、α 权重调节与示例；包含交互式说明。 | [`index.html`](./index.html) |
| 02 | 2026-10-15 | [Qwen3.5-9B：Hybrid Prefix Geometry 扩展实验](https://wzhogqag.github.io/hybrid-LLMs/qwen3.5-9b-extension-experiments.html) | Qwen3.5-9B（GDN + Full Attention）的缓存几何分析；验证 vLLM 0.30.0 的 528-token 对齐与 Mooncake 512-token 共享前缀错位，并对照 SGLang。 | [`qwen3.5-9b-extension-experiments.html`](./qwen3.5-9b-extension-experiments.html) |
| 03 | 2026-10-15 | [Marconi：论文实验与实现考证](https://wzhogqag.github.io/hybrid-LLMs/marconi-experiments-implementation-memory-analysis.html) | 按 Fig. 6–13 梳理实验；考证 vLLM+ / SGLang+ 基线、TTFT profiling + trace 回放的方法，以及 KV / SSM 逻辑状态与 GPU 物理分配实现的证据边界。 | [`marconi-experiments-implementation-memory-analysis.html`](./marconi-experiments-implementation-memory-analysis.html) |
| 04 | 2026-10-18 | [Jenga：异构内存管理、前缀复用与两级驱逐](https://wzhogqag.github.io/hybrid-LLMs/jenga-memory-prefix-cache-guide.html) | 结合 SOSP'25 论文与固定版本原型源码，解析 LCM 大页/子页、组内布局与地址映射、请求亲和分配、跨类型复用和两级驱逐；含交互例子。 | [`jenga-memory-prefix-cache-guide.html`](./jenga-memory-prefix-cache-guide.html) |
| 05 | 2026-10-25 | [Motivation：LMCache Agent Trace 原始等待回放](https://wzhogqag.github.io/hybrid-LLMs/hybrid-cache-agent-natural-waits-results-2026-10-25.html) | Qwen3.5-9B / vLLM 0.30.0 / 单张 A800；10 会话、479 请求，保留原始请求间等待。分析总体 89.896% 的联合复用率、≥4 分钟等待后的 25.781% 联合复用率，以及 FA KV 与 recurrent checkpoint 的驻留失配。 | [`hybrid-cache-agent-natural-waits-results-2026-10-25.html`](./hybrid-cache-agent-natural-waits-results-2026-10-25.html) |

| 06 | 2026-10-26 | [Agent Trace：六种重放方式对比](https://wzhogqag.github.io/hybrid-LLMs/agent-trace-replay-six-methods.html) | 用相同的两轮对话例子比较固定原始 Prompt、模型输出反馈、真实 Agent 闭环、合成消息反馈、Block Hash 重建和 Teacher Forcing；说明原始前缀结构与 Decode KV 复用的一致性取舍，并给出 LMCache / AgentX 实验建议。 | [`agent-trace-replay-six-methods.html`](./agent-trace-replay-six-methods.html) |

## 在线阅读

- **GitHub Pages 首页**：https://wzhogqag.github.io/hybrid-LLMs/（当前为 Marconi 机制介绍）。
- 其他报告均有独立页面，可通过上表的报告名称直接打开。
- 报告中的实验结果与实现判断以各自记载的**版本、配置、工作负载与限定条件**为准，不能直接作为不同框架之间的统一性能排名。

> 本目录的顺序以文档首次上传的提交时间为准；后续修改某个 HTML 不改变它在索引中的位置。
