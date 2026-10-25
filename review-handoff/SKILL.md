---
name: review-handoff
description: Hand finished code changes to the user for review with a short review plan, key diff excerpts, and inline Hunk comments when a Hunk session is open. Use when handing finished work to the user for review, or when the user asks for a review plan. Not for reports between agents.
---

# Review Handoff

The user reviews the code; the review plan only orients them. Write plainly, no jargon, and pick the smallest view that makes each point clear.

## Review plan

- **Why**: one sentence.
- **Shape**: one compact view of what changed (a file tree with one-line responsibilities, a call tree, pseudocode, or a type), as a `diff` block when an existing shape changed. Optional: skip it when the change is small enough to read directly.
- **Review order**: the general reading path through the change, one stop per logical change, `path:line`: what to check there. The reasoning goes in the Hunk comment, or under the line when Hunk is unavailable.
- **Watch out**: 1-3 bullets for surprises, risks, or deliberate omissions not tied to one line of code. `None.` when there are none.
- **Key diff excerpts**: the lines where a bug could hide (edge cases, data loss, contracts, surprising decisions), not repeated from Watch out, each with its file, line, and reasoning. Write `None.` when there are none.

## Review in Hunk

If the `hunk-review` skill is available, or `hunk skill show` runs, put the review order and the key diff excerpts into Hunk as inline comments, like a GitHub PR review:

1. Run `hunk session list`. If no session exists for this repo, ask the user to open `hunk diff` in another terminal. If they decline, use the fallback below.
2. Follow the `hunk-review` skill (or the `hunk skill show` output). Add at most one comment per review stop or key diff excerpt, and skip the ones the code explains. More comments than changed lines of code is a red flag. Order the batch by review order and send it in one `hunk session comment apply --focus` call. The summary is the one-liner; the rationale is 1-3 plain sentences.
3. In the terminal, start the review plan with one line saying the review comments are in Hunk. The review order stays as its one-liners, and each key diff excerpt shrinks to `path:line`: why it needs attention. This is the user's starting point; the reasoning lives in the Hunk comment. Stops without a comment keep only their one-liner.

If Hunk is unavailable or no session is open, tell the user that Hunk review is unavailable, add the 1-3 sentence rationale under each review-order line, and give the key diff excerpts in full in the terminal.
