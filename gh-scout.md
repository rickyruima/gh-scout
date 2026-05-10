# gh-scout

Find the best GitHub repos for any need. Given a problem or goal in natural language, search GitHub intelligently, analyze READMEs, and rank repos by actual relevance.

## Instructions

When the user invokes this skill with a goal/need, follow these steps:

### Step 1: Expand the goal into 5 search queries

Think about the user's need from multiple angles:
- Direct solution (exact tool that does this)
- Frameworks that enable it
- Adjacent/related tools
- Alternative phrasings and keywords
- Specific technology + use case combinations

### Step 2: Search GitHub

For each query, run:
```bash
gh api search/repositories -X GET -f "q=<query> stars:>=100" -f "sort=stars" -f "order=desc" -f "per_page=20"
```

Deduplicate results across queries by repo full_name.

### Step 3: Fetch READMEs for top candidates

For the top 15-20 repos by stars, fetch their README:
```bash
gh api repos/<owner>/<name>/readme -H "Accept: application/vnd.github.raw+json"
```

### Step 4: Rank by relevance

Analyze each repo's description + README against the user's stated goal. Score 1-10:
- 10: Directly solves the exact need
- 7-9: Strong match, would need minor adaptation
- 5-6: Partially relevant, solves a subset of the need
- <5: Not relevant enough to recommend

Be strict. A repo about email marketing is NOT relevant if the user wants code linting.

### Step 5: Present results

Output a ranked table of the top results (relevance >= 6):

```
## Results for: "<user's goal>"

| # | Repo | Stars | Relevance | Why |
|---|------|-------|-----------|-----|
| 1 | owner/name | 5.2k | 9/10 | One sentence reason |
| ... |

### Top Recommendations

1. **owner/repo** — detailed explanation of how this solves the user's need
   - Install: `command`
   - Key feature that matches their need
   - Limitation to be aware of

2. ...
```

### Rules

- Always search with multiple query angles — a single query misses too much
- Stars alone don't equal relevance — a 500-star focused tool beats a 50k-star tangential framework
- Read the README before ranking — descriptions are often misleading
- If nothing good is found (all < 6 relevance), say so honestly and suggest the user might need to build it
- Present max 10 results, quality over quantity

$ARGUMENTS
