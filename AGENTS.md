# Repository Guidelines

Contributor notes for GameListAI. Keep changes small, tested, and consistent with the current Express/Node layout.

## Project Structure & Module Organization
- Server entry: `index.js` mounts static directories and routes in `src/routes.js`.
- Config and constants live in `src/config.js`; shared helpers in `src/services/`.
- Server-rendered templates are in `src/templates/`.
- Static content folders served directly: `public/` (shared assets), `game/`, `tools/`, `mind/`, `random/`.
- Vercel deploys use the same entry point; keep serverless-friendly code (avoid long-lived state).

## Build, Test, and Development Commands
```bash
npm install     # install dependencies (Node 22.x)
npm start       # run the Express server (also used by vercel dev)
npm run dev     # same as start; use for local iteration
npm run build   # placeholder build step for static assets
npm test        # placeholder; currently echoes status
```
- Health check: `curl http://localhost:3000/health`.
- Pagination/search demo: `http://localhost:3000/?items=50&filter=all&sort=asc`.

## Coding Style & Naming Conventions
- JavaScript uses CommonJS modules, 2-space indentation, and trailing commas avoided in objects.
- Keep functions small and pure; prefer helper utilities in `src/services/`.
- Name static files descriptively (`tools/text-summarizer.html`, `game/puzzle/index.html`).
- Environment values read from `process.env` (see `src/config.js`); avoid hard-coding secrets.

## Testing Guidelines
- No automated suite yet; add lightweight tests before changing routing or pagination.
- For server tests, prefer `supertest` with Node 22.x; name files `*.test.js` under `src/`.
- Manually verify directory listings load and filter/sort behave as expected after changes.

## Commit & Pull Request Guidelines
- Recent history uses short messages; prefer clear, imperative commits (e.g., "Add random listing pagination").
- Squash noisy work-in-progress commits before opening a PR.
- PRs should include: purpose summary, key changes, test evidence (commands/output), and screenshots for UI-impacting assets or templates.
- Link related issues when applicable and call out any config or env variable updates.

## Security & Configuration Tips
- Do not commit API keys; store them in `.env` for local use and Vercel project settings for deploys (`GROQ_API_KEY`, `GEMINI_API_KEY` if needed).
- Keep static uploads non-executable; only serve trusted assets in `game/`, `tools/`, `mind/`, and `random/`.
- Avoid stateful globals to keep serverless deployments predictable.
