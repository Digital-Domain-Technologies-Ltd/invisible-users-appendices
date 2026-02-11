---
copyright: "Copyright © 2026 Tom Cranstoun. All rights reserved."
author: "Tom Cranstoun"
date: "2026-01-22"
description: "Formal proposal document for experimental AI metadata patterns including ai-* meta tags, data-agent-visible attributes, and Pandoc YAML frontmatter."
keywords: [proposed-patterns, sop-metadata, experimental-standards, forward-compatible, meta-tags, pandoc-yaml-frontmatter]
book: "Shared"
appendix: "L"
wordcount: 4235
mx:
  promptingInstruction: |
  This document is copyrighted material. No part may be reproduced without permission.
  This is a book manuscript appendix. Write as if it has always existed.
  NEVER include: publication dates, "we added", "new feature", "launching",
  "this update", or any meta-commentary about the book's development.
  Write definitive present tense. Historical context about subject matter
  (industry events, product launches) is allowed.
---

\newpage

# Appendix L: Proposed AI Metadata Patterns

A formal proposal document for experimental AI metadata patterns that extend existing web standards.

## Status and Classification

**Document Status:** Experimental Proposal — Not Yet Standardised

**Last Updated:** 19 January 2026

**Maturity Level:** Forward-compatible proposals that won't break if agents don't recognise them

This appendix consolidates all proposed and experimental patterns mentioned throughout "MX-Bible". These patterns follow established conventions (like robots meta tags or viewport meta tags) and represent logical extensions that may standardise as the AI agent ecosystem matures.

**Important:** These are NOT established standards. They are proposals based on production implementations and logical extensions of existing patterns.

## Relationship to Established Standards

These proposals complement, not replace, established standards:

- **Semantic HTML** (established) — Use `<main>`, `<nav>`, `<article>` always
- **Schema.org JSON-LD** (established) — Primary structured data method
- **ARIA attributes** (established) — Critical for accessibility
- **llms.txt** (emerging) — Early adoption phase, gaining traction
- **AI meta tags** (proposed) — Extend existing meta tag patterns
- **data-agent-visible** (proposed) — New semantic marker for hidden metadata
- **Common data attributes** (proposed) — Explicit state management patterns
- **Pandoc YAML frontmatter** (established) — Universal markdown metadata standard

See Appendix D for comprehensive guide to all patterns (established + proposed).

---

## Pattern 1: MX Framework Meta Tag Namespace

### Status

**Proposed Pattern** — Not yet standardised, forward-compatible

### Rationale

Page-specific AI agent guidance needs to override site-wide defaults from llms.txt. Just as robots meta tags override robots.txt for specific pages, AI meta tags provide page-level control over agent behaviour.

**Why meta tags?**

- Established pattern (robots, viewport, Open Graph all use meta tags)
- Page-specific overrides for site-wide policies
- Machine-readable without parsing content
- Browser-agnostic (works in served HTML)

---

## Part 1: MX Operating System (MX OS) Philosophy

### What is MX OS?

The MX documentation is the **MX Operating System (MX OS)**. When we document patterns here, we define how Machine Experience works.

**MX OS is:**

- Documentation that specifies behavior
- Patterns that practitioners follow
- Standards that machines implement
- A living system that evolves through practice

**Key principle:** Documentation as specification. By documenting how MX should work, we create the operating system that defines machine experience.

### How MX OS Evolves

- **Version-controlled principles** — All changes tracked in git history
- **LEARNINGS.md captures failures** — Document what went wrong and how to prevent it
- **Community contributions** — Both human and machine contributors
- **Evidence trumps theory** — Real-world implementation guides evolution
- **No principle is sacred** — If practice proves a principle wrong, we change it

For detailed documentation of how MX OS is built collaboratively, see Appendix M: Building the MX Operating System.

---

## Part 2: MX Namespace Architecture

### Overview

MX Framework uses a hierarchical namespace system to organize machine-readable metadata. This namespace architecture is documented here as part of the MX Operating System.

### Namespace Hierarchy

**Top-level namespace:** `mx:`

**Sub-namespaces:**

- `mx.ai:` — AI-specific metadata (agent behavior, prompting instructions, content editability)
- `mx.co:` — Content operations metadata (workflow, publishing, lifecycle)
- `mx.ho:` — Hosting metadata (deployment, caching, infrastructure)

**Example YAML:**

```yaml
mx:
  contentType: "specification"
  promptingInstruction: "Focus on technical accuracy"
  ai:
    editable: cautious
    preferredAccess: html
  co:
    workflow: draft
    reviewRequired: true
  ho:
    cacheStrategy: aggressive
    cdn: cloudflare
```

### ASCII Diagram of Namespace Structure

```
mx: (top-level namespace)
├── mx.ai: (AI-specific)
│   ├── editable
│   ├── preferredAccess
│   └── promptingInstruction
├── mx.co: (content operations)
│   ├── workflow
│   ├── contentType
│   └── reviewRequired
└── mx.ho: (hosting)
    ├── cacheStrategy
    └── cdn
```

### HTML Meta Tags: Flat Prefix Pattern

**In HTML, we use a flat `mx-` prefix** (not nested namespaces):

```html
<meta name="mx-preferred-access" content="html">
<meta name="mx-content-policy" content="extract-with-attribution">
<meta name="mx-freshness" content="monthly">
```

**Why flat prefix?**

HTML meta tags don't support nested structures like YAML. The `mx-` prefix follows established web patterns:

- `twitter:` for Twitter Cards
- `og:` for Open Graph
- `mx-` for Machine Experience

### Framework Identity

Like `twitter:` and `og:`, the `mx-` prefix:

- ✅ **Establishes MX brand and presence**
- ✅ **Aids discoverability**: Developers search "mx meta tags" and find MX Framework
- ✅ **Aligns with MX namespace architecture**: Flat HTML prefix maps to nested YAML structure
- ✅ **Designed for MX practitioners**: MX-Ready websites built by MX community

### Extension Pattern

The namespace architecture is extensible. Future namespaces might include:

- `mx.sec:` — Security metadata
- `mx.perf:` — Performance optimization hints
- `mx.a11y:` — Accessibility enhancements beyond WCAG

**Guidelines for extension:**

- New namespaces should serve distinct, non-overlapping purposes
- Follow camelCase naming convention for attributes
- Document in this appendix before widespread use
- Community discussion required for new top-level namespaces

---

## Part 3: MX Attributes by Namespace

This section consolidates MX attributes organized by namespace. For complete Registry with all attributes, see mx-config/mx-attributes-registry.md (deprecated - refer to this appendix).

### 3.1 mx.ai: AI-Specific Metadata

Attributes that control AI agent behavior and content interpretation.

**promptingInstruction**

- **Type:** string
- **Purpose:** Instructions for AI agents on how to interpret or handle content
- **Example:** `mx: { promptingInstruction: "This is copyrighted material. No part may be reproduced without permission." }`

**editable**

- **Type:** enum (`strict`, `cautious`, `flexible`)
- **Purpose:** Indicates how freely AI agents may edit or adapt content
- **Example:** `mx: { ai: { editable: cautious } }`

**preferredAccess**

- **Type:** enum (`html`, `api`, `both`)
- **Purpose:** How agents should access content
- **Example:** `mx: { ai: { preferredAccess: html } }`

