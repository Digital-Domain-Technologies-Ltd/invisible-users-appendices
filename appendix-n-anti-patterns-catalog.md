---
author: "Tom Cranstoun"
date: "2026-01-22"
description: "Comprehensive reference of the 13 most common mistakes that break AI agent compatibility, with detection methods and complete fixes for each pattern."
keywords: [anti-patterns, common-mistakes, visual-only-state, client-rendering, broken-hierarchy, accessibility-failures, detection-methods, quick-wins]
ai-instruction: |
  This is a book appendix cataloging anti-patterns. Write as if it has always
  existed. NEVER include: publication dates about the appendix itself, "we
  added", "new pattern", "this update", or any meta-commentary about the
  document's development. Write definitive present tense. Historical context
  about subject matter (industry practices, common failures) is allowed.
---

# Appendix N: Anti-Patterns Catalog

**Purpose:** Comprehensive reference of the 13 most common mistakes that break AI agent compatibility, with detection methods and complete fixes for each pattern.

**How to use this catalog:**

1. **For audits:** Run through all 13 patterns when evaluating a site
2. **For debugging:** Find specific failures you're encountering
3. **For prevention:** Review before implementing new features
4. **For training:** Teach teams what to avoid

---

## The Invisible Barriers

You can implement every GEO pattern correctly—semantic HTML, Schema.org markup, proper navigation—and still make your site invisible to AI agents with a few specific mistakes. These anti-patterns appear repeatedly in production sites, often introduced with good intentions but catastrophic results for agent compatibility.

This appendix catalogs the 13 most common anti-patterns, explains why they fail, and provides complete fixes with before/after code examples.

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

---

## 1. Visual-Only Information

### The Problem

Information conveyed purely through visual styling (colour, size, position, borders) without semantic backing in HTML.

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

**What humans see:** Professional tier highlighted with gold border, larger size, "Most Popular" badge.

**What AI sees:** Three identical div structures. No indication that Professional is recommended.

### The Fix

Make recommendations explicit in HTML structure and content:

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

**Chapter reference:** 11, 12.5

---

## 2. Content in Images

### The Problem

Text embedded in images without proper alt text or supplementary HTML text.

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

**What AI sees:** "Our services" - no detail whatsoever.

### The Fix

Provide information in both image and text:

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

**Chapter reference:** 11, 12.5

---

## 3. Generic Link Text

### The Problem

Links with meaningless text like "click here", "read more", "learn more" that provide no information about destinations.

### Detection Method

Extract all links and read as list - are they self-explanatory?

```javascript
Array.from(document.querySelectorAll('a'))
  .map(a => a.textContent.trim())
  .forEach((text, i) => console.log(`${i + 1}. ${text}`));
```

### The Fix

Make link text descriptive:

**Before:**

```html
<section>
  <h3>Edge Delivery Services Migration</h3>
  <p>We help companies migrate from traditional CMS platforms...</p>
  <a href="/services/eds-migration">Learn more</a>
</section>
```

**After:**

```html
<section>
  <h3>Edge Delivery Services Migration</h3>
  <p>We help companies migrate from traditional CMS platforms...</p>
  <a href="/services/eds-migration">Explore our EDS migration services</a>
</section>
```

**Alternative (if design requires short text):**

```html
<a href="/services/eds-migration"
   aria-label="Learn more about Edge Delivery Services migration">
  Learn more
</a>
```

**Chapter reference:** 12, 12.5

---

## 4. Broken Heading Hierarchy

### The Problem

Headings used for styling rather than structure, creating illogical hierarchies that confuse semantic understanding.

### Detection Method

```javascript
Array.from(document.querySelectorAll('h1, h2, h3, h4, h5, h6'))
  .forEach(h => {
    const level = h.tagName[1];
    const indent = '  '.repeat(parseInt(level) - 1);
    console.log(`${indent}${h.tagName}: ${h.textContent.trim()}`);
  });
```

### The Fix

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

**After (logical hierarchy):**

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

**Chapter reference:** 11, 12, 12.5

---

## 5. JavaScript-Only Navigation

### The Problem

Navigation menus that only exist after JavaScript executes, invisible to raw parsers.

### Detection Method

View page source - is `<nav>` element empty?

### The Fix

**Before:**

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

**After:**

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
  // JavaScript can enhance (dropdowns, mobile menu)
  // But base navigation works without it
