# Tutorial Videos

This directory links to two tutorial videos explaining the conceptual foundations and openEHR modeling of the episode-oriented medical record examined in this study.

The tutorials provide educational context for the repository. They are not evidence from the functional or architectural evaluations.

## Tutorial Session 1: Episode-Oriented Medical Record

**Solon's Episode-Oriented Medical Record: High-Level EHR Organization**

This tutorial introduces Solon's episode-oriented medical record and explains how clinical information can be organized by Care Encounter, Episode of Care, Clinical Section, and derived views, including Episode, Diagnosis, and Problem Lists.

It provides background for the conceptual model and implementation patterns examined in the study.

-   Project page: https://jpm-consulting.ch/episode-oriented-medical-record.html
-   Vimeo: https://vimeo.com/1167309403

## Tutorial Session 2: Modeling in openEHR

**Solon's Episode-Oriented Medical Record: Modeling in openEHR**

Building on Session 1, this tutorial explores how the episode-oriented medical record can be represented in openEHR.

It introduces the logical data model and openEHR templates for Care Encounters, Episodes of Care, and clinical Medical Record Entries. It then presents three approaches to representing relationships between these objects in openEHR:

-   FOLDER-based organization
-   LINK-based relationships
-   CLUSTER-based archetyped relationships

The tutorial reflects modeling work developed for the openEHR Masterclass thesis. Some aspects were subsequently refined in the comparative evaluation and the accompanying reproducibility artifacts. The tutorial should not be treated as a record of the final evaluation results.

-   Project page: https://jpm-consulting.ch/episode-oriented-medical-record.html
-   Vimeo: https://vimeo.com/1168024722

## Relationship to the reproducibility package

The tutorials provide explanatory context. The study's design artifacts and evaluation evidence are documented separately in this repository, including:

-   the conceptual model
-   the three openEHR implementation patterns
-   the synthetic longitudinal dataset
-   the functional design evaluation
-   the architectural evaluation framework and evidence
-   retrieval examples
-   the technical proof-of-concept evidence and its documented limitations
-   the mapping between manuscript claims and repository artifacts

The tutorials are **supporting educational material, not independent evaluation evidence**.
