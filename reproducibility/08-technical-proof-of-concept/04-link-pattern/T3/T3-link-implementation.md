# T3 — LINK implementation (context COMPOSITIONs first)

## Objective and difference from T2

T3 implements the LINK pattern with the opposite creation order and link direction from T2. The two Care Encounter (CE1, CE2) and four Episode-of-Care (EP1–EP4) COMPOSITIONs are persisted first. Subsequently, nine Medical Record (MR1–MR9) COMPOSITIONs are persisted with outgoing LINKs to existing context COMPOSITIONs. In T2, CE/EP COMPOSITIONs contain LINKs to MR COMPOSITIONs or clinical ENTRYs. In T3, each MR COMPOSITION contains an encounter LINK, and its clinical ENTRYs contain episode LINKs. The two scenarios use isolated EHRs, and their identifiers must not be interchanged.

## Model

- `COMPOSITION.links` on each MR: one `LINK.type.value = encounter`, with a `DV_EHR_URI` target referencing CE1 or CE2.
- `ENTRY.links` on each clinical OBSERVATION or INSTRUCTION: one `episode-of-care-primary` LINK referencing an EP COMPOSITION.
- Optional `episode-of-care-associated` LINKs represent clinically relevant secondary episode associations (MR1/MR7 blood pressure → EP3, and MR2 height, weight, and BMI → EP4).
- EP1 General Health Problem serves as a default assignment, not as a hierarchical parent of EP2–EP4.
- `LINK.meaning.value` is `documents` for encounter associations and `is related to the same episode` for episode assignments.
- LINK target format: `ehr://<ehr_id>/<composition_uuid>::local.ehrbase.org::1`.

## Clinical unit versus technical ENTRY

Each SOAP COMPOSITION (MR4 and MR8) contains a `SECTION.soap.v0` with four child sections (S/O/A/P), each containing one `OBSERVATION.progress_note.v1`. Clinically, each SOAP note is one indivisible document, and all four technical ENTRYs are assigned to the same primary episode, EP2, in this implementation. The ENTRY `uid` is absent (optional in the Reference Model). The `archetype_node_id` identifies an archetype node, not a unique ENTRY instance. View assembly must therefore account for the COMPOSITION UID and section structure rather than treating the four ENTRYs as independent clinical notes.

## Creation and validation

1. Create isolated EHR `f4908498-afef-4e3c-8cc4-bbdf16d808bf`.
2. Persist CE1–CE2 and EP1–EP4 as six context COMPOSITIONs.
3. Persist MR1–MR9 with outgoing encounter and episode LINKs. The nine MR POST requests returned HTTP 201, and subsequent independent GET requests returned HTTP 200.
4. Use AQL to inventory 15 COMPOSITIONs and retrieve nine `COMPOSITION.links` rows, 22 OBSERVATION-level LINK rows, and two INSTRUCTION-level LINK rows. Compare the results with persisted JSON to inspect primary-assignment uniqueness per ENTRY.
5. Retrieve episode-oriented clinical content through inverse searches on `ENTRY.links/target/value`, joining the containing COMPOSITION's encounter LINK within the same AQL query. This demonstrates application-driven retrieval, not automatic target dereferencing or a fully implemented clinical-view service.

## Evidence limits

The documented operations demonstrate storage, retrieval, and AQL filtering in the tested EHRbase 2.30.1 environment. They do not establish automatic resolution or validation of `DV_EHR_URI` targets, repository-enforced uniqueness of primary episode assignments, preservation of LINK targets across all subsequent versions, or implementation of clinical-view assembly as a service. The clinical correctness of coded microbiology interpretation values remains subject to independent terminology verification.
