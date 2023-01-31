---
layout: default
title: Feature Model Analysis
parent: CECore
nav_order: 2
permalink: ce-core/fma
---

# Feature Model Analysis
{: .no_toc }
{: .d-inline-block }

v1.1.2-alpha-10
{: .label .label-green }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Simple usage

The following example shows a simple usage:

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/basic_featureide_redundant1.xml");

// 1. Create the factory for anomaly feature models
IFeatureBuildable featureBuilder = new AnomalyAwareFeatureBuilder();
FMParserFactory<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    factory = FMParserFactory.getInstance(featureBuilder);

// 2. Create the parser
@Cleanup("dispose")
FeatureModelParser<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    parser = factory.getParser(fileFM.getName());

// 3. Parse the feature model
FeatureModel<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    featureModel = parser.parse(fileFM);

// 4. Create an analyzer
FMAnalyzer analyzer = new FMAnalyzer(featureModel);

// 5. Select analysis operations to be performed
EnumSet<AnomalyType> options = EnumSet.of(AnomalyType.DEAD,
    AnomalyType.FULLMANDATORY,
    AnomalyType.REDUNDANT);

// 6. Generate VoidFMAnalysis, DeadFeatureAnalysis, FullMandatoryAnalysis, and RedundancyAnalysis
// And Run the analyzer
// (true - trigger the corresponding explanator if the assumption is violated)
analyzer.generateAndRun(options, true);

// 7. Print the result
AutomatedAnalysisExplanation explanation = new AutomatedAnalysisExplanation();
System.out.println(explanation.getDescriptiveExplanation(analyzer.getAnalyses(), options));
// generated explanations depends on options
// in this case where options don't include VOID, the VoidFMAnalysis' results won't be printed
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

If you want to perform all built-in analyses, you can replace the statement in Step 5 by the following statement:

{% capture code %}
{% highlight java linenos %}
EnumSet<AnomalyType> options = EnumSet.allOf(AnomalyType.class);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## Usage of the `FMAnalyzer`'s `run()` method

Use this method if you read test cases from a file.

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/basic_featureide_redundant1.xml");

// 1. Create the factory for anomaly feature models
IFeatureBuildable featureBuilder = new AnomalyAwareFeatureBuilder();
FMParserFactory<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    factory = FMParserFactory.getInstance(featureBuilder);

// 2. Create the parser
@Cleanup("dispose")
FeatureModelParser<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    parser = factory.getParser(fileFM.getName());
// 3. Parse the feature model
FeatureModel<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    featureModel = parser.parse(fileFM);

// 4. Create an analyzer
FMAnalyzer analyzer = new FMAnalyzer(featureModel);

// 5. Read test cases from a file and add to analyzer
...

// 6. Run the analyzer
// (true - trigger the corresponding explanator if the assumption is violated)
// execute the VoidFMAnalysis first if there is any
analyzer.run(true);

// 8. Print the result
EnumSet<AnomalyType> options = EnumSet.allOf(AnomalyType.class);
    AutomatedAnalysisExplanation explanation = new AutomatedAnalysisExplanation();
    System.out.println(explanation.getDescriptiveExplanation(analyzer.getAnalyses(), options));
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## [`AutomatedAnalysisBuilder`] and [`AutomatedAnalysisExplanation`]

These classes are utility classes that provides useful and shortcut ways to build built-in analyses
and to explain the results of analyses.
However, you can also use directly specific builder and explanation classes to build and explain analyses.
The following example shows how to analysis dead features by using [`DeadFeatureAnalysisBuilder`] and [`CompactExplanation`]:

{% capture code %}
{% highlight java linenos %}
File fileFM = new File("src/test/resources/bamboobike_featureide_deadfeature1.xml");

// 1. Create the factory for anomaly feature models
IFeatureBuildable featureBuilder = new AnomalyAwareFeatureBuilder();
FMParserFactory<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    factory = FMParserFactory.getInstance(featureBuilder);

