# Technical Proof-of-Concept Plan

**Status:** Technical test plan for scenarios T1–T5. All five scenarios were executed within their documented test scopes. T1 clinical-view reconstruction remains partially verified. This plan specifies the procedures and acceptance criteria. Actual execution results, deviations, and evidence boundaries are documented in [PoC Results](DOC-04-poc-results.md).

## Objective and Scope

The technical proof of concept (PoC) was designed to implement and evaluate three alternative patterns for representing relationships between Care Encounters, Episodes of Care, and Medical Record Entries in openEHR:

1. **FOLDER-based pattern:** Relationships are represented through the openEHR FOLDER structure.
2. **LINK-based pattern:** Relationships are represented using the openEHR Reference Model’s LINK mechanism.
3. **CLUSTER-based pattern:** Relationships are represented using dedicated archetyped CLUSTER structures.

The PoC focuses on the technical implementation, persistence, maintenance, and retrieval of these relationships.

The clinical information is based on the same synthetic patient medical history, comprising two Care Encounters, four Episodes of Care, and the associated Medical Record Entries. The three patterns were evaluated using identical clinical content and the same predefined relationship assignments.

The PoC does not aim to evaluate the completeness of clinical documentation, terminology interoperability, or clinical decision support. See [PoC Scenario](DOC-01-poc-scenario.md) for the clinical dataset and templates.

## General Test Principles

### Isolated EHR Environments

Each test scenario was performed using a newly created, initially empty EHR representing a synthetic patient. This separation prevents clinical information or relationships persisted in one scenario from affecting another.

| Test | EHR | Pattern | Implementation scenario |
| --- | --- | --- | --- |
| T1 | Patient 1 | FOLDER | Create clinical COMPOSITIONs and subsequently establish FOLDER relationships |
| T2 | Patient 2 | LINK | Medical Record Entries first, followed by Care Encounters and Episodes of Care |
| T3 | Patient 3 | LINK | Care Encounters and Episodes of Care first, followed by Medical Record Entries |
| T4 | Patient 4 | CLUSTER | Medical Record Entries first, followed by Care Encounters and Episodes of Care |
| T5 | Patient 5 | CLUSTER | Care Encounters and Episodes of Care first, followed by Medical Record Entries |

Each test uses a separate EHR-ID.

### Identical Clinical Dataset

All five scenarios use the same synthetic clinical dataset:

- Two Care Encounters: November 15 and November 17, 2024.
- Four Episodes of Care: General health problem, urinary tract infection, arterial hypertension, and obesity WHO grade I.
- Medical Record Entries covering vital signs, body measurements, urinalysis, microbiology results, medication orders, and SOAP progress notes.

The clinical content, timestamps, and intended episode assignments remain consistent across all scenarios. The FOLDER pattern represents episode membership without explicitly encoding Primary/Associated roles. The role distinction is evaluated only where the selected relationship mechanism represents it. The FOLDER and LINK patterns use the same clinical templates and COMPOSITION structures. The CLUSTER pattern uses separate template variants incorporating the archetyped relationship structures. The clinical data elements themselves remain identical.

### Relationship Requirements

The implementation must support the relationships illustrated in the implementation-pattern diagrams (Figures 3–6). The table specifies each relationship by its source, target, reference mechanism, and target granularity (COMPOSITION or ENTRY).

