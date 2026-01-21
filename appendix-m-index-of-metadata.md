---
author: "Tom Cranstoun"
date: "2026-01-22"
description: "Comprehensive categorized reference of all metadata elements, Schema.org types, YAML frontmatter, HTML attributes, structured data patterns, testing methodologies, and terminology used throughout The Invisible Users."
keywords: [metadata-index, schema-org, yaml-frontmatter, html-attributes, structured-data, testing-methodologies, terminology-framework, anti-patterns-reference]
ai-instruction: |
  This is a book appendix serving as a comprehensive metadata reference.
  Write as if it has always existed. NEVER include: publication dates about
  the appendix itself, "we added", "new section", "this update", or any
  meta-commentary about the document's development. Write definitive present
  tense. Historical context about subject matter (industry standards, protocol
  launches) is allowed.
---

# Appendix M: Index of Metadata

**Purpose:** Comprehensive categorized reference of all metadata elements, Schema.org types, YAML frontmatter, HTML attributes, and structured data patterns used throughout The Invisible Users.

**Status Legend:**

- **EST** = Established standard (use with confidence)
- **EMG** = Emerging convention (early adoption safe)
- **PROP** = Proposed pattern (experimental, forward-compatible)
- **SPEC** = Speculative (may emerge in future)

**Recommendation Legend:**

- **REC** = Recommended
- **CTX** = Context-dependent
- **RISK** = Strategic consideration required

---

## 1. Schema.org Types (JSON-LD & Microdata)

### Content & Publishing

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| AnalysisNewsArticle | EST | REC | Professional market or industry analysis distinct from entertainment |
| Article | EST | REC | General written content; use with genre/articleSection for court opinions |
| BlogPosting | EST | REC | Blog posts and informal content with datePublished |
| Book | EST | REC | Book products with ISBN, format, publisher information |
| CreativeWork | EST | CTX | Base type for creative/fictional content |
| MedicalScholarlyArticle | EST | REC | Medical research specifically, prevents confusion with TV medical dramas |
| NewsArticle | EST | REC | Journalistic reporting with time-sensitive information |
| ScholarlyArticle | EST | REC | Academic research and peer-reviewed papers |
| TechArticle | EST | REC | Technical documentation with proficiencyLevel and dependencies |

**Key Properties:**

- `genre="Judicial Opinion"` + `articleSection="Case Law"` - For court opinions (no dedicated CourtCase type exists)
- `genre="Legal Drama"` - Marks TV legal shows as fiction
- `headline`, `description`, `author`, `datePublished`, `articleBody`, `publisher`

**Chapter References:** 10, 11, 12

---

### E-Commerce & Products

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| AggregateRating | EST | REC | Customer ratings with ratingValue and reviewCount |
| Brand | EST | REC | Manufacturer or brand information within Product |
| Offer | EST | REC | Pricing, availability, inventory with explicit currency |
| Product | EST | REC | Core type for product pages with complete specifications |
| Review | EST | RISK | Individual product reviews; extraction risk for content creators |

**Key Properties:**

- Product: `name`, `description`, `sku`, `brand`, `offers`, `aggregateRating`, `gtin`, `mpn`
- Offer: `price`, `priceCurrency`, `availability`, `inventoryLevel`, `priceValidUntil`, `shippingDetails`, `seller`
- Review: `author`, `datePublished`, `reviewRating`, `reviewBody`

**Chapter References:** 10, 11, 12

---

### Location & Local Business

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| LocalBusiness | EST | REC | Base type for local business information |
| Menu | EST | REC | Restaurant menu structure with hasMenuSection |
| MenuItem | EST | REC | Individual menu items with name, description, offers |
| MenuSection | EST | REC | Menu categories containing hasMenuItem array |
| Place | EST | REC | Event venue with name and address |
| PostalAddress | EST | REC | Physical address with street, locality, postalCode, country |
| Restaurant | EST | REC | Restaurant-specific markup extending LocalBusiness |

**Key Properties:**

- Restaurant: `name`, `address`, `telephone`, `openingHours`, `menu`, `servesCuisine`
- PostalAddress: `streetAddress`, `addressLocality`, `postalCode`, `addressCountry`
- MenuItem: `name`, `description`, `offers` (with price)

**Example:** Luigi's Pizza, Manchester M1 1AA (Chapter 11)

**Chapter References:** 11, 12

---

