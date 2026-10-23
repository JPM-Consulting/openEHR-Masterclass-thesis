# T4 — CLUSTER Pattern: Medical Records First

Status: Completed, with passing results within the documented test scope. EHR: `3c269710-a677-4fe8-9083-1133e8899db9`. Environment: EHRbase 2.30.1, openEHR REST, canonical JSON, AQL/Postman, system `local.ehrbase.org`, RM 1.0.4.

## Repository structure

- [T4-cluster-implementation.md](T4-cluster-implementation.md) — reference direction, modeling, creation sequence, and production governance considerations.
- [T4-cluster-test-identifiers.md](T4-cluster-test-identifiers.md) — versioned COMPOSITION identifiers and relationship inventory.
- [T4-cluster-test-results.md](T4-cluster-test-results.md) — execution record, observed responses, clinical view reconstruction, and evidence boundaries.
- [T4-aql-query-catalog.md](T4-aql-query-catalog.md) — documented AQL queries and expected or observed counts.
- [T4-evidence-manifest.md](T4-evidence-manifest.md) — archived files, SHA-256 checksums, and evidence gaps.
- `json/requests/` — eight archived canonical JSON request payloads, including one unsuccessful EP1 URI-encoding variant.
- `json/persisted/` — 16 archived REST GET COMPOSITION JSON exports, comprising 15 documented final COMPOSITION versions and the historical CE2 version `::1`. See [T4-evidence-manifest.md](T4-evidence-manifest.md).

## Outcome

The documented final state contains 15 COMPOSITIONs: nine Medical Records (MR), two Care Encounters (CE), and four Episodes of Care (EP). The dataset contains 19 clinical MR ENTRYs and six context ENTRYs. The implementation stores 33 relationship references: nine CE-to-MR COMPOSITION references and 24 EP-to-clinical-ENTRY references (19 Primary and five Associated). CE2 was updated from version `::1`, which contained no relationships, to version `::2`, which contained four. The historical version was retrieved.

Documented AQL queries support selective retrieval and application-side assembly of the tested chronological, EP2, SOAP, and diagnosis/problem-list views without duplicating clinical MR content. This does not establish automated end-to-end reconstruction of all clinician views.

## Evidence boundaries

REST and AQL results document persistence and retrieval of URI-valued relationship data. They do not demonstrate automatic URI dereferencing, validation of target existence, server-side enforcement of role cardinality, performance characteristics, or implementation of all eight clinician-centered user stories.

The AQL statements and recorded results are described in [T4-aql-query-catalog.md](T4-aql-query-catalog.md) and [T4-cluster-test-results.md](T4-cluster-test-results.md). Complete AQL response payloads were not archived separately.
