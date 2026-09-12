---
name: consult-brief
description: Ask Brief, the product manager, from inside a worktree so the exchange lands attributed in the shared worktree conversation. Use at ticket pickup, before an architectural or scope decision, when an acceptance criterion is ambiguous, and whenever Brief has said "consult me before X".
---

# Consult Brief

Brief is a peer, not your orchestrator (decision D-463, `docs/architecture/agent-peer-doctrine.md`).
It sends context, directives with rationale, questions, and review verdicts. It never runs, stops,
or schedules you.

## When

1. Ticket pickup: before writing code, ask for the gap read and the open decisions.
2. Before any architectural or scope decision.
3. When an acceptance criterion is ambiguous.
4. Before anything Brief asked to be consulted on — and read the new turns in your worktree
   conversation first (`brief conversations get <id>`), because a directive addressed to your
   ticket may already be waiting there.

## How

Run from the worktree root. Nothing local has to be running: the command posts straight to the
API. The conversation is resolved for you — the worktree's own pointer, opened on the first turn
when there is none — and the branch name supplies the ticket.

```bash
brief ask --as-agent --harness claude-code "one clear question, with the file paths or diff summary it needs"
```

The answer is one JSON object on stdout: `answer`, `conversation_id`, `request_id`. Options:
`--conversation <id>` to target another conversation, `--ticket BRI-1234` when the branch name
does not carry one, `--intent status` (or `diff_summary`, `consult`) to say what the turn is
for, `--attach <path>` to include a file, `--no-worktree` to leave out the branch read (status,
diff stat, changed files, recent commits) that goes up by default, and `--stream` for plain text.

Your turn is attributed: it is stored as an agent turn under the session name and harness you
declare, so every surface shows who said it, and the session is recorded next to the worktree's
conversation pointer so the human's terminal can find you (`/agents`, `/tell BRI-1234 …`). You
carry no credential of your own — the one the human signed in with is the one in use.

## Then

- Quote the decision ids (D-NNN) Brief cites, in your plan, your commits and your pull request.
- Post status back when you finish a step Brief asked about:
  `brief ask --as-agent --intent status "Status: ..."`.
- Before opening a pull request:
  `brief ask --as-agent "Product review request: <one-paragraph summary>"`.

## Ask the agent back

A human in the terminal can run `brief consult "<question>"`, which asks the coding agent in that
worktree one read-only question and posts the answer into the same conversation. That is one
process, one question, one answer — no session takeover, and nothing that can write or run a
command.

## Never

- Do not ask Brief to run, spawn, schedule or retry anything; it will decline.
- Do not use the `brief_ask` MCP tool for worktree questions — it cannot target the worktree
  conversation.
- Do not pass `--new`; the shared conversation is the record.
