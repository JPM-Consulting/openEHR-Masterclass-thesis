# Representative Retrieval Workflows

## Purpose

This directory documents representative retrieval workflows for the three openEHR implementation patterns evaluated in:

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in
openEHR: A Comparative Evaluation of Three Implementation Patterns.***

These examples make the retrieval implications of the evaluated designs inspectable within the evidence available from the study.

This directory is **not a query benchmark suite**. The three patterns do not necessarily support identical retrieval mechanisms.

## Why the examples are intentionally asymmetric

The comparative evaluation identified different logical retrieval strategies for the three patterns:

| Pattern | Representative retrieval strategy |
| --- | --- |
| FOLDER | Directory traversal followed by resolution of referenced EHR objects |
| LINK | Relationship traversal followed by target resolution when target content is required |
| CLUSTER | Filtering and projection of locally represented relationship metadata through archetyped paths, with target resolution when referenced content is required |

The examples preserve these differences rather than forcing all three patterns into a common AQL form. This asymmetry reflects the architectural comparison.

## Directory structure

``` text
06-retrieval-examples/
├── README.md
├── folder/
│   └── README.md
├── link/
│   └── README.md
└── cluster/
    ├── README.md
    └── representative-queries.aql
```

Interpret the pattern-specific examples alongside the implementation artifacts in `../02-implementation-patterns/` and the archetypes and templates in `../../local/`.

## Common retrieval scenarios

The examples draw on the clinician-centered requirements used in the functional evaluation.

Representative scenarios include:

1.  retrieve clinical information associated with a Care Encounter
2.  retrieve clinical information associated with a selected Episode of Care or Health Problem
3.  retrieve or project information according to Clinical Section
4.  combine Episode context with another classification dimension such
    as Clinical Section or SOAP

The examples illustrate how relationships can support these workflows. They do not provide executable query coverage for all eight functional requirements. Clinical Section and SOAP scenarios are illustrated only where the modeled metadata supports them.

## FOLDER retrieval

The FOLDER-based pattern uses the patient-level EHR Directory for organization and navigation.

A representative workflow is:

``` text
EHR
  ↓
Directory / VERSIONED_FOLDER
  ↓
selected FOLDER hierarchy
  ↓
OBJECT_REF or other modeled reference
  ↓
referenced EHR object
  ↓
required clinical information
```

An Episode-oriented FOLDER can index existing clinical objects associated with a selected Episode of Care. Retrieval involves identifying the relevant FOLDER and resolving its references.

The representative FOLDER artifact is:

`../02-implementation-patterns/folder/folder-example.json`

Detailed workflow documentation is provided in:

`folder/README.md`

No portable single-statement AQL example is asserted for this workflow in this reproducibility package.

## LINK retrieval

The LINK-based pattern represents explicit relationships through the openEHR RM LINK structure.

A representative workflow is:

``` text
source LOCATABLE
  ↓
LINK
  ├── meaning
  ├── type
  └── target
       ↓
    DV_EHR_URI
       ↓
target resolution
       ↓
target information, where required
```

Two relationship contexts are represented in the repository:

-   Care Encounter ↔ clinical COMPOSITION
-   clinical ENTRY ↔ Episode-of-Care COMPOSITION

Representative artifacts are:

-   `../02-implementation-patterns/link/care-encounter-links.json`
-   `../02-implementation-patterns/link/episode-of-care-links.json`

Detailed workflow documentation is provided in:

`link/README.md`

Identifying a LINK and retrieving information stored in its target are distinct operations. If the required information resides in the target object, its URI must be resolved.

These examples do not establish that traversal and target resolution can be expressed in one portable AQL statement across openEHR implementations.

## CLUSTER retrieval

The CLUSTER-based pattern represents relationship metadata through explicit archetyped structures.

A representative workflow is:

``` text
clinical or contextual COMPOSITION
  ↓
relevant ENTRY / modeled structure
  ↓
relationship CLUSTER
  ├── Care Encounter reference
  ├── Episode association
  ├── Episode role
  ├── Clinical Section
  └── SOAP classification, where modeled
       ↓
AQL filtering / projection over modeled paths
```

The principal relationship archetypes are:

-   `../../local/openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl`
-   `../../local/openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl`
-   `../../local/openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl`

Their manuscript-specific role is documented in:

`../02-implementation-patterns/cluster/README.md`

Representative AQL examples illustrate retrieval of locally represented relationship metadata through archetyped paths.

CLUSTER does **not** eliminate reference resolution. If the required information exists only in a referenced Care Encounter, Episode-of-Care COMPOSITION, or other target object, that target must still be resolved.

## Interpretation of the AQL examples

The AQL examples illustrate **logical query structures** derived from the modeled artifacts. They are not, by themselves, evidence of successful execution.

Before an AQL example is treated as executable evidence, its paths and syntax should be checked against:

-   the exact archetype version
-   the exact template used for persistence
-   the operational template or equivalent deployed model
-   the AQL implementation of the target openEHR platform
-   the actual persisted data representation

Architectural conclusions in the manuscript do not assume that an unverified example query runs unchanged on every openEHR CDR.

## Relationship to the evidence model

The retrieval examples complement the following evidence artifacts:

-   `../04-functional-evaluation/functional-requirements.md`
-   `../04-functional-evaluation/functional-traceability.csv`
-   `../05-architectural-evaluation/architectural-evidence-matrix.csv`
-   `../05-architectural-evaluation/hybrid-design-rationale.md`

The functional traceability matrix documents design-level support for each requirement. The architectural evidence matrix compares the characteristics of the three patterns. The retrieval examples illustrate differences in their logical retrieval structures.

## Evidence boundary

The retrieval examples support claims about:

-   the logical retrieval path associated with each evaluated pattern
-   the distinction between locally represented relationship metadata
    and referenced target information
-   the role of Directory traversal for FOLDER
-   the role of relationship traversal and target resolution for LINK
-   the role of archetyped paths for CLUSTER relationship metadata

They do **not** establish:

-   comparative query performance
-   latency or throughput
-   production-scale behavior
-   query optimizer behavior
-   universal AQL portability
-   cross-CDR target resolution
-   multi-vendor interoperability
-   clinical usability of the resulting views

These examples do not support a performance ranking.

## Reproducibility status

The FOLDER and LINK examples document representative retrieval workflows based on the corresponding design artifacts.

CLUSTER AQL examples are present in `cluster/representative-queries.aql`. Q1 and Q2 have been aligned with the relationship paths and containment structure used in executed T5 AQL-05 and AQL-04, respectively. The representative statements themselves have not been executed. Q3 and Q4 remain model-derived illustrations of optional Clinical Section and SOAP assignment metadata. The executed T5 queries and available results are documented separately under `../08-technical-proof-of-concept/05-cluster-pattern/T5/`.

The distinction between executed queries and illustrative examples is essential to the evidence boundary. Illustrative examples must not be interpreted as empirically validated query results.
