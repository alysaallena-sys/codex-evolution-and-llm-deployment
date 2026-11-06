# Evidence and Reproduction

A learning record should help readers locate the original material, understand the checks actually performed and judge whether the method fits their environment.

## Evidence types

| Type | What it supports | What requires separate verification |
| --- | --- | --- |
| Author or project statement | What the source publicly states | Whether the statement holds in the target environment |
| Original-source or code review | The documents, interfaces or implementation at a specified revision | Unread paths and actual runtime behavior |
| Static or synthetic checks | Results for specified inputs and assertions | Real devices, networks, accounts and product effects |
| Real local execution | Actual behavior in the specified environment | Behavior on other hardware, loads, models or inputs |
| Device or service acceptance | The final readback on a specified device or service | Cross-platform compatibility and continued availability |
| Publication readback | A particular published revision is accessible | Later changes, business outcomes and performance gains |

These types describe scope. A document can contain several types of evidence.

## Minimum record

1. The problem to solve.
2. Original links, pinned commits or versions, and observation dates.
3. Relevant environment conditions. Use generic paths and placeholders in examples.
4. Steps actually executed and the input scope.
5. Results that can be read back, and the meaning of a pass or failure.
6. Items that remain unverified.
7. The decision about the existing method: keep, merge, replace or withdraw.

## Pinned and current versions

For research on a pinned commit, retain its URL. For current functionality, pricing or service defaults, check the official source and record the observation date.

A code commit does not pin model weights. Record the weight source, revision, quantization, precision and model license separately. State any missing information.

## Comparing changes

Fix the input, environment, method and pass criteria before comparison. Retain the baseline, failures, retries and recovery path. Report quality, speed, cost or context gains only when actual measurements support them.

When no applicable improvement exists, keep the current method and explain why. A plan, a saved document or a larger skill count does not establish better results.

## Reproduction scope

This repository retains reproduction instructions that can be made public. Private originals and sensitive execution logs stay outside the notes. A sanitized summary cannot replace missing original validation. State that limitation explicitly.
