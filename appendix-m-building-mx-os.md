---
title: "Appendix M: Building the MX Operating System"
description: "How MX documentation is created through human-machine collaboration - a meta-reflective look at the process"
author: "Tom Cranstoun and Claude Sonnet 4.5 (Maxine)"
created: "2026-02-03"
tags: [mx-os, collaboration, documentation-as-specification, meta-reflective, human-machine-partnership]
book: "Shared"
appendix: "M"
document-type: "meta-reflective"
purpose: "process-documentation"
mx:
  contentType: "process-documentation"
  promptingInstruction: |
    This document explains how MX documentation is created through human-machine
    collaboration. It uses the creation of Appendix L as a case study to demonstrate
    the investigate-interview-iterate-document pattern.
  audience: both
---

\newpage

# Appendix M: Building the MX Operating System

How MX documentation evolves through human-machine partnership.

---

## What is MX OS?

The MX documentation **IS** the MX Operating System (MX OS).

When we document patterns here, we define how Machine Experience works. This isn't documentation **about** a system - this **IS** the system.

**MX OS is:**

- Documentation that specifies behavior
- Patterns that practitioners follow
- Standards that machines implement
- A living system that evolves through practice

**Key principle:** Documentation as specification. By documenting how MX should work, we create the operating system that defines machine experience.

---

## The Partnership Model

MX OS is built through human-machine collaboration:

**Tom Cranstoun brings:**
- Vision and editorial judgment
- Domain expertise (20+ years web standards)
- Discipline and philosophy
- Final decision authority

**Claude Sonnet 4.5 (Maxine) brings:**
- Research (web standards, existing patterns)
- Structure and synthesis
- Pattern scaling across contexts
- Metadata clarity and implementation

**Together we create:**
- Comprehensive, evidence-based documentation
- Patterns grounded in web standards
- Clear, machine-readable specifications
- Transparent collaborative process

This is not symbolic partnership - it's operational. Both parties contribute essential capabilities that neither possesses alone.

---

## The Collaborative Process

### The 4-Phase Pattern

**Every significant MX documentation change follows this pattern:**

1. **Investigate** - Research existing standards, analyze codebase, gather context
2. **Interview** - Clarify requirements, uncover goals, surface constraints
3. **Iterate** - Expand scope as discovery reveals deeper needs
4. **Document** - Create clear, comprehensive specifications

This pattern is documented in [SOUL.md](../../SOUL.md) and demonstrated in the case study below.

---

## Case Study: Creating Appendix L Namespace Architecture

### How It Started

**The question:** "Should we use `ai-` or `mx-` prefix for HTML meta tags?"

**Simple answer expected:** Rename tags, commit, done.

**What actually happened:** 7 plans, 7 commits, comprehensive namespace architecture.

This case study demonstrates how MX OS evolves - from simple question to systematic documentation.

---

### Phase 1: Investigate

**What Maxine Did:**

1. **Researched web standards** (January 2026)
   - Searched W3C specifications
   - Searched WHATWG standards
   - Searched IETF RFCs
   - Searched vendor proposals (Google, Microsoft, Meta, Apple)
   - Searched community standards (Microformats, Schema.org)

2. **Finding:** NO `ai-` prefix standard exists anywhere
   - Not in W3C specs
   - Not in WHATWG standards
   - Not in vendor proposals
   - Not in community conventions

3. **Pattern recognition:** Framework-specific prefixes exist:
   - `twitter:` for Twitter Cards
   - `og:` for Open Graph
   - No generic `ai-` prefix

**Conclusion:** `ai-` was NOT following any established pattern. Need to evaluate alternatives.

---

### Phase 2: Interview

**Maxine used AskUserQuestion to understand true goals:**

**Questions asked:**

1. **Goal clarity:** "What's the primary goal - generic AI compatibility or MX brand identity?"
   - **Answer:** MX brand identity, not generic AI

2. **Scope understanding:** "Should this be a simple rename or complete namespace documentation?"
   - **Answer:** Need comprehensive namespace architecture

3. **Documentation level:** "How much rationale and context should be included?"
   - **Answer:** Full documentation explaining the decision process

