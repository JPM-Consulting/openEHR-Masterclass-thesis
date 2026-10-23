# T3 — AQL Query Catalog

Endpoint: `POST http://localhost:8080/ehrbase/rest/openehr/v1/query/aql`  
Headers: `Content-Type: application/json`, `Accept: application/json`  
Body: `{"q":"<AQL query>"}` (JSON-escape line breaks when sending).  
EHR: `f4908498-afef-4e3c-8cc4-bbdf16d808bf`.

The SQL-like AQL statements below document query logic associated with the recorded T3 tests in [T3-link-test-results.md](T3-link-test-results.md). Some statements were reconstructed from the recorded test conditions rather than retained as byte-for-byte Postman exports. They are reproduction templates, not original request artifacts, and their inclusion does not establish a new execution or independent revalidation.

### T3.5.1 — COMPOSITION inventory

Recorded expected/observed result: 15 COMPOSITIONs (2 CE, 4 EP, 9 MR).

```sql
SELECT c/uid/value AS composition_uid, c/name/value AS composition_name
FROM EHR e CONTAINS COMPOSITION c
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
```

### T3.5.2 — Encounter LINKs

Recorded expected/observed result: 9 encounter LINK rows, 6 context COMPOSITIONs with null links.

```sql
SELECT c/uid/value AS composition_uid, c/links/type/value AS link_type, c/links/target/value AS encounter_uri
FROM EHR e CONTAINS COMPOSITION c
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
```

### T3.5.4 — All OBSERVATION LINKs

Recorded expected/observed result: 22 LINK rows = 17 primary + 5 associated.

```sql
SELECT c/uid/value AS composition_uid, o/name/value AS entry_name, o/links/type/value AS link_type, o/links/target/value AS target_uri
FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION o
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
```

### T3.5.5 — All INSTRUCTION LINKs

Recorded expected/observed result: 2 primary EP2 links.

```sql
SELECT c/uid/value AS composition_uid, i/name/value AS entry_name, i/links/type/value AS link_type, i/links/target/value AS target_uri, i/narrative/value AS narrative
FROM EHR e CONTAINS COMPOSITION c CONTAINS INSTRUCTION i
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
```

### T3.6.1 — EP2 OBSERVATION Inverse Lookup

Recorded expected/observed result: 10 technical OBSERVATION links.

```sql
SELECT c/uid/value AS composition_uid, o/name/value AS entry_name, o/links/type/value AS link_type
FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION o
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND o/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1'
```

### T3.6.2 — EP2 INSTRUCTION Inverse Lookup

Recorded expected/observed result: 2 medication INSTRUCTIONs.

```sql
SELECT c/uid/value AS composition_uid, i/narrative/value AS narrative
FROM EHR e CONTAINS COMPOSITION c CONTAINS INSTRUCTION i
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND i/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1'
```

### T3.6.4 — SOAP Leaf Sections

Recorded expected/observed result: 8 SOAP leaf-section rows. The section-name filter depends on language and template.

```sql
SELECT c/uid/value AS composition_uid, s/name/value AS section_name, o/name/value AS entry_name, o/data/events/data/items/value/value AS clinical_text
FROM EHR e CONTAINS COMPOSITION c CONTAINS SECTION s CONTAINS OBSERVATION o
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND c/archetype_details/template_id/value = 'JPM_SOAP_Progress_Note.v1'
AND s/name/value != 'SOAP headings'
```

### T3.6.11 — Paired Microbiology Susceptibility Results

Recorded expected/observed result: 5 paired antimicrobial-agent / interpretation rows.

```sql
SELECT c/uid/value AS composition_uid,
 susceptibility/items[at0010]/value/value AS antimicrobial_agent,
 susceptibility/items[at0012]/value/value AS interpretation
FROM EHR e CONTAINS COMPOSITION c
CONTAINS OBSERVATION o[openEHR-EHR-OBSERVATION.laboratory_test_result.v1]
CONTAINS CLUSTER microbiology[openEHR-EHR-CLUSTER.lab_microscopy_culture.v0]
CONTAINS CLUSTER susceptibility[at0009]
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND c/uid/value = '1f0eaddc-8750-4fe0-a4a8-3162fa2383a3::local.ehrbase.org::1'
```

### T3.6.12 — Six Distinct EP2 MR Documents

Recorded expected/observed result: 6 documents, three per encounter.

```sql
SELECT DISTINCT c/uid/value AS composition_uid, c/name/value AS composition_name, c/context/start_time/value AS start_time
FROM EHR e CONTAINS COMPOSITION c CONTAINS ENTRY entry
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND entry/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1'
ORDER BY c/context/start_time/value ASC
```

### T3.6.13 — EP2 Documents with Encounter URI

Recorded expected/observed result: 6 documents, correct CE1/CE2 assignment.

