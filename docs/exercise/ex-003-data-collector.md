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
        * You are looking for a `Then` step that is verifying if a customer was created successfully.

    ??? tip "Hint B"
        * The relevant step are `Given the customer first name is "Max"`and `And the customer last name is "Mustermann"`.
        * Look at the implementation in the step definition, how it clutters the scenario and the initialized fields.
        * Identify an existing consistent expression instead.

    ??? tip "Step by Step Walkthrough"
        * The relevant step are `Given the customer first name is "Max"`and `And the customer last name is "Mustermann"`.
        * The consistent way to initialize `firstName`and `lastName` is the step `Given the customer name is Rose Smith`
        * Replace the original steps with `Given the customer name is Max Mustermann`
        * Delete the dead step implementations `Given the customer first name is "Max"`and `And the customer last name is "Mustermann"`.
    
