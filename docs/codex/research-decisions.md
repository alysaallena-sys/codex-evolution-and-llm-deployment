# 研究取舍：跨宿主可复用的机制

历史核查日期：2026-11-02。导出整理日期：2026-11-06。

本页总结六类研究的适配判断。取材范围是当时保留的来源核查与验收记录。本次没有重新抓取上游，也没有重跑模型或安装这些项目。以下判断绑定列出的固定提交；后续版本需要重新核对。

## Super-agent：把上下文、权限和执行归属分开

核查对象是公开的研究原型，而非完整内部系统。固定源码中的 Router 仍持有部分执行工具。它的职责收窄依赖提示与具体守卫，不能把“Router”这个名称当作权限隔离。Worker 以操作者的系统身份运行；目录和命令包装器提供默认行为，无法建立操作系统级隔离。[固定执行说明](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/6337fc823ce20251c8de8085948165c81aaa701e/docs/003-execution.md)、[会话实现](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/6337fc823ce20251c8de8085948165c81aaa701e/src/app/sessions.ts)

可复用的部分是清楚的责任边界：同一事项优先交给已有执行者；订阅得到上下文，并不得到新的操作权限；投递、读取和完成分别记录。检查点保留下一步必需的信息，长证据保留明确引用。每次沿引用读取时，仍要检查范围。[固定授权说明](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/6337fc823ce20251c8de8085948165c81aaa701e/docs/002-authorization.md)

实际取舍是复用已有协调、检查点和证据记录。没有启用新的 Watchdog、定时器、云执行器或模型路由。原始长文当时受到明确的站点安全限制，完整正文与图示未读；独立公开源码核查没有补齐这项长文证据缺口。本地没有运行该原型，也没有复现它的性能结果。

## Memdoor：多角色结果必须按预算和样本解释

