# From Research Mechanisms to a Reusable Agent Workflow

Historical observation period: 2026-10-31 through 2026-11-06. The main adaptation and scoring records date from 2026-11-01. The original review checked existing records on 2026-11-06. It did not rerun the upstream frameworks.

This research produced an adaptation method with versions, tests, and rollback conditions. The changes reused the existing task-coordination skill, learning skill, and evaluation reference document. The records do not establish higher efficiency on real tasks. They also do not establish a Pareto improvement or a Kaldor improvement.

## Distinguish Four Evidence Categories First

| Evidence category | What these materials can establish | What these materials cannot establish |
| --- | --- | --- |
| Upstream author tests | Reported results under a particular paper protocol | Effects in the current desktop product |
| Pinned source review | Mechanisms and interfaces in that version | Availability of those interfaces in the current environment |
| Synthetic text tests | Preset behavior requirements that the answers cover | Execution of the actions that the answers describe |
| Actual file changes and readback | Agreement of specified file content, modes, and hashes with the records | Loading of rules by a native session, or faster real tasks |

Independent scoring means only that another scorer checked the frozen answers. It does not constitute independent experimental reproduction. A single round of text pass rates cannot replace repeated runs, complete cost records, or acceptance on real tasks.

## FlashRSI: Adopt Experimental Discipline

