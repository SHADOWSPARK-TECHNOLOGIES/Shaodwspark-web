ShadowSpark production app (Next.js App Router + Prisma + BullMQ + Firecrawl RAG).

Architecture: see [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Getting Started

Install dependencies with pnpm, then start the development server:

```bash
pnpm install --frozen-lockfile
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Deploy

Hosting is Railway only. Build with `pnpm build` and start with `pnpm start`. Configure the Railway service from `.env.example`. Do not add Vercel or Netlify project config.

## Learn More

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.
