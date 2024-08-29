# Practice Repositories

To help users learn about and practice identifying and removing code smells in Gherkin and Cucumber, we have set up a series of practice repositories. Each repository is dedicated to a different programming language and provides a hands-on environment where you can work with Gherkin feature files and Cucumber scenarios. These repositories allow you to explore various code smells, understand their impact, and practice refactoring to remove them.

## Available Repositories

The practice repositories are hosted on GitHub under the [Cucumber-Diseases](https://github.com/Cucumber-Diseases) organization. The repositories are as follows:

- [`cucumber-diseases-java`](https://github.com/Cucumber-Diseases/cucumber-diseases-java)
- [`cucumber-diseases-python`](https://github.com/Cucumber-Diseases/cucumber-diseases-python)
- [`cucumber-diseases-go`](https://github.com/Cucumber-Diseases/cucumber-diseases-go)
- [`cucumber-diseases-csharp`](https://github.com/Cucumber-Diseases/cucumber-diseases-csharp)

Each repository implements the same basic and simple application, using the `Customer.feature` file as a starting point. This consistent baseline allows you to compare and contrast the different smells and their resolutions across languages.

## How to Use the Repositories

### 1. Cloning the Repository:
To start practicing, clone the repository for the language you are interested in:

```bash
git clone https://github.com/Cucumber-Diseases/cucumber-diseases-<language>.git
```

Replace `<language>` with the programming language of your choice, such as `java`, `python`, `go`, or `csharp`.

### 2. Repository Structure:
Each repository contains:

- **Feature Files:** Starting with `Customer.feature`, where you can observe and practice identifying Gherkin and Cucumber-related code smells.
- **Tags for Smells:** The commit history of the `main` branch includes Git tags that correspond to specific code smells, allowing you to jump to a state where a particular smell is present.
- **Source Code of the Example Service**: Each repository contains a very slim implementation of a service that will be tested. It is simple and easy on purpose to not destract from the testing code.
- **Test Step Implementation**: The test suite is set up in a way that it works from the start. It should run all tests green directly after cloning and contains all relevant step definitions for the Gherkin feature file included.

### 3. Using Git Tags to Explore Smells:
The repositories utilize Git tags to help you navigate through different states of the codebase, each representing a specific code smell and its resolution. The tags follow a consistent naming convention:

- **`smell-XX`:** A tag that marks the state of the codebase where a specific code smell (`XX` corresponds to the smell ID) is present.
- **`smell-XX-solution`:** A tag that marks the state of the codebase after the smell has been removed.

To explore a specific code smell:

- **Checkout the Smell:** To view the codebase with a particular smell, use the following command:
```bash
git checkout tags/smell-XX
```

Replace `XX` with the specific smell ID you want to explore.

- **Compare with the Solution:** To see the changes required to remove the smell, you can use Git's diff command to compare the `smell-XX` tag with its corresponding `smell-XX-solution` tag:

```bash
git diff smell-XX smell-XX-solution
```

This will show you the differences between the smelly code and the refactored solution, helping you understand how to address the issue.

### 4. Setting Up the Project:
After checking out a specific state of the repository, refer to the README file for instructions on setting up the project in your local environment. This includes installing dependencies, running tests, and other language-specific setup steps.

### 5. Starting with Code Smell Identification and Refactoring:

Once you've set up the repository and are familiar with the structure, you can begin practicing the identification and refactoring of code smells:

* *Start with Exploration:* Begin by checking out the initial Customer.feature file in the repository. Examine the feature file and associated step definitions to see if you can identify any potential code smells on your own.
* *Use Git Tags for Guided Practice:* If you're unsure where to start, use the Git tags to jump directly to known code smells. For example, check out the smell-01 tag to explore the first documented code smell in the repository.
* *Refactor the Smell:* Once you've identified a smell, either by your own exploration or by checking out a tagged commit, try refactoring the code to remove the smell. Consider what changes are necessary to improve readability, maintainability, and the overall quality of the test code.
* *Validate Your Solution*: After making your changes, compare your refactoring with the solution provided under the corresponding smell-XX-solution tag. This will help you validate your approach and understand any differences.