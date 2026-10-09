# ShadowSpark Chatbot — Install Guide

A floating chat bubble that explains ShadowSpark's services, powered by Claude Haiku 4.5.
The chat route ships with the Next.js app on Railway. Set `ANTHROPIC_API_KEY` on that service.

## What's included
1. `route.ts` — the API endpoint that talks to Claude (with your ShadowSpark knowledge baked in)
2. `ChatWidget.tsx` — the floating chat bubble UI (dark theme, orange accent to match your site)

## Install (3 steps)

### 1. Drop the files into your Next.js project (`~/shadowspark-clean`)

```bash
# API route
mkdir -p app/api/chat
cp route.ts app/api/chat/route.ts

# Component
mkdir -p components
cp ChatWidget.tsx components/ChatWidget.tsx
```

### 2. Mount the widget in your root layout

In `app/layout.tsx`, import and render it once (it floats over everything):

```tsx
import ChatWidget from "@/components/ChatWidget";

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        {children}
        <ChatWidget />
      </body>
    </html>
  );
}
```

### 3. Add your Anthropic API key on Railway

Set `ANTHROPIC_API_KEY` on the Railway service. For local runs, put the same variable in `.env.local`.

Get a key at: https://console.anthropic.com/settings/keys

## Deploy

Deploy the Next.js app on Railway. The chat route is part of that service (`pnpm build`, then `pnpm start`).

## Test locally first (optional)

```bash
pnpm dev
# open http://localhost:3000 — the bubble appears bottom-right
```

## Cost

Claude Haiku 4.5 is $1 per million input tokens, $5 per million output tokens.
A typical site chat (a few short turns) costs a fraction of a cent.
The API route trims history to the last 10 messages to keep costs predictable.

## Customizing what the bot knows

Edit the `SYSTEM_PROMPT` string at the top of `route.ts`. That's the bot's entire
knowledge — update services, add FAQs, change tone, etc. Redeploy after editing.

## Notes
- The widget uses inline styles so it works without Tailwind config — but you can
  swap to your own classes if you prefer.
- `runtime = "edge"` gives fast cold starts. Remove that line to use the Node runtime
  if you later need Node-only APIs.
- No data is stored — conversations live only in the browser session.
