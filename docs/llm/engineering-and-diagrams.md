# Integrating Engineering Methods and Checking Diagram Acceptance Coverage

This article records two completed adaptations. The first integrated defect diagnosis methods into an existing skill. The second integrated mechanism diagram generation and acceptance checks into the same entry point. Neither adaptation added a global skill. A later adaptation added rules for choosing between GUI and file tools.

Compilation date: 2026-11-06. This compilation read only historical completion turns and explicitly named original records. It did not rerun tests, start models, or change the original records. All pass results below belong to the original tasks.

## 1. Turn external methods into executable steps

The first group of methods came from Matt Pocock's skills repository. The adaptation fixed the source at commit [`49dd158d1076134a641b33efb035946536778336`](https://github.com/mattpocock/skills/tree/49dd158d1076134a641b33efb035946536778336). It adopted defect diagnosis, independent expected results, and minimal changes. It did not copy continuous interviews, tracker setup, or repeated confirmation procedures.

The adopted steps were as follows.

1. **Capture the specified failure first.** Run the check through the actual failure path. The assertion must address the symptom that the user reported. For intermittent failures, record both the attempt count and the failure count.
2. **Reduce the reproduction conditions.** Remove only one input or step at a time. Each check must preserve the same symptom.
3. **Write a prediction for each proposed cause.** Each candidate cause must produce a prediction that a probe can disprove. Each probe changes only one factor.
4. **Obtain expected results independently.** Use an identified original implementation, a specification, or an independent worked example. Assertions must not recalculate the formula from the implementation under test.
5. **Change only one observed behavior per iteration.** Reuse existing interfaces. Add an abstraction only for a specific variation or isolation requirement. Check the order, errors, and side effects that callers can observe.
6. **Check both paths after the fix.** Rerun the original scenario. Then rerun the reduced regression scenario. Delete temporary probes. Retain the first failure and the final result.

Research can continue without a runtime environment. In that case, retain static findings and mark proposed causes as provisional. Static reasoning does not replace reproduction of the actual failure.

The original task added these rules to an existing skill. Structure checks passed. Independent checks covered a numerical defect scenario and a research scenario without a runtime environment. These checks did not establish improvements for all future engineering tasks.

