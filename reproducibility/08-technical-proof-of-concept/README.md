# Technical Proof of Concept

This technical proof of concept (PoC) examines three openEHR implementation patterns for representing relationships among Care Encounters, Episodes of Care, and Medical Record Entries:

- **FOLDER-based:** openEHR FOLDER structures.
- **LINK-based:** openEHR Reference Model LINK relationships.
- **CLUSTER-based:** dedicated archetyped relationship CLUSTERs.

Five isolated test scenarios (T1–T5) use the same smaller synthetic clinical case to examine the persistence, maintenance, and retrieval of Care Encounter and Episode of Care relationships. This PoC dataset is distinct from the larger longitudinal dataset used for the design-level functional evaluation. A preliminary FOLDER feasibility experiment (T0) is documented separately. Clinical Section FOLDER organization (R03) was outside the tested scope, and existing clinical `SECTION` structures remained unchanged. The two relationship creation sequences examined for LINK and CLUSTER are test scenarios rather than additional implementation patterns.

## Documentation

- [PoC Scenario](DOC-01-poc-scenario.md): Clinical case, modeling constraints, template inventory, and test dataset.
- [Clinical Relationship Specification](DOC-02-poc-clinical-relationships.md): Clinical relationship matrix, CR-001–CR-027 register, and validation rules.
- [PoC Plan](DOC-03-poc-plan.md): Objectives, technical requirements R01–R15, test scenarios, and evaluation criteria.
- [PoC Results](DOC-04-poc-results.md): Baseline validation (30/30 PASS), execution records, observations, and results for T0–T5, including limitations.
- [Evidence Availability](DOC-05-poc-evidence-availability.md): Cross-scenario inventory of archived requests, persisted exports, execution records, and evidence gaps.

## Technical artifacts

| Directory | Contents |
| --- | --- |
| `01-test-dataset/` | Synthetic clinical test dataset and source spreadsheet |
| `02-templates/opt/` | 16 Operational Templates used for CDR deployment |
| `02-templates/zip/` | 16 template packages containing associated archetypes and CLUSTERs |
| `03-folder-pattern/` | T0 preliminary feasibility, T1 basic FOLDER, and exploratory extended FOLDER artifacts |
| `04-link-pattern/` | T2 and T3 LINK artifacts, relationship tests, and retrieval examples |
| `05-cluster-pattern/` | T4 and T5 CLUSTER artifacts, persisted COMPOSITIONs, AQL queries, and evidence |
| `06-reproduction-guide/` | Instructions for reproducing T0–T5. Independent end-to-end reproduction has not been documented. |
| `07-environment/` | Technical environment, configuration, and reproducibility prerequisites |

The PoC-specific templates in `02-templates/` were remodeled for the technical tests. They are distinct from the earlier modeling artifacts in the repository's [`local/`](../../local/README.md) directory. The `opt/` directory contains the operational templates, while `zip/` provides packages with their associated archetypes and CLUSTERs.

## Execution status and evidence boundaries

The following table summarizes outcomes reported in [DOC-04](DOC-04-poc-results.md). Detailed execution records and available evidence are provided in the pattern-specific directories.

| Test | Pattern or purpose | Recorded outcome | Evidence boundary |
| --- | --- | --- | --- |
| Baseline | Template and COMPOSITION validation | 30/30 PASS | Baseline validation only |
| T0 | Preliminary FOLDER feasibility | PASS | Preliminary feasibility, not an additional comparison pattern |
| T1 | Basic FOLDER | Core relationship operations PASS | Full clinical-view reconstruction only partially verified |
| T2 | LINK, context-to-record direction | PASS within tested scope | Manual and AQL-driven reconstruction. Automatic reference dereferencing was not demonstrated. |
| T3 | LINK, record-to-context direction | PASS within tested scope | Manual and AQL-driven reconstruction. Automatic reference dereferencing was not demonstrated. |
| T4 | CLUSTER, context-to-record direction | PASS within tested scope | Reference persistence and AQL retrieval, not general referential-integrity enforcement |
| T5 | CLUSTER, clinical ENTRY-to-context direction | PASS within tested scope | 15 regular COMPOSITIONs and a separate RI-02 negative-test COMPOSITION |

In T5, the 15 regular COMPOSITIONs contain 19 clinical ENTRYs and 43 persisted `DV_EHR_URI` occurrences representing 33 logical relationships. In the separate RI-02 negative test, the tested EHRbase 2.30.1 configuration accepted and persisted a dangling episode reference. This observation does not establish general behavior across other configurations or implementations. See the T5 results and evidence manifest for details.

The recorded results support conclusions about selected technical properties in the documented EHRbase test environment. They do not demonstrate automatic `DV_EHR_URI` dereferencing, comprehensive clinical-view reconstruction across all scenarios, production readiness, cross-vendor interoperability, or runtime performance. The availability and limitations of supporting evidence are documented in [DOC-05](DOC-05-poc-evidence-availability.md).
