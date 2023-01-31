---
layout: default
title: Configurator
parent: CECore
nav_order: 5
permalink: ce-core/ce
---

# Configurator
{: .no_toc }
{: .d-inline-block }

v1.1.2-alpha-10
{: .label .label-purple }

<dl style="background:#FEFBE7; border:solid 1px black; width:400px;">
    <dt><strong>groupID</strong></dt>
    <dd><em>at.tugraz.ist.ase</em></dd>
    <dt><strong>artifactID</strong></dt>
    <dd><em>ce</em></dd>
</dl>

TBD
{: .label .label-yellow }

<!-- Supports two modes: -->
<!-- 1. Compact mode -->
<!-- 2. Control mode -->

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<!-- {% capture code %} -->
<!-- {% highlight java linenos %} -->
<!-- // create a configurator -->
<!-- Configurator configurator = new Configurator(kb, true, new FMSolutionTranslator()); -->

<!-- // initilize the configurator with KB or with not(KB) -->
<!-- configurator.initializeWithKB(); -->
<!-- // configurator.initializeWithNotKB(); -->

<!-- // identify solutions -->
<!-- configurator.find(43, 0); -->

<!-- // reset the configurator -->
<!-- configurator.reset(); -->

<!-- // print out the solutions -->
<!-- for (Solution s : configurator.getSolutions()) { -->
<!--     System.out.print(++counter + " " + s + " - "); -->
<!-- } -->

<!-- Sau khi reset, nếu thực hiện tìm lại thì sẽ lấy lại các solutions cũ. -->
<!-- {% endhighlight %} -->
<!-- {% endcapture %} -->
<!-- {% include fix_linenos.html code=code %} -->
<!-- {% assign code = nil %} -->

<!-- {: .highlight } -->
<!-- After resetting, -->

<!-- Example 1: Sử dụng vòng lặp tìm cho đến khi nào hết solutions thì dùng -->

<!-- Configurator configurator = new Configurator(kb, true, new FMSolutionTranslator()); -->
<!-- configurator.initializeWithKB(); -->

<!-- // Identify solutions -->
<!-- while (configurator.find(1, 0, null)) { -->
<!--     // Do something with the solution -->
<!--     } -->

<!-- configurator.reset(); -->