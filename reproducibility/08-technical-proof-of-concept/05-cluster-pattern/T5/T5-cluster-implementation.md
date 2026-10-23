# T5 — Implementation and Modeling

## Relationship Direction and Location

T5 represents relationships from clinical Medical Record ENTRYs to existing Care Encounter and Episode of Care COMPOSITIONs, reversing the context-to-clinical direction used in T4. Each clinical ENTRY carries `CLUSTER.eoc_relationships_entry.v0` in its `protocol` `ITEM_TREE`. The Contact reference (`at0001/at0009`) stores a versioned Care Encounter `DV_EHR_URI`. Episode references (`at0109/at0147`) store versioned Episode of Care `DV_EHR_URI` values with an associated episode role (`at0153`). The role codes are `at0154` for Primary and `at0155` for Associated. The clinical ENTRYs include OBSERVATION and INSTRUCTION archetypes.

A SOAP progress note is one clinical documentation unit represented technically by four `OBSERVATION.progress_note.v1` ENTRYs within a SOAP SECTION hierarchy. In the tested records, all four ENTRYs of each SOAP note carry the same Care Encounter and Episode of Care associations. This observed consistency does not establish automatic enforcement across ENTRYs.

## Tested Clinical Structures

- MR1/MR7: Blood pressure and pulse, with hypertension (EP3) associated with blood pressure.
- MR2: Height, weight, and BMI, each additionally associated with obesity (EP4).
- MR3: Urinalysis, with existing `protocol` method data retained alongside the relationship CLUSTER.
- MR4/MR8: SOAP progress notes, each represented by four ENTRYs. Queries must account for the nested SECTION hierarchy to avoid duplicate results for individual SOAP components.
- MR5/MR9: Medication orders (`INSTRUCTION.medication_order.v3`) with relationship CLUSTERs in `protocol`.
- MR6: Microbiology result, with its clinical microbiology CLUSTER retained.

## Relationship Optionality and Production Governance

In this PoC, the relationship CLUSTER archetypes and templates permit initial persistence of clinical information without references to existing Care Encounter or Episode of Care COMPOSITIONs. This optionality supports the comparative investigation of object creation sequences, including the Medical Record-first sequence in T4. T5 instead uses existing context COMPOSITIONs as relationship targets when clinical ENTRYs are persisted.

In a production environment involving multiple vendors, required contextual associations may warrant stricter constraints. Archetype and template validation can enforce the presence and structure of modeled relationships where the relevant constraints are defined. Confirming that referenced target objects exist, and that the references remain valid, requires additional mechanisms beyond structural validation. Such mechanisms were not demonstrated by these tests.

The optionality in this PoC is an experimental design choice, not a recommended production configuration.

## Evidence Boundaries

AQL retrieves stored URI values but does not demonstrate automatic URI dereferencing. An independent GET of EP2 confirms the existence of that particular target, not the validity of all stored references. The documented RI-02, RI-03, and RI-04 tests show that a dangling URI could be persisted and queried in the tested EHRbase 2.30.1 environment. This observation is configuration-specific and does not establish behavior across openEHR implementations. Server-side enforcement of relationship cardinality and consistency across SOAP ENTRYs was not independently demonstrated. The documented queries support selective retrieval and application-side assembly of clinical information, not an implemented end-to-end clinical-view service. Production UI rendering and multi-vendor interoperability were not tested.
