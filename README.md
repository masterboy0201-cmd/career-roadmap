# Career Roadmap

A single-page, 4-year roadmap for a BTech cybersecurity student in India, from first year to job-ready. Plain HTML, CSS and JavaScript in one file. No backend, no build step, no remote images.

## Files

| File | Purpose |
|---|---|
| `career-roadmap.html` | The whole site: layout, styles, logic and content |
| `README.md` | This file |

## Run it

- Open `career-roadmap.html` in a browser. It works from the local file system.
- Fonts (Anton, Inter, JetBrains Mono) load from Google Fonts. Offline, the site falls back to Oswald/Impact, system sans-serif and monospace.
- To host it, upload the file to any static host (for example GitHub Pages) and rename it `index.html` if the host requires that.

## Pages

Routing uses the URL hash.

| Route | Page |
|---|---|
| `#/` | Home: hero, practice strip, four year cards, timeline |
| `#/y1` to `#/y4` | Year pages, 11 sections each, plus the legal footer |
| `#/progress` | Progress by year, phase and section; export and import |

Year 4 also has a specialization selector with 5 tracks (Penetration Tester, SOC Analyst, DFIR, Application Security, Cloud Security). The choice is saved.

## Editing content

All roadmap content is in the `ROADMAP` object at the top of the `<script>` block. Layout code does not need to change.

```js
ROADMAP.years[i] = {
  theme, goal, hrs,           // strings
  out: [3 strings],           // key outcomes shown on the home card
  skills: { "Group": [..] },  // section 1, every item is a checkbox
  phases: [{ m, f, tasks: [..], d }],  // section 2: months, focus, tasks, deliverable
  tools: [..], res: [..],     // sections 3 and 4, shown as chips
  projects: [..],             // section 5, checkboxes
  certs: "string",            // section 6
  split: [["Label", hours]],  // section 7, total is computed
  exit: [..],                 // section 8, checkboxes
  qa: [["Question", "Short answer"]],  // section 9
  bad: [..],                  // section 10
  tracks: [{ n, s, c, r, k }] // Year 4 only: name, skills, certs, roles, capstone
}
```

### Checkbox IDs

IDs are generated from list position:

| Section | ID format |
|---|---|
| Skills | `y1-s{group}-{item}` |
| Phase tasks | `y1-p{phase}-t{task}` |
| Projects | `y1-pr{n}` |
| Exit criteria | `y1-e{n}` |

Because IDs depend on position, add new items at the end of a list. Inserting, deleting or reordering items shifts the IDs and misaligns progress already saved in a browser.

## Progress calculation

- Year progress = checked boxes / total boxes in sections 1, 2, 5 and 8.
- Phase progress uses the tasks in that phase only.
- Overall progress covers all four years.
- The Progress page shows each year by section (skills, phase tasks, projects, exit criteria) and by phase.

## Storage

- Data is stored in `localStorage` under the key `cr1`, wrapped in try/catch. If storage is blocked (some private modes), the site works but nothing persists.
- Stored: checked IDs, notes per year, the Year 4 track choice, and the theme.
- Data is per browser and per device. It does not sync.
- Clearing site data deletes progress. Export first.

### Export and import

- **Export** writes JSON (checked IDs, notes, track) into a text box and tries to copy it to the clipboard. Save it in a file yourself.
- **Import** reads pasted JSON and replaces the current checked IDs, notes and track. The theme is not included.
- Browser file downloads are not used, because they fail in some embedded and hosted contexts.

### Reset

The nav "Reset" button opens a confirmation dialog. Confirming clears checked IDs, notes and the track choice. The theme setting is kept.

## Design

- Black, white and greys only. Off-white background `#f4f4f2` with a halftone texture drawn on a canvas: dense at the edges, clear in the center.
- Dark mode inverts colors and texture. Default follows the system setting; the nav toggle overrides it.
- Headings use a condensed grotesque (Anton), body text uses Inter, small labels use JetBrains Mono.
- The hero shield graphic is inline SVG.
- Print layout: white background, black text, no nav, no texture. All collapsible sections open before printing.

## Content notes

- Months count from the start of the academic year. Reduce weekly hours in exam weeks.
- Hours, problem counts and application counts are suggested planning defaults, not research-backed figures.
- Platform path names, certification objectives and legal sections change. Verify them on the official site.
- The site contains no URLs to external resources, certification costs or salary figures.
- Content is a condensed version of the full spec. Skill lists, phase tasks and self-check questions are shorter than the original. Expand them in `ROADMAP`.

## Known limitations

- Not tested across browsers or devices. Check mobile layout and dark mode before relying on it.
- Notes and progress are plain `localStorage`. There is no account, backup or sync.
- Self-check answers are short summaries, not full explanations.

## Legal notice

Test only systems you own or have written permission to test. Unauthorized access is an offense under the Information Technology Act, 2000 (see Sections 43 and 66).
