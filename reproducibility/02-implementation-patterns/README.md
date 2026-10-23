# Implementation Patterns

## Overview

This study examines three implementation patterns for representing relationships in an episode-oriented medical record using openEHR: **FOLDER**, **LINK**, and **CLUSTER**. All three use existing openEHR Reference Model constructs without extending the Reference Model.

The patterns differ primarily in **where relationships are represented**, **how they are navigated**, and **how their semantics are governed**. The patterns are not mutually exclusive and may be combined to address specific implementation requirements.

## Functional requirements

The table summarizes how each pattern can represent the core relationship requirements at the design level. It does not indicate that all mechanisms or clinical views were implemented or experimentally verified.

| Functional requirement | FOLDER | LINK | CLUSTER |
| --- | --- | --- | --- |
| Chronological assignment to Care Encounters | Supported | Supported | Supported |
| Longitudinal assignment to Episodes of Care | Supported | Supported | Supported |
| Multiple Episode-of-Care relationships (`1..*`) | Modeled through references | Modelled through multiple LINKs | Explicitly modeled through repeatable Episode references |
| `Primary` / `Associated` relationship roles | Additional relationship metadata | Project-specific LINK types or equivalent conventions | Explicit role attribute |
| No duplication of clinical content | Supported through references | Supported through references | Supported through references |

The episode-oriented model allows a clinical documentation unit to be associated with multiple Episodes of Care, with one **Primary** Episode and optional **Associated** Episodes. Technical ENTRY granularity does not always correspond to the clinical unit of documentation. For example, a complete SOAP progress note is treated as one clinical unit even when it contains multiple ENTRYs.

## Comparison of implementation patterns

| Dimension | FOLDER | LINK | CLUSTER |
| --- | --- | --- | --- |
| **Core principle** | Hierarchical organization and referencing | Explicit relationships between openEHR objects | Archetyped relationship information |
| **Main openEHR constructs** | `FOLDER`, `OBJECT_REF`, `FOLDER.details` | `LOCATABLE.links`, `LINK`, `DV_EHR_URI` | `CLUSTER`, `DV_EHR_URI` |
| **Relationship granularity** | COMPOSITION references, with finer-grained associations through additional metadata | COMPOSITION- and ENTRY-level relationships | Relationships embedded in relevant archetyped contexts, including ENTRYs |
| **Role representation** | Additional relationship metadata where required | Project-specific LINK types or equivalent conventions | Explicit `Role` attribute |
| **Semantic governance** | FOLDER structure and application-level rules | LINK conventions and application-level rules | Archetype and template constraints, supplemented by application rules |
| **Navigation and retrieval** | Hierarchical navigation and reference resolution | Relationship-oriented retrieval | Queries over archetyped relationship metadata and reference resolution |
| **Versioning of relationship data** | DIRECTORY versioning | Versioning of the containing versioned openEHR object | Versioning of the containing COMPOSITION |
| **Combination with other patterns** | Possible | Possible | Possible |

Within the evaluated design, CLUSTER provides stronger **in-template semantic governance**, FOLDER supports hierarchical organization, and LINK provides flexible relationship modeling. These observations describe architectural characteristics rather than an overall ranking of the patterns.

The direction of LINK relationships and the choice to persist one or both directions are implementation decisions. Bidirectional navigation does not necessarily require storing relationships in both directions. Where these roles are required, the distinction between `Primary` and `Associated` must remain interpretable regardless of relationship direction.

Archetype cardinalities do not necessarily enforce every clinical invariant. For example, a repeatable Episode reference (`1..*`) does not by itself ensure that exactly one Episode has the role `Primary`. Additional validation may be required.

## Pattern documentation

| Pattern | Documentation | Focus |
| --- | --- | --- |
| **FOLDER** | [FOLDER-based implementation pattern](folder/README.md) | Hierarchical organization of Care Encounters, Episodes of Care, and Clinical Sections |
| **LINK** | [LINK-based implementation pattern](link/README.md) | Explicit relationships using the openEHR `LINK` class |
| **CLUSTER** | [CLUSTER-based implementation pattern](cluster/README.md) | Archetyped relationship structures and semantic constraints |

The CLUSTER archetypes and templates are maintained in the repository's [`local/`](../../local/) directory, alongside `reproducibility/`.

## Scope and evidence

The pattern descriptions and illustrative artifacts support the **conceptual and architectural comparison**. A separate technical proof of concept (T0–T5) investigated selected persistence and retrieval mechanisms using EHRbase. It does not establish automatic `DV_EHR_URI` dereferencing, referential-integrity enforcement, production-scale performance, or complete reconstruction of every clinician-centered view.

See the [Technical Proof of Concept](../08-technical-proof-of-concept/README.md) for the executed scenarios, results, and limitations. The longitudinal synthetic evaluation dataset contains **121 Medical Record Entries**. The technical proof of concept uses a separate, smaller test dataset.

The proposed hybrid architecture is a design synthesis derived from the comparison, **not a fourth empirically evaluated implementation pattern**.
