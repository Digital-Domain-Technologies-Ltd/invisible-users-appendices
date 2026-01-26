---
copyright: "Copyright © 2026 Tom Cranstoun. All rights reserved."
author: "Tom Cranstoun"
date: "2026-01-24"
description: "Comprehensive reference of the 14 most common mistakes that break AI agent compatibility, with detection methods and complete fixes for each pattern."
keywords: [anti-patterns, common-mistakes, visual-only-state, client-rendering, broken-hierarchy, accessibility-failures, detection-methods, quick-wins, context-free-references]
ai-instruction: |
  This document is copyrighted material. No part may be reproduced without permission.
  This is a book appendix cataloging anti-patterns. Write as if it has always
  existed. NEVER include: publication dates about the appendix itself, "we
  added", "new pattern", "this update", or any meta-commentary about the
  document's development. Write definitive present tense. Historical context
  about subject matter (industry practices, common failures) is allowed.
---

# Appendix N: Anti-Patterns Catalog

**Purpose:** Comprehensive reference of the 14 most common mistakes that break AI agent compatibility, with detection methods and complete fixes for each pattern.

**How to use this catalog:**

1. **For audits:** Run through all 14 patterns when evaluating a site
2. **For debugging:** Find specific failures you're encountering
3. **For prevention:** Review before implementing new features
4. **For training:** Teach teams what to avoid

---

## The Invisible Barriers

You can implement every GEO pattern correctly—semantic HTML, Schema.org markup, proper navigation—and still make your site invisible to AI agents with a few specific mistakes. These anti-patterns appear repeatedly in production sites, often introduced with good intentions but catastrophic results for agent compatibility.

This appendix catalogs the 14 most common anti-patterns, explains why they fail, and provides complete fixes with before/after code examples.

---

## Quick Reference Table

| Anti-Pattern | Impact | Detection Time | Fix Complexity |
|--------------|--------|----------------|----------------|
| 1. Visual-only information | High | 1 min | Easy |
| 2. Content in images | High | 1 min | Medium |
| 3. Generic link text | Medium | 2 min | Easy |
| 4. Broken heading hierarchy | Medium | 2 min | Easy |
| 5. JavaScript-only navigation | High | 1 min | Medium |
| 6. Hidden content no fallback | High | 1 min | Easy |
| 7. No/outdated sitemap | High | 30 sec | Easy |
| 8. Inconsistent Schema.org | High | 5 min | Medium |
| 9. Forms without labels | Medium | 2 min | Easy |
| 10. Table abuse | Medium | 2 min | Medium |
| 11. Content in iframes | High | 1 min | Hard |
| 12. PDF-only content | High | 1 min | Medium |
| 13. Auto-playing content | Medium | 1 min | Easy |
| 14. Context-free references | Medium | 2 min | Easy |

---

## Anti-Pattern 1: Visual-Only Information

**Pattern ID:** `mx.anti-pattern.css.visual-only-information`
**Status:** active
**Intent:** Avoid conveying critical information through visual styling alone, as it remains invisible to AI agents and accessibility users

### Context

This anti-pattern commonly appears in:

- E-commerce sites with pricing tiers and "recommended" plans
- SaaS products with feature comparison tables
- Marketing sites with highlighted calls-to-action
- Dashboard interfaces with status indicators and alerts
- Product catalogs with "bestseller" or "featured" badges

It's typically introduced when:

- Designers specify visual emphasis without semantic requirements
- Developers implement designs directly from visual mockups without accessibility considerations
- CSS frameworks encourage class-based visual styling patterns
- Time pressure leads to visual-first implementation without semantic planning
- Teams lack awareness of how non-visual users consume content

### The Problem

Information conveyed purely through visual styling (colour, size, position, borders) without semantic backing in HTML.

Humans perceive visual cues immediately—a gold border indicates "recommended", larger size suggests importance, green means "success". AI agents and screen readers parse HTML structure and content, not CSS styling. When critical information exists only in CSS, it's invisible to these users.

**Impact:**

- AI agents cannot identify recommended products or important options when making decisions
- Screen reader users miss visual emphasis, recommendations, and status indicators
- Search engines cannot understand content importance or relationships
- Automated testing cannot verify visual-only patterns
- Content loses meaning when CSS fails to load or is overridden

### Real Example

```html
<div class="pricing-tiers">
  <div class="tier tier-basic">
    <div class="tier-name">Basic</div>
    <div class="tier-price">£29</div>
  </div>

  <div class="tier tier-pro tier-featured">
    <div class="tier-name">Professional</div>
    <div class="tier-price">£99</div>
    <div class="tier-badge">Most Popular</div>
  </div>

  <div class="tier tier-enterprise">
    <div class="tier-name">Enterprise</div>
    <div class="tier-price">£299</div>
  </div>
</div>
```

```css
.tier-featured {
  border: 3px solid gold;
  background: #fffef0;
  transform: scale(1.05);
}
```

**What humans see:** Professional tier highlighted with gold border, larger size, subtle yellow background tint—clearly the recommended option.

**What AI agents see:** Three identical `<div>` structures. The "Most Popular" badge appears, but there's no semantic indication that "Professional" is actually recommended. The CSS class `tier-featured` means nothing without visual rendering.

**What screen readers announce:** "Pricing tiers. Basic £29. Professional £99 Most Popular. Enterprise £299." No indication of recommendation or importance.

### Forces

- **Design flexibility:** CSS-only highlighting is faster to implement and easier to change than restructuring HTML with semantic elements
- **Developer convenience:** Adding a CSS class (`tier-featured`) is simpler than adding semantic HTML, ARIA attributes, and explicit text
- **Framework habits:** Modern CSS frameworks (Bootstrap, Tailwind) encourage class-based styling patterns without semantic backing
- **Visual requirements:** Design specifications focus on visual appearance without considering non-visual users
- **Time pressure:** Semantic HTML requires more planning and implementation time than adding visual-only classes
- **Browser compatibility:** Visual approaches work consistently across all browsers with minimal testing
- **Perceived simplicity:** Developers see CSS styling as "cleaner" than semantic HTML with additional attributes

### The Fix (Solution)

Make recommendations explicit in HTML structure and content using semantic elements, ARIA attributes, and visible text:

```html
<section class="pricing-tiers">
  <article class="tier tier-basic">
    <h3>Basic</h3>
    <data value="29">£29</data>
    <span class="period">/month</span>
  </article>

  <article class="tier tier-pro" aria-label="Recommended plan">
    <h3>Professional <span class="badge" aria-label="Most popular plan">Most Popular</span></h3>
    <data value="99">£99</data>
    <span class="period">/month</span>
    <p><strong>Recommended for most businesses</strong></p>
  </article>

  <article class="tier tier-enterprise">
    <h3>Enterprise</h3>
    <data value="299">£299</data>
    <span class="period">/month</span>
  </article>
</section>
```

**Key improvements:**

- **Semantic container:** `<section>` groups pricing tiers with clear purpose
- **Article elements:** Each tier is an `<article>` (self-contained content)
- **ARIA label:** `aria-label="Recommended plan"` makes recommendation machine-readable
- **Explicit text:** "Recommended for most businesses" appears in HTML (not CSS)
- **Proper data elements:** `<data value="99">` provides machine-readable price
- **Semantic headings:** `<h3>` creates proper document outline

### Resulting Context

After implementing semantic fixes:

- **Agent understanding:** AI agents can identify recommended options through HTML structure, ARIA attributes, and explicit text without requiring visual parsing
- **Screen reader clarity:** Screen reader users hear "Recommended plan: Professional. Most popular plan. Recommended for most businesses" with proper context
- **Search indexing:** Search engines understand content hierarchy, relative importance, and recommendations
- **Maintainability:** Semantic HTML is self-documenting—developers understand intent from structure
- **CSS-independent:** Content retains meaning even when CSS fails to load or is overridden by user stylesheets
- **Testing capability:** Automated accessibility tests can verify semantic structure using Pa11y, axe, or similar tools
- **SEO improvement:** Search engines give appropriate weight to recommended content, improving discoverability

### Consequences

**Positive:**

- **Universal accessibility:** Pattern works for AI agents, screen readers, keyboard users, and visual users without modification
- **WCAG 2.1 AA compliance:** Satisfies success criteria 1.3.1 (Info and Relationships) and 1.4.1 (Use of Colour)
- **Reduced CSS dependency:** Semantic HTML provides meaning even when CSS is disabled or overridden
- **Better SEO:** Search engines understand content importance, hierarchy, and recommendations
- **Easier testing:** Semantic structure enables automated accessibility testing with standard tools
- **Future-proof:** Pattern works across new AI systems and assistive technologies without updates
- **Progressive enhancement:** Content accessible at HTML level, visual enhancements layered with CSS

**Negative/Trade-offs:**

- **More HTML markup:** Semantic structure requires additional elements (`<section>`, `<article>`) and attributes (`aria-label`)
- **Upfront planning:** Requires thinking about semantics during design phase, not just visual implementation
- **Framework compatibility:** May conflict with CSS framework patterns that assume visual-only styling (requires custom implementation)
- **Learning curve:** Development teams need training on semantic HTML patterns, ARIA attributes, and accessibility principles
- **Code complexity:** More complex HTML structure than simple `<div>` + CSS class pattern
- **Initial development time:** Takes longer to implement semantic patterns than visual-only approaches

### Known Uses

**Common in:**

- Bootstrap-based sites relying solely on `.btn-primary`, `.badge-success` classes for visual emphasis without semantic backing
- React applications using styled-components or CSS-in-JS without considering semantic HTML structure
- WordPress themes implementing visual-only featured content indicators through CSS classes alone
- Tailwind CSS projects where utility classes (`border-4 border-yellow-400 scale-105`) replace semantic HTML
- Admin dashboards using colour-coded status indicators (red/yellow/green) without text labels or semantic attributes

**Specific examples:**

- SaaS pricing pages with CSS-highlighted "recommended" tiers (gold borders, larger size, background tint) but no semantic indication
- E-commerce category pages with visually emphasized "bestseller" badges that are pure CSS `::before` pseudo-elements
- Dashboard interfaces with colour-coded status indicators (success=green, warning=yellow, error=red) without accompanying text
- Feature comparison tables using background colours to show "included" vs "not included" without checkmarks, text, or semantic markup
- Mobile app landing pages with visually prominent "Get Started" buttons that lack semantic distinction from other buttons

### Related Patterns

**Fixes this anti-pattern:**

- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Provides semantic alternatives to visual-only patterns
- Pattern 18: Explicit State Attributes (Appendix M) - Shows how to make application state machine-readable
- Pattern 12: WCAG 2.1 AA Compliance (Chapter 12.12) - Ensures visual information has non-visual alternatives

**Related anti-patterns:**

- Anti-pattern 6: Hidden Content Without Fallback - Similar CSS-dependence issue where content is inaccessible without styles
- Anti-pattern 13: Auto-Playing Content - Also assumes visual presentation without considering alternative access methods
- Anti-pattern 3: Generic Link Text - Another pattern where visual context (surrounding content) isn't available to non-visual users

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Semantic First principle)
- Chapter 11.3: The Convergence Principle (patterns helping both agents and accessibility users)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)
- Chapter 12.12: Pattern 12 (WCAG 2.1 AA Compliance)

---

## Anti-Pattern 2: Content in Images

**Pattern ID:** `mx.anti-pattern.media.content-in-images`
**Status:** active
**Intent:** Prevent critical content from being trapped in non-text formats where it's inaccessible to AI agents and screen readers

### Context

This anti-pattern commonly appears in:

- Marketing sites using infographics to explain complex services or processes
- Product pages with feature comparison charts embedded as images
- Educational content with text-heavy diagrams or flowcharts
- Social media sharing where text is rendered into images for visual appeal
- Dashboard screenshots showing data tables or metrics

It's typically introduced when:

- Designers create compelling visual content without considering text alternatives
- Marketing teams prioritize visual aesthetics over accessibility
- Content is migrated from print materials to web without adaptation
- Teams use design tools that export text as rasterized images
- Social media requirements favour image-based content over plain text

### The Problem

Text embedded in images without proper alt text or supplementary HTML text.

When critical information exists only as pixels in an image, it's completely inaccessible to non-visual users. AI agents cannot extract text from images (OCR is unreliable and not universally available), and screen readers can only announce the alt text—which is often generic or missing entirely.

**Impact:**

- AI agents cannot parse service descriptions, pricing details, or feature lists embedded in images
- Screen reader users miss essential information that's trapped in infographics
- Search engines cannot index text content that exists only as image pixels
- Translation tools cannot convert text in images to other languages
- Users with low bandwidth may block images entirely, losing all content
- Content becomes unsearchable with browser find-in-page functionality

### Real Example

Service offerings described entirely in an infographic:

```html
<img src="our-services-infographic.png" alt="Our services">
```

**What the image contains:**

- Web Development: Full-stack development with modern frameworks
- Mobile Apps: iOS and Android native applications
- Cloud Infrastructure: AWS and Azure deployment
- DevOps: CI/CD pipelines

**What AI agents see:** "Our services" - no detail whatsoever. The alt text provides no information about the actual services offered.

**What screen readers announce:** "Image: Our services" - users with vision impairments receive no information about the four service categories or their descriptions.

**What search engines index:** Only "Our services" - the detailed service descriptions remain invisible to Google, Bing, and other search engines.

### Forces (Anti-Pattern 2)

- **Visual appeal:** Infographics and visual designs are more engaging than plain text
- **Design tool workflow:** Designers work in Figma, Photoshop, or Canva, exporting designs as images
- **Print legacy:** Content originally created for print materials (brochures, flyers) is simply uploaded as images
- **Social media optimization:** Platforms like Instagram and Pinterest favour image-based content
- **Perceived efficiency:** Easier to embed a screenshot than to recreate content in HTML
- **Brand consistency:** Maintaining exact fonts, colours, and layouts requires image formats
- **Developer availability:** Marketing teams can upload images without developer assistance

