# Exercise 010: Replace Hardcoded Parameters
:link: [Related Smell: 010 - Hardcoded Parameters](/smells/010-hardcoded-parameters)

## Purpose
* Learn to identify the `Hardcoded Parameters` smell.
* Understand which complications arise from having empty step definitions and how to spot them.

## Your Task
Within the `Customer.feature` file there is a `When` and `Then` step a hardcoded parameter. Find at least
one such step definition and implement the correct assertion.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for steps with hardcoded paramters in the business calls.
        * Hardcoded paramters can be of any type. In our exercise you neeed to find two strings

    ??? tip "Hint B"
        * The relevant step is `When the customer Sabine Mustermann is searched` and `Then the customer Sabine Mustermann can be found`.
        * Look in the `Customer.feature` file how it's used. 
        * Are there any similar occurrances?
        * What is you next step?

    ??? tip "Step by Step Walkthrough"
        * The relevant step is `When the customer Sabine Mustermann is searched` and `Then the customer Sabine Mustermann can be found`.
        * We introduce parameters for `firstName`and `secondName`. Implement it like in `Given the customer name is ...`.
        * The step with the expression `Then the customer can be found` is similar but uses fields instead orf paramters.
    

=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/af50463422630062a14596d66164249274249fe4)
    
    === "Python"

    === "C#"

    === "Go"


