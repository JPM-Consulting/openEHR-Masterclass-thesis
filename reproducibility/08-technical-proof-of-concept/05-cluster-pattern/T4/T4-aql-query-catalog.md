# T4 – AQL Query Catalog

The following AQL statements were documented for the interactive T4 test session. Submit each statement using `POST /ehrbase/rest/openehr/v1/query/aql` with `Content-Type: application/json`, `Accept: application/json`, and a request body of `{"q":"<AQL>"}`. The result counts in the headings are reported from that session. Raw server response files are not available in this archive, and the queries were not re-executed during this editorial review.

## COMPOSITION Inventory – 15 COMPOSITIONs

```aql
SELECT c/uid/value AS composition_uid, c/archetype_details/template_id/value AS template_id, c/name/value AS composition_name, c/context/start_time/value AS start_time FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c ORDER BY c/context/start_time/value ASC
```

## Care Encounter to Medical Record – 9 References

```aql
SELECT c/uid/value AS care_encounter_uid, rel/name/value AS relationship_name, ref/name/value AS reference_name, ref/value/value AS target_uri FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.encounter.v1] CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0] CONTAINS ELEMENT ref[at0147]
```

## Episode of Care to Clinical ENTRY – 24 References

```aql
SELECT c/uid/value AS episode_uid, rel/name/value AS relationship_name, ref/name/value AS relationship_role, ref/name/defining_code/code_string AS role_code, ref/value/value AS target_uri FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.problem_list.v2] CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0] CONTAINS ELEMENT ref[at0147]
```

## All ENTRYs – 25

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS contact_time, entry/archetype_node_id AS entry_archetype, entry/name/value AS entry_name FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c CONTAINS ENTRY entry ORDER BY c/context/start_time/value ASC
```

## Clinical Medical Record ENTRYs – 19

```aql
SELECT c/uid/value AS composition_uid, c/context/start_time/value AS contact_time, c/archetype_details/template_id/value AS template_id, entry/archetype_node_id AS entry_archetype, entry/name/value AS entry_name FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c CONTAINS ENTRY entry WHERE c/name/value != 'Care Encounter - CLUSTER relationships' AND c/name/value != 'Episode of Care - CLUSTER relationships' ORDER BY c/context/start_time/value ASC
```

## EP2 Relationships – 12

```aql
SELECT c/uid/value AS episode_uid, ref/name/value AS relationship_role, ref/value/value AS clinical_entry_uri FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.problem_list.v2] CONTAINS CLUSTER rel[openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0] CONTAINS ELEMENT ref[at0147] WHERE c/uid/value = '78d056e3-258f-4407-8b65-0130459c194d::local.ehrbase.org::1'
```

## MR3 Full Urinalysis – 1

```aql
SELECT entry AS clinical_entry FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[uid/value='07a28bae-85fb-4da7-99b7-dfef08289351::local.ehrbase.org::1'] CONTAINS OBSERVATION entry[openEHR-EHR-OBSERVATION.urinalysis.v1]
```

## MR4 SOAP SECTION – 1

```aql
SELECT s AS soap_section FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[uid/value='115c09a9-622d-43f3-91d5-dbff7af0ec79::local.ehrbase.org::1'] CONTAINS SECTION s[openEHR-EHR-SECTION.soap.v0]
```

## MR8 SOAP SECTION – 1

```aql
SELECT s AS soap_section FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[uid/value='8bb59241-2eda-42a2-9399-276a0f452f6a::local.ehrbase.org::1'] CONTAINS SECTION s[openEHR-EHR-SECTION.soap.v0]
```

## Diagnosis and Problem List – 4 Rows

```aql
SELECT c/uid/value AS episode_uid, d/data/items[at0002]/value/value AS diagnosis, d/data/items[openEHR-EHR-CLUSTER.problem_qualifier.v2]/items[at0060]/value/value AS current_past, d/data/items[openEHR-EHR-CLUSTER.problem_qualifier.v2]/items[at0003]/value/value AS active_inactive FROM EHR e[ehr_id/value='3c269710-a677-4fe8-9083-1133e8899db9'] CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.problem_list.v2] CONTAINS EVALUATION d[openEHR-EHR-EVALUATION.problem_diagnosis.v1]
```

## Interpretation Limits

These AQL queries return stored URI strings rather than automatically dereferenced clinical ENTRYs. SOAP ENTRY paths in EP2 are percent-encoded. Retrieving a SOAP SECTION using a known Medical Record COMPOSITION UID requires a separate query. The filter used to identify 19 clinical Medical Record ENTRYs relies on display names and is specific to this synthetic test dataset. The documented results do not establish automatic end-to-end reconstruction of clinical views.
