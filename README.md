# EuroMotors AG – Reusable Workflows

This repository hosts the **official reusable GitHub Actions workflows**
used across all **EuroMotors AG** repositories.  
They standardize CI/CD for code quality, builds, tests, and deployments.

---

## Overview

EuroMotors provides **five reusable and recommended workflows**:

| 🔧 Workflow | 📝 Description | ✅ Recommended Use |
|-------------|----------------|--------------------|
| 🧩 **ci.yml** | Runs core jobs — **Lint → Build → Test** in sequence. | Default choice for most repositories. |
| 🧱 **build.yml** | Compiles and validates **TypeScript/React** projects. | For repos needing only build verification. |
| 🧹 **lint.yml** | Runs **ESLint** and formatting checks. | For lightweight or static repositories. |
| 🧪 **test.yml** | Executes **unit/integration tests** via `pnpm test`. | For backend or shared libraries. |
| 🤖 **dependabot.yml** | Automates dependency and Actions updates. | Active in all repositories. |

---

## Usage

In any EuroMotors repository, reference these workflows with `uses:`:

```yaml
jobs:
  ci:
    uses: euromotors-ag/eumotors-actions/.github/workflows/ci.yml@v1
    secrets: inherit

```

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
