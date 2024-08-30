# Overview
In this section we list all the Cucumber/Gherkin/BDD smells we catelogued. Navigate to any specific diseases to learn about the details!

## Desciption of Smells
All Cucumber smells are described in the same layout to make it easier for you to navigate. The all

* Start with a description of the smell
* *Impact:* Describe the impact if present in your tests
* *You Task*: Tell you what you need to do in order to remove them.

## Rating of Impacts
In order to make it easier for you to understand the severity of the impacts described in the smells, there is a simple rating system in place:

<div class="grid cards" markdown>
- !!! bug "Makes your tests useless. It is a bug. Remove immediately."
- !!! danger "Introduces a grave problem that will screw up in the near future. Get rid of it asap!"
- !!! failure "This is a problem. It will not bite you immediately, but increases technical debt drastically. Future maintenance is impacted."
- !!! warning "It is a concern. You can live with it for some time, but it will bite your back in a couple of months."
</div>

## List of all Smells
| ID# | Name | Short Description |
|-----|------|-------------|
| [001](001-missing-then.md) | Missing 'Then' Implementation | A scenario lacks a `Then` step or an assertion in the step, leaving it essentially unverfied |
