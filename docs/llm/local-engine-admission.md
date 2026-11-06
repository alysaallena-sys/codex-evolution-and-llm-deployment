# Local Models and Inference Engines: Establish Fit Before Deployment

Observation dates: 2026-10-22 through 2026-11-04. Compilation date: 2026-11-06.

This article summarizes historical asset reviews, research at fixed source code versions, and adoption of candidate screening knowledge. It does not rank the current “best models.” This compilation did not download weights, start services, or rerun inference.

## Distinguish four kinds of evidence first

| Evidence | What it establishes | What it does not yet establish |
| --- | --- | --- |
| Model files exist on disk | Someone previously obtained those files | The current service uses them |
| Configuration contains model and engine names | The configuration expresses an intended setup | Correct dependencies, a working endpoint, or correct generated results |
| A process exists or a connection check passes | The corresponding process exists, or the specified endpoint accepted a connection during that check | Acceptance of the specified model, modality, and feature |
| A fixed task produces results that can be read back | Actual behavior under those conditions | The same behavior for other models, devices, or future versions |

The historical review found two sets of local weights and MLX engine configuration. It did not obtain runtime acceptance evidence for the inference service at that time. The search did not find another common tool at the inspected installation locations or service entry points. This establishes only that the search did not find it. It does not establish that nobody had ever installed it. Public examples omit personal paths, ports, and device identifiers.

## A reusable candidate admission sequence

1. **Identify the actual source.** Record the publisher, base model, derived model, and weight license separately. A publishing organization's name does not establish the base model's identity.
2. **Fix the complete version.** Record the code commit, inference engine version, quantization format, weight revision, and required dependencies. Successful loading does not establish a correct computation path.
3. **Check the device path.** Distinguish CPU, GPU, Metal/MPS, and MLX implementations. A CPU policy for one component does not establish CPU-only support for the complete service.
4. **Estimate total resource requirements.** Weight size accounts for only part of memory use. Include the runtime framework, caches, context, temporary buffers, and concurrency.
5. **Check content destinations.** Review weight downloads, image URLs, telemetry, request logs, caches, and cloud object storage separately. Local code execution does not establish that content stays on the computer.
6. **Design a minimal acceptance check with actual execution.** Fix the input, expected output, tool permissions, timeout, and exit conditions. Execute only within the authorized scope. Retain candidate status or `KEEP_BASE` when conditions are incomplete.

Historical model screening on 2026-10-25 also exposed a dependency version issue. That review listed the MLX 4bit version of LFM2.5-24B-A2B as the first candidate to try. It listed the MLX quantized version of Granite 4.2 8B as another resource candidate. At the time, the LFM model card required MLX-LM 0.32.0 or later. The historical material recorded that an older version might load the model while routing experts incorrectly. That round did not download candidates or perform inference. Its source assessment therefore does not constitute a runtime pass or a current recommendation.

