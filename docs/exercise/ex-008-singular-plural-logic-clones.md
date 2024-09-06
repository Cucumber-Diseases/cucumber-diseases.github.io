# Exercise 008: Merge Singular-Plural Logic Clones
:link: [Related Smell: 008 - Singular-Plural Logic Clones](/smells/008-singular-plural-logic-clones)

## Purpose
* Learn to identify the `Singular-Plural Logic Clones` smell.
* Understand what complications arise from merging similar step definitions and how to spot them.

## Your Task
Within the step implementation there is a singular and plural expression with a similar implementation. Find 
the 2 steps, learn how to merge them and which complications you shoud consider.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking two `Given` steps: first, creation of a single customer and second multiple customers.

    ??? tip "Hint B"
        * The relevant steps are `Given there is a customer` and `Given there are some customers`.
        * Look at the implementation of the code in the step definition. 
        * How can we merge the implementation? What kind of conflicts do we expect?

    ??? tip "Step by Step Walkthrough"
        * The relevant steps are `Given there is a customer` and `Given there are some customers`.
        * We move the two expression in the code over one implementation i.e. two expression and one function
        * The problem is that the single case doesn't expect a header. So we need to add the header in all scenarios in the `Customer.feature` file, too.

=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/c95d3624178dc279fff2cbfb5dcf48af3f70aa9d)
    
    === "Python"

    === "C#"

    === "Go"
