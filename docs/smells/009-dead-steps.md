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

When changing or refactoring scenarios or step implementations periodically review your step definitions and remove unused ones. Use version control history to identify steps that were once relevant but are no longer needed.

## Code Examples
These code examples are a bit harder to show as we are looking for some steps that are defined in the implementation that are never used within the Gherkin feature files. There are some telltale signs, such as missing functionality in the step definition code that can point to such smells though.

=== "Java"
    ```java title="CustomerStepDefinitions.java"
    @Given("there are no customers") // (1)!
    public void thereAreNoCustomers() {
    }

    @Given("no customers exist")
    public void noCustomersExist() {
    }
    ```

    1. The steps `there are no customers` and `no customers exist` have a similar meaning. You can clearly see that none of them really has any functionality, which may also hint to the [Rotten Steps smell](/smells/007-rotting-steps). If none of these are used in any of the scenarios they are to be considered `dead steps`.

=== "Python"
    ```python title="features/steps/steps.py"
    @given("there are no customers") # (1)!
    def step_impl(comtext):
        pass

    @given("no customer exists")
    def step_impl(comtext):
        pass

    ```

    1. The steps `there are no customers` and `no customers exist` have a similar meaning. You can clearly see that none of them really has any functionality, which may also hint to the [Rotten Steps smell](/smells/007-rotting-steps). If none of these are used in any of the scenarios they are to be considered `dead steps`.

=== "C#"
    ```csharp title="CustomerStepDefinitions.cs"
    [Given("there are no customers")] // (1)!
    public void GivenThereAreNoCustomers()
    {
    }

    [Given("are no customers")]
    public void GivenNoCustomersExists()
    {
    }
    ```
    
    1. The steps `there are no customers` and `no customers exist` have a similar meaning. You can clearly see that none of them really has any functionality, which may also hint to the [Rotten Steps smell](/smells/007-rotting-steps). If none of these are used in any of the scenarios they are to be considered `dead steps`.

=== "Go"
    ```go title="customer_test.go"
    func InitializeScenario(sc *godog.ScenarioContext) {
        // ...
        sc.Given(`there are no customers`, t.thereAreNoCustomers)       // (1)!
	    sc.Given(`no customers exist`, t.noCustomersExist)
        // ...
    }

    
    func (t *CustomerTestSteps) thereAreNoCustomers(ctx context.Context) error {
        return nil
    }

    func (t *CustomerTestSteps) noCustomersExist(ctx context.Context) error {
        return nil
    }
    ```

    1. The steps `there are no customers` and `no customers exist` have a similar meaning. You can clearly see that none of them really has any functionality, which may also hint to the [Rotten Steps smell](/smells/007-rotting-steps). If none of these are used in any of the scenarios they are to be considered `dead steps`.
