# Technical Proof of Concept: Independent Reproduction Guide

Status: Reproduction instructions based on archived test evidence. not independently re-executed.  
Scope: Preliminary T0 and five isolated test scenarios T1–T5.  
Evidence policy: This guide points to the original test records instead of rewriting historical observations as newly executed results. Where a complete executable sequence cannot be established from the archive, that limitation is stated explicitly.

## 1. Purpose and boundaries

This guide helps an independent investigator repeat the documented openEHR FOLDER, LINK, and CLUSTER relationship tests. The historical design, execution observations, and acceptance criteria are recorded in [DOC-01](../DOC-01-poc-scenario.md), [DOC-02](../DOC-02-poc-clinical-relationships.md), [DOC-03](../DOC-03-poc-plan.md), and [DOC-04](../DOC-04-poc-results.md). The technical PoC dataset (nine clinical Medical Record COMPOSITIONs, two Care Encounters and four Episodes of Care) must not be confused with the 121-entry design-level longitudinal dataset.

A new execution creates new EHR and COMPOSITION identifiers. Archived UUIDs, versioned UIDs and URI references are historical examples, not portable constants. The archived tests do not establish fully automatic clinical-view generation, general referential-integrity enforcement, performance, or cross-vendor interoperability.

## 2. Environment and prerequisites

1. Prepare an isolated EHRbase instance with a PostgreSQL database and openEHR REST/AQL access. See [Environment documentation](../07-environment/README.md) for the documented environment and remaining provenance uncertainties. The historical tests report EHRbase 2.30.1. the available Docker Compose file specifies image tag `ehrbase/ehrbase:2.11.0`. A server status response reports 2.30.1. Do not assume the supplied Compose file by itself reproduces the observed historical runtime.
2. If using the available Compose configuration, ensure its referenced `init.sql` is available, check image versions, ports, authentication and initialization, and verify the running server through its status endpoint before loading test data. The Compose manifest and SQL initialization script are available separately. They were not included in the original repository snapshot.
3. Provide an HTTP client (Postman was used historically) capable of sending canonical JSON, REST requests and AQL requests. Configure the server base URL, authentication if applicable, and an EHR-ID variable per test.
4. Import all 16 OPTs once during initial CDR setup, using [02-templates/opt/](../02-templates/opt/). The [template README](../02-templates/README.md) distinguishes FOLDER/LINK variants from CLUSTER variants. Check which template IDs and versions are already registered. Do not re-upload an existing template version. Verify that the required templates are available before running T0–T5.
5. Read the [synthetic test dataset](../01-test-dataset/README.md), the [relationship specification](../DOC-02-poc-clinical-relationships.md), and the test-specific README and evidence manifest. Establish a separate, initially empty EHR for each T1–T5. do not mix persisted data across scenarios.

Prerequisite not fully packaged: The archive does not establish a single, end-to-end automated setup with pinned container image digests and a fully tested import-and-execution script. Some request sequences depend on identifiers assigned by the target CDR.

## 3. Common execution protocol

Before the test series, record the available environment information (server status, software versions, date and relevant configuration) once and check that the required REST and AQL endpoints respond. This is a recommended reproducibility measure, not a claim that these checks were performed before every historical test. Repeat the checks only if the deployment changes or troubleshooting requires them. The OPTs are imported once during setup (Section 2), not per scenario.

For each scenario:

1. Create a fresh EHR. record its EHR-ID and keep it isolated from the other scenarios.
2. Use the previously imported template family: FOLDER/LINK for T1–T3 and CLUSTER for T4–T5. Verify the relevant template IDs as needed. Do not re-upload the same OPT version.
3. Use the test-specific canonical JSON request files where archived. Preserve the clinical content and intended relationships from DOC-02, but replace historical identifiers and relationship URIs with the identifiers generated in the new environment. In scenarios where archived requests already embed historical identifiers, they are not directly portable without this adaptation.
4. Execute the requests in the order described by the relevant test-specific implementation/README and the scenario plan. Record HTTP method, endpoint, request file, returned status, EHR-ID, COMPOSITION UID/version and response. Do not infer success from the presence of a request file.
5. Retrieve the persisted COMPOSITIONs/DIRECTORY using REST GET and compare structural and relationship properties with the archived `json/persisted/` evidence and evidence manifest. Compare logical relationships and normalized paths, not newly generated UUID strings.
6. Run the documented AQL queries where available, adapting EHR and COMPOSITION identifiers. Distinguish originally archived requests, subsequently reconstructed executable queries, reported observed outcomes, and new responses. Save the new AQL responses independently.
7. Report deviations and unverified claims. do not classify a test as reproduced solely because its JSON files are syntactically valid.

