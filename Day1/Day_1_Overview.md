OK, lets go into more detail for Day 1. Include details and commands to getup a github repo, that was can add days 2,3,4 and 5 at a latter date. Be sure to include all code to get it up and running and tested. Include 2 versions, one Linux one Windows.

---


Absolutely, Nick — here is a **fully detailed Day 1 course**, expanded to include:

✔ Full Playwright introduction
✔ Step‑by‑step setup of a **new GitHub repo**
✔ Complete setup of a **Playwright project**
✔ Working sample tests
✔ Separate instructions for **Linux** and **Windows**
✔ Commands you can run *today* so that Days 2–5 can be added later

All written with the perspective of a **DevOps engineer preparing CI/CD foundations**.

***

# ⭐ **Day 1 — Playwright Foundations + GitHub Repository Setup**

### *1 hour | Practical & DevOps oriented*

***

# 🔹 **Part 1 — Playwright Overview (10 minutes)**

### What Playwright Is

Playwright is a Microsoft‑built end‑to‑end testing framework that automates real browsers (Chromium, Firefox, WebKit) with:

*   Auto‑waiting (avoids brittle timing issues)
*   Cross‑browser support
*   Built‑in test runner
*   Traces, videos, screenshots
*   Parallelism out of the box
*   CI‑friendly execution (headless, deterministic)

### Why DevOps Should Care

*   Generates executable artifacts (videos, traces, reports) you store in CI
*   Needs configuration for Linux build agents
*   Plays well in pipeline gates
*   Supports sharding + parallelism
*   Can run inside containers (important for reproducibility)

***

# 🔹 **Part 2 — Environment Setup (20 minutes)**

Below are **two fully‑separated installation paths**.

***

# 🐧 **Linux Setup (Ubuntu, Debian, RHEL‑like)**

## 1. Install Node.js (LTS)

```bash
sudo apt update
sudo apt install -y curl git

curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

Verify:

```bash
node -v
npm -v
```

***

## 2. Create a folder for your work

```bash
mkdir playwright-training
cd playwright-training
```

***

# 🪟 **Windows Setup (PowerShell)**

## 1. Install Node.js

Download LTS from:
<https://nodejs.org/en/download>

Verify:

```powershell
node -v
npm -v
```

## 2. Create workspace folder:

```powershell
mkdir playwright-training
cd playwright-training
```

***

# 🔹 **Part 3 — Create a GitHub Repository (10 minutes)**

You will create a local project → then push it to GitHub.

### 1. Create a new repo on GitHub

*   Go to: <https://github.com/new>
*   **Repository name:** `playwright-training`
*   Choose **Public** or **Private**
*   **Do NOT** add README, `.gitignore`, or license (we’ll do this locally)

### 2. Initialize Git locally

## Linux

```bash
git init
git branch -m main
```

## Windows (PowerShell)

```powershell
git init
git branch -m main
```

***

# 🔹 **Part 4 — Add Playwright to the Project (15 minutes)**

This installs everything, including browsers.

```bash
npm init playwright@latest
```

Choose:

*   ❯ **TypeScript** or **JavaScript** (choose JS if unsure)
*   Add GitHub Actions? → **No** (we will add CI pipelines on Days 3–5)
*   Install browsers? → **Yes**

Project structure created:

    playwright.config.(js|ts)
    tests/
      example.spec.(js|ts)
    package.json

***

# 🔹 **Part 5 — Run Your First Playwright Test (10 minutes)**

```bash
npx playwright test
```

View the report:

```bash
npx playwright show-report
```

View generated artifacts (important for DevOps):

    playwright-report/
    test-results/

***

# 🔹 **Part 6 — Add a Simple Custom Test (Optional Today)**

Create file:

`tests/homepage.spec.js`

```javascript
const { test, expect } = require('@playwright/test');

test('homepage has correct title', async ({ page }) => {
  await page.goto('https://example.com');
  await expect(page).toHaveTitle(/Example/);
});
```

Run it:

```bash
npx playwright test
```

***

# 🔹 **Part 7 — Commit and Push to GitHub (10 minutes)**

## 1. Create `.gitignore`

Playwright will generate long trace/video files, so ignore them:

`.gitignore`

    node_modules/
    test-results/
    playwright-report/

***

## 2. Commit Code

### Linux

```bash
git add .
git commit -m "Day 1: Initial Playwright setup"
```

### Windows

```powershell
git add .
git commit -m "Day 1: Initial Playwright setup"
```

***

## 3. Connect to GitHub Repo

Replace `<YOUR-USERNAME>`:

```bash
git remote add origin https://github.com/<YOUR-USERNAME>/playwright-training.git
git push -u origin main
```

***

# 🎉 **Day 1 Completed — What You Now Have**

### You now have:

✔ A GitHub repo prepared for the rest of the week
✔ A working Playwright project
✔ Browsers installed
✔ A working sample test
✔ Playwright HTML reporting
✔ Git versioning + push to GitHub

This gives a clean foundation so when we hit **Day 2** we can add:

*   Page objects
*   Locators
*   Assertions
*   Trace recording
*   Debugging test failures

And on **Day 3** we introduce:

*   Azure DevOps pipelines
*   Linux pipeline agents
*   Artifacts
*   Browser dependencies
*   Running tests in CI

***

# Want me to generate **Day 2** with the same level of detail?

Or do you want me to create:

✅ A full Azure DevOps pipeline YAML (for Linux CI)
✅ A Windows self‑hosted agent Playwright pipeline
✅ A Dockerfile for consistent local & CI environments

Just tell me — I can generate any of them.
