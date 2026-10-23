# Normative Sources

## Purpose

This document identifies the normative openEHR specifications referenced by the architectural evidence matrix in this reproducibility package.

Each source identifier in `architectural-evidence-matrix.csv` maps to a named openEHR specification and, where available, a fixed release. These mappings establish an auditable specification baseline for the architectural evaluation.

Normative sources support architectural statements grounded directly in openEHR specifications. Conclusions drawn from comparing the three implementation patterns are classified separately as comparative architectural inference or design synthesis.

## Source identifier conventions

Source identifiers use the following abbreviations:

-   **NS**: Normative Source
-   **RM**: Reference Model
-   **EHR**: Electronic Health Record
-   **COMMON**: Common Information Model
-   **DATATYPES**: Data Types Information Model
-   **BASE**: openEHR Base Model
-   **ARCH**: Architecture Overview
-   **AM**: Archetype Model
-   **AQL**: Archetype Query Language

For example, `NS-RM-EHR` denotes the normative source for the EHR Information Model within the openEHR Reference Model.

## Specification baseline

| Source ID | Expanded source | openEHR component | Specification | Release identifier |
| --- | --- | --- | --- | --- |
| `NS-RM-EHR` | Normative Source – Reference Model – EHR | RM | EHR Information Model | Release 1.1.0 |
| `NS-RM-COMMON` | Normative Source – Reference Model – Common | RM | Common Information Model | Release 1.1.0 |
| `NS-RM-DATATYPES` | Normative Source – Reference Model – Data Types | RM | Data Types Information Model | Release 1.1.0 |
| `NS-BASE-ARCH` | Normative Source – Base Model – Architecture | BASE | Architecture Overview | Release 1.2.0 |
| `NS-AM` | Normative Source – Archetype Model | AM | Archetype Technology Overview | Release 2.3.0 |
| `NS-AQL` | Normative Source – Archetype Query Language | QUERY | Archetype Query Language (AQL) | Release 1.1.0 |


## NS-RM-EHR: Reference Model, EHR Information Model

**Source identifier:** `NS-RM-EHR`\
**Component:** openEHR Reference Model (RM)\
**Release:** 1.1.0\
**Specification:** EHR Information Model

### Relevant scope

This specification supports statements about:

-   EHR-level organisation;
-   FOLDER hierarchies used to index COMPOSITIONs;
-   references from FOLDER structures to COMPOSITIONs;
-   multiple FOLDER references to the same target object;
-   logical patient-level organisation using FOLDER structures; and
-   the use of FOLDER structures for logical groupings such as episodes.

### Official specification

https://specifications.openehr.org/releases/RM/Release-1.1.0/ehr.html

## NS-RM-COMMON: Reference Model, Common Information Model

**Source identifier:** `NS-RM-COMMON`\
**Component:** openEHR Reference Model (RM)\
**Release:** 1.1.0\
**Specification:** Common Information Model

### Relevant scope

This specification supports statements about:

-   `LOCATABLE` and its `LINK` relationships;
-   the structure and semantics of `FOLDER` and `VERSIONED_FOLDER`;
-   `OBJECT_REF`-based FOLDER items;
-   versioning of FOLDER structures;
-   archetypable FOLDER structures and FOLDER metadata; and
-   generic openEHR versioning and change-control semantics relevant to the evaluated patterns.

### Official specification

https://specifications.openehr.org/releases/RM/Release-1.1.0/common.html

## NS-RM-DATATYPES: Reference Model, Data Types Information Model

**Source identifier:** `NS-RM-DATATYPES`\
**Component:** openEHR Reference Model (RM)\
**Release:** 1.1.0\
**Specification:** Data Types Information Model

### Relevant scope

This specification supports statements about:

-   `DV_EHR_URI` as an EHR reference datatype;
-   references to EHR content;
-   addressing of top-level EHR structures; and
-   addressing of nodes within a top-level structure using an openEHR path.

### Official specification

https://specifications.openehr.org/releases/RM/Release-1.1.0/data_types.html

## NS-BASE-ARCH: Base Model, Architecture Overview

**Source identifier:** `NS-BASE-ARCH`\
**Component:** openEHR Base Model (BASE)\
**Release:** 1.2.0\
**Specification:** Architecture Overview

### Relevant scope

This specification supports high-level architectural statements about:

-   separation between the Reference Model and domain content models;
-   multi-level modelling;
-   version-controlled structures;
-   paths and locators;
-   archetypes and templates; and
-   the general relationship between RM structures, archetypes, templates and queries.

### Official specification

https://specifications.openehr.org/releases/BASE/Release-1.2.0/architecture_overview.html

## NS-AM: Archetype Model, Archetype Technology Overview

**Source identifier:** `NS-AM`\
**Component:** openEHR Archetype Model (AM)\
**Release:** 2.3.0\
**Specification:** Archetype Technology Overview

### Relevant scope

This specification supports statements about:

-   formal archetype-based constraint definitions;
-   reusable archetyped structures;
-   archetype composition;
-   template composition;
-   narrowing and mandating constraints; and
-   archetypes and templates as computable semantic definitions.

### Official specification

https://specifications.openehr.org/releases/AM/Release-2.3.0/Overview.html

## NS-AQL: Archetype Query Language

**Source identifier:** `NS-AQL`\
**Component:** openEHR Query Language (QUERY)\
**Release:** 1.1.0\
**Status:** STABLE\
**Specification:** Archetype Query Language (AQL)

### Relevant scope

This specification supports statements about:

-   querying openEHR Reference Model structures;
-   archetype-based query predicates;
-   hierarchical containment using `CONTAINS`;
-   traversal of hierarchical RM/archetype structures; and
-   use of archetype paths in query expressions.

### Official specification

https://specifications.openehr.org/releases/QUERY/Release-1.1.0/AQL.html

## Evidence-use rule

A normative source identifier in the architectural evidence matrix indicates that the corresponding architectural statement is grounded in the cited openEHR specification, within the scope described above.

A normative source identifier does **not** imply that the openEHR specification endorses any episode-oriented implementation pattern examined in this study.

Pattern-specific conclusions, comparisons among the FOLDER-, LINK-, and CLUSTER-based approaches, and the proposed hybrid design remain study-specific architectural interpretations. They are classified as **comparative architectural inference** or **design synthesis**, as appropriate.

## Versioning and archival release

This registry documents the openEHR specification versions used as normative references in the architectural evaluation. The source identifiers and specification releases are intended to remain consistent with the architectural evidence matrix and the references cited in the manuscript.

The registry is maintained within the same version-controlled repository as the corresponding evaluation artifacts, allowing the normative reference baseline to be traced to a specific repository release.