Memdoor 的团队解题流程复现了 GVS5H 思路。多个全新角色实例可以减少相互锚定，但不能把同一模型的不同角色写成多个不同模型。来源中的十题、每题五次复现，与原研究的任务规模也需要分开。[Memdoor 固定流程](https://github.com/guregodevo/memdoor/blob/e6fb85e7e2aab55309d191ea56f50626edaa6193/examples/workflows/team-solve/README.md)、[GVS5H 固定说明](https://github.com/slee-persis/GVS5H/blob/b4cc2f734a28fdab6c37af48e612c4d9e40a7a20/README.md)

当时对公开完成记录的复算得到 49/50；作者对照记录为 48/50。完成记录的费用合计为 35.7914 美元。这个合计没有覆盖中断运行的所有成本，也没有提供相同预算下的完整对照，因此不能推出普遍模型优势或固定成本节省比例。本地没有复现该基准。[公开运行表](https://github.com/guregodevo/memdoor/blob/e6fb85e7e2aab55309d191ea56f50626edaa6193/examples/workflows/team-solve/bench/results/parity-5pass/runs.tsv)、[作者对照表](https://github.com/guregodevo/memdoor/blob/e6fb85e7e2aab55309d191ea56f50626edaa6193/examples/workflows/team-solve/bench/results/parity-5pass/authors.tsv)

适配时采用已有的有限角色分工、实际命令验证、独立验收和保留基线机制。没有安装共享记忆服务或切换模型。模型提出的反例应进入可执行验证；单有批评文字不能证明代码失败。评估还应保留失败、修复和未完成运行，避免只计算成功样本。

## Spec Kit：需求覆盖、任务勾选和行为验收各自成立

固定版本提供规格、计划、任务、实现、分析和收敛等入口，也包含 Codex 适配文档。完整规格流程不是每次微小修改都必须采用的前提。它的分析覆盖率表示“至少有一个任务关联的需求比例”，不能代替测试覆盖率。收敛流程没有发现可操作事项，也不等于独立运行验收通过。[固定 README](https://github.com/github/spec-kit/blob/acf4b00b16159b003294afc797e0d30dd37d4b49/README.md)、[分析模板](https://github.com/github/spec-kit/blob/acf4b00b16159b003294afc797e0d30dd37d4b49/templates/commands/analyze.md)、[收敛模板](https://github.com/github/spec-kit/blob/acf4b00b16159b003294afc797e0d30dd37d4b49/templates/commands/converge.md)

可复用的是需求、任务、源码和验收证据之间的映射。已勾选任务也应接受实际证据复查。发现缺口时保留原任务标识，再追加修复项。把“尚未验证”单列出来，并给循环设置次数或成本上限。本次保留已有流程，没有安装 Spec Kit，没有改动宿主事件、项目配置或全局技能，也没有运行真实 Spec Kit 项目。

## Understand Anything：图谱提供检查线索

固定版本把文件、符号和关系组织为图谱。差异分析会寻找相邻节点，帮助安排检查顺序；这个过程没有执行程序，也没有证明相邻关系具备真实调用语义。空的影响列表不能证明修改没有影响。[固定源码树](https://github.com/Egonex-AI/Understand-Anything/tree/4e6d3299017a7432da15957874992837a315c5b4)、[差异分析实现](https://github.com/Egonex-AI/Understand-Anything/blob/4e6d3299017a7432da15957874992837a315c5b4/understand-anything-plugin/src/diff-analyzer.ts)

增量流程保留旧符号和提交基线，并校对计划与补丁中的版本标识。这些做法适合复用。与此同时，选定的完成入口没有重新核对实际工作区的全部即时内容；图谱、指纹和元数据也分别写入。单个文件的临时写入再重命名，不能代表多个文件组成一个事务。[准备入口](https://github.com/Egonex-AI/Understand-Anything/blob/4e6d3299017a7432da15957874992837a315c5b4/understand-anything-plugin/skills/understand/prepare-incremental.mjs)、[完成入口](https://github.com/Egonex-AI/Understand-Anything/blob/4e6d3299017a7432da15957874992837a315c5b4/understand-anything-plugin/skills/understand/finalize-incremental.mjs)

本次保留已有检索与源码核验方式。未来若采用图谱，应绑定源码提交和工作区状态，再用实际调用路径与测试验证候选影响。未知、陈旧和获取失败都不能显示为已确认的新鲜状态。本次只做静态核查，没有生成图谱、启动看板或验证 Codex 自动更新。

## 文件活动面板：观察提示不能代替完成证据

claude-files-pane v0.8.2 的固定实现依赖 Claude Code 的事件与界面接口。它没有展示可直接放入 Codex 的适配层。可跨宿主复用的机制是把工具触碰文件、真实 Git 状态和验收结果分别记录。[固定版本](https://github.com/Marius-Adam/claude-files-pane/tree/3794eea05ed1fca0d23ff5307cd89182d180c9fb)、[事件注册](https://github.com/Marius-Adam/claude-files-pane/blob/3794eea05ed1fca0d23ff5307cd89182d180c9fb/hooks/register.tsx)、[活动记录](https://github.com/Marius-Adam/claude-files-pane/blob/3794eea05ed1fca0d23ff5307cd89182d180c9fb/hooks/activity.ts)

一个文件变色，只能提示发生了某类活动。它不能证明内容正确、提交成功或发布通过。活动列表还有容量限制，因此不能替代完整证据记录。只读面板同样不能限制原代理的写入工具。未来适配应在采集与索引之前限定项目范围，不能先采集所有项目再过滤展示。

当时阅读了实现与模拟测试定义，没有运行这些测试，也没有安装面板或验收真实界面。实际取舍是复用现有任务记录，不另建跨项目观察器。

## 长任务循环：根据反馈选择复杂度

官方工程文章支持从简单方案开始，再按任务需要加入并行分支、调度者与执行者、评价与修复。循环需要环境反馈、阶段检查点和停止条件。重复调用自身不能单独证明通用能力提升。[Building effective agents](https://www.anthropic.com/research/building-effective-agents)、[Effective harnesses for long-running agents](https://www.anthropic.com/research/effective-harnesses-for-long-running-agents)

该研究还涉及一段转述视频。完整字幕和全部传播链没有核实，因此没有采用其中的百分比或“某种架构必然替代另一种架构”的结论。适配只保留独立分支的明确输入、共享改动的单一执行者、真实结果核对，以及有限重试。没有新增后台循环、框架或任务激活规则。

## 一套可重复的取舍步骤

先把文章中的主张拆成具体行为，再到固定源码中找到相应入口。确认宿主 API、外部请求、文件写入、后台进程和权限来源。随后判断既有流程是否已经覆盖该职责。已有覆盖时保留基线，并保存来源特有的发现。出现真实缺口时，再提出单个可回退候选。

候选测试应同时包含正常情况、失败情况和未验证情况。源码中存在测试文件、模板写有验收要求、面板显示完成，以及代理报告成功，都各自只说明对应状态。对外报告最终结果时，仍须给出实际效果与验收范围。
