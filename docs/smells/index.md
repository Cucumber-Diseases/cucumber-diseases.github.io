# Overview
In this section we list all the Cucumber/Gherkin/BDD smells we catelogued. Navigate to any specific diseases to learn about the details!

## Desciption of Smells
All Cucumber smells are described in the same layout to make it easier for you to navigate. The all

* Start with a description of the smell
* *Impact:* Describe the impact if present in your tests
* *You Task*: Tell you what you need to do in order to remove them.
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
