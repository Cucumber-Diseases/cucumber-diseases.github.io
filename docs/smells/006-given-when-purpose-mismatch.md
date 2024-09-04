# 006: Given/When Purpose Mismatch

The *Given/When Purpose Mismatch* occurs when the roles of `Given` and `When` steps are confused or misused in a Gherkin scenario. It happens when the Given step is intended to set up test data, while the `When` step is meant to test a function that creates something. In a proper setup (`Given`), the focus should be on preparing the necessary context or state, without concern for validation or correctness. However, the implementation of these steps may be similar or identical, leading to confusion.

## Impact

!!! failure "Harder Maintenance"
    Maintaining such tests becomes challenging, as the conflation of setup and behavior testing can lead to brittle tests that are difficult to update or refactor.

!!! failure "Unreadable Code"
    Scenarios become harder to understand because the purpose of each step is unclear, leading to confusion about what is being tested.

!!! failure "Reduced Clarity"
    The distinction between preparation and verification blurs, making it difficult to discern whether the scenario is setting up context or validating functionality.

!!! failure "Increased Complexity"
    This smell can increase the complexity of tests, as it introduces unnecessary checks and validations in the setup phase, complicating the logic of the test steps.

## Required Action
When you identify a `Given/When Purpose Mismatch` in the scenarios, there are multiple ways to resolve them:

1. **Separate Concerns:** Clearly differentiate between `Given` and `When` steps. Ensure that Given steps are solely for setting up the context without any assertions, and `When` steps are used to trigger the behavior you want to test, including necessary validations.
2. **Refactor Steps:** If you identify a `Given` step that performs validation or verification, refactor it into a `When` step to align with the intended purpose. Similarly, ensure that `When` steps do not involve unnecessary setup.
3. **Use Scenario Outlines:** If multiple scenarios share similar setups, use scenario outlines to parameterize the Given step and avoid code duplication.
4. **Use Data Tables:** If your scenario needs different test data of the same kind pass a data tale instead of duplicating your `Given` steps.

Depending on the exact situation different actions may be appropriate.

## Code Examples
### Gherkin
```gherkin title="Customer.feature"

Scenario: Should be able to create two customer with different names
   Given the customer name is Max Mustermann
   Given the second customer is Sabine Mustermann
   When the customer is created
# (1)!
   When the second customer is created
   Then the second customer can be found
```

1. In this case the creation of the first customer is only executed as a `When` step in order to then execute the creation of the second customer. The actual behaviour under test is the creation of the second customer. A possible solution here would be to create a `Then` step that includes the creation of the first customer.
