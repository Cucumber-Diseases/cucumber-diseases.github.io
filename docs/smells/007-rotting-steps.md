# 007: Rotting Steps

“Rotting Steps” refer to Gherkin steps within a scenario that lack meaningful purpose or relevance.
These steps may have empty implementations or contribute nothing substantial to the scenario.
They often appear in `Given` steps, where they set up initial conditions but fail to add value.

## Impact

!!! danger "Misleading Code"
    Readers may assume these steps play a crucial role when they don’t.

!!! failure "Harder Maintenance"
    Empty or irrelevant steps require unnecessary upkeep.

!!! warning "Scenario Clutter"
    Unnecessary steps make scenarios harder to read and understand.

## Required Action
Eliminate steps that don’t contribute to the behavior being tested. Indicators are:

* `Given` step used only once and implicitly setup,
* `Given` steps covered already by a `Background` step or scenario initialisation (e.g. default starting conditions)
* Empty implementations


## Code Examples

```gherkin title="Customer.feature"
Scenario: Should find newly created customer
    Given there are no customers # (1)!
    And the customer name is Rose Smith
    When the customer is created
    Then the customer can be found
```
1. The step `Given there are no customers` does not add any value as this is the default condition for a scenario. It is verbose expressiveness without adding function or value to the step.
