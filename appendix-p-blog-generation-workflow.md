---
copyright: "Copyright © 2026 Tom Cranstoun. All rights reserved."
author: "Tom Cranstoun"
date: "2026-01-26"
description: "Complete blog generation workflow demonstrating Machine Experience principles through metadata-driven content management, state tracking, and WCAG 2.1 AA compliance."
keywords: [blog-workflow, metadata-schema, yaml-frontmatter, html-generation, wcag-compliance, state-tracking, content-management, ai-friendly-html]
book: "MX-Bible"
appendix: "P"
wordcount: 5800
ai-instruction: |
  This is a book manuscript appendix. Write as if it has always existed.
  NEVER include: publication dates, "we added", "new feature", "launching",
  "this update", or any meta-commentary about the book's development.
  Write definitive present tense. Historical context about subject matter
  (industry events, product launches) is allowed.
  This document is copyrighted material. No part may be reproduced without permission.
---

\newpage

# Appendix P - Blog Generation Workflow

A practical demonstration of Machine Experience principles through metadata-driven content management.

## Overview

This appendix documents a complete blog generation workflow that embodies the Machine Experience principles discussed throughout this book. The workflow transforms markdown drafts into WCAG 2.1 AA compliant HTML with comprehensive metadata, state tracking, and AI-friendly semantic structure.

**Why this workflow matters:** Most content management systems treat metadata as optional decorations added after content creation. This workflow inverts that relationship - metadata drives the process from draft to publication, ensuring both humans and AI agents can understand content state, relationships, and context at every stage.

**What you'll learn:**

- Metadata schema design for both human and machine readability
- State tracking through the content lifecycle
- Automated HTML generation preserving semantic structure
- WCAG 2.1 AA compliance verification patterns
- File organization strategies that work across tools

This workflow runs in production for all Machine Experience blog content. Every pattern shown has been tested with real AI agents, screen readers, and human visitors.

## Metadata Schema Design

### Core Principle: Metadata as First-Class Content

Traditional blogging platforms add metadata after writing. This workflow requires metadata before generation. The metadata schema serves three audiences:

1. **Content creators** - Track draft state, target filenames, publication status
2. **AI agents** - Understand content purpose, keywords, parsing instructions
3. **Build tools** - Generate HTML, CSS, social cards with correct naming and structure

### Markdown YAML Frontmatter

Every blog markdown file must include YAML frontmatter with mandatory fields:

```yaml
---
title: "Blog Post Title"
author: "Tom Cranstoun"
date: "2026-01-26"                    # Last modified date (ISO format)
blog-state: "draft"                   # Current state in workflow
blog-filename: "url-friendly-name"    # Target filename (no extension)
blog-url: ""                          # Full URL (empty until published)
publication-date: ""                  # Publication date (empty until published)
description: "Brief summary for meta description and social cards (1-2 sentences)"
keywords: [keyword1, keyword2, keyword3]  # 3-5 relevant keywords
ai-instruction: "Context for AI agents parsing this content"
---
```

### Field Descriptions and Validation Rules

**title** (required, string)

- The blog post title as it appears in H1 and HTML `<title>`
- Maximum recommended length: 60 characters (SEO best practice)
- Must not contain special characters that break URLs

**author** (required, string)

- Attribution for content authorship
- Used in Schema.org Person markup and meta tags

**date** (required, ISO date string YYYY-MM-DD)

- Last modification date
- Must be valid ISO 8601 date format
- Updates with every significant content revision

**blog-state** (required, enum)

- Current position in content lifecycle
- Valid values: `draft`, `in-review`, `published`, `archived`
- Drives file location and processing rules

**blog-filename** (required, string)

- URL-friendly target filename without extension
- Pattern: lowercase, hyphens only, no special characters
- Example: "machine-experience-adding-metadata"
- Becomes base for HTML, CSS, and SVG filenames

**blog-url** (optional, URL string)

- Full canonical URL after publication
- Empty string until content is live on web
- Format: `https://allabout.network/blogs/mx/[filename].html`

**publication-date** (optional, ISO date string)

- Date content went live on website
- Empty string until published state transition
- Used in Schema.org datePublished field

**description** (required, string)

- Brief summary (1-2 sentences) for meta description tag
- Maximum recommended length: 155 characters (SEO best practice)
- Appears in search results and social media cards

**keywords** (required, array of strings)

- 3-5 relevant topic keywords
- Used in meta keywords tag and content categorization
- Format: lowercase, no special characters

**ai-instruction** (optional, string)

- Guidance for AI agents parsing the content
- Explains document purpose, special considerations
- Example: "This blog post compares two architectural approaches. Pay attention to the trade-offs section."

### HTML Meta Tags

Generated HTML files include comprehensive meta tags in the `<head>` section. The generation script automatically creates these from markdown frontmatter:

```html
<head>
  <!-- Blog State Tracking (generated from frontmatter) -->
  <meta name="blog-state" content="in-review">
  <meta name="blog-draft-date" content="2026-01-20">
  <meta name="blog-review-date" content="2026-01-25">
  <meta name="blog-publication-date" content="">
  <meta name="blog-last-modified" content="2026-01-26">
  <meta name="blog-review-status" content="final-committee-review">

  <!-- Standard SEO metadata -->
  <title>Blog Post Title</title>
  <meta name="description" content="Brief summary from frontmatter">
  <meta name="keywords" content="keyword1, keyword2, keyword3">
  <meta name="author" content="Tom Cranstoun">

  <!-- Canonical URL (empty until published) -->
  <link rel="canonical" href="">

  <!-- Open Graph for social sharing -->
  <meta property="og:title" content="Blog Post Title">
  <meta property="og:description" content="Brief summary">
  <meta property="og:type" content="article">
  <meta property="og:url" content="">
  <meta property="og:image" content="/blogs/mx/[filename]-social.svg">

  <!-- Schema.org JSON-LD -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "BlogPosting",
    "headline": "Blog Post Title",
    "description": "Brief summary",
    "author": {
      "@type": "Person",
      "name": "Tom Cranstoun"
    },
    "dateModified": "2026-01-26",
    "keywords": "keyword1, keyword2, keyword3"
  }
  </script>
</head>
```

### CSS Comment Headers

CSS files include metadata as comment headers for human maintainability:

```css
/**
 * Blog Post Styles
 * Title: Blog Post Title
 * Filename: blog-filename.css
 * Blog State: in-review
 * Last Modified: 2026-01-26
 * Author: Tom Cranstoun
 *
 * WCAG 2.1 AA compliant styling scoped to this blog post.
 */

/* Style rules follow... */
```

## State Tracking System

### Four States in the Content Lifecycle

The workflow defines four distinct states that content passes through from draft to publication. Each state determines file location, required metadata, and allowed operations.

#### 1. Draft State

**Characteristics:**

- Work in progress, not ready for review
- Markdown files only (no HTML generated)
- May be incomplete, have TODOs, lack illustrations

**File Location:**

- `structure/` (top-level drafts)
- `structure/blog-drafts/` (organized drafts)

**Required Metadata:**

```yaml
blog-state: "draft"
# blog-url and publication-date must be empty
```

**Allowed Operations:**

- Edit markdown content freely
- Update frontmatter metadata
- Add/remove sections, illustrations, examples

#### 2. In-Review State

**Characteristics:**

- HTML generated and ready for technical/editorial review
- All assets extracted (CSS, SVG diagrams, social cards)
- Content frozen pending approval

**File Location:**

- `outputs/bible/blogs/mx/[filename].html` (and associated assets)

**Required Metadata (HTML):**

```html
<meta name="blog-state" content="in-review">
<meta name="blog-review-date" content="2026-01-26">
<meta name="blog-review-status" content="final-committee-review">
```

**Required Metadata (Markdown):**

```yaml
blog-state: "in-review"
```

**Review Sub-States:**

The `blog-review-status` meta tag tracks granular review progression:

- `initial-review` - First technical and editorial pass
- `technical-review` - Technical accuracy validation
- `editorial-review` - Writing quality and style review
- `final-committee-review` - Final approval before publication
- `ready-for-publication` - Approved and cleared for deployment

**Allowed Operations:**

- Review HTML in browser
- Validate WCAG 2.1 AA compliance
- Check HTML validation
- Verify all image/SVG paths exist
- Run accessibility checkers (Pa11y, WAVE, Lighthouse)

#### 3. Published State

**Characteristics:**

- Live on website and accessible to public
- Canonical URL assigned and active
- Schema.org datePublished set

**File Location:**

- `outputs/bible/blogs/mx/[filename].html` (same as in-review)
- Also deployed to web server at `https://allabout.network/blogs/mx/[filename].html`

**Required Metadata (HTML):**

```html
<meta name="blog-state" content="published">
<meta name="blog-publication-date" content="2026-01-26">
<link rel="canonical" href="https://allabout.network/blogs/mx/[filename].html">
```

**Required Metadata (Markdown):**

```yaml
blog-state: "published"
blog-url: "https://allabout.network/blogs/mx/[filename].html"
publication-date: "2026-01-26"
```

**Allowed Operations:**

- Content is now immutable (corrections require versioning)
- Can transition to archived state
- Can update review dates for corrections

#### 4. Archived State

**Characteristics:**

- No longer current but preserved for reference
- May have outdated information or superseded content
- Still accessible but marked as archived

**File Location:**

- `outputs/bible/blogs/mx/[filename].html` (same location)

**Required Metadata:**

```html
<meta name="blog-state" content="archived">
```

**Considerations:**

- Add visible archive notice to HTML
- Optionally add "This content is archived" banner
- Preserve original publication date
- Keep canonical URL active (no redirects)

### State Transition Rules

State transitions must follow specific rules to maintain metadata consistency:

#### Draft → In Review

**Trigger:** Running the HTML generation script

**Process:**

1. Verify markdown has `blog-state: "draft"`
2. Run generation script: `node scripts/generate-blog-html.js [markdown-file]`
3. Script generates HTML, CSS, SVG files in `outputs/bible/blogs/mx/`
4. Update markdown frontmatter:

   ```yaml
   blog-state: "in-review"
   ```

5. Add `blog-review-date` to HTML:

   ```html
   <meta name="blog-review-date" content="2026-01-26">
   ```

**Validation:**

- All HTML files must pass `npx html-validate`
- All SVG files must pass `xmllint --noout`
- Markdown must pass markdownlint

#### In Review → Published

**Trigger:** Content approval and web deployment

**Process:**

1. Verify HTML in `outputs/bible/blogs/mx/` is approved
2. Deploy HTML, CSS, SVG to web server
3. Update markdown frontmatter:

   ```yaml
   blog-state: "published"
   blog-url: "https://allabout.network/blogs/mx/[filename].html"
   publication-date: "2026-01-26"
   ```

4. Update HTML meta tags:

   ```html
   <meta name="blog-state" content="published">
   <meta name="blog-publication-date" content="2026-01-26">
   <link rel="canonical" href="https://allabout.network/blogs/mx/[filename].html">
   ```

5. Update Schema.org JSON-LD with `datePublished`

**Validation:**

- Verify live URL returns 200 status
- Check canonical URL is accessible
- Validate social media cards display correctly

#### Published → Archived

**Trigger:** Content becomes outdated or superseded

**Process:**

1. Update markdown frontmatter:

   ```yaml
   blog-state: "archived"
   ```

2. Update HTML meta tag:

   ```html
   <meta name="blog-state" content="archived">
   ```

3. Add visible archive notice to HTML:

   ```html
   <aside role="note" class="archive-notice">
     <p><strong>Archived Content:</strong> This blog post was published on [date] and may contain outdated information.</p>
   </aside>
   ```

**Considerations:**

- Keep canonical URL active
- Preserve all original metadata
- No redirects (content remains accessible)

## File Organization

The workflow separates draft content from generated HTML using clear directory boundaries:

```text
structure/
├── *.md                              # Top-level draft blogs (blog-state: "draft")
└── blog-drafts/                      # Organized draft workspace
    ├── *.md                          # Draft markdown files
    ├── contrasts/                    # Draft series: contrasts
    └── joiners/                      # Draft series: joiners

outputs/bible/blogs/mx/              # Generated content (in-review or published)
├── *.html                           # Blog post HTML
├── *.css                            # Blog-specific styles (WCAG 2.1 AA)
└── *.svg                            # Diagrams and social cards
```

### Naming Conventions

All generated files use the `blog-filename` from markdown frontmatter as the base:

**For blog post:** `machine-experience-adding-metadata`

**Generated files:**

```text
machine-experience-adding-metadata.html         # Main blog HTML
machine-experience-adding-metadata.css          # Scoped styles
machine-experience-adding-metadata-social.svg   # Social media card (1200x630px)
machine-experience-adding-metadata-diagram-1.svg # Extracted diagrams (numbered)
machine-experience-adding-metadata-diagram-2.svg
```

**Diagram naming:** SVG diagrams extracted from markdown use descriptive suffixes:

```text
machine-experience-adding-metadata-5-stage-agent-journey.svg
machine-experience-adding-metadata-human-vs-agent-behavior.svg
```

### Why This Structure Works

**Clear separation:** Draft content (docs/structure/) never mixes with generated HTML (outputs/)

**Flat hierarchy:** All generated blogs live at the same level, no deep nesting

**Predictable names:** Given a blog filename, you know exactly what files exist

**Symlink convenience:** Root-level symlink `blogs/ → outputs/bible/blogs/` provides shorter access path

## Generation Workflow

### Script: generate-blog-html.js

The generation script transforms markdown drafts into complete HTML packages with all required assets.

**Command:**

```bash
node scripts/generate-blog-html.js <markdown-file> [custom-filename]
```

**Input:**

- Markdown file with YAML frontmatter
- Optional custom filename override

**Output:**

- HTML file with semantic structure
- CSS file with WCAG 2.1 AA compliant styles
- SVG social media card (1200×630px)
- Extracted SVG diagrams with semantic filenames
- All files placed in `outputs/bible/blogs/mx/`

### Generation Process Steps

#### 1. Parse Markdown Frontmatter

Extract and validate all required YAML fields:

```javascript
const matter = require('gray-matter');
const fs = require('fs');

const markdown = fs.readFileSync(markdownFile, 'utf8');
const { data, content } = matter(markdown);

// Validate required fields
const required = ['title', 'author', 'date', 'blog-state', 'blog-filename', 'description', 'keywords'];
required.forEach(field => {
  if (!data[field]) {
    throw new Error(`Missing required field: ${field}`);
  }
});
```

#### 2. Generate HTML Structure

Create semantic HTML5 structure with ARIA landmarks:

```html
<!DOCTYPE html>
<html lang="en-GB">
<head>
  <!-- Meta tags from frontmatter -->
  <!-- Schema.org JSON-LD -->
  <link rel="stylesheet" href="[filename].css">
</head>
<body>
  <header role="banner">
    <h1 id="top">[title]</h1>
    <p class="meta">
      By <span class="author">[author]</span> |
      <time datetime="[date]">[formatted-date]</time> |
      <span class="reading-time">[calculated] min read</span> |
      <span class="word-count">[calculated] words</span>
    </p>
  </header>

  <nav role="navigation" aria-label="Table of Contents">
    <h2>Contents</h2>
    <ol>
      <!-- Generated from H2 headings -->
    </ol>
  </nav>

  <main role="main">
    <article>
      <!-- Converted markdown content -->
    </article>
  </main>

  <footer role="contentinfo">
    <p>© 2026 Tom Cranstoun. All rights reserved.</p>
  </footer>
</body>
</html>
```

#### 3. Convert Markdown to HTML

Use markdown-it with plugins for semantic conversion:

```javascript
const markdownIt = require('markdown-it');
const markdownItAnchor = require('markdown-it-anchor');
const markdownItAttrs = require('markdown-it-attrs');

const md = markdownIt({ html: true, linkify: true, typographer: true })
  .use(markdownItAnchor, {
    permalink: markdownItAnchor.permalink.headerLink(),
    level: [2, 3, 4, 5, 6]  // Generate IDs for H2-H6
  })
  .use(markdownItAttrs);

const htmlContent = md.render(content);
```

#### 4. Extract and Process SVG Diagrams

Find inline SVG elements and extract to separate files:

```javascript
const cheerio = require('cheerio');

function extractSVGs(html, baseFilename) {
  const $ = cheerio.load(html);
  const svgs = [];

  $('svg').each((i, elem) => {
    const svgContent = $.html(elem);
    const svgFilename = `${baseFilename}-diagram-${i + 1}.svg`;

    // Extract descriptive ID if present
    const svgId = $(elem).attr('id');
    if (svgId) {
      svgFilename = `${baseFilename}-${svgId}.svg`;
    }

    fs.writeFileSync(`outputs/bible/blogs/mx/${svgFilename}`, svgContent);

    // Replace inline SVG with img reference
    $(elem).replaceWith(`<img src="${svgFilename}" alt="[descriptive alt text]">`);

    svgs.push(svgFilename);
  });

  return { html: $.html(), svgs };
}
```

#### 5. Generate Social Media Card

Create 1200×630px SVG social card:

```javascript
function generateSocialCard(title, description, filename) {
  const svg = `
<svg viewBox="0 0 1200 630" xmlns="http://www.w3.org/2000/svg">
  <rect width="1200" height="630" fill="#1a1a1a"/>
  <text x="600" y="280" text-anchor="middle"
        font-family="system-ui, sans-serif" font-size="48"
        fill="#ffffff" font-weight="bold">
    ${title}
  </text>
  <text x="600" y="350" text-anchor="middle"
        font-family="system-ui, sans-serif" font-size="24"
        fill="#cccccc">
    ${description}
  </text>
  <text x="600" y="550" text-anchor="middle"
        font-family="system-ui, sans-serif" font-size="20"
        fill="#888888">
    allabout.network
  </text>
</svg>`;

  fs.writeFileSync(`outputs/bible/blogs/mx/${filename}-social.svg`, svg);
}
```

#### 6. Generate CSS with WCAG 2.1 AA Compliance

Create scoped styles meeting contrast requirements:

```css
/* WCAG 2.1 AA Contrast Requirements:
 * - Normal text (< 18pt): 4.5:1 minimum
 * - Large text (≥ 18pt or ≥ 14pt bold): 3:1 minimum
 * - UI components: 3:1 minimum
 */

body {
  font-family: system-ui, -apple-system, sans-serif;
  line-height: 1.6;
  color: #1a1a1a;           /* 16.7:1 on white (exceeds 4.5:1) */
  background: #ffffff;
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

h1, h2, h3, h4, h5, h6 {
  color: #000000;           /* 21:1 on white (maximum contrast) */
  line-height: 1.3;
  margin-top: 1.5em;
  margin-bottom: 0.5em;
}

a {
  color: #0066cc;           /* 7.3:1 on white (exceeds 4.5:1) */
  text-decoration: underline;
}

a:hover {
  color: #0052a3;           /* 8.7:1 on white */
  text-decoration: none;
}

code {
  background: #f5f5f5;      /* Background for code blocks */
  color: #1a1a1a;           /* 14.5:1 on #f5f5f5 */
  padding: 0.2em 0.4em;
  border-radius: 3px;
  font-family: 'Courier New', monospace;
}

pre code {
  display: block;
  padding: 1rem;
  overflow-x: auto;
}
```

#### 7. Calculate Reading Time and Word Count

Add metadata to HTML:

```javascript
function calculateReadingStats(content) {
  const plainText = content.replace(/<[^>]+>/g, '');  // Strip HTML
  const wordCount = plainText.split(/\s+/).length;
  const readingTime = Math.ceil(wordCount / 200);  // 200 words per minute

  return { wordCount, readingTime };
}
```

#### 8. Generate Table of Contents

Extract H2 headings and create navigation:

```javascript
function generateTOC(html) {
  const $ = cheerio.load(html);
  const toc = [];

  $('h2[id]').each((i, elem) => {
    const id = $(elem).attr('id');
    const text = $(elem).text();
    toc.push({ id, text });
  });

  const tocHTML = `
<nav role="navigation" aria-label="Table of Contents">
  <h2>Contents</h2>
  <ol>
    ${toc.map(item => `<li><a href="#${item.id}">${item.text}</a></li>`).join('\n    ')}
  </ol>
</nav>`;

  return tocHTML;
}
```

### Complete Generation Example

**Input markdown** (`machine-experience-adding-metadata.md`):

```markdown
---
title: "Machine Experience: Adding Metadata"
author: "Tom Cranstoun"
date: "2026-01-20"
blog-state: "draft"
blog-filename: "machine-experience-adding-metadata"
blog-url: ""
publication-date: ""
description: "How metadata transforms websites from opaque to transparent for AI agents"
keywords: [metadata, schema-org, ai-agents, semantic-html]
ai-instruction: "This post explains metadata's role in AI agent compatibility"
---

# Machine Experience: Adding Metadata

Metadata isn't decoration. It's structure that lets AI agents understand your content.

## Why Metadata Matters

[Content continues...]
```

**Generated files:**

```text
outputs/bible/blogs/mx/
├── machine-experience-adding-metadata.html
├── machine-experience-adding-metadata.css
└── machine-experience-adding-metadata-social.svg
```

## WCAG 2.1 AA Compliance

### Contrast Requirements

All blog styles must meet WCAG 2.1 AA contrast ratios:

**Normal text (< 18pt):** 4.5:1 minimum

- Body text: #1a1a1a on #ffffff (16.7:1) ✓
- Link text: #0066cc on #ffffff (7.3:1) ✓
- Code text: #1a1a1a on #f5f5f5 (14.5:1) ✓

**Large text (≥ 18pt or ≥ 14pt bold):** 3:1 minimum

- Headings: #000000 on #ffffff (21:1) ✓

**UI components and graphics:** 3:1 minimum

- Navigation borders: #666666 on #ffffff (5.7:1) ✓
- Button backgrounds: #0066cc on #ffffff (7.3:1) ✓

### Semantic HTML Requirements

#### Heading Hierarchy

Headings must follow logical order without skipping levels:

```html
<!-- ✓ CORRECT -->
<h1>Blog Post Title</h1>
  <h2>Major Section</h2>
    <h3>Subsection</h3>
    <h3>Another Subsection</h3>
  <h2>Another Major Section</h2>

<!-- ✗ WRONG: Skips from H1 to H3 -->
<h1>Blog Post Title</h1>
  <h3>Subsection</h3>
```

#### ARIA Landmarks

Use semantic HTML5 elements and ARIA roles for navigation:

```html
<header role="banner">...</header>
<nav role="navigation" aria-label="Table of Contents">...</nav>
<main role="main">...</main>
<footer role="contentinfo">...</footer>
```

#### Link Purpose

All links must have clear purpose from link text alone:

```html
<!-- ✓ CORRECT: Purpose clear from text -->
<a href="/appendix-d.html">Appendix D: AI-Friendly HTML Guide</a>

<!-- ✗ WRONG: "Click here" is meaningless -->
<a href="/appendix-d.html">Click here</a> for the AI-Friendly HTML Guide
```

#### Image Alt Text

All images must have descriptive alt attributes:

```html
<!-- ✓ CORRECT: Describes diagram content -->
<img src="workflow-diagram.svg" alt="Five-stage workflow from draft to publication showing state transitions and validation checkpoints">

<!-- ✗ WRONG: Generic or missing alt text -->
<img src="workflow-diagram.svg" alt="diagram">
```

### Validation Process

After HTML generation, validate compliance:

#### 1. HTML Validation

```bash
npx html-validate outputs/bible/blogs/mx/[filename].html
```

Fix all errors before proceeding. Common issues:

- Unclosed tags
- Unencoded special characters (`&` must be `&amp;`)
- Invalid nesting (e.g., `<p>` inside `<p>`)

#### 2. SVG/XML Validation

```bash
for svg in outputs/bible/blogs/mx/[filename]-*.svg; do
  xmllint --noout "$svg" 2>&1 || echo "✗ $svg has XML errors"
done
```

Fix XML entity errors:

- Unencoded `&` → `&amp;`
- Unencoded `<` → `&lt;`
- Unencoded `>` → `&gt;`

#### 3. Accessibility Scanning

Use automated tools to catch common issues:

```bash
# Pa11y scan
npx pa11y outputs/bible/blogs/mx/[filename].html

# Lighthouse accessibility audit
npx lighthouse outputs/bible/blogs/mx/[filename].html --only-categories=accessibility
```

Address all errors and warnings. Common findings:

- Missing alt text on images
- Insufficient colour contrast
- Skipped heading levels
- Missing ARIA labels on custom controls

#### 4. Manual Screen Reader Testing

Automated tools catch ~40% of accessibility issues. Manual testing with real screen readers is essential:

**macOS:** VoiceOver (Cmd+F5)
**Windows:** NVDA (free) or JAWS
**Linux:** Orca

Test navigation:

- Can you navigate by headings?
- Do links announce clear purposes?
- Are images described sufficiently?
- Is the table of contents accessible?

## Practical Implementation

### Integrating with Existing Tools

The blog workflow integrates with standard publishing tools through file-based interfaces:

**Static site generators (Hugo, Jekyll, Gatsby):**

- Place generated HTML in appropriate directory
- Use frontmatter metadata for site navigation
- Override default templates if needed

**Content management systems (WordPress, Ghost):**

- Import HTML as custom post type
- Map frontmatter to post metadata fields
- Preserve canonical URLs and Schema.org markup

**Custom publishing pipelines:**

- Read generated HTML from `outputs/bible/blogs/mx/`
- Parse meta tags for deployment routing
- Respect blog-state for workflow gates

### Extending the Workflow

Add custom generation steps by modifying `scripts/generate-blog-html.js`:

**Add custom metadata fields:**

```javascript
// In frontmatter parsing section
if (data.seriesName) {
  // Add series navigation
  // Link to other posts in series
}
```

**Generate additional assets:**

```javascript
// After SVG social card generation
generateThumbnail(filename);  // Create thumbnail image
generateAMP(html, filename);  // Create AMP version
generatePDF(html, filename);  // Create PDF version
```

**Integrate with deployment:**

```javascript
// After file generation
if (data.blogState === 'ready-for-publication') {
  deployToProduction(filename);
  notifyTeam(data.title);
}
```

## Related Documentation

**Complete Metadata Schema:**
[Blog Metadata Schema and State Tracking](https://github.com/ddttom/invisible-users/blob/main/docs/structure/blog-metadata-schema.md)

**Repository Architecture:**
[doc-architecture.md](https://github.com/ddttom/invisible-users/blob/main/docs/architecture/doc-architecture.md#blog-content-workflow)

**AI-Friendly HTML Patterns:**
Appendix D - AI-Friendly HTML Guide

**WCAG 2.1 Guidelines:**
<https://www.w3.org/WAI/WCAG21/quickref/>

**Schema.org Vocabulary:**
<https://schema.org/BlogPosting>

## Key Takeaways

This blog workflow demonstrates Machine Experience principles in practice:

1. **Metadata-driven:** Content state and structure encoded explicitly, readable by both humans and machines

2. **State-explicit:** Every file knows where it is in the lifecycle through machine-parseable fields

3. **Semantically structured:** HTML uses proper heading hierarchy, ARIA landmarks, and Schema.org markup

4. **WCAG 2.1 AA compliant:** All colour contrasts meet minimum ratios, semantic HTML aids screen readers

5. **File organization:** Clear separation between draft (docs/) and generated (outputs/) content

6. **Automated validation:** HTML, XML, and accessibility checks prevent deployment of broken content

7. **Human and machine readable:** Same metadata serves content creators, build tools, search engines, and AI agents

The workflow inverts the traditional "content first, metadata later" approach. By requiring metadata before generation, it ensures machine-readable structure from the start - not as an afterthought, but as a fundamental property of the content itself.

This is Machine Experience: designing systems where explicit structure, semantic markup, and machine-parseable metadata enable both automated processing and human understanding.
