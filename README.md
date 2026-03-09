
# [-> Click Here for Block Chain Dev List Concepts Demo <-](https://openresearchcommunicationsystem.github.io/Proof_Of_Concept-BlockChain-DevList-Tools/)

# Blockchain Forensics: Discover Once/Use Many

Open-source proofs of concept exploring common workflow challenges faced by users of OSINT, PAI, and CAI tools — with a focus on blockchain investigation.

> **Disclaimer:** This is an individual's personal hobby project. It represents one practitioner's brainstorm — a collection of open-source ideas meant to inspire other users and developers to come up with their own solutions. It does not represent official requirements, requests, or positions of any organization. It is not endorsed by any employer, agency, or government entity. If something here is useful to you, great. If not, that is equally fine.

---

## Executive Summary

OSINT, PAI, and CAI platforms — including blockchain forensics tools — have built exceptional analytical capabilities. Where the industry has not yet invested as deeply is in what happens after an analyst finds something.

The core problem is redundancy. Analysts discover data, then retype it. They tag an address, then search for it again in a different view. They find a counterparty relationship, then manually note it somewhere outside the tool. They build a table of findings, then reformat it for a report, then reformat it again for a spreadsheet, then again for a briefing.

**The principle behind these proofs of concept is simple: an analyst should only have to discover or mark something once, then be able to use it in many different ways with minimal extra work.**

These proofs of concept explore three expressions of that principle:

1. **Investigation-Integrated Tagging** — Tag an address once; see that context everywhere — in transaction tables, flow analysis, counterparty lists, dossiers, and search results. Share investigation state across team members through export and merge.
2. **Clipboard Collection** — Find a data point once; collect it without leaving the tool; export it in multiple formats without reformatting.
3. **Plain Language Data Presentation** — The structured data already exists on screen. Convert it to readable, properly cited sentences automatically instead of making the analyst retype it.

None of these require proprietary data. None conflict with existing platform capabilities. They are presented as ideas that any tool — commercial, open-source, or homegrown — could adopt, adapt, or ignore entirely.

### Who Benefits

| Stakeholder | Redundancy They Face | How It Could Be Reduced |
|-------------|---------------------|------------------------|
| **Investigator / Analyst** | Retypes data; re-searches for addresses across views; context-switches between tool, documents, and spreadsheets | Tags once, sees context everywhere; collects findings as they work; exports in the format they need |
| **Prosecutor / Legal** | Receives screenshots and manually-typed summaries; must trust the retyping was accurate | Receives properly cited, plain-language statements assembled directly from structured data |
| **Task Force / Partner Agency** | Rebuilds investigation context from scratch; compares case files manually for overlap | Receives exported investigation state; merges independently-built datasets to surface cross-case connections |
| **Team Lead / Supervisor** | Reviews are verbal or ad hoc; no structured view of what was found or how it connects | Reviews structured Dev Lists showing findings, relationships, and analysis history |

---

## The Problem

### What Tools Do Well

OSINT, PAI, and CAI platforms — blockchain forensics tools in particular — excel at their core analytical functions. Address clustering, risk scoring, entity identification, transaction graphing, and compliance screening are mature capabilities. The industry has invested heavily in data coverage, attribution databases, and visualization.

### Where the Workflow Gaps Are

The moment an investigator moves from "looking at data" to "building a case," the tooling support thins out significantly. The common thread across most of these gaps is redundancy — the analyst has already found the information, but has to re-discover it, retype it, or reformat it to make it usable.

**Investigation state is ad hoc.** An analyst examining 40 addresses across three cases typically has no structured way to track which addresses belong to which investigation, what role each address plays, or how counterparties relate to addresses of interest. In practice, analysts take notes externally, rely on memory, or use the platform's graph as a de facto case file — which it was never designed to be.

**Collection is manual.** When an analyst finds a relevant transaction, counterparty, or data point, there is generally no way to "add it to the clipboard" for later use. The workflow becomes: screenshot, switch to a document, retype what was on screen, switch back, continue analysis. Every context switch is a chance for transposition errors, and every screenshot turns searchable data into an unsearchable image.

