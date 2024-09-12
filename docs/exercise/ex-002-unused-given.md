# Exercise 002: Remove Unused Given Parameter
:link: [Related Smell: 002 - Unused Given Parameter](/smells/002-unused-given)

## Purpose
* Learn to identify the `Unused Given Parameter` smell.
* Understand how to clean it up and how to find all occurances spread over different locations.

## Your Task
Within the step implementation file there is field, which is intialized by a `Given`step in the `Customer.feature`but never used. Find at least
one such field and remove the code and the step.

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
        * Remove the step `And the customer's birthday is 2000/03/19` in the `Customer.feature` file.

=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/0599fd71870bc62255c9b1d7a6c2a012fa1ad7e9)
    
    === "Python"

    === "C#"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-csharp/commit/879feb59ee2abf83a8e37598b2237624c4c69d4d)

    === "Go"


