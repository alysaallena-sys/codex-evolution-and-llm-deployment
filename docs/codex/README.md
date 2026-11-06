# Codex Workflow Evolution: Reusable Methods and Validation Boundaries

This directory collects learning and adaptation records from 2026-10-31 through 2026-11-06. The compilation date is 2026-11-06. The focus is to incorporate mechanisms supported by external research into existing workflows, while retaining failures, rollbacks, and unverified items.

These documents provide original summaries of historical research. They do not provide installation instructions for the current Codex product. Pinned commits identify the versions that the historical review examined. They do not guarantee later versions. The original export phase only exported documents. That phase did not install plugins, call models, start services, or publish a repository.

## Where to Start

| Document | Question | Main topics |
| --- | --- | --- |
| [Workflow evolution](workflow-evolution.md) | How can external research on self-improvement inform an existing workflow? | FlashRSI, Harness², frozen baselines, holdout sets, rollback after failure, and integration by responsibility |
| [Validation and failures](validation-and-failures.md) | How do tests, actual effects, and completion status relate? | TokenEconomizer, negative and positive controls for local cleanup, T3 asset verification, and runtime blockers |
| [Context and tool boundaries](context-and-tool-boundaries.md) | Do caches, compaction advice, and component bundles actually reduce costs? | Compact-Adviser, Playwright, Stagehand, WebMCP, and ECC |
| [Research decisions](research-decisions.md) | Which mechanisms transfer across hosts, and which require the existing implementation? | Super-agent, Memdoor, Spec Kit, knowledge graphs, file activity panels, and loops for long tasks |

To reuse the operating method, start with workflow evolution, then read validation and failures. Before adopting a tool, examine its pinned source and evidence level. Then design a bounded validation of your own.

## Describe Evidence by Level

| Level | What it can establish | What it cannot establish |
| --- | --- | --- |
| Author or paper report | The author reported a result under specified tasks, budgets, and conditions | Local gains, general superiority, or superiority under an equal budget |
| Pinned source and documentation review | Interfaces, call order, configuration, and implementation constraints in a specified version | Execution of the code, or agreement between remote behavior and documentation |
| Local static or synthetic validation | The state of inspected files and assertion results for synthetic inputs | Acceptance of the complete product, real model requests, or every production entry point |
| Actual runtime validation | Actual behavior in a specified environment through a specified entry point | Acceptance on other devices, through other entry points, or in later versions |
| Real-device validation | Actual operations and results on a specified device | Acceptance on other devices, operating systems, or remote hosts |
| Independent acceptance | Results that another reviewer confirmed within an explicit scope | Long-term operation, cost, or security properties outside that scope |
| Publication acceptance | The version and behavior read back from the actual publication target | Publication on the basis of a build, generated files, or local tests alone |

One task can contain several evidence levels. For example, file changes can be real while behavior scores still come from synthetic text. The documents state each separately. `KEEP_BASE` means retain the existing implementation. A candidate, intake record, source review, or successful format check does not establish activation.

## Established Working Methods

1. Define the goal, permitted inputs, permitted changes, and acceptance evidence before choosing tools.
2. Pin the source commit. State which files the review read and which parts it did not read.
3. Identify existing responsibilities. Prefer integration, replacement, or deduplication. Do not create another system without a distinct responsibility.
4. Freeze the baseline, evaluation criteria, and stop conditions before editing. Retain failed candidates.
5. Give each candidate a fresh holdout set. Turn exposed counterexamples into regression cases.
6. Record actual effects. Distinguish exit codes, receipt flags, and the state of the target object.
7. Validate rollback and repeated execution. Cleanup covers only temporary resources with clear ownership, exclusive use, and no remaining purpose.
8. Record context, tool metadata, model requests, subagents, runtime, and monetary cost separately. Mark unmeasured data as unknown.

Scale these steps to the change. Small reversible changes can use fewer checks. Complex behavior changes require frozen criteria and independent acceptance. A large procedure cannot replace judgment about actual risk.

## What This Directory Does Not Establish

This directory does not establish general efficiency gains, actual token savings, stronger model capabilities, or compatibility across all platforms. It does not provide acceptance evidence for large-model deployment, real devices, or publication. Historical failures in file handoff across devices remain failures.

Some records contain only pinned source evidence. Others contain local synthetic tests. A few contain actual file changes and rollback. Each document states its scope. Research results do not authorize account operations, spending, access to protected data, or production changes.

## Public Scope and Reuse

The text contains only original method summaries, public source links, and necessary version information. This directory excludes original conversations, private resource ledgers, internal configuration, complete third-party skills or code, model weights, archives, and scripts without verified portability. The licenses of public sources continue to apply to their respective third-party materials.

The original source materials, read scopes, file hashes, and cleanup receipts remain outside the publication directory. Completion of document delivery in the original export phase did not establish that the repository was public. It also did not establish publication acceptance for any product.
