Absolutely, Nick — here is a **fully expanded, deeply detailed Day 2**, written specifically for a **DevOps engineer supporting developers who will use Playwright**.  
This includes: authoring basics (so you can debug failures), configuration, environment handling, and what matters from a DevOps reliability/support perspective.

***

# ⭐ **Day 2 — Writing & Running Playwright Tests (1 Hour Deep Dive for DevOps Engineers)**

### 🎯 **Goal:**

By the end of this session, you’ll understand how Playwright tests are written, how they behave, how locators & assertions work, how config impacts CI, and how to use tools like the Inspector and Trace Viewer to debug CI failures.  
You’ll also gain the technical depth needed to support engineers when their tests fail in pipelines.

***

# ✅ **Day 2 Agenda (1 Hour Total)**

| Time      | Topic                                                         |
| --------- | ------------------------------------------------------------- |
| 0–10 min  | Core Playwright test structure & test runner                  |
| 10–25 min | Locators, assertions, and auto-waiting                        |
| 25–40 min | Config files, retries, workers, and environments              |
| 40–50 min | Page Object Model (POM) basics                                |
| 50–60 min | Debugging tools: Inspector, trace viewer, videos, screenshots |

***

# 🧩 **1. Playwright Test Structure (10 minutes)**

### Playwright Test Runner (most teams use this)

The built‑in test runner provides:

*   Parallel execution
*   Built-in retries
*   HTML/Trace/Video reporting
*   Configuration per project (browser, device, env)
*   Test isolation via contexts

### Basic test example

```ts
import { test, expect } from '@playwright/test';

test('homepage has title', async ({ page }) => {
  await page.goto('https://example.com');
  await expect(page).toHaveTitle(/Example/);
});
```

### Test Anatomy

*   **test()** — defines a test
*   **page fixture** — Playwright provides a fresh browser page per test
*   **expect()** — assertion library with auto‑wait
*   **async / await** — required for all interactions

***

# 🔍 **2. Locators, Assertions & Auto‑Wait (15 minutes)**

Playwright uses **locator-based targeting**.  
Unlike Selenium, Playwright does *auto-retries* for elements until they’re ready.

### Locators

```ts
const loginBtn = page.getByRole('button', { name: 'Login' });
await loginBtn.click();
```

Common types:

*   `getByRole()`
*   `getByText()`
*   `getByTestId()`
*   CSS locators

### Assertions (auto‑wait)

```ts
await expect(page.getByText('Welcome')).toBeVisible();
await expect(page).toHaveURL(/dashboard/);
await expect(page.locator('#price')).not.toHaveText('$0.00');
```

Assertions automatically retry until:

*   The condition passes
*   The timeout expires

### DevOps relevance:

When flakes happen in CI:

*   Check if tests rely on timing
*   Ask devs to replace hard waits with locators
*   Encouraged: **role-based locators** over brittle CSS

***

# ⚙️ **3. Configuration: retries, workers, browsers, env vars (15 minutes)**

Playwright uses `playwright.config.ts`.

### Key Settings (CI Focus)

```ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 4 : 1,
  use: {
    headless: true,
    trace: 'retain-on-failure',
    screenshot: 'only-on-failure'
  }
});
```

### Why this matters to DevOps

| Setting    | Why it matters in CI                   |
| ---------- | -------------------------------------- |
| `retries`  | Helps reduce flaky failures            |
| `workers`  | Controls parallelism → CPU/mem usage   |
| `timeout`  | Misconfigured timeout = stalled agents |
| `reporter` | Generates CI‑viewable HTML reports     |
| `trace`    | Essential for debugging failures       |

### Handling environment variables

(Test URLs, credentials, flags)

Example:

```ts
const baseUrl = process.env.BASE_URL;
await page.goto(baseUrl);
```

Recommend using:

*   Azure DevOps variable groups
*   Key Vault secrets in CI

***

# 🏗️ **4. Intro to Page Object Model (10 minutes)**

POM helps structure tests:

### Example: LoginPage.ts

```ts
export class LoginPage {
  constructor(private page) {}

  username = this.page.getByTestId('username-input');
  password = this.page.getByTestId('password-input');
  loginBtn = this.page.getByRole('button', { name: 'Login' });

  async login(user, pass) {
    await this.username.fill(user);
    await this.password.fill(pass);
    await this.loginBtn.click();
  }
}
```

### Usage:

```ts
test('user can log in', async ({ page }) => {
  const login = new LoginPage(page);
  await login.login('admin', 'pass');
});
```

### DevOps relevance:

*   POM improves maintainability → fewer pipeline failures
*   Common cause of flakes: brittle locators → POM improves stability
*   Cleaner test logs for debugging

***

# 🐛 **5. Debugging Tools: Inspector, Trace Viewer, Videos (10 minutes)**

### Inspector (interactive stepping through test)

```bash
npx playwright test --debug
```

Why DevOps cares:

*   Useful for reproducing CI failures locally
*   Shows exact locator queries & page state

***

### Trace Viewer

Generate traces:

```bash
npx playwright test --trace on
npx playwright show-trace trace.zip
```

A trace contains:

*   DOM snapshots
*   Network requests
*   Console logs
*   Step-by-step timeline

DevOps impact:

*   Makes CI failures *actionable*
*   Great for distributed teams
*   Eliminates "can't reproduce locally" issues

***

### Screenshots & Video

Config:

```ts
use: {
  screenshot: 'only-on-failure',
  video: 'retain-on-failure'
}
```

These become pipeline artifacts.

DevOps benefits:

*   Videos expose UI timing issues
*   Screenshots show final UI state
*   Helps root cause flakiness quickly

***

# 🧪 **Hands‑On Exercises (Optional but useful)**

## 1. Write a navigation test

```ts
test('navigate to pricing', async ({ page }) => {
  await page.goto('https://playwright.dev');
  await page.getByRole('link', { name: 'Docs' }).click();
  await expect(page).toHaveURL(/docs/);
});
```

## 2. Generate a trace and inspect it

```bash
npx playwright test --trace on
npx playwright show-trace
```

## 3. Change config to simulate CI flakiness

Increase parallel workers and observe runtime behavior.

***

# 🎯 **Day 2 Outcomes**

By the end of Day 2, you’ll confidently understand:

### ✅ How tests are structured

### ✅ How selectors, assertions, and auto‑waiting work

### ✅ How to debug failing tests using trace, video, screenshots

### ✅ How config impacts developer experience AND CI stability

### ✅ How to read/triage Playwright test failures

### ✅ What causes flaky tests and how to advise developers

***

If you want, I can also produce:

🔧 **Day 3 “Playwright in CI” expanded version**  
📘 **A DevOps Debugging Guide for Playwright Failures**  
📂 **A complete Azure DevOps ready-to-use pipeline template**  
🏗️ **A Playwright Dockerfile for Linux agents**

Just tell me what you'd like next.
