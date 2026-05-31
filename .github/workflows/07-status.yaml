# GitHub Actions Post Section Example

This workflow demonstrates how to implement Jenkins-style post actions in GitHub Actions using conditional expressions.

Unlike Jenkins, GitHub Actions does not provide a dedicated:

```text
post {
}
```

block.

Instead, post-build behavior is implemented using:

```yaml
if:
```

conditions with built-in workflow status functions such as:

* `success()`
* `failure()`
* `cancelled()`
* `always()`

These conditions are commonly used in CI/CD pipelines for:

* Notifications
* Cleanup tasks
* Rollbacks
* Log uploads
* Deployment status handling

This workflow intentionally fails the build step to demonstrate post-condition behavior.

---

# Workflow File

```yaml
jobs:

  # --------------------------------------------------------
  # JOB NAME
  # --------------------------------------------------------

  build:

    # GitHub runner machine
    runs-on: ubuntu-latest

    steps:

      # --------------------------------------------------------
      # MAIN JOB STEPS
      # --------------------------------------------------------

      # Simulate repository checkout
      - name: Checkout

        run: echo "Cloning repo..."

      # --------------------------------------------------------
      # BUILD STEP
      # --------------------------------------------------------

      - name: Run build

        run: |

          # Print build message
          echo "Running build..."

          # Force step failure intentionally
          # exit code 1 = failure
          exit 1

      # --------------------------------------------------------
      # POST SECTION (Jenkins Style)
      # --------------------------------------------------------

      # --------------------------------------------------------
      # SUCCESS HANDLER
      # --------------------------------------------------------

      # Executes only when all previous steps succeed
      - name: Post - Success

        if: ${{ success() }}

        run: echo "🎉 Job SUCCESS — run success tasks here"

      # --------------------------------------------------------
      # FAILURE HANDLER
      # --------------------------------------------------------

      # Executes only when workflow/job fails
      - name: Post - Failure

        if: ${{ failure() }}

        run: echo "❌ Job FAILED — run failure actions here"

      # --------------------------------------------------------
      # CANCEL HANDLER
      # --------------------------------------------------------

      # Executes only when workflow gets cancelled
      - name: Post - Cancelled

        if: ${{ cancelled() }}

        run: echo "🛑 Job CANCELLED — run cancel handlers here"

      # --------------------------------------------------------
      # ALWAYS HANDLER
      # --------------------------------------------------------

      # Executes regardless of workflow result
      # Commonly used for cleanup tasks
      - name: Post - Always

        if: ${{ always() }}

        run: echo "🔄 ALWAYS — this runs no matter what (cleanup)"
```

---

# Important Concepts

# success()

```yaml
if: ${{ success() }}
```

Runs step only when:

```text
All previous steps completed successfully
```

Used for:

* Success notifications
* Deployment completion
* Release tagging
* Artifact publishing

---

# failure()

```yaml
if: ${{ failure() }}
```

Runs step only when:

```text
Any previous step fails
```

In this workflow:

```yaml
exit 1
```

forces build failure.

Therefore:

```text
Post - Failure step executes
```

Used for:

* Slack alerts
* Rollback execution
* Error reporting
* Incident notifications

---

# cancelled()

```yaml
if: ${{ cancelled() }}
```

Runs step only when workflow execution is cancelled.

Cancellation may happen because:

* Manual cancellation
* Concurrency cancellation
* Timeout termination

Used for:

* Cleanup tasks
* Release unlocks
* Resource destruction

---

# always()

```yaml
if: ${{ always() }}
```

Runs regardless of:

* Success
* Failure
* Cancellation

Equivalent to:

```text
finally block
```

in programming languages.

Commonly used for:

* Cleanup operations
* Log collection
* Artifact uploads
* Temporary file deletion

---

# exit 1

```yaml
exit 1
```

returns:

```text
Non-zero exit code
```

Linux exit codes:

```text
0     → success
non-0 → failure
```

GitHub Actions treats non-zero exit codes as failed steps.

---

# Workflow Execution Flow

```text
Workflow Starts
       ↓
Checkout Step Executes
       ↓
Build Step Executes
       ↓
Build Fails (exit 1)
       ↓
Success Handler → Skipped
       ↓
Failure Handler → Executes
       ↓
Cancelled Handler → Skipped
       ↓
Always Handler → Executes
       ↓
Workflow Complete
```

---

# Actual Result in This Workflow

Because:

```yaml
exit 1
```

forces failure:

| Step             | Result     |
| ---------------- | ---------- |
| Checkout         | ✅ Executes |
| Run build        | ❌ Fails    |
| Post - Success   | ⏭️ Skipped |
| Post - Failure   | ✅ Executes |
| Post - Cancelled | ⏭️ Skipped |
| Post - Always    | ✅ Executes |

---

# Real DevOps Use Cases

# success()

Used for:

* Production deployment notifications
* Success reporting
* Release publishing

---

# failure()

Used for:

* Slack alerts
* PagerDuty incidents
* Rollback triggers
* Debug log collection

---

# cancelled()

Used for:

* Cleanup interrupted deployments
* Remove temporary resources
* Unlock deployment pipelines

---

# always()

Used for:

* Uploading logs
* Cleaning workspaces
* Sending final notifications
* Archiving reports

---

# Jenkins vs GitHub Actions

# Jenkins

```groovy
post {
   success { }
   failure { }
   always { }
}
```

---

# GitHub Actions

```yaml
if: success()
if: failure()
if: always()
```

Both provide similar post-build behavior.

---

# Why Post Conditions Are Important

Without post-condition handling:

* Failures may go unnoticed
* Cleanup may never happen
* Logs may be lost
* Deployments may remain inconsistent

Post conditions help create:

* Reliable CI/CD pipelines
* Better observability
* Safer deployments
* Automated recovery workflows

---

# Best Practice

Always include:

```yaml
if: always()
```

for:

* Cleanup
* Artifact upload
* Log collection

even when workflow fails.

---

# Benefits of This Workflow Design

* Better failure handling
* Automated cleanup
* Improved debugging
* Reliable notifications
* Safer deployments

---

# Why This Workflow Is Important

This workflow demonstrates advanced CI/CD pipeline control using:

* GitHub Actions
* Conditional execution
* Workflow status functions
* Failure handling
* Cleanup automation

These concepts are widely used in enterprise DevOps automation pipelines.

---

# How to Run

1. Push code to repository

2. Open GitHub Actions tab

3. Observe workflow execution

4. Notice:

   * Build step fails
   * Failure handler executes
   * Always handler executes

5. Review workflow logs

---
