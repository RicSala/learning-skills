---
name: capture
description: >-
  Use when the user wants to capture, save, or document something they learned
  while coding (e.g. "save this learning", "I want to remember this",
  "/learning:capture"). Also offer it PROACTIVELY when the user has a learning
  moment — phrases like "oh, I didn't know that", "TIL", "so THAT's how it
  works", "huh, so that was the problem?", or after a conversation explains a
  concept the user was missing. Saves a standalone learning note into a single
  central folder so notes are never scattered across projects again.
---

# Capture Learning

Save things the user learns while coding into ONE central folder, so learnings
are never spread across individual project repos again.

The goal is to capture **fundamental knowledge** — how things actually work —
not just a runbook of steps. See "What a learning is" below.

**Write at the depth of a good technical book chapter, not a wiki page.**
The user is saving this so they can re-learn the topic cold months from now
without re-having the original conversation. That means the document must
*teach*, not *remind*. Explain mechanisms thoroughly. Build the mental model
from first principles. Include the misunderstandings the user worked through
on the way to the insight, not just the final answer. Length is a *result* of
covering the material properly, not a goal — but if a document comes out short
you have almost certainly under-explained.

## Where learnings live

Everything goes in **`~/Desktop/Learnings/`** — one Markdown file per
independent learning, plus a `README.md` index.

Always run this first so the folder exists:

```bash
mkdir -p ~/Desktop/Learnings
```

## What a learning is

A learning document explains **fundamentals the user did not understand before
the conversation and now does**. It is *not* a runbook or a list of steps to
repeat.

- A learning can come from an error — but it does not have to. The user often
  learns how something works simply through the course of a conversation.
- **Errors are optional.** If an error did prompt the learning, capture what we
  were doing and the actual error message — but the document should be framed
  around the underlying knowledge, not the error.
- Summarize **everything** the user learned about the topic during the
  conversation — every concept, mental model, and "aha" — written up nicely
  with proper explanations.
- Include **related topics** the user should also know. Connected knowledge
  aids retention, so link the new learning to the wider picture.

## Workflow

1. **Check for duplicates.** List `~/Desktop/Learnings/` and look for a file on
   the same topic. If one already exists, **update it** instead of creating a
   duplicate.
2. **Draft the learning** using the template below.
3. **Show the draft to the user and confirm before writing.** The user is the
   one who has to learn from it — let them correct anything inaccurate, missing,
   or unclear first.
