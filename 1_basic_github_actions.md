# Introduction to GitHub Actions

Key Concepts: Workflows, Jobs, Steps, Actions.
YAML syntax overview.
Overview of the GitHub Actions marketplace.

# Creating Your First Workflow

Hands-On Exercise:
Create a simple workflow that runs on push to the main branch.

Example:
```yaml
name: First Workflow
on: push
jobs:
    build:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
          uses: actions/checkout@v2
        - name: Run a sample script
          run: echo "Hello, GitHub Actions!"
```
Run the workflow and review the output.
Discussion on the YAML file structure and how to interpret the workflow logs.

[next >>](./2_intermediate_github_actions.md)