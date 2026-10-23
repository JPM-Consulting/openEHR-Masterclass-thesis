# Technical PoC: Environment and Reproduction Prerequisites

## Purpose and evidence status

This document describes the technical environment of the episode-oriented openEHR proof of concept (PoC), including the available configuration files, recorded software versions, and remaining reproducibility limitations. It documents the existing evidence and does not constitute a newly validated installation procedure.

The technical PoC comprises a preliminary FOLDER feasibility test (T0) and five isolated test scenarios (T1–T5). The longitudinal dataset used for the design-level functional evaluation is distinct from the smaller technical PoC dataset.

## Documented environment

| Component | Recorded information | Evidence / qualification |
| --- | --- | --- |
| Clinical Data Repository | EHRbase 2.30.1 reported by GET Status Check. Compose declares `ehrbase/ehrbase:2.11.0`. | The queried service reported 2.30.1. The deployment was initially installed in 2024 and may have been updated subsequently. This plausibly explains the differing image tag, but the actual upgrade history has not been verified. The status response does not independently establish the runtime version during every historical test. |
| Data interface | openEHR REST API | Used for COMPOSITION, DIRECTORY, template and retrieval operations as documented by the scenarios. |
| Data representation | Canonical openEHR JSON | Archived request payloads and retrieved COMPOSITION exports. |
| Query interface | Archetype Query Language (AQL) | Queries and observations recorded in the scenario documentation; some executable query bodies were reconstructed later. |
| API client | Postman 12.16.4 | Recorded version; its use during every original test has not been independently established. Original collection revision remains unknown. |
| Container desktop application | Docker Desktop 4.70.0 | Recorded version; its use during every original test has not been independently established. |
| Host computer and operating system | MacBook Air running macOS Tahoe 26.5.1 | Recorded host operating-system version; no system-generated version report is archived. |
| Database container | `postgres:16` in Compose. PostgreSQL 16.6 in GET Status Check. | Running server reports `PostgreSQL 16.6 (Debian 16.6-1.pgdg120+1)` on aarch64; image digest not established. |
| Deployment configuration | Docker Compose | Available `docker-compose.yaml`; the manifest used for each original test has not been established. |
| Modelling application | Archetype Designer (browser-based) | The template documentation records version 1.25.16 as the version recorded at documentation time, not as the verified version for every historical export. |
| Archetype language | ADL 1.4 | Recorded in `../02-templates/README.md`. |
| openEHR Reference Model | RM 1.0.4 | Explicitly recorded in the T3 and T4 scenario READMEs; not independently verified for every scenario. |
| Version UID system identifier | `local.ehrbase.org` | Appears in archived version identifiers and scenario documentation; not a deployment hostname or endpoint specification. |
| Operational Templates | 16 `.opt` files | Archived under `../02-templates/opt/`; eight template types, each with FOLDER/LINK and CLUSTER variants. |
| Modelling export packages | 16 ZIP packages | Archived under `../02-templates/zip/`; successful reimport has not been independently tested. |
| Source of canonical clinical examples | Medblocks Postman Collection | Described in `../01-test-dataset/README.md` and `../02-templates/README.md`; exact collection revision is not established. |

## Docker Compose configuration

The available `docker-compose.yaml` was obtained from the EHRbase download page. It was added to the documentation after the original repository snapshot. Its exact correspondence to the configuration used for each original test is not established.

| Setting | Value declared in available Compose file | Interpretation |
| --- | --- | --- |
| EHRbase image | `ehrbase/ehrbase:2.11.0` | Differs from EHRbase 2.30.1 reported by GET Status Check. The deployment was initially installed in 2024 and may have been updated later. The upgrade sequence and historical image have not been verified. |
| PostgreSQL image | `postgres:16` | Major-version image tag; does not establish exact patch release or image digest. |
| EHRbase database URL | `jdbc:postgresql://db:5432/ehrbase` | Internal container connection. |
| EHRbase exposed port | `8080:8080` | Host-to-container port mapping, not proof of a historical request base URL. |
| PostgreSQL exposed port | `5432:5432` | Host-to-container port mapping. |
| Database volume | `ehrbase_data:/var/lib/postgresql/data` | Named persistent Docker volume. |
| Database initialisation | `./init.sql:/docker-entrypoint-initdb.d/init.sql` | `init.sql` is available separately. It initializes roles, the `ehrbase` database, schemas, extension and database defaults. |
| Experimental FOLDER AQL | `EHRBASE_AQL_EXPERIMENTAL_AQLONFOLDER_ENABLED: 'true'` | Declared enabled in this manifest; relevance to T0/T1 must be evaluated against the historical runtime version. |
| Database users | Administrative and restricted EHRbase accounts | Credentials are declared in the available manifest; do not commit real credentials to a public repository. |

The available Compose file contains plaintext credentials described as examples. A publicly shared version should replace passwords with placeholders or environment-variable references. No credentials are reproduced in this README.

### Observed server status (Postman GET Status Check)

The GET Status Check returned the following runtime-reported values for the queried instance. They are not inferred from the Compose manifest:

| Status field | Observed value |
| --- | --- |
| `ehrbase_version` | `2.30.1` |
| `openehr_sdk_version` | `2.31.0` |
| `archie_version` | `3.13.0` |
| `jvm_version` | `Eclipse Adoptium 25.0.2+10-LTS` |
| `os_version` | `Linux aarch64 6.12.76-linuxkit` (container environment, not macOS host version) |
| `postgres_version` | `PostgreSQL 16.6 (Debian 16.6-1.pgdg120+1) on aarch64-unknown-linux-gnu, compiled by gcc (Debian 12.2.0-14) 12.2.0, 64-bit` |

