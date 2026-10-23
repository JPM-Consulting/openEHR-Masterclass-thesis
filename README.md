# openEHR Episode-Oriented Medical Record Research

This repository brings together the modeling artifacts, publications, and reproducibility materials from research on representing an episode-oriented medical record in openEHR.

The research began with the 2025 openEHR Masterclass thesis:

**Data Model of the Episode-Oriented Medical Record according to Solon in openEHR**

The work subsequently informed an accepted EHRCON26 conference contribution and the comparative study:

**Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns**

The comparative study examines how relationships among Care Encounters (Contacts), Episodes of Care (Health Problems), and clinical information can be represented using existing openEHR structures without modifying the Reference Model.

## Research context

The conceptual information model distinguishes three principal dimensions:

-   Care Encounter (Contact): the chronological care-event dimension
-   Episode of Care: the longitudinal representation of a distinct Health Problem
-   Administrative Encounter: the organizational care-period dimension

Clinical statements are represented as archetyped ENTRYs within clinical COMPOSITIONs. Clinical Sections provide an additional dimension for semantic classification.

The study compares three openEHR implementation patterns for representing relationships among these dimensions:

1.  **FOLDER-based organization**
2.  **LINK-based relationships**
3.  **CLUSTER-based relationship structures**

These patterns offer alternative architectural representations of relationships within a shared episode-oriented information model. They do not constitute separate clinical information models.

## Publications

The `publications/` directory traces the research through three related but distinct scholarly outputs:

### Masterclass thesis

**Jean-Pierre Messerli. *Data Model of the Episode-Oriented Medical Record according to Solon in openEHR.* openEHR Masterclass Thesis, 2025.**

The thesis presents the original conceptual model and its openEHR mapping, together with background research, implementation considerations, and an initial evaluation.

Repository location:

`publications/masterclass-thesis/Messerli_2025_Masterclass_Thesis.pdf`

### EHRCON26 conference abstract

**Jean-Pierre Messerli. *Modelling the Episode-Oriented Medical Record according to Solon in openEHR: Patterns for Longitudinal, Problem- and Episode-Centred Care.* EHRCON26, Amsterdam, 2026.**

The accepted conference abstract presents an intermediate stage of the research, linking the Masterclass thesis to the subsequent full manuscript.

Repository location:

`publications/ehrcon26/Messerli_2026_EHRCON26_Abstract.pdf`

### Frontiers manuscript

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.* 2026.**

The manuscript extends the original work through a structured, design-level comparison of the FOLDER-, LINK-, and CLUSTER-based implementation patterns.

Publication status and future article reference:

[`publications/frontiers/README.md`](publications/frontiers/README.md)

The manuscript is not included in this public repository during preparation, submission, or peer review.

The manuscript-specific evidence package is maintained separately under `reproducibility/`.

For additional information on the publication pathway, see:

[`publications/README.md`](publications/README.md)

## Repository structure

``` text
openEHR-Masterclass-thesis/
│
├── README.md
├── CITATION.cff
├── LICENSE.md
│
├── publications/
│   ├── README.md
│   ├── masterclass-thesis/
│   │   └── Messerli_2025_Masterclass_Thesis.pdf
│   ├── ehrcon26/
│   │   └── Messerli_2026_EHRCON26_Abstract.pdf
│   └── frontiers/
│       ├── README.md
│       └── [supporting figures]
│
├── local/
│   ├── README.md
│   └── [openEHR archetypes and templates]
│
└── reproducibility/
    ├── README.md
    ├── 01-conceptual-model/
    ├── 02-implementation-patterns/
    ├── 03-synthetic-dataset/
    ├── 04-functional-evaluation/
    ├── 05-architectural-evaluation/
    ├── 06-retrieval-examples/
    ├── 07-manuscript-mapping/
    ├── 08-technical-proof-of-concept/
    └── 09-supporting-material/
```