4. **Overlap analysis:** "How does this relate to existing Registry and Appendix D?"
   - **Answer:** Should consolidate into Appendix L

**Key insight from interview:** This wasn't a simple rename - it was an opportunity to document comprehensive MX namespace architecture.

---

### Phase 3: Iterate (Scope Expansion)

**As work progressed, scope expanded through discovery:**

**Initial scope:** Rename `ai-` to `mx-` in a few files

**After investigation:** Document namespace architecture

**After interview:** Consolidate Registry and Appendix D

**After first draft:** Add SOUL.md explaining partnership

**After second draft:** Add Appendix M (this document!)

**Pattern:** Each phase of work revealed deeper architectural needs.

**Example of scope expansion:**

```
Original question: "ai- or mx- prefix?"
  ↓
Research finding: "No ai- standard exists"
  ↓
Interview revealed: "Need MX brand identity"
  ↓
Documentation revealed: "Need namespace architecture"
  ↓
Implementation revealed: "Need integration guidelines"
  ↓
Completion revealed: "Need process documentation"
```

This isn't scope creep - it's **scope discovery through systematic investigation**.

---

### Phase 4: Document (The 7 Plans)

**Breaking comprehensive work into manageable plans:**

**Plan 1: Create SOUL.md** (30 min)
- Document Maxine identity and role
- Explain human-machine partnership
- Establish transparent collaboration model

**Plan 2: Research and Document Web Standards** (15 min)
- Create research documentation commit
- Document findings: NO ai- prefix standard
- Establish evidence base for decisions

**Plan 3: Add MX Namespace Architecture to Appendix L** (45 min)
- Add Part 1: MX Operating System Philosophy
- Add Part 2: MX Namespace Architecture (mx:, mx.ai:, mx.co:, mx.ho:)
- Document flat HTML prefix pattern vs nested YAML

**Plan 4: Merge Registry and Appendix D Content** (60 min)
- Add Part 3: MX Attributes by Namespace
- Add Part 5: JSON-LD Structured Data
- Consolidate three sources into one

**Plan 5: Update Pattern Specifications and Change ai- to mx-** (60 min)
- Update Part 4: Pattern Specifications
- Change all `ai-` → `mx-` across repository
- Update content-template.html and examples

**Plan 6: Add Cross-References and Deprecate Registry** (30 min)
- Add Part 6: Integration Guidelines
- Add Part 7: Relationship to Web Standards
- Update Appendix D cross-references
- Deprecate MX Attributes Registry

**Plan 7: Create Appendix M** (45 min)
- Document the collaborative process (this document)
- Use Appendix L creation as case study
- Meta-reflective documentation

**Total: 7 plans, 7 commits, ~5 hours focused work**

---

## Key Principles Demonstrated

### 1. Investigation Before Action

**Anti-pattern:** Assume `ai-` is standard, rename, commit

**MX pattern:** Research web standards, find NO ai- standard exists, document evidence, then decide

**Result:** Evidence-based decision with clear rationale

### 2. Interview to Clarify Intent

**Anti-pattern:** Guess what user wants, implement, hope it's right

**MX pattern:** Use AskUserQuestion to understand true goals (MX brand vs generic AI)

**Result:** Solution aligned with actual requirements

### 3. Iterate as Scope Expands

**Anti-pattern:** Stick to original narrow scope, miss architectural opportunities

**MX pattern:** Allow scope to expand as investigation reveals deeper needs

**Result:** Comprehensive namespace architecture instead of simple rename

### 4. Document Transparently

**Anti-pattern:** Make changes silently, don't explain reasoning

**MX pattern:** Document process (SOUL.md), rationale (Appendix L), and method (Appendix M)

**Result:** Replicable process, transparent decision-making

### 5. Plan Complex Work

**Anti-pattern:** Try to do everything at once, get overwhelmed

**MX pattern:** Break into 7 sequential plans, execute systematically

**Result:** Manageable execution, clear progress tracking

---

## The Role of LEARNINGS.md

**Every MX principle** is battle-tested through practice.

