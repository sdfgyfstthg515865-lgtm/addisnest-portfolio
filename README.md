# ADDISNEST — production-style portfolio workspace

ADDISNEST is a modern React + TypeScript portfolio project with two independently deployable front ends:

- `apps/ecommerce` — customer storefront: discovery, search/filtering, product detail, cart and explicitly non-payment demo checkout.
- `apps/admin` — operations dashboard: KPIs, visual sales chart, products add/edit, inventory, order workflow, customers and analytics.
- `packages/shared` — typed business model and sample data shared by both apps.

## Technology and design decisions

| Concern | Choice | Why |
|---|---|---|
| UI framework | React 18 + TypeScript | component-based, typed, scalable portfolio code |
| Tooling | Vite | fast development and static production builds |
| Icons / charts | Lucide React + Recharts | professional UI primitives without paid services |
| State | React local component state | fully usable without credentials or a backend |
| Backend path | Supabase-ready data boundary | optional free-tier persistence later; no secret is included |
| Hosting | GitHub Pages via Actions | free static deployment from `main` |

This is deliberately **not** a real payment, authentication, or customer-data system. It does not claim those features and does not contain secrets. The checkout is a portfolio demonstration only.

## Local development

1. Install Node.js 20+.
2. In this folder, run `npm install`.
3. Start the storefront with `npm run dev:shop` or the dashboard with `npm run dev:admin`.
4. Build both with `npm run build`; type-check both with `npm run typecheck`.

## GitHub Pages deployment (free)

1. Create a new GitHub repository and upload the **contents** of this folder (including `.github/workflows/deploy-pages.yml`).
2. Push to the `main` branch.
3. In GitHub, open **Settings → Pages → Build and deployment** and select **GitHub Actions**.
4. Wait for the “Deploy ADDISNEST to GitHub Pages” action to finish.
5. Your public URLs will be `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/ecommerce/` and `/admin/`.

The workflow installs the public open-source dependencies, builds each app with the correct repository base path, then deploys the static `dist` directory. Run `npm install` once before your first push so `package-lock.json` is committed; after that, you may change the workflow command to `npm ci` for repeatable builds.

## Optional free Supabase phase

When you want shared persistent data, create a free Supabase project and add tables for `products`, `orders`, `order_items`, and `customers`, using the types in `packages/shared/src/index.ts` as the model. Put only the public URL and anon key in `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` locally, then configure the same values as GitHub repository secrets. Enable row-level security before exposing any table. Never put a service-role key in client code.

## Verification status

Source structure and TypeScript configuration have been created. The next required verification is `npm install`, `npm run typecheck`, and `npm run build`; these need internet access to retrieve open-source packages because this workspace did not contain an existing Node installation or dependency cache. Once packages install, the GitHub workflow performs the same production build on every deployment.

## Portfolio demonstration

“I built ADDISNEST as a two-application React workspace: a polished customer storefront and a connected operations dashboard. I defined reusable business types, developed the product and fulfilment flows in small verifiable components, and made it deployable through GitHub Pages at no hosting cost. The current version is local-first by design; the typed data boundary makes a secure free Supabase integration the next incremental step.”