## 4. Scenario-specific procedures

### T0 — Preliminary FOLDER feasibility

Source: [T0 README](../03-folder-pattern/T0/README.md). archived payloads in [`T0/tests/`](../03-folder-pattern/T0/tests/).

- Start with a test EHR and exercise the preliminary DIRECTORY operations using the four archived JSON files as evidence of the attempted variants.
- Distinguish the unencoded and URI-encoded variants of the ENTRY-reference experiment. URI brackets require appropriate URL encoding when used in request URLs. the unencoded variant was not successful in the historical test.
- Verify the resulting DIRECTORY and version changes. T0 is exploratory, not a sixth comparison pattern.

Limit: The archived files and README are the authoritative record for which request variants were attempted. a turnkey Postman collection and all historical HTTP responses are not established by this guide.

### T1 — FOLDER: basic relationship structure

Sources: [T1 README](../03-folder-pattern/T1/README.md), [identifiers](../03-folder-pattern/T1/T1-basic-folder-test-identifiers.md), [evidence manifest](../03-folder-pattern/T1/T1-evidence-manifest.md). DIRECTORY requests in [`T1/tests/`](../03-folder-pattern/T1/tests/).

- In a fresh EHR, persist the nine clinical MR, two CE, and four EP COMPOSITIONs using the FOLDER/LINK template family and the documented synthetic dataset.
- Construct the DIRECTORY referencing the newly persisted objects. Follow the archived initial POST and versioned PUT operations. distinguish the alternative PUT payloads from a mandatory linear sequence.
- Retrieve the final DIRECTORY and verify 33 references: nine Care Encounter `OBJECT_REF` targets and 24 Episode-of-Care `DV_EHR_URI` targets. Compare the final state rather than summing references across historical DIRECTORY versions.
- Clinical Section FOLDER → ENTRY organization (R03) is out of scope. Full clinical-view reconstruction was only partially verified historically.

### T2 — LINK: Medical Records first, context → clinical

Sources: [T2 README](../04-link-pattern/T2/README.md), [implementation](../04-link-pattern/T2/T2-link-implementation.md), [identifiers](../04-link-pattern/T2/T2-link-test-identifiers.md), [evidence manifest](../04-link-pattern/T2/T2-evidence-manifest.md).

- Create a fresh EHR. Persist the nine MR COMPOSITIONs first, then the two CE and four EP COMPOSITIONs containing LINK relationships to the clinical data.
- Inspect the ten archived request payloads and 15 persisted GET exports in the T2 `json/` directories. use the implementation notes to determine which are submissions and which are final server exports.
- Verify 33 LINK instances: nine encounter links and 24 episode links (19 Primary, five Associated). Confirm the reported EP2 retrieval of 12 technical ENTRYs from six MR COMPOSITIONs.
- URI storage and application/AQL interpretation do not demonstrate automatic target dereferencing.

### T3 — LINK: context first, clinical → context

Sources: [T3 README](../04-link-pattern/T3/README.md), [implementation](../04-link-pattern/T3/T3-link-implementation.md), [AQL catalog](../04-link-pattern/T3/T3-aql-query-catalog.md), [test results](../04-link-pattern/T3/T3-link-test-results.md), [evidence manifest](../04-link-pattern/T3/T3-evidence-manifest.md).

- Create a fresh EHR. Persist the two CE and four EP context COMPOSITIONs first, followed by nine clinical MR COMPOSITIONs with links to the appropriate context objects.
- Adapt the nine archived MR request payloads to newly generated context IDs. Retrieve the final 15 COMPOSITIONs.
- Verify 33 LINK instances and the reported EP2 selection of 12 technical ENTRYs across six MR COMPOSITIONs.
- Some executable AQL requests were reconstructed from reported historical queries. do not represent them as archived original request/response captures. Complete historical AQL response bodies are not archived.

### T4 — CLUSTER: Medical Records first, context → clinical

