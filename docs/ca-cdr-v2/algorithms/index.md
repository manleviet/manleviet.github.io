---
layout: default
title: Algorithms
parent: CA-CDR-V2
nav_order: 6
has_children: true
permalink: ca-cdr-v2/algorithms
has_toc: false
---

# Algorithms
{: .no_toc }
{: .d-inline-block }

v1.3.9-alpha-52
{: .label .label-purple }

<dl style="background:#FEFBE7; border:solid 1px black; width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd><em>ca-cdr-v2</em></dd>
</dl>

## List of algorithms:

_ca-cdr-v2_ provides the following algorithms:

1. [QuickXPlain](quickxplain) [1]
2. [FastDiag](fastdiag) [2]
3. [MSS-based FastDiag](mss_fastdiag) [15]
4. [FlexDiag](flexdiag) [3]
5. [HS-tree](hstree) [8]
6. [HSDAG](hsdag) [9]
7. [DirectDebug](directdebug) [4, 5, 6, 7]
8. [DirectDiag](directdiag)
9. [WipeOutR_T](wipeoutr_t) [12, 13]
10. [WipeOutR_FM](wipeoutr_fm) [12, 13]
11. (coming soon) AggregatedTest [14]
12. (coming soon) LevelWiseParallelHSDAG [10, 11]
13. (coming soon) FullParallelHSDAG [10, 11]
14. (coming soon) FastDiagP [15] - [Python implementation]
15. (coming soon) KBDiag [the related paper submitted on January 2023]
16. (coming soon) InformedQX
17. (coming soon) ParallelWipeOutR_T
18. (coming soon) ParallelWipeOutR_FM

### Examples
{: .no_toc }

There are some test models in [here](https://github.com/manleviet/CDRModel/tree/main/src/main/java/at/tugraz/ist/ase/cdrmodel/test/model) and some examples, showing how to use these algorithms, in [here](https://github.com/manleviet/CA-CDR/tree/main/src/test/java/at/tugraz/ist/ase/cacdr/algorithms).

## [References](/references)

<!-- Links -->
[Python implementation]: https://github.com/manleviet/PyFastDiagP-ver2