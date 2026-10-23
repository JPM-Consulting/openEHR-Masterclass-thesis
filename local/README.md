# Original openEHR Modeling Artifacts

## Purpose

The `local/` directory preserves the archetypes and template exports from the original Masterclass Thesis modeling work on the episode-oriented medical record. These artifacts document the study's initial information model and provide historical context for the subsequent comparative evaluation of the FOLDER, LINK, and CLUSTER implementation patterns.

They are **not the operational templates used in the technical proof of concept (PoC)**. The PoC templates were modeled separately for tests T0–T5 and are maintained under [`reproducibility/08-technical-proof-of-concept/02-templates/`](../reproducibility/08-technical-proof-of-concept/02-templates/README.md).

## Contents

The directory contains:

- **18 ADL archetypes**, including reused clinical models and four project-specific CLUSTER archetypes.
- **7 `.t.json` template exports** covering administrative and care encounters, episodes of care, SOAP documentation, and diagnosis and problem lists.
- [`PROVENANCE.md`](PROVENANCE.md), which documents the origin and governance status of the project-specific models and distinguishes them from reused artifacts.

The four project-specific CLUSTER archetypes are `episode_of_care_header.v0`, `eoc_relationships_entry.v0`, `eoc_relationships_care_encounter.v0`, and `eoc_relationships_episode_of_care.v0`. The three `eoc_relationships_*` archetypes represent the relationship structures explored in the CLUSTER-based design. Their presence here does not establish their integration into the original `.t.json` templates.

## Relationship to the Technical PoC

The technical PoC used **16 separately modeled Operational Templates (OPTs)**: two variants of each of eight template types. The FOLDER and LINK patterns share one variant, while the CLUSTER pattern uses a variant with additional archetyped relationship structures.

The PoC artifacts are available in two complementary formats:

- [`02-templates/opt/`](../reproducibility/08-technical-proof-of-concept/02-templates/opt/) contains the OPT files used to define the structures for PoC COMPOSITIONs.
- [`02-templates/zip/`](../reproducibility/08-technical-proof-of-concept/02-templates/zip/) contains Archetype Designer export packages with the corresponding templates and dependent archetypes and CLUSTERs.

See the [PoC template documentation](../reproducibility/08-technical-proof-of-concept/02-templates/README.md) for the variant definitions, artifact chain, and scope of technical use. The original `local/` exports should not be substituted for the PoC-specific artifacts when reproducing tests T0–T5.

## Provenance and Evidence Boundary

Authorship, licensing, and governance status differ across the supplied archetypes. Consult [`PROVENANCE.md`](PROVENANCE.md) and the metadata embedded in each artifact before reuse. The presence of an artifact in `local/` does not establish CKM publication, complete template integration, successful CDR persistence, or technical validation. Technical observations and their limitations are documented separately in the [PoC evidence package](../reproducibility/08-technical-proof-of-concept/README.md).
