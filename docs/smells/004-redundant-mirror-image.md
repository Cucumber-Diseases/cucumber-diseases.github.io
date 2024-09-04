# 004: Redundant Mirror Image

The “Redundant Mirror Image” code smell involves code duplication within your Gherkin scenarios.
When the same implementation logic appears multiple times with different expressions, consider consolidating it into reusable expressions.
Even if the expressions seem completely mismatched (representing opposite behaviors, such as success and failure cases), both scenarios verify the same behavior.

## Impact
!!! danger "Test Inconsistency"
    If one side of the mirror image is updated without considering the other, scenarios may become inconsistent.

!!! failure "Harder Maintenance"
    Any change to one step affects all implementations.

## Required Action
Identify steps that share the same implementation but describe asymmetric behavior. 
If you find such steps, consider consolidating them by using multiple expressions for a single implementation.

## Code Examples

=== "Java"
    ```java title="CustomerStepDefinitions.java"
    @When("the customer is created") // (1)!
    public void theCustomerIsCreated() {
        try {
            customerService.addCustomer(firstName, lastName, DEFAULT_BIRTHDAY);
        } catch (IllegalArgumentException e) {
            error = e;
        }
    }

    @When("an invalid customer is created")
    public void anInvalidCustomerIsCreated() {
        try {
            customerService.addCustomer(firstName, lastName, DEFAULT_BIRTHDAY);
        } catch (IllegalArgumentException e) {
            error = e;
        }
    }
    ```

     1. `anInvalidCustomerIsCreated` contains the same implementation as `theCustomerIsCreated`. It is the logical opposite, but does the same thing, just that we expect it to throw an `IllegalArgumentException` in one case and have `error` be `null` in the other. The only real difference comes from the subsequent `Then` step that makes a distinction in the verification.

=== "Python"
    ```python title="features/steps/steps.py"
    when(u'the customer is created') # (1)!
    def step_impl(context):
        try:
            context.service.add_customer(context.first_name, context.last_name, context.default_birthday)
        except ValueError as e:
            context.error = e

    @when(u'an invalid customer is created')
    def step_impl(context):
        try:
            context.service.add_customer(context.first_name, context.last_name, context.default_birthday)
        except ValueError as e:
            context.error = e
    ```

    1. `the customer is created` contains the same implementation as `an invalid customer is created`. It is the logical opposite, but does the same thing, just that we expect it to throw a `ValueError` in one case and have `context.error` be `None` in the other. The only real difference comes from the subsequent `Then` step that makes a distinction in the verification.

=== "C#"
    ```csharp title="CustomerStepDefinitions.cs"
    [When("the customer is created")]
    public void WhenTheCustomerIsCreated() // (1)!
    {
        try
        {
            _customerService.AddCustomer(_firstName, _lastName, DefaultBirthday);
        }
        catch (ArgumentException ex)
        {
            _error = ex;
        }
    }

    [When("an invalid customer is created")]
    public void WhenAnInvalidCustomerIsCreated()
    {
        try
        {
            _customerService.AddCustomer(_firstName, _lastName, DefaultBirthday);
        }
        catch (ArgumentException ex)
        {
            _error = ex;
        }
    }
    ```

     1. `WhenAnInvalidCustomerIsCreated` contains the same implementation as `WhenTheCustomerIsCreated`. It is the logical opposite, but does the same thing, just that we expect it to throw a `ArgumentException` in one case and have `_error` be `None` in the other. The only real difference comes from the subsequent `Then` step that makes a distinction in the verification.

=== "Go"
    ```go title="customer_test.go"
    func (t *CustomerTestSteps) theCustomerCreationShouldBeSuccessful(ctx context.Context) error {
        // ...
        sc.When(`^the customer is created$`, t.theCustomerIsCreated)
        sc.When(`an invalid customer is created`, t.anInvalidCustomerIsCreated) // (1)!
        // ...
    }

    func (t *CustomerTestSteps) anInvalidCustomerIsCreated(ctx context.Context) error {
        t.err = t.customerService.AddCustomer(t.firstName, t.lastName, DEFAULT_BIRTHDAY)
        return nil
    }

    func (t *CustomerTestSteps) theCustomerIsCreated(ctx context.Context) error {
        t.err = t.customerService.AddCustomer(t.firstName, t.lastName, DEFAULT_BIRTHDAY)
        return nil
    }
    ```

    1. `anInvalidCustomerIsCreated` contains the same implementation as `theCustomerIsCreated`. It is the logical opposite, but does the same thing, just that we expect it to set an error instead of returnung `nil` for an error. The only real difference comes from the subsequent `Then` step that makes a distinction in the verification.