# T4 — Test Identifiers and Relationship Inventory

**EHR ID:** `3c269710-a677-4fe8-9083-1133e8899db9`  
**System ID:** `local.ehrbase.org`

The identifiers below reflect the documented final state of the T4 execution. CE2 is the only COMPOSITION updated during T4.

| Object | Documented final versioned COMPOSITION UID | Description |
|---|---|---|
| CE1 | `125bbcd3-94d7-40d1-95bb-57921bae7134::local.ehrbase.org::1` | 15 Nov 2024, five Medical Record references |
| CE2 | `ebe7f166-85c0-4c68-bf8a-572f32cc2c3c::local.ehrbase.org::2` | 17 Nov 2024, version `::2` contains four Medical Record references |
| EP1 | `63d77635-2e03-48ef-86f5-6614011aea14::local.ehrbase.org::1` | General health problem, 7 Primary |
| EP2 | `78d056e3-258f-4407-8b65-0130459c194d::local.ehrbase.org::1` | Urinary tract infection, 12 Primary |
| EP3 | `6e827bf6-e492-481c-8da3-129a0e06a690::local.ehrbase.org::1` | Arterial hypertension (diagnosed 2009), 2 Associated |
| EP4 | `c739a163-b142-430b-adce-7bab517af22d::local.ehrbase.org::1` | Obesity, WHO grade I, 3 Associated |
| MR1 | `1bfd53df-f670-407d-a7bc-bdd6ace292e1::local.ehrbase.org::1` | Vital signs (2 ENTRYs) |
| MR2 | `6cd82ad3-c4e1-454c-a0f8-b3f75bb3d30c::local.ehrbase.org::1` | Body measurements (3 ENTRYs) |
| MR3 | `07a28bae-85fb-4da7-99b7-dfef08289351::local.ehrbase.org::1` | Urinalysis (1 ENTRY) |
| MR4 | `115c09a9-622d-43f3-91d5-dbff7af0ec79::local.ehrbase.org::1` | SOAP (4 ENTRYs) |
| MR5 | `ea5e5931-5d1d-49dc-9ec1-1c6d7adcc676::local.ehrbase.org::1` | Medication order (1 ENTRY) |
| MR6 | `9e9a8965-367a-4bbb-9279-7a223b5fa811::local.ehrbase.org::1` | Microbiology (1 ENTRY) |
| MR7 | `6b0ec61c-37d1-4bc5-a239-cde980469ee2::local.ehrbase.org::1` | Vital signs (2 ENTRYs) |
| MR8 | `8bb59241-2eda-42a2-9399-276a0f452f6a::local.ehrbase.org::1` | SOAP (4 ENTRYs) |
| MR9 | `6d7c00cb-b738-4975-b38e-7b5e2eb2575d::local.ehrbase.org::1` | Medication order (1 ENTRY) |

## CE2 Version History

- Original: `ebe7f166-85c0-4c68-bf8a-572f32cc2c3c::local.ehrbase.org::1` — Created by POST without a relationship CLUSTER. The original version was retrieved independently by GET before and after the update.
- Updated: `ebe7f166-85c0-4c68-bf8a-572f32cc2c3c::local.ehrbase.org::2` — Updated by PUT to include MR6–MR9 references and retrieved independently by GET.
- The AQL inventory of current COMPOSITION versions returns CE2 `::2`. This does not imply that historical version `::1` was deleted.

## Complete Relationship Matrix

| Source | Target MR(s) | Reference granularity | Primary | Associated | Total |
|---|---|---|---:|---:|---:|
| CE1 | MR1–MR5 | COMPOSITION | — | — | 5 |
| CE2 `::2` | MR6–MR9 | COMPOSITION | — | — | 4 |
| EP1 | MR1 BP/Pulse (2), MR2 height/weight/BMI (3), MR7 BP/Pulse (2) | ENTRY | 7 | 0 | 7 |
| EP2 | MR3 urinalysis (1), MR4 SOAP (4), MR5 medication (1), MR6 microbiology (1), MR8 SOAP (4), MR9 medication (1) | ENTRY | 12 | 0 | 12 |
| EP3 | MR1 BP (1), MR7 BP (1) | ENTRY | 0 | 2 | 2 |
| EP4 | MR2 height/weight/BMI (3) | ENTRY | 0 | 3 | 3 |
| **Total** | | | **19** | **5** | **33** |

The matrix records nine Care Encounter-to-Medical Record references and 24 Episode of Care-to-clinical ENTRY references, totaling 33 technical reference occurrences. The 19 Primary and five Associated references are Episode of Care references only. Each SOAP note is one clinical unit represented by four technical ENTRYs in a single Medical Record COMPOSITION. These counts describe the documented T4 test data and do not establish server-side enforcement of relationship consistency.
