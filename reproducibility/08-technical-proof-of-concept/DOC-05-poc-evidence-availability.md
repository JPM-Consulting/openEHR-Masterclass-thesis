# Technical Proof of Concept — Evidence Availability

## 1. Purpose and scope

This document provides a cross-scenario index of the **archived evidence** supporting the technical proof of concept (PoC). It covers preliminary FOLDER feasibility test T0 and implementation scenarios T1–T5. It complements the [PoC results](DOC-04-poc-results.md), scenario-specific records and evidence manifests. It does not repeat the test results or claim independent re-execution.

The inventory distinguishes archived request payloads, persisted server-state exports, reported execution observations, and subsequently reconstructed query artifacts. File availability alone does not establish successful execution or the correctness of a clinical interpretation.

## 2. Evidence categories

| Category | Meaning | Interpretation |
| --- | --- | --- |
| **Request payload** | Archived JSON intended for a REST operation. | May include unsuccessful or alternative variants. Does not prove a successful HTTP response. |
| **Persisted export** | Archived JSON representing a retrieved DIRECTORY or COMPOSITION. | Inspectable evidence of stored structure. Original HTTP status and headers are not necessarily archived. |
| **Execution record** | README, implementation notes or results describing observed requests, statuses, counts or AQL outcomes. | Reported historical observation, not equivalent to an archived raw response. |
| **Reconstructed AQL** | Query text prepared after execution from recorded queries or session information. | Useful for inspection and future reproduction, but not an original execution capture. |
| **Evidence manifest** | Scenario inventory, often with file-level SHA-256 checksums. | Supports archive integrity and provenance checks, not independent runtime validation. |

## 3. Evidence availability by scenario

| Scenario | Archived request evidence | Archived persisted evidence | AQL and execution evidence | Primary references |
| --- | --- | --- | --- | --- |
| **T0 — preliminary FOLDER** | Four DIRECTORY JSON variants in `tests/`, including the failed URI-encoding attempt and corrected payload. | Final DIRECTORY retrieval and version sequence described in the test record. No complete raw HTTP exchange archive established. | REST outcomes and URI-encoding observations documented. No comprehensive AQL-response archive established. | [T0 README](03-folder-pattern/T0/README.md) |
| **T1 — basic FOLDER** | Four DIRECTORY request JSON files. Alternative PUT variants must not be treated as a single successful sequence. | 16 JSON exports: 15 COMPOSITIONs and the final DIRECTORY. | DIRECTORY version and relationship checks recorded. Full clinical-view reconstruction only partially verified. | [T1 README](03-folder-pattern/T1/README.md) · [manifest](03-folder-pattern/T1/T1-evidence-manifest.md) |
| **T2 — LINK, context → clinical** | 10 archived request JSON files, including exploratory and unsuccessful variants. | 15 final COMPOSITION JSON exports. | Executed AQL queries and reported EP2 reconstruction documented. Full raw AQL response payloads not separately archived. | [T2 README](04-link-pattern/T2/README.md) · [manifest](04-link-pattern/T2/T2-evidence-manifest.md) |
| **T3 — LINK, clinical → context** | **9** clinical MR request JSON files. | 15 final COMPOSITION JSON exports. | AQL query catalog and test results available. Original AQL response files and Postman collection export absent. | [T3 README](04-link-pattern/T3/README.md) · [manifest](04-link-pattern/T3/T3-evidence-manifest.md) |
| **T4 — CLUSTER, context → clinical** | 8 context-side request JSON files, including one unsuccessful URI-encoding variant. Original T4-specific MR1–MR9 POST payloads are not archived in that request set. | 16 COMPOSITION JSON exports: 15 current and historical CE2 `::1`. | AQL results reported in test records. Original Postman AQL response exports and complete HTTP header and status logs absent. | [T4 README](05-cluster-pattern/T4/README.md) · [manifest](05-cluster-pattern/T4/T4-evidence-manifest.md) |
| **T5 — CLUSTER, clinical → context** | 9 clinical MR POST JSON files and 1 RI-02 negative-test request. | 16 COMPOSITION JSON exports: 15 regular and 1 RI-02. | Reconstructed AQL request bodies available. Original AQL and POST response payloads not separately archived. | [T5 README](05-cluster-pattern/T5/README.md) · [manifest](05-cluster-pattern/T5/T5-evidence-manifest.md) |

**Separate baseline validation:** The 30/30 COMPOSITION validation results (15 clinical COMPOSITIONs in two template variants) are documented in [DOC-04](DOC-04-poc-results.md). They are not additional T1–T5 scenario runs and should not be counted as such.

## 4. Evidence gaps and interpretation limits

- **HTTP provenance:** The archive generally preserves submitted JSON and retrieved final-state JSON more completely than raw HTTP request/response pairs, response headers, timestamps, and Postman collection exports. The scenario-specific manifests describe the actual coverage.
- **AQL provenance:** Documented historical AQL execution and later reconstructed executable AQL request bodies are distinct. Complete original AQL response files are not available for all scenarios.
- **Scenario-specific coverage:** T1's full clinician-view reconstruction was only partially verified. T4's historical CE2 version is a version-history artifact, not an additional current COMPOSITION. T5's RI-02 record is a separate negative-test artifact, not part of the 15-COMPOSITION reference dataset.
- **Referential integrity:** The recorded T5 RI-02 acceptance of a dangling reference (HTTP 201) is evidence for the tested configuration, not proof of general CDR behavior. Stored references alone do not demonstrate automatic dereferencing or validation of all target paths.
- **Re-execution:** The archive has not been independently replayed as an end-to-end test suite. Follow the [Reproduction Guide](06-reproduction-guide/README.md) for a new execution and keep any newly collected evidence separate from the historical record.

## 5. Evidence interpretation

The available artifacts support retrospective inspection of the persisted relationship structures and comparison with the documented test observations. Evidence strength varies by scenario and claim. Inspectable persisted JSON, archived request payloads, and reported query outcomes are not interchangeable forms of proof. The scenario-specific manifests, such as the [T1 evidence manifest](03-folder-pattern/T1/T1-evidence-manifest.md), provide detailed file inventories and checksums where available. [DOC-04](DOC-04-poc-results.md) remains the authoritative consolidated account of reported technical outcomes.
