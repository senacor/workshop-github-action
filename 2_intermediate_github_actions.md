# Next level

## Pre-build actions

Pre-built actions from the GitHub Marketplace (e.g., setting up Node.js, running tests) provide flexibility and simple workflows.
The actions provide additional commands or functionality within your job. Such as the Setup Node.js Action provide a working node environment

Usage:
```yaml
name: Node.js CI
on: [push]
jobs:
    build:
      runs-on: ubuntu-latest
      steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
```

## Using docker images as base

Usage:
```yaml
name: Node.js CI
on: [push]
jobs:
  docker-base:
      runs-on: ubuntu-latest
      container: node:hydrogen-alpine
      steps:
        - uses: actions/checkout@v4
        - name: Install dependencies
          run: npm install
        - name: Run tests
          run: npm test
```

The defined container image is used as base for the following steps within the jobs. 

## Parallel Jobs and Matrix Builds

Steps within a Job are running sequentially. Multiple jobs run in parallel as long no dependencies between jobs are defined.

You want to test your application against multiple node version, this is used in libraries. 
You can use matrix build, defining multiple node version and referencing in the job, spawns for every defined version a job.
Example: https://github.com/senacor/azure-function-middleware/blob/master/.github/workflows/ci.yml#L13

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [10, 12, 14]
    steps:
    - uses: actions/checkout@v2
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm install
    - run: npm test
```

## Using Secrets in Workflows

As every other build system secrets are used to install apps in a cloud or kubernetes environment.

```yaml
name: Deploy to Production
on: push
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    - name: Deploy
      run: ./deploy/deploy.sh
      env:
        API_TOKEN: ${{ secrets.API_TOKEN }}
```

[next >>](./3_advanced_github_actions.md)