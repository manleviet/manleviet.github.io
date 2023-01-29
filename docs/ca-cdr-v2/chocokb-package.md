---
layout: default
title: chocokb-package
parent: CA-CDR-V2
nav_order: 3
permalink: ca-cdr-v2/chocokb-package
---

# chocokb-package
{: .no_toc }
{: .d-inline-block }

v1.3.9-alpha-52
{: .label .label-green }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

| **groupID**    | **_at.tugraz.ist.ase_** |
|----------------|-------------------------|
| **artifactID** | **_choco-kb-v2_**       |
| **version**    | **_1.3.9-alpha-42_**    |

## `FMKB`

In the current version of this package, the [**FMKB**](https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/chocokb-package/src/main/java/at/tugraz/ist/ase/kb/fm/FMKB.java)
class is generic.

The following code shows how to create a FMKB object with a feature model as an input.

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/smartwatch.sxfm");

// create a parser for the given file
@Cleanup("dispose")
FeatureModelParser<Feature, AbstractRelationship<Feature>, CTConstraint> parser = FMParserFactory.getInstance().getParser(fileFM.getName());

// parse the feature model file
FeatureModel<Feature, AbstractRelationship<Feature>, CTConstraint> fm = parser.parse(fileFM);

// create a FMKB object with the given feature model and requires to generate the negation of constraints
FMKB<Feature, AbstractRelationship<Feature>, CTConstraint> kb = new FMKB<>(fm, true);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## Other examples

- [Unit tests](https://github.com/manleviet/CA-CDR-V2/tree/21-uses-generics-for-feature-model/chocokb-package/src/test/java/at/tugraz/ist/ase/kb/fm)



[//]: # (The package allows to manage a CSP representation of a knowledge base/feature model using an abstract class [**KB**]&#40;&#41;.)

[//]: # (It provides the following functionalities:)

[//]: # ()
[//]: # (You can implement your knowledge base by inheriting the [**KB**]&#40;&#41; class.)

[//]: # (You can find an implementation of **Renault** and **PC** knowledge bases in here and here.)

[//]: # (You can also find an implementation of a CSP representation for feature models &#40;**FMKB** class&#41; in here.)

[//]: # (The input of **FMKB** is a **FeatureModel** object &#40;from [fm-package]&#40;&#41;&#41;.)

[//]: # (So, you can use **FMKB** for all feature models you have, i.e., no need to implement a specific [**KB**]&#40;&#41; class compared to **PC** or **Renault**.)

[//]: # ()
[//]: # (For each KB &#40;KB class&#41;, you will have a list of variables &#40;Variable class&#41;, each variable has a domain &#40;Domain class&#41;, and a list of constraints &#40;Constraint class&#41;. There are two types of variables, i.e., integer variables &#40;IntVariable class&#41; and bool variables &#40;BoolVariable class&#41;.)

[//]: # ()
[//]: # (For feature models, each feature is a bool variable.)

[//]: # (For Renault and PC, each variable is an integer variable.)

[//]: # ()
[//]: # (Each Constraint class manages many Choco constraints and maybe many negations of these Choco constraints. Negative Choco constraints are very important to the WipeOutR algorithms.)

[//]: # ()
[//]: # (Why does a Constraint object manage many Choco constraints?)

[//]: # (A Constraint object represents a CSP constraint. In Choco Solver, a CSP constraint will be translated into many Choco constraints in some cases. For example, in the following figure, line 46 shows a CSP constraint “4wheel = yes => type = xdrive”. After executing line 46, we have 4 Choco constraints in the model &#40;see the panel Debug&#41;.)

[//]: # (![]&#40;img/Picture 1.png&#41;)

[//]: # ()
[//]: # (Example – how to use Variable, Domain, and Constraint classes:)

[//]: # (-	3 unit tests)

[//]: # (-	PC knowledge base &#40;focus on the functions defineDomains, defineVariables, and defineConstraints&#41;)

[//]: # (-	FMKB &#40;focus on the functions defineDomains, defineVariables, and defineConstraints&#41;)

[//]: # ()
[//]: # (Example – how to create and use an object of FMKB, PCKB, and RenaultKB:)

[//]: # (-	FMKB)

[//]: # (-	PCKB)

[//]: # (-	RenaultKB)

[//]: # (-	KBStatistics)
