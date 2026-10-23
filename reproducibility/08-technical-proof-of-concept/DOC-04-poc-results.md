# Technical Proof-of-Concept Results

**Status:** Baseline COMPOSITION validation COMPLETED (30/30 PASS). Preliminary FOLDER feasibility test T0 COMPLETED (PASS). T1 FOLDER core relationship operations COMPLETED (PASS), full clinical-view reconstruction PARTIALLY VERIFIED. T2 LINK relationship persistence, retrieval, and manual EP2 clinical-view reconstruction COMPLETED (PASS within tested scope). T3 COMPLETED (PASS within tested scope). T4 CLUSTER COMPLETED (PASS within tested scope). T5 CLUSTER COMPLETED (PASS within tested scope), including negative referential-integrity tests. Additional semantic FOLDER/CLUSTER exploration recorded separately.

The five implementation scenarios are defined in [PoC Plan](DOC-03-poc-plan.md). This results document uses the same scenario numbering: `T1` = FOLDER, `T2–T3` = LINK, `T4–T5` = CLUSTER. The historical execution-session labels “T1 Extended FOLDER” and “T2 Basic FOLDER” do not denote the scenarios used here. The Basic FOLDER execution is reported under scenario T1. The Extended FOLDER implementation is documented as a separate exploratory investigation. Clinical Section FOLDER organization was not implemented in T1. Administrative Encounter relationships (R11) and Episode-to-Episode relationships (R15) were not tested. Plan alignment: DOC-03 explicitly lists R03 (Clinical Section FOLDER → ENTRY) as OUT OF SCOPE, consistent with this results document. Figure 3 depicts this dimension conceptually, but no R03 implementation is claimed in T1. The results are reported here, with available HTTP evidence and payloads retained in the pattern directories. Status categories are PASS, FAIL, PARTIALLY VERIFIED, BLOCKED, and NOT EXECUTED.

## Baseline COMPOSITION Validation

**Status: COMPLETED — 30/30 PASS (POST, GET, and clinical content verification).** This baseline validation is separate from scenarios T1–T5, which are reported below.

**Scope and environment.** Fifteen synthetic COMPOSITIONs (two Care Encounters, four Episodes of Care, and nine Medical Records) were tested in two template variants: FOLDER/LINK and CLUSTER. All were persisted to and retrieved from EHRbase 2.30.1 using the openEHR REST API and canonical JSON. The validation EHR was `dad938aa-02ff-4e55-8f36-3f7aabeabf76`. The baseline EHR and COMPOSITION identifiers are not evidence for the isolated T1–T5 scenarios.

### Validation results

| COMPOSITION | Variant | POST | GET | Clinical data verified | Result | COMPOSITION UUID |
| --- | --- | --- | --- | --- | --- | --- |
| CE1 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `5ef81f23-d31a-46ff-8c3e-08ab7f3715d3` |
| CE1 | CLUSTER | PASS | PASS | PASS | **PASS** | `d0d9f79f-0a4b-43ed-a386-0b6f8c51eaff` |
| CE2 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `c93dc6ca-e201-4142-81b9-b31b72bb19cb` |
| CE2 | CLUSTER | PASS | PASS | PASS | **PASS** | `67c24d86-691a-4194-8b36-3afd5a8d8dda` |
| EP1 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `c8131bf8-c9dc-4602-880b-951643080c7d` |
| EP1 | CLUSTER | PASS | PASS | PASS | **PASS** | `b8f7abcb-967c-432d-974f-547209e94b33` |
| EP2 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `33311c9d-7e1b-4930-8f0c-00585ad4a0ff` |
| EP2 | CLUSTER | PASS | PASS | PASS | **PASS** | `ca0c943f-9507-4e9a-9b94-78284a81ea23` |
| EP3 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `2dd610ff-043a-4cd6-8e97-b29397cd29c9` |
| EP3 | CLUSTER | PASS | PASS | PASS | **PASS** | `2b523818-7b37-4570-a6c7-8b55bd457faf` |
| EP4 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `7685e3eb-808a-46b3-9ed1-5e0390d5e858` |
| EP4 | CLUSTER | PASS | PASS | PASS | **PASS** | `cd1ecc22-efc2-40b3-8782-c5dae19a4016` |
| MR1 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `cc518ee1-7b89-446e-948b-b4774b485eb3` |
| MR1 | CLUSTER | PASS | PASS | PASS | **PASS** | `644bbe17-dc26-413e-a365-73912dc06886` |
| MR2 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `75e4802b-5ae5-461a-b469-96e7ffffbff5` |
| MR2 | CLUSTER | PASS | PASS | PASS | **PASS** | `097f52dc-b827-4e62-8dd6-03cf7523e85e` |
| MR3 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `163701a6-03c4-47f9-a710-fabbeeefa7d1` |
| MR3 | CLUSTER | PASS | PASS | PASS | **PASS** | `ee80670f-7dc0-4dd2-adbc-b4c760146dbb` |
| MR4 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `f9a437e2-a2a1-4acd-a54e-3724a7d909e3` |
| MR4 | CLUSTER | PASS | PASS | PASS | **PASS** | `4374b63c-8c6e-4ba3-9ecd-f4e7f73caca5` |
| MR5 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `c4da3f28-bba5-4a0b-a12b-c419b7250ae5` |
| MR5 | CLUSTER | PASS | PASS | PASS | **PASS** | `9fb7bda1-1344-496e-acb9-44cd9d22da70` |
| MR6 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `9c77a016-8896-4fb4-a141-ab8e6e98d1f6` |
| MR6 | CLUSTER | PASS | PASS | PASS | **PASS** | `3972a1cf-bf9f-4c4b-a923-c6229950ec6d` |
| MR7 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `b5027bd9-c7cf-442f-875a-6f1b0a0b6c52` |
| MR7 | CLUSTER | PASS | PASS | PASS | **PASS** | `821ab743-34df-471a-bfc8-44c6e9e731d5` |
| MR8 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `b632952f-31d4-48d9-b4a6-fc193a8a0a90` |
| MR8 | CLUSTER | PASS | PASS | PASS | **PASS** | `0cb3d446-9d1c-409f-87a9-7e4e3cee4c5d` |
| MR9 | FOLDER/LINK | PASS | PASS | PASS | **PASS** | `16e02c3d-bc6c-4920-a25c-6d7e715479be` |
| MR9 | CLUSTER | PASS | PASS | PASS | **PASS** | `947f85ca-f42b-488e-a591-b7f0eacb194f` |

**Totals:** 30/30 POST PASS, 30/30 GET PASS, and 30/30 clinical data verified. **Overall: 30/30 PASS.** All returned versioned identifiers follow `<COMPOSITION UUID>::local.ehrbase.org::1`.

### Validation observations

The following observations describe the retrieved baseline content and structure. The term *CLUSTER variant* denotes the designated template, **not** an instantiated episode-of-care relationship CLUSTER, relationship instances were intentionally omitted from all baseline COMPOSITIONs.