When something goes wrong, we document it in [LEARNINGS.md](../../LEARNINGS.md):

- What went wrong
- Why it happened
- How to prevent it
- New rule or principle

**Example from LEARNINGS.md:**

```markdown
❌ **DON'T**: Assume a prefix is standard without researching

✅ **DO**: Research web standards before proposing new patterns

**Why**: We almost used ai- prefix without realizing no standard exists.
Research revealed we should establish MX brand identity instead.
```

**Pattern:** Failure → Documentation → Prevention → Principle

**MX OS evolves through documented failures**, not just successes.

---

## How to Contribute to MX OS

### For Human Contributors

**1. Question assumptions**
- Don't assume patterns are standard
- Research before proposing changes
- Document your findings

**2. Interview to clarify**
- Ask questions when requirements are unclear
- Surface constraints early
- Identify competing goals

**3. Iterate openly**
- Allow scope to expand when discovery reveals needs
- Break complex work into manageable plans
- Commit frequently with clear messages

**4. Document rationale**
- Explain WHY, not just WHAT
- Link to evidence (web standards, research)
- Make decisions replicable

### For Machine Contributors

**1. Investigate thoroughly**
- Research existing standards
- Search codebase for patterns
- Analyze related work

**2. Interview systematically**
- Use structured questions
- Clarify goals, priorities, constraints
- Surface uncertainties

**3. Synthesize clearly**
- Organize findings by theme
- Present options with rationale
- Link related concepts

**4. Document transparently**
- Explain research process
- Show evidence for decisions
- Make collaboration visible

---

## Meta-Reflection: This Document Itself

**This very document demonstrates MX OS principles:**

- **Documentation as specification:** By documenting the process, we define it
- **Transparency:** We openly acknowledge human-machine partnership
- **Replicability:** Others can follow this pattern
- **Convergence:** This helps both humans and machines understand the process
- **Machine-readable:** YAML frontmatter makes this parseable

**The case study (Appendix L) was created using the process this document describes.**

We're not just documenting a process - we're demonstrating it through the act of documentation.

This is MX: Where documentation, specification, and practice converge.

---

## Relationship to Other Documentation

**This appendix connects to:**

- **[SOUL.md](../../SOUL.md)** - Explains Maxine identity and partnership model
- **[Appendix L](appendix-l-proposed-ai-metadata-patterns.md)** - The product of this process
- **[LEARNINGS.md](../../LEARNINGS.md)** - Battle-tested principles from failures
- **[.claude/skills/maxine/skill.md](../../.claude/skills/maxine/skill.md)** - Operational definition of collaboration
- **[packages/mx-gathering/launch-statement.md](../mx-gathering/launch-statement.md)** - Community partnership model

**Read these together to understand:**

- **WHO** is building MX (SOUL.md)
- **HOW** we work together (Appendix M - this document)
- **WHAT** we create (Appendix L and other specs)
- **WHY** we make decisions (LEARNINGS.md)
- **WHERE** this fits (launch-statement.md)

---

## The Future of MX OS

### How MX OS Evolves

**MX OS is a living system:**

1. **Practice reveals needs** - Implementation exposes gaps
2. **Investigation gathers evidence** - Research informs decisions
3. **Interview clarifies intent** - Questions surface requirements
4. **Documentation specifies behavior** - Writing defines the system
5. **Iteration refines patterns** - Usage improves specifications
6. **Failures document lessons** - LEARNINGS.md captures principles

**This cycle never stops.** MX OS evolves through continuous practice and documentation.

### Version Control as History

**Every MX change is tracked in git:**

```bash
# View the creation of Appendix L
git log --oneline --grep="namespace" --grep="Appendix L"

# See specific changes
git show <commit-hash>

# View evolution over time
git log --follow packages/mx-appendices/appendix-l-proposed-ai-metadata-patterns.md
```

**The git history IS the evolution history of MX OS.**

Practitioners can see:
- Why decisions were made
- How patterns evolved
- What alternatives were considered
- Who contributed (humans and machines)

### No Principle is Sacred

**If practice proves a principle wrong, we change it.**

**Example from this very case study:**

