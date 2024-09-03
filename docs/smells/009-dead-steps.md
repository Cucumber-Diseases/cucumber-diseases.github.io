# 009: Dead Steps

“Dead Steps” refer to step implementations that exist within your codebase but are not used by any feature file.
These steps may have been created for various reasons (e.g., experimentation, incomplete scenarios, or refactoring) but are now obsolete.
Detecting and removing them can be challenging because they don’t contribute to any scenario.

## Impact
!!! failure "Harder Maintenance"
    Dead steps clutter your test codebase, making it harder to maintain.

!!! failure "Cusing Confision" 
    Developers and testers may wonder why certain steps exist without corresponding scenarios.

!!! warning "Potential Misuse"
    If someone accidentally uses a dead step, it can lead to false positives or negatives in test results and increas complexity and maintenance efforts later on.

## Required Action
Search for the `Dead Steps` in the step implementation file. Either use the tools provided in your IDE or the search functionality. If a step is not used, analyse the history or look out for similar steps. A reason for `Dead Steps` are incomplete refactorings due to renaming expressions or new steps in scenarios instead of reusage. 

Delete the unused steps from the code and commit your changes. 

In your daily business periodically review your step definitions and remove unused ones. Use version control history to identify steps that were once relevant but are no longer needed.

## Code Examples
=== "Java"
    ```java title="src/test/java/org/training/customer/CustomerStepDefinitions.java"
    @Given("there are no customers") //(1)!
    public void thereAreNoCustomers() {
    }

    @Given("no customers exist")
    public void noCustomersExist() {
    }
    ```
    1. The steps `there are no customers` and `no customers exist` have a similar meaning. Only one step is used by the scenarios in the `Customer.feature`. It seems that somebody created a new step instead of reusing the existing.

=== "Python"
    ```python title="features/steps/steps.py"

    ```

=== "C#"
    ```csharp title="CucumberDiseases.Specs/StepDefinitions/CustomerStepDefinitions.cs"

    ```

=== "Go"
    ```go title="customer_test.go"

    ```