Sources: [T4 README](../05-cluster-pattern/T4/README.md), [implementation](../05-cluster-pattern/T4/T4-cluster-implementation.md), [AQL catalog](../05-cluster-pattern/T4/T4-aql-query-catalog.md), [test results](../05-cluster-pattern/T4/T4-cluster-test-results.md), [evidence manifest](../05-cluster-pattern/T4/T4-evidence-manifest.md).

- Create a fresh EHR, use the previously imported CLUSTER template variants, and persist the nine MR COMPOSITIONs first.
- Persist/update the two CE and four EP context COMPOSITIONs with archetyped relationship CLUSTERs referencing the newly created clinical targets. Inspect the eight archived request JSON files: one is a failed URI-encoding variant, not a successful step to reproduce blindly.
- Retrieve the final 15 COMPOSITIONs and, where reproduced, the prior CE2 version. Verify 33 references (nine CE→MR and 24 EP→ENTRY, including 19 Primary and five Associated).
- Run the documented AQL retrievals. Distinguish the archived historical CE2 `::1` from the final CE2 `::2`. do not count both as separate current COMPOSITIONs.

### T5 — CLUSTER: context first, clinical ENTRY → context

Sources: [T5 README](../05-cluster-pattern/T5/README.md), [implementation](../05-cluster-pattern/T5/T5-cluster-implementation.md), [AQL catalog](../05-cluster-pattern/T5/T5-aql-query-catalog.md), [test results](../05-cluster-pattern/T5/T5-cluster-test-results.md), [evidence manifest](../05-cluster-pattern/T5/T5-evidence-manifest.md).

- Create a fresh EHR, use the previously imported CLUSTER template variants, and persist two CE and four EP context COMPOSITIONs first.
- Adapt and submit the nine archived clinical MR requests, with relationship CLUSTERs in clinical ENTRY `protocol` referring to the newly created CE/EP targets. Retrieve all 15 regular COMPOSITIONs.
- Verify 33 logical relationships, represented by 43 stored `DV_EHR_URI` occurrences (19 CE occurrences and 24 EP occurrences). SOAP notes are single clinical units, but each contains four technical `OBSERVATION.progress_note.v1` ENTRYs. do not confuse technical repetition with additional independent clinical assignments.
- Execute the documented AQL checks. the archived `json/aql/` request bodies were reconstructed from reported executed queries, and full original AQL response payloads were not separately archived.
- RI-02 is a separate negative test: only in an isolated/safely controlled test context, submit a reference to a non-existent EP and inspect the response and persisted object. Historically EHRbase accepted it (HTTP 201). this does not establish universal CDR behavior. The negative-test COMPOSITION is excluded from baseline counts (its inclusion produces 16 COMPOSITIONs and 45 URI occurrences in the archived post-test state).

## 5. Verification and evidence recording

Retain one environment/status record for the test series. For each test, retain a local execution log with the following fields: template IDs, request ordering, generated EHR/COMPOSITION IDs, response status and headers, REST GET evidence, normalized relationship target/path checks, executed AQL text and full response, observed counts, and deviations. Compare with [DOC-04](../DOC-04-poc-results.md) and the scenario evidence manifests. Mark each outcome reproduced, partially reproduced, not reproduced, or not assessed, and explain why.

Do not use historical archive counts as a substitute for measuring a new run. If the new runtime differs from the historical EHRbase 2.30.1 environment, record that difference before interpreting discrepancies.

## 6. Known limitations and non-goals

- No verified, fully automated end-to-end deployment and test runner is included in the archived material.
- Exact historical infrastructure/image digests, all HTTP response bodies and some original AQL request bodies are not available.
- Historical identifiers and hard-coded relationship URIs require adaptation in new EHRs. archived JSON payloads are not guaranteed plug-and-play.
- Some test cases include intentional failure variants, version-history examples, or the RI-02 dangling-reference negative test. these must not be treated as normal baseline inputs.
- This guide does not establish automatic URI dereferencing, runtime reference-integrity enforcement, complete US1–US8 application workflows, production performance, or cross-vendor interoperability.
- This guide is documentation, not a claim that the procedure was independently executed or validated after publication.

## 7. Evidence and maintenance

The procedures in this guide are based on the documented T0–T5 test artifacts, the environment description and the available runtime status and Docker configuration. Original test records remain the reference for observed outcomes. Record any future changes to the environment or procedures separately. do not overwrite the original evidence.
