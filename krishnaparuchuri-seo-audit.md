# SEO Audit — krishnaparuchuri.com
**Prepared for:** Krishna Paruchuri  
**Date:** May 26, 2026  
**Auditor:** AI SEO Analyst  
**Scope:** Full site crawl — homepage + demo subdomains  

---

## 1. Overall SEO Scores

| Dimension | Score | Rationale |
|---|---|---|
| **Keyword Targeting** | 5 / 10 | Branded terms covered well; industry long-tails nearly absent |
| **On-Page SEO** | 6 / 10 | Title, meta, OG tags solid; schema markup and canonical missing |
| **Internal Linking** | 2 / 10 | Single-page anchor links only; zero cross-page link equity |
| **Content Depth** | 5 / 10 | Good project descriptions; no case studies, blog, or measurable impact narrative |
| **Technical SEO** | 4 / 10 | HTTPS + mobile OK; sitemap/robots unknown; no schema; subdomains leak equity |
| **Personal Branding SEO** | 6 / 10 | Name is prominent; OG/Twitter cards set up; missing thought leadership and social proof |

**Composite average: 4.7 / 10**

---

## 2. What Is Working Well

- **Branded title tag is clean and sharp.** "Krishna Paruchuri — Product Leader" hits the exact search intent for anyone Googling your name. The em-dash signals confidence and reads well in SERPs.
- **Meta description is fact-dense.** "16+ years... healthcare, fintech, and AI... IBM Watson Health... Reliance Jio... Experian" packs credential signals into under 155 characters. Most portfolios leave this field empty or boilerplate.
- **OG and Twitter card metadata is complete.** `og:title`, `og:description`, `og:image` with dimensions and alt text, `twitter:card: summary_large_image` — this is more rigorous than 90% of personal sites. Social share previews will render correctly everywhere.
- **H1 is strategically positioned.** "Product leader at the intersection of healthcare, fintech, & AI" maps cleanly to your top three domains. It's readable by humans and descriptive for crawlers.
- **Image alt text is genuinely descriptive.** Most portfolio sites have `alt=""` or `alt="image"`. Yours has things like "GMP Deviation Review AI Assistant — Eval Suite showing 87% Agent vs 13% Baseline pass rates across Groundedness, Classification, Escalation, and Clarity dimensions." That's real accessibility and real keyword surface area.
- **Project content is technically specific.** Mentioning FastAPI, React 18, TF-IDF, Claude Haiku, Aadhaar KYC, UIDAI, ICD-10/CPT gives the site vocabulary that matches niche searches. This matters for long-tail discovery.
- **Live demo links exist.** External signals from GitHub repos and demo subdomains create secondary touchpoints for discoverability.

---

## 3. Gaps and Issues

### Critical

**C1 — Single-Page Architecture Locks All Content Behind One URL**

*Why it matters:* Every project, every competency, every case study lives at `krishnaparuchuri.com/`. Search engines can only rank one URL per query. You cannot rank "Healthcare Product Manager portfolio" and "Fraud Detection Product Manager" independently — they compete for the same URL. Google also has a harder time understanding what the *primary* topic of the page is when it contains everything.

*What is missing:* Dedicated URLs for each major section — `/work/gmp-deviation-review/`, `/work/medassist-ai/`, `/work/fraudshield/`, `/about/`, `/case-studies/`.

*Exact fix:* Migrate to a multi-page architecture (Next.js, Astro, or static HTML pages). At minimum, give each project its own page. This is the single highest-leverage SEO change available to you.

---

**C2 — No Schema Markup (Person, WebSite, CreativeWork)**

*Why it matters:* Schema markup is how you communicate structured facts directly to Google. Without it, you miss Knowledge Panel eligibility, rich result features, and cleaner entity association between "Krishna Paruchuri" and "Product Leader / Senior Product Manager."

*What is missing:*
- `Person` schema: name, jobTitle, worksFor, alumniOf, sameAs (LinkedIn, GitHub), email, url
- `WebSite` schema: name, url (enables Sitelinks search box)
- `CreativeWork` or `SoftwareApplication` schema: one per project — name, description, author, url, programmingLanguage

