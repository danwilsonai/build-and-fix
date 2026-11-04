# Install (instructions for Claude)

The user asked you to install these principles. Before you change anything, tell them in a few lines what you're about to do (the three parts below, and that nothing gets cut without their approval) and wait for them to say go.

**1. Add the principles.** Copy `principles.md` from this repo, unchanged (download the exact text from https://raw.githubusercontent.com/danwilsonai/build-and-fix/main/principles.md, for example with `curl`, because web fetch tools may return a summary instead), into the user's `~/.claude/CLAUDE.md` so it applies in every project (create the file if it doesn't exist; use a project's `CLAUDE.md` instead if the user asked for one project). Append it and leave the rest of the file alone. If a section with the same heading is already there, replace that section, since this is an update. Add today's date after the source link.

If the user is on claude.ai rather than Claude Code, there is no CLAUDE.md: give them the text of `principles.md` to paste into their profile preferences or a project's instructions, and stop there.

**2. Measure what loads every session.** Find everything Claude Code reads into context at the start of a session here (every CLAUDE.md in scope and the files they import, rules files without a `paths:` filter, the memory index, skill and agent descriptions) and estimate the tokens each one costs (about 4 characters per token; say it's an estimate, and mention that `/context` gives the exact figure). Show the user the total and the biggest files, including what the principles you just added cost.

**3. Cut it back and structure it well.** Go through the user's setup the way the principles say: what loads every session, then their other rules, skills, agents, prompts and automations, then the repo you're working in. Look for:

- instructions that no longer serve a goal, duplicate or contradict each other, dictate method where only the goal matters, or patch an old mistake that deleting something would have fixed
- content that is only needed for some tasks but loads every session; it belongs somewhere that loads on demand (a path-scoped rule, a skill, or a file the CLAUDE.md points to), and each fact should live in one place with pointers to it
- scheduled and background agent runs (cron jobs, CI, scripts calling `claude -p` or the SDK) that load the whole interactive setup, meaning every CLAUDE.md, rule, memory file and tool server, on every turn when the job needs none of it. Usually the biggest saving there is, because it's paid on every turn of every run. With the Claude Code CLI, `--setting-sources ""` and `--strict-mcp-config` drop that preamble; the job's prompt then has to carry everything it needs, and the tools it uses have to be declared explicitly. Check `claude --help` for the user's version, and run the job once before and after to confirm the output doesn't change
- steps in an automation whose output nobody uses; delete them rather than make them cheaper

Show the user what you'd delete, move or simplify and why, with the token saving for each, and change nothing until they approve. Never remove a safety, security, legal or compliance instruction unless the user explicitly says to. When moving content, write it to its new home before removing it from the old one, so a failed write never loses anything. After applying what they approved, measure again and show the before and after: tokens loaded every session, and how much was saved.
