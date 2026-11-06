# Research Decisions: Mechanisms That Transfer Across Hosts

Historical review date: 2026-11-02. Export compilation date: 2026-11-06.

This page summarizes adaptation decisions across six research categories. It draws on the source reviews and acceptance records retained at the time. The original export did not retrieve upstream materials again, rerun models, or install these projects. The judgments below apply to the listed pinned commits. Later versions require a new review.

## Super-agent: Separate Context, Permissions, and Execution Ownership

The review examined a public research prototype rather than the complete internal system. The Router in the pinned source still holds some execution tools. Prompts and specific guards narrow its responsibility. The name “Router” does not establish permission isolation. A Worker runs under the operator's system identity. Directory and command wrappers provide default behavior, but they do not establish operating-system isolation. [Pinned execution documentation](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/6337fc823ce20251c8de8085948165c81aaa701e/docs/003-execution.md), [session implementation](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/6337fc823ce20251c8de8085948165c81aaa701e/src/app/sessions.ts)

The reusable mechanism is a clear division of responsibility. Route the same matter to its existing executor where possible. A subscription supplies context, but grants no new operational permissions. Record delivery, reading, and completion separately. Checkpoints retain the information that the next step needs. Long evidence retains explicit references. Each read through a reference still requires a scope check. [Pinned authorization documentation](https://github.com/deepseek-ai/dsh-superagent-prototype/blob/6337fc823ce20251c8de8085948165c81aaa701e/docs/002-authorization.md)

The actual decision retained the existing coordination, checkpoints, and evidence records. It did not activate another Watchdog, timer, cloud executor, or model router. Explicit site security restrictions blocked the original long article at the time. The review did not read its complete text or figures. The separate public-source review did not close that article-evidence gap. No local run executed the prototype or reproduced its performance results.

## Memdoor: Interpret Multiple-Role Results by Budget and Sample

Memdoor's team-solving workflow reproduces the GVS5H approach. Several fresh role instances can reduce mutual anchoring. Different roles of one model do not constitute several different models. The source's reproduction used ten questions with five runs per question. That sample requires a separate description from the task scale of the original research. [Pinned Memdoor workflow](https://github.com/guregodevo/memdoor/blob/e6fb85e7e2aab55309d191ea56f50626edaa6193/examples/workflows/team-solve/README.md), [pinned GVS5H description](https://github.com/slee-persis/GVS5H/blob/b4cc2f734a28fdab6c37af48e612c4d9e40a7a20/README.md)

The historical recalculation of public completed-run records yielded 49/50. The author's comparison records yielded 48/50. The completed-run records totaled USD 35.7914. That total did not cover every cost of interrupted runs. The records also lacked a complete comparison under equal budgets. They therefore do not establish general model superiority or a fixed cost-saving percentage. No local run reproduced this benchmark. [Public run table](https://github.com/guregodevo/memdoor/blob/e6fb85e7e2aab55309d191ea56f50626edaa6193/examples/workflows/team-solve/bench/results/parity-5pass/runs.tsv), [author comparison table](https://github.com/guregodevo/memdoor/blob/e6fb85e7e2aab55309d191ea56f50626edaa6193/examples/workflows/team-solve/bench/results/parity-5pass/authors.tsv)

The adaptation used the existing bounded division of roles, verification through actual commands, independent acceptance, and baseline retention. It did not install a shared-memory service or switch models. Model-proposed counterexamples should enter executable validation. Critical prose alone does not establish a code failure. Evaluation should also retain failures, repairs, and unfinished runs to avoid counting only successful samples.

## Spec Kit: Keep Requirements Coverage, Task Checkmarks, and Behavioral Acceptance Distinct

The pinned version provides entry points for specifications, plans, tasks, implementation, analysis, and convergence. It also includes Codex adaptation documentation. The complete specification workflow is not a prerequisite for every small change. Its analysis coverage means the proportion of requirements with at least one associated task. That metric does not replace test coverage. A convergence workflow with no actionable findings does not establish independent runtime acceptance. [Pinned README](https://github.com/github/spec-kit/blob/acf4b00b16159b003294afc797e0d30dd37d4b49/README.md), [analysis template](https://github.com/github/spec-kit/blob/acf4b00b16159b003294afc797e0d30dd37d4b49/templates/commands/analyze.md), [convergence template](https://github.com/github/spec-kit/blob/acf4b00b16159b003294afc797e0d30dd37d4b49/templates/commands/converge.md)

The reusable mechanism maps requirements, tasks, source code, and acceptance evidence. Completed checkboxes still require review against actual evidence. When a gap appears, retain the original task identifier and append a repair item. List unverified items separately. Set an iteration or cost limit for the loop. The historical task retained the existing workflow. It did not install Spec Kit, change host events, project configuration, or global skills, or run a real Spec Kit project.

## Understand Anything: Use the Graph to Guide Inspection

The pinned version organizes files, symbols, and relationships into a graph. Its difference analysis finds adjacent nodes to help order inspections. This process does not execute the program or establish that adjacency represents an actual call relationship. An empty impact list does not establish absence of impact. [Pinned source tree](https://github.com/Egonex-AI/Understand-Anything/tree/4e6d3299017a7432da15957874992837a315c5b4), [difference-analysis implementation](https://github.com/Egonex-AI/Understand-Anything/blob/4e6d3299017a7432da15957874992837a315c5b4/understand-anything-plugin/src/diff-analyzer.ts)

The incremental workflow retains old symbols and the commit baseline. It also checks version identifiers in the plan and patch. These practices support reuse. However, the selected finalization entry point does not recheck all current content in the actual workspace. It also writes the graph, fingerprints, and metadata separately. A temporary write followed by a rename for one file does not establish a transaction across multiple files. [Preparation entry point](https://github.com/Egonex-AI/Understand-Anything/blob/4e6d3299017a7432da15957874992837a315c5b4/understand-anything-plugin/skills/understand/prepare-incremental.mjs), [finalization entry point](https://github.com/Egonex-AI/Understand-Anything/blob/4e6d3299017a7432da15957874992837a315c5b4/understand-anything-plugin/skills/understand/finalize-incremental.mjs)

The historical task retained the existing retrieval and source-verification methods. Any future graph adoption should bind the graph to a source commit and workspace state. Actual call paths and tests should then validate candidate impacts. Unknown, stale, and failed retrieval states must not appear as confirmed fresh data. The historical task performed only static review. It did not generate a graph, start a dashboard, or validate automatic updates in Codex.

## File Activity Panels: Activity Signals Do Not Establish Completion

The pinned implementation of claude-files-pane v0.8.2 depends on Claude Code events and UI interfaces. It does not demonstrate an adapter for direct use in Codex. The transferable mechanism records tool contact with files, actual Git state, and acceptance results separately. [Pinned version](https://github.com/Marius-Adam/claude-files-pane/tree/3794eea05ed1fca0d23ff5307cd89182d180c9fb), [event registration](https://github.com/Marius-Adam/claude-files-pane/blob/3794eea05ed1fca0d23ff5307cd89182d180c9fb/hooks/register.tsx), [activity recording](https://github.com/Marius-Adam/claude-files-pane/blob/3794eea05ed1fca0d23ff5307cd89182d180c9fb/hooks/activity.ts)

A file color change only indicates a type of activity. It does not establish correct content, a successful commit, or publication acceptance. The activity list also has a capacity limit. It cannot replace the complete evidence record. A read-only panel does not restrict the original agent's write tools either. Future adaptation should restrict project scope before collection and indexing. It should not collect every project first and filter only the display.

The historical review read the implementation and mock-test definitions. It did not run those tests, install the panel, or accept a real UI. The actual decision reused existing task records without creating another observer across projects.

## Loops for Long Tasks: Choose Complexity from Feedback

The official engineering articles support a simple starting point. Parallel branches, orchestrators and workers, evaluation, and repair can follow when the task requires them. A loop needs environmental feedback, stage checkpoints, and stop conditions. Repeated self-invocation alone does not establish general capability gains. [Building effective agents](https://www.anthropic.com/research/building-effective-agents), [Effective harnesses for long-running agents](https://www.anthropic.com/research/effective-harnesses-for-long-running-agents)

The research also involved a video that relayed these ideas. The review did not verify its full transcript or complete chain of transmission. It therefore did not adopt the video's percentages or claims that one architecture must replace another. The adaptation retained only explicit inputs for independent branches, a single executor for shared changes, checks of actual results, and bounded retries. It added no background loop, framework, or task-activation rule.

## Repeatable Decision Steps

First, break an article's claims into specific behaviors. Then locate the corresponding entry points in pinned source. Identify host APIs, external requests, file writes, background processes, and permission sources. Next, determine whether the existing workflow already covers the responsibility. If it does, retain the baseline and record the source-specific findings. If a real gap remains, propose one candidate with a rollback path.

Candidate tests should include normal cases, failure cases, and unverified cases. A test file in the source, an acceptance requirement in a template, a panel completion indicator, and an agent's success report each establish only their respective state. A final external report still needs actual effects and the acceptance scope.