- **CE1 / CE2 — Care Encounters:** Both encounters were persisted and retrieved in both variants. Their event context and synthetic encounter chronology were preserved: CE1 on November 15, 2024, and CE2 on November 17, 2024. No episode-of-care relationship structures were instantiated.
- **EP1 — General health problem (Default Episode of Care):** The Episode-of-Care COMPOSITION was persisted and retrieved in both variants, preserving the general active acute problem context. Its default-assignment function is defined in DOC-02 but was not tested in this relationship-free baseline.
- **EP2 — Urinary tract infection:** The Episode-of-Care COMPOSITION was persisted and retrieved in both variants, preserving the active acute diagnosis context.
- **EP3 — Arterial hypertension:** The Episode-of-Care COMPOSITION was persisted and retrieved in both variants, including the chronic diagnosis and recognition year 2009.
- **EP4 — Obesity WHO grade I:** The Episode-of-Care COMPOSITION was persisted and retrieved in both variants, preserving the active chronic diagnosis context.
- **MR1 — Vital Signs (CE1):** Both variants preserved blood pressure 140/90 mm[Hg] and pulse 75/min.
- **MR2 — Body Measurements (CE1):** Both variants preserved height 168 cm, weight 86 kg, and BMI 30.5 kg/m².
- **MR3 — Urinalysis (CE1):** Both variants preserved the five reported ordinal results: leukocytes 3+, nitrite positive, blood 1+, protein trace, and pH 6.0.
- **MR4 — SOAP Progress Note (CE1):** Both variants preserved the complete Subjective, Objective, Assessment, and Plan text. The SOAP note is one clinical unit represented technically by four `OBSERVATION.progress_note.v1` ENTRYs within one `SECTION.soap.v0` and one COMPOSITION. Episode assignment of the entire note remains to be tested.
- **MR5 — Medication Order (CE1):** Both variants preserved the trimethoprim–sulfamethoxazole order (TMP 160 mg / SMX 800 mg), oral route, `PO 2x1` directions, and `R/2024-11-15T09:00:00+01:00/PT12H` timing. No treatment duration was specified.
- **MR6 — Microbiology Result (CE2):** Both variants preserved the urine culture identifying *Escherichia coli* (≥10⁵ CFU/mL reported within the test name), with resistance to trimethoprim–sulfamethoxazole and ciprofloxacin and susceptibility to amoxicillin–clavulanate, nitrofurantoin, and fosfomycin. **Unresolved:** the local coded value `at0015` used for “Resistant (R)” requires independent verification against the applicable archetype. Successful retrieval alone does not establish terminology correctness. The clinical microbiology culture CLUSTER is distinct from an episode-of-care relationship CLUSTER.
- **MR7 — Vital Signs (CE2):** Both variants preserved blood pressure 142/85 mm[Hg] and pulse 72/min at `2024-11-17T09:00:00+01:00`.
- **MR8 — SOAP Progress Note (CE2):** Both variants preserved the four texts verbatim: Subjective “Still experiencing urinary symptoms”. Objective “Urine culture: Escherichia coli resistant to current antibiotic”. Assessment “Acute bacterial cystitis”. Plan “Switch antimicrobial therapy”. The four `OBSERVATION.progress_note.v1` ENTRYs remained grouped within one SOAP COMPOSITION, with consistent timestamps. Episode-of-care assignment remains untested.
- **MR9 — Medication Order (CE2):** Both variants preserved “Amoxicillin 500 mg / Clavulanate 125 mg film-coated tablet”, oral route, `PO 3x1` directions and narrative, and `R/2024-11-17T09:00:00+01:00/PT8H` timing. The eight-hour interval is an explicit modeling assumption for three-times-daily dosing, no treatment duration was specified. Successful persistence does not establish clinical appropriateness or execution of the dosing schedule.

### Baseline validation conclusion and limitations

All 30 baseline COMPOSITIONs were successfully persisted and retrieved, and their expected clinical data were verified. The FOLDER/LINK and CLUSTER template variants preserved equivalent clinical content, providing a controlled starting point for the subsequent pattern evaluation. The tests establish **baseline persistence and retrieval only**. They do not demonstrate FOLDER, LINK, or archetyped CLUSTER relationship behavior, clinical view reconstruction, or satisfaction of the eight functional requirements and six architectural criteria. The local MR6 resistance code requires independent semantic verification. The implementation scenarios use isolated EHRs and record results below.

---

## Preliminary FOLDER Feasibility Test — T0

**Status: COMPLETED — PASS (T0.1–T0.3).** T0 is an isolated preliminary feasibility test of the FOLDER-based relationship representation. It is **not** the full T1 implementation scenario. It does not change the status of T1–T5.

**Environment and scope.** EHRbase 2.30.1, openEHR REST API, canonical JSON. Test EHR: `d95b9e3d-758b-4e8d-9b88-757290c2653f`. The DIRECTORY includes one Care Encounter FOLDER (CE1), four Episode-of-Care FOLDERs (EP1–EP4), and references to six existing COMPOSITIONs (CE1, EP1–EP4, MR1). Three ENTRY-level Episode-of-Care relationships were tested. The CE1-to-MR1 relationship was represented separately through `FOLDER.items`. This EHR is distinct from the isolated T1 EHR.

### Execution results

| Test | Activity | Actual result | Status |
| --- | --- | --- | --- |
| T0.1 | Create and retrieve DIRECTORY hierarchy | POST and independent GET returned the root `Directory`, `Contacts/CE1`, and `Episodes/EP1–EP4` FOLDER hierarchy with preserved FOLDER identifiers. Initial DIRECTORY version `::1`. | **PASS** |
| T0.2 | Persist and retrieve COMPOSITION references | PUT and independent GET preserved CE1 → MR1 via `FOLDER.items` (`OBJECT_REF`), CE1 → CE1 COMPOSITION via `FOLDER.details` (`DV_EHR_URI`), and EP1–EP4 → respective Episode COMPOSITIONs via `FOLDER.details`. DIRECTORY version `::2`. | **PASS** |
| T0.3 | Persist and retrieve ENTRY-level Episode relationships | PUT and independent GET preserved three relationship `CLUSTER`s with ENTRY `DV_EHR_URI` references and locally coded `Primary`/`Associated` roles. DIRECTORY version `::3`. | **PASS** |

### Verified clinical relationships

| Relationship | Representation | Result |
| --- | --- | --- |
| CR-001 | CE1 FOLDER `items` → MR1 versioned COMPOSITION (`49d6b0a1-9ef2-48b8-91d8-e4abfadc172e`) | **PASS** |
| CR-010 | MR1 Blood Pressure ENTRY → EP1, `Primary` | **PASS** |
| CR-011 | MR1 Blood Pressure ENTRY → EP3, `Associated` | **PASS** |
| CR-012 | MR1 Pulse ENTRY → EP1, `Primary` | **PASS** |

**Final DIRECTORY version:** `9b073e8e-31c5-4558-833f-3ca23c5aa5df::local.ehrbase.org::3` (confirmed by independent GET).

### Technical observations

- `FOLDER.folders` preserved the Contact/Episode hierarchy. `FOLDER.items` accepted an `OBJECT_REF` with `type: VERSIONED_COMPOSITION` and `namespace: local`. `FOLDER.details` accepted `ITEM_TREE` metadata containing `ELEMENT` references to COMPOSITIONs and repeatable `CLUSTER` structures for ENTRY relationships.
- Each relationship `CLUSTER` paired an ENTRY reference (`DV_EHR_URI`) with a relationship role (`DV_CODED_TEXT`, local codes `primary` or `associated`). The same Blood Pressure ENTRY was referenced from EP1 as `Primary` and EP3 as `Associated`, without copying the clinical ENTRY into the DIRECTORY.
- An initial T0.3 PUT returned HTTP 400 during URI deserialization because unescaped square brackets in the ENTRY path were rejected by Java `URI`. Encoding `[` as `%5B` and `]` as `%5D` resolved this syntax error. The corrected PUT and subsequent GET succeeded.
- An earlier T0.2 HTTP 400 (`Invalid UUID string: `) was traced to an unset Postman environment variable (`VersionCompositionId`), not to the relationship representation. The unchanged payload succeeded once the variable was configured.
- DIRECTORY versions progressed from `::1` (T0.1) through `::2` (T0.2) to `::3` (T0.3), with the existing hierarchy and FOLDER identifiers retained.

### Conclusion and limitations

**T0 Overall: PASS.** In EHRbase 2.30.1, the proposed FOLDER-based representation of COMPOSITION and ENTRY-level Episode-of-Care relationships was successfully **persisted and retrieved** using existing openEHR Reference Model structures, without an RM extension. The test demonstrated storage of distinct `Primary` and `Associated` assignments to the same clinical ENTRY without duplicating its clinical content.

**Limits of evidence:** Successful persistence and retrieval of `DV_EHR_URI` strings do **not** establish automatic dereferencing, path resolution, referential integrity enforcement, or semantic validity of the referenced targets. The `at0001`–`at0004` metadata node identifiers and locally coded relationship roles were not independently validated against a governed FOLDER archetype or terminology binding. No clinician-centred view reconstruction, complete set of 27 clinical relationships, or T1–T5 functional/architectural evaluation was performed in T0. In particular, the URI-encoded ENTRY paths are **stored references**, not yet proven resolvable by EHRbase.

---

## Overview

| Scenario | Pattern | Creation sequence | EHR-ID | Overall status |
| --- | --- | --- | --- | --- |
| **T1** | **FOLDER (Basic, manuscript Figure 3 mechanism)** | COMPOSITIONs first, FOLDER relationships subsequently | `8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b` | **CORE OPERATIONS PASS, CLINICAL VIEWS PARTIALLY VERIFIED** |
| **T2** | **LINK** | Medical Record Entries first | `dc1bb0c2-342f-4f6a-b426-65b63dffa9a0` | **PASS: relationship operations and manual EP2 reconstruction, automation not tested** |
| **T3** | **LINK** | Care Encounters and Episodes of Care first | `f4908498-afef-4e3c-8cc4-bbdf16d808bf` | **PASS: relationship persistence, AQL and application-driven episode-view reconstruction** |
| **T4** | **CLUSTER** | Medical Record Entries first | `3c269710-a677-4fe8-9083-1133e8899db9` | **PASS within tested scope** |
| **T5** | **CLUSTER** | Care Encounters and Episodes of Care first | `16fe2926-c82a-462c-93f2-d5e67a29656f` | **PASS within tested scope, referential-integrity limitation demonstrated** |