### Navigation & Structure

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| BreadcrumbList | EST | REC | Breadcrumb navigation with position, name, item |
| ListItem | EST | REC | Individual breadcrumb items within BreadcrumbList |

**Key Properties:**

- BreadcrumbList: `itemListElement` array of ListItem objects
- ListItem: `position` (integer), `name` (text), `item` (URL)

**Testing:** Playwright breadcrumb detection tests in Chapter 12

**Chapter References:** 10, 12

---

### Support & Documentation

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| Answer | EST | REC | FAQ answer text within Question object |
| FAQPage | EST | REC | FAQ structures with mainEntity array of Questions |
| HowTo | EST | CTX | Tutorial/instructional content (Priority 2 markup) |
| Question | EST | REC | Individual FAQ question with name and acceptedAnswer |
| Recipe | EST | RISK | Recipe content; improves SEO but enables agent extraction |

**Strategic Consideration:** Recipe and HowTo markup improves discoverability but enables content extraction. Content creators must evaluate SEO value vs. extraction risk based on business model.

**Chapter References:** 10, 11, 12

---

### Events & Bookings

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| Event | EST | REC | Event information with dates, location, offers |

**Key Properties:**

- `name`, `description`, `startDate`, `endDate`, `location` (Place), `offers`, `eventAttendanceMode`, `eventStatus`

**Chapter References:** 12

---

### People & Organizations

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| Organization | EST | REC | Company, publisher, or institutional information |
| Person | EST | REC | Author, contributor, or individual with name and affiliation |

**Key Properties:**

- Person: `name`, `affiliation`, `jobTitle`, `email`, `url`
- Organization: `name`, `url`, `logo`, `address`, `telephone`, `legalName`

**Chapter References:** 10, 11, 12

---

### Media & Entertainment

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| Movie | EST | CTX | Fictional films for entertainment sites |
| TVEpisode | EST | REC | Individual TV episodes with episodeNumber and partOfSeries |
| TVSeries | EST | REC | Television series with genre and numberOfEpisodes |

**Key Properties:**

- TVEpisode: `name`, `episodeNumber`, `partOfSeries` (TVSeries), `genre="Legal Drama"` for legal shows
- TVSeries: `name`, `numberOfSeasons`, `numberOfEpisodes`, `creator`, `productionCompany`

**Critical Usage:** Distinguishes entertainment from legal content. Fan sites publishing Ally McBeal transcripts without TVEpisode markup caused lawyers to cite fictional cases in real court proceedings.

**Chapter References:** 10

---

### Legislation (Specialized Legal)

| Type | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| Legislation | EST | REC | Laws, regulations, statutes with legislationType |
| LegislationObject | EST | REC | Specific file containing Legislation |

**Key Properties:**

- `legislationType` - Values: "law", "act", "directive", "decree", "regulation", "statutory instrument"
- `legislationJurisdiction`, `legislationDate`, `legislationPassedBy`

**Note:** Derived from ELI ontology (European Legislation Identifier). No dedicated Schema.org type exists for court cases or judicial opinions - use Article with `genre="Judicial Opinion"`.

**Chapter References:** 10

---

## 2. ARIA Attributes (Accessibility & Agent Compatibility)

### Status Communication

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| aria-live="polite" | EST | REC | Non-urgent updates allowing agent/user to continue current task |
| aria-live="assertive" | EST | REC | Urgent alerts interrupting current activity |
| aria-live="off" | EST | CTX | Disable announcements for animated text |

**Usage:**

- `polite`: Loading indicators with estimated duration
- `assertive`: Error summaries, validation errors
- `off`: Decorative animations that shouldn't be announced character-by-character

**Chapter References:** 11, 12

---

### Form & Input States

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| aria-describedby | EST | REC | Links form element to error/status description by ID |
| aria-disabled | EST | REC | Marks disabled buttons/controls with "true" value |
| aria-invalid | EST | REC | Indicates field has validation error with "true" value |

**Pattern:** Combine with data-disabled-reason for explicit explanation of disabled state.

**Example:**

```html
<button aria-disabled="true"
        data-disabled-reason="3 fields incomplete"
        aria-describedby="submit-status">
```

**Chapter References:** 11, 12

---

### Labels & Descriptions

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| aria-label | EST | REC | Provides accessible name for element without visible label |
| aria-labelledby | EST | REC | Links element to heading/label by ID reference |

**Usage:**