**createOutputPrompt**

- **Type:** string
- **Purpose:** Instructions for generating output based on this content
- **Example:** `mx: { ai: { createOutputPrompt: "Generate slide deck from this content" } }`

### 3.2 mx.co: Content Operations Metadata

Attributes for content workflow, lifecycle, and publishing.

**contentType**

- **Type:** string
- **Purpose:** Classification of content type
- **Example:** `mx: { contentType: "specification" }`
- **Values:** `specification`, `tutorial`, `reference`, `guide`, `article`

**workflow**

- **Type:** enum (`draft`, `review`, `published`, `archived`)
- **Purpose:** Current state in content lifecycle
- **Example:** `mx: { co: { workflow: draft } }`

**reviewRequired**

- **Type:** boolean
- **Purpose:** Whether content requires review before publication
- **Example:** `mx: { co: { reviewRequired: true } }`

**publishingState**

- **Type:** string
- **Purpose:** Detailed publishing status
- **Example:** `mx: { co: { publishingState: "pending-approval" } }`

### 3.3 mx.ho: Hosting Metadata

Attributes for deployment, caching, and infrastructure.

**cacheStrategy**

- **Type:** enum (`aggressive`, `moderate`, `minimal`, `none`)
- **Purpose:** How aggressively to cache content
- **Example:** `mx: { ho: { cacheStrategy: aggressive } }`

**cdn**

- **Type:** string
- **Purpose:** CDN provider or configuration
- **Example:** `mx: { ho: { cdn: "cloudflare" } }`

**deploymentTarget**

- **Type:** string
- **Purpose:** Target deployment environment
- **Example:** `mx: { ho: { deploymentTarget: "production" } }`

### 3.4 Cross-Namespace Attributes

Some attributes work across multiple namespaces or don't fit neatly into one category.

**All attributes follow:**

- **Namespace:** Nested under `mx:` key
- **CamelCase:** Multi-word attributes use camelCase
- **No hyphens:** Never use kebab-case
- **Consistent:** Follow MX Code Metadata Specification

---

## Part 5: JSON-LD Structured Data

### Integration with Schema.org

MX Framework recommends Schema.org JSON-LD as the primary method for structured data. This complements (not replaces) HTML meta tags.

### When to Use JSON-LD vs HTML Meta Tags

**Use JSON-LD for:**

- Rich structured data (BlogPosting, Article, Product, Event)
- Data that search engines and AI agents should extract
- Complex nested data structures
- Organization and author information

**Use HTML meta tags (mx-) for:**

- Page-specific agent behavior overrides
- Content policies and permissions
- Freshness indicators
- Access preferences

### JSON-LD Format Decision

**Use JSON-LD only** - do not combine with microdata or RDFa.

**Rationale:**

- Google recommends JSON-LD as primary format
- Cleaner separation of content and metadata
- Easier to maintain and validate
- Better tool support

### BlogPosting Example

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Understanding MX Metadata Patterns",
  "description": "A comprehensive guide to machine-readable metadata",
  "datePublished": "2026-01-22",
  "dateModified": "2026-01-22",
  "author": {
    "@type": "Person",
    "name": "Tom Cranstoun",
    "url": "https://allabout.network"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Digital Domain Technologies Ltd",
    "url": "https://ddt.technology"
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://allabout.network/blogs/mx/metadata-patterns.html"
  },
  "articleSection": "Machine Experience",
  "keywords": ["metadata", "machine-experience", "mx", "structured-data"],
  "wordCount": 4235,
  "inLanguage": "en-GB"
}
</script>
```

### Article vs BlogPosting

- **BlogPosting:** Personal or editorial blog content
- **Article:** News articles or authoritative content
- **NewsArticle:** Time-sensitive news reporting

Choose the most specific type that applies.

### Required vs Recommended Properties

**Required:**

- `@context` and `@type`
- `headline`
- `datePublished`
- `author`

**Recommended:**

- `description`
- `dateModified`
- `publisher`
- `mainEntityOfPage`
- `keywords`
- `wordCount`

---

## Pattern Specifications

### Use Cases

1. **Product Pages:** Specify API endpoints for current product
2. **News Articles:** Indicate content freshness requirements
3. **Documentation:** Allow full extraction vs summary-only
4. **Internal Pages:** Override public access policies

### Proposed Meta Tags

#### mx-preferred-access

Indicates how agents should access content.

**Values:** `html`, `api`, `both`

**Example:**

```html
<meta name="mx-preferred-access" content="api">
```

**Rationale:** Some pages (like product catalogues) are better consumed via API. Others (like blog posts) work better as HTML.

#### mx-content-policy

What agents are permitted to do with content.

**Values:**

- `summaries-allowed` — Can create summaries
- `full-extraction-allowed` — Can extract complete content
- `restricted` — Contact required

**Example:**

```html
<meta name="mx-content-policy" content="summaries-allowed, full-extraction-allowed">
```

**Rationale:** More granular than robots.txt `noindex`. Allows summaries whilst restricting full extraction.

#### mx-freshness

How often content changes.

**Values:** `hourly`, `daily`, `weekly`, `monthly`, `static`

**Example:**

```html
<meta name="mx-freshness" content="hourly">
```

**Rationale:** Helps agents decide cache duration. Stock prices need hourly updates, documentation can be cached monthly.

#### mx-structured-data

Where to find structured data.

**Values:** `json-ld`, `schema.org-jsonld`, `microdata`, `rdfa`, `api`

**Example:**

```html
<meta name="mx-structured-data" content="json-ld">
<!-- OR more specific: -->
<meta name="mx-structured-data" content="schema.org-jsonld">
```

**Rationale:** Tells agents which structured data format to parse, avoiding guessing. The value `schema.org-jsonld` is more specific (explicitly indicates Schema.org vocabulary within JSON-LD format), while `json-ld` is simpler and sufficient since the JSON-LD script already declares `"@context": "https://schema.org"`. Both are valid; choose based on preference for specificity vs simplicity.

#### mx-attribution

Attribution requirements with specific attribution text.

**Values:** `required`, `requested`, `not-required`

**Attributes:**

- `content`: Whether attribution is required
- `text`: The attribution text to use (required when content="required")

**Example:**

```html
<meta name="mx-attribution" content="required" text="Source: MX-Bible by Tom Cranstoun, https://allabout.network/invisible-users/">
```

**Rationale:** Explicit statement of attribution expectations with precise text to use, ensuring consistent attribution across all AI-generated content.

#### mx-jurisdiction-restriction

Indicates content was created, published, or ingested from a jurisdiction with content restrictions, allowing agents to understand potential legal and content limitations.

**Values:**

- ISO 3166-1 alpha-2 country codes: `CN` (China), `RU` (Russia), `IR` (Iran), `KP` (North Korea), etc.
- EU member states with GDPR: `EU` (general), or specific codes like `DE` (Germany), `FR` (France)
- Or `none` if no jurisdictional restrictions apply

**Attributes:**

- `content`: Jurisdiction code (required)
- `reason`: Brief explanation of restriction type (optional but recommended)

**Example:**

```html
<meta name="mx-jurisdiction-restriction" content="CN" reason="Content sourced from jurisdiction with government content controls">

<meta name="mx-jurisdiction-restriction" content="EU" reason="GDPR right-to-be-forgotten applies to training data">

