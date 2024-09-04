# 001: Missing Then Implementation

This smell refers to steps within your Gherkin scenarios that lack assertions (specifically, `Then` steps).
When you encounter a step without an assertion, it means that the scenario doesn’t verify any expected outcome or behavior.
Essentially, it’s like having a test case without an assertion in your test suite.

## Impact
!!! bug "Missing System Validation"
    Without assertions, your scenarios may not effectively validate the system’s behavior.

!!! bug "Makes BDD Irrelevant"
    It undermines the purpose of behavior-driven development (BDD) because the scenarios don’t provide meaningful feedback.

!!! danger "False-Negatives"
    Unverified steps can lead to false negatives (where a scenario passes even if it shouldn’t).

## Required Action
Identify all steps within your Gherkin scenarios that lack assertions. Then, choose one of these steps to implement the missing assertion.

Decide which criteria apply and select the step depending on your answers:

* **Simplicity**: Selected for a straightforward  step
* **Relevance**: Ensure that the selected step makes sense in your scenarios
* **No Further Improvement Needed**: Confirm that there’s no additional enhancement required for the chosen step.
*Reverse Implementation: Check if there’s another `Then` step that expresses the opposite behavior

## Code Examples
=== "Java"
    ```java title="CustomerStepDefinitons.java"
    @Then("the customer creation should be successful")
    public void theCustomerCreationShouldBeSuccessful() {
       //(1)!
    }
    ```

    1. Note that the step `Then the customer creation should be successful` contains no code. It should contain a `assert`-Statement.

=== "Python"
    ```python title="features/steps/steps.py"
    @then(u'the customer creation should be successful')
    def step_impl(context):
        pass #(1)!
    ```

    1. Note that the step `Then the customer creation should be successful` contains no code. It should contain a `assert`-Statement.

=== "C#"
    ```csharp title="StepDefinitions/CustomerStepDefinitions.cs"
    [Then("the customer creation should be successful")]
    public void ThenTheCustomerCreationShouldBeSuccessful()
    {
        //(1)!
    }
    ```

    1. Note that the step `Then the customer creation should be successful` contains no code. It should contain a `assert`-Statement.

=== "Go"
    ```go
    func (t *CustomerTestSteps) theCustomerCreationShouldBeSuccessful(ctx context.Context) error {
        return nil //(1)!
    }
    // ...

    func InitializeScenario(sc *godog.ScenarioContext) {
    // ...

    sc.Then(`the customer creation should be successful`, t.theCustomerCreationShouldBeSuccessful)
    
    // ...
    }
    ```

    1. Note that the step `Then the customer creation should be successful` contains no code. It should contain an assertion.
