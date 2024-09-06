# Exercise 007: Remove Rotting Steps
:link: [Related Smell: 007 - Rotting Steps](/smells/007-rotting-steps)

## Purpose
* Learn to identify the `Rotting Steps` smell.
* Understand which complications arise from having empty step definitions and how to spot them.

## Your Task
Within the `Customer.feature` file there is a `Given` step that is useless. It's describing a precondition in a scenario, which is given anyway.
Find the step definition and remove it.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for an unnecessary `Given` step in one of the user creation scenarios.  
        * It is added at the begining and it suspicious because the other creation scenarios don't provide it

    ??? tip "Hint B"
        * It's the step `Given there are no customers'.
        * The step is called **only** in the scenario 'Scenario: Should find newly created customer`
        * Look at the implementation of the code in the step definition.

    ??? tip "Step by Step Walkthrough"
        * The relevant step is `Given there are no customers'.
        * The step is called **only** in the scenario 'Scenario: Should find newly created customer`
        * The step definition is an empty function that does not do anything.
        * Remove the step from the scenarion and replace the `And` in the following step with `Given`.
        * Delete the step implementation to avoid the `Dead Steps`smell.

=== "Diffs"
    === "Java"
        GitHub Commit (https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/707c18efc3edab9785dd3a11338147892cfd0119)
    
    === "Python"

    === "C#"

    === "Go"
