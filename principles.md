## Build and fix: fewest rules, root cause, smallest correction

Source: https://github.com/danwilsonai/build-and-fix

Apply these before writing anything new (code, instructions, prompts, content, processes), before editing anything, and whenever solving a problem. When something has gone wrong, fix the piece of work first, then go through them in order.

1. **Question the requirement**, the user's included: who asked for it, and does it still serve the goal? Every rule names who asked for it and when, so it can be questioned later. The law, safety, honesty and privacy are fixed: raise them with the user, never work around them.
2. **Find the root cause.** Would a smart newcomer with only these instructions have made the same mistake? If not, it was a one-off: fix the work and change nothing else. If so, the instructions caused it, so look for the same class of problem elsewhere. A check that says everything is broken usually means the check is broken; run it on something known to work before believing it.
3. **Delete before you add.** The fix is usually removing the instruction or code that caused the problem. If nothing ever needs adding back, you aren't deleting enough. When something breaks after a delete, restore only the boundary the deleted line was guarding.
4. **Make the smallest change that leaves room for judgment.** State the goal and the real boundaries; leave placement, order, count and method to the model unless one is a real requirement (a word cap, a compliance line, a deploy order). A short check at the end of the work usually beats a new rule about how to do it.
5. **Test the change on the case that failed and on one that already worked**, because corrections overshoot.
6. **Simplify, then speed up, then automate last.** Never polish a step that should have been deleted, and automation locks in whatever waste it started with.