**Scope and terminology.** The evaluated FOLDER mechanism is the reference-based approach represented in the manuscript's original Figure 3: FOLDER structures associate care contacts with clinical COMPOSITIONs and episodes of care with clinical ENTRYs within COMPOSITIONs, without copying clinical content. The figure also depicts a Clinical Sections FOLDER dimension, which was **not implemented** in this execution. The evaluated Basic FOLDER implementation has **no `Primary`/`Associated` relationship role**. A separately tested relationship-role CLUSTER is an exploratory extension, **not** a fourth pattern and **not** evidence for the evaluated Basic FOLDER implementation.

## FOLDER-Based Pattern

### T1 – FOLDER-Based Relationships (Basic FOLDER implementation)

**Environment:** EHRbase 2.30.1, openEHR REST API, canonical JSON. Postman. **Isolated EHR:** `8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b`. **Root DIRECTORY identifier:** `7961df16-9674-4959-8048-ea016c48dfcb`. The test EHR and all clinical COMPOSITION identifiers are distinct from the baseline, T0, and exploratory Extended FOLDER EHRs.

#### Execution results

| Step | Test activity | Expected result | Observed result | Status |
| --- | --- | --- | --- | --- |
| T1.1 | Create isolated EHR | New EHR available | EHR created, EHR-ID recorded above. | **PASS** |
| T1.2 | Persist clinical COMPOSITIONs | Two Care Encounters, four Episodes of Care, and nine Medical Records available | All **15** COMPOSITIONs persisted, AQL inventory returned 15. | **PASS** |
| T1.3 | Establish FOLDER relationships | Contacts and Episodes represented without duplicating clinical ENTRYs | Single DIRECTORY POST returned **201**. **33** initial references (9 `OBJECT_REF` to Medical Record COMPOSITIONs, 18 clinical `DV_EHR_URI` references, 6 CE/EP COMPOSITION metadata references), DIRECTORY `::1`. | **PASS** |
| T1.4 | Retrieve FOLDER relationships | Persisted hierarchy and references retrievable | Independent DIRECTORY GET returned **200**, preserving the two Contact FOLDERs, four Episode FOLDERs, and 33 references. | **PASS** |
| T1.5 | Retrieve referenced clinical content and reconstruct views | Referenced ENTRY/SECTION content retrievable, clinician-centred views reconstructed | Individual COMPOSITION targets inspected. AQL returned one Blood Pressure OBSERVATION and one complete SOAP SECTION with its four nested progress-note observations. Full care-contact/episode view reconstruction and the eight clinician-centred use cases were not executed. | **PARTIALLY VERIFIED** |
| T1.6 *(additional)* | Add episode-to-clinical-content relationship | Add a reference without changing the clinical COMPOSITION | Added EP3 → MR1 Pulse. DIRECTORY changed from `::2` (33 references) to `::3` (34 references). Independent GET verified new EP3 reference and retained EP1 → MR1 Pulse. | **PASS** |
| T1.7 *(additional)* | Remove episode-to-clinical-content relationship | Remove only EP3 → MR1 Pulse, preserve EP1 assignment and clinical content | PUT returned **200** and DIRECTORY `::4` with **33** references. Independent GET confirmed EP3 returned to two Blood Pressure references, while EP1 retained MR1 Pulse. Independent GET of MR1 confirmed BP **140/90 mm[Hg]**, Pulse **75/min**, and unchanged COMPOSITION version `::1`. | **PASS** |

**T1 status**: Core relationship creation, persistence, targeted retrieval, addition, and removal: PASS. Full clinician-centred view reconstruction: PARTIALLY VERIFIED / remaining work. This is **not** a claim that all functional requirements and architectural criteria have been evaluated.

#### Persisted data and relationship model

The T1 EHR contains **15 COMPOSITIONs**: CE1–CE2 (Care Encounters), EP1–EP4 (Episodes of Care), and MR1–MR9 (Medical Records). The DIRECTORY contains `Contacts/CE1`, `Contacts/CE2`, and `Episodes/EP1` through `Episodes/EP4`. A separate `Clinical Sections` FOLDER branch was not created. Each Contact FOLDER references its Medical Record COMPOSITIONs using `FOLDER.items` / `OBJECT_REF` (`VERSIONED_COMPOSITION`). Each CE and EP FOLDER has a `FOLDER.details` `DV_EHR_URI` reference to its corresponding context COMPOSITION. Episode FOLDERs additionally store repeatable `ELEMENT` values of type `DV_EHR_URI` pointing to clinical content within Medical Record COMPOSITIONs.

| Relationship category | Initial `::1` | After addition `::3` | After removal `::4` |
| --- | ---: | ---: | ---: |
| Contact → Medical Record COMPOSITION (`OBJECT_REF`) | 9 | 9 | 9 |
| Episode → clinical ENTRY/SECTION (`DV_EHR_URI`) | 18 | 19 | 18 |
| CE/EP FOLDER → own context COMPOSITION (`DV_EHR_URI`) | 6 | 6 | 6 |
| **Total** | **33** | **34** | **33** |

The 18 initial episode-level clinical references are distributed as EP1: 7, EP2: 6, EP3: 2, EP4: 3. The same Blood Pressure ENTRY from MR1 is referenced in both EP1 and EP3. The SOAP notes MR4 and MR8 are referenced at SECTION.soap.v0 level, preserving each complete SOAP note as a clinical unit despite its four technical OBSERVATION.progress_note.v1 components.

**URI representation:** The stored episode-to-content links use `DV_EHR_URI` values of the form `ehr://<ehr_id>/versioned_composition/<composition_uuid>/content%5B<archetype_id>%5D`. Percent-encoded square brackets were used. The Basic FOLDER relationship metadata are unqualified links: they **do not** encode `Primary` or `Associated` roles.

#### Versioned relationship changes

| DIRECTORY version | Operation / observation | Clinical references in EP3 | Total references |
| --- | --- | ---: | ---: |
| `::1` | Initial POST (201), independently retrieved | 2 (MR1 BP, MR7 BP) | 33 |
| `::2` | Unchanged DIRECTORY PUT ultimately accepted (200), earlier attempts returned 400 | 2 | 33 |
| `::3` | PUT added MR1 Pulse to EP3 (200), independent GET verified | 3 | 34 |
| `::4` | PUT removed MR1 Pulse from EP3 (200), independent GET verified | 2 | 33 |

**Final root DIRECTORY UID:** `7961df16-9674-4959-8048-ea016c48dfcb::local.ehrbase.org::4`.

**Integrity verification:** Following removal, MR1 remained retrievable as `a5b1e471-f28f-4365-b0b0-51c1fb03b112::local.ehrbase.org::1`, containing Blood Pressure 140/90 mm[Hg] and Pulse 75/min. The EP1 reference to the same Pulse ENTRY remained in the retrieved DIRECTORY. The operation changed the current DIRECTORY relationship set, not the clinical COMPOSITION. Retrieval of a historical DIRECTORY version was **not** separately tested.

#### Targeted retrieval and technical observations

- GET of the EP3 context COMPOSITION confirmed the chronic arterial-hypertension problem entry. GET of MR1 confirmed its Blood Pressure and Pulse observations. GET of MR4 confirmed `SECTION.soap.v0` containing the Subjective, Objective, Assessment, and Plan sections with four progress-note observations.
- An exploratory COMPOSITION GET with `?path=/content[openEHR-EHR-OBSERVATION.blood_pressure.v2]` returned the **full COMPOSITION**, not a filtered ENTRY. This does not demonstrate path-based REST dereferencing.
- AQL successfully selected a Blood Pressure `OBSERVATION` from MR1 and the complete SOAP `SECTION` from MR4 (each query returned one result). These are **targeted AQL queries**, not evidence that EHRbase natively dereferences the complete stored `DV_EHR_URI`.
- The initial full DIRECTORY POST succeeded with all 33 references in a single request. Some subsequent PUT attempts returned HTTP **400** with `duplicate entry for DbJsonPath{path=fo0.fo0.dt.i0.}`. An unchanged PUT later succeeded and the next versioned updates also succeeded. **Root cause is undetermined**. No general claim about update reliability or order dependence is warranted from these observations.
- `DV_EHR_URI` storage and retrieval establish preservation of the reference strings. They do **not** establish automatic target validation, referential integrity enforcement, or native URI resolution. An archetype-ID-based selector may be ambiguous if multiple instances of the same archetype occur within a COMPOSITION. This case was not tested.
- No `Primary`/`Associated` role distinction was represented in this Basic FOLDER execution. No quantitative performance, concurrency, long-term maintenance, or complete clinician-view reconstruction evaluation was performed.