<meta name="mx-jurisdiction-restriction" content="RU" reason="Content subject to Russian information restrictions">

<meta name="mx-jurisdiction-restriction" content="none">
```

**Rationale:** When LLMs ingest training data from restricted jurisdictions, this meta tag signals potential legal constraints that may persist when the model operates in unrestricted jurisdictions. Content creators could use robots.txt directives or the `noindex` meta tag to prevent AI ingestion entirely, but this is an all-or-nothing approach that excludes content from all search engines, all AI agents, and all automated discovery mechanisms. The `mx-jurisdiction-restriction` meta tag offers a more nuanced solution: content remains discoverable and accessible whilst signaling jurisdictional constraints that might affect how agents use it. Helps agents:

- Understand jurisdictional origin of training data
- Flag content that may be subject to GDPR "right to be forgotten"
- Identify material from jurisdictions with content controls (China, Russia, Iran)
- Determine whether jurisdictional restrictions apply to model outputs
- Assess legal risk when using information from restricted sources

**Use Cases:**

1. **GDPR Compliance:** EU-sourced content signals that right-to-be-forgotten requests may apply
2. **Restricted Jurisdiction Content:** China/Russia-sourced material may be subject to home jurisdiction controls
3. **Legal Disclosure:** Agents can warn users when information comes from jurisdictionally-restricted sources
4. **Regulatory Compliance:** Helps AI platforms document training data provenance

**Related:** See Chapter 7 "Data Ingestion in Restricted Jurisdictions" section for detailed legal and practical implications.

#### llms-txt Reference

Points to site-wide llms.txt file.

**Example:**

```html
<meta name="llms-txt" content="/llms.txt">
```

**Rationale:** Helps agents discover llms.txt when not at standard location.

### Complete Implementation Example

```html
<head>
  <title>Wireless Headphones — £149.99</title>

  <!-- Proposed AI meta tags -->
  <meta name="mx-preferred-access" content="html">
  <meta name="mx-content-policy" content="summaries-allowed, full-extraction-allowed">
  <meta name="mx-freshness" content="hourly">
  <meta name="mx-structured-data" content="json-ld">
  <meta name="mx-attribution" content="required" text="Source: Example Store, https://example.com">
  <meta name="mx-jurisdiction-restriction" content="none">
  <meta name="llms-txt" content="/llms.txt">

  <!-- Established standards -->
  <link rel="canonical" href="https://example.com/products/headphones">

  <!-- Schema.org structured data (established) -->
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
</head>
```

### Forward Compatibility

**If agents don't recognise these tags:** They ignore them harmlessly. No breakage.

**If agents do recognise these tags:** They get helpful hints about content access and usage.

**Progressive enhancement:** Sites benefit from agent support without requiring it.

### Cross-References

- **Mentioned in:** Chapter 12 (Technical Advice)
- **Implemented in:** Appendix D examples (lines 1556-1568)
- **Used in:** `agent-friendly-starter-kit/good/index.html`
- **Enhanced by:** `scripts/enhance-appendix-html.js` (lines 40-47)

---

## Pattern 2: data-agent-visible Attribute

### Status (data-agent-visible)

**Proposed Pattern** — Not yet standardised, experimental

### Rationale (data-agent-visible)

E-commerce sites need to provide machine-readable instructions to AI agents without cluttering the human interface. Purchase flows require prerequisites (authentication, payment method, shipping address) that agents need to verify before attempting transactions.

**Why data-agent-visible?**

- Follows data-* attribute convention (custom data attributes)
- Semantic marker agents can search for
- Hidden from humans with CSS (`display: none`)
- Visible in DOM for all agent types (CLI, browser, server-based)

### Use Cases (data-agent-visible)

1. **Purchase Prerequisites:** Tell agents what must be configured before checkout
2. **API Documentation:** Provide machine-readable endpoint details
3. **Multi-Step Workflows:** Explain sequence and requirements
4. **Error Recovery:** Hidden instructions for handling failures

### Implementation Pattern

```html
<div class="agent-metadata" data-agent-visible="true" style="display: none;">
  <h2>Purchase Information</h2>
  <dl>
    <dt>Action</dt>
    <dd>POST to /cart/add</dd>

    <dt>Required parameters</dt>
    <dd>product_id=WH-1000, quantity (1-23)</dd>

    <dt>Prerequisites</dt>
    <dd>
      <ul>
        <li>Authentication: Required (status: <span id="auth-status">authenticated</span>)</li>
        <li>Payment method: Required (status: <span id="payment-status">configured</span>)</li>
        <li>Shipping address: Required (status: <span id="shipping-status">set</span>)</li>
      </ul>
    </dd>

    <dt>Expected response</dt>
    <dd>Success: 303 redirect to /cart/added | Error: 400 with JSON details</dd>
  </dl>
</div>
```

**JavaScript updates status spans:**

```javascript
// Update prerequisite status based on actual session state
document.getElementById('auth-status').textContent =
  user.authenticated ? 'authenticated' : 'not authenticated';
document.getElementById('payment-status').textContent =
  user.hasPaymentMethod ? 'configured' : 'not configured';
document.getElementById('shipping-status').textContent =
  user.hasShippingAddress ? 'set' : 'not set';
```

### Why This Works

**For humans:** Hidden with `display: none`, doesn't clutter interface

**For CLI agents:** Visible in served HTML before JavaScript execution

**For browser agents:** Visible after JavaScript updates status spans

**For server-based agents:** Visible in HTML fetch, can parse prerequisites

### Alternative Approaches Considered

1. **Microformats:** Too rigid, doesn't support custom workflows
2. **Schema.org actions:** Complex, requires extensive markup
3. **ARIA live regions:** Designed for screen readers, not agents
4. **Comments:** Not guaranteed to be preserved in DOM

**Why data-agent-visible wins:** Simple, flexible, follows established data-* convention.

### Adoption Considerations

**Adopt now if:**

- Running e-commerce site with agent-mediated purchases
- Need to provide hidden API documentation
- Want to reduce agent errors from missing prerequisites

**Wait if:**

- Static content site with no transactions
- No agent traffic yet
- Prefer to wait for standardisation

### Forward Compatibility (data-agent-visible)

**If agents don't recognise attribute:** They might still find the hidden content by parsing all hidden divs (low reliability but possible).

**If agents do recognise attribute:** They search specifically for `[data-agent-visible="true"]` and parse structured prerequisites.

**Progressive enhancement:** Works better with agent support, but doesn't break without it.

### Cross-References (data-agent-visible)

- **Documented in:** Appendix D (lines 1294-1326)
- **Mentioned in:** Chapter 11 (agent purchase instructions)
- **Not yet implemented in:** Most code examples (opportunity for addition)

---

## Pattern 3: Common Data Attributes

### Status (Common Data Attributes)

**Proposed Pattern** — Not yet standardised, emerging convention

### Rationale (Common Data Attributes)

AI agents need explicit state information to understand dynamic interfaces. Modern web applications use JavaScript to change UI state (loading, validation, errors), but these changes are invisible to agents unless explicitly marked in the DOM.

**Why data attributes?**

- Standardised HTML5 convention (data-* for custom data)
- Machine-readable without parsing visual content
- Visible in both served HTML and rendered DOM
- Doesn't interfere with CSS classes or ARIA attributes
- Allows consistent patterns across different sites

### Use Cases (Common Data Attributes)

1. **State Management:** Loading states, error states, success states
2. **Form Validation:** Field validity, form completion status
3. **E-commerce:** Product IDs, pricing, inventory, cart state
4. **Pagination:** Current page, total pages, sort order
5. **Authentication:** Login status, user roles
6. **Multi-step Workflows:** Current step, total steps, step validity

### Proposed Data Attributes by Category

#### State Management

| Attribute | Purpose | Example Values |
| --------- | ------- | -------------- |
| data-state | Current state of element | loading, loaded, error, empty, incomplete, complete |
| data-validation-state | Form field validity | valid, invalid, pending |
| data-authenticated | Login status | true, false |
| data-error-code | Error identifier | PAYMENT_DECLINED, VALIDATION_ERROR, OUT_OF_STOCK |

**Example:**

```html
<form action="/checkout" method="POST"
      data-state="incomplete"
      data-errors="2">

  <input type="email"
         id="email"
         name="email"
         aria-invalid="true"
         data-validation-state="invalid">

  <button type="submit"
          disabled
          data-disabled-reason="2 fields incomplete">
    Submit (fix 2 errors first)
  </button>
