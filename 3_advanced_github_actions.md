# Setting Up Self-Hosted Runners (On-Premises) (30 minutes)

Hands-On Exercise:
Set up a self-hosted runner on a local machine or VM.
Configure a GitHub Actions workflow to run on the self-hosted runner.
Discussion on the differences between GitHub-hosted and self-hosted runners.
Troubleshooting common issues.

# Optimizing Workflows with Caching (20 minutes)

Hands-On Exercise:
Implement caching in a workflow to speed up build times.
Example:
```yaml
- name: Cache dependencies
  uses: actions/cache@v2
  with:
      path: node_modules
      key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
      restore-keys: |
        ${{ runner.os }}-node-
```
  Discussion on when and how to use caching effectively. 

# Parallel Jobs and Matrix Builds (20 minutes)

Hands-On Exercise:
Create a workflow that runs tests in parallel using a matrix build.
Example:
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
Discussion on how to use matrix builds for cross-platform or multi-environment testing.

[next >>](./4_own_github_actions.md)