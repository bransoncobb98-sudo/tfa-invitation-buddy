# Decisions and open items

This file records every place where something was not decided in the Q&A spec, plus how conflicts between the spec and the **2026 TFA Constitution (revised Oct 2025)** were handled. Please review, and change anything you disagree with.

## 1. Decisions you made (2026-10-09)

| Topic | Your decision | How it's built |
|---|---|---|
| Scope | Add a toggle between **TFA Required Information Only** and **Detailed Invitation Builder** | A "Builder mode" switch in the header and on the start screen. Answers are shared between modes. Each mode shows and outputs only its own questions. |
| Required-only content | Only the 9 items in your table (C1–C7 required; D1–D2 conditional) | Spec "extras" are **detailed-mode only**: the C1 panel size and even-number warning, the C2 "no sweepstakes" option and warning, the C3 reminder, the C4 method sentence, the C5 World Schools impromptu checks and elimination questions, the C6 duplicate warnings and "debated in order" line, the C7 acknowledgments and safeguards, the D1 "no limit" switch, and the D2 declaration method and deadline. |
| Basics in both modes | Required: tournament name, host school(s), swing box, dates, and qualification checkboxes (TFA, TOC, NIETOC, NCFL) | Host schools are a list (add as many as you need). Name, at least one host, both dates, and at least one qualification box are required (they block output). |
| Events list in required-only mode | Give the option to include it | Checkbox "Include an 'Events Offered' list in my output", **on by default**. Detailed mode always includes it, as the spec says. |
| Tagline | Keep as written | Unchanged. |
| Look and feel | Make it look more like TFA | Uses a palette drawn from Texas forensics colors (royal blue, gold, flame orange, red, black, steel blue) and a slab-serif display font. **No TFA logo or official marks are used**, and the disclaimer stays on every screen. Your original brief said "Do not use TFA's logo or anything that looks official." I kept the no-logo part. If you want the logo, check with TFA first. |

### Changes you requested on 2026-10-10

| Item | Change |
|---|---|
| C1 debate | The question now reads "In debate events, what is the first round you guarantee to use judge panels?" The dropdown offers Semi-Finals, Quarters, Octos, All Elim Rounds, All Rounds (including prelims), or Other. Other opens a text box. Output example: "Judge panels will be used beginning in quarterfinals in Public Forum Debate." There is no longer a "single judges throughout" answer; hosts can say that through Other. |
| C1 individual events | The question now reads "Will you use judge panels in Individual Events prior to the finals round?" **No** prints: "Per the TFA Constitution (Requirement #19), we disclose that judge panels will be used in the finals of all TFA individual events offered: [checked IEs]." **Yes** shows the same round dropdown and Other box. See the note below. |
| C2 | New option: "It is listed on our Tabroom page," with an optional "Which Tabroom tab or page?" box. Output: "The sweepstakes formula is posted on this tournament's Tabroom page[, under X]." |
| C6 | Each session (each prelim session, semifinals, finals) now has one box where the host types the legislation docket for that round, one item per line, in debate order. Several lines print as a numbered list; a single line (for example "Fall Docket items 6–10") prints as a sentence. The item table and order-number column were removed, so the "duplicate order number" warning is gone. The "same item in more than one session" warning remains (detailed mode). |

### Additions learned from five sample invitations (2026-10-10)

Sources: Churchill Classic (2026 and 2027 editions), Clear Creek Classic, and the Foster–Summer Creek swing (two Tabroom pages). **Everything below is Detailed-mode only, so Required-only mode is unchanged.** None of these is a TFA rule except where a citation is given.

