# Security And Privacy

This case study is written from production work, but it is not a source release. The public repo shows architecture, screenshots, and engineering decisions while keeping sensitive implementation details in the private repositories.

## Kept Private

- Production source code.
- Environment variables, API keys, signing keys, certificates, service accounts, and webhook secrets.
- Deployment hosts, internal routes, queue payloads, and provider credentials.
- Raw datasets, database dumps, raw logs, and user/payment/order data.
- Full database schema, proprietary business rules, and detailed role/permission matrices.

## Shared Publicly

- High-level architecture diagrams.
- Product screenshots.
- Summaries of technical decisions and trade-offs.
- Careful descriptions of CI/CD, performance testing, RBAC, caching, indexes, and worker-based async processing.

The goal is to make the engineering work reviewable without turning a live private product into an open-source release.