| ID | Pattern | Source | Target | Relationship / Reference mechanism | Target level | PoC scope |
| --- | --- | --- | --- | --- | --- | --- |
| R01 | FOLDER | Contact FOLDER | Care Encounter COMPOSITION | `details` | COMPOSITION | IN SCOPE |
| R02 | FOLDER | Contact FOLDER | Clinical COMPOSITION | `items` | COMPOSITION | IN SCOPE |
| R03 | FOLDER | Clinical Section FOLDER | Clinical ENTRY | `details` | ENTRY | OUT OF SCOPE |
| R04 | FOLDER | Episode of Care FOLDER | Episode of Care COMPOSITION | `details` | COMPOSITION | IN SCOPE |
| R05 | FOLDER | Episode of Care FOLDER | Clinical ENTRY | `details` | ENTRY | IN SCOPE |
| R06 | LINK | Care Encounter COMPOSITION | Clinical COMPOSITION | `LINK-E1` — documented by | COMPOSITION | IN SCOPE |
| R07 | LINK | Clinical COMPOSITION | Care Encounter COMPOSITION | `LINK-E1i` — documents | COMPOSITION | IN SCOPE |
| R08 | LINK | Clinical ENTRY | Episode of Care COMPOSITION | `LINK-DO` — primary / associated | COMPOSITION | IN SCOPE |
| R09 | LINK | Episode of Care COMPOSITION | Clinical ENTRY | `LINK-DO` — primary / associated | ENTRY | IN SCOPE |
| R10 | CLUSTER | Care Encounter COMPOSITION | Clinical COMPOSITION | Clinical COMPOSITION references | COMPOSITION | IN SCOPE |
| R11 | CLUSTER | Care Encounter COMPOSITION | Administrative Encounter | Administrative Encounter reference | COMPOSITION | OUT OF SCOPE |
| R12 | CLUSTER | Clinical ENTRY | Care Encounter COMPOSITION | Care Encounter reference | COMPOSITION | IN SCOPE |
| R13 | CLUSTER | Clinical ENTRY | Episode of Care COMPOSITION | Episode reference (Link + Role) | COMPOSITION | IN SCOPE |
| R14 | CLUSTER | Episode of Care COMPOSITION | Clinical ENTRY | Clinical ENTRY references | ENTRY | IN SCOPE |
| R15 | CLUSTER | Episode of Care COMPOSITION | Related Episode of Care COMPOSITION | Related Episode references | COMPOSITION | OUT OF SCOPE |

**PoC scope clarification**

- **Clinical Section FOLDER organization (OUT OF SCOPE):** The PoC evaluates Care Encounter and Episode of Care relationships only. This does not exclude openEHR `SECTION` structures within clinical COMPOSITIONs (for example `SECTION.soap.v0`).
- **R03 (OUT OF SCOPE):** Clinical Section FOLDER → Clinical ENTRY references are not implemented or evaluated.

- **R11 (OUT OF SCOPE):** Administrative Encounter references are not evaluated. No separate Administrative Encounter objects are included in the synthetic PoC dataset.
- **R15 (OUT OF SCOPE):** Although the underlying `CLUSTER.eoc_relationships_episode_of_care.v0` archetype provides elements for relationships between Episodes of Care (including primary diagnosis, complication, and recurrence references), these elements were deliberately excluded from the Episode of Care template used in this PoC. Episode-to-Episode relationships are therefore not implemented or evaluated.
- **R01–R02, R04–R10, and R12–R14 (IN SCOPE):** These 12 requirements define the relationship mechanisms evaluated in T1–T5.

Clinical assignment principle (clinical specification, not a universal storage requirement): Each clinical ENTRY has exactly one Primary Episode of Care and may have zero or more Associated Episodes of Care. EP1 (General Health Problem) is the Default Episode of Care when no specific episode applies as the primary clinical context. It is not a parent grouping of other episodes. For the blood pressure ENTRYs in MR1 and MR7, the intended assignments are EP1 = Primary and EP3 (Arterial Hypertension) = Associated. The same clinical ENTRY must be referenced without duplication. The intended episode memberships apply across T1–T5. Explicit representation of the Primary/Associated distinction is not required for the Basic FOLDER implementation (T1), which follows Figure 3 and tests episode-to-ENTRY references. Role semantics are examined for LINK and CLUSTER where applicable; a CLUSTER-qualified FOLDER representation was explored separately and is not part of the evaluated T1 pattern. See DOC-02 for the complete clinical specification.

**Notes**

