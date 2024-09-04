# 003: The Data Collector

The “Data Collector” code smell occurs within your “Given” steps in Gherkin scenarios.
It’s related to the use of the Builder pattern, where you set the values of fields incrementally across multiple steps.
By passing data piece by piece, this pattern leads to long scripts with individual steps for each field.

## Impact
!!! failure "Harder Maintenance"
    Any change to the domain object requires updating multiple steps.

!!! failure "Increased Complexity"
    Readers must follow a sequence of steps to understand the complete data setup.

!!! failure "Increased Coupling" 
    The coupling between scenarios and step implementation increases, especially when the order of steps matters. Changes in one step may ripple through others, affecting the entire scenario.

!!! warning "Increased Script Length"
    The scenario becomes verbose due to numerous steps dedicated to setting field values.

## Required Action
Replace multiple `Given` steps with a single step that passes the entire data object (from the same domain) at once. If required introduce a new step that initializes a domain object with all parameters required in a single step.

## Code Examples

### Gherkin
```gherkin
Scenario: Should successfully create new customer
    Given the customer first name is "Max"
    And the customer last name is "Mustermann"
# (1)!
    When the customer is created
    Then the customer creation should be successful
```

1. The data for a customer is collected in two different steps. Merge the steps to pass the data at once instead.
