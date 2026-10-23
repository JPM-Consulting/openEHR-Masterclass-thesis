# openEHR Templates and Modeling Artifacts

## Overview

This directory contains the openEHR modeling artifacts used in the technical proof of concept (PoC) for the FOLDER, LINK, and CLUSTER implementation patterns.

The PoC templates were modeled separately from the original Masterclass Thesis artifacts preserved in the repository's `local/` directory. The `local/` artifacts are not the authoritative templates for the technical PoC.

## Modeling Environment

| Component | Specification |
|---|---|
| Modeling tool | Archetype Designer (browser-based) |
| Version observed during documentation | 1.25.16 |
| Archetype Definition Language | ADL 1.4 |

The browser-based application may be updated over time. Version 1.25.16 was observed during documentation. The exact version used for each original export has not been established.

## Template Variants

Two variants were modeled for each of eight template types:

| Variant | Purpose |
|---|---|
| FOLDER/LINK | Shared clinical templates without the additional relationship CLUSTERs |
| CLUSTER | Separate templates supporting archetyped relationship information |

The absence of relationship CLUSTERs from FOLDER/LINK templates is intentional.

The CLUSTER variant uses these relationship archetypes:

- `CLUSTER.eoc_relationships_entry.v0`
- `CLUSTER.eoc_relationships_care_encounter.v0`
- `CLUSTER.eoc_relationships_episode_of_care.v0`

## Artifacts

| Directory | Contents |
|---|---|
| `opt/` | Operational Templates defining the structures used for the PoC COMPOSITIONs |
| `zip/` | Archetype Designer export packages containing the corresponding template and dependent modeling artifacts |

The export packages include the template definition, relevant archetypes and CLUSTERs, and the OPT. They are intended to support reimport into Archetype Designer and further modeling. Successful reimport into the current application version has not been independently demonstrated.

## Relationship to the Test Dataset

The Operational Templates were uploaded to the openEHR CDR via HTTP POST and used to generate example COMPOSITIONs through the Medblocks Postman Collection. These examples provided the structural basis for the canonical JSON test dataset, which was populated with clinical information from the synthetic patient medical record.

Separate OPTs were used for the FOLDER/LINK and CLUSTER variants. The canonical JSON examples derived from both variants intentionally exclude openEHR `LINK`s and relationship CLUSTERs. The CLUSTER templates nevertheless support the addition of archetyped relationships in the corresponding technical tests.

The clinical JSON examples are documented in the [test dataset README](../01-test-dataset/README.md).

The artifact chain is:

1. Archetypes and CLUSTERs define reusable clinical structures.
2. Templates assemble and constrain those structures.
3. OPTs provide their operational representation.
4. Canonical JSON examples provide clinical data based on the corresponding OPTs.

Persistence and retrieval are evaluated separately in the technical PoC scenarios. Creating an example from an OPT does not by itself demonstrate conformance or successful persistence.

## Provenance

The `zip/` and `opt/` artifacts document the modeling state used for the technical PoC. The separate `local/` directory at the repository root retains the original, broader Masterclass Thesis modeling artifacts. Those historical artifacts are outside the scope of this editorial review.