- The FOLDER pattern uses `items` for COMPOSITION references and `details` for additional COMPOSITION- and ENTRY-level references, as established in preliminary technical tests.
- The LINK pattern distinguishes two directions of stored references. These are evaluated separately in T2 and T3.
- The CLUSTER pattern uses dedicated archetyped relationship structures at Care Encounter, Episode of Care, and Medical Record ENTRY level.
- Primary and associated Episode-of-Care relationships must remain distinguishable **where the evaluated pattern explicitly represents these roles**. T1 tests episode membership without encoding the role in its FOLDER references.
- The table specifies the intended relationship structures. Their systematic persistence, retrieval, and use in reconstructing clinical views are evaluated in T1–T5.

**Reference diagrams:** Figures 3–6 of *Frontiers figures V3* (FOLDER, LINK Care Encounter, LINK Episode of Care, and CLUSTER). The figures are referenced by their manuscript numbering.

### Persistence and Retrieval

For each scenario, the following operations are documented at the level needed to support the evaluation:

- Creation and persistence of clinical COMPOSITIONs.
- Creation and persistence of relationship structures.
- Retrieval of persisted clinical information.
- Retrieval and reconstruction of relationships.
- Updates to existing objects, where required.
- Relevant version identifiers and version changes.

The resulting structures and retrieval results are compared across the three implementation patterns.

## Test Scenario T1 – FOLDER-Based Pattern

**Patient:** 1  
**Objective:** Evaluate the representation, retrieval, and maintenance of Care Encounter-to-COMPOSITION and Episode-of-Care-to-clinical-ENTRY relationships using the openEHR FOLDER structure, as depicted in Figure 3. Explicit Primary/Associated relationship roles are not part of the evaluated T1 representation.

**Execution identifier:** `8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b`  The execution results and deviations are documented in DOC-04.

**Procedure**

1. **Create EHR:** Create a new, empty EHR for Patient 1.
2. **Persist clinical information:** Create and persist all clinical COMPOSITIONs representing two Care Encounters, four Episodes of Care, and all Medical Record Entries. At this stage, no FOLDER-based relationships have been established.
3. **Establish FOLDER relationships:** After all 15 COMPOSITIONs have been persisted, construct the complete Care Encounter and Episode of Care FOLDER hierarchy and submit it in a single Directory API request. Exclude Clinical Section FOLDERs (R03). Investigate the reference granularity supported by FOLDER items. Do not assume ENTRY-level referencing where only COMPOSITION-level references are supported. Avoid duplication of underlying clinical information.
4. **Retrieve relationships:** Retrieve the FOLDER hierarchy and confirm that Care Encounter COMPOSITION references and Episode-of-Care clinical-content references are preserved. Independently retrieve selected referenced clinical ENTRYs and the SOAP SECTION through AQL. Distinguish targeted AQL retrieval from native `DV_EHR_URI` dereferencing.
5. **Maintain relationships:** Add an episode-to-ENTRY reference and subsequently remove it through versioned DIRECTORY updates. Verify the resulting hierarchy and that other episode assignments remain intact. Retrieve the original clinical COMPOSITION to check that clinical data are unchanged.
6. **Reconstruct clinical views:** Evaluate the feasibility of Care Encounter and Episode-of-Care views using the persisted relationships. Record any views not fully reconstructed rather than treating selective retrieval as full view reconstruction.
7. **Document results:** Record the FOLDER structure, object references, retrieval operations, version changes, and implementation constraints in DOC-04.

**Expected Result:** Clinical information can be organized and retrieved through the FOLDER structure without duplication of underlying COMPOSITIONs, subject to verified FOLDER reference semantics.

**Reference granularity and limitations:** The Basic FOLDER execution stores COMPOSITION references as `OBJECT_REF` entries in `FOLDER.items` and clinical ENTRY/SECTION references as `DV_EHR_URI` values in `FOLDER.details`. The latter are stored URI references, not demonstrated native dereferences. Identification of multiple occurrences of the same archetype within one COMPOSITION requires further investigation.

