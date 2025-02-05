# 📂 Project Setup & Folder Structure

## 🚀 Introduction

Setting up a well-structured test automation project is crucial for maintainability, scalability, and collaboration. This guide provides best practices for organizing your **Automation Playbook** repository efficiently.

---

## 📌 Recommended Folder Structure

A clean and modular folder structure improves readability and ease of maintenance. Below is a suggested structure for automation projects:

```plaintext
automation-playbook/
│-- src/                      # Source files (test framework, utilities, etc.)
│   ├── pages/                # Page Object Model (POM) files
│   │   ├── login.page.ts     # Example: Login page actions
│   │   ├── dashboard.page.ts # Example: Dashboard page actions
│   ├── tests/                # Test scripts
│   │   ├── login.test.ts     # Example: Login test cases
│   │   ├── dashboard.test.ts # Example: Dashboard test cases
│   ├── utils/                # Helper functions (e.g., waitFor, API handlers)
│   ├── config/               # Configuration files (e.g., environment settings)
│   ├── data/                 # Test data files (e.g., JSON, CSV, DB data)
│-- reports/                  # Test reports & logs
│-- docs/                     # Documentation (guides, API references)
│-- .github/                  # GitHub-specific files (CI/CD workflows, issue templates)
│-- package.json              # Dependencies & scripts
│-- tsconfig.json             # TypeScript configuration
│-- README.md                 # Project documentation
```

---

## 📌 Explanation of Folders

### 📂 `src/`

Houses the main test automation framework, including:

- **`pages/`**: Implements the Page Object Model (POM) to separate UI interactions.
- **`tests/`**: Contains test cases organized by feature.
- **`utils/`**: Utility/helper functions for better reusability.
- **`config/`**: Stores environment variables, API URLs, and configurations.
- **`data/`**: Test data in various formats (JSON, CSV, etc.).

### 📂 `reports/`

Stores test execution reports and logs. Tools like **Allure, Mochawesome, or HTML reports** can be integrated.

### 📂 `docs/`

Contains documentation, including setup guides and API references.

### 📂 `.github/`

Includes GitHub-specific files:

- **CI/CD workflows** (e.g., GitHub Actions YAML files for test execution).
- **Issue templates** to streamline bug reporting.

### 📄 `package.json`

Defines dependencies and npm scripts for automation execution.

### 📄 `tsconfig.json`

Configures TypeScript settings for the automation framework.

---

## 🔧 Setting Up the Project

### 1️⃣ Clone the Repository

```sh
git clone https://github.com/yourusername/automation-playbook.git
cd automation-playbook
```

### 2️⃣ Install Dependencies

```sh
npm install  # For Node.js & TypeScript projects
pip install -r requirements.txt  # For Python projects
composer install  # For PHP projects
```

### 3️⃣ Run Tests

```sh
npm test  # Run tests for Node.js projects
pytest    # Run tests for Python projects
vendor/bin/codecept run  # Run tests for PHP projects
```

---

## 🎯 Best Practices

✅ **Follow a Modular Approach** – Keep reusable functions in the `utils/` directory.  
✅ **Separate Test Data from Test Logic** – Store data in `data/` and avoid hardcoded values.  
✅ **Use Environment Variables** – Keep sensitive data like API keys in `.env` files.  
✅ **Organize Tests Logically** – Group tests based on features (e.g., `tests/authentication/`).  
✅ **Enable Logging & Reporting** – Generate logs in the `reports/` directory for easy debugging.

---

## 📢 Conclusion

A well-structured automation framework ensures better test management, collaboration, and scalability. Follow these best practices to keep your test suite clean and efficient. 🚀
