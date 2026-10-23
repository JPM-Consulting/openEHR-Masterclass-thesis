# Reproducibility Package

## Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns

This directory contains the manuscript-specific artifacts that support the comparative design evaluation presented in:

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.***

The study examines how an episode-oriented medical record can be represented using the existing openEHR architecture. It compares three implementation patterns for expressing relationships among Care Encounters, Episodes of Care, and clinical information:

1.  **FOLDER-based organization**
2.  **LINK-based relationships**
3.  **CLUSTER-based relationship structures**

The package establishes traceability among the conceptual model, implementation patterns, synthetic evaluation dataset, functional requirements, and architectural findings reported in the manuscript. A complementary technical proof of concept (PoC) documents selected implementation and retrieval experiments conducted with EHRbase.

## Scope of the package

The package supports a **design-level comparative evaluation** and a **complementary technical proof of concept** conducted with EHRbase.

The design-level evaluation examines how a shared episode-oriented information model can be expressed through FOLDER-, LINK-, and CLUSTER-based mechanisms. It draws on a synthetic longitudinal patient history, eight clinician-centered functional requirements, and a qualitative architectural comparison.

The technical PoC examines selected implementation characteristics through openEHR REST API operations, persistence and retrieval of openEHR objects, AQL queries, and relationship-reference tests. The design-level evaluation and technical PoC use distinct datasets and support different types of claims.

The package provides:

-   the conceptual information model and its mapping to openEHR
-   the openEHR archetypes and templates used in the modeling work
-   representative examples of the FOLDER-, LINK-, and CLUSTER-based implementation patterns
-   the synthetic longitudinal patient history used for the functional evaluation
-   the eight clinician-centered functional requirements
-   traceability between requirements, implementation patterns, artifacts, and evaluation results
-   the evidence basis for the comparative architectural evaluation
-   representative design-level retrieval examples
-   the technical PoC scenario definitions, implementation artifacts, persisted objects, AQL queries, and recorded test results for T0–T5
-   a mapping between manuscript sections and reproducibility artifacts

The package does **not** contain three complete production implementations of the evaluated patterns. It provides no evidence of comparative runtime performance, clinical usability, deployment scalability, or empirically validated multi-vendor or cross-repository interoperability.

In the functional comparison, a finding that an implementation pattern supports a requirement means **support at design level** within the evaluated information model and synthetic dataset. The technical PoC provides additional execution evidence for specific scenarios. Its results do not establish runtime validation of the complete longitudinal evaluation dataset.

## Common information model

The three implementation patterns do not represent three different clinical information models.

Instead, they provide alternative mechanisms for representing relationships within a shared episode-oriented information model.

The model distinguishes three principal dimensions:

-   **Care Encounter (Contact)**: the chronological care-event dimension
-   **Episode of Care**: the longitudinal representation of a distinct Health Problem
-   **Administrative Encounter**: the organizational care-period dimension

Clinical statements remain represented as archetyped ENTRYs within clinical COMPOSITIONs. Clinical Section provides an additional classification dimension.

The evaluated patterns differ primarily in the location of relationship information, the governance of its semantics, and the mechanisms used to retrieve and navigate the resulting structures.

## Repository organization

``` text
reproducibility/
├── README.md
├── 01-conceptual-model/
│   ├── README.md
│   ├── figure-1-conceptual-model.pdf
│   └── figure-2-openehr-mapping.pdf
├── 02-implementation-patterns/
│   ├── folder/
│   │   ├── README.md
│   │   ├── figure-3-folder-pattern.pdf
│   │   └── folder-example.json
│   ├── link/
│   │   ├── README.md
│   │   ├── figure-4-5-link-patterns.pdf
│   │   ├── care-encounter-links.json
│   │   └── episode-of-care-links.json
│   └── cluster/
│       ├── README.md
│       └── figure-6-cluster-pattern.pdf
├── 03-synthetic-dataset/
│   ├── README.md
│   ├── synthetic-patient-medical-record.xlsx
│   └── synthetic-patient-medical-record.csv
├── 04-functional-evaluation/
│   ├── functional-requirements.md
│   ├── functional-traceability.csv
│   └── functional-traceability.xlsx
├── 05-architectural-evaluation/
│   ├── architectural-evidence-matrix.csv
│   └── hybrid-design-rationale.md
├── 06-retrieval-examples/
│   ├── README.md
│   ├── folder/
│   │   └── README.md
│   ├── link/
│   │   └── README.md
│   └── cluster/
│       ├── README.md
│       └── representative-queries.aql
├── 07-manuscript-mapping/
│   └── manuscript-artifact-mapping.md
├── 08-technical-proof-of-concept/
│   ├── README.md
│   ├── 01-test-dataset/
│   ├── 02-templates/
│   ├── 03-folder-pattern/
│   ├── 04-link-pattern/
│   ├── 05-cluster-pattern/
│   ├── 06-reproduction-guide/
│   └── 07-environment/
└── 09-supporting-material/
    └── README.md
```

