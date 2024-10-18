# Exercise 014: Refactor Scenario Overload
:link: [Related Smell: 014 - Scenario Overload](/smells/014-scenario-overload)

## Purpose
* Learn to identify the `Scenario Overload` smell.
* Understand how separating different behaviors into multiple Gherkin scenarios improves readability and maintainability.

## Your Task
Find at leastone scenario that tests multiple behaviors in one go. Refactor the scenario by splitting the behaviors into individual scenarios. Ensure each new scenario focuses on testing only one behavior.

=== "Hints"

    ??? tip "Hint A"
        * Which parts of the new scenarios test different behaviors?

    ??? tip "Hint B"
        * Look at how the customer creation and search steps are mixed. Should they be tested in one scenario or split into separate ones?

    ??? tip "Hint C"
        * Notice that both creation and search are combined. Try to focus on one behavior per scenario to avoid overloading.

    ??? tip "Hint D"
        * Refactor by splitting the creation and search steps into their own scenarios. Each should focus on a single aspect of customer management.

