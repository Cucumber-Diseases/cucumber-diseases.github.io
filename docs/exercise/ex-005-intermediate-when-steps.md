# Exercise 005: Refactor Intermediate When Steps
:link: [Related Smell: 005 - Intermediate When Steps](/smells/005-intermediate-when-steps)

## Purpose
* Learn to identify the `Intermediate When Steps` smell.
* Learn how to avoid multiple `When`steps and understand that multiple actions lead to unclear scenarios.

## Your Task
Within the `Customer.feature` file there are scenerios with multiple `When` steps. One of those stores an intermediate result to verify it afterwards. Find the `When`steps and merge them so that the intermediate result is not necessary anymore.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for a second intermediate `When` step that is searching for all customers.
        * Make sure you also consider `And` steps.

    ??? tip "Hint B"
        * The relevant step is `And all customers are searched`
        * Look at the implemenation. Why is the `When`step necessary?

    ??? tip "Hint C"
        * The relevant step is `And all customers are searched`
        * The `And all customers are searched` stores a count, which is checked by the `Then`step.
        * Check the name of the scenario, how can the existing steps be replaced with a step which expresses the intention more clearly?

    ??? tip "Step by Step Walkthrough"
        * The relevant step is `And all customers are searched`
        * The scenario is create a customer and find it afterwords. 
        * Searching and counting doesn't clearly express this business need.
        * Instead the `Then`step should find by name the created customer and check if it matches.
        * Replace `And all customers are searched` and `Then the number of customers found is 1` with `Then the customer can be found`

=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/9cb5d2440e2d7bcf6caeb846e2ea3befe05c4625)
    
    === "Python"

    === "C#"

    === "Go"