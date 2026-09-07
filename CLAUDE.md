@AGENTS.md

# [Client Name] — Programmatic Local SEO Site

## What this project is

A programmatic, SEO-ready marketing website for [Client Name], a [type of business] serving
[region]. The site generates a large set of location and service pages from structured data
rather than hand-written files, so one content model produces the homepage, service hubs,
city hubs, and every [service]/[location] landing page.

Stack: Next.js (App Router), TypeScript, Tailwind. Hosted on Vercel or Cloudflare Pages,
DNS on Cloudflare.

The goal is organic ranking for local intent searches ("[service] in [city]") and clean,
machine-readable output for AI crawlers and answer engines.

## Project structure

```
app/
  page.tsx                     Homepage. Brand, primary services, main conversion path.
  [service]/page.tsx           Service hub. Explains one service, links to every city for it.
  city/[city]/page.tsx         City hub. Everything offered in one city, links to services there.
  [service]/[location]/page.tsx  Programmatic landing pages. The bulk of the site.
  locations/page.tsx           Link hub listing every city and service page, for crawl depth.
  sitemap.ts                   Generates sitemap.xml from the same data the pages come from.
  robots.ts                    Crawl rules. Allows all AI and search bots.
  layout.tsx                   Root layout, global metadata defaults, nav, footer, schema.
  llms.txt/route.ts            Plain-text site summary for LLM crawlers.
  claude.md/route.ts           Markdown site summary served at a public URL.
  ai.xml/route.ts              Structured AI-readable feed of services and locations.

data/
  locations.ts                 Every city or area served: name, slug, county, population, notes.
  keywords.ts                  Target keyword per service and per service/location pair.
  tiers.ts                     Which pages are indexed, which are noindex. Tier lists only.
  business.ts                  Single source of truth for brand data: name, phone, address,
                               hours, license numbers, service areas, social links.

components/                    Reusable UI: hero, CTA blocks, service cards, FAQ, testimonials,
                               call button, footer. All brand data arrives via props from data/.

lib/
  seo.ts                       Builds titles, meta descriptions, canonicals, JSON-LD schema.
  content-resolver.ts          Maps a service + location pair to its page content and copy.
  ai-layer.ts                  Builds the payloads served by llms.txt, claude.md, and ai.xml.

research/                      Keyword research, competitor notes, SERP snapshots. Reference
                               material, not shipped code.

public/                        Static assets. Images, logos, favicons, verification files.
```

## Rules

- Never edit the tier-indexing logic. Only edit the lists inside `data/tiers.ts`.
- Never flip an indexed page to noindex.
- Never hardcode brand data in a component. It comes from `data/business.ts`.
- Never fabricate a metric, review, testimonial, star rating, or year founded. If a number is
  not in `data/business.ts` or supplied by the client, leave a placeholder and ask.
- Never block an AI bot in `robots.ts`. GPTBot, ClaudeBot, PerplexityBot, and the rest stay
  allowed.
- Never install a package without asking first.
- Never edit a file you were not asked to edit.
- Always put `'use client'` at the top of any file that uses hooks or event handlers.

## Standards every page meets

- Title tag under 60 characters.
- Meta description under 160 characters.
- Exactly one H1 per page.
- Programmatic pages carry 1,000+ words of unique, useful copy.
- A CTA above the fold and another at the bottom of the page.
- Phone number is a click-to-call `tel:` link everywhere it appears.
- Image filenames include the target keyword and the city, and every image has alt text.
- No em dashes.
- No exclamation marks in body copy.
- Active voice.

## The loop

1. Describe the change in plain language, including which files are in scope.
2. Claude edits only those files.
3. Review the diff before anything else.
4. Test locally with `npm run dev` and load the affected routes.
5. Commit.

Run the build and the type check before every push. A push that has not been built is not
ready.

## Commands

```
npm run dev        Local dev server
npm run build      Production build, run before every push
npx tsc --noEmit   Type check, run before every push
```

## Client-specific notes

- Client: [Client Name]
- Business type: [type of business]
- Primary region: [region]
- Domain: [domain]
- Host: [Vercel or Cloudflare Pages]
- Phone: [phone number]
- Service area: [list of cities or counties]
- Services offered: [list of services]
- Brand voice: [notes]
- Things to avoid saying: [notes]
- Licenses or credentials to display: [notes]
- Analytics and Search Console access: [notes]
- Open questions for the client: [notes]
