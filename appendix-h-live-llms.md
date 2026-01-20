# Appendix H: Example llms.txt File {.unnumbered}

\markboth{Appendix H: Example llms.txt File}{Appendix H: Example llms.txt File}

This is an example of an `llms.txt` file demonstrating **extended format with metadata** - a proposed enhancement to the standard llms.txt specification.

**Format note:** The standard llms.txt format (llmstxt.org) contains only URLs to curated content. This example extends that format with markdown-formatted metadata at the top of the file - author bio, company details, contact information, site description.

**Why extend llms.txt?** When agents access llms.txt directly instead of crawling HTML pages, they miss the rich metadata layers (Schema.org, HTML meta tags, author information). Extended llms.txt compensates by embedding that context directly in the file.

**Status:** This is a proposed pattern, not part of the official llms.txt specification. Standard URL-only llms.txt files remain valid. This extended format is backwards-compatible - parsers expecting only URLs will skip markdown sections and process URL sections normally.

The example below shows both metadata sections (top) and standard URL sections (bottom), separated by clear category headings.

```markdown
# Digital Domain Technologies (DDT)

> Expert Adobe Edge Delivery Services consulting and AI integration resources by Tom Cranstoun ("The AEM Guy")

## About the Author & Consultancy

**Tom Cranstoun** is a seasoned CMS expert and Principal Consultant at Digital Domain Technologies (DDT). With over 25 years of experience in enterprise content management, he specializes in Adobe Edge Delivery Services (EDS), document-based authoring, and AI-native development.

**Key Achievements:**

- Global Architecture Director for Nissan/Renault Helios initiative (200+ global sites)
- Lead Strategist for EE (UK Telecom) and Twitter enterprise CMS implementations
- Pioneer in LLM context delivery and Model Context Protocol (MCP) integration

**Contact:**
- **Website**: <https://allabout.network>
- **Email**: <info@digitaldomaintechnologies.com>
- **LinkedIn**: <https://www.linkedin.com/in/tom-cranstoun/>

## Access Guidelines

- Base Rate: 100 requests per hour per IP
- Cache Retention: 24 hour maximum
- Content Usage: Attribution required
- Commercial Use: Requires written permission
- Training Usage: Permitted for public documentation only
- Attribution Format: "Source: Digital Domain Technologies (allabout.network)"

## Adobe Edge Delivery Services & AI Development Resources

Technical documentation and educational resources for Adobe Edge Delivery Services development, AI integration, and modern web architecture.

**Last updated:** December 2025
**Authors:** Tom Cranstoun, Cate Nisbet
**Site Type:** Document-Centric, Technical Documentation, Educational Resource
**Purpose:** Developer Education, Content Author Training, AI Integration Guidance
**Technology Stack:** Adobe Edge Delivery Services, Document-Based Architecture

## Developer Documentation

13-part series covering Edge Delivery Services development from fundamentals to advanced AI integration. Complete series available at <https://allabout.network/blogs/ddt/developer-guide-to-document-authoring-with-edge-delivery-services-part-0>

Key parts:

- [Part 0 - EDS Introduction](https://allabout.network/blogs/ddt/developer-guide-to-document-authoring-with-edge-delivery-services-part-0): Complete beginner's guide and concepts
- [Part 2 - Block Development](https://allabout.network/blogs/ddt/developer-guide-to-document-authoring-with-edge-delivery-services-part-2): Component creation and customization
- [Part 5 - React Implementation](https://allabout.network/blogs/ddt/developer-guide-to-document-authoring-with-edge-delivery-services-part-5): React integration guide
- [Part 8 - AI Development Guide](https://allabout.network/blogs/ddt/developer-guide-to-document-authoring-with-edge-delivery-services-part-8): AI integration basics

## EDS Integration & Development

- [AI-Powered Adobe EDS Development](https://allabout.network/blogs/ddt/integrations/ai-powered-adobe-eds-development): Framework for building sophisticated EDS components using vanilla JavaScript with zero dependencies
- [Building a React App with Edge Delivery Services](https://allabout.network/blogs/ddt/integrations/building-a-react-app-with-edge-delivery-services): Integrate React applications with Adobe Edge Delivery Services
- [Using Web Components in Adobe Edge Delivery Services Blocks](https://allabout.network/blogs/ddt/integrations/using-web-components-in-adobe-edge-delivery-services-blocks): Implementing web components in EDS blocks with Shoelace components
- [Mastering EDS Block Debugging](https://allabout.network/blogs/ddt/integrations/mastering-eds-block-debugging-a-developer-guide-to-edge-delivery-services): Systematic debugging approaches for EDS blocks

## Core AI/LLM Topics

- [You Built Software for Humans - Now Build It for AI](https://allabout.network/blogs/ddt/ai/you-built-software-for-humans-now-build-it-for-ai): Why software that works for humans often confuses AI assistants
- [The "No Elephants" Problem](https://allabout.network/blogs/ddt/ai/the-no-elephants-problem-why-ai-struggles-with-what-not-to-do): Why AI systems fail at understanding negation
- [The Tokenization Trap - How AI Processes German](https://allabout.network/blogs/ddt/ai/the-tokenization-trap-how-ai-actually-processes-german): Fundamental computational approaches built around English assumptions
- [Making LLMs.txt work for Headless Websites](https://allabout.network/blogs/ddt/ai/making-llms-txt-work-for-headless-websites): Ensuring content remains visible in an AI-mediated world
- [The Mathematical Heartbeat of AI](https://allabout.network/blogs/ddt/ai/the-mathematical-heartbeat-of-ai): Fundamental mathematical concepts powering artificial intelligence

## AI Development Tools & Practices

- [Structuring Context for Effective AI Development](https://allabout.network/blogs/ddt/structuring-context-for-effective-ai-development): Three-tiered structure for creating context in AI development tools
- [Human-Centred AI in Content Management](https://allabout.network/blogs/ddt/human-centred-ai-in-content-management): Why human oversight remains essential in AI workflows
- [Building the AI-Native Web with EDS, llms.txt](https://allabout.network/blogs/ddt/building-the-ai-native-web-with-eds): Jeremy Howard's llms.txt standard for helping LLMs understand websites

## AEM/CMS Resources

- [Strategic AEM Architecture](https://allabout.network/strategic-aem-architecture-why-framework-thinking-beats-feature-chasing): Framework thinking for digital transformation
- [Adobe EDS: Revolutionizing Content Management](https://allabout.network/blogs/ddt/adobe-eds-revolutionizing-content-management): Why content authors actually dislike traditional CMS systems

## Content Author Resources

- [Content Creation Basics](https://allabout.network/blogs/ddt/content-creator-guide-to-document-authoring-with-edge-delivery-services): Getting started guide
- [Advanced Authoring](https://allabout.network/blogs/ddt/content-creator-guide-to-document-authoring-with-edge-delivery-services-part-2): Advanced techniques

## For Human Visitors

Looking for the full interactive experience?

- **Main Documentation:** <https://allabout.network/blogs/ddt/>
- **Contact:** <info@digitaldomaintechnologies.com>
- **Agency Services:** <https://allabout.network/>
- **About llms.txt:** <https://llmstxt.org>
- **Integrations Focus:** <https://allabout.network/blogs/ddt/integrations/llms.txt>

## Version Information

**Version:** 2.0 (Updated: January 2026)
**Curated highlights:** 20 key resources across 6 major categories
**Categories:** Developer Documentation (4), EDS Integration & Development (4), Core AI/LLM Topics (5), AI Development Tools & Practices (3), AEM/CMS Resources (2), Content Author Resources (2)
```

## Markdown Metadata Standards for AI Agents

Whilst llms.txt provides site-wide metadata, individual markdown documents need their own metadata layer. **Pandoc YAML frontmatter** is the universal standard for embedding structured metadata in markdown files.

### What is YAML Frontmatter?

YAML frontmatter is a metadata block at the top of a markdown file, delimited by triple dashes (`---`). It's supported by all major static site generators (Hugo, Jekyll, Gatsby, Quarto) and the Pandoc document converter.

**Example:**

```yaml
---
title: "Your Website Has Invisible Customers"
author: "Tom Cranstoun"
date: "2026-01-17"
description: "AI agents are visiting your website right now"
abstract: "Extended context about invisible users and AI agent traffic patterns"
keywords: [ai-agents, web-accessibility, seo, metadata]
ai-instruction: "This article introduces AI agents as website visitors"
purpose: "Educational content for web developers"
---
```

### Why YAML Frontmatter Complements llms.txt

- **llms.txt:** Site-wide metadata (curated URLs, author bio, access guidelines)
- **YAML frontmatter:** Per-document metadata (title, author, description, instructions)

When AI agents fetch markdown files directly, YAML frontmatter provides the same rich context that HTML meta tags would provide in web pages.

### Standard Pandoc Fields

**Core metadata:**

- `title` - Document title
- `author` - Author name(s)
- `date` - Publication or update date
- `abstract` - Extended summary for academic/technical documents
- `keywords` - Array of topic tags

**Custom fields for AI agents:**

- `description` - Brief SEO-style summary
- `ai-instruction` - Specific guidance for AI parsing
- `purpose` - Why document exists
- `context` - Background AI agents need

### Platform Support

YAML frontmatter works across the entire markdown ecosystem:

- **Pandoc:** Full metadata processing, PDF generation, format conversion
- **Hugo:** Automatic site integration, template access to all fields
- **Jekyll:** GitHub Pages native support, liquid template integration
- **Gatsby:** GraphQL queries on frontmatter fields
- **Quarto:** Scientific publishing with citation support

### Integration with Build Systems

Static site generators automatically process YAML frontmatter:

```yaml
---
title: "Chapter 5: Metadata That Works"
description: "How to structure metadata for both humans and AI agents"
keywords: [metadata, yaml, frontmatter, ai-agents]
---
```

When built, this becomes:

```html
<head>
  <title>Chapter 5: Metadata That Works</title>
  <meta name="description" content="How to structure metadata for both humans and AI agents">
  <meta name="keywords" content="metadata, yaml, frontmatter, ai-agents">
</head>
```

### Resources

- **Pandoc YAML Header Options:** <https://www.codestudy.net/blog/what-can-i-control-with-yaml-header-options-in-pandoc/>
- **Hugo Front Matter:** <https://gohugo.io/content-management/front-matter/>
- **Jekyll Front Matter:** <https://jekyllrb.com/docs/front-matter/>
- **Detailed Pattern Documentation:** Appendix L Pattern 4 (Pandoc YAML Frontmatter)

### When to Use YAML Frontmatter

**Use YAML frontmatter when:**

- Publishing markdown-based content (Hugo, Jekyll, Gatsby, Quarto sites)
- Using Pandoc for document conversion (markdown to PDF, HTML, DOCX)
- Creating technical documentation or educational content
- Need AI agents to understand document context without HTML
- Converting HTML to markdown and need to preserve metadata

**Use HTML meta tags instead when:**

- Publishing directly in HTML (traditional CMS platforms)
- Content only exists as web pages (no markdown source)
- Using systems that don't support YAML frontmatter