Method sources: [defect diagnosis](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/skills/engineering/diagnosing-bugs/SKILL.md), [testing methods](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/skills/engineering/tdd/SKILL.md), and [codebase design](https://github.com/mattpocock/skills/blob/49dd158d1076134a641b33efb035946536778336/skills/engineering/codebase-design/SKILL.md). This article explains the adapted methods. It does not distribute the upstream skill text.

## 2. Test the diagram workflow with one mechanism diagram

The diagram experiment used `diagram-design` at fixed commit [`550fd66edff058bc73056c3416b76d69cfe865ba`](https://github.com/cathrynlavery/diagram-design/tree/550fd66edff058bc73056c3416b76d69cfe865ba). The original task used the upstream light theme template, flowchart rules, offline checker, geometry checker, and SVG export script. It retained the contents of the upstream checking scripts.

The experiment produced one static numerical flowchart. The diagram explained why the same input corresponded to `149` and `150` under two recorded control states. Those results came from existing function-level records. The diagram task did not rerun the original function or start the full game.

The generation and acceptance steps were as follows.

| Step | Action | Retained evidence |
| --- | --- | --- |
| Bind content to sources | Select nodes for inputs, transformations, branches, and results; identify sources for values and states | Original numerical records and expected diagram content |
| Fix the deliverables | Generate standalone HTML with inline SVG; use system fonts | Offline resource checks and final files |
| Check structure | Check accessible names, descriptions, and canvas bounds | Check output and exit codes |
| Check geometry | Check connection paths; separately compare expected and detected connection counts | Geometry results and coverage counts |
| Check the checkers | Inject three deliberate faults: a missing description, a diagonal line, and an incorrect value | Failure results for each faulty example |
| Check rendering | Check text bounds, node layout, and scrolling in a narrow viewport | Browser measurements and screenshots |
| Bind evidence to the version | Calculate hashes for the final HTML and SVG | Correspondence between file identities and browser receipts |

The original task recorded **17/17 checks passed**. An independent agent reran the checks and obtained the same result. That rerun used retained browser receipts. It did not operate the browser again.

The desktop check confirmed text bounds. The narrow viewport check requested a width of 390 pixels and confirmed that keyboard scrolling could reveal the complete result on the right. The measured browser content width was 375 pixels. The measured diagram container width was 343 pixels. Records must distinguish the requested dimensions from the actual content area dimensions. This result did not include acceptance on a physical phone.

## 3. Confirm object detection before trusting zero warnings

The initial experiment retained an important missed detection. The diagram placed `marker-end` on a parent `<g>` element. The browser correctly displayed the inherited arrows. The fixed version of the geometry checker did not resolve that inheritance.

The checker therefore returned these results for a diagram with deliberately diagonal lines:

| Observation | Initial result |
| --- | --- |
| Expected connections | 6 |
| Connections detected by the checker | 0 |
| Problems reported by the checker | 0 |
| Checker exit code | 0 |

Exit code 0 meant only that the check reported no problems. It did not establish coverage of the diagram's connections.

The adaptation introduced two measures. First, each connection explicitly declared its arrow marker. Second, a coverage gate required the expected connection count to equal the detected count. The final diagram met `expected=6` and `detected=6`. The diagonal-line example with explicit markers then returned exit code 1. The coverage gate also correctly rejected the earlier sample with 0 detected connections.

The later skill integration recorded **10/10 checks passed**. An independent agent ran checks from the updated entry point. The agent rejected the initial diagram with missed detections and accepted the limited conclusions for the final diagram. This integration added no browser session, game execution, or execution of the original function.

Node coverage had a separate limitation. The diagram contained **7 semantic nodes**. The geometry checker used only a rectangle heuristic and recognized **6 rectangles with explicit strokes**. It did not include the decision diamond in its node checks. The early claim of “coverage of all 7 nodes” therefore exceeded the evidence. The public conclusion follows the later, narrower result: **the checker recognized all 6 connections; the diamond and text still require browser checks.**

This case supports a reusable rule: record both the problem count and the count of objects that each automated check actually covered. At least one deliberately incorrect sample must trigger a failure. Geometry checks, content checks, and actual rendering each serve different acceptance purposes.

## 4. Select GUI or file tools according to the task

The later method study used Microsoft Mage at fixed commit [`d213d430de4875c4c5c90e84b792410f704c8a23`](https://github.com/microsoft/Mage/tree/d213d430de4875c4c5c90e84b792410f704c8a23). The local adaptation adopted task allocation and acceptance methods. It did not install or run Mage.

The rules added to the existing workflow included the following:

- Preserve the specified interaction path when the user requires a browser or GUI.
- Use specialist libraries, APIs, or connectors when the task permits direct editing of structured files.
- Read back values, formulas, and saved content when checking file semantics.
- Perform interactions in the actual session when checking web behavior.
- Inspect actual rendering when checking charts and layout.
- Save, exit, and reopen as the task requires when checking persistence.
- Fix the input, initial state, tool permissions, and timing method when comparing completion times.

Matching screenshots do not establish correct file values. Correct file values do not establish correct layout. Demonstrations with different tool permissions can illustrate workflow differences. They cannot independently measure model capability.

This adaptation changed three files across two existing skills. The original task recorded passes for two format checks, three file reference checks, five scenario decisions, and fifteen scenario criteria. The first format check failed because PyYAML was missing. The original task then used an existing environment and passed the check. It did not install dependencies for this purpose.

Those results cover formatting, references, and scenario decisions. They do not cover actual web workflows, application workflows, model inference, or device outcomes. [Mage's architecture and evaluation documentation](https://github.com/microsoft/Mage/blob/d213d430de4875c4c5c90e84b792410f704c8a23/mage_vl_cowork/README.md) supplies the method source. The local pass results come from historical adaptation receipts.

## 5. Verification scope

| Evidence level | Completed work | Conclusion limit |
| --- | --- | --- |
| Upstream sources | The original tasks fixed code versions for the engineering methods, diagram tools, and Mage | This compilation did not recheck current upstream sources |
| Local static checks | The original tasks checked source identity, skill structure, references, diagram content, and file hashes | These checks do not establish the effectiveness of future skill execution |
| Scripts and deliberate failure cases | The original tasks retained the 17/17 and 10/10 results, the initial missed detection, and the correction | These results do not establish checker support for all SVG features |
| Browser | The original task retained desktop and narrow viewport measurements for this one diagram | The results do not cover physical phones, other diagram types, or animation |
| Actual workflows | The later rule adaptation passed scenario decision checks | It added no acceptance result for an actual application or model execution |

This article does not treat the early exploration of ten projects as runtime acceptance of ten projects. It also did not repeat acceptance checks for local models, inference engines, the full game, brand imports, or full plugin integration. Original records and complete hashes remain in the private evidence inventory. The public article retains only methods, fixed sources, and applicability limits.
