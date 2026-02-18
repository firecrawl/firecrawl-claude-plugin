---
description: Generate a complete Agent Skill from a documentation URL using Firecrawl
argument-hint: <documentation-url>
---

# Generate Skill from Documentation

Create a complete, production-ready Agent Skill by scraping documentation with Firecrawl. The skill you build is for an AI agent to use — include information that is beneficial and non-obvious. Consider what procedural knowledge, domain-specific details, or reusable assets would help an agent execute tasks more effectively.

The user provided this documentation URL: **$ARGUMENTS**

## Step 1: Scrape the documentation

Use the `firecrawl` skill to fetch the documentation at `$ARGUMENTS`:

1. **Map the site** to discover all relevant pages:
   ```
   firecrawl map $ARGUMENTS --search "<tool-name> API reference getting started"
   ```
2. **Scrape the key pages** (API reference, quickstart, core concepts, auth, examples):
   ```
   firecrawl scrape <page-url> --format markdown
   ```
3. For large doc sites, crawl with limits:
   ```
   firecrawl crawl $ARGUMENTS --maxDepth 2 --limit 15
   ```

Focus on API references, getting started guides, core concepts, authentication, and code examples. Skip changelogs, blog posts, and community pages.

## Step 2: Clarify the skill scope

After scraping, ask the user 1-2 brief questions (skip if already clear):

- What should the skill be named? (suggest a kebab-case name based on the docs)
- What are the 2-3 primary use cases? (e.g., "What would a user say that should trigger this skill?")

## Step 3: Plan the skill contents

Analyze each use case by considering how to execute it from scratch, then identify what reusable resources would help when doing it repeatedly.

Decision guide for resource types:

- **Scripts** (`scripts/`) — when the same code would be rewritten each time (e.g., a `pdf-editor` skill for "rotate this PDF" → `scripts/rotate_pdf.py`)
- **References** (`references/`) — when the agent needs to re-discover schemas, specs, or domain knowledge each time (e.g., a `big-query` skill → `references/schema.md` for table schemas)
- **Assets** (`assets/`) — when the same boilerplate is needed each time (e.g., a `webapp-builder` skill → `assets/hello-world/` template)

## Step 4: Present the plan for approval

**MANDATORY — do NOT write any files before this step.**

Present the user with a complete overview of what will be created:

1. The proposed directory tree (all files and folders)
2. A brief summary of what each file will contain
3. The proposed SKILL.md frontmatter (`name` and `description`)

Wait for the user to approve the plan before proceeding. If the user requests changes, revise the plan and present it again.

## Step 5: Ask where to place the skill

**MANDATORY — do NOT write any files before asking.**

Ask the user where the skill should be saved. Present these options:

1. **Project** — `.claude/skills/<skill-name>/` in the current working directory. The skill will only be available in this project.
2. **Global** — `~/.claude/skills/<skill-name>/` in the user's home directory. The skill will be available across all projects.
3. **Custom path** — let the user specify any directory.

Do NOT default to any location. Always ask and wait for the user's explicit choice before writing any files.

## Step 6: Build the skill

Only after the user has approved the plan AND chosen a location, write all files following the skill format reference below.

If the skill includes scripts, test them by running them to verify they work before delivering. If there are many similar scripts, test a representative sample.

## Step 7: Validate the skill

After writing all files, run these concrete checks and report results:

1. **Frontmatter check** — read SKILL.md and verify:
   - Has `name` field (kebab-case, max 64 chars, no consecutive hyphens, doesn't start/end with hyphen)
   - Has `description` field (non-empty, max 1024 chars)
   - `name` matches the parent directory name exactly
2. **Line count check** — count lines in SKILL.md and confirm it is under 500 lines:
   ```
   wc -l <path-to-SKILL.md>
   ```
3. **No junk files check** — confirm the skill directory does NOT contain README.md, CHANGELOG.md, INSTALLATION_GUIDE.md, or any other auxiliary documentation
4. **References depth check** — confirm all reference files are one level deep from SKILL.md (no nested subdirectories inside references/)

Report each check as PASS or FAIL. If any check fails, fix the issue before delivering.

## Step 8: Deliver

Present to the user:

- Summary of what was built
- Full directory tree with line counts
- Validation results (all checks should be PASS)
- The location where files were saved

---

## Skill format reference

### SKILL.md structure

```
<skill-name>/
├── SKILL.md          (required)
├── scripts/          (optional — executable code for deterministic tasks)
├── references/       (optional — docs loaded into context on-demand)
└── assets/           (optional — templates/files used in output, not loaded into context)
```

### Frontmatter

```yaml
---
name: <skill-name>
description: |
  What this skill does AND when to use it. Max 1024 chars.
  Include specific triggers and contexts. This is the primary activation mechanism.
  All "when to use" info goes HERE — not in the body (the body loads after triggering).
---
```

- `name`: kebab-case, max 64 chars, lowercase + numbers + hyphens, must match directory name
- `description`: the most important field — the agent uses this to decide when to activate the skill

Good description example:
```yaml
description: |
  Comprehensive document creation, editing, and analysis with support for tracked
  changes, comments, formatting preservation, and text extraction. Use when working
  with professional documents (.docx files) for: (1) Creating new documents,
  (2) Modifying or editing content, (3) Working with tracked changes,
  (4) Adding comments, or any other document tasks.
```

### Body

- Keep under 500 lines. Use imperative/infinitive form.
- **The agent is already very smart.** Only add context it doesn't already have. Challenge each paragraph: "Does this justify its token cost?"
- Prefer concise examples over verbose explanations.
- Do NOT add "When to Use This Skill" sections in the body — that belongs in the description.

### Degrees of freedom

Match specificity to the task's fragility:

- **High freedom** (text instructions) — multiple valid approaches, context-dependent decisions
- **Medium freedom** (pseudocode/parameterized scripts) — preferred pattern exists, some variation OK
- **Low freedom** (exact scripts, few params) — fragile operations, consistency critical

Think of the agent exploring a path: a narrow bridge needs guardrails (low freedom), an open field allows many routes (high freedom).

### Progressive disclosure patterns

**Pattern 1 — High-level guide with references:**
```markdown
## Quick start
[core example]

## Advanced
- **Feature A**: See [references/feature-a.md](references/feature-a.md)
- **Feature B**: See [references/feature-b.md](references/feature-b.md)
```

**Pattern 2 — Domain-specific organization:**
```
skill/
├── SKILL.md (overview + navigation)
└── references/
    ├── finance.md
    ├── sales.md
    └── product.md
```
The agent loads only the relevant domain file.

**Pattern 3 — Conditional details:**
```markdown
## Basic usage
[simple instructions]

**For advanced feature X**: See [references/feature-x.md](references/feature-x.md)
```

When splitting content into reference files, clearly describe in SKILL.md when to read each file. For reference files over 100 lines, include a table of contents at the top.

### Workflow patterns for SKILL.md body

**Sequential workflows** — break multi-step processes into numbered steps:
```markdown
Processing involves these steps:
1. Analyze the input (run scripts/analyze.py)
2. Validate (run scripts/validate.py)
3. Execute (run scripts/process.py)
```

**Conditional workflows** — guide through decision points:
```markdown
1. Determine the type:
   **Creating new?** → Follow "Creation workflow" below
   **Editing existing?** → Follow "Editing workflow" below
```

### Output patterns for SKILL.md body

**Template pattern** — when consistent output format matters:
```markdown
## Output structure
ALWAYS use this template:
# [Title]
## Summary
## Key findings
## Recommendations
```

**Examples pattern** — when style/quality depends on seeing examples:
```markdown
**Input:** Added JWT authentication
**Output:**
feat(auth): implement JWT-based authentication
Add login endpoint and token validation middleware
```

Examples help the agent understand desired style better than descriptions alone.

### Key rules

- **No auxiliary docs** — do NOT create README.md, CHANGELOG.md, or any extra files
- **No duplication** — info lives in SKILL.md OR references, never both
- **References one level deep** — all reference files link directly from SKILL.md
- **Split at 500 lines** — move details to `references/` when SKILL.md approaches the limit
- **Large references** (>10k words) — include grep search patterns in SKILL.md for discovery
