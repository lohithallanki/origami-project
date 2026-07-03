# origami.we — Backend API

Lightweight Express API that powers the login/register screen in `login.html`.

## Setup

```bash
cd server
npm install
cp .env.example .env   # edit JWT_SECRET
npm start               # or: npm run dev (auto-restart)
```

Server runs at `http://localhost:3000`.

## Endpoints

| Method | Route          | Body                              | Notes                          |
|--------|----------------|------------------------------------|---------------------------------|
| POST   | /api/register  | `{ name, email, password }`        | Creates a user, returns token   |
| POST   | /api/login     | `{ email, password }`              | Returns token on success        |
| GET    | /api/me        | — (`Authorization: Bearer <token>`)| Returns the logged-in user      |
| GET    | /api/health    | —                                  | Health check                    |

## Storage

Users are stored in `users.json` (created automatically on first register).
Passwords are hashed with bcrypt — never stored in plain text.
Swap this file-based store for a real database (e.g. MongoDB/Postgres) for production use.

## Security notes for production

- Set a strong, random `JWT_SECRET` in `.env` (never commit `.env`).
- Use HTTPS.
- Replace the JSON file store with a real database.
- Add rate limiting on `/api/login` and `/api/register`.
