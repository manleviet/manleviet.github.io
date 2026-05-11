---
layout: default
title: Research – Viet-Man Le
---

## Research

My research centers on **Knowledge-based Diagnosis**, **Configuration Systems**, and **Explanations in AI**. The goal is to make knowledge-based systems faster, more transparent, and more useful for end users, by combining classical constraint reasoning with modern learning-based techniques.

### Research Interests

* Knowledge-based Diagnosis and Conflict Detection
* Constraint Acquisition and Constraint Solving
* Feature Models and Software Product Line
* Explanations in AI for Configuration Systems and Recommender Systems

### Projects

**MIRROR** — *Material Improvement through Reflective Review of Outputs and Resources.* A teaching innovation project (funded by *Projektfonds Lehre 2026*, TU Graz Vice-Rectorate for Teaching; co-PI with Professor Alexander Felfernig), which uses Large Language Models to analyze anonymized student submissions from the *Introduction to Structured Programming* course and propose targeted didactic improvements for the upcoming summer semester.

**[GenRE](https://ase.sai.tugraz.at/research-projects/genre-generative-ai-for-requirements-engineering/)** — *Generative AI for Requirements Engineering.* An FFG Bridge project (2024–2027) developing LLM-based techniques for requirements elicitation, quality assurance, and validation in software engineering. Industry partner: Morgendigital; external evaluation partners: Innovation Service Network and Uniquare.

**[OpenSpace](https://ase.sai.tugraz.at/research-projects/openspace-ffg-bridge/)** — *AI Techniques for Testing Highly-Variant Software.* An FFG Bridge project developing machine learning approaches for testing and debugging variability-intensive software, including automated analysis of variability models and the identification of faulty components and suboptimal parameterizations. Industry partner: Uniquare GmbH.

**[ParXCel](https://ase.sai.tugraz.at/research-projects/parxcel-ffg-bridge/)** — *Machine Learning and Parallelization for Scalable Constraint Solving.* An FFG Bridge project integrating machine learning into constraint-based reasoning to enable personalized configuration, and parallelizing analysis operations such as conflict detection and diagnosis to boost performance. Industry partner: Combeenation GmbH.

### Software & Tools

**[flamapy](https://www.flamapy.org)** *(Python)* — open-source ecosystem for the automated analysis of feature models. Contributed **FastDiagP**, **DirectDebug**, and **WipeOutR** as plugins. **FastDiagP** is also accessible interactively through the browser-based environment [flamapy.ide](https://ide.flamapy.org).

**[FMTesting](https://github.com/AIG-ist-tugraz/FMTesting)** *(Java, FeatureIDE plug-in)* — Eclipse plug-in for feature model testing and debugging, built on top of **hiconfit-core**. Integrates **DirectDebug**, **WipeOutR**, and **AggregatedTest**.

**Restful Configurator Webservice** *(Java, REST API, Spring Boot)* — REST API for developing product configurators, built on top of **hiconfit-core**. Provides domain reduction, matrix factorization-based configuration and recommendation, option reordering via Value Variable Heuristics, and conflict and diagnosis detection.

**[DirectDebug](https://github.com/AIG-ist-tugraz/DirectDebug)** *(Java)* — software package for the automated testing and debugging of variability models. Published in *Software Impacts* (2021).

**[FM2ExConf](https://fm2exconf.sai.tugraz.at)** *(Java)* — converts feature models into executable Excel-based configurators, built on top of **hiconfit-core**. Supports anomaly detection and configuration explanation, making configuration accessible to non-IT stakeholders.

**[HiConfiT](https://hiconfit.github.io/)** *(Java)* — *High Performance Knowledge Based Configuration Techniques.* A suite of open-source libraries (**hiconfit-core**) and command-line apps (**KBStatistics**, **FMGen**) for Knowledge-Based Configuration Systems. Used by **FMTesting** and **FM2ExConf**.
