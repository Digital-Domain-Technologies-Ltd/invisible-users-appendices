---
copyright: "Copyright © 2026 Tom Cranstoun. All rights reserved."
title: "Appendix O: Pattern Documentation Templates"
author: "Tom Cranstoun"
date: "2026-01-26"
description: "Reusable templates for MX pattern documentation including Pattern Intent, ADR format, Quick Start Cards, and validation checklists"
keywords: [patterns, templates, adr, documentation, validation]
ai-instruction: "This document is copyrighted material. No part may be reproduced without permission. This appendix provides standardised templates for pattern documentation. When creating patterns, follow these templates exactly to ensure consistency across all MX pattern documentation. All patterns must include YAML frontmatter for machine readability."
purpose: "Reference templates for pattern authors"
---

# Appendix O: Pattern Documentation Templates

## Introduction

This appendix provides standardised templates for documenting MX patterns. These templates ensure consistency across pattern documentation and enable both human understanding and machine processing.

**Four templates are provided:**

1. **Pattern Intent Template** - Core pattern documentation format (ADR-inspired)
2. **ADR Format Template** - For anti-patterns and decision records
3. **Quick Start Card Template** - YAML format for rapid implementation
4. **Pattern Validation Checklist** - Quality assurance for pattern publication

All templates support machine readability through structured metadata and consistent formatting.

## 1. Pattern Intent Template

Use this template when creating new MX patterns. This format combines the clarity of Architectural Decision Records (ADRs) with machine-readable metadata.

### Template Structure

```markdown
---
title: "Pattern Name: Brief Description"
author: "Author Name"
date: "YYYY-MM-DD"
description: "One-sentence pattern description"
keywords: [pattern, domain, technology, platform]
ai-instruction: "Instructions for AI agents parsing this pattern"
purpose: "Pattern documentation"
pattern-id: "mx.pattern.domain.purpose.platform"
version: "1.0.0"
maturity: "draft|proposed|adopted|mature|deprecated|archived"
---

# Pattern Name: Brief Description

## Pattern Intent

**Name:** `mx.pattern.<domain>.<purpose>.<platform>`
**Version:** 1.0.0
**Maturity:** [draft|proposed|adopted|mature|deprecated|archived]
**Intent:** One-sentence description of what this pattern enables

### Context

- **Platform:** [macOS|Linux|Windows|Cloud|Hybrid|Cross-platform]
- **Agent runtime:** [Clawdbot|Custom|Other]
- **Model runtime:** [Ollama|OpenAI|Anthropic|Cloud provider|Hybrid]
- **Boundary:** [local-only|cloud|hybrid|mixed]
- **Audience:** [Developers|Operators|Authors|Agents|All]

### Problem

Describe the problem this pattern solves in 2-3 sentences.
Focus on clarity, reproducibility, and machine-human collaboration.

### Forces

List the competing concerns and constraints that influence the solution:

- Force 1: [e.g., privacy requirements]
- Force 2: [e.g., reproducibility needs]
- Force 3: [e.g., local vs cloud trade-offs]
- Force 4: [e.g., governance or metadata requirements]
- Force 5: [e.g., performance considerations]

### Solution

Short description of the approach this pattern defines.
Explain the architecture at a high level without implementation detail.

Include:
- Core approach
- Key components
- Critical decisions
- Boundary definitions

### Resulting Context

List the outcomes after implementing this pattern:

- Outcome 1: [e.g., agent runs locally with predictable behaviour]
- Outcome 2: [e.g., model provenance is explicit]
- Outcome 3: [e.g., boundaries are clearly defined]
- Outcome 4: [e.g., risks are identified and mitigated]

### Consequences

**Positive:**
- Benefit 1: [specific advantage]
- Benefit 2: [specific advantage]
- Benefit 3: [specific advantage]

**Negative/Trade-offs:**
- Trade-off 1: [specific limitation or cost]
- Trade-off 2: [specific limitation or cost]
- Trade-off 3: [specific limitation or cost]

### Known Uses

List projects, teams, or examples using this pattern:

- Project/team name - Brief description of usage
- Project/team name - Brief description of usage

### Related Patterns

Link to patterns that:
- Complement this pattern
- Extend this pattern
- Provide alternatives
- Share context

Format: `mx.pattern.<something-related>` - Brief relationship description

## Implementation Steps

Provide concrete, reproducible implementation steps.

### Step 1: [Action]

```bash
# Code examples
```

Explanation of what this step accomplishes.

### Step 2: [Action]

```bash
# Code examples
```

Explanation of what this step accomplishes.

[Continue for all steps]

## Validation

Describe how to verify the pattern is correctly implemented:

- [ ] Validation check 1
- [ ] Validation check 2
- [ ] Validation check 3

## Governance Notes

- **Boundary clarity:** [Explicit boundary declarations]
- **Provenance:** [Source tracking requirements]
- **Co-authorship:** [Human-machine collaboration notes]
- **Reproducibility:** [Determinism guarantees]

## References

- Related MX-Bible chapters
- External documentation
- Tool documentation
- Research papers
```

