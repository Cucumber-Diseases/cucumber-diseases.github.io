# Exercise 010: Replace Hardcoded Parameters
:link: [Related Smell: 010 - Hardcoded Parameters](/smells/010-hardcoded-parameters)

## Purpose
* Learn to identify the `Missing Then Step` smell.
* Understand which complications arise from having empty step definitions and how to spot them.

## Your Task
Within the `Customer.feature` file there is a `Then` step that does not do anything. Find at least
one such step definition and implement the correct assertion.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for a `Then` step that is verifying if a customer was created successfully.

    ??? tip "Hint B"
        * The relevant step is `Then the customer creation should be successful`.
        * Look at the implementation of the code in te step definition.

    ??? tip "Hint C"
        * The relevant step is `Then the customer creation should be successful`.
        * The step definition is an empty function that does not do anything.
        * Think of what it should actually do and implement the correct assertion.

    ??? tip "Step by Step Walkthrough"
        * The relevant step is `Then the customer creation should be successful`.
        * The step definition is an empty function that does not do anything.
        * The function should implement an assertion of the error field.
        * Assert that the error field (e.g. `this.error` in java or `t.err` in go) is null.
    
