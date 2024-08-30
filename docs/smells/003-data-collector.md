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

## Your taks
Find the “Data Collector” in the customer.feature file. Replace the multiple 'Given' steps with a single step that passes the entire data object (from the same domain) at once.