## openEHR modeling artifacts

The `local/` directory contains openEHR archetypes and templates developed or used in the research.

The artifacts address:

-   Administrative Encounters
-   Care Encounters
-   Episodes of Care
-   Health Problems
-   Diagnosis and Problem Lists
-   SOAP-oriented documentation
-   Clinical Sections
-   relationship structures between clinical ENTRYs, Care Encounters, and Episodes of Care

This directory includes both supporting openEHR models and project-specific artifacts. Inclusion does not imply that every artifact was integrated into or tested as part of an executable end-to-end implementation.

For artifact provenance and licensing information, see:

[`local/README.md`](local/README.md)

## Reproducibility package

The `reproducibility/` directory provides the evidence package accompanying the manuscript:

***Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.***

The package includes:

-   the conceptual information model and its openEHR mapping
-   representative artifacts for the FOLDER-, LINK-, and CLUSTER-based patterns
-   the synthetic longitudinal patient record used for the functional design evaluation
-   the eight clinician-centered functional requirements
-   functional traceability across requirements and implementation patterns
-   the evidence matrix for the architectural comparison
-   representative retrieval workflows and archetype-derived AQL examples
-   the rationale for the proposed hybrid architecture
-   explicit mapping between manuscript claims and repository artifacts
-   documented technical PoC tests (T0–T5), their archived evidence, environment information, and reproduction instructions
-   supporting research and presentation materials

For details, see:

[`reproducibility/README.md`](reproducibility/README.md)

## Evidence boundaries

The study primarily presents a **design-level comparative evaluation**, complemented by a scoped technical proof of concept. The two evidence levels are documented separately.

The repository provides materials for examining and, where the supplied artifacts permit, reproducing:

-   the conceptual information-model design
-   the openEHR modeling approach
-   the three evaluated relationship patterns
-   the functional design evaluation against eight clinician-centered requirements
-   the qualitative architectural comparison
-   the reasoning leading to the proposed hybrid architecture

These materials do **not** constitute three complete production implementations or demonstrate independent end-to-end reproduction of every reported result.

The available evidence does not establish:

-   runtime superiority of one pattern
-   comparative query performance
-   production-scale scalability
-   clinical usability
-   clinical or patient outcomes
-   cross-CDR reference resolution
-   empirically validated multi-vendor interoperability

Accordingly, the proposed hybrid architecture remains a **testable design hypothesis**, not a production-validated architecture.

## Relationship between the thesis, EHRCON26 abstract, and current study

The Masterclass thesis documents the initial research and modeling work.

The EHRCON26 abstract presents the research in a focused conference format.

The comparative manuscript refines the terminology, distinguishes functional adequacy from architectural characteristics, systematically compares the three implementation patterns, and specifies the evidentiary limits of the evaluation.

When terminology, evaluation scope, implementation details, or conclusions differ across the publications, the **current manuscript and its `reproducibility/` package take precedence** for interpreting the comparative study.

The thesis and conference abstract remain available as separate records of the research trajectory.

## Reuse

The repository is intended to support:

-   inspection of the episode-oriented information model
-   reuse and further development of the modeling approach
-   implementation experiments with FOLDER, LINK, and CLUSTER patterns
-   independent evaluation of the proposed architecture
-   future multi-vendor and cross-platform validation

Reuse should preserve the distinction between design artifacts, documented PoC observations, and claims supported by empirical validation.

## Citation

Repository-level citation metadata are provided in:

[`CITATION.cff`](CITATION.cff)

Each publication should be cited according to its bibliographic status. After publication of the full article, the repository metadata can be updated with its definitive citation and persistent identifier.

## License

For repository-level licensing information and guidance on third-party or derived openEHR artifacts, see:

[`LICENSE.md`](LICENSE.md)

Individual openEHR archetypes and other reused artifacts may be subject to their original provenance and licensing terms. Inclusion in this repository does not supersede those terms.
