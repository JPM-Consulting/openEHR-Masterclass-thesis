# Manuscript–Artifact Mapping

## Purpose

This document links the manuscript’s principal claims, methods, results, tables, and figures

**Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns**

to the reproducibility artifacts supplied in this repository.

The mapping supports traceability and helps readers and reviewers distinguish between:

-   source model and dataset artifacts
-   functional design evaluation
-   technical proof-of-concept observations
-   comparative architectural inference
-   design synthesis
-   claims that remain outside the empirical scope of the study

A reference in this mapping does not change an artifact’s evidentiary status. In particular, a design artifact is not treated as runtime validation merely because it is referenced by the manuscript.

## Evidence categories

| Evidence category | Meaning in this repository |
| --- | --- |
| **Source / design artifact** | Conceptual model, archetype, template, synthetic dataset, or representative serialization used to make the design inspectable |
| **Functional design evaluation** | Assessment of the three patterns against the eight clinician-centered requirements using the common conceptual model and synthetic longitudinal record |
| **Technical PoC observation** | Results recorded for explicitly executed scenarios in the EHRbase test environment, limited to the documented test data and operations |
| **Comparative architectural inference** | Qualitative comparison derived from the structural characteristics of the three designs |
| **Archetype-derived retrieval example** | Retrieval structure derived from modeled paths without claiming execution against a deployed CDR |
| **Design synthesis** | Architectural recommendation derived from the comparative findings rather than evaluated as a fourth implementation pattern |
| **Not evaluated** | Runtime performance, production behavior, usability, clinical outcomes, and empirical multi-vendor interoperability |

## 1. Conceptual model and openEHR mapping

### Manuscript scope

The conceptual model distinguishes:

-   Administrative Encounter
-   Care Encounter (Contact)
-   Episode of Care / Health Problem
-   Medical Record Entry
-   Partial Contact
-   Clinical Section
-   Diagnosis and Problem List

Care Encounters provide the chronological care-event dimension. Episodes of Care provide the longitudinal Health Problem dimension. Administrative Encounters provide the organizational care-period dimension.

### Repository artifacts

-   `../01-conceptual-model/figure-1-conceptual-model.pdf`
-   `../01-conceptual-model/figure-2-openehr-mapping.pdf`
-   `../../local/JPM - Admin Encounter.t.json`
-   `../../local/JPM - Contact - Care Encounter.t.json`
-   `../../local/JPM - Episode of care.t.json`
-   `../../local/openEHR-EHR-ADMIN_ENTRY.admin_encounter.v1.adl`
-   `../../local/openEHR-EHR-COMPOSITION.encounter.v1.adl`
-   `../../local/openEHR-EHR-COMPOSITION.problem_list.v2.adl`
-   `../../local/openEHR-EHR-EVALUATION.problem_diagnosis.v1.adl`

### Evidence classification

**Source / design artifact**

These artifacts document the conceptual separation and its openEHR-oriented representation. They do not by themselves establish production implementation or clinical effectiveness.

## 2. Synthetic longitudinal patient record

### Manuscript scope

The comparative evaluation uses the same synthetic longitudinal patient history for all three implementation patterns. The record contains 121 Medical Record Entries and provides a common information basis for the clinician-centered requirements.

### Repository artifacts

-   `../03-synthetic-dataset/synthetic-patient-medical-record.xlsx`
-   `../03-synthetic-dataset/README.md`

### Evidence classification

**Source / design artifact**

The workbook contains synthetic evaluation data. It is not patient-derived clinical data and is not evidence of production-scale behavior.

## 3. Eight clinician-centered functional requirements

### Manuscript scope

The study evaluates whether each pattern can support eight requirements:

1.  chronological retrieval by Care Encounter
2.  Episode-oriented retrieval for a selected Health Problem
3.  organization by Clinical Section
4.  combined Clinical Section × Care Encounter/Episode views
5.  linear Diagnosis and Problem Lists: two derived views of
    Episode-of-Care COMPOSITIONs, selected by `Classification = Diagnosis`
    or `Classification = Problem`
