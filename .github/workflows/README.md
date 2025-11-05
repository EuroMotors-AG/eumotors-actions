# EuroMotors AG – Workflow Templates

This folder contains the **official CI and automation workflow templates** used across all **EuroMotors AG** repositories.  
They define our standardized **GitHub Actions** pipelines for code quality, builds, testing, and dependency maintenance.

---

## Overview

EuroMotors provides **five reusable and recommended workflow templates**:

| 🔧 Template | 📝 Description | ✅ Recommended Use |
|-------------|----------------|--------------------|
| 🧩 **ci.yml** | Runs all core jobs: **Lint → Build → Test** in sequence. | ✅ Default choice for most repositories. |
| 🧱 **build.yml** | Compiles and validates **TypeScript/React** projects. | For projects that only need build verification. |
| 🧹 **lint.yml** | Runs **ESLint** and formatting checks for TypeScript/React codebases. | For lightweight or static repositories. |
| 🧪 **test.yml** | Executes **unit and integration tests** using `pnpm test`. | For backend or library testing. |
| 🤖 **dependabot.yml** | Keeps dependencies and GitHub Actions versions up-to-date automatically. | ✅ Active in all repositories. |

---

## How to Use

When creating a new repository in the **EuroMotors AG** organization:

1. Navigate to the **Actions** tab.  
2. Click **New workflow**.  
3. Under **“By EuroMotors AG”**, choose one of the templates (preferably **CI (Lint + Build + Test)**).  
4. Click **Configure** → **Commit changes**.  
5. GitHub automatically places the file under `.github/workflows/`.

Once committed, workflows run automatically on every **push** or **pull request** to your default branch.

---

## Dependabot Automation

EuroMotors uses **Dependabot** to monitor and maintain package and workflow dependencies:

- Automatically scans all repositories for vulnerable or outdated packages.  
- Opens weekly PRs for dependency upgrades (`pnpm`, `npm`, and GitHub Actions).  
- Triggers the CI pipeline (`ci.yml`) on every update PR.  
- Keeps the ecosystem stable, secure, and current.

**Configuration file:**  
`.github/dependabot.yml`

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

<br/>

>[!NOTE]
>Dependabot PRs must pass the CI checks before merge, as enforced by branch protection rules.
