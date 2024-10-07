# Deliberate Exercises

## Fixing first smells
Once you've set up the [repository](https://cucumber-diseases.github.io/repos/) and are familiar with the structure, you can begin practicing the identification and refactoring of code smells:

* [Start with Exploration:](repos/index#compare-with-the-solution) Begin by checking out the initial `Customer.feature` file in the repository. Examine the feature file and associated step definitions to see if you can identify any potential code smells on your own.
* [Use Git Tags for Guided Practice:](repos/index#using-git-tags-to-explore-smells) If you're unsure where to start, use the Git tags to jump directly to known code smells. For example, check out the smell-01 tag to explore the first documented code smell in the repository.
* Refactor the Smell: Once you've identified a smell, either by your own exploration or by checking out a tagged commit, try refactoring the code to remove the smell. Consider what changes are necessary to improve readability, maintainability, and the overall quality of the test code.
* Validate Your Solution: After making your changes, compare your refactoring with the solution provided under the corresponding smell-XX-solution tag. This will help you validate your approach and understand any differences.

We generally advise you to start with the [first smell "Missing Then Implementation"](ex-001-missing-then.md) and then gradually work to the next one. The smells presented are usually getting harder to detect and fix the higher you go up in the list. Once you are more accustomed to identifying and refactoring Cucumber smells, you can start checking out different ones in no specific order.

