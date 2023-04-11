---
layout: default
title: TestCase and TestSuite
parent: CA-CDR-V2
nav_order: 3
permalink: ca-cdr-v2/testing
---

# TestCase and TestSuite
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.3.9-alpha-52</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>cdrmodel-v2</em></dd>
</dl>{: .label .label-yellow }

In Knowledge Base Enginering, test cases are used to induce conflicts in the knowledge base.
**CA-CDR-V2** provides also Test Case Driven Algorithms [4].
Thus, _cdrmodel-v2_ provides base classes for managing test cases and test suites.

{: .highlight }
For more details related to knowledge base test cases, we refer to [4] in [References].

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What the package provides

### [`TestCase`]

A test case is a conjunction of assignments, e.g., `A=a1 & B=b3 & C=c2 & ...`,
where `A=a1` is an assignment, ‘&’ represents an AND operator.
To feature models, test cases are simpler, e.g., `A & ~B & C`,
where `A` represents `A=true` and `~B` represents `B=false`.

A test suite is a set of test cases.

_cdrmodel-v2_ provides the following classes:

1.	[`ITestCase`] – an interface that defines which functionalities every type of test case needs to support.
In another project, I have a new type of test case called [`AggregatedTestCase`].
2.	[`TestCase`] – a test case that manages a list of assignments, a corresponding list of Choco constraints, and maybe a corresponding list of negative Choco constraints.
3.	[`TestSuite`] – manages a list of [`ITestCase`].
4.	[`TestSuiteBuilder`] – provides a function (`buildTestSuite`) that reads a test suite from a test suite file.
A test suite file will contain a total number of test cases in the first line and each test case written in other lines.
If you need to support other structures of test suite files, you need to implement the interface `ITestSuiteBuildable`.
5.	[`FMTestCaseBuilder`] – provides the capability of translating a feature model test case into a `TestCase` object.
To support other test case types (such as [Renault] test case - `Var1 = S64 & Var3 = M9`), you need to implement the interface `ITestCaseBuildable`.

## How tos

### Using [`TestCase`] and [`TestSuite`] classes

{: .important-title }
> Examples
>
> -	[Unit tests]()
> -	[WipeOutR_T_Model1](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/test/java/at/tugraz/ist/ase/wipeoutr/testmodel/WipeOutR_T_Model1.java)
> -	[WipeOutR_T_Model2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/test/java/at/tugraz/ist/ase/wipeoutr/testmodel/WipeOutR_T_Model2.java)
> -	[RuntimeForTestcasesV2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/RuntimeForTestcasesV2.java)
> -	[WipeOutTEvaluationV2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/WipeOutRTEvaluationV2.java)


TBD
{: .label .label-yellow }

<!-- Links -->
[References]: /references