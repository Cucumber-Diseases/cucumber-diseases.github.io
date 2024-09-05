# Exercise 001: Implement Missing Then Implementation
:link: [Related Smell: 001 - Missing Then Implementation](/smells/001-missing-then)

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
        * The relevant step is `Given the customer first name is "Max"`and `And the customer last name is "Mustermann"`.
        * Look at the implementation in the step definition, how it clutters the scenario and the initialized fields.
        * Identify an existing consistent expression instead.

    ??? tip "Step by Step Walkthrough"
        * The relevant step is `Given the customer first name is "Max"`and `And the customer last name is "Mustermann"`.
        * The consistent way to initialize `firstName`and `lastName` is the step `Given the customer name is Rose Smith`
        * Replace the original steps with `Given the customer name is Max Mustermann`
        * Delete the dead step implementations `Given the customer first name is "Max"`and `And the customer last name is "Mustermann"`.