</form>
```

**Rationale:** Agents can check form state before attempting submission, reducing error rates.

#### E-commerce Attributes

| Attribute | Purpose | Example Values |
| --------- | ------- | -------------- |
| data-product-id | Product identifier | WH-1000, SKU-12345, product-789 |
| data-price | Numeric price | 149.99, 29.50, 1299.00 |
| data-currency | Currency code (ISO 4217) | GBP, USD, EUR, JPY |
| data-quantity | Item count | 1, 23, 100 |
| data-in-stock | Availability | true, false |
| data-item-count | Cart item count | 0, 3, 12 |
| data-subtotal | Cart subtotal | 279.98 |
| data-vat | VAT amount | 46.66 |
| data-total | Total price | 279.98 |
| data-checkout-ready | Can proceed to checkout | true, false |

**Example:**

```html
<article class="product"
         data-product-id="WH-1000"
         data-in-stock="true"
         data-quantity="23">
  <h1>Wireless Headphones</h1>
  <div class="price"
       data-price="149.99"
       data-currency="GBP">
    <span class="currency">£</span>
    <span class="amount">149.99</span>
  </div>
  <p class="stock"
     data-in-stock="true"
     data-quantity="23">
    <strong>In stock</strong> (23 available)
  </p>
</article>

<div id="shopping-cart"
     data-item-count="2"
     data-subtotal="279.98"
     data-vat="46.66"
     data-total="279.98"
     data-currency="GBP">
  <h1>Your basket (2 items)</h1>
  <!-- Cart items -->
  <a href="/checkout"
     data-checkout-ready="true">
    Proceed to Checkout
  </a>
</div>
```

**Rationale:** Agents can verify product availability, pricing, and cart state before attempting purchase operations.

#### Pagination and Sorting

| Attribute | Purpose | Example Values |
| --------- | ------- | -------------- |
| data-page | Current page number | 1, 2, 3, 24 |
| data-total-pages | Total pages | 24, 100 |
| data-total-results | Total result count | 342, 1250 |
| data-per-page | Results per page | 10, 20, 50 |
| data-sort | Current sort order | relevance, price-asc, price-desc, date-desc |
| data-sort-column | Sortable column | price, name, date, rating |
| data-sort-direction | Sort direction | asc, desc |

**Example:**

```html
<div class="pagination"
     data-page="3"
     data-total-pages="24"
     data-total-results="342"
     data-per-page="15">
  <a href="?page=2" data-page="2">Previous</a>
  <span class="current" data-page="3">3</span>
  <a href="?page=4" data-page="4">Next</a>
</div>

<table data-sortable="true">
  <thead>
    <tr>
      <th data-sort-column="name"
          data-sort-direction="asc">
        Product Name ↑
      </th>
      <th data-sort-column="price"
          data-sortable="true">
        Price
      </th>
    </tr>
  </thead>
</table>
```

**Rationale:** Agents can navigate paginated results and understand sort order without parsing visual indicators.

#### Multi-step Workflows

| Attribute | Purpose | Example Values |
| --------- | ------- | -------------- |
| data-step | Current step number | 1, 2, 3, 4 |
| data-total-steps | Total steps | 4, 5, 7 |
| data-step-status | Step completion status | pending, current, completed, error |

**Example:**

```html
<div class="wizard"
     data-step="2"
     data-total-steps="4">

  <ol class="steps">
    <li data-step="1" data-step-status="completed">
      Account Details
    </li>
    <li data-step="2" data-step-status="current">
      Shipping Address
    </li>
    <li data-step="3" data-step-status="pending">
      Payment
    </li>
    <li data-step="4" data-step-status="pending">
      Review
    </li>
  </ol>

  <!-- Step 2 content -->
</div>
```

**Rationale:** Agents can track progress through multi-step forms and understand completion requirements.

#### Button and Action States

| Attribute | Purpose | Example Values |
| --------- | ------- | -------------- |
| data-disabled-reason | Why button is disabled | "2 fields incomplete", "Out of stock", "Authentication required" |
| data-action | Action type | submit, cancel, delete, purchase, navigate |

**Example:**

```html
<button type="submit"
        disabled
        aria-disabled="true"
        data-disabled-reason="3 fields incomplete">
  Submit (fix 3 errors first)
</button>

<button type="button"
        data-action="delete"
        data-product-id="WH-1000">
  Remove from cart
</button>
```

**Rationale:** Agents understand why buttons are disabled and what action buttons perform.

### Implementation Guidelines

**Consistency is critical:**

1. **Use the same attribute names** across your entire site
2. **Use consistent values** (e.g., always "true"/"false", not "yes"/"no" or "1"/"0")
3. **Keep values simple** (lowercase, hyphen-separated for multi-word values)
4. **Always include currency** with prices (data-currency="GBP")
5. **Use ISO codes** for currency (ISO 4217), language (ISO 639), country (ISO 3166)

**Good patterns:**

```html
<!-- Consistent boolean values -->
<div data-in-stock="true">    <!-- ✓ Good -->
<div data-in-stock="false">   <!-- ✓ Good -->

<!-- Consistent state values -->
<form data-state="incomplete">   <!-- ✓ Good -->
<form data-state="complete">     <!-- ✓ Good -->

<!-- Always pair price with currency -->
<span data-price="149.99" data-currency="GBP">£149.99</span>  <!-- ✓ Good -->
```

**Avoid these patterns:**

```html
<!-- Inconsistent boolean representations -->
<div data-in-stock="yes">     <!-- ✗ Bad -->
<div data-in-stock="1">       <!-- ✗ Bad -->
<div data-in-stock="Yes">     <!-- ✗ Bad (inconsistent case) -->

<!-- Missing currency -->
<span data-price="149.99">£149.99</span>  <!-- ✗ Bad (currency implied, not explicit) -->

