# Licensing and Third-Party Materials

This repository contains original research documentation, historical publication materials, openEHR clinical models, and technical proof-of-concept (PoC) artifacts. These materials do not necessarily share the same copyright ownership or license. The license applicable to a particular file must be determined from its provenance and any file-specific notices.

## Original Repository Documentation

Unless a file states otherwise, original documentation authored by Jean-Pierre Messerli for this repository is offered under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license. This designation applies only to material for which the author holds the necessary rights. It does not extend to third-party content incorporated into a document or to artifacts subject to separate license terms.

Copyright © Jean-Pierre Messerli, for original material to which this notice applies.

License text: https://creativecommons.org/licenses/by/4.0/

## openEHR Archetypes and Model Artifacts

The `local/` directory includes project-specific archetypes and reused or adapted openEHR models. The supplied ADL files contain different license declarations, including **CC BY-SA 3.0** and **CC BY-SA 4.0**. Some draft archetypes have no explicit license declaration in their embedded metadata. The absence of a license field must not be interpreted as permission to relicense or freely redistribute an artifact.

The following `local/` files have no explicit license declaration in the supplied ADL metadata:

- `openEHR-EHR-CLUSTER.composition_context_detail.v1.adl`
- `openEHR-EHR-EVALUATION.health_issue_contsys.v1.adl`
- `openEHR-EHR-EVALUATION.health_thread_contsys.v1.adl`

All third-party rights, attribution requirements, and applicable ShareAlike obligations remain in force. A project-specific archetype may have its own declared license, and the project-specific authorship of an archetype does not supersede obligations arising from any incorporated or adapted third-party material. See [`local/PROVENANCE.md`](local/PROVENANCE.md) for provenance information.

## Technical Proof-of-Concept Templates and Archives

The technical PoC uses separately modeled template variants stored in [`reproducibility/08-technical-proof-of-concept/02-templates/`](reproducibility/08-technical-proof-of-concept/02-templates/). This directory includes operational templates (`.opt`) and ZIP packages containing associated modeling artifacts. These files are distinct from the earlier modeling materials under `local/`.

The repository's CC BY 4.0 notice does **not** automatically apply to an `.opt` file, a template export, or the contents of a ZIP archive. Included or derived archetypes may carry their own licenses and attribution requirements. A package must be assessed at the level of its constituent artifacts before it is described as licensed under a single set of terms.

## Historical Publications and Conference Materials

Publications, posters, slides, and other historical materials retain their applicable author, publisher, and third-party rights. Inclusion in this repository does not alter their existing terms. In particular, the licensing of an article published by Frontiers is determined by the publisher's applicable publication agreement and article license, rather than by this repository notice.

Frontiers ordinarily publishes research articles under **CC BY 4.0**. This does not require the repository's clinical model artifacts to be relicensed under CC BY 4.0.

## Attribution and Embedded Rights

When redistributing or adapting models, preserve applicable authorship, contributor, copyright, license, custodian, namespace, provenance, and modification notices. Embedded terminology or other third-party content may require additional permissions. A license notice for a surrounding document or archive does not override those rights.

## Scope and Outstanding Verification

This notice distinguishes intended licensing of original repository documentation from the rights governing individual research artifacts. It does not establish that every file has been cleared for redistribution or that all embedded licenses are mutually compatible. In particular, source rights and license declarations for artifacts without explicit metadata, and the contents of the PoC ZIP packages, require file-level verification before an unqualified repository-wide licensing statement can be made.

For license interpretation, consult the applicable license legal code and the rights holder where necessary. This document is a rights and attribution statement, not a legal opinion.
