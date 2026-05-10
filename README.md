# gh-scout

> Find the best GitHub repo for any need — a Claude Code skill.

Given a problem or goal in natural language, searches GitHub from multiple angles, reads READMEs, and ranks repos by actual relevance.

## Install

Copy to your Claude Code commands directory:

```bash
cp gh-scout.md ~/.claude/commands/
```

## Usage

```
/gh-scout promote my open source developer tool
/gh-scout automate iOS App Store screenshots
/gh-scout self-hosted alternative to Datadog
/gh-scout parse terraform plans in CI pipelines
```

## How it works

1. Expands your goal into 5 search queries (different angles)
2. Searches GitHub via `gh` CLI
3. Fetches READMEs for top candidates
4. Ranks by relevance to your specific need (not just stars)
5. Presents actionable recommendations

## Requirements

- [Claude Code](https://claude.ai/claude-code) CLI
- `gh` CLI (authenticated)

## License

MIT
