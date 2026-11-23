# Why these rules work

The evidence behind the rules in `SKILL.md`. Each principle gives its **goal**, **why it works**, and **other ways** to reach the same goal when the default rule doesn't fit.

---

## P0 · No bullshit: content, grounding, meaning

- **Goal:** Every element on the page helps the reader get the answer, trust it, or read it correctly.
- **Why it works:** Tufte's data-ink ratio extends from ink to words: an intro paragraph is non-data ink (P5). Readers scan and skip, so every extra element pushes the result away from where they look (P1). Anything colored or bold competes for preattentive attention (P4). Grounding is not an optional extra: it is its own pattern group in real dashboards (P8).
- **Other ways:** move grounding that only serves checking into "Definitions and data" or a collapsed detail.

## P1 · Lead with the answer

- **Goal:** The reader knows the main finding within about five seconds†, before reading a chart.
- **Why it works:**
  - A dashboard's job is to communicate critical information at a glance ([NN/g](https://www.nngroup.com/articles/dashboards-preattentive/); Few).
  - Scanning readers see the top and the first words of lines; the remedy is to put the key information first ([NN/g](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/)).
  - Titles drive memory. In an eye-tracking study of 393 visualizations, titles were among the most-read elements and improved recall of the message ([Borkin et al. 2016](https://vcg.seas.harvard.edu/publications/20150101-beyond-memorability-visualization-recognition-and-recall)).
  - Titles set the takeaway. In Kong et al.'s experiments, people shown the same chart with differently slanted titles reported the message of their title ([CHI 2018](https://mail.zcliu.cs.umd.edu/vistitles/CHI18-VisTitles.pdf)). Practitioners call these action titles ([Storytelling with Data](https://www.storytellingwithdata.com/blog/2020/3/5/transforming-slide-titles), [think-cell](https://www.think-cell.com/en/resources/content-hub/how-to-tell-a-better-data-story-one-slide-at-a-time)).
  - Kong et al. also found that readers take charts as neutral and believe a slanted title. So the finding line may only say what the numbers show: it states and compares, and never grades.
- **Other ways:** the finding sentence itself as the title (works when there are no filters, e.g. a print version); a callout next to the bar that proves the point; the finding as the lead sentence of the message that carries the file.

## P2 · Every rate shows its base

- **Goal:** Nobody misreads a rate, least of all on small groups.
- **Why it works:**
  - A percentage without its count hides how much evidence stands behind it: 100% of 2 looks better than 60% of 50.
  - Two rates over different bases look contradictory unless both bases are named.
  - Tools compute the "same" metric differently: GitHub Copilot and DX each define acceptance rate in their own way ([GitHub](https://docs.github.com/en/copilot/reference/copilot-usage-metrics/interpret-copilot-metrics), [DX](https://docs.getdx.com/reports/cursor-adoption/)), and Google Ads counts both applying and dismissing a recommendation as handling it ([Google](https://support.google.com/google-ads/answer/9061546?hl=en)). Naming the base removes the guesswork.
  - Below 10 cases, one case moves a rate by 10 points or more. Hence the small-n treatment, and the precision rule: never show more decimals than one case can move.
  - A rate that leaves cases out of its base can look better than reality (e.g. acceptance among those who answered, when many never answered). Show the related rate next to it.
- **Other ways:** counts as the main figure with the rate beside it; the base as its own table column; confidence intervals (only for readers who use statistical vocabulary).

## P3 · Show quantities as length and position

- **Goal:** Comparisons between groups are accurate and take no effort.
- **Why it works:**
  - Cleveland & McGill (1984) ranked how precisely people read visual encodings: position on a common scale first, then length, then angle and slope, area, volume, and color last ([paper notes](https://vis.pku.edu.cn/course/visclass_f25/material/Graphical_perception.pdf)).
  - NN/g applies this to dashboards: use bars, lines and dots; avoid pies, donuts, gauges, treemaps and 3D; sorted bars make ranking immediate ([NN/g](https://www.nngroup.com/articles/dashboards-preattentive/)).
- **Other ways:** a dot plot (0–100%) when visual comparison of one rate matters most; a bullet graph when there is a target; a sorted plain table. For more forms, look up the relationship (ranking, part-to-whole, change over time, distribution) in the [FT Visual Vocabulary](https://github.com/Financial-Times/chart-doctor/blob/main/visual-vocabulary/README.md).

## P4 · Color has one job

- **Goal:** Color guides the eye to meaning and means the same thing everywhere on the page.
- **Why it works:**
  - Color is preattentive: it pops out before conscious reading, so every colored element competes for attention ([NN/g](https://www.nngroup.com/articles/dashboards-preattentive/)).
  - Color is the weakest channel for amounts (Cleveland & McGill).
  - Part of every audience, mostly men, has a color vision deficiency, and red/green is the most common confusion pair. Color is therefore never the only cue.
  - Bach et al. found "shared color" (the same color for the same data across views) as a recurring pattern in 144 dashboards ([patterns](https://dashboarddesignpatterns.github.io/patterns.html)).
  - The UK Analysis Function caps a chart at four colors and asks for direct labels instead of color-matched legends ([charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/)).
- **Other ways:** emphasis (one bar in the accent, the rest neutral) when the story is one group; grouping and position instead of color; texture fills for print.

## P5 · Ink only for data

- **Goal:** The data is the loudest thing on the page.
- **Why it works:** Tufte's data-ink ratio ([lecture notes](https://faculty.cc.gatech.edu/~stasko/7450/16/Notes/tufte.pdf)). The UK Analysis Function removes backgrounds, borders, legend boxes, shadows and 3D, and keeps gridlines light gray ([charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/)).
- **Other ways:** for grounding only, quiet it (muted ink) or move it to the details layer (P7) instead of deleting it.

## P6 · Same thing, same way

- **Goal:** The reader learns to read one block and can then read every block.
- **Why it works:** Tufte's small multiples: one design repeated, so the eye compares data, not formats. Bach et al.'s "shared color". One word per idea prevents "is this the same number?" questions.
- **Other ways:** small multiples (one mini chart per group, same scale); a fixed section template (title → finding line → chart → note).

## P7 · Overview first, details on demand

- **Goal:** The page stays short and calm without hiding anything.
- **Why it works:**
  - Shneiderman's mantra: "Overview first, zoom and filter, then details-on-demand" ([1996](https://drum.lib.umd.edu/handle/1903/5784)).
  - AWS Cloudscape orders a dashboard into bands by importance, keeps charts to about seven items, and keeps long lists off the dashboard ([static dashboard](https://cloudscape.design/patterns/general/service-dashboard/static-dashboard/)). IBM Carbon says a presentation dashboard shows status and drops distractions ([dashboards](https://v10.carbondesignsystem.com/data-visualization/dashboards)).
  - Few defines a dashboard as a single screen. A scrolling page is a dashboard on top of a report; that trade-off is acceptable only if the first screen works on its own.
  - One row of filters above everything it scopes is the common pattern ([Plausible](https://docs.plausible.io/guided-tour)). So is one measure sliced by one dimension per view ([Linear Insights](https://linear.app/docs/insights)).
- **Other ways:** tabs; an appendix section at the end of the same file; a print stylesheet that expands everything.

## P8 · Show where every number comes from

- **Goal:** The reader trusts the numbers and can defend them in a meeting.
- **Why it works:** Bach et al.'s "meta information" pattern group (data source, disclaimer, data description, update information, annotations). And because the same metric name hides different calculations across tools (P2), a written definition is what makes a number defensible.
- **Other ways:** an "i" button that opens a definition on tap or click (never hover only); a cover note in the message that carries the file.

## Contrast

- Text needs at least 4.5:1 against its background, at every size used ([WCAG 2.2 Contrast (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)).
- Marks need at least 3:1, or the value is printed beside the mark ([Non-text Contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)).
- Computed 2026-11-05 for the "no text on fills" rule: dark ink `#0b0b0b` on blue is 4.46:1; light ink `#f0efec` on the dark-mode fills is 2.96–3.38:1; white on any fill is 2.82–4.42:1. Pure black would pass but doesn't flip with the theme.

---

## Sources

✅ = read in full on 2026-11-04. The rest come from abstracts, search summaries, reviews or lecture notes.

**Research**
- ✅ NN/g, [Dashboards and preattentive processing](https://www.nngroup.com/articles/dashboards-preattentive/) (P0, P1, P3, P4) · [F-shaped reading pattern](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/) (P0, P1)
- Borkin et al. (2016), [Beyond Memorability: Visualization Recognition and Recall](https://vcg.seas.harvard.edu/publications/20150101-beyond-memorability-visualization-recognition-and-recall) (P1)
- Kong, Liu & Karahalios (CHI 2018), [Frames and Slants in Titles of Visualizations on Controversial Topics](https://mail.zcliu.cs.umd.edu/vistitles/CHI18-VisTitles.pdf) (P1)
- Cleveland & McGill (1984), *Graphical Perception*, JASA 79(387): [lecture notes](https://vis.pku.edu.cn/course/visclass_f25/material/Graphical_perception.pdf) (P3, P4)
- Shneiderman (1996), [The Eyes Have It](https://drum.lib.umd.edu/handle/1903/5784) (P7)
- ✅ Bach et al. (2022), [Dashboard Design Patterns](https://dashboarddesignpatterns.github.io/patterns.html) (P0, P4, P6, P8)
- Few, *Information Dashboard Design*, 2nd ed., 2013, via reviews (P1, P7) · Tufte, [lecture notes](https://faculty.cc.gatech.edu/~stasko/7450/16/Notes/tufte.pdf) (P0, P5, P6)
- [Storytelling with Data](https://www.storytellingwithdata.com/blog/2020/3/5/transforming-slide-titles) · [think-cell](https://www.think-cell.com/en/resources/content-hub/how-to-tell-a-better-data-story-one-slide-at-a-time) (P1) · [FT Visual Vocabulary](https://github.com/Financial-Times/chart-doctor/blob/main/visual-vocabulary/README.md) (P3)

**Standards and design systems**
- W3C, WCAG 2.2 [Contrast (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html) · [Non-text Contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)
- ✅ UK Government Analysis Function, [Charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/) (P4, P5)
- ✅ AWS Cloudscape, [Static dashboard](https://cloudscape.design/patterns/general/service-dashboard/static-dashboard/) (P7) · IBM Carbon, [Dashboards](https://v10.carbondesignsystem.com/data-visualization/dashboards) (P7)
- Plausible, [Dashboard tour](https://docs.plausible.io/guided-tour) (P7) · Linear, [Insights](https://linear.app/docs/insights) (P7)
- `dataviz` skill reference palette and validator (bundled with Claude Code), run 2026-11-04 (color tokens)

**Same metric, different definitions**
- ✅ GitHub, [Interpreting Copilot metrics](https://docs.github.com/en/copilot/reference/copilot-usage-metrics/interpret-copilot-metrics) (P2) · DX, [Cursor adoption](https://docs.getdx.com/reports/cursor-adoption/) (P2)
- Google Ads, [About optimization score](https://support.google.com/google-ads/answer/9061546?hl=en) (P2)