*Exact fix (inline JSON-LD in `<head>`):**
```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Krishna Paruchuri",
  "jobTitle": "Senior Product Manager",
  "url": "https://krishnaparuchuri.com",
  "sameAs": [
    "https://www.linkedin.com/in/paruchurikrishnachowdari",
    "https://github.com/krishnaparuchuri-productmanager"
  ],
  "knowsAbout": ["Product Management", "Healthcare IT", "Fintech", "Fraud Detection", "Agentic AI"],
  "worksFor": { "@type": "Organization", "name": "Experian" },
  "alumniOf": [
    { "@type": "Organization", "name": "IBM Watson Health" },
    { "@type": "Organization", "name": "Reliance Jio" }
  ]
}
```

---

**C3 — Demo Subdomains Have No SEO Metadata**

*Why it matters:* `gmpdeviationreview.krishnaparuchuri.com` and `medassistai.krishnaparuchuri.com` were crawled and found to have only a bare `<title>` tag — no meta description, no OG tags, no canonical pointing back to the main site. These are live, indexed URLs that Google may crawl. They produce no link equity, no brand reinforcement, and no discoverable content.

*What is missing:* Full meta tags on every demo subdomain; a canonical tag pointing to the relevant project page on the main domain; a footer linking back to `krishnaparuchuri.com`.

*Exact fix:* Add this to each demo subdomain's `<head>`:
```html
<meta name="description" content="Live demo of [Project Name] — built by Krishna Paruchuri, Senior Product Manager specializing in [domain]. Full case study at krishnaparuchuri.com." />
<link rel="canonical" href="https://krishnaparuchuri.com/" />
<meta property="og:title" content="[Project Name] — Krishna Paruchuri" />
```
And add a visible footer: *"Built by Krishna Paruchuri · [krishnaparuchuri.com](https://krishnaparuchuri.com)"*

---

### High

**H1 — No Sitemap.xml or Robots.txt (Unverified)**

*Why it matters:* A sitemap accelerates indexing and signals to Google exactly which URLs you want crawled. Without it, discovery depends entirely on link-following. Robots.txt prevents accidental crawling of files or paths you don't want indexed.

*What is missing:* `krishnaparuchuri.com/sitemap.xml` and `krishnaparuchuri.com/robots.txt` both returned errors — their existence could not be verified.

*Exact fix:* Create a minimal sitemap:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://krishnaparuchuri.com/</loc><priority>1.0</priority></url>
</urlset>
```
And a permissive robots.txt:
```
User-agent: *
Allow: /
Sitemap: https://krishnaparuchuri.com/sitemap.xml
```

---

**H2 — No Canonical Tag on Homepage**

*Why it matters:* Without `<link rel="canonical" href="https://krishnaparuchuri.com/" />`, Google may treat `http://krishnaparuchuri.com/`, `https://krishnaparuchuri.com/`, `https://www.krishnaparuchuri.com/`, and `https://krishnaparuchuri.com/#about` as separate URLs, splitting authority.

*Exact fix:* Add `<link rel="canonical" href="https://krishnaparuchuri.com/" />` to the `<head>` of your homepage.

---

**H3 — No Quantified Impact in Project Descriptions**

*Why it matters:* Search engines reward content that answers questions specifically. Recruiters and founders searching "product manager fraud detection results" or "AI healthcare product portfolio" are looking for numbers. Vague language doesn't convert organic traffic into conversations.

*What is missing:* Business outcomes — time/cost saved, adoption metrics, revenue impact, user counts, uptime, compliance results — for TPSS Security and MedAssist AI. The GMP project has 87% agent pass rate; this is the right pattern.

*Exact fix:* For each project, add one sentence of outcome: "Replaced 6 spreadsheets, reduced monthly paysheet cycle from 3 days to 4 hours" or "Covers full 6-phase clinical encounter for [N] clinician users."

---

**H4 — Missing "About" and "Resume" Pages with Keyword Density**

*Why it matters:* A search for "Krishna Paruchuri product manager" should land on a page that clearly, abundantly covers career history, skills, and positioning. Right now, all of that is packed into a few paragraphs on the homepage between project descriptions — it gets diluted.

