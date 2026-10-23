# Provenance of local openEHR modeling artifacts

The `local/` directory preserves modeling artifacts from the original Masterclass work. It includes project-specific archetypes and reused openEHR archetypes and templates. Inclusion in the repository does not imply common authorship, governance, or publication status.

## Project-specific archetypes

Jean-Pierre Messerli, JPM Consulting GmbH, created four CLUSTER archetypes for this research project:

- `openEHR-EHR-CLUSTER.episode_of_care_header.v0.adl`
- `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl`
- `openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl`
- `openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl`

The three `eoc_relationships_*` archetypes define relationship structures for the CLUSTER-based implementation pattern. The `episode_of_care_header.v0` archetype represents Episode-of-Care information.

Their ADL metadata identify Jean-Pierre Messerli and JPM Consulting GmbH as the authoring source, `JPM Consulting GmbH` as the original publisher and custodian organization, and `ch.jpm-consulting` as the original and custodial namespace. Their lifecycle state is `unmanaged`.

These are project-specific research artifacts, not published or governed openEHR Clinical Knowledge Manager (CKM) archetypes. Their `openEHR-EHR-CLUSTER...` identifiers follow openEHR naming conventions but do not establish CKM publication, openEHR Foundation governance, or endorsement.

## Reused modeling artifacts

Other archetypes and templates in `local/` were reused or adapted as supporting resources. Their authorship, copyright, licensing, namespace, and governance status remain subject to the metadata and terms of the respective source artifacts. Including local copies does not transfer authorship or imply project ownership of third-party artifacts.

## Relationship to the technical proof of concept

The files in `local/` document the original modeling work. The technical proof of concept (T0–T5) used separately modeled template variants and their associated archetype packages, documented in [`reproducibility/08-technical-proof-of-concept/02-templates/`](../reproducibility/08-technical-proof-of-concept/02-templates/). The original files in `local/` should not be treated as the definitive operational templates used in those tests.

## Evidence boundary

The project-specific archetypes document the intended relationship structures and support the design-level evaluation. Their presence does not demonstrate CKM acceptance, complete template integration, production deployment, multi-vendor interoperability, runtime performance, or openEHR Foundation endorsement. Technical PoC observations and their limitations are documented separately under `reproducibility/08-technical-proof-of-concept/`.
