# Exploratory FOLDER Extension: Role-Qualified Relationships

## Purpose and classification

This directory documents an exploratory extension of the FOLDER-based representation using relationship metadata to distinguish `Primary` and `Associated` episode-of-care relationships. It is not the official T1 Basic FOLDER scenario or a fourth implementation pattern. Its evidence is not included in the T1 results. The separate preliminary feasibility test is documented in [`T0/`](../T0/), and the evaluated Basic FOLDER scenario is documented in [`T1/`](../T1/).

## Archived artifacts

- [`relationship-manifest-27.json`](relationship-manifest-27.json): Relationship manifest describing the proposed 27-relationship dataset and its recorded source status.
- [`tests/directory-27-relationships.json`](tests/directory-27-relationships.json): Candidate DIRECTORY request payload.
- `tests/diagnostics/`: Eleven diagnostic JSON payload variants for incremental or alternative DIRECTORY construction, including steps labeled STEP2–STEP7 and baseline and negative variants.

The manifest records the EHR identifier `25bf624b-c4ee-43e7-b695-a8d69c37f7f1`. Source filenames retain historical `T1.3` labels. These labels do not establish that the official T1 Basic FOLDER scenario used the extended dataset.

## Evidence status and limitations

The manifest records the status `READY FOR T1.3 POST TRIAL; EHRbase validation and URI dereferencing not yet tested`. This is an archived source statement, not an independently verified account of subsequent execution. The presence of POST/PUT request payloads or diagnostic variants does not establish that the requests were executed, accepted, persisted, or independently retrieved.

This directory contains no independent HTTP response captures or persisted DIRECTORY GET exports demonstrating successful execution of the complete 27-relationship extension. Claims about individual diagnostic attempts require separately documented results. These artifacts do not establish native `DV_EHR_URI` dereferencing, target existence, referential-integrity enforcement, or clinical-view reconstruction.

## Relation to the comparative evaluation

The official T1 evaluation uses the Basic FOLDER representation without `Primary`/`Associated` role qualifiers. This extension is retained as supplementary exploratory material and remains separate from T0 and T1 in the methods, results, and architectural comparison. See the [FOLDER pattern overview](../README.md) and [DOC-04 PoC results](../../DOC-04-poc-results.md) for the documented test scope and results.
