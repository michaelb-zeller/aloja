# Zelene

**Creator platform · Web3 integrations · Built in public**

[Website](https://zelene.org) · [Development portal](https://zelene.dev) · [GitHub organization](https://github.com/zelene-official)

## About Zelene

Zelene is an emerging platform designed to help creators share content, build communities, and explore ways to monetize their work. Its proposed experience combines creator tools with Solana-based payment integrations where blockchain adds practical value.

**This repository documents the ongoing development of Zelene's web application.** Features are added progressively, with implementation details and status updated as the project advances. It is not limited to the sign-in page.

## Development status

The authentication experience is the first frontend area being developed. The items below distinguish available interface work from planned platform capabilities; an interface or integration point does **not** imply a complete backend workflow.

| Area | Current status |
| --- | --- |
| Responsive sign-in and registration screens | UI implemented; backend integration pending |
| Password recovery and form feedback | UI and request handling prepared; backend required |
| Social sign-in | Provider entry points; OAuth configuration required |
| Solana wallets | Wallet selection and integration entry points; verification/backend work required |
| Localization | English and Spanish for the current authentication interface |
| Initial loading experience | Implemented in the frontend |
| Creator profiles and dashboard | Planned / upcoming development |
| Content publishing and memberships | Planned |
| Tips, paid content, and Solana payments | Planned |
| Messaging, analytics, and media experiences | Planned |

This table describes the project at its current stage, not a committed release schedule. See the repository history for ongoing changes.

## Technology

### Used in the current frontend

- **React + TypeScript + Vite** for the web application
- **CSS** for the current interface and responsive layouts
- **i18next + react-i18next** for interface localization
- **Browser APIs and HTTP requests** for authentication and wallet integration entry points

### Proposed platform architecture

The broader Zelene architecture is being developed and may evolve as requirements and testing progress:

- **Frontend UI:** Tailwind CSS and shadcn/ui, introduced as the application grows
- **Backend:** NestJS + TypeScript, REST APIs
- **Data and background processing:** PostgreSQL, Redis, BullMQ
- **Media:** Cloudflare R2 and Cloudflare Stream
- **Blockchain:** Solana integration; Rust + Anchor where smart contracts are needed

The proposed technologies above should **not** be interpreted as already implemented in this repository.

## Getting started

Use a Node.js version compatible with the Vite version in `package.json`.

```bash
npm install
npm run dev
```

Open the local address printed by Vite (usually `http://localhost:5173`).

To check a production build locally:

```bash
npm run build
npm run preview
```

> Building the frontend does not verify external authentication providers, a live NestJS backend, or Solana wallet-signature verification.

### API configuration

If the current authentication service uses `VITE_API_URL`, configure a local environment file as needed:

```dotenv
VITE_API_URL=http://localhost:3000
```

When this variable is not set, the current service may use same-origin `/api/` routes, depending on its configuration. A running API or proxy is required for those requests to succeed.

Never store private keys, API secrets, wallet recovery phrases, or server credentials in `VITE_` variables: Vite exposes these values to the client bundle.

## Project structure

The structure below describes the initial frontend implementation. New features and directories will be introduced progressively.

```text
zelene-platform/
├── public/
│   ├── icons/                 # Language flags and wallet icons
│   ├── images/                # Zelene visual assets
│   └── locales/
│       ├── en/
│       │   ├── auth.json
│       │   └── common.json
│       └── es/
│           ├── auth.json
│           └── common.json
├── src/
│   ├── components/
│   │   ├── AuthIcons.tsx
│   │   ├── LanguageSwitcher.tsx
│   │   ├── LoadingScreen.tsx
│   │   └── SocialButtons.tsx
│   ├── pages/
│   │   └── LoginPage.tsx
│   ├── services/
│   │   └── auth.ts
│   ├── App.tsx
│   ├── i18n.ts
│   ├── main.tsx
│   └── styles.css
├── index.html
└── package.json
```

## Internationalization

Zelene uses `react-i18next` and JSON translation namespaces. The current authentication interface is available in **English** and **Spanish**.

- The user's previously selected language takes priority when saved
- Otherwise, the application detects the browser's preferred language
- Unsupported languages fall back to English
- Language changes update the interface without a full page reload

Translation catalogs are stored under `public/locales/<language>/<namespace>.json`. As new modules are developed, they can introduce separate catalogs such as `creator.json`, `payments.json`, or `messaging.json`.

Only enable a new language once its interface strings and accessibility messages have been translated and reviewed.

## Security and integration notes

The current frontend includes authentication-related interface elements and request handlers. Complete email authentication, password recovery, OAuth callbacks, secure sessions, and Solana signature verification depend on separately configured and tested backend services.

- Do not use real credentials in an unverified development preview
- Never request or expose wallet seed phrases or private keys
- Verify wallet challenges, expiration, and replay protection on the server
- Protect server-side credentials and keep local environment files out of version control

## Contributing and progress

Zelene is being developed iteratively. New commits may introduce new pages, UI components, translations, integrations, or architectural changes. Descriptions and development-status entries will be updated as functionality becomes available.

Before sharing a development build, run `npm run build`, review responsive layouts and accessibility, verify translation keys, and clearly label any unfinished integrations.

For general information, visit [zelene.org](https://zelene.org). Development updates are shared through [zelene.dev](https://zelene.dev) and the [Zelene GitHub organization](https://github.com/zelene-official).

---