```sql
SELECT DISTINCT c/uid/value AS composition_uid, c/name/value AS composition_name, c/context/start_time/value AS start_time, c/links/target/value AS care_encounter_uri
FROM EHR e CONTAINS COMPOSITION c CONTAINS ENTRY entry
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND entry/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1'
ORDER BY c/context/start_time/value ASC
```

### T3.6.15 — EP2 in CE1

Recorded expected/observed result: 3 distinct documents.

```sql
SELECT DISTINCT c/uid/value AS composition_uid, c/name/value AS composition_name
FROM EHR e CONTAINS COMPOSITION c CONTAINS ENTRY entry
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND entry/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1'
AND c/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/a942e76a-471d-4e43-9d8b-e9318c2c0498::local.ehrbase.org::1'
```

### T3.6.16 — EP2 in CE2

Recorded expected/observed result: 3 distinct documents.

```sql
SELECT DISTINCT c/uid/value AS composition_uid, c/name/value AS composition_name
FROM EHR e CONTAINS COMPOSITION c CONTAINS ENTRY entry
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND entry/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1'
AND c/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/4612e7a1-047a-466c-a5bf-42be2711f044::local.ehrbase.org::1'
```

### T3.6.17 — EP3 Observations

Recorded expected/observed result: 2 BP observations.

```sql
SELECT c/uid/value AS composition_uid, o/name/value AS entry_name, o/links/type/value AS link_type
FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION o
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND o/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/4e2fa228-1857-4a60-9cc1-53a6d7f54a00::local.ehrbase.org::1'
AND o/links/type/value = 'episode-of-care-associated'
```

### T3.6.19 — EP4 Observations

Recorded expected/observed result: 3 body measurements.

```sql
SELECT c/uid/value AS composition_uid, o/name/value AS entry_name, o/links/type/value AS link_type
FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION o
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND o/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/50a0b2b8-9a3c-46f5-b802-0b634f75415b::local.ehrbase.org::1'
AND o/links/type/value = 'episode-of-care-associated'
```

### T3.6.20 — EP1 Observations

Recorded expected/observed result: 7 observations.

```sql
SELECT c/uid/value AS composition_uid, o/name/value AS entry_name, o/links/type/value AS link_type
FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION o
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND o/links/target/value = 'ehr://f4908498-afef-4e3c-8cc4-bbdf16d808bf/25e56fbc-9c74-4c6e-8ce9-a3e97a0250b1::local.ehrbase.org::1'
AND o/links/type/value = 'episode-of-care-primary'
```

### T3.6.21 — All Primary ENTRY LINKs

Recorded expected/observed result: 19 primary LINK rows (per-ENTRY uniqueness independently checked in JSON).

```sql
SELECT c/uid/value AS composition_uid, entry/name/value AS entry_name, entry/links/target/value AS target_uri
FROM EHR e CONTAINS COMPOSITION c CONTAINS ENTRY entry
WHERE e/ehr_id/value = 'f4908498-afef-4e3c-8cc4-bbdf16d808bf'
AND entry/links/type/value = 'episode-of-care-primary'
```

## Observed Errors and Corrections

- T3.6.3: Unfiltered `SECTION s CONTAINS OBSERVATION o` returned 16 rather than 8 SOAP rows because both parent and leaf sections matched. The corrected query adds `AND s/name/value != 'SOAP headings'` (T3.6.4). Archetype-node identifiers are preferable to display labels for robust implementations.
- T3.6.9: `CONTAINS OBSERVATION o CONTAINS CLUSTER susceptibility[at0009]` returned HTTP 400: `Parent CONTAINS expression 'OBSERVATION' must have either an archetype predicate or node predicate when containing at-code expressions`. Adding an OBSERVATION archetype predicate alone returned zero because susceptibility CLUSTERs are nested within the microbiology CLUSTER. The corrected query explicitly traverses `CLUSTER microbiology[openEHR-EHR-CLUSTER.lab_microscopy_culture.v0]` before `CLUSTER susceptibility[at0009]` (T3.6.11).
- T3.6.14: `GROUP BY` produced HTTP 400 `mismatched input 'GROUP' expecting {<EOF>, ORDER, LIMIT, '--'}`. `GROUP BY` is not part of the standard AQL grammar. The test is classified as N/A. Aggregation can be performed in application code.
- T3.5.2 initial variant: An `ORDER BY` path not present in `SELECT` returned HTTP 400. The corrected query succeeded. The catalogue avoids requiring that ordering.
- Data semantics: `DV_ORDINAL` display labels use `value/symbol/value`, whereas `value/value` accesses the numeric ordinal. AQL LINK unnesting may return multiple rows for one clinical ENTRY.

Reference: [openEHR AQL specification](https://specifications.openehr.org/releases/QUERY/latest/AQL.html).
