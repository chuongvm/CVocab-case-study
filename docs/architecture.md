# System Architecture

CVocab is split into separate client apps, a NestJS backend, background workers, data-processing jobs, and a dedicated performance test suite. The split keeps user-facing product work, admin operations, and offline processing from stepping on each other.

## Components

| Component                   | Responsibility                                                                                                             |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Flutter mobile app          | Primary iOS/Android learning experience, authentication, local state, audio/speech, push notifications, subscription flows |
| Next.js web app             | Public and authenticated web experience, localized content, auth integration                                               |
| Next.js backoffice          | Admin workflows for operating content, users, products, versions, queues, promotions, and support tasks                    |
| NestJS API                  | User/admin REST APIs, auth, validation, localization, queue orchestration, database access                                 |
| PostgreSQL                  | Primary relational store                                                                                                   |
| Redis + BullMQ              | Cache layer and asynchronous job queue                                                                                     |
| Workers                     | Email, image processing, notification, webhook, scheduler, review computation, account deletion, and operational jobs      |
| Python data-processing jobs | Internal data preparation, validation, transformation, and import/export workflows                                         |
| k6 test suite               | Smoke/load/stress/spike/endurance testing for critical backend flows                                                       |
| CI/CD pipelines             | Automated build, test, and deployment workflows for the repositories that need release automation                           |

## Container View

See [container-architecture.mmd](../diagrams/container-architecture.mmd).

```mermaid
flowchart LR
  subgraph Clients
    Mobile["Flutter mobile app"]
    Web["Next.js web"]
    BO["Next.js backoffice"]
  end

  subgraph Backend
    API["NestJS API"]
    Workers["BullMQ workers"]
  end

  subgraph Data
    DB[("PostgreSQL")]
    Redis[("Redis")]
    Pipeline["Python data-processing jobs"]
  end

  subgraph Quality
    K6["k6 performance tests"]
    CICD["CI/CD pipelines"]
  end

  Mobile --> API
  Web --> API
  BO --> API
  API <--> DB
  API <--> Redis
  API --> Redis
  Redis --> Workers
  Workers --> DB
  Pipeline --> DB
  CICD --> API
  CICD --> Web
  CICD --> BO
  K6 --> API
```

## Request Lifecycle

See [request-lifecycle.mmd](../diagrams/request-lifecycle.mmd).

```mermaid
sequenceDiagram
  autonumber
  actor Learner
  participant App as Mobile/Web client
  participant API as NestJS API
  participant Cache as Redis cache
  participant DB as PostgreSQL
  participant Queue as BullMQ queue
  participant Worker as Background worker

  Learner->>App: Starts a product action
  App->>API: Authenticated request
  API->>API: Validate, authorize, resolve locale
  API->>Cache: Read cached metadata
  API->>DB: Read/write product data
  API->>Queue: Enqueue async side effects
  API-->>App: Return response
  Queue-->>Worker: Process job later
  Worker->>DB: Persist job result
```

## Release And Quality Gates

See [release-overview.mmd](../diagrams/release-overview.mmd).

```mermaid
flowchart LR
  Code["Private repos"] --> Checks["Lint, type checks, tests"]
  Checks --> Smoke["Smoke / integration checks"]
  Smoke --> Perf["k6 checks for backend flows"]
  Perf --> Review["Manual release review"]
  Review --> Prod["Production surfaces<br/>mobile stores, web, API, BO, data jobs"]
```

## CI/CD

See [ci-cd-overview.mmd](../diagrams/ci-cd-overview.mmd).

All release-critical repositories have CI/CD automation. Each pipeline is shaped around the same idea: run repeatable checks close to the codebase, build the deployable artifact, then verify the release path before production traffic depends on it.

```mermaid
flowchart LR
  Commit["Private repo commit"] --> Checks["Install, lint, type check, test"]
  Checks --> Build["Build artifact"]
  Build --> Deploy["Deploy or prepare release"]
  Deploy --> Verify["Smoke checks / manual verification"]
  Verify --> Monitor["Observe production signals"]
```

## Key Design Decisions

- Separate mobile/web/backoffice clients so user-facing product work and internal operations can evolve independently.
- Keep the backend as the contract boundary for authentication, validation, localization, user data, purchases, and review workflows.
- Move slow or unreliable work into queues and workers, especially email, notification, image processing, scheduled jobs, webhook handling, and review computations.
- Keep internal data processing outside the API runtime so operational jobs do not compete with user traffic.
- Maintain a dedicated k6 repository so performance tests can be run independently from feature development.
- Use CI/CD quality gates so common checks run consistently before release or deployment.
