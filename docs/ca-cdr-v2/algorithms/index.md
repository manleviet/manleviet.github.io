---
layout: default
title: Algorithms
parent: CA-CDR-V2
nav_order: 5
<!-- has_children: true -->
permalink: ca-cdr-v2/algorithms
<!-- has_toc: false -->
---

# Algorithms
{: .no_toc }
{: .d-inline-block }

v1.3.9-alpha-52
{: .label .label-purple }

<dl>
    <dt><strong>groupID</strong></dt>
    <dd><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd><em>ca-cdr-v2</em></dd>
</dl>

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

1. [QuickXPlain](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/QuickXPlain.java) [1]
2. [FastDiag](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/FastDiagV2.java) [2]
3. [MSS-based FastDiag](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/FastDiagV3.java) [15]
4. [FlexDiag](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/FlexDiag.java) [3]
5. [HS-tree](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/hs/HSTree.java) [8]
6. [HSDAG](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/hs/HSDAG.java) [9]
7. [DirectDebug](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/DirectDebug.java) [4, 5, 6, 7]
8. (coming soon) DirectDiag - [third_release](https://github.com/manleviet/CA-CDR-V2/blob/third_release/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/DirectDiag.java)
9. (coming soon) WipeOutR_T [12, 13]
10. (coming soon) WipeOutR_FM [12, 13] - [third_release](https://github.com/manleviet/CA-CDR-V2/blob/third_release/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/algorithms/WipeOutR_FM.java)
11. (coming soon) AggregatedTest [14]
12. (coming soon) LevelWiseParallelHSDAG [10, 11]
13. (coming soon) FullParallelHSDAG [10, 11]
14. (coming soon) FastDiagP [15] - [Python implementation](https://github.com/manleviet/PyFastDiagP-ver2)
15. (coming soon) KBDiag [the related paper submitted on January 2023]
16. (coming soon) InformedQX
17. (coming soon) ParallelWipeOutR_T
18. (coming soon) ParallelWipeOutR_FM

This package also provides a [Choco Consistency Checker](https://github.com/manleviet/CA-CDR-V2/blob/main/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/checker/ChocoConsistencyChecker.java), supporting the consistency checks for sets of constraints or sets of test cases.

### Examples
{: .no_toc }

There are some test models in [here](https://github.com/manleviet/CDRModel/tree/main/src/main/java/at/tugraz/ist/ase/cdrmodel/test/model) and some examples, showing how to use these algorithms, in [here](https://github.com/manleviet/CA-CDR/tree/main/src/test/java/at/tugraz/ist/ase/cacdr/algorithms).
