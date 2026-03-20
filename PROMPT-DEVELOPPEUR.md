# 🎹 Developer Prompt — Emmanuelle Facchineri Website
## "Convert the HTML prototype into a real structured web project"

---

## CONTEXT

You are receiving an `emmanuelle-facchineri.html` file: a complete and functional prototype of a professional website for **Emmanuelle Facchineri**, piano teacher in Saint-Étienne. The design, content, CSS styles, and JS navigation are finalized in this single file.

**Your mission: transform this one-file prototype into a professional, organized, maintainable web project ready for deployment.**

---

## RECOMMENDED TECH STACK

**Option A — Modern static site (recommended if no backend needed)**
- **Framework**: [Astro](https://astro.build/) v4+
- **Styling**: CSS modules or component-scoped styles (no third-party CSS framework)
- **Deployment**: Vercel or Netlify (free, automatic HTTPS, CI/CD)
- **Contact form**: Formspree.io (HTTPS, direct email, no backend)
- **CMS (optional)**: Decap CMS (formerly Netlify CMS) so Emmanuelle can edit news herself

**Option B — Next.js (if future evolution toward student area, online payment, etc. is needed)**
- **Framework**: Next.js 14+ App Router
- **Styling**: CSS Modules
- **Backend**: API Routes for contact form
- **Deployment**: Vercel

---

## PROJECT STRUCTURE (Option A — Astro)

```
emmanuelle-piano/
│
├── public/
│   ├── images/
│   │   ├── hero-accueil.jpg          ← 📸 HOME HERO PHOTO (1920×440px)
│   │   ├── hero-fonctionnement.jpg   ← 📸 HOW IT WORKS HERO PHOTO (cat on piano)
│   │   ├── hero-tarifs.jpg           ← 📸 PRICING HERO PHOTO (grand piano)
│   │   ├── hero-parcours.jpg         ← 📸 JOURNEY HERO PHOTO (concert/studio)
│   │   ├── portrait-emmanuelle.jpg   ← 📸 MAIN PORTRAIT (400×500px)
│   │   ├── cours-debutants.jpg       ← 📸 HOW IT WORKS SECTION left
│   │   ├── cours-avances.jpg         ← 📸 HOW IT WORKS SECTION right
│   │   ├── cours-piano-section.jpg   ← 📸 HOME SECTION right
│   │   ├── galerie-01.jpg            ← 📸 GALLERY (x6, 600×600px squares)
│   │   ├── galerie-02.jpg
│   │   ├── galerie-03.jpg
│   │   ├── galerie-04.jpg
│   │   ├── galerie-05.jpg
│   │   ├── galerie-06.jpg
│   │   ├── og-cover.jpg              ← 📸 OG IMAGE (1200×630px, social media SEO)
│   │   └── logo.png                  ← LOGO (if existing)
│   ├── videos/
│   │   ├── concert-01.mp4            ← 🎬 VIDEO 1 (or YouTube embed)
│   │   └── concert-02.mp4            ← 🎬 VIDEO 2
│   ├── favicon-32x32.png
│   ├── favicon-16x16.png
│   ├── apple-touch-icon.png
│   ├── site.webmanifest
│   └── robots.txt                    ← SEO: generate with correct domain
│
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro          ← Common layout: SEO <head>, header, footer, sticky bar
│   │
│   ├── components/
│   │   ├── Header.astro              ← Sticky navigation + mobile hamburger
│   │   ├── Footer.astro              ← Footer
│   │   ├── HeroBand.astro            ← Reusable hero (props: image, title, eyebrow, height)
│   │   ├── Planning.astro            ← Schedule table (present on all pages)
│   │   ├── ContactForm.astro         ← Contact form (present on all pages)
│   │   ├── TestimonialsCollapsible.astro
│   │   ├── TarifCard.astro           ← Individual pricing card
│   │   ├── QuoteBlock.astro
│   │   ├── StatRow.astro
│   │   ├── TimelineItem.astro
│   │   ├── GalleryGrid.astro
│   │   └── StickyBar.astro           ← Floating Planning & Contact buttons
│   │
│   ├── pages/
│   │   ├── index.astro               ← Home
│   │   ├── fonctionnement.astro
│   │   ├── tarifs.astro
│   │   ├── parcours.astro
│   │   ├── actualites.astro
│   │   ├── galeries.astro
│   │   ├── avis.astro
│   │   └── contact.astro
│   │
│   ├── content/                      ← Editable content (Markdown or JSON)
│   │   ├── actualites/               ← News articles (one .md file per article)
│   │   │   ├── rentree-2024.md
│   │   │   └── duo-aube.md
│   │   └── temoignages/              ← Testimonials
│   │       ├── sophie-m.md
│   │       └── thomas-b.md
│   │
│   ├── styles/
│   │   ├── global.css                ← CSS variables, reset, typography, utilities
│   │   └── pages/
│   │       ├── accueil.css
│   │       ├── tarifs.css
│   │       └── galeries.css
│   │
│   └── data/
│       ├── horaires.json             ← Schedule data
│       ├── tarifs.json               ← Pricing data
│       └── temoignages.json          ← Testimonials (if not managed via content/)
│
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── .env                              ← Secret variables (Formspree email, API keys)
```

---

## PROTOTYPE MIGRATION — STEPS

### Step 1: Project setup
```bash
npm create astro@latest emmanuelle-piano -- --template minimal
cd emmanuelle-piano
npm install
```

### Step 2: Extract styles
- Copy all `<style>` content from the prototype into `src/styles/global.css`
- Declare CSS `:root` variables in global.css
- Import global.css in `BaseLayout.astro`

### Step 3: Create reusable components
Prioritize extracting components present on **all pages**:
1. `Planning.astro` — The weekly schedule table
2. `ContactForm.astro` — The contact form with Formspree submission
3. `Header.astro` — Navigation (replace JS onclick with `<a href="/page">` links)
4. `Footer.astro`
5. `StickyBar.astro`

### Step 4: Create pages
Each page in `src/pages/` takes the HTML content from the corresponding prototype page, using the Astro components created in step 3.

### Step 5: Replace image placeholders
See the complete list of images to provide in `public/images/`. Each placeholder is documented in the source HTML file with a `📸 PHOTO` comment.

### Step 6: Contact form
Create an account on [Formspree.io](https://formspree.io):
```html
<!-- In ContactForm.astro -->
<form action="https://formspree.io/f/YOUR_FORMSPREE_ID" method="POST">
  <!-- form fields -->
  <input type="hidden" name="_replyto" value="">
  <input type="hidden" name="_subject" value="New lesson request — Emmanuelle Facchineri Website">
</form>
```

### Step 7: Final SEO
- Replace all `YOUR-DOMAIN.fr` in JSON-LD with the real domain
- Generate favicons at https://realfavicongenerator.net
- Update phone number in JSON-LD
- Add Google Maps CID in `sameAs`
- Submit sitemap to Google Search Console after deployment

---

## CONTACT FORM CONFIGURATION

The form must send emails to: `emmanuelle.facchineri@gmail.com`

**Required fields:**
- First & Last Name (required)
- Email (required)
- Phone (optional)
- Desired level (select)
- Desired duration (select)
- Format: home / Teams video / WhatsApp video (select)
- Message (required, textarea)

**Anti-spam:** Add a hidden honeypot field + enable Formspree protection.

---

## POST-DEPLOYMENT SEO CHECKLIST

### Google
- [ ] Create/claim **Google Business Profile** (formerly Google My Business)
  → https://business.google.com
  → Category: "Music school" or "Music teacher"
  → Add photos, hours, description, website link
- [ ] Submit site to **Google Search Console**
  → Verify ownership via HTML tag or DNS
  → Submit sitemap.xml
- [ ] Check **Core Web Vitals** (PageSpeed Insights)

### Bing
- [ ] Submit to **Bing Webmaster Tools** → https://www.bing.com/webmasters
- [ ] Create/claim a **Bing Places for Business** listing

### Local directories (backlinks + local presence)
- [ ] **PagesJaunes.fr** — free "Piano teacher" listing
- [ ] **Kompass.com** — B2B directory
- [ ] **Yelp.fr** — local listing with reviews
- [ ] **Tripadvisor** (if applicable)
- [ ] **Mappy.com** — local listing
- [ ] **Annuaire-musique.fr** or specialized music directories
- [ ] **CercleHarmonique** or equivalent piano teacher directories France

### Additional SEO content (optional, high impact)
Create a **blog** or "Tips" section with target articles:
- "How to choose your first piano in Saint-Étienne"
- "What age to start piano?"
- "Classical piano lessons vs contemporary music: what are the differences?"
- "Learning piano online: advantages and tips"
→ Each article = one indexable URL = more chances to appear on Google

---

## ENVIRONMENT VARIABLES (.env)

```env
# Formspree
PUBLIC_FORMSPREE_ID=xxxxxxxxxxxx

# Google Analytics (optional)
PUBLIC_GA_ID=G-XXXXXXXXXX

# Facebook Page ID (optional, for review integration)
PUBLIC_FB_PAGE_ID=xxxxxxxxxxxxxxxxx
```

---

## RECOMMENDED DEPLOYMENT

**Vercel (free, HTTPS, automatic deployment from Git)**
```bash
npm install -g vercel
vercel
```
→ Connect GitHub/GitLab repo for automatic deployment on every push.

**Recommended domain:**
- `emmanuelle-facchineri-piano.fr`
- `cours-piano-saint-etienne.fr` ← excellent for local SEO
- `piano-saint-etienne.fr`

---

## IMPORTANT NOTES

1. **All pages must include** the Planning and Contact Form (reusable Astro components).
2. **Navigation** must change from JS `onclick="showPage()"` to real `<a href="/page">` links so Google can index each page separately.
3. **Images** must be optimized with Astro's `<Image>` component (automatic WebP compression).
4. **JSON-LD** on each page must reference the correct canonical URL for that page.
5. **Accessibility**: check color contrasts (gold on dark background = OK, gold on light background = to verify) and add meaningful `alt` attributes to all images.