### Field Descriptions

**YAML Frontmatter Fields:**

| Field | Required | Description |
|-------|----------|-------------|
| `title` | Yes | Pattern name with brief description |
| `author` | Yes | Primary pattern author(s) |
| `date` | Yes | Pattern creation/publication date |
| `description` | Yes | One-sentence summary |
| `keywords` | Yes | Searchable tags (array) |
| `ai-instruction` | No | Agent parsing guidance |
| `purpose` | Yes | "Pattern documentation" |
| `pattern-id` | Yes | Unique identifier following naming convention |
| `version` | Yes | Semantic version (MAJOR.MINOR.PATCH) |
| `maturity` | Yes | Lifecycle stage |

**Pattern Intent Fields:**

| Field | Required | Description |
|-------|----------|-------------|
| Name | Yes | Unique identifier (mx.pattern format) |
| Version | Yes | Pattern version |
| Maturity | Yes | Lifecycle stage |
| Intent | Yes | One-sentence purpose |
| Context | Yes | Where/when pattern applies |
| Problem | Yes | What issue it addresses |
| Forces | Yes | Competing concerns (3-5 items) |
| Solution | Yes | Core approach description |
| Resulting Context | Yes | Outcomes after implementation |
| Consequences | Yes | Benefits and trade-offs |
| Known Uses | No | Real-world examples |
| Related Patterns | No | Links to other patterns |

## 2. ADR Format Template

Use this template for anti-patterns and architectural decision records. This format emphasises problems and consequences.

### Template Structure

```markdown
## [Pattern Type] [Number]: [Pattern Name]

**Pattern ID:** `mx.[pattern|anti-pattern].domain.name`
**Status:** [active|deprecated|superseded]
**Intent:** One-sentence description of what this addresses

### Context

Where and when this pattern (or anti-pattern) appears:

- Industry context
- Technical context
- Business context
- Common scenarios

### Problem

Detailed description of the problem or anti-pattern.

For anti-patterns:
- What goes wrong
- Why it's problematic
- Who is affected (agents, users, developers)

For solution patterns:
- What challenge exists
- Why traditional approaches fail
- What's needed

### Forces

Competing concerns that influence the situation:

- Force 1: [e.g., developer convenience]
- Force 2: [e.g., agent compatibility]
- Force 3: [e.g., user experience]
- Force 4: [e.g., business requirements]

### Solution

For anti-patterns: How to fix or avoid the problem
For solution patterns: The recommended approach

Include:
- Concrete steps
- Code examples
- Best practices
- Tools and techniques

### Resulting Context

What changes after addressing this pattern:

- Outcome 1: [specific improvement]
- Outcome 2: [specific improvement]
- Outcome 3: [specific improvement]

### Consequences

**Positive:**
- Benefit 1: [specific advantage]
- Benefit 2: [specific advantage]

**Negative/Trade-offs:**
- Trade-off 1: [specific cost or limitation]
- Trade-off 2: [specific cost or limitation]

### Known Uses

Real-world examples:

- Organisation/project: Description
- Organisation/project: Description

### Related Patterns

Cross-references:

- Pattern that complements this
- Pattern that extends this
- Alternative pattern

### References

- MX-Bible chapters
- External resources
- Tool documentation
```

