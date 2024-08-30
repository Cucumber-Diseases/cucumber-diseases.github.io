# Getting Started

## Things to learn here
tbd

## What are code smells?
The term code smell was originally mentioned by Kent Beck as explained by Martin Fowler’s [description](https://www.martinfowler.com/bliki/CodeSmell.html) of code smells.

!!! quote ""

    "A code smell is a surface indication that usually corresponds to a deeper problem in the system." 
    
    Kent Beck, Martin Fowler



While a code smell doesn't necessarily mean the code is incorrect or non-functional, it suggests that the code may be poorly designed, difficult to maintain, or prone to bugs. Code smells often point to deeper issues in the codebase that could lead to more significant problems if not addressed.

There are several lists of code smells available online. One of the most well-known is found in Martin Fowler’s book Refactoring. Additionally, you can explore other widely recognized lists on platforms such as Wikipedia, [Coding Horror](https://blog.codinghorror.com/code-smells/) and [Refactoring Guru](https://refactoring.guru/refactoring/smells). These resources provide comprehensive overviews of common code smells and offer insights into best practices for identifying and addressing them.

## Fixing first smells
Once you've set up the repository and are familiar with the structure, you can begin practicing the identification and refactoring of code smells:

* [Start with Exploration:](repos/index.md#using-git-tags-to-explore-smells) Begin by checking out the initial `Customer.feature` file in the repository. Examine the feature file and associated step definitions to see if you can identify any potential code smells on your own.
* [Use Git Tags for Guided Practice:](repos/index.md#compare-with-the-solution) If you're unsure where to start, use the Git tags to jump directly to known code smells. For example, check out the smell-01 tag to explore the first documented code smell in the repository.
* Refactor the Smell: Once you've identified a smell, either by your own exploration or by checking out a tagged commit, try refactoring the code to remove the smell. Consider what changes are necessary to improve readability, maintainability, and the overall quality of the test code.
* Validate Your Solution: After making your changes, compare your refactoring with the solution provided under the corresponding smell-XX-solution tag. This will help you validate your approach and understand any differences.

We generally advise you to start with the [first smell "Missing Then Implementation"](smells/001-missing-then.md) and then gradually work to the next one. The smells presented are usually getting harder to detect and fix the higher you go up in the list. Once you are more accustomed to identifying and refactoring Cucumber smells, you can start checking out different ones in no specific order.
