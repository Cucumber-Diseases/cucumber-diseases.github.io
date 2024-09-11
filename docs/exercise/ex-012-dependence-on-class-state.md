# Exercise 011: Remove Dependence on Class State
:link: [Related Smell: 011 - Dependence on Class State](/smells/011-dependence-on-class-state)

## Purpose
* Learn to identify the `Dependence on Class State` smell.
* Understand how complexity increases from having shared data on multiple places instead of local parameters.

## Your Task
The step implementation has different fields i.e class state, which can be grouped by system under test, input data and results. 
We want to get rid of the input data and replace it with local parameters and variables.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * Identify the three groups of class state in your step implementation:
            * system under test
            * input data
            * results

    ??? tip "Hint B"
        * The input data state is storing information about the customers to be created: first name, last name, ...
        * Remove the first name and last name and analyse the compiler errors.
        * What else can we remove now?

    ??? tip "Hint C"
        * Remove the first name and last name.
        * Remove all `Given`steps in your step implementation and in the `Customer.feature` file dealing with first name and last name. 
        * How can we deal with the missing data in the `When` and `Then` steps that instead?

    ??? tip "Hint D"
        * Remove the first name and last name.
        * Remove all `Given`steps in your step implementation and in the `Customer.feature` file dealing with first name and last name. 
        * Add the parameters `firstName` and `lastName` to 'When the customer is created'. 
        * Remove `Then the customer can be found` because there is already a expression with the parameters.
        * Change the `Customer.feature` file accordingly and pass the parameters via the steps.
        * Which class state can be remove now?

    ??? tip "Step by Step Walkthrough"
        * Remove the first name and last name.
        * Remove all `Given`steps in your step implementation and in the `Customer.feature` file dealing with first name and last name. 
        * Add the parameters `firstName` and `lastName` to 'When the customer is created'. 
        * Remove `Then the customer can be found` because there is already a expression with the parameters.
        * Change the `Customer.feature` file accordingly and pass the parameters via the steps.
        * Remove the state for handling a second customer in the same way as previously the first name and last name.
        * Pass parameters to the expression for the second customer. 
        * Merge the expression and delete the unnecessary functions for example: 'Then the customer {} {} can be found'  and 'Then the second customer {} {} can be found' 
    
=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/b04a747098b0813640f6c7ac35bc163c54465967)
    
    === "Python"

    === "C#"

    === "Go"