The study's openEHR archetypes and templates remain in the repository's `local/` directory. This package references those artifacts rather than duplicating them.

The `08-technical-proof-of-concept/` directory contains implementation and test artifacts for scenarios T0–T5, including technical documentation, templates, test requests, persisted objects, AQL queries, and recorded results. The `09-supporting-material/` directory contains supplementary research materials. Each directory has its own README with further navigation guidance.

## Synthetic evaluation dataset

The functional evaluation uses a synthetic longitudinal patient history containing **121 Medical Record Entries**.

The dataset includes acute and chronic clinical trajectories spanning multiple Care Encounters and Episodes of Care. Each Medical Record Entry is associated with the contextual information required to exercise the functional requirements, including chronological context, Episode-of-Care association, and Clinical Section classification.

The dataset contains no real patient data.

The synthetic dataset supports an assessment of whether each implementation pattern can represent and derive the information needed for the eight clinician-centered views. It is not intended to be statistically representative of a clinical population.

## Functional evaluation

Eight clinician-centered functional requirements are evaluated.

They cover:

-   chronological retrieval by Care Encounter
-   longitudinal retrieval by Episode of Care
-   organization by Clinical Section
-   combined chronological, Episode-oriented, and section-oriented views
-   derivation of a longitudinal Health Problem list
-   representation of a clinician-curated hierarchical Diagnosis and Problem List
-   SOAP-oriented documentation associated with one or more Health Problems
-   Clinical Section-oriented dashboard views

The file `04-functional-evaluation/functional-traceability.csv` links each requirement to:

-   evidence in the synthetic dataset
-   the common information model
-   its representation under each implementation pattern
-   the corresponding modeling or example artifact
-   the resulting design-level evaluation
-   the applicable evidence boundary
-   the corresponding manuscript result

The traceability matrix provides the evidence base for the functional comparison presented in Table 1 of the manuscript.

## Implementation patterns

### FOLDER-based pattern

The FOLDER-based pattern uses the openEHR EHR Directory to provide patient-level hierarchical organization of existing EHR content.

The representative example demonstrates alternative organizational perspectives, including Care Encounters, Episodes of Care, and Clinical Sections, without duplicating the referenced clinical content.

The example illustrates the evaluated relationship and navigation pattern. It does not provide a complete FOLDER representation of all 121 Medical Record Entries.

### LINK-based pattern

The LINK-based pattern uses the openEHR Reference Model `LINK` mechanism to represent explicit relationships between versioned EHR objects and contained LOCATABLE structures.

Two representative examples correspond to the two relationship levels evaluated in the manuscript:

-   relationships between Care Encounter COMPOSITIONs and clinical COMPOSITIONs
-   relationships between clinical ENTRYs and Episode-of-Care COMPOSITIONs

The examples document the direction, meaning, type, and target selection of relationships in the evaluated design.

### CLUSTER-based pattern

The CLUSTER-based pattern represents relationship metadata using archetyped and template-constrained structures.

The principal relationship archetypes are maintained in the repository's `local/` directory:

-   `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0`
-   `openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0`
-   `openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0`

These structures represent relationship metadata at the relevant levels of the information model and serve as the principal design artifacts for this pattern.