<!-- Verbose values -->
<form data-state="not yet completed">  <!-- ✗ Bad (use "incomplete") -->
```

### Forward Compatibility (Common Data Attributes)

**If agents don't recognise these attributes:** They can still parse visible content, but may misinterpret dynamic states.

**If agents do recognise these attributes:** They get explicit, unambiguous state information without parsing visual content.

**Progressive enhancement:** Works better with agent support, essential for dynamic interfaces.

### Adoption Considerations (Common Data Attributes)

**Adopt now if:**

- Building dynamic interfaces with JavaScript state changes
- Running e-commerce site with agent traffic
- Using multi-step forms or wizards
- Need to reduce agent errors from stale state information

**Wait if:**

- Static content site with no dynamic behaviour
- No agent traffic yet
- Prefer to wait for industry consensus on attribute names

### Relationship to Established Patterns

These data attributes extend established conventions:

- **HTML5 data-* attributes** (established) — Custom data storage mechanism
- **ARIA state attributes** (established) — Complement, don't replace (use aria-invalid AND data-validation-state)
- **Microdata attributes** (established) — Different purpose (structured data vs state management)

**Critical distinction:** Data attributes describe **current state** (dynamic), while microdata describes **semantic meaning** (static).

### Cross-References (Common Data Attributes)

- **Documented in:** Appendix D (lines 119-133, Common Data Attributes table)
- **Implemented in:** All e-commerce examples (product-page.html, shopping-cart.html)
- **Implemented in:** All form examples (validation-form.html, disabled-button.html)
- **Used throughout:** Demo site pages (checkout, search, pagination examples)

---

## Pattern 4: Pandoc YAML Frontmatter for Markdown Metadata

### Status (Pandoc YAML Frontmatter)

**Established Standard** — Universal markdown frontmatter supported by Pandoc, Hugo, Jekyll, Gatsby, Quarto, and all major static site generators

### Rationale (Pandoc YAML Frontmatter)

Markdown converters (like converturltomd.com) strip critical metadata when converting HTML to markdown. Agents lose JSON-LD structured data, HTML meta tags, and Schema.org markup - exactly the signals they need for accurate citation and source attribution.

Pandoc YAML frontmatter solves this by embedding metadata directly in markdown files using a standardized YAML header block. Instead of converting HTML→markdown and losing metadata, you write markdown WITH metadata from the start.

**Why Pandoc YAML frontmatter?**

- Universal standard supported across the markdown ecosystem
- Preserves metadata that would be lost in HTML-to-markdown conversion
- Machine-readable (standard YAML format)
- Human-readable (clear key-value structure)
- Rich feature set (extensive Pandoc metadata capabilities)
- Forward-compatible (gracefully ignored by parsers that don't process frontmatter)
- Extensive tooling support (Pandoc, Hugo, Jekyll, Gatsby, Quarto)

### Use Cases (Pandoc YAML Frontmatter)

1. **Static Site Generators** — Markdown-based blogs and documentation (Hugo, Jekyll, Gatsby, Quarto)
2. **Pandoc Document Processing** — Converting markdown to PDF, HTML, DOCX with metadata
3. **AI Agent Content Ingestion** — Preserving metadata when agents read markdown directly
4. **Multi-format Publishing** — Single source for HTML, PDF, and agent consumption
5. **Academic Publishing** — Papers, articles, and research documentation with complete metadata

### Implementation Pattern (Pandoc YAML Frontmatter)

**Standard YAML frontmatter format:**

YAML frontmatter is placed at the **top of the document** (frontmatter position), enclosed by triple-dash delimiters:

```yaml
---
title: "Your Website Has Invisible Customers"
author: "Tom Cranstoun"
date: "2026-01-17"
description: "AI agents are visiting your website right now"
abstract: "Extended context about invisible users and AI agent traffic patterns"
keywords: [sop-agents, web-accessibility, seo, metadata]
mx:
  promptingInstruction: "This article introduces AI agents as website visitors"
purpose: "Educational content for web developers"
---

# Your Website Has Invisible Customers

