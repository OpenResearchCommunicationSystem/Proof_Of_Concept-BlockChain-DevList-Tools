
# [-> Click Here for Block Chain Dev List Concepts Demo <-](https://openresearchcommunicationsystem.github.io/Proof_Of_Concept-BlockChain-DevList-Tools/)

### The "depth" tool is not operational in this demo, it is a place holder

---

## Summary

| What these tools demonstrate | Why it matters |
|---|---|
| Analyst defines the query before pulling data | Fewer, smaller API calls per investigation |
| Persistent team memory via Dev Lists | No duplicate pulls, no re-discovery, no lost context |
| Saved filters with one-click re-apply | No re-entering known parameters; loads unfiltered to prevent silent exclusion |
| Selective clipboard export | Analysts export what matters, not everything |
| Cross-investigation discovery | Connections across cases detected automatically |
| Tertiary analysis with nine structured queries | Guided exploration without full graph rendering |
| Plain language clipboard with multiple export formats | Eliminates retyping; preserves attribution across formats |
| Front-end operations for most features | Near-zero additional server cost; scales across users with minimal infrastructure expense |

The concept is not that existing tools are insufficient. It is that the workflow around those tools can be made more efficient — and that many of the improvements are lightweight, front-end operations that cost relatively little to build and very little to run.

The analyst already does the hard work of knowing what to look for. These tools make sure the machine does not waste their time making them do it the hard way.

## The Premise

Blockchain analysis tools are powerful. They index millions of transactions, flag known entities, score risk, and visualize connections. The core analytical engines are genuinely impressive, and they continue to improve — often in direct response to analyst feedback.

But there is a gap between what these tools can surface and what an analyst actually needs to do with it. That gap is not about capability. It is about workflow.

In many common workflows, the analyst already knows what they are looking for. They know the time window. They know the direction. They know the threshold that separates signal from noise. But the available interfaces often require pulling a broad dataset first and filtering after. The analyst ends up spending time on data handling — sorting, re-entering, re-pulling, re-discovering — instead of analysis.

These proof-of-concept tools demonstrate a complementary approach: let the analyst define the question first, pull only what answers it, and remember what the team has already found. These are workflow enhancements designed to work alongside existing platforms, not replace them.

---

## What Happens Today

### The Pull Problem

An analyst receives a seed transaction. They need to understand what happened around it — say, ten days in either direction. To do that, they pull the address history.

In some tools and workflows, time sorting is limited to greater-than or less-than — not between. So to isolate a ten-day window around a transaction, the analyst may have to download up to a thousand transactions, open Excel, and apply the date range filter manually.

The analyst already knew the time window. The extra steps are data handling, not analysis.

### The Re-Pull Problem

An analyst identifies five counterparties worth investigating on a Monday. They tag them in their notes, maybe a spreadsheet, maybe a sticky note. On Wednesday, a colleague picks up the same case. They pull the same addresses again. They run the same filters. They arrive at the same conclusions — if they are lucky. If they are not lucky, they miss something the first analyst caught, or they waste hours rediscovering what was already known.

There is no persistent team memory. Every analyst starts from zero.

### The Re-Entry Problem

An analyst develops a set of filter parameters that work well for a particular type of investigation. Income direction, depth of two hops, minimum 5% of total flow. They use these parameters three times a week. Every time, they re-enter them from scratch.

If they are disciplined, they wrote the parameters down somewhere. If they are not, they reconstruct them from memory. Either way, the tool does not remember.

### The Export Problem

The analyst finds what they need. Three addresses, two transaction patterns, one connection to a flagged entity. Now they need to get that information out of the tool.

The tool offers a full CSV export. Five hundred rows. The analyst needed three. So they export everything, open a spreadsheet, delete 497 rows, and reformat what remains for a report.

Or they take a screenshot. Which converts usable data into a picture that cannot be searched, copied, parsed, or verified.

Or they retype the values by hand into another window. Every retype is a chance for a misspelled address, a transposed amount, a misattributed transaction.

The tool did the hard part — finding the data. Then it made the easy part — getting the data out — unnecessarily painful.

---

## The Principle

Every feature in these proof-of-concept tools expresses one idea:

**Do not make the analyst do work the machine already has the information to do.**

- The data is already structured on screen — do not make the analyst retype it.
- The analyst already knows what they are looking for — do not make them pull everything.
- The team already identified this address last month — do not make the next analyst rediscover it.
- The analyst already figured out the right parameters — do not make them re-enter them.
- The analyst only needs three rows — do not make them export five hundred.

---

## What These Tools Demonstrate

### Tool 1: Flow Analysis

Flow Analysis starts with a target address and asks: where does money come from, and where does it go? But instead of pulling every transaction and rendering a link chart, it asks the analyst to define the question first.

**Filtered, directed pulls.** The analyst sets direction (income or expense), depth (how many hops), and minimum percentage (ignore anything below this threshold). On a live API, this translates to a bounded query — a fraction of the calls that a full address pull would require.

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
| Pull full address history (all transactions, all time) | Pull transactions matching direction, depth, time window, and threshold |
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