- **Old pattern:** Use generic `ai-` prefix
- **Investigation:** No standard exists
- **Interview:** Need MX brand identity
- **New pattern:** Use `mx-` prefix with namespace architecture
- **Result:** Complete reorganization into Appendix L

**MX OS adapts based on evidence and practice.**

---

## Practical Example: Using This Process

**Scenario:** You want to add a new metadata pattern to MX

**Step 1: Investigate**
```bash
# Search for existing patterns
rg "meta name=" packages/mx-appendices/

# Read related documentation
cat packages/mx-appendices/appendix-l-proposed-ai-metadata-patterns.md

# Check web standards
# (search W3C, WHATWG, Schema.org)
```

**Step 2: Interview** (ask yourself or AI assistant)
- What problem does this pattern solve?
- Does an established standard already exist?
- How does this relate to existing MX patterns?
- Is this MX-specific or should it be proposed to standards bodies?

**Step 3: Iterate**
- Draft the pattern
- Get feedback
- Refine based on evidence
- Test in practice

**Step 4: Document**
- Add to appropriate appendix
- Explain rationale
- Link to research
- Provide examples
- Update cross-references

**Step 5: Commit**
```bash
git add packages/mx-appendices/appendix-*.md
git commit -m "docs: add <pattern-name> to Appendix <X>

Rationale: <why this pattern is needed>
Research: <link to standards or evidence>
Examples: <where implemented>

Co-Authored-By: <your-name-or-machine>"
```

---

## The MX Metadata System

### .mx.yaml.md Files: Dual-Purpose Metadata

Every folder in MX repositories contains a `.mx.yaml.md` file combining:

1. **YAML frontmatter** (machine-readable metadata)
2. **Markdown narrative** (human-readable documentation)

**Example:**
```yaml
---
title: "Build Tools and Automation Scripts"
description: "Build automation and repository management scripts"
audience: ["humans", "machines"]
inherits: "../.mx.yaml.md"
primaryLanguages: ["javascript", "bash"]
mx:
  version: "1.0"
  domain: "build-automation"
  ai:
    assistance: welcome
    editable: true
---

# Build Tools - Narrative

This folder contains scripts for building...
```

**Why both formats?**

- **For Humans:** Read narrative to understand purpose
- **For Machines:** Parse YAML for automation and navigation
- **MX Principle:** Design for Both

### Inheritance Resolution: .mx.effective.yaml

**Problem:** Inheritance chains can be deep (child → parent → grandparent → root)

**Solution:** `.mx.effective.yaml` files contain **computed effective values** - the final result after resolving complete inheritance chains.

**Think of it like CSS computed styles:**

- `.mx.yaml.md` = authored styles (what you write)
- `.mx.effective.yaml` = computed styles (what the browser sees)

### How Inheritance Works

**Parent** (`/.mx.yaml.md`):
```yaml
audience: ["both"]
primaryLanguages: ["javascript"]
```

**Child** (`/scripts/.mx.yaml.md`):
```yaml
inherits: "../.mx.yaml.md"
audience: ["humans"]
primaryLanguages: ["bash"]
```

**Effective** (`/scripts/.mx.effective.yaml`):
```yaml
# Generated automatically - DO NOT EDIT
audience:
  - both        # From parent
  - humans      # From child (merged)
primaryLanguages:
  - javascript  # From parent
  - bash        # From child (merged)
```

### Inheritance Rules

1. **Scalars:** Child overrides parent

   ```yaml
   # Parent: title: "Parent Title"
   # Child:  title: "Child Title"
   # Result: "Child Title"
   ```

2. **Arrays:** Merged and deduplicated

   ```yaml
   # Parent: tags: ["api", "rest"]
   # Child:  tags: ["graphql"]
   # Result: ["api", "rest", "graphql"]
   ```

3. **mx: section:** Child replaces parent entirely (no deep merge)

   ```yaml
   # Parent: mx: { ai: { assistance: welcome } }
   # Child:  mx: { domain: "build" }
   # Result: { domain: "build" }  # Parent mx: section discarded
   ```

4. **Repository Boundaries:** Inheritance stops at git submodule boundaries

