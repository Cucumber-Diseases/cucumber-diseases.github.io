# 010: Hardcoded Parameters

“Hardcoded Parameters” occur when Gherkin scenarios use fixed, literal values instead of parameters or placeholders.
Instead of leveraging reusable parameters, steps directly reference specific values.
This leads to redundancy, as multiple steps end up performing the same action with hardcoded data.

## Impact

!!! failure "Harder Maintenance"
    Steps with identical hardcoded values create unnecessary repetition. If a value changes, you must update it in multiple places.

!!! failure "Unreadable Code"
    Non parameterized steps reduce the scenario readability. Parameterization allows flexibility and reusability.

## Required Action
Check your code for step definitions that use data that could be exchanged with other data (e.g. names, dates, quantities, ...) but are not parametrized within the step implementation code. 

When introducing new steps or refactoring existing steps make sure that you are parametrizing potentially exchangeable parts of the step that are actually data. For example in the step 

```gherkin 
Given there is a user born on 1970-01-01
```

the date of `1970-01-01` should be a parameter in the step definition and not hardcoded.

* Parameterize: Implement a new step with placeholders and parameters for dynamic values. Replace all hardcoded steps with the new step and remove the previous step implementations.
* Reuse Existing Steps: If a parameterized version exists, ensure consistent usage.
* Merge similar scenarios to a 'Scenario Outline'

## Code Exmaples
tbd