</script>
```

**Chapter reference:** 12, 12.5

---

## 6. Hidden Content with No Fallback

### The Problem

Content hidden behind interactions (`display: none`) with no alternative access method for non-JavaScript agents.

### Detection Method

Disable JavaScript - does critical content remain hidden?

### The Fix

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
  // JavaScript collapses items after page load
  document.querySelectorAll('.accordion-item').forEach(item => {
    const button = item.querySelector('.accordion-header');
    const content = item.querySelector('.accordion-content');

    // Collapse by default
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

**Chapter reference:** 11, 12, 12.5

---

## 7. No Sitemap or Outdated Sitemap

### The Problem

Missing sitemap or sitemap containing broken links/outdated URLs.

### Detection Method

Visit `/sitemap.xml` - does it exist? Check dates and URLs.

### The Fix

Generate sitemaps automatically:

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

**Chapter reference:** 10, 12, 12.5

---

## 8. Inconsistent Schema.org

### The Problem

Schema.org markup that contradicts visible content or is incomplete.

### Real Example

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

- Name mismatch ("Standing Desk" vs "Professional Standing Desk - White Oak Finish")
- Price mismatch (£599 in Schema vs £499 visible)
- Sale price not reflected

### The Fix

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
  "offers": {
    "@type": "Offer",
    "price": "499",
    "priceCurrency": "GBP",
    "priceValidUntil": "2026-12-31",
    "availability": "https://schema.org/InStock"
  }
}
</script>
```

**Chapter reference:** 10, 11, 12.5

---

## 9. Forms Without Labels

### The Problem

Form inputs identified only by placeholder text, creating ambiguity and accessibility failures.

### Detection Method

Inspect forms - does each input have a `<label>` element?

### The Fix

**Before:**

```html
<form>
  <input type="text" placeholder="Your name">
  <input type="email" placeholder="Email address">
  <textarea placeholder="Your message"></textarea>
  <button>Send</button>
</form>
```

**After:**

```html
<form>
  <div class="form-field">
    <label for="name">Your Name</label>
    <input type="text" id="name" name="name" required>
  </div>

  <div class="form-field">
    <label for="email">Email Address</label>
    <input type="email" id="email" name="email" required>
  </div>

  <div class="form-field">
    <label for="message">Your Message</label>
    <textarea id="message" name="message" rows="5" required></textarea>
  </div>

  <button type="submit">Send Message</button>
</form>
```

**Chapter reference:** 11, 12, 12.5

---

## 10. Table Abuse

### The Problem

Tables used for layout OR data tables without proper structure (no `<th>`, `<caption>`, scope attributes).

### The Fix

**For layout:** Use CSS Grid or Flexbox instead of tables.

**For data tables:**

**Before:**

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

**After:**

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

**Chapter reference:** 11, 12, 12.5

---

## 11. Content in Iframes

### The Problem

Important content loaded in iframes from external sources, inaccessible to agents.

### The Fix

Pull content server-side and render in HTML:

**Before:**

```html
<h2>Our Latest News</h2>
<iframe src="https://news-widget.example.com/feed"></iframe>
```

**After:**

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

**Chapter reference:** 11, 12, 12.5

---

## 12. PDF-Only Content

### The Problem

Important information only available as PDF downloads, potentially unreadable or poorly parsed by agents.

### The Fix

Provide information in HTML, offer PDF as alternative:

**Before:**

```html
<h2>Our Services</h2>
<p>Download our services brochure to learn more.</p>
<a href="/brochure.pdf">Download PDF (2.3 MB)</a>
```

**After:**

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
      (2.3 MB)
    </p>
  </aside>
</section>
```

**Chapter reference:** 11, 12.5

---

## 13. Auto-Playing Content

### The Problem

Content that changes automatically (carousels, testimonials) making specific information hard to reference.

### The Fix

Show all content in HTML, add carousel as enhancement:

**Before:**

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

**After:**

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
  // JavaScript can add carousel functionality
  // Use CSS to show one at a time visually
  // But keep all content in DOM for agents
</script>
```

**Chapter reference:** 11, 12.5

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

**Scoring:** Each passing check is one point. 11-13 points = excellent, 8-10 = good, 5-7 = moderate issues, 0-4 = significant problems.

---

## Further Reading

- **Chapter 10:** GEO patterns and discovery strategies
- **Chapter 11:** Designing for both humans and agents
- **Chapter 12:** Technical implementation and testing
- **Appendix M:** Complete metadata index

---

**Document Status:** Complete anti-patterns catalog covering all 13 documented patterns with detection methods and fixes.