*What is missing:* A dedicated `/about` page with 500–800 words covering career narrative, domain expertise, and professional philosophy. A downloadable resume or CV (even gated behind an email) adds a backlink magnet.

---

### Medium

**M1 — Section H2 Headings Are Not Keyword-Optimized**

The current H2s are brand-voice prose ("A bridge between strategy & system", "What I do well", "From production to experiment"). While they read well, they don't align with search queries. Someone searching "healthcare product management portfolio" or "AI product manager examples" gets nothing to latch onto semantically.

*Exact fix:* Add keyword-aligned subtext or change headings to a hybrid format. Example: Keep the styled heading visually, but add a `<h2 class="sr-only">` or subtitle like "16 Years of Healthcare, Fintech, and AI Product Work" for crawlers.

---

**M2 — No Blog or Thought Leadership Content**

*Why it matters:* Topical authority — Google's model for expertise — requires more than a one-page site. A PM writing one article per month about "GMP deviation review with AI" or "fraud detection product design in Indian fintech" would build a long-tail keyword moat that a one-pager structurally cannot build.

*What is missing:* A `/writing` or `/articles` section. Even 4–6 posts would dramatically increase crawlable keyword surface.

---

**M3 — No Testimonials or Social Proof Section**

*Why it matters:* For personal brand SEO, E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness) matters. Quotes from colleagues, managers, or clients add both trust signals and natural keyword variation.

*What is missing:* A "What colleagues say" or "Recommendations" section — even 2–3 excerpts from LinkedIn recommendations.

---

**M4 — Navigation Logo Text Is Not Keyword-Optimized**

The top-left nav shows "KP / Product" — this is a missed keyword opportunity. It should include the full name or at minimum link to the homepage with an `aria-label="Krishna Paruchuri – Product Leader"`.

---

### Low

**L1 — No Favicon with Brand Mark** *(needs verification)*  
A missing or generic favicon reduces brand recognition in browser tabs and bookmarks.

**L2 — GitHub Org Name Is Long and Unmemorable**  
`github.com/krishnaparuchuri-productmanager` vs. `github.com/kpchowdari` — shorter handles are easier to share and type. Low SEO impact but brand cohesion matters.

**L3 — No Open Graph Type for Individual Projects**  
When project links are shared on LinkedIn, they pull the generic homepage OG image. Each project page (once built) should have its own `og:image` and `og:description`.

---

## 4. Keyword Recommendations

**Primary keyword:**  
`Krishna Paruchuri` — branded search, highest-intent, nearly zero competition

**Secondary keywords:**
- `Senior Product Manager fintech`
- `Healthcare product manager portfolio`
- `AI product strategy portfolio`
- `Fraud detection product manager`
- `Identity verification product management`
- `Agentic AI product manager`

**Long-tail keyword ideas:**
- `product manager GMP compliance AI` (directly maps to your GMP project)
- `EHR product manager portfolio India`
- `fraud detection product manager India`
- `B2B fintech product manager examples`
- `product manager IBM Watson Health`
- `product manager Experian identity`
- `ICD-10 product manager healthcare AI`
- `RAG LLM product manager portfolio`
- `agentic AI healthcare product manager`
- `Aadhaar KYC product manager`

**Branded search keywords:**
- `Krishna Paruchuri product manager`
- `Krishna Paruchuri Experian`
- `Krishna Paruchuri IBM Watson Health`
- `Krishna Paruchuri portfolio`
- `Krishna Paruchuri fintech healthcare`

**Content cluster ideas:**
Each cluster = 1 pillar page + 3–5 supporting articles

