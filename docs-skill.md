---
name: uniswap-docs-qa
description: "Apply this skill when reviewing or creating any page for docs.uniswap.org. It enforces the Uniswap content style guide: progressive disclosure, sidebar-friendly titles, semantic HTML, low word count with cross-linking, consistent terminology, frontmatter requirements, Diataxis page types, and SEO optimization. Use for QA audits, new page creation, and content consistency checks across the Uniswap docs-content repo (github.com/Uniswap/docs-content)."
---

# Uniswap Docs Content QA Skill

This skill defines the canonical content standard for every page in `github.com/Uniswap/docs-content`. Use it to audit existing pages, create new ones, or ensure consistency across `docs.uniswap.org`.

## 0. Canonical Source and Migration Scope (MANDATORY)

`github.com/Uniswap/docs-content` is the single source of truth for final published documentation.

This skill applies to content that originates from:
- `docs.uniswap.org`
- `api-docs.uniswap.org`
- `docs.unichain.org`

### Migration Objective
Consolidate and normalize all relevant documentation into `docs-content` so final output remains consistent in structure, terminology, metadata, and navigation regardless of source origin.

### Non-Negotiable Rules
1. Final state must always be represented in `docs-content`.
2. New or updated content from any source must be reconciled in `docs-content` before being considered complete.
3. Do not preserve source-specific wording if it conflicts with canonical terminology or style.
4. Use one canonical page per concept/task/reference; avoid duplicate pages across migrated sources.
5. Internal links must point to canonical `docs-content` destinations (no legacy source links except temporary migration notes).

## 1. Content Principles

These five principles govern every page. When in doubt, refer back here.

### 1.1 Progressive Disclosure

Nest pages wherever it makes sense to minimize the total number of top-level entries in each sidebar category. Reveal complexity gradually: overviews link to concepts, concepts link to guides, guides link to reference.

### 1.2 Brief but Clear Titles

Page titles should rarely spill onto two lines in the sidebar. Keep them short, but never sacrifice clarity. Understanding what a page covers is more important than character count. Aim for 35 characters or fewer. Allow up to 50 only when necessary for comprehension.

### 1.3 Semantic HTML

Use H1, H2, H3 headings correctly. They improve readability for humans, search engine ranking, and AI parsing (LLM context files, llms.txt). The `title:` frontmatter renders as the page's only H1. Body content starts at H2.

### 1.4 Low Word Count, Generous Cross-Linking

Sections should be easy to scan and quick to read. Do not repeat explanations that exist elsewhere. Cross-link to them with anchor links. Every concept mention is an opportunity to link.

### 1.5 Consistent Grammar and Terminology

Use the canonical terms in the Terminology Dictionary (section 8) everywhere. Never deviate.

## 2. Frontmatter Requirements (MANDATORY)

Every `.md` / `.mdx` file MUST have:

```yaml
---
title: "Title Case, Max 60 Chars, No Period"
description: "One action-oriented sentence, 60-160 chars. Include primary keyword. No markdown."
---
```

### Rules

| Field | Required | Format | SEO / LLM Impact |
|---|---|---|---|
| `title` | Yes | Title Case. 60 chars max. No trailing period. Brief enough for sidebar. | Renders as `<title>` and H1. Parsed by LLMs for context. |
| `description` | Yes | 60-160 chars. Action verb start. Include "Uniswap" and version when relevant. | Renders as `<meta name="description">`. Used by search engines and LLM context files. |
| `id` | Conditional | If an `id:` already exists, keep it. If it doesn't exist, don't add one. IDs are useful for stable routing and migration compatibility. | Balances maintainability with backward compatibility.|

### Description Formula

```
[Action verb] + [what] + [on/with Uniswap vX] + [optional: using Contract/SDK/API]
```

