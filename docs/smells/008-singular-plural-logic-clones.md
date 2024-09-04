# 008: Singular-Plural Logic Clones

This code smell occurs when there are multiple, nearly identical implementations of step definitions to handle singular and plural cases. These implementations often share similar logic but differ only in the handling of singular and plural nouns. The underlying idea is akin to the “Don’t Repeat Yourself” (DRY) principle, which encourages code reuse and consolidation.

## Impact

!!! danger "Test Inconsistency"
    Inconsistent parameter handling syntax can lead to errors and inconsistencies.

!!! failure "Unreadable Code"
    The code becomes less readable and harder to understand due to the duplication.

!!! failure "Harder Maintainability"
    Changes to the underlying logic must be applied to multiple step definitions, increasing maintenance effort.

!!! failure "Increased Complexity"
    The codebase becomes more complex and harder to manage with redundant implementations.


## Required Action
When you identify a `Singular-Plural Logic Clones` in your scenario, there are multiple ways to resolve them:

* **Combine Step Definitions**: Merge the singular and plural step definitions into a single definition with multiple expressions and using parameterization to handle variations.
* **Use Regular Expressions / Leverage Parameter Handling**: Consider using regular expressions or custom parameter types to handle dynamic values effectively.
* **Ensure Consistent Syntax**: Standardize the parameter handling syntax across all step definitions to improve readability and maintainability.

## Code Examples
To understand this smell, please refer to the Gherkin code as well as the code in the implementation in one of the programming languages. It makes the most sense if the scenarios and the implementation are both read together.

### Gherkin
```gherkin title="Customer.feature"

# (1)!
Scenario: Should find an existing customer
    Given there is a customer 
        | Sabine | Mustermann |
    Then the customer Sabine Mustermann can be found

# ...

Scenario: Should find multiple customers
    Given there are some customers # (1)
        | firstname | lastname   |
        | Max       | Mustermann |
        | Sabine    | Mustermann |
        | Horst     | Mustermann |
    When all customers are searched
    Then the number of customers found is 3
```

1. The steps `Given there is a customer` and `Given there are some customers` are in different scenarios, but essentially have the same meaning. The only difference is that one gives the precondition of having a singular customer with a given name and the other provides multiple customers based on a list of given names. While linguistically different, the implementation of both steps should refer to the same, more generic, step implementation.

### Step Implementation
=== "Java"
    ```java title="src/test/java/org/training/customer/CustomerStepDefinitions.java"
    @Given("there is a customer")  // (1)!
    public void thereIsACustomer(DataTable customerTable) {
        List<List<String>> row = customerTable.asLists(String.class);

        customerService.addCustomer(row.get(0).get(0), row.get(0).get(1), DEFAULT_BIRTHDAY);
    }

    @Given("there are some customers")
    public void thereAreSomeCustomers(DataTable customerTable) {
        List<Map<String, String>> rows = customerTable.asMaps(String.class, String.class);
        for (Map<String, String> col : rows) {
            customerService.addCustomer(col.get("firstname"), col.get("lastname"), DEFAULT_BIRTHDAY);
        }
    }
    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.
    
=== "Python"
    ```python title="features/steps/steps.py"
    @given(u'there is a customer') # (1)!
    def step_impl(context):
            table = context.table
            context.service.add_customer(table.headings[0], table.headings[1], context.default_birthday)

    @given(u'there are some customers')
    def step_impl(context):
        for row in context.table.rows:
            context.service.add_customer(row["firstname"], row["lastname"], context.default_birthday)

    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.


=== "C#"
    ```csharp title="CucumberDiseases.Specs/StepDefinitions/CustomerStepDefinitions.cs"
    [Given("there is a customer")] // (1)!
    public void GivenThereIsACustomer(Table customerTable)
    {
        var customer = customerTable.Header.ToArray();
        _customerService.AddCustomer(customer[0], customer[1], DefaultBirthday);
    }

    [Given("there are some customers")]
    public void GivenThereAreSomeCustomers(Table customerTable)
    {
        var customers = customerTable.CreateSet<CustomerData>(() => new CustomerData("John", "Doe", DefaultBirthday));
        foreach (var customer in customers)
        {
            _customerService.AddCustomer(customer.FirstName, customer.LastName, customer.Birthday);
        }
    }
    ```

    1. The expressions `there is a customer` and `there are some customers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.

=== "Go"
    ```go title="customer_test.go"
    func InitializeScenario(sc *godog.ScenarioContext) {
        // ...
        // (1)!
        sc.Given(`there is a customer`, t.thereIsACustomer)
	    sc.Given(`there are some customers`, t.thereAreSomeCustomers)
        // ...
    }

    func (t *CustomerTestSteps) thereIsACustomer(ctx context.Context, table *godog.Table) error {
        row := table.Rows[0]
        t.customerService.AddCustomer(row.Cells[0].Value, row.Cells[1].Value, DEFAULT_BIRTHDAY)
        return nil
    }

    func (t *CustomerTestSteps) thereAreSomeCustomers(ctx context.Context, table *godog.Table) error {
        for i, row := range table.Rows {
            if i == 0 {
                continue // skip header...
            }
            t.customerService.AddCustomer(row.Cells[0].Value, row.Cells[1].Value, DEFAULT_BIRTHDAY)
        }
        return nil
    }
    ```

    1. The functions `thereIsACustomer` and `thereAreSomeCustomers` handle the singular and plural case of the same step. The share a similar logic and can therefore be merged.