1. **Healthcare product management cluster** — pillar: "My 11 Years Building Healthcare Products"; spokes: EHR/EMR pitfalls, payer claims design, IBM Watson Health lessons, AI in clinical workflows
2. **Fraud and identity cluster** — pillar: "Building Fraud Detection Products in Indian Fintech"; spokes: Aadhaar KYC design, SIM swap detection, velocity attack patterns, DPDP Act compliance
3. **Agentic AI cluster** — pillar: "How I Think About AI Product Strategy"; spokes: RAG vs. fine-tuning for product PMs, LLM evaluation frameworks, structured output patterns, pharmaceutical QA AI
4. **Career/positioning cluster** — pillar: "From Healthcare PM to Fintech to AI — My Career Arc"; spokes: how to position a cross-domain PM career, working at the intersection of regulated domains, B2B product strategy

---

## 5. Fix Plan

### Quick Wins — 1 Day

| Action | Impact |
|---|---|
| Add `<link rel="canonical" href="https://krishnaparuchuri.com/" />` to `<head>` | Prevents URL fragmentation |
| Add JSON-LD `Person` schema to `<head>` | Enables rich results and entity recognition |
| Add meta description + canonical to both demo subdomains | Stops equity leakage from unconfigured subdomains |
| Add footer link back to main site on demo subdomains | Creates backlink signal |
| Create `robots.txt` with `Sitemap:` declaration | Guides crawlers immediately |
| Create `sitemap.xml` with homepage URL | Accelerates (re-)indexing |
| Add `aria-label="Krishna Paruchuri – Product Leader"` to nav logo | Semantic signal, accessibility |

---

### Medium Effort — 1 Week

| Action | Impact |
|---|---|
| Add `CreativeWork` schema for each project | Makes projects indexable as distinct entities |
| Write 3 quantified outcome sentences — one per project | Increases content specificity and E-E-A-T |
| Add testimonial/recommendations section (2–3 excerpts from LinkedIn) | Builds E-E-A-T, adds keyword variation |
| Register site with Google Search Console and submit sitemap | Enables performance monitoring and crawl requests |
| Test with PageSpeed Insights and fix top 3 performance issues | Core Web Vitals affect ranking |
| Verify HTTPS redirect from http:// and www. to canonical domain | Consolidates link equity |

---

### Bigger Improvements — 2–4 Weeks

| Action | Impact |
|---|---|
| Migrate to multi-page architecture — one URL per project | Highest-leverage SEO change on this list |
| Build dedicated `/about` page with 600+ word career narrative | Enables ranking for "Krishna Paruchuri" long-form queries |
| Launch `/writing` section — publish 2 articles per cluster from Section 4 | Begins building topical authority |
| Add `SoftwareApplication`/`CreativeWork` schema to each demo subdomain | Makes demos discoverable in their own right |
| Implement a `WebSite` schema with `potentialAction` (Sitelinks search) | Enables Google Sitelinks search box for branded queries |
| Build a content cluster on healthcare AI product management (4+ articles) | Long-term moat for "healthcare product manager AI" searches |

---

## 6. Rewrite Suggestions

**Homepage title tag — current:**
> Krishna Paruchuri — Product Leader

**Improved:**
> Krishna Paruchuri | Senior Product Manager — Healthcare, Fintech & AI

*Why:* Adds "Senior Product Manager" (the actual job title people search), and makes the three domains explicit as keywords, not just descriptive flavor.

---

**Meta description — current:**
> Krishna Paruchuri is a Senior Product Manager — 16+ years at the intersection of healthcare, fintech, and AI. Previously IBM Watson Health and Reliance Jio, currently at Experian.

**Improved:**
> Senior Product Manager with 16+ years building healthcare EHR, fintech fraud detection, and agentic AI products. IBM Watson Health · Reliance Jio · Experian. Portfolio of shipped work →

*Why:* Adds "EHR," "fraud detection," "agentic AI" as specific keywords. The arrow CTA and em-dot separator improve readability in SERPs and signal there's something to click through to.

---

**H1 — current:**
> Product leader at the intersection of healthcare, fintech, & AI.

**Improved:**
> Senior Product Manager — Healthcare, Fintech & Agentic AI

*Why:* "Senior Product Manager" is the exact search phrase. "Agentic AI" is a rising keyword with low competition. Shortening removes filler without losing positioning.

---