#### T1 conclusion

The Basic FOLDER proof of concept demonstrates, for this isolated synthetic dataset in EHRbase 2.30.1, that an openEHR DIRECTORY can preserve relationships from care contacts to Medical Record COMPOSITIONs and from episodes of care to clinical ENTRYs (or a SOAP SECTION) inside COMPOSITIONs. References can be added and removed by versioning the DIRECTORY, while the referenced clinical COMPOSITION remains unchanged and other episode assignments are preserved. **The primary manuscript evaluation is restricted to this reference-based mechanism**. Relationship-role semantics and full clinical-view reconstruction remain outside the demonstrated T1 results.

---

### Additional exploration – Semantic qualification of FOLDER relationships (not a separate scenario)

**Scope:** Exploratory Extended FOLDER implementation, using a relationship `CLUSTER` within `FOLDER.details` to pair an ENTRY-level `DV_EHR_URI` with a locally coded `Primary` or `Associated` role. **Isolated EHR:** `25bf624b-c4ee-43e7-b695-a8d69c37f7f1`. This investigation is **distinct from T0**, the Basic FOLDER T1 evaluation, and the manuscript's standalone CLUSTER pattern (T4–T5).

**Observed implementation:** 15 clinical COMPOSITIONs were created. The intended 33-reference DIRECTORY structure was ultimately persisted and retrieved through successive versioned updates, reaching root DIRECTORY 351d32cf-f50d-4f73-b46e-a66d4f0c3865::local.ehrbase.org::7. The implementation represented 9 Contact-to-Medical-Record OBJECT_REF references, 6 CE/EP metadata COMPOSITION references, and 18 episode-to-clinical-content references carrying relationship metadata. An initial full DIRECTORY POST returned HTTP 400 with duplicate entry for DbJsonPath{path=fo0.fo0.dt.i0.}. Incremental updates ultimately succeeded. The underlying cause was not established.

**Interpretation**: The tests provide evidence that the role-qualified relationship representation can be stored and retrieved in this environment. They do not constitute the same systematic addition/removal, native URI dereferencing, clinical-view reconstruction, terminology governance, or architectural evaluation performed or planned for the Basic FOLDER mechanism. In particular, the locally coded relationship roles and metadata identifiers were not independently validated against a governed archetype/terminology specification. The extension should therefore be mentioned, if relevant, in Discussion / Future Work, not counted as a fourth pattern or included in the principal FOLDER comparison.

---

## LINK-Based Pattern

### T2 – Medical Record Entries First

**Status: COMPLETED — PASS for the defined relationship-persistence, retrieval, and manual EP2-view reconstruction tests.** Native LINK dereferencing, automatic clinical-view assembly, and repository-enforced referential or role constraints were **not demonstrated**. The detailed evidence is retained in `04-link-pattern/T2/T2-link-test-identifiers.md`, with implementation details in `04-link-pattern/T2/T2-link-implementation.md` and original REST request/response JSON artifacts in `04-link-pattern/T2/json/`.

**Environment:** EHRbase 2.30.1, openEHR REST API, canonical JSON, Postman, AQL. **Isolated EHR:** `dc1bb0c2-342f-4f6a-b426-65b63dffa9a0` (distinct from the baseline, T0, and T1 EHRs). Nine Medical Record COMPOSITIONs (MR1–MR9) were persisted before relationship-bearing Care Encounter and Episode-of-Care COMPOSITIONs. The final state comprises **15 COMPOSITIONs**: nine Medical Records, two Care Encounters, and four Episodes of Care.

#### Execution results

| Step | Test activity | Observed result | Status |
| --- | --- | --- | --- |
| T2.1 | Create isolated EHR | EHR created. Identifier recorded above. | **PASS** |
| T2.2 | Persist Medical Record COMPOSITIONs | MR1–MR9 persisted. ENTRY structures subsequently verified by GET/AQL. Nine MR COMPOSITIONs contain 19 clinical ENTRYs, counting the four technical progress-note ENTRYs in each SOAP note. | **PASS** |
| T2.3 | Persist Care Encounter LINKs | CE1 version `::2` references MR1–MR5 (five `encounter` LINKs). CE2 version `::1` references MR6–MR9 (four LINKs). Independent AQL retrieval returned five and four rows respectively. | **PASS** |
| T2.4 | Test episode LINK representation and selective content retrieval | Primary and Associated references persisted and retrieved in initial smoke tests. URI-encoding correction required for square brackets. AQL retrieved a targeted Blood Pressure ENTRY. A REST GET with a `path` query parameter returned the full COMPOSITION, not an ENTRY-only response. | **PASS** for storage/AQL. **NOT VERIFIED** for native URI dereferencing |
| T2.5 | Validate ENTRY paths and complete EP LINK sets | All MR1–MR9 ENTRY structures checked. EP1 version `::2` has seven Primary LINKs. EP2 version `::1` twelve Primary. EP3 version `::2` two Associated. EP4 version `::1` three Associated. Individual episode AQL retrieval returned 7/12/2/3 rows. | **PASS** |
| T2.6 | Consolidated relationship retrieval and uniqueness check | AQL returned 24 episode LINKs across EP1–EP4: 19 Primary and 5 Associated. Together with nine encounter LINKs, 33 persisted LINKs were retrieved. Manual inspection confirmed one Primary per each of 19 distinct ENTRYs, without duplicates in the defined dataset. | **PASS** (application-level verification) |
| T2.7a | Resolve EP2 relationship targets | AQL returned twelve Primary LINKs to twelve distinct ENTRY paths in six Medical Record COMPOSITIONs (MR3, MR4, MR5, MR6, MR8, MR9). | **PASS** |
| T2.7b | Retrieve EP2 clinical ENTRY content | Six AQL requests retrieved all twelve ENTRYs: MR3 (1), MR4 SOAP (4), MR5 (1), MR6 (1), MR8 SOAP (4), MR9 (1). Nested microbiology culture/susceptibility CLUSTER and medication INSTRUCTION structures were preserved. | **PASS** |
| T2.7c | Assemble EP2 clinical view | Retrieved content was **manually** organised by CE1 (15 November 2024) and CE2 (17 November 2024), showing the progression from suspected cystitis and empirical TMP–SMX to resistant *E. coli* and changed therapy. No duplicate clinical ENTRYs were created. | **PASS — manual feasibility demonstration** |

#### Persisted relationships and identifiers

| Context COMPOSITION | Current versioned UID | LINK count | Relationship role |
| --- | --- | ---: | --- |
| CE1 | `677552a4-fd78-4678-b91c-0172bc118017::local.ehrbase.org::2` | 5 | `encounter` |
| CE2 | `4805a3a9-7518-4bd8-9f5f-e57bcfcb30c2::local.ehrbase.org::1` | 4 | `encounter` |
| EP1 | `6e963022-99a0-45ff-803b-24b835f254ce::local.ehrbase.org::2` | 7 | `episode-of-care-primary` |
| EP2 | `9f04a0d0-1eed-4688-9d19-04cf3f1d5210::local.ehrbase.org::1` | 12 | `episode-of-care-primary` |
| EP3 | `e7aaa7a9-c8d9-4533-8725-9c51d4d7e003::local.ehrbase.org::2` | 2 | `episode-of-care-associated` |
| EP4 | `81bcb7b2-7db7-480c-abcd-9c5441e51f73::local.ehrbase.org::1` | 3 | `episode-of-care-associated` |
| **Total** | **6 relationship-bearing COMPOSITIONs** | **33** | **9 encounter + 19 Primary + 5 Associated** |

Care Encounter LINKs target versioned Medical Record COMPOSITIONs. Episode LINKs target individual clinical ENTRY paths inside versioned Medical Record COMPOSITIONs. Each SOAP note (MR4 and MR8) is treated as one indivisible clinical unit although represented by four OBSERVATION.progress_note.v1 ENTRYs under SECTION.soap.v0. All four technical ENTRYs of each SOAP note have the same Primary assignment to EP2. EP1 is a default episode, not a parent of the other episodes. The role and uniqueness rules were checked against the synthetic dataset. They were not enforced by EHRbase in these tests.

#### Clinical-view reconstruction and evidence limits

EP2's twelve LINK targets cover six Medical Record COMPOSITIONs across two Care Encounters. AQL returned the clinical ENTRY objects (including nested structures), and the results were manually assembled into a chronological episode-oriented view. The resulting narrative follows the urinalysis and suspected cystitis on 15 November 2024, followed by microbiology results and revised antimicrobial treatment on 17 November 2024. This demonstrates feasibility of an application-driven reconstruction for the tested dataset, without duplicating the clinical ENTRYs. It does not demonstrate automatic traversal or dereferencing of stored DV_EHR_URI targets by EHRbase, an implemented view-assembly service, or execution of all eight clinician-centred user stories.

