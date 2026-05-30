# GitHub Actions Workflow Inputs Example

This workflow demonstrates how to use manual inputs in GitHub Actions using `workflow_dispatch`.

Workflow inputs allow users to provide values dynamically while triggering workflows from the GitHub Actions UI. This makes CI/CD pipelines flexible and reusable instead of hardcoding values directly inside workflow files.

The workflow includes multiple input types such as:

* String input
* Environment input
* Boolean input
* Choice dropdown
* Numeric/text input

These inputs are commonly used in DevOps pipelines for:

* Deployment environment selection
* Version selection
* Deployment approvals
* Debug mode configuration
* Runtime customization

---

# Workflow File

```yaml
# Workflow name shown in GitHub Actions UI
name: Inputs Demo

# --------------------------------------------------------
# MANUAL WORKFLOW TRIGGER
# --------------------------------------------------------

on:

  # Allows workflow execution from GitHub UI
  workflow_dispatch:

    # --------------------------------------------------------
    # WORKFLOW INPUTS
    # --------------------------------------------------------

    inputs:

      # --------------------------------------------------------
      # STRING INPUT
      # --------------------------------------------------------

      # User name input
      name:

        # Description shown in UI
        description: "Enter your name"

        # Input is mandatory
        required: true

        # Default value shown in UI
        default: "DevOps Engineer"

      # --------------------------------------------------------
      # ENVIRONMENT INPUT
      # --------------------------------------------------------

      # GitHub environment selector
      env:

        # Description shown in UI
        description: "Select environment (GitHub environment type)"

        # Input required
        required: true

        # Environment input type
        # Displays GitHub environments list
        type: environment

      # --------------------------------------------------------
      # BOOLEAN INPUT
      # --------------------------------------------------------

      # Checkbox input
      deploy:

        # Description shown in UI
        description: "Do you want to deploy?"

        # Boolean type
        type: boolean

        # Mandatory input
        required: true

        # Default checkbox value
        default: false

      # --------------------------------------------------------
      # CHOICE INPUT
      # --------------------------------------------------------

      # Dropdown selection input
      log_level:

        # Description shown in UI
        description: "Choose log level"

        # Dropdown type
        type: choice

        # Allowed dropdown options
        options:
          - info
          - warn
          - error

        # Mandatory selection
        required: true

        # Default selected option
        default: info

      # --------------------------------------------------------
      # TEXT/NUMBER INPUT
      # --------------------------------------------------------

      # Retry count input
      retry_count:

        # Description shown in UI
        description: "Number of retries"

        # Optional input
        required: false

        # Default value
        default: "3"

jobs:

  # --------------------------------------------------------
  # JOB DEFINITION
  # --------------------------------------------------------

  print-inputs:

    # GitHub runner machine
    runs-on: ubuntu-latest

    steps:

      # --------------------------------------------------------
      # PRINT INPUT VALUES
      # --------------------------------------------------------

      - name: Print Inputs

        run: |

          # Print string input
          echo "Name: ${{ github.event.inputs.name }}"

          # Print selected environment
          echo "Environment: ${{ github.event.inputs.env }}"

          # Print retry count
          echo "Retry Count: ${{ github.event.inputs.retry_count }}"
```

---

# Important Concepts

# workflow_dispatch

```yaml
workflow_dispatch
```

Allows workflows to be triggered manually from GitHub UI.

Commonly used for:

* Deployments
* Infrastructure changes
* Release management
* Manual approvals

---

# Inputs

```yaml
inputs:
```

Creates interactive fields in GitHub Actions UI.

Users can provide runtime values while starting workflow.

---

# String Input

```yaml
name:
```

Simple text field input.

Example:

```text
DevOps Engineer
Surendra
Production Deployment
```

---

# Environment Input

```yaml
type: environment
```

Displays available GitHub environments.

Examples:

```text
dev
qa
uat
prod
```

Benefits:

* Standardized environment selection
* Environment protection support
* Safer deployments

---

# Boolean Input

```yaml
type: boolean
```

Creates checkbox input.

Values:

```text
true
false
```

Used for:

* Deployment approvals
* Feature toggles
* Debug mode
* Optional execution

---

# Choice Input

```yaml
type: choice
```

Creates dropdown selection.

Example:

```yaml
options:
  - info
  - warn
  - error
```

Benefits:

* Prevents invalid input
* Standardizes values
* Improves workflow safety

---

# Default Values

```yaml
default:
```

Pre-populates input values in UI.

Example:

```yaml
default: info
```

---

# Accessing Input Values

Inputs are accessed using:

```yaml
${{ github.event.inputs.<input_name> }}
```

Example:

```yaml
${{ github.event.inputs.name }}
```

---

# Workflow Execution Flow

```text
User opens GitHub Actions
           ↓
Selects workflow
           ↓
Enters input values
           ↓
Starts workflow
           ↓
GitHub runner starts
           ↓
Workflow reads inputs
           ↓
Job executes using provided values
```

---

# Real DevOps Use Cases

# Environment Selection

Used for:

* dev deployments
* qa deployments
* staging deployments
* production deployments

---

# Deployment Control

Using boolean input:

```yaml
deploy:
```

to:

* Enable deployment
* Skip deployment
* Trigger optional stages

---

# Logging Configuration

Using:

```yaml
log_level:
```

to dynamically configure:

* Debug logs
* Warning logs
* Error-only logs

---

# Retry Logic

Using:

```yaml
retry_count:
```

to configure:

* Deployment retries
* API retries
* Automation retries

---

# Why Workflow Inputs Are Important

Without inputs:

* Pipelines become hardcoded
* Multiple workflow files are needed
* Reusability decreases

Workflow inputs help create:

* Dynamic CI/CD pipelines
* Reusable automation
* Controlled deployments
* User-friendly workflows

They are widely used in modern DevOps automation using GitHub Actions.

---

# How to Run

1. Open GitHub repository
2. Go to Actions tab
3. Select `Inputs Demo`
4. Click `Run workflow`
5. Enter input values
6. Start workflow
7. Observe printed values in workflow logs

---
