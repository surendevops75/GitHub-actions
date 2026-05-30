# GitHub Actions Conditional Execution Example

This workflow demonstrates how to use conditional execution in GitHub Actions using the `if` keyword.

Conditional execution allows specific steps or jobs to run only when certain conditions are met. This is commonly used in CI/CD pipelines to trigger different deployment stages based on:

* Branch names
* Tags
* Workflow status
* Environment selection

In this workflow:

* Production deployment runs only for the `main` branch
* Development deployment runs for feature branches

This helps automate branch-based deployment strategies.

---

# Workflow File

```yaml
# Workflow name shown in GitHub Actions UI
name: Conditions

# Trigger workflow on every push
on: [push]

jobs:

  # Job name
  conditions-demo:

    # GitHub runner machine
    runs-on: ubuntu-latest

    steps:

      # --------------------------------------------------------
      # BASIC STEP
      # --------------------------------------------------------

      - name: Print Hello World
        run: echo "Hello, world!"

      # --------------------------------------------------------
      # PRODUCTION DEPLOYMENT STEP
      # --------------------------------------------------------

      # Execute only when branch is main
      - name: trigger PROD deploy

        # Condition
        if: github.ref == 'refs/heads/main'

        run: echo "deploy to PROD"

      # --------------------------------------------------------
      # DEVELOPMENT DEPLOYMENT STEP
      # --------------------------------------------------------

      # Execute for feature branches
      - name: trigger DEV deploy

        # startsWith() is recommended for branch pattern matching
        if: startsWith(github.ref, 'refs/heads/feature-')

        run: echo "deploy to DEV"
```

---

# Important Concepts

# if Condition

```yaml
if:
```

controls conditional execution in GitHub Actions.

If condition evaluates to:

```text
true  → step executes
false → step skips
```

---

# github.ref

```yaml
github.ref
```

contains the full Git reference of the branch or tag that triggered workflow.

Examples:

```text
refs/heads/main
refs/heads/dev
refs/heads/feature-login
```

---

# Production Deployment Condition

```yaml
if: github.ref == 'refs/heads/main'
```

This means:

* Execute step only for `main` branch

Commonly used for:

* Production deployments
* Release workflows
* Main branch validations

---

# Feature Branch Condition

Original code:

```yaml
if: github.ref == 'refs/heads/feature-*'
```

This does NOT work correctly in GitHub Actions because wildcard matching is not supported with `==`.

Correct approach:

```yaml
if: startsWith(github.ref, 'refs/heads/feature-')
```

This checks whether branch name starts with:

```text
feature-
```

Examples:

```text
feature-login
feature-payment
feature-auth
```

---

# startsWith()

```yaml
startsWith()
```

is a GitHub Actions expression function used for pattern matching.

Syntax:

```yaml
startsWith(string, searchValue)
```

Example:

```yaml
startsWith(github.ref, 'refs/heads/feature-')
```

---

# Workflow Execution Flow

# Push to Main Branch

```text
Developer pushes code → main
               ↓
Workflow starts
               ↓
Hello World step runs
               ↓
PROD deployment executes
               ↓
DEV deployment skipped
```

---

# Push to Feature Branch

```text
Developer pushes code → feature-login
               ↓
Workflow starts
               ↓
Hello World step runs
               ↓
PROD deployment skipped
               ↓
DEV deployment executes
```

---

# Real DevOps Use Cases

# Production Deployment

```yaml
if: github.ref == 'refs/heads/main'
```

Used for:

* Production releases
* Infrastructure deployments
* Database migrations

---

# Feature Branch Pipelines

```yaml
startsWith(github.ref, 'refs/heads/feature-')
```

Used for:

* Pull request testing
* Development deployments
* Temporary environments
* Feature validation

---

# Other Common Conditional Functions

# contains()

```yaml
contains(github.ref, 'release')
```

Checks whether string contains value.

---

# endsWith()

```yaml
endsWith(github.ref, '-prod')
```

Checks whether string ends with value.

---

# success()

```yaml
if: success()
```

Runs only if previous steps succeed.

---

# failure()

```yaml
if: failure()
```

Runs only if workflow fails.

---

# Why Conditional Execution Is Important

Without conditions:

* Every branch may deploy applications
* Production environments become unsafe
* CI/CD pipelines waste resources

Conditional execution helps:

* Separate environments
* Automate branch strategies
* Protect production deployments
* Optimize pipeline execution

---

# Best Practice

Instead of:

```yaml
github.ref == 'refs/heads/feature-*'
```

Use:

```yaml
startsWith(github.ref, 'refs/heads/feature-')
```

for proper branch pattern matching.

---

# Benefits of This Workflow Design

* Branch-based deployment automation
* Safer production releases
* Faster feature validation
* Cleaner CI/CD pipelines
* Better deployment control

---

# Why This Workflow Is Important

This workflow demonstrates core CI/CD automation concepts using:

* GitHub Actions
* Conditional execution
* Branch-based deployment logic
* Workflow expression functions

These concepts are foundational in modern DevOps pipeline design.

---

# How to Run

1. Push code to main branch
2. Observe PROD deployment step execution

OR

1. Push code to feature branch

2. Observe DEV deployment step execution

3. Review workflow logs in GitHub Actions tab

---
