---
layout: default
title: Design Directives
parent: For developers
nav_order: 2
permalink: dev/design_directives
---

# Design Directives
{: .no_toc }

This page lists out our design directives for the library.

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## _fm-v2_

1. Provides a _generic_ mechanism that helps to easily obtain custom feature models, e.g., attribute-based feature models,
cardinality-based feature models, anomaly-aware feature models, etc.
2. Base classes (e.g., `Feature`, `Relationship`, `CTConstraint`, etc.) are immutable.
Mutable versions of these classes should be implemented in other packages to keep this package clean.
3. Supports only to _basic_ feature models, i.e., feature models with four relationships (_mandatory_, _optional_, _or_,
and _alternative_) and two cross-tree constraints (_requires_ and _excludes_).
Other types of feature models should be implemented in other packages to keep this package simple.
4. Supports to arbitrary constraints with complex operators (e.g., $$\wedge$$, $$\vee$$, $$\neg$$, $$\rightarrow$$, $$\leftrightarrow$$).
5. Supports common feature model formats found in the literature, i.e., [SPLOT], [FeatureIDE].

<!-- Linsk -->
[SPLOT]: http://www.splot-research.org
[FeatureIDE]: https://featureide.github.io