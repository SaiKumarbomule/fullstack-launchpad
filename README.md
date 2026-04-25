# fullstack-launchpad

> A production-ready full-stack starter kit — React + Node.js + PostgreSQL + Docker + CI/CD. Clone it, configure it, ship it.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Stars](https://img.shields.io/github/stars/SaiKumarbomule/fullstack-launchpad?style=social)](https://github.com/SaiKumarbomule/fullstack-launchpad)

---

## The problem

Every time you start a new project, you spend the first 2–3 days wiring up the same things: auth, database, Docker, environment configs, CI/CD, error handling, logging. None of it is interesting. All of it is necessary.

**fullstack-launchpad** is everything that should already exist before you write your first line of real business logic.

---

## What's included

### Frontend
- React 18 + TypeScript
- Tailwind CSS for styling
- React Router v6 for navigation
- Axios for API calls with interceptors
- Protected routes + auth context built in

### Backend
- Node.js + Express + TypeScript
- JWT authentication (register, login, refresh tokens)
- PostgreSQL with Prisma ORM
- Input validation with Zod
- Centralized error handling middleware
- Request logging with Morgan

### Infrastructure
- Docker + Docker Compose (one command to run everything)
- GitHub Actions CI/CD pipeline (lint → test → build → deploy)
- Environment-based config (dev / staging / production)
- Health check endpoints

### Developer experience
- ESLint + Prettier configured
- Husky pre-commit hooks
- Separate dev / prod Docker configs
- Hot reload in development

---

## Quick start

```bash
# 1. Clone the repo
git clone https://github.com/SaiKumarbomule/fullstack-launchpad.git
cd fullstack-launchpad

# 2. Copy environment files
cp .env.example .env

# 3. Start everything with Docker
docker-compose up --build

# Frontend → http://localhost:3000
# Backend  → http://localhost:4000
# Database → localhost:5432
```

That's it. You have a running full-stack app.

---

## Project structure

```
fullstack-launchpad/
├── client/                  # React frontend
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   ├── pages/           # Route-level page components
│   │   ├── hooks/           # Custom React hooks
│   │   ├── context/         # Auth context, global state
│   │   ├── api/             # Axios instances + API calls
│   │   └── types/           # TypeScript interfaces
│   └── Dockerfile
│
├── server/                  # Node.js backend
│   ├── src/
│   │   ├── routes/          # Express route handlers
│   │   ├── controllers/     # Business logic
│   │   ├── middleware/       # Auth, error handling, logging
│   │   ├── services/        # Database + external service calls
│   │   ├── prisma/          # Schema + migrations
│   │   └── utils/           # Helpers, validators
│   └── Dockerfile
│
├── .github/
│   └── workflows/
│       └── ci.yml           # GitHub Actions pipeline
│
├── docker-compose.yml
├── docker-compose.prod.yml
└── .env.example
```

---

## Architecture decisions

### Why Prisma over raw SQL?
Prisma gives you type-safe database queries, automatic migrations, and a clean schema definition — without the overhead of a heavy ORM like Sequelize. For a starter kit, the developer experience win is worth it.

### Why JWT with refresh tokens?
Short-lived access tokens (15 min) + long-lived refresh tokens (7 days) stored in httpOnly cookies. This balances security with usability — better than storing JWTs in localStorage.

### Why Docker Compose for local dev?
Eliminates the "works on my machine" problem completely. New developers clone, run one command, and have the exact same environment as production.

### Why Zod for validation?
Zod validates at runtime AND generates TypeScript types — so your API contracts are always in sync with your types. No more writing the same shape twice.

---

## API reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Create a new account |
| POST | `/api/auth/login` | Login and get tokens |
| POST | `/api/auth/refresh` | Refresh access token |
| POST | `/api/auth/logout` | Clear tokens |
| GET | `/api/users/me` | Get current user (protected) |
| GET | `/api/health` | Health check |

---

## CI/CD pipeline

The included GitHub Actions workflow runs on every push and pull request:

```
Push / PR
    │
    ├── Lint (ESLint + Prettier check)
    ├── Type check (tsc --noEmit)
    ├── Unit tests (Jest)
    ├── Build Docker images
    └── Deploy to staging (on merge to main)
```

---

## Environment variables

```env
# Server
NODE_ENV=development
PORT=4000
DATABASE_URL=postgresql://user:password@db:5432/launchpad
JWT_ACCESS_SECRET=your-access-secret
JWT_REFRESH_SECRET=your-refresh-secret
JWT_ACCESS_EXPIRY=15m
JWT_REFRESH_EXPIRY=7d

# Client
VITE_API_URL=http://localhost:4000
```

---

## Roadmap

- [ ] Email verification flow
- [ ] OAuth (Google, GitHub) via Passport.js
- [ ] Role-based access control (RBAC)
- [ ] File upload with S3
- [ ] WebSocket support
- [ ] Redis caching layer
- [ ] Kubernetes deployment manifests
- [ ] Terraform AWS infrastructure

---

## Contributing

Contributions are very welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a pull request.

1. Fork the repo
2. Create your branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a pull request

---

## Author

**Sai Kumar Jee** — Full-Stack Software Architect, Dallas TX

- GitHub: [@SaiKumarbomule](https://github.com/SaiKumarbomule)
- LinkedIn: [linkedin.com/in/saikumarjee](https://linkedin.com/in/saikumarjee)

If this project saved you time, consider giving it a star. It helps others find it.

---

## License

MIT © [Sai Kumar Jee](LICENSE)
