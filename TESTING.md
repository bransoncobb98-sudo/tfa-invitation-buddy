# Test report

**Tested:** 2026-10-09/10 · `index.html` (final build) · Windows 11, Claude in-app browser (Chromium), headless Microsoft Edge, Microsoft Word (Office 16)

**Method:** scripted checks run inside the live page against the real form controls and engine, plus external checks: `unzip -t`, Word COM automation, and Edge print-to-PDF. No Node, Python, pandoc, or LibreOffice were available, so Word and Edge were used instead.

## Summary

| # | Check | Result |
|---|---|---|
| 1 | Sample tournament (Congress, PF, World Schools, 2 IEs): conditional questions appear and hide | **Pass** |
| 2 | Uncheck events after answering: they vanish from every output | **Pass** |
| 3 | Required items block output; "Generate anyway" warns and unlocks; every spec validation fires | **Pass** |
| 4 | Blank optional fields leave no empty headings or labels | **Pass** (see note) |
| 5 | HTML uses only allowed tags and escapes `< > & "` | **Pass** |
| 6 | `.docx` is a valid ZIP and opens in Word; PDF print view paginates cleanly | **Pass** |
| 7 | Works with localStorage unavailable and available; light and dark mode | **Pass** |
| 8 | Accessibility: keyboard walkthrough, labels, contrast | **Pass** (see limits) |

## 1. Sample tournament: conditional questions

Required-only mode, driven through the real form controls (typing, clicks, radio buttons). Events: Public Forum, World Schools, Congressional Debate, Original Oratory, Dramatic Interpretation.

- Steps shown: Tournament basics, Events, Required disclosures, Congress options, Review. The detailed-only steps were hidden.
- Required disclosures showed C1–C7. C1 showed both the debate panel question and the IE panel question.
- C5 showed "resolution for Public Forum Debate" plus "World Schools Debate motions." It did **not** show Policy or LD.
- C7's "first draft" banner appeared after answering Yes. The detailed-only acknowledgments did not appear.
- Congress options showed D1 and D2. D2 did not ask for the declaration method in this mode.
- Detailed mode, same events: also showed E1–E10, the C1 panel size, C2's third option, the World Schools round table and elimination questions, the C7 acknowledgments, and the D2 method and deadline.
- An accessibility sweep turned on every conditional branch in both modes and visited every step. It found zero unlabeled controls, zero duplicate IDs and zero unnamed buttons.

## 2. Unchecking events

After answering World Schools and Congress questions, both events were unchecked. A search for "World Schools", "Congress", "Presiding", "docket" and the docket and motion text found **no matches** in any of these:

- the live preview,
- the checklist,
- the Tabroom HTML,
- the plain-text copy,
- the print/PDF view (`#print-root`),
- the DOCX `document.xml`.

Other results:

- The Congress options step disappeared.
- C1's sentence was rebuilt from the remaining checked events.
- Answers are kept, so re-checking an event restores them.

## 3. Blocking, "Generate anyway", and every validation

With C2's formula and C4 blank, Review showed "Final output is blocked" listing both items, and the export buttons were hidden.

1. "Generate anyway" opened a modal dialog naming both missing items.
2. Confirming unlocked export, and a note listed what is missing.
3. Creating a *new* problem (clearing C1) re-locked output.

Each validation was fired against a valid baseline (detailed mode, all events). The baseline itself had 0 blocks and 0 warnings.

