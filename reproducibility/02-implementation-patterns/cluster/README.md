# CLUSTER-based implementation pattern

## Purpose

This directory documents the CLUSTER-based implementation pattern examined in:

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.***

Unlike the FOLDER and LINK directories, this directory does not contain a separate illustrative relationship artifact. The principal CLUSTER relationship archetypes are maintained in the repository's `local/` directory. This README maps those artifacts to the conceptual relationships examined in the study and to Figure 6 of the manuscript.

## Core design principle

In the CLUSTER-based pattern, relationship information is represented as explicit archetyped content within the relevant openEHR structures.

The pattern separates three relationship contexts:

1.  relationship context attached to a clinical ENTRY
2.  relationship context represented for a Care Encounter
3.  relationship context represented for an Episode of Care

Archetypes and templates can constrain relationship semantics, cardinalities, and relevant classifications, reducing reliance on application-specific conventions.

Relationship CLUSTERs do not replace the referenced clinical objects. Clinical statements remain in their source ENTRYs and COMPOSITIONs, while the CLUSTERs represent structured metadata and references linking those objects.

## Existing relationship archetypes

The following three archetypes in `local/` are the principal manuscript-specific artifacts for the CLUSTER pattern.

### 1. `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl`

**Role:** Relationship context for a clinical ENTRY.

This archetype represents relationships that place an individual Medical Record Entry within the multidimensional episode-oriented model.

In the evaluated design, the ENTRY-level relationship structure can represent:

-   a reference to the corresponding Care Encounter
-   one or more Episode references, each comprising one reference to an Episode-of-Care COMPOSITION and one relationship role
-   a constrained relationship role of `Primary` or `Associated` for each Episode reference
-   Clinical Section classification
-   SOAP classification where applicable

The `Episode reference` CLUSTER is repeatable (`1..*`). Within each Episode reference, `Link` and `Role` occur exactly once (`1..1`), thereby maintaining an explicit association between the referenced Episode of Care and its role.

This structure provides a modeled basis for associating clinical ENTRYs with Care Encounters and Episodes of Care. It also accommodates Clinical Section and SOAP classifications where these are represented in the evaluated design. The contribution of these elements to individual functional requirements is documented in the functional traceability matrix.

### 2. `openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl`

**Role:** Relationship context for the Care Encounter representation.

This archetype represents relationship information associated with the Care Encounter COMPOSITION.

In the evaluated design, the Care Encounter relationship structure supports references to clinical information belonging to the Care Encounter and can carry the relationship context required to connect the chronological care-event dimension with the wider episode-oriented record.

Care Encounter and Episode of Care remain distinct conceptual dimensions. A Care Encounter may include clinical information associated with multiple Health Problems.

This archetype provides a modeled basis for relationships originating from the Care Encounter context. Its contribution to the functional evaluation is documented in the functional traceability matrix.

### 3. `openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl`

**Role:** Relationship context for the Episode-of-Care representation.

This archetype represents relationship information associated with an Episode-of-Care COMPOSITION.

In the evaluated design, the Episode-level relationship structure supports references from the longitudinal Episode representation to related clinical information and relationship context.

In the adopted model, the Episode-of-Care COMPOSITION represents the longitudinal identity and lifecycle of a distinct Health Problem. It does not contain duplicate copies of all related clinical content.

This archetype provides a modeled basis for relationships originating from the Episode-of-Care context. Its contribution to the functional evaluation is documented in the functional traceability matrix.

## Supporting modeling artifacts

The three relationship CLUSTER archetypes are designed to complement the common clinical information model used across all three implementation patterns.

The common information model provides the clinical and contextual structures for Care Encounters, Episodes of Care, Medical Record Entries, and clinical documentation. The CLUSTER-based pattern adds archetyped relationship structures to represent associations between these elements.

The underlying clinical archetypes and templates are maintained in the repository’s `local/` directory and are not specific to the CLUSTER-based implementation pattern.

## Mapping to Figure 6

Figure 6 of the manuscript illustrates the CLUSTER pattern across three principal contexts.

| Figure 6 context | Repository artifact | Function in the evaluated design |
| --- | --- | --- |
| Clinical ENTRY | `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl` | Relates a clinical ENTRY to its Care Encounter and to one or more Episodes of Care. Each Episode reference pairs a COMPOSITION reference with a constrained role and may include governed classification metadata. |
| Care Encounter COMPOSITION | `openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl` | Represents relationship context associated with the chronological Care Encounter. |
| Episode-of-Care COMPOSITION | `openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl` | Represents relationship context associated with the longitudinal Episode of Care or Health Problem. |

Figure 6 provides a conceptual overview of how the three relationship archetypes represent associations between clinical ENTRYs, Care Encounters, and Episodes of Care in the CLUSTER-based implementation pattern.

## Relationship cardinality and Episode roles

A central requirement of the evaluated model is that each clinical ENTRY is associated with:

-   exactly one primary Episode of Care
-   zero or more additional associated Episodes of Care where clinically relevant

In `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0`, Episode associations are represented by the repeatable `Episode reference` CLUSTER (`1..*`). Each Episode reference contains exactly one `Link` (`1..1`) to an Episode-of-Care COMPOSITION and exactly one `Role` (`1..1`). The Role value is constrained to `Primary` or `Associated`.

The archetype pairs each Episode reference with a relationship role. However, it does not independently enforce the model-level invariant that exactly one Episode reference associated with a clinical ENTRY has the role `Primary`. This invariant requires additional enforcement, such as template-level constraints where expressible or application-level validation.

This distinction is important for clinical information that is primarily documented in relation to one Health Problem but is also clinically relevant to additional Health Problems.

## Clinical Section and SOAP classification

Clinical Section and SOAP provide additional classification dimensions over the same underlying clinical information.

In the CLUSTER-based design, these classifications can be represented as governed relationship or contextual metadata associated with the relevant clinical ENTRY.

This allows the same source clinical information to participate in:

-   chronological Care Encounter views
-   longitudinal Episode-oriented views
-   Clinical Section-oriented views
-   SOAP-oriented documentation views

without creating separate authoritative copies of the clinical statement for each view.

## Queryability

A principal architectural characteristic of the CLUSTER pattern is that modeled relationship attributes are exposed through archetyped paths.

This allows locally represented relationship metadata, such as Care Encounter references, Episode associations, Clinical Section, or SOAP classification, to participate in AQL filtering and projection using stable modeled paths.

This does **not** eliminate the need for reference resolution.

Where information required by a query resides only in the referenced Care Encounter, Episode-of-Care COMPOSITION, or another target object, that target still has to be resolved.

The relevant distinction is therefore between:

-   querying relationship metadata represented locally in the CLUSTER
-   retrieving information that exists only in the referenced target object

The comparison addresses this distinction at the level of query design. No comparative runtime benchmarks were performed.

## Semantic governance

The CLUSTER pattern places relationship semantics and constraints within archetypes and templates.

Compared with relationship structures governed primarily through directory organization or application conventions, this provides an explicit location for defining:

-   relationship elements
-   cardinalities
-   value constraints
-   Episode roles
-   Clinical Section or SOAP classifications where modeled
-   reusable paths for querying relationship metadata

The extent of this governance depends on the constraints expressible in the corresponding archetype or template. Model-level invariants that are not explicitly enforced by these constraints require additional validation.

The manuscript therefore characterizes CLUSTER as providing the strongest **in-template semantic governance in the evaluated design**.

This finding is specific to the evaluated architecture and does not establish universal superiority over FOLDER or LINK.

## Versioning and provenance

Relationship CLUSTERs are persisted as part of their containing COMPOSITION.

A change to relationship information represented by such a CLUSTER therefore follows the version lifecycle of the owning version-controlled COMPOSITION.

This differs from the FOLDER pattern, in which changes to the patient-level directory organization are versioned separately from the referenced clinical COMPOSITIONs.

The CLUSTER pattern consequently couples relationship changes to the version history of the clinical or contextual COMPOSITION in which the relationship structure is embedded.

## Cross-system interpretation

Shared archetypes and templates can communicate the structure and constraints of CLUSTER-based relationship information between systems.

However, shared models alone do not guarantee cross-system semantic interoperability.

Cross-CDR use additionally depends on matters such as:

-   shared terminology and model governance
-   stable identifiers
-   compatible reference conventions
-   agreed mechanisms for resolving referenced objects

The study does not empirically demonstrate multi-vendor or cross-repository interoperability.

## Relationship to the functional evaluation

The contribution of the CLUSTER relationship artifacts to individual functional requirements is documented in the CLUSTER column of:

`../../04-functional-evaluation/functional-traceability.csv`

The functional evaluation should be interpreted as a combination of:

1.  the common information model
2.  the synthetic longitudinal patient medical record
3.  the relationship structures represented by these archetypes and templates

The relationship archetypes alone do not constitute a complete clinical record.

## Relationship to the hybrid design

The CLUSTER pattern also contributes to the hybrid architecture synthesized from the comparative evaluation.

In that synthesis:

-   the Episode-of-Care COMPOSITION provides the longitudinal representation of a distinct Health Problem
-   relationship CLUSTERs provide governed semantic association metadata
-   FOLDER can provide patient-wide hierarchical navigation and indexing
-   LINK can be used selectively where an explicit RM-level object-to-object relationship is appropriate
-   clinical ENTRYs remain the authoritative source of clinical statements
-   lists and other views can be derived at query or application level without duplicating clinical content

The hybrid architecture was **not evaluated as a fourth implementation pattern**. It remains a design synthesis and testable architectural hypothesis derived from the comparison.

## Evidence boundary

The CLUSTER archetypes and templates enable inspection of the relationship structures modeled in the study.

Together with the functional and architectural evaluation artifacts, they support design-level claims concerning:

-   explicit archetyped representation of relationship metadata
-   governed Care Encounter and Episode associations
-   explicit pairing of each Episode reference with a constrained `Primary` or `Associated` role
-   Clinical Section and SOAP classification where modeled
-   stable archetyped paths for querying locally represented relationship metadata
-   coupling of relationship changes to the version lifecycle of the owning COMPOSITION

They do **not** demonstrate:

-   production deployment of the complete design
-   runtime or query-performance superiority
-   clinical usability
-   production-scale concurrency behavior
-   empirically validated multi-vendor interoperability
-   automatic resolution of all referenced targets
-   archetype-level enforcement of the model-level invariant requiring exactly one `Primary` Episode association per clinical ENTRY
-   universal architectural superiority of CLUSTER over FOLDER or LINK

## Traceability

This README should be interpreted together with:

-   `../../../local/`
-   `../../04-functional-evaluation/functional-requirements.md`
-   `../../04-functional-evaluation/functional-traceability.csv`
-   the architectural evidence matrix in `../../05-architectural-evaluation/`

This directory does not duplicate the relationship archetypes. The files in `local/` remain the authoritative repository artifacts referenced here.
