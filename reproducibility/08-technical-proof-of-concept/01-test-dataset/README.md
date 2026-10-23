# Technical Proof-of-Concept Test Dataset

## Overview

This directory contains the synthetic clinical dataset used in the technical proof of concept (PoC) for the FOLDER, LINK, and CLUSTER implementation patterns.

The dataset is a deliberately reduced subset of the longitudinal synthetic patient medical record. It supports testing selected persistence and retrieval mechanisms, not reproducing the complete longitudinal history.

## Dataset

| Component | Count |
|---|---:|
| Care Encounters | 2 |
| Episodes of Care | 4 |
| Medical Record COMPOSITIONs | 9 |
| **Total COMPOSITIONs** | **15** |

The nine Medical Record COMPOSITIONs contain 19 technical clinical ENTRYs representing 13 clinical documentation units.

The clinical scenario and relationships are documented in:

- [PoC Scenario](../DOC-01-poc-scenario.md)
- [Clinical Relationships](../DOC-02-poc-clinical-relationships.md)

## Canonical JSON Examples

The `canonical-json/` directory contains two sets of clinical COMPOSITION examples:

| Directory | Purpose |
|---|---|
| `folder-link/` | Examples created using the FOLDER/LINK operational templates |
| `cluster/` | Examples created using the CLUSTER operational templates |

Both sets represent the same clinical test scenario. The JSON examples were created from the corresponding Operational Templates (OPTs) documented in [02-templates](../02-templates/README.md).

Both sets of canonical JSON examples intentionally exclude openEHR `LINK`s and relationship CLUSTERs, including the examples based on the CLUSTER templates. This relationship-neutral baseline allows the same clinical content to be used across all three implementation patterns. Pattern-specific relationships are introduced in the technical test payloads, not in these canonical examples.

## Creation of Canonical JSON Examples

The canonical JSON examples were prepared from example COMPOSITION structures generated using the Medblocks Postman Collection. The corresponding OPTs for both FOLDER/LINK and CLUSTER variants had previously been uploaded to the openEHR Clinical Data Repository (CDR) via HTTP POST.

The generated structures were then populated with clinical information derived from the synthetic patient medical record. This workflow provides a traceable connection to the PoC templates, but does not independently establish template conformance.

## Clinical Relationships

The clinical relationships are specified independently of the implementation patterns in [DOC-02](../DOC-02-poc-clinical-relationships.md).

In the defined clinical relationship model, each clinical documentation unit has one Primary Episode of Care and may have additional Associated Episodes of Care. Their technical representation differs among FOLDER, LINK, and CLUSTER. The relationship-neutral canonical JSON examples do not themselves encode these assignments.

A complete SOAP Progress Note is treated as one clinical documentation unit, even when the template represents it using multiple technical ENTRYs.

## Scope and Evidence

These JSON examples provide clinical input for the technical PoC. Their derivation from OPT-generated structures documents their preparation process but does not, by itself, demonstrate OPT conformance, successful persistence, retrieval, automatic reference resolution, or referential integrity.

Experimental procedures and observed results are documented separately in [DOC-03](../DOC-03-poc-plan.md) and [DOC-04](../DOC-04-poc-results.md).
