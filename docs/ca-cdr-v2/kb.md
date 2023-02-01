---
layout: default
title: Knowledge Bases
parent: CA-CDR-V2
nav_order: 1
permalink: ca-cdr-v2/kb
---

# Knowledge Bases
{: .no_toc }
{: .d-inline-block }

v1.3.9-alpha-52
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd><em>choco-kb-v2</em></dd>
</dl>{: .label .label-yellow }

**CA-CDR-V2** allows to represent knowledge bases as [Constraint Satisfaction Problems].
_choco-kb-v2_ provides classes managing a (Choco) CSP representation of a knowlege base.

{: .highlight }
Feature model is a type of knowledge represention.
For more details related to what **CA-CDR-V2** supports for feature models, we refer to [Feature model].

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Features

_choco-kb-v2_ provides the following features:

- An abstract [`KB`] class managing variables ([`Variable`]), variable domains ([`Domain`]), and constraints ([`Constraint`]) of a knowledge base/feature model.
- Two types of variables:
    1. Integer variables ([`IntVariable`])
    2. Boolean variables ([`BoolVariable`])
- Two interfaces specifying the behaviors of the knowledge base:
    1. [`IIntVarKB`] returns Choco's [`IntVar`]
    2. [`IBoolVarKB`] returns Choco's [`BoolVar`]
- [`Constraint`] manages corresponding Choco constraints, as well as their negation.
- Two utility builder [`IntVarConstraintBuilder`] and [`BoolVarConstraintBuilder`] help to build a [`Constraint`] object from a list of Choco constraints.
- Already encoded knowledge bases:
    1. [`FMKB`] - an implementation for a CSP representation of a feature model.
    The input of [`FMKB`] is a [`FeatureModel`] object.
    So you can use [`FMKB`] for any feature models you have, i.e., no need to implement a specific [`KB`] class for an individual feature model.
    [`FMKB`] uses [`BoolVariable`]s, and conforms [`IBoolVarKB`]. [`FMKB`] uses [`BoolVarConstraintBuilder`] to build constraints.
    2. [`PCKB`] - an implementation of [PC Configuration Knowledge Base].
    [`PCKB`] uses [`IntVariable`]s, and conforms [`IIntVarKB`]. [`PCKB`] uses [`IntVarConstraintBuilder`] to build constraints.
    3. [`RenaultKB`] - an implementation of [Renault Configuration Knowledge Base].
    [`RenaultKB`] uses [`IntVariable`]s, and conforms [`IIntVarKB`]. [`RenaultKB`] uses [`IntVarConstraintBuilder`] to build constraints.
    4. [`CameraKB`] - an implementation of [Camera Configuration Knowledge Base].
    [`CameraKB`] uses [`IntVariable`]s, and conforms [`IIntVarKB`]. [`CameraKB`] uses [`IntVarConstraintBuilder`] to build constraints.
- [`Assignment`] class represents an assignment of a value to a variable.
It could represent a CSP assignment or a SAT clause, e.g., `F1 = true`.
Besides, it could represent a preference of a user requirement, e.g., `Modell = limousine`.
- Two interfaces [`IAssignmentsTranslatable`] and [`ILogOpCreatable`] specifying the behaviors of a translator from an assignment to Choco constraints.
[`FMAssignmentsTranslator`] is a specific translator for feature model's assignments.
- Utility functions for variables ([`VariableUtils`]) and constraints ([`ConstraitUtils`])

{: .highlight }
Negative constraints are used in the algorithms [WipeOutR_T](algorithms/wipeoutr_t), [WipeOutR_FM](algorithms/wipeoutr_fm).

## How tos

### Encoding your own knowledge base

You can implement your knowledge base by inheriting the [`KB`] class.

{: .important-title }
> Examples
>
> [`PCKB`], [`FMKB`]

### Creating a [`FMKB`] object for a feature model readed from a file

