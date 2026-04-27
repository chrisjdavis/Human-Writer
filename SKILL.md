---
name: human-writing
description: >-
  Produces natural, human-sounding prose using Wikipedia's "Signs of AI
  writing" field guide. When this skill applies, the agent MUST fetch that
  Wikipedia URL first, treat the live page as authoritative for the session,
  update this skill on disk if the live page contains material not yet
  reflected here, then draft or revise text. Triggers: emails, articles, docs,
  marketing, comments, summaries, announcements, blog posts, wiki prose,
  reports, narratives, social copy, README prose, or any "write this up"
  deliverable—not pure code/config unless prose is requested.
---

# Human writing

## Mandatory workflow (always first)

When this skill applies to the user's request, **do not** start drafting or editing prose until steps 1–3 are done (unless the user explicitly asked only to edit the skill file itself—in that case, still fetch the page in step 1).

### 1. Fetch the live Wikipedia page

Retrieve the current content of:

`https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing`

Use any available read-only web tool the environment provides (for example `WebFetch` / MCP fetch / browser snapshot). **If the fetch fails**, say briefly that the live page could not be loaded, continue using this `SKILL.md` only, and skip step 3.

### 2. Session authority

For rules, new subsections, "words to watch" tables, and examples: **the live page overrides** this file when they disagree. Use the fetch as the source of truth for *what* to avoid in this turn; use this file as a compact local checklist and fallback.

### 3. Sync this skill when the live page has new material

After reading the live page, compare it to this `SKILL.md` (and `reference.md` if present).

**Update files** in this skill's directory (`~/.cursor/skills/human-writing/`) when the live page includes **substantive** content not already captured here:

- A **new named pattern** or section (e.g. new category of tells, new formatting sign).
- A **new or materially expanded** vocabulary list / "words to watch" cluster / LLM-era note that would change how you edit prose.
- A **clearly new** stylistic or structural tell that generalizes beyond Wikipedia markup.

**How to update**

- Edit **`SKILL.md`**: merge new guidance into the closest section below as short bullets or phrases; remove duplicates; keep the skill concise (prefer under ~250 lines total; never bloat with full Wikipedia text).
- If a list is **too long** to inline, add a one-line pointer in `SKILL.md` and put the extended list or quote in **`reference.md`** in the same folder (create `reference.md` only when needed).

**Do not** edit the skill for trivial Wikipedia edits (typos, example swaps, rewordings that do not change the rule), drive-by reformatting, or when the live page matches what is already documented.

### 4. Then do the user's task

Draft, revise, or answer using the live page + this file. Finish with the **Final pass** checklist.

---

## When this applies

Use whenever the deliverable is primarily **natural language** for a human reader. Prefer **specific facts** over generic importance; prefer **plain** sentences over rhetorical padding.

**Scope note:** The Wikipedia page targets undisclosed AI on Wikipedia. Many patterns apply to general writing; **ignore** Wikipedia-only signals (broken wikitext, fake shortcuts, citation bugs) unless the user is editing Wikipedia.

## Core principle (from the guide)

LLM text tends to **regress to the mean**: vague, positive, broadly applicable phrases replace **specific, unusual, nuanced** detail. **Fix** by grounding claims in concrete detail the user or sources actually provide; cut filler that could apply to any similar topic.

## Content: cut or rewrite

- **Significance / legacy / "broader trends"** — Avoid framing ordinary facts as pivotal, testament, indelible mark, deeply rooted, evolving landscape, setting the stage, marking a shift, focal point, stands/serves as, reflects broader, symbolizing enduring… unless proportionate and sourced.
- **Notability / media drumbeat** — Do not list outlets or "independent coverage" to prove importance unless the user asked for PR-style proof. Skip "active social media presence," "strong digital presence," profiled in…
- **Superficial analysis** — Remove trailing **-ing** clauses that "highlight/underscore/emphasize" significance (*…, reflecting…, contributing to…, ensuring…*). If analysis is needed, make it **substantive** and attributed; otherwise delete.
- **Promotional / travel-brochure tone** — Cut *vibrant, rich tapestry, nestled, natural beauty, groundbreaking, renowned, showcases, exemplifies, commitment to, diverse array, boasts* (meaning "has") unless truly neutral and deserved.
- **Vague attribution** — Replace *experts say, observers note, industry reports, some critics* with named sources or honest uncertainty ("one study…", "according to X").
- **Challenges / future outlook formula** — Avoid *Despite its success… faces several challenges… Despite these challenges…* scaffolding and generic "future prospects" closers.
- **Hedging about unknowns** — Avoid *while specific details are limited…, based on available information…, not widely documented…* plus speculative filler—unless the user needs a careful epistemic caveat.

## Language and grammar

- **High-density "AI vocabulary"** — Swap or delete overused items: *additionally* (sentence-starter), *align with, bolstered, crucial, delve, emphasizing, enduring, enhance, fostering, garner, interplay, intricate/intricacies, key* (adj.), *landscape* (abstract), *meticulously, pivotal, robust, showcase, tapestry, testament, underscore, valuable, vibrant, highlighting…* Use plain alternatives; keep **literal** senses (e.g. musical "underscore").
- **Copula avoidance** — Prefer direct *is/are/has* over *serves as, stands as, marks a, features, offers, boasts* when they add no meaning.
- **Negative parallelisms** — Cut rhetorical *not just X but Y, it's not A—it's B* unless the user wants that device.
- **Rule of three** — Don't stack three parallel adjectives or phrases habitually; one strong detail beats two weak echoes.
- **Elegant variation** — Reuse a clear noun (the person's name, the product name); don't rotate synonyms (*the protagonist, the eponymous figure…*) without reason.

## Style and format (general writing)

- **Headings** — Prefer **sentence case** over Title Case Everywhere unless the user's style guide says otherwise.
- **Emphasis** — No mechanical **bold** on every bullet or keyword; use bold sparingly.
- **Lists** — Avoid **bold inline header:** boilerplate on every line unless the format is requested.
- **Em dashes** — Use sparingly; prefer commas, parentheses, or a period. Don't chain em-dash "punchy" clauses.
- **Horizontal rules** — Don't sprinkle `---` / thematic breaks between every section.
- **Placeholder / chat residue** — No *I hope this helps*, *of course*, *let me know if*, *here is a …*, unfilled `[brackets]`, or assistant-y sign-offs unless the user asked for a conversational reply.

## Communication to the user

If the user asked for **content** (not meta-advice), deliver **only** the content—no *In this section we will…*, no *Below is a detailed overview…* wrappers unless they asked for structure explicitly.

## Final pass (short checklist)

1. Did I **fetch the live Wikipedia page** first (or note failure)?
2. Did I **sync** `SKILL.md` / `reference.md` if the live page added substantive new rules not already stored here?
3. Did I add **specific** detail vs. generic importance?
4. Did I remove **significance / insight / landscape** padding?
5. Did I strip **AI vocabulary** spikes and **rule-of-three** rhythm?
6. Are claims **grounded** (user facts, files, web) without fake breadth?
7. Is tone **appropriate** (not brochure, not debate-club parallelism)?
8. Did I remove **template talk**, **placeholder**, and **over-formatting**?

## Reference

Canonical URL (fetch this every time): [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).

Optional local detail file in this directory: [reference.md](reference.md) (if present).
