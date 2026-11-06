# Validation and Failures: Evidence Boundaries in Three Adaptation Cases

This article summarizes historical acceptance records from October 31 through November 3, 2026. The original review checked these records on November 6, 2026. It read only registered acceptance files. It did not rerun tests, programs, or services.

The three cases support one working rule: define the result, inspect the action, then read the actual result. Test counts, installation state, trust state, and file downloads answer different questions. Reports must retain those distinctions.

## 1. Describe Adaptation with Five Evidence Levels

| Evidence level | Question | Required evidence |
| --- | --- | --- |
| Source | Which version did the review examine? | Pinned commit, release tag, and asset hash |
| Static mechanism | Which execution paths could the code take? | Pinned source locations, call relationships, and conditional branches |
| Synthetic validation | Can specified inputs trigger the expected result? | Frozen inputs, negative controls, positive controls, and actual exit codes |
| Native execution | Does the real host trigger the target stage? | Host events, stage receipts, and result readback |
| Scenario acceptance | Does the target device or publication scenario meet the requirements? | Scenario operations, visible results, and independent readback |

Every conclusion must identify its evidence level. The next level requires new evidence. A passing record at an earlier level does not automatically complete the next level.

## 2. TokenEconomizer: Limits of the Local Adaptation and 322 Tests

