# My Role And Contributions

CVocab is a team-built product. I worked as the owner and technical lead, designed the full system architecture, and was the main developer across the core production codebase.

Team members contributed to English/business logic, data processing, design, testing, and implementation work. My responsibility was to keep the product and engineering direction coherent across the mobile app, web apps, backend, data-processing jobs, CI/CD, and performance testing.

Production surfaces:

- Web: [cvocab.app](https://cvocab.app)
- iOS App Store: [CVocab - English vocabulary](https://apps.apple.com/vn/app/cvocab-english-vocabulary/id6760455273)
- Google Play: [CVocab - English vocabulary](https://play.google.com/store/apps/details?id=app.cvocab)

## Role

My main contribution was connecting product ownership with production engineering: defining the system shape, shipping core user-facing and backend features, leading technical decisions, and adding the operational pieces needed to keep the system maintainable after release.

## What I Built

- Flutter mobile app for iOS and Android release.
- NestJS backend API serving mobile, web, and backoffice clients.
- Background worker system for asynchronous operational tasks.
- Next.js public web app with localized content and auth integration.
- Next.js backoffice for internal operations and content/product management.
- Python data-processing automation for preparing, validating, transforming, and importing product data.
- k6 test suite for smoke, load, stress, spike, and endurance coverage.
- CI/CD workflows for the repositories that need build, release, or deployment automation.

## Engineering Impact

- Shipped a real multi-platform product instead of a single demo application.
- Designed clear boundaries between user-facing clients, admin operations, backend APIs, workers, and offline data processing.
- Improved operational reliability by moving slow or failure-prone work into asynchronous queues.
- Improved backend performance with database indexes, Redis caching, async workers, and API/query review.
- Added RBAC authorization for admin and protected backend operations.
- Created internal data-processing workflows outside the latency-sensitive API path.
- Added performance testing around critical flows to catch bottlenecks before they become production issues.
- Added CI/CD gates so builds, tests, and deployment steps are repeatable across repositories.

## Topics I Can Discuss In Depth

- How the backend separates user APIs and admin APIs.
- How RBAC is modeled without coupling authorization to UI-only checks.
- When to use workers instead of synchronous API work.
- How database indexing, caching, and queueing work together to improve API latency.
- How mobile auth, secure storage, push notifications, and purchases are handled in production.
- How data-processing jobs can run without impacting live API traffic.
