---
allowed-tools: Bash, Read, Agent
description: "Use when the user wants to find existing GitHub repos, tools, libraries, or solutions for a problem. Triggers on: 'find me a tool', 'is there a repo for', 'what's the best library for', 'search GitHub for', 'any open source solution for', or any request to discover existing software/tools/repos that solve a problem."
---

# gh-scout: Find the best GitHub repos for any need

When the user describes a need, problem, or goal, find the most relevant GitHub repos that solve it.

## Process

### Step 1: Expand into 5 search queries

Think about the user's need from multiple angles:
- Direct solution (exact tool name or category)
- Frameworks/libraries that enable it
- Adjacent tools in the same ecosystem
- Alternative phrasings (what would someone name this tool?)
- Technology-specific terms (e.g., "golang CLI" or "python library")

### Step 2: Search GitHub

For each query, run:
```bash
gh api search/repositories -X GET -f "q=<query> stars:>=100" -f "sort=stars" -f "order=desc" -f "per_page=20"
```

Collect and deduplicate results by `full_name`.

### Step 3: Fetch READMEs for top 15 candidates (by stars)

```bash
gh api repos/<owner>/<name>/readme -H "Accept: application/vnd.github.raw+json"
```

Read the first 2000 characters to understand what each repo actually does.

### Step 4: Rank by relevance (be strict)

Score each repo 1-10 against the user's specific need:
- **10:** Directly solves the exact need, ready to use
- **8-9:** Strong match, may need minor config/adaptation
- **6-7:** Partially relevant, solves a subset
- **< 6:** Not relevant enough — exclude

**Be strict.** A popular repo that's tangentially related is NOT a good result. Quality > quantity.

### Step 5: Present results

Output format:

```
## GitHub Scout: "<user's goal>"

| # | Repo | ⭐ | Relevance | Why |
|---|------|-----|-----------|-----|
| 1 | owner/name | 12.3k | 9/10 | Direct solution — does exactly X |
| 2 | ... |

### Recommendations

**Best match: [owner/repo](url)**
- What it does and why it fits
- How to install/use
- Any limitations

**Also worth considering: [owner/repo2](url)**
- ...
```

### Rules

- Search with multiple query angles — a single query misses too much
- Stars ≠ relevance. A 500⭐ focused tool > 50k⭐ tangential framework
- Read the README before ranking — titles/descriptions are often misleading
- If nothing good exists (all < 6), say so honestly and suggest building it
- Max 10 results, ranked by relevance (not stars)
- Include install commands when available

$ARGUMENTS
