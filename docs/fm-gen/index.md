---
layout: default
title: FMGenerator
nav_order: 6
permalink: fm-gen
---

# Synthesized Feature Model Generator
{: .d-inline-block }

<span style = "text-transform: lowercase">v1.3</span>
{: .label .label-green }

`fm_gen` is a Java `jar` tool that generates synthesized feature models on the basis of the [Betty framework].

## Parameters

The tool supports the following parameters:

| parameter |required|default value| description |
|:---|:---|:---|:---|
|-h|no| - | prints the app's usage info |
|`-c`|yes| - |number of relationships and cross tree constraints|
|`-fm`|yes| - |number of generated feature models|
|`-ctc`|no| `0.8` |ratio of cross tree constraints|
|`-g`|no|`5`|maximum of generations, used in the evolutionary generator|
|`-out`|no|`./`|folder saving generated feature models|

## How it works

The number of features in each generated feature model is specified by the following formula:
```java
numFeatures = numConstraints * 3 / 4;
```

In case of `numFeatures < 10`, the tool uses the _Random generation_.
Otherwise, it uses an [_Evolutionary generator_].

Generated feature models are saved in the [SPLOT format].

## Usage

**Download**: [Latest (v1.3)]{: .label .label-green }

**Requirements**: [Latest Java]{: .label .label-green }

**Syntax**:
```bash
java -jar fm_gen.jar [-h] -c <#constraints> -fm <#generated_feature_models> [-ctc <ratio_cross_tree_constraints>] [-g <#max_generations>] [-out <path_to_folder>]
```

[Latest (v1.3)]: https://github.com/manleviet/CA-CDR-V2/releases/tag/fm-gen-v1.3
[Betty framework]: https://www.isa.us.es/betty/welcome
[_Evolutionary generator_]: https://www.isa.us.es/betty/documentation
[SPLOT format]: http://www.splot-research.org
[Latest Java]: https://www.java.com/en/download/manual.jsp