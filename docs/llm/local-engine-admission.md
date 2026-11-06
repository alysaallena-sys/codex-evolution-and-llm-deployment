# 本地模型与推理引擎：先证明适配，再决定部署

观察日期：2026-10-22 至 2026-11-04。整理日期：2026-11-06。

本文总结历史资产审查、固定源码研究和候选知识采用。它不提供当前“最佳模型”排名。本次整理没有下载权重、启动服务或重跑推理。

## 先区分四种事实

| 事实 | 可以证明什么 | 还不能证明什么 |
| --- | --- | --- |
| 磁盘中存在模型文件 | 曾经取得这些文件 | 当前服务正在使用它们 |
| 配置中存在模型和引擎名称 | 配置表达了某种意图 | 依赖正确、端点可用或生成结果正确 |
| 找到进程或通过连接检查 | 对应进程存在，或指定端点在该次检查中可连接 | 指定模型、模态和功能已经通过验收 |
| 在固定任务上读回结果 | 这组条件下的实际行为 | 其它模型、设备或未来版本也会相同 |

历史审查发现两套本地权重及 MLX 引擎配置，但没有取得当时的推理服务运行验收。另一项常见工具在所查安装位置和服务入口中没有出现。这只能说明该次搜索没有找到它，不能推出“从未安装过”。公开例子不保留个人路径、端口或设备标识。

## 可复用的候选准入顺序

1. **识别真实来源。** 分别记录发布者、基础模型、派生模型和权重许可。发布组织名称不能替代基础模型身份。
2. **固定完整版本。** 记录代码提交、推理引擎版本、量化格式、权重 revision 和必要依赖。模型能载入不代表计算路径正确。
3. **核对设备路径。** 分开 CPU、GPU、Metal/MPS、MLX 等实现。一个局部 CPU 策略不能证明整个服务支持纯 CPU。
4. **估算完整资源。** 权重大小只是内存的一部分。还要考虑运行框架、缓存、上下文、临时缓冲区和并发。
5. **检查内容出口。** 分别核对权重下载、图像 URL、遥测、请求日志、缓存和云对象存储。代码在本机运行不等于内容没有外传。
6. **设计最小真实验收。** 固定输入、预期输出、工具权限、超时和退出条件。只在已授权范围执行。缺少条件时保留候选或 `KEEP_BASE`。

2026-10-25 的历史模型筛选还揭示了依赖版本问题。当时将 LFM2.5-24B-A2B 的 MLX 4bit 版本列为首试候选，将 Granite 4.2 8B 的 MLX 量化版本列为另一项资源候选。LFM 模型卡在当时要求 MLX-LM 至少为 0.32.0；历史资料记录旧版可能载入模型，却错误路由专家。该轮没有下载候选或执行推理，因此不能把资料判断写成运行通过，也不能沿用为今天的推荐。

