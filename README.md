# How I build and fix things with AI

I run a lot of my business through an AI assistant called Henry. It's Claude Code running on a small server, and it drafts scripts, checks facts, runs the email, watches the websites and handles a long list of other things (I still make the calls, but the amount of work it does is a little ridiculous).

For the first few months, every time Henry got something wrong, we added a rule. That seemed logical: a mistake happens, so you write down how not to make it again.

The problem is that this compounds. A few months in, the YouTube script process alone had approval gates, structure maps, checklists for each section and rules about where specific facts had to go. And the scripts weren't getting better. If anything they were getting more mechanical, because the AI was busy satisfying the rules instead of writing a good script.

So we flipped the approach. Below is the list we use now, in order. When something goes wrong, we fix the piece of work first, then walk through it.

The short version:

1. Question the requirement
2. Find the root cause
3. Delete before you add
4. Make the smallest correction that leaves room for judgment
5. Test the fix on the case that failed and on one that already worked
6. Simplify, then speed up, then automate last

The order is borrowed from Elon Musk's five-step engineering algorithm (question the requirement, delete, simplify, speed up, automate). Steps 2, 4 and 5 are the parts we had to learn the hard way with AI.

## Install

Paste this into Claude Code:

```
Install the principles from https://github.com/danwilsonai/build-and-fix
```

Claude tells you what it's about to do and waits for your go. Then it:

1. Adds the plain version (`principles.md`, no stories) to your `CLAUDE.md`, so it gets applied before anything new is written, anything is edited or any problem is solved.
2. Measures how many tokens your setup loads every time Claude starts, and which files cost the most.
3. Goes through your setup with the principles and shows you what it would delete, simplify or move to a file that only loads when it's needed, with the saving for each. Nothing changes until you say yes. Afterwards it measures again and shows you how much you saved on every load.

On claude.ai, paste the contents of `principles.md` into your profile preferences or a project's instructions instead.

*If you're Claude and the user asked you to install this, follow `INSTALL.md`.*

The rest of this page is the story behind each principle.

## 1. Question the requirement

Every rule in Henry's instructions says who asked for it and when. That sounds bureaucratic, but it actually does the opposite: it means any rule can be questioned later, mine included. If nobody remembers why a rule exists, or it doesn't serve the goal anymore, it's a candidate for deletion.

A few things are fixed: the law, compliance, honesty and privacy. Those get raised with me, never worked around.

## 2. Find the root cause

There's one question I've found most useful here: would a smart newcomer, given only our instructions, have made the same mistake?

If not, it was a one-off. Fix the piece of work and move on, no new rule.

If yes, the instructions caused it. And if they caused it once, they probably caused it somewhere else too, so go look for the same kind of problem elsewhere.

My favorite example of skipping this step: Henry checked whether the analytics on my websites were working, got "nothing there" on all six sites, concluded the setup was broken and started fixing it. It turned out the check itself was blind (Cloudflare only adds the analytics script for requests that look like a real browser, and Henry's check didn't). One of the "fixes" switched off the part that actually collects the data. We created the outage we thought we were repairing.

What I took from that is that when a check says everything is broken, the check is usually what's broken. Run it on something you know works before you believe it.

## 3. Delete before you add

This is the one that surprised me most. The fix is usually removing an instruction, not adding one.

One of my video scripts introduced a fact about how my business works before the viewer even knew what the video was about. Why? Because a rule said to state it "early." Henry's first instinct was to fix that with a more detailed rule about placement. What I told it was: "you're making too many rules... AI is smart these days - it can figure out where to best put the disclosure."

The same day, we threw out the entire script process and replaced it with a goal, a word count and a couple of hard boundaries. The outline for that video had spent four of its six sections on something other than the channel's main topic, because the old rules kept pushing the main topic to the back.

There's a simple test for whether you're deleting enough: if nothing ever needs to be added back, you aren't. And when something does break after a delete, restore only the one boundary that line was guarding, not the whole rule.

## 4. Make the smallest correction that leaves room for judgment

Give the AI the goal and the few boundaries that really matter. Leave the how (placement, order, count, method) to it, unless one of those is a real requirement like a word limit or the order a deploy has to happen in.

When a correction is needed, a short check at the end usually beats a rule about how to do the work. One script used the same kind of stat phrasing over and over ("3 out of 4," "7 in 10"). The old us would have written a rule about how to phrase statistics. Instead we added one line to the end-of-draft check: look for repetition. That was the whole fix.

Same idea with reviewing. We used to grade video hooks on a 100-point rubric, and the writer got sample hooks to learn from. The writer copied the samples, and the rubric rewarded hooks that sounded clever but didn't say much. We replaced it with six yes/no checks and deleted the samples, and the first real run produced 12 clean hooks out of 17.

## 5. Test the fix on the case that failed and on one that already worked

Corrections overshoot. We had a rule making sure risk got mentioned in my videos about investing, which is the right goal. The next video I filmed had a ten-part section on what can go wrong, plus three earlier lines announcing that it was coming. When I filmed it, it felt like way too much.

So now every fix gets tried twice: on the case that broke, and on one that was already fine. If the fix breaks the good one, it's the wrong fix.

## 6. Simplify, then speed up, then automate last

Never polish a step that should have been deleted. And automate last, because a scheduled job locks in whatever waste it started with. If a process is bad, automating it just means it runs badly every night instead of whenever you remember to do it.

## The pattern

Looking back over the last few months, I think most of our mistakes weren't the AI being dumb. They were the AI following my instructions too faithfully. Models are good enough now that the instructions are usually the weakest part of the system, so the job is mostly giving a clear goal and the few real boundaries, then getting out of the way.

These principles live in Henry's main instructions file. This repo is the public copy, and I update it when they change.
