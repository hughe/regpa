# ReGPA — The Recalculation Desk

Admissions offices rarely use the GPA printed on your transcript. They rebuild it —
dropping courses, stripping your school's weighting, and adding their own. Enter a
transcript once and see what each published formula makes of it.

**Live:** https://hughe.github.io/regpa/

One static HTML file and its fonts. No build step, no dependencies, no server, no
analytics, and no third-party requests — everything you type stays in your browser.

## A warning

**This was vibe coded.** An AI wrote it, a human has tested it lightly, and it may or may
not do what it claims. Don't rely on it for anything. Every formula card links to the
office's own published rule — check any number that matters against that.

## What it computes

Seventeen figures from the same coursework. Each is implemented from the office's own
published description, linked on its card in the app.

| Formula | Rule |
|---|---|
| Unweighted 4.00 | Every course, plus/minus counted. The floor to measure the rest against. |
| Core unweighted | Five academic areas on a flat 4.0 scale, no rigor bonus. The shape attributed to many selective privates — no college publishes it, so it carries no source. |
| Core unweighted, no freshman year | The same core over 10th–12th. Rumoured of several selective privates; nobody publishes it. The gap from the row above is what 9th grade is worth. |
| Typical school weighting | Every course, +1.0 advanced / +0.5 honors. Shown for contrast — no authority behind it. |
| [UC](https://admission.universityofcalifornia.edu/admission-requirements/first-year-requirements/gpa-requirement.html) capped weighted | a–g only, 10th–11th only, +1 per honors **semester**, capped at 8 with at most 4 from 10th grade. |
| UC fully weighted | Same courses, cap lifted. |
| UC unweighted | Same courses, no honors points. |
| [Cal State](https://www.calstate.edu/apply/eligibility-index) | a–g, 10th–**12th**, 8 honors semesters with at most **2** from 10th. |
| [University of Georgia](https://admissions.uga.edu/admissions/first-year/first-year-admission-criteria/) | Five core areas, all years, **+1.0 for AP and IB only** — nothing for honors or dual enrollment. |
| [Georgia Tech](https://admission.gatech.edu/first-year/academic-preparation) | Core only, +0.5 for AP, IB, dual enrollment, A-Levels. |
| [HOPE / Zell Miller](https://www.gafutures.org/hope-state-aid-programs/hope-zell-miller-scholarships/hope-scholarship/understanding-the-high-school-hope-gpa/) | Core 9th–12th, school weighting stripped, +0.5 for AP/IB/DE — but nothing above 4.0, so only B and below can gain. |
| [University of Florida](https://admissions.ufl.edu/apply/freshman/our-decision-process) | Core plus any AP/IB/AICE, +1.0 advanced / +0.5 honors and pre-. |
| [UCF](https://www.ucf.edu/admissions/undergraduate/question/how-competitive-is-it-to-get-accepted-into-ucf/) | Academic core, same two tiers. |
| Bright Futures | 16 core credits, a flat +0.5 per weighted year-long course. |
| [TOPS](https://www.osfa.la.gov/schgrt6a37.htm) (Louisiana) | Core curriculum on a 4.0 scale, but advanced courses are graded out of 5 and rescaled proportionally — a C in honors is 2.40, an A gains nothing. |
| [NCAA Division I](https://www.ncaa.org/eligibility-center/initial-eligibility-requirements/division-i/) | Best 16 core units, unweighted, no plus/minus. The test-score sliding scale was dropped in 2023. |
| Ivy Academic Index | Reconstructed, **not a published formula**. Marked ★ unverified in the app. |

Cards marked **★ unverified** reflect a practice attributed to colleges that publish no formula; every other card links to the office's own rule. The footer lists published formulas that were found but deliberately not modelled — South Carolina's Uniform Grading Policy, Iowa's Regent Admission Index, Georgia's Freshman Index, Cal Poly's MCA and Harvard's reader ratings — with the reason for each.

The differences are not cosmetic. On the sample transcript the same coursework reads
anywhere from **3.58 to 4.42** depending on who is holding it.

## Using it

**Enter the transcript.** One row per course: subject, level, grades, and which year of
high school it belongs to. Grades go in per semester — leave **S2** on `(year)` where the
transcript shows one mark for the whole year, or `(none)` where the second semester has
not been graded yet.

**Grades in hand.** Set the cut-off to the last year you have marks for. Everything
recomputes on that slice, and each card shows its running value at every earlier year;
hover a point on the sparkline for the figure and the change. A formula whose window has
not closed is flagged *provisional* — UC's window is 10th–11th, so a GPA computed after
9th grade is not a UC GPA at all, and the card says so instead of showing a number.

**Save File / Load File.** Writes the whole state — name, courses, residency, SAT, cut-off
— as `[Name]s-GPA-[YYYYMMDD].json`, and reads it back. Nothing is uploaded anywhere; the
file lands in your downloads folder and stays on your machine. Use this rather than
keeping a real transcript in the page source.

**Print.** A print stylesheet turns the page into a one-column document: course rows
collapse to one line, controls flatten to the values they hold, and a dateline carries the
name and the date. About four pages.

## What it can't do

- Decide whether your school's "Honors" section is *UC-certified*, or your dual-enrollment
  course *degree-level*. Both change the answer and neither is knowable from a grade.
- Know which of your courses sit on your state's approved list.
- Reproduce the reader who looks at your transcript next to your school's profile and
  never reduces it to one number. Highly selective private colleges mostly do that.

Course-count requirements (UF's 16 academic units, Bright Futures' 16 credits, NCAA's
distribution rule) are not checked — only the GPA arithmetic is. Plus and minus grades are
used only in the baseline rows; every recalculation here discards them, as their
published rules specify.

These formulas change. Check the linked source before relying on a number.

## Running it locally

```sh
git clone https://github.com/hughe/regpa
open regpa/index.html
```

That is the whole thing. `index.html` plus `fonts/` — the three typefaces are served from
this repo rather than a CDN, so the page calls nothing outside itself and works offline.

## Publishing

GitHub Pages serves this repo's root as-is. **Settings → Pages → Source: Deploy from a
branch → `main` / `/ (root)`.** There is nothing to build.

Note that a Pages site is publicly readable even when the repository is private, so keep
real transcripts out of the committed source and load them from a JSON file instead.

## License

MIT — see [LICENSE](LICENSE).