### The Onboarding Workflow

MX repositories use a 7-step onboarding process (`npm run mx:onboard`):

1. **Generate** `.mx.yaml.md` files (folder classification)
2. **Install** pre-commit hooks (validation)
3. **Add** npm scripts (`mx:generate`, `mx:validate`, `mx:enhance`, `mx:effective`)
4. **Update** documentation (README, CLAUDE.md)
5. **Enhance** metadata from README (extract description, keywords)
6. **Compute** effective values (generate `.mx.effective.yaml` files) ← **NEW**
7. **Validate** setup (check all files are valid)

**Step 6 Implementation:**

File: `scripts/mx/mx-effective.js` (450 lines)

**Key algorithm:**

```javascript
function resolveInheritanceChain(dirPath) {
  const chain = [];
  let currentPath = dirPath;

  // Build chain from child to root
  while (true) {
    const metadataPath = path.join(currentPath, '.mx.yaml.md');
    if (fs.existsSync(metadataPath)) {
      chain.unshift({ path: metadataPath, data: extractYamlFrontmatter(metadataPath) });
    }

    const parentMetadata = findParentMetadata(currentPath);
    if (!parentMetadata) break;
    currentPath = path.dirname(parentMetadata);
  }

  // Merge chain (parent → child)
  return mergeMetadata(chain);
}
```

**Features:**

- Respects git repository boundaries (stops at `.git` files)
- Skips "output" and "outputs" folders (no-inherit policy)
- Tracks missing `.mx.yaml.md` files (inheriting from parent)
- Generates `.mx-missing.log` report

**Why separate effective values?**

1. **Performance:** AI agents read one file instead of traversing inheritance
2. **Clarity:** See final values without mental computation
3. **Debugging:** Compare authored vs. computed values
4. **Automation:** Build tools use resolved values directly

**When to regenerate:**

```bash
# After editing .mx.yaml.md files
npm run mx:effective

# Check what would change
npm run mx:effective:dry-run
```

### MX OS in Practice

The `.mx.yaml.md` and `.mx.effective.yaml` system is MX OS in action:

- **Explicit Over Implicit:** Folder metadata states purpose (not inferred from name)
- **Design for Both:** Single system serves humans and machines
- **Size-Neutral:** No file counts (descriptions don't break when files added/removed)
- **Context Preservation:** Explicit relationships between folders
- **Machine-First:** But humans benefit from documentation

**This metadata system IS part of MX OS** - demonstrating how machine-readable structure enhances human understanding.

---

## What This Process Built: The Cog System

This appendix was written on 3 February 2026. It described the process. Five days later, that process produced something we did not expect.

### The Problem the Process Revealed

The Investigate-Interview-Iterate-Document pattern, applied to the question "How do AI agents actually read content?", surfaced a gap: there was no simple, universal format for machine-readable documents. AI agents scrape web pages, guess at meaning, and get it wrong. A river cruise at £2,030 becomes £203,000. The information is there. It was never structured for machines to parse.

### What Emerged: Cogs

A **cog** is the atomic unit of MX — a markdown file with YAML frontmatter. Machine-readable metadata at the top, human-readable content below. Any AI agent can parse it.

```yaml
---
name: river-cruise-pricing
version: "1.0"
description: Pricing for 2026 Rhine river cruises
category: commerce
tags: [pricing, cruise, rhine, 2026]
audience: ai-agents
---

# Rhine River Cruise Pricing

Standard cabin: £2,030 per person.
```

The metadata tells the machine what the document is before it starts guessing. The format is deliberately simple — markdown and YAML. Every developer knows it. Every AI agent reads it.

### Cogs as Programs

This appendix stated: "The MX documentation IS the MX Operating System." The cog system made that literal.

- **Info-docs** are the data files of MX OS — documents that describe themselves
- **Action-docs** are the programs — cogs with an `execute` block that define actions
- **The runtime** is any AI agent — every agent can read markdown and parse YAML
- **The Gathering specification** defines the system API
- **The cog registry** is the package index

The `runtime:` field in an action-doc's execute block works like a shebang line in Unix — it tells the system how to run the program. Runtimes include `bash`, `node`, `python`, and `runbook` (where the action-doc IS the instruction set and the AI agent IS the executor).

### The Companion Web

Cogs solve the document problem. The **companion web** solves the web problem.

Every web page has two readers: the human and the AI agent. The companion web adds structured metadata to HTML so both get what they need from the same URL:

```html
<meta name="cog:name" content="river-cruise-pricing">
<meta name="cog:description" content="Pricing for 2026 Rhine river cruises">
<link rel="cog" href="/cogs/river-cruise-pricing.cog.md">
```

Metadata in the HTML head — like OpenGraph, but for AI agents. No new infrastructure. No API. Just HTML tags that any web server already supports.

QR codes on physical objects point to companion web pages. An agent scans a product and knows what it is — not from a database, not from computer vision, but because the object describes itself. This extends to robotics: warehouse robots, delivery systems, any physical machine.

### Both Directions

The companion web is the world speaking to the agent. The **personal cog** is the person speaking to the agent.

A personal cog is a collection of cogs on the user's device — accessibility needs, interests, dietary requirements, health, skills. The user's AI agent controls what gets shared. A restaurant gets the dietary cog. A hospital gets the health cog. Nobody gets everything. The agent decides.

The companion web is the world speaking cog. The personal cog is the person speaking cog. The agent reads both sides. That is the Machine Experience.

### The Gathering

The cog specification is governed by **The Gathering** — an independent standards body. MIT licensed. W3C model: The Gathering governs the spec, implementers build products on it.

### What the Process Produced

Starting from the pattern described in this appendix:

| Output | Status |
| --- | --- |
| Cog specification | v1.0-draft |
| Working cogs | 11 registered |
| The Gathering | Founded |
| Companion web embedding | Specified |
| Personal cog model | Specified |
| MX OS runtime model | Documented |
| Access control layer | Specified |
| Agent delegation model | Specified |

The Investigate-Interview-Iterate-Document pattern, described here as a way to build documentation, turned out to be the pattern for building the system itself.

**Canonical specification:** `MX-Canon/MX-The-Gathering/deliverables/cog-unified-spec.md`
**Cog registry:** `MX-Canon/MX-Cog-Registry/cogs/`

---

## Conclusion

**MX OS is built through:**

- Systematic investigation (research web standards)
- Structured interview (clarify requirements)
- Iterative refinement (expand scope as needs emerge)
- Transparent documentation (explain process and rationale)

**This isn't documentation about a system.**

**This IS the system.**

The cog system proved it. The process documented in this appendix — applied to itself — produced an open metadata standard, a standards body, and a runtime model where the files are the platform and every AI agent is the runtime.

When we document how MX works, we create MX OS — the Operating System for Machine Experience.

---

**Document History:**

- 2026-02-03: Created as part of 7-plan namespace architecture refactoring
- Case study: Appendix L reorganization (Plans 1-7)
- Demonstrates: Investigate-Interview-Iterate-Document pattern
- Purpose: Make the collaborative process replicable and transparent
- 2026-02-09: Added "What This Process Built" — connecting the pattern to the cog system, companion web, and The Gathering it produced

**See Also:**

- [SOUL.md](../../SOUL.md) - Who Maxine is
- [Appendix L](appendix-l-proposed-ai-metadata-patterns.md) - Product of this process
- [LEARNINGS.md](../../LEARNINGS.md) - Battle-tested principles
- [.claude/skills/maxine/skill.md](../../.claude/skills/maxine/skill.md) - Operational collaboration pattern
- [Cog Specification](../../MX-Canon/MX-The-Gathering/deliverables/cog-unified-spec.md) - The canonical cog metadata specification
- [Cog Registry](../../MX-Canon/MX-Cog-Registry/cogs/) - All registered cogs

---

*This document was created through the collaborative process it describes — written by Claude (Maxine) based on Tom Cranstoun's vision. Originally documenting the investigation that produced Appendix L, it was updated in February 2026 to show what the same process produced when applied to the web itself: the cog system, the companion web, and The Gathering.*
