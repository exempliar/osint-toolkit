# OSINT Toolkit

Self-contained, teaching-first tools for open source intelligence work. Every tool is a single HTML file you download and open by double-click. Nothing you enter ever leaves the page — no backend, no accounts, no telemetry.

The goal is not just to automate lookups. It is to teach the method behind them, so you get faster and sharper at the actual work.

## What is inside

| Tool | File | What it does |
|------|------|--------------|
| OSINT Learning Tool | [`tools/OSINT-Learning-Tool.html`](tools/OSINT-Learning-Tool.html) | Teaching-first pivot console. Type any indicator, learn where to look and why, get a model-agnostic AI prompt, paste findings back to extract pivots, and build an exportable case you can view as a node map. |
| SONAR — Image OSINT Cockpit | [`tools/SONAR-OSINT-Cockpit.html`](tools/SONAR-OSINT-Cockpit.html) | Everything-from-a-picture cockpit. Drop an image, pull EXIF and OCR, copy a prompt to your AI, paste back to reconcile and pivot. Geolocation, transport visuals, and documents. **Needs a connection on first load** — see [below](#one-thing-to-know-before-you-use-it). |
| MANIFEST — Records Cockpit | [`tools/MANIFEST-Records-Cockpit.html`](tools/MANIFEST-Records-Cockpit.html) | The non-image companion to SONAR. Pick an entity type, drop the selector, and get targeted registry and tracker lookups, a prompt tuned per type, first moves, and a findings log. |
| DORK — Query Builder | [`tools/DORK-Query-Builder.html`](tools/DORK-Query-Builder.html) | Compose search queries across five engines with every operator explained as it goes in. Anatomy breakdown, cross-engine support matrix, and a checker for the mistakes that silently break a dork. |

More tools will land here over time. See the [roadmap](#roadmap).

## Repository layout

```
tools/            One self-contained HTML file per tool.
CONTRIBUTING.md   House style and conventions for adding a tool.
LICENSE           MIT.
```

Pick a tool from the table above, download the one file, and open it by double-click. Nothing else is needed — each tool is independent and runs offline from disk.

To grab the whole repo:

```
git clone https://github.com/exempliar/osint-toolkit.git
```

## OSINT Learning Tool

Type any indicator (IP, domain, URL, email, username, hash, crypto wallet, person, phone, company, image, or topic). The tool names what it is, frames what you are actually trying to learn, and then walks you through the pivot.

What it gives you:

- **Detection and framing.** It recognizes the indicator type and states the question you should be answering before you start clicking.
- **Mapped sources with reasoning.** The places to look, each with a short note on *why* that source matters for this indicator type, not just a bare link.
- **Model-agnostic AI prompts** in four modes: Learn, Pivot, Verify, and Report. Copy the prompt, run it in whatever AI you use, and bring the answer back.
- **Paste-back pivot extraction.** Drop the AI's answer into the tool and it pulls out new indicators as clickable pivots, so a lead turns into the next step.
- **A running Case,** viewable as a list or as a node map so the chain of pivots is visible, and exportable to Markdown.
- **Local memory.** Favorites, notes, and custom sources persist in the browser you open it in. Nothing is uploaded anywhere.

### Run it locally

1. Download [`tools/OSINT-Learning-Tool.html`](tools/OSINT-Learning-Tool.html) (on the file page, click the download / raw button and save it).
2. Double-click the file. It opens in your default browser and runs fully offline.
3. That is it. No install, no accounts, no server.

### How to use it, step by step

1. **Type an indicator** into the input at the top (for example an email, a domain, or a username). The tool detects the type. If it guesses wrong, override it with the dropdown.
2. **Read the frame line.** It states what you are trying to learn from this kind of indicator. This is the part that teaches the method.
3. **Work the sources.** Each listed source explains why it is worth checking for this indicator type. Passive sources (safe to browse) and active sources (may alert the target) are marked differently, so you know what leaves a footprint.
4. **Pick a prompt mode and copy it:**
   - **Learn** builds your background understanding of the indicator type.
   - **Pivot** asks the AI for the next indicators to chase.
   - **Verify** pressure-tests a finding before you trust it.
   - **Report** turns what you have into a clean writeup.
5. **Run the prompt in your AI**, then **paste the answer back** into the tool. It extracts any new indicators as clickable pivots.
6. **Click a pivot** to start the loop again on the new lead. The Case grows as you go.
7. **Switch the Case to map view** to see the chain of pivots as a node graph, and **export to Markdown** when you are done.

## SONAR — Image OSINT Cockpit

Everything you can get from a picture, in one place. Drop an image and SONAR pulls the EXIF metadata and runs OCR over any text in the frame, then hands you a copy-to-AI prompt tuned to what you are trying to establish. Paste the answer back to reconcile the model's claims against what the file actually says, and pivot on whatever survives.

Built for image work in three directions: geolocation, transport and vehicle visuals, and photographed documents.

**Teaches** what metadata does and does not prove, and how to pressure-test a confident AI reading against the evidence in the file.

### One thing to know before you use it

SONAR is the only tool here that needs a network connection. It loads two open-source libraries when you open it — [`exifr`](https://github.com/MikeKovarik/exifr) for EXIF parsing and [`tesseract.js`](https://github.com/naptha/tesseract.js) for OCR — from a public CDN, because bundling Tesseract's OCR language data into a single file would push it into the megabytes.

What this means in practice:

- **Your images are never uploaded.** Both libraries run inside your browser. No image, and nothing you type, is transmitted anywhere.
- **You need a connection on first load** for EXIF and OCR to work. Offline, the rest of the tool still opens and it tells you plainly that the libraries did not load, rather than failing silently.
- **The CDN sees a request** from your IP for two very common open-source libraries, as it would for any of the thousands of ordinary sites that use them.

## MANIFEST — Records Cockpit

The non-image companion to SONAR, for the recon, company, vessel, and infrastructure work that image tooling does not touch.

Pick an entity type — person, company, vessel, aircraft, domain and infrastructure, username, military, or historical — drop in your selector, and MANIFEST builds targeted lookups that inject the selector straight into the right registries and trackers. Each entity type comes with a research prompt tuned to it, a set of suggested first moves, and a findings log.

**Teaches** which registry actually answers which question, and what order to work an entity in so early findings narrow the later ones.

MANIFEST makes no network requests of its own. Every lookup is a link you choose to open.

## DORK — Query Builder

The other tools tell you where to look. This one tells you what to type once you get there.

Pick an engine — Google, Bing, DuckDuckGo, GitHub code search, or Shodan — and either start from an objective (exposed documents, directory listings, login pages, subdomains, secrets in code, exposed services) or build the query by hand. As each operator goes in, the tool explains what it does and why it matters for OSINT.

What makes it a teaching tool rather than a query box:

- **Live anatomy.** The finished query is broken into its parts, each labelled with what it is doing and why that matters.
- **Cross-engine support matrix.** The same capability has different syntax on different engines, and some engines simply lack it. `inbody:` on Bing is `intext:` on Google; `ip:` exists on Bing and nowhere else. The matrix makes that visible instead of leaving you to discover it by failure.
- **A checker that catches silent failures.** Two `site:` operators AND together and return nothing. Lowercase `or` is not an operator. An ungrouped `OR` swallows the rest of the query. DuckDuckGo ignores unsupported operators rather than rejecting them. These are the mistakes that make a dork look precise while doing almost nothing, and the tool flags them before you run.
- **Operator reference** for the selected engine — what each one does, why it matters, an example, and what to watch out for.
- **Footprint framing.** Searching is passive: you are querying an index someone else built, and the target learns nothing. Opening a result is not — that is the moment you appear in their logs.

**Teaches** what each operator actually does, how support differs between engines, and why zero results usually means the query is too tight rather than the thing not existing.

DORK makes no network requests of its own. Queries are composed locally, and only leave your machine if you click through to an engine. Saved queries are stored in your browser.

## Privacy and safety

Applies to every tool in this repo:

- Each tool is a single static HTML file with no backend, no accounts, and no telemetry.
- Anything you type stays in your browser. Favorites, notes, findings, and cases use local browser storage, which never leaves your machine, and none of it is written back into the HTML file.
- Prompts are copy and paste on purpose, so the tools stay model-agnostic and you stay in control of what goes to any AI.
- Passive vs active sources are labeled so you can avoid tipping off a target when that matters.
- The Learning Tool and MANIFEST make no network requests at all. SONAR loads two libraries from a CDN, as described above.

Use these only against targets you are authorized to investigate, and follow the terms of service of the sources you visit.

## Roadmap

Planned and in consideration:

- Step-by-step playbooks per indicator type (ordered first moves).
- A decode and convert workbench — identify and convert encodings, timestamps, and coordinate formats, and explain how each was recognised.
- A timeline reconciler — build a chronology from events across sources with mixed timezones, and flag contradictions.
- More self-contained tools alongside the Learning Tool.

## Contributing

Issues and pull requests are welcome. The house style is simple: one self-contained file per tool, offline first, no build step, and every feature should teach the method as well as run it.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full conventions, including the shared palette and the checklist for adding a tool.

## License

Released under the [MIT License](LICENSE). Use it, fork it, build on it.