The supplied `.t.json` template exports do not contain references to the three `eoc_relationships_*` archetypes. The repository therefore documents these relationship CLUSTERs as developed design artifacts, but does not use **those original template exports** as evidence of their end-to-end template integration or execution.

Subsequently, the technical PoC implemented and evaluated two complementary CLUSTER-based relationship patterns:

-   **T4:** Relationship CLUSTERs in Care Encounter and Episode-of-Care COMPOSITIONs, referencing clinical COMPOSITIONs and ENTRYs.
-   **T5:** Relationship CLUSTERs within clinical ENTRYs, referencing Care Encounter and Episode-of-Care COMPOSITIONs.

The corresponding implementation templates, persisted COMPOSITIONs, AQL queries, and test results are documented in `08-technical-proof-of-concept/`. These experiments demonstrate technical feasibility within the tested EHRbase environment and scenarios. They do not establish automatic reference resolution, enforced referential integrity, or cross-platform interoperability.


## Technical proof of concept

The complementary technical PoC evaluates selected FOLDER-, LINK-, and CLUSTER-based implementations in an EHRbase test environment. Its small synthetic test dataset is distinct from the longitudinal dataset used for the design-level functional evaluation.

| Scenario | Focus | Documented evidence boundary |
| --- | --- | --- |
| T0 | Preliminary FOLDER feasibility | Initial technical feasibility, not a complete functional evaluation |
| T1 | Basic FOLDER implementation | Core operations verified. Clinical-view coverage is partial |
| T2 | LINK from contextual objects to clinical content | Executed and verified within the documented test scope |
| T3 | LINK from clinical content to contextual objects | Executed and verified within the documented test scope |
| T4 | CLUSTER relationships from contextual objects to clinical content | Executed and verified within the documented test scope |
| T5 | CLUSTER relationships from clinical ENTRYs to contextual objects | Executed and verified within the documented test scope, including a referential-integrity negative test |

The test plan and recorded results are documented in `08-technical-proof-of-concept/`, especially `DOC-03-poc-plan.md` and `DOC-04-poc-results.md`. The latter is the reference for actual execution status and observed outcomes. Successful persistence, independent retrieval, AQL-based reference extraction, automatic target dereferencing, and clinical-view reconstruction are distinct claims. The PoC evidence supports only those operations explicitly tested.

## Architectural evaluation

The architectural comparison evaluates the three patterns independently of their common functional adequacy.

The file `05-architectural-evaluation/architectural-evidence-matrix.csv` distinguishes the evidence supporting each architectural finding using the following categories:

-   **Specification**: properties defined by the openEHR specifications
-   **Design artifact**: properties demonstrated by the modeled structures or representative examples
-   **Comparative architectural inference**: qualitative conclusions derived from comparing the architectural consequences of the patterns
-   **Design synthesis**: architectural decisions derived from the comparative evaluation

These categories distinguish properties specified by openEHR, characteristics of the evaluated designs, and empirical observations.

No runtime performance benchmarking was performed.

## Technical environment

The following software environment was used during the modeling and technical assessment of the openEHR artifacts:

-   EHRbase 2.30.1 with PostgreSQL 16.6, deployed using the Docker Compose distribution provided by EHRbase
-   Postman 12.16.4
-   Medblocks openEHR Technical Course Postman collection
-   EHRbase openEHR SDK 2.31.0

This environment was used to execute the complementary technical PoC scenarios documented in `08-technical-proof-of-concept/`. The experiments include persistence and retrieval of openEHR objects, representations of relationships using FOLDER, LINK, and CLUSTER mechanisms, and selected AQL-based retrieval and reconstruction tests.

Validation is limited to the documented scenarios and test environment. No comparative performance benchmarking, production deployment validation, or multi-vendor interoperability testing was performed.

## Manuscript-to-artifact traceability

The file `07-manuscript-mapping/manuscript-artifact-mapping.md` maps the principal methods, results, tables, figures, and architectural claims of the manuscript to the corresponding repository artifacts.

The mapping distinguishes between source/design artifacts, functional design evaluation, comparative architectural inference, archetype-derived retrieval examples, and design synthesis. It also records important evidence boundaries so that representative design material is not interpreted as production or runtime validation.

