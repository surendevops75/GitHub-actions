# --------------------------------------------------------
# INPUT TYPES EXPLAINED
# --------------------------------------------------------
#
# string/default input
# → normal text field
#
# boolean
# → checkbox (true/false)
#
# choice
# → dropdown selection
#
# environment
# → GitHub environments (dev/staging/prod)
#
# required: true
# → user must provide value
#
# default:
# → pre-filled default value
#
# github.event.inputs.<input_name>
# → syntax used to access input values
#
# --------------------------------------------------------
# HOW TO RUN
# --------------------------------------------------------
#
# 1. Go to GitHub Repository
# 2. Open Actions tab
# 3. Select "Inputs Demo"
# 4. Click "Run workflow"
# 5. Fill all input values
# 6. Run workflow
#
# --------------------------------------------------------
# REAL DEVOPS USE CASES
# --------------------------------------------------------
#
# env          → deploy to dev/staging/prod
# deploy       → enable/disable deployment
# log_level    → control application logging
# retry_count  → retry failed deployment steps
# name         → trigger workflow for specific user/team


This GitHub Actions workflow demonstrates how to use manual inputs with workflow_dispatch. 
When a user runs the workflow from the GitHub Actions UI, GitHub displays a form where values can be entered before execution. 
These inputs help make workflows dynamic and reusable instead of hardcoding values inside the YAML file.

The workflow contains multiple input types to show how GitHub Actions handles different user interactions. 
The name input is a simple text field where users can enter any value. 
The env input uses the special environment type, which automatically displays available GitHub environments such as dev, staging, or prod. 
The deploy input is a boolean type that appears as a checkbox and is commonly used to enable or disable deployment execution. 
The log_level input uses the choice type, which creates a dropdown menu with predefined options like info, warn, and error. 
The retry_count input accepts a value that can be used to control retry logic in automation tasks.

Inside the workflow, these input values are accessed using the syntax:

${{ github.event.inputs.<input_name> }}

For example:

${{ github.event.inputs.name }}

This allows the workflow to dynamically use the values entered by the user during runtime.

In real DevOps projects, this feature is extremely useful for creating reusable CI/CD pipelines. 
Teams commonly use workflow inputs to choose deployment environments, control release behavior, enable debugging, select application versions, 
or trigger optional deployment stages. 
Instead of maintaining multiple workflow files for different scenarios, a single workflow can handle multiple use cases based on user-provided inputs.

Overall, workflow_dispatch inputs improve flexibility, automation control, and reusability in GitHub Actions workflows,
making them highly valuable in modern DevOps pipelines using GitHub Actions.