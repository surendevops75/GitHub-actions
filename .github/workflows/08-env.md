# GitHub Actions Environment Variables Example

This workflow demonstrates how environment variables (`env`) work in GitHub Actions at different levels:

* Workflow level
* Job level
* Step level

Environment variables help make CI/CD pipelines:

* Reusable
* Configurable
* Easier to maintain

Instead of hardcoding values multiple times, variables can be defined once and reused throughout the workflow.

This workflow also demonstrates how to use built-in GitHub context variables such as:

* `github.repository`
* `github.ref_name`
* `github.sha`

These variables are heavily used in real DevOps automation pipelines.

---

# Workflow File

```yaml
# Workflow name shown in GitHub Actions UI
name: Environment Example

# Trigger workflow on every push
on: [push]

# --------------------------------------------------------
# WORKFLOW-LEVEL ENVIRONMENT VARIABLES
# --------------------------------------------------------

# Variables defined here are available
# to all jobs and steps in workflow
env:

  # Application name
  APP_NAME: my-app

  # Global timeout value
  GLOBAL_TIMEOUT: 30

  # Owner or team name
  OWNER: "Join DevOps"

jobs:

  # --------------------------------------------------------
  # JOB DEFINITION
  # --------------------------------------------------------

  demo:

    # GitHub runner machine
    runs-on: ubuntu-latest

    # --------------------------------------------------------
    # JOB-LEVEL ENVIRONMENT VARIABLES
    # --------------------------------------------------------

    # Variables defined here are available
    # only inside this job
    env:

      # Job-specific variable
      JOB_ENV: "job-level-value"

      # AWS region example
      REGION: "ap-south-1"

    steps:

      # --------------------------------------------------------
      # PRINT WORKFLOW + JOB VARIABLES
      # --------------------------------------------------------

      - name: Show workflow-level + job-level env

        run: |

          echo "APP_NAME: $APP_NAME"
          echo "GLOBAL_TIMEOUT: $GLOBAL_TIMEOUT"
          echo "OWNER: $OWNER"

          echo "JOB_ENV: $JOB_ENV"
          echo "REGION: $REGION"

      # --------------------------------------------------------
      # STEP-LEVEL ENVIRONMENT VARIABLES
      # --------------------------------------------------------

      - name: Step with custom environment variables

        # Variables available only inside this step
        env:

          # Overrides workflow-level APP_NAME
          APP_NAME: "my-app-step"

          # Step-specific variable
          STEP_VAR2: "world"

        run: |

          echo "APP_NAME: $APP_NAME"
          echo "STEP_VAR2: $STEP_VAR2"

      # --------------------------------------------------------
      # GITHUB CONTEXT VARIABLES
      # --------------------------------------------------------

      - name: Using GitHub context

        run: |

          # Repository name
          echo "REPO: ${{ github.repository }}"

          # Current branch name
          echo "BRANCH: ${{ github.ref_name }}"

          # Commit SHA hash
          echo "COMMIT: ${{ github.sha }}"
```

---

# Important Concepts

# Environment Variables (`env`)

```yaml
env:
```

defines reusable variables inside workflow.

Benefits:

* Avoid hardcoding values
* Improve reusability
* Simplify maintenance
* Support dynamic configurations

---

# Workflow-Level Variables

Defined at top level:

```yaml
env:
```

Available to:

```text
All jobs
All steps
```

Example:

```yaml
APP_NAME: my-app
```

can be accessed anywhere using:

```yaml
$APP_NAME
```

---

# Job-Level Variables

Defined inside a job:

```yaml
jobs:
  demo:
    env:
```

Available only inside that specific job.

Example:

```yaml
REGION: "ap-south-1"
```

Commonly used for:

* AWS regions
* Deployment environments
* Job-specific configuration

---

# Step-Level Variables

Defined inside a step:

```yaml
steps:
  - name:
    env:
```

Available only inside that single step.

Example:

```yaml
STEP_VAR2: "world"
```

Useful for:

* Temporary variables
* Script customization
* One-time configurations

---

# Variable Override Priority

Environment variables follow this hierarchy:

```text
Step Level
    ↓
Job Level
    ↓
Workflow Level
```

Higher level overrides lower level.

---

# Example Override

Workflow level:

```yaml
APP_NAME: my-app
```

Step level:

```yaml
APP_NAME: my-app-step
```

Inside that step:

```text
my-app-step
```

will be used instead of:

```text
my-app
```

---

# Accessing Environment Variables

Variables are accessed using shell syntax:

```yaml
$VARIABLE_NAME
```

Example:

```yaml
echo "$APP_NAME"
```

---

# GitHub Context Variables

GitHub automatically provides runtime context variables.

---

# github.repository

```yaml
${{ github.repository }}
```

Returns:

```text
owner/repository-name
```

Example:

```text
surendra-devops/github-actions-demo
```

Used for:

* Logging
* Dynamic tagging
* Notifications

---

# github.ref_name

```yaml
${{ github.ref_name }}
```

Returns current branch name.

Examples:

```text
main
dev
feature-login
```

Used for:

* Branch-based deployments
* Conditional execution
* Environment selection

---

# github.sha

```yaml
${{ github.sha }}
```

Returns Git commit SHA hash.

Example:

```text
f9a12e45c67...
```

Used for:

* Docker image tagging
* Release tracking
* Deployment auditing

---

# Workflow Execution Flow

```text
Workflow Starts
       ↓
Workflow-level variables loaded
       ↓
Job starts
       ↓
Job-level variables loaded
       ↓
Step executes
       ↓
Step-level variables override values
       ↓
GitHub context variables printed
       ↓
Workflow Complete
```

---

# Real DevOps Use Cases

# Workflow-Level Variables

Used for:

* Global application names
* Shared configuration
* Organization-wide settings

---

# Job-Level Variables

Used for:

* Region selection
* Deployment environments
* Cloud provider settings

---

# Step-Level Variables

Used for:

* Temporary credentials
* Build arguments
* Dynamic script values

---

# GitHub Context Variables

Used for:

* Docker image versioning
* Deployment tracking
* Branch-specific automation
* Release management

Example:

```yaml
docker build -t app:${{ github.sha }}
```

---

# Why Environment Variables Are Important

Without environment variables:

* Workflows become hardcoded
* Duplicate values increase
* Maintenance becomes difficult

Environment variables help create:

* Reusable pipelines
* Cleaner YAML files
* Dynamic automation
* Easier configuration management

---

# Best Practice

Store sensitive values such as:

* API keys
* Passwords
* AWS credentials

inside:

```yaml
secrets
```

NOT inside:

```yaml
env
```

Example:

```yaml
${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

---

# Benefits of This Workflow Design

* Better configuration management
* Cleaner CI/CD pipelines
* Easier maintenance
* Reusable automation
* Dynamic workflow behavior

---

# Why This Workflow Is Important

This workflow demonstrates foundational DevOps automation concepts using:

* GitHub Actions
* Environment variables
* Variable scoping
* GitHub runtime contexts
* Dynamic pipeline configuration

These concepts are widely used in enterprise CI/CD pipelines.

---

# How to Run

1. Push code to repository
2. Open GitHub Actions tab
3. Observe workflow logs
4. Notice:

   * Workflow-level variables available everywhere
   * Job-level variables available only inside job
   * Step-level variables override values locally
   * GitHub context variables print repository details

---
