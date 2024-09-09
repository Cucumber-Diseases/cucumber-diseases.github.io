# Exercise 013: Refactor Test Code Impurity
:link: [Related Smell: 013 - Test Code Impurity](/smells/013-test-code-impurity)

## Purpose
* Learn to identify the `Test Code Impurity` smell.
* See how this smell differs from the other smells and how complicated the refactoring is about, if there is already a lot of test automation code available.

## Your Task
We will only change the step implementation file. Create a new file and add a driver implementation. Move all calls to the system under test to the driver class.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * How can we split the refactoring to reduce the risk?

    ??? tip "Hint B"
        * We have steps that deal with the creation and steps that provide the search business logic.
        * Which is the simplest first refactoring?

    ??? tip "Hint C"
        * The simplest refactoring is moving the code from the step `Given there is a customer` and `Given there are some customers` to a driver class.
        * Why is this so simple?

    ??? tip "Hint D"
        * The simplest refactoring is moving the code from the step `Given there is a customer` and `Given there are some customers` to a driver class.
        * It handles only the `Given` steps to create customers in the system under test and it doesn't deal with state in the test implementation.
        * We can create the new class and inject the driver into the step implementation.
        * Then create a new method and move the code into it. Replace the code with a call to the driver instead.
        * How to continue?
    
    ??? tip "Step by Step Walkthrough"
        * The simplest refactoring is moving the code from the step `Given there is a customer` and `Given there are some customers` to a driver class.
        * It handles only the `Given` steps to create customers in the system under test and it doesn't deal with state in the test implementation.
        * We can create the new class and inject the driver into the step implementation.
        * Then create a new method and move the code into it. Replace the code with a call to the driver instead.
        * Next we continue with the customer creation in the `When`steps. 
        * Start with a public `error` field in the driver and access it in the step implementation.
        * Then encapsulate the `error` with a method to check if the creation failed or was successful.
        * Next move the search business logic to the driver class.
        * Finally cleanup your step implementation. You get rid of the system under test and all fields dealing with results. There is only a reference to the driver class.


=== "Diffs"
    === "Java"
        :link: [GitHub Commit](https://github.com/Cucumber-Diseases/cucumber-diseases-java/commit/7f1bc88a325fd86a4e42b8a75a363e2195af6a0a)
    
    === "Python"

    === "C#"

    === "Go"


