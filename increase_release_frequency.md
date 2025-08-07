
# 📈 How We Increase Release Frequency: From 1 in 3 Months to 1 in 2 Weeks Without Loss of Quality

---

## 1. QA Process Improvements

### Shift-Left QA

- QA participated in requirements and design discussions.
- QA participated throughout the software development lifecycle (SDLC).
- Developed and reviewed acceptance criteria before coding began.

### Testcases selection

- We prioritized test cases based on their impact and usage, with a focus on automating high-priority cases. 
- Manual work was focused on high-risk and critical paths.

### Definition of Done for Every New Feature

- Automated tests for high-priority cases written and passed
- Manual exploratory tests completed
- Regression testing done (by auto tests)
- Code reviewed and merged to the release branch

---

## 2. Test Automation Strategy

### Full Test Automation

Strict rule: all high-priority test cases of new features must be autometed

| Type | Running |
|------|----------------|
| **Unit Tests** | High coverage, run on every commit |
| **API Tests** | Automate critical endpoints (Postman) |
| **UI Tests** | Automate at least high-priority scenarios (Selenium, Cucumber, C#) |
| **Smoke Tests** | Automated tests for each deploy |
| **Regression Tests** | Everyday and on-demund runs |

### Test Runs

- Unit, Integration, Smoke and UI (High-Priority) tests for every pre-merge
- UI for everyday and on-demund runs
- Full regression before production releases

---

## 3. CI/CD Pipeline Optimization

### CI/CD Tools

- Used **TeamCity**
- Triggered builds on every pull requests and merges
- Run automated tests for every pull request
- No need for cleaning after test run

### Build Stages and Environments

- Test environment created for every pull request
- Build → Unit Tests → Integration/API → Create Environment and Deploy → Smoke -> UI (High-Priority) → Approval → Merge

- Pre-Prod environment created for every release
- Create Environment and Deploy → UI (High-Priority) → Regress → Approval 


### Parallel Test Execution Used

- Split test suites by components
- Used Selenide test runner

---


## 🔁 4. Release Process Transformation

### Adopt Trunk-Based Development

- Merged small, frequent changes to `main`
- Used feature toggles to deploy incomplete features safely

### Create a Release Checklist

- Automated test suite status
- Manual exploratory test confirmation
- Changelog review
- Rollback plan (Feture toggles, Canary releases)

---

## 5. Team Collaboration

### Communication

- Used release dashboards
- Post status updates in Slack

### Cross-Functional Reviews

- QA, Dev, Product, and DevOps sign off together
- Retrospectives after each release to refine process

---

