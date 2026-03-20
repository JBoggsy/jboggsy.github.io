---
applyTo: "**/index.html"
---

# Auto-Update Website Project Descriptions

Update the project descriptions on the personal website to reflect the current state of each project's GitHub repository. This skill fetches live repo data and rewrites descriptions in-place — it does **not** add changelogs, update logs, or new sections.

## Context

- The website is a single-page Bootstrap site at `index.html`.
- Projects are displayed as Bootstrap cards inside `<div id="projects">`.
- Each card has:
  - A **title** (`<h4 class="card-title">`)
  - A **description** (`<p class="card-text">`) summarizing what the project does
  - A **"Current progress"** paragraph (`<p class="card-text"><strong>Current progress:</strong>...`) summarizing current status
  - **Technology badges** (`<span class="badge badge-primary">`) and a **status badge** (`<span class="badge badge-secondary">`)
- The owner's GitHub profile is **https://github.com/JBoggsy**.

## Known Project-to-Repo Mapping

Use this mapping as a starting point. If a project has no repo listed, try searching `https://github.com/JBoggsy?tab=repositories&q=<keyword>` to find it. If no repo is found, skip that project and report it.

| Project (card title)              | GitHub Repo                                      |
|-----------------------------------|--------------------------------------------------|
| Shortlist                         | `JBoggsy/shortlist`                              |
| User Environment Simulator        | `JBoggsy/ues`                                    |
| Hopfield Network Explorer         | *(no repo — skip)*                               |
| AIPA — AI Personal Assistant      | `JBoggsy/aipa`                                   |

> **Maintaining this table:** When the user adds a new project card to the page, add its repo mapping here so future runs can find it immediately.

## Workflow

### Step 1 — Discover projects

1. Read `index.html`.
2. Parse the `<div id="projects">` section and extract every project card.
3. For each card, note:
   - The card title (used to match repos)
   - The current description text
   - The current "Current progress" text
   - The technology badges and status badge

### Step 2 — Fetch repo state

For each project that has a matching GitHub repo:

1. **Fetch the repo's README** via `https://github.com/JBoggsy/<repo>` (use `fetch_webpage`). Extract:
   - The project summary / what it does
   - Key features or architecture highlights
   - Tech stack mentioned
2. **Fetch the releases page** via `https://github.com/JBoggsy/<repo>/releases` (use `fetch_webpage`). Extract:
   - Latest release tag and name (if any)
   - Brief summary of what the latest release includes
3. **Fetch recent commits** via `https://github.com/JBoggsy/<repo>/commits` (use `fetch_webpage`). Extract:
   - Themes of recent work (e.g., "UI overhaul", "added tests", "API refactor")
   - Rough activity level (active, dormant, etc.)

Combine these into a **repo snapshot**: a concise understanding of what the project currently is and where it stands.

### Step 3 — Draft updated descriptions

For each project, rewrite **two things** based on the repo snapshot:

1. **The main description paragraph** — Update to accurately describe what the project currently does, its architecture, and key features. Keep the same tone and approximate length as the existing description (3–6 sentences). Do not copy the README verbatim; synthesize it into polished website copy.

2. **The "Current progress" paragraph** — Update to reflect the latest version (if releases exist), what's actively being worked on (from recent commits), and the overall status. Keep to 2–3 sentences.

Additionally update if needed:
- **Technology badges** — Add or remove badges to match the current tech stack.
- **Status badge** — Update the text (e.g., `v0.11.0 · Active`, `Early Development`, `Complete`, `Functional`) to match the current state.

### Step 4 — Apply edits

Use `replace_string_in_file` (or `multi_replace_string_in_file` for efficiency) to update each card's content in `index.html`. Preserve:
- All HTML structure and class names
- The card layout and ordering
- The `&mdash;`, `&middot;`, `&amp;` HTML entities style
- Indentation (spaces, not tabs)

### Step 5 — Verify

1. Re-read the edited `index.html` to confirm all changes look correct.
2. Report a summary of what was updated:
   - Which projects were updated and what changed
   - Which projects were skipped and why (no repo found, repo unchanged, etc.)

## Rules

- **No changelogs.** Do not add "Updates", "Changelog", "What's New", or any timestamped history section.
- **In-place only.** Only modify existing card content. Do not add new cards, remove cards, or restructure the HTML.
- **Skip gracefully.** If a project has no repo or the repo hasn't changed meaningfully, leave the card as-is and note it in the summary.
- **Preserve voice.** Match the existing writing style: concise, technical but accessible, third-person description of the project.
- **Be conservative with badges.** Only add a tech badge if the technology is prominently used. Only change the status badge if the status has clearly changed.
- **Do not hallucinate features.** Only describe functionality that is evidenced by the README, releases, or commit history. If uncertain, keep the existing description.
