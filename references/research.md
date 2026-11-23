# Why these rules work

This file holds the evidence behind the rules in `SKILL.md`. For each principle it gives the **goal**, **why it works**, and **other ways** to reach the same goal when the default rule doesn't fit. Use it to judge an edge case, or to explain a rule to someone who asks why.

The evidence comes in three strengths, and the text says which one it uses:
- **Experiments** on how people read charts (Cleveland & McGill, Heer & Bostock, Borkin et al., Kong et al.).
- **Standards and design-system guidance** (WCAG, UK Government Analysis Function, AWS Cloudscape, IBM Carbon). These are expert consensus, not experiments.
- **Descriptive studies** of what real dashboards do (Bach et al.). These show common practice, not what works best.

Where the skill goes further than its sources, this file says so.

## At a glance

| Rule in `SKILL.md` | Principle | Main evidence | Why it matters |
|---|---|---|---|
| 1 Lead with the answer | P1 | NN/g on scanning; Borkin et al. 2016; Kong et al. 2018 | Readers scan the top and the titles, and the title shapes what they take away from a chart. |
| 2 Every rate shows its base | P2 | The arithmetic of small groups; GitHub, DX and Google Ads metric definitions | A rate without its count hides how much evidence backs it, and the same metric name hides different formulas. |
| 3 Length and position for numbers | P3 | Cleveland & McGill 1984, replicated by Heer & Bostock 2010; NN/g | People compare positions and lengths more precisely than angles, areas or shading. |
| 4–5 Color: one job, never alone | P4 | NN/g on preattentive processing; UK Analysis Function; color-vision statistics | Color grabs attention before reading starts, is a weak channel for amounts, and is partly lost on color-blind readers. |
| 6 Same thing, same way | P6 | Tufte's small multiples; Bach et al. 2023 | When the format stays the same, the eye compares the data instead of decoding a new layout. |
| 7 Overview first | P7 | Shneiderman 1996; Few; AWS Cloudscape; IBM Carbon | The first screen must answer on its own, with details below it for readers who need them. |
| 8 Text is ink | Contrast | WCAG 2.2 | Below 4.5:1, part of the audience can't read small text. |
| 9 Every number is traceable | P8 | Metric-definition differences (P2); Bach et al. 2023 | A number the reader can't trace back can't be defended in a meeting. |
| 10 No bullshit | P0, P5 | Tufte's data-ink ratio; UK Analysis Function; NN/g | Every element that isn't data, grounding or meaning pushes the answer away from where the reader looks. |

---

## P0 · No bullshit: content, grounding, meaning

- **Goal:** Every element on the page helps the reader get the answer, trust it, or read it correctly.
- **Why it works:**
  - Tufte's data-ink ratio asks that ink go to data (P5). This skill extends the idea from ink to words: an intro paragraph is non-data ink. The extension is the skill's own, not Tufte's.
  - Readers scan and skip, so every extra element pushes the result away from where they look (P1).
  - Anything colored or bold competes for preattentive attention (P4).
  - Grounding is part of the content, not decoration. Real dashboards commonly carry it: Bach et al. found a whole group of "meta information" patterns (data source, update time, disclaimers). Their study describes practice, so the case for grounding rests on P2 and P8.
- **Other ways:** move grounding that only serves checking into "Definitions and data" or a collapsed detail.

## P1 · Lead with the answer