Examples:
- Good: `"Mint a concentrated liquidity position on Uniswap v4 using PositionManager."`
- Good: `"Learn how swap fees, protocol fees, and fee tiers work across Uniswap v2, v3, and v4."`
- Bad: `"This page describes fees."` (too short, passive, no keywords)
- Bad: `"A comprehensive guide to understanding the various fee mechanisms..."` (filler words)

## 3. Heading Hierarchy (Semantic HTML)

| Level | Usage | Casing | Count per Page |
|---|---|---|---|
| H1 (`#`) | NEVER in body. `title:` frontmatter is the H1. | N/A | 0 in body |
| H2 (`##`) | Major sections | Title Case | 2 to 6 |
| H3 (`###`) | Sub-topics within H2 | Sentence case | 0 to 4 per H2 |
| H4 (`####`) | Rare. Only deeply nested content. | Sentence case | 0 to 2 per H3 |

### Rules
- Never skip levels (H2 to H4 is invalid; always H2 then H3 then H4)
- H2 titles should be scannable. A reader should understand the page structure from H2s alone.
- Use descriptive headings, not generic ones like "Introduction", "Details", or "More Info"
- Headings are parsed by search engines and LLM context files. Make them keyword-rich.

## 4. Page Types (Diataxis Framework)

### 4.1 Overview Pages (`/overview`, `index.md`)
**Purpose:** Orient the reader within a section. Keep under 300 words before linking out.

Template:
```markdown
---
title: "Uniswap v4"
description: "Get started with Uniswap v4 protocol integration, including hooks, flash accounting, and the singleton PoolManager."
---

[2-3 sentence section intro. State what this section covers and who it is for.]

## Choose Your Integration Path

### Smart contracts
[1 sentence + link]

### SDK
[1 sentence + link]

### Uniswap API
[1 sentence + link]
```

"Where to go next" guidance: Evaluate case-by-case for overview pages. Add a structured navigation section (for example, "Choose your integration path") only when readers benefit from explicit branching beyond sidebar navigation.

Ensure every docs section is evaluated for an Overview page; create one only when it improves orientation or route selection, keep it concise and non-duplicative, and if no Overview section exists yet in this skill, add one with this rule and examples.

Common overview problems to avoid:
- Do not open with "Welcome to..." or "This page describes..."
- Do not duplicate deployment tables or code that belongs in reference/guide pages
- Do not include FAQ sections in overviews (split into a separate FAQ page)
- Do not include CI badge images (those belong in the GitHub README, not docs)
- Do not let the overview exceed 400 words. If it does, content needs to move to sub-pages.

### 4.2 Concept Pages (`/concepts/`)
**Purpose:** Explain WHAT something is and WHY it exists. No step-by-step code.

Template:
```markdown
---
title: "Flash Accounting"
description: "Understand flash accounting in Uniswap v4 and how deferred balance settlement reduces gas costs."
---

[1-3 sentence intro: what it is and why it matters.]

## How It Works

[Explanation. Diagrams if helpful. Cross-link to related concepts.]

## Key Properties

[Enumerate important characteristics. Keep it scannable.]
```

"Where to go next" guidance: Evaluate case-by-case. Add if the reader clearly needs guidance on what to read next (for example, a concept that directly leads to a guide). Omit if the sidebar navigation is sufficient.

### 4.3 Guide Pages (`/guides/`)
**Purpose:** Step-by-step HOW to accomplish a task.

Template:
```markdown
---
title: "Create Pool"
description: "Initialize a new Uniswap v4 pool with or without initial liquidity using PoolManager."
---

[1-2 sentence intro: what you will accomplish.]

## Prerequisites

- [List tools, versions, prior knowledge with links]

## Step 1: [Action Verb Phrase]

[Explanation + code block. Keep prose minimal.]

## Verification

[How to confirm it worked. Expected output, transaction hash, etc.]
```

"Where to go next" guidance: Quickstarts and getting-started guides SHOULD have a "Where to go next" section. Mid-sequence guides (step 2 of 5) generally do not need one because the sidebar nav buttons handle sequential navigation.