### ADR-Specific Guidelines

**For Anti-Patterns:**

1. **Be specific:** Show actual code that demonstrates the problem
2. **Explain impact:** Describe how agents fail with this pattern
3. **Provide alternatives:** Always include the correct approach
4. **Include validation:** Show how to detect the anti-pattern

**For Solution Patterns:**

1. **Show benefits:** Explain advantages for both agents and humans
2. **Provide evidence:** Include real examples or test results
3. **Discuss trade-offs:** Be honest about costs
4. **Enable adoption:** Make implementation straightforward

## 3. Quick Start Card Template

Use this template for rapid-reference implementation guides. Quick Start Cards provide YAML metadata plus condensed instructions.

### Template Structure

```markdown
### Pattern Quick Start: [Pattern Name]

```yaml
card:
  id: mx.card.[domain].[purpose].[context]
  pattern: mx.pattern.[domain].[purpose].[platform]
  title: "[Clear, Action-Oriented Title]"
  version: "1.0.0"
  authors:
    - "Author Name"
    - "Co-Author Name"
  purpose: "[One-sentence description of what this enables]"
  boundary: "[local-only|cloud|hybrid|page-level|system-level]"
  tags:
    - tag1
    - tag2
    - tag3
  last_updated: "YYYY-MM-DD"
```

**Prerequisites:**
- Prerequisite 1
- Prerequisite 2

**Implementation Steps:**

1. **[Action 1]**
   ```bash
   # Command or code
   ```
   Brief explanation

2. **[Action 2]**
   ```bash
   # Command or code
   ```
   Brief explanation

3. **[Action 3]**
   ```bash
   # Command or code
   ```
   Brief explanation

**Expected Outcome:**
- Outcome 1: What you should see
- Outcome 2: What should work
- Outcome 3: How to verify success

**Validation:**
- [ ] Check 1: How to verify
- [ ] Check 2: How to verify
- [ ] Check 3: How to verify

**Troubleshooting:**
- **Issue:** Common problem
  **Solution:** How to fix

- **Issue:** Common problem
  **Solution:** How to fix

**Related Patterns:**
- Pattern name ([mx.pattern.id](link)) - Relationship

**References:**
- [MX-Bible Chapter X](link)
- [Tool Documentation](link)
```

### Quick Start Card Guidelines

**Card ID Naming:**
- Format: `mx.card.<domain>.<purpose>.<context>`
- Example: `mx.card.html.semantic-structure.product-pages`
- Keep concise but descriptive

**Purpose Statement:**
- Single sentence
- Action-oriented
- Specific outcome
- No jargon

**Implementation Steps:**
- 3-7 steps maximum
- Each step is atomic
- Include code examples
- Explain what each step accomplishes

**Validation Checklist:**
- Concrete checks
- Measurable outcomes
- Tool-based where possible
- Manual checks when needed

## 4. Pattern Validation Checklist

Use this checklist before publishing any pattern documentation.

### Pre-Publication Validation

**Metadata Validation:**

- [ ] YAML frontmatter is valid (no syntax errors)
- [ ] Pattern ID follows naming convention (`mx.pattern.domain.purpose.platform`)
- [ ] Version uses semantic versioning (MAJOR.MINOR.PATCH)
- [ ] Maturity level is specified and appropriate
- [ ] All required fields are present
- [ ] Keywords are relevant and complete
- [ ] Author attribution is correct

**Structural Validation:**

- [ ] Pattern Intent section is complete
- [ ] All template sections are present
- [ ] Context section describes where pattern applies
- [ ] Problem section clearly states the issue
- [ ] Forces section lists 3-5 competing concerns
- [ ] Solution section provides clear approach
- [ ] Resulting Context lists specific outcomes
- [ ] Consequences include both positive and negative
- [ ] Related Patterns includes cross-references

**Content Quality:**

