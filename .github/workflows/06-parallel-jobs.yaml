# GitHub Actions Parallel and Sequential Jobs Example

This workflow demonstrates how jobs execute in parallel and sequential order in GitHub Actions using the `needs` keyword.

By default:

```text
GitHub Actions runs jobs in parallel
```

However, some jobs may depend on other jobs and should only execute after previous jobs complete successfully. The `needs` keyword is used to create these dependencies.

This workflow contains:

* Parallel jobs
* Sequential jobs
* Job dependency chaining

which are very common concepts in CI/CD pipeline design.

---

# Workflow File

```yaml
# Workflow name shown in GitHub Actions UI
name: parellel

# Trigger workflow on every push
on: [push]

jobs:

  # --------------------------------------------------------
  # JOB 1
  # --------------------------------------------------------

  job-1:

    # GitHub runner machine
    runs-on: ubuntu-latest

    steps:

      # Simulate long-running task
      - name: Print Hello World

        # Sleep for 20 seconds
        run: sleep 20

  # --------------------------------------------------------
  # JOB 2
  # --------------------------------------------------------

  job-2:

    # This job depends on job-1
    # job-2 starts only after job-1 completes successfully
    needs: job-1

    runs-on: ubuntu-latest

    steps:
      - name: Print Hello World
        run: sleep 20

  # --------------------------------------------------------
  # JOB 3
  # --------------------------------------------------------

  job-3:

    # No dependency defined
    # Runs immediately in parallel
    runs-on: ubuntu-latest

    steps:
      - name: Print Hello World
        run: sleep 20

  # --------------------------------------------------------
  # JOB 4
  # --------------------------------------------------------

  job-4:

    # Depends on job-2
    # Starts only after job-2 completes successfully
    needs: job-2

    runs-on: ubuntu-latest

    steps:
      - name: Print Hello World
        run: sleep 20
```

---

# Important Concepts

# Parallel Job Execution

By default:

```text
Jobs without dependencies run in parallel
```

In this workflow:

* `job-1`
* `job-3`

start simultaneously because they do not depend on each other.

This helps:

* Reduce workflow execution time
* Improve CI/CD efficiency
* Optimize runner utilization

---

# needs Keyword

```yaml
needs:
```

creates dependency between jobs.

Example:

```yaml
needs: job-1
```

means:

```text
job-2 waits for job-1
```

If `job-1` fails:

* `job-2` will not execute

---

# Sequential Job Execution

Dependency chain in this workflow:

```text
job-1 → job-2 → job-4
```

This creates sequential execution flow.

Used when:

* One job requires artifacts from another
* Deployment must happen after build
* Tests must pass before release

---

# Independent Parallel Job

```yaml
job-3
```

runs independently because:

```yaml
needs:
```

is not defined.

This job executes immediately in parallel with `job-1`.

---

# sleep 20

```yaml
run: sleep 20
```

pauses execution for:

```text
20 seconds
```

This is used to simulate:

* Long-running tasks
* Build processes
* Test execution
* Deployment operations

It helps visualize:

* Parallel execution
* Sequential execution timing

---

# Workflow Execution Flow

```text
Workflow Starts
       ↓
job-1 ───────────────┐
                     │
job-3 ───────────────┘   (parallel execution)
       ↓
job-2 waits for job-1
       ↓
job-4 waits for job-2
       ↓
Workflow Complete
```

---

# Actual Execution Order

## Step 1

```text
job-1 and job-3 start together
```

because they are independent.

---

## Step 2

```text
job-2 waits for job-1
```

---

## Step 3

```text
job-4 waits for job-2
```

---

# Real DevOps Use Cases

# Parallel Jobs

Used for:

* Running tests simultaneously
* Security scanning
* Linting
* Multi-platform builds
* Docker image builds

Example:

```text
Frontend Tests
Backend Tests
Security Scan
```

running together.

---

# Sequential Jobs

Used for:

* Build → Test → Deploy pipelines
* Terraform workflows
* Kubernetes deployments
* Release pipelines

Example:

```text
Build Application
        ↓
Run Tests
        ↓
Push Docker Image
        ↓
Deploy to Kubernetes
```

---

# Benefits of Parallel Execution

* Faster CI/CD pipelines
* Reduced deployment time
* Better runner utilization
* Faster feedback to developers

---

# Benefits of Sequential Execution

* Controlled workflow order
* Dependency management
* Safer deployments
* Better release orchestration

---

# What Happens If Dependency Fails?

Example:

```text
job-1 fails
      ↓
job-2 skipped
      ↓
job-4 skipped
```

This prevents invalid downstream execution.

---

# Best Practice

Use:

```yaml
needs:
```

only when jobs truly depend on each other.

Too many dependencies:

* Slow pipelines
* Reduce parallelism
* Increase execution time

---

# Why This Workflow Is Important

This workflow demonstrates core CI/CD pipeline orchestration concepts using:

* GitHub Actions
* Parallel job execution
* Sequential job dependencies
* Workflow optimization

These concepts are heavily used in enterprise DevOps automation pipelines.

---

# How to Run

1. Push code to repository

2. Open GitHub Actions tab

3. Observe workflow execution order

4. Notice:

   * `job-1` and `job-3` run together
   * `job-2` waits for `job-1`
   * `job-4` waits for `job-2`

5. Review workflow timing in Actions UI

---