**Technical observations:** Literal `[` and `]` in `DV_EHR_URI` target paths produced HTTP 400 during Java URI parsing, encoding them as `%5B` and `%5D` enabled persistence. An exploratory REST COMPOSITION GET with `?path=...` returned the full COMPOSITION, so it did not establish ENTRY-level REST dereferencing. AQL selected the required clinical ENTRY independently of the stored LINK string. The application would need to interpret LINK targets and issue suitable retrieval queries. No general performance, concurrency, referential integrity, automatic update propagation, or cross-version target-resolution claims are supported.

**Archived artifacts**: The consolidated T2 archive contains ten POST/PUT request JSON files and 15 independently exported final COMPOSITION JSON files (MR1–MR9, CE1–CE2, EP1–EP4), including T2-MR9-final.json. The archived versioned COMPOSITION identifiers are documented in the T2 evidence manifest. The six CE/EP exports contain all 33 LINKs. This archive consistency check is separate from the live execution results. Executed AQL queries and observed results are documented in the T2 test records, but complete AQL response payloads were not separately archived.

#### T2 conclusion

**T2 overall:** PASS within the tested scope. EHRbase 2.30.1 preserved and returned 33 LINK relationships spanning two care encounters and four episodes of care, including Primary and Associated relationships to existing clinical ENTRYs. All twelve EP2 ENTRYs were individually retrieved and manually assembled into a coherent longitudinal view without copying the underlying clinical content. Native LINK dereferencing, automated clinical-view generation, and repository-enforced relationship semantics remain unverified. The full eight clinician-centred functional requirements and six architectural criteria have not yet been evaluated comparatively.

### T3 – Care Encounters and Episodes of Care First

**Status: COMPLETED — PASS within tested scope.** EHRbase 2.30.1, canonical JSON, REST API, Postman and AQL. **Isolated EHR:** `f4908498-afef-4e3c-8cc4-bbdf16d808bf`. T3 reverses T2's creation order and LINK direction: CE/EP COMPOSITIONs were persisted first. Subsequently each MR COMPOSITION links to its CE, and each clinical ENTRY links to its primary EP (with optional associated EPs). Detailed evidence and query catalogue: [`04-link-pattern/T3/README.md`](04-link-pattern/T3/README.md), [`T3-link-test-results.md`](04-link-pattern/T3/T3-link-test-results.md), [`T3-link-test-identifiers.md`](04-link-pattern/T3/T3-link-test-identifiers.md), and [`T3-aql-query-catalog.md`](04-link-pattern/T3/T3-aql-query-catalog.md).

| Step | Test activity | Observed result | Status |
| --- | --- | --- | --- |
| T3.1 | Create isolated EHR | EHR `f4908498-afef-4e3c-8cc4-bbdf16d808bf` created and used for all subsequent T3 operations | **PASS** |
| T3.2 | Persist Care Encounters | CE1 and CE2 persisted, version `::1` | **PASS** |
| T3.3 | Persist Episodes of Care | EP1–EP4 persisted, version `::1` | **PASS** |
| T3.4 | Persist MR1–MR9 with outgoing LINKs | All nine MR POST HTTP 201 and independent GET HTTP 200. 33 LINKs verified in persisted COMPOSITIONs | **PASS** |
| T3.5 | Retrieve relationships via AQL | Inventory 15 COMPOSITIONs. 9 encounter LINKs, 22 OBSERVATION LINK rows and 2 INSTRUCTION LINK rows | **PASS** |
| T3.6 | Reconstruct and validate clinical content | EP2: 12 technical ENTRYs across 6 MR documents and 2 encounters. SOAP, urinalysis, microbiology, medications and individual LINK cardinalities verified, documented AQL syntax exceptions corrected | **PASS within tested scope** |
| T3.7 *(additional)* | Validate longitudinal and associated episode views | EP2 six distinct MR documents (CE1 three, CE2 three). EP3 two associated BP observations. EP4 three associated body measurements. Reused T3.6 AQL evidence | **PASS within tested scope** |

#### Relationship inventory

| Category | Count | Meaning |
| --- | ---: | --- |
| MR COMPOSITION → Care Encounter | 9 | `COMPOSITION.links`, type `encounter` |
| Clinical ENTRY → primary Episode of Care | 19 | `ENTRY.links`, type `episode-of-care-primary` |
| Clinical ENTRY → associated Episode of Care | 5 | `ENTRY.links`, type `episode-of-care-associated` |
| **Total** | **33** | **19 technical ENTRYs across 9 MR COMPOSITIONs** |

**Episode allocation:** EP1 primary 7 ENTRYs (MR1 2, MR2 3, MR7 2). EP2 primary 12 ENTRYs (MR3 1, MR4 4, MR5 1, MR6 1, MR8 4, MR9 1). EP3 associated 2 BP observations (MR1/MR7). EP4 associated 3 body measurements (MR2). EP1 is a default episode, not a parent of the others. SOAP MR4 and MR8 each remain **one clinical note** despite their four technical `OBSERVATION.progress_note.v1` ENTRYs. All four carry the same EP2 primary assignment. The clinical ENTRYs are not duplicated by associated links.

#### Retrieval and clinical reconstruction

AQL inverse filtering by `ENTRY.links/target/value` identified the EP2 content, and combining this with `COMPOSITION.links/target/value` assigned MR3/MR4/MR5 to CE1 (2024-11-15) and MR6/MR8/MR9 to CE2 (2024-11-17). The reconstructed sequence covers urinalysis, suspected cystitis, empirical TMP–SMX, subsequent resistant *E. coli* urine culture and switch to amoxicillin–clavulanate. Separate AQL filters returned the two EP3 BP observations and three EP4 measurements. The resulting episode views were **assembled/interpreted at application level**, not automatically generated by the repository.

#### Technical observations and limitations

- `SECTION CONTAINS OBSERVATION` initially returned parent- and leaf-section matches for SOAP (16 vs expected 8 rows). Filtering out `SOAP headings` returned the expected eight leaf rows. Display-name filters are not ideal for production use.
- Nested microbiology `CLUSTER[at0009]` traversal initially produced HTTP 400 / zero rows, adding the OBSERVATION archetype predicate **and intermediate microbiology CLUSTER** yielded five correct antibiotic/interpretation pairs.
- A `GROUP BY` query returned HTTP 400 because `GROUP BY` is not standard AQL: test T3.6.14 is **N/A**, not a repository defect.
- AQL can expand multiple `links` into multiple rows for one ENTRY. Persisted JSON was independently inspected to confirm **exactly one primary EP link per each of 19 ENTRYs**.
- `DV_ORDINAL` clinical display labels (e.g. urinalysis leukocytes `3+`) are stored in `symbol/value`, not the numeric ordinal.
- `DV_EHR_URI` targets were persisted, retrieved and searched, **not natively dereferenced**. Automatic view assembly, repository-enforced relationship cardinality and referential integrity, concurrency, performance and all eight clinician-centred use cases/six architectural criteria were **not demonstrated**.
- The `04-link-pattern/T3/json/requests/` folder contains seven verified T3-labelled request JSONs, it is **not** a complete export of original REST/AQL responses. See the evidence manifest.

**T3 conclusion:** **PASS within the defined relationship persistence, retrieval, integrity and application-driven episode-view reconstruction scope.** All **15** COMPOSITIONs and **33** LINK instances were persisted and checked, 19/19 ENTRY primary assignments and 5/5 associated assignments were confirmed. Creation-order and link-direction differences versus T2 are established. A full comparative architectural evaluation remains outstanding.

## CLUSTER-Based Pattern

### T4 – Medical Record Entries First

**Status: COMPLETED — PASS within tested scope.** **Environment:** EHRbase 2.30.1, openEHR REST API, canonical JSON, Postman and AQL. **Isolated EHR:** `3c269710-a677-4fe8-9083-1133e8899db9`. T4 tests relationship CLUSTERs held by Care Encounter and Episode-of-Care COMPOSITIONs, with nine Medical Record COMPOSITIONs persisted first and left unchanged. Detailed documentation: [`05-cluster-pattern/T4/README.md`](05-cluster-pattern/T4/README.md), [`T4-cluster-test-results.md`](05-cluster-pattern/T4/T4-cluster-test-results.md), [`T4-cluster-test-identifiers.md`](05-cluster-pattern/T4/T4-cluster-test-identifiers.md), [`T4-aql-query-catalog.md`](05-cluster-pattern/T4/T4-aql-query-catalog.md), and [`T4-evidence-manifest.md`](05-cluster-pattern/T4/T4-evidence-manifest.md).