## Hybrid architecture

The hybrid architecture described in the manuscript is **not a fourth evaluated implementation pattern**.

It is a design synthesis derived from the comparative evaluation.

The proposed architecture combines:

-   an Episode-of-Care COMPOSITION as the longitudinal representation of an individual Health Problem
-   governed CLUSTER structures for relationship metadata
-   FOLDER structures for patient-level navigation and indexing
-   selective LINKs where explicit Reference Model-level relationships are beneficial
-   archetyped ENTRYs within clinical COMPOSITIONs as the authoritative representation of clinical statements
-   query and application logic for derived lists and views

The rationale for this synthesis is documented in `05-architectural-evaluation/hybrid-design-rationale.md`.

The proposed hybrid architecture is therefore a **testable design hypothesis**, not a production-validated architecture.

## Retrieval examples

Representative retrieval examples are provided for each implementation pattern:

-   `06-retrieval-examples/folder/README.md` documents Directory traversal and resolution of referenced EHR objects
-   `06-retrieval-examples/link/README.md` documents LINK traversal and target resolution
-   `06-retrieval-examples/cluster/README.md` documents retrieval based on the modeled relationship CLUSTER paths
-   `06-retrieval-examples/cluster/representative-queries.aql` contains representative AQL examples derived from the CLUSTER archetype structure

These examples illustrate **design-level** retrieval logic and query paths relevant to the functional requirements. They are neither a comprehensive query library nor evidence of comparative query performance.

Separately, `08-technical-proof-of-concept/` contains AQL queries executed against the experimental EHRbase dataset, together with documented results. Design-level examples and executed PoC queries serve different purposes and are not interchangeable forms of evidence.

The CLUSTER AQL examples are **archetype-derived examples**. They have not been execution-validated against the complete dataset of 121 Medical Record Entries in an identified openEHR CDR. They therefore do not constitute runtime validation.

Where relationship targets require explicit reference resolution, the documented workflow distinguishes retrieval of relationship metadata from subsequent resolution of the referenced target.

## Relationship to the original Masterclass thesis

The research reported in the manuscript builds on modeling work originally developed as part of the author's openEHR Masterclass thesis.

The thesis provides broader background material, additional modeling artifacts, and earlier forms of the evaluation.

For the purposes of reproducing the manuscript, the artifacts in this `reproducibility/` directory and the explicitly referenced models in `local/` constitute the manuscript-specific evidence package.

Where the thesis and the manuscript differ in terminology, evaluation framing, or interpretation, the **manuscript and this reproducibility package represent the authoritative version for the published study**.

## Reuse and interpretation

The artifacts support inspection, reproduction of the design reasoning, and subsequent implementation and evaluation.

Users of the package should distinguish between:

-   reproducibility of the information-model design
-   reproducibility of the functional design evaluation
-   implementation of the patterns in a particular openEHR platform
-   empirical evaluation of runtime, interoperability, scalability, or clinical usability

The first two are addressed by the design-level evaluation. In addition, the technical PoC artifacts support inspection and, subject to the documented environment and prerequisites, reproduction of selected implementation experiments. The package does not establish production readiness, comparative runtime performance, clinical usability, deployment scalability, or multi-vendor interoperability.

## Use of Generative AI

ChatGPT (OpenAI, including GPT-5.6 and GPT-6 models, accessed in 2026, https://chatgpt.com) was used to support the preparation, structuring, and refinement of this reproducibility package. Its use included drafting and editing technical and scientific documentation, preparing and refining evaluation and traceability matrices, performing cross-document consistency checks, and providing AI-assisted scientific and editorial review. The author critically reviewed and revised AI-assisted outputs, including the functional traceability matrix, and remains responsible for verifying the scientific interpretations, technical accuracy, and integrity of the research artifacts. AI-assisted review does not constitute independent experimental validation or reproduction of the reported results.

## Citation

A versioned archival release of this reproducibility package will be deposited in a persistent research repository.

The final release DOI and recommended citation will be added here once the manuscript-specific artifact set has been frozen.