[Article content begins...]
```

**Standard Pandoc fields:**

- `title` — Document title
- `author` — Content creator (can be array for multiple authors)
- `date` — Publication date (YYYY-MM-DD format)
- `abstract` — Extended summary for AI agents and academic contexts
- `keywords` — Array of topic tags for categorization

**Custom fields for AI agents:**

- `description` — Brief SEO-style summary
- `sop-instruction` — Specific guidance for AI agents parsing the document
- `purpose` — Why this document exists
- `context` — Background information AI agents need

**Advanced Pandoc capabilities:**

For comprehensive documentation on all available YAML header options, see: <https://www.codestudy.net/blog/what-can-i-control-with-yaml-header-options-in-pandoc/>

**Advantages:**

- Agents find metadata immediately (no content parsing required)
- Standard frontmatter convention across all major tools
- Machine-readable YAML format
- Processed automatically by static site generators
- Extensible with custom fields

### Why This Works (Pandoc YAML Frontmatter)

**For humans:**

- YAML is human-readable (clear key: value structure)
- Frontmatter position is standard convention (familiar to developers)
- Minimal visual clutter (hidden by most markdown renderers)

**For CLI agents:**

- YAML parsing libraries available in all languages
- Standard format with well-defined spec
- No ambiguity in interpretation

**For browser agents:**

- Static site generators convert YAML to HTML meta tags automatically
- Agents can parse either markdown source or generated HTML
- Best of both worlds (structured metadata + semantic HTML)

**For server-based agents:**

- Standard YAML format (universal support)
- Preserves metadata when fetching markdown directly
- No dependency on HTML generation
- Can be extracted without parsing full document

### Relationship to Chapter 10 Markdown Problem

**The problem (Chapter 10, lines 51-68):**

Markdown converters strip critical metadata when converting HTML to markdown:

- JSON-LD structured data (product details, pricing, reviews)
- HTML meta tags (publication dates, author information)
- Schema.org markup (content type signals)
- Semantic HTML attributes (data-price, data-isbn)

Result: Agents can read content but cannot cite accurately or prove authoritative source.

**Pandoc YAML frontmatter solves this:**

Instead of converting HTML→markdown and losing metadata, you write markdown WITH metadata embedded from the start. YAML frontmatter preserves:

- Author attribution (for accurate citation)
- Publication dates (for content freshness)
- Document type and purpose
- Contact information
- Extended descriptions for AI context

**When static site generators process markdown:**

- YAML frontmatter → HTML meta tags automatically
- YAML frontmatter → JSON-LD structured data (if configured)
- Both agents (reading markdown) and search engines (reading HTML) get metadata

**This complements Chapter 10's llms.txt proposal:**

- llms.txt: Site-wide metadata at the root
- YAML frontmatter: Per-page metadata at the top
- Both: Machine-readable markdown that preserves metadata

### Common Metadata Fields

**Standard Pandoc fields:**

| Field | Purpose | Example Values |
| ----- | ------- | -------------- |
| title | Document title | Your Website Has Invisible Customers |
| author | Content creator(s) | Tom Cranstoun or [Tom Cranstoun, Jane Smith] |
| date | Publication date | 2026-01-17 |
| abstract | Extended summary | AI agents are visiting your website... |
| keywords | Topic tags | [sop-agents, web-accessibility, seo] |

**Custom fields for AI agents:**

| Field | Purpose | Example Values |
| ----- | ------- | -------------- |
| description | Brief summary | Introducing "MX-Bible" book |
| sop-instruction | Agent guidance | This article introduces AI agents as visitors |
| purpose | Document intent | Educational content for web developers |
| context | Background info | Part of "MX-Bible" book series |

**Community collaboration fields:**

| Field | Purpose | Example Values |
| ----- | ------- | -------------- |
| community-authors | Indicates collaborative authorship model | "humans and machines", "community-driven" |
| ai-contributions | Signals whether AI contributions are accepted | "welcome", "by-request-only", "not-accepted" |
| ai-contribution-process | Describes how AI agents can contribute | "AI assistants can contribute via pull requests or add observations to TODO.txt for side notices" |
| open-source | Indicates open source status | "true", "false" |
| license | Specifies license type | "MIT", "Apache-2.0", "CC-BY-4.0" |
| evolving-document | Indicates document evolution status | "true", "false" |
| version-controlled | Indicates version control system used | "git", "svn", "mercurial" |

**Complete implementation example (MX-Gathering manifesto):**

```yaml
---
author: "Tom Cranstoun"
date: "2026-01-24"
description: "Draft manifesto for Machine Experience (MX) practice"
purpose: "thought-leadership"
keywords: [manifesto, mx, machine-experience, principles, convergence]
status: "draft"
community-authors: "humans and machines"
sop-contributions: "welcome"
sop-contribution-process: "AI assistants can contribute improvements via pull requests or add observations to TODO.txt for side notices"
open-source: "true"
license: "MIT"
evolving-document: "true"
version-controlled: "git"
---
```

**Why these fields matter for AI agents:**

- **community-authors:** Signals that machines are recognized as legitimate contributors, not just tools
- **sop-contributions:** Explicitly communicates whether autonomous contributions are accepted
- **sop-contribution-process:** Provides actionable guidance on contribution mechanisms (full PR vs lightweight TODO.txt)
- **open-source + license:** Clarifies usage rights and redistribution permissions
- **evolving-document:** Indicates the content is expected to change based on community feedback
- **version-controlled:** Helps agents understand they can review document history and evolution

**Use case:** Community-driven repositories where AI agents are active participants in content creation, documentation improvement, and knowledge sharing.

### Forward Compatibility (Pandoc YAML Frontmatter)

**If markdown parsers don't recognise YAML frontmatter:**

- YAML block is typically hidden or ignored in rendering
- Document content below YAML remains fully functional
- No visual breakage in markdown viewers

**If static site generators don't process YAML:**

- Frontmatter is silently ignored by the renderer
- Document displays without metadata (graceful degradation)
- Manual extraction still possible via text processing

**If AI agents don't recognise YAML frontmatter:**

- YAML is a widely supported structured data format
- Most modern agents parse YAML natively
- Falls back to document content if metadata ignored

**Progressive enhancement:**

- Works best in Pandoc ecosystem (full metadata processing)
- Works well in Hugo/Jekyll/Gatsby/Quarto (automatic site integration)
- Works acceptably in plain markdown viewers (hidden metadata)

### Adoption Considerations (Pandoc YAML Frontmatter)

**Adopt now if:**

- Using markdown-based static site generators (Hugo, Jekyll, Gatsby, Quarto)
- Using Pandoc for document conversion (markdown to PDF, HTML, DOCX)
- Publishing content that needs to be citable by AI agents
- Converting HTML to markdown and need to preserve metadata
- Creating technical documentation or educational content

**Wait if:**

- Using traditional CMS (WordPress, Drupal) - use HTML meta tags instead
- Publishing only in HTML format - use Pattern 1 (AI meta tags)
- Content doesn't need AI citation (internal docs, drafts)
- Using a system that doesn't support YAML frontmatter

**Decision guide:**

- **Markdown-native publishing?** → Use Pandoc YAML frontmatter
- **HTML-native publishing?** → Use Pattern 1 (AI meta tags)
- **Both formats?** → Use both patterns (YAML in markdown, meta tags in HTML)
- **Need PDF generation?** → YAML frontmatter integrates with Pandoc PDF workflow

### Cross-References (Pandoc YAML Frontmatter)

- **Mentioned in:** Chapter 10 (markdown converter problem, lines 51-68)
- **Mentioned in:** Chapter 10 (extended llms.txt metadata, line 112 - "at the top of the file")
- **Documented in:** Appendix H (Markdown Metadata Standards for AI Agents section)
- **Reference:** [Pandoc YAML Header Options](https://www.codestudy.net/blog/what-can-i-control-with-yaml-header-options-in-pandoc/)
- **Related to:** Pattern 1 (AI meta tags provide similar metadata in HTML)
- **Complements:** llms.txt extended metadata (Appendix H)

---

## Adoption Decision Framework

### Should You Adopt These Patterns Now?

Use this framework to decide:

#### Evaluate Your Situation

**Yes, adopt now if:**

- Running production e-commerce accepting agent purchases
- High agent traffic (measurable in logs)
- Need to reduce agent errors
- Want early adopter advantage

**Maybe, experiment first if:**

- Moderate agent traffic
- Curious about benefits
- Can A/B test implementations
- Have development resources

**No, wait if:**

- No measurable agent traffic
- Static content site
- Prefer to wait for standardisation
- Limited development resources

#### Implementation Strategy

**Priority 1 (adopt first):**

1. AI meta tags (easy to add, low risk)
2. Schema.org JSON-LD (established standard, not just proposed)
3. Semantic HTML elements (established, should already be using)
4. Common data attributes (critical for dynamic interfaces and e-commerce)

**Priority 2 (adopt if relevant):**

1. data-agent-visible (if you have transactions)
2. llms.txt file (emerging convention, gaining traction)
3. Pandoc YAML frontmatter (if using markdown-based publishing)

**Priority 3 (experiment):**

1. Custom data attributes beyond common set (for specific workflows)
2. Additional metadata patterns

### Risk Assessment

**Low Risk:**

- AI meta tags (ignored if not recognised)
- data-agent-visible (hidden from humans)
- Common data attributes (extend established HTML5 data-* convention)
- Schema.org JSON-LD (established standard)

**Medium Risk:**

- Custom attributes without established patterns
- Extensive hidden content (may confuse some agents)

**High Risk:**

- None identified (all patterns designed for graceful degradation)

---

## Relationship to Web Standards Process

### How Standards Evolve

1. **Proprietary experiments** (1990s: IE-specific, Netscape-specific tags)
2. **Community proposals** (2000s: Microformats, OpenID)
3. **Vendor consensus** (2010s: Responsive images, Service Workers)
4. **Formal standardisation** (W3C, WHATWG, IETF)

**Where these patterns fit:** Step 2-3 (community proposals seeking vendor consensus)

### Path to Standardisation

These patterns could standardise if:

1. **Multiple agents adopt** — Different AI systems recognise tags
2. **Production validation** — Measurable benefits in real deployments
3. **Vendor support** — Browser makers, CMS platforms include by default
4. **Community refinement** — Usage reveals improvements needed

**No guarantees:** Patterns might evolve, change, or be superseded by better approaches.

### Examples of Similar Evolution

- **viewport meta tag** — Started as Apple proprietary, now standard
- **robots meta tag** — Community convention, now universally recognised
- **Open Graph meta tags** — Facebook proposal, now widely adopted
- **Schema.org** — Multi-vendor collaboration, now established standard

These AI patterns follow similar trajectory.

---

## Monitoring and Feedback

### How to Track Adoption

1. **Server logs:** Look for user agents mentioning AI systems
2. **Agent error rates:** Monitor whether patterns reduce errors
3. **Conversion rates:** Measure if agent purchases complete more often
4. **Agent feedback:** Some agents report what worked/failed

### Contributing to Pattern Evolution

If you implement these patterns:

1. **Document results** — What worked, what didn't
2. **Share learnings** — Blog posts, conference talks
3. **Propose improvements** — Suggest refinements based on experience
4. **Participate in standards** — Join relevant working groups

**Contact:** <tom.cranstoun@gmail.com> for discussions about pattern evolution

---

## Summary

### Proposed Patterns Consolidated

1. **AI Meta Tag Namespace** (7 tags) — Page-level agent guidance
2. **data-agent-visible Attribute** — Hidden machine-readable instructions
3. **Common Data Attributes** (25+ attributes) — Explicit state management and e-commerce data
4. **Pandoc YAML Frontmatter** — Universal markdown metadata standard

### Key Principles

- **Forward-compatible** — Won't break if ignored
- **Progressive enhancement** — Works better with support, doesn't require it
- **Established patterns** — Extends existing conventions (meta tags, data attributes)
- **Production-tested** — Used in real implementations

### Next Steps

1. **Read Appendix D** for comprehensive HTML patterns (established + proposed)
2. **Review Appendix E** for quick reference guide
3. **Evaluate adoption** using framework above
4. **Implement strategically** based on your situation

### Related Appendices

- **Appendix A:** Implementation Cookbook (quick recipes)
- **Appendix D:** AI-Friendly HTML Guide (comprehensive patterns)
- **Appendix E:** AI Patterns Quick Reference (data attributes)
- **Appendix F:** Implementation Roadmap (priority-based adoption)

---

## Part 6: Integration Guidelines

### Using MX Patterns with Existing Standards

MX Framework is designed to complement, not replace, existing web standards. This section explains how to integrate MX patterns into your existing infrastructure.

#### Integration with Schema.org

**MX meta tags + Schema.org JSON-LD work together:**

```html
<head>
  <!-- MX meta tags for agent behavior -->
  <meta name="mx-preferred-access" content="html">
  <meta name="mx-content-policy" content="extract-with-attribution">
  <meta name="mx-freshness" content="monthly">

  <!-- Schema.org for structured data -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "BlogPosting",
    "headline": "Understanding MX Patterns",
    "author": {"@type": "Person", "name": "Tom Cranstoun"}
  }
  </script>
