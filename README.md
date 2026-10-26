# Planora AI

A personal year-at-a-glance planner with private accounts, a 12-month planning board, a regular calendar, and an activity history.

## Run locally

1. Install Node.js 20 or newer.
2. Run `npm install`.
3. Copy `.env.example` to `.env` and add your AI provider API key to enable the planning assistant.
4. Run `npm run dev`.
5. Open the Vite URL shown in the terminal (usually `http://localhost:5173`).

The Vite development server forwards `/api` requests to the Express API on port 3001. The API creates `planora.db` in the project root on its first start; set `DATABASE_PATH` if you want to store it elsewhere. The planning assistant supports OpenAI-compatible chat completions APIs. Set `PLANORA_AI_API_KEY`, and optionally set `PLANORA_AI_BASE_URL` and `PLANORA_AI_MODEL`, in your local `.env` file. The API key stays on the server. Without a key, the rest of the planner works normally and the assistant explains how to configure it. Your conversation and the selected month's saved note are sent to the configured AI provider when you ask for suggestions. Set `PORT` to change the API port; update the Vite proxy in `vite.config.js` to match.

## Production

Run `npm run build`, then start the API with `npm start` and `NODE_ENV=production`. The API serves the built frontend from `dist`. The SQLite database and its journal files are local application data and are excluded from version control.

## Included

- Email and password registration and sign-in, with bcrypt password hashes and expiring server-side sessions.
- A personal 12-month board with notes, image uploads, and a freehand doodle canvas.
- A navigable calendar, recent account and planning activity, theme settings, and sign-out.
- An AI planning companion that suggests achievable month-by-month steps and lets you save its suggestions to your plan.
- SQLite persistence for accounts, sessions, month plans, and activity.

## Configuration and current scope

The only external service configured by this project is an optional OpenAI-compatible chat completions API. Set `PLANORA_AI_API_KEY` in `.env` to enable it; `PLANORA_AI_BASE_URL` and `PLANORA_AI_MODEL` are optional. Keep real credentials in `.env`, which is ignored by Git, and use `.env.example` as the placeholder template.

The current application uses local SQLite storage and its own email/password accounts. Supabase and Google Calendar OAuth are not configured or implemented in this version. Google Calendar features therefore require future implementation and credentials before they can be used.

## Checks

Run `npm run build` to create the production frontend bundle. This project does not currently define lint, typecheck, or test scripts in `package.json`.