- [ ] Writing follows MX voice (first-person, British English)
- [ ] Technical accuracy verified by expert reviewer
- [ ] Code examples are tested and working
- [ ] No future-tense statements about the pattern itself
- [ ] No unnecessary superlatives or marketing language
- [ ] Examples are concrete and realistic
- [ ] Trade-offs are honestly presented

**Implementation Steps:**

- [ ] Steps are reproducible
- [ ] Code examples are complete (no pseudocode)
- [ ] Commands are tested on target platform
- [ ] Dependencies are explicitly listed
- [ ] Each step explains what it accomplishes
- [ ] Steps are in logical order
- [ ] No steps are skipped or assumed

**Validation Section:**

- [ ] Validation checks are specific
- [ ] Checks can be automated where possible
- [ ] Manual checks have clear criteria
- [ ] Tools are named and linked
- [ ] Success criteria are measurable

**Cross-References:**

- [ ] All pattern links resolve correctly
- [ ] Related patterns are bidirectionally linked
- [ ] MX-Bible chapter references are accurate
- [ ] External links are valid and stable
- [ ] Tool documentation links are current

**Markdown Quality:**

- [ ] Passes `markdownlint` with project config
- [ ] Code blocks specify language
- [ ] Headings follow hierarchy (no skipped levels)
- [ ] Lists have blank lines before/after
- [ ] Tables are properly formatted
- [ ] Links use proper markdown syntax

**Accessibility:**

- [ ] Diagrams have text descriptions
- [ ] Code examples have explanatory text
- [ ] Abbreviations are expanded on first use
- [ ] Colour is not the only means of conveying information
- [ ] Language is clear and concise

**Machine Readability:**

- [ ] YAML frontmatter is parseable
- [ ] Pattern ID is unique
- [ ] Structured sections use consistent formatting
- [ ] Metadata includes ai-instruction field
- [ ] All tags are lowercase with hyphens

### Automated Validation Tools

**Recommended Tools:**

```bash
# Markdown linting
markdownlint -c config/.markdownlint.json [file.md]

# YAML validation
yamllint [file.md]

# Link checking
markdown-link-check [file.md]

# Spell checking
aspell check [file.md]
```

**Custom Validation Script:**

```bash
#!/bin/bash
# validate-pattern.sh
# Validates MX pattern documentation

FILE=$1

echo "Validating pattern: $FILE"

# Check YAML frontmatter
echo "✓ Checking YAML frontmatter..."
grep -q "^---$" "$FILE" || { echo "✗ Missing YAML frontmatter"; exit 1; }

# Check pattern ID
echo "✓ Checking pattern ID..."
grep -q "pattern-id:.*mx\.pattern\." "$FILE" || { echo "✗ Invalid pattern ID"; exit 1; }

# Check required sections
echo "✓ Checking required sections..."
grep -q "## Pattern Intent" "$FILE" || { echo "✗ Missing Pattern Intent"; exit 1; }
grep -q "### Context" "$FILE" || { echo "✗ Missing Context"; exit 1; }
grep -q "### Problem" "$FILE" || { echo "✗ Missing Problem"; exit 1; }
grep -q "### Forces" "$FILE" || { echo "✗ Missing Forces"; exit 1; }
grep -q "### Solution" "$FILE" || { echo "✗ Missing Solution"; exit 1; }

# Run markdownlint
echo "✓ Running markdown linter..."
markdownlint -c config/.markdownlint.json "$FILE"

echo "✓ Validation complete"
```

### Manual Review Checklist

**Technical Review:**

- [ ] Pattern addresses real problem
- [ ] Solution is technically sound
- [ ] Trade-offs are accurately described
- [ ] Dependencies are complete
- [ ] Security implications considered
- [ ] Performance implications noted

**Editorial Review:**

- [ ] Voice matches MX-Bible style
- [ ] Grammar and spelling correct
- [ ] British English used consistently
- [ ] Technical terms defined on first use
- [ ] Examples support explanations
- [ ] Logical flow from problem to solution

**Community Review (for public patterns):**

