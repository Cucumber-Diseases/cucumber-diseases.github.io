# Exercise 004: Refactor Redundant Mirror Image
:link: [Related Smell: 004 - Redundant Mirror Image](/smells/004-redundant-mirror-image)

## Purpose
* Learn to identify the `Redundant Mirror Image` smell.
* Recognize the pattern of duplication even though the expressions are asymmetric.

## Your Task
Within the step implementation are two steps with a similar implemention but an asymmetric expression. Find those steps and merge the expressions.


## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for two `When` steps that are creating a customer with exactly the same implementation.

    ??? tip "Hint B"
        * The relevant steps are `When the customer is created` and `When an invalid customer is created`.
        * Think about how to merge the code in the step implementation.

    ??? tip "Step by Step Walkthrough"
        * The relevant steps are `When the customer is created` and `When an invalid customer is created`.
        * Move the expression `When an invalid customer is created` to the implementation of `When the customer is created`.
        * Rename the name of the function to something more general.
        * Remove the code of `When an invalid customer is created`.
    
