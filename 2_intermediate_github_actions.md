# Exploring Pre-built Actions (20 minutes)

Hands-On Exercise:
Use pre-built actions from the GitHub Marketplace (e.g., setting up Node.js, running tests).
Example:
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
Discussion on the flexibility of using community actions.

# Workflow Triggers and Contexts (20 minutes)

Hands-On Exercise:
Explore different triggers (push, pull_request, schedule, etc.).
Use contexts and expressions to add conditional logic to workflows.
Example: Conditionally run jobs only on certain branches.

# Using Secrets in Workflows (20 minutes)

Hands-On Exercise:
Store sensitive data using GitHub Secrets.
Create a workflow that uses a secret for deployment.
Example:
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
      run: ./deploy.sh
      env:
        API_TOKEN: ${{ secrets.API_TOKEN }}
```
Discussion on security best practices.

[next >>](./3_advanced_github_actions.md)