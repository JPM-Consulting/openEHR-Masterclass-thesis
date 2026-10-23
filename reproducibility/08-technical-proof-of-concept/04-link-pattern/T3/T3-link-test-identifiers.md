# T3: Identifiers and Relationship Inventory

EHR ID: `f4908498-afef-4e3c-8cc4-bbdf16d808bf`. EHRbase system: `local.ehrbase.org`. All listed COMPOSITION versions are `::1` and represent the documented T3 test state.

## Complete COMPOSITION Identifier Register

| Item | Versioned COMPOSITION UID | LINK target URI |
|---|---|---|
| CE1 | `a942e76a-471d-4e43-9d8b-e9318c2c0498::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/a942e76a-471d-4e43-9d8b-e9318c2c0498::local.ehrbase.org::1` |
| CE2 | `4612e7a1-047a-466c-a5bf-42be2711f044::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/4612e7a1-047a-466c-a5bf-42be2711f044::local.ehrbase.org::1` |
| EP1 | `25e56fbc-9c74-4c6e-8ce9-a3e97a0250b1::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/25e56fbc-9c74-4c6e-8ce9-a3e97a0250b1::local.ehrbase.org::1` |
| EP2 | `12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1` |
| EP3 | `4e2fa228-1857-4a60-9cc1-53a6d7f54a00::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/4e2fa228-1857-4a60-9cc1-53a6d7f54a00::local.ehrbase.org::1` |
| EP4 | `50a0b2b8-9a3c-46f5-b802-0b634f75415b::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/50a0b2b8-9a3c-46f5-b802-0b634f75415b::local.ehrbase.org::1` |
| MR1 | `74b167c9-faa7-4716-b653-c0644b85b9f5::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/74b167c9-faa7-4716-b653-c0644b85b9f5::local.ehrbase.org::1` |
| MR2 | `c93029ec-3295-4a70-bd4d-37d5d010d029::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/c93029ec-3295-4a70-bd4d-37d5d010d029::local.ehrbase.org::1` |
| MR3 | `75462d29-d528-4991-8543-42ee971cab25::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/75462d29-d528-4991-8543-42ee971cab25::local.ehrbase.org::1` |
| MR4 | `7f2afe1e-9c14-4f36-88e1-e3edb5d50c4f::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/7f2afe1e-9c14-4f36-88e1-e3edb5d50c4f::local.ehrbase.org::1` |
| MR5 | `8817d768-f57a-48ae-a1a3-768f89db6ed9::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/8817d768-f57a-48ae-a1a3-768f89db6ed9::local.ehrbase.org::1` |
| MR6 | `1f0eaddc-8750-4fe0-a4a8-3162fa2383a3::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/1f0eaddc-8750-4fe0-a4a8-3162fa2383a3::local.ehrbase.org::1` |
| MR7 | `475ea309-9de7-4033-9589-24fa6a84aa7a::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/475ea309-9de7-4033-9589-24fa6a84aa7a::local.ehrbase.org::1` |
| MR8 | `f0116bb9-2067-431f-b3c2-6c0fab9d9e09::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/f0116bb9-2067-431f-b3c2-6c0fab9d9e09::local.ehrbase.org::1` |
| MR9 | `0f7b9524-7308-4321-8e6f-6cd23aad9d22::local.ehrbase.org::1` | `ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/0f7b9524-7308-4321-8e6f-6cd23aad9d22::local.ehrbase.org::1` |

## Medical Record Relationships

| MR | Clinical document | Encounter | Versioned UID | ENTRYs | Primary EP LINKs | Associated EP LINKs | Total LINKs incl. encounter | Status |
|---|---|---|---|---:|---:|---:|---:|---|
| MR1 | Vital Signs | CE1 | `74b167c9-faa7-4716-b653-c0644b85b9f5::local.ehrbase.org::1` | 2 | 2 | 1 | 4 | PASS |
| MR2 | Body Measurements | CE1 | `c93029ec-3295-4a70-bd4d-37d5d010d029::local.ehrbase.org::1` | 3 | 3 | 3 | 7 | PASS |
| MR3 | Urinalysis | CE1 | `75462d29-d528-4991-8543-42ee971cab25::local.ehrbase.org::1` | 1 | 1 | 0 | 2 | PASS |
| MR4 | SOAP Progress Note | CE1 | `7f2afe1e-9c14-4f36-88e1-e3edb5d50c4f::local.ehrbase.org::1` | 4 | 4 | 0 | 5 | PASS |
| MR5 | Medication Order | CE1 | `8817d768-f57a-48ae-a1a3-768f89db6ed9::local.ehrbase.org::1` | 1 | 1 | 0 | 2 | PASS |
| MR6 | Microbiology Result | CE2 | `1f0eaddc-8750-4fe0-a4a8-3162fa2383a3::local.ehrbase.org::1` | 1 | 1 | 0 | 2 | PASS |
| MR7 | Vital Signs | CE2 | `475ea309-9de7-4033-9589-24fa6a84aa7a::local.ehrbase.org::1` | 2 | 2 | 1 | 4 | PASS |
| MR8 | SOAP Progress Note | CE2 | `f0116bb9-2067-431f-b3c2-6c0fab9d9e09::local.ehrbase.org::1` | 4 | 4 | 0 | 5 | PASS |
| MR9 | Medication Order | CE2 | `0f7b9524-7308-4321-8e6f-6cd23aad9d22::local.ehrbase.org::1` | 1 | 1 | 0 | 2 | PASS |

The documented inventory contains 9 encounter LINKs, 19 primary episode LINKs, and 5 associated episode LINKs, totaling 33 technical LINK instances across 19 technical ENTRYs. The primary episode LINKs comprise 7 for EP1 and 12 for EP2. The associated episode LINKs comprise 2 for EP3 and 3 for EP4. These counts describe technical LINK instances rather than distinct clinical documents or independent clinical relationships.

## Explicit Episode Distribution

| Episode | Clinical ENTRYs / records | Relationship type |
|---|---|---|
| EP1 — General Health Problem | MR1 blood pressure and pulse, MR2 height, weight, and BMI, and MR7 blood pressure and pulse (7 technical ENTRYs) | primary |
| EP2 — Urinary Tract Infection | MR3 urinalysis (1), MR4 SOAP S/O/A/P (4), MR5 medication (1), MR6 microbiology (1), MR8 SOAP S/O/A/P (4), and MR9 medication (1). Total: 12 technical ENTRYs in 6 clinical documents | primary |
| EP3 — Arterial Hypertension | MR1 blood pressure and MR7 blood pressure (2) | associated |
| EP4 — Obesity | MR2 height, body weight, BMI (3) | associated |

## Chronological EP2 Clinical Documents

| Care Encounter | Date (+01:00) | Documents | Count |
|---|---|---|---:|
| CE1 | 2024-11-15 09:00 | MR3 Urinalysis, MR4 SOAP, MR5 Medication Order | 3 |
| CE2 | 2024-11-17 09:00 | MR6 Microbiology, MR8 SOAP, MR9 Medication Order | 3 |

Ordering within a shared timestamp is not guaranteed by `ORDER BY start_time` alone. The six documents are distinct COMPOSITIONs. The 12 technical ENTRYs do not represent 12 independent clinical documents. Each SOAP progress note remains one clinical unit despite its four technical ENTRYs.
