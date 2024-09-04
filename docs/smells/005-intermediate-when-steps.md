# 005: Intermediate When Steps

The *Intermediate When Steps* (also called "When/Then Mismatch) code smell violates the fundamental principle of Behavior-Driven Development (BDD): **One Scenario, One Behavior!**

When a scenario contains multiple `When` steps, it indicates an issue within the scope or the purpose of your test case. Are you using "Intermediate When Steps" to store multiple results? This leads to unclear and suspicious assertions in the `Then` step.

If you encounter this smell, the `When` step is misused in order to execute or prepare a functionality that is not directly under test by the scenario for it's side effects. Very often this is to prepare some condition required by the verification in the following `Then` steps.

It is very strongly related to [Given/When Purpose Mismatch](/smells/006-given-when-purpose-mismatch). The significant difference is that this smell executes an action that is relevant for the `Then` step while the "Given/When Purpose Mismatch" executes something as a `When` as preparation for another `When` step step that should be part of a `Given` step.

## Impact:

!!! failure "Reduced Clarity"
    Combining behaviors into a single scenario leads to ambiguity and miscommunication.

!!! failure "Harder Analysis"
    When a test fails, identifying the root cause becomes challenging because it could be related to any of the multiple behaviors.

!!! warning "Duplication"
    Scenarios that repeat the same sequence of steps instead of isolating behaviors risk unnecessary duplication.

## Required Action
Look for scenarios that have more than one `When` (or `When ... And ...`) steps and inspect them for what they are trying to achieve. There are three common ways to resolve this situation:

1. **Merge Steps**: In the case of multiple "When" steps the most obvious solution could be merging the implementation into something new. Consider also merging or replacing multiple "When" steps with a  "Then" step. This happens if you storing multiple results or there is something suspicious in your assertion.
2. **Rearrange Steps**: This is similar to merging steps. Ask your self, which steps are describing the action and which of them are preparing or asserting the scenarios.
3. **Isolate Behaviors:** Create separate scenarios for each distinct behavior.

## Code Examples
### Gherkin
```gherkin
Scenario: Should find newly created customer
    Given the customer name is Rose Smith
    When the customer is created
    And all customers are searched
# (1)!
    Then the number of customers found is 1
```
1. Note the `When ... And ...` composition of the scenario. In this case the author is misusing `And all customers are searched` as a `When` clause, even though it is not the functionality under test. Instead, searching all customers is part of the verification and assertion of the `Then` step. A viable solution would be to introduce a `Then` step that represents `search and check the returned number of customers`.