The GET Status Check resolves which EHRbase and PostgreSQL versions the queried service reported at the time of the check. It does not explain why the available Compose manifest declares `ehrbase/ehrbase:2.11.0`, nor independently establish which deployment or image digest was used for each historical T0–T5 test. The deployment was originally installed in 2024 and may have been updated later. The update history has not been verified.

### PostgreSQL initialisation (`init.sql`)

The available `init.sql` is referenced by the Compose file. Static inspection identifies the following operations:

1. Reads four database user/password values from environment variables through `psql` `\set` commands.
2. Creates a restricted role and an administrative role, and creates the UTF-8 `ehrbase` database using locale `C`.
3. Grants database privileges and configures `ehr` and `ext` schemas with distinct access rights.
4. Installs the `uuid-ossp` extension in schema `ext`.
5. Sets database-level `search_path` to `ext` and `intervalstyle` to `iso_8601`.
6. Alters the estimated row count of `jsonb_path_query(jsonb,jsonpath,jsonb,boolean)` to `ROWS 1`.

This is configuration evidence, not evidence that the script has been re-executed successfully in a new environment. The Compose manifest and SQL script should be archived together in a secure, reproducible form. The original Compose file includes plaintext example credentials and should not be published unchanged.

### Outstanding provenance and configuration questions

- Compose image mismatch and update history: The available manifest declares `ehrbase/ehrbase:2.11.0`, whereas the queried server reports EHRbase 2.30.1. The deployment was originally installed in 2024 and may have been updated later. The update history has not been verified. This is a plausible explanation, not a verified upgrade record. Preserve both values and do not silently change the declared image tag.
- macOS host version: The recorded host version is macOS Tahoe 26.5.1. No machine-generated system report is archived.
- Historical timing: The recorded Docker Desktop 4.70.0, Postman 12.16.4, and GET Status Check describe the environment at the time of documentation. Their exact applicability to each historical T0–T5 run has not been independently demonstrated.
- Exact deployment: Docker Engine/Compose CLI versions, image digests, original Postman collection/environment revision, deployment startup logs and full historical HTTP responses remain unavailable.
- Execution protocol: A machine-executable sequence for template upload, EHR creation, ID substitution, test execution and environment reset remains to be documented.

The new evidence substantially improves environment transparency but does not yet establish a byte-for-byte historical deployment or turnkey reproduction procedure.

## Artefacts available for independent examination

| Location relative to `08-technical-proof-of-concept/` | Role |
| --- | --- |
| [`DOC-01-poc-scenario.md`](../DOC-01-poc-scenario.md) | Clinical scenario, modelling constraints and technical PoC dataset. |
| [`DOC-02-poc-clinical-relationships.md`](../DOC-02-poc-clinical-relationships.md) | Relationship specification and expected associations. |
| [`DOC-03-poc-plan.md`](../DOC-03-poc-plan.md) | Planned technical requirements, test cases and acceptance criteria. |
| [`DOC-04-poc-results.md`](../DOC-04-poc-results.md) | Reported historical test outcomes, observations and limitations. |
| [`01-test-dataset/`](../01-test-dataset/README.md) | Canonical synthetic test data and provenance notes. |
| [`02-templates/`](../02-templates/README.md) | Operational Templates and modelling export packages. |
| [`03-folder-pattern/`](../03-folder-pattern/README.md) | T0 and T1 FOLDER test evidence. |
| [`04-link-pattern/`](../04-link-pattern/README.md) | T2 and T3 LINK test evidence. |
| [`05-cluster-pattern/T4/`](../05-cluster-pattern/T4/README.md) | T4 CLUSTER test evidence. |
| [`05-cluster-pattern/T5/`](../05-cluster-pattern/T5/README.md) | T5 CLUSTER test evidence, including RI-02. |

## Prerequisites for a new reproduction attempt

An independent researcher would need to provide and document a compatible openEHR CDR instance with REST and AQL access, import the appropriate archived OPTs, initialize fresh EHRs, prepare the canonical synthetic data, and adapt the archived request payloads to new EHR IDs, COMPOSITION version UIDs, and environment-specific API parameters. Each scenario should use an isolated EHR or an equivalently controlled starting state. The exact API calls, ordering and variable substitutions must be established from the relevant scenario documentation before execution.

The FOLDER/LINK and CLUSTER template variants are intentionally different. Use the FOLDER/LINK OPTs for T1–T3 rather than substituting CLUSTER OPTs. T0's exploratory use of a role-bearing CLUSTER is not part of the systematically evaluated Basic FOLDER pattern T1.

For T1, distinguish the final DIRECTORY version from intermediate states. For T4, distinguish the current COMPOSITIONs from the historical CE2 export. For T5, keep the separate RI-02 negative-test COMPOSITION outside the original 15-COMPOSITION dataset. The observed acceptance of a dangling URI in RI-02 applies only to the tested configuration and must not be generalised to all CDRs.

## Evidence and reproducibility limits

The archived requests and persisted exports support retrospective inspection of the tested structures and documented observations. They do not constitute a turnkey executable test suite. Complete original AQL response payloads were not separately archived for all scenarios, and some query request bodies were reconstructed from the historical test record. Such reconstructions must not be represented as byte-identical original execution artefacts.

A new execution would be a new experiment and should record its own software versions, deployment configuration, template-upload results, EHR IDs, HTTP request/response pairs, AQL results, timestamps and deviations from the historical protocol. This document makes no claim that such a new execution has been performed.

## Documentation provenance

This description is based on the archived PoC documentation and the available Docker Compose manifest, PostgreSQL initialisation script, software-version information and Postman GET Status Check. This editorial review does not modify the original clinical data, persisted COMPOSITIONs, or recorded test results.
