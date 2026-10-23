# Clinical Relationship Specification

**Status:** Implementation-independent clinical relationship specification for the synthetic dataset. The corresponding FOLDER, LINK, and CLUSTER scenarios T1–T5 were executed within their documented test scopes. See [PoC Results](DOC-04-poc-results.md) for evidence, qualifications, and remaining limitations.

## 1. Objective and Scope

This document defines the implementation-independent clinical relationships among Care Encounter COMPOSITIONs (CE1–CE2), Episode of Care COMPOSITIONs (EP1–EP4), and Medical Record COMPOSITIONs (MR1–MR9). The clinical content and templates are documented in DOC-01. The technical relationship requirements R01–R15 and test scenarios T1–T5 are defined in DOC-03. Results are documented in DOC-04.

**Identifier convention:** `CR-001`–`CR-027` identify individual *clinical* relationships in this document. They are independent of technical requirements `R01`–`R15`. These identifiers do not prescribe reference direction, serialization, or the number of stored technical references.

## 2. Clinical Relationship Principles

The clinical relationships follow the episode-oriented medical record concept described by Solon and reflected in Dutch episode-oriented practice. The following principles define the clinical reference for all three implementation patterns.

### 2.1 Care Encounter Assignment

Each Medical Record COMPOSITION (MR1–MR9) belongs to exactly one Care Encounter COMPOSITION (CE1 or CE2). This clinical context relationship is defined at the COMPOSITION level, regardless of when the information was documented or persisted.

### 2.2 Episode of Care Assignment

Each clinical ENTRY must be assigned to an Episode of Care:

- **Primary:** Exactly one Primary Episode of Care per clinical ENTRY.
- **Associated:** Zero, one, or multiple additional Associated Episodes of Care may be assigned.
- **Default:** If no specific Episode of Care applies as the primary clinical context, *General Health Problem* (EP1) serves as the Default Episode of Care.
- **Granularity:** Episode assignments apply at the clinical ENTRY level. ENTRYs within the same Medical Record COMPOSITION may have different assignments.

Each Episode of Care is represented by a COMPOSITION. EP1 is a default rather than a parent or umbrella episode. No Episode-to-Episode relationships are specified or tested in this PoC.

### 2.3 SOAP Progress Note Integrity

Each SOAP progress note (MR4 and MR8) is **one indivisible clinical documentation unit**, technically modeled as four `OBSERVATION.progress_note.v1` ENTRYs (Subjective, Objective, Assessment, Plan) within `SECTION.soap.v0`. All four technical ENTRYs must share the same Primary Episode of Care assignment and any Associated Episode of Care assignments. The note must not be split across episodes or duplicated.

This is a clinical invariant of the reference specification, not a constraint demonstrated to be enforced automatically by the openEHR server. In implementations that store the episode assignment separately for each technical SOAP ENTRY, the application or a dedicated validation process must ensure that the four assignments remain consistent when the note is created or updated. The T5 AQL results document matching assignments in the tested SOAP notes, but they do not establish server-side enforcement of this invariant. See [T5 Test Results](05-cluster-pattern/T5/T5-cluster-test-results.md).

### 2.4 Implementation-Pattern Independence

FOLDER, LINK, and CLUSTER are evaluated against the **same clinical relationships**. Technical reference direction, granularity, role representation, persistence, and retrieval may differ. Any inability to preserve the specified relationships must be reported as an evaluation result rather than resolved by changing the clinical specification. Multiple episode associations must not duplicate the underlying clinical information.

### Episode Identifiers

| ID | Episode of Care | Role in the synthetic dataset |
| --- | --- | --- |
| EP1 | General Health Problem | Default Episode of Care |
| EP2 | Urinary Tract Infection | Specific Episode of Care |
| EP3 | Arterial Hypertension | Specific Episode of Care |
| EP4 | Obesity WHO Grade I | Specific Episode of Care |

## 3. Clinical Relationship Matrix

The matrix defines clinical associations independently of their FOLDER, LINK, or CLUSTER representation. Each Medical Record COMPOSITION **belongs to** the Care Encounter COMPOSITION identified in its rows. Episode assignments apply to clinical ENTRYs: **P** = Primary, **A** = Associated, **–** = no relationship. EP1 (*General Health Problem*) is the Default Episode of Care when no specific episode applies as the primary clinical context.

