# 013: Test Code Impurity
“Test Code Impurity” arises when step definitions contain complex business logic that goes beyond their primary purpose—acting as a bridge between human-readable scenarios and underlying automation code. Instead of keeping step definitions simple, they become heavily tied to the details of the system under test (SUT). This impurity in test code results in a step definition that becomes too verbose (often exceeding 10 lines) and overly reliant on the system’s inner workings, which increases the risk of tight coupling. As a result, the tests are less adaptable to changes in the SUT and require significant effort to modify and update.

## Impact

!!! failure "Unreadable Code"
    When business logic is mixed with test code, it becomes harder to understand the purpose of each step. Developers may struggle to differentiate between actual test steps and implementation details.

!!! failure "Harder Maintenance"
    When business logic is embedded in step definitions, even small changes in the SUT can require extensive rework of the test automation. This increases the effort needed to maintain the tests over time, especially in complex or large-scale projects.
    
!!! warning "Increased Coupling"
    The business logic embedded within step definitions creates a strong dependency between the test code and the SUT. Any changes to the business rules or system behavior can propagate throughout the entire test suite, leading to maintenance difficulties.

!!! warning "Missing Scalability"
    Complex step definitions hinder scalability. As the number of scenarios grows, managing intertwined business logic becomes unwieldy as they are tightly coupled to the system's implementation..

!!! warning "Limited Reusability"
    Heavily logic-driven step definitions are often too specific, making it difficult to reuse them across different scenarios.

The tight coupling introduced by this code smell makes the test suite challenging to maintain and less adaptable to changes in the SUT.

## Required Action

* **Keep Step Definitions Simple:** Step definitions should act as a thin layer between Gherkin scenarios and automation code. They should be concise, typically no longer than 10 lines, and focus only on calling methods that implement the behavior being tested. Avoid putting complex business logic directly in step definitions.

* **Use a Design with different Test Automation Layers:** Seperate different concerns of the test automation code into different levels for example a business rule, workflow and technical level. Introduce pattern like Page Objects, Drivers and Helper Classes and extract the code according to your selected test automation architecture. This separation of concerns ensures that the test automation code remains modular and easy to maintain. Step definitions should focus solely on describing what action is being performed, not how it is implemented.

* **Extract Helper Classes**: If a test action requires complex logic, encapsulate that logic in a well-named method in a helper class. This keeps the step definition readable while still achieving the necessary functionality.

* **Use Builders or Factories for Complex Test Data**: For scenarios requiring complex test data, avoid constructing objects directly within the step definitions. Instead, use builder patterns or factory classes to encapsulate the creation of test data. This keeps the step definitions clean, while the builder or factory handles the complexity of constructing objects with various configurations. This approach also encourages reusability and reduces duplication in your test data setup.


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