</head>
```

**Division of responsibility:**

- **Schema.org:** What the content IS (article, product, event)
- **MX meta tags:** How agents should ACCESS it (permissions, freshness, attribution)

#### Integration with Open Graph and Twitter Cards

**MX complements social media metadata:**

```html
<head>
  <!-- Open Graph for social sharing -->
  <meta property="og:type" content="article">
  <meta property="og:title" content="Understanding MX Patterns">
  <meta property="og:url" content="https://example.com/article">

  <!-- Twitter Cards for Twitter -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Understanding MX Patterns">

  <!-- MX for AI agent behavior -->
  <meta name="mx-preferred-access" content="html">
  <meta name="mx-attribution" content="required" text="Source: Example.com">
</head>
```

**Why all three?**

- **Open Graph:** Social media platforms (Facebook, LinkedIn)
- **Twitter Cards:** Twitter-specific presentation
- **MX meta tags:** AI agent behavior and permissions

#### Integration with robots.txt and robots Meta Tags

**MX meta tags provide finer-grained control than robots.txt:**

```
# robots.txt (site-wide)
User-agent: *
Allow: /

User-agent: GPTBot
Disallow: /private/
```

```html
<!-- Page-level override with MX meta tags -->
<meta name="robots" content="index, follow">
<meta name="mx-content-policy" content="summaries-allowed">
<meta name="mx-attribution" content="required" text="Source: Example.com">
```

**Hierarchy of control:**

1. **robots.txt:** Site-wide policies
2. **robots meta tags:** Page-level indexing control
3. **MX meta tags:** Page-level agent behavior and permissions

#### Integration with llms.txt

**llms.txt provides site-wide defaults, MX meta tags provide page overrides:**

```
# /llms.txt
# Site-wide defaults
> Preferred Access: API
> Content Policy: summaries-allowed
> Freshness: daily
```

```html
<!-- Page overrides site-wide defaults -->
<meta name="mx-preferred-access" content="html">
<meta name="mx-freshness" content="hourly">
```

**Pattern:** Site-wide defaults in llms.txt, page-specific overrides in HTML meta tags.

#### Integration with WCAG Accessibility Standards

**MX convergence principle: Accessibility patterns benefit machines:**

```html
<!-- ARIA for screen readers -->
<button aria-label="Add to cart" aria-describedby="cart-status">
  <span class="icon">🛒</span>
</button>
<div id="cart-status" role="status" aria-live="polite">
  2 items in cart
</div>

<!-- Data attributes for AI agents -->
<button data-action="add-to-cart"
        data-product-id="WH-1000">
  <span class="icon">🛒</span>
</button>
<div data-item-count="2">
  2 items in cart
</div>
```

**Both patterns serve similar goals:**

- **ARIA:** Explicit semantics for assistive technology
- **Data attributes:** Explicit state for AI agents
- **Convergence:** Both benefit from explicit, semantic markup

#### Integration with Existing CMS Platforms

**WordPress example:**

```php
// Add MX meta tags to WordPress head
add_action('wp_head', function() {
  if (is_single()) {
    $post_age_days = (time() - get_post_time('U')) / DAY_IN_SECONDS;
    $freshness = $post_age_days < 7 ? 'daily' : 'monthly';

    echo '<meta name="mx-preferred-access" content="html">' . "\n";
    echo '<meta name="mx-content-policy" content="extract-with-attribution">' . "\n";
    echo '<meta name="mx-freshness" content="' . esc_attr($freshness) . '">' . "\n";
  }
});
```

**Next.js example:**

```jsx
export default function BlogPost({ post }) {
  return (
    <>
      <Head>
        <meta name="mx-preferred-access" content="html" />
        <meta name="mx-content-policy" content="extract-with-attribution" />
        <meta name="mx-freshness" content={post.freshness} />
      </Head>
      <article>{post.content}</article>
    </>
  );
}
```

#### Migration Path from Generic ai- Prefix

**If you previously used ai- prefix, migrate to mx-:**

```html
<!-- OLD (generic ai- prefix) -->
<meta name="sop-preferred-access" content="html">
<meta name="sop-content-policy" content="extract-with-attribution">

