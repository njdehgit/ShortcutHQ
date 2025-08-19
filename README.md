
# ShortcutHQ — Team Link Manager (Micro‑SaaS)

Internal **team-wide short links** for docs, dashboards, and assets. Create memorable slugs like `/go/ops/oncall`. Includes **teams**, **invites**, **Stripe team subscriptions**, and **usage limits**.

- Next.js (App Router, TypeScript)
- Prisma + SQLite (easy to swap Postgres)
- NextAuth (GitHub) for auth
- Stripe Subscriptions (team-level) with webhooks
- Team Invites & Roles (owner/admin/member)
- Free plan (20 links, 3 members), Pro (unlimited links, 25 members)

## Quick Start

```bash
npm install
cp .env.example .env
npx prisma db push
npm run dev
```

**Set env:** `NEXTAUTH_SECRET`, `GITHUB_ID`, `GITHUB_SECRET`, `STRIPE_SECRET_KEY`, `STRIPE_PUBLIC_KEY`, `STRIPE_PRICE_ID`, `APP_URL`, `NEXTAUTH_URL`.

**Stripe Webhook (dev):**
```bash
stripe listen --events checkout.session.completed,customer.subscription.updated,customer.subscription.deleted   --forward-to localhost:3000/api/stripe/webhook
```
Copy `whsec_...` to `STRIPE_WEBHOOK_SECRET` in `.env`.

## Deploy
- Vercel + hosted Postgres (Neon/Supabase) recommended.
- Set production webhook to `https://YOURDOMAIN/api/stripe/webhook`.
- Run `npx prisma db push` after setting `DATABASE_URL`.

## License
MIT
