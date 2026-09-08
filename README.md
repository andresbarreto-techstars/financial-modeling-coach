# Financial Modeling Coach

A Claude skill that coaches a pre-seed or seed founder through building a **driver-based, monthly, cash-first financial model** — or reviews the one they already have — and hands back a workbook they can keep using without Claude, a scorecard of red and yellow flags, and a one-page summary.

**A test track for decisions — not a fundraising prop.** Every number in the model traces to a named input with a source. Growth comes from levers the founder can measure, never from a percentage. Spend can wait for the round by formula, so "what if the seed slips nine months" is one cell change. The model is built to be updated by the founder alone in under an hour a month.

## What it does

Trigger it whenever a founder mentions a financial model, projections, forecast, runway, burn, use of funds, unit economics, "a model for investors," how much to raise — or just says "can you look at my numbers" or "help me with the finance tab of the deck."

It works three ways:

| Starting point | What the skill does |
| --- | --- |
| No model, or a projection table typed into cells | Runs intake, picks the business-model archetype, walks the driver stack and cost lines in conversation, generates the workbook, and stress-tests it with you |
| An existing model | Extracts its assumptions, rebuilds them in the template so the integrity checks can run, compares inputs to the archetype's sourced benchmarks, and delivers findings as coaching |
| A folder of documents, no founder present (IC prep) | Renders the founders' plan faithfully from the record, marks every estimate "founder to confirm," reconciles figures that disagree, and produces the questions list |

The skill knows 41 pre-seed business-model archetypes across 11 verticals (software and marketplaces, aerospace and defense, healthcare, life sciences, fintech, energy and critical infrastructure, deep tech, physical AI and robotics, consumer products, AI services, cybersecurity). Each carries its driver stack, required cost lines, intake questions, red flags, and benchmarks with sources and dates. Anything outside the library is composed from a small set of revenue, cost, and timing primitives and flagged as such. Cap table, dilution, and valuation are out of scope by design; the model carries one cap-table number, post-round cash.

## What it produces

A workbook a founder can open in Excel or Google Sheets and keep using with nothing else installed:

    CompanyName_financial_model.xlsx
    ├── Guide           ← how to use the file: colors, scenarios, gated spend, monthly update
    ├── Assumptions     ← every input, named, with units and source; Base / Downside / Upside columns + Scenario dropdown
    ├── Drivers         ← the archetype's revenue engine, month by month
    ├── PnL             ← revenue, contra-revenue, COGS, gross margin (computed), OpEx, net income
    ├── Hiring          ← role-by-role plan; start months can wait for a financing event
    ├── Cash            ← beginning cash, burn, financing, ending cash, reconciliation check
    ├── WorkingCapital  ← (when the archetype needs it) receivable lag → cash collected
    ├── Assets          ← (when the archetype needs it) CapEx, depreciation, inventory, restricted cash
    ├── Summary         ← archetype checklist, runway, min cash, contribution per unit, use of funds vs deck, MODEL OK, three charts
    ├── Reference       ← the archetype library behind the dropdowns and lookups
    └── Actuals         ← dated metrics the model was calibrated to, for the monthly update

Plus a **scorecard** (red flags that would embarrass the founder in front of an investor, yellow flags with the benchmark and its source, questions for the founder, questions for the mentor) and a **one-page summary** in a fixed format that `investor-deck-builder`, `data-room-coach`, and IC skills can consume.

The workbook is generated, not hand-built: a JSON spec captured in conversation drives `generate_model.py`, LibreOffice recalculates it, and `check_model.py` runs structural and integrity checks (no hardcodes, row-consistent formulas, every input named and sourced, tie-outs hold) before anything is delivered.

## Install

Pick the option that matches your comfort level. All three end up at the same place — Financial Modeling Coach loaded into Claude.

