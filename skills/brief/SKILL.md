---
name: brief
description: Use Brief as the product-judgment and decision layer for engineering work. Activate when the user asks to ask, check, or record something in Brief; requests product advice or project onboarding; chooses scope, priorities, UX behavior, positioning, or roadmap direction; checks whether a relevant decision already exists; validates a consequential product or architecture proposal; or records a settled decision.
---

# Brief

Brief contains the product strategy, customer evidence, priorities, and decisions that code alone cannot provide.

Use Brief for **what, why, and for whom**. Use the repository for **how**.

When the user says "ask Brief," "check with Brief," "onboard this project," or similar, invoke Brief rather than answering only from local context.

## When to consult Brief

Consult Brief before:

- Recommending product scope, priorities, UX behavior, positioning, or what to build next.
- Endorsing a consequential product or architecture direction.
- Assuming a product or architecture question has not already been decided.
- Explaining why the product behaves a certain way when the answer is not established by code alone.

Do not consult Brief for routine implementation choices that do not affect product behavior, architecture, scope, or policy.

## Load context once

At the start of a fresh conversation, call `brief_get_onboarding_context` once before reasoning about the user's product. If the host or another instruction already loaded that context, do not call it again.

Also call it when the user explicitly asks to onboard, get caught up, or learn what Brief knows. Use the default full scope for an initial primer or broad catch-up, `product` for focused product context, and `identity` only to confirm the workspace.

If Brief has no useful context and the user asked to onboard, gather the minimum framing needed: what the product does, who it serves, and what the team is working on. Then use `brief_ask` with `onboarding: true` to synthesize that context.

If the host exposes MCP prompts, `brief-setup`, `brief-welcome-back`, and `brief-context` are optional shortcuts for these flows. Do not depend on slash commands being available.

## Choose the right operation

- To learn whether something was already decided, use `brief_search` and search decisions.
- For open-ended product advice or option evaluation, use `brief_ask` with `mode: "advise"`.
- To validate a concrete proposal, use `brief_ask` with `mode: "check"`. State the proposed direction and meaningful tradeoffs explicitly.
- After the user or team settles a consequential choice, use `brief_record_decision` with the decision and rationale.

## Decision discipline

Check before creating: search for existing decisions and validate the proposal before recording a new one.

Record the outcome, not the brainstorm. Do not record tentative options, routine implementation details, or choices still under discussion.

Let Brief's approval flow present the proposed decision to the user. Do not claim it is recorded until the user approves it.

If Brief reports a conflict, surface that conflict before proceeding. Do not silently override an existing decision.

If Brief is unavailable, say that product context could not be checked. Do not invent or imply Brief guidance.