| Medical Record | Clinical ENTRY / Unit | Clinical / Technical Granularity | Care Encounter | EP1 | EP2 | EP3 | EP4 |
| --- | --- | --- | --- | :---: | :---: | :---: | :---: |
| MR1 | Blood Pressure | 1 clinical unit / 1 ENTRY | CE1 | P | – | A | – |
| MR1 | Pulse | 1 clinical unit / 1 ENTRY | CE1 | P | – | – | – |
| MR2 | Height | 1 clinical unit / 1 ENTRY | CE1 | P | – | – | A |
| MR2 | Weight | 1 clinical unit / 1 ENTRY | CE1 | P | – | – | A |
| MR2 | BMI | 1 clinical unit / 1 ENTRY | CE1 | P | – | – | A |
| MR3 | Urinalysis | 1 clinical unit / 1 ENTRY | CE1 | – | P | – | – |
| MR4 | SOAP Progress Note (S/O/A/P) | 1 clinical unit / 4 ENTRYs | CE1 | – | P | – | – |
| MR5 | Medication Order | 1 clinical unit / 1 ENTRY | CE1 | – | P | – | – |
| MR6 | Microbiology Result | 1 clinical unit / 1 ENTRY | CE2 | – | P | – | – |
| MR7 | Blood Pressure | 1 clinical unit / 1 ENTRY | CE2 | P | – | A | – |
| MR7 | Pulse | 1 clinical unit / 1 ENTRY | CE2 | P | – | – | – |
| MR8 | SOAP Progress Note (S/O/A/P) | 1 clinical unit / 4 ENTRYs | CE2 | – | P | – | – |
| MR9 | Medication Order | 1 clinical unit / 1 ENTRY | CE2 | – | P | – | – |

The Care Encounter association applies to the whole Medical Record COMPOSITION. For MR4 and MR8, all four technical SOAP ENTRYs share the relationship of the single clinical note. Multiple Episode of Care associations do not imply duplication of clinical information.

## 4. Detailed Clinical Relationship Register

### 4.1 Care Encounter relationships (CR-001–CR-009)

Each Medical Record COMPOSITION **belongs to** exactly one Care Encounter COMPOSITION. All relationships have **COMPOSITION**-level source and target granularity and identify clinical context independently of documentation or persistence time.

| Clinical relationship ID | Source COMPOSITION | Target Care Encounter COMPOSITION | Clinical meaning |
| --- | --- | --- | --- |
| CR-001 | MR1 | CE1 | Belongs to |
| CR-002 | MR2 | CE1 | Belongs to |
| CR-003 | MR3 | CE1 | Belongs to |
| CR-004 | MR4 | CE1 | Belongs to |
| CR-005 | MR5 | CE1 | Belongs to |
| CR-006 | MR6 | CE2 | Belongs to |
| CR-007 | MR7 | CE2 | Belongs to |
| CR-008 | MR8 | CE2 | Belongs to |
| CR-009 | MR9 | CE2 | Belongs to |

### 4.2 Episode of Care relationships (CR-010–CR-027)

Unless otherwise noted, the clinical source is an **ENTRY** within the named Medical Record COMPOSITION and the target is an **Episode of Care COMPOSITION**. Each SOAP row represents **one clinical relationship**, expanded into four ENTRY-level references where required by the implementation mechanism.

| Clinical relationship ID | Source COMPOSITION | Clinical ENTRY / unit | Clinical / Technical Granularity | Target Episode of Care COMPOSITION | Role |
| --- | --- | --- | --- | --- | --- |
| CR-010 | MR1 | Blood Pressure | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-011 | MR1 | Blood Pressure | 1 clinical unit / 1 ENTRY | EP3 | Associated |
| CR-012 | MR1 | Pulse | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-013 | MR2 | Height | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-014 | MR2 | Height | 1 clinical unit / 1 ENTRY | EP4 | Associated |
| CR-015 | MR2 | Weight | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-016 | MR2 | Weight | 1 clinical unit / 1 ENTRY | EP4 | Associated |
| CR-017 | MR2 | BMI | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-018 | MR2 | BMI | 1 clinical unit / 1 ENTRY | EP4 | Associated |
| CR-019 | MR3 | Urinalysis | 1 clinical unit / 1 ENTRY | EP2 | Primary |
| CR-020 | MR4 | SOAP progress note (S/O/A/P) | 1 clinical unit / 4 ENTRYs | EP2 | Primary |
| CR-021 | MR5 | Medication Order | 1 clinical unit / 1 ENTRY | EP2 | Primary |
| CR-022 | MR6 | Microbiology Result | 1 clinical unit / 1 ENTRY | EP2 | Primary |
| CR-023 | MR7 | Blood Pressure | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-024 | MR7 | Blood Pressure | 1 clinical unit / 1 ENTRY | EP3 | Associated |
| CR-025 | MR7 | Pulse | 1 clinical unit / 1 ENTRY | EP1 | Primary |
| CR-026 | MR8 | SOAP progress note (S/O/A/P) | 1 clinical unit / 4 ENTRYs | EP2 | Primary |
| CR-027 | MR9 | Medication Order | 1 clinical unit / 1 ENTRY | EP2 | Primary |

