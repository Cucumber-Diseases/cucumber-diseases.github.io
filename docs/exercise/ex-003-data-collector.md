# Exercise 003: Remove Data Collector
:link: [Related Smell: 003 - The Data Collector](/smells/003-data-collector)

## Purpose
* Learn to identify the `The Data Collector` smell.
* Recognize how multiple `Given`steps 

## Your Task
Within the `Customer.feature` file there is a scenario with multiple `Given` steps, each collecting a part of the data needed in the following `When` step. Identify the data collector and replace it with a consistent implementation.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for a scenario with multiple `Given` steps for creating customers.

    ??? tip "Hint B"
        * The relevant steps is `` and .
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
    