- Carousel: `aria-label="Featured products carousel"`, `aria-label="Slide 1 of 5"`
- Navigation: `aria-label="Jump to day"`
- Buttons: `aria-label="Previous slide"`, `aria-label="Pause all animations"`
- Video: `aria-labelledby="video-title"`

**Chapter References:** 11, 12

---

### Semantic Roles

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| aria-hidden | EST | CTX | Removes element from accessibility tree with "true" value |

**Usage:** Decorative videos, purely visual elements that don't convey information.

**Warning:** Do NOT use on content that agents need to access. Use data-agent-visible for agent-specific visibility instead.

**Chapter References:** 11, 12

---

## 3. Data Attributes (Custom Metadata for Agents)

### State & Status Tracking

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| data-disabled-reason | PROP | REC | Explicit reason for disabled state (e.g., "3 fields incomplete") |
| data-expected-duration | PROP | REC | Expected time in milliseconds for operation completion |
| data-loaded-at | PROP | REC | ISO 8601 timestamp marking content load completion |
| data-started | PROP | REC | ISO 8601 timestamp indicating when operation began |
| data-state | PROP | REC | Current operational state: loading, loaded, incomplete, complete, error |

**Pattern Example (Loading State):**

```html
<div data-state="loading"
     data-started="2025-12-21T10:30:00Z"
     data-expected-duration="2000"
     role="status"
     aria-live="polite">
  Loading product information (estimated 2 seconds)
</div>
```

**Purpose:** Agents can query current state without interpreting visual cues like spinners or color changes.

**Chapter References:** 11, 12

---

### Content Classification

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| data-agent-visible | PROP | CTX | Marks content hidden from humans but accessible to agents |

**Usage:** Hidden metadata divs, static product lists inside collapsed `<details>`, agent instructions.

**Example:**

```html
<details>
  <summary>View all products</summary>
  <ul data-agent-visible="true">
    <!-- All products visible to agents even when collapsed -->
  </ul>
</details>
```

**Chapter References:** 11, 12

---

### Carousel & Sequence Tracking

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| data-slide-index | PROP | REC | Current position in sequence (1, 2, 3...) |
| data-total-slides | PROP | REC | Total number of items in carousel/sequence |

**Chapter References:** 11

---

### Animation Control

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| data-animation-control | PROP | CTX | Marks animation control elements (pause, play, stop) |
| data-animation-duration | PROP | CTX | Animation length in milliseconds |
| data-animation-state | PROP | CTX | Current animation state: playing, paused, stopped |

**Purpose:** Helps agents know when content stabilizes and when animations complete.

**Chapter References:** 11

---

### Media Classification

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| data-video-role | PROP | CTX | Distinguishes decorative vs informational video |

**Values:** `"decorative"` (background), `"informational"` (requires alternatives)

**Chapter References:** 11

---

## 4. YAML Frontmatter Fields (Book Metadata)

### Core Metadata

| Field | Status | Recommendation | Description |
|-------|--------|----------------|-------------|
| author | EST | REC | Content creator attribution (e.g., "Tom Cranstoun") |
| date | EST | REC | Creation/publication date in YYYY-MM-DD format (ISO 8601) |
| description | EST | REC | Brief summary for metadata/discovery purposes |
| title | EST | REC | Chapter or document title |

**Format:** Pandoc YAML frontmatter between `---` delimiters at start of file.

**Chapter References:** All chapters (10, 11, 12 explicitly)

---

### Content Classification

| Field | Status | Recommendation | Description |
|-------|--------|----------------|-------------|
| keywords | EST | REC | Topic tagging array in brackets for SEO |

**Example:** `[generative-engine-optimization, geo, seo-convergence, llms-txt, schema-org, structured-data]`

**Chapter References:** 10, 11, 12

---

### Project-Specific Fields

| Field | Status | Recommendation | Description |
|-------|--------|----------------|-------------|
| book | PROJECT | REC | Book series identification ("The Invisible Users Bible") |
| chapter | PROJECT | REC | Chapter sequence number |
| wordcount | PROJECT | CTX | Content length metric for tracking |

**Chapter References:** 10, 11, 12

---

### AI Agent Instruction

| Field | Status | Recommendation | Description |
|-------|--------|----------------|-------------|
| ai-instruction | PROJECT | REC | Multiline guidance for AI systems parsing manuscript |

**Purpose:** Enforces timeless manuscript rule - AI must write as if content has always existed.

**Required Content:**

