# 011: Dependence on Class State
This code smell occurs when everything is stored either in a context or in the fields of your step implementation. Often, this state is even duplicated because we prepared the state of the application previously. This can lead to tightly coupled tests that are difficult to maintain and understand.

## Impact

!!! failure "Unreadable Code"
    Tests become harder to understand as the state of the application is scattered across multiple locations.
    
!!! failure "Harder Maintenance"
    Changes to the system under test may require extensive modifications to step definitions, increasing maintenance effort.

!!! failure "Increased Complexity"
    The codebase becomes more complex and difficult to manage due to the use of class state over different steps.

!!! warning "Increased Coupling"
    Tests become tightly coupled to the system's state, making them less reusable and more prone to breaking. Further they become less reliable if the state of the application is not properly managed or controlled.

## Required Action

!!! warning "TODO"
    describe details of exercise

* **Pass Data Explicitly**: Reduce the reliance on class state by passing data directly to step definitions as parameters.
* **Avoid Premature Data Gathering**: Gather data only when needed. If data can be collected later in the scenario, defer its retrieval to a later step and pass it to the subsequent steps as necessary.
* **Reuse Application State**: Don't hold data twice in your application and in your test classes. Prefer the usage of test data in your application state for example a database instead of temporary storage in your objects.
* **Use Scenario Context Sparingly**: While scenario context can be useful, avoid overusing it. Limit the amount of data stored in the context to essential information. Consider whether a step really needs access to the entire context or if a smaller subset suffices.

## Code Examples
!!! warning "TODO"
To understand this smell, please refer to the Gherkin code as well as the code in the implementation in one of the programming languages. It makes the most sense if the scenarios and the implementation are both read together.

### Gherkin
```gherkin title="Customer.feature"

# (1)!
Scenario: ...

```

1. Notes ...

### Step Implementation
=== "Java"
    ```java title="CustomerStepDefinitions.java"
    ...
    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.
    
=== "Python"
    ```python title="features/steps/steps.py"
    ...
    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.


=== "C#"
    ```csharp title="CucumberDiseases.Specs/StepDefinitions/CustomerStepDefinitions.cs"
    ...
    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.

=== "Go"
    ```go title="customer_test.go"
    ...
    ```

    1. The functions `thereIsACustomer` and `thereAreSomeCustomers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.