| Spec item | Test case | Result |
|---|---|---|
| A1 blocks | name, host, start date blank | 3 blocks ✔ |
| A1 date window | July dates; Thanksgiving weekend 2026; 3rd Feb weekend 2027 | warning ✔ ×3 |
| A1 window (no warning) | last full Aug weekend 2026; 2nd full Feb weekend 2027 | no warning ✔ |
| B1 | no events; 2 events | block ✔; "at least four" warning ✔ |
| C1 | debate answer blank; panel size 4 | block ✔; odd-number warning ✔ |
| C2 | none chosen; Include with blank formula; "start of tournament" | block ✔; block ✔; warning ✔ |
| C5 | blank PF resolution; no impromptu WS prelim; multiple elims with no impromptu | block ✔ ×3 (spec wording) |
| C6 | semifinal session with no items; duplicate item across sessions; duplicate order number | block ✔; warning ✔ ×2 |
| C7 | unanswered; Yes with 2 of 4 acknowledgments | block ✔ ×2 |
| D2 | Yes with no declaration method (detailed) | block ✔ |
| E2 | Policy with 2 prelims | warning ✔ |
| E3 | uncovered-entry fee without acknowledgment; then acknowledged | block ✔; cleared ✔ |
| E4 | Round at 12:30 a.m. Saturday | midnight warning ✔ |
| E4 | 6 PF rounds on one day, 3-day tournament; same on a 2-day tournament | warning ✔; none ✔ (Requirements #26) |
| E5 | IE fee, no payment instructions | warning ✔ |
| E9 | bad email; name and email blank | warning ✔; block ✔ ×2 |

## 4. No empty headings

A detailed-mode invitation with all optional E-items blank had **no** Schedule, Entries and Fees, or Additional Information sections. A regex search for empty `<li>`, empty `<p>`, labels with no value, and headings followed directly by another heading found nothing.

Note: Judging, Awards and Qualification, and Logistics still appear. They hold the spec's on-by-default lines: the judge-graduation line, the qualification statement, and Tabroom.com as the tab software. These are defaults, not blank answers. See DECISIONS.md 3.11.

## 5. HTML safety

- Tournament name `Katy <Fall> Classic & "Swing"` came out as `Katy &lt;Fall&gt; Classic &amp; &quot;Swing&quot;`.
- Sweepstakes text containing `<b>bold?</b>` came out as literal text.
- `&` in resolutions was escaped.
- The built-in checker parses the output as XML and allows only `h2 h3 p ul ol li strong em a br table thead tbody tr th td`, with only `href` on links and `style` on table cells. The page reported: "Well-formed, and uses only allowed tags."
- The page loads nothing external. The only `src`/`href` resource is an empty `data:` favicon. A Content-Security-Policy blocks network requests.
- The footer TFA link uses `target="_blank" rel="noopener noreferrer"`.

## 6. Word and PDF exports

### .docx

The sample had headings, bullets, a nested list, two numbered docket lists, two tables, three hyperlinks (including one with `&` in the URL), the special-character title, and a control character in the notes.

- All 7 XML parts parsed as well-formed XML in the browser.
- `unzip -t sample.docx`: "No errors detected" (7 files).
- **Microsoft Word opened it with no repair prompt.**
  - Word found 95 paragraphs, 2 tables, 3 hyperlinks and 3 pages.
  - Headings use real Heading styles, and bullets are real Word lists.
  - Word then saved it to PDF, and the rendering was checked visually.
- The `.doc` fallback path exists but did not need to trigger.

### PDF (print view)

A large detailed invitation (10 events, 5-session docket, 14-row schedule) was printed to PDF with headless Edge, using the real print stylesheet.

- 6 pages, each with a "Page N of 6" footer.
- No form, buttons or page chrome were printed.
- Headings stayed with their content.
- The schedule table continued across a page break with its header row repeated.
- Rows were not split.

## 7. Storage and color modes

**localStorage unavailable:** the test pane loads local files as `data:` URLs, where storage is blocked. Every test above ran in that state.

- The yellow notice "Your browser is not letting this page save your answers…" appeared.
- Everything worked.
- A leave-page warning is active only in this state.

**localStorage available** (simulated with an in-memory stand-in):

- The notice was hidden.
- Answers, mode and step were restored on reload.
- "Clear all answers" opened a confirmation dialog, then erased everything and kept the current mode.

**Light and dark mode:** both themes were checked visually. Dark mode was applied by injecting the dark tokens, because the pane can't emulate dark mode for local files.

Contrast ratios, computed from the CSS tokens:

| Theme | Text pairs | Focus ring | Control borders |
|---|---|---|---|
| Light | 5.9–19.4 : 1 | 4.7 : 1 | darkened to pass 3 : 1 after the first check failed at 2.06 |
| Dark | 7.9–16.9 : 1 | 6.3 : 1 | darkened to pass 3 : 1 |

The header passes too: gold on royal blue is 7.4 : 1, and white on royal blue is 10.7 : 1.

## 8. Accessibility

Keyboard-only walkthrough with real key presses:

1. Tab moved through the controls in order, and every stop showed a solid focus outline.
2. Enter on Start entered the builder and moved focus to the step heading.
3. Space on a "Why?" button opened it (`aria-expanded="true"`).
4. Escape closed it and returned focus to the button.

Also in place:

- Radio groups are single Tab stops.
- Dialogs use native `<dialog>`, and focus returns to the trigger when they close.
- Copy and download confirmations go to an `aria-live` region and a visible toast.
- Tables collapse to labeled cards on phones.
- At 375px wide there is no horizontal scroll. The mode switch stacks, and Questions/Preview become tabs.

**Limits:** this was a scripted and keyboard audit, not a screen-reader session. Please do a quick pass with NVDA or Narrator, and on a real phone, before wide release.

## Retest after the 2026-10-10 changes (C1, C2, C6)

All checks were driven through the real form controls in required-only mode, with Public Forum, Congress, Original Oratory and Dramatic Interpretation checked.

**C1: judge panels**
- The new question wording appears.
- The debate dropdown lists exactly: Semi-Finals, Quarters, Octos, All Elim Rounds, All Rounds (including prelims), Other.
- Choosing Other shows a text box, and its text prints in the invitation.
- IE **No**: no dropdown appears, and the Requirement #19 disclosure prints, naming only the checked IEs.
- IE **Yes**: the dropdown appears. "All Elim Rounds" prints "…in all elimination rounds in Original Oratory and Dramatic Interpretation."
- Both blank questions block output with the new messages.
- Detailed mode: the panel size prints ("Panels of 4 judges…") and the even-number warning still fires.

**C2: Tabroom option**
- Choosing "Listed on our Tabroom page" shows the optional field.
- Blank field: prints the sentence without a location.
- Filled field (`the "Sweepstakes & Awards" page`): the location is added, with `"` and `&` escaped.

**C6: docket boxes**
- There is one docket box per session (Prelim 1, Prelim 2, Finals).
- An empty session blocks output ("Enter the legislation docket for Finals.").
- Several lines print as a numbered list; a single line prints as a paragraph.

**Exports**
- The HTML check passes.
- All DOCX XML parts parse.

## Retest after adding features from the sample invitations (2026-10-10)

The test case was a detailed-mode Foster-style swing: PF, World Schools, Congress, USX, DI and OO, with every new field filled in.

**Output**
- No script errors.
- Steps shown: Tournament basics, Welcome letter, Events, Required disclosures, Congress options, Event details, Schedule/fees/judging/awards, Logistics/policies/contact, Review.
- Sections came out in the expected order: the welcome block (no heading) first, then Eligibility and Policies placed between Logistics and Contact.
- All 13 new pieces of output appeared, including:
  - swing description and bid details,
  - the three new deadlines,
  - Other Events and Divisions,
  - the host-ineligible sweepstakes line,
  - debate break policy,
  - IE format and extemp topics,
  - per-event fees, discounts, late payments and caps,
  - judge expectations and missed-round fine,
  - eligibility statements citing Requirements #14.
- Typed URLs became links, and trailing periods were left outside the links: `https://example.org/pizza`, `https://example.org/pay`, `https://forms.gle/abc123`.

**Validation**
- A missed-round fine with no acknowledgment blocked output. Checking the acknowledgment cleared it.

**Required-only isolation**
- With the same answers, required-only mode output had only Tournament Information, Events Offered and TFA Required Disclosures.
- None of the new text leaked in (swing description, NIETOC detail, other events, letter, sweepstakes line, IE patterns, #14 statement, new deadlines, pizza update).

**Exports**
- The HTML check passes.
- All DOCX parts parse.
- The plain-text copy omits the empty welcome heading.

**Section Copy buttons**
- Ten buttons appear on Review, one per section.
- Clicking one in the test pane showed the "Copy failed" fallback message, because that pane blocks clipboard access for scripted clicks.
- The section HTML itself was checked directly.
- **Real clipboard copying should be confirmed in a normal browser.**

## Not tested here

- **Pasting into Tabroom's editor.** The HTML is deliberately simple, but this hasn't been confirmed. See the README.
- ~~Real-browser localStorage over `https://`~~: **confirmed** on the live GitHub Pages site (2026-10-10). Storage works and the "not saving" notice stays hidden.
- **Safari and Firefox.** Only Chromium-based browsers were tested.
