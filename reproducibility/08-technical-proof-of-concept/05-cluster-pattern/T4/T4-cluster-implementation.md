# T4 — CLUSTER Implementation and Design

## Research scenario

T4 evaluates the Medical Record-first creation order for the CLUSTER pattern. Clinical Medical Record (MR) COMPOSITIONs are persisted first, without relationship CLUSTERs. Care Encounter (CE) COMPOSITIONs subsequently store references to MR COMPOSITIONs (R10), while Episode of Care (EP) COMPOSITIONs store references to clinical ENTRYs (R14). The inverse MR-to-CE and MR-to-EP directions (R12 and R13) are evaluated in T5, not T4.

## Execution sequence

1. Create isolated EHR `3c269710-a677-4fe8-9083-1133e8899db9`.
2. POST MR1–MR9, all at version `::1`, without relationship CLUSTERs. Independently GET each COMPOSITION.
3. POST CE1 with five MR COMPOSITION references. GET CE1 `::1`.
4. POST CE2 without references. GET CE2 `::1`.
5. PUT CE2 with four MR references. GET CE2 `::2` and historical version `::1`.
6. POST EP1–EP4 with 7, 12, 2, and 3 clinical ENTRY references, respectively. GET each COMPOSITION.
7. Verify the documented counts of 15 COMPOSITIONs, 9 CE-to-MR references, and 24 EP-to-clinical-ENTRY references. Perform the documented AQL retrievals supporting application-side clinical-view assembly.

## Relationship representation

- CE: `CLUSTER.eoc_relationships_care_encounter.v0`, `ELEMENT[at0147]` labeled Link. `DV_EHR_URI` values reference versioned MR COMPOSITIONs.
- EP: `CLUSTER.eoc_relationships_episode_of_care.v0`, `ELEMENT[at0147]` labeled Primary (`at0163`) or Associated (`at0164`). `DV_EHR_URI` values reference versioned MR COMPOSITIONs and clinical ENTRY paths.
- SOAP notes: Four `OBSERVATION.progress_note.v1` ENTRYs are nested under one `SECTION.soap.v0`, with four leaf sections (S/O/A/P). Each SOAP note is one clinical unit, and all four ENTRYs share the same EP2 role in this dataset. The four technical references do not represent four independent SOAP notes.
- URI encoding: Square brackets in ENTRY paths must be percent-encoded (`%5B`, `%5D`) for accepted `DV_EHR_URI` values in the tested EHRbase configuration. An initial EP1 request with unencoded brackets returned HTTP 400. The corrected request returned HTTP 201.

## Relationship optionality and production governance

For this proof of concept, the relationship CLUSTER archetypes and corresponding templates deliberately permit initial persistence of clinical information without references to existing Care Encounter or Episode of Care COMPOSITIONs. This choice enables evaluation of different object-creation sequences, including the Medical Record-first scenario (T4).

In a multi-vendor production environment, stronger relationship constraints may be appropriate to reduce the risk of clinical entries lacking required contextual associations. Archetype and template validation can constrain the presence and structure of relationship data. Validation of referenced target existence and referential integrity requires additional mechanisms. These production requirements were not validated by T4.

The optionality in this PoC is an experimental design choice, not a recommended production configuration.

## Interpretation limits

The documented tests support persistence and targeted retrieval of relationship references through REST and AQL within the tested environment. They do not establish native `DV_EHR_URI` dereferencing, referential integrity enforcement, automatic end-to-end reconstruction of clinician-facing views, server-side primary-role uniqueness, or cross-vendor interoperability. In T4, CE and EP COMPOSITIONs carry the relationship data. The clinical MR COMPOSITIONs were not modified to add inverse relationships.
