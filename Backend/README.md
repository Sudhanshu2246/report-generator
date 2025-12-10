# Backend — Puppeteer / PDF notes

This project uses Puppeteer to generate multi-page PDF reports.

Common deployment issues
- Puppeteer may fail to find a Chrome/Chromium binary in some hosted environments.

Quick fixes
- Install Puppeteer's browser during build:

  ```powershell
  # Run from the Backend folder during build or manually on the server
  npx puppeteer browsers install chrome
  ```

- Or set an environment variable pointing to an installed Chrome/Chromium binary:
  - `PUPPETEER_EXECUTABLE_PATH`
  - `CHROME_PATH`
  - `GOOGLE_CHROME_BIN`

Notes
- The PDF generator includes a fallback that searches common system paths and environment variables and will attempt to launch Puppeteer with an explicit `executablePath` if available.
- On Linux hosts you may need to install system packages for Chromium to run in headless mode. See the Puppeteer docs: https://pptr.dev/guides/environment

Health check
- A lightweight health-route exists at `GET /api/reports/puppeteer-health` (requires authentication) which will attempt to launch and close Puppeteer and return status.

If you want, I can also add a Dockerfile snippet or CI step to run the browser install as part of builds.