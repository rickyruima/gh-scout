# Promotional posts — gh-scout

Repo: https://github.com/rickyruima/gh-scout
Generated: 2026-05-27T05:06:50.849910+00:00

## twitter (270 chars)

Star count is a popularity contest, not a relevance signal. gh-scout takes your goal in plain English, runs 5 search angles, reads the READMEs, and ranks repos by actual fit. MIT, one-file install, lives in Claude Code. #ClaudeCode
https://github.com/rickyruima/gh-scout

## linkedin (1670 chars)

Ever searched GitHub for "rate limiter for Node" and gotten back a wall of repos sorted by stars — half of them abandoned, half solving a slightly different problem than yours?

That's the part I always found tedious. Star count tells you something was popular once. It doesn't tell you whether the thing fits what you're actually trying to build today.

I've been using gh-scout for this and figured it was worth sharing.

You describe your goal in plain English — something like "I need a library to parse and diff JSON config files in Python." Instead of running one literal search, it expands that into about 5 different search angles, pulls the candidates, and actually reads the READMEs before ranking them by how well they match what you described.

So the ordering is relevance to your problem, not popularity. A 300-star repo that does exactly what you need beats a 20k-star one that's close-but-not-quite.

A few things I like about how it's built:

- It's a native Claude Code skill. No separate service, no account, no API key to wrangle — it runs inside Claude Code.
- One-file install. Drop it into ~/.claude/commands/ and you're done.
- It's built on the official gh CLI, so it's using GitHub's own tooling underneath.
- MIT licensed.

It hasn't replaced my judgment — I still open the repos and read the code before committing to a dependency. But it's cut down the "open 15 tabs and skim" phase quite a bit, which is most of the annoyance.

If you live in Claude Code and find yourself hunting for libraries often, it's worth ten minutes to try.

Repo here: https://github.com/rickyruima/gh-scout

#ClaudeCode #DeveloperTools #OpenSource #GitHub #Python

## reddit (2280 chars)
**Title:** gh-scout: Claude Code skill — find the best GitHub repo for any need

I made a Claude Code skill that finds GitHub repos by what they do, not by stars

I kept hitting the same annoyance: I'd search GitHub for something like "rate limit middleware for FastAPI," get a wall of results sorted by stars, and the top hits would be huge frameworks that technically mention the keyword but aren't actually what I need. Meanwhile the 80-star repo that does exactly the thing is on page 3.

So I wrote `gh-scout`. It's a Claude Code skill (just a command file, no service to run).

You describe your goal in plain English. It then:

- expands that one goal into ~5 different search angles (because the way *you* phrase a problem is rarely the way the repo author tagged it)
- runs those searches through the official `gh` CLI
- actually reads the READMEs of the candidates
- ranks them by how well they fit what you described, not by star count

The README-reading part is what made the difference for me. Star count tells you a project is popular; it doesn't tell you whether it solves *your* problem. Reading the README before recommending catches the "this looks relevant but actually does something else" cases that keyword search alone misses.

I'm the author, so usual disclaimer applies — but it's MIT and it's one file, so you can read the whole thing in a couple minutes and decide for yourself.

**Details:**
- MIT licensed
- Install is dropping one file into `~/.claude/commands/`
- Built on the official `gh` CLI (so it uses your existing auth)
- Runs inside Claude Code

Repo: https://github.com/rickyruima/gh-scout

Honest about the limits: it's only as good as the `gh` search API underneath, and "reads the README" means the model reads it — so for niche stuff you should still sanity-check the picks. It's also obviously only useful if you already live in Claude Code. If you don't, this won't be for you.

Curious whether the multi-angle search actually helps for other people's queries or if it's just solving my own search habits. Feedback welcome, and happy to take issues/PRs.

**TL;DR:** Claude Code skill. Describe what you want in plain English → it searches GitHub from several angles, reads the READMEs, and ranks repos by fit instead of stars. MIT, one-file install, built on `gh`. I made it. https://github.com/rickyruima/gh-scout

## hackernews (2152 chars)
**Title:** Show HN: gh-scout – Claude Code skill — find the best GitHub repo for any need

Show HN: gh-scout – describe a goal in plain English, get GitHub repos ranked by fit

I kept running into the same problem with GitHub search: I'd type some keywords, get a wall of results sorted by stars, and the top hits were usually either abandoned "awesome-X" lists or popular projects that didn't actually do the thing I needed. Finding the right small library for a specific problem meant opening 15 tabs and reading READMEs by hand.

gh-scout is a Claude Code skill that does that reading for me. You describe what you're trying to do in a sentence, and it:

- expands your one goal into ~5 different search angles (because the words you'd use and the words the maintainer used are often not the same),
- runs those searches through the `gh` CLI,
- pulls and reads the READMEs of the candidates,
- and ranks them by how well they match your stated need rather than by star count.

The star-count thing was the main motivation. Stars correlate with age and marketing, not with whether a repo solves your problem. A 200-star library written last year is often a better fit than the 30k-star framework everyone links to, and keyword search buries it.

Some technical notes:

- It's a single Markdown file you drop into `~/.claude/commands/`. No server, no API key beyond what you already have, nothing running in the background.
- It shells out to the official `gh` CLI for search and content, so auth and rate limits are whatever you've already set up with GitHub.
- It runs entirely inside Claude Code — the model does the query expansion and the README reading/ranking, the skill just structures the workflow.
- MIT licensed.

It's deliberately small. There's no scoring model or embedding index — it leans on the LLM that's already in the loop to judge relevance, which is the part that was annoying to do manually anyway.

Repo: https://github.com/rickyruima/gh-scout

Curious whether other people hit the same star-ranking frustration, and how you currently work around it. Also interested if the multi-angle search expansion is actually pulling its weight or if a single good query would do as well — I haven't measured that rigorously yet.
