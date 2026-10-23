# T5 AQL Query Catalog

Endpoint: `POST http://localhost:8080/ehrbase/rest/openehr/v1/query/aql`  
Headers: `Content-Type: application/json`, `Accept: application/json`.

The corresponding JSON request bodies are archived in `json/aql/`. The row counts below are reported observations from the original interactive test session, not independently reproduced results. They do not describe a fresh query execution after the additional RI-02 test COMPOSITION was persisted. Unrestricted inventory and relationship queries could therefore return different counts against the later database state.

## AQL-01: 15 observed result rows

Request file: [`json/aql/AQL-01.json`](json/aql/AQL-01.json)

```aql
SELECT c/uid/value AS composition_uid, c/name/value AS composition_name, c/archetype_details/template_id/value AS template_id, c/context/start_time/value AS start_time FROM EHR e CONTAINS COMPOSITION c WHERE e/ehr_id/value = '16fe2926-c82a-462c-93f2-d5e67a29656f' ORDER BY c/context/start_time/value ASC
```

## AQL-02: 19 observed result rows

Request file: [`json/aql/AQL-02.json`](json/aql/AQL-02.json)

```aql
SELECT c/uid/value AS composition_uid, entry/name/value AS entry_name, rel/name/value AS relationship_name FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0]
```

## AQL-03: 24 observed result rows

Request file: [`json/aql/AQL-03.json`](json/aql/AQL-03.json)

```aql
SELECT c/uid/value AS composition_uid, entry/name/value AS entry_name, rel/items[at0001]/items[at0009]/value/value AS contact_uri, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0]
```

## AQL-04: 12 observed result rows

Request file: [`json/aql/AQL-04.json`](json/aql/AQL-04.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, entry/name/value AS entry_name, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE rel/items[at0109]/items[at0147]/value/value = 'ehr://c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1' ORDER BY c/context/start_time/value ASC
```

## AQL-05: 8 observed result rows

Request file: [`json/aql/AQL-05.json`](json/aql/AQL-05.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, entry/name/value AS entry_name, rel/items[at0001]/items[at0009]/value/value AS contact_uri FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE rel/items[at0001]/items[at0009]/value/value = 'ehr://bd0bb285-e61d-411b-8c4f-d06a05b53ba6::local.ehrbase.org::1' ORDER BY c/context/start_time/value ASC
```

## AQL-06: 6 observed result rows

Request file: [`json/aql/AQL-06.json`](json/aql/AQL-06.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, entry/name/value AS entry_name, rel/items[at0001]/items[at0009]/value/value AS contact_uri, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE rel/items[at0001]/items[at0009]/value/value = 'ehr://bd0bb285-e61d-411b-8c4f-d06a05b53ba6::local.ehrbase.org::1' AND rel/items[at0109]/items[at0147]/value/value = 'ehr://c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1' ORDER BY c/context/start_time/value ASC
```

## AQL-07: 5 observed result rows

Request file: [`json/aql/AQL-07.json`](json/aql/AQL-07.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, entry/name/value AS entry_name, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE rel/items[at0109]/items[at0153]/value/defining_code/code_string = 'at0155' ORDER BY c/context/start_time/value ASC
```

## AQL-08: 2 observed result rows

Request file: [`json/aql/AQL-08.json`](json/aql/AQL-08.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, entry/name/value AS entry_name, entry/data AS clinical_data, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE rel/items[at0109]/items[at0147]/value/value = 'ehr://364fa3f4-acba-4b9b-9c5c-4feb0f5cbff3::local.ehrbase.org::1' ORDER BY c/context/start_time/value ASC
```

## AQL-09: 4 observed result rows

Request file: [`json/aql/AQL-09.json`](json/aql/AQL-09.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, entry/name/value AS entry_name, entry/data AS clinical_data, rel/items[at0001]/items[at0009]/value/value AS contact_uri, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE c/uid/value = '6b11b73e-7536-4399-9406-644a54a0d2cb::local.ehrbase.org::1'
```

## AQL-10: 8 observed result rows

Request file: [`json/aql/AQL-10.json`](json/aql/AQL-10.json)

```aql
SELECT c/uid/value AS composition_uid, s/name/value AS section_name, entry/name/value AS entry_name, entry/data AS clinical_data FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS SECTION s CONTAINS ENTRY entry WHERE c/uid/value = '6b11b73e-7536-4399-9406-644a54a0d2cb::local.ehrbase.org::1'
```

## AQL-11: 4 observed result rows

Request file: [`json/aql/AQL-11.json`](json/aql/AQL-11.json)

```aql
SELECT c/uid/value AS composition_uid, s/name/value AS soap_section, entry/name/value AS entry_name, entry/data/events[at0002]/data[at0003]/items[at0004]/value/value AS progress_note FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS SECTION s CONTAINS ENTRY entry WHERE c/uid/value = '6b11b73e-7536-4399-9406-644a54a0d2cb::local.ehrbase.org::1' AND s/name/value != 'SOAP headings'
```

## AQL-12: 8 observed result rows

Request file: [`json/aql/AQL-12.json`](json/aql/AQL-12.json)

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS start_time, s/name/value AS soap_section, entry/data/events[at0002]/data[at0003]/items[at0004]/value/value AS progress_note, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS SECTION s CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE s/name/value != 'SOAP headings' AND rel/items[at0109]/items[at0147]/value/value = 'ehr://c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1' ORDER BY c/context/start_time/value ASC
```

## RI-01: 0 observed result rows

Request file: [`json/aql/RI-01.json`](json/aql/RI-01.json)

```aql
SELECT c/uid/value AS composition_uid FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c WHERE c/uid/value = '00000000-0000-4000-8000-000000000099::local.ehrbase.org::1'
```

## RI-04: 1 observed result row

Request file: [`json/aql/RI-04.json`](json/aql/RI-04.json)

```aql
SELECT c/uid/value AS composition_uid, entry/name/value AS entry_name, rel/items[at0001]/items[at0009]/value/value AS contact_uri, rel/items[at0109]/items[at0147]/value/value AS episode_uri, rel/items[at0109]/items[at0153]/value/value AS episode_role FROM EHR e[ehr_id/value='16fe2926-c82a-462c-93f2-d5e67a29656f'] CONTAINS COMPOSITION c CONTAINS ENTRY entry CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_entry.v0] WHERE c/uid/value = '056c6620-67b0-408f-bf90-1f8458fe8b66::local.ehrbase.org::1'
```


## Interpretation Limits

The AQL statements are preserved as documented and have not been modified or re-executed during this editorial review. Reported row counts describe the original execution observations. AQL-10 returns eight SECTION-related rows, which should not be interpreted as eight independent clinical documentation units. The four technical ENTRYs of each SOAP progress note form one clinical unit. The RI-01 and RI-04 queries are evidence of the recorded query observations, not proof that referential integrity was enforced by the server. Complete original AQL response payloads were not separately archived.
