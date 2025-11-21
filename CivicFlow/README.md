# CivicFlow: Government Lending CRM

CivicFlow streamlines micro-business grant and loan workflows for government agencies and lending partners. It packages intake, rules, case management, and reporting into one place so teams can move quickly without juggling spreadsheets.

## Quick start (Docker)
1. Copy the Docker environment file: `cp .env.docker .env`
2. Bring up the stack: `docker-compose up -d`
3. Run migrations and seed data:
   ```bash
   docker-compose exec api npm run migrate
   docker-compose exec api npm run seed
   ```

Detailed options live in [docs/DOCKER.md](docs/DOCKER.md).

## Local development
1. Install dependencies: `npm install`
2. Copy the sample env: `cp .env.example .env`
3. Update `.env` with your database and Redis settings
4. Apply migrations and seeds:
   ```bash
   npm run migrate up
   npm run seed all
   ```
5. Start the app with hot reload: `npm run dev`

## Common scripts
- `npm run migrate up` — apply pending migrations
- `npm run migrate status` — check migration state
- `npm run migrate rollback` — undo the last migration (use carefully)
- `npm run seed all` — load sample and rule data
- `npm run seed rules` — load program rules only
- `npm run seed test` — load test fixtures for development
- `npm run build` — compile for production
- `npm start` — launch the compiled server

## Project layout
```
src/
├── config/       # App, database, and Redis configuration
├── database/     # Migrations, seeds, and schema docs
├── middleware/   # Express middleware
├── routes/       # API routes (health checks, etc.)
├── scripts/      # Migration and seed runners
├── utils/        # Shared utilities
├── app.ts        # Express app wiring
└── index.ts      # Server entry point
```

## Environment variables
Review `.env.example` for the full set of configuration keys used across the app.

## Deployment
- **Docker Compose:** `make up` for production defaults, `make up-dev` for a hot-reload stack. Use `make logs-*`, `make migrate`, and `make seed` for maintenance.
- **Kubernetes:** from the `k8s/` directory run `./deploy.sh` (Linux/Mac) or `./deploy.ps1` (Windows), or apply manifests with `kubectl apply -k k8s/`.

## Health endpoints
- `GET /api/v1/health` — service heartbeat
- `GET /api/v1/ready` — readiness probe

