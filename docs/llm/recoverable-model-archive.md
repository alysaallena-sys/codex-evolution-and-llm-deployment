# Recoverable Cold Archive for Local Models

Observation date: 2026-10-31.

This case completed a cold archive of two groups of local model assets. The records show that the operation deleted only five weight files after archive verification passed. The computer retained the other model files and the runtime environment. Disk space checks recorded an increase of approximately 18.82 GB in available space.

The acceptance scope covered archive integrity and release of a specified set of source files. This case did not start model inference. It also did not complete a full restoration acceptance check with the real models.

## Define the assets and deletion scope first

The asset review starts with a file inventory. The inventory must associate each source file with its size and SHA-256. The deletion plan must list specific files. A model directory alone does not define the deletion scope.

The plan in this case recorded the following scope:

| Item | Record from 2026-10-31 |
| --- | ---: |
| Model asset groups | 2 |
| Source files | 49 |
| Total source file size | 18,883,668,178 bytes |
| Weight files permitted for deletion | 5 |
| Total weight size permitted for deletion | 18,817,247,079 bytes |
| Model files to retain | 44 |
| Total size of model files to retain | 66,421,099 bytes |

Preflight checks found no symbolic links or special files. Each source file had one hard link at the time of the check. Preflight checks also inspected open files in the target model directories and specified inference processes. These findings describe that check only. They do not replace later checks.

The following table shows generic directory roles. The placeholders do not represent the actual paths in this case.

| Placeholder | Purpose |
| --- | --- |
| `<MODEL_ROOT>` | Stores local model files |
| `<ARCHIVE_ROOT>` | Stores archive parts and recovery materials |
| `<RESTORE_ROOT>` | Receives restored files |

## Use ordered parts to fit the archive medium

This case used an external FAT32 volume. The recovery instructions explicitly required a destination other than FAT32 for oversized weight files. The archive procedure first generated a standard tar stream. It then split the stream into ordered parts.

This case set the part size limit to 2,147,483,648 bytes, or 2 GiB. The complete archive contained nine parts. Each of the first eight parts occupied 2,147,483,648 bytes. The final part occupied 1,703,847,936 bytes. The complete archive occupied 18,883,717,120 bytes.

The 2 GiB value was an archive parameter for this case. It was neither a model format requirement nor a file size limit for the recovery destination. Recovery must reconstruct the original files. The recovery destination must therefore support the original weight file sizes.

The part manifest must retain the order, size, and SHA-256 of each part. The complete archive also requires its own SHA-256. A part count alone cannot establish archive content integrity.

## Make verification a deletion gate

This case recorded three levels of content verification:

1. Check the SHA-256 of each part.
2. Check the SHA-256 of the complete tar stream after concatenating the parts in order.
3. Check the size and SHA-256 of every file inside the archive.

The first full verification passed for all 49 files. An independent verification then read data through the recovery program and manifests on the archive medium. The second verification also passed for all 49 files. Both passes recorded the same SHA-256 for the complete archive.

An early review identified a limitation: archive creation used the source inventory held in memory. Completion of archive creation could therefore not directly authorize source file deletion. The later gate required independent reading of the recovery materials from the archive medium and verification of their hashes.

The deletion gate also rechecked the SHA-256 of all 49 source files. It permitted deletion of only the five weight files in the approved list. This sequence separated archive creation from authorization to release source files.

## Recovery must reject corruption and conflicting overwrites

The recovery instructions required the program to retain existing files with identical content. They also required it to reject overwrites of existing files with different content.

An early review identified a concurrency risk: another process could create a destination file during recovery. The recorded correction first wrote a temporary file, then read it back. After SHA-256 verification, the program committed the file through an atomic hard link operation that did not overwrite an existing destination.

Fixture tests used three files and ten parts. The test records contained the following results:

| Test subject | Recorded result | Supported scope |
| --- | --- | --- |
| Recovery across part boundaries | Pass | The small fixture supported recovery across part boundaries |
| Empty file | Pass | The fixture covered an empty file |
| Corrupt part | Rejected | Failed part verification stopped processing |
| Readback after recovery | Pass | Recovered fixture contents passed readback verification |
| Atomic commit without overwrite | Pass | The fixture covered the commit path |
| Concurrently created destination file | Rejected | The test preserved the file that another operation created |
| Cleanup of temporary files from this recovery | Pass | The fixture recorded cleanup results for its own temporary files |

These results support the small fixture test conclusions about the recovery mechanism. They do not prove full restoration of the real models.

## Check before and after deleting source files

Deletion requires concurrent satisfaction of the asset scope, archive integrity, and source identity checks. After deletion, check file states again. The deletion command's exit code alone is insufficient.

The checks after deletion recorded the following results:

- All five specified weight files were absent from the source directories.
- The other 44 model files passed SHA-256 verification.
- The release result on the archive medium matched the local record.
- The archive still contained nine parts.
- The complete archive hash matched the record before deletion.
- The runtime entry point still existed.

The release record explicitly stated that the operation did not start inference or stop existing services. The remaining entry point therefore establishes only that the entry file still existed. It does not establish that a model service could load the weights or perform inference.

## Distinguish logical size from available space

| Metric | Record from 2026-10-31 |
| --- | ---: |
| Logical size of deleted weights | 18,817,247,079 bytes |
| Local available space before the operation | 255,376,113,664 bytes |
| Local available space after the operation | 274,193,506,304 bytes |
| Observed increase in available space | 18,817,392,640 bytes |

The logical size of deleted files and the space change reported by the file system are different metrics. This article retains both values. It does not attribute the difference to an unverified system mechanism.

## Recovery requirements and verification limits

The recovery instructions required an internal APFS volume that supports large files and hard links. They estimated a need for approximately 19 GB of available space and recommended at least 25 GB. The model service still requires a separate check after restoration.

Both full archive verification results recorded zero restored real files. This case therefore supports three conclusions: the archive contents passed full readback verification at that time; release of the specified source files passed checks before and after deletion; and the recovery mechanism passed small fixture tests.

This case provides no acceptance results for full restoration of real models, model loading after restoration, inference output, inference performance, medium health on later dates, or long-term offline retention. This compilation did not reconnect the medium or rerun the archive program.

This article draws on the plan, two archive verification results, the part manifest, recovery instructions, review records, fixture test results, the deletion gate, the release result, and checks after deletion. All figures come from those original records dated 2026-10-31.

The original records under review provided neither external upstream URLs nor fixed model revisions. This case therefore has no external upstream version binding. Local directory names cannot establish model provenance, licenses, or versions. This article does not reproduce model weights, the archive program, or third-party code.