### Solution (Anti-Pattern 2)

Provide information in both image and accessible text format using semantic HTML:

```html
<section>
  <h2>Our Services</h2>

  <img src="our-services-infographic.png"
       alt="Infographic showing four service categories: Web Development, Mobile Apps, Cloud Infrastructure, and DevOps">

  <div class="services-text">
    <article>
      <h3>Web Development</h3>
      <p>Full-stack development with modern frameworks including React, Vue, and Node.js</p>
    </article>

    <article>
      <h3>Mobile Apps</h3>
      <p>iOS and Android native applications built with Swift and Kotlin</p>
    </article>

    <article>
      <h3>Cloud Infrastructure</h3>
      <p>AWS and Azure deployment and management with infrastructure as code</p>
    </article>

    <article>
      <h3>DevOps</h3>
      <p>CI/CD pipelines and containerization with Docker and Kubernetes</p>
    </article>
  </div>
</section>
```

**Key improvements:**

- **Semantic container:** `<section>` groups related content with clear heading
- **Enhanced alt text:** Describes what the infographic shows (four service categories) instead of generic "Our services"
- **Text alternative:** All content from image is provided as semantic HTML below the image
- **Article elements:** Each service is an `<article>` with proper heading hierarchy
- **Searchable content:** All service descriptions are indexable text, not pixels
- **Progressive enhancement:** Visual users see the infographic, non-visual users get equivalent text content

**Alternative approach (text with visual enhancement):**

```html
<section>
  <h2>Our Services</h2>

  <div class="services-grid">
    <article>
      <h3>Web Development</h3>
      <p>Full-stack development with modern frameworks including React, Vue, and Node.js</p>
    </article>
    <!-- Additional services... -->
  </div>

  <!-- Infographic as optional visual enhancement -->
  <figure>
    <img src="our-services-infographic.png" alt="Visual summary of our four service categories" aria-hidden="true">
    <figcaption>Visual representation of services detailed above</figcaption>
  </figure>
</section>
```

This approach treats text as primary content and image as visual enhancement.

### Resulting Context (Anti-Pattern 2)

After implementing text alternatives:

- **Agent understanding:** AI agents can parse all service descriptions, features, and details from structured HTML
- **Screen reader access:** Screen reader users receive complete information through semantic headings and text content
- **Search discoverability:** Search engines index all service descriptions, improving SEO rankings
- **Translation capability:** Browser translation tools and services can convert text content to other languages
- **Find-in-page:** Users can search for specific services or keywords using browser find functionality
- **Low-bandwidth friendly:** Users who block images still receive complete information
- **Content reuse:** Structured HTML content can be repurposed for APIs, mobile apps, or other formats

### Consequences (Anti-Pattern 2)

**Positive:**

- **Universal accessibility:** Content accessible to AI agents, screen readers, search engines, and translation tools
- **WCAG 2.1 AA compliance:** Satisfies success criteria 1.1.1 (Non-text Content) and 1.4.5 (Images of Text)
- **Better SEO:** Search engines index detailed text content, not just generic alt text
- **Content portability:** Structured text can be syndicated, translated, or exported to other formats
- **Future-proof:** Works with emerging AI systems and assistive technologies
- **Responsive design:** Text reflows and adapts to different screen sizes, unlike fixed-size images
- **Maintenance:** Easier to update text content than recreating images

**Negative/Trade-offs:**

- **More initial work:** Requires creating both visual design and equivalent HTML text
- **Design complexity:** Need to ensure text content works visually without relying on image
- **File size:** Additional HTML text increases page weight (usually minimal compared to images)
- **Visual consistency:** May be harder to maintain exact brand styling with HTML/CSS vs images
- **Content duplication:** Information exists in two places (image and text), requiring synchronized updates
- **Design tool limitations:** Workflow doesn't support automatic text extraction from design files

### Known Uses (Anti-Pattern 2)

**Common in:**

- Marketing landing pages using Canva or similar tools to create infographic-style service descriptions
- B2B SaaS sites with feature comparison charts created in design tools and exported as PNGs
- Educational platforms with text-heavy diagrams explaining processes or concepts
- Social media content where text is rendered into images for Instagram/Facebook sharing
- E-commerce sites with size charts, specifications, or instructions embedded as images

**Specific examples:**

- Agency websites with "Our Process" infographics showing 5-step workflows as single images
- Product pages with specification tables photographed from print catalogs
- Tutorial sites with code screenshots instead of actual code blocks
- Restaurant websites with menu images (photographed menus) instead of HTML text
- Conference sites with schedule infographics instead of structured timetables

### Related Patterns (Anti-Pattern 2)

**Fixes this anti-pattern:**

- Pattern 4: Text Alternatives for Images (Chapter 12.4) - Comprehensive guidance on alt text and text alternatives
- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Shows how to structure text content properly
- Pattern 21: Responsive Images (Appendix M) - Modern image handling with appropriate text alternatives

**Related anti-patterns:**

- Anti-pattern 12: PDF-Only Content - Similar content trap where information is locked in non-HTML format
- Anti-pattern 11: Content in iframes - Another pattern where content is inaccessible to parsing
- Anti-pattern 1: Visual-Only Information - Related pattern of relying on visual presentation

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Content First principle)
- Chapter 11.3: The Convergence Principle (text alternatives help everyone)
- Chapter 12.4: Pattern 4 (Text Alternatives)
- Chapter 12.12: Pattern 12 (WCAG 2.1 AA Compliance)

---

## Anti-Pattern 3: Generic Link Text

**Pattern ID:** `mx.anti-pattern.html.generic-link-text`
**Status:** active
**Intent:** Ensure link text provides meaningful context about destinations, enabling AI agents and screen reader users to understand links without surrounding context

### Context (Anti-Pattern 3)

This anti-pattern commonly appears in:

- Marketing sites with repeated "Learn more" or "Read more" CTAs across multiple sections
- Blog listing pages where every post has identical "Read full article" links
- Product catalog pages with generic "View details" or "See more" links
- SaaS landing pages with multiple "Get started" buttons linking to different destinations
- Service pages with "Click here" links scattered throughout descriptive paragraphs

It's typically introduced when:

- Designers prioritize visual consistency over semantic clarity (all CTAs look identical)
- Content writers follow print conventions where context is always visible
- Content management systems use generic default link text for cards and teasers
- Marketing teams optimize for brevity without considering accessibility implications
- Developers implement templates with hardcoded generic link text that content editors don't customize

### Problem (Anti-Pattern 3)

Links with meaningless text like "click here", "read more", "learn more", "see more", "view details" that provide no information about destinations when read without surrounding context.

Sighted users see links in context—a "Learn more" link below a heading about "Edge Delivery Services Migration" is obviously about that topic. AI agents and screen reader users often navigate by extracting all links from a page as a list. When every link says "Learn more", "Read more", or "Click here", the list becomes useless:

1. Learn more
2. Read more
3. Learn more
4. Click here
5. See details

**Impact:**

- AI agents cannot build accurate page summaries or determine relevant destinations
- Screen reader users must navigate back to surrounding context to understand each link
- Search engines cannot determine link relevance or target page topics
- Automated testing cannot verify that correct links point to intended destinations
- Voice interface users cannot specify which "learn more" link they want to activate

### Detection Method (Anti-Pattern 3)

Extract all links and read as list - are they self-explanatory?

```javascript
Array.from(document.querySelectorAll('a'))
  .map(a => a.textContent.trim())
  .forEach((text, i) => console.log(`${i + 1}. ${text}`));
```

### Forces (Anti-Pattern 3)

- **Visual design consistency:** Designers want uniform CTA appearance and length across all cards and sections
- **Content brevity:** Character limits in card layouts force generic text like "More" or "View"
- **Print convention legacy:** Print design assumes readers see surrounding context for every element
- **CMS template limitations:** Default templates include hardcoded generic link text that content editors don't customize
- **Marketing copy patterns:** Marketing teams use action verbs ("Learn", "Discover", "Explore") without objects
- **Visual hierarchy:** Designers prioritize heading clarity over link specificity, assuming context is always visible
- **Translation simplification:** Generic links reduce translation costs by reusing identical text across pages

### Solution (Anti-Pattern 3)

Make link text descriptive and self-contained, so it conveys destination meaning without surrounding context.

**Before:**

```html
<section>
  <h3>Edge Delivery Services Migration</h3>
  <p>We help companies migrate from traditional CMS platforms...</p>
  <a href="/services/eds-migration">Learn more</a>
</section>
```

**After (best approach - descriptive link text):**

```html
<section>
  <h3>Edge Delivery Services Migration</h3>
  <p>We help companies migrate from traditional CMS platforms...</p>
  <a href="/services/eds-migration">Explore our EDS migration services</a>
</section>
```

**Alternative (if design requires short text - use aria-label):**

```html
<a href="/services/eds-migration"
   aria-label="Learn more about Edge Delivery Services migration">
  Learn more
</a>
```

**Note:** The aria-label approach is a compromise. Descriptive visible link text is always preferable because it benefits all users, not just assistive technology users.

### Resulting Context (Anti-Pattern 3)

After implementing descriptive link text:

- **Agent understanding:** AI agents can extract meaningful link lists and understand page navigation structure
- **Screen reader navigation:** Screen reader users can browse links as a list and understand each destination
- **Search indexing:** Search engines understand link relationships and can weight target page relevance
- **Voice interface clarity:** Voice users can specify exactly which link they want ("click EDS migration services link")
- **Keyboard navigation:** Keyboard users navigating by links hear distinct, meaningful descriptions
- **Testing automation:** Automated tests can verify correct link destinations by matching descriptive text
- **Content comprehension:** All users benefit from explicit link descriptions, reducing cognitive load

### Consequences (Anti-Pattern 3)

**Positive:**

- **Universal accessibility:** Works for AI agents, screen readers, voice interfaces, and keyboard navigation
- **WCAG 2.1 AA compliance:** Satisfies success criteria 2.4.4 (Link Purpose in Context) and 2.4.9 (Link Purpose)
- **Better SEO:** Search engines understand link context and anchor text relevance
- **Improved UX:** All users benefit from explicit link descriptions without needing surrounding context
- **Testing reliability:** Automated tests can verify link destinations by matching visible text
- **Content portability:** Links remain meaningful when extracted to feeds, summaries, or link lists
- **Voice interface support:** Users can activate specific links by speaking descriptive link text

**Negative/Trade-offs:**

- **Longer link text:** Descriptive links require more characters than generic "Learn more" (may affect card layouts)
- **Design flexibility:** Less visual consistency if link text varies in length across similar sections
- **Content effort:** Requires content editors to write unique, descriptive link text for each instance
- **Translation costs:** More varied link text increases translation word count and localization effort
- **Visual hierarchy:** Longer link text may compete with headings for visual attention
- **Template complexity:** CMS templates need dynamic link text fields instead of hardcoded strings

### Known Uses (Anti-Pattern 3)

**Common in:**

- WordPress themes using hardcoded "Read More" links on blog listing pages
- Bootstrap-based marketing sites with repeated "Learn More" CTAs in feature cards
- E-commerce platforms with generic "View Product" links that don't include product names
- SaaS landing pages with multiple "Get Started" buttons linking to different signup flows
- News sites with "Continue reading" links on article excerpts without article titles

**Specific examples:**

- Blog archives where every post has identical "Read full article" link text
- Service comparison tables with "Learn more" in every cell, all linking to different pages
- Product listing pages with "Add to basket" buttons that don't specify product names
- Documentation sites with "Next step" links that don't indicate next topic
- Footer navigation with "Privacy policy", "Terms", "Contact" followed by generic "Click here" links

### Related Patterns (Anti-Pattern 3)

**Fixes this anti-pattern:**

- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Demonstrates proper link text within semantic context
- Pattern 14: Clear Navigation Labels (Appendix M) - Provides guidance on descriptive navigation text
- Pattern 3: Keyboard Navigation (Chapter 12.3) - Shows how keyboard users navigate links and why descriptive text matters

**Related anti-patterns:**

- Anti-pattern 14: Context-Free References - Similar problem where meaning depends on visual context
- Anti-pattern 1: Visual-Only Information - Related pattern of assuming visual context is always available
- Anti-pattern 4: Broken Heading Hierarchy - Also impacts content structure comprehension

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Semantic First principle)
- Chapter 11.3: The Convergence Principle (descriptive links help everyone)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)
- Chapter 12.3: Pattern 3 (Keyboard Navigation)

---

## Anti-Pattern 4: Broken Heading Hierarchy

**Pattern ID:** `mx.anti-pattern.html.broken-heading-hierarchy`
**Status:** active
**Intent:** Maintain logical heading hierarchies that reflect content structure, enabling AI agents and assistive technology to understand document organization

### Context (Anti-Pattern 4)

This anti-pattern commonly appears in:

- Marketing sites where designers choose heading sizes based on visual aesthetics rather than semantic structure
- WordPress themes that encourage using h3 or h4 for visual consistency across widgets and sidebars
- Component libraries where heading levels are hardcoded in components without considering page context
- Legacy sites where CSS classes like `.small-heading` or `.large-heading` replaced semantic heading usage
- Single-page applications where sections use arbitrary heading levels without considering overall hierarchy

It's typically introduced when:

- Designers specify heading styles in visual mockups without considering semantic HTML levels
- Developers use headings as styling tools ("h3 looks better than h2 here")
- CSS frameworks provide utility classes that override heading semantics
- Component-based development isolates heading choices without page-level hierarchy review
- Content editors select headings from WYSIWYG dropdowns based on appearance, not structure
- Legacy print design conventions influence web heading selection

### Problem (Anti-Pattern 4)

Headings used for styling rather than structure, creating illogical hierarchies that confuse semantic understanding. Common patterns include skipping levels (h1 → h3), reversing hierarchy (h2 under h3), or using headings purely for visual sizing.