| If you... | Use |
| --- | --- |
| just want to download a zip and click upload | [Option A — One-click zip](#option-a--one-click-zip-no-terminal-no-git) |
| are comfortable in the terminal and use Claude Code | [Option B — Claude Code plugin](#option-b--claude-code-plugin) |
| want to clone the repo and copy folders manually | [Option C — Manual git install](#option-c--manual-git-install) |

---

### Option A — One-click zip (no terminal, no git)

The easiest way. You'll download one zip file and upload it to Claude. No command line, no GitHub account, no git.

**Step 1 — Download the skill**

Go to the [latest release](https://github.com/andresbarreto-techstars/financial-modeling-coach/releases/latest) and download `financial-modeling-coach.zip`.

Direct link (always points to the most recent build):
<https://github.com/andresbarreto-techstars/financial-modeling-coach/archive/refs/heads/main.zip>

**Step 2 — Upload it to Claude**

Where you upload depends on which Claude product you're using:

**Claude.ai (web)**

1. Go to [claude.ai](https://claude.ai) and sign in.
2. Click your profile (bottom-left or top-right depending on the layout) → **Settings**.
3. Open **Capabilities** → **Skills** (the menu may also call it **Custom skills**).
4. Click **Add skill** (or **Upload skill** / **Create skill** / the **+** button).
5. Drag `financial-modeling-coach.zip` onto the upload area, or click to browse and select it.
6. Wait for the green checkmark / "uploaded" confirmation.

The skill is now available in any new conversation. To trigger it, just ask Claude something like *"help me build a financial model for my pre-seed round."*

**Claude desktop app / Cowork**

1. Open the Claude desktop app.
2. Open **Settings** (cog icon).
3. Go to **Plugins & Skills** (or **Capabilities**).
4. Click **Add custom skill** / **Upload skill** / the **+** button.
5. Drag `financial-modeling-coach.zip` onto the upload area, or click to browse and select it.
6. Confirm when it appears in your installed skills list.

**Step 3 — Update later**

When the skill gets updated, just come back to the [latest release page](https://github.com/andresbarreto-techstars/financial-modeling-coach/releases/latest), download the new `financial-modeling-coach.zip`, and re-upload it the same way. Claude replaces the old version.

> **Don't see a Skills / Plugins section in your settings?** Custom skill upload may not be available in every Claude plan or product yet. If that's you, try Option B or Option C, or check Anthropic's [help docs](https://support.claude.com) for the current way to add custom skills.

---

### Option A.5 — Manual zip from this repo (fallback if Releases is empty)

If the Releases page hasn't been built yet, or you prefer to grab files directly from the repo, follow this path. Slightly more steps than Option A but no command line.

1. On the repo's [main page](https://github.com/andresbarreto-techstars/financial-modeling-coach), click the green **Code** button.
2. Click **Download ZIP** at the bottom of the dropdown. This downloads the whole repo as `financial-modeling-coach-main.zip`.
3. Open the downloaded zip (double-click on Mac/Windows). You'll get a folder called `financial-modeling-coach-main`.
4. Inside that folder, find `skills/financial-modeling-coach/`. **This** is the skill — not the parent folder.
5. Compress just that `financial-modeling-coach` folder:
   - **Mac:** right-click `financial-modeling-coach` → **Compress "financial-modeling-coach"**. You'll get `financial-modeling-coach.zip`.
   - **Windows:** right-click `financial-modeling-coach` → **Send to** → **Compressed (zipped) folder**. You'll get `financial-modeling-coach.zip`.
6. Upload that `financial-modeling-coach.zip` to Claude using the steps in Option A → Step 2.

---

### Option B — Claude Code plugin

If you use [Claude Code](https://docs.claude.com/en/docs/claude-code), this is the cleanest path. The plugin auto-updates from this repo.

    /plugin marketplace add andresbarreto-techstars/financial-modeling-coach
    /plugin install financial-modeling-coach@financial-modeling-coach

To pick up the latest version later:

    /plugin marketplace update financial-modeling-coach

---

### Option C — Manual git install

For terminal users who prefer dropping the skill folder directly into their Claude skills directory.

    git clone https://github.com/andresbarreto-techstars/financial-modeling-coach.git
    cp -r financial-modeling-coach/skills/financial-modeling-coach ~/.claude/skills/

To update later:

    cd financial-modeling-coach
    git pull
    cp -r skills/financial-modeling-coach ~/.claude/skills/

## How to use it

Once installed, just ask Claude something like:

- "Help me build a financial model for my pre-seed round"
- "How much should I raise, and how long does it last?"
- "Review my model before I send it to investors"
- "What happens to my runway if the seed slips six months?"
- "My deck says $4M over 18 months — does the plan actually spend that?"
- "Build the finance section of my data room"

The skill diagnoses where you are — nothing yet, a model to review, or a folder of documents — identifies the business-model archetype the numbers describe, and coaches you through the drivers, the cost lines founders usually leave out (per-unit variable cost, compliance, capitalized or restricted cash, implementation per customer), the hiring plan, and the financing. You get the workbook, the scorecard, and the summary; then you flip the Scenario dropdown and start testing.

**The scripts need Python 3 with `openpyxl`, and LibreOffice for recalculation.** Claude runs them in its own environment when you use the skill through Claude.ai or Claude Code; you only need them locally if you want to run the generator or checker yourself (see `skills/financial-modeling-coach/scripts/README.md`).

## Repo layout

    financial-modeling-coach/
    ├── .claude-plugin/
    │   ├── plugin.json                       ← plugin manifest
    │   └── marketplace.json                  ← marketplace manifest
    ├── .github/workflows/
    │   └── release.yml                       ← auto-publishes the zip to Releases
    ├── skills/
    │   └── financial-modeling-coach/
    │       ├── SKILL.md                      ← entry point: intake, routing, build / review / record modes, scorecard and summary formats, rules
    │       ├── SCOPE.md                      ← what the skill does and does not do; the authority when in doubt
    │       ├── references/
    │       │   ├── conventions.md            ← spreadsheet conventions the generator applies and the checker tests
    │       │   ├── primitives.md             ← revenue engines, cost blocks, timing patterns; how to compose an unlisted archetype
    │       │   ├── buyer-profiles.md         ← sales cycle, payment terms, procurement, compliance by buyer type
    │       │   └── archetypes/
    │       │       ├── README.md             ← how the archetype files are structured; the four cross-cutting cost lines
    │       │       ├── software-and-marketplaces.md
    │       │       ├── aerospace-defense.md
    │       │       ├── healthcare.md
    │       │       ├── life-sciences.md
    │       │       ├── fintech.md
    │       │       ├── energy-critical-infrastructure.md
    │       │       ├── deep-tech.md
    │       │       ├── physical-ai-robotics.md
    │       │       ├── consumer-products.md
    │       │       ├── ai-services.md
    │       │       ├── cybersecurity.md
    │       │       └── drafts/               ← archetypes composed on demand, promoted after three sightings
    │       └── scripts/
    │           ├── README.md                 ← spec format, engines, checker output
    │           ├── generate_model.py         ← JSON spec → workbook
    │           ├── recalc.py                 ← LibreOffice recalculation (from Anthropic's xlsx skill)
    │           ├── check_model.py            ← structural, integrity, and value checks; founder-to-confirm list
    │           ├── run_scenarios.py          ← coach-side what-ifs the three scenario columns cannot express
    │           ├── make_broken_examples.py   ← regression set the checker must catch
    │           ├── office/soffice.py         ← LibreOffice helper
    │           └── examples/                 ← two worked specs and their generated workbooks
    ├── README.md
    └── LICENSE

## License

MIT — see [LICENSE](LICENSE).
