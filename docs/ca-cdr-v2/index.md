---
layout: default
title: CA-CDR-V2
nav_order: 3
has_children: true
permalink: ca-cdr-v2
has_toc: true
---

# CA-CDR-V2
{: .no_toc }
{: .d-inline-block }

v1.3.9-alpha-52
{: .label .label-purple }

**CA-CDR-V2** is a Java library for **Consistency-based Algorithms for Conflict Detection and Resolution** (CA-CDR).

{: .highlight }
**Conflict Detection and Resolution** is a substantial task in **Knowledge Base Engineering** (KBE).
Intelligent mechanisms are urgently needed, especially in large-scale knowledge bases.
This repository publishes our implementations for some/our consistency-based algorithms,
which can be utilized in all three phases of KBE, i.e., _design_, _testing and debugging_,
and _configuration_.

## What CA-CDR-V2 provide

The library is organized in 7 following Maven packages:

| *package*                                       | *description*                            |
|----------------------------------------------|------------------------------------------|
| [ca-cdr-v2]     | provides implementations of Consistency-based Algorithms for Conflict Detection and Resolution (CA-CDR) and a ChocoConsistencyChecker |
| [cdrmodel-v2] | provides an programmatic approach to manage/prepare the constraints/test cases for consistency-based algorithms |
| [choco-kb-v2]    | provides classes managing CSP (Choco) representations of a knowlege base/feature model |
| [fm-v2]         | provides the management functionalities for basic feature models |
| [eval-v2]     | provides a performance evaluator, i.e., counters and timers, which could be used to measure the performance of algorithms |
| [csp2choco-v2] | provides a translator which enables converting CSP constraints into Choco Solver commands |
| [common-v2] | a Maven package for utility functions |

<!-- provides core functionalities related to knolwedge base testing and debugging tasks -->

The following diagram shows the packages' dependency.

```mermaid
flowchart BT
    subgraph Third-party libraries
        A([opencsv])
        B([choco-solver])
        C([jakarta.mail])
        D([args4j])
        E([guava])
        F([lombok])
        G([slf4j-api])
        Q([json])
        H([antlr4])
        K([javatuples])
    end
    A --> L([common-v2])
    B --> L
    C --> L
    D --> L
    E --> L
    F --> L
    G --> L
    H --> M([csp2choco-v2])
    K --> M
    Q --> O([fm-v2])
    H --> O
    subgraph CA-CDR-V2
        L --> M
        L --> O
        L --> N([eval-v2])
        P([sxfm]) --> O
        O --> R([choco-kb-v2])
        N --> R
        R --> S([cdrmodel-v2])
        M --> S
        S --> T([ca-cdr-v2])
    end
```

<!-- Links -->
[References]: /references
[ca-cdr-v2]: algorithms
[cdrmodel-v2]: cdrmodel
[choco-kb-v2]: kb
[fm-v2]: fm
[eval-v2]: eval
[csp2choco-v2]: csp2choco
[common-v2]: common-utils