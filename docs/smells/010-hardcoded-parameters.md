# 010: Hardcoded Parameters

“Hardcoded Parameters” occur when Gherkin scenarios use fixed, literal values instead of parameters or placeholders.
Instead of leveraging reusable parameters, steps directly reference specific values.
This leads to redundancy, as multiple steps end up performing the same action with hardcoded data.

## Impact

!!! failure "Harder Maintenance"
    Steps with identical hardcoded values create unnecessary repetition. If a value changes, you must update it in multiple places.

!!! failure "Unreadable Code"
    Non parameterized steps reduce the scenario readability. Parameterization allows flexibility and reusability.

## Required Action
Check your code for step definitions that use data that could be exchanged with other data (e.g. names, dates, quantities, ...) but are not parametrized within the step implementation code. 

When introducing new steps or refactoring existing steps make sure that you are parametrizing potentially exchangeable parts of the step that are actually data. For example in the step 

```gherkin 
Given there is a user born on 1970-01-01
```

the date of `1970-01-01` should be a parameter in the step definition and not hardcoded.

* **Leverage Parameter Handling**: Implement a new step with placeholders and parameters for dynamic values. Replace all hardcoded steps with the new step and remove the previous step implementations.
* **Ensure Consistent Syntax**: Standardize the parameter handling syntax across all step definitions to improve readability and maintainability.
* **Reuse Existing Steps**: If a parameterized version exists, ensure consistent usage.
* **Avoid Duplication in Scenarios**: Merge similar scenarios to a data driven test ('Scenario Outline' in Gherkin) and provide mulitple examples in tables.

## Code Examples
=== "Java"
    ```java title="CustomerStepDefinitions.java"
    @When("the customer Sabine Mustermann is searched") // (1)!
    public void theCustomerSabineMustermannIsSearched()
    {
        _count = _customerService.FindCustomers("Sabine", "Mustermann").Count;
    }
    ```

    1. In the step definition the name `Sabine Mustermann` is hard coded. It should be a parameter instead that can be changed to e.g. `Rose Smith` to avoid duplicates for the same functionality but slightly different scenarios.

=== "Python"
    ```python title="features/steps/steps.py"
    @when(u'the customer Sabine Mustermann is searched') # (1)!
    def step_impl(context):
       context.count = len(context.service.search_customers("Sabine", "Mustermann"))   
    ```

    1. In the step definition the name `Sabine Mustermann` is hard coded. It should be a parameter instead that can be changed to e.g. `Rose Smith` to avoid duplicates for the same functionality but slightly different scenarios.

=== "C#"
    ```csharp title="CustomerStepDefinitions.cs"
    [When("the customer Sabine Mustermann is searched")] // (1)!
    public void WhenTheCustomerSabineMustermannIsSearched()
    {
        _count = _customerService.FindCustomers("Sabine", "Mustermann").Count;
    }
    ```
    
    1. In the step definition the name `Sabine Mustermann` is hard coded. It should be a parameter instead that can be changed to e.g. `Rose Smith` to avoid duplicates for the same functionality but slightly different scenarios.

=== "Go"
    ```go title="customer_test.go"
    func InitializeScenario(sc *godog.ScenarioContext) {
        // ...
        sc.When(`the customer Sabine Mustermann is searched`, t.theCustomerSabineMustermannIsSearched)
        // ...
    }

    // (1)!
    func (t *CustomerTestSteps) theCustomerSabineMustermannIsSearched(ctx context.Context) error {
	   t.count = len(t.customerService.SearchCustomersByName("Sabine", "Mustermann"))
	   return nil
    }

    ```

    1. In the step definition the name `Sabine Mustermann` is hard coded. It should be a parameter instead that can be changed to e.g. `Rose Smith` to avoid duplicates for the same functionality but slightly different scenarios.