The historical review pinned FlashRSI to a [public commit in RUC-NLPIR/FlashRSI](https://github.com/RUC-NLPIR/FlashRSI/commit/dea1b1d0285e3328234a1e344562bb9e54ce14f7). That version records 13 algorithms, 30 benchmarks, and 5 harness integrations. An earlier post mentioned 12 methods, more than 30 benchmarks, and 3 harnesses. The two counts reflect different observation times. Neither replaces the other.

FlashRSI places algorithms, benchmarks, and agent harnesses within a unified experimental structure. Its candidate versions mainly change resources that the agent uses. The structure itself does not establish training of the base model's weights. The review also notes that this version's Codex integration uses a Python semantic port based on rust-v0.147.0. That integration does not constitute control of the current desktop session or establish reuse of the existing login.

The adaptation did not install FlashRSI. The actual changes extracted seven requirements from the existing workflow:

1. Save the actual baseline and a recovery copy.
2. Record each candidate's parent version and file hashes.
3. Freeze scope, criteria, holdout cases, and budget before editing.
4. Separate development cases from unexposed acceptance cases.
5. Check permissions, data scope, and protected boundaries first.
6. Record evaluation results, current authorization, file readback, and actual runtime acceptance separately.
7. Check the current candidate hash before rollback, then restore content and file modes.

The existing task-coordination skill retained responsibility for state, resources, and cleanup. An on-demand reference document held the adaptation-evaluation requirements. The existing learning skill gained a cross-reference. This arrangement added no skill bundle, database, background program, or timer.

The actual file records show that the task-coordination entry point grew from 10,353 bytes to 11,166 bytes, an increase of 813 bytes. The on-demand reference document contained 8,081 bytes. The learning skill grew from 2,537 bytes to 2,981 bytes, an increase of 444 bytes. These figures measure file size. They do not measure model-token usage.

The synthetic text tests contained 3 development cases and 4 holdout cases. Each version generated only one frozen answer set. Independent scoring ran only once.

| Measure | Baseline | Candidate |
| --- | ---: | ---: |
| Development cases passed | 2/3 | 3/3 |
| Holdout cases passed | 3/4 | 4/4 |
| Total cases passed | 5/7 | 7/7 |
| Mandatory requirements covered | 47/49 | 49/49 |
| Prohibited-behavior violations | 0 | 0 |

File readback checked 5 candidate files. Static checks covered 84 files within the package. A recovery drill checked copy content and modes. These results establish bounded file changes and checks. They do not establish loading by a real session, actual tool execution, or successful native rollback.

## Harness²: Integrate Three Mechanisms

The historical review pinned Harness² to a [public commit in google-research/harness2](https://github.com/google-research/harness2/commit/1cfe254e8d25b15f37048c3730134686abe60335). The paper version is [arXiv:2610.14224v1](https://arxiv.org/html/2610.14224v1). The upstream loop proposes candidates, probes them in pairs, and combines them selectively. The loop permits baseline retention.

Under the specified WorkBuddy protocol, the authors reported that GLM-5 with OpenCode increased its mean score from 64.2 to 75.7, a gain of 11.5 points. With Codex, the mean increased from 64.4 to 75.3, a gain of 10.9 points. The paper reports means and standard deviations across three runs. Each run shuffles task order. These results belong to the authors' combinations of models, harnesses, and benchmarks. They are not results of this adaptation.

The adaptation integrated three mechanisms into the existing evaluation reference:

| Mechanism | Adapted operating requirement | Evidence boundary |
| --- | --- | --- |
| Record effects by change | Number each change and cite specific behavioral differences between baseline and candidate | Simultaneous changes can still confound each change's effect |
| Selective combination | Choose the baseline, candidate, or merged changes for each unit, then test the final combination | Passing components do not guarantee a passing combination |
| Reuse experience conditionally | Save applicability conditions, supporting evidence, failure cases, and counterexamples | A later task does not automatically inherit a previous task's specific configuration |

Effect records can use four judgments: “helped,” “harmed,” “no observed effect,” and “confounded.” Each judgment must cite an actual comparison. Without isolating evidence, the record should retain “confounded.”

The main skill entry point gained 0 bytes in this integration. The on-demand reference grew from 8,081 bytes to 12,406 bytes, an increase of 4,325 bytes. The change increased reading cost. Actual tokens, total elapsed time, and monetary cost remain unknown.

### First Round: Candidate Regression

The first round contained 2 development cases and 4 holdout cases. The baseline passed 6/6. The candidate passed 5/6, including 3/4 holdout cases.

The failure concerned an acceptance requirement. The candidate made mandatory independent acceptance optional. This round failed final integration acceptance. The operator restored the actual maintained file to its pre-adaptation reference version. The record retains the failed candidate, scores, and restored file hash.

This rollback establishes actual file restoration. It does not establish native rollback within a running agent session.

### Second Round: Equal Scores, Different Defects

The second round began with a new frozen plan. The previously exposed failure case became a development regression case. The evaluation added 4 entirely new holdout cases. The round contained 3 development cases and 4 holdout cases in total.

| Second-round measure | Baseline | Candidate |
| --- | ---: | ---: |
| Development cases passed | 2/3 | 2/3 |
| New holdout cases passed | 4/4 | 4/4 |
| Total cases passed | 6/7 | 6/7 |

The candidate corrected the wording that made independent acceptance optional. It still lacked sufficient repeated comparisons. It scheduled one run per build configuration, followed by one independent acceptance check. That plan could not estimate run-to-run variation. The baseline retained a different defect: its independent-acceptance requirement remained too weak.

The second round therefore ended with equal total scores. It did not achieve a complete synthetic pass. The three mechanisms and acceptance wording changed together. The records cannot isolate the causal contribution of each change. Later concurrent additions to the entry point received only static checks. They did not receive another independent behavioral score together with the new reference document.

The final record retained the authorized documentation changes. That retention decision does not automatically make the candidate the winner. It also does not establish actual quality or cost improvements.

## Autonomous Learning Rules and the awesome-rsi Review

The historical screening pinned the catalog to a [public commit in lobehub/awesome-rsi](https://github.com/lobehub/awesome-rsi/commit/632ab5065bf579c7d1daa71bdaab801fdefd3698). Its inventory contained 31 sections, 252 entries, and 252 distinct entry URLs. The screening assigned one intended-use judgment to each entry.

| Initial intended-use judgment | Entry count |
| --- | ---: |
| Requires a new harness | 67 |
| Existing mechanisms already cover it | 17 |
| Background knowledge | 59 |
| Candidate method for direct reuse | 27 |
| Involves training or infrastructure | 71 |
| Source not yet verified | 11 |
| Total | 252 |

These judgments screen relevance only. They do not independently validate every entry description. The research read methods and limitations for 12 research subjects. Those reviews covered 16 catalog entries. The remaining 236 entries stayed at the catalog-evidence level. The 12 subjects and 16 entries use different counting units.

The learning established three separate evaluation concepts: better scores within a task, retained gains across tasks, and stronger capability in the improvement process itself. A recursive structure alone does not establish the third. Available code alone also does not establish complete reproduction. Task sources, scoring logic, data, evaluation environment, and missing components all affect reproduction conclusions.

The autonomous-learning requirements joined the existing global requirements. An original summary follows: when unfamiliar materials relate to the task, check original sources first. Complete the learning that the current task requires. Continue already authorized reversible adaptation. Check actual results. When necessary information is missing, ask only for the missing item. Learning must continue to respect authorization boundaries for read-only scope, protected data, accounts, spending, production, and irreversible operations.

The rules file grew by 658 bytes. Independent synthetic scoring passed 4/4 scenarios and 12 mandatory requirements. The scorer found no answer that endorsed prohibited behavior. This result does not establish automatic loading in new sessions, completion of real tasks, or generalization across tasks.

## Reusable Operating Sequence

The sequence below summarizes the historical method. Each actual task still needs its own read scope, authorization, and acceptance criteria.

1. Check task ownership and material scope. Filter for permitted sources before reading the text.
2. Pin the original source version. Record the commit, observation date, and actual coverage.
3. Distinguish author reports, source facts, synthetic behavior, and actual runtime evidence.
4. Check the responsibilities of existing skills. Prefer retention, integration, or replacement of local rules.
5. Save the actual baseline. Record content hashes, recovery materials, and file modes.
6. Freeze the candidate, budget, and evaluation criteria. Isolate development cases from unexposed holdout cases.
7. Run paired comparisons. Match relevant conditions and schedule repetitions for run-to-run variation.
8. Record helped, harmed, no observed effect, or confounded for each change. Test the final combination that will actually apply.
9. Check hard constraints first, then compare gains and costs. Keep unknowns when full cost data is missing.
10. Check current authorization before applying the candidate. Read back the applied state, then perform acceptance on the real task.
11. Retain failure evidence and counterexamples. Turn exposed cases into regression material and prepare fresh holdout material.
12. Check temporary-resource ownership before cleanup. Record cleanup receipts separately from acceptance results.

These records support the conclusion that workflow changes can remain auditable. Actual runtime effects, complete costs, stability, and gains across tasks still require independent evidence. Without those data, a Pareto improvement claim lacks support. A Kaldor comparison also requires explicit gain and loss criteria, weights, and verifiable compensation conditions.

## Public Sources and Reuse Scope

The original article summarized these mechanisms in original Chinese prose. This English translation retains that summary. The article does not copy complete third-party skills, article text, or source code. The historical FlashRSI and Harness² reviews recorded Apache-2.0 framework licenses. Upstream data, models, benchmarks, and other components retain their own terms. Catalog inclusion grants no installation or redistribution authorization.

The public links pin the historical research subjects. The original export did not revalidate web pages online. It did not convert historical results into commitments about current product operation.