This historical navigation comes from the final research response from that round. There is no separate model screening original record or fixed model card revision. This compilation does not add a current model ranking. Sources: [Liquid's official explanation](https://www.liquid.ai/blog/lfm2-5-24b-a2b), [LFM MLX model card](https://huggingface.co/LiquidAI/LFM2.5-24B-A2B-MLX-4bit), [IBM's official explanation](https://research.ibm.com/blog/introducing-granite-4-2), and [Granite MLX model card](https://huggingface.co/ibm-granite/granite-4.2-8b-q4-mlx).

## Case one: Mage-VL-Cowork labels, benchmarks, and platforms

The earlier Kapitsa review on 2026-10-22 followed the same principles. Its historical completion response noted that power modes, quantization, and replay protocol differences affect comparisons. That round completed source review only. It did not run a local model or retain a separately named source verification original record. This article keeps it as historical navigation with weaker evidence. It does not claim benchmark reproduction. Source: [fixed Kapitsa commit](https://github.com/nace-ai/kapitsa/tree/5b20f648ce519f5dd27ac9de54ca1f5f53e2cdb6).

Observation date: 2026-10-31. Fixed code commit: `d213d430de4875c4c5c90e84b792410f704c8a23`.

The model card states that the backbone includes Mage-ViT and Qwen3-4B-Instruct-2507. Model provenance review must therefore continue through the base weights. It cannot stop at the publisher's label. Source: [model card](https://huggingface.co/microsoft/Mage-VL-Cowork).

The authors reported an average of approximately 66.04% across two OSWorld-Verified runs. They also documented task exclusions and a 50-step budget. This is an author result under specified conditions. This compilation did not reproduce it. Source: [fixed README](https://github.com/microsoft/Mage/blob/d213d430de4875c4c5c90e84b792410f704c8a23/mage_vl_cowork/README.md).

In the official spreadsheet demonstration, one workflow used Python file tools. The other mainly used GUI tools. Different tool permissions change the execution path. The time difference therefore cannot entirely establish a difference in model inference speed. A fair comparison must fix tools, inputs, initial state, and timing methods. It must also report one-time environment preparation costs separately. Source: [official demonstration](https://microsoft.github.io/Mage/cowork/).

Approximately 9.48 GB of BF16 weight files does not equal total runtime memory. The fixed evaluation materials used GPU containers and desktop virtual machines. That study did not establish an official Apple Silicon/MLX/Metal path. The conclusion was insufficient evidence for deployment on that platform. It was not a finding of absolute incompatibility. Source: [evaluation environment](https://github.com/microsoft/Mage/blob/d213d430de4875c4c5c90e84b792410f704c8a23/mage_vl_cowork/osworld_eval/README.md).

## Case two: FreeToken's partial CPU capability does not establish Mac support

Observation date: 2026-11-03. Source commit: `9cacd0896c9beb67d88c22a38be54236023b4605`. The stable release record separately identified `v0.2.1 / ba31db2ea708b61d7313bccb3ee4adf9d11ecb90`.

The inherited review of fixed source code supplied no evidence of native macOS/Metal support. Linux, Windows, or experimental AMD paths do not automatically establish Mac support. The MoE CPU policy concerns only some expert computation. It does not replace review of the full dependency and GPU paths. Source: [fixed installation instructions](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/docs/install.md).

The material also distinguished local directories from remote model identifiers. Remote identifiers may trigger weight downloads. Image URLs may also require network access. Optional request logging requires a separate check. API compatibility does not require use of that API brand's cloud service. It also does not establish equivalence across all protocol behavior. Sources: [model documentation](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/docs/models.md) and [request logging source](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/python/freetoken/server/request_logger.py).

The direct source recheck in that round encountered an unavailable tool and obtained no new page content. This public article therefore identifies these findings as inherited conclusions. The actual decision retained the existing deployment plan as `KEEP_BASE` and registered a candidate only. The task did not install the engine or call a model.

The engine code uses Apache-2.0. That license does not replace review of model weight licenses. Source: [fixed license](https://github.com/FlashML-org/FreeToken/blob/9cacd0896c9beb67d88c22a38be54236023b4605/LICENSE).

## Case three: SIE requires separate acceptance checks for each Mac path

Observation date: 2026-11-04. Fixed commit: `8563ef3bf92e181c7ddd32356be78d7a15599d45`.

The inherited source review distinguished MPS embedding/rerank on Apple Silicon from a separate MLX text generation path. The MLX path had image, video, and grammar limitations. Its presence does not establish Mac availability for all models or tools. Sources: [fixed project documentation](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/README.md) and [MLX generation adapter](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/adapters/mlx/generation.py).

The material recorded that the adapter accepted `revision` but did not pass it to the subprocess. Fixing the SIE code version therefore did not fix the actual model weights. Later runtime acceptance must check the actual download source and weight revision. Source: [MLX subprocess implementation](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/adapters/mlx/_server.py).

The server version in the same commit was 0.11.0. The material recorded these defaults: listening on all network interfaces; unauthenticated mode when both authentication configuration and a token were absent; and enabled telemetry. README statements about loopback listening and telemetry disabling conditions for the future 0.13.0 version do not apply to this commit. The MCP edge anonymous switch and connector secret conditions require separate checks. Sources: [CLI](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/cli.py), [authentication](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/core/server_auth.py), and [telemetry](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/packages/sie_server/src/sie_server/observability/telemetry.py).

The absence of prompts from a particular anonymous telemetry payload does not establish their absence from all logging, proxy, or observability paths. Cache fallback, initial weight downloads, and cloud storage require separate explanations.

Adoption covered candidate screening knowledge only. The task did not install software, replace a deployment, or run a model. The promotional 98%/3% figures lacked the original experiment definition. The available quality and fixed-rate records did not replace that benchmark. This compilation did not validate cost or quality benefits. Source: [public benchmark methodology](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/examples/evaluations/published-benchmarks/README.md).

The code uses Apache-2.0. Each model license and cloud resource cost requires an independent check. Source: [fixed license](https://github.com/superlinked/sie/blob/8563ef3bf92e181c7ddd32356be78d7a15599d45/LICENSE).

## Evidence scope

- **Source research:** fixed version materials and existing review findings. The assessment retains failures to read some external sources.
- **Local static results:** the task documented and read back candidate conditions. It explicitly retained version, scope, and source limits.
- **Actual local execution:** this research obtained no runtime acceptance result for the candidate engines or models above.
- **Devices and publication:** the work added no device tests or deployment publication.

The admission sequence and evidence distinctions are reusable. Inclusion in candidate documentation does not constitute admission to production.
