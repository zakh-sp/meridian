# Database

Meridian uses [Neon](https://neon.tech) (serverless PostgreSQL) with [Drizzle ORM](https://orm.drizzle.team) for schema management and migrations.

## Branches

| Neon Branch | Purpose | Connected to |
|---|---|---|
| `production` | Live data | `main` git branch |
| `staging` | Pre-release testing | Pull requests |

## Local setup

1. Copy `.env.example` to `.env.local`:
   ```bash
   cp .env.example .env.local
   ```

2. Fill in `DATABASE_URL` with your local or staging connection string from [Neon Console](https://console.neon.tech) → your branch → **Connection Details**.

## Schema

The schema lives in `src/db/schema.ts`. Tables:

| Table | Description |
|---|---|
| `trips` | Core trip records (name, destination, dates) |
| `itinerary_items` | Day-by-day activities per trip |
| `expenses` | Budget tracking entries per trip |
| `packing_items` | Packing list items per trip |

The database client is exported from `src/db/index.ts`:

```ts
import { db } from "@/db";
const trips = await db.query.trips.findMany();
```

## Making schema changes

1. Edit `src/db/schema.ts`
2. Generate a migration file:
   ```bash
   npm run db:generate
   ```
3. Commit the generated file in `drizzle/`
4. Open a PR — the staging migration runs automatically

Migration files are append-only SQL. Never edit an existing one; add a new migration instead.

## CI/CD sync

```
Pull Request opened
  └─ GitHub Actions runs db:migrate against STAGING_DATABASE_URL

PR merged to main
  └─ GitHub Actions runs db:migrate against PRODUCTION_DATABASE_URL
```

### Required GitHub secrets

Go to **Settings → Secrets and variables → Actions** and add:

| Secret | Value |
|---|---|
| `STAGING_DATABASE_URL` | Connection string for the `staging` Neon branch |
| `PRODUCTION_DATABASE_URL` | Connection string for the `production` Neon branch |

## Useful commands

| Command | Description |
|---|---|
| `npm run db:generate` | Generate a migration from schema changes |
| `npm run db:migrate` | Apply pending migrations (uses `DATABASE_URL`) |
| `npm run db:studio` | Open Drizzle Studio in the browser |
| `npm run db:push` | Push schema directly (dev only, skips migration files) |