- [ ] Pattern fills genuine need
- [ ] Pattern doesn't duplicate existing patterns
- [ ] Pattern name is clear and descriptive
- [ ] Pattern is discoverable (good keywords)
- [ ] Pattern invites contribution
- [ ] Licensing is clear

## Usage Guidelines

### When to Use Each Template

**Pattern Intent Template:**
- New pattern documentation
- Comprehensive pattern descriptions
- Patterns requiring detailed context
- Patterns with complex implementations

**ADR Format Template:**
- Anti-pattern documentation
- Architectural decision records
- Problem-focused documentation
- Refactoring guidance

**Quick Start Card Template:**
- Rapid implementation guides
- Getting started tutorials
- Common pattern applications
- Reference cards for developers

**Validation Checklist:**
- Before pattern publication
- During pattern review
- For pattern quality assurance
- As contribution guideline

### Customising Templates

Templates can be adapted for specific contexts:

**For Short Patterns:**
- Combine Related Patterns and References sections
- Reduce number of Forces to 3
- Simplify Consequences to essential trade-offs

**For Complex Patterns:**
- Add Architecture Diagram section
- Expand Implementation Steps with subsections
- Include Performance Considerations section
- Add Security Implications section

**For Multi-Platform Patterns:**
- Add Platform Variants section
- Include platform-specific notes in Implementation
- Create separate Quick Start Cards per platform

## Pattern Naming Convention

### Standard Format

```
mx.pattern.<domain>.<purpose>.<platform>@<version>
```

**Components:**

| Component | Description | Examples |
|-----------|-------------|----------|
| `mx.pattern` | Prefix (required) | Always `mx.pattern` |
| `<domain>` | Subject area | `html`, `metadata`, `agent`, `security` |
| `<purpose>` | What it does | `semantic-structure`, `validation`, `local-agent` |
| `<platform>` | Where it runs | `macos`, `linux`, `windows`, `web`, `cross-platform` |
| `@<version>` | Version (optional) | `@1.0.0`, `@2.1.3` |

**Examples:**

```
mx.pattern.html.semantic-structure.web
mx.pattern.agent.local-boundary.macos
mx.pattern.metadata.schema-org.ecommerce
mx.pattern.security.authentication.cross-platform@2.0.0
```

### Naming Guidelines

1. **Use lowercase** throughout
2. **Use hyphens** for word separation
3. **Be specific** but not verbose
4. **Include platform** even if cross-platform
5. **Version explicitly** for published patterns

## Pattern Lifecycle

Patterns progress through maturity stages:

| Stage | Description | Review Required |
|-------|-------------|-----------------|
| **Draft** | Initial development, incomplete | Internal only |
| **Proposed** | Complete, ready for review | Community review |
| **Adopted** | Accepted by community | Editorial + technical |
| **Mature** | Proven in production use | Periodic review |
| **Deprecated** | Superseded by better pattern | Retirement plan |
| **Archived** | Historical reference only | No further updates |

**Transition Criteria:**

- **Draft → Proposed:** All template sections complete, validated
- **Proposed → Adopted:** Community review passed, no blocking issues
- **Adopted → Mature:** Used in 3+ production deployments, 6+ months stable
- **Mature → Deprecated:** Better pattern available, migration path documented
- **Deprecated → Archived:** All users migrated, historical value only

## References

**Related MX-Bible Chapters:**

- Chapter 11: Designing for Both (pattern philosophy)
- Chapter 12: Technical Advice (implementation patterns)
- Appendix N: Anti-Patterns Catalogue (ADR examples)

**Related Resources:**

- [Gang of Four Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns)
- [Architectural Decision Records (ADRs)](https://adr.github.io/)
- [Christopher Alexander's Pattern Language](https://en.wikipedia.org/wiki/Pattern_language)

**MX Pattern Documentation:**

- [Plan 1: Extract patterns to MX-Bible](../../docs/structure/plan-1-extract-patterns-to-bible.md)
- [Plan 2: MX Patterns book structure](../../docs/structure/plan-2-mx-patterns-book-structure.md)
- [Project Roadmap](../../docs/structure/project-roadmap-mx-patterns.md)