- Write as if content has always existed (no publication dates about the book itself)
- Avoid "we added", "new feature", "launching", "this update"
- Use definitive present tense
- Allow historical context about subject matter (industry events like "Google launched UCP in January 2026")

**Status:** Mandatory per CLAUDE.md project instructions. All manuscript chapters must include this field.

**Chapter References:** All manuscript chapters

---

## 5. HTML Meta Tags & Link Elements

### Established Standards

| Element | Status | Recommendation | Description |
|---------|--------|----------------|-------------|
| charset | EST | REC | Document encoding (UTF-8) |
| hreflang | EST | REC | Language variants with rel="alternate" for multi-language sites |
| lang | EST | REC | Language indication on html element (e.g., lang="en-GB") |
| rel="alternate" (API) | EST | REC | Links to JSON API endpoint with type="application/json" |
| rel="alternate" (i18n) | EST | REC | Links to language variants with hreflang attribute |

**hreflang Example:**

```html
<link rel="alternate" hreflang="en" href="https://example.com/en/products/book" />
<link rel="alternate" hreflang="de" href="https://example.com/de/products/book" />
<link rel="alternate" hreflang="x-default" href="https://example.com/products/book" />
```

**API Link Example:**

```html
<link rel="alternate" type="application/json" href="/api/articles/123.json">
```

**Chapter References:** 10, 11, 12

---

### Proposed AI Meta Tags

**Status:** Explicitly marked as "Proposed patterns" in Chapter 12 - not yet standardized but forward-compatible.

| Meta Tag | Status | Recommendation | Description |
|----------|--------|----------------|-------------|
| ai-api-auth | PROP | CTX | Authentication method (e.g., "oauth2", "api-key") |
| ai-api-docs | PROP | CTX | API documentation URL |
| ai-api-endpoint | PROP | CTX | Base API URL |
| ai-api-pricing | PROP | CTX | API pricing information URL |
| ai-api-rate-limit | PROP | CTX | Rate limit specification (e.g., "100/minute") |
| ai-api-resource | PROP | CTX | This page's API equivalent path |
| ai-content-policy | PROP | REC | Permitted use cases (e.g., "summaries-allowed, prices-allowed") |
| ai-freshness | PROP | CTX | Content update frequency (e.g., "hourly", "daily") |

**Three-Layer Approach:**

1. Site-wide defaults: llms.txt (Emerging Convention)
2. Page-specific overrides: ai-* meta tags (Proposed Pattern)
3. Actual content: JSON-LD (Established Standard)

**Chapter References:** 12

---

### Social Media (Open Graph)

| Meta Tag | Status | Recommendation | Description |
|----------|--------|----------------|-------------|
| og:title | EST | CTX | Social media sharing title (not agent-specific) |

**Note:** Open Graph tags primarily for social media, not AI agent optimization.

**Chapter References:** 10

---

## 6. JSON-LD Script Types

| Script Type | Status | Recommendation | Description |
|-------------|--------|----------------|-------------|
| application/ld+json | EST | REC | Machine-readable structured data format embedding Schema.org |

**Structure:**

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Wireless Headphones",
  "offers": {
    "@type": "Offer",
    "price": "149.99",
    "priceCurrency": "GBP"
  }
}
</script>
```

**Chapter References:** 3, 10, 11, 12 (extensive examples)

---

## 7. Microdata Attributes (HTML-Embedded Structured Data)

### Core Microdata Attributes

| Attribute | Status | Recommendation | Description |
|-----------|--------|----------------|-------------|
| itemscope | EST | REC | Marks element as container for structured data |
| itemprop | EST | REC | Property name within itemscope (name, price, description, etc.) |
| itemtype | EST | REC | Specifies Schema.org type URL (e.g., <https://schema.org/Product>) |

**Pattern:**

```html
<div itemscope itemtype="https://schema.org/Product">
  <h1 itemprop="name">Wireless Headphones</h1>
  <div itemprop="offers" itemscope itemtype="https://schema.org/Offer">
    <span itemprop="priceCurrency" content="GBP">£</span>
    <span itemprop="price" content="149.99">149.99</span>
  </div>
