# Overview
In this section we list all the Cucumber/Gherkin/BDD smells we catelogued. Navigate to any specific diseases to learn about the details!

## What are code smells?
The term code smell was originally mentioned by Kent Beck as explained by Martin Fowler’s [description](https://www.martinfowler.com/bliki/CodeSmell.html) of code smells.

!!! quote ""

    "A code smell is a surface indication that usually corresponds to a deeper problem in the system." 
    
    Kent Beck, Martin Fowler

While a code smell doesn't necessarily mean the code is incorrect or non-functional, it suggests that the code may be poorly designed, difficult to maintain, or prone to bugs. Code smells often point to deeper issues in the codebase that could lead to more significant problems if not addressed.

There are several lists of code smells available online. One of the most well-known is found in Martin Fowler’s book Refactoring. Additionally, you can explore other widely recognized lists on platforms such as Wikipedia, [Coding Horror](https://blog.codinghorror.com/code-smells/) and [Refactoring Guru](https://refactoring.guru/refactoring/smells). These resources provide comprehensive overviews of common code smells and offer insights into best practices for identifying and addressing them.

## Description of Smells
All Cucumber smells are described in the same layout to make it easier for you to navigate. The all

* Start with a description of the smell
* *Impact:* Describe the impact if present in your tests
* *Required Action*: Tell you what you need to do and lists different alternative solutions in order to remove them.
* *Code Samples*: Examples in some programming languages to show you how it looks in the wild.

## Rating of Impacts
In order to make it easier for you to understand the severity of the impacts described in the smells, there is a simple rating system in place:

<div class="grid cards" markdown>
- !!! bug "Makes your tests useless. It is a bug. Remove immediately."
- !!! danger "Introduces a grave problem that will screw up in the near future. Get rid of it asap!"
- !!! failure "This is a problem. It will not bite you immediately, but increases technical debt drastically. Future maintenance is impacted."
- !!! warning "It is a concern. You can live with it for some time, but it will bite your back in a couple of months."
</div>

Regardless of the rating, all the impacts described are a problem. The whole purpose of this list is to educate you how to prevent them. So, there's no arguing about getting even rid of concerns. We would not talk about it, if it would not be relevant.

## List of all Smells
| ID# | Name | Short Description |
|-----|------|-------------|
| [001](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [002](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [003](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [004](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [005](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [006](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [007](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [008](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [009](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [010](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [011](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [012](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
| [013](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
