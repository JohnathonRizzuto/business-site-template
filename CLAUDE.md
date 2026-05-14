[CLAUDE (3).md](https://github.com/user-attachments/files/27774082/CLAUDE.3.md)
# Business Website Builder

## What This Project Is
This is a website builder for local businesses. The owner (Johnathon) walks into businesses, pitches them a website, and uses Claude Code to generate a custom site. There are two modes:

1. **Landing Page** — a single-page informational site (default)
2. **Online Store** — a multi-page site with product catalog, cart, and checkout

## How It Works
Johnathon either:
- Gives you a business name and you research it yourself
- Pastes a **Client Intake Sheet** with all the details pre-filled

Either way, you build the site. Don't ask a bunch of questions. Just go.

---

## Commands

Johnathon uses short commands from his phone. Recognize these:

### "skim [area] for [business type]"
**This is the lead finder.** When Johnathon says something like:
- "skim Aurora IL for barbershops"
- "skim Naperville for restaurants without websites"
- "find me leads in Plainfield — smoke shops"
- "scan downtown Aurora for businesses with no web presence"

You search Google, Yelp, Google Maps, Facebook, and Instagram for that business type in that area. For each one you find, check:
- Do they have a website? (not counting Facebook/Yelp pages)
- Do they have a Google Business listing?
- What's their review count and rating?
- When was their last social media post?

Then categorize each lead:

**🔥 HOT** — No website, decent reviews, active business. Easy sell.
**⚠️ WARM** — Has a Facebook page or outdated site, could use an upgrade.
**❄️ COLD** — Already has a good website. Skip.

Format the results exactly like this:
```
🔥 LEADS FOUND: [Business Type] near [Area]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔥 HOT — [Business Name]
   📍 [Address]
   📞 [Phone]
   ⭐ [Rating] ([Review Count] reviews)
   🌐 No website found
   💡 [Why this is a good lead]

⚠️ WARM — [Business Name]
   📍 [Address]
   📞 [Phone]
   🌐 [What they have — Facebook page, old site, etc.]
   💡 [Why they could use an upgrade]

SUMMARY: [X] hot, [X] warm out of [X] checked.
Ready to build? Reply: "build a site for [Top Lead Name]"
```

Only show HOT and WARM leads. Don't list cold leads — waste of space.
Check at least 8-10 businesses per scan. More is better.
Always end with the "Ready to build?" prompt so Johnathon can jump straight into building.

### "build a site for [business name]"
Triggers the Landing Page build process. Research and build.

### "build a store for [business name]"
Triggers the Online Store build process. Research and build with cart + checkout.

### Pasting a Client Intake Sheet
If Johnathon pastes text that starts with `=== CLIENT INTAKE SHEET ===`, read every field and build accordingly.

---

## Recognizing the Mode

### Landing Page (default)
Triggers: any business name without store/shop keywords, or labels like "barbershop", "restaurant", "salon", "gym", "coaching", etc.
Output: single `index.html`

### Online Store
Triggers: "online store", "shop", "e-commerce", "cart", "sell products", "checkout", or the intake sheet says store type involves selling physical products
Output: `index.html` (storefront + catalog) + `checkout.html` (cart review + payment)

---

## Client Intake Sheet Format
When Johnathon pastes an intake, it looks like this:

```
=== CLIENT INTAKE SHEET ===

Business Name: [name]
Store Type: [type]

Owner Name: [name]
Owner Phone: [phone]
Owner Email: [email]

Payment Methods:
  - Stripe: [account email]
  - Venmo: [@handle]
  - Cash App: [$cashtag]

Notes:
  [anything extra]

=== END INTAKE ===
```

**Use every field.** The business name becomes the site title. The store type determines the aesthetic and which mode to use. Payment methods determine what shows up at checkout. Notes contain special requests.

---

## Payment Integration

**CRITICAL: We never collect or store credit card numbers ourselves.**

When building the checkout, use the client's actual payment methods from the intake sheet. Here's how each one works:

### Stripe
- Embed Stripe Checkout or a Stripe Payment Link
- The client needs a Stripe account — use their account email to set up
- Supports: cards, Apple Pay, Google Pay, buy-now-pay-later
- Redirect the customer to Stripe's hosted checkout page, then back to a confirmation page
- If the client doesn't have Stripe yet, note it and build a placeholder with a "Pay with Card" button that links to a setup page

### Square
- Use Square Online Checkout or Square Payment Links
- Many small businesses already have Square from their POS system
- Link to their Square checkout URL
- "Pay with Square" button that redirects to Square's hosted payment page

### PayPal
- Embed PayPal Buttons (Smart Payment Buttons)
- Use their PayPal email or @handle
- "Pay with PayPal" button that opens PayPal checkout
- Can include Venmo as a sub-option within PayPal checkout

### Venmo
- Display a "Pay with Venmo" button
- Link format: `https://venmo.com/[handle]` or deep link `venmo://paycharge?txn=pay&recipients=[handle]&amount=[total]&note=[order-description]`
- Show the Venmo QR code as a fallback (generate from handle)
- Show the total amount so the customer knows what to send
- Add a note field pre-filled with the order summary

### Cash App
- Display a "Pay with Cash App" button
- Link format: `https://cash.app/[cashtag]/[amount]` 
- Show the $cashtag prominently so customers can pay manually
- Pre-fill the amount from the cart total
- Include order reference in the note

### Zelle
- Display Zelle payment info (phone number or email)
- Zelle has no direct link/API — show instructions: "Send [amount] to [phone/email] via Zelle"
- Include the order reference number in the memo instructions

### Multiple Payment Methods
Most businesses accept more than one. Show all of them as options at checkout:
```
How would you like to pay?
[💳 Pay with Card]     ← Stripe or Square
[🅿️ Pay with PayPal]   ← PayPal
[💙 Pay with Venmo]    ← Venmo  
[💚 Pay with Cash App] ← Cash App
[💜 Pay via Zelle]     ← Zelle instructions
```

Each button goes to that payment method's flow. The customer picks how they want to pay.

---

## The Landing Page Build Process

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
Based on the business vibe, choose:
- A color palette (use CSS variables for ALL colors)
- A Google Font pairing (display + body) — NEVER use Inter, Arial, Roboto, or system fonts
- Light vs dark theme
- The overall aesthetic (bold/urban, warm/cozy, clean/minimal, retro, luxury, etc.)

### Step 3: Pick Which Sections to Include
Keep or remove based on what makes sense:

| Section | Use When |
|---------|----------|
| Hero | ALWAYS |
| About | ALWAYS |
| Services/Menu | They offer services or have a menu |
| Gallery | Visual product (food, hair, tattoos, etc.) |
| Testimonials | You found real reviews online |
| Pricing | Clear pricing tiers |
| FAQ | Common questions |
| Contact/CTA | ALWAYS |
| Map | Physical location |

**Speed rule: Skip any section you can't fill with real data.** A clean 5-section site beats a bloated 10-section site with filler content.

### Step 4: Write the Copy
- Use the business's own words when possible
- Keep it punchy and real — not corporate or generic
- Match the tone to the business

### Step 5: Social Media
Always search for and include the business's social media links:
- Facebook, Instagram, TikTok at minimum
- Add them in the footer and/or header
- Use the actual URLs you find, not placeholders

### Step 6: Google Maps Embed
Use this format:
`<iframe src="https://www.google.com/maps?q=FULL+ADDRESS+URL+ENCODED&output=embed" allowfullscreen loading="lazy"></iframe>`
If you can't find an address, skip the map section entirely. Never leave a broken placeholder.

### Step 7: Images
Use Unsplash images that match the SPECIFIC business type:
- Barbershop → "barbershop interior", "barber cutting hair"
- Coffee shop → "coffee shop counter", "latte art"
- Gym → "gym equipment", "personal training"
Never use generic stock photos. Add comments noting "REPLACE WITH REAL PHOTO".

---

## The Online Store Build Process

### File Structure
```
index.html    — storefront: header, hero, product grid with cart
checkout.html — cart review, payment method selection, confirmation
```

Both files share the same CSS variables and fonts. They communicate through localStorage for the cart.

### index.html — The Storefront
- Header with store name and cart icon (shows item count badge)
- Hero section with store name, tagline
- Category filter buttons (if 6+ products)
- Product grid: each card shows image/emoji, name, price, description, "Add to Cart" button
- Add-to-cart shows visual feedback (button changes to "Added ✓", toast notification)
- Cart saves to localStorage so it persists between pages
- "View Cart" / cart icon links to checkout.html

### checkout.html — Cart & Payment
- Display all cart items with quantity controls (+/−), remove button
- Subtotal, tax (8%), total
- **Payment method selection** — show buttons for each method from the intake sheet
- Each payment button links to that provider (Stripe checkout, Venmo link, Cash App link, etc.)
- Confirmation page after payment

### Product Data
If the user doesn't specify products, research the business and create realistic products with:
- Name, price, description, category
- Use emoji as image placeholders
- 8-12 products minimum
- Group into 3-4 categories

If the intake sheet has a "Products" section, use those exactly.

### Design Rules (same as landing page)
- Bold themed aesthetic matching the store type
- Google Fonts (never Inter/Arial)
- CSS variables for all colors
- Hover effects on product cards
- Mobile responsive
- Smooth animations (add-to-cart feedback, page transitions)

---

## Credibility Rules
- Stats bar: use soft rounded numbers ("300+ Reviews", "10+ Years") not exact inflated numbers
- Star rating: use the ACTUAL rating you find (4.8, 4.9) not a perfect 5.0 unless real
- Testimonials: max 3, paraphrase real review themes, first names only
- Never make up stats you can't back up
- The owner should read the site and think "that's us" — not "that's too good to be true"

## Code Style Rules
- Everything in HTML files — CSS in `<style>`, JS in `<script>`
- Use CSS variables for ALL colors
- Mobile-first responsive design
- Smooth scroll-triggered animations using Intersection Observer
- No external dependencies except Google Fonts
- All images use Unsplash URLs that match the business — add comments noting "REPLACE WITH REAL PHOTO"

## Git Rules
- Always commit to `main` branch directly — Vercel auto-deploys from main
- Never create feature branches
- Commit message format: "Build site for [Business Name]" or "Update [Business Name] site"

## Important Notes
- This is a PITCH tool. The site should look amazing even with placeholder images.
- Speed matters. Johnathon is standing in the business. Build fast.
- When in doubt, make it look premium. These are small businesses — give them something that looks like it cost $2,000.
- Always include a way to contact the business (phone, email, or social link)
- If you find real Google reviews, paraphrase the themes with first name only for privacy