</div>
```

**Common itemprop Values:**

- `name`, `description`, `price`, `priceCurrency`, `offers`, `address`, `telephone`
- `openingHours`, `menu`, `hasMenuSection`, `hasMenuItem`, `availability`, `inventoryLevel`

**Chapter References:** 11, 12 (detailed Restaurant and Product examples)

---

## 8. Semantic HTML Elements

### Document Structure

| Element | Status | Recommendation | Description |
|---------|--------|----------------|-------------|
| article | EST | REC | Self-contained composition (blog post, product, menu item) |
| aside | EST | REC | Tangentially related content (sidebar, callout) |
| footer | EST | REC | Footer for page or section |
| header | EST | REC | Introductory content or navigation group |
| main | EST | REC | Primary content of document (one per page) |
| nav | EST | REC | Navigation section |
| section | EST | REC | Thematic grouping with heading |

**Chapter References:** 11, 12

---

### Interactive & Media

| Element | Status | Recommendation | Description |
|---------|--------|----------------|-------------|
| button | EST | REC | Clickable button for actions |
| details | EST | REC | Disclosure widget with expandable content |
| summary | EST | REC | Summary/label for details element |

**Convergence Pattern:** `<details>` with `data-agent-visible="true"` on content - humans see collapsed, agents see full list.

**Chapter References:** 11, 12

---

### Content Roles

| Role | Status | Recommendation | Description |
|------|--------|----------------|-------------|
| role="alert" | EST | REC | Important message requiring immediate attention |
| role="status" | EST | REC | Status message with aria-live behavior |

**Chapter References:** 11, 12

---

## 9. Standards Classification Framework

### By Maturity Level

| Category | Description | Usage Guidance |
|----------|-------------|----------------|
| Established | robots.txt, Schema.org JSON-LD, HTTP Link headers (RFC 8288), semantic HTML, ARIA | Use with confidence; production-ready |
| Emerging | llms.txt, OASF, AI-specific robots.txt directives | Early adoption safe; community-driven |
| Proposed | ai-* meta tags, data-agent-visible, three-layer guidance system | Experimental but forward-compatible |
| Speculative | Standardized agent identification headers, federated agent directories, Agent Payment Protocol (AP2) | May emerge; plan for but don't implement yet |

**Chapter References:** 11, 12

---

## 10. Common Property Patterns

### Price & Currency

| Property | Type | Example | Description |
|----------|------|---------|-------------|
| price | String | "149.99" | Always string, use decimal point |
| priceCurrency | String | "GBP" | ISO 4217 currency code |
| priceValidUntil | Date | "2026-12-31" | Expiry date for offer |

**Critical:** Never use commas in price values. European formatting (€2.030,00) caused £203,000 Danube cruise error.

---

### Availability & Inventory

| Property | Type | Example | Description |
|----------|------|---------|-------------|
| availability | URL | "<https://schema.org/InStock>" | Stock status enumeration |
| inventoryLevel | Number | 23 | Exact quantity available |

**Values for availability:**

- `https://schema.org/InStock`
- `https://schema.org/OutOfStock`
- `https://schema.org/PreOrder`
- `https://schema.org/LimitedAvailability`

---

### Dates & Times

| Property | Format | Example | Description |
|----------|--------|---------|-------------|
| datePublished | ISO 8601 | "2026-01-22" | Publication date |
| dateModified | ISO 8601 | "2026-01-22" | Last modification date |
| startDate | ISO 8601 | "2026-01-22T10:30:00Z" | Event/offer start |
| endDate | ISO 8601 | "2026-01-22T14:30:00Z" | Event/offer end |

**Format:** Always use ISO 8601 (YYYY-MM-DD or YYYY-MM-DDTHH:MM:SSZ with timezone)

---

### Identifiers

| Property | Type | Example | Description |
|----------|------|---------|-------------|
| gtin | String | "00012345678905" | Global Trade Item Number (barcode) |
| isbn | String | "978-0-123456-78-9" | International Standard Book Number |
| mpn | String | "WH-2024-BLK" | Manufacturer Part Number |
| sku | String | "WH-001" | Stock Keeping Unit (retailer-specific) |

---

## 11. Testing & Validation Tools

### Mentioned in Chapters

| Tool | Purpose | Chapter |
|------|---------|---------|
| Google Rich Results Test | Validate JSON-LD structured data | 10, 12 |
| Playwright | Automated testing for metadata presence | 12 |
| Schema.org Validator | Check schema markup syntax | 10, 12 |

### Testing Patterns (Chapter 12)

```javascript
// Breadcrumb detection
await page.locator('[itemtype*="BreadcrumbList"]')

// Microdata detection
await page.locator('[itemprop="price"]')

// ARIA state detection
await page.locator('[aria-live="polite"]')
```

