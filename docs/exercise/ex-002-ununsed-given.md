# Exercise 002: 
:link: [Related Smell: 002 - Unused Given Parameter](/smells/002-unused-given.md)

## Purpose
* Learn to identify the `Unused Given Parameter` smell.
* Understand which complications arise from having empty step definitions and how to spot them.

## Your Task
Within the `Customer.feature` file there is a `Then` step that does not do anything. Find at least
one such step definition and implement the correct assertion.

## Solution

=== "Hints"
    ??? tip "Hint A"
        * You are looking for a `Then` step that is verifying if a customer was created successfully.

    ??? tip "Hint B"
        * The relevant step is `Then the customer creation should be successful`.
        * Look at the implementation of the code in te step definition.

    ??? tip "Hint C"
        * The relevant step is `Then the customer creation should be successful`.
        * The step definition is an empty function that does not do anything.
        * Think of what it should actually do and implement the correct assertion.

    ??? tip "Step by Step Walkthrough"
        * The relevant step is `Then the customer creation should be successful`.
        * The step definition is an empty function that does not do anything.
        * The function should implement an assertion of the error field.
        * Assert that the error field (e.g. `this.error` in java or `t.err` in go) is null.
    

=== "Diffs"

    === "Java"
        ```diff
        --- a/src/test/java/org/training/customer/CustomerStepDefinitions.java
        +++ b/src/test/java/org/training/customer/CustomerStepDefinitions.java
        @@ -81,6 +81,7 @@ public class CustomerStepDefinitions {

            @Then("the customer creation should be successful")
            public void theCustomerCreationShouldBeSuccessful() {
        +        Assertions.assertThat(error).isNull();
            }

            @Then("the customer creation should fail")
        ```
    
    === "Python"
        ```diff
        --- a/features/steps/steps.py
        +++ b/features/steps/steps.py
        @@ -88,7 +88,14 @@ def step_impl(context):

        @then(u'the second customer creation should fail')
        def step_impl(context):
        -    pass
        +    caught = None
        +    try:
        +        context.service.add_customer(context.second_first_name, context.second_last_name, context.default_birthday)
        +    except ValueError as e:
        +        caught = e
        +
        +    assert_that(caught).is_not_none()
        +    assert_that(str(caught)).is_equal_to("Customer already exists")


        @given(u'there is a customer')
        ```

    === "C#"
        ```diff
        --- a/CucumberDiseases.Specs/StepDefinitions/CustomerStepDefinitions.cs
        +++ b/CucumberDiseases.Specs/StepDefinitions/CustomerStepDefinitions.cs
        @@ -91,6 +91,7 @@ public class CustomerStepDefinitions
            [Then("the customer creation should be successful")]
            public void ThenTheCustomerCreationShouldBeSuccessful()
            {
        +        _error.Should().BeNull();
            }

            [Then("the customer creation should fail")]
        ```

    === "Go"
        ```diff
        --- a/customer_test.go
        +++ b/customer_test.go
        @@ -67,6 +67,9 @@ func (t *CustomerTestSteps) anInvalidCustomerIsCreated(ctx context.Context) erro
        }

        func (t *CustomerTestSteps) theCustomerCreationShouldBeSuccessful(ctx context.Context) error {
        +       if t.err != nil {
        +               return fmt.Errorf("expected no error but got %v", t.err)
        +       }
                return nil
        }
        ```