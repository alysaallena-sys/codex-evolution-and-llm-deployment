# 上下文、浏览器工具与组件包的证据边界

本文整理 2026 年 11 月 4 日至 6 日的历史研究。本文导出日期为 2026 年 11 月 6 日。结论只适用于下列固定版本。本文不承诺当前产品行为。

本次导出读取既有研究回执。本次导出没有重新读取 X 或上游网站。本次导出没有安装组件、调用模型或测试运行行为。

## 版本与核查范围

| 对象 | 固定版本或提交 | 历史记录日期 | 核查范围 |
| --- | --- | --- | --- |
| Compact-Adviser | 0.1.14；`37fa1a665b8933de68c90014312060e862cf121a` | 2026-11-04 | README、许可证、包元数据和五份 Codex 适配文件的静态核查 |
| Playwright MCP | 0.0.84；`50b004fb3d3ee17f9710f067ed1b6d59fd16e4a1` | 2026-11-05 | README 中的操作、会话复用、配置与安全段落 |
| Stagehand | 4.4.0；`ce298c60bd7e617e38d67db8db7d34de9d37cd18` | 2026-11-05 | 两份缓存与提示文档；没有核查服务实现 |
| WebMCP | 2026-11-02 的社区组草案；`6cd745ac8a186122bd3f4aeaeb1d6cfa820251d2` | 2026-11-05 | README 相关段落、规范元数据、工具注解和安全讨论 |
| ECC | v2.2.3；`c05b2d6614f62f6db0047669aa4eefb223d478f9` | 2026-11-06 | 发布版 README、Codex 插件 README、钩子入口和两份成本文档的限定核查 |

Compact-Adviser 回执记录 MIT 代码许可证。其他三项浏览器资料的交接清单分别记录 Apache-2.0、MIT 和 W3C Software and Document License。ECC 来源方记录 MIT。接收方没有逐项复核全部许可证和分发包。代码许可证不证明远程服务的账户、收费、隐私或保留条款。

## Compact-Adviser：分类建议与任务恢复分开

固定源码把 Compact-Adviser 实现为外部上下文边界分类器。默认路径向 `api.typesafe.ai/v1/systemone` 发送请求。默认模型名为 `jev-latest`。输入可以包含用户文本、助手文本、工具结果片段、旧摘要、产物路径和覆盖标记。它发送的内容超过 token 计数。源码把整个序列化请求限制为 32,000 个 UTF-8 字节。历史核查没有发送或观察真实请求。[固定源码：judge.ts](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/judge.ts)、[固定源码：snapshot.ts](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/snapshot.ts)

该版本的 Codex 适配器提供 `hint` 和 `off` 模式。`hint` 返回建议消息。该适配器没有实现自动执行压缩的路径。默认评分使用 `P(finished) × (0.5 + 0.5 × P(hands_on))`。用量条件可把阈值从 0.90 改为 0.50。评分只表达分类判断。`checkpointKey` 只用文本哈希去重建议。它没有保存可恢复的任务状态。恢复还需要独立保存并读回任务目标、决定、权限边界和下一步。[固定源码：config.ts](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/config.ts)、[固定源码：hook.ts](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/hook.ts)、[评分源码](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/judge.ts)

关闭顺序决定实际边界。在有效的 `onStop` 路径中，读取历史、完成交换记录和写入会话状态先于 `mode=off` 判断。`off` 随后阻止密钥解析、快照构建和分类请求。入口禁用检查更早执行；它先于标准输入解析和事件处理。历史核查没有审计全部导入副作用。因此，单看 `off` 或入口检查不能证明整个进程零读写。[固定源码：hook.ts](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/hook.ts)

历史读取器最多读取 8 MiB 尾部。长文件另读最多 256 KiB 头部。映射上限为 4,096 条消息。选定的助手消息映射没有检查 channel。秘密模式与敏感文件启发式只提供尽力过滤。它们没有证明任意个人信息都不会外发。以上结论描述静态潜在路径；历史核查没有证明真实泄露。[固定源码：rollout.ts](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/rollout.ts)、[过滤源码](https://github.com/kunchenguid/compact-adviser/blob/37fa1a665b8933de68c90014312060e862cf121a/packages/codex-plugin/src/snapshot.ts)

历史结果支持保留既有恢复方法。它没有支持安装或启用该程序。分类正确率、压缩安全、恢复质量、本机 token 节省和费用节省均无本地运行证据。远程模型的收费与数据保留条件也未核实。

## 浏览器工具：执行、缓存与授权分开

Playwright MCP 的确定性操作应用不能证明模型选对目标或流程。固定 README 明确说明该工具不构成安全边界。扩展可以复用登录会话。登录状态只提供操作能力。当前任务仍需独立授权。这里的目标选择与授权判断属于适配结论。[固定 README](https://github.com/microsoft/playwright-mcp/blob/50b004fb3d3ee17f9710f067ed1b6d59fd16e4a1/README.md)

Stagehand 文档描述 Browserbase 服务端结果缓存。本地浏览器的缓存选项在该文档条件下没有效果。`HIT` 可以省去该次响应的 LLM 推理。`MISS` 和 `DISABLED` 不能证明整个任务零 token、零费用或固定加速。[固定缓存文档](https://github.com/browserbase/stagehand/blob/ce298c60bd7e617e38d67db8db7d34de9d37cd18/packages/docs/v4/best-practices/caching.mdx)

缓存键包含指令、页面内容、选项和 URL。缓存键排除模型配置。`locator` 或 `ignoreLocators` 会关闭该次调用的缓存读取和写入。无效选择器或缓存不可用可能触发推理回退。两份已读文档没有确定选择器回退后的最终状态值。此处只记录文档条件；没有运行缓存请求。[固定缓存文档](https://github.com/browserbase/stagehand/blob/ce298c60bd7e617e38d67db8db7d34de9d37cd18/packages/docs/v4/best-practices/caching.mdx)

Stagehand 的变量机制可以让模型看不到实际值。缓存服务仍可能接收实际值。文档要求含凭据的调用使用 `cache:false`。文档也要求秘密输入关闭日志。示例代码没有覆盖全部正文要求。因此，变量替换或关闭缓存都不能单独证明完整保密。历史任务没有修改缓存或日志配置。[固定缓存文档](https://github.com/browserbase/stagehand/blob/ce298c60bd7e617e38d67db8db7d34de9d37cd18/packages/docs/v4/best-practices/caching.mdx)、[固定提示文档](https://github.com/browserbase/stagehand/blob/ce298c60bd7e617e38d67db8db7d34de9d37cd18/packages/docs/v4/best-practices/prompting-best-practices.mdx)

WebMCP 需要页面注册工具。固定 README 把命令式 `registerTool` API 与声明式表单探索分开。规范文件标记 `CG-DRAFT`。历史核查在完整取回的固定规范中没有找到旧符号 `requestUserInteraction`。旧示例和持续更新的浏览器指南不能因此证明当前 API 兼容。[固定 README](https://github.com/webmachinelearning/webmcp/blob/6cd745ac8a186122bd3f4aeaeb1d6cfa820251d2/README.md)、[固定规范](https://github.com/webmachinelearning/webmcp/blob/6cd745ac8a186122bd3f4aeaeb1d6cfa820251d2/index.bs)

WebMCP 的只读、后果和不可信内容注解来自工具作者。规范的非规范性安全讨论指出，恶意页面可以错误描述这些注解。代理仍需核对授权。代理也需读回实际效果。注解没有替代这两项检查。[固定规范：工具注解与安全讨论](https://github.com/webmachinelearning/webmcp/blob/6cd745ac8a186122bd3f4aeaeb1d6cfa820251d2/index.bs)

历史接收结果只把六项来源条件写入任务状态并读回。既有方法与工具路由继续保留。后续回执修正只补充 `reason` 字段。原校验器随后通过结构检查。该结果没有证明业务效果或程序采用。历史任务没有安装、执行上游、调用缓存或运行付费模型。

## ECC：按宿主区分入口与成本

ECC v2.2.3 的发布 README 列出 68 个 agents、293 个 skills 和 94 个 commands。同一发布版的 Codex 插件 README 仍写 281 个 skills。来源方另报主分支快照 `b38be6a7f6350964d59328b52f0624e1d1d552d1` 的数量为 71、314 和 98。接收方没有重读该主分支快照。以上数字来自不同文档或版本。它们没有构成 npm 分发包清单。[固定发布 README](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/README.md)、[固定 Codex 插件 README](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/.codex-plugin/README.md)、[来源方记录的主分支快照](https://github.com/affaan-m/ECC/tree/b38be6a7f6350964d59328b52f0624e1d1d552d1)

发布 README 的简易设置段落针对 Claude 插件。同一 README 另设多宿主向导，并列出 Codex 路径。因此，不能把局部设置说明推广为“ECC 不支持 Codex”。原生 Codex 插件、已弃用的旧同步方式和把 ECC 打开为工作区是三条不同路径。旧同步会写入宿主配置目录。文档要求避免把旧同步与原生插件叠加。[固定发布 README](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/README.md)、[固定 Codex 插件 README](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/.codex-plugin/README.md)

Codex 钩子投影包含 `SessionStart` 的 Node 命令定义。该入口可以执行程序。插件注册、插件启用、原生钩子信任、MCP 访问和任务授权各自独立。历史核查只读取钩子定义，没有执行命令。启动链、间接依赖和完整数据流仍未审计。[固定钩子定义](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/hooks/codex-hooks.json)

组件成本至少分列以下四项。每项都需要目标宿主的实测依据。

| 成本项 | 需要识别的内容 | 历史测量结果 |
| --- | --- | --- |
| 常驻规则与入口 | 宿主实际载入的规则和入口 | unknown |
| 按需正文 | 当前任务实际读取的技能、规则正文 | unknown |
| 目录与工具 schema | 组件目录、工具定义等元数据 | unknown |
| 子代理与运行请求 | 子代理调用、模型请求和服务调用 | unknown |

成本文档含 Claude 或具体任务的行为说明与估算。它们没有证明 Codex 的实际加载机制。`87 × 500 = 43,500 tokens` 只是文档估算。历史任务没有测得“本机固定占用 40k tokens”。历史任务也没有测得对应节省。组件数量和磁盘字节不能代替实际上下文 token。免费代码也不能证明模型或服务免费。[固定 token 文档](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/docs/token-optimization.md)、[固定上下文预算文档](https://github.com/affaan-m/ECC/blob/c05b2d6614f62f6db0047669aa4eefb223d478f9/skills/context-budget/SKILL.md)

ECC 历史任务只向既有专业说明加入一段原创成本分类，并读回该段落。既有技能与运行配置继续保留。没有安装、同步、启动、启用钩子或开启 MCP。文档合入证明知识复用；它没有证明 ECC 运行验收。

## 证据使用规则

来源方读取 X，不能证明接收方重新读取 X。浏览器资料与 ECC 的接收回执均明确保留这一差别。Compact-Adviser 回执也说明没有重读原始中文贴文；该次交接包记录的是完整自动翻译。本次导出只整理上述回执，不扩大原始阅读覆盖。

来源声明、固定文档、静态源码、本地文档读回和运行验收属于不同证据层。历史成果支持版本限定的知识复用。历史成果没有证明当前浏览器兼容、账户权限、登录状态、真实账单、模型表现、设备行为或发布结果。
