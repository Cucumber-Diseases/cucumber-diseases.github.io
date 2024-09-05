# 011: Dependence on Class State
The "Dependence on Class State" occurs when step definitions rely heavily on class fields or context objects to store and share data between steps. Often, this state is duplicated or overlaps with previously prepared data in the application, leading to unnecessary complexity. In this scenario, the state is stored either in the fields of the step definition class or in a shared context object, which is akin to a global variable. This approach introduces hidden dependencies between steps and can result in tightly coupled tests where the behavior of one step is implicitly tied to the internal state managed by the class or context. This creates a brittle test structure where understanding and maintaining the state becomes challenging, especially as the test suite grows.

## Impact

!!! failure "Unreadable Code"
    Tests become harder to understand as the state of the application is scattered across multiple locations.
    
!!! failure "Harder Maintenance"
    Storing state in class fields or context introduces tight coupling between steps. As tests evolve, changing the state management in one step could inadvertently break others, leading to fragile and harder-to-maintain test cases.

!!! failure "Increased Complexity"
    Shraing state always increases complexity, as developers need to understand not only the logic of each step but also how the state is manipulated across multiple steps. This makes the tests more prone to errors and bugs, especially in large test suites.

!!! warning "Increased Coupling"
    Using context or class fields to manage state creates implicit dependencies between steps, violating the principle of isolation between tests. This can lead to flakiness, where tests might pass or fail depending on the order in which they are executed.

## Required Action

### Fixing

* **Pass Data Explicitly**: Instead of relying on fields in the step implementation class, refactor your steps and pass data directly between steps via method parameters or use clear, explicit constructs like local variables. This keeps the state management simple, localized, and easy to follow.
* **Refactor Tests to Reduce Duplication**: Ensure that state is only prepared once in the Given step, avoiding the need for duplicated or redundant state management. Ensure each step has a clear and distinct responsibility, and refactor any steps that introduce unnecessary coupling or complexity through shared state.
* **Use Scenario Context Sparingly**: Context objects can act like global variables, leading to unclear and tightly coupled tests, avoid overusing it. Limit the amount of data stored in the context to essential information. Consider whether a step really needs access to the entire context or if a smaller subset suffices.
* **Replace static objects with context objects**: Never use static shared objects to exchange state between steps. If you must share state across steps, dependency injection of context objects to manage it in a controlled and transparent way. This allows for better control over the lifecycle and visibility of shared state.

### Prevention

* **Reuse Application State**: Don't hold data twice in your application and in your test classes. Prefer the usage of test data in your application state for example a database instead of temporary storage in your objects.
* **Keep Steps Isolated**: Steps should not depend on state manipulated by previous steps. Each step should be able to stand alone and express its purpose clearly. If state sharing is necessary, consider refactoring the test logic to make the dependencies explicit and well-defined.
* **Avoid Premature Data Gathering**: Gather data only when needed. If data can be collected later in the scenario, defer its retrieval to a later step and pass it to the subsequent steps as necessary.


## Code Examples


### Step Implementation
=== "Java"
    ```java title="CustomerStepDefinitions.java"
    private String firstName; // (1)!
    private String lastName;

    @Given("the customer name is {} {}")
    public void theCustomerNameIs(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    @When("the customer is created")
    @When("an invalid customer is created")
    public void createCustomerAndStoreSuccess() {
        try {
            customerService.addCustomer(firstName, lastName, DEFAULT_BIRTHDAY);
        } catch (IllegalArgumentException e) {
            error = e;
        }
    }

    @Then("the customer can be found")
    public void theCustomerCanBeFound() {
        var customer = customerService.searchCustomer(firstName, lastName);
        Assertions.assertThat(customer).isNotNull();
    }
    ```

    1. The fields `firstName` and `lastName` are populuted over all steps. Consider passing them as parameters. This makes the steps independent and reusable for other fields, too.
    
=== "Python"
    ```python title="features/steps/steps.py"
    ...
    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.


=== "C#"
    ```csharp title="CustomerStepDefinitions.cs"
    private string _firstName; // (1)!
    private string _lastName;

    [Given("the customer name is {} {}")]
    public void GivenTheCustomerNameIs(string firstName, string lastName)
    {
        _firstName = firstName;
        _lastName = lastName;
    }
    
    [When("the customer is created")]
    [When("an invalid customer is created")]
    public void CreateCustomerAndStoreSuccess()
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

    [Then("the customer can be found")]
    public void ThenTheCustomerCanBeFound()
    {
        var customer = _customerService.FindCustomer(_firstName, _lastName);
        customer.Should().BeEquivalentTo(new { FirstName = _firstName, LastName = _lastName });
    }
    ```

    1. The fields `firstName` and `lastName` are populuted over all steps. Consider passing them as parameters. This makes the steps independent and reusable for other fields, too.

=== "Go"
    ```go title="customer_test.go"
    ...
    ```

    1. The functions `thereIsACustomer` and `thereAreSomeCustomers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.
