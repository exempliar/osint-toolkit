# OSINT Toolkit

Self-contained, teaching-first tools for open source intelligence work. Every tool is a single HTML file you download and open by double-click. Nothing you enter ever leaves the page — no backend, no accounts, no telemetry.

The goal is not just to automate lookups. It is to teach the method behind them, so you get faster and sharper at the actual work.

## What is inside

Three tools, one per stage of the work.

| Tool | File | What it does |
|------|------|--------------|
| MANIFEST — Entity Console | [`tools/MANIFEST-Entity-Console.html`](tools/MANIFEST-Entity-Console.html) | **Where to look.** Drop in a selector across sixteen entity types — from IP, domain and handle through to vessel, aircraft, military and historical. It names the entity, frames what you are trying to learn, gives you ordered first moves, maps the registries that answer it, extracts pivots from a pasted-back AI answer, and builds an exportable case you can view as a node map. |
| SONAR — Image OSINT Cockpit | [`tools/SONAR-OSINT-Cockpit.html`](tools/SONAR-OSINT-Cockpit.html) | **What is in the picture.** Drop an image, pull EXIF and OCR, copy a prompt to your AI, paste back to reconcile and pivot. Geolocation, transport visuals, and documents. **Needs a connection on first load** — see [below](#one-thing-to-know-before-you-use-it). |
| DORK — Query Builder | [`tools/DORK-Query-Builder.html`](tools/DORK-Query-Builder.html) | **What to type.** Compose search queries across five engines with every operator explained as it goes in. Anatomy breakdown, cross-engine support matrix, and a checker for the mistakes that silently break a dork. |

They hand work to each other. A lead SONAR pulls out of a photograph goes straight to MANIFEST as the right entity type; a selector in MANIFEST goes to DORK as a ready-made query. The **Send to** buttons pass it through the URL fragment, so it works offline from disk with no storage and no server.

More tools will land here over time. See the [roadmap](#roadmap).

## Repository layout

```
tools/            One self-contained HTML file per tool.
CONTRIBUTING.md   House style and conventions for adding a tool.
LICENSE           MIT.
```

Pick a tool from the table above, download the one file, and open it by double-click. Nothing else is needed — each tool is independent and runs offline from disk.

Every tool carries a **Toolkit** switcher in its header linking to the other two. Those links resolve against the sibling files in the same folder, so they work once you have the whole `tools/` directory and do nothing if you grabbed a single file. Everything else in a tool works either way.

To grab the whole repo:

```
git clone https://github.com/exempliar/osint-toolkit.git
```

## MANIFEST — Entity Console

Drop in any selector and MANIFEST names the entity, frames what you are actually trying to learn from it, and walks you through working it.

Sixteen entity types: IP, domain, URL, email, username, file hash, person, phone, company, crypto wallet, vessel, aircraft, military, historical, image, and topic. It detects the type where the shape of the value allows and you pick it from the grid where it does not.

What it gives you:

- **Detection and framing.** It recognises the entity and states the question you should be answering before you start clicking.
- **First moves.** An ordered opening sequence per entity type. The sources tell you where to look; this tells you what order to work them in, which is the part that saves time.
- **Registries with reasoning.** The places worth checking, each with a note on *why* it matters for this entity, what it tells you, and where it pivots. Passive sources (safe to browse) and active sources (may alert the target) are marked differently.
- **Model-agnostic AI prompts** in four modes: Learn, Pivot, Verify, and Report. Copy the prompt, run it in whatever AI you use, and bring the answer back.
- **Paste-back pivot extraction.** Drop the AI's answer in and it pulls out new selectors as clickable pivots.
- **A running case,** viewable as a list or a node map, exportable to Markdown.
- **Local memory.** Favourites, notes, and custom sources persist in the browser you open it in. Nothing is uploaded anywhere.

### How to use it, step by step

1. **Drop in a selector** — an email, a domain, a company, a ship's IMO number. It detects the type; if it guesses wrong, click the right entity in the grid.
2. **Read the frame line.** It states what you are trying to learn from this kind of entity. This is the part that teaches the method.
3. **Work the first moves in order.** They are sequenced so early findings narrow the later ones.
4. **Work the sources.** Each one explains why it is worth checking, and whether it leaves a footprint.
5. **Pick a prompt mode and copy it** — Learn builds background, Pivot asks for next steps, Verify pressure-tests a finding, Report turns it into a writeup.
6. **Paste the AI's answer back** to extract new selectors as pivots, or hand one to DORK with **Send to**.
7. **Switch the case to map view** to see the chain of pivots, and **export to Markdown** when you are done.

MANIFEST makes no network requests of its own. Every lookup is a link you choose to open.

## SONAR — Image OSINT Cockpit

Everything you can get from a picture, in one place. Drop an image and SONAR pulls the EXIF metadata and runs OCR over any text in the frame, then hands you a copy-to-AI prompt tuned to what you are trying to establish. Paste the answer back to reconcile the model's claims against what the file actually says, and pivot on whatever survives.

Built for image work in three directions: geolocation, transport and vehicle visuals, and photographed documents.

**Teaches** what metadata does and does not prove, and how to pressure-test a confident AI reading against the evidence in the file.

### Read only the part that matters

OCR degrades sharply the more of a frame it has to look at. A busy photograph — a street, a container terminal, a crowd — is mostly noise to it, and the noise drowns the few characters you actually want. Run a full frame through and you often get pages of garbage with your answer nowhere in it.

So drag a box over the text before you read. SONAR crops at full resolution and enlarges the crop before handing it to the OCR engine, which reads small text far better scaled up than as raw pixels.

Two honest limits, because this is not magic:

- **Enlarging cannot recover detail that was never captured.** If a glyph is only a few pixels tall in the original, no amount of interpolation will resolve it, and you will get a plausible wrong character rather than a blank.
- **Widely letter-spaced text reads badly** regardless of size — the engine tends to lose it or split it.

Treat any OCR digit you cannot see with your own eyes as a lead to verify, not a fact. There is also an **Invert** toggle for light-text-on-dark material, which sometimes helps and sometimes makes things worse; it is off by default and worth trying only when a read comes back poor.

### One thing to know before you use it

SONAR is the only tool here that needs a network connection. It loads two open-source libraries when you open it — [`exifr`](https://github.com/MikeKovarik/exifr) for EXIF parsing and [`tesseract.js`](https://github.com/naptha/tesseract.js) for OCR — from a public CDN, because bundling Tesseract's OCR language data into a single file would push it into the megabytes.

What this means in practice:

- **Your images are never uploaded.** Both libraries run inside your browser. No image, and nothing you type, is transmitted anywhere.
- **You need a connection on first load** for EXIF and OCR to work. Offline, the rest of the tool still opens and it tells you plainly that the libraries did not load, rather than failing silently.
- **The CDN sees a request** from your IP for two very common open-source libraries, as it would for any of the thousands of ordinary sites that use them.

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
- MANIFEST and DORK make no network requests at all. SONAR loads two libraries from a CDN, as described above.

Use these only against targets you are authorized to investigate, and follow the terms of service of the sources you visit.

## Roadmap

Planned and in consideration:

- Step-by-step playbooks per indicator type (ordered first moves).
- A decode and convert workbench — identify and convert encodings, timestamps, and coordinate formats, and explain how each was recognised.
- A timeline reconciler — build a chronology from events across sources with mixed timezones, and flag contradictions.
- More self-contained tools alongside these three.

## Contributing

Issues and pull requests are welcome. The house style is simple: one self-contained file per tool, offline first, no build step, and every feature should teach the method as well as run it.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full conventions, including the shared palette and the checklist for adding a tool.

## License

Released under the [MIT License](LICENSE). Use it, fork it, build on it.
