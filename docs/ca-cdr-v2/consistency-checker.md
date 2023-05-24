---
layout: default
title: Consistency Checker
parent: CA-CDR-V2
nav_order: 5
permalink: ca-cdr-v2/consistency-checker
---

# Consistency Checker
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.3.9-alpha-53</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>ca-cdr-v2</em></dd>
</dl>{: .label .label-yellow }

_ca-cdr-v2_ provides a consistency checker class ([`ChocoConsistencyChecker`]) supporting to check the consistency of sets of constraints or sets of test cases.

TBD
{: .label .label-yellow }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

[`ChocoConsistencyChecker`] provides a variant of isConsistent functions with different parameters. In the current version 1.2.20, the class provides five isConsistent functions as the following:

1.	isConsistent(Collection<Constraint> C) – checks the consistency of set of constraints
2.	isConsistent(Collection<Constraint> C, ITestCase testcase) – checks the consistency of a test case with the background knowledge (a set of constraints).
3.	Set<ITestCase> isConsistent(Collection<Constraint> C, Collection<ITestCase> TC, boolean onlyOne) – checks the consistency of a set of test cases with the background knowledge (a set of constraints). The function returns violated test cases. If onlyOne=true, the function returns the first violated test case.
4.	isConsistent(ITestCase testcase, ITestCase neg_testcase) – checks the consistency between two test cases (testcase /\ ¬neg_testcase) to identify a redundant test case. If the output is false (inconsistent), then neg_testcase is a redundant test case. This function is used in the WipeOutR_T algorithm.
5.	isConsistent(Collection<Constraint> C, Constraint cstr) – checks the consistency of (C - {cstr} ∪ {¬cstr}) to identify the redundant constraints. If the output is false (inconsistent), then cstr is a redundant constraint. This function is used by the WipeOutR_FM algorithm.

## How tos

### Use the two last `isConsistent` functions

You can inherit the ChocoConsistencyChecker to add your new isConsistent function, or you can ask me to help you.
                Example – how to use the two last isConsistent functions:
                -	[two algorithms WipeOutR_FM and WipeOutR_T](https://github.com/AIG-ist-tugraz/WipeOutR/tree/main/src/main/java/at/tugraz/ist/ase/wipeoutr/algorithm)

<!-- Links -->
[`ChocoConsistencyChecker`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/ca-cdr-package/src/main/java/at/tugraz/ist/ase/cacdr/checker/ChocoConsistencyChecker.java