6.  hierarchical Diagnosis and Problem List: a separate, clinically
    curated COMPOSITION containing hierarchy and references to existing
    Episode-of-Care COMPOSITIONs
7.  problem-oriented SOAP documentation
8.  section-oriented dashboard views

### Repository artifacts

-   `../04-functional-evaluation/functional-requirements.md`
-   `../04-functional-evaluation/functional-traceability.csv`
-   `../03-synthetic-dataset/synthetic-patient-medical-record.xlsx`

### Manuscript mapping

-   **Methods:** definition of the clinician-centered evaluation
    requirements
-   **Results 3.4:** functional evaluation
-   **Table 1:** comparison against the eight functional requirements

### Evidence classification

**Functional design evaluation**

"Supported" denotes **support at the design level**. It does not mean that every user story was executed as an end-to-end application workflow in a deployed production system. In particular, the persisted hierarchical Diagnosis and Problem List is distinct from FOLDER-based patient navigation.

### User-story evidence coverage

The following matrix qualifies the positive design-level support assessments for US1–US8. It maps each requirement to its principal evidence tier and an explicit validation boundary. The technical PoC observations are selective and do not constitute eight independently validated clinical workflows.

| User story | Design-level capability | Available evidence tier | Boundary of the claim |
| --- | --- | --- | --- |
| US1 | Chronological retrieval by Care Encounter | Functional design evaluation, with selected PoC relationship and retrieval observations | No complete clinician-facing chronological workflow was validated. |
| US2 | Episode-oriented retrieval for a selected Health Problem | Functional design evaluation, with selected LINK and CLUSTER PoC relationship and retrieval observations | FOLDER membership in T1 does not encode Primary/Associated Episode roles. Complete end-to-end Episode view generation was not demonstrated. |
| US3 | Organization by Clinical Section | Functional design evaluation, with illustrative retrieval structures | No complete section-oriented clinical application workflow was validated. |
| US4 | Combined Clinical Section × Care Encounter/Episode views | Functional design evaluation, with illustrative retrieval structures | Combined views are conceptually derivable. They were not validated as complete end-to-end workflows. |
| US5 | Separate linear Diagnosis and Problem Lists | Functional design evaluation using Episode-of-Care `Classification` | Complete classification-filtered lists were not independently validated as application workflows. |
| US6 | Clinician-curated hierarchical Diagnosis and Problem List | Functional design evaluation of a separate hierarchical-list COMPOSITION | The curated hierarchy is a shared modeled dependency, not an inherent feature of any one relationship pattern. Complete hierarchy management was not implemented and tested across all three patterns. |
| US7 | Problem-oriented SOAP documentation | Functional design evaluation, with selected SOAP-related PoC reconstruction observations | One clinical SOAP note may contain four technical ENTRYs. Consistent Episode assignment across those ENTRYs was observed in the test data, not demonstrated as a server-enforced invariant. No complete documentation workflow was validated. |
| US8 | Section-oriented dashboard views | Functional design evaluation and modeled information availability | No clinician-facing dashboard or its usability was implemented and evaluated. |

The matrix describes the documented scope of evidence, not a new test execution. In particular, an illustrative retrieval query is not an executed PoC result. A successful relationship-metadata query does not by itself demonstrate reference dereferencing, clinical-view assembly, or user-interface behavior. The PoC evidence and its limits are detailed in [DOC-04](../08-technical-proof-of-concept/DOC-04-poc-results.md) and [DOC-05](../08-technical-proof-of-concept/DOC-05-poc-evidence-availability.md).

## 4. FOLDER-based implementation pattern

### Manuscript scope

The FOLDER pattern represents patient-level organization through the EHR Directory. Care Encounter-, Episode-, and Clinical Section-oriented structures can index existing clinical content without duplicating the source clinical statements.

Each FOLDER hierarchy is managed as a `VERSIONED_FOLDER`. The complete hierarchy, rather than an individual FOLDER subtree, constitutes the versioned unit.

### Repository artifacts