**Separate exploratory extension (not part of T1 evaluation):** An additional FOLDER representation placed a relationship CLUSTER in `FOLDER.details` to pair clinical references with `Primary`/`Associated` roles. Preliminary persistence and retrieval were demonstrated, but systematic maintenance, retrieval, and view-reconstruction tests were not completed. Its evidence belongs in the exploratory section of DOC-04 and any manuscript discussion/future work, not as a fourth implementation pattern.

## Test Scenarios T2 and T3 – LINK-Based Pattern

The LINK-based pattern is evaluated using two creation sequences to investigate how the direction of stored LINK relationships influences creation, maintenance, and retrieval.

### T2 – Medical Record Entries First

**Patient:** 2  
**Objective:** Evaluate the LINK-based pattern when Medical Record Entries are persisted before their Care Encounter and Episode-of-Care relationship structures.

**Procedure**

1. **Create EHR:** Create a new, empty EHR for Patient 2.
2. **Persist Medical Record Entries:** Create and persist all clinical Medical Record Entries using the FOLDER/LINK template variants.
3. **Persist Care Encounters:** Create two Care Encounter COMPOSITIONs and establish LINK relationships from Care Encounters to previously persisted Medical Record Entries.
4. **Persist Episodes of Care:** Create four Episode-of-Care COMPOSITIONs and establish LINK relationships from Episodes of Care to corresponding Medical Record Entries.
5. **Retrieve relationships:** Retrieve LINK relationships and reconstruct clinical information by Care Encounter and Episode of Care.
6. **Document results:** Document LINK structures, targets, persistence operations, and retrieval results.

**Expected Result:** Care Encounters and Episodes of Care can reference previously persisted Medical Record Entries using LINK relationships, which can be retrieved to reconstruct clinical views.

### T3 – Care Encounters and Episodes of Care First

**Patient:** 3  
**Objective:** Evaluate the LINK-based pattern when Care Encounters and Episodes of Care are created before associated Medical Record Entries.

**Procedure**

1. **Create EHR:** Create a new, empty EHR for Patient 3.
2. **Persist Care Encounters:** Create and persist two Care Encounter COMPOSITIONs.
3. **Persist Episodes of Care:** Create and persist four Episode-of-Care COMPOSITIONs.
4. **Persist Medical Record Entries:** Create clinical Medical Record Entries sequentially and establish LINK relationships from each Medical Record Entry to its corresponding Care Encounter and Episode of Care.
5. **Retrieve relationships:** Retrieve LINK relationships and reconstruct clinical information by Care Encounter and Episode of Care.
6. **Document results:** Document LINK structures, targets, persistence operations, and retrieval results.

**Expected Result:** Medical Record Entries can reference previously persisted Care Encounters and Episodes of Care using LINK relationships. The resulting clinical views should be equivalent to those obtained in T2, despite the different direction of stored references.

**Specific evaluation focus:** Reference direction, target existence, subsequent updates, versioning, retrieval complexity, and equivalence of clinical views.

**Technical clarification:** openEHR LINK relationships are directed. T2 and T3 evaluate opposite stored reference directions, not an automatically bidirectional mechanism.

## Test Scenarios T4 and T5 – CLUSTER-Based Pattern

The CLUSTER-based pattern is evaluated using two creation sequences. Relationship information is represented through dedicated archetyped CLUSTER structures:

- `CLUSTER.eoc_relationships_entry.v0`
- `CLUSTER.eoc_relationships_care_encounter.v0`
- `CLUSTER.eoc_relationships_episode_of_care.v0`

### T4 – Medical Record Entries First

**Patient:** 4  
**Objective:** Evaluate the CLUSTER-based pattern when Medical Record Entries are persisted before Care Encounter and Episode-of-Care relationship structures.

**Procedure**

