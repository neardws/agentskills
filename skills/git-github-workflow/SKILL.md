---
name: git-github-workflow
description: Standard Git and GitHub workflow practices, including Conventional Commits, Pull Request creation/merging/review, and using the GitHub CLI (gh). Use when managing code versions, collaborating on PRs, or organizing commit history.
---

# Git/GitHub Workflow Skill

This skill provides instructions for professional Git and GitHub collaboration workflows.

## Git Commit Standards (Conventional Commits)

Always use the [Conventional Commits](https://www.conventionalcommits.org/) format for commit messages:

`<type>(<scope>): <description>`

### Common Types:
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `perf`: A code change that improves performance
- `test`: Adding missing tests or correcting existing tests
- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to our CI configuration files and scripts
- `chore`: Other changes that don't modify src or test files
- `revert`: Reverts a previous commit

## GitHub Pull Request Workflow

1. **Branching**: Create a new branch for each feature or fix.
   ```bash
   git checkout -b <branch-name>
   ```
2. **Commit**: Use Conventional Commits.
3. **Push**: Push the branch to the remote repository.
   ```bash
   git push -u origin <branch-name>
   ```
4. **Create PR**: Use `gh pr create` or the GitHub web interface.
   - Provide a clear title and description.
   - Reference related issues (e.g., `Closes #123`).
5. **Review**: Reviewers provide feedback. Address feedback with additional commits.
6. **Merge**: Once approved and CI passes, merge the PR (Squash and Merge is often preferred).
7. **Cleanup**: Delete the local and remote branch.

## Using GitHub CLI (`gh`)

The `gh` tool speeds up common GitHub tasks:

- **Issues**: `gh issue list`, `gh issue create`, `gh issue view <id>`
- **Pull Requests**: `gh pr list`, `gh pr create`, `gh pr checkout <id>`, `gh pr merge`
- **Actions**: `gh run list`, `gh run view`
- **Workflow**: `gh browse` to open the repo in a browser.

## Best Practices

- Keep PRs small and focused.
- Ensure all tests pass before requesting a review.
- Write descriptive PR summaries.
- Use `git pull --rebase` to keep a clean history.
