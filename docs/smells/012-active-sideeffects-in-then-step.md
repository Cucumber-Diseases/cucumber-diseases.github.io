# 012: Active Sideeffects in Then Step
This code smell, known as “Active Sideeffects in Then Step,” manifests when we invoke functions within our application from a Then step in our Cucumber scenario. These functions modify the internal state of the application, such as creating or altering data. However, this practice misaligns with the intended purpose of the Then step, which primarily focuses on asserting outcomes based on the actions performed in the preceding Given and When steps.


## Impact
The presence of this smell can lead to several problems and risks:

!!! failure "Unreadable and unclear Code"
    Code becomes harder to understand due to mixed responsibilities within the Then step.
    Developers may struggle to differentiate between verification logic and data manipulation.

!!! failure "Harder Maintenance"
    When data preparation occurs in the Then step, any changes to the data creation process require modifying multiple places.
    This increases maintenance effort and the likelihood of introducing errors.

!!! failure "Increased Complexity"
    Direct function calls in the Then step tightly couple verification logic with data setup.
    The complexity of the step grows, making it challenging to reason about the scenario. Further you might need to consider cleanup procedures even though you would expect it here.

!!! failure "Harder Analysis"
    When a step fails it becomes harder to analyse because of the active side effects in the application.

## Required Action

* **Separate Concerns**: Clarify if the side effect the purpose of the side effect. If it's data preparation (e.g., creating test data), move it  to the `Given` step. Otherwies it could be a result of the `When` step, then move it there and retrieve the result in the `Then`step. Reserve the `Then` step exclusively for verification and assertions.
* **Use Background Steps**: Utilize the `Background` section to set up common data or preconditions shared across multiple scenarios. Keep the `Then` step focused on verifying outcomes without introducing side effects.
* **Custom Step Definitions**: Create custom step definitions for specific data setup tasks. These custom steps can encapsulate data creation, making the scenario more modular and readable.

Remember that adhering to the intended purpose of each step (`Given`, `When`, `Then`) promotes cleaner, more maintainable Gherkin scenarios and reduces the risk of introducing Cucumber diseases like this one. 😊

## Code Examples
To understand this smell, please refer to the Gherkin code as well as the code in the implementation in one of the programming languages. It makes the most sense if the scenarios and the implementation are both read together.


### Step Implementation
=== "Java"
    ```java title="CustomerStepDefinitions.java"
    @Then("the second customer can be found")
    public void theSecondCustomerCanBeFound() {
        customerService.addCustomer(secondFirstName, secondLastName, DEFAULT_BIRTHDAY); // (1)!
        var customer = customerService.searchCustomer(secondFirstName, secondLastName);

        Assertions.assertThat(customer.firstName).isEqualTo(secondFirstName);
        Assertions.assertThat(customer.lastName).isEqualTo(secondLastName);}
    ```

    1. Creating the customer in the `Then` step is an active side effect. Since we are checking exactly this data, we should move it to a appropiate `When` impelementation. 
    
=== "Python"
    ```python title="features/steps/steps.py"
    ...
    ```

    1. Creating the customer in the `Then` step is an active side effect. Since we are checking exactly this data, we should move it to a appropiate `When` impelementation. 


=== "C#"
    ```csharp title="CustomerStepDefinitions.cs"
    [Then("the second customer can be found")]
    public void ThenTheSecondCustomerCanBeFound()
    {
        _customerService.AddCustomer(_secondFirstName, _secondLastName, DefaultBirthday); // (1)!
        var customer = _customerService.FindCustomer(_secondFirstName, _secondLastName);

        customer.Should().BeEquivalentTo(new { FirstName = _secondFirstName, LastName = _secondLastName });
    }
    ```

    1. Creating the customer in the `Then` step is an active side effect. Since we are checking exactly this data, we should move it to a appropiate `When` impelementation. 

=== "Go"
    ```go title="customer_test.go"
    ...
    ```

    1. Creating the customer in the `Then` step is an active side effect. Since we are checking exactly this data, we should move it to a appropiate `When` impelementation. 
