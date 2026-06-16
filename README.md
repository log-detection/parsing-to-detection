# Parsing-to-Detection Reproducibility Package

This repository provides the reproducibility materials for the paper:

**When Parsing Goes Wrong: Revisiting Log Anomaly Detection from Parsing to Deployment**

## Overview

Log analysis is commonly treated as a pipeline in which raw logs are first parsed into event templates and then used by downstream anomaly detection models. However, prior studies often evaluate log parsing and anomaly detection as separate technical tasks. This separation makes it difficult to understand how parsing errors propagate to anomaly detection, how such effects vary across datasets and models, and whether external public logs can help industrial anomaly detection under data scarcity.

This repository supports the reproducibility of our mixed-method empirical study on log parsing and anomaly detection. The study examines the interaction between upstream parsing quality and downstream detection performance across public LogHub datasets and proprietary industrial log datasets collected from contemporary production systems.

The repository provides implementation materials, configuration files, annotation guidelines, and the practitioner interview protocol used in the study. The proprietary industrial datasets are not included in this repository due to confidentiality, intellectual property, and operational security restrictions.

## What This Repository Provides

To support reproducibility while respecting industrial confidentiality constraints, this repository provides the following materials:

- source code and configuration files for the evaluated log parsing methods;
- source code and configuration files for the evaluated anomaly detection models;
- annotation guidelines for anomaly labeling and parsing-error coding;
- practitioner interview protocol;
- documentation of the experimental setup and evaluation protocol.

The proprietary industrial datasets used in the paper cannot be publicly released because they are derived from real-world production systems and contain sensitive operational information, proprietary logging formats, domain-specific configurations, and system behaviors subject to confidentiality and intellectual property restrictions.

## Public Dataset Access

The public datasets used in this study should be obtained from the official LogPAI repositories:

- **LogHub:** https://github.com/logpai/loghub
- **LogHub-2.0:** https://github.com/logpai/loghub-2.0

Researchers who use these public datasets should follow the corresponding dataset licenses, usage conditions, and citation requirements specified by the original LogPAI repositories.

## Why Parsing-to-Detection Matters

In practical log analysis, parsing errors are not isolated preprocessing issues. They can distort event templates, remove anomaly-related cues, merge semantically different events, split equivalent events into sparse templates, or misrepresent important parameters. These errors may then propagate to downstream anomaly detection models and affect detection reliability.

This problem is especially important in industrial software systems. Industrial logs are often more heterogeneous, domain-specific, and operationally sensitive than public benchmark logs. They may involve embedded controllers, process sensors, SCADA nodes, enterprise workflows, access-control records, safety events, transaction audits, and evolving software services. As a result, a parser that performs well on public benchmarks may still produce misleading templates in real-world deployment.

Our study therefore revisits log anomaly detection from an end-to-end pipeline perspective. Rather than asking only which parser has the highest parsing accuracy, we examine which types of parsing errors occur, how they affect anomaly detection, whether expert correction improves detection results, and when external public logs can or cannot help industrial anomaly detection.

## Research Questions Supported by This Repository

This repository provides materials related to the following research questions:

1. **RQ1: What types of parsing errors occur in public and industrial logs?**  
   We identify and formalize six recurring parsing-error types through expert review of rule-based and LLM-based parsers.

2. **RQ2: How do parsing errors affect downstream anomaly detection?**  
   We compare anomaly detection performance under original parsed logs and expert-corrected parsed logs.

3. **RQ3: Can external public logs improve anomaly detection on data-scarce industrial datasets?**  
   We evaluate whether curated public logs from LogHub improve industrial anomaly detection and examine negative transfer through ablation experiments.

4. **RQ4: How do practitioners interpret industrial log analysis challenges?**  
   We conduct semi-structured practitioner interviews to understand how engineers perceive industrial logs, parsing errors, public benchmarks, data scarcity, external augmentation, and deployment requirements.

## Data Availability

The study uses public LogHub datasets and proprietary industrial datasets.

The public datasets can be downloaded from the official LogPAI repositories listed above. This repository does not redistribute the LogHub datasets directly. Users should download them from the original sources to ensure consistency with the official versions and citation requirements.

The proprietary industrial datasets are not included in this repository. They are derived from real-world production systems and are restricted by confidentiality agreements, intellectual property constraints, and operational security requirements. Therefore, exact end-to-end reproduction of all numerical results involving industrial data is not possible using this public repository alone.

## Parsing-Error Taxonomy

The study identifies six recurring parsing-error types:

1. **Template Over-Merging**  
   Distinct log events are incorrectly collapsed into one template.

2. **Template Over-Splitting**  
   Messages that express the same event are incorrectly split into multiple templates.

3. **Variable Boundary / Extraction Error**  
   Dynamic variables are partially or incorrectly extracted.

4. **Inconsistent Parameter Masking**  
   The same type of parameter is masked inconsistently across similar messages.

5. **Unseen Template / OOV Handling Error**  
   New, rare, or evolving templates are incorrectly matched or assigned.

6. **LLM Semantic Rewriting / Hallucinated Template**  
   An LLM-based parser rewrites, paraphrases, or introduces content that is not faithfully present in the raw log.

The annotation guidelines included in this repository describe the coding rules, priority rules, correction principles, adjudication process, and reliability assessment used for parsing-error coding.

## Evaluated Methods

### Log Parsers

The study evaluates representative rule-based and LLM-based parsers, including:

- Drain
- Spell
- AEL
- DivLog
- LILAC
- LUNAR

### Anomaly Detection Models

The study evaluates five representative anomaly detection models:

- PLELog
- LogBERT
- SemiRALD
- SemiSMAC
- LogRobust

The provided configuration files document the settings used for parsing, sequence construction, model training, validation, and testing.

## Annotation Guidelines

This repository includes the annotation guidelines used for anomaly labeling and parsing-error coding.

The guidelines cover:

- annotation goals and annotator roles;
- anomaly label definitions;
- sequence-level labeling rules;
- parsing-error coding rules;
- six parsing-error categories;
- priority rules for ambiguous parsing errors;
- correction principles for RQ2;
- adjudication procedures;
- reliability assessment;
- confidentiality and anonymization requirements.

These guidelines are intended to help researchers understand how expert labels, parsing-error codes, and corrected templates were produced in the study.

## Practitioner Interview Protocol

This repository includes the practitioner interview protocol used in RQ4.

The interviews examine:

- characteristics of industrial logs;
- differences between industrial logs and public benchmarks;
- practical consequences of parsing errors;
- data scarcity and labeling constraints;
- usefulness and risks of external public logs;
- deployment requirements for log parsing and anomaly detection systems;
- the importance of robustness, faithfulness, traceability, and actionability.

The interview protocol includes the interview procedure, consent and confidentiality requirements, 28 interview questions used in the study, thematic analysis procedure, saturation checking, member checking, and reporting guidelines.

## Acknowledgment

We thank our industrial partners and practitioner participants for supporting this study. Their collaboration made it possible to examine log parsing and anomaly detection under realistic deployment constraints.

