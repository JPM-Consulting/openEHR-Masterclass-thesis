# T5 – Test Identifiers

The documented T5 execution used EHR `16fe2926-c82a-462c-93f2-d5e67a29656f` and system identifier `local.ehrbase.org`. The following versioned COMPOSITION UIDs represent the recorded execution state (`::1`). They are not assertions about the current state of a subsequently modified EHR.

| Object | Versioned COMPOSITION UID |
|---|---|
| CE1 | `6617f878-b798-4422-979f-524d44dc1385::local.ehrbase.org::1` |
| CE2 | `bd0bb285-e61d-411b-8c4f-d06a05b53ba6::local.ehrbase.org::1` |
| EP1 | `78967a71-271e-462f-ae85-2bfcaba1768e::local.ehrbase.org::1` |
| EP2 | `c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1` |
| EP3 | `364fa3f4-acba-4b9b-9c5c-4feb0f5cbff3::local.ehrbase.org::1` |
| EP4 | `3af7b6c8-ae69-481a-b01c-31e804be99bc::local.ehrbase.org::1` |
| MR1 | `9a500145-37ec-4710-b573-6fabf11b42a0::local.ehrbase.org::1` |
| MR2 | `86603afd-080c-46df-af9b-9c7f8b7b02e0::local.ehrbase.org::1` |
| MR3 | `8e457025-3785-40ef-9e47-117c09f4d803::local.ehrbase.org::1` |
| MR4 | `69dd2dcd-9211-4b23-92d0-038cc2c450fe::local.ehrbase.org::1` |
| MR5 | `4eb9ce0f-1911-4638-aadc-287e34e62335::local.ehrbase.org::1` |
| MR6 | `27bbcc6e-d6a9-4e49-a155-fc4b2bfce0ff::local.ehrbase.org::1` |
| MR7 | `8754b7f5-8cc9-4fb6-885e-e7d37a313fbe::local.ehrbase.org::1` |
| MR8 | `6b11b73e-7536-4399-9406-644a54a0d2cb::local.ehrbase.org::1` |
| MR9 | `eda7279d-6e66-4efc-bdc5-96e6e1d2bf76::local.ehrbase.org::1` |
| RI02 | `056c6620-67b0-408f-bf90-1f8458fe8b66::local.ehrbase.org::1` |

The `RI02` COMPOSITION is a separately created negative-test record and is not part of the original 15-COMPOSITION dataset. Its episode target, `ehr://00000000-0000-4000-8000-000000000099::local.ehrbase.org::1`, was not found in the documented RI-01 lookup. The Care Encounter reference, `ehr://6617f878-b798-4422-979f-524d44dc1385::local.ehrbase.org::1`, points to CE1. The acceptance of the RI-02 write request is an observation from the tested environment, not evidence that the episode target exists or that referential integrity is enforced.

| Episode | Name | Status | Progression | Classification |
|---|---|---|---|---|
| EP1 | General health problem | Active | Acute | Problem |
| EP2 | Urinary tract infection | Active | Acute | Diagnosis |
| EP3 | Arterial hypertension (diagnosed 2009) | Active | Chronic | Diagnosis |
| EP4 | Obesity WHO grade I | Active | Chronic | Diagnosis |

| MR | Date | ENTRYs | Episode relationships | Contact |
|---|---|---:|---|---|
| MR1 | 2024-11-15 | 2 | EP1 Primary ×2, EP3 Associated ×1 | CE1 |
| MR2 | 2024-11-15 | 3 | EP1 Primary ×3, EP4 Associated ×3 | CE1 |
| MR3 | 2024-11-15 | 1 | EP2 Primary ×1 | CE1 |
| MR4 | 2024-11-15 | 4 | EP2 Primary ×4 | CE1 |
| MR5 | 2024-11-15 | 1 | EP2 Primary ×1 | CE1 |
| MR6 | 2024-11-17 | 1 | EP2 Primary ×1 | CE2 |
| MR7 | 2024-11-17 | 2 | EP1 Primary ×2, EP3 Associated ×1 | CE2 |
| MR8 | 2024-11-17 | 4 | EP2 Primary ×4 | CE2 |
| MR9 | 2024-11-17 | 1 | EP2 Primary ×1 | CE2 |

The relationship counts in the Medical Record inventory refer to technical ENTRY-level occurrences. The four ENTRYs of each SOAP note remain one clinical documentation unit and share the same Episode-of-Care assignment in the test dataset. The inventory does not establish server-side enforcement of that assignment.
