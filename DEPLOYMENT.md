# Vela — Deployment and Environment Setup

## Environment variables

Create a `.env.local` (already created) for local dev and configure the same variables in your deployment provider:

```
NEXT_PUBLIC_APP_NAME=Vela
NEXT_PUBLIC_APP_DESCRIPTION=Vela application
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```

Add any integration secrets as needed (examples):

```
# example third‑party secrets (uncomment and set if used)
# NEXTAUTH_URL=
# NEXTAUTH_SECRET=
# DATABASE_URL=
# SENTRY_DSN=
# STRIPE_SECRET_KEY=
# STRIPE_WEBHOOK_SECRET=
```

Keep a template in `.env.example` (already added).

## Local development

1. Node version is pinned in `.nvmrc` to `v20.18.0`. Use `nvm use` to switch.
2. Install dependencies:
   ```
   npm install
   ```
3. Run the dev server:
   ```
   npm run dev
   ```

## Deploy to Vercel

Option A — Dashboard:
1. Create a new Vercel project and import the repository/folder `Vela/` (team/projects page: [lfosignals-projects](https://vercel.com/lfosignals-projects)).
2. Framework preset: Next.js. Build command and output will be auto‑detected.
3. Set environment variables in Vercel Project Settings → Environment Variables:
   - `NEXT_PUBLIC_APP_NAME`
   - `NEXT_PUBLIC_APP_DESCRIPTION`
   - `NEXT_PUBLIC_BASE_URL` (e.g., your production URL)
   - Any integration secrets you use (see examples above)
4. Set Node version to “20.x” (Project Settings → Node version) or rely on the repo’s `.nvmrc`.
5. Deploy. Vercel will run `npm install` and `npm run build` automatically.

Option B — CLI (non‑interactive):
1. Ensure dev dependency `vercel` is installed (already added).
2. Export your Vercel token and optional team scope:
   ```
   export VERCEL_TOKEN=***your_token***
   # optional, if deploying under a team
   export VERCEL_SCOPE=lfosignals-projects
   ```
3. Link the project (creates `.vercel` directory with project/org IDs):
   ```
   npm run vercel:link -- ${VERCEL_SCOPE:+--scope $VERCEL_SCOPE} --yes
   ```
4. Deploy preview:
   ```
   npm run deploy:preview -- --token $VERCEL_TOKEN ${VERCEL_SCOPE:+--scope $VERCEL_SCOPE}
   ```
5. Deploy production:
   ```
   npm run deploy -- --token $VERCEL_TOKEN ${VERCEL_SCOPE:+--scope $VERCEL_SCOPE}
   ```

## Notes

- If you add `images.domains` or other Next options, edit `next.config.ts`.
- For SEO, `robots.ts` and `sitemap.ts` are present in `src/app/`.
- Keep env values in sync across environments (Preview/Production) via Vercel’s environment scopes.


