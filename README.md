[![Playwright Tests](https://github.com/DonyMagRony/test-automatization/actions/workflows/playwright.yml/badge.svg?branch=main)](https://github.com/DonyMagRony/test-automatization/actions/workflows/playwright.yml)


## CI

[![Playwright Tests](https://github.com/DonyMagRony/test-automatization/actions/workflows/playwright.yml/badge.svg?branch=main)](https://github.com/DonyMagRony/test-automatization/actions/workflows/playwright.yml)

**CI system:** GitHub Actions. It is integrated with GitHub, supports parallel test execution through matrix jobs, and provides artifact storage.

**Pipeline** (`.github/workflows/playwright.yml`):
- Runs on every push and pull request.
- Installs dependencies using `npm ci` with npm caching.
- Installs Chromium for Playwright.
- Runs the complete Playwright test suite split into 4 parallel shards.
- The `merge-reports` job combines blob reports into HTML and JUnit reports.
- Artifacts include HTML reports, traces, screenshots, videos and JUnit results. Reports are retained for 14 days.

**CI settings** (`playwright.config.ts`, when `CI=true`):
- `forbidOnly: true`
- `retries: 2`
- Reporters: `list`, `blob`, `junit`
- `trace: 'on-first-retry'`

### Runtime comparison

| Configuration | Total run time | Run tests step (slowest shard) | Run |
|---|---|---|---|
| 1 shard | 1m 20s| 1m  | [run](https://github.com/DonyMagRony/test-automatization/actions/runs/45279032512/job/138058289503) |
| 4 shards + merge | To be measured | To be measured | [run](LINK) |

**Conclusion:** To be completed after measuring both configurations.

### Running locally

```bash
npm ci
npx playwright install chromium
npx playwright test
```