-   `../02-implementation-patterns/folder/README.md`
-   `../02-implementation-patterns/folder/folder-example.json`
-   `../06-retrieval-examples/folder/README.md`
-   `../08-technical-proof-of-concept/DOC-03-poc-plan.md` (T0–T1)
-   `../08-technical-proof-of-concept/DOC-04-poc-results.md` (T0–T1)

### Manuscript mapping

-   **Methods:** FOLDER-based referencing
-   **Results 3.3:** representation of the FOLDER pattern
-   **Results 3.5:** architectural comparison
-   **Results 3.5.2:** query and retrieval workflow
-   **Results 3.5.4:** versioning and provenance
-   **Results 3.5.6:** cross-system dependencies
-   **Table 2:** FOLDER architectural characteristics
-   **Figure 3:** FOLDER-based implementation pattern

### Evidence classification

The JSON and documentation are **source / design artifacts**.

The conclusions concerning navigation, governance location, lifecycle responsibility, and retrieval structure are **comparative architectural inference**.

The retrieval workflow is represented as:

`Directory → FOLDER → reference → referenced EHR object`

No runtime performance or portable single-statement AQL claim is made.

## 5. LINK-based implementation pattern

### Manuscript scope

The LINK pattern uses the openEHR Reference Model `LINK` mechanism for explicit relationships between LOCATABLE objects.

The evaluated design considers:

-   Care Encounter ↔ clinical COMPOSITION relationships
-   clinical ENTRY ↔ Episode-of-Care relationships
-   one primary Episode and optional associated Episodes
-   alternative relationship directions
-   target representation through `DV_EHR_URI`

### Repository artifacts

-   `../02-implementation-patterns/link/README.md`
-   `../02-implementation-patterns/link/care-encounter-links.json`
-   `../02-implementation-patterns/link/episode-of-care-links.json`
-   `../06-retrieval-examples/link/README.md`
-   `../08-technical-proof-of-concept/DOC-03-poc-plan.md` (T2–T3)
-   `../08-technical-proof-of-concept/DOC-04-poc-results.md` (T2–T3)

### Manuscript mapping

-   **Methods:** Reference Model LINK-based referencing
-   **Results 3.3:** representation of the LINK pattern
-   **Results 3.5:** architectural comparison
-   **Results 3.5.2:** query and retrieval workflow
-   **Results 3.5.4:** versioning and provenance
-   **Results 3.5.6:** cross-system dependencies
-   **Table 2:** LINK architectural characteristics
-   **Figures 4 and 5:** Care Encounter and Episode LINK configurations

### Evidence classification

The representative JSON relationships are **source / design artifacts**.

The conclusions concerning application responsibility, relationship conventions, target resolution, and retrieval workflow are **comparative architectural inference**.

The representative retrieval workflow is:

`source LOCATABLE → LINK → DV_EHR_URI → target resolution where required`

The repository does not claim universal AQL dereferencing, automatic target resolution, or empirical multi-vendor LINK interoperability.

## 6. CLUSTER-based implementation pattern

### Manuscript scope

The CLUSTER pattern represents relationship metadata through explicit archetyped structures. The evaluated design defines relationship contexts for:

-   clinical ENTRYs
-   Care Encounter COMPOSITIONs
-   Episode-of-Care COMPOSITIONs

The ENTRY relationship structure includes Care Encounter reference, repeating Episode associations, Episode role, Clinical Section, and SOAP classification.

### Repository artifacts

Primary relationship models:

-   `../../local/openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl`
-   `../../local/openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl`
-   `../../local/openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl`

Supporting models and templates:

-   `../../local/openEHR-EHR-CLUSTER.episode_of_care_header.v0.adl`
-   `../../local/JPM - Contact - Care Encounter.t.json`
-   `../../local/JPM - Episode of care.t.json`
-   `../../local/JPM - SOAP initial encounter .t.json`
-   `../../local/JPM - SOAP progress note.t.json`
-   `../02-implementation-patterns/cluster/README.md`

Retrieval documentation:

-   `../06-retrieval-examples/cluster/README.md`
-   `../06-retrieval-examples/cluster/representative-queries.aql`
-   `../08-technical-proof-of-concept/DOC-03-poc-plan.md` (T4–T5)
-   `../08-technical-proof-of-concept/DOC-04-poc-results.md` (T4–T5)

### Manuscript mapping

-   **Methods:** archetyped CLUSTER-based relationship representation
-   **Results 3.3:** representation of the CLUSTER pattern
-   **Results 3.5:** architectural comparison
-   **Results 3.5.2:** query and retrieval workflow
-   **Results 3.5.4:** versioning and provenance
-   **Results 3.5.6:** cross-system dependencies
-   **Table 2:** CLUSTER architectural characteristics
-   **Figure 6:** CLUSTER-based relationship representation

### Evidence classification

The ADL relationship models are **source / design artifacts**.

The AQL examples are **archetype-derived retrieval examples**.

The conclusions concerning in-template semantic governance, stable modeled paths, and implementation responsibility are **comparative architectural inference**.

### Important template-integration boundary

The original design artifact set contains the three `eoc_relationships_*` archetypes. Inspection of the original `local/` `.t.json` templates did not identify references integrating these three relationship archetypes into those particular template exports.

Accordingly, the repository supports the claim that the relationship CLUSTERs were **developed as part of the design**, but it does not use those original template exports as evidence that these relationship CLUSTERs were integrated and executed end to end.

Separately, the subsequent T4 and T5 technical PoC scenarios document implementation templates, persisted COMPOSITIONs, and executed AQL queries for selected CLUSTER relationship structures in EHRbase. This later evidence demonstrates feasibility only within the tested scenarios; it does not retroactively establish integration in the original `local/` template exports.

The representative AQL examples in `06-retrieval-examples/` remain illustrative and must not be cited as executed queries. The distinct queries actually executed in T4–T5 are documented under
`08-technical-proof-of-concept/`.

## 7. Functional equivalence and architectural non-equivalence

### Manuscript scope

All three implementation patterns support the eight clinician-centered requirements at design level, while differing in where relationship information is represented, governed, maintained, versioned, and retrieved.

### Repository artifacts

-   `../04-functional-evaluation/functional-traceability.csv`
-   `../05-architectural-evaluation/architectural-evidence-matrix.csv`
-   `../06-retrieval-examples/README.md`

### Manuscript mapping

-   **Results 3.4:** functional evaluation
-   **Results 3.5:** architectural comparison
-   **Results 3.5.2:** query and retrieval workflow
-   **Table 1:** functional evaluation
-   **Table 2:** architectural comparison

### Evidence classification

The statement that all three patterns support the eight requirements is
**functional design evaluation**, subject to the requirement-specific evidence boundaries in the user-story matrix above. It establishes representability against the defined criteria, not functional equivalence in implemented workflows.

The statement that they are architecturally non-equivalent is
**comparative architectural inference**.

Neither statement constitutes evidence of equivalent or different runtime performance.

## 8. Query and retrieval implications

### Manuscript scope

The three patterns result in different logical retrieval strategies:

-   **FOLDER:** directory traversal and reference resolution
-   **LINK:** relationship traversal and target resolution
-   **CLUSTER:** archetype-path-based filtering of governed relationship
    metadata, with reference resolution where required

### Repository artifacts

-   `../06-retrieval-examples/README.md`
-   `../06-retrieval-examples/folder/README.md`
-   `../06-retrieval-examples/link/README.md`
-   `../06-retrieval-examples/cluster/README.md`
-   `../06-retrieval-examples/cluster/representative-queries.aql`

### Evidence classification

The distinction between the retrieval structures is **comparative architectural inference** supported by the corresponding design artifacts.

The CLUSTER queries in `06-retrieval-examples/` are **archetype-derived retrieval examples**, not executed test evidence. Selected executed AQL queries and their reported results are documented separately in
`../08-technical-proof-of-concept/DOC-04-poc-results.md` and are classified as **Technical PoC observation**. Their execution does not establish complete automated target dereferencing or end-to-end clinical view generation.

