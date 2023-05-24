---
layout: default
title: CDRModels
parent: CA-CDR-V2
nav_order: 4
permalink: ca-cdr-v2/cdrmodel
---

# CDRModels
{: .no_toc }
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.3.9-alpha-53</span>
{: .label .label-purple }

<dl style="width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd style = "text-transform: lowercase"><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd style = "text-transform: lowercase"><em>cdrmodel-v2</em></dd>
</dl>{: .label .label-yellow }

The input of consistency-based algorithms, such as WipeOutR_T or WipeOutR_FM, is a set of constraints or test cases.
Therefore, CDRModels are created to manage/prepare the constraints/test cases before passing them to the algorithms.

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

The abstract class CDRModel manages:
-	a set of constraints which we assume to be always correct (a background knowledge) – correctConstraints.
-	a set of constraints that could be faulty – possiblyFaultyConstraints.
We denote correctConstraints as B and possiblyFaultyConstraints as C in some consistency-based algorithms.
New CDRModel inheritance needs to override the initialize function, where we add constraints from the KB class to sets of constraints, i.e., add correct constraints to correctConstraints and possible faulty constraints to possiblyFaultyConstraints.
You can directly pass constraints from the KB class to consistency-based algorithms. However, in this case, it’s challenging to manage your code. With CDRModels, you know where you need to take care of constraints that will be passed to algorithms.
For the WipeOutR project, a new CDRModel class needs to implement the interface IDebuggingModel, which requires the new class to provide a set of test cases. In this context, the initialize function needs an additional step to translate test cases into Choco constraints.
The TestCaseBuilders can only read and create TestCase objects. It couldn’t translate these test cases into Choco constraints since it doesn’t know the Choco Model, in which these test cases will be checked. On the contrary, CDR models hold a Choco Model taken from a KB object. So, the responsibility of translating test cases into Choco constraints belongs to CDR models and should be implemented inside the initialize function.

## [`FMCdrModel`] and [`FMDebuggingModel`]

The [`FMCdrModel`] and [`FMDebuggingModel`] classes are representations of knowledge-based models for diagnosis tasks,
debugging tasks as well as analysis operations of feature models.
The main purpose of these classes is to manage two sets of constraints, i.e., a background knowledge `B`
and a set of constraints to be diagnosed `C`.
These two sets of constraints are used as inputs for the diagnosis algorithms.

These classes are generic now.
The following codes shows how to use them:

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/survey.fm4conf");

// create a parser for the given file
@Cleanup("dispose")
FeatureModelParser<Feature, AbstractRelationship<Feature>, CTConstraint> parser = FMParserFactory.getInstance().getParser(fileFM.getName());
// parse the feature model file
FeatureModel<Feature, AbstractRelationship<Feature>, CTConstraint> fm = parser.parse(fileFM);

// create a FMCdrModel object
FMCdrModel<Feature, AbstractRelationship<Feature>, CTConstraint>
    model = new FMCdrModel<>(fm, true, false, true);
model.initialize(); // assigns the constraints to the background knowledge and the constraints to be diagnosed

// create a checker
ChocoConsistencyChecker checker = new ChocoConsistencyChecker(testCaseModel);

// get the CF
List<Constraint> CF = new LinkedList<>(testCaseModel.getPossiblyFaultyConstraints());

// execute the WipeOutR_FM to identify the redundancy-free feature model
WipeOutR_FM wipeOut = new WipeOutR_FM(checker);
reset(); // reset timers and counters
List<Constraint> newCF = wipeOut.run(CF);

System.out.println("Redundancy-free feature model:");
newCF.forEach(System.out::println);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/survey.fm4conf");

// create a parser for the given file
@Cleanup("dispose")
FeatureModelParser<Feature, AbstractRelationship<Feature>, CTConstraint>
    parser = FMParserFactory.getInstance().getParser(fileFM.getName());
// parse the feature model file
FeatureModel<Feature, AbstractRelationship<Feature>, CTConstraint>
    fm = parser.parse(fileFM);

// read the test suite using a TestSuiteBuilder
TestSuiteReader builder = new TestSuiteReader();
FMTestCaseBuilder testCaseFactory = new FMTestCaseBuilder();
@Cleanup InputStream is = getInputStream(FMDebuggingModelTest.class.getClassLoader(), "survey.testcases");

TestSuite testSuite = builder.read(is, testCaseFactory);

FMTestCaseTranslator translator = new FMTestCaseTranslator();
// create a debugging model object
FMDebuggingModel<Feature, AbstractRelationship<Feature>, CTConstraint> model = new FMDebuggingModel<>(fm, testSuite, translator, false, true, false);
model.initialize(); // assigns the constraints to the background knowledge and the constraints to be diagnosed

// create a checker
ChocoConsistencyChecker checker = new ChocoConsistencyChecker(model);

// execute the DirectDebug to identify the faulty constraints
DirectDebug directDebug = new DirectDebug(checker);
reset(); // reset timers and counters
Map.Entry<Set<ITestCase>, Set<Constraint>> result = directDebug.findDiagnosis(model.getPossiblyFaultyConstraints(),
                                                                            model.getCorrectConstraints(),
                                                                            model.getTestcases());

// print the result
Set<Constraint> diag = result.getValue();
System.out.println("\t\tDiag: " + diag);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## Other examples

- [Unit tests of FMDebuggingModel](https://github.com/manleviet/CA-CDR-V2/tree/21-uses-generics-for-feature-model/cdrmodel-package/src/test/java/at/tugraz/ist/ase/cdrmodel/fm)
- [WipeOutRFMTest](https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/ca-cdr-package/src/test/java/at/tugraz/ist/ase/cacdr/algorithms/WipeOutRFMTest.java)
- [DirectDebugTest](https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/ca-cdr-package/src/test/java/at/tugraz/ist/ase/cacdr/algorithms/DirectDebugTest.java)

Example – how to create a new CDRModel that implements the interface IDebuggingModel:
-	[WipeOutR_T_Model1](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/test/java/at/tugraz/ist/ase/wipeoutr/testmodel/WipeOutR_T_Model1.java)
-	[WipeOutR_T_Model2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/test/java/at/tugraz/ist/ase/wipeoutr/testmodel/WipeOutR_T_Model2.java)
-	[WipeOutRTModel.java](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/model/WipeOutRTModel.java)
-	[WipeOutRFMModel.java](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/model/WipeOutRFMModel.java)
Example – how to use the above models:
-	[RuntimeForTestcasesV2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/RuntimeForTestcasesV2.java)
-	[WipeOutTEvaluationV2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/WipeOutRTEvaluationV2.java)
-	[SolverRuntimeEvaluation](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/SolverRuntimeEvaluation.java)
-	[WipeOutFMEvaluationV2](https://github.com/AIG-ist-tugraz/WipeOutR/blob/main/src/main/java/at/tugraz/ist/ase/wipeoutr/app/eval/WipeOutRFMEvaluationV2.java)