#### Execution results

| Step | Test activity | Observed result | Status |
| --- | --- | --- | --- |
| T4.1 | Create isolated EHR | POST HTTP 201. Independent EHR GET HTTP 200. | **PASS** |
| T4.2 | Persist Medical Records first | MR1–MR9 POST HTTP 201 and independent GET HTTP 200, all nine are version `::1`, with no relationship CLUSTERs, 19 clinical ENTRYs. | **PASS** |
| T4.3 | Persist CE1 with relationship CLUSTER | CE1 POST 201 and GET 200, `CLUSTER.eoc_relationships_care_encounter.v0` holds five `DV_EHR_URI` references to MR1–MR5. | **PASS** |
| T4.4 | Persist CE2 without references | CE2 POST 201 and GET 200 for version `::1`, relationship CLUSTER absent. | **PASS** |
| T4.5 | Update CE2 with relationship CLUSTER | PUT HTTP 200 produced CE2 `::2` with four references to MR6–MR9, GET 200 verified both `::2` and historical `::1` (without relationships). | **PASS** |
| T4.6 | Persist EP1–EP4 with relationship CLUSTERs | Four POST 201 and independent GET 200, `CLUSTER.eoc_relationships_episode_of_care.v0` holds 7 + 12 + 2 + 3 = 24 ENTRY references. | **PASS** |
| T4.7 | Validate REST/AQL COMPOSITION inventory | EHR GET 200, AQL returned 15 current COMPOSITIONs (9 MR, 2 CE, 4 EP). | **PASS** |
| T4.8 | Retrieve relationships via AQL | AQL returned nine CE→MR references and 24 EP→ENTRY references, 33 total. | **PASS** |
| T4.9 | Reconstruct clinical views | AQL returned 19 clinical MR ENTRYs, EP2 12 references, complete MR3 urinalysis, MR4/MR8 SOAP sections, four diagnoses with Current/Active qualifiers. | **PASS within tested views** |
| T4.10 | Document and archive evidence | Eight CE/EP request JSONs and 16 persisted COMPOSITION JSON exports documented (15 current versions plus historical CE2 `::1`), detailed test log, identifiers, query catalogue and checksum manifest prepared. | **DOCUMENTED** |

#### Relationship representation and inventory

| Relationship category | Location / representation | Count |
| --- | --- | ---: |
| Care Encounter → Medical Record COMPOSITION | CE `context.other_context`, `CLUSTER.eoc_relationships_care_encounter.v0`, `DV_EHR_URI` | 9 |
| Episode of Care → primary clinical ENTRY | EP `context.other_context`, `CLUSTER.eoc_relationships_episode_of_care.v0`, role `Primary` (`at0163`) | 19 |
| Episode of Care → associated clinical ENTRY | Same EP relationship CLUSTER, role `Associated` (`at0164`) | 5 |
| **Total** | **9 CE→MR + 24 EP→ENTRY** | **33** |

CE1 references MR1–MR5 (five), CE2 `::2` references MR6–MR9 (four). EP1 contains seven Primary references, EP2 twelve Primary, EP3 two Associated (blood pressure), and EP4 three Associated (body measurements). EP2's twelve technical ENTRY references span six Medical Record COMPOSITIONs across two encounters. EP1 is a default episode, not a parent of the other episodes. MR4 and MR8 each represent **one clinically indivisible SOAP note** through four `OBSERVATION.progress_note.v1` ENTRYs grouped in one `SECTION.soap.v0`, all four ENTRYs of each note have the same Primary assignment to EP2 in the tested dataset. No clinical ENTRY duplication or MR version change was required.

#### Clinical-view reconstruction

AQL retrieved 25 ENTRYs overall, including 19 clinical MR ENTRYs (11 at the first encounter on 15 November 2024 and eight at the follow-up on 17 November 2024), two Care Encounter EVALUATIONs and four Episode-of-Care EVALUATIONs. EP2 relationship filtering returned twelve Primary URI strings pointing to MR3, MR4, MR5, MR6, MR8 and MR9. A separate AQL query retrieved the complete MR3 urinalysis. Queries for `SECTION.soap.v0` returned one complete SOAP section in each of MR4 and MR8, including the four nested Subjective, Objective, Assessment and Plan sections and their respective progress-note ENTRYs. These results support application-level reconstruction of the course from suspected cystitis and empirical trimethoprim–sulfamethoxazole to persistent symptoms, resistant *E. coli* and antimicrobial therapy change. A separate AQL query reconstructed the four-item diagnosis/problem list (General health problem. Urinary tract infection. Arterial hypertension (Dx 2009). Obesity WHO grade I), each with `Current` and `Active` qualifiers. These are **queried and interpreted clinical views**, not a demonstrated automatic CDR view-assembly service.

#### Versioning, technical observations and evidence

- CE2 was created as `ebe7f166-85c0-4c68-bf8a-572f32cc2c3c::local.ehrbase.org::1` without relationships and updated to `::2` with four CE→MR references. Both JSON versions were independently retrieved and archived, the nine MR COMPOSITIONs remained at `::1`.
- The initial EP1 request with literal square brackets in ENTRY URI paths returned HTTP 400, percent-encoding as `%5B` and `%5D` allowed the corrected POST (201). Both request variants are retained as separate negative/successful evidence, not counted as two successful writes.
- The archive contains eight CE/EP request JSON files (including the unsuccessful EP1 variant) and **16 actual persisted COMPOSITION JSON response bodies**: nine MR, two current CE, four EP and the historical CE2 `::1`. The evidence manifest records their versioned identifiers and SHA-256 hashes. Original MR POST request bodies, REST status/header exports and raw Postman AQL response exports are not included, test-session responses were observed and documented.
- AQL retrieved stored `DV_EHR_URI` **strings**, not automatically dereferenced target objects. Clinical content was retrieved with separate AQL queries using known COMPOSITION/ENTRY identifiers. Native URI resolution, server-enforced referential integrity, relationship cardinality and primary uniqueness, concurrency, performance, and a full comparative evaluation of all eight clinician-centred user stories and six architectural criteria were **not tested**.

#### Relationship optionality and production governance

For the purposes of this proof of concept, the relationship CLUSTER archetypes and corresponding templates were deliberately modelled to permit the initial persistence of clinical information without references to existing Care Encounter or Episode of Care COMPOSITIONs. This design enables the evaluation of different object creation sequences, particularly the Medical Record-first scenario (T4).

In a production environment involving multiple software vendors, mandatory relationship constraints would be preferable to ensure that clinical entries are not persisted without the required contextual associations. Such constraints could be enforced through archetype and template validation, while referential integrity and the existence of referenced target objects would require additional validation mechanisms.

The optionality implemented in this PoC therefore represents a deliberate experimental design choice rather than a recommended production configuration.

**T4 conclusion:** **PASS within tested scope.** EHRbase 2.30.1 persisted and returned CE/EP-held, archetyped CLUSTER relationships to nine pre-existing Medical Record COMPOSITIONs and their clinical ENTRYs. All 33 stored references were retrievable through AQL, both CE2 versions were preserved, and the tested chronological, episode-oriented, SOAP and diagnosis views were reconstructed without duplicating clinical MR content. The experiment does **not** demonstrate native `DV_EHR_URI` dereferencing or repository-enforced relationship semantics.

### T5 – Care Encounters and Episodes of Care First

**Status: COMPLETED — PASS within tested scope.** **Environment:** EHRbase 2.30.1, openEHR REST API, canonical JSON, Postman and AQL. **Isolated EHR:** `16fe2926-c82a-462c-93f2-d5e67a29656f`. T5 reverses T4's creation order and relationship direction: Care Encounter (CE) and Episode of Care (EP) COMPOSITIONs are created first, each subsequently persisted Medical Record (MR) holds an archetyped relationship CLUSTER within each clinical ENTRY's `protocol`, referencing its existing CE and one or more EPs. Detailed documentation: [`05-cluster-pattern/T5/README.md`](05-cluster-pattern/T5/README.md), [`T5-cluster-test-results.md`](05-cluster-pattern/T5/T5-cluster-test-results.md), [`T5-cluster-test-identifiers.md`](05-cluster-pattern/T5/T5-cluster-test-identifiers.md), [`T5-aql-query-catalog.md`](05-cluster-pattern/T5/T5-aql-query-catalog.md), and [`T5-evidence-manifest.md`](05-cluster-pattern/T5/T5-evidence-manifest.md). The original **15-COMPOSITION reference dataset** must be distinguished from the additional **RI-02 negative-test COMPOSITION**.

#### Execution results