No comparative benchmark of latency, throughput, execution plans, or production-scale workloads is part of the study.

## 9. Technical proof-of-concept evidence

### Manuscript scope

The supplementary technical proof of concept tests selected mechanisms for each pattern in an EHRbase test environment. Its small synthetic test dataset is distinct from the 121-entry longitudinal dataset used for functional design evaluation. Technical observations supplement, but do not replace, design-level architectural comparison.

| Pattern | Scenarios | Documented observation and boundary |
| --- | --- | --- |
| FOLDER | T0 exploratory; T1 | Selected Directory operations, versioning, and references were exercised. Clinical Section FOLDER → ENTRY retrieval (R03) was out of scope. No complete clinical-view assembly was demonstrated. |
| LINK | T2 context-to-clinical; T3 clinical-to-context | LINK-bearing structures were persisted and selected retrieval operations exercised in both directions. Automatic target resolution and full application views were not demonstrated. |
| CLUSTER | T4 context-to-clinical; T5 clinical-to-context | Relationship CLUSTERs were persisted and selected AQL retrieval of relationship metadata executed. In T5, negative test RI-02 showed that a dangling reference was accepted on persistence. Referential integrity was not automatically enforced in that test. |

### Repository artifacts

-   `../08-technical-proof-of-concept/DOC-03-poc-plan.md`
-   `../08-technical-proof-of-concept/DOC-04-poc-results.md`
-   supporting scenario-specific requests, templates, and results under
    `../08-technical-proof-of-concept/`

### Evidence classification

**Technical PoC observation**, strictly limited to operations and results recorded in DOC-04. Persistence, retrieval of relationship metadata, resolution of referenced objects, and construction of a clinically meaningful view are separate evidence claims. The PoC does not establish complete functional coverage, performance superiority, production readiness, or cross-vendor interoperability.

The historical execution environment and evidence provenance remain subject to documented limitations. The queried EHRbase service reported version 2.30.1, while the available Docker Compose configuration specifies image tag 2.11.0. Their historical equivalence has not been established. Archived requests and persisted exports do not constitute complete original HTTP/AQL response records, and matching archive checksums do not establish byte-for-byte identity with the original execution artifacts. No independent end-to-end reproduction has been performed. See the [environment record](../08-technical-proof-of-concept/07-environment/README.md) and [evidence availability inventory](../08-technical-proof-of-concept/DOC-05-poc-evidence-availability.md).

## 10. Architectural comparison

### Manuscript scope

The manuscript compares the three patterns across architectural concerns including:

-   location of relationship representation
-   semantic governance
-   relationship granularity
-   multiple Episode associations
-   patient-wide navigation
-   query and retrieval workflow
-   versioning and provenance
-   implementation responsibility
-   cross-system dependencies
-   principal strengths
-   principal trade-offs

### Repository artifact

-   `../05-architectural-evaluation/architectural-evidence-matrix.csv`

### Manuscript mapping

-   **Results 3.5**
-   **Results 3.5.2:** query and retrieval workflow
-   **Results 3.5.4:** versioning and provenance
-   **Results 3.5.6:** cross-system dependencies
-   **Table 2**

### Evidence classification

**Comparative architectural inference**

The matrix documents the reasoning underlying the manuscript comparison. It is not a quantitative scoring model and does not establish universal superiority of one pattern.

## 11. Hybrid architecture

### Manuscript scope

The manuscript proposes a hybrid architecture that allocates different responsibilities to the mechanisms best suited to them in the evaluated design:

| Concern | Proposed mechanism |
| --- | --- |
| Longitudinal Health Problem representation | Episode-of-Care COMPOSITION |
| Governed Episode/Care Encounter relationship metadata | Relationship CLUSTERs |
| Patient-level navigation/index | FOLDER |
| Selective explicit object-to-object relationship | LINK |
| Clinical statements | Archetyped ENTRYs within clinical COMPOSITIONs |
| Linear Diagnosis List | Derived view of Episode-of-Care COMPOSITIONs with `Classification = Diagnosis` |
| Linear Problem List | Derived view of Episode-of-Care COMPOSITIONs with `Classification = Problem` |
| Hierarchical Diagnosis and Problem List | Separate, clinically curated COMPOSITION holding a hierarchy and references to existing Episode-of-Care COMPOSITIONs; distinct from FOLDER navigation |
| SOAP progress note | One clinical documentation unit, even where represented by four technical `OBSERVATION.progress_note.v1` ENTRYs under `SECTION.soap.v0`; consistent Episode-of-Care assignment |
| Other derived views | Query/application layer, without duplicating authoritative clinical statements |

### Repository artifact

-   `../05-architectural-evaluation/hybrid-design-rationale.md`

### Manuscript mapping

-   **Results:** hybrid architecture / architectural synthesis
-   **Table 3:** proposed allocation of responsibilities
-   **Discussion:** interpretation and implications
-   **Conclusion:** proposed architecture as a testable design
    hypothesis

### Evidence classification

**Design synthesis**

The hybrid architecture was not evaluated as a fourth implementation pattern.

It should be described as a **testable design hypothesis**, not as a validated final architecture.

## 12. Figures

| Figure | Manuscript role | Repository evidence | Evidence category |
| --- | --- | --- | --- |
| Figure 1 | Conceptual episode-oriented information model | `../01-conceptual-model/figure-1-conceptual-model.pdf` | Source / design artifact |
| Figure 2 | Mapping of conceptual dimensions to openEHR | `../01-conceptual-model/figure-2-openehr-mapping.pdf`, relevant `local/` models | Source / design artifact |
| Figure 3 | FOLDER pattern | `../02-implementation-patterns/folder/folder-example.json` | Source / design artifact |
| Figure 4 | LINK pattern for Care Encounter | `../02-implementation-patterns/link/care-encounter-links.json` | Source / design artifact |
| Figure 5 | LINK pattern for Episode association | `../02-implementation-patterns/link/episode-of-care-links.json` | Source / design artifact |
| Figure 6 | CLUSTER relationship pattern | `local/eoc_relationships_*` ADL artifacts and `../02-implementation-patterns/cluster/README.md` | Source / design artifact |

The figures illustrate the evaluated designs. They should not be interpreted as screenshots of a production implementation.

## 13. Tables

| Table | Manuscript role | Repository evidence | Evidence category |
| --- | --- | --- | --- |
| Table 1 | Functional evaluation against US1–US8 | `../04-functional-evaluation/functional-traceability.csv` | Functional design evaluation |
| Table 2 | Architectural comparison of FOLDER, LINK, and CLUSTER | `../05-architectural-evaluation/architectural-evidence-matrix.csv` | Comparative architectural inference |
| Table 3 | Proposed hybrid allocation of responsibilities | `../05-architectural-evaluation/hybrid-design-rationale.md` | Design synthesis |

## 14. Claims deliberately outside the evidence boundary

The repository should not be interpreted as providing empirical evidence for:

-   runtime superiority of one implementation pattern
-   latency, throughput, or query optimizer performance
-   production-scale scalability
-   production concurrency behavior
-   clinical usability
-   clinician efficiency
-   patient or clinical outcomes
-   deployment security
-   operational cost
-   cross-CDR reference resolution
-   empirical multi-vendor interoperability
-   universal portability of the representative AQL examples
-   validation of the hybrid architecture as a final solution

Addressing these questions requires further implementation and empirical evaluation.

## 15. Traceability summary

The evidence chain can be summarized as:

``` text
Conceptual model
        ↓
openEHR design artifacts
        ↓
common synthetic longitudinal record
        ↓
eight clinician-centered requirements
        ↓
three implementation patterns
        ↓
functional design evaluation
        ↓
comparative architectural analysis
        ↘
         selected technical PoC observations (T0–T5)
        ↓
representative retrieval workflows
        ↓
hybrid design synthesis
```

This structure preserves the distinction between what was modeled, what was evaluated at design level, what was observed in selected technical tests, what was inferred architecturally, and what is proposed for subsequent empirical validation.
