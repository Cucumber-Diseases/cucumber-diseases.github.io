# Collaboration Approach for Contributing New Smells

When contributing new smells to the `cucumber-diseases.github.io` repository, follow this collaboration process to ensure the new smells are documented and implemented across language-specific repositories, while minimizing the effort for contributors.

## 1. **Contribute the Smell to the Central Repository**
   - Create a pull request (PR) in the `cucumber-diseases.github.io` repository for your new smell.
   - Follow the contribution steps:
     - **Describe the new smell** using the smell template.
     - **Add a new exercise** that addresses the smell, using the exercise template.
     - If necessary, update **"golden master" feature files** to reflect changes in Gherkin syntax.
     - If needed, describe in the PR how to fix the smell in at least one **programming language**.

## 2. **Manually Open Issues in Language-Specific Repositories**
   - Once your PR is ready or merged into the documentation repository, **manually open issues** in all relevant language-specific repositories (e.g., Java, Python, C#, Go).
   - In each issue, include:
     - A brief description of the smell and how it affects the codebase.
     - A link to the documentation PR that introduces the new smell.
     - Any specific instructions for how the smell and its exercise should be implemented in that language.

## 3. **Link Issues in Your Documentation PR**
   - In the PR you open for the documentation, include **links to the manually created issues** in the language-specific repositories.
   - This will ensure visibility across all repositories and help track the adaptation process.

   Example:
   ```markdown
   Linked issues for language repositories:
   - [Java repository issue](https://github.com/cucumber-diseases-java/issues/123)
   - [Python repository issue](https://github.com/cucumber-diseases-python/issues/456)
   ```

## 4. **Cross-Repository Labeling and Tracking**
   - In the issues you create, use a consistent label like `smell-to-implement` to mark new smells requiring adaptation.
   - Optionally, maintain a **status dashboard** or tracking table in the documentation repository to monitor which smells have been implemented across different language repositories.

## 5. **Adaptation by Language-Specific Maintainers**
   - Contributors can provide a high-level description of how to address the smell in specific programming languages.
   - However, **language-specific maintainers** will handle the actual adaptation of the smell and exercise to their respective codebases, ensuring it aligns with the language's conventions and architecture.

## 6. **Streamlined Collaboration**
   - This process ensures contributors focus primarily on documenting new smells and exercises, while language maintainers focus on adapting them.
   - By manually creating issues and linking them in the documentation PR, contributors and maintainers can easily track progress across repositories.

