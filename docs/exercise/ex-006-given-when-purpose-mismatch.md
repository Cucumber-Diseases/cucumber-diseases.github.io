# Exercise 006: Refactor Given/When Purpose Mismatch
:link: [Related Smell: 006 - Given/When Purpose Mismatch](/smells/006-given-when-purpose-mismatch)

## Purpose
* Learn to identify the `Given/When Purpose Mismatch` smell.
* Understand the different meaning of the steps `Given`versus `When` even the functionality is the same.

## Your Task
Within the `Customer.feature` file there are multiple occurances of this smell. The exercise is prepared in a way that you only need to refactor steps in the scenarios. Be aware that this is not always the case.  
Find all scenarios with the smell and replace the `When` steps with `Given` instead.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * Find all occurances of the smell. You are looking for three scenarios.

    ??? tip "Hint B"
        * The first occurance is here:
        ```
        Scenario: Should be able to create two customer with different names
            Given the customer name is Max Mustermann
            When the customer is created
            Given the second customer is Sabine Mustermann
            When the second customer is created
            Then the second customer can be found
        ```
        * Identify which `When` should become a `Given` step.
        * What's wrong using a `When` step?

    ??? tip "Hint C"
        * The step `When the customer is created` should be replaced.
        * This `When` has two purposes: create an customer and focus on the error handling in the code. 
        * We only want to verified the creation of the 2nd customer, the 1st is the `Given/When Purpose Mismatch` smell.
        * Which existing 'Given' step can we you instead?

    ??? tip "Step by Step Walkthrough"
        * The step `When the customer is created` should be replaced.
        * We can use this `Given` step insted:
        ```
        Given there is a customer
            | Max | Mustermann |    
        ```
        Find the two remaining `Given/When Purpose Mismatch` smells

    ??? tip "Remove all smells"
        * Repeat the previous solution in the scenario `Scenario: Cannot create two customer with the same name` and `Scenario: Should find customers by name`


=== "Diffs"
    === "Gherkin"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/cf2078f5a223f96665d33d460dc465d55114f9d7)
