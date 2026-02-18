---
description: Generate a complete Agent Skill from a documentation URL using Firecrawl
argument-hint: <documentation-url>
---

# Generate Skill from Documentation

Create a complete, production-ready Agent Skill by scraping documentation with Firecrawl and applying the skill-creator methodology.

The user provided this documentation URL: **$ARGUMENTS**

## Step 1: Load the skill-creator skill

**MANDATORY — do this first before anything else.**

Invoke the `skill-creator` skill now using the Skill tool:

```
Skill(skill: "skill-creator")
```

This loads Claude's official skill creation methodology, design patterns, and validation rules. All subsequent steps MUST follow the skill-creator's guidance. Do NOT skip this step. Do NOT proceed without it.

If the skill-creator skill fails to load or is not available, use the fallback rules in the "Fallback: Skill format reference" section at the bottom of this file.

## Step 2: Scrape the documentation

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

## Step 3: Clarify the skill scope

After scraping, ask the user 1-2 brief questions (skip if already clear):

- What should the skill be named? (suggest a kebab-case name based on the docs)
- What are the 2-3 primary use cases?

## Step 4: Plan the skill contents

Analyze the scraped docs and determine:

1. **Core capabilities** the skill should provide
2. **Scripts** (`scripts/`) — for operations that are deterministic and would be rewritten each time
3. **References** (`references/`) — for large docs to load on-demand (API schemas, detailed configs)
4. **Assets** (`assets/`) — templates or boilerplate files used in output

## Step 5: Present the plan for approval

**MANDATORY — do NOT write any files before this step.**

Present the user with a complete overview of what will be created:

1. The proposed directory tree (all files and folders)
2. A brief summary of what each file will contain
3. The proposed SKILL.md frontmatter (`name` and `description`)

Wait for the user to approve the plan before proceeding. If the user requests changes, revise the plan and present it again.

## Step 6: Ask where to place the skill

**MANDATORY — do NOT write any files before asking.**

Ask the user where the skill should be saved. Present these options:

1. **Project** — `.claude/skills/<skill-name>/` in the current working directory. The skill will only be available in this project.
2. **Global** — `~/.claude/skills/<skill-name>/` in the user's home directory. The skill will be available across all projects.
3. **Custom path** — let the user specify any directory.

Do NOT default to any location. Always ask and wait for the user's explicit choice before writing any files.

## Step 7: Build the skill

Only after the user has approved the plan AND chosen a location, write all files.

## Step 8: Validate the skill

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

## Step 9: Deliver

Present to the user:

- Summary of what was built
- Full directory tree with line counts
- Validation results (all checks should be PASS)
- The location where files were saved

---

## Fallback: Skill format reference

Use ONLY if the skill-creator skill failed to load in Step 1.

### SKILL.md format

Every skill is a directory with a required `SKILL.md` containing YAML frontmatter + Markdown body:

```
<skill-name>/
├── SKILL.md          (required)
├── scripts/          (optional)
├── references/       (optional)
└── assets/           (optional)
```

**Frontmatter (required):**
```yaml
---
name: <skill-name>
description: |
  What this skill does AND when to use it. Max 1024 chars.
  Include specific triggers. This is the primary activation mechanism.
---
```

- `name`: kebab-case, max 64 chars, lowercase + numbers + hyphens, must match directory name
- `description`: describe what AND when — all "when to use" info goes here, NOT in the body

**Body:** Markdown instructions. Keep under 500 lines. Use imperative form. Only include info Claude doesn't already know. Prefer examples over verbose explanations.

### Key principles

- **Concise is key** — context window is shared. Challenge every paragraph: "Does Claude need this?"
- **Progressive disclosure** — metadata always loaded (~100 tokens), SKILL.md body on trigger (<5k tokens), references on-demand
- **Degrees of freedom** — high (text) for flexible tasks, low (scripts) for fragile operations
- **No auxiliary docs** — do NOT create README.md, CHANGELOG.md, or any extra documentation files
- **No duplication** — info lives in SKILL.md OR references, never both
- **References one level deep** — all reference files link directly from SKILL.md

### Reference file guidelines

- If SKILL.md approaches 500 lines, split details into `references/` files
- For files >10k words, include grep patterns in SKILL.md
- Organize by domain or variant (e.g., `references/aws.md`, `references/gcp.md`)
