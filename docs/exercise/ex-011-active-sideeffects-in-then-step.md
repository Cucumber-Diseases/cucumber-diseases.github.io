# Exercise 012: Refactor Active Side Effects in Then Step
:link: [Related Smell: 012 - Active Side Effects in Then Step](/smells/012-active-sideeffects-in-then-step)

## Purpose
* Learn to identify the `Active Side Effects in Then Step` smell.
* Recognize the misuse when changing an application state in a `Then`step.

## Your Task
The step implementation consists two `Then` steps that changes the data of the system under tests. 
Find the `Then` steps with the smell and move the state change to a fitting `When` step.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for a `Then` steps that deal with the verification of the second customer.

    ??? tip "Hint B"
        * The relevant step are `Then the second customer creation should fail` and `Then the second customer can be found`.
        * Look at the implementation of the code in the step definition.
        * Which code is concerning the active side effect?

    ??? tip "Hint C"
        * The relevant step are `Then the second customer creation should fail` and `Then the second customer can be found`.
        * Both implementations are creating a new customer object!
        * Where does this code belong to?

    ??? tip "Step by Step Walkthrough"
        * The relevant step are `Then the second customer creation should fail` and `Then the second customer can be found`.
        * Both implementations are creating a new customer object!
        * Remove the creation of the customer object.
        * Create the customer in the step `When the second customer is created` instead. 
        * Implement it similar as in `When the customer is created`.
        * Should we merge the expressions of `When the customer is created` and `When the second customer is created`, or keep it?
    
=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/16a21fa3d5411ab632a831d81ad1a6e930ae4513)
    
    === "Python"

    === "C#"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-csharp/commit/43d56bf2cbdea90cf1e88487cafc39fdbf42d2ce)

    === "Go"


