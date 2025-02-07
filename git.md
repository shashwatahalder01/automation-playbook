# 🚀 Git & Version Control Guide

## 📌 Introduction

Git is a powerful distributed version control system widely used for tracking changes in code, collaborating in teams, and automating CI/CD pipelines. This guide provides an in-depth look into Git best practices, automation strategies, and conventions to streamline version control processes.

---

## 📖 What You’ll Learn

- 🌱 **Git Basics** – Repositories, branches, commits, merges, and more.
- 🔄 **Git Workflow Strategies** – Git Flow, GitHub Flow, Trunk-Based Development.
- ✅ **Commit Message Conventions** – How to write meaningful commit messages.
- ⚡ **Git Automation** – Hooks, CI/CD, and scripting.
- 🔐 **Security Best Practices** – Secrets management, access control.
- 🛠 **Git Tools & Extensions** – CLI tools, GUI tools, and plugins.

---

## 📂 Git Basics

### 🏗️ Key Concepts

- **Repository**: A project’s version-controlled directory.
- **Commit**: A snapshot of changes in the repository.
- **Branch**: A parallel version of the project.
- **Merge**: Integrating changes from one branch into another.
- **Rebase**: Reapplying commits from one branch to another.
- **Remote**: A reference to a repository hosted elsewhere (e.g., GitHub, GitLab).
- **Pull Request (PR)**: A request to merge changes into the main branch.

### 🌱 Common Git Commands

```bash
# Initialize a new repository
git init

# Clone an existing repository
git clone <repo-url>

# Check repository status
git status

# Add files to staging
git add <file>

# Commit changes
git commit -m "Your commit message"

# Push changes to remote
git push origin <branch>

# Fetch and merge changes from remote
git pull origin <branch>

# Create a new branch
git checkout -b <new-branch>

# Switch to an existing branch
git checkout <branch>

# Merge branches
git merge <branch>
```

---

## 🛠 Git Workflow Strategies

### 🔄 **Git Flow**

A structured branching model with:

- `main` (Stable Production Code)
- `develop` (Integration & Ongoing Development)
- Feature, Release, Hotfix Branches

### 🔹 **GitHub Flow**

- Simpler, continuous deployment-friendly workflow.
- Develop on `main` branch using feature branches.
- Merge frequently and deploy continuously.

### 🔥 **Trunk-Based Development**

- Keep a single `main` branch, avoid long-lived branches.
- Use feature flags for incomplete work.
- Encourages rapid integration and minimal merge conflicts.

---

## ✅ Commit Message Conventions

A well-structured commit message improves collaboration, debugging, and automation. Follow the conventional commit format:

```
<type>(<scope>): <subject>

<body>  # Optional
<footer>  # Optional (e.g., references to issues, breaking changes)
```

### 🔹 **Types of Commits**

| Type      | Description                                         |
|-----------|-----------------------------------------------------|
| feat      | Introduces a new feature                           |
| fix       | Fixes a bug                                        |
| chore     | Maintenance tasks (e.g., build changes, tooling)   |
| docs      | Updates documentation                             |
| style     | Code style changes (e.g., formatting, no logic)   |
| refactor  | Code restructuring without changing functionality |
| perf      | Performance improvements                          |
| test      | Adds or updates tests                             |
| ci        | Continuous integration-related changes           |
| build     | Changes affecting the build system or dependencies |
| revert    | Reverts a previous commit                        |

### Commit Scope (Optional)

The scope specifies the part of the codebase affected, such as:

```
feat(auth): add JWT-based authentication
fix(api): resolve CORS issue
test(ui): add Cypress tests for login page
```

### Best Practices

✅ Use the imperative mood: "Add feature" instead of "Added feature".  
✅ Keep the subject line under 72 characters.  
✅ Use present tense (e.g., "fix bug" instead of "fixed bug").  
✅ Reference issues if needed: `fix(auth): resolve #123`.  
✅ Avoid generic messages like "fixed issue".  

---

## ✅ Sample Commit Message Examples

