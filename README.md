# Tour Platform

An [Nx](https://nx.dev) monorepo for the Tour Platform — a tour browsing/booking product made up of a public web app, an admin dashboard, and a backing API gateway.

## Apps

| App | Path | Stack | Purpose |
| --- | --- | --- | --- |
| `api-gateway` | `apps/api-gateway` | NestJS | Backend API gateway |
| `app-user` | `apps/app-user` | Next.js | Customer-facing web app |
| `app-dashboard` | `apps/app-dashboard` | React + Vite | Internal/admin dashboard |

Each app has a matching `*-e2e` project (e.g. `app-user-e2e`) with [Playwright](https://playwright.dev) end-to-end tests.

## Prerequisites

- Node.js 20+
- npm

## Getting started

```sh
npm install
```

Run an app in development mode:

```sh
npx nx dev app-user        # Next.js dev server
npx nx dev app-dashboard    # Vite dev server
npx nx serve api-gateway    # NestJS API
```

## Common tasks

Run a target for a single project:

```sh
npx nx <target> <project-name>
# e.g. npx nx build app-user
# e.g. npx nx test api-gateway
```

Run a target across every project, or only what's affected by your changes:

```sh
npx nx run-many -t build
npx nx affected -t test lint
```

Available targets per project (build, dev/serve, test, lint, e2e) are either inferred from each app's tooling config (Next.js, Vite, Webpack, Jest, Playwright, ESLint) or defined in its `package.json`. Run `npx nx show project <name>` to see exactly what's available.

Explore how the projects relate to one another:

```sh
npx nx graph
```

## Project structure

```
apps/
  api-gateway/        NestJS API gateway
  api-gateway-e2e/
  app-user/            Next.js customer app
  app-user-e2e/
  app-dashboard/       React + Vite admin dashboard
  app-dashboard-e2e/
packages/              Shared libraries (none yet)
```

## Keeping TypeScript project references in sync

Nx keeps TypeScript [project references](https://www.typescriptlang.org/docs/handbook/project-references.html) in `tsconfig.json` files up to date based on each project's dependencies. This runs automatically for tasks like `build`/`typecheck`, or manually via:

```sh
npx nx sync
```

To verify references are correct in CI without modifying files:

```sh
npx nx sync:check
```

## Useful links

- [Nx documentation](https://nx.dev)
- [Running tasks](https://nx.dev/features/run-tasks)
- [Nx and CI](https://nx.dev/ci/intro/ci-with-nx)

## License

MIT