### 4.4 Reference Pages (`/deployments/`, `/endpoints/`, `/common-errors`)
**Purpose:** Look-up information. Tables, addresses, error codes.

Template:
```markdown
---
title: "Ethereum Deployments"
description: "Uniswap v4 contract deployment addresses on Ethereum Mainnet."
---

[One sentence of context.]

| Contract | Address | Notes |
|---|---|---|
| PoolManager | `0x000...` | Singleton |
```

"Where to go next" guidance: Generally NOT needed. Glossary, deployments, error reference, and endpoint docs do not need closing navigation because the sidebar buttons are enough.

## 5. "Where to Go Next" Decision Framework

The existing sidebar navigation buttons handle page-to-page movement in the content tree. A dedicated "Where to go next" section is an additional navigation aid. Use it selectively.

| Page Type | Add "Where to Go Next"? | Reasoning |
|---|---|---|
| Quickstarts / Getting started | Yes | Reader just completed something and needs guidance |
| Overviews | Yes (as integration paths) | That is the page's primary purpose |
| Concept pages (standalone) | Case-by-case | Add if concept directly leads to a specific guide |
| Concept pages (in a sequence) | Usually no | Sidebar handles sequential navigation |
| Guide pages (first in sequence) | Yes | Orient the reader before a multi-step journey |
| Guide pages (mid-sequence) | No | Sidebar "next" button is sufficient |
| Guide pages (final in sequence) | Yes | Reader finished the sequence. Where next? |
| Reference / Deployments | No | Look-up pages. Sidebar is enough. |
| Glossary | No | Reference material |
| Endpoint docs | No | API reference. Self-contained. |

When you DO add it:

```markdown
## Where to Go Next

- [Action phrase describing destination](/docs/path)
- [Another follow-up](/docs/path)
```

Rules:
- Default to 2-3 links for non-getting-started pages
- Use action phrases, not raw page titles: "Create your first pool" not "Create Pool"
- Links should follow logical reading order

### 5.1 Getting Started Navigation Coverage (MANDATORY)

For any `getting-started` page inside a `guides/` section, the `## Where to Go Next` section must cover all sibling pages in the nearest `meta.json` `pages` array, excluding the current `getting-started` page.

Rules:
- Resolve siblings from the nearest directory `meta.json`.
- Include every sibling slug exactly once in `Where to Go Next`.
- If a sibling is a subsection directory (for example `swapping`), link to that subsection's `getting-started` page when it exists; otherwise link to the subsection entry route.
- Apply this coverage rule only within `guides/` trees.
- During audits, verify there are no missing or extra `Where to Go Next` links versus `meta.json`.
## 6. Language and Tone