**Output is raw, not narrative.** Blockchain data is structured — addresses, amounts, timestamps, directions. But reports, affidavits, and intelligence summaries require sentences. "Address TRfG...x9Q2 received $47,231.00 USDT from address TKp4...mN81 on March 14, 2025" is what the analyst types manually while looking at a table row that already contains every one of those values. This retyping happens hundreds of times per investigation.

**Findings do not transfer between team members.** Two analysts working the same case on separate systems each build their own mental model of the investigation. When they compare notes, the comparison is verbal or manual. Whatever one analyst tagged, traced, or discovered has to be communicated and re-entered by the other.

---

## Concept 1: Investigation-Integrated Tagging (Dev Lists)

### What It Is

A Dev List is a structured investigation manifest. Each list represents a case or line of inquiry. Within a list, addresses are classified by their investigative role:

| Type | Purpose |
|------|---------|
| **AoI** (Address of Interest) | Primary targets — numbered sequentially (Cougar 001, Cougar 002) |
| **Counterparty** | Addresses that transact with AoIs — tagged automatically or manually |
| **Traced** | Addresses discovered through transaction tracing |
| **Tertiary Party** | Second-hop connections identified through flow analysis |
| **Transaction** | Specific transaction hashes relevant to the investigation |

### Why It Matters

**Tag once, see everywhere.** When an address is tagged as "Cougar 004," that tag appears everywhere — in transaction tables, flow analysis results, counterparty lists, graph visualizations, and search results. The analyst never has to ask "have I seen this address before?" The tool answers that question automatically, on every screen. No re-searching, no cross-referencing notes.

**Programmatic relationship derivation.** This is where investigation tagging becomes analytically powerful, not just organizationally useful. When an analyst opens the dossier for any address, the system programmatically determines which AoIs that address is a counterparty of — not from a stored note, but by traversing the actual data:

> **CtrPty of Cougar 004, Koala 008**

This appears automatically in the address header. It means: "This address appears in the vendor flow data or transaction history of these specific AoIs." If an address shows up as a counterparty of targets from two separate investigations, that is an immediate cross-case signal — shared infrastructure, a common facilitator, or a convergence point — surfaced without the analyst ever building a graph.

**Cross-investigation visibility.** An address tagged in Operation Cougar that also appears in Operation Koala's flow data surfaces that connection automatically. This is the kind of cross-case intelligence that currently requires either a shared database (which most agencies don't have) or manual comparison of case files.

**Counterparty auto-tagging.** When counterparty flow data is imported for an AoI, every counterparty address is automatically tagged on the same Dev List. When flow analysis is run against an AoI, discovered counterparties are surfaced as suggestions with accept/dismiss controls. The investigation manifest grows as the analysis progresses — without the analyst having to manually record each discovery.

**Team collaboration through merge.** Investigation state can be exported and shared. Two analysts working the same case on separate systems can independently import data, tag addresses, and build Dev Lists. When they merge databases, the combined dataset is immediately available — including all the programmatic relationship derivation that depends on having complete data. No re-entry, no verbal handoffs.

### The Broader Idea

Most analytical tools offer some form of labels or tags. What is less common is the full integration of those tags into the investigative workflow:

- Structured classification by investigative role (AoI vs. counterparty vs. traced) rather than flat labels
- Sequential numbering that creates a portable reference system ("Cougar 004" means the same thing regardless of which analyst says it)
- Programmatic relationship derivation that surfaces tertiary connections without manual graphing
- Tags that propagate into every analytical view — transaction tables, flow results, counterparty lists — not just a profile page
- Investigation state that can be exported, shared, and merged across analysts and systems

The underlying idea is that investigation state could be treated as a first-class data structure — something that integrates into every analytical workflow rather than sitting in a separate notes panel.

---

## Concept 2: Clipboard Collection (Shopping Cart for Investigations)

### What It Is

A companion proof-of-concept (see `Samples/Proof of Concept-Data to Plain Language Clip Board.html`) demonstrates a clipboard system that works like a shopping cart: the analyst collects structured data points — transactions, relationships, flow percentages — without leaving the analytical tool. Each collected item retains its structured fields and source attribution. The clipboard then exports to multiple formats:

