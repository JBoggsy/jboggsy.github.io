# Copilot Instructions — jboggsy.github.io

This is James Boggs' personal website, hosted via GitHub Pages. It is a **single static HTML page** (`index.html`) with no build step, no templating engine, and no server-side logic.

## Tech Stack

- **Bootstrap 4.5.0** loaded from CDN (StackPath). Do not upgrade or switch to a local copy without being asked.
- **jQuery 3.5.1 slim**, **Popper.js 1.16.0**, **Bootstrap JS 4.5.0** — all CDN. Same rule: don't change versions unprompted.
- **Font Awesome** via kit script. Use `<i>` tags with FA class names for icons.
- No build tools, bundlers, or preprocessors. Keep the site fully static.

## HTML Conventions

- **Indentation:** 4 spaces. No tabs.
- **Line width:** Wrap at ~120 characters (matches `rewrap.wrappingColumn` in workspace settings).
- **HTML entities:** Use named entities for special characters — `&mdash;` (em dash), `&middot;` (middle dot), `&amp;` (ampersand), `&lt;`/`&gt;`, etc. Do not use raw Unicode equivalents in HTML text content.
- **Structure:** The page is a single Bootstrap grid. Content is split into tabs (`#aboutme`, `#projects`) using Bootstrap's tab component. Do not restructure the layout unless explicitly asked.
- **Classes:** Use Bootstrap 4 utility classes. Do not introduce custom CSS unless absolutely necessary.

## Writing Style

- **About Me tab:** First person, polished, academic-but-accessible tone.
- **Projects tab intro:** Third person ("A selection of personal projects...").
- **Project cards:** Third person, technical but readable. Describe what the project *does*, its architecture, and key features in 3–6 sentences. Keep "Current progress" to 2–3 sentences.
- **No changelogs or timestamps.** Never add "Updated on...", "What's New", or changelog sections.
- **Only state facts.** Do not describe features or capabilities that aren't evidenced in the source code or repository. When uncertain, keep existing text.

## Project Card Template

Every project card in the `#projects` tab follows this structure:

```html
<div class="card mb-4">
    <div class="card-body">
        <h4 class="card-title">Project Name</h4>
        <p class="card-text">
            Description of what the project does...
        </p>
        <p class="card-text"><strong>Current progress:</strong>
            Status summary...
        </p>
        <span class="badge badge-primary">Tech1</span>
        <span class="badge badge-primary">Tech2</span>
        <span class="badge badge-secondary">Status Label</span>
    </div>
</div>
```

When editing or adding project cards, preserve this exact structure. Use `badge-primary` for technologies and `badge-secondary` for the status label.

## Owner Info

- **Name:** James Boggs
- **GitHub:** https://github.com/JBoggsy
- **Role:** AI Research Scientist at the Center for Integrated Cognition
- **Education:** Ph.D. in CSE from University of Michigan (completed)

When editing biographical content, keep it consistent across the page (sidebar summary and About Me body should agree).