| Rule | Do | Do Not |
|---|---|---|
| Voice | Active, second person ("you"), present tense | Passive voice |
| Contractions | Use naturally (you'll, it's, don't) | Overly formal (you will, it is, do not) |
| Opening | State what + why immediately | "Welcome to...", "This page describes..." |
| Technical terms | Bold on first use, then plain text | Repeated bolding of the same term |
| Word count | Keep sections scannable. Cross-link instead of repeating. | Walls of text, duplicated explanations |
| Code references | Backticks: `swap()`, `poolKey`, `PositionManager` | Plain text for code identifiers |
| Dashes | Use "to" for ranges (2 to 6). No em-dashes. | Em-dashes, en-dashes |
| Neutrality | Use neutral, evidence-based phrasing ("It is expected...", "Historically...") | First-person ownership/control claims ("we expect", "we anticipate", "our view") |

### Neutral Language Guidance
Prefer neutral, objective phrasing that does not imply ownership or control over outcomes.
- Preferred: "It is expected that...", "It is anticipated that...", "Historically..."
- Avoid: "We expect...", "We anticipate...", "Our view is..."
Use modal qualifiers where appropriate: "may", "can", "typically", "in many cases".

## 7. Code Block Standards

Always specify the language tag. Show full imports. Comments explain WHY, not WHAT. After runnable code, show expected output.

Rules:
- Language tags required: `solidity`, `typescript`, `bash`, `graphql`, `json`
- Show full imports. Do not assume the reader knows the package structure.
- After runnable code, show expected output
- Use `// highlight-next-line` or `// highlight-start` / `// highlight-end` for emphasis

## 8. Terminology Dictionary (MANDATORY)

These are the canonical terms. Every page MUST use these exact forms.

| Correct | Wrong | Notes |
|---|---|---|
| Uniswap v1, v2, v3, v4 | V1, V2, V3, V4 | Lowercase "v" always, except in API enum values like `protocols: ['V2']` where it is a code literal |
| Uniswap API | Trading API | The product name is "Uniswap API" |
| Developer Platform | Developer Portal | Official name is "Developer Platform" |
| GitHub | Github, github | Capital H always |
| `PoolManager` | Pool Manager, Poolmanager | PascalCase, in backticks when referencing code |
| `PositionManager` | Position Manager | PascalCase, in backticks |
| `ERC-6909` | ERC6909, ERC 6909 | Hyphenated |
| `EIP-7702` | EIP7702, EIP 7702 | Hyphenated |
| UniswapX | Uniswap X, uniswapX | One word, capital X |
| Unichain | UniChain, unichain | One word, capital U only |
| hooks | Hooks | Lowercase in prose, unless starting a sentence |
| flash accounting | Flash Accounting | Lowercase in prose |
| concentrated liquidity | Concentrated Liquidity | Lowercase in prose |
| liquidity provider (LP) | Liquidity Provider | Lowercase in prose, abbreviation in parens on first use |
| onchain | on-chain, on chain | One word, no hyphen |
| offchain | off-chain, off chain | One word, no hyphen |
| calldata | call data, call-data | One word |
| smart contract | Smart Contract | Lowercase in prose |
| Solidity | solidity | Capital S |
| TypeScript | Typescript, typescript | Capital T and S |
| SDK | sdk | Always uppercase |

Note on API enum values: When showing code that uses API protocol enums (for example `protocols: ['V2', 'V3']`), uppercase V is correct because it is a code literal. In prose, always use lowercase: "Uniswap v2".

Lowercase "v" is a prose rule only. Preserve uppercase protocol versions in any code/literal context (\V2\, \V3\, \V4\), including inline code, code blocks, payloads, and enums.

### 8.1 Legal Language Requirements (MANDATORY)

These rules come from Uniswap Labs legal team review. They are non-negotiable and apply to all docs content.

#### Goals

- Assume every public word is official. Be clear, transparent, and technically precise.
- Highlight Uniswap Labs contributions accurately. Do not use hype, guarantees, or language that overstates Labs' role.

#### Principles

##### 1) Execution Language

The Uniswap API helps with routing and transaction preparation but does not execute trades. The user (or signer) performs final transaction submission onchain.

| Do | Do Not |
|---|---|
| "Submit the transaction with your signer" | "Execute the trade" / "The API executes the swap" |
| "The API provides routing and calldata" | "The API handles execution" |
| "Send the transaction onchain with your signer" | "Uniswap executes the transaction for you" |
| "Use the most efficient route based on current inputs" | "Best execution", "best pricing", "cheapest" |
| "Use reliable routing logic (where accurate)" | Guaranteed outcomes language |

Rules:
- Never use "execute" with the Uniswap API as the subject.
- Never imply auto-routing or automatic execution on behalf of the user.
- Always include signer responsibility in end-to-end flow descriptions.
- Prefer "most efficient" when discussing route quality. Avoid language implying guaranteed outcomes.

##### 2) Entity Separation and Naming

- Avoid promoting "Uniswap" or "Unichain" generally.
- Use "Uniswap Labs" for company actions and product names where applicable (for example: "Uniswap Wallet", "Uniswap Trading Protocol").
- Keep protocol statements factual and scoped to protocol behavior, not marketing claims.

##### 3) No Trading Outcome Claims

- Do not imply Uniswap Labs determines execution outcomes on behalf of users.
- Do not imply custody, discretion, or intermediary execution by Labs.
- Use precise phrasing: "The API returns quotes/routes/calldata; users sign and submit."

##### 4) Comparisons

- Neutral factual references are allowed (for example: "Uniswap v2, v3, v4").
- Do not use unsubstantiated value judgments ("superior to competitors", "best in class").
- Avoid promotional comparative claims about the Uniswap protocol.

##### 5) Avoid Loaded Terms

- Avoid ambiguous terms such as "fairness" unless explicitly defined.
- Prefer objective, verifiable phrasing.

#### Legal Review Examples

- Issue: "best execution" plus "auto-routing" can imply Labs determines outcomes for users.
  - Preferred: "most efficient route based on current inputs" and "users sign and submit the transaction."

- Issue: "fairness" can be interpreted in multiple legal/market senses.
  - Preferred: "Anyone will be able to verify blocks were built by priority ordering on Unichain."

## 9. SEO and LLM Checklist (Per Page)

Run this checklist when auditing or creating any page:

- [ ] `title:` present, Title Case, 60 chars max, includes primary keyword, 35 chars ideal for sidebar
- [ ] `description:` present, 60-160 chars, action-oriented, includes "Uniswap" and version
- [ ] If `id:` exists, keep it. If absent, don't add one.
- [ ] No `#` (H1) in body. Only `##` and below.
- [ ] Heading hierarchy is sequential (H2 then H3 then H4, no skips)
- [ ] Headings are descriptive and keyword-rich (not "Introduction" or "Details")
- [ ] First paragraph states what the page covers immediately (no filler)
- [ ] Word count is low. Cross-links replace duplicated explanations.
- [ ] Internal links use absolute paths (`/docs/...`)
- [ ] Code blocks have language tags
- [ ] Terminology matches dictionary (section 8). No "Trading API", "V4", "Github".
- [ ] "Where to go next" included only where appropriate (see section 5 decision framework)
- [ ] Page title does not duplicate another page's title (make unique per section)
- [ ] Overview pages are under 400 words and do not duplicate content from sub-pages

## 10. QA Audit Workflow

When auditing an existing page:

1. Frontmatter: title + description present and formatted correctly? Existing id preserved?
2. Headings: No H1 in body? Proper hierarchy? Proper casing? Keyword-rich?
3. Opening: First paragraph immediately states what + why? No "Welcome to..."?
4. Word count: Under 1500 words? If over, can sections be split or cross-linked?
5. Terminology: All terms match dictionary (section 8)?
6. Code: Language tags? Full imports? WHY comments?
7. Links: Absolute paths? No broken references? Cross-linked generously?
8. Navigation: "Where to go next" present where needed, absent where not needed (see section 5)?
9. Title length: Fits sidebar without wrapping to two lines?
10. Overview audit: If this is an overview, does it orient without duplicating sub-page content?
11. Log issues in the Content QA Tracker with severity and recommended fix.

## 11. File Naming Conventions

- Lowercase, hyphenated: `create-pool.mdx`, `flash-accounting.md`
- No spaces, underscores, or camelCase in filenames
- Use `.mdx` if the page contains JSX components (`<Cards>`, `<Tabs>`, `<Callout>`, etc.), `.md` otherwise
- Section entry: use `overview.md` or `index.md` (not both in the same directory)
- Filename equals URL slug. Choose descriptive, keyword-rich names.

## 12. Navigation and Routing Conventions (MANDATORY)

### meta.json Structure

Every directory that should appear in the sidebar needs a `meta.json` file.

| Property | Required | Notes |
|---|---|---|
| `title` | Yes | Display name in the sidebar |
| `root` | Only for top-level sections | Set `true` for sections listed in the root `meta.json` |
| `pages` | Yes | Ordered array of slugs matching filenames (without extension) or subdirectory names |
| `defaultOpen` | No | Omit entirely. `false` is the default behavior. Only set `true` if you need the section expanded. |

### Filename-to-Route Mapping

The filename determines the URL slug. The `title` frontmatter controls the display name. These are independent.

```
File:  get-started/your-first-swap.mdx
Route: /docs/get-started/your-first-swap
Title: "Your First Swap" (from frontmatter)
```

### Renaming Routes

When renaming a file (and therefore its route):

1. Rename the file
2. Update the `pages` array in the parent `meta.json`
3. Search the entire repo for internal links to the old path and update them all
4. Verify with `grep -r "/docs/old-path" .` that zero references remain

### Route Naming Rules

- Use lowercase, hyphenated slugs: `how-uniswap-works`, `your-first-swap`, `using-the-api`
- Slugs should be descriptive and keyword-rich, not generic (`overview` is acceptable for section entry points)
- Filename should match what the page is about, not legacy or internal names
- If a page has an `id:` in frontmatter that differs from the filename, the framework may use the `id` for routing. Keep both aligned or remove the `id` if it conflicts.

### Internal Link Rules

- Always use absolute paths: `/docs/ecosystem/governance/overview`, not `../governance/overview`
- After any rename, audit all files for stale references to the old path
- Never link to `/docs/resources/` (legacy), always `/docs/ecosystem/`
- Cross-reference checklist: quickstart paths, concept paths, guide paths, glossary paths

### Top-level Section Order

The root `meta.json` defines the global sidebar order. Current canonical order:

```json
["get-started", "trading", "liquidity", "ai-toolkit", "api", "protocols", "sdks", "unichain", "ecosystem"]
```

Changes to this order require team review.

## 13. Migration Workflow (docs.uniswap + api-docs + docs.unichain)

For each migrated page:
1. Classify source page type (Overview / Concept / Guide / Reference).
2. Create mapping record:
   - `source_url`
   - `destination_path` in `docs-content`
   - `content_owner`
   - `status`: `draft | in-review | migrated | verified`
3. Normalize frontmatter and headings per sections 2 and 3.
4. Apply terminology dictionary (section 8) and style/tone rules (section 6).
5. Merge overlapping pages into one canonical destination page when possible.
6. Replace or redirect legacy links to canonical destination.
7. Run QA checklist (section 9) plus migration checks below.
8. Mark as complete only when Definition of Done is met.

### Migration Consistency Checks (MANDATORY)
- [ ] Canonical destination exists in `docs-content`
- [ ] No conflicting duplicate page remains
- [ ] Terminology is fully normalized
- [ ] Navigation placement matches destination IA
- [ ] Cross-links updated to canonical destinations
- [ ] Legacy/source-specific wording removed or rewritten
- [ ] Technical accuracy validated against current product behavior

### Definition of Done for Migrated Content
A migrated item is done only when:
- It is published from `docs-content` as the canonical version
- It passes QA + migration consistency checks
- It does not require readers to rely on legacy source pages for core understanding

## 14. Migration Safety and Validation Workflow (MANDATORY)

This skill must not remove guide code wholesale. 

Preserve existing code until the replacement is reviewed and validated.

### Rules 

1. Do not delete or overwrite the original guide in a single step. 
2. Migrate guides one by one. 
3. Before replacing content, rename the previous version with an \-old\ suffix (or equivalent agreed convention) to keep a reviewable baseline. 
4. Compare old vs new for technical accuracy, completeness, and link integrity before finalizing. 
5. Mark each migrated page with status: \proposed\, \in-review\, \validated\, \final\. 
6. Only remove/archive old versions after validation is complete and stakeholders confirm.

### Autonomy Boundary 

This skill is not 100% autonomous. It provides structured guidance, proposed changes, and progress checkpoints so humans can validate direction, quality, and consistency during migration.

