# Shared Appendices

**Comprehensive implementation guides, code examples, and resources shared across all book variants.**

## Context: Why AI-Friendly Patterns Matter

AI agents are machines with technical capabilities similar to users with disabilities. They cannot see CSS, they struggle with JavaScript-only state, and they need semantic HTML to understand content structure.

**The convergence principle:** One implementation serves three audiences:

1. **Users with disabilities** - Screen readers, keyboard users
2. **Search engines** - Google, Bing
3. **AI agents** - ChatGPT, Copilot, Perplexity

These appendices provide battle-tested patterns that work for all three audiences. They're derived from real client projects implementing the book's principles in production environments.

## Repository Purpose and Structure

**This is a content-only repository used as a git submodule.**

This repository exists for **separation of concerns** - keeping content version-controlled independently from build tooling and orchestration. Key characteristics:

- **No package.json** - No npm packages, no dependencies, no scripts, no dependency management
- **No build tooling** - Cannot be built independently
- **Content focus** - Pure markdown content and reference files for version control
- **Parent repository controls building** - All build commands, HTML generation, and linting are executed from the parent `invisible-users` repository

To work with this content:

1. Use the parent repository (`invisible-users`) for all build operations
2. Edit content directly in this submodule
3. Commit changes here first, then update the parent repository pointer

See the parent repository's [CLAUDE.md](../../CLAUDE.md) and [docs/repo/GIT-README.md](../../docs/repo/GIT-README.md) for comprehensive guidance.

## Overview

These appendices support both "The Bible" (comprehensive guide) and "Don't Make AI Think" (practical guide). They provide:

- **Implementation patterns** with step-by-step guidance
- **Code examples** ready for production use
- **Reference materials** for ongoing work
- **Industry developments** tracking the evolving ecosystem

## Status

**Publication:** Due Q1 2026
**Word count:** ~58,600 words
**Current state:** Complete and ready for publication

## Appendices

### Implementation Guides

- **Appendix A:** Implementation Cookbook - Recipes for common patterns
- **Appendix B:** Battle-Tested Lessons - Real-world learnings from client projects
- **Appendix C:** Web Audit Suite Guide - Using the companion analysis tool
- **Appendix D:** AI-Friendly HTML Guide - Complete reference with code examples
- **Appendix E:** AI Patterns Quick Reference - Cheat sheet for developers
- **Appendix F:** Implementation Roadmap - Priority-based approach
- **Appendix K:** Common Page Patterns - E-commerce, blogs, documentation, forms

### Resources and References

- **Appendix G:** Resource Directory - Curated tools, libraries, and documentation
- **Appendix H:** Live llms.txt - Example file with 20 curated links
- **Appendix I:** Pipeline Failure Case Study - Real incident analysis
- **Appendix J:** Industry Developments - Tracking the agent ecosystem
- **Appendix L:** Proposed AI Metadata Patterns - Emerging conventions

### Web Materials

- **web/** - HTML versions of appendices, news page, back cover

## Dual-File Structure

Some appendices use a dual-file pattern for maximum utility:

**Appendix D (AI-Friendly HTML Guide):**

- `appendix-d-ai-friendly-html-guide.txt` - Raw guide (source of truth, ~3,000 lines)
- `appendix-d-ai-friendly-html-guide.md` - Markdown wrapper with TOC

**Appendix H (Example llms.txt):**

- `appendix-h-live-llms.txt` - The actual llms.txt content (20 curated links)
- `appendix-h-live-llms.md` - Markdown wrapper with introduction

**Why both?** The .txt files can be copied directly into AI assistants or used as implementation templates. The .md wrappers include context and are included in PDF generation.

## Build Commands

Generate web versions (from repository root):

```bash
# Generate HTML pages for each appendix
npm run pdf:appendix

# Includes automatic enhancement with Chapter 10 patterns
# Also generates sitemap.xml for search engine discovery
```

## Writing Style

- **British English** throughout (organise, colour, whilst)
- **Technical reference tone** with practical examples
- **Code-first approach** - working examples over theory
- **Self-contained sections** - each appendix stands alone

See [docs/for-ai/writing-style.md](../../docs/for-ai/writing-style.md) for complete guidelines.

## Usage Across Books

**The Bible references:**

- All appendices as supplementary material
- Cited in chapters for deeper implementation details

**Don't Make AI Think references:**

- Appendix E (Quick Reference) for at-a-glance patterns
- Appendix F (Implementation Roadmap) for practical next steps
- Appendix K (Common Page Patterns) for specific implementations

## Updating Appendices

When updating dual-file appendices (D and H):

1. **Edit the .txt file first** (source of truth)
2. **Update the .md wrapper** if TOC or introduction changed
3. **Test PDF generation** to verify formatting

See [CLAUDE.md section on dual-file structure](../../CLAUDE.md#dual-file-appendix-structure) for details.

## Web Publication

The `web/` directory contains public-facing HTML versions:

- **news.html** - Industry developments feed (<https://allabout.network/invisible-users/news.html>)
- **back-cover.html** - Book back cover for screenshot generation
- **Individual appendix pages** - Generated by `npm run pdf:appendix`

## Contributing

These appendices are in final editing for publication. For questions or corrections:

- Email: <tom.cranstoun@gmail.com>
- Website: <https://allabout.network>

## License

PROPRIETARY - All rights reserved