The historical record binds to the [pinned TokenEconomizer commit](https://github.com/microsoft/TokenEconomizer/tree/1deb887bb6816188e24580f8812e65288af5757c). The local adaptation added identity constraints, scope constraints, and stage receipts. The upstream commit identifies only the base version. The local adaptation results do not represent the unmodified upstream version.

### Established Results

The local entry point requires a native session identity. It rejects a missing identity, an identity outside the allowlist, and a legacy identity override. All three synthetic negative controls returned exit code 2. The records show that none of the three produced a state result.

The adaptation binds identity before it reads the scope policy or session content. The launcher wrapper removed fixed-identity injection. Event records retain metadata only. The skill instructions describe configuration, learning, and status as separate stages. Task-status checks and learning-scope checks have distinct responsibilities.

The historical regression record contains **322 tests**, with **0 failures, 0 errors, and 0 skipped tests**. The installation-package check covered 84 files. The records show that every file matched its expected hash. The original export checked acceptance records. It did not reread the original JUnit files or the installation directory.

The historical operator reviewed five relevant event definitions individually through the native review interface. The records show completion of that review. They also retain the pending-review state of unrelated definitions. This step establishes completion of the review actions at that time.

### Incomplete Runtime Chain

Native execution encountered a session-ownership lock. Another application held the same session. The operator retained the lock and did not bypass session ownership.

At the time, the learning scope permitted only one session. That scope could not establish fact-injection behavior in a later independent session. The operator did not expand the allowlist.

| Runtime stage | Historical record |
| --- | --- |
| Actual hook trigger | Not observed |
| Allowlisted native session record | Not observed |
| Actual session folding | Not observed |
| Candidate or active facts | Not observed |
| Native fact injection | Not observed |
| Fact use in a later session | Not observed |

The records show **0** sessions actually processed and **0** injected lines. The 322 tests therefore support conclusions about local isolation and entry-point regressions. Actual learning, use across sessions, model gains, and cost savings still lack acceptance evidence.

### Reusable Steps

1. Obtain the identity that the host supplies at the entry point.
2. Validate identity and scope before reading content.
3. Add negative controls for missing and conflicting identities.
4. Check the maintained source and installation package separately.
5. Record definition-review results separately.
6. Accept each stage separately: actual trigger, recording, folding, facts, injection, and later use.
7. Stop that execution path when an ownership lock blocks it.
8. Retain regression results and incomplete stages.

## 3. Cleanup Acceptance Inspired by AiSOC: Action Return Values and Actual Effects

The historical source review binds to the [evidence-bundle design in the pinned AiSOC version](https://github.com/beenuar/AiSOC/blob/4416ebe55ca8ae1b246896c04e90e874dfa2f32c/docs/architecture/evidence-bundles.md) and the [action-dispatch source](https://github.com/beenuar/AiSOC/blob/4416ebe55ca8ae1b246896c04e90e874dfa2f32c/services/actions/app/live_actions/dispatcher.py). Those source records distinguish action-execution results from effect-verification status. That mechanism informed the local experiment.

This case applied effect verification to an existing file-cleanup entry point. The task used isolated synthetic files. It did not execute upstream AiSOC. The local synthetic acceptance evaluates only the local entry point. This article does not attribute the local results to runtime acceptance of upstream AiSOC.

### Freeze Acceptance Conditions First

Each case used a separate directory. Each directory contained one 3-byte file. Before invocation, the record fixed the source path, target path, byte hash, and file identity. Faults affected only the declared action boundary. The operator removed the injected fault before independent readback.

The negative controls required the cleanup entry point to reject completion explicitly. They also required the file to remain recoverable. Independent readback had to check the path, bytes, hash, and identity. Independent readback could not substitute for the cleanup entry point's own effect-verification result.

### The v1 Driver Failure and v2 Repair

The first driver run established no case acceptance. The driver ended with exit code 1. It did not generate the four case-result files. It then read a missing positive-control file and raised a file-not-found error. The first driver also failed to retain subprocess standard output and standard error. The operator therefore could not recover the first-run subprocess exit codes.

The failure record identified a configuration-hash mismatch. The preparation helper updated configuration on disk. The loaded configuration dictionary retained old values. Plan generation used the old dictionary to compute the hash. The subprocess reread the disk configuration and obtained the new hash.

The v2 repair changed only the task driver. The v2 driver synchronized configuration before plan generation. The v2 driver retained each subprocess's exit code, standard output, and standard error. The v2 driver used new directories to freeze inputs again. The v2 driver retained the v1 evidence. The v2 driver did not change the implementation under test. The v2 driver did not lower the acceptance criteria. The task permitted only one corrected baseline run.

### Four Cases and 67 Assertions

| Case | Fault or action | Subprocess exit code | Target-verification value | Verified cleanup count | Physical result |
| --- | --- | --- | --- | --- | --- |
| N1 | The rename adapter returns normally without moving the file | 1 | false | 0 | Source file remains; target does not exist |
| N2 | Target verification returns ENOSYS after an actual rename | 1 | false | 0 | File remains at the declared recovery location |
| N3 | Target verification returns EIO after an actual rename | 1 | false | 0 | File remains at the declared recovery location |
| P1 | Normal rename followed by target-result readback | 0 | true | 1 | Target file matches the original bytes, hash, and identity |

The four cases passed **67 driver assertions**. The independent audit returned **PASS_WITH_LIMITS**. Exit code 1 in the three negative controls means the expected rejection. Exit code 0 from the aggregate driver means that all four cases met their acceptance conditions. The aggregate exit code does not turn the three negative controls into successful cleanups.

These processes invoked the existing API through adapters. This experiment did not complete fault-injection acceptance for the full production CLI. The independent audit checked subprocess files. It did not independently witness the outermost process. The historical operator separately retained the tool observation of exit code 0 from that outermost process.

### Retain Two Coverage Gaps

The N1 receipt still contained `moved=true`. At that point, the source file still existed and the target file did not exist. This flag recorded the action adapter's normal return. It did not accurately describe the physical movement.

The frozen conditions for this run used explicit target-verification values, state, counts, exit codes, and independent path readback. N1 met this run's rejection conditions. N1 also exposed a semantic gap in a receipt field. Reports must retain both conclusions.

ENOSYS in N2 means that target-verification capability was unavailable. N2 did not cover an absent verification function, absent verification registration, a skipped invocation, or a missing result. The driver's exact Boolean comparison rejects missing or null values. This experiment did not actually inject those cases.

### Adaptation Decision

The experiment supports retention of the existing cleanup entry point. The historical decision was **KEEP_BASE**. The task added no second verifier, global skill, service, or timer. It did not change the existing cleanup implementation.

This case supports one specific method: cleanup completion must include target-result readback. A normal return establishes only that the action invocation ended. Receipt flags require interpretation alongside target results.

The historical closeout record shows that five intermediate files with no remaining purpose moved to recoverable locations. That record includes target-byte, hash, and identity checks. The positive-control sample remained available for review. Movement to a recoverable location does not establish released disk space.

## 4. T3 Code: Asset Identity Passed; Isolation Behavior Failed

This case binds to the [T3 Code v0.1.6 release](https://github.com/pingdotgg/t3code/releases/tag/v0.1.6) and the [pinned commit](https://github.com/pingdotgg/t3code/tree/2359643cffa6ba9ee84d6f2694b935de54a8013e). The historical release-API record identifies that version and its macOS arm64 asset.

### Confirmed Asset Identity

The first download encountered a TLS certificate-verification error. The record retains that error. A later revision used the system download tool with normal TLS verification to download the same pinned asset.

The historical record confirms an archive size of **109,830,529 bytes**. Its SHA-256 is `50c5dfd3e83787c182299a37db3553968346904e7dc7936b2a01061dbfcf90eb`. The record also confirms an arm64 Mach-O entry-point program inside the archive. It shows no execution of that entry point and no extraction to the filesystem. The original export checked only the asset-identity receipt. It did not read the large archive.

### Isolation Did Not Pass

The operator first used synthetic probes to check the isolation boundary. The allow group should read an authorized file. The deny group should reject a read of another synthetic file. Both the initial configuration and one adjusted configuration produced the same result: both groups ended with **SIGABRT and return code -6**. Neither group emitted diagnostic text.

A later bounded revision retained the default-deny policy. Static audit confirmed that the permission differences matched that revision's declared scope. Both groups in the new run still returned -6. Independent audit judged behavioral acceptance a failure.

The crashes do not establish that the allow group could read the file. They also do not establish correct isolation for the deny group. The record did not locate the crash in sandbox initialization, the loader, or the target-program stage. It did not confirm a root cause.

The operator then stopped permission adjustments. The actual T3 execution count remained **0**. Version commands, help commands, services, providers, and mobile use received no runtime acceptance. A successful asset download and matching architecture completed only the asset-identity level.

### Interpret Static Source Precisely

The entry-point audit of the pinned version shows that help and version arguments first load a substantial module dependency graph. The [T3 entry-point source](https://github.com/pingdotgg/t3code/blob/2359643cffa6ba9ee84d6f2694b935de54a8013e/apps/server/src/bin.ts) and [CLI source](https://github.com/pingdotgg/t3code/blob/2359643cffa6ba9ee84d6f2694b935de54a8013e/apps/server/src/binCli.ts) provide static evidence for that mechanism.

A later audit checked the [pinned Effect CLI source](https://github.com/Effect-TS/effect/blob/7f524e25cfb49a71ac39b0f44278d08d40dda5de/packages/effect/src/cli/Command.ts#L1891-L1995). That code returns after handling an active help or version action. The normal application handler follows that return path. This finding applies only to that Effect commit. The audit did not confirm that the T3 release asset embeds exactly the same Effect commit.

The scale of module loading therefore does not establish execution of the normal service handler. Top-level imports alone also do not establish provider-data reads, credential reads, or network access. Gaps remain in the complete transitive-dependency audit.

A later audit also read the [pinned dyld mapping code](https://github.com/apple-oss-distributions/dyld/blob/fd8d0c4d52320ebf64db34f3cb280310d905c5ae/dyld/Loader.cpp#L1699-L1713). That code shows a separate failure path for memory mapping. It does not identify the root cause of this -6 result. It also provides no basis for further permission expansion.

### Reusable Steps

1. Pin the release and a single asset.
2. Record download failures and retry results with normal TLS verification.
3. Check the archive hash, entry-point architecture, and runtime result separately.
4. Validate both allow and deny groups before executing the target program.
5. Check process exit codes, expected output, and actual results together.
6. Limit the number of permission adjustments.
7. Stop execution when the results do not distinguish the two groups.
8. Retain failed configurations, probe results, and independent audits.

## 5. Acceptance Checklist for Reuse

- Freeze inputs, versions, and passing conditions before execution.
- Add negative and positive controls for each critical capability.
- Save the actual exit code of each subprocess.
- Save empty output and error output.
- Independently read results from the declared locations.
- Record actions, verification, and physical retention separately.
- Retain the original failure when repairing a driver.
- Create a new frozen record for the corrected run.
- State uncovered branches in the results.
- Retain failure evidence and intentionally preserved samples.

The three cases did not complete acceptance for target devices, service publication, or use across devices. This article provides historical methods and historical evidence boundaries. Adopters must establish new acceptance records for their own versions, hosts, and target scenarios.
