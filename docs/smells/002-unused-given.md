# 002: Unused Given Parameter

This code smell occurs when a field or property is initialized within a `Given` step but remains unused throughout the scenario.
Essentially, it’s like setting up a variable or resource but never actually utilizing it in subsequent steps.

Possible reasons include:

* Redundancy: The parameter duplicates information already available elsewhere.
* Obsolete Logic: The parameter was relevant in an earlier version of the scenario but is no longer necessary.
*Incomplete Implementation: The parameter was added but not fully integrated into the scenario.

## Impact
!!! danger "Misleading Code"
    They can mislead readers into thinking that the parameter plays a crucial role in the scenario.

!!! failure "Harder Maintenance"
    Maintenance becomes harder as unused parameters accumulate over time.

!!! failure "Increased Complexity"
    Unused parameters clutter the scenario and add unnecessary complexity.

## Required Action
Search your code for any field/property which is initialized by a step but never used afterwards. Find these fields, analyze why it is not used and decide either to remove it or to use it: 

* **Remove It**: If the parameter serves no purpose, eliminate it.
* **Use It**: If the parameter has a valid role, ensure it’s utilized appropriately.

## Code Examples

=== "Gherkin"
    ```gherkin title="Customer.feature"
        Scenario: Should successfully create new customer
        Given the customer first name is "Max"
        And the customer last name is "Mustermann" # (1)
        And the customer's birthday is 2000/03/19 
        When the customer is created
        Then the customer creation should be successful
    ```


    1. Mind that `birthday` is set but not checked in the `Then` steps. The `birthday` is also not evaluated in any hidden assertions within the `Then the customer creation should be successful` step.
