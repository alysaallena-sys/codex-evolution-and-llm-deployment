# Remote Model Gateway Admission: Quotas, Costs, Model Identity, and Content Destinations

This article presents a method for screening remote model gateways. The case fixes the source at `tashfeenahmed/freellmapi@73e3f05843c6d6d7041171225a27defa6a82ecf1`. The source package bears the date 2026-11-06. This article inherits the package's review findings for selected source code paths and official documentation from three providers. It did not revisit upstream pages.

The work completed knowledge organization and static document checks. It did not run the gateway, call a model, or verify an actual bill. Provider quotas below represent only the official documentation snapshots in the source package dated 2026-11-06. Readers must recheck terms and account eligibility before actual integration.

## Identify the gateway's role first

FreeLLMAPI forwards requests to remote providers. It does not supply local model weights. Deploying the gateway program does not establish local model inference.

Admission of local weights usually requires review of model provenance, weight version, weight license, format, quantization, memory, and disk space. A remote gateway also requires review of upstream accounts, quota ownership, billing conditions, and recipients of request content. Both sets of conditions serve specific purposes.

The author's model counts, endpoint counts, and monthly token totals describe catalog scale under the author's counting method. They do not establish that a particular account has those quotas. A catalog subscription also does not include inference quota. Source: [fixed version README](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/README.md).

## Calculate shared quotas by account or project

Identify the entity that owns a quota before calculating the total. Multiple keys may share one account or project quota. Multiplying a single quota by the number of keys can count the same shared pool more than once.

The table restates only **the three official documentation snapshots in the source package dated 2026-11-06**. These figures do not represent current available quotas or runtime results for any account.

| Provider | Official conditions in the source package | Candidate admission assessment |
| --- | --- | --- |
| Google Gemini API | Quotas apply to a shared project. Keys do not have independent quotas. | Group keys by project first. Then check the project's actual limits. |
| OpenRouter | Free models allow 50 requests per day before the documented credit purchase condition; they allow 1000 requests per day after that condition. Failed requests also count toward the daily limit. | The fixed source code's default of 1000 lacks sufficient conditions by itself. Check account eligibility before setting local limits. |
| Cloudflare Workers AI | The free allocation is 10,000 neurons per account per day. Paid conditions may incur overage charges. | Aggregate usage by account. Check local estimation thresholds separately from provider billing limits. |

Official sources: [Gemini rate limits](https://ai.google.dev/gemini-api/docs/rate-limits), [OpenRouter limits](https://openrouter.ai/docs/api_reference/limits), [OpenRouter free model catalog](https://openrouter.ai/collections/free-models), and [Cloudflare Workers AI pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/). These pages can change. This article did not check changes after the source package date.

## Separate the success ledger, failed-attempt consumption, and actual bills

The source package recorded a default monthly cap of `0` in the fixed version. Here, `0` means unlimited. Integrators must actively set a limit. Source: [monthly budget implementation](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/services/key-budget.ts).

| Record or mechanism | What it establishes | What it does not establish alone |
| --- | --- | --- |
| Token estimate | Request size according to local estimation rules | Exact usage for the provider's final settlement |
| SQLite monthly ledger of successful requests | Cumulative successful requests that the gateway recorded | All consumption from failed attempts or all charges |
| In-memory lease in the current process | Temporary allocation that the current process registered | Complete provider accounting across processes, keys, and clients |
| Local rate limiting and synchronization | The gateway applies limits according to local state | The provider has rejected every over-limit request |
| Provider usage records and bills | Usage and settlement records for the actual account | Acceptance of request content handling, actual model identity, or client compatibility |

Failed requests can consume quota. The package's official OpenRouter snapshot explicitly counted failed requests toward the daily limit. Whether a failed request incurs a monetary charge requires a new check for the actual provider and request. Request failure does not establish zero consumption. Source: [rate limiting implementation](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/services/ratelimit.ts).

The Cloudflare path's local estimation threshold of 9000 neurons does not constitute a hard provider billing cap. Estimation error, other requests on the shared account, and best-effort synchronization can cause differences between the two sets of records. Paid overage conditions also require separate treatment. Source: [Cloudflare usage handling](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/services/cloudflare-neurons.ts).

“Free model,” “local cap configured,” “successful requests only in the ledger,” and “request failed” therefore do not guarantee zero cost. A zero-cost claim requires evidence of actual account conditions, consumption from failed attempts, and provider bills.

## State the limits of retry counts and time budgets

The source package recorded defaults of 20 total attempts and a 45-second base budget. The first two attempts had budget exemptions. Historical time to first byte (TTFB) from successful requests could also relax the budget. These defaults therefore do not establish a strict stop within 45 seconds. Sources: [fallback loop](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/lib/fallback-loop.ts) and [time budget handling](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/lib/ttfb-budget.ts#L162-L179).

Admission records must separately state the total attempt count, time budget, exemption conditions, and relaxation conditions. If later execution receives authorization, it must also check actual cancellation, timeout responses, and upstream abort behavior. A retry budget does not replace a cost budget.

## Establish model identity from the actual source

The source package recorded default mappings from `opus`, `sonnet`, and `haiku` to the `auto` pool. An alias alone does not establish use of the corresponding Claude model. Check the final provider, actual model identifier, and provenance information in the response. Source: [alias mapping implementation](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/services/anthropic-map.ts).

Responses or Messages protocol conversion establishes only that the gateway offers the corresponding interface conversion path. It does not establish compatibility with a particular client. Client acceptance also requires evidence from actual requests, streaming output, tool calls, and error handling. This article did not complete those acceptance checks. Sources: [free model route](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/routes/free-tier.ts) and [fallback route](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/routes/fallback.ts).

## Check content destinations, logs, and caches separately

The review of fixed source code in the package recorded three conditions that require separate treatment:

1. Analytics saved raw IP addresses and User-Agent values by default. This behavior differed from the documentation's NoPII and IP-hash descriptions. `REQUEST_ANALYTICS_LOG_CLIENT=false` disabled only this client information record. It did not establish that all logging had stopped.
2. Encryption of keys at rest protected stored keys. It did not prevent upstream providers from reading the prompts they received.
3. The optional SQLite response cache used plaintext. Its activation conditions, access scope, and retention period require separate checks.

Fixed sources: [client information handling](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/lib/client-context.ts), [request log handling](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/lib/request-log.ts), and [fixed version README](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/README.md). This article retains the package's summaries of caching and encryption. It did not independently review every implementation path.

The package also recorded that the catalog contacted a signed update service every 12 hours by default. That interaction included version information and optional license information. This record does not exhaust all outbound gateway behavior. Source: [catalog synchronization implementation](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/server/src/services/catalog-sync.ts).

## Reuse one admission procedure

1. **Fix the source.** Retain the repository name, commit, review date, and license. Record whether each conclusion comes from original documentation, source code review, or runtime observation.
2. **Identify the inference location.** Specify local weights or remote providers. For remote paths, list the final recipients of content.
3. **Aggregate shared quotas.** Group keys by actual account or project. Check free, credit purchase, and Paid conditions. Do not multiply shared quotas by key count.
4. **Check cost limits.** State the default meaning of the cap. Separate successful usage, failed attempts, local estimates, and provider bills. Do not promise zero cost without billing evidence.
5. **Check retry limits.** State the attempt count, base budget, exemptions, and relaxation conditions. When a strict deadline matters, make actual stopping behavior a separate acceptance condition.
6. **Check model provenance.** Trace aliases to actual providers and model identifiers. Check protocol conversion separately from compatibility with a specific client.
7. **Check content and retention.** Review prompt destinations, raw client information, request logs, plaintext caches, and catalog update interactions. Record switches, defaults, and verification gaps for each item.
8. **Make a bounded decision.** Approve only verified uses when the conditions are complete. Retain the existing deployment decision when conditions are insufficient. Adopt candidate screening knowledge only when runtime evidence is absent.

These steps support initial screening during document review. Account operations, model calls, payments, production changes, and publication each require their own authorization. Document screening does not expand execution permissions.

## Correct common claims

| Original claim | Acceptable statement |
| --- | --- |
| “Multiple keys multiply the quota.” | “Aggregate the shared pool by account or project first. Then check the actual quota.” |
| “The monthly cap is 0, so there are no charges.” | “This fixed version uses 0 to mean unlimited. Actual charges still require reconciliation.” |
| “The ledger records only successes, so failures consume nothing.” | “The success ledger does not cover all failed-attempt consumption. Check failure rules for each provider.” |
| “The default budget is 45 seconds, so requests always stop within 45 seconds.” | “The base budget has exemptions and relaxation conditions. A strict deadline still requires runtime acceptance.” |
| “The request uses the opus alias, so the actual model is Claude.” | “The alias enters the auto pool by default. The actual model source still requires verification.” |
| “Key encryption keeps prompts local.” | “Key encryption at rest does not prevent upstream receipt of prompts.” |
| “Disabling client information records disables all logs.” | “The switch covers specified records only. Other logs and caches require separate checks.” |
| “The MIT code license removes provider, model, and cost restrictions.” | “MIT covers the corresponding code. Model rights, provider terms, and billing conditions require separate checks.” |

## Apply acceptance checks at each evidence level

| Level | Evidence required for a pass | Status in this article |
| --- | --- | --- |
| Sources and versions | Fixed commit, date, license, and original links | Inherited from the source package. This article did not reopen upstream sources. |
| Static knowledge organization | Conclusions match source scope; the article retains limitations and avoids claims beyond the evidence | Complete. |
| Gateway execution | Observations of actual routing, retries, cancellation, logs, and caches | Unverified. |
| Client and model | The specified client completes the target workflow; actual model provenance is clear | Unverified. |
| Quotas and bills | Actual account eligibility, shared pool usage, failed-attempt consumption, and bill reconciliation | Unverified. |
| Product or production | The specified use meets acceptance conditions; the publication target and rollback conditions are clear | Unverified. |

The adaptation decision covered only adoption of remote gateway candidate screening knowledge. It retained the existing deployment plan. This article does not establish gateway deployment, actual model calls, or zero-cost operation.

## Source scope and rights

The fixed upstream source is [FreeLLMAPI commit 73e3f05843c6d6d7041171225a27defa6a82ecf1](https://github.com/tashfeenahmed/freellmapi/tree/73e3f05843c6d6d7041171225a27defa6a82ecf1). The code at that commit uses [MIT](https://github.com/tashfeenahmed/freellmapi/blob/73e3f05843c6d6d7041171225a27defa6a82ecf1/LICENSE). The code license does not replace provider terms, model licenses, or billing rules.

This article presents an original summary, now in English. It does not reproduce source code, complete articles, or model weights. Source paths and configuration identifiers serve only to locate review subjects.

The material covers selected fixed source paths and the package's official documentation checks for three providers. It does not cover all 34 providers, a full security audit, a full license audit, client execution, actual network and log output, actual model provenance, real bills, or production acceptance.
