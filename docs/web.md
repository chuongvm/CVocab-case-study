# Public Web App

The public web app is the browser-facing experience for CVocab. It supports localized pages, authentication, public content, and authenticated user surfaces.

## Stack

- Next.js and React.
- TypeScript.
- NextAuth integration.
- next-intl for localization.
- MDX content support.
- Tailwind CSS.
- SWR for client data fetching.

## Responsibilities

- Public product/content pages.
- Authenticated user web experience.
- Locale-aware routing and content.
- API integration with the NestJS backend.
- Shared layout, UI components, providers, and auth components.

## Screenshots

These screenshots show the browser learning experience and parity with the mobile product surface.

| Learning topics                                                                                | Flashcard learning                                                                                   |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| <img src="../screenshots/web-frontend/learn-topics.png" alt="Web learning topics" width="420"> | <img src="../screenshots/web-frontend/learn-flashcard.png" alt="Web flashcard learning" width="420"> |

| Dictionary                                                                                     | Learning summary                                                                                 |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| <img src="../screenshots/web-frontend/dictionary.png" alt="Web dictionary lookup" width="420"> | <img src="../screenshots/web-frontend/learn-summary.png" alt="Web learning summary" width="420"> |

## Engineering Notes

- Public and authenticated areas are separated by route groups.
- Localized content is organized separately from application logic.
- Auth integration stays close to framework routing and API boundaries.
- The web app consumes backend APIs rather than duplicating backend business rules.