// 2. Create the parser
@Cleanup("dispose")
FeatureModelParser<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    parser = factory.getParser(fileFM.getName());
// 3. Parse the feature model
FeatureModel<AnomalyAwareFeature, AbstractRelationship<AnomalyAwareFeature>, CTConstraint>
    featureModel = parser.parse(fileFM);

// 4. Create an analyzer
FMAnalyzer analyzer = new FMAnalyzer(featureModel);

// (omitted) 5. Select analysis operations to be performed

// 6. Generates analyses and add them to the analyzer (USING DeadFeatureAnalysisBuilder)
DeadFeatureAnalysisBuilder deadFeatureAnalysisBuilder = new DeadFeatureAnalysisBuilder();
deadFeatureAnalysisBuilder.build(featureModel, analyzer);

// 7. Run the analyzer
// (true - trigger the corresponding explanator if the assumption is violated)
analyzer.run(true);

// 8. Print the result (USING CompactExplanation)
CompactExplanation explanation = new CompactExplanation();
System.out.println(explanation.getDescriptiveExplanation(analyzer.getAnalyses(), DeadFeatureAnalysis.class, AnomalyType.DEAD));
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

{: .note }
> [`CompactExplanation`] provides explanations for four analyses, including `DeadFeatureAnalysis`, `FalseOptionalAnalysis`,
> `FullMandatoryAnalysis`, and `ConditionallyDeadAnalysis`.

## How to monitor the progress of analysis

Before executing the analyzer, you can register a listener to monitor the progress of analysis.

{% capture code %}
{% highlight java linenos %}
analyzer.setMonitor(new ProgressMonitor()); // MONITOR
// 7. Run the analyzer
analyzer.run(true);
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

In this way, the program will print the progress of analysis to the console.

_Example_: [testLargeModel_2]

## How to add a new analysis operation

1. Create a new enum type that conforms the interface [`IAnomalyType`].
2. Create a new "Assumptions" class that conforms the class [`IFMAnalysisAssumptionCreatable`].
Assumptions classes are used to generate test cases for the analysis operation.
3. Create a new "Analysis" class that extends the class [`AbstractFMAnalysis`].
Analysis classes are used to perform the analysis operation.
4. Create a new "Explanator" class that extends the class [`AbstractAnomalyExplanator`].
Explanator classes are used to identify diagnoses for violated assumptions.
5. Create a new "Builder" class that conforms the class [`IAnalysisBuildable`].
Builder classes are used to generate analyses.
6. Create a new "Explanation" class that conforms the class [`IAnalysisExplanation`].
Explanation classes are used to generate explanations for the analysis results.

<!-- Links -->
[`AutomatedAnalysisBuilder`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/builder/AutomatedAnalysisBuilder.java
[`AutomatedAnalysisExplanation`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/explanation/AutomatedAnalysisExplanation.java
[`DeadFeatureAnalysisBuilder`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/builder/DeadFeatureAnalysisBuilder.java
[`CompactExplanation`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/explanation/CompactExplanation.java
[`IAnomalyType`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/anomaly/IAnomalyType.java
[`IFMAnalysisAssumptionCreatable`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/assumption/IFMAnalysisAssumptionCreatable.java
[`AbstractFMAnalysis`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/analysis/AbstractFMAnalysis.java
[`AbstractAnomalyExplanator`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/explanator/AbstractAnomalyExplanator.java
[`IAnalysisBuildable`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/builder/IAnalysisBuildable.java
[`IAnalysisExplanation`]: https://github.com/manleviet/CA-CDR-V2/blob/21-uses-generics-for-feature-model/fma/src/main/java/at/tugraz/ist/ase/fma/explanation/IAnalysisExplanable.java
[testLargeModel_2]: https://github.com/manleviet/CA-CDR-V2/blob/720fd21afa83caac8c2d8604632b7c595e6e8abe/fma/src/test/java/at/tugraz/ist/ase/fma/FMAnalyzerTest.java#L785