1. **Create EHR:** Create a new, empty EHR for Patient 4.
2. **Persist Medical Record Entries:** Create and persist clinical Medical Record Entries using CLUSTER template variants. Corresponding Care Encounters and Episodes of Care do not yet exist, so references cannot initially resolve to persisted targets. Verify whether the template constraints permit this creation sequence and what incomplete relationship data, if any, can be stored.
3. **Persist Care Encounters:** Create and persist two Care Encounter COMPOSITIONs and establish archetyped relationships to previously persisted Medical Record Entries.
4. **Persist Episodes of Care:** Create and persist four Episode-of-Care COMPOSITIONs and establish archetyped relationships to corresponding Medical Record Entries.
5. **Complete relationship information:** Where required and permitted, update previously persisted COMPOSITIONs to establish or complete intended relationship structures.
6. **Retrieve relationships:** Retrieve relationship CLUSTERs and reconstruct clinical information by Care Encounter and Episode of Care.
7. **Document results:** Document archetyped relationship structures, persistence operations, version changes, and retrieval results.

**Expected Result:** Investigate whether the CLUSTER-based pattern can support this creation order and, if so, which additional updates are needed. A failed initial persistence due to mandatory references is a relevant result, not something to bypass without documentation.

### T5 – Care Encounters and Episodes of Care First

**Patient:** 5  
**Objective:** Evaluate the CLUSTER-based pattern when Care Encounters and Episodes of Care are persisted before associated Medical Record Entries.

**Procedure**

1. **Create EHR:** Create a new, empty EHR for Patient 5.
2. **Persist Care Encounters:** Create and persist two Care Encounter COMPOSITIONs.
3. **Persist Episodes of Care:** Create and persist four Episode-of-Care COMPOSITIONs.
4. **Persist Medical Record Entries:** Create and persist clinical Medical Record Entries sequentially using CLUSTER template variants. Each Medical Record Entry includes archetyped relationships referencing its Care Encounter, primary Episode of Care, additional associated Episodes of Care where applicable, as defined by the template.
5. **Retrieve relationships:** Retrieve relationship CLUSTERs and reconstruct clinical information by Care Encounter and Episode of Care.
6. **Document results:** Document archetyped relationship structures, persistence operations, version changes, and retrieval results.

**Expected Result:** Medical Record Entries can be persisted with explicitly modelled relationships to existing Care Encounters and Episodes of Care. The resulting clinical views should be equivalent to those obtained in T4 where T4 is technically feasible.

**Specific evaluation focus:** Reference direction, target existence, subsequent COMPOSITION updates, versioning, semantic explicitness, and retrieval complexity.

## Cross-Pattern Evaluation

Following the five scenarios, results are compared across the three implementation patterns.

### Functional Evaluation

Verify whether the eight predefined clinician-centred requirements can be fulfilled using persisted clinical information and relationship structures. This includes reconstruction by Care Encounter and Episode of Care, longitudinal health problems, and alternative views of the same clinical information without duplication.

### Architectural Evaluation

Examine the patterns using the six architectural criteria defined in the research methodology. Particular attention is given to relationship representation, semantic explicitness, implementation complexity, maintainability, and object creation and versioning.

T2/T3 and T4/T5 are consolidated at the pattern level. They do not constitute additional patterns.

## Documentation and Reproducibility

| Artefact | Description |
| --- | --- |
| EHR identifier | Unique identifier of the synthetic patient EHR |
| Templates | OPTs used for the scenario |
| COMPOSITION payloads | Canonical JSON submitted to EHRbase |
| COMPOSITION identifiers | Versioned COMPOSITION IDs |
| Relationship structures | FOLDER, LINK, or CLUSTER representation |
| API requests | Requests used for persistence and retrieval |
| API responses | Relevant EHRbase responses |
| AQL queries | Queries used to retrieve and reconstruct clinical information |
| Test results | Expected and actual outcomes |
| Observations | Implementation constraints, deviations, and limitations |

Technical artefacts are retained in the corresponding pattern directories. The concise execution tables and observations are maintained in [PoC Results](DOC-04-poc-results.md), without reproducing every request and response in prose.
