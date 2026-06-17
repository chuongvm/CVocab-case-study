# Screenshot Policy

Only commit screenshots that are already redacted and safe for public viewing.

## Good Candidates

- Public App Store or Play Store screenshots.
- Public website pages.
- Mobile app screens with no private user information.
- Backoffice screens after blurring emails, IDs, order/payment data, tokens, and private content.
- k6 summaries after removing base URLs, tokens, internal hostnames, and exact production identifiers.

## Do Not Commit

- Raw screenshots.
- Production logs.
- Browser DevTools screenshots with headers or tokens.
- Admin screens containing real user data.
- Store/payment/provider dashboards.

Use `screenshots/raw/` locally only. It is gitignored.

## Current Public Screenshot Sets

| Folder | Product surface | Used in docs |
| --- | --- | --- |
| `mobile/` | Flutter app for iOS and Android | `README.md`, `docs/mobile-app.md` |
| `web-frontend/` | Public/authenticated web frontend | `README.md`, `docs/web.md` |
| `web-backoffice/` | Internal backoffice | `README.md`, `docs/backoffice.md` |

Some screenshots are kept in the folder but not embedded in the main pages because they reveal more operational detail than the case study needs.