| Step | Test activity | Observed result | Status |
| --- | --- | --- | --- |
| T5.1 | Create isolated EHR | EHR `16fe2926-c82a-462c-93f2-d5e67a29656f` created, POST HTTP 201. | **PASS** |
| T5.2 | Persist Care Encounters first | CE1 and CE2 POST 201 and independent GET 200, both `::1`, no outgoing relationship CLUSTER. | **PASS** |
| T5.3 | Persist Episodes of Care first | EP1–EP4 POST 201 and independent GET 200, all `::1`, clinical problem/diagnosis content retained. | **PASS** |
| T5.4 | Persist MR1–MR9 with relationship CLUSTERs | All nine MR POST 201 and independent GET 200, 19 clinical ENTRYs (17 OBSERVATION, 2 INSTRUCTION), each with a relationship CLUSTER in `ENTRY.protocol`, all 33 logical associations represented. | **PASS** |
| T5.5 | Retrieve relationships and reconstruct views | Twelve AQL queries successfully retrieved inventory, 19 relationship-bearing ENTRYs, 24 episode-role rows, EP2 and CE2 views, associated EP3/EP4 observations, clinical BP values, and SOAP notes. Independent EP2 COMPOSITION GET returned 200. | **PASS within tested views** |
| T5.6 | Referential-integrity negative tests | RI-01 AQL confirmed target UID absent (0 rows), RI-02 POST accepted a new MR with invalid EP URI (201), RI-03 independent GET returned the URI unchanged (200), RI-04 AQL retrieved the same invalid URI (1 row). | **PASS — limitation demonstrated** |

#### Persisted COMPOSITIONs and identifiers

All UIDs below are versioned `OBJECT_VERSION_ID` values with system `local.ehrbase.org`, version `::1`. Each of the original 15 COMPOSITIONs was independently retrieved (GET HTTP 200).

| Object | Clinical content | Versioned COMPOSITION UID |
| --- | --- | --- |
| CE1 | Initial consultation, 2024-11-15 | `6617f878-b798-4422-979f-524d44dc1385::local.ehrbase.org::1` |
| CE2 | Follow-up consultation, 2024-11-17 | `bd0bb285-e61d-411b-8c4f-d06a05b53ba6::local.ehrbase.org::1` |
| EP1 | General health problem (default episode) | `78967a71-271e-462f-ae85-2bfcaba1768e::local.ehrbase.org::1` |
| EP2 | Urinary tract infection | `c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1` |
| EP3 | Arterial hypertension (Dx 2009) | `364fa3f4-acba-4b9b-9c5c-4feb0f5cbff3::local.ehrbase.org::1` |
| EP4 | Obesity WHO grade I | `3af7b6c8-ae69-481a-b01c-31e804be99bc::local.ehrbase.org::1` |
| MR1 | Vital signs, CE1 | `9a500145-37ec-4710-b573-6fabf11b42a0::local.ehrbase.org::1` |
| MR2 | Body measurements, CE1 | `86603afd-080c-46df-af9b-9c7f8b7b02e0::local.ehrbase.org::1` |
| MR3 | Urinalysis, CE1 | `8e457025-3785-40ef-9e47-117c09f4d803::local.ehrbase.org::1` |
| MR4 | SOAP progress note, CE1 | `69dd2dcd-9211-4b23-92d0-038cc2c450fe::local.ehrbase.org::1` |
| MR5 | Medication order, CE1 | `4eb9ce0f-1911-4638-aadc-287e34e62335::local.ehrbase.org::1` |
| MR6 | Microbiology result, CE2 | `27bbcc6e-d6a9-4e49-a155-fc4b2bfce0ff::local.ehrbase.org::1` |
| MR7 | Vital signs, CE2 | `8754b7f5-8cc9-4fb6-885e-e7d37a313fbe::local.ehrbase.org::1` |
| MR8 | SOAP progress note, CE2 | `6b11b73e-7536-4399-9406-644a54a0d2cb::local.ehrbase.org::1` |
| MR9 | Medication order, CE2 | `eda7279d-6e66-4efc-bdc5-96e6e1d2bf76::local.ehrbase.org::1` |

**Templates and placement.** CE COMPOSITIONs use `JPM_Care_Encounter_Cluster.v1`, EP COMPOSITIONs use `JPM_Episode_of_Care_Cluster.v1` and `openEHR-EHR-COMPOSITION.problem_list.v2`. The nine MRs use their designated `JPM_Medical_Record_*_Cluster.v1` or `JPM_SOAP_Progress_Note_Cluster.v1` templates. Relationship instances are stored in `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0` inside the `protocol` ITEM_TREE of each clinical OBSERVATION or INSTRUCTION. CE and EP context COMPOSITIONs do not carry these outgoing MR relationship CLUSTERs in T5.

#### Relationship representation and inventory

| Relationship category | Location / representation | Logical count | Persisted URI occurrences |
| --- | --- | ---: | ---: |
| Medical Record → Care Encounter | Contact reference (`at0001` → `at0009`) within each ENTRY relationship CLUSTER, `DV_EHR_URI` | 9 distinct MR→CE associations | 19 |
| Clinical ENTRY → primary Episode of Care | Episode reference (`at0109` → `at0147`), role `Primary` (`at0154`) | 19 | 19 |
| Clinical ENTRY → associated Episode of Care | Same repeatable Episode reference, role `Associated` (`at0155`) | 5 | 5 |
| **Total** | **9 MR→CE + 24 ENTRY→EP** | **33** | **43** |

The nine MR→CE associations are logical relationships: the same CE URI is repeated within each of the 19 clinical ENTRY relationship CLUSTERs. Do not confuse 43 persisted URI occurrences with 33 logical relationships, or AQL result-row expansion with additional stored references. EP allocation: EP1 seven Primary ENTRYs (MR1 two, MR2 three, MR7 two), EP2 twelve Primary ENTRYs (MR3 one, MR4 four, MR5 one, MR6 one, MR8 four, MR9 one), EP3 two Associated blood-pressure observations (MR1/MR7), EP4 three Associated body measurements (MR2). EP1 is a default episode, not a parent of EP2–EP4. No clinical ENTRY duplication is required for Associated assignments.

MR1 contains blood pressure 140/90 mm[Hg] and pulse 75/min, MR2 height 168 cm, weight 86 kg and BMI 30.5 kg/m², MR3 urinalysis (leukocytes 3+, nitrite positive, blood 1+, protein trace, pH 6.0), MR4 the initial SOAP note, MR5 the TMP–SMX order. MR6 preserves urine culture (*Escherichia coli*, ≥10⁵ CFU/mL) and five antimicrobial susceptibility results, MR7 blood pressure 142/85 mm[Hg] and pulse 72/min, MR8 the follow-up SOAP note, MR9 the amoxicillin–clavulanate order. The baseline caveat about independently verifying the local resistance code `at0015` remains applicable. Existing clinical `protocol` information (including the MR3 urinalysis method) coexists with the appended relationship CLUSTER.

#### AQL retrieval and clinical-view reconstruction

**Twelve AQL tests (AQL-01–AQL-12) completed successfully in the tested scope:**

| Query | Verified result |
| --- | --- |
| AQL-01 | 15 current reference COMPOSITIONs (2 CE, 4 EP, 9 MR), before RI-02 was added. |
| AQL-02 | 19 clinical ENTRYs containing `eoc_relationships_entry.v0` (including both OBSERVATION and INSTRUCTION). |
| AQL-03 | 24 EP relationship rows: 19 Primary and 5 Associated, with correctly paired role and URI, repeated contact URI in expanded rows does not imply extra stored contact references. |
| AQL-04 | EP2 longitudinal selection: 12 technical ENTRYs across six MR COMPOSITIONs, spanning both encounters. |
| AQL-05 | CE2 view: eight ENTRYs across MR6, MR7, MR8 and MR9. |
| AQL-06 | CE2 ∩ EP2: six ENTRYs in MR6, MR8 and MR9, excludes MR7 vital signs. |
| AQL-07 | Five Associated EP rows: two EP3 blood-pressure and three EP4 body-measurement observations, filtered by coded role `at0155`. |
| AQL-08 | EP3 blood-pressure history with clinical `HISTORY` structures: 140/90 mm[Hg] (2024-11-15) and 142/85 mm[Hg] (2024-11-17). |
| AQL-09 | Four MR8 SOAP ENTRYs with complete clinical data and identical CE2/EP2 Primary references. |
| AQL-10 | Eight rows due to hierarchical SECTION matching: four under parent `SOAP headings` and four under leaf S/O/A/P sections, **four unique ENTRYs**, not eight. |
| AQL-11 | Four non-duplicated MR8 SOAP leaf sections with directly extracted progress-note text, excluding parent `SOAP headings`. |
| AQL-12 | Eight leaf-section rows representing **two complete SOAP notes** (MR4 and MR8), selected solely by EP2 URI, with consistent `Primary` role and chronological encounter dates. |

