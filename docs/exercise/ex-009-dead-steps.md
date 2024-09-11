# Exercise 009: Remove Dead Steps
:link: [Related Smell: 009 - Dead Steps](/smells/009-dead-steps)

## Purpose
* Learn to identify the `Dead Steps` smell.
* Learn how to search for dead steps and why it's important to remove them asap instead.

## Your Task
Within the step implementation there are 3 steps that are not used by the `Customer.feature`file. 
Find and delete them.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * After solving some exercises and understanding the business, you have maybe an idea which steps are unused.
        * Review the `Customer.feature`file and then scroll through the step implementation, do you find it?

    ??? tip "Hint B"
        * Two steps are empty at all, that means they provide no functionality.
        * The third step implements the negation of finding a customer.

    ??? tip "Hint C"
        * The relevant steps are 
            * `Given no customers exist`
            * `When the customer Rose Smith is searched`
            * `Then the customer can not be found`
        * Brainstorm why this steps are not used anymore

    ??? tip "Step by Step Walkthrough"
        * The relevant steps are 
            * `Given no customers exist`
            * `When the customer Rose Smith is searched`
            * `Then the customer can not be found`
        * Possible explainations:
            * The step was copied and renamed
            * Somebody didn't find a step and created a similar one
            * It was replaced with parameters or the input data in the scenario was changed
            * Gold plating: implement a step for the future even if currently not used
        * Remove the implementation from the step definition file.
    
=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/cb0b2d68fb727dc34597e2ea5072831d3fa37d59)
    
    === "Python"

    === "C#"
        The reqnroll extensions of MS Visual Studio provides a popup menue `Find unused Step Definitions`. That's the easiest way to solve this smell.

    === "Go"
