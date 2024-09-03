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
* **Combine Step Definitions**: Merge the singular and plural step definitions into a single definition with multiple expressions and using parameterization to handle variations.
* **Use Regular Expressions / Leverage Parameter Handling**: Consider using regular expressions or custom parameter types to handle dynamic values effectively.
* **Ensure Consistent Syntax**: Standardize the parameter handling syntax across all step definitions to improve readability and maintainability.



## Code Examples

```gherkin title="Java"
    @Given("there is a customer")
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
