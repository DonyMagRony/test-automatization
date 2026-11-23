Help me build a CI pipeline for a Playwright (TypeScript) project on GitHub Actions. Reply concisely, give ready-to-run PowerShell (Windows) commands step by step, and always say which folder to run them from.

ASSIGNMENT ("SIS 2")
Add to my repository:
1. .github/workflows/playwright.yml
   - triggers: on push and on pull_request, no branch filters (plus workflow_dispatch)
   - setup-node with cache: npm, npm ci, npx playwright install --with-deps chromium
   - full test run, no --grep / --project filters
   - 4-shard matrix (--shard=i/4, fail-fast: false) + a separate merge-reports job that merges blob reports into one HTML report and one JUnit file
   - artifacts: playwright-report, test-results-1..4 (traces), junit-report; retention-days: 14
2. playwright.config.ts: when process.env.CI is set -> forbidOnly: true, retries: 2, reporters list + blob + junit, trace: 'on-first-retry'. Plus merge.config.ts.
3. README with a CI section: status badge for main, which CI system and why, before/after timing table (1 shard vs 4 shards, from GitHub Actions runs, median of 2-3 workflow_dispatch runs, with links) and a one-sentence conclusion, local run instructions.
4. If AI was used: a .md file with model, prompts and explanation.

Submission checklist: separate runs for a push to a feature branch and for a PR; npm cache restored in the second run's setup-node log; browser install + unfiltered test step visible in the log; playwright-report and test-results-1..4 artifacts, a trace opens on trace.playwright.dev; run graph shows 4 parallel shards + Merge reports; timing table in README; badge shows main status (after PR merge).

MY PROJECT
Repo: https://github.com/DonyMagRony/test-automatization (public). Playwright project is in the subfolder qa-playwright-ts/ (tests against https://practicesoftwaretesting.com, page objects + fixtures). Workflow lives in the repo root .github/workflows/. Test user password comes from process.env.TEST_PASSWORD (.env locally via dotenv, GitHub Actions secret on CI).

CURRENT PROBLEM
On GitHub, tests that need a logged-in/registered user fail even after retries (login: getByTestId('page-title') not found on /account; register: getByTestId('login-submit') not found after redirect to /auth/login; buy-product: order confirmation not visible). Other shards pass. Locally all 9 tests pass. Suspects: missing TEST_PASSWORD secret (user-factory falls back to an empty string), or the demo site slowing/blocking GitHub runners. Cause not confirmed yet.

CONSTRAINTS
- Use ubuntu-latest runners (no self-hosted Windows runner), otherwise shards won't run in parallel.
- Never commit secrets, .env, node_modules or runner credentials.
- GitHub pages can't be fetched by you, so I'll paste files, logs and screenshots as text/images.

Start by asking me for what you need to diagnose the failures (failure screenshot or error-context.md, src/api/users-api.ts, src/fixtures.ts), then guide me through: fixing the failures, timing measurements, README table, and the submission checklist.

please provide step by step instructions
result
<img width="1155" height="662" alt="изображение" src="https://github.com/user-attachments/assets/7534d3ca-104b-41cc-8ae3-187a48637614" />

