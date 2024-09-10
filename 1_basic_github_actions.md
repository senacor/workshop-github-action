# Introduction to GitHub Actions

# How to ?

* Create a yaml file unter ``.github/workflows``
* Every file needs the following information:
** name -> name of the workflow
** on -> trigger for the workflow
** jobs -> list of jobs to execute

```yaml
name: First Workflow
on: push
jobs:
    build:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
          uses: actions/checkout@v4
        - name: Run a sample script
          run: echo "Hello, GitHub Actions!"
```

## Details: Trigger

* Trigger are different GIT or Github Events
* Git Events (https://docs.github.com/de/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows):
** push: [BRANCH oder TAG] -> Run on a ``git push``
* Github Events (example):
** pull_request -> Run on every push within a pull request
** issue_comment -> Run on comment within a pull request or issue

# Exercise: Your First Workflow

Hands-On Exercise: `Create a simple workflow that runs on push to the main branch.`

* Create a new branch within this repository (with your name or codename)
* Create a workflow file
* Run the workflow file

[next >>](./2_intermediate_github_actions.md)