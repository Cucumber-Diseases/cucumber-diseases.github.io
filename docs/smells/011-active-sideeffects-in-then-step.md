# 011: Active Side Effects in Then Step
The *Active Side Effects in Then Step* occurs when a `Then` step, which should be used exclusively for verifying outcomes, is incorrectly used to perform actions that modify the application's internal state, such as creating or altering data.

This is a case of misaligned purpose, where operations meant for 

* `Given` (for setup) or 
* `When` (for executing actions) 

steps are mistakenly placed in the `Then` step. The `Then` step is intended solely for assertions and validation, ensuring that the application behaves as expected based on the actions performed.

Introducing state changes in this step confuses the purpose of the test and can lead to unreliable or misleading results.

## Impact

!!! failure "Unreadable Code"
    The scenario becomes harder to read and understand because the distinction between setting up, acting, and verifying is blurred. This can make it difficult to discern the intent behind each step and what is being tested.

!!! failure "Harder Maintenance"
    Tests that include state changes in `Then` steps are more difficult to maintain. Since `Then` steps are expected to be idempotent (i.e., not change the system's state), including state-altering actions here can lead to fragile tests that are sensitive to changes in the application's logic or structure.

!!! failure "Harder Analysis"
    Mixing state changes with assertions in `Then` steps diminishes the clarity of the test, making it unclear what the expected outcome is supposed to validate, as action and validation are confused. This makes it harder to analyse when your scenarios are failing. 

!!! failure "Increased Complexity"
    Introducing side effects in `Then` steps lead to tighter coupling between tests and the underlying code, increasing the complexity and interdependencies between steps. This makes the test suite more brittle and less modular. Further you might need to consider cleanup procedures even though you would expect it here.

## Required Actions

### Fixing

* **Separate Concerns**: Ensure that any action that changes the state of the application is placed in the appropriate `Given` or `When` step. Given should handle all setup and preconditions, while When should execute the actions that the scenario is testing.
* **Use Background Steps**: Utilize the `Background` section to set up common data or preconditions shared across multiple scenarios. Keep the `Then` step focused on verifying outcomes without introducing side effects.

Remember that adhering to the intended purpose of each step (`Given`, `When`, `Then`) promotes cleaner, more maintainable Gherkin scenarios and reduces the risk of introducing Cucumber diseases like this one.

### Prevention

* **Refactor the Then Steps**: If you find state-altering code within a `Then` step, refactor it by moving those actions to a Given or When step, depending on where it logically belongs. `Then` steps should be refocused on assertions that check the results of actions performed in the When step.
* **Review Scenarios for Alignment**: Regularly review your scenarios to ensure that each step is aligned with its intended purpose. `Given` sets up the context, When performs the actions, and `Then` verifies the outcomes. This alignment helps maintain clear and understandable tests.
* **Use Mocks or Stubs**: If the `Then` step is intended to validate interactions without causing side effects, consider using mocks or stubs. This approach allows you to simulate the interaction without actually changing the application's state, keeping your `Then` steps focused on validation.

## Code Examples

=== "Java"
    ```java title="CustomerStepDefinitions.java"
    @Then("the second customer can be found")
    public void theSecondCustomerCanBeFound() {
        customerService.addCustomer(secondFirstName, secondLastName, DEFAULT_BIRTHDAY); // (1)!
        var customer = customerService.searchCustomer(secondFirstName, secondLastName);

        Assertions.assertThat(customer.firstName).isEqualTo(secondFirstName);
        Assertions.assertThat(customer.lastName).isEqualTo(secondLastName);
    }
    ```

    1. Creating the customer in the `Then` step is an active side effect. Since we are checking exactly this data, we should move it to a appropiate `When` impelementation. 
    
=== "Python"
    ```python title="features/steps/steps.py"
    @then(u'the creation of customer (?P<first_name>.*?) (?P<last_name>.*?) should fail')
    def step_impl(context, first_name, last_name):
        caught = None
        try:
            # (1)!
            context.service.add_customer(first_name, last_name, context.default_birthday) 
        except ValueError as e:
            caught = e

        assert_that(caught).is_not_none()
        assert_that(str(caught)).is_equal_to("Customer already exists")

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
    func InitializeScenario(sc *godog.ScenarioContext) {
        // ...
        sc.Then(`the second customer creation should fail`, t.theSecondCustomerCreationShouldFail)
        // ...
    }

    func (t *CustomerTestSteps) theSecondCustomerCreationShouldFail(ctx context.Context) error {
        // (1)!
        err := t.customerService.AddCustomer(t.secondFirstName, t.secondLastName, DEFAULT_BIRTHDAY)
        if err == nil {
            return fmt.Errorf("expected error but got nil")
        }

        if err.Error() != "customer already exists" {
            return fmt.Errorf("expected 'customer already exists' error but got '%s'", err.Error())
        }

        return nil
    }
    ```

    1. Creating the customer in the `Then` step is an active side effect. Since we are checking exactly this data, we should move it to a appropiate `When` impelementation. 
