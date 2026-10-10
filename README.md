# TFA Invitation Buddy

**Answer a few questions, and get a rules-ready tournament invitation you can paste into Tabroom.**

> **Disclaimer:** TFA Invitation Buddy is an independent tool. It is not affiliated with, endorsed by, or sponsored by the Texas Forensic Association. It is provided as a convenience, does not constitute official guidance, and does not guarantee compliance. The tournament host is responsible for making sure the invitation and tournament follow the current TFA rules.

## What it does

Schools hosting a TFA Invitational Qualifying Tournament (IQT) answer a guided questionnaire. The tool builds an invitation that you can:

- copy as HTML to paste into Tabroom.com,
- copy as formatted text,
- download as an `.html` file,
- print or save as a PDF,
- download as a Word `.docx` file.

There are two modes, switchable at any time from the **Builder mode** switch at the top of the page. Your answers are kept when you switch.

| Mode | What you get |
|---|---|
| **TFA Required Information Only** | Tournament basics (name, host school(s), swing, dates, qualification offered), an optional Events Offered list, and only the disclosures the TFA Constitution requires on an IQT invitation: judge panels, sweepstakes formula, power-matching, bracket breaking, debate topics, Congress docket, and host-school eligibility. If you offer Congress, it also includes the per-item limit and Presiding Officer statements when you use those options. |
| **Detailed Invitation Builder** | A complete invitation: everything above, plus a welcome letter and dated updates, bid and swing details, the full deadline set, other (non-TFA) events and divisions, schedule, per-event fees and policies, judging expectations, awards and qualification points, debate and IE format (including extemp topic areas), eligibility and tournament policies, logistics, contacts, and additional information. These fields were modeled on several well-regarded Texas invitations. |

How it works:

- **Events:** only the events you check appear anywhere: in questions, the preview, the checklist, and every export.
- **Checklist:** the Review step lists each required disclosure as Pass or Needs attention, with a link back to the question.
- **Blocking:** final output is blocked until required items are answered, unless you choose **Generate anyway** after a warning that names what is missing.
- **Privacy:** everything runs in your browser. Nothing is sent anywhere: no server, no analytics, no external requests. Answers are autosaved in your browser's local storage when it's available. Use **Clear all answers** at the bottom of the page to erase them.
- **Offline:** the tool is one file, `index.html`, and works offline once loaded.

## Pasting into Tabroom

**Check Tabroom's handling of the HTML before you publish.** The tool's HTML output uses only simple tags (`h2`, `h3`, `p`, `ul`, `ol`, `li`, `strong`, `em`, `a`, `br`, and basic tables with inline borders). However, it has **not** been verified against Tabroom's editor.

1. In Tabroom's invitation editor, switch to **HTML / source mode**.
2. Paste the HTML from **Copy HTML**.
3. Switch back and check Tabroom's preview before publishing.

If you post parts of the invitation on separate Tabroom pages (for example "Judge Information" or "Debate Topics"), use the per-section **Copy** buttons on the Review step.

If Tabroom strips or changes something, the HTML renderer is one small, isolated function (`toTabroomHTML` and the `TAB` style constants in `index.html`), so it's easy to adjust.

## Deploy on GitHub Pages

1. Install Git and create a free GitHub account if you don't have them.
2. In this folder, run:
   ```bash
   git init
   git add index.html README.md DECISIONS.md TESTING.md
   git commit -m "TFA Invitation Buddy"
   ```
3. On GitHub, click **New repository**, name it (for example `tfa-invitation-buddy`), leave it empty (no README), and create it.
4. Connect and push. Replace `YOUR-NAME` with your GitHub user name:
   ```bash
   git branch -M main
   git remote add origin https://github.com/YOUR-NAME/tfa-invitation-buddy.git
   git push -u origin main
   ```
5. In the repository on GitHub, go to **Settings > Pages**. Under **Build and deployment**, choose **Deploy from a branch**, then select **main** and **/ (root)**, and click **Save**.
6. After a minute or two, the site is live at `https://YOUR-NAME.github.io/tfa-invitation-buddy/`.

You can also open `index.html` directly from your computer; no server is needed.

## Updating the rules each year

All rule content lives at the top of the `<script>` in `index.html`, above the line `END OF CONFIGURATION`. You should not need to touch the engine or renderers below it.

| What changed | Where to edit |
|---|---|
| Rules version (footer and About text) | `CONFIG.rulesVersion` and `CONFIG.rulesVersionAbout` |
| Disclaimer, tagline, TFA link | `CONFIG.disclaimer`, `CONFIG.tagline`, `CONFIG.tfaUrl` |
| Events (add, rename, regroup) | `CONFIG.events`. Each event's flags (`panel`, `topic`, `ws`, `congress`, `prelims`, `minPrelims`, `fee`, `minEntries`) decide which questions it switches on. |
| Minimum entries, minimum schools, minimum events | `minEntries` on each event; `CONFIG.minSchoolsForPoints`; `CONFIG.minEvents` |
| IQT date windows | `CONFIG.iqtWindows` |
| Rounds-per-day limit | `CONFIG.maxRoundsPerDay`, `CONFIG.maxRoundsMinDays` |
| Question wording, help, "Why?" text, citations | the matching entry in `RULES` (`title`, `help`, `why`, and each field's `label`) |
| Validation messages | the question's `required:` strings and its `validate()` function |
| Output wording | the question's `output()` function |
| Section order in the invitation | `SECTIONS` |
| Form steps | `STEPS`, plus each question's `step` |

After editing, open `index.html` and walk through both modes. Check that the Review checklist and preview look right.

## Verifying citations against the Constitution

Every "Why?" tooltip quotes its citation (for example "IQT Manual, Requirements #19 and #25a (pp. 101–102)"). To check them against a new Constitution:

1. Open the current Constitution PDF from texasforensicassociation.com.
2. Most invitation rules are in **Standing Rules: Invitational Qualifying Tournament** (in the 2026 edition: "Hosting an IQT" p. 96–98, "Qualifying Numbers" p. 98, "Requirements" p. 99–102; item 25 lists what must be on the invitation).
3. Congress items are in **Congressional Debate** rules 3.l, 3.m, and 4.e (pp. 76–77) and **Congressional Debate Tabulation, Presiding Officers** (pp. 108–109).
4. Power-matching and bracket rules are in **Debate Tabulation** (p. 105) and **World Schools Tabulation** (p. 112).
5. For each question in `RULES`, search the PDF for the rule's key phrase. Confirm the item number, page, and wording, then update `why` and `CONFIG.rulesVersion`.

`DECISIONS.md` lists the places where the spec and the 2026 Constitution differ and how each was handled.

## Files

- `index.html`: the whole tool (inline CSS and JavaScript, no dependencies)
- `DECISIONS.md`: assumptions, defaults used, and spec/Constitution conflicts
- `TESTING.md`: the test report