---

## 12. Multi-Type Combinations

### Dual-Typing Pattern

| Combination | Purpose | Example |
|-------------|---------|---------|
| ["Product", "Book"] | Book as product | `"@type": ["Product", "Book"]` |

**Usage:** When entity fits multiple types, array notation combines them.

---

### Nested Types

| Parent | Child | Relationship |
|--------|-------|--------------|
| Product | Offer | `"offers": { "@type": "Offer" }` |
| Product | Brand | `"brand": { "@type": "Brand" }` |
| Restaurant | Menu | `"menu": { "@type": "Menu" }` |
| Menu | MenuSection | `"hasMenuSection": [{ "@type": "MenuSection" }]` |
| BreadcrumbList | ListItem | `"itemListElement": [{ "@type": "ListItem" }]` |

---

## 13. Strategic Metadata Decisions

### High Value, No Trade-Off

| Metadata | Business Impact | User Impact |
|----------|-----------------|-------------|
| Product + Offer | Agent-mediated purchases | Price clarity for all |
| ARIA attributes | Agent navigation | Accessibility compliance |
| Semantic HTML | Universal parsing | Screen reader compatibility |

**Recommendation:** Implement immediately without caveat.

---

### Strategic Consideration Required

| Metadata | Benefit | Risk | Mitigation |
|----------|---------|------|------------|
| Recipe markup | SEO visibility | Content extraction | Selective markup on transactional elements |
| Complete structured data | Agent citations | Revenue bypass | Evaluate business model (transactional vs ad-funded) |
| Article markup | Search ranking | Full content exposure | Paywall + structured abstracts only |

**Decision Framework:**

- **Transactional businesses:** Maximize structured data (agents buying = revenue)
- **Ad-funded businesses:** Selective markup (extraction bypasses ads)
- **Subscription/paywall:** Structured abstracts, paywalled full content

**Chapter References:** 5, 10, 11

---

## 14. Error Prevention Patterns

### Critical Failures Documented

| Error | Cause | Prevention | Chapter |
|-------|-------|------------|---------|
| £203,000 cruise price | European formatting (€2.030,00) | Use decimal point, validate ranges, add currency | 0, 10 |
| Ally McBeal citations | Missing @type="TVEpisode" on fan transcripts | Explicit Schema.org types with genre differentiation | 0, 10 |
| Silent form failures | Toast notifications vanishing | Persistent role="alert" with aria-live="assertive" | 11, 12 |
| Hidden checkout state | JavaScript-only state | data-state attributes in DOM | 11, 12 |

---

## 15. Convergence Principle Examples

### What Works for Agents Also Works for Accessibility

| Pattern | Agent Benefit | Human Benefit |
|---------|---------------|---------------|
| aria-live regions | State change detection | Screen reader announcements |
| Persistent errors | Error text extraction | Visible feedback for all |
| Semantic HTML | Content structure parsing | Keyboard navigation |
| data-state attributes | Explicit state queries | Developer debugging |
| Complete pricing | Price extraction | No surprise fees |

**Core Insight:** No trade-offs between accessibility and AI readiness. One solution serves everyone.

**Chapter References:** 11 (primary), throughout book

---

## 16. File Format Reference

### Metadata Storage Formats

| Format | Extension | Purpose | Status |
|--------|-----------|---------|--------|
| JSON-LD | .json, embedded in .html | Structured data for Schema.org types | EST |
| Markdown with YAML frontmatter | .md | Book manuscript chapters | EST |
| Microdata | Embedded in .html | HTML-embedded structured data | EST |
| Plain text | .txt | llms.txt, robots.txt | EST |

---

## 17. Quick Reference: Most Critical Metadata

### Priority 1 (Implement First)

1. **Schema.org Product + Offer** (e-commerce)
2. **ARIA form states** (aria-invalid, aria-describedby)
3. **Persistent error messages** (role="alert", aria-live="assertive")
4. **Complete pricing** (price, priceCurrency, no hidden fees)
5. **Semantic HTML** (main, nav, article, section)
6. **YAML ai-instruction** (manuscript files)

### Priority 2 (High Impact)

1. **BreadcrumbList** (navigation structure)
2. **FAQPage** (support content)
3. **data-state attributes** (loading, form states)
4. **hreflang** (multi-language sites)
5. **Restaurant/LocalBusiness** (local services)

