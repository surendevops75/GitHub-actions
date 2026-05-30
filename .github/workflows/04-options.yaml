# GitHub Actions Timeout and Concurrency Example

This workflow demonstrates how to use:

* `timeout-minutes`
* `concurrency`

in GitHub Actions.

These features are very important in CI/CD pipelines because they help:

* Prevent stuck workflows
* Avoid duplicate executions
* Optimize runner usage
* Protect deployments from conflicts

This workflow intentionally runs a long-running task to demonstrate how timeout behavior works.

---

# Workflow File

```yaml
# Workflow name shown in GitHub Actions UI
name: Timeout Example

# Trigger workflow on every push
on: [push]

# --------------------------------------------------------
# CONCURRENCY CONFIGURATION
# --------------------------------------------------------

concurrency:

  # Unique concurrency group
  # Combines repository + branch reference
  group: ${{ github.repository }}-${{ github.ref }}

  # If a new workflow starts for same group:
  # - cancel currently running workflow
  # - start latest workflow
  cancel-in-progress: true

jobs:

  # Job name
  test-timeout:

    # GitHub runner machine
    runs-on: ubuntu-latest

    # --------------------------------------------------------
    # JOB TIMEOUT
    # --------------------------------------------------------

    # Maximum execution time allowed for job
    # GitHub automatically terminates job after 5 minutes
    timeout-minutes: 5

    steps:

      # --------------------------------------------------------
      # START STEP
      # --------------------------------------------------------

      - name: Start job
        run: echo "This job will timeout if it runs longer than 5 minutes."

      # --------------------------------------------------------
      # LONG RUNNING TASK
      # --------------------------------------------------------

      - name: Simulate long running task

        run: |

          # Print message in logs
          echo "Sleeping for 10 minutes..."

          # Sleep for 600 seconds (10 minutes)
          sleep 600
```

---

# Important Concepts

# timeout-minutes

```yaml
timeout-minutes: 5
```

Defines maximum execution time for a job.

If job execution exceeds:

```text
5 minutes
```

GitHub Actions:

* Stops the job
* Marks workflow as failed
* Releases runner resources

---

# Why Timeout Is Important

Without timeout:

* Jobs may run forever
* Pipelines may get stuck
* Runner resources get wasted
* CI/CD queues become blocked

Timeout helps:

* Improve pipeline reliability
* Reduce infrastructure waste
* Prevent infinite execution loops

---

# sleep 600

```yaml
sleep 600
```

Pauses execution for:

```text
600 seconds = 10 minutes
```

This intentionally exceeds:

```yaml
timeout-minutes: 5
```

so GitHub terminates the job automatically.

---

# concurrency

```yaml
concurrency:
```

Prevents multiple workflows from running simultaneously for same group.

Useful for:

* Deployments
* Infrastructure changes
* Shared resource pipelines

---

# group

```yaml
group: ${{ github.repository }}-${{ github.ref }}
```

Creates unique concurrency identifier.

Breakdown:

```text
github.repository → repository name
github.ref        → branch reference
```

Example generated group:

```text
roboshop-catalogue-refs/heads/main
```

This means:

* Each branch gets separate concurrency control

---

# cancel-in-progress

```yaml
cancel-in-progress: true
```

Behavior:

* Existing running workflow gets cancelled
* Latest workflow starts immediately

Example:

```text
Push commit A
      ↓
Workflow starts
      ↓
Push commit B
      ↓
Workflow A cancelled
      ↓
Workflow B starts
```

---

# Why Concurrency Is Important

Without concurrency:

* Multiple deployments may run simultaneously
* Older deployments may overwrite newer changes
* Runner resources may be wasted

Concurrency helps:

* Ensure latest code gets priority
* Prevent deployment conflicts
* Reduce duplicate executions

---

# Workflow Execution Flow

```text
Developer pushes code
          ↓
Workflow starts
          ↓
Concurrency group check
          ↓
Previous workflow cancelled (if running)
          ↓
Runner starts job
          ↓
Long-running task begins
          ↓
Job exceeds 5 minutes
          ↓
GitHub automatically terminates job
          ↓
Workflow marked as failed
```

---

# Real DevOps Use Cases

# timeout-minutes

Used for:

* Long-running test protection
* Deployment timeout control
* Terraform execution safety
* Kubernetes rollout monitoring

Example:

```yaml
timeout-minutes: 30
```

---

# concurrency

Used for:

* Production deployments
* Infrastructure provisioning
* Terraform apply protection
* Kubernetes deployment locking

Common example:

```text
Only one production deployment at a time
```

---

# Production Best Practices

## Use Timeouts

Always define:

```yaml
timeout-minutes:
```

for:

* Build jobs
* Test jobs
* Deployment jobs

---

## Use Concurrency

Recommended for:

* Production pipelines
* Stateful deployments
* Shared infrastructure automation

---

# Benefits of This Workflow Design

* Prevents stuck CI/CD jobs
* Saves GitHub runner minutes
* Avoids duplicate deployments
* Prioritizes latest changes
* Improves pipeline stability

---

# Why This Workflow Is Important

This workflow demonstrates advanced CI/CD control mechanisms using:

* GitHub Actions
* Timeout management
* Concurrency control
* Workflow cancellation handling

These concepts are heavily used in enterprise DevOps environments to build reliable and scalable automation pipelines.

---

# How to Run

1. Push code to repository

2. Open GitHub Actions tab

3. Observe workflow execution

4. Notice:

   * Workflow starts
   * Sleep command runs
   * Job gets terminated after 5 minutes

5. Push multiple commits quickly to observe concurrency behavior

---