### 1. Initializing the Project
```
init: initialize project structure

Set up initial directory structure with basic configuration files for the project.
```

### 2. Build & CI Setup
```
ci: add GitHub Actions for CI pipeline

Configured GitHub Actions to run tests and deploy on push to main branch.
```

### 3. Make a Release
```
release: v1.0.0

Initial release of the project with basic features and CI pipeline setup.
```

### 4. Add Features
```
feat(auth): implement JWT authentication

Added JWT-based authentication for user login and token validation.
```
```
feat(cart): add item quantity update functionality

Users can now update the quantity of items in the shopping cart.
```

### 5. Fix Bugs
```
fix(ui): resolve login form validation bug

Fixed an issue where the login form was incorrectly validating empty fields.
```
```
fix(cart): correct price calculation when updating quantity

Fixed a bug where the price was not recalculated correctly after updating item quantity.
```

### 6. Add Tests
```
test(auth): add unit tests for JWT token validation

Created tests to ensure the JWT token validation logic works as expected.
```
```
test(cart): add integration tests for cart item updates

Added integration tests to verify the cart item update functionality.
```

### 7. Add ReadMe/Docs
```
docs(readme): update setup instructions

Updated the README with clear setup and installation instructions.
```
```
docs(api): add API documentation for user authentication

Documented the endpoints and request/response formats for user authentication.
```

### 8. Refactor Code
```
refactor(auth): simplify JWT token generation

Refactored the JWT token generation logic to make it more concise and efficient.
```
```
refactor(cart): extract cart logic into separate service

Moved the cart logic into a dedicated service for better code organization.
```

### 9. Improve Performance
```
perf(cart): optimize cart item update algorithm

Improved the cart item update algorithm to reduce computation time for large carts.
```
```
perf(api): enhance API response time for product list

Optimized database queries to improve API response time when fetching product list.
```

---

## 🔄 Git Automation

### 🔥 **Git Hooks**

Git hooks allow automation of tasks like running tests before committing.

- **Pre-commit hook** – Runs before committing.
- **Pre-push hook** – Runs before pushing.
- **Post-merge hook** – Runs after merging branches.

Example: **Enforce commit message convention** (pre-commit hook)

```bash
#!/bin/sh
commit_msg=$(cat "$1")
if ! echo "$commit_msg" | grep -E '^(feat|fix|docs|style|refactor|test|chore)'; then
  echo "🚨 Commit message must follow convention!"
  exit 1
fi
```

Save this script in `.git/hooks/pre-commit` and make it executable:

```bash
chmod +x .git/hooks/pre-commit
```

### ⚡ **CI/CD Integration**

Use Git automation tools like GitHub Actions, GitLab CI/CD, or Jenkins.

**Example: GitHub Actions CI/CD Pipeline**

```yaml
name: Run Tests
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 16
      - name: Install Dependencies
        run: npm install
      - name: Run Tests
        run: npm test
```

---

## 🔐 Security Best Practices

### 🚨 **Avoid Storing Secrets in Git**

- Use `.gitignore` to exclude sensitive files.
- Use environment variables or secret managers.
- Rotate credentials frequently.

**Example: Adding sensitive files to `.gitignore`**

```
.env
secrets.json
config/private/
```

### ✅ **Signing Commits**

Sign your commits for authenticity:

```bash
gpg --gen-key
git config --global user.signingkey <GPG-KEY-ID>
git commit -S -m "Signed commit"
```

---

## 🛠 Useful Git Tools & Extensions

### 🔥 **CLI Enhancements**

- `git log --oneline --graph --decorate --all` – Visualizes history.
- `git diff --color-words` – Highlights text differences.

### 📊 **GUI Tools**

- **GitKraken** – Graphical UI for Git.
- **Sourcetree** – Visual Git client.
- **GitHub Desktop** – Simplifies workflows.

---

## 🚀 Conclusion

By following these Git best practices, automation strategies, and security measures, you can create a robust version control workflow. Master Git hooks, commit conventions, and CI/CD integrations to enhance your development process! 🚀

---

Happy coding! 💻🔥
