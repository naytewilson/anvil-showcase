# ANVIL · Evidence and verification model

> **Purpose:** define how a claim about an autonomous system should be supported. This is a public methodological description, not a certification report for the private ANVIL deployment.

[← Project overview](../README.md) · [Architecture](ARCHITECTURE.md) · [Evidence pipeline](EVIDENCE_PIPELINE.md)

## Verification is a chain, not a status badge

There are materially different meanings of “working.” A mature agent operating system must keep them distinct.

| Level | What may be claimed | Minimum relevant evidence | What is **not** implied |
| :-- | :-- | :-- | :-- |
| **Design** | A contract or approach has been specified. | Versioned specification or decision record. | Implementation. |
| **Source** | A change exists at a particular revision. | Exact commit/diff and provenance. | A successful build. |
| **Build** | Software can be built in a specified environment. | Reproducible build result and toolchain context. | Correct behavior. |
| **Test** | Specific cases passed on specific inputs. | Test command, fixture, expected/actual outputs, exit status. | Exhaustive coverage or deployment. |
| **Integration** | The relevant components exchanged data as intended. | End-to-end test and component revision linkage. | Installation on the target hosts. |
| **Deployment** | A specified artifact is installed/activated on a target. | Host-observed version and service state. | Operator-visible usability. |
| **Operational acceptance** | The actual workflow works under the accepted constraints. | Direct execution, observed result, recovery/failure checks, independent readback where appropriate. | A guarantee of all future outcomes. |

**A successful earlier level is not a substitute for proof at a later level.**

## Evidence object: conceptual fields

A defensible engineering assertion should normally identify:

```text
claim        — narrow, falsifiable statement
scope        — component, host/environment, revision, configuration
inputs       — exact workload, fixture or requested action
method       — command/protocol, instrumentation and acceptance rule
observation  — captured output, measurement, or runtime state
provenance   — origin, timestamp, artifact/reference identity
limitations  — unmeasured dimensions, conflicts, uncertainty
decision     — accepted, rejected, pending, or blocked
```

This is an **illustrative checklist**, not an excerpt from ANVIL's internal database schema, API, or receipt format.

## Epistemic states

A measurement or observation needs more than a nullable field.

- **Verified:** directly supported by evidence matching the claim's scope.
- **Unknown:** evidence is unavailable; no favorable value may be inferred.
- **Stale:** once valid but not current enough for the decision.
- **Conflicted:** credible observations disagree; the discrepancy remains visible.
- **Zero:** a measured numerical value, distinct from absent data.
- **Inferred:** a conclusion derived from evidence, labeled as such.

For example, an unreachable host does not prove that no agents are running on it. Similarly, a model compiler's preferred-device assignment is not itself a direct measurement of exclusive physical accelerator execution.

## Tests and benchmarks

Benchmarks should disclose workload, shape, machine class, toolchain, measurement boundary, sample count, repeatability criteria, and error/variance where relevant. Results from different implementations or revisions should not be silently pooled.

For numerical systems research, useful checks include absolute error, relative error, numerical stability, output parity, and runtime placement. Which metric matters depends on the actual claim. ANVIL's public showcase does not imply that independent ANE research measurements are agent-orchestration benchmarks.

Related published examples and methodology are maintained separately by [MacBrains Labs](https://macbrainslabs.org/research/) and its [methods documentation](https://macbrainslabs.org/methods/).

## Scientific qualification and publishing authority

ANVIL's research evidence pipeline adds two independent conditions beyond ordinary software verification:

1. **Claim qualification:** the underlying sources, methods, measurements, exact artifacts, review record, and uncertainty must justify the scientific statement being made.
2. **Release qualification:** a distinct, current authorization must permit the specific publication effect; producing or approving a finding does not implicitly grant that authority.

The observed research surface can retain **explicit eligibility blockers** for findings that are not qualified for release. Native agent sandbox controls already exist in ANVIL source, but the **dedicated prepublication test sandbox** is still being qualified. Separately, source-level cryptographic signing and transaction-fenced publication authority are under review rather than production-accepted.

A deterministic test, signature, or model-review receipt can be necessary evidence without constituting scientific validation. Conversely, scientifically credible research does not justify publishing without explicit release authority and independent external readback. See [the full evidence pipeline](EVIDENCE_PIPELINE.md).

## Evidence precedence and conflict resolution

The strongest source is the one that **owns the asserted fact**:

- A Git object proves source contents at that object, not the active state of a server.
- A service manager proves process/service state, not application correctness.
- A runtime probe proves the property it observed, not untested side effects.
- A dashboard can represent an observation but must not silently invent it.
- A worker's self-report is useful evidence, not automatically independent acceptance.

Where evidence conflicts, preserve the disagreement and acquire a fresh, higher-authority observation. Do not average incompatible claims into an artificial answer.

## Completion boundary

The project is successful when it turns agent work into **inspectable, recoverable, accountable outcomes**, rather than merely producing convincing status reports. That standard deliberately distinguishes an engineering aspiration from a demonstrated production outcome.

This document describes how ANVIL approaches evidence. It does **not** publish private test runs, current fleet health, security posture, or production acceptance.