Screen readers and AI agents rely on heading hierarchy to understand document structure and create navigation outlines. A properly structured page uses headings like a table of contents: h1 for page title, h2 for major sections, h3 for subsections, and so on. When headings are chosen for visual appearance rather than semantic meaning, the document outline becomes incoherent.

**Example of broken outline generated by poor heading hierarchy:**

```text
H1 Welcome to Digital Domain
  H3 Our Services              ← Skipped H2
    H2 Web Development         ← H2 under H3 (reversed)
      H4 About Us              ← Skipped H3, H4 without parent H3
```

**Impact:**

- AI agents cannot generate accurate page summaries or understand content organization
- Screen reader users navigating by headings encounter illogical jumps that break comprehension
- Search engines misunderstand content hierarchy and relative importance of sections
- Accessibility scanning tools flag heading hierarchy violations as WCAG failures
- Automated content extraction produces nonsensical outlines
- Browser reader modes may incorrectly parse article structure

### Detection Method (Anti-Pattern 4)

Extract heading hierarchy and visualize as nested outline:

```javascript
Array.from(document.querySelectorAll('h1, h2, h3, h4, h5, h6'))
  .forEach(h => {
    const level = h.tagName[1];
    const indent = '  '.repeat(parseInt(level) - 1);
    console.log(`${indent}${h.tagName}: ${h.textContent.trim()}`);
  });
```

### Forces (Anti-Pattern 4)

- **Visual design requirements:** Designers specify heading sizes based on visual hierarchy, not semantic structure
- **CSS framework defaults:** Frameworks like Bootstrap provide heading styles that developers use for sizing, not semantics
- **Component isolation:** Component-based development (React, Vue) isolates heading choices from overall page hierarchy
- **WYSIWYG editors:** Content editors see visual dropdown of heading options and choose based on appearance
- **Legacy print conventions:** Print design background encourages "headline", "subhead", "deck" thinking instead of semantic levels
- **Developer convenience:** Easier to use h3 for visual consistency than to fix CSS or choose semantically correct level
- **Design system constraints:** Design systems specify limited heading sizes (e.g., "Display", "Headline", "Title") that don't map to HTML levels
- **Responsive sizing:** Different heading sizes needed for mobile vs desktop, leading to semantic choices based on viewport

### Solution (Anti-Pattern 4)

Use heading levels to reflect content structure, not visual styling. Separate semantic meaning (HTML heading level) from visual presentation (CSS styling).

**Before (illogical hierarchy):**

```html
<h1>Welcome to Digital Domain</h1>

<div class="services-section">
  <h3>Our Services</h3>  <!-- Skipped h2 -->

  <div class="service">
    <h2>Web Development</h2>  <!-- h2 under h3 -->
  </div>
</div>

<div class="about-section">
  <h4>About Us</h4>  <!-- h4 without h2 or h3 -->
</div>
```

**After (logical hierarchy with semantic HTML and CSS styling):**

```html
<h1>Welcome to Digital Domain</h1>

<section>
  <h2>Our Services</h2>

  <article>
    <h3>Web Development</h3>
    <p>We build modern web applications...</p>
  </article>

  <article>
    <h3>Consulting</h3>
    <p>Strategic guidance for your projects...</p>
  </article>
</section>

<section>
  <h2>About Us</h2>
  <p>Founded in 1999...</p>
</section>
```

**CSS approach for visual flexibility:**

```css
/* Separate semantic structure from visual styling */
.services-section h2 {
  font-size: 1.5rem;  /* Smaller visual size */
  font-weight: 600;
}

.about-section h2 {
  font-size: 2rem;    /* Larger visual size */
  font-weight: 700;
}

/* Or use utility classes that don't affect semantics */
<h2 class="text-xl">Our Services</h2>  <!-- Semantic h2, styled smaller -->
<h2 class="text-3xl">About Us</h2>     <!-- Semantic h2, styled larger -->
```

### Resulting Context (Anti-Pattern 4)

After implementing logical heading hierarchy:

- **Agent understanding:** AI agents can generate accurate page outlines and understand content organization
- **Screen reader navigation:** Screen reader users can navigate by heading level and understand document structure
- **Search indexing:** Search engines correctly understand content hierarchy and relative section importance
- **Accessibility compliance:** WCAG 2.1 success criterion 1.3.1 (Info and Relationships) satisfied
- **Browser reader modes:** Reader views correctly parse article structure and presentation
- **Content extraction:** Automated tools produce coherent outlines for summaries and navigation
- **Maintainability:** Content structure is explicit in HTML, making it easier to understand and update

### Consequences (Anti-Pattern 4)

**Positive:**

- **Universal accessibility:** Logical structure benefits AI agents, screen readers, search engines, and reader modes
- **WCAG 2.1 AA compliance:** Satisfies success criterion 1.3.1 (Info and Relationships)
- **Better SEO:** Search engines understand content hierarchy and weigh sections appropriately
- **Improved navigation:** Screen reader users can jump between heading levels efficiently
- **Content portability:** Document outline remains coherent when content is extracted or syndicated
- **Maintainability:** Semantic structure is self-documenting and easier to understand
- **Future-proof:** Works with emerging AI systems that rely on semantic HTML

**Negative/Trade-offs:**

- **CSS complexity:** Requires CSS to control visual presentation separately from semantic structure
- **Design constraints:** Designers must think about semantic levels in addition to visual hierarchy
- **Component complexity:** React/Vue components need to accept heading level as prop rather than hardcoding
- **Migration effort:** Fixing existing broken hierarchies across large sites requires comprehensive audit
- **Team training:** Developers and content editors need training on semantic heading usage
- **CMS limitations:** Some content management systems don't provide easy heading level customization

### Known Uses (Anti-Pattern 4)

**Common in:**

- WordPress sites where widget headings use h3 regardless of page context
- Bootstrap-based sites where developers use `.h3` class and actual `<h3>` element interchangeably
- React/Vue component libraries with hardcoded heading levels (e.g., Card component always uses h3)
- Landing page builders (Unbounce, Leadpages) where headings are chosen from visual size dropdown
- E-commerce platforms where product titles use h4 for visual sizing across category pages

**Specific examples:**

- Marketing sites with h1 page title, then h4 for section headings (skipping h2, h3)
- Blog posts using h3 for post titles within listing pages that already have h2 section headings
- Sidebar widgets using h2 or h3 without considering main content hierarchy
- Footer sections using h4 for "About Us", "Contact" when no h2 or h3 exists
- Product comparison tables using h5 for all product names regardless of page structure

### Related Patterns (Anti-Pattern 4)

**Fixes this anti-pattern:**

- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Comprehensive semantic HTML guidance including heading hierarchy
- Pattern 12: WCAG 2.1 AA Compliance (Chapter 12.12) - Covers accessibility requirements for heading structure
- Pattern 1: HTML Document Structure (Chapter 12.1) - Demonstrates proper document outline organization

**Related anti-patterns:**

- Anti-pattern 10: Table Abuse for Layout - Similar misuse of semantic elements for visual purposes
- Anti-pattern 1: Visual-Only Information - Related pattern of prioritizing visual presentation over semantic meaning
- Anti-pattern 3: Generic Link Text - Also impacts content navigation and comprehension

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Semantic First principle)
- Chapter 11.3: The Convergence Principle (semantic structure helps everyone)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)
- Chapter 12.1: Pattern 1 (HTML Document Structure)

---

## Anti-Pattern 5: JavaScript-Only Navigation

**Pattern ID:** `mx.anti-pattern.javascript.client-only-navigation`
**Status:** active
**Intent:** Ensure navigation menus exist in served HTML so AI agents and non-JavaScript environments can discover and navigate site structure

### Context (Anti-Pattern 5)

This anti-pattern commonly appears in:

- Single-page applications (React, Vue, Angular) where navigation is entirely client-side rendered
- Sites built with JavaScript frameworks that assume JavaScript execution for all functionality
- Progressive web apps (PWAs) where developers prioritize JavaScript-enhanced experience
- Marketing sites using JavaScript-heavy page builders (Webflow, Wix) with client-rendered navigation
- E-commerce platforms where navigation menus are dynamically loaded from APIs

It's typically introduced when:

- Modern JavaScript frameworks default to client-side rendering without SSR (server-side rendering)
- Developers build SPAs without considering progressive enhancement
- Navigation data comes from APIs and developers don't implement server-side fallbacks
- Performance optimization attempts defer navigation rendering until after JavaScript loads
- Framework documentation emphasizes JavaScript-first development patterns
- Mobile-first design prioritizes JavaScript hamburger menus without HTML fallbacks

### Problem (Anti-Pattern 5)

Navigation menus that only exist after JavaScript executes, making them invisible to CLI agents, search engine crawlers that prioritize served HTML, and users in low-JavaScript environments.

CLI agents and many search engine crawlers parse served HTML (the initial HTML response from the server) without executing JavaScript. When navigation exists only as an empty `<nav id="main-nav"></nav>` element that JavaScript populates, these agents see no navigation structure at all.

**Impact:**

- CLI agents cannot discover site structure or navigate beyond the current page
- Search engines may not crawl linked pages if navigation isn't in served HTML
- Users with JavaScript disabled or blocked see no navigation options
- Screen readers encounter empty navigation landmarks
- Progressive web app "add to home screen" initial loads show no navigation
- Performance metrics show longer time-to-interactive due to JavaScript-dependent navigation
- Automated testing must wait for JavaScript execution to verify navigation

### Detection Method (Anti-Pattern 5)

View page source (Ctrl+U or View → Page Source) - is `<nav>` element empty in served HTML?

```bash
# Check served HTML without JavaScript execution
curl -s https://example.com | grep -A 5 '<nav'

# Should show actual links, not empty element
```

Browser-based detection:

```javascript
// In browser console
document.querySelector('nav').innerHTML.trim() === ''
// Returns true if navigation is JavaScript-only
```

### Forces (Anti-Pattern 5)

- **Framework defaults:** React, Vue, and Angular default to client-side rendering without SSR
- **Development speed:** Client-only rendering is faster to implement than SSR or progressive enhancement
- **API-driven content:** Navigation data from APIs requires JavaScript to fetch and render
- **Dynamic content:** Personalized navigation based on user state (logged in, cart items) seems to require JavaScript
- **Performance perception:** Developers believe deferring navigation rendering improves initial load time
- **Modern tooling:** Build tools and frameworks prioritize JavaScript-first development patterns
- **Mobile optimization:** Hamburger menus with JavaScript animations seen as better mobile experience
- **Developer experience:** Easier to build navigation once in JavaScript than maintain HTML + JavaScript versions

### Solution (Anti-Pattern 5)

Implement navigation in served HTML with JavaScript providing progressive enhancement for interactions.

**Before (JavaScript-only navigation):**

```html
<nav id="main-nav"></nav>

<script>
  const navItems = [
    { text: 'Home', url: '/' },
    { text: 'Services', url: '/services' }
  ];

  const navHTML = navItems.map(item =>
    `<a href="${item.url}">${item.text}</a>`
  ).join('');

  document.getElementById('main-nav').innerHTML = navHTML;
</script>
```

**After (progressive enhancement approach):**

```html
<nav id="main-nav">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/services">Services</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>

<script>
  // JavaScript can enhance navigation (dropdowns, mobile menu, animations)
  // But base navigation works without it
  const nav = document.getElementById('main-nav');

  // Add mobile menu toggle (enhancement only)
  if (window.innerWidth < 768) {
    // Add hamburger menu functionality
    enhanceMobileNav(nav);
  }
</script>
```

**For API-driven navigation, use server-side rendering:**

```javascript
// Server-side (Node.js/Express example)
app.get('/', async (req, res) => {
  const navItems = await fetchNavigationFromAPI();

  res.render('index', {
    navigation: navItems  // Rendered into HTML on server
  });
});
```

### Resulting Context (Anti-Pattern 5)

After implementing navigation in served HTML:

- **Agent accessibility:** CLI agents and search engines can discover full site structure from any page
- **JavaScript-free environments:** Users with JavaScript disabled can still navigate the site
- **Performance improvement:** Navigation visible immediately, no JavaScript execution delay
- **Screen reader compatibility:** Navigation landmarks populated with meaningful links from page load
- **SEO benefits:** Search engines index navigation links without requiring JavaScript execution
- **Progressive enhancement:** JavaScript can add interactions (dropdowns, animations) without breaking core functionality
- **Testing simplification:** Automated tests can verify navigation without JavaScript execution

### Consequences (Anti-Pattern 5)

**Positive:**

- **Universal accessibility:** Works for CLI agents, search engines, screen readers, and JavaScript-disabled users
- **Better SEO:** Search engines discover all pages through HTML navigation links
- **Improved performance:** Navigation visible without waiting for JavaScript execution (better FCP, LCP metrics)
- **Progressive enhancement:** Core functionality works everywhere, enhancements available where supported
- **Resilient UX:** Site remains navigable if JavaScript fails to load or execute
- **Accessibility compliance:** WCAG 2.1 AA criterion 2.4.1 (Bypass Blocks) requires navigation landmarks
- **Testing simplicity:** Navigation can be verified without complex JavaScript execution in tests

**Negative/Trade-offs:**

- **Server-side rendering complexity:** Requires SSR setup (Next.js, Nuxt, or custom implementation)
- **Build complexity:** Need to maintain both server-rendered and client-enhanced navigation
- **API coordination:** Server must fetch navigation data before rendering page
- **Caching challenges:** Dynamic navigation (user-specific) harder to cache with SSR
- **Development time:** Progressive enhancement requires more planning than client-only approach
- **Framework limitations:** Some frameworks don't support SSR without significant refactoring

### Known Uses (Anti-Pattern 5)

**Common in:**

- React applications built with Create React App (CRA) without SSR
- Vue.js applications without Nuxt.js or custom SSR implementation
- Single-page applications (SPAs) that prioritize client-side routing
- Headless CMS implementations where navigation is fetched from APIs client-side
- JavaScript framework tutorials that demonstrate client-only patterns

**Specific examples:**

- E-commerce sites where navigation loads from product API after page load
- SaaS dashboards where navigation depends on fetching user permissions via JavaScript
- Marketing sites built with React where navigation is hardcoded in components but rendered client-side
- Portfolio sites using Gatsby or Next.js without SSR configuration
- Admin panels using Vue Router without server-side navigation fallback

### Related Patterns (Anti-Pattern 5)

**Fixes this anti-pattern:**

- Pattern 23: Progressive Enhancement (Chapter 12.8) - Core principle of building HTML-first with JavaScript enhancement
- Pattern 7: Server-Side Rendering (Appendix M) - Technical implementation of SSR for frameworks
- Pattern 14: Clear Navigation Labels (Appendix M) - Guidance on navigation structure and labeling

**Related anti-patterns:**

- Anti-pattern 6: Hidden Content with No Fallback - Similar JavaScript-dependency issue
- Anti-pattern 11: Content in iframes - Another pattern making content inaccessible to parsers
- Anti-pattern 1: Visual-Only Information - Related pattern of information inaccessible without specific rendering

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Progressive Enhancement principle)
- Chapter 11.3: The Convergence Principle (HTML-first benefits everyone)
- Chapter 12.8: Pattern 8 (Client-Side JavaScript)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)

---

## Anti-Pattern 6: Hidden Content with No Fallback

**Pattern ID:** `mx.anti-pattern.css.hidden-content-no-fallback`
**Status:** active
**Intent:** Ensure content is accessible by default with JavaScript providing optional interactions, not required functionality

### Context (Anti-Pattern 6)

This anti-pattern commonly appears in:

- Accordion components where FAQ content is hidden until users click to expand
- Tab interfaces where only the first tab panel is visible, others are `display: none`
- Modal dialogs with critical information that JavaScript shows on button click
- Collapsible sections where content is hidden by default to save vertical space
- "Read more" truncated content that expands only when JavaScript executes

It's typically introduced when:

- Developers prioritize compact visual design over content accessibility
- Component libraries default to hiding content until JavaScript-triggered interactions
- UX designers specify collapsible patterns without considering non-JavaScript scenarios
- Mobile-first design emphasizes space savings through hidden content
- Marketing sites hide long-form content assuming users prefer scannable pages
- Performance optimization attempts defer below-the-fold content rendering

### Problem (Anti-Pattern 6)

Content hidden behind interactions (`display: none`, `visibility: hidden`, or off-screen positioning) with no alternative access method for non-JavaScript agents or environments where JavaScript fails to load.

CLI agents and search engines parsing served HTML cannot execute JavaScript click handlers or trigger interactions. When content is hidden by default with CSS (`style="display: none"`) and only revealed through JavaScript, these agents never see the content. This creates information gaps where critical details like business hours, pricing, contact information, or FAQ answers remain invisible.

**Impact:**

- CLI agents cannot access hidden content, missing critical business information
- Search engines may not index content hidden behind JavaScript interactions
- Users with JavaScript disabled or failed loads see incomplete pages
- Screen readers encounter empty sections or unclear interactive patterns
- Automated testing requires JavaScript execution to verify content presence
- Poor initial page rendering (FOUC - Flash of Unstyled Content) when JavaScript delays
- SEO penalties for "thin content" when hidden text isn't indexed

### Detection Method (Anti-Pattern 6)

Disable JavaScript in browser settings, then reload page - does critical content remain hidden?

**Browser-based test:**

```javascript
// Check for content with display: none that might be critical
Array.from(document.querySelectorAll('[style*="display: none"], [style*="display:none"]'))
  .filter(el => el.textContent.trim().length > 50)
  .forEach(el => console.log('Hidden content:', el.textContent.substring(0, 100)));
```

### Forces (Anti-Pattern 6)

- **Visual design aesthetics:** Designers prefer clean, compact layouts with minimal scrolling
- **Mobile-first constraints:** Limited vertical space on mobile devices encourages content hiding
- **Component library defaults:** React, Vue, Bootstrap accordion/tab components default to hiding inactive content
- **Performance perception:** Developers believe hiding content improves perceived load time
- **User behavior assumptions:** Assumption that users prefer scannable pages over long-form content
- **Framework patterns:** JavaScript frameworks encourage interaction-driven content reveal patterns
- **Vertical space optimization:** Hiding content reduces page height, especially for FAQs and documentation
- **Developer convenience:** Easier to hide content with CSS than implement progressive enhancement

### Solution (Anti-Pattern 6)

Use progressive enhancement: show content by default in HTML, then JavaScript can add collapsing behavior as an enhancement.

**Before (content hidden by default):**

```html
<div class="accordion">
  <button class="accordion-header">What are your opening hours?</button>
  <div class="accordion-content" style="display: none;">
    Monday to Friday, 9am to 5pm
  </div>
</div>
```

**After (progressive enhancement):**

```html
<section class="accordion-section">
  <article class="accordion-item">
    <h3>
      <button class="accordion-header" aria-expanded="true">
        What are your opening hours?
      </button>
    </h3>
    <div class="accordion-content">
      Monday to Friday, 9am to 5pm
    </div>
  </article>
</section>

<script>
  // JavaScript collapses items after page load (enhancement only)
  document.querySelectorAll('.accordion-item').forEach(item => {
    const button = item.querySelector('.accordion-header');
    const content = item.querySelector('.accordion-content');

    // Collapse by default (JavaScript enhancement)
    content.style.display = 'none';
    button.setAttribute('aria-expanded', 'false');

    // Add click handler to toggle
    button.addEventListener('click', () => {
      const expanded = button.getAttribute('aria-expanded') === 'true';
      button.setAttribute('aria-expanded', !expanded);
      content.style.display = expanded ? 'none' : 'block';
    });
  });
</script>
```

**Key principle:** Content is visible in served HTML. JavaScript adds collapsing behavior as progressive enhancement.

### Resulting Context (Anti-Pattern 6)

After implementing progressive enhancement for hidden content:

- **Agent accessibility:** CLI agents and search engines see all content in served HTML
- **JavaScript-free environments:** Users with JavaScript disabled see all content
- **Improved SEO:** Search engines index all content, improving ranking signals
- **Screen reader compatibility:** Content accessible without requiring interaction
- **Performance improvement:** Content visible immediately, no wait for JavaScript
- **Resilient UX:** Site remains functional if JavaScript fails to load or execute
- **Better crawling:** Web crawlers discover all information without JavaScript execution

### Consequences (Anti-Pattern 6)

**Positive:**

- **Universal accessibility:** Content available to CLI agents, search engines, screen readers, and JavaScript-disabled users
- **Better SEO:** All content indexed by search engines, improving content depth signals
- **WCAG 2.1 AA compliance:** Satisfies criterion 4.1.2 (Name, Role, Value) for interactive controls
- **Improved performance:** Content visible without JavaScript execution delay
- **Resilient UX:** Progressive enhancement ensures functionality without JavaScript
- **Testing simplicity:** Content can be verified in served HTML without JavaScript execution
- **Future-proof:** Works with emerging AI systems that prioritize served HTML

**Negative/Trade-offs:**

- **Longer pages:** Showing all content by default increases vertical page length
- **Initial visual complexity:** More content visible initially may feel overwhelming
- **JavaScript overhead:** Need to collapse content after load creates brief visual shift (FOUC)
- **Design constraints:** Progressive enhancement requires rethinking interaction patterns
- **Component library limitations:** Popular component libraries default to hide-first patterns
- **Mobile scrolling:** Longer pages on mobile require more scrolling
- **Development effort:** Progressive enhancement requires more planning than hide-by-default approach

### Known Uses (Anti-Pattern 6)

**Common in:**

- Bootstrap accordion components with `data-bs-toggle` that hide panels by default
- React/Vue tab interfaces where inactive tab panels have `display: none`
- WordPress themes with FAQ sections using JavaScript-dependent show/hide
- E-commerce sites with "Product Details" sections collapsed until user clicks
- Documentation sites with collapsible API reference sections

**Specific examples:**

- FAQ pages where answers are hidden until questions are clicked, making content invisible to search engines
- Product pages with specifications hidden behind "View More Details" buttons
- Contact pages with business hours hidden in collapsed accordion until expanded
- Terms and conditions pages with sections collapsed by default (potential legal issues)
- Pricing pages with feature comparison tables hidden behind "Compare Plans" toggle

### Related Patterns (Anti-Pattern 6)

**Fixes this anti-pattern:**

- Pattern 23: Progressive Enhancement (Chapter 12.8) - Core principle of building functionality in layers
- Pattern 8: Client-Side JavaScript (Chapter 12.8) - Guidance on JavaScript as enhancement, not requirement
- Pattern 12: Explicit State Management (Appendix M) - How to make interactive states accessible

**Related anti-patterns:**

- Anti-pattern 5: JavaScript-Only Navigation - Similar JavaScript-dependency issue
- Anti-pattern 11: Content in iframes - Another pattern trapping content from parsers
- Anti-pattern 1: Visual-Only Information - Related pattern of inaccessible information

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Progressive Enhancement principle)
- Chapter 11.3: The Convergence Principle (accessible patterns help agents)
- Chapter 12.8: Pattern 8 (Client-Side JavaScript)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)

---

## Anti-Pattern 7: No Sitemap or Outdated Sitemap

**Pattern ID:** `mx.anti-pattern.navigation.missing-sitemap`
**Status:** active
**Intent:** Provide always-current XML sitemaps that enable AI agents and search engines to discover all site content efficiently

### Context (Anti-Pattern 7)

This anti-pattern commonly appears in:

- Small business websites where sitemaps were never created during initial development
- Rapidly-growing content sites where sitemaps aren't regenerated after new pages are added
- Legacy sites migrated from old platforms without sitemap migration
- Custom-built sites without automated sitemap generation in the build process
- E-commerce platforms where product pages are added but sitemaps aren't updated

It's typically introduced when:

- Developers skip sitemap creation for "small" sites, assuming manual navigation is sufficient
- Content management systems don't have automatic sitemap generation enabled
- Site migrations or redesigns break sitemap generation without being noticed
- Dynamic content (products, blog posts) is added without triggering sitemap regeneration
- Sitemap generation scripts break due to dependency updates or infrastructure changes
- Manual sitemap maintenance is neglected as sites grow beyond initial scope

### Problem (Anti-Pattern 7)

Missing sitemap.xml file or sitemap containing broken links, outdated URLs, or stale lastmod dates that mislead search engines and AI agents about site structure.

Search engines and AI agents use sitemaps as authoritative sources for discovering content. When sitemaps are missing, outdated, or incorrect, agents may miss new content, waste crawl budget on deleted pages, or fail to prioritize recently-updated pages. This is especially problematic for large sites where navigation links don't reach all pages or for dynamic content that changes frequently.

**Impact:**

- AI agents cannot efficiently discover all site pages, missing critical content
- Search engines waste crawl budget on deleted pages or miss new pages entirely
- New content takes longer to be indexed and appear in search results
- Automated testing tools cannot verify complete site coverage
- SEO auditing tools report incomplete site crawling
- Content discovery by AI systems is limited to followed links, missing orphaned pages
- Analytics show lower organic search traffic due to poor content indexing

### Detection Method (Anti-Pattern 7)

Visit `/sitemap.xml` - does it exist? Check dates and URLs for currency.

```bash
# Check if sitemap exists
curl -I https://example.com/sitemap.xml

# Download and inspect sitemap
curl -s https://example.com/sitemap.xml | head -50

# Validate lastmod dates are recent
curl -s https://example.com/sitemap.xml | grep '<lastmod>' | head -10
```

**Common issues to check:**

- Sitemap returns 404 (doesn't exist)
- Sitemap contains URLs that return 404 (broken links)
- `<lastmod>` dates are years old despite recent content updates
- Sitemap is missing recently added pages
- Sitemap contains URLs that redirect (should be canonical URLs)

### Forces (Anti-Pattern 7)

- **Development oversight:** Sitemaps often forgotten during initial site development
- **Manual maintenance burden:** Updating sitemaps manually is tedious and error-prone
- **Build process gaps:** Sitemap generation not integrated into deployment workflows
- **CMS limitations:** Some content management systems don't include sitemap generation by default
- **Dynamic content complexity:** Products, blog posts, user-generated content change frequently
- **Small site assumption:** Developers assume small sites don't need sitemaps (incorrect)
- **Lack of monitoring:** No alerts when sitemap generation fails or becomes outdated
- **Migration neglect:** Sitemaps often missed during platform migrations or redesigns

### Solution (Anti-Pattern 7)

Generate sitemaps automatically as part of build/deployment process, ensuring they always reflect current site structure.

**Automated generation (Node.js/Express example):**

```javascript
// Dynamic sitemap generation (Node.js/Express example)
app.get('/sitemap.xml', async (req, res) => {
  const pages = await getAllPages();
  const posts = await getAllBlogPosts();
  const products = await getAllProducts();

  let xml = '<?xml version="1.0" encoding="UTF-8"?>\n';
  xml += '<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">\n';

  [...pages, ...posts, ...products].forEach(item => {
    xml += '  <url>\n';
    xml += `    <loc>${item.url}</loc>\n`;
    xml += `    <lastmod>${item.updated.toISOString().split('T')[0]}</lastmod>\n`;
    xml += `    <priority>${item.priority || 0.8}</priority>\n`;
    xml += '  </url>\n';
  });

  xml += '</urlset>';

  res.header('Content-Type', 'application/xml');
  res.send(xml);
});
```

**Static site generation (build-time):**

```javascript
// scripts/generate-sitemap.js
const fs = require('fs');
const glob = require('glob');

// Find all HTML pages
const pages = glob.sync('dist/**/*.html');

const urls = pages.map(file => {
  const stats = fs.statSync(file);
  const url = file.replace('dist/', '').replace('/index.html', '/');

  return {
    loc: `https://example.com${url}`,
    lastmod: stats.mtime.toISOString().split('T')[0],
    priority: url === '/' ? 1.0 : 0.8
  };
});

const xml = generateSitemapXML(urls);
fs.writeFileSync('dist/sitemap.xml', xml);
```

**Best practices:**

- Regenerate sitemap whenever content changes (automated, not manual)
- Include accurate `<lastmod>` dates from actual content update times
- Use canonical URLs (no redirects)
- Submit sitemap to Google Search Console and Bing Webmaster Tools
- Monitor sitemap accessibility (set up alerts for 404s)
- Use sitemap index files for large sites (>50,000 URLs)

### Resulting Context (Anti-Pattern 7)

After implementing automated sitemap generation:

- **Agent discovery:** AI agents can efficiently discover all site content through sitemap
- **Improved crawling:** Search engines optimize crawl budget by following sitemap URLs
- **Faster indexing:** New content discovered and indexed more quickly
- **Better SEO:** Complete site coverage in search results
- **Accurate priorities:** `<priority>` values help search engines understand page importance
- **Fresh content signals:** `<lastmod>` dates tell search engines which pages changed recently
- **Monitoring capability:** Can track sitemap errors through Search Console

### Consequences (Anti-Pattern 7)

**Positive:**

- **Complete content discovery:** AI agents and search engines find all pages efficiently
- **Better SEO:** Improved indexing leads to more organic search traffic
- **Crawl budget optimization:** Search engines focus on actual content, not dead links
- **Faster new content indexing:** New pages discovered within hours instead of weeks
- **Improved rankings:** Fresh content signals through lastmod dates help SEO
- **Monitoring:** Search Console reports sitemap errors for proactive fixes
- **Compliance:** Meets search engine best practices and AI agent discovery standards

**Negative/Trade-offs:**

- **Build complexity:** Need to integrate sitemap generation into deployment pipeline
- **Server load:** Dynamic sitemap generation adds database queries (cache recommended)
- **Maintenance overhead:** Must keep sitemap generation logic updated as site evolves
- **Large site challenges:** Sites with millions of URLs need sitemap index files
- **Testing requirements:** Must test sitemap generation in CI/CD pipeline
- **Dependency management:** Third-party sitemap libraries need regular updates

### Known Uses (Anti-Pattern 7)

**Common in:**

- Small business websites built by freelancers without SEO expertise
- Custom-built sites where developers didn't implement sitemap generation
- WordPress sites without Yoast SEO or similar plugins
- Static sites built with custom generators missing sitemap scripts
- E-commerce platforms with thousands of products but no automated sitemap updates

**Specific examples:**

- Agency portfolio sites where new case studies are added but sitemap never updated
- Blog platforms where sitemap generated once during setup but never regenerated
- E-commerce sites with seasonal products where sitemap contains discontinued items
- Documentation sites where sitemap lists old versions but not latest docs
- Multi-language sites with broken sitemap links for non-English pages

### Related Patterns (Anti-Pattern 7)

**Fixes this anti-pattern:**

- Pattern 19: XML Sitemaps (Chapter 10) - Complete sitemap implementation guidance
- Pattern 15: robots.txt Configuration (Chapter 10) - Sitemap declaration in robots.txt
- Pattern 11: Content Discoverability (Appendix M) - Overall content discovery strategies

**Related anti-patterns:**

- Anti-pattern 5: JavaScript-Only Navigation - Similar discoverability issue
- Anti-pattern 11: Content in iframes - Content that's hard for agents to discover
- Anti-pattern 12: PDF-Only Content - Content that sitemaps can't help with

**Related chapters:**

- Chapter 10: How AI Agents Discover and Navigate Websites
- Chapter 12.10: Pattern 10 (Navigation Structure)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)

---

## Anti-Pattern 8: Inconsistent Schema.org

**Pattern ID:** `mx.anti-pattern.metadata.inconsistent-schema`
**Status:** active
**Intent:** Ensure Schema.org structured data matches visible content exactly, providing trustworthy machine-readable information

### Context (Anti-Pattern 8)

This anti-pattern commonly appears in:

- E-commerce product pages where Schema.org markup isn't updated when prices or availability change
- Event listing pages where Schema.org dates don't match visible dates after rescheduling
- Recipe sites where Schema.org ingredient lists are shortened or simplified
- Local business pages where Schema.org addresses or phone numbers don't match footer contact details
- Article pages where Schema.org publish dates differ from visible dates

It's typically introduced when:

- Schema.org markup is generated once during page creation but never updated
- Content editors update visible content without understanding Schema.org requirements
- Automated content management doesn't synchronize Schema.org with HTML updates
- Developers hardcode Schema.org data separately from dynamic content rendering
- Marketing teams run promotions that update visible prices but not structured data
- Template systems don't bind Schema.org properties to the same data sources as HTML

### Problem (Anti-Pattern 8)

Schema.org markup that contradicts visible content or is incomplete, creating confusion and trust issues for AI agents relying on structured data.

AI agents often prioritize Schema.org structured data over parsing HTML because it provides unambiguous, machine-readable information. When Schema.org markup contradicts visible content (different prices, names, dates, or availability), agents face a dilemma: trust the structured data or the HTML? This inconsistency erodes trust and can lead to agents making incorrect decisions or purchases based on inaccurate information.

**Impact:**

- AI agents use incorrect information (wrong prices, outdated availability, mismatched names)
- Trust erosion when agents discover structured data doesn't match visible content
- Search engine penalties for misleading structured data (Google rich snippet removal)
- Compliance violations (showing higher prices in Schema.org than visible prices)
- Failed Schema.org validation tests in Google Search Console
- AI agents may ignore all structured data after detecting inconsistencies
- Customer complaints when AI agents act on inaccurate structured data

### Real Example (Anti-Pattern 8)

**Before (inconsistent Schema.org):**

```html
<h1>Professional Standing Desk - White Oak Finish</h1>
<p>Price: £599 (currently on sale for £499)</p>

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Standing Desk",
  "offers": {
    "@type": "Offer",
    "price": "599",
    "priceCurrency": "GBP"
  }
}
</script>
```

**Problems:**

- Name mismatch: "Standing Desk" in Schema vs "Professional Standing Desk - White Oak Finish" in HTML
- Price mismatch: £599 in Schema vs £499 visible sale price
- Sale price not reflected in structured data
- Missing required fields: `availability`, `priceValidUntil`
- Missing optional but valuable fields: `brand`, `description`, `image`

### Forces (Anti-Pattern 8)

- **Content management separation:** Schema.org often generated from different data source than HTML
- **Marketing agility:** Promotions and price changes happen quickly without technical updates
- **Template complexity:** Harder to maintain synchronization across multiple output formats
- **Developer awareness:** Developers don't always understand Schema.org importance or requirements
- **Content editor training:** Editors update visible content but don't know Schema.org exists
- **Testing gaps:** Visual QA catches HTML issues but not Schema.org inconsistencies
- **Performance assumptions:** Developers believe updating Schema.org on every content change is too expensive
- **Legacy systems:** Old CMSes don't provide tools for synchronized Schema.org management

### Solution (Anti-Pattern 8)

Bind Schema.org properties to the same data sources as visible HTML, ensuring automatic synchronization.

**After (synchronized Schema.org):**

```html
<h1>Professional Standing Desk - White Oak Finish</h1>
<p>
  <span class="original-price">Was: £599</span>
  <strong class="sale-price">Now: £499</strong>
</p>

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Professional Standing Desk - White Oak Finish",
  "description": "Height-adjustable standing desk with white oak finish, supporting healthy work posture.",
  "brand": {
    "@type": "Brand",
    "name": "ErgoDesk Pro"
  },
  "image": "https://example.com/images/standing-desk-oak.jpg",
  "offers": {
    "@type": "Offer",
    "price": "499",
    "priceCurrency": "GBP",
    "priceValidUntil": "2026-12-31",
    "availability": "https://schema.org/InStock",
    "url": "https://example.com/products/standing-desk-oak"
  }
}
</script>
```

**Best practices for synchronization:**

```javascript
// Template approach (e.g., React, Vue, templating engines)
const product = {
  name: "Professional Standing Desk - White Oak Finish",
  price: 499,
  originalPrice: 599,
  currency: "GBP",
  inStock: true,
  saleEndDate: "2026-12-31"
};

// Render both HTML and Schema.org from same data
<h1>{product.name}</h1>
<p>
  <span className="original-price">Was: £{product.originalPrice}</span>
  <strong className="sale-price">Now: £{product.price}</strong>
</p>

<script type="application/ld+json">
{generateProductSchema(product)}
</script>
```

### Resulting Context (Anti-Pattern 8)

After synchronizing Schema.org with visible content:

- **Agent trust:** AI agents can rely on structured data as accurate and current
- **Consistent information:** All users (human and AI) see identical information
- **Better SEO:** Google rewards accurate structured data with rich snippets
- **Compliance:** No risk of consumer protection violations (price misrepresentation)
- **Easier maintenance:** Single data source reduces update errors
- **Validation success:** Passes Schema.org validators and Google Search Console checks
- **Enhanced features:** Accurate data enables rich search results, knowledge panels, voice assistant answers

### Consequences (Anti-Pattern 8)

**Positive:**

- **Agent reliability:** AI agents can trust structured data for accurate decision-making
- **Better SEO:** Rich snippets in search results (star ratings, prices, availability)
- **Legal compliance:** No price misrepresentation or false advertising violations
- **Improved conversions:** Accurate information in rich snippets drives qualified traffic
- **Trust building:** Consistent data builds confidence with AI agents
- **Future-proof:** Emerging AI systems rely heavily on Schema.org for understanding
- **Testing automation:** Automated tests can verify data consistency

**Negative/Trade-offs:**

- **Development complexity:** Requires data binding and synchronization logic
- **Template updates:** Must update both HTML and Schema.org when data model changes
- **Performance considerations:** Generating Schema.org on every page render (cache recommended)
- **Validation overhead:** Need to test Schema.org validators on every content update
- **Team training:** Content editors need to understand Schema.org impact
- **Debugging complexity:** Harder to diagnose issues spanning HTML and structured data

### Known Uses (Anti-Pattern 8)

**Common in:**

- E-commerce platforms where product prices update frequently but Schema.org is static
- Event management sites where Schema.org isn't updated after date changes
- Restaurant websites with Schema.org menus that don't match PDF menus
- Real estate listings where Schema.org prices lag behind visible prices
- Job boards where Schema.org postings show closed positions as still open

**Specific examples:**

- Amazon third-party sellers where listing updates don't regenerate Schema.org markup
- WordPress sites using outdated Schema.org plugins that don't sync with content
- Custom CMSes where marketing teams update prices but Schema.org remains static
- Recipe sites where Schema.org ingredient counts differ from visible recipe cards
- Local business directories where Schema.org phone numbers are outdated

### Related Patterns (Anti-Pattern 8)

**Fixes this anti-pattern:**

- Pattern 18: Schema.org Metadata (Chapter 12.18) - Complete Schema.org implementation guide
- Pattern 16: Structured Data Testing (Appendix M) - Testing and validation strategies
- Pattern 2: Page Metadata (Chapter 12.2) - General metadata synchronization principles

**Related anti-patterns:**

- Anti-pattern 1: Visual-Only Information - Related issue of information inaccessibility
- Anti-pattern 14: Context-Free References - Similar inconsistency problem
- Anti-pattern 2: Content in Images - Information not available in machine-readable format

**Related chapters:**

- Chapter 10: How AI Agents Discover and Navigate Websites (Schema.org discovery)
- Chapter 11.3: The Convergence Principle (accurate data helps everyone)
- Chapter 12.18: Pattern 18 (Schema.org Metadata)
- Chapter 12.2: Pattern 2 (Page Metadata)

---

## Anti-Pattern 9: Forms Without Labels

**Pattern ID:** `mx.anti-pattern.forms.missing-labels`
**Status:** active
**Intent:** Provide explicit label elements for all form inputs, enabling AI agents and assistive technologies to understand form structure and purpose

### Context (Anti-Pattern 9)

This anti-pattern commonly appears in:

- Modern minimalist design where designers rely on placeholder text for labels
- Mobile-first forms where screen space constraints encourage label omission
- Login forms with just "Username" and "Password" placeholder text
- Newsletter signup forms with single email input and placeholder
- Search forms with placeholder-only text like "Search..."

It's typically introduced when:

- Designers prioritize visual minimalism over semantic clarity
- Mobile app design patterns (placeholder-only) are copied to web without adaptation
- CSS frameworks demonstrate forms with placeholder-only patterns in documentation
- Developers don't understand the difference between placeholders and labels
- Rapid prototyping tools generate forms without proper label markup
- Time pressure leads to skipping "extra" HTML for labels

### Problem (Anti-Pattern 9)

Form inputs identified only by placeholder text, creating ambiguity and accessibility failures for AI agents, screen readers, and form-filling automation.

Placeholders are temporary hint text that disappears when users start typing. They're not substitutes for labels. AI agents and screen readers cannot reliably access placeholder text, and even when they can, the information disappears once the field has a value. This makes it impossible to review form data before submission or understand what a pre-filled field contains.

**Impact:**

- AI agents cannot understand form structure or determine which fields require what information
- Screen readers don't announce placeholder text consistently across browsers
- Form auto-fill features cannot correctly match labels to inputs
- Users cannot see field purpose once they start typing (placeholder disappears)
- Validation errors are ambiguous ("Email address is required" - which field was that?)
- Automated testing cannot reliably identify form fields
- Browser password managers cannot correctly associate credentials with fields

### Detection Method (Anti-Pattern 9)

Inspect forms - does each input have an associated `<label>` element?

```javascript
// Check for inputs without labels
Array.from(document.querySelectorAll('input, textarea, select'))
  .filter(input => {
    const id = input.id;
    const hasLabel = id && document.querySelector(`label[for="${id}"]`);
    return !hasLabel;
  })
  .forEach(input => {
    console.log('Input without label:', input.placeholder || input.type);
  });
```

### Forces (Anti-Pattern 9)

- **Visual minimalism:** Designers prefer clean forms with less visual clutter
- **Space constraints:** Mobile screens have limited vertical space for labels above inputs
- **App design influence:** Mobile app patterns (placeholder-only) seem modern and clean
- **Framework examples:** Bootstrap and other frameworks show placeholder-only forms in demos
- **Development speed:** Faster to add placeholder than both label and placeholder
- **Perceived redundancy:** Developers think label + placeholder is duplicative
- **User experience assumptions:** Belief that users prefer simpler-looking forms

### Solution (Anti-Pattern 9)

Always use explicit `<label>` elements properly associated with form inputs via `for` and `id` attributes.

**Before (placeholder-only):**

```html
<form>
  <input type="text" placeholder="Your name">
  <input type="email" placeholder="Email address">
  <textarea placeholder="Your message"></textarea>
  <button>Send</button>
</form>
```

**After (proper labels):**

```html
<form>
  <div class="form-field">
    <label for="name">Your Name</label>
    <input type="text" id="name" name="name" required
           placeholder="John Smith">
  </div>

  <div class="form-field">
    <label for="email">Email Address</label>
    <input type="email" id="email" name="email" required
           placeholder="john@example.com">
  </div>

  <div class="form-field">
    <label for="message">Your Message</label>
    <textarea id="message" name="message" rows="5" required
              placeholder="Tell us about your project..."></textarea>
  </div>

  <button type="submit">Send Message</button>
</form>
```

**Note:** Placeholders can still be used for format hints (e.g., `john@example.com`) when proper labels exist.

### Resulting Context (Anti-Pattern 9)

After implementing proper form labels:

- **Agent understanding:** AI agents can identify form structure and required fields
- **Screen reader accessibility:** Screen readers announce labels consistently
- **Form auto-fill:** Browsers can correctly match saved data to fields
- **Better UX:** Users always see field purpose, even while typing
- **Clear validation:** Error messages can reference visible labels
- **Password managers:** Browsers can reliably associate credentials with correct fields
- **Testing reliability:** Automated tests can locate fields by label text

### Consequences (Anti-Pattern 9)

**Positive:**

- **Universal accessibility:** Works for AI agents, screen readers, keyboard navigation, form auto-fill
- **WCAG 2.1 AA compliance:** Satisfies success criteria 1.3.1 (Info and Relationships), 3.3.2 (Labels or Instructions), 4.1.2 (Name, Role, Value)
- **Better form completion rates:** Clear labels reduce user confusion and abandonment
- **Improved auto-fill:** Browser auto-fill works reliably, speeding up form completion
- **Clear error messaging:** Validation errors can reference specific label text
- **Testing automation:** Tests can reliably locate and fill form fields
- **Password manager support:** Browsers correctly save and fill credentials

**Negative/Trade-offs:**

- **More vertical space:** Labels above inputs increase form height
- **Visual complexity:** More visible text elements create denser appearance
- **Design constraints:** Labels limit layout flexibility compared to placeholder-only
- **Mobile considerations:** Labels take more vertical space on small screens
- **Localization overhead:** More text to translate (labels + placeholders)

### Known Uses (Anti-Pattern 9)

**Common in:**

- Minimalist landing pages with single email signup forms using placeholder-only
- Mobile apps ported to web without adapting to proper HTML form semantics
- Login forms with just username/password placeholders and no labels
- Search bars with placeholder "Search..." and no visible label
- Contact forms designed for visual appeal over accessibility

**Specific examples:**

- Newsletter signup forms: `<input type="email" placeholder="Enter your email">`
- Search interfaces: `<input type="search" placeholder="Search products...">`
- Login pages: `<input type="password" placeholder="Password">` without label
- Comment forms: `<textarea placeholder="Leave a comment...">` without label
- Quick contact forms on mobile sites with placeholder-only inputs

### Related Patterns (Anti-Pattern 9)

**Fixes this anti-pattern:**

- Pattern 13: Form Accessibility (Chapter 12.13) - Complete form accessibility guidance
- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Proper HTML form elements
- Pattern 3: Keyboard Navigation (Chapter 12.3) - Form keyboard accessibility

**Related anti-patterns:**

- Anti-pattern 3: Generic Link Text - Similar issue of unclear element purpose
- Anti-pattern 1: Visual-Only Information - Related pattern of inaccessible information
- Anti-pattern 4: Broken Heading Hierarchy - Also impacts document structure understanding

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Semantic First principle)
- Chapter 11.3: The Convergence Principle (accessible forms help everyone)
- Chapter 12.13: Pattern 13 (Form Accessibility)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)

---

## Anti-Pattern 10: Table Abuse for Layout

**Pattern ID:** `mx.anti-pattern.html.table-for-layout`
**Status:** active
**Intent:** Use tables exclusively for tabular data with proper semantic structure, not for visual layout purposes

### Context (Anti-Pattern 10)

This anti-pattern commonly appears in:

- Legacy websites (pre-2010) where tables were the primary layout tool before CSS Grid/Flexbox
- Email templates where table-based layouts remain necessary due to email client limitations
- Sites migrated from older CMSes without layout modernization
- Data tables created by developers unfamiliar with semantic table markup
- Pricing comparison pages where tables lack proper header structure

It's typically introduced when:

- Developers maintain legacy code without modernizing layout patterns
- Tables are used for visual alignment without considering semantic meaning
- Data tables are created quickly without accessibility considerations
- WYSIWYG editors generate table-based layouts for visual positioning
- Developers copy email template patterns (table layouts) to web pages
- Framework components generate tables without proper semantic structure

### Problem (Anti-Pattern 10)

Tables used for layout purposes OR data tables without proper semantic structure (missing `<th>`, `<caption>`, `<thead>`, `<tbody>`, or scope attributes).

AI agents and screen readers rely on table markup to understand data relationships. When tables are used purely for layout, agents misinterpret content as tabular data. When data tables lack semantic structure (header cells, captions, scope attributes), agents cannot distinguish headers from data cells or understand row/column relationships.

**Impact:**

- AI agents misinterpret layout tables as containing related data
- Screen readers announce layout tables cell-by-cell, creating confusion
- Data tables without headers are incomprehensible to screen reader users
- Search engines cannot extract structured data from improperly marked tables
- Automated testing cannot verify table data relationships
- Voice interfaces cannot answer questions about table data
- SEO penalties for data tables presented as plain text (missing semantic structure)

### Forces (Anti-Pattern 10)

- **Legacy patterns:** Tables were standard for layout before CSS Grid/Flexbox
- **Email compatibility:** Table layouts still necessary for HTML emails
- **Quick implementation:** Faster to use all `<td>` cells than think about `<th>` structure
- **Visual appearance:** Tables "just work" for visual alignment without CSS knowledge
- **WYSIWYG editor output:** Visual editors generate table-heavy HTML
- **Framework gaps:** Some component libraries don't generate semantic table markup
- **Developer awareness:** Not all developers understand semantic table requirements
- **Migration reluctance:** Modernizing legacy table layouts requires significant effort

### Solution (Anti-Pattern 10)

**For layout:** Use CSS Grid or Flexbox instead of tables.

**For data tables:** Include proper semantic structure with `<caption>`, `<thead>`, `<th>`, scope attributes.

**Before (improper data table):**

```html
<table>
  <tr>
    <td>Plan</td>
    <td>Price</td>
    <td>Users</td>
  </tr>
  <tr>
    <td>Basic</td>
    <td>£29</td>
    <td>5</td>
  </tr>
</table>
```

**After (proper semantic data table):**

```html
<table>
  <caption>Pricing Plan Comparison</caption>
  <thead>
    <tr>
      <th scope="col">Plan Name</th>
      <th scope="col">Monthly Price</th>
      <th scope="col">Maximum Users</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Basic</th>
      <td>£29</td>
      <td>5</td>
    </tr>
    <tr>
      <th scope="row">Professional</th>
      <td>£99</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
```

**For layout replacement (CSS Grid example):**

```html
<!-- Before: Table for layout -->
<table>
  <tr>
    <td>Sidebar content</td>
    <td>Main content</td>
  </tr>
</table>

<!-- After: CSS Grid -->
<div class="layout-grid">
  <aside>Sidebar content</aside>
  <main>Main content</main>
</div>

<style>
.layout-grid {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 20px;
}
</style>
```

### Resulting Context (Anti-Pattern 10)

After implementing proper table semantics:

- **Agent understanding:** AI agents correctly identify tabular data and understand relationships
- **Screen reader clarity:** Screen readers announce "Plan Name column header: Basic" instead of "Plan Basic"
- **Data extraction:** Search engines and AI can extract structured data from tables
- **Voice interface support:** Users can ask "What's the price for Professional plan?" and get accurate answers
- **Better SEO:** Rich snippets can display table data in search results
- **Testing reliability:** Automated tests can verify table data structure
- **Maintainability:** Semantic markup is self-documenting

### Consequences (Anti-Pattern 10)

**Positive:**

- **Universal accessibility:** Tables understandable by AI agents, screen readers, and search engines
- **WCAG 2.1 AA compliance:** Satisfies criterion 1.3.1 (Info and Relationships)
- **Data extraction:** Search engines can extract and display table data in rich results
- **Voice interface answers:** AI assistants can answer questions about table contents
- **Better navigation:** Screen readers can jump between table headers
- **Testing automation:** Tests can verify data relationships programmatically
- **Future-proof:** Semantic tables work with emerging AI analysis tools

**Negative/Trade-offs:**

- **More markup:** Semantic tables require more HTML than simple `<td>` grids
- **Learning curve:** Developers need to understand `<th>`, `scope`, `<caption>`, `<thead>`, `<tbody>`
- **Migration effort:** Converting layout tables to CSS Grid/Flexbox is time-intensive
- **Legacy support:** Some very old browsers don't fully support CSS Grid (increasingly rare)
- **Email templates:** Table-based layouts still necessary for HTML email compatibility

### Known Uses (Anti-Pattern 10)

**Common in:**

- Legacy corporate websites built before 2010 with table-based layouts
- WordPress themes from early 2000s using tables for page structure
- Pricing comparison pages where all cells are `<td>` without `<th>` headers
- E-commerce product specifications using tables without semantic structure
- Email templates (justified for emails, anti-pattern when copied to web)

**Specific examples:**

- SaaS pricing tables showing plan features without column/row headers
- Restaurant menu tables with dish names and prices using only `<td>` cells
- Technical specification tables for products lacking `<th>` elements
- Event schedules in tables without `<caption>` or proper time/session headers
- Course catalogs with table listings but no semantic row/column relationships

### Related Patterns (Anti-Pattern 10)

**Fixes this anti-pattern:**

- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Complete semantic HTML guidance including tables
- Pattern 6: Data Tables (Appendix M) - Comprehensive table accessibility patterns
- Pattern 12: WCAG 2.1 AA Compliance (Chapter 12.12) - Accessibility requirements for tables

**Related anti-patterns:**

- Anti-pattern 4: Broken Heading Hierarchy - Similar misuse of semantic elements
- Anti-pattern 1: Visual-Only Information - Related pattern of ignoring semantic meaning
- Anti-pattern 9: Forms Without Labels - Also about missing semantic relationships

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Semantic First principle)
- Chapter 11.3: The Convergence Principle (semantic tables help everyone)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)
- Chapter 12.12: Pattern 12 (WCAG 2.1 AA Compliance)

---

## Anti-Pattern 11: Content in Iframes

**Pattern ID:** `mx.anti-pattern.html.iframe-content-trap`
**Status:** active
**Intent:** Render critical content directly in HTML rather than loading it through iframes, ensuring AI agent accessibility

### Context (Anti-Pattern 11)

This anti-pattern commonly appears in:

- Marketing sites embedding third-party widgets (social feeds, reviews, calendars)
- Corporate websites using iframe-based content management for news or events
- Sites embedding external booking systems, forms, or scheduling tools
- Documentation sites using iframe-embedded interactive examples
- Multi-brand sites using iframes to include content from other company domains

It's typically introduced when:

- Third-party services provide only iframe embed codes, not APIs
- Content management workflows separate content into different systems
- Security policies restrict direct domain integration
- Legacy systems integrate via iframes rather than modern APIs
- Marketing teams add widgets without developer involvement
- Cross-origin resource sharing (CORS) limitations prevent direct integration

### Problem (Anti-Pattern 11)

Important content loaded in iframes from external sources, making it inaccessible to CLI agents and difficult for search engines to index.

Iframes create content boundaries that AI agents typically cannot cross. When agents parse a page containing `<iframe src="external-url">`, they see only the iframe element itself, not the content within. This is by design - iframes are security boundaries preventing cross-origin access. For agents to access iframe content, they must separately fetch and parse the iframe source URL, which many agents don't do automatically.

**Impact:**

- CLI agents cannot see content within iframes, missing critical information
- Search engines may not index iframe content or associate it with the parent page
- Screen readers encounter iframe boundaries that interrupt content flow
- Automated testing cannot access iframe content without special handling
- SEO penalties for "thin content" when important text is in iframes
- Analytics cannot track user interactions within third-party iframes
- Performance issues from loading multiple separate documents

### Forces (Anti-Pattern 11)

- **Third-party integration ease:** Iframe embed codes are quickest integration method
- **Security isolation:** Iframes prevent third-party JavaScript from accessing parent page
- **Cross-domain policies:** CORS restrictions make direct integration complex
- **Content management separation:** Different teams manage different content systems
- **Legacy system integration:** Older systems offer only iframe-based integration
- **Marketing autonomy:** Non-technical teams can add iframes without developer help
- **Vendor limitations:** Some services provide only iframe embeds, not APIs

### Solution (Anti-Pattern 11)

Pull content server-side via APIs and render directly in HTML, avoiding iframes for critical content.

**Before (iframe-embedded content):**

```html
<h2>Our Latest News</h2>
<iframe src="https://news-widget.example.com/feed"></iframe>
```

**After (server-side rendering):**

```html
<section>
  <h2>Our Latest News</h2>

  <article>
    <h3><a href="/news/new-service-launch">New Service Launch</a></h3>
    <time datetime="2024-03-20">20 March 2024</time>
    <p>We're introducing Edge Delivery Services consulting...</p>
  </article>

  <article>
    <h3><a href="/news/team-expansion">Team Expansion</a></h3>
    <time datetime="2024-03-15">15 March 2024</time>
    <p>Digital Domain welcomes three new consultants...</p>
  </article>