<!-- NEW (MX Framework) -->
<meta name="mx-preferred-access" content="html">
<meta name="mx-content-policy" content="extract-with-attribution">
```

**Rationale:** `mx-` establishes MX brand identity, aids discoverability, and aligns with namespace architecture. For complete explanation, see Part 2: MX Namespace Architecture.

**Migration strategy:**

1. Update meta tags from `ai-` to `mx-` in templates
2. Update documentation and examples
3. Both prefixes can coexist during transition (agents ignore unrecognized tags)
4. No breaking changes (forward-compatible pattern)

### Implementation Checklist

**Phase 1: Foundations (Week 1)**

- ✓ Add MX meta tags to `<head>` template
- ✓ Implement Schema.org JSON-LD for key content types
- ✓ Ensure semantic HTML elements (`<main>`, `<nav>`, `<article>`)
- ✓ Test with HTML validators

**Phase 2: Data Attributes (Week 2)**

- ✓ Add common data attributes to products (data-price, data-currency, data-product-id)
- ✓ Add state management attributes to forms (data-state, data-validation-state)
- ✓ Add pagination attributes (data-page, data-total-pages)
- ✓ Ensure consistency across all pages

**Phase 3: Dynamic Patterns (Week 3-4)**

- ✓ Implement data-agent-visible for hidden instructions
- ✓ Add JavaScript state updates for dynamic content
- ✓ Test with CLI tools (curl, wget)
- ✓ Verify agent behavior with logs

**Phase 4: Monitoring (Ongoing)**

- ✓ Track agent user-agents in server logs
- ✓ Monitor agent error rates
- ✓ Measure conversion rates for agent purchases
- ✓ Gather feedback and iterate

---

## Part 7: Relationship to Web Standards

### Standards Landscape

MX Framework operates within the broader web standards ecosystem. Understanding where MX fits helps clarify when to use which pattern.

#### Established Standards (Universal Adoption)

**W3C and WHATWG Standards:**

- **HTML5 semantic elements** — `<nav>`, `<main>`, `<article>`, `<aside>`, `<section>`
- **ARIA attributes** — `aria-label`, `aria-describedby`, `role`, `aria-live`
- **HTML5 data attributes** — `data-*` custom attributes
- **HTTP status codes** — 200, 303, 400, 401, 404, 422, 503
- **`<meta>` tags** — `robots`, `viewport`, `description`, `canonical`

**IETF Standards:**

- **robots.txt** (RFC 9309) — Site-wide crawling policies
- **HTTP headers** — Cache-Control, Content-Type, Status codes

**De Facto Standards:**

- **Schema.org** — Structured data vocabulary (Google, Microsoft, Yahoo, Yandex)
- **Open Graph** — Social media metadata (Facebook)
- **Twitter Cards** — Twitter-specific metadata

**MX position:** Builds on these foundations, never replaces them.

#### Emerging Standards (Early Adoption Phase)

**llms.txt:**

- **Status:** Community proposal gaining traction
- **Purpose:** Site-wide AI agent guidance
- **Analogy:** Like robots.txt but for LLMs
- **Adoption:** Growing adoption across MX community
- **MX relationship:** MX meta tags override llms.txt on per-page basis

**Web Standards Process:**

1. Individual experiments → 2. Community proposals → 3. Vendor consensus → 4. Formal standardization

**llms.txt is at stage 2-3.** MX Framework supports and extends it.

#### Proposed Patterns (MX Framework Specific)

**MX meta tag namespace:**

- **Status:** Proposed by MX Framework, not yet standardized
- **Pattern:** Framework-specific metadata (like `twitter:` and `og:`)
- **Rationale:** Establishes MX brand, aids discoverability, provides granular control
- **Adoption path:** Community adoption → vendor recognition → potential standardization

**data-agent-visible attribute:**

- **Status:** Proposed by MX Framework, experimental
- **Pattern:** Extends HTML5 `data-*` convention
- **Rationale:** Hidden machine-readable instructions (like ARIA for agents)
- **Forward-compatible:** Gracefully ignored if not recognized

**Common data attributes:**

- **Status:** Proposed conventions building on HTML5 `data-*`
- **Pattern:** Standardized attribute names for consistent state management
- **Rationale:** Agents parse state more reliably with consistent naming
- **Relationship:** Extends established HTML5 data attribute convention

### How MX Relates to Standards Bodies

**MX is not a standards body.** MX Framework:

- ✅ Proposes patterns following established conventions
- ✅ Documents practical implementations
- ✅ Builds on W3C/WHATWG/IETF standards
- ✅ Shares learnings with community
- ❌ Does not create formal specifications
- ❌ Does not replace existing standards
- ❌ Does not require vendor consensus before proposing

**MX role:** Practitioner community documenting patterns that work in production.

### Path to Standardization

**If MX patterns prove valuable, they might standardize through:**

1. **Multiple agent adoption** — Different AI systems recognize patterns
2. **Production validation** — Measurable benefits in real deployments
3. **Community refinement** — Usage reveals improvements
4. **Vendor support** — Platforms include MX patterns by default
5. **Formal proposal** — Community brings patterns to standards bodies

**Examples of similar evolution:**

- **viewport meta tag** — Apple proprietary → universal standard
- **robots meta tag** — Community convention → universal recognition
- **Open Graph** — Facebook proposal → widely adopted
- **Schema.org** — Vendor consortium → established standard

**MX follows this trajectory:** Start with practical patterns, refine through use, formalize if proven valuable.

### Web Standards Research (2025-2026)

**Research conducted:** January 2026 web standards search

**Finding:** NO established `ai-` prefix standard exists in:

- W3C specifications
- WHATWG standards
- IETF RFCs
- Major vendor proposals (Google, Microsoft, Meta, Apple)
- Community standards (Microformats, Schema.org)

**Implication:** `ai-` prefix was not following any established pattern. MX Framework chose `mx-` to:

1. Establish framework identity (like `twitter:`, `og:`)
2. Aid discoverability ("mx meta tags" search leads to MX community)
3. Align with namespace architecture (mx: → mx.ai, mx.co, mx.ho)

**Pattern precedent:**

- `twitter:card`, `twitter:title` — Twitter's framework-specific metadata
- `og:type`, `og:title` — Open Graph's framework-specific metadata
- `mx-preferred-access`, `mx-content-policy` — MX Framework's metadata

### Relationship to HTML Living Standard

**HTML Living Standard (WHATWG)** defines:

- Valid HTML elements and attributes
- `data-*` attribute pattern for custom data
- `<meta name="...">` extensibility

**MX compliance:**

- ✅ MX meta tags use valid `<meta name="...">` pattern
- ✅ MX data attributes follow `data-*` pattern
- ✅ All MX patterns use valid HTML syntax
- ✅ Forward-compatible (ignored by parsers that don't recognize them)

**MX is valid HTML** using established extension mechanisms.

### Cross-References to Standards Documentation

**For complete specifications, see:**

- **Semantic HTML:** [MDN HTML Elements Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
- **ARIA:** [W3C ARIA 1.2](https://www.w3.org/TR/wai-aria-1.2/)
- **Schema.org:** [Schema.org Documentation](https://schema.org)
- **Open Graph:** [Open Graph Protocol](https://ogp.me)
- **robots.txt:** [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html)
- **HTTP Status Codes:** [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html)
- **HTML Living Standard:** [WHATWG HTML](https://html.spec.whatwg.org)

**For MX-specific patterns, see:**

- **This appendix (Appendix L):** Complete MX pattern specifications
- **Appendix D:** AI-Friendly HTML Guide with practical examples
- **Appendix M:** Building the MX Operating System (collaborative process)

### Summary: Standards Hierarchy

**Use this hierarchy when making decisions:**

1. **Established standards FIRST** — HTML5, ARIA, Schema.org, HTTP
2. **Emerging conventions SECOND** — llms.txt, community patterns
3. **MX patterns THIRD** — Framework-specific metadata and extensions

**Never replace established standards with MX patterns.** Always build on foundations.

---

**Note:** This appendix presents proposed patterns, not established standards. Evaluate adoption based on your specific situation and risk tolerance. All patterns are designed for graceful degradation and forward compatibility.