4. **Write the file** as `~/Desktop/Learnings/YYYY-MM-DD-short-descriptive-title.md`
   (today's real date, kebab-case title).
5. **Update the index** `~/Desktop/Learnings/README.md` (see below).
6. **Tell the user how to open it in Cursor.** Always finish your reply with a
   ready-to-paste command (one per file written or updated) so the user can
   jump straight into the document and review/edit it:

   ```bash
   cursor ~/Desktop/Learnings/YYYY-MM-DD-short-descriptive-title.md
   ```

   If multiple learnings were captured in one session, list one `cursor ...`
   command per file. Use the literal `~` path so it works from any cwd.
   Don't open the file automatically — just give the user the command.

When triggering proactively (the user had a learning moment but didn't ask to
save it), **ask first** — don't write a file unprompted.

## Core principles

- **Teach the fundamentals at book depth.** Each major idea gets a proper
  treatment: what the thing is, why it exists, the precise mechanism by which
  it works, a worked example, and the failure modes. Aim for the depth of a
  well-written technical book chapter or a senior engineer's blog post — the
  kind of write-up the user would *bookmark*, not just skim. Build up from
  primitives; do not assume the reader already groks the surrounding ideas.
- **Standalone.** The user will NOT remember the context later. The document
  must explain everything from scratch — including jargon, background
  technologies, and any prior knowledge the original conversation took for
  granted. Never write "as we discussed" or "from earlier"; the document IS
  the only memory.
- **Capture the whole topic.** Write up everything the user learned about this
  topic during the conversation, plus closely related concepts the agent
  thinks are worth knowing. Include the misconceptions the user held on the
  way to understanding — the wrong mental model is often *the most useful
  thing to record*, because they will likely fall into it again.
- **Mechanism over outcome.** Don't just say "X causes Y" — explain *how*.
  Walk through the steps of the process. If there's a data structure or
  algorithm or protocol involved, describe it. If multiple components
  interact, describe the interaction in order.
- **Show real code, real paths, real errors.** Use the actual file paths,
  package names, version numbers, and command outputs from the conversation
  where possible. Specifics are more memorable than abstractions. If an error
  was involved, paste the literal error text.
- **Use worked examples.** Pick a concrete scenario (often the one from the
  conversation) and trace through it step by step. Abstractions land harder
  when they're grounded in a specific case the reader can simulate in their
  head.
- **Match the language** of the conversation in which the learning happened.
- **ASCII diagrams when they help.** Not mandatory — but if a diagram makes a
  relationship, flow, or structure clearer, include one. Place it inline, right
  next to the explanation it supports — never in a separate section. Don't be
  shy about including several diagrams in one document if the topic has
  several distinct shapes (a pipeline, a tree, a table, a state machine).
- **Capture the explanations the user asked for.** The Q&A section is not
  decorative — it is the record of which specific questions tripped the user
  up. If something needed to be re-explained before it clicked, that
  re-explanation belongs in the document.
- **Cover the surrounding ecosystem.** A good learning on, say, "pnpm peer
  cascades" should also surface how npm and yarn behave differently, what the
  related config knobs are, what the analogous bugs look like in other
  bundlers, and how to detect this class of problem in general. Connected
  knowledge sticks; isolated facts do not.
- **One learning per file.** Even if topics are related, keep them in
  separate files. Cross-link via the Related Topics section.
- **Depth, not padding.** Long because the topic is dense, not long because
  you're repeating yourself in different words. Every paragraph should add a
  fact, a mechanism, an example, or a connection. Cut filler ruthlessly. If
  a sentence could be deleted without losing information, delete it.

## File template

The template below is a *minimum* skeleton. Real learnings expand it: split
"What I Learned" into multiple `###` subsections (one per sub-mechanism),
add a worked example, a "Common misconceptions" section if relevant, a
"How to detect this" section if relevant, a "Comparison with X" section
when adjacent ecosystems are illuminating, etc. The template is a starting
point, not a cap.

````markdown
---
title: <Concise descriptive title>
date: <YYYY-MM-DD>
topic: <Broad area — e.g. React, Docker, Git, Postgres>
tags: [<keyword>, <keyword>, <keyword>]
project: <Name or path of the project where this came up>
---

# <Title>

## Context
What we were building or trying to do, with enough background that this makes
sense read cold months from now. If an error or problem prompted the learning,
describe what was going on and include the actual error message here — but the
learning does not depend on there having been an error.

Include enough detail that the reader can reconstruct what the codebase looked
like at the time: what was being built, what stack, which file paths and
package names were involved, what specific configuration was in play.

## What I Learned
The core of the document, expanded into several `###` sub-sections — one per
distinct sub-idea. Each sub-section should:
  - Open with a clear claim or definition.
  - Explain the mechanism in detail. If steps are involved, number them.
  - Include real code, real paths, real outputs.
  - Where helpful, add an ASCII diagram (inline).
  - Connect to the larger picture: how does this piece fit with the others?

Where useful, include:
  - **A worked example** that traces through a concrete scenario step by step.
  - **A "common misconceptions" sub-section** capturing the wrong mental
    models the user held on the way to understanding — these are often the
    most valuable thing to record.
  - **Edge cases and limits** — when does this stop being true?

```<lang>
// illustrative code with real names and paths from the conversation
```

## Why It Works
The deeper reason — what happens under the hood, and the principles that make
the explanations above hold. This is the "Sediment vs. behaviour" section:
behaviour is what you observe, sediment is the design decisions, history, and
constraints that produced that behaviour. Cover the sediment.

If there are trade-offs the designers made (caching for performance vs.
correctness, isolation vs. ergonomics, etc.), describe both sides honestly so
the reader understands *why* the system is the way it is and not just *that*
it is that way.

## How to detect this in the future
(Include this section whenever the learning is about a class of bug or
trap. A one-liner shell command, a config check, a code-review heuristic —
whatever a future-you would actually use to spot the same shape of problem.)

## Related Topics
Connected concepts worth knowing — adjacent ideas that came up, or that the
agent thinks tie into this. For each one:
  - Name it
  - Say in 1-3 sentences how it relates
  - Optionally, link to another learning if one exists

Cover both:
  - **Topics from this conversation** that didn't make it into the main body.
  - **Adjacent ecosystem topics** — how do npm/yarn/Vite/webpack handle this?
    What's the React/Vue/Svelte equivalent? Is there a Postgres analogue?

## Q&A
Capture the questions the user actually asked during the conversation, and the
explanations that finally made the topic click. These are often the *real*
content of the learning — written more conversationally and concretely than
the main body. Don't paraphrase the user's questions into generic FAQ format;
keep them specific.

**Q: <a specific question the user asked, or one likely to come up later>**
A: <the explanation — full paragraphs are fine; this is not Twitter>

**Q: ...**
A: ...
````

## Index (README.md)

Keep `~/Desktop/Learnings/README.md` as a browsable index. After adding or
updating a learning, ensure it has a row in the table:

```markdown
# Learnings

A central index of everything learned while coding.

| Date | Learning | Topic | Tags |
|------|----------|-------|------|
| 2026-05-19 | [How React closures capture state](./2026-05-19-react-closures-capture-state.md) | React | hooks, closures |
```

If `README.md` doesn't exist yet, create it with this header and table. Keep
rows sorted newest-first.
