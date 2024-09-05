# Exercise 002: Remove Unused Given Parameter
:link: [Related Smell: 002 - Unused Given Parameter](/smells/002-unused-given)

## Purpose
* Learn to identify the `Unused Given Parameter` smell.
* Understand how to clean it up and how to find all occurances spread over different locations.

## Your Task
Within the step implementation file there is field, which is intialized by a `Given`step in the `Customer.feature`but never ued. Find at least
one such fieldkd and remove the code and the step.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for a field in the step implementation, which is set but not read.

    ??? tip "Hint B"
        * The relevant field is `birthday`.
        * Search for all occurances.

    ??? tip "Hint C"
        * The relevant field is `birthday`.
        * The field `birthday` is only initialized in the step `And the customer's birthday is 2000/03/19`.
        * Search for other occurances of a date in the code.

    ??? tip "Step by Step Walkthrough"
        * The relevant field is `birthday`.
        * The field `birthday` is only initialized in the step `And the customer's birthday is 2000/03/19`.
        * A default birthday is passed to the business function 'Add Customer' in multiple steps.
        * Decide to use the default birthday, since there is no assertion on the correct birthday.
        * Remove the in the step from the step implementation file .
        * Remove the in `Custoer.feature' the step `And the customer's birthday is 2000/03/19`.
    