</section>
```

**Server-side implementation example:**

```javascript
// Server-side (Node.js/Express)
app.get('/', async (req, res) => {
  // Fetch content from API instead of embedding iframe
  const newsArticles = await fetch('https://api.example.com/news/recent')
    .then(r => r.json());

  res.render('index', {
    articles: newsArticles  // Rendered directly in HTML
  });
});
```

**When iframes are necessary:** Use them only for truly isolated functionality (payment forms, third-party authentication) and provide alternative text description.

### Resulting Context (Anti-Pattern 11)

After rendering content directly in HTML:

- **Agent accessibility:** AI agents can parse all content without iframe barriers
- **Better SEO:** Search engines index content as part of the main page
- **Improved performance:** Single page load instead of multiple iframe requests
- **Screen reader continuity:** Content flows naturally without iframe interruptions
- **Analytics visibility:** User interactions tracked in main page analytics
- **Testing simplification:** Automated tests access all content without iframe handling
- **Consistent styling:** Content matches site design without iframe CSS constraints

### Consequences (Anti-Pattern 11)

**Positive:**

- **Universal accessibility:** Content available to all AI agents and search engines
- **Better SEO:** Full content indexed and associated with page
- **Improved performance:** Fewer HTTP requests, faster page loads
- **Design consistency:** Content styled with main site CSS
- **Analytics integration:** All user interactions tracked
- **Testing simplicity:** No special iframe handling in tests
- **User experience:** No iframe scrollbars or layout issues

**Negative/Trade-offs:**

- **Development complexity:** Server-side API integration more complex than iframe embeds
- **Security considerations:** Must sanitize third-party content carefully
- **Caching challenges:** Need to implement caching for external content
- **API dependencies:** Requires reliable APIs, not just embed codes
- **Cross-origin limitations:** Some content genuinely can't be fetched cross-origin
- **Maintenance overhead:** Must handle API changes and errors

### Known Uses (Anti-Pattern 11)

**Common in:**

- Corporate websites embedding third-party event calendars via iframes
- E-commerce sites using iframe-embedded product reviews (Trustpilot, Feefo)
- Restaurant websites embedding booking widgets in iframes
- News sites embedding social media feeds via iframe widgets
- Portfolio sites with iframe-embedded case studies from external CMSes

**Specific examples:**

- Google Calendar embeds on company "Events" pages
- Twitter/X timeline widgets embedded in "Latest Updates" sections
- Instagram feed widgets on photography portfolio sites
- External blog platform content embedded on main company site
- Third-party forms (Typeform, Google Forms) embedded for contact/survey

### Related Patterns (Anti-Pattern 11)

**Fixes this anti-pattern:**

- Pattern 17: Server-Side Rendering (Appendix M) - Technical approach for rendering external content
- Pattern 19: API Integration (Appendix M) - Best practices for third-party API usage
- Pattern 5: Semantic HTML Structure (Chapter 12.5) - Proper HTML content structure

**Related anti-patterns:**

- Anti-pattern 5: JavaScript-Only Navigation - Similar content accessibility issue
- Anti-pattern 6: Hidden Content with No Fallback - Related content isolation problem
- Anti-pattern 12: PDF-Only Content - Another pattern trapping content in inaccessible formats

**Related chapters:**

- Chapter 10: How AI Agents Discover and Navigate Websites
- Chapter 11.3: The Convergence Principle (direct HTML benefits everyone)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)
- Chapter 12.8: Pattern 8 (Client-Side JavaScript)

---

## Anti-Pattern 12: PDF-Only Content

**Pattern ID:** `mx.anti-pattern.content.pdf-only`
**Status:** active
**Intent:** Provide content in accessible HTML format with PDF as optional download, not as the only format

### Context (Anti-Pattern 12)

This anti-pattern commonly appears in:

- Corporate websites offering services brochures, white papers, or case studies as PDF-only downloads
- Government and academic sites publishing reports exclusively as PDFs
- Restaurant websites with menus only available as scanned PDF documents
- Event sites with schedules, speaker bios, or programmes as PDF downloads
- Product documentation sites requiring PDF downloads to read instructions

It's typically introduced when:

- Content originates from print design workflows (brochures, reports) and isn't adapted for web
- Content management systems don't support rich web content, defaulting to PDF uploads
- Print-first organizations prioritize PDF as "official" format
- Marketing teams create PDFs in design tools without considering web alternatives
- Legal/compliance teams require "final" PDF versions, discouraging HTML versions
- Legacy workflows assume PDFs preserve formatting better than HTML

### Problem (Anti-Pattern 12)

Important information only available as PDF downloads, creating accessibility barriers for AI agents and many human users who cannot easily parse or navigate PDF content.

PDF files are designed for print, not digital accessibility. AI agents struggle to extract structured information from PDFs - text order may not match visual layout, tables become plain text, headings aren't semantic, and forms aren't interactive. Many mobile users find PDFs difficult to read, and screen reader users encounter unpredictable PDF accessibility depending on how the file was created.

**Impact:**

- CLI agents cannot reliably extract structured information from PDFs
- Search engines index PDFs less effectively than HTML, reducing SEO
- Mobile users struggle with PDF navigation and zooming
- Screen readers encounter variable PDF accessibility (often poor)
- Users must download files to view content, adding friction
- Content not searchable within page (need to download and open)
- Analytics cannot track user engagement with PDF content
- No responsive design - PDFs don't adapt to screen sizes

### Forces (Anti-Pattern 12)

- **Print-first workflows:** Content created for print assumes PDF is natural digital format
- **Design tool outputs:** InDesign, Illustrator, Canva export to PDF, not HTML
- **Perceived professionalism:** PDFs seen as more "official" or "polished" than web pages
- **Format preservation:** PDFs maintain exact layout across platforms (HTML doesn't)
- **Legal requirements:** Some organizations require "final" PDF versions for compliance
- **Legacy infrastructure:** Older CMSes make PDF upload easier than rich HTML creation
- **Brand consistency:** Marketing teams control PDF design, less control over HTML rendering
- **Workflow inertia:** Existing processes produce PDFs, changing workflows requires effort

### Solution (Anti-Pattern 12)

Provide content in HTML as primary format, offer PDF as optional download for printing or offline use.

**Before (PDF-only):**

```html
<h2>Our Services</h2>
<p>Download our services brochure to learn more.</p>
<a href="/brochure.pdf">Download PDF (2.3 MB)</a>
```

**After (HTML primary, PDF optional):**

```html
<section>
  <h2>Our Services</h2>

  <article>
    <h3>Edge Delivery Services</h3>
    <p>Modern web delivery using Adobe's Edge Delivery Services platform...</p>
    <ul>
      <li>Migration from legacy CMS platforms</li>
      <li>Custom block development</li>
      <li>Performance optimization</li>
    </ul>
  </article>

  <article>
    <h3>AEM Consulting</h3>
    <p>Strategic advisory for Adobe Experience Manager implementations...</p>
    <ul>
      <li>Architecture planning</li>
      <li>Implementation guidance</li>
      <li>Team training</li>
    </ul>
  </article>

  <aside>
    <p>
      <a href="/services-brochure.pdf">Download this information as PDF</a>
      (2.3 MB, for printing or offline reading)
    </p>
  </aside>
</section>
```

### Resulting Context (Anti-Pattern 12)

After providing HTML versions of PDF-only content:

- **Agent accessibility:** AI agents can parse structured HTML content reliably
- **Better SEO:** Search engines index HTML content effectively
- **Mobile friendly:** Responsive HTML adapts to all screen sizes
- **Instant access:** No download required, content visible immediately
- **In-page search:** Users can use browser find (Ctrl+F) without downloading
- **Analytics tracking:** Can measure user engagement with content
- **Screen reader accessibility:** Semantic HTML works consistently with assistive technology
- **Print option still available:** PDF still offered for users who prefer it

### Consequences (Anti-Pattern 12)

**Positive:**

- **Universal accessibility:** Content accessible to AI agents, mobile users, screen readers
- **Better SEO:** HTML content indexed and ranked higher than PDFs
- **Improved user experience:** No download friction, instant access
- **Responsive design:** Content adapts to all screen sizes and devices
- **Analytics integration:** Track content engagement and user behavior
- **Lower friction:** Users don't need PDF readers or downloads
- **Future-proof:** HTML works on emerging platforms and devices

**Negative/Trade-offs:**

- **Dual maintenance:** Need to maintain both HTML and PDF versions
- **Workflow changes:** Requires adapting print-first content creation processes
- **Design control:** Less precise layout control compared to PDF
- **CMS requirements:** Need CMS capable of rich HTML content, not just file uploads
- **Team training:** Content creators need HTML/CMS skills, not just design tools
- **Brand consistency challenges:** Harder to enforce exact visual consistency across browsers

### Known Uses (Anti-Pattern 12)

**Common in:**

- Corporate annual reports published as PDF-only downloads
- Restaurant menus as scanned PDF files instead of HTML
- Government policy documents and regulations as PDF-only publications
- University course catalogs and syllabi as downloadable PDFs
- White papers and research reports available exclusively as PDFs

**Specific examples:**

- Service provider "Services" pages with single PDF brochure link
- Event sites with speaker schedules only in downloadable PDF programme
- Product sites with instruction manuals only as PDF downloads
- Real estate listings with property details in PDF flyers
- Healthcare sites with patient information sheets as PDF-only downloads

### Related Patterns (Anti-Pattern 12)

**Fixes this anti-pattern:**

- Pattern 5: Semantic HTML Structure (Chapter 12.5) - How to structure content in HTML
- Pattern 20: Accessible Documents (Appendix M) - When PDFs are necessary, making them accessible
- Pattern 2: Page Metadata (Chapter 12.2) - Proper metadata for HTML content

**Related anti-patterns:**

- Anti-pattern 2: Content in Images - Similar content trap in non-HTML format
- Anti-pattern 11: Content in Iframes - Another pattern isolating content from agents
- Anti-pattern 6: Hidden Content with No Fallback - Related accessibility barrier pattern

**Related chapters:**

- Chapter 10: How AI Agents Discover and Navigate Websites
- Chapter 11.3: The Convergence Principle (HTML benefits everyone)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)
- Chapter 9: Content That Works for Agents

---

## Anti-Pattern 13: Auto-Playing Content

**Pattern ID:** `mx.anti-pattern.media.auto-playing`
**Status:** active
**Intent:** Ensure all content is statically accessible in HTML with auto-play as optional visual enhancement, not a requirement for content access

### Context (Anti-Pattern 13)

This anti-pattern commonly appears in:

- Homepage hero sections with auto-rotating carousel slides
- Testimonial sections with testimonials cycling every few seconds
- News/blog sections with auto-scrolling latest articles
- Product showcase pages with auto-advancing feature highlights
- Portfolio sites with auto-playing project galleries

It's typically introduced when:

- Marketing teams request "dynamic" visual effects for engagement
- Design trends favor carousel components for space efficiency
- UX assumptions prioritize visual variety over content accessibility
- Component libraries include auto-play as default behavior
- Developers implement "modern" interactions without considering agent access
- Mobile design patterns encourage single-item-at-a-time displays

### Problem (Anti-Pattern 13)

Content that changes automatically (carousels, testimonials, rotating banners) making specific information impossible to reference directly and inaccessible to AI agents that parse static HTML.

AI agents parse HTML at a single moment in time. They cannot wait for carousel rotations or witness auto-playing content changes. When only the first carousel slide exists in served HTML (others loaded via JavaScript), agents see only that first item. Even when all slides exist in HTML but are hidden (`display: none`), agents may struggle to determine which content is actually "current" or relevant.

**Impact:**

- AI agents see only the first carousel slide, missing other content entirely
- Users cannot directly link to specific carousel items
- Screen reader users must wait through auto-play cycles to hear all content
- Search engines may index only the first visible item
- Auto-play violates WCAG 2.1 criterion 2.2.2 (Pause, Stop, Hide) when content moves for >5 seconds
- Analytics cannot track which carousel items users actually viewed
- Voice interface users cannot request specific carousel items by name

### Forces (Anti-Pattern 13)

- **Visual dynamism:** Auto-play creates perception of "modern" interactive site
- **Space efficiency:** Carousels show multiple items in limited vertical space
- **Marketing pressure:** Teams want to highlight multiple features/products prominently
- **Engagement assumptions:** Belief that movement increases user engagement
- **Component library defaults:** Popular libraries (Slick, Swiper) default to auto-play
- **Mobile optimization:** Single-item display seen as better for small screens
- **Design trends:** Industry patterns favor carousel components

### Solution (Anti-Pattern 13)

Show all content in static HTML, use JavaScript/CSS for optional visual carousel behavior.

**Before (auto-playing, limited HTML):**

```html
<div class="testimonials-carousel" data-autoplay="3000">
  <div class="testimonial">
    <p>"Great service!" - Client A</p>
  </div>
  <div class="testimonial">
    <p>"Highly recommend" - Client B</p>
  </div>
</div>
```

**After (all content in HTML, carousel as enhancement):**

```html
<section class="testimonials">
  <h2>Client Testimonials</h2>

  <article class="testimonial">
    <blockquote>
      <p>Digital Domain transformed our web presence. The migration to Edge Delivery Services was seamless.</p>
    </blockquote>
    <figcaption>
      <cite>Sarah Johnson, CTO at AutoCorp</cite>
    </figcaption>
  </article>

  <article class="testimonial">
    <blockquote>
      <p>Tom's expertise in AEM saved us months of development time.</p>
    </blockquote>
    <figcaption>
      <cite>David Chen, Head of Digital at FinanceGroup</cite>
    </figcaption>
  </article>

  <article class="testimonial">
    <blockquote>
      <p>The training programme upskilled our entire team.</p>
    </blockquote>
    <figcaption>
      <cite>Emma Williams, Development Manager at RetailHub</cite>
    </figcaption>
  </article>
</section>

<script>
  // JavaScript can add carousel functionality as visual enhancement
  // Use CSS to show one at a time visually for human users
  // But keep all content in DOM for AI agents and screen readers
  // Disable auto-play by default (let users control)
</script>
```

### Resulting Context (Anti-Pattern 13)

After providing all content in static HTML:

- **Agent accessibility:** AI agents see all carousel content without waiting
- **Direct linking:** Each item can be linked to directly via anchor IDs
- **Screen reader access:** All content available immediately, no forced waiting
- **Search indexing:** All carousel items indexed by search engines
- **WCAG compliance:** Satisfies 2.2.2 (Pause, Stop, Hide) by avoiding auto-play
- **Analytics tracking:** Can measure actual user interaction with each item
- **User control:** Users can navigate carousel at their own pace

### Consequences (Anti-Pattern 13)

**Positive:**

- **Universal accessibility:** All content accessible to AI agents, screen readers, search engines
- **WCAG 2.1 AA compliance:** Satisfies criterion 2.2.2 (Pause, Stop, Hide) and 2.1.1 (Keyboard)
- **Better SEO:** All items indexed, not just the first slide
- **User control:** Users navigate at their own pace without forced auto-play
- **Direct linking:** Specific carousel items can be bookmarked and shared
- **Reduced cognitive load:** Content doesn't disappear before users finish reading
- **Testing simplicity:** All content present in HTML for automated testing

**Negative/Trade-offs:**

- **Longer pages:** All content visible increases vertical page length
- **Less visual dynamism:** Static content perceived as less "interactive"
- **Design constraints:** Need to design for all-items-visible layout
- **Component library conflicts:** Popular carousel libraries assume auto-play
- **Marketing resistance:** Teams may resist losing animated visual effects
- **Mobile scrolling:** More content means more scrolling on small screens

### Known Uses (Anti-Pattern 13)

**Common in:**

- Homepage hero sections with auto-rotating banner slides showcasing different services
- Bootstrap Carousel components with `data-ride="carousel"` auto-play enabled
- Testimonial sections using Slick Slider with auto-advance every 3-5 seconds
- Product showcase carousels auto-cycling through feature highlights
- News sections with auto-scrolling latest articles

**Specific examples:**

- E-commerce homepages with hero carousels cycling through promotional banners
- Agency portfolio sites with auto-playing project showcases
- SaaS landing pages with feature carousels that auto-advance
- Restaurant sites with auto-rotating food photo galleries
- Real estate sites with auto-playing property listings on homepage

### Related Patterns (Anti-Pattern 13)

**Fixes this anti-pattern:**

- Pattern 23: Progressive Enhancement (Chapter 12.8) - Carousel as visual enhancement, not requirement
- Pattern 12: Explicit State Management (Appendix M) - Making carousel state accessible
- Pattern 22: Animation and Motion (Appendix M) - Accessible animation patterns

**Related anti-patterns:**

- Anti-pattern 6: Hidden Content with No Fallback - Similar content hiding issue
- Anti-pattern 1: Visual-Only Information - Related assumption of visual presentation
- Anti-pattern 5: JavaScript-Only Navigation - Similar dependence on JavaScript for core functionality

**Related chapters:**

- Chapter 11.2: Four Guiding Principles (Progressive Enhancement, Semantic First)
- Chapter 11.3: The Convergence Principle (static content helps everyone)
- Chapter 12.8: Pattern 8 (Client-Side JavaScript)
- Chapter 12.12: Pattern 12 (WCAG 2.1 AA Compliance)

---

## Anti-Pattern 14: Context-Free References

**Pattern ID:** `mx.anti-pattern.content.context-free-references`
**Status:** active
**Intent:** Preserve document context when files are extracted from repository structure by providing both relative and absolute references

### Context (Anti-Pattern 14)

This anti-pattern commonly appears in:

- GitHub repository documentation with relative links between markdown files
- Technical documentation repositories with cross-file references
- Multi-repository project documentation with links to other repos
- README files referencing other docs via relative paths like `../../docs/guide.md`
- Confluence/wiki exports with broken relative links

It's typically introduced when:

- Documentation is written within IDEs where relative links work perfectly
- Version control workflows prioritize repository-relative paths
- Markdown editors show working relative links in preview
- Documentation generators expect repository context
- Teams don't consider documents being read outside repository structure
- PDF generation or documentation exports aren't tested

### Problem (Anti-Pattern 14)

Relative links in documentation that lose all context when files are extracted, downloaded, printed to PDF, or processed by AI agents outside the repository structure.

When AI agents fetch individual documentation files (via API, web scraping, or direct download), they receive files without repository context. A link like `[README.md](../../README.md)` becomes meaningless - what's two directories up from a standalone file? Where does the path resolve to? Which repository? What branch? The link destination cannot be determined without the original file system structure.

**Impact:**

- AI agents cannot follow cross-document references in extracted documentation
- PDF exports of documentation have broken or meaningless links
- Documentation portability breaks when files are copied or moved
- Search engines cannot understand document relationships
- Citation tools cannot generate proper references
- Users downloading individual docs cannot find related documents
- Knowledge bases lose navigation when importing markdown files

### Real Example (Anti-Pattern 14)

**Before (context-dependent link):**

```markdown
**For complete overview, see:** [README.md](../../README.md)

**Key purposes:**
- Event organization resources
- Discussion archives
```

When extracted or printed, the link `../../README.md` is meaningless. What's two directories up? Where is this file located? What repository? Context is completely lost.

### Detection Method (Anti-Pattern 14)

Extract or print a single documentation file - can you still find referenced documents?

```bash
# Test: Extract single file and check if links work
curl -O https://raw.githubusercontent.com/org/repo/main/docs/guide.md
# Open guide.md - can you follow links to other docs?
```

### Forces (Anti-Pattern 14)

- **IDE convenience:** Relative links work perfectly in IDEs and git repositories
- **Version control patterns:** Git workflows encourage repository-relative references
- **Markdown preview:** Preview tools show working links within repository context
- **Documentation generators:** Tools like MkDocs, Docusaurus expect relative paths
- **Portability assumptions:** Teams assume documentation stays in repository structure
- **Link maintenance:** Relative links easier to maintain when moving files within repo
- **Cross-repo complexity:** Absolute URLs harder to maintain across repository branches

### Solution (Anti-Pattern 14)

Provide both relative links (for IDE navigation) and absolute URLs with document titles (for context preservation).

**After (context-preserving references):**

```markdown
**For complete overview, see:** [README.md](../../README.md) ("MX-Gathering: Community Resources and Thought Leadership" at <https://github.com/Digital-Domain-Technologies-Ltd/MX-Gathering/blob/main/README.md>)

**For development workflow, see:** [ENVIRONMENTS.md](../development/ENVIRONMENTS.md) ("MX-Gathering Development Environments" at <https://github.com/Digital-Domain-Technologies-Ltd/MX-Gathering/blob/main/docs/development/ENVIRONMENTS.md>)
```

**Pattern:**

```markdown
[filename](relative-path) ("Document Title" at <absolute-url>)
```

**When to apply:**

- ✅ All cross-document references (links to other files in repo)
- ❌ Internal section anchors within same document (`#contents` - these maintain context)
- ❌ External links (already absolute, no relative path to preserve)

**What this accomplishes:**

- **For humans in IDEs:** Clickable relative links work normally for local navigation
- **For machines/extracted files:** Full document title and absolute URL provide complete context
- **For AI agents:** Can understand relationships even when file is processed outside repository
- **For PDF readers:** Know exactly where to find referenced documents online
- **For citations:** Can generate proper references with full context

### Resulting Context (Anti-Pattern 14)

After implementing context-preserving references:

- **Agent understanding:** AI agents can follow references even with extracted files
- **PDF exports:** Generated PDFs include full context for all referenced documents
- **Documentation portability:** Files maintain meaning when copied or moved
- **Citation tools:** Can generate proper academic/technical citations
- **Search indexing:** Search engines understand document relationships
- **Knowledge base imports:** Documentation maintains navigation in external systems
- **User benefit:** Anyone reading documentation can find referenced materials

### Consequences (Anti-Pattern 14)

**Positive:**

- **Universal accessibility:** Links work for IDE users, AI agents, PDF readers, and extracted files
- **Future-proof:** Documents remain meaningful regardless of distribution method
- **Better discoverability:** Search engines and AI can understand document relationships
- **Citation support:** Academic and technical citations have complete context
- **Portability:** Documentation works in wikis, knowledge bases, and other systems
- **User experience:** Readers always have enough context to find referenced documents
- **Testing validation:** Can verify link targets programmatically via absolute URLs

**Negative/Trade-offs:**

- **Verbosity:** Links become longer with title and absolute URL
- **Maintenance overhead:** Must update both relative and absolute URLs when files move
- **Visual clutter:** More text in link annotations may impact readability
- **Branch management:** Absolute URLs typically point to specific branch (main/master)
- **Repository changes:** If repo moves or renames, absolute URLs need updating
- **Markdown rendering:** Some renderers may not style dual-format links elegantly

### Known Uses (Anti-Pattern 14)

**Common in:**

- GitHub project documentation with relative links between markdown files
- Multi-repository projects where docs reference other repos via relative paths
- Documentation generators (MkDocs, Docusaurus) using relative navigation
- Technical specifications with cross-document references
- README files linking to other documentation files

**Specific examples:**

- Open source project READMEs linking to `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md` with relative paths
- Technical docs with `../../API.md` references that break in PDF exports
- Multi-repo documentation linking between repositories via relative paths
- Wiki exports where relative links become meaningless outside wiki context
- Documentation sites where PDF downloads have broken internal references

### Related Patterns (Anti-Pattern 14)

**Fixes this anti-pattern:**

- Pattern 2: Page Metadata (Chapter 12.2) - Comprehensive metadata including canonical URLs
- Pattern 21: Documentation Structure (Appendix M) - Best practices for cross-document references
- Pattern 11: Content Discoverability (Appendix M) - Making content findable across contexts

**Related anti-patterns:**

- Anti-pattern 8: Inconsistent Schema.org - Similar problem of context/reference mismatches
- Anti-pattern 3: Generic Link Text - Also about providing meaningful link context
- Anti-pattern 7: No Sitemap - Related discoverability issue

**Related chapters:**

- Chapter 9: Content That Works for Agents
- Chapter 10: How AI Agents Discover and Navigate Websites
- Chapter 11.3: The Convergence Principle (clear references help everyone)
- Chapter 12.5: Pattern 5 (Semantic HTML Structure)

---

## Quick Wins Summary

If you can only fix 5 things immediately, prioritize these for maximum impact:

### 1. Add Proper Heading Hierarchy (30 minutes)

Run through all pages and ensure h1 → h2 → h3 logical structure. Use CSS to adjust visual sizes if needed.

**Impact:** Enables agents to understand document structure and content relationships.

### 2. Fix Link Text (1-2 hours)

Replace all "click here" and "learn more" with descriptive labels that explain destinations.

**Impact:** Agents can navigate your site intelligently without visiting every URL.

### 3. Add Image Alt Text (2-3 hours)

Write meaningful alt text for all images describing what they show, not just generic labels.

**Impact:** Makes visual content accessible to raw parsers and screen readers.

### 4. Create or Update Sitemap (1 hour)

Generate sitemap.xml automatically from your content management system or build process.

**Impact:** Ensures agents can discover all your pages systematically.

### 5. Add Basic Schema.org to Homepage (1 hour)

Implement Organization or LocalBusiness markup with contact details and key information.

**Impact:** Enables accurate citations and "find near me" queries.

**Total time investment:** 6-8 hours
**Impact:** Solves 80% of common agent-readability problems

---

## Validation Checklist

Use this checklist to audit pages for all 13 anti-patterns:

- [ ] 1. Check for visual-only information (gold borders, colour coding without text)
- [ ] 2. Verify images have meaningful alt text or HTML alternatives
- [ ] 3. Extract links - are they self-explanatory?
- [ ] 4. Validate heading hierarchy - logical h1 → h2 → h3?
- [ ] 5. View source - is navigation in HTML?
- [ ] 6. Disable JS - does essential content appear?
- [ ] 7. Check sitemap.xml exists and is current
- [ ] 8. Validate Schema.org matches visible content
- [ ] 9. Verify forms have proper label elements
- [ ] 10. Ensure data tables use th, caption, scope
- [ ] 11. Identify iframes with critical content
- [ ] 12. Find PDF-only information
- [ ] 13. Locate auto-playing carousels/rotators
- [ ] 14. Check documentation links preserve context when extracted

**Scoring:** Each passing check is one point. 12-14 points = excellent, 9-11 = good, 6-8 = moderate issues, 0-5 = significant problems.

---

## Further Reading

- **Chapter 10:** GEO patterns and discovery strategies
- **Chapter 11:** Designing for both humans and agents
- **Chapter 12:** Technical implementation and testing
- **Appendix M:** Complete metadata index

---

**Document Status:** Complete anti-patterns catalog covering all 14 documented patterns with detection methods and fixes.
