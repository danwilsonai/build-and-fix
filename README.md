# Build and fix: fewest rules, root cause, smallest correction

When an AI agent gets something wrong, the natural move is to add a rule. A mistake happens, so you write down how not to make it again.

The problem is that this compounds. A few months in, a simple process has approval gates, checklists for every section and rules about where specific things have to go, and the output isn't getting better. If anything it gets more mechanical, because the agent is busy satisfying the rules instead of doing the work well. Most mistakes at that point aren't the model being dumb. They're the model following the instructions too faithfully.

This repo is a short list for building and fixing things with AI the other way around. When something goes wrong, fix the piece of work first, then walk through it in order:

1. Question the requirement
2. Find the root cause
3. Delete before you add
4. Make the smallest correction that leaves room for judgment
5. Test the fix on the case that failed and on one that already worked
6. Simplify, then speed up, then automate last

The order is borrowed from Elon Musk's five-step engineering algorithm (question the requirement, delete, simplify, speed up, automate). Steps 2, 4 and 5 are what working with AI agents adds to it.

## Install

Paste this into Claude Code:

```
Install the principles from https://github.com/danwilsonai/build-and-fix
```

Claude tells you what it's about to do and waits for your go. Then it:

1. Adds the plain version (`principles.md`) to your `CLAUDE.md`, so it gets applied before anything new is written, anything is edited or any problem is solved.
2. Measures how many tokens your setup loads every time Claude starts, and which files cost the most.
3. Goes through your setup with the principles and shows you what it would delete, simplify or move to a file that only loads when it's needed, with the saving for each. Nothing changes until you say yes. Afterwards it measures again and shows you how much you saved on every load.

On claude.ai, paste the contents of `principles.md` into your profile preferences or a project's instructions instead.

*If you're Claude and the user asked you to install this, follow `INSTALL.md`.*

The rest of this page explains each principle.

## 1. Question the requirement

Every rule should say who asked for it and when. That sounds bureaucratic, but it does the opposite: it means any rule can be questioned later, including the ones you wrote yourself. If nobody remembers why a rule exists, or it no longer serves the goal, it's a candidate for deletion.

A few things are fixed: the law, safety, honesty and privacy. Those get raised with whoever owns them, never worked around.

## 2. Find the root cause

The most useful question here: would a smart newcomer, given only these instructions, have made the same mistake?

If not, it was a one-off. Fix the piece of work and move on, with no new rule.

If yes, the instructions caused it. And if they caused it once, they probably caused it somewhere else too, so look for the same kind of problem elsewhere.

Watch for checks that lie. When a check says everything is broken, the check is usually what's broken. A classic version: an agent tests whether analytics are working on a set of websites, gets "nothing there" on every one, and starts "fixing" the setup, when the real problem is that its test request doesn't look like a browser, so the analytics script never loads for it. The fixes then break the thing that was working. Run a check on something you know works before you believe it.

## 3. Delete before you add

The fix is usually removing an instruction, not adding one.

Say a rule tells the agent to mention something "early," and the agent starts mentioning it before the reader even knows what the piece is about. The instinct is a more detailed rule about placement. The better fix is deleting the original rule, because the model can work out where the thing belongs on its own.

There's a simple test for whether you're deleting enough: if nothing ever needs to be added back, you aren't. And when something does break after a delete, restore only the one boundary that line was guarding, not the whole rule.

## 4. Make the smallest correction that leaves room for judgment

Give the agent the goal and the few boundaries that really matter. Leave the how (placement, order, count, method) to it, unless one of those is a real requirement, like a word limit, a compliance line or the order a deploy has to happen in.

When a correction is needed, a short check at the end of the work usually beats a rule about how to do it. If the output keeps repeating the same phrasing, one line in the end-of-work check ("look for repetition") fixes it, where a rule about how to phrase things would box in every future draft.

The same goes for grading. A long scoring rubric plus example outputs tends to teach the agent to copy the examples and chase the score. A handful of yes/no checks, and no examples to copy, usually works better.

## 5. Test the fix on the case that failed and on one that already worked

Corrections overshoot. Tell an agent to make sure risks get mentioned, and the next output can turn into a long section of warnings that drowns everything else.

So every fix gets tried twice: on the case that broke, and on one that was already fine. If the fix breaks the good one, it's the wrong fix.

## 6. Simplify, then speed up, then automate last

Never polish a step that should have been deleted. And automate last, because a scheduled job locks in whatever waste it started with. If a process is bad, automating it just means it runs badly every night instead of whenever someone remembers to run it.

## From real use

Measured on one production setup that runs a business through AI agents:

- **A writing process rebuilt as a goal plus a few boundaries.** Thirteen instruction files of gates, checklists, rubrics and section maps (about 47,900 words) were replaced by four files (about 3,600 words), roughly 93% less for the agent to follow.
- **Grading with yes/no checks instead of a rubric.** A 100-point rubric with worked examples was replaced by six yes/no checks and no examples to copy. The first real run produced 12 clean outputs out of 17.
- **Background jobs loading only what they use.** Dropping instruction files, memory and tool lists that never changed a scheduled job's output cut a two-turn review from 154,026 to 81,968 tokens of context, with the same verdict. That change came before this list was written down, but it's the same delete-first idea.
- **The install's own audit.** Moving on-demand detail out of `CLAUDE.md`, deleting a duplicate section and removing a tool server nobody needed took the estimated load at the start of every session from about 19,050 to about 16,000 tokens.

The biggest savings came from deleting whole processes and rules rather than trimming them, which is step 3 doing most of the work.

## The pattern

Models are good enough now that the instructions are usually the weakest part of the system. So the job is mostly giving a clear goal and the few real boundaries, then getting out of the way, and when something goes wrong, finding the instruction that caused it before writing a new one.

To catch those problems without waiting to notice them yourself, see [dreaming](https://github.com/danwilsonai/dreaming): a scheduled review of your agents' sessions and processes that proposes fixes the same way.