| Format | Audience |
|--------|----------|
| **Plain text** | Email, chat, quick notes |
| **RTF with footnotes** | Word documents with proper sourced citations that survive copy-paste |
| **CSV (flat table)** | Spreadsheets, databases |
| **CSV (node/edge)** | Link analysis tools (Analyst's Notebook, Maltego, etc.) |
| **PROV-O JSON-LD** | W3C provenance standard for big data / linked data systems |

### The Problems It Solves

**The Retyping Tax.** Every time an analyst copies a data point from a tool into a report, they retype information they are already looking at on screen. Every retype is a chance for misspelled entity names, transposed addresses, and misattributed amounts. These are quiet errors that propagate downstream into affidavits, intelligence reports, and court exhibits.

**The Screenshot Problem.** When retyping feels too slow or error-prone, analysts take screenshots. Screenshots turn structured, searchable, verifiable data into pictures. Anyone downstream who needs the actual values has to retype from the image. The error chain starts again.

**Split-Screen Context Switching.** When the tool does not export well, analysts split their screen between the analytical platform, a Word document, a spreadsheet, and email. Every window switch is a chance to paste the wrong value in the wrong place. The cognitive load of maintaining context across four applications is real and measurable.

**Footnotes Do Not Survive Copy-Paste.** HTML footnotes are stripped when copying to Word. There is zero chance of preserving citations through the browser clipboard. Every source attribution has to be manually reconstructed, every time. RTF export with embedded footnotes solves this completely.

**The Friction Scales With Utility.** The better the tool, the more it gets used. The more it gets used, the more retyping, screenshotting, and reformatting. The most valuable analytical platforms create the most export friction for their most active users.

### Why Not Generative AI?

Sentence assembly from structured fields is deterministic — it produces the same correct output every time, instantly, with zero infrastructure cost. Generative AI adds latency, cost, and the possibility of hallucinated values in a context where a single wrong digit in an address or amount can undermine an entire case. The clipboard runs entirely in the browser with no server calls.

### The Broader Idea

If a tool lets users copy one data point, it could let them copy many. That is what turns a convenience feature into a workflow tool. The clipboard concept is format-agnostic and could wrap around any structured display in any analytical platform — transaction tables, flow diagrams, graph views, risk reports, entity profiles. The analyst finds the data once; the tool handles the reformatting.

---

## Concept 3: Plain Language Data Presentation

### What It Is

Every structured data point in an analytical tool can be expressed as a readable sentence with proper attribution:

> *Address TRfG...x9Q2 received 47,231.00 USDT from Binance Hot Wallet (TKp4...mN81) on March 14, 2025, representing 15.2% of total income for the reporting period.*
>
> — Source: Vendor Export, exported March 20, 2025

The fields already exist in the tool's data model: sender, receiver, amount, asset, timestamp, percentage, source. The sentence is assembled deterministically from those fields. No AI, no natural language processing, no ambiguity.

### Why It Matters

**The audience is not the analyst.** The person using the analytical tool is rarely the final consumer of the information. Prosecutors need sentences for affidavits. Task force leads need summaries for briefings. Partner agencies need intelligence products, not raw data exports. Compliance officers need narrative suspicious activity reports.

Every one of these downstream consumers currently receives either:
- Raw data they cannot interpret without training
- Screenshots they cannot search or verify
- Manually retyped summaries with undetectable errors

Plain language presentation with retained sourcing solves all three — and eliminates an entire category of redundant manual work.

**Citation formats matter.** Different audiences need different citation styles. A footnoted report for a prosecutor is different from an in-text citation for an intelligence summary is different from no citation at all for a quick email. The clipboard PoC demonstrates toggling between citation modes (footnote, in-text, none) for the same underlying data.

### The Broader Idea

The structured data already exists in most analytical tools. Sentence templates are trivial to implement. The value is not in the technology — it is in recognizing that the analyst's job is not finished when the data is on screen. The job is finished when the data is in the hands of the person who needs it, in the format they can use. The data was already discovered; the only remaining work should be choosing the output format.

---

## About This Proof of Concept

The working demo (`offline-dist/Proof-Of-Concept-Blockchain-Export-Analyst.html`) implements the following:

- **Multi-format CSV import** with vendor-aware auto-detection (transfer ledgers, entity flows, counterparty flows, graph exports, legal support records)
- **Dev List management** with AoI/counterparty/traced/tertiary classification, sequential numbering, cross-investigation search, and import/export
- **Address Dossier** — consolidated 360-degree view of any address including entity associations, transaction history, counterparty summaries, vendor flow analysis (bidirectional), programmatic AoI relationship badges, and tertiary analysis
- **Transaction Tracing** with configurable time windows and value tolerances
- **Income/Expense Flow Analysis** with percentage-based counterparty breakdown, multi-level drill-down, and automatic counterparty discovery with accept/dismiss workflow
- **Tertiary Analysis** identifying shared counterparties, common funding sources, and inter-counterparty links
- **Database backup/restore/merge** for team collaboration
- **Dust and zero-value filtering** across all import paths

The companion clipboard PoC (`Samples/Proof of Concept-Data to Plain Language Clip Board.html`) demonstrates the data-to-plain-language collection and multi-format export concepts independently.

Both demos are delivered as self-contained HTML files with zero external dependencies — they run offline in any browser, including on air-gapped systems. This packaging choice was made so the demos themselves can be shared freely and evaluated by anyone without setup, accounts, or installation. It is a property of the demo, not a product recommendation.

---

## Why Open Source

These proofs of concept are published openly so that anyone in the OSINT, PAI, and CAI community — individual practitioners, developers, tool vendors, researchers, or agencies — can see them, evaluate them, and build on them if they find them useful.

The concepts are not complicated. They do not require new data sources, new infrastructure, or changes to existing analytical capabilities. They layer on top of what already exists. Whether they end up integrated into commercial platforms, built as standalone open-source utilities, or simply spark someone's own better idea — any of those outcomes would be worthwhile.

The underlying principle is straightforward: when an analyst has already found, tagged, or structured a piece of information, they should not have to find, tag, or structure it again just because they need it in a different context. Reducing that redundancy is where small workflow improvements can make an outsized difference.


## What These Tools Demonstrate

### Tool 1: Flow Analysis

Flow Analysis starts with a target address and asks: where does money come from, and where does it go? But instead of pulling every transaction and rendering a link chart, it asks the analyst to define the question first.

**Filtered, directed pulls.** The analyst sets direction (income or expense), depth (how many hops, not operational in demo), and minimum percentage (ignore anything below this threshold). On a live API, this translates to a bounded query — a fraction of the calls that a full address pull would require.

**Counterparty breakdown.** Results appear as a table showing each counterparty's share of total flow. Not a hairball graph with a thousand nodes. A ranked list that an analyst can read in seconds.

**Tertiary analysis.** Nine structured queries that surface patterns one hop beyond the counterparties: shared exchanges, blocklisted connections, inter-counterparty links, common first transactions, shared gas sources. These are the questions an experienced analyst asks instinctively — automated into one-click operations that return concise summaries, not sprawling visualizations.

**Selective clipboard.** Every row in every result table has a copy button. The analyst picks what matters, collects it in a side panel, and exports only that. Not everything. Not nothing. Exactly what they chose.

### Tool 2: Transaction Tracing

Transaction Tracing starts from a specific transaction and works outward. The analyst enters a seed transaction hash, identifies the target address, and searches for related transactions using filtered criteria.

**Saved filters.** Filter combinations auto-save when the analyst runs a search. Next time, one click to re-apply. Maximum of twenty saved filters per tool, oldest unpinned filters rotate out automatically. The analyst never re-enters parameters they have already proven useful.

**Always loads unfiltered.** This is a deliberate design choice. Analysts forget filters are active. A stale filter silently excludes relevant data. Every page load starts clean. If the analyst wants their previous parameters, they re-apply with one click — a conscious choice, not an invisible default.

**Dirty state detection.** When a saved filter is active and the analyst changes any parameter, the interface shows the filter as modified. No ambiguity about whether the current view matches a saved configuration or has been adjusted.

### Tool 3: Dev Lists

Dev Lists are the persistent team memory layer. They solve the re-pull and re-discovery problems.

**What a Dev List is.** A "Developmental Address of Interest" list — a team-maintained registry of addresses that matter to an investigation, with classifications, aliases, and notes. Not a graph. Not a database of every transaction. A curated list of what humans decided was worth tracking.

**Classifications.** Each address gets a classification: Address of Interest (auto-numbered per investigation), Transaction Trace, Counterparty, Tertiary Party, or Traced Through. These are not risk scores. They are investigative roles — they describe why the team cares about this address.

**Cross-tool awareness.** When an address appears in any tool — Flow Analysis, Transaction Tracing — and it matches a Dev List entry, a badge appears inline. The analyst sees immediately: "This address was already flagged in investigation AARDVARK as AoI-003." No re-pulling. No re-discovering. No asking a colleague if anyone has looked at this before.

**Cross-investigation discovery.** In this proof of concept, the system detects when an address appears across multiple investigations by comparing results against active Dev Lists. If AoI-003 from AARDVARK shows up as a counterparty in investigation BADGER, the tool surfaces that connection with a distinct visual indicator. In a production environment, the scale and performance characteristics of this feature would depend on implementation — but the concept demonstrates the value of automated cross-referencing that does not rely on the analyst remembering every address from every case.

**Storage footprint.** A Dev List for a complex investigation might contain a few hundred entries. A full transaction graph for the same investigation could contain hundreds of thousands of nodes and edges. The Dev List captures the analytical conclusions. The graph captures the raw data. Both have their place — network-scale graphing is essential for certain types of analysis. But for team coordination and institutional memory, the curated conclusions are often what matter most, and they are dramatically cheaper to store and query.

---

## The Cost Argument

Every feature in these tools reduces API calls or eliminates redundant work. This matters because blockchain API calls are not free — they consume rate limits, compute resources, and in many cases, direct dollar costs.

### Fewer Calls Per Investigation

| Without targeted filtering | With targeted filtering |
|---|---|
| Pull full address history (all transactions, all time) | Pull transactions matching direction, depth (not operational in demo), time window, and threshold |
| Download to Excel, apply filters manually | Results arrive pre-filtered, ready for analysis |
| Re-pull when parameters change | Adjust parameters and re-query with bounded scope |

The difference is not marginal. A single active Tron address can have thousands of transactions. Pulling all of them to find the twenty that fall within a ten-day window and exceed 5% of total flow is like downloading an entire phone book to find one number.

### Fewer Duplicate Pulls Across Analysts

| Without Dev Lists | With Dev Lists |
|---|---|
| Each analyst pulls the same addresses independently | First analyst flags the address; subsequent analysts see it immediately |
| Investigation context lives in personal notes or memory | Classifications, aliases, and notes persist in the shared list |
| Cross-case connections discovered by chance | Cross-investigation discovery surfaces connections automatically |

### Fewer Wasted Exports

| Without selective clipboard | With selective clipboard |
|---|---|
| Export full CSV (hundreds of rows), delete what is not needed | Copy individual rows that matter to a side panel |
| Re-open the tool to find something previously seen | Clipboard persists during the session; export at any time |
| Retype values into reports, risking transcription errors | Paste structured data directly from clipboard |

### Front-End Operations Add Near-Zero Server Cost

Several features in these tools — Dev List badge rendering, saved filter management, clipboard accumulation, dirty state detection — run entirely in the browser. The provider's servers are not involved in these operations. These features scale across users with near-zero additional infrastructure cost. The development effort to build them is real, but the ongoing operational cost is minimal.

---

## For the Analyst

You already do this work. You already know what time window matters. You already know which counterparties are worth investigating. You already develop a sense for which filter parameters produce useful results.

These tools do not change how you think. They change how much manual work sits between your judgment and your output.

- You define the filter criteria. The tool pulls only what matches.
- You flag an address. Every tool in the suite knows about it from that point forward.
- You develop a useful filter combination. The tool remembers it for next time.
- You find three important data points in a five-hundred-row result set. You export three rows, not five hundred.

The tertiary analysis feature is worth specific attention. The nine query types — top addresses, shared exchanges, blocklisted connections, inter-counterparty links, counterparty commons, shared first transactions, shared gas sources, shared permissions, and Dev List cross-references — are the questions you ask when you are two hours into an investigation and trying to find the thread. They are automated here. Each one returns a concise summary, not a graph to untangle.

Cross-investigation discovery deserves attention too. If you have worked multiple cases and noticed an address appearing across them, you know how easy it is to miss that connection. The system checks every result against every active investigation automatically. When it finds a match, it tells you — with a distinct visual indicator so you do not confuse it with a regular Dev List badge.

---

## For the Developer

### What runs where

**Front-end only (near-zero incremental server cost):**
- Saved filter persistence and re-application
- Dev List badge rendering (lookup against local state)
- Clipboard accumulation and selective export
- Dirty state detection on filter parameters
- Cross-investigation discovery detection (set intersection on local data)
- Plain language conversion (string concatenation from structured fields)

**Requires API calls (but fewer and smaller):**
- Filtered transaction queries (bounded by direction, depth, threshold, time range)
- Address history retrieval (scoped to analyst-defined parameters)

**Lightweight persistence (small payloads):**
- Dev List storage (flat table, typically hundreds of entries per investigation)
- Saved filter storage (maximum 20 JSON objects per tool per user)

### What this is not

This is not a graph database. It does not attempt to store or query the full transaction network. The Dev List is a curated index — an intentionally small dataset that captures investigative conclusions rather than raw blockchain data.

The tertiary analysis feature explores one to two hops beyond known counterparties, which on a live API means a bounded number of additional calls. It does not crawl the network. It asks nine specific, structured questions and returns summarized answers.

### Implementation complexity

The most complex feature is cross-investigation discovery, which requires comparing result sets against multiple Dev Lists in real time. In practice, this is a set intersection operation across small datasets (hundreds of entries). It is computationally trivial.

Saved filters are serialized JSON objects with a twenty-item cap per tool. Auto-naming generates a human-readable label from the filter values (e.g., "Income | Depth 2 | Min 5%"). Pinning, renaming, and deletion are standard list operations.

The clipboard is a session-scoped array of structured objects. Copy-all serializes to tab-separated text. Individual copy writes a single formatted line. No server involvement.

The plain-language clipboard (demonstrated in the companion proof of concept) converts structured fields to sentences using a deterministic code-to-predicate mapping table. No generative AI. No API calls. No hallucination risk. The same output every time.

### What would change with live API integration

The simulated data layer (`simulated-data.ts`) would be replaced with API calls to TronGrid or TronScan. The filter parameters that currently constrain simulated data generation would become query parameters on those API calls. The front-end rendering, Dev List logic, clipboard, and saved filters would remain unchanged.

The key architectural point: filtering happens before the pull, not after. The API receives a bounded request and returns a bounded response. The front end never needs to ingest, store, or render the full transaction history of an address.

---

## For the Manager

### Time savings

Every feature addresses a specific time cost that analysts currently absorb:

| Task | Current workflow | With these tools |
|---|---|---|
| Isolate a time window | Pull all transactions, export to Excel, filter manually | Set date range in the tool, pull only matching transactions |
| Re-apply known filter parameters | Re-enter from memory or notes each session | One-click re-apply from saved filters |
| Check if an address was previously investigated | Ask colleagues, search personal notes, re-pull and compare | Dev List badge appears automatically in every tool |
| Find connections across investigations | Manual comparison of separate case files | Cross-investigation discovery detects matches automatically |
| Export specific findings | Download full CSV, delete unneeded rows, reformat | Select individual rows to clipboard, export once |
| Convert structured data to report text | Retype from screen into document | Plain language clipboard (companion POC) |

### API cost reduction

Targeted filtering reduces the volume of API calls per investigation. Instead of pulling an entire address history and filtering locally, the analyst defines constraints that reduce the query scope before execution. Fewer calls per analyst, per investigation, per day.

Dev Lists reduce duplicate calls across the team. When the first analyst flags an address, subsequent analysts see it without re-querying the blockchain. The institutional knowledge persists.

### Scalability

Front-end features (saved filters, clipboard, Dev List badge rendering, cross-investigation discovery) run on the analyst's machine. Adding more analysts does not add server load for these operations.

Dev List storage is lightweight. A complex investigation with hundreds of flagged addresses requires a fraction of the storage that a full transaction graph demands.

### Risk reduction

- Saved filters that always load unfiltered eliminate the risk of stale filters silently excluding relevant data.
- Dev List cross-references reduce the risk of an analyst missing a previously identified address.
- Cross-investigation discovery reduces the risk of failing to connect related cases.
- Selective clipboard export reduces transcription errors from manual retyping.
- Deterministic plain language conversion (no generative AI) eliminates hallucination risk in report text.

---

## For the Analyst Who Just Joined This Work

You are here because the results speak for themselves. These tools are designed to help you — and everyone on the team — move faster on the next case.

Here is what matters:

**Dev Lists are your team's memory.** When you open an investigation, the Dev List tells you what has already been found: which addresses matter, why they were flagged, what classification they received, and any notes from the analyst who flagged them. You do not start from zero. You start from where the last person left off.

**Saved filters are your muscle memory, preserved.** When you find a filter combination that works — direction, depth, percentage threshold — the tool saves it automatically. Next time, one click. You do not have to remember the parameters or write them down.

**The clipboard is your evidence bag.** As you work through results, you pick the items that matter. They accumulate in a side panel. When you are done, you export exactly what you collected — not everything, not nothing.

**Cross-investigation discovery watches your back.** If an address you are looking at appeared in a different investigation, the tool tells you. You do not have to know to look for it. You do not have to remember every address from every case. The system does that comparison for you, automatically, against every active investigation.

**The tools reset on every page load.** No hidden filters. No stale parameters from yesterday. You always see the full picture first, then narrow down intentionally. This prevents the single most common analytical error: missing something because a filter you forgot about was still active.

---

## What This Does Not Do

This proof of concept uses simulated data. It does not connect to live blockchain APIs. It does not perform real risk scoring. It does not access KYC information.

What it demonstrates is methodology, not capability. The question is not whether the blockchain data can be retrieved — existing tools already do that well. The question is whether the workflow surrounding that retrieval can be made more efficient, more targeted, and more persistent across a team.

These tools are complementary to existing platforms, not replacements. They demonstrate features that could be integrated into the tools analysts already use, reducing the friction between the platform's analytical power and the analyst's actual workflow.

---

## The Companion Proof of Concept: Data to Plain Language Clipboard

A separate single-page proof of concept demonstrates the output side of the workflow: converting structured data (subject, predicate, object, source) into plain language sentences with proper attribution.

Key points:

- **Deterministic conversion.** A mapping table translates relationship codes (`FORMER_CEO`, `BOARDMEMBER`) into full predicates ("is the former CEO of," "is on the board of"). No generative AI. No hallucination. Same input, same output, every time.
- **Multiple citation modes.** Footnote, in-text, no citation, and graph view — same data, right presentation for each audience.
- **Five export formats.** Plain text, RTF with real Word footnotes, flat CSV, graph-ready node/edge CSV, and W3C PROV-O JSON-LD.
- **Runs entirely in the browser.** Near-zero server cost. Instant performance. No data leaves the machine.
- **Solves the footnote problem.** HTML footnotes do not survive copy-paste into word processors. RTF export generates real page-bottom footnotes with superscript markers — something no amount of browser copy-paste can achieve.

Together, the two proof of concepts cover the full analytical cycle: the blockchain tools show how to find what matters efficiently, and the plain language clipboard shows how to get it out in the format the audience actually needs.


---
ORCS Mission: To present practical, open-source proofs of concept that address common challenges in OSINT, PAI, and CAI workflows — empowering stakeholders to develop tailored requirements and solutions.

GitHub: [ORCS GitHub](https://github.com/OpenResearchCommunicationSystem)

YouTube: [ORCS Youtube](https://www.youtube.com/channel/UC0hlqOtxWemIo7AIR0KkCfg)

Blog: [ORCS Blog](https://publish.obsidian.md/openresearchcommunicationssystem)

Other Active Proof's of concept

[Data to Plain Language Clipboard](https://openresearchcommunicationsystem.github.io/Proof-of-Concept-Data-to-Plain-Language-Clip-Board/)