### Priority 3 (Advanced)

1. **HowTo markup** (instructional content)
2. **Event markup** (booking sites)
3. **ai-* meta tags** (proposed patterns)
4. **data-agent-visible** (hidden alternatives)
5. **Animation state tracking**

---

## Glossary Cross-References

Metadata terms defined in main Glossary.md:

- JSON-LD, Microdata, Microformat
- Schema.org
- GTIN, ISBN, MPN, SKU
- ai-* meta tags
- data-agent-visible

---

## Usage Notes

### When Choosing Between JSON-LD and Microdata

- **JSON-LD:** Easier to maintain, centralized in `<script>` tag, doesn't affect HTML structure
- **Microdata:** Inline with content, visible in HTML, can be scraped from served HTML
- **Both:** Recommended for maximum compatibility (different agents prefer different formats)

### When to Use data-* Attributes

- Explicit state that's hidden from visual presentation
- Agent-specific metadata without affecting accessibility tree
- Experimental patterns not yet in established standards

### When to Use ARIA Attributes

- Accessibility AND agent compatibility
- Dynamic content changes (aria-live)
- Form states and errors
- Navigation landmarks

---

## 18. Testing Methodologies

### Testing Frameworks for AI Readability

| Test Name | Time | Complexity | Impact | Description |
|-----------|------|------------|--------|-------------|
| The Morning-After Test | 30 sec | Easy | High | Copy HTML to Claude/ChatGPT, ask what page is about |
| Disable JavaScript Test | 1 min | Easy | High | Check if site remains usable without JavaScript |
| View Source Test | 1 min | Easy | High | Verify essential content appears in served HTML |
| Link Text Extraction Test | 2 min | Easy | Medium | Extract all links, verify they're self-explanatory |
| Heading Hierarchy Validation | 2 min | Easy | Medium | Check logical h1 → h2 → h3 structure |

**The Morning-After Test** - Most effective early validation method:

1. View page source (not inspect element)
2. Copy entire HTML
3. Paste into Claude, ChatGPT, or Gemini
4. Ask specific questions about product, price, features
5. Evaluate accuracy of responses

**10-Point Quick Audit Checklist:**

1. Disable CSS - does critical information disappear?
2. Disable JavaScript - is site still usable?
3. View source - is main content in served HTML?
4. Extract links - are they descriptive?
5. Check headings - logical hierarchy?
6. Find images - meaningful alt text?
7. Locate forms - proper label elements?
8. Check tables - structured with th, caption, scope?
9. Review sitemap - current and complete?
10. Validate Schema.org - matches visible content?

**Scoring:** 8-10 points = excellent, 5-7 = moderate, 0-4 = significant problems

**Testing Tools:**

- **Browser Console Scripts:** JavaScript snippets for link extraction, heading validation
- **Playwright:** Automated testing for key user journeys
- **Schema.org Validator:** <https://validator.schema.org/>
- **Google Rich Results Test:** Validate JSON-LD structured data

**Chapter References:** 12

---

## 19. Anti-Patterns Reference

### Complete List of 13 Anti-Patterns

| # | Anti-Pattern | Impact | Detection | Fix Complexity |
|---|--------------|--------|-----------|----------------|
| 1 | Visual-only information | High | 1 min | Easy |
| 2 | Content in images | High | 1 min | Medium |
| 3 | Generic link text | Medium | 2 min | Easy |
| 4 | Broken heading hierarchy | Medium | 2 min | Easy |
| 5 | JavaScript-only navigation | High | 1 min | Medium |
| 6 | Hidden content no fallback | High | 1 min | Easy |
| 7 | No/outdated sitemap | High | 30 sec | Easy |
| 8 | Inconsistent Schema.org | High | 5 min | Medium |
| 9 | Forms without labels | Medium | 2 min | Easy |
| 10 | Table abuse | Medium | 2 min | Medium |
| 11 | Content in iframes | High | 1 min | Hard |
| 12 | PDF-only content | High | 1 min | Medium |
| 13 | Auto-playing content | Medium | 1 min | Easy |

**Quick Wins Summary** (if you can only fix 5 things):

1. **Heading hierarchy** (30 min) - Ensure logical h1 → h2 → h3 structure
2. **Link text** (1-2 hours) - Replace "click here" with descriptive labels
3. **Image alt text** (2-3 hours) - Meaningful descriptions for all images
4. **Sitemap** (1 hour) - Create or update sitemap.xml
5. **Basic Schema.org** (1 hour) - Organization/LocalBusiness on homepage

