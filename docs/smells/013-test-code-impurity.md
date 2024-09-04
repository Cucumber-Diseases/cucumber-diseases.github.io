# 013: Test Code Impurity

“Test Code Impurity” occurs when the step definition contains significant business logic, resulting in tightly coupled test code. In other words, the test code becomes heavily reliant on the syntax and intricacies of the system under test (SUT). This tight coupling makes the test suite challenging to maintain and less adaptable to changes in the SUT.

## Impact

!!! failure "Unreadable Code"
    When business logic is mixed with test code, it becomes harder to understand the purpose of each step. Developers may struggle to differentiate between actual test steps and implementation details.

!!! failure "Harder Maintenance"
    As the system evolves, maintaining and updating the test code becomes cumbersome. Changes to business rules may require modifications across multiple step definitions, increasing the risk of errors.
    
!!! warning "Increased Coupling"
    The business logic embedded within step definitions creates a strong dependency between the test code and the SUT. Any changes to the business rules or system behavior can propagate throughout the entire test suite, leading to maintenance difficulties.

!!! warning "Missing Scalability"
    Complex step definitions hinder scalability. As the number of scenarios grows, managing intertwined business logic becomes unwieldy.

!!! warning "Limited Reusability"
    Tests become less reusable as they are tightly coupled to the system's implementation.

This code smell occurs when everything is stored either in a context or in the fields of your step implementation. Often, this state is even duplicated because we prepared the state of the application previously. This can lead to tightly coupled tests that are difficult to maintain and understand.

## Required Action

!!! warning "TODO"
    describe details of exercise


* Separation of Concerns: Extract business logic from step definitions. Keep the test code focused on expressing the intended behavior without diving into implementation details. Create separate utility methods or helper classes to encapsulate business rules.
* Leverage Page Objects: Use page objects to encapsulate interactions with the UI, reducing the amount of business logic in step definitions.
* Dependency Inversion: Introduce a test design where the test implementation defines interfaces to be fulfilled by utilities or drivers. By applying the principles of dependency inversion, you enable easy exchange of the test object (e.g., REST service instead of UI) while maintaining a clean separation between test code and SUT.

## Code Examples
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
