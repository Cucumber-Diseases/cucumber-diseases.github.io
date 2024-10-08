# Exercise 010: Replace Hardcoded Parameters
:link: [Related Smell: 010 - Hardcoded Parameters](/smells/010-hardcoded-parameters)

## Purpose
* Learn to identify the `Hardcoded Parameters` smell.
* Understand how hardcoded parameters are introducing duplication and decreasing flexibility in your code.

## Your Task
Within the `Customer.feature` file there is a `When` and `Then` step witn a hardcoded parameter. Find at least
one such step definition and implement the correct assertion.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for steps with hardcoded paramters in the business calls. 
        * A hardcoded parameter is expressed in the Gherkin expression.
        * Hardcoded paramters can be of any type. In our exercise you neeed to find two strings.

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
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/39a124e645f3fb991464c0761e2f295a442f98ed)
    
    === "Python"

    === "C#"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-csharp/commit/dcae9c64e59b87511165a5e901cc402bc2a50491)

    === "Go"


