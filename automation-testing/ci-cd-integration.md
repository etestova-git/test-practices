# CI/CD Integration with GitHub Actions

---

## 🛠️ Creating a Workflow File
Create a new file at `.github/workflows/ci-cd.yml` with the following example:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Node.js / Python / etc.
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test

    - name: Build project
      run: npm run build

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Deploy (Example - use rsync, FTP, or deployment scripts)
      run: echo "Deploying..."
```

---

## 🔐 Secrets & Environment Variables
Store sensitive credentials (e.g., API keys, SSH private keys) securely using **GitHub Secrets**:
- Navigate to `Settings > Secrets and variables > Actions`
- Add your secrets (e.g., `PRODUCTION_API_KEY`, `SSH_PRIVATE_KEY`)
- Access them in the workflow with `${{ secrets.YOUR_SECRET_NAME }}`

---

## 💡 Best Practices
- Use separate jobs for **build**, **test**, and **deploy** stages.
- Set up branch protection rules to enforce CI checks before merge.
- Use caching (`actions/cache`) to speed up workflows.
- Name your workflows clearly and keep them under version control.

---

## 📚 Resources
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Starter Workflows](https://github.com/actions/starter-workflows)
- [Security Best Practices](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)

---