- **Goal:** The reader knows the main finding within about five seconds†, before reading a chart.
- **Why it works:**
  - A dashboard's job is to communicate critical information at a glance ([NN/g](https://www.nngroup.com/articles/dashboards-preattentive/); Few).
  - Scanning readers fixate most on the top lines and the first words of lines, so key information belongs there ([NN/g](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/)).
  - Titles draw attention. In an eye-tracking study of 393 visualizations with 33 participants, titles drew the most fixations, and titles that stated the message went with better recall of it. The link is a correlation, not a controlled test ([Borkin et al. 2016](https://doi.org/10.1109/TVCG.2015.2467732)).
  - Titles shape the takeaway. In Kong et al.'s experiments, people shown the same chart under differently slanted titles more often recalled the message their title emphasized. The charts were built to support either reading ([CHI 2018](https://zcliu.cs.umd.edu/vistitles/CHI18-VisTitles.pdf)). Practitioners call such titles action titles ([Storytelling with Data](https://www.storytellingwithdata.com/blog/2020/3/5/transforming-slide-titles), [think-cell](https://www.thinkcell.com/en/blog/how-to-tell-a-better-data-story-one-slide-at-a-time)).
  - Kong et al. also found that most readers rated the charts as neutral and rarely noticed the slant. A finding line is that powerful, so it may only say what the numbers show: it states and compares, and never grades.
- **Other ways:** the finding sentence itself as the title (works when there are no filters, e.g. a print version); a callout next to the bar that proves the point; the finding as the lead sentence of the message that carries the file.

## P2 · Every rate shows its base

- **Goal:** Nobody misreads a rate, least of all on small groups, and nobody acts on a gap that chance can explain.
- **Why it works:**
  - A percentage without its count hides how much evidence stands behind it: 100% of 2 looks better than 60% of 50.
  - Two rates over different bases look contradictory unless both bases are named. The base the reader's question names is the default, because that is the rate they asked for.
  - Tools compute the "same" metric differently. GitHub reports Copilot's acceptance rate as the share of suggestions accepted ([GitHub](https://docs.github.com/en/copilot/reference/copilot-usage-metrics/interpret-copilot-metrics)); DX computes it over suggestions for tab completions but over lines for chat ([DX](https://docs.getdx.com/reports/cursor-adoption/)). Google Ads raises its optimization score both when a recommendation is applied and when it is dismissed ([Google](https://support.google.com/google-ads/answer/9061546?hl=en)). Naming the base removes the guesswork.
  - Below 10 cases, one case moves a rate by 10 points or more. Hence the small-n treatment. The 10-case line† is a house default.
  - Precision balances two risks. Too many decimals suggest more certainty than the base supports (28.6% from 2 of 7). Too few hide real gaps between small rates (7.5% and 5.8% become 8% and 6%). Hence whole percent by default, one decimal for rates under 10%, and whole percent for small n.
  - A small-n group can still produce the largest rate on the page. If it leads the chart or sets the scale, the eye lands first on the number least worth reading. Hence small-n rows sit below the others and never set the scale.
  - A rate that leaves cases out of its base can look better than reality (e.g. acceptance among those who answered, when many never answered). Show the related rate next to it.
  - Small n is only the extreme case. With hundreds of cases per group, a gap of a few points can still be chance. A two-proportion test or an interval tells the reader whether to act on it. This is standard statistics; the "close calls" wording is the skill's own.
- **Other ways:** counts as the main figure with the rate beside it; the base as its own table column; confidence intervals on the chart (for readers who use statistical vocabulary).

## P3 · Show quantities as length and position

- **Goal:** Comparisons between groups are accurate and take no effort.
- **Why it works:**
  - Cleveland & McGill (1984) ranked how precisely people judge visual encodings: position on a common scale first, then position on unaligned scales, then length, direction and angle, then area, then volume and curvature, and shading or color saturation last. Part of the ranking was a hypothesis, but their experiments confirmed the key steps ([doi](https://doi.org/10.1080/01621459.1984.10478080)).
  - Heer & Bostock (2010) largely replicated the ranking with crowdsourced experiments ([doi](https://doi.org/10.1145/1753326.1753357)).
  - NN/g applies this to dashboards. It recommends avoiding pie and donut charts most of the time, along with gauges, treemaps and 3D, and notes that sorted bars make ranking immediate ([NN/g](https://www.nngroup.com/articles/dashboards-preattentive/)).
- **Where the evidence pushes back:**
  - For judging one share of a single whole, pies can be as accurate as bars, and better for sums of parts (A + B against C + D) ([Spence & Lewandowsky 1991](https://doi.org/10.1002/acp.2350050106)).
  - Pies seem to be read by area and arc rather than angle ([Kosara 2019](https://doi.org/10.1109/VISUAL.2019.8933547)), so the angle step of Cleveland & McGill's ranking is only part of the argument.
  - The UK Analysis Function allows a pie for up to five categories with one dominant share.
  - The rule still holds for this skill's pages, which mostly compare groups and need exact values. A single share is a sentence or a hero figure, and a split is a segmented bar with counts, which keeps one design for every whole on the page (P6).
- **Other ways:** a dot plot (0–100%) when visual comparison of one rate matters most; a bullet graph when there is a target; a sorted plain table. For more forms, look up the relationship (ranking, part-to-whole, change over time, distribution) in the [FT Visual Vocabulary](https://github.com/Financial-Times/chart-doctor/blob/main/visual-vocabulary/README.md).

## P4 · Color has one job

- **Goal:** Color guides the eye to meaning and means the same thing everywhere on the page.
- **Why it works:**
  - Color is preattentive: it pops out before conscious reading, so every colored element competes for attention ([NN/g](https://www.nngroup.com/articles/dashboards-preattentive/)).
  - Shading and color saturation rank last for reading amounts (Cleveland & McGill, P3).
  - About 1 in 12 men have a color vision deficiency, far more than women, and the most common type makes red and green hard to tell apart ([NEI](https://www.nei.nih.gov/learn-about-eye-health/eye-conditions-and-diseases/color-blindness)). Color is therefore never the only cue, and green is never used to grade.
  - The UK Analysis Function recommends at most four categories per chart as best practice ([colours](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-colours-in-charts/)) and asks for direct labels instead of legends where possible ([charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/)).
  - Using the same color for the same data across views is common practice: Bach et al. found this "shared color" pattern in about a third of the 144 dashboards they studied ([paper](https://arxiv.org/abs/2205.00757), [patterns](https://dashboarddesignpatterns.github.io/patterns.html)).
  - Why states and not groups: a page usually slices by several groupings (plan, channel, team), but has one set of outcomes. Coloring the outcomes keeps one meaning per color across every chart. Groups get color only where position and labels can't separate the marks (several lines, a scatter); that exception is a house rule, in line with the four-category limit above.
- **Other ways:** emphasis (one bar in the accent, the rest neutral) when the story is one group; grouping and position instead of color; texture fills for print.

## P5 · Ink only for data

- **Goal:** The data is the loudest thing on the page.
- **Why it works:** Tufte's data-ink ratio ([lecture notes](https://faculty.cc.gatech.edu/~stasko/7450/16/Notes/tufte.pdf)). The UK Analysis Function removes backgrounds, borders, legend boxes, shadows and 3D, and keeps gridlines light gray ([charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/)).
- **Other ways:** for grounding only, quiet it (muted ink) or move it to the details layer (P7) instead of deleting it.

## P6 · Same thing, same way

- **Goal:** The reader learns to read one block and can then read every block.
- **Why it works:** Tufte's small multiples: one design repeated, so the eye compares data, not formats. Bach et al.'s "shared color" shows the same idea in practice. One word per idea prevents "is this the same number?" questions.
- **Other ways:** small multiples (one mini chart per group, same scale); a fixed section template (title → finding line → chart → note).

## P7 · Overview first, details on demand

- **Goal:** The page stays short and calm without hiding anything.
- **Why it works:**
  - Shneiderman's mantra: "Overview first, zoom and filter, then details-on-demand" ([1996](https://drum.lib.umd.edu/handle/1903/5784)).
  - AWS Cloudscape orders a dashboard into bands by importance, suggests seven items as the limit for a chart, and keeps long lists off the dashboard ([static dashboard](https://cloudscape.design/patterns/general/service-dashboard/static-dashboard/)). IBM Carbon says a presentation dashboard shows the status of key metrics and strips away anything that could distract ([dashboards](https://carbondesignsystem.com/data-visualization/dashboards/)).
  - Few defines a dashboard as information arranged on a single screen. A scrolling page is a dashboard on top of a report; that trade-off is acceptable only if the first screen works on its own.
  - Analytics tools put filters in one row above the data they scope; Plausible, for example, puts filters and the date picker at the top ([Plausible](https://plausible.io/docs/guided-tour)). Linear Insights shows one measure by one slice per view, with an optional segment ([Linear](https://linear.app/docs/insights)).
- **Other ways:** tabs; an appendix section at the end of the same file; a print stylesheet that expands everything.

## P8 · Show where every number comes from

- **Goal:** The reader trusts the numbers and can defend them in a meeting.
- **Why it works:** The same metric name hides different calculations across tools (P2), so a written definition is what makes a number defensible. Real dashboards show this kind of information in Bach et al.'s "meta information" patterns: data source, disclaimer, data description, update information and annotations. An interpretation is only as good as the data behind it, so "Not in the data" names what the decision needs that the page doesn't have.
- **Other ways:** an "i" button that opens a definition on tap or click (never hover only); a cover note in the message that carries the file.

## Contrast

- WCAG requires at least 4.5:1 for normal text and 3:1 for large text (18pt, or 14pt bold) ([WCAG 2.2 Contrast (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)). This skill applies 4.5:1 at all sizes, as a stricter house rule: values and labels are small, and readers need them exact.
- Marks need at least 3:1 against their background, unless the same information is given as text ([Non-text Contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)). Hence: fills below 3:1 always carry their value beside the mark.
- Computed 2026-11-05 for the "no text on fills" rule: dark ink `#0b0b0b` on blue is 4.46:1; light ink `#f0efec` on the dark-mode fills is 2.96–3.38:1; white on any fill is 2.82–4.42:1. Pure black would pass but doesn't flip with the theme.
- Token contrasts in `SKILL.md` §6.1 are measured on `--surface`. On `--page` they are slightly lower (muted ink 4.85:1 in light mode). On `--wash-hl`, muted ink falls below 4.5:1, so only `--ink` and `--ink2` go there.

---

## Sources

✅ = read in full. The rest come from the paper's abstract, reviews, lecture notes or secondary summaries. URLs were checked on 2026-11-23.

**Experiments and research**
- Cleveland & McGill (1984), Graphical Perception, *JASA* 79(387): [doi](https://doi.org/10.1080/01621459.1984.10478080) (P3, P4)
- Heer & Bostock (2010), Crowdsourcing Graphical Perception, CHI: [doi](https://doi.org/10.1145/1753326.1753357) (P3)
- Spence & Lewandowsky (1991), Displaying Proportions and Percentages, *Applied Cognitive Psychology* 5(1): [doi](https://doi.org/10.1002/acp.2350050106) (P3, counter-evidence)
- Kosara (2019), Evidence for Area as the Primary Visual Cue in Pie Charts, IEEE VIS: [doi](https://doi.org/10.1109/VISUAL.2019.8933547) (P3, counter-evidence)
- Borkin et al. (2016), Beyond Memorability: Visualization Recognition and Recall, *IEEE TVCG* 22(1): [doi](https://doi.org/10.1109/TVCG.2015.2467732) (P1)
- Kong, Liu & Karahalios (2018), Frames and Slants in Titles of Visualizations on Controversial Topics, CHI: [pdf](https://zcliu.cs.umd.edu/vistitles/CHI18-VisTitles.pdf) (P1)
- Shneiderman (1996), [The Eyes Have It](https://drum.lib.umd.edu/handle/1903/5784) (P7)
- ✅ Bach et al. (2023), Dashboard Design Patterns, *IEEE TVCG* 29(1): [paper](https://arxiv.org/abs/2205.00757) · [pattern catalog](https://dashboarddesignpatterns.github.io/patterns.html), the catalog read in full (P0, P4, P6, P8)
- ✅ NN/g, [Dashboards and preattentive processing](https://www.nngroup.com/articles/dashboards-preattentive/) (P0, P1, P3, P4) · [F-shaped reading pattern](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/) (P0, P1)
- Few, *Information Dashboard Design*, 2nd ed., 2013, via reviews (P1, P7) · Tufte, via [lecture notes](https://faculty.cc.gatech.edu/~stasko/7450/16/Notes/tufte.pdf) (P0, P5, P6)
- National Eye Institute, [Color blindness](https://www.nei.nih.gov/learn-about-eye-health/eye-conditions-and-diseases/color-blindness) (P4)

**Standards and design systems**
- W3C, WCAG 2.2 [Contrast (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html) · [Non-text Contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)
- ✅ UK Government Analysis Function, [Charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/) · [Colours](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-colours-in-charts/) (P3, P4, P5)
- ✅ AWS Cloudscape, [Static dashboard](https://cloudscape.design/patterns/general/service-dashboard/static-dashboard/) (P7) · IBM Carbon, [Dashboards](https://carbondesignsystem.com/data-visualization/dashboards/) (P7)
- Plausible, [Guided tour](https://plausible.io/docs/guided-tour) (P7) · Linear, [Insights](https://linear.app/docs/insights) (P7)
- [Storytelling with Data](https://www.storytellingwithdata.com/blog/2020/3/5/transforming-slide-titles) · [think-cell](https://www.thinkcell.com/en/blog/how-to-tell-a-better-data-story-one-slide-at-a-time) (P1) · [FT Visual Vocabulary](https://github.com/Financial-Times/chart-doctor/blob/main/visual-vocabulary/README.md) (P3)
- `dataviz` skill reference palette and validator (bundled with Claude Code), run 2026-11-04 (color tokens)

**Same metric, different definitions**
- ✅ GitHub, [Interpreting Copilot metrics](https://docs.github.com/en/copilot/reference/copilot-usage-metrics/interpret-copilot-metrics) (P2) · DX, [Cursor adoption](https://docs.getdx.com/reports/cursor-adoption/) (P2)
- Google Ads, [About optimization score](https://support.google.com/google-ads/answer/9061546?hl=en) (P2)