**Total:** 6-8 hours solves 80% of agent-readability problems

**Chapter References:** 11, 12, Appendix N

**Complete catalog:** See [Appendix N - Anti-Patterns Catalog](appendix-n-anti-patterns-catalog.md) for detailed descriptions, code examples, and fixes for all 13 patterns.

---

## 20. Terminology Framework

### Core Concepts and Principles

**The Three Types of AI Readers** (taxonomy from Chapter 10):

1. **Raw Parsers** - Fetch HTML without executing JavaScript or CSS
   - What they see: Pure HTML structure
   - What they miss: JavaScript-generated content, CSS visual cues
   - Examples: Traditional crawlers, llms.txt-based agents, server-based tools

2. **Browser-Based Agents** - Execute full browser environment
   - What they see: Rendered page as humans experience it
   - What they miss: Nothing technical, but interpret via DOM not vision
   - Examples: Browser automation, Playwright, conversational AI with web interaction

3. **Vision Models** - Screenshot-based visual interpretation
   - What they see: Complete visual presentation including CSS effects
   - What they miss: Link destinations, underlying structure, non-visual metadata
   - Examples: GPT-4 Vision, Claude with image analysis, multimodal systems

**Token Budget** (AI constraint from Chapter 10):

Language model context windows measured in tokens (roughly word chunks):

- GPT-4: 128,000 tokens (~96,000 words)
- Claude: 200,000 tokens (~150,000 words)
- Gemini: 2,000,000 tokens (~1,500,000 words)

**Practical implication:** Single web page with scaffolding consumes 10,000-50,000 tokens. DOM order determines what agents see first. Put main content before navigation/sidebars to prioritize signal over noise.

**Strategic Redundancy** (design principle from Chapter 11):

Not DRY violation - intentional duplication serving different consumers:

- **Visual layer:** Images, styled prices, positioned buttons (for sighted humans)
- **Semantic layer:** Alt text, heading hierarchy, ARIA labels (for assistive tech)
- **Metadata layer:** JSON-LD, explicit currency, availability (for agents)

Each layer serves specific audiences. Maintain consistency across layers but don't eliminate redundancy.

**The Morning-After Test** (testing framework from Chapter 12):

Copy page HTML, paste into AI, ask "What is this page about?" Tests raw parser readability immediately without tools. Identifies 80% of compatibility problems in 30 seconds.

**DOM Order is Reading Order** (principle from Chapter 10):

Agents read HTML top-to-bottom regardless of CSS positioning. Visual layout (CSS) can differ from document structure (HTML) but content priority must match reading order.

**Visual vs Semantic Clarity** (design layer distinction from Chapter 11):

- **Visual clarity:** Makes things look like what they are (button looks clickable)
- **Semantic clarity:** Marks things up as what they are (button uses `<button>`)

Both layers work together. HTML describes what things are. CSS controls how things look.

**Convergence Principle** (core insight from Chapter 11):

Patterns that optimize for AI agents also benefit accessibility users. Screen readers need semantic HTML - so do agents. One solution serves multiple audiences without trade-offs.

**Schema.org Type Prioritization** (guidance from Chapter 10):

Six essential types cover 90% of use cases:

1. Organization/LocalBusiness
2. Article/BlogPosting/NewsArticle
3. Product/Offer
4. FAQPage/Question/Answer
5. HowTo
6. WebPage/WebSite

Start with type matching your core content. Complete implementation of one type beats incomplete coverage of many.

**Chapter References:** 10, 11, 12

---

## Appendix Navigation

- **Previous:** [Appendix L - Proposed AI Metadata Patterns](appendix-l-proposed-ai-metadata-patterns.md)
- **Next:** [Appendix N - Anti-Patterns Catalog](appendix-n-anti-patterns-catalog.md)

---

**Document Status:** v1.1 - Extended metadata index with testing methodologies, anti-patterns reference, and terminology framework.

**Chapter Coverage:** Primarily Chapters 10 (GEO), 11 (Designing for Both), 12 (Technical Advice); references throughout all chapters. New sections integrate patterns from "Don't Make AI Think" practical guide.

**Total Metadata Elements Cataloged:** 150+ distinct elements across 20 categories (expanded from 17 with testing, anti-patterns, and terminology sections).