这项历史导航来自当时的最终研究答复，没有单独模型筛选原件，也没有固定模型卡 revision。本次不补做实时模型排名。[Liquid 官方说明](https://www.liquid.ai/blog/lfm2-5-24b-a2b)、[LFM MLX 模型卡](https://huggingface.co/LiquidAI/LFM2.5-24B-A2B-MLX-4bit)、[IBM 官方说明](https://research.ibm.com/blog/introducing-granite-4-2)、[Granite MLX 模型卡](https://huggingface.co/ibm-granite/granite-4.2-8b-q4-mlx)

## 案例一：Mage-VL-Cowork 的标签、基准与平台

更早的 2026-10-22 Kapitsa 审查也采用了相同原则。历史完成答复指出，电源模式、量化与回放协议差异会影响比较。该轮只完成来源审查，没有本地模型运行，也没有单独命名核源原件。本次将它保留为证据较弱的历史导航，不据此声称复现基准。[Kapitsa 固定提交](https://github.com/nace-ai/kapitsa/tree/5b20f648ce519f5dd27ac9de54ca1f5f53e2cdb6)

观察日期：2026-10-31。固定代码提交：`d213d430de4875c4c5c90e84b792410f704c8a23`。

模型卡说明其骨干包含 Mage-ViT 与 Qwen3-4B-Instruct-2507。因此，模型来源判断需要沿基础权重继续追溯，不能止于发布者标签。[模型卡](https://huggingface.co/microsoft/Mage-VL-Cowork)

作者报告了 OSWorld-Verified 两次运行的均值约 66.04%，并说明任务排除项和 50 步预算。这是特定设置下的作者结果；本次没有复现。[固定 README](https://github.com/microsoft/Mage/blob/d213d430de4875c4c5c90e84b792410f704c8a23/mage_vl_cowork/README.md)

官方表格演示中，一条流程使用 Python 文件工具，另一条流程主要使用 GUI。不同的工具权限会改变完成路径。演示的用时差不能全部归因于模型推理速度。公平比较需要固定工具、输入、初态和计时口径，并单列一次性环境准备成本。[官方演示](https://microsoft.github.io/Mage/cowork/)

约 9.48 GB 的 BF16 权重文件也不等于完整运行内存。固定评估材料使用 GPU 容器与桌面虚拟机；该次研究没有建立官方 Apple Silicon/MLX/Metal 路径。结论是“证据不足以支持该平台部署”，而不是断言绝对不兼容。[评估环境](https://github.com/microsoft/Mage/blob/d213d430de4875c4c5c90e84b792410f704c8a23/mage_vl_cowork/osworld_eval/README.md)

## 案例二：FreeToken 的局部 CPU 能力不是 Mac 支持证明

观察日期：2026-11-03。源码提交：`9cacd0896c9beb67d88c22a38be54236023b4605`。稳定发布另记为 `v0.2.1 / ba31db2ea708b61d7313bccb3ee4adf9d11ecb90`。

继承的固定源码审查材料没有提供 macOS/Metal 原生支持证据。Linux、Windows 或实验性 AMD 路径不能自动外推到 Mac。MoE 的 CPU 策略只涉及部分专家计算，也不能替代完整依赖与 GPU 路径审查。[固定安装说明](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/docs/install.md)

材料还区分了本地目录与远端模型标识：后者可能下载权重；图像 URL 也可能联网。可选请求日志需要单独核对。兼容某种 API 不意味着必须调用该 API 品牌的云服务，也不证明全部协议等价。[模型说明](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/docs/models.md)、[请求日志源码](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/python/freetoken/server/request_logger.py)

该轮直接源码复核遇到工具不可用，未取得新的正文。因此，公开稿将这些判断标为继承材料结论。实际结果是保留现有部署方案 `KEEP_BASE`，只登记候选，不安装引擎或调用模型。

引擎代码采用 Apache-2.0；这不替代模型权重许可审查。[固定许可](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/LICENSE)

## 案例三：SIE 的 Mac 能力需要分路径验收

观察日期：2026-11-04。固定提交：`8563ef3bf92e181c7ddd32356be78d7a15599d45`。

继承的源码审查区分 Apple Silicon 的 MPS embedding/rerank 与独立 MLX 文本生成路径。MLX 路径存在图像、视频和 grammar 限制，不能据此宣称所有模型或全部工具在 Mac 可用。[固定项目说明](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/README.md)、[MLX 生成适配](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/adapters/mlx/generation.py)

材料记录：适配层接受 `revision`，但未把它传给子进程。固定 SIE 代码不等于固定真实模型权重。后续运行验收需要核对实际下载来源和权重 revision。[MLX 子进程实现](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/adapters/mlx/_server.py)

同一提交中的 server 为 0.11.0。材料记录其默认监听所有网络接口；无认证配置且无 token 时采用无认证模式；telemetry 默认开启。README 对未来 0.13.0 的回环监听和遥测关闭条件不能套用到这个提交。MCP edge 的匿名开关和 connector secret 条件还要另行核对。[CLI](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/cli.py)、[认证](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/core/server_auth.py)、[遥测](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/observability/telemetry.py)

特定匿名遥测 payload 不含 prompt，也不能证明所有日志、代理或可观测性路径都没有请求内容。缓存回退、首次权重下载和云存储需要分别说明。

实际采用仅限候选筛选知识。没有安装、替换部署或运行模型。宣传中的 98%/3% 缺少原实验定义，现有质量和固定速率记录不能替代该基准。本次没有验证其成本或质量收益。[公开基准方法](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/examples/evaluations/published-benchmarks/README.md)

代码采用 Apache-2.0；各模型许可和云资源费用独立核对。[固定许可](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/LICENSE)

## 本文的证据范围

- **来源研究**：固定版本材料与已有审查结论；部分外部读取失败也保留在判断中。
- **本地静态结果**：候选条件已整理并读回；版本、范围和来源限制明确。
- **本地真实运行**：上述候选引擎和模型没有在本次研究中取得运行验收。
- **设备与发布**：没有新增设备测试或部署发布。

可复用的是准入顺序和证据分层。候选进入说明文档，仍然不等于进入生产。