**Longitudinal EP2 view.** The six MRs associated with EP2 are MR3, MR4 and MR5 on 15 November 2024 (urinalysis, suspected cystitis SOAP note, empirical TMP–SMX order), followed by MR6, MR8 and MR9 on 17 November 2024 (resistant *E. coli* microbiology, follow-up SOAP note, changed antimicrobial therapy). The two SOAP notes are **two clinically indivisible documentation units**, although technically represented by eight `OBSERVATION.progress_note.v1` ENTRYs. In AQL-12, grouping by COMPOSITION UID and the specific leaf SECTION labels reconstructs the two S/O/A/P units without prior knowledge of their MR COMPOSITION UIDs. AQL `ORDER BY` on timestamps alone does not guarantee S/O/A/P ordering within a note, SECTION labels must be used.

**Target retrieval.** The stored EP2 `DV_EHR_URI` is `ehr://c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1`. A separate GET using its versioned COMPOSITION UID returned HTTP 200 and confirmed the Episode of Care header (Urinary tract infection. Active. Acute. Diagnosis) and `EVALUATION.problem_diagnosis.v1` (Current. Active). This proves independent target existence and retrieval for EP2, **not** native automatic `DV_EHR_URI` dereferencing or server-side join/traversal.

#### Referential-integrity negative tests (T5.6)

**Test target (intentionally absent):** `ehr://00000000-0000-4000-8000-000000000099::local.ehrbase.org::1`. **Additional test COMPOSITION:** `056c6620-67b0-408f-bf90-1f8458fe8b66::local.ehrbase.org::1` (Medication order, CE1, invalid EP Primary reference).

| Test | Observation | Status |
| --- | --- | --- |
| RI-01 | AQL lookup of target UID returned `resultsize = 0`, no such COMPOSITION in the test EHR at query time. | **PASS** |
| RI-02 | POST of an additional MR Medication Order with the invalid EP URI returned HTTP **201 Created**, response preserved CE1 and the invalid EP URI. | **PASS — invalid reference accepted** |
| RI-03 | Independent GET of the newly created COMPOSITION returned HTTP **200 OK** with the same invalid EP URI and `Primary` role unchanged. | **PASS — persistence confirmed** |
| RI-04 | AQL over the new MR returned exactly **one row**, including the invalid EP URI, CE1 URI and `Primary` role. | **PASS — queryability confirmed** |

**Interpretation:** The tested EHRbase 2.30.1 configuration **did not enforce target existence** for this syntactically valid `DV_EHR_URI` in `CLUSTER.eoc_relationships_entry.v0`. This does not establish that all openEHR reference types, configurations, or repositories lack integrity checking. Archetype/template constraints can define relationship structure and cardinality, but the tested constraints did not validate target existence. Additional application or service-layer validation would be required for production governance.

**Dataset isolation:** Original T5 reference dataset: **15 COMPOSITIONs, 19 clinical ENTRYs, 33 logical associations and 43 persisted URI occurrences**. After RI-02, the same EHR contains **16 COMPOSITIONs, 20 clinical ENTRYs, 35 logical associations and 45 URI occurrences**. The RI-02 test object is **excluded** from reference-dataset counts and comparative analyses. Unfiltered repeat inventory or relationship queries after RI-02 would include this extra object, filter by the original COMPOSITION UIDs or use the recorded pre-RI results.

#### Relationship optionality and production governance

For the purposes of this proof of concept, the relationship CLUSTER archetypes and corresponding templates were deliberately modelled to permit the initial persistence of clinical information without references to existing Care Encounter or Episode of Care COMPOSITIONs. This design enables the evaluation of different object creation sequences, particularly the Medical Record-first scenario (T4).

In a production environment involving multiple software vendors, mandatory relationship constraints would be preferable to ensure that clinical entries are not persisted without the required contextual associations. Such constraints could be enforced through archetype and template validation, while referential integrity and the existence of referenced target objects would require additional validation mechanisms.

The optionality implemented in this PoC therefore represents a deliberate experimental design choice rather than a recommended production configuration.

#### Technical observations, evidence limits and conclusion

- **T4 versus T5:** T4 stores relationships in the context COMPOSITIONs (CE→MR, EP→ENTRY) after creating MR objects, T5 stores them in the clinical ENTRYs (MR/ENTRY→CE/EP) after creating CE/EP objects. Both implement the same 33 logical associations for the synthetic dataset but distribute relationship governance and update responsibilities differently. No measured performance or maintenance comparison is claimed.
- **SOAP unit of documentation:** Both MR4 and MR8 have four technical `OBSERVATION.progress_note.v1` ENTRYs grouped into one SOAP COMPOSITION. All four have consistent EP2 Primary references in the observed data. This is verified dataset consistency, **not** a repository-enforced atomic episode-assignment rule across all four ENTRYs.
- **AQL cardinality:** `CONTAINS SECTION s CONTAINS ENTRY entry` can match both parent and leaf SECTIONs, expanding SOAP results, filtering `s/name/value != 'SOAP headings'` returned the four desired leaf rows per note. Production queries should prefer stable coded/archetype constraints over display-name strings where possible.
- **Dereferencing and integrity:** AQL returned stored URI values and clinical data, EP2 was fetched in a separate GET. Native automatic dereferencing, target existence enforcement, automatic view assembly, relationship cardinality enforcement, primary uniqueness, concurrency, and performance were **not** demonstrated. Target existence enforcement was specifically **negatively tested** for one invalid EP URI.
- **Evidence:** Successful HTTP responses and AQL results were observed in the interactive test session. Request JSON artifacts and an AQL query catalogue were prepared, full raw server-side GET/POST/AQL response exports were **not independently established as a complete archive** and must not be claimed as such. See the T5 evidence manifest for the exact available artifacts.
- **Comparative scope:** The complete eight clinician-centred functional requirements and six architectural criteria have not yet been systematically scored across all five scenarios.

**T5 conclusion: PASS within tested scope.** EHRbase 2.30.1 successfully persisted and retrieved all 15 reference COMPOSITIONs and the 33 logical relationships represented through archetyped ENTRY-level CLUSTERs. AQL reconstructed longitudinal episode and contact views, Associated episode observations, and both complete SOAP notes without clinical content duplication. A separate negative test demonstrated that a non-existent Episode of Care reference can be accepted, persisted, and queried in the tested configuration. This provides concrete evidence for the need to distinguish semantic relationship modeling from enforced referential integrity.

## Summary of Results

**Summary:** Baseline validation: 30/30 PASS. Preliminary FOLDER feasibility T0: PASS (T0.1–T0.3). T1 Basic FOLDER: core relationship operations PASS, complete clinician-centred view reconstruction PARTIALLY VERIFIED. Extended FOLDER semantic-role exploration: persistence/retrieval demonstrated, systematic evaluation incomplete. T2 LINK: 33 LINKs persisted/retrieved, 19 Primary and 5 Associated episode assignments verified in the synthetic dataset, and all 12 EP2 ENTRYs retrieved and manually assembled into a chronological view (PASS within scope), native dereferencing and automated assembly NOT VERIFIED. T3 LINK: 15 COMPOSITIONs, 33 LINKs (9 encounter, 19 Primary, 5 Associated) verified, EP2 six documents across two encounters, EP3 two and EP4 three associated observations, PASS within tested scope. T4 CLUSTER: 15 COMPOSITIONs and 33 CLUSTER-held references (9 CE→MR, 19 Primary and 5 Associated EP→ENTRY) verified, 16 persisted JSON versions archived including historical CE2 ::1, clinical SOAP, episode and diagnosis views reconstructed (PASS within tested scope). T5 CLUSTER: 15 reference COMPOSITIONs, 19 clinical ENTRYs, 33 logical relationships (9 MR→CE, 19 Primary and 5 Associated ENTRY→EP) represented by 43 persisted URI occurrences, twelve AQL queries and independent EP2 GET verified episode/contact/SOAP views. RI-01–RI-04 demonstrated acceptance, persistence and AQL retrieval of a reference to a non-existent EP in one additional test COMPOSITION (PASS within tested scope). The five scenarios represent three patterns (FOLDER, LINK, CLUSTER), not five patterns. The full eight clinician-centred functional requirements and six architectural criteria remain to be evaluated comparatively. R03 (Clinical Section FOLDER → ENTRY) remained OUT OF SCOPE under DOC-03 and was not implemented or tested, the conceptual figure does not constitute implementation evidence.
