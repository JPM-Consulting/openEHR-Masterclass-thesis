# FOLDER-Based Pattern — Technical PoC Artifacts

This directory contains the evaluated Basic FOLDER pattern (official scenario T1) and a separate exploratory extension that uses CLUSTER metadata to qualify relationship roles. Historical internal labels such as `T1 Extended FOLDER` and `T2 Basic FOLDER` in source artifacts do not correspond to the official scenario numbering in [DOC-03](../DOC-03-poc-plan.md). Official scenario T2 evaluates the LINK pattern.

## Contents

- `T0/`: Preliminary FOLDER feasibility experiment, separate from the systematically evaluated T1 scenario. See [`T0/README.md`](T0/README.md).
- `T1/`: DIRECTORY JSON requests and persisted JSON exports for the evaluated Basic FOLDER implementation. Relationships use `FOLDER.items` for clinical COMPOSITION references and `FOLDER.details` with `DV_EHR_URI` for references to context COMPOSITIONs and clinical ENTRY or SOAP SECTION content. The evaluated implementation does not encode `Primary` or `Associated` relationship roles. See [`T1/README.md`](T1/README.md).
- `exploratory-extension/`: Separate technical exploration of relationship CLUSTER metadata with `Primary` and `Associated` roles. This extension is not a fourth evaluated pattern and is excluded from the principal FOLDER comparison. See [`exploratory-extension/README.md`](exploratory-extension/README.md).

**Provenance limitation:** The available artifacts document the PoC execution and its results. However, historical byte-for-byte equivalence with the original execution artifacts has not been independently verified.

## Scientific Scope and Evidence

The original FOLDER diagram also depicts a Clinical Sections FOLDER dimension. A separate Clinical Sections FOLDER hierarchy was not implemented in T1 (R03 is out of scope). SOAP `SECTION` content within a clinical COMPOSITION was inspected, but this does not constitute implementation of the Clinical Sections FOLDER dimension. EHRbase persistence and retrieval of `DV_EHR_URI` values do not demonstrate native URI dereferencing or referential-integrity enforcement. Targeted AQL queries retrieved selected clinical content. Complete reconstruction of all clinician-centered views was not demonstrated.

The test plan and results are documented in [DOC-03](../DOC-03-poc-plan.md) and [DOC-04](../DOC-04-poc-results.md). The T0 and exploratory-extension directories contain request payloads rather than independently archived HTTP response captures. T1 also includes exported persisted JSON files. Documented HTTP and AQL outcomes must not be inferred from request filenames alone.