| Where | Added |
|---|---|
| New **E11** (own step, "Welcome letter") | "Last updated" note; Important Updates (one per line, at the top); welcome letter; signatures. This prints under the tournament name with no section heading. |
| A1 | Swing description (shown when Swing is checked); bid and qualifier details (shown when TOC, NIETOC, or NCFL is checked); Registration opens, Fees freeze, and Judge information due, alongside the entry and drop deadlines. |
| B1 | "Other events or divisions" (Novice LD/PF, Prose, Poetry, Impromptu…). These print under "Other Events and Divisions" but **do not** count toward the four-event minimum or trigger any TFA question. |
| C2 | Optional "host school(s) are not eligible for sweepstakes" line. |
| E2 | "How will debate entries advance to elimination rounds?" (for example, break to the highest level of guaranteed TFA points). |
| New **E12** "Individual events format" (shown when any IE is checked) | IE prelim count, elimination rounds, cross-entry patterns (Section A/B), and extemp topic areas by round (shown when USX or IX is checked). "Why?" cites Requirements #5 and #7. |
| E3 | Judge expectations (paradigms, staying one round past elimination); missed-round (no-show) fine; link for people who want to be hired. **A no-show fine now also triggers the judging-fee acknowledgment**, because it is a judging-related charge (Requirements #15). |
| E5 | "Separate fee for each event" switch (World Schools often costs more); fees for other events; discounts; late-payment policy; entry caps and waitlist. |
| New **E13** "Entry eligibility and tournament policies" | Optional standard statements: Texas affiliation with no Texas mavericks (**Requirements #14, p. 100**), and an adult school representative on site. Optional text for out-of-state/independent entries, novice definition, middle school entries, late-arrival/forfeit policy, and campus rules. Printed as a new "Eligibility and Policies" section after Logistics. |
| All modes | Web addresses typed in any answer become links (http/https only). The Review step has a **Copy button for each section**, for hosts who post judging, topics, or policies on separate Tabroom pages. |

Found while reading: the Churchill invite cites "TFA Constitution pg 72" for the affiliation rule. In the 2026 Constitution it is **Requirements #14, p. 100**. The tool cites #14.

Considered and left out: an automatic table of contents (Tabroom HTML can't link within a page), and a structured sweepstakes points table (free text already handles every format seen).

**Note on the C1 "No" wording.** Requirement #19 requires IQTs to *disclose* whether panels are used in IE finals. It does not require IQTs to use them. (Panels of 3+ in all elimination rounds is a **State Tournament** rule, Judging 1, p. 123.) So the sentence says the host is disclosing *per* the Constitution, not that the Constitution requires the panels. It also lists only the IEs you checked, so unchecked events never appear.

## 2. Spec "Open decisions" you didn't answer: the spec's defaults were used

| Item | Default used |
|---|---|
| C1 | Keep the panel-size follow-up and the even-number warning (detailed mode). |
| C2 | Keep "will not award sweepstakes" (detailed mode only) and the warning as written. |
| C3 | Keep the plain-language definitions of high-high and high-low. **Please confirm they match TFA usage.** |
| C4 | Answer is required (blank does not silently print "will not be broken"). |
| C5 | No "topic change" note. |
| C6 | No paste-a-docket feature. |
| C7 | Safeguards are listed in the invitation by default (detailed mode; switchable). |
| D1, D2 | "No" prints nothing. D1 has an optional "State that there is no per-item limit" switch, off by default (detailed mode). |
| Section order | As in "General output rules." |
| E6 | Keep the qualification-points statement (on by default) and the optional minimum-entries list. The numbers live in `CONFIG.events[].minEntries`. Whoever maintains the tool should re-check them each season. |
| E10 | Both standard statements are optional checkboxes, unchecked by default. |

Spec "notes" questions that had no stated default (I chose the option that adds the least):

- B1: no reminder about separate men/women or pre-qualified divisions.
- D2: no "qualification speech of up to one minute" sentence.
- E2: no preliminary-round count for individual events.
- E4: one schedule table, not one per day.
- E5: no other fee formats (per round, per student).
- E8: no extra fields.

## 3. Judgment calls where the spec was silent or unclear

1. **A1 date-window warning.** Hosting item 3 defines a "full calendar weekend" as Fri–Sat–Sun in one month, and a "tournament weekend" as Wednesday–Tuesday.
   - Each window runs from the **Wednesday before** its first allowed weekend to the **Tuesday after** its last one.
   - The **Wednesday–Tuesday week around the weekend after Thanksgiving** is excluded.
   - The spring window starts with the first full weekend whose Friday is January 2 or later ("following January 1").
   - Detailed mode only. It warns but does not block. The tool can't know the TSCA Convention dates.
2. **E4 schedule checks.**
   - The Day column is a dropdown of the dates in your A1 range.
   - The Event column is a dropdown of your checked events.
   - A row counts as a **round** when it has an event and its Activity contains a word like round, prelim, octo/octa, quarter, semi, final, elim, or session.
   - "After midnight on Friday or Saturday" means a round row on a **Saturday or Sunday between 12:00 and 5:59 a.m.**
3. **E4 5-rounds-per-day warning** fires only when the A1 dates span **three or more calendar days**, because Requirements #26 applies only to tournaments "over three calendar days." The spec's warning had no such condition.
4. **C5 World Schools (detailed mode).** The spec asked for both a Round/Motion table and a separate count of impromptu rounds, and those could disagree. Instead, each round row has a Prepared/Impromptu choice, and the impromptu count is worked out from the rows and shown.
   - Multiple elimination rounds: you check which of Octafinals, Quarterfinals, Semifinals, or Finals are impromptu.
   - Required-only mode: World Schools motions are a simple one-per-line list, with no impromptu checks.
5. **"Generate anyway"** unlocks output for whatever is missing at that moment. If a *new* problem appears later, output locks again.
6. **Disclosures section layout.** Subheadings in this order: Judge Panels (C1), Sweepstakes (C2), Power-Matching and Brackets (C3, C4, E1), Debate Topics (C5), Congressional Debate Docket (C6, then D1, D2), Host-School Students (C7), Cross-Entries and Event Format (E2).
7. **Deadlines are free text** ("Enter dates and deadlines exactly as you want schools to read them"). The D2 declaration deadline is therefore text too, pre-filled from the A1 entry deadline. The spec said "date picker."
8. **Format option** is labeled "Hybrid" instead of "Hybrid (swing)", because swing is now its own checkbox.
9. **A1 output.**
   - Virtual or hybrid access instructions are printed after the platform. The spec asked for them but its output wording left them out.
   - Swing prints "This is a swing tournament."
   - Qualification prints "Qualification offered: TFA and TOC."
   - **Please review both wordings.**
10. **Multiple host schools.** C7 asks once for all hosts. The eligibility sentence and safeguards name every host school.
11. **On-by-default lines create sections.** These spec defaults print even when nothing else in their section is filled in, so those sections are never empty:
    - E3: the judge-graduation line, which creates the Judging section.
    - E6: the qualification statement, which creates Awards and Qualification.
    - E7: Tabroom.com as the tab software, which creates Logistics.

    Hosts can switch each one off.
12. **E4 output.** When a row has an event, the event name is added after the activity, for example "Round 1 (Public Forum Debate)".
13. **Heading levels.** Tabroom output may only use `h2` and `h3`:
    - Tournament name and section titles are `h2`.
    - Subsections are `h3`.
    - Third-level headings (World Schools, Congress session names) are bold paragraphs.

    In Word they map to Title, Heading 1, Heading 2, and Heading 3.
14. **Minimum entries wording.** Duo and Duet show "10 teams," and World Schools shows "6 teams" (World Schools rule 11). All other events show "10 entries."
15. **Links.** Email addresses become `mailto:` links. A registration answer that is a web address becomes a link. Only `http(s)` and `mailto` links are ever written.
16. **Optional footer line.** "Invitation prepared with TFA Invitation Buddy." It is **on by default**, and you can switch it off on the Review step. The invitation body carries no other branding.
17. **"Why?" text in required-only mode.** For C5 and C6, it cites only the table's sources (#25e; #25f and Congress 4.e). The longer detailed-mode text also cites World Schools and Congress 3.m rules that aren't part of that mode.

## 4. Spec vs. 2026 Constitution: conflicts and clarifications

| # | Where | What the Constitution says | What the spec says | What I did |
|---|---|---|---|---|
| 1 | C7 acknowledgment #4 | Requirements #18: "At least two schools must compete for the **tournament's** entries to receive IQT points." | "at least two schools will compete in **each event**." | **Kept the spec wording.** Please decide whether to match #18. |
| 2 | E4 rounds per day | Requirements #26 applies to IQTs that take place "over three calendar days." | Warning had no three-day condition. | Warning fires only for 3+ day tournaments (see 3.3). |
| 3 | E2 prelim minimum | World Schools rule 12 (p. 74): IQTs must offer at least 3 prelim rounds (one impromptu), plus minimum breaks by entry count. | E2 warning covers only Policy, PF, and LD (Requirements #8). | Left as the spec has it; World Schools is **not** in the warning. Tell me if you want it added. |
| 4 | C4 and World Schools | World Schools Tabulation, Elimination brackets 1: "Follow the same procedures as LD, Policy, and PF above." | Spec asked whether C4 applies to World Schools. | Confirmed it does. C4 shows for World Schools. |
| 5 | C6 "Why?" citation, Congress 3.m | 3.m says items are debated in the order stipulated by the host "on their **IQT webpage**." Tabulation (p. 109) says "the invitation will specify the order." | Cites 3.m for invitation debate order. | Citation kept (p. 109 supports it). Noted here because 3.m itself says "webpage," not "invitation." |
| 6 | C3 strength | Debate and World Schools Tabulation: tournaments "**should** announce" the method; Requirements #25c lists it among "information **required**" on the invitation. | Required. | Kept Required (#25c). |

All page and item numbers cited in the spec matched the 2026 PDF, including the corrected E1 citation (Hosting item 12, p. 98).