The following code shows how to create a [`FMKB`] object for a feature model which is parsed from a file.

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/smartwatch.sxfm");

// create a parser for the given file
@Cleanup("dispose")
FeatureModelParser<Feature, AbstractRelationship<Feature>, CTConstraint>
    parser = FMParserFactory.getInstance().getParser(fileFM.getName());

// parse the feature model file
FeatureModel<Feature, AbstractRelationship<Feature>, CTConstraint>
    fm = parser.parse(fileFM);

// create a FMKB object with the given feature model and requires to generate also the negative constraints
FMKB<Feature, AbstractRelationship<Feature>, CTConstraint>
    kb = new FMKB<>(fm, true);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{: .highlight }
For more examples related to feature models, we refer to [Feature model].

### Creating and using an object of [`FMKB`], [`PCKB`], [`RenaultKB`], and [`CameraKB`]

{: .important-title }
> Examples
>
> [`KBStatistics`], [FMKBTests], [PCKBTest], [RenaultKBTest], and [CameraKBTest]

### Implementing a new assignment translator

{: .important-title }
> Example
>
> [`FMAssignmentsTranslator`]

### How to for Utility functions

TBD
{: .label .label-yellow }

<!-- Links -->
[Feature model]: fm
[Constraint Satisfaction Problems]: https://en.wikipedia.org/wiki/Constraint_satisfaction_problem
[PC Configuration Knowledge Base]: https://www.itu.dk/research/cla/externals/clib/
[Renault Configuration Knowledge Base]: https://www.itu.dk/research/cla/externals/clib/
[Camera Configuration Knowledge Base]: https://www.itu.dk/research/cla/externals/clib/
[`KB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/KB.java
[`Variable`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/Variable.java
[`IntVariable`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/IntVariable.java
[`BoolVariable`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/BoolVariable.java
[`IIntVarKB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/IIntVarKB.java
[`IBoolVarKB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/IBoolVarKB.java
[`IntVar`]: https://choco-solver.readthedocs.io/en/latest/2_modelling.html
[`BoolVar`]: https://choco-solver.readthedocs.io/en/latest/2_modelling.html
[`Domain`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/Domain.java
[`Constraint`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/Constraint.java
[`IntVarConstraintBuilder`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/builder/IntVarConstraintBuilder.java
[`BoolVarConstraintBuilder`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/builder/BoolVarConstraintBuilder.java
[`Assignment`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/Assignment.java
[`FMAssignmentsTranslator`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/translator/fm/FMAssignmentsTranslator.java
[`IAssignmentsTranslatable`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/translator/IAssignmentsTranslatable.java
[`ILogOpCreatable`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/core/translator/ILogOpCreatable.java
[`VariableUtils`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/common/VariableUtils.java
[`ConstraitUtils`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/common/ConstraintUtils.java
[`FMKB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/fm/FMKB.java
[`CameraKB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/camera/CameraKB.java
[`RenaultKB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/renault/RenaultKB.java
[`PCKB`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/pc/PCKB.java
[`FeatureModel`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/fm-package/src/main/java/at/tugraz/ist/ase/fm/core/FeatureModel.java
[`KBStatistics`]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/app-KBStatistics/src/main/java/at/tugraz/ist/ase/kb/app/KBStatistics.java
[FMKBTests]: https://github.com/manleviet/CA-CDR-V2/tree/third_release/chocokb-package/src/test/java/at/tugraz/ist/ase/kb/fm
[PCKBTest]: https://github.com/manleviet/CA-CDR-V2/tree/third_release/chocokb-package/src/test/java/at/tugraz/ist/ase/kb/pc
[RenaultKBTest]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/test/java/at/tugraz/ist/ase/kb/renault/RenaultKBTest.java
[CameraKBTest]: https://github.com/manleviet/CA-CDR-V2/blob/third_release/chocokb-package/src/test/java/at/tugraz/ist/ase/kb/camera/CameraKBTest.java