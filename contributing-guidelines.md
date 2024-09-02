# Contributing to SCAR-iT-COLO LWM Linux Module 

So you're interested in contributing to the SCAR-iT LWM Linux Module? This document outlines the process for contributing to our project.

## Code of Conduct

By participating in this project, you agree to abide by our [Code of Conduct](code-of-conduct.md).

## How Can I Contribute?

Submit a [Pull Request](./PullRequestTemplate.md)  - and fill out the template.

### How to Reporting Bugs:

- Before creating bug reports, please check the issue list as you might find out that you don't need to create one.
- When you are creating a bug report, please include as many details as possible and follow the [Issue Template](./IssueTemplate.md)

### Suggesting Enhancements:

- Before creating enhancement suggestions, please check the issue list as you might find out that you don't need to create one.
- When you are creating an enhancement suggestion, please include as many details as possible.

### Your First Code Contribution:

1. Fork the repo.
2. Create your feature branch (`git checkout -b AmazingFeatureToAdd`)
3. Add the untracked files the the new branch! (`git add .`)
4. Commit your changes (`git commit -a`)
5. Add a comment into the text editor that has just appeared - noting what you added or changed.
6. Push to the branch (`git push`)
7. Open a Pull Request with the upstream repo (SCAR-iT LWM Module `dev` branch)

### Git Commit Messages:

- Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less.

### Documentation Styleguide:

- Use [Style Guide](StyleGuide.md) for documentation.

### Helpful Issue and Pull Request Labels:

- `bug` - Something isn't working
- `duplicate` - This issue or pull request already exists
- `enhancement` - New feature or request
- `help wanted` - Extra attention needed
- `invalid` - Doesn't seem right
- `question` - Further information is requested
- `wontfix` - This won't be fixed

## Branching Strategy
### As discussed earlier, Please label new branches with the suggested feature request or Bug report.
- `main` branch contains the stable, released version
- `dev` branch is for ongoing development (Pull Requests go here)
- `Feature` branches should be created for new content or significant changes

## Release Cycle

- Pull requests are merged into the `dev` branch when I get a chance.
The `main` branch is updated with the 'dev' branch when there are substantial changes.
- `Hotfixes` for critical issues should be flagged as `CRITICAL` and follow the same branch structure as everything else.

# Thank you for your time and contributions to the SCAR-iT-COLO LWM Module!!
