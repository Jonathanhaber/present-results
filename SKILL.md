---
name: present-results
description: Use when building or reviewing a page, report or HTML artifact whose job is to communicate analysis results or metrics to a reader, such as analysis write-ups, KPI reports, experiment or A/B readouts, comparisons, research findings and static dashboards. Also use when such a page is cluttered, hard to read at a glance, uses pies or rainbow colors, or shows rates without their base. Not for app UIs that merely contain a table, marketing pages, or live monitoring dashboards.
---

# Present results

A results page answers one question for one reader, and the reader should get the answer in about five seconds. This manual decides what goes on the page, in what order, and how it looks.

**Every rule has a goal and a source.** The core rules come from perception research (Cleveland & McGill, Tufte, Shneiderman, eye-tracking studies) and from published standards (WCAG, the UK Government Analysis Function, Bach et al.'s dashboard patterns). `references/research.md` gives each rule's goal, its evidence, and other ways to reach the goal. Read it when a rule doesn't fit the case or someone asks why. Values marked † are house defaults, not research findings.

**Rules serve goals.** Break a rule only if the page still meets that rule's goal. Say which rule you broke and why in an HTML comment at the top of the file and in your reply.

**Precedence.** If a project has its own design manual, it wins over this one. If a `dataviz` skill (chart mechanics, palette validation) or the `artifact-design` skill (Claude artifact page contract) is available, use it for the parts this manual doesn't cover; where they conflict, this manual wins. Everything here works without them.

---

## 1. The no-bullshit rule

Only three things go on the page:

| Layer | What it is | Examples |
|---|---|---|
| **Content** | the data that answers the reader's question | numbers, charts, tables, verbatim quotes from the data |
| **Grounding** | what lets the reader trust it and read it correctly | source, period, pull date, base (n), excluded cases, definitions, method in one line, caveats |
| **Meaning** | what the data says, in one sentence with its number | finding lines, comparisons, the answer to the question |

**Deletion test, for every element:** *Without it, could the reader still get the answer to their question (§3, step 1), trust it and read it correctly?* If so, delete it. If you're unsure about content or meaning, delete it. If you're unsure about grounding, or it is needed only to check a number (field names, query details), move it to "Definitions and data".

**Always cut:**
- Intros and outros: "This report shows…", "In summary…", "Key takeaways", a conclusion that repeats the finding lines.
- Headings, cards or sections without a number or a definition in them.
- Decoration: icons, emojis, illustrations, hero images, gradients, shadows, chart frames, boxes around legends, colored warning boxes, and logos unless the reader's organization requires one.
- Grading words: "impressive", "only", "poor", "strong", "significant" (unless a test was run and is named).
- Methodology prose beyond one line.
- Recommendations nobody asked for, or that no number on the page supports.
- A chart for what one sentence says. Two or three numbers are a sentence or tiles, not a chart.
- Deltas, trend arrows and sparklines without a real earlier period to compare to.
- A number shown twice. There are four exceptions: a finding line may cite numbers shown below it; the first section's finding line may restate the header's when that section carries the answer; the hero figure may reappear as its own part of the split right below it; and a count may reappear as the base of a different rate.
- Legends that repeat direct labels, and axis titles that repeat the chart title.
- Tooltips that repeat a value already printed beside the mark.
- Interactivity nobody needs to answer the question: filters, tabs, toggles, animation.
- Placeholders, "TBD", "coming soon", filler tiles to make a grid even.

**Meaning is not opinion.** A finding line states and compares what the numbers show. It doesn't grade, guess causes or claim more than the data shows.

**Interpretation, only when asked.** If the reader's question asks for causes or next steps ("where should we put more effort?"), answer it in an **interpretation line**:
- It sits directly after the finding line it follows from. When it answers the page's question, it goes in the header (§4).
- It starts with "This suggests…", is set in secondary ink, and ties every claim to a number on the page.
- "Definitions and data" lists what the decision needs that the data doesn't have (cost, time, quality), under "Not in the data".

---

## 2. The ten rules

1. **Lead with the answer.** The page and every section open with a finding line: one sentence with its number and base.
2. **Every rate shows its base:** `20%` with `412 of 2,060 finished trials`. Use the base the reader's question names ("per lead contacted" means every lead contacted). Cases that never reached the person (bounced, wrong number) stay in that base; give the rate without them in a footnote. If the base leaves cases out, show next to the rate how many it leaves out.
3. **Use length and position for numbers.** Bars sit on one zero baseline. No pies, donuts, gauges, 3D or dual axes.
4. **Color marks states, not groups.** It has one job per page and means the same thing in every chart. Groups get color only where marks can't be told apart otherwise (§6.1).
5. **Never use color alone.** A label, count or legend sits beside every colored mark.
6. **Same thing, same way:** one component, one scale and one word per idea.
7. **Overview first.** The answer fits the first screen, and details sit below it.
8. **Text is ink.** It reaches 4.5:1 contrast or more and never sits on a solid colored fill.
9. **Every number is traceable:** source, period, pull date, definitions, caveats.
10. **No bullshit.** If it isn't content, grounding or meaning, delete it (§1).

---

## 3. Workflow

Do these in order, before writing HTML.

1. **Question and reader.** Write the reader's question in one line, and who reads the page: their role, what they already know, their device, and how much time they have. State any assumption.
2. **The answer.** Write one sentence with the key number. If you can't, analyze further; don't design yet.
3. **Findings.** List up to five† supporting findings, each one sentence with its number and base. Drop any that don't serve the question. For every difference the reader will act on, check whether chance could explain it (§7, close calls).
4. **Form.** Pick a form for each finding (§5). Sometimes the form is a sentence or a single number.
5. **Grounding.** Collect the source, period, pull date, bases, excluded cases, definitions and caveats. Look for cases that had little time to reach an outcome before the pull date: keep them in the base unless a definition excludes them, check whether the answer holds without them, and report the check in "Definitions and data".
6. **Build** from the skeleton (§4), starting from `assets/starter.html`.
7. **Cut.** Run the deletion test (§1) on every element.
8. **Check** against §10, and look at the rendered page.

---

## 4. Page skeleton

```
┌──────────────────────────────────────────────────────────────┐
│ HEADER       Title (topic, 2–6 words†)                         │
│              Finding line: the answer, with its number         │
│              Interpretation line (only if asked for, §1)       │
│              Grounding line: source · period · n · pulled on   │  first
├──────────────────────────────────────────────────────────────┤  screen
│ AT A GLANCE  Hero figure + base · up to 4 tiles                │
│              (optional) the split the hero is part of          │
├──────────────────────────────────────────────────────────────┤
│ SECTIONS     one per finding: title → finding line →           │
│              chart or table → footnotes                        │
├──────────────────────────────────────────────────────────────┤
│ DEFINITIONS AND DATA   terms · source · method · caveats ·     │
│                        not in the data                         │
└──────────────────────────────────────────────────────────────┘
```

- Use a single column with full-width sections, so the reading order is the same on laptop and phone.
- The header and "at a glance" fit the first 720px† of viewport height (a 1440 × 900 laptop minus browser chrome). A reader who stops there still has the answer.
- The most important number sits top-left: the hero figure, then the tiles.
- Order sections by importance to the question, not by the order of the analysis.
- A small result (one or two findings) skips "at a glance" and has no hero figure: header, sections, definitions.

---

## 5. Picking the form

| The reader must… | Use | Not |
|---|---|---|
| Read one number | hero figure or tile, with its base | a one-bar chart |
| Read two or three numbers | a sentence or tiles | a chart |
| Rank or compare groups on one measure | sorted horizontal bars | a color per group |
| Compare groups on several measures | comparison table with a thin split bar | several charts with different scales |
| See how one whole splits (≤ 6† parts) | segmented bar normalized to 100%, legend with counts | pie, donut |
| Compare the parts of a whole | ranked horizontal bars | segments |
| Compare a value with a target | bar with a target tick (bullet graph), the gap in the finding line | gauge |
| Compare share of effort with share of result | paired horizontal bars on one scale, per group | two separate charts |
| See change over time | line for many points, columns for up to 12† periods | stacked areas with many series |
| See one group against the rest | emphasis: that group in the accent, the rest neutral | a rainbow |
| See before → after per item | dumbbell or slope chart | two side-by-side charts |
| See a spread | histogram or dot plot | an average alone |
| See whether two measures move together | scatter; groups as small multiples or emphasis | two y-axes |
| See who did what for whom | matrix with counts (§7) | a network diagram |
| Read themes in free text | themes with counts and quotes (§7) | a word cloud |
| Look up exact values | table | labels on every point |

- **Bars start at zero**, because the length is the value. Lines may zoom the axis† if the axis labels show where it starts.
- **Horizontal bars for named categories** keep labels readable on a phone.
- **Sort** by the measure being compared, unless the categories have a natural order (time, plan size, scale steps).
- **One measure per axis.** Two measures get two charts, unless they share a unit and the reader compares them directly (share of effort against share of result).
- **Size limits†:** at most seven series or segments per chart. Sorted bars carry up to about 20 rows; beyond that use a table, or the top rows plus "All others".
- For more forms, look up the relationship in the [FT Visual Vocabulary](https://github.com/Financial-Times/chart-doctor/blob/main/visual-vocabulary/README.md).

---

## 6. Foundations

### 6.1 Color

**Tokens** (the starter page defines them; both modes):

| Role | Token | Light | Dark | Use (contrast on `--surface`, light / dark) |
|---|---|---|---|---|
| Page | `--page` | `#f9f9f7` | `#0d0d0d` | background |
| Surface | `--surface` | `#fcfcfb` | `#1a1a19` | cards |
| Ink | `--ink` | `#0b0b0b` | `#f0efec` | titles, values, finding lines |
| Secondary ink | `--ink2` | `#52514e` | `#c3c2b7` | body, labels, interpretation line (7.7 / 9.7:1) |
| Muted ink | `--muted` | `#6f6e69` | `#9a9890` | notes, axes, small n (5.0 / 6.0:1): the lightest text allowed |
| Gridline | `--grid` | `#e1e0d9` | `#2c2c2a` | hairlines, bar tracks |
| Axis | `--axis` | `#c3c2b7` | `#383835` | baselines |
| Border | `--border` | `rgba(11,11,11,.10)` | `rgba(255,255,255,.10)` | card edges |
| Neutral mark | `--neutral` | `#898781` | `#898781` | context bars, totals, "the rest" in emphasis (3.5 / 4.9:1) |
| Remainder | `--rest` | `#b5b4ac` | `#5a5954` | leftover states: "other", "no answer", "expired", "still open" (2.0 / 2.5:1) |
| State 1 | `--s1` | `#2a78d6` | `#3987e5` | the accent; the state the page is about (4.3 / 4.8:1) |
| State 2 | `--s2` | `#eb6834` | `#d95926` | second state (3.1 / 4.5:1) |
| State 3 | `--s3` | `#1baf7a` | `#199e70` | third state (2.7 / 5.1:1) |
| Highlight | `--hl` | `#e87ba4` | `#d55181` | the one thing to stand out when `--s1` already means something; as a wash `--wash-hl`, 28% / 32% |

The utility tokens are `--hover` (row hover wash) and `--tip-bg` / `--tip-ink` (tooltip, inverted ink). States 1–3 come from the `dataviz` reference palette and pass a colorblind check for all pairs in both modes (worst ΔE 9.2 light, 9.4 dark; target ≥ 8). If you add or change a color, check it with a colorblind simulator (or the `dataviz` validator, if available).

**States and groups.** A *state* is what an item can end up as (converted, cancelled, expired; accepted, declined). A *group* is anything you slice by (plan, channel, team, client, platform). States can get colors. Groups are rows and labels. Groups get color only where marks would otherwise be indistinguishable (several lines on one time axis, groups in a scatter): at most four, each labeled directly at the mark, the same color for that group everywhere on the page. Bars are never colored by group.

**Pick the one job color does on this page:**

| Job | Colors |
|---|---|
| **Emphasis** (default) | everything in `--neutral`, the one thing that matters in `--s1` |
| **States that are the subject** | `--s1` for the state the page is about, then `--s2`, `--s3`; leftover states last, the largest in `--rest`, the next in `--neutral`; merge any more into "Other" with a footnote |
| **Magnitude** (heatmap) | one hue, light → dark: `--s1` washes at 15%, 35%, 60%, 100%† (or the `dataviz` sequential ramp) |
| **Above or below a midpoint** | `--s1` ↔ `--s2` with `--rest` at the midpoint (or the `dataviz` diverging ramp) |
| **Groups that can't be told apart otherwise** | `--s1`, `--s2`, `--s3`, `--hl`, in that order, each directly labeled |

**Rules:**
- The same color means the same thing on the whole page. The order is fixed and never cycled by rank, and a filter never recolors anything.
- Bars for a rate take the color of the state they count (a conversion rate is in the "converted" color). A measure without a state uses `--s1`, or `--neutral` if `--s1` is taken.
- At most four colors per chart, the remainder gray included. At most one highlighted thing per chart, and its legend says what it is.
- Don't use a red/green pair for bad/good, and never give a negative state the green `--s3`: it fails for color-blind readers and it grades. If good or bad is the point, say it in words.
- Fills below 3:1 (state 3 light, remainder, highlight) always carry their value beside the mark or in the legend.
- **No text on a solid colored fill.** The page's ink doesn't reach 4.5:1 on the state fills (`--s1`–`--s3`). Values go beside the bar or into the legend. A light wash behind text is fine if the ink on it reaches 4.5:1: on `--wash-hl`, use `--ink` or `--ink2` only.

### 6.2 Typography

All sizes are house choices†.

| Role | Size / weight | Note |
|---|---|---|
| Page title (`h1`) | 28px / 650 | the topic, 2–6 words |
| Section title | 19px / 650 | |
| Finding line | 16px / 400 | ink |
| Interpretation line | 15px / 400 | secondary ink |
| Hero figure | 56px / 650 | at most one per page |
| Tile value | 26px / 650 | |
| Body | 15px / 400 | |
| Table text, row labels, bases | 14px | |
| Labels, notes, axis, tags | 12–13px | secondary or muted ink |
| Footnote markers | 11px | muted ink, superscript |

- Use one family, `system-ui, -apple-system, "Segoe UI", sans-serif`, with no web fonts.
- Use sentence case for titles and labels.
- Use `tabular-nums` in tables, value columns, legends and axes. Large standalone numbers keep proportional figures.

### 6.3 Layout and marks

All values are house choices†.

- Content max width is 1140px. Side padding is 24px, or 16px under 640px.
- Cards have a 1px hairline edge, 14px radius and 24px padding (16px on phones), with 16px between cards. Nothing inside a card gets another border; group with whitespace.
- Spacing comes in steps of 4px.
- No page-level horizontal scroll at 375px. A wide table scrolls inside its own container.
- Gridlines are 1px solid hairlines, at most five per chart, never dashed.
- Bars are at most 24px thick, rounded 4px at the data end and square at the baseline. Segmented bars round both ends: 28px tall when they stand alone, 10px in a table.
- Touching segments get a 2px surface-colored gap, never a stroke.
- No shadows, except on the floating tooltip.

### 6.4 Numbers

| Kind | Format | Example |
|---|---|---|
| Rate | whole percent; one decimal when the rates compared are under 10% or every base is above 1,000†. One precision per chart, table and finding line, except small-n rows, which always show whole percent. Round halves up. A true zero is `0%`; never round a nonzero rate to 0%, write `<1%` | `20%`, `7.5%` |
| Base | "x of n" plus the base noun, which may stand once in a column header | `412 of 2,060 finished trials` |
| Difference of rates | percentage points, never % | `18 points`, `+4 pts` |
| Change of an amount | percent, with both values in the finding line | `+12% (€410k → €459k)` |
| Count | integer, comma from 1,000 | `2,290` |
| Large number | abbreviate from 10,000† in tiles and labels; exact in tables | `1.2M`, `48k` |
| Money | currency symbol, no decimals above 100† | `€4,120`, `$18.50` |
| Negative | true minus sign | `−3 pts` |
| Shares of a whole | precision as for rates, using the whole's n; may sum to 99–101% from rounding; footnote it once | `63%` |
| Duration | hours under one day, otherwise days with one decimal | `5 h`, `6.5 days` |
| Date | day, short month, year | `3 Oct 2026` |
| Period | en dash range | `1 Jul – 30 Sep 2026` |
| Zero | `0` (empty matrix cells stay blank, §7) | `0` |
| Not applicable | en dash | `–` |

Every number has its unit, either beside it or in the column header. Use English number formats unless the page is in German (`1.234,5`).

### 6.5 Words

- Use the reader's words, not the database's. Table names, field names and internal codes appear only in "Definitions and data".
- One word per idea, defined once in "Definitions and data".
- Labels start with the word that carries the information: "Cancelled: 343", not "Number of trials that were cancelled".
- Use plain English, active verbs and short sentences: "Customers cancelled 343", not "343 trials were set to cancelled".
- Don't use abbreviations the reader doesn't use themselves.

---

## 7. Components

Each component lists its **goal**, then its anatomy and rules. The starter page contains the header, hero, tiles, segmented bar, ranked bars, comparison table, small n, footnotes, tooltip script and definitions.

- **Header.** *Frames the page and gives the answer.* Title (topic) · finding line · interpretation line if asked for (§1) · grounding line (source · period · n · pull date).
- **Finding line.** *The meaning of a section in one sentence.* It sits directly under the section title and contains the number and its base. Templates in §8.
- **Hero figure.** *The one number the page leads with.* Label, value, and base on the line below. At most one per page.
- **Tile.** *A supporting number.* Label, value, and a one-line definition visible without hovering. Up to four, and no filler tiles.
- **Segmented bar.** *How one whole splits.* Normalized to 100%, parts in a fixed order, no text inside the fills. The legend underneath gives name, count and share per part: "Cancelled **343** · 17%".
- **Ranked bars.** *Compares groups on one measure.* Horizontal and sorted, with one header row naming the measure and base noun. Label on the left, "value · x of n" on the right. Bar length runs from zero to the largest value among rows that are not small n.
- **Comparison table.** *Compares groups on several measures in one reusable block.* Columns: group · split bar (10px, no text) · base · counts per part · rates. Every bar segment has its count and share in a column. Show all rows, sorted. Numbers are right-aligned in tabular figures, with one legend under the table. Make columns sortable when there are more than 7† rows.
- **Small n.** *Stops anyone over-reading a rate from a few cases.* Groups with fewer than 10† cases get muted text, a "small n" tag, whole-percent rates and a faded bar. They sit below the other rows, sorted among themselves by the same rule, and are left out of rankings in finding lines. They never set a chart's scale: a small-n row whose value would exceed the largest other bar shows its printed value without a bar.
- **Unknown groups.** *Nothing disappears silently.* Items without a group ("No channel recorded", "Unassigned") stay visible as the last row and count in totals and shares. A footnote says what is missing and why, if known. They are left out of rankings in finding lines.
- **Close calls.** *Stops anyone acting on a gap that chance can explain.* When the reader must choose between groups or variants, test each difference they will act on (two-proportion test at the 5% level, or 95% intervals). If chance can explain it, say so under the chart in plain words ("At these numbers, a gap this size can be chance") and don't rank those groups against each other. If the top groups are a close call, name them together ("Cold calls and LinkedIn book the most meetings; the gap between them can be chance"). Name the test in "Definitions and data". Show intervals on the chart only for readers who use them.
- **Time chart.** *Shows when things happened.* Columns per period, or a line. The note says which date it counts by ("by payment date") and when a week starts. Events are annotated in place ("price change 14 Aug"), not in a legend. An incomplete last period is marked ("partial, to 14 Nov") or left out, so it doesn't read as a drop.
- **Matrix.** *Shows who did what for whom.* Rows and columns are groups, cells are counts, with row and column totals. Empty cells stay blank, because a grid of zeros hides the few real counts. Only the exceptions get a wash (highlight); the expected cells stay plain.
- **Themes from free text.** *Explains the "why" in the reader's own words.* Per theme: name, a one-line description, count and share, a bar, and one to three verbatim quotes trimmed with "…". Sort themes by count, and don't put personal names in attributions. One line says who grouped the texts (e.g. "grouped by Claude"). The full list sits behind a toggle.
- **Footnotes.** *A caveat that applies to one number.* A marker (¹) on the number, and the note below the chart in muted ink.
- **Tooltip.** *Gives an exact value that isn't printed nearby.* Opens on hover, tap and keyboard focus, and is never the only way to reach a value. Leave it out where the value already sits beside the mark.
- **Detail list.** *Raw rows or verbatim comments.* Shows the first 10† and collapses the rest.
- **Definitions and data.** *Makes every number traceable.* A definition list closing the page: every term, the source, how and when it was pulled, the method, the caveats, and "Not in the data" when the page carries an interpretation line.
- **Empty data.** *The page never shows an empty chart.* A section or selection without data shows one sentence: "No trials in this selection."
- **Filters** (only if the reader needs to slice the data). One row above everything it scopes, with a count of matching items and a reset. Finding lines recompute from the selection, and a filter never recolors anything. A section that ignores a filter says so in one line.

---

## 8. Finding lines

Fill these from the data (in code, when the page has filters):

| Kind | Template |
|---|---|
| Level | "{Measure} is {x} ({a} of {n} {base noun})." |
| Comparison | "{A} {measure} is {x} ({a} of {n}), {d} points above {B} ({y}, {b} of {m})." |
| Ranking | "Highest {measure}: {group} ({x}, {a} of {n}). Lowest: {group} ({y}, {b} of {m})." |
| Change | "{Measure} went from {x} ({a} of {n}) in {period 1} to {y} ({b} of {m}) in {period 2}." |
| Concentration | "{k} of {n} {items} account for {share} of {total}." |
| Split | "Largest share: {part} ({x}, {a} of {n} {items})." |
| Close call | "{A} ({x}, {a} of {n}) and {B} ({y}, {b} of {m}) have the highest {measure}; the gap between them can be chance." |

- It names the measure it ranks by, and leaves small-n groups, unknown groups and close calls out of rankings.
- It is true for exactly what is shown, under every filter.

---

## 9. In a Claude artifact or HTML file

- Start from `assets/starter.html`. Its token block already follows the artifact page contract (tokens on `:root`, dark mode under `prefers-color-scheme` and `[data-theme="dark"]`, explicit body background).
- Keep the page self-contained: system fonts, inline CSS and JS, no images. In a Claude artifact, external scripts may come only from the CDNs `artifact-design` allows.
- The `<title>` is a 2–4 word name of the topic; the `h1` may add the period ("Trial conversion, Q3 2026").

---

## 10. Ship checklist

**Content, grounding, meaning**
- [ ] Every element passes the deletion test, and nothing from the "always cut" list is on the page.
- [ ] The page and every section except "Definitions and data" have a finding line with a number and its base, true for the data shown (also under filters).
- [ ] Every rate shows its base on the page, and excluded cases are shown next to the rate.
- [ ] Differences the reader will act on were tested; close calls are named, not ranked.
- [ ] The header gives source, period, n and pull date.
- [ ] Every term the reader may not know is defined; interpretation is in an interpretation line, and "Not in the data" lists what it lacks.

**Charts**
- [ ] No pie, donut, gauge, 3D or dual-axis chart.
- [ ] Bars start at zero; segmented bars are normalized to 100%; small-n rows don't set the scale.
- [ ] Color does one job; no bars colored by group; at most four colors per chart; no red/green, no green for a negative state.
- [ ] Every value is reachable without hovering, and no tooltip repeats a printed value.

**Words and numbers**
- [ ] One precision per chart, table and finding line; no nonzero rate shown as 0%; shares sum to 100% or carry a rounding footnote.
- [ ] No database names, codes or internal jargon outside "Definitions and data".

**Build**
- [ ] All text reaches 4.5:1 in light and dark mode, and none sits on a solid colored fill.
- [ ] No page-level horizontal scroll at 375px (check in device emulation or a 375px iframe); header plus "at a glance" fit the first 720px of height.
- [ ] If the page has tooltips, they open on hover, tap and keyboard focus.
- [ ] Rendered and checked by eye in light and dark mode.
