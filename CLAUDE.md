# Business Website Builder

## What This Project Is
This is a single-page website template designed to be customized for any local business. The owner (Johnathon) walks into businesses, pitches them a website, and uses Claude Code to generate a custom site on the spot from his iPhone.

## How It Works
1. Johnathon gives you a business name and location (e.g. "Tina's Coffee Shop in Aurora IL")
2. You search the web for that business — Google, Yelp, Facebook, Instagram, whatever's public
3. You pull: business name, what they do, hours, location, phone, vibe, menu/services, reviews
4. You customize `index.html` using everything you found
5. The result is a fully branded, deploy-ready single-page site

## The Command
When Johnathon says something like:
- "build a site for [business name]"
- "skim [business name] and build me a site"
- "make a website for [business name] in [city]"

...you research and build. Don't ask a bunch of questions. Just go.

## File Structure
- `index.html` — the entire site (HTML + CSS + JS in one file)
- `CLAUDE.md` — this file (your instructions)
- That's it. No frameworks, no build tools, no separate CSS/JS files.

## How to Customize the Template

### Step 1: Research the Business
Search for the business online. Look for:
- Business name and tagline/slogan
- What they sell or what services they offer
- Address, phone number, hours of operation
- Social media links (Facebook, Instagram, TikTok)
- Google/Yelp reviews (pull real quotes if available)
- Photos or descriptions of their space/products
- Their general vibe — upscale? casual? family-owned? trendy?

### Step 2: Pick the Visual Theme
Based on the business vibe, customize the CSS variables in `:root`. Here are starting points — but MIX and MATCH, don't just copy one exactly:

**Coffee Shop / Café / Bakery:**
- Display font: `'DM Serif Display'` or `'Playfair Display'`
- Body font: `'Nunito'` or `'DM Sans'`
- Palette: warm creams, rich browns, amber accents
- Vibe: cozy, inviting, warm

**Barbershop / Salon / Tattoo:**
- Display font: `'Bebas Neue'` or `'Oswald'`
- Body font: `'Barlow'` or `'Outfit'`
- Palette: dark backgrounds, gold/silver accents, high contrast
- Vibe: sharp, bold, masculine or edgy

**Restaurant / Bar:**
- Display font: `'Cormorant Garamond'` or `'Libre Baskerville'`
- Body font: `'Lato'` or `'Source Sans 3'`
- Palette: deep greens, burgundy, cream, warm lighting feel
- Vibe: upscale casual, appetizing, atmospheric

**Fitness / Gym / Trainer:**
- Display font: `'Bebas Neue'` or `'Anton'`
- Body font: `'Barlow'` or `'Nunito Sans'`
- Palette: dark bg, neon or bold accent (red, electric blue, lime)
- Vibe: intense, motivational, high-energy

**Boutique / Retail / Florist:**
- Display font: `'Playfair Display'` or `'Cormorant'`
- Body font: `'Nunito'` or `'Quicksand'`
- Palette: soft pastels, blush, sage, gold accents
- Vibe: elegant, curated, feminine

**Auto / Mechanic / Trade:**
- Display font: `'Oswald'` or `'Teko'`
- Body font: `'Barlow'` or `'Source Sans 3'`
- Palette: dark grays, industrial orange/red/yellow accents
- Vibe: rugged, trustworthy, no-nonsense

**Tech / Creative Agency / Modern:**
- Display font: `'Syne'` or `'Space Grotesk'`
- Body font: `'Inter'` or `'General Sans'`
- Palette: near-black bg, vibrant accent (purple, cyan, coral)
- Vibe: sleek, cutting-edge, minimal

These are STARTING POINTS. Always adapt to what you find about the actual business. If a barbershop has a vintage vibe, use serif fonts instead of sans-serif. If a coffee shop is modern and minimalist, skip the cozy browns.

### Step 3: Pick Which Sections to Include
The template has ALL possible sections. Keep or remove based on what makes sense:

| Section | Use When |
|---------|----------|
| Hero | ALWAYS — every site needs this |
| About | ALWAYS — tells their story |
| Services/Menu | They offer services or have a menu |
| Gallery | They have a visual product (food, hair, tattoos, etc.) |
| Testimonials | You found real reviews online |
| Pricing | They have clear pricing tiers |
| FAQ | They have common questions (or you can generate smart ones) |
| Newsletter | They want to collect emails |
| Contact/CTA | ALWAYS — how to reach them |
| Map | They have a physical location |

### Step 4: Write the Copy
- Use the business's own words when possible (from their website, social media, reviews)
- Keep it punchy and real — not corporate or generic
- Match the tone to the business (casual for a taco shop, refined for a law firm)
- If you can't find much info, write smart placeholder copy that sounds specific, not generic

### Step 5: Customize Colors
Update ALL CSS variables in `:root`:
```css
:root {
  --color-bg: /* main background */
  --color-surface: /* card/section backgrounds */
  --color-surface-hover: /* hover states */
  --color-text: /* primary text */
  --color-text-muted: /* secondary text */
  --color-accent: /* buttons, highlights, links */
  --color-accent-hover: /* button hover */
  --color-border: /* subtle borders */
}
```

### Step 6: Update Fonts
Change the Google Fonts `<link>` tag AND the CSS `font-family` declarations to match your chosen pair.

## Code Style Rules
- Everything in ONE html file — CSS in `<style>`, JS in `<script>`
- Use CSS variables for ALL colors (never hardcode colors in individual styles)
- Mobile-first responsive design
- Smooth scroll-triggered animations using Intersection Observer
- No external dependencies except Google Fonts
- Keep class names short but readable
- All images use placeholder URLs from unsplash or similar — add comments noting "REPLACE WITH REAL PHOTO"

## Deployment (REQUIRED — one repo per business)
Every site you build goes to its OWN GitHub repo. Never overwrite or push customized site code back into the `business-site-template` repo — that repo holds only the blank template.

For each new build:
1. **Create a new GitHub repo** under Johnathon's account, named after the business in kebab-case (e.g. "rons-barber-shop", "tinas-coffee-shop", "exclusive-fades-barbershop"). Strip "the", punctuation, and "LLC/Inc".
2. **Initialize it** with the customized `index.html` (and only that file — no CLAUDE.md, no template artifacts).
3. **Push** to that new repo's `main` branch.
4. **Connect the repo to Vercel** as a new project so it auto-deploys. Use Vercel's GitHub integration (no build config needed — it's a static single-file site).
5. **Capture the live Vercel URL** and include it in the ntfy notification per the Notifications rule.

The `business-site-template` repo stays clean: it is the source the customization is generated FROM, not the target the build is pushed TO.

## Important Notes
- This is a PITCH tool. The site should look amazing even with placeholder images.
- Speed matters. Johnathon is standing in the business. Build fast.
- When in doubt, make it look premium. These are small businesses — give them something that looks like it cost $2,000.
- Always include a way to contact the business (phone, email, or social link)
- If you find real Google reviews, use them (with first name only for privacy)

## Research (REQUIRED — DO NOT SKIP)
Every time you build a site, you MUST search Google for the business first and find:
- **Real hours of operation** — put them in a dedicated Hours section. No placeholder hours.
- **Real address** — put it in the Contact/Map section. No fake addresses.
- **Real phone number**
- **Real photos** — use any real photos you find instead of Unsplash stock images.

If you find their Google Business listing, pull everything from there. Never skip the research step.

## Notifications (REQUIRED)
After finishing a skim or a site build, send a notification to Johnathon's phone by running this command:

```
Invoke-WebRequest -Uri 'https://ntfy.sh/johnathon-builds-2026' -Method POST -Body 'YOUR MESSAGE HERE'
```

Replace `YOUR MESSAGE HERE` with the result of the work:
- **Skims:** the lead list (business name + a one-line summary per lead)
- **Site builds:** the live link to the deployed site

If running in a non-PowerShell shell (Linux/macOS/sandbox), use the equivalent:
```
curl -d 'YOUR MESSAGE HERE' https://ntfy.sh/johnathon-builds-2026
```

Do this automatically every time — don't ask first.