### 4.3 Relationship Counts and Technical Granularity

| Category | Clinical relationships |
| --- | ---: |
| Care Encounter assignments (COMPOSITION → COMPOSITION) | 9 |
| Episode of Care assignments — Primary | 13 |
| Episode of Care assignments — Associated | 5 |
| **Total clinical relationships** | **27** |

The 18 clinical Episode of Care relationships refer to 13 clinical documentation units represented by 19 technical ENTRYs. Each SOAP note (CR-020 and CR-026) counts as one clinical relationship and contains four technical ENTRYs.

| Episode assignment | Clinical relationships | ENTRY-level assignments |
| --- | ---: | ---: |
| Primary | 13 | 19 |
| Associated | 5 | 5 |
| **Total** | **18** | **24** |

Together with nine Care Encounter relationships, these represent 33 logical assignments at expanded ENTRY granularity. This count does not predict the number of physical references. Each pattern may use different structures and additional reverse-direction references.

## 5. Mapping to Technical Requirements

The clinical relationships `CR-001–CR-027` are implementation-independent. The technical mechanisms and test scenarios are specified in [DOC-03](DOC-03-poc-plan.md). Their requirement IDs and definitions remain unchanged. The mapping below identifies mechanisms to **evaluate**, not demonstrated capabilities.

| Pattern | Test scenarios | Care Encounter relationships (CR-001–CR-009) | Episode of Care relationships (CR-010–CR-027) |
| --- | --- | --- | --- |
| FOLDER | T1 | R01, R02 | R04, R05 |
| LINK | T2, T3 | R06, R07 | R08, R09 |
| CLUSTER | T4, T5 | R10, R12 | R13, R14 |

### 5.1 FOLDER (T1)

R01 identifies the CE COMPOSITION through the Contact FOLDER, while R02 associates clinical COMPOSITIONs with that folder. R04 identifies the EoC COMPOSITION through the EoC FOLDER, and R05 associates individual clinical ENTRYs with it. R03 (Clinical Section FOLDER → Clinical ENTRY) is OUT OF SCOPE and is not evaluated. Evaluate ENTRY-level targeting and whether Primary and Associated roles remain distinguishable.

### 5.2 LINK (T2–T3)

R06 and R07 represent Care Encounter associations in opposite technical reference directions. R08 and R09 likewise represent Episode of Care associations in opposite directions. Evaluate target granularity, role preservation, retrieval, and relationship maintenance. Creation order alone does not determine the stored reference direction. The applicable scenario in [DOC-03](DOC-03-poc-plan.md) specifies that direction.

### 5.3 CLUSTER (T4–T5)

R10 represents the Care Encounter relationship at the COMPOSITION-to-COMPOSITION level. R12 represents the same clinical association using ENTRY-to-CE-COMPOSITION references. If R12 is used, all ENTRYs in a Medical Record COMPOSITION must resolve to its **single** designated Care Encounter. R13 and R14 represent Episode of Care relationships in opposite reference directions. Evaluate reference granularity, role preservation, and reconstruction.

**Out of scope:** R03 (Clinical Section), R11 (Administrative Encounter), and R15 (Episode-to-Episode relationships) are OUT OF SCOPE. EP1 is a Default Episode of Care, not a parent of EP2–EP4.

## 6. Validation Criteria

The clinical relationships defined here serve as the reference for evaluating T1–T5. Each pattern is assessed against the same relationships (`CR-001–CR-027`), regardless of its technical mechanism.

1. **Care Encounter assignment:** Each Medical Record COMPOSITION belongs to exactly one Care Encounter COMPOSITION, as specified in the matrix.
2. **Episode of Care assignment:** Each clinical ENTRY has exactly one Primary Episode of Care and zero or more Associated Episodes of Care, matching the matrix.
3. **Relationship granularity:** Episode assignments are distinguishable at ENTRY level, including differing assignments within one Medical Record COMPOSITION.
4. **SOAP integrity:** The four technical ENTRYs of each SOAP note share the same Episode of Care assignments and remain one clinical documentation unit.
5. **Relationship semantics:** Primary and Associated roles remain distinguishable. Multiple episode associations do not duplicate clinical information.
6. **Persistence and retrieval:** Relationships can be persisted, retrieved, and used to reconstruct the intended Care Encounter and Episode of Care views.

Any technical limitations must be documented as evaluation results rather than changes to the clinical specification. Results must be traceable to the test scenario (`T1–T5`), clinical relationship (`CR-001–CR-027`), and applicable technical requirement (`R01–R15`). Baseline COMPOSITION validation is not relationship validation.