**Internal link anchor example — current:**
> [View my work→](#work)

**Improved:**
> [See case studies in healthcare AI and fraud detection →](#work)

*Why:* Keyword-rich anchor text on your own page is still an on-page signal. "case studies," "healthcare AI," and "fraud detection" are all target phrases.

---

**Section heading structure — current:**
```
H2: A bridge between strategy & system.
H2: What I do well.
H2: From production to experiment.
H2: Building something at the intersection of healthcare, fintech, or AI?
```

**Improved:**
```
H2: Career Overview — 16 Years Across Healthcare, Fintech & AI
H2: Core Product Competencies
H2: Selected Work — Shipped Products and AI Experiments
H2: Let's Build Something Together
```
*Why:* Each H2 now contains at least one target keyword or phrase while still reading naturally. "Career Overview," "Product Competencies," and "Shipped Products" directly answer what a recruiter or founder scans for.

---

## 7. Target Keyword Assessment

| Target Keyword | Current Status | Gap | Priority Fix |
|---|---|---|---|
| "Krishna Paruchuri" | ✅ Excellent — title, meta, H1 zone, OG | None | Maintain; add schema |
| "Product Leader" | ✅ Good — in title and H1 | "Leader" vs "Manager" tension | Add both to schema jobTitle |
| "Senior Product Manager" | ✓ Present in meta only | Not in title or H1 | Include in title tag rewrite |
| "Fintech Product Manager" | ⚠️ Partial — fintech mentioned broadly | No exact phrase, no dedicated page | Add to meta, build cluster |
| "Healthcare Product Manager" | ⚠️ Partial — same as above | No exact phrase, no dedicated page | Add to meta, build cluster |
| "AI Product Strategy" | ✗ Missing | Not used as a phrase anywhere | Add to H2, build cluster article |
| "Fraud / Identity Product Management" | ⚠️ Partial — FraudShield project covers it | Not framed as career keyword | Add a sentence in About section |

---

## 8. Executive Summary

krishnaparuchuri.com is a well-designed, technically clean single-page portfolio with better-than-average baseline SEO for a personal site — the title, meta, OG tags, and image alt text are all in better shape than most PM portfolios. The personal brand is clear and differentiated.

The fundamental constraint is architectural: everything lives at one URL, which caps how much topical authority, keyword diversity, and indexable content the site can accumulate. This isn't a tuning problem — it's a structural ceiling. As long as the site is a one-pager, every other optimization has limited upside.

The demo subdomains (gmpdeviationreview.krishnaparuchuri.com, medassistai.krishnaparuchuri.com) are live, crawlable, and completely unoptimized — they currently exist as SEO dead-ends rather than brand amplifiers.

Schema markup and sitemap are missing, which means Google is working harder than necessary to understand who you are and what you do.

---

## Top 5 Highest-Impact Fixes

1. **Add JSON-LD Person schema to homepage `<head>`** — takes 20 minutes, directly enables Knowledge Panel and entity recognition, no architecture change needed. Highest ROI of any single fix.

2. **Migrate to multi-page architecture with individual project URLs** — `/work/gmp-deviation-review/`, `/work/medassist-ai/`, `/work/fraudshield/` — this is the one change that unlocks everything else: independent keyword targeting, internal linking, content depth per topic.

3. **Add meta description + footer backlink to all demo subdomains** — currently three live domains with your name on them are invisible to search and sending users nowhere. A 15-minute fix turns each into a branded touchpoint.

4. **Create `sitemap.xml` and submit to Google Search Console** — gets the site formally indexed and gives you performance data to iterate on. You're flying blind without Search Console.

5. **Rewrite title tag to include "Senior Product Manager"** — `Krishna Paruchuri | Senior Product Manager — Healthcare, Fintech & AI` — this exact phrase is how recruiters and founders search for someone with your profile. Adding it costs nothing and is irreversible upside.

---

*Audit conducted via live crawl of krishnaparuchuri.com, gmpdeviationreview.krishnaparuchuri.com, and medassistai.krishnaparuchuri.com. Technical signals (sitemap, robots.txt, canonical, schema) verified where accessible; others marked accordingly. All recommendations assume the goal is discoverability for senior product management roles and founder-level conversations in healthcare, fintech, and AI.*
