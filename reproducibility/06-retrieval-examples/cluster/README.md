# CLUSTER-Based Retrieval Examples

This directory documents representative retrieval approaches for the CLUSTER-based implementation pattern evaluated in:

**Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns**

The examples are derived from the relationship archetypes supplied with this repository and illustrate retrieval through archetype-defined paths. The four example queries have **not been executed verbatim**. Q1 and Q2 reflect retrieval mechanisms separately tested in T5, whereas Q3 and Q4 are model-derived illustrations without corresponding executed tests. These examples do not establish runtime performance, portability across openEHR implementations, or production readiness.

## Contents

``` text
cluster/
├── README.md
└── representative-queries.aql
```

The corresponding relationship archetypes are maintained in the repository-level `local/` directory.

## Relationship model

The CLUSTER-based pattern represents relationship context as archetyped content rather than through Directory organization or Reference Model LINK relationships.

The design uses three project-specific relationship archetypes:

``` text
../../../local/openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl
../../../local/openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl
../../../local/openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl
```

They address relationship context at three complementary levels:

-   **ENTRY level:** associations of a clinical ENTRY with its Care Encounter and one or more Episodes of Care, together with Clinical Section and optional SOAP classifications
-   **Care Encounter level:** relationship context associated with a Care Encounter
-   **Episode-of-Care level:** relationship context associated with the longitudinal Episode-of-Care representation

The retrieval examples focus on `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0`, which exposes references and classifications associated with an individual clinical ENTRY.

## ENTRY relationship archetype

The relevant structure of `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0` is:

``` text
CLUSTER[at0000]  EoC Relationships entry
│
├── CLUSTER[at0001]  Contact reference [1..1]
│   └── ELEMENT[at0009]  Link [1..1]
│       └── DV_EHR_URI
│
├── CLUSTER[at0109]  Episode reference [1..*]
│   ├── ELEMENT[at0147]  Link [1..1]
│   │   └── DV_EHR_URI
│   └── ELEMENT[at0153]  Role [1..1]
│       └── DV_CODED_TEXT
│           ├── at0154  Primary
│           └── at0155  Associated
│
├── CLUSTER[at0003]  Assignments [0..1]
│   ├── ELEMENT[at0010]  Clinical Section [0..1]
│   │   └── DV_CODED_TEXT
│   └── ELEMENT[at0011]  SOAP [0..1]
│       └── DV_CODED_TEXT
│
└── ELEMENT[at0005]  Comment [0..1]
    └── DV_TEXT
```

This structure provides the modeled paths used in the representative AQL in `representative-queries.aql`.

## Representative retrieval questions

The AQL file illustrates four retrieval questions relevant to the functional evaluation.

### 1. Retrieve relationship context for a Care Encounter

The Care Encounter reference is represented as a `DV_EHR_URI` under:

``` text
items[at0001]/items[at0009]
```

This path can be used to identify clinical information associated with a specified Care Encounter.

Conceptually:

``` text
clinical information
        ↓
EoC relationship CLUSTER
        ↓
Contact reference
        ↓
Care Encounter
```

The example illustrates retrieval by Care Encounter reference. Its relationship to the functional requirements is documented in `../../04-functional-evaluation/functional-traceability.csv`.

### 2. Retrieve relationship context for an Episode of Care

Episode references are represented by the repeatable `Episode reference` CLUSTER under:

``` text
items[at0109]/items[at0147]
```

with the associated role represented under:

``` text
items[at0109]/items[at0153]
```

The role terminology distinguishes:

``` text
at0154  Primary
at0155  Associated
```

These values distinguish a primary Episode association from additional associated Episodes.

The `Episode reference` CLUSTER is repeatable (`1..*`). Each Episode reference contains exactly one `Link` (`1..1`) and exactly one `Role` (`1..1`), thereby explicitly pairing the referenced Episode-of-Care COMPOSITION with its relationship role. The Role value is constrained to `Primary` or `Associated`. The additional model-level invariant requiring exactly one `Primary` Episode association per clinical ENTRY is not independently enforced by the archetype and requires additional validation in the implementation context.

The example illustrates retrieval by Episode reference and association role. The functional traceability matrix documents the corresponding design-level assessment.

### 3. Retrieve information by Clinical Section

The Clinical Section assignment is represented under:

``` text
items[at0003]/items[at0010]
```

and uses coded values defined by the archetype.

Where this optional classification is populated, the modeled path can be used to filter or project clinical information by Clinical Section.

Conceptually:

``` text
clinical information
        ↓
EoC relationship CLUSTER
        ↓
Assignments
        ↓
Clinical Section
```

This is a model-derived example. No corresponding populated T5 data or executed query was established for this classification.

### 4. Combine Episode, Clinical Section, and SOAP context

The archetype provides paths for multiple contextual dimensions within one governed structure.

The SOAP assignment is represented under:

``` text
items[at0003]/items[at0011]
```

with coded values for Subjective, Objective, Assessment, Plan, and Not applicable.

Representative retrieval can therefore combine:

-   Episode-of-Care reference
-   Episode association role
-   Clinical Section
-   SOAP assignment

At design level, these paths illustrate how different contextual classifications could be combined without duplicating the underlying clinical statement. This combination was not validated by executing Q4.

## Representative AQL

`representative-queries.aql` contains four illustrative queries derived from the modeled paths.

The examples use the relationship archetype as a query constraint:

``` text
CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0]
```

and then address relationship attributes through archetype paths.

The queries make the proposed retrieval approach inspectable. They are neither a conformance suite nor validated portable production queries.

## Reference resolution

The relationship archetypes use `DV_EHR_URI` for references to related openEHR objects.

A query can retrieve a stored reference through an archetype path. Retrieving attributes held only in the referenced target requires separate resolution supported by the implementation or application architecture.

The examples in this repository do **not** demonstrate portable AQL dereferencing of `DV_EHR_URI` targets.

## Semantic governance

The CLUSTER pattern expresses relationship structures through archetypes, with further constraints possible through templates.

In the evaluated design this provides explicit paths and controlled structures for concepts such as:

-   Care Encounter reference
-   Episode-of-Care reference
-   primary or associated Episode role
-   Clinical Section
-   SOAP assignment

In the evaluated design, these explicit constraints support the comparative assessment that CLUSTER offers the strongest **in-template semantic governance** of the three patterns. This is an architectural inference, not a claim of universal superiority.

## Relationship to the supplied templates

The relationship CLUSTER archetypes are supplied in `local/`.

The `.t.json` exports under `local/` must not be confused with the scenario-specific templates and persisted JSON used in the technical PoC. The T5 tests independently document the integration and successful persistence of `eoc_relationships_entry.v0` at `ENTRY.protocol` in scenario-specific MR templates. This does not demonstrate that every `.t.json` file under `local/` includes these relationship structures.

The design artifacts and the scenario-specific technical evidence therefore have different evidentiary roles.

## Evidence boundary

The material in this directory supports inspection of the modeled structures and design-level retrieval reasoning.

It documents:

-   explicit archetype paths for relationship information
-   the proposed retrieval structure of the CLUSTER pattern
-   how Care Encounter, Episode-of-Care, Clinical Section, and SOAP context can be addressed in the model
-   how representative AQL statements can be derived from those paths

It does **not** demonstrate:

-   verbatim execution of the four example queries
-   successful execution of Q3/Q4 against a named CDR/version
-   query-performance characteristics
-   production scalability
-   portable automatic dereferencing of `DV_EHR_URI`
-   empirical multi-vendor interoperability
-   clinical usability or clinical outcomes

The examples should therefore be described as **archetype-derived representative queries**, not as validated runtime queries.

## Recommended future validation

A subsequent technical evaluation could strengthen the evidence by:

1.  executing the illustrative queries against a specified CDR and documenting any required adaptations
2.  populating and testing the optional Clinical Section and SOAP assignment metadata used by Q3 and Q4
3.  documenting expected and observed result sets
4.  repeating the evaluation across multiple implementations, where feasible

Such work would move the evidence from design-level retrieval plausibility toward empirical implementation validation.

## Traceability

The broader retrieval comparison is documented in:

`../README.md`

The CLUSTER implementation-pattern documentation is located at:

`../../02-implementation-patterns/cluster/README.md`

The functional evaluation is documented under:

`../../04-functional-evaluation/`

The architectural comparison is documented under:

`../../05-architectural-evaluation/`

The manuscript-to-artifact mapping is maintained in:

`../../07-manuscript-mapping/manuscript-artifact-mapping.md`

## Relationship to executed T5 retrieval evidence

The technical PoC documents **executed** T5 AQL queries against EHRbase 2.30.1. AQL-05 provides evidence for Care Encounter-oriented retrieval corresponding to Q1 (8 reported rows for CE2), while AQL-04 provides evidence for Episode-oriented retrieval corresponding to Q2 (12 reported rows for EP2). Executed query texts and reported results are documented in `../../08-technical-proof-of-concept/05-cluster-pattern/T5/T5-aql-query-catalog.md`.

The four queries in `representative-queries.aql` remain **adapted illustrations** and were not executed verbatim. Q3 and Q4 use optional Clinical Section and SOAP assignment metadata for which neither populated T5 data nor corresponding executed queries have been established. The documented SOAP reconstruction instead used SECTION traversal (AQL-09–AQL-12), not the optional SOAP assignment field illustrated by Q4. No additional EHRbase tests were performed for this documentation update.
