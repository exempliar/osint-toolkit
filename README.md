# OSINT Toolkit

Self-contained, teaching-first tools for open source intelligence work. Every tool is a single HTML file: open it by double-click, it runs offline, and nothing you type ever leaves the page.

The goal is not just to automate lookups. It is to teach the method behind them, so you get faster and sharper at the actual work.

## What is inside

| Tool | File | What it does |
|------|------|--------------|
| OSINT Learning Tool | [`OSINT-Learning-Tool.html`](OSINT-Learning-Tool.html) | Teaching-first pivot console. Type any indicator, learn where to look and why, get a model-agnostic AI prompt, paste findings back to extract pivots, and build an exportable case. |

More tools will land here over time. See the [roadmap](#roadmap).

## OSINT Learning Tool

Type any indicator (IP, domain, URL, email, username, hash, crypto wallet, person, phone, company, image, or topic). The tool names what it is, frames what you are actually trying to learn, and then walks you through the pivot.

What it gives you:

- **Detection and framing.** It recognizes the indicator type and states the question you should be answering before you start clicking.
- **Mapped sources with reasoning.** The places to look, each with a short note on *why* that source matters for this indicator type, not just a bare link.
- **Model-agnostic AI prompts** in four modes: Learn, Pivot, Verify, and Report. Copy the prompt, run it in whatever AI you use, and bring the answer back.
- **Paste-back pivot extraction.** Drop the AI's answer into the tool and it pulls out new indicators as clickable pivots, so a lead turns into the next step.
- **A running Case.** Everything you collect is gathered into a case you can export to Markdown.
- **Local memory.** Favorites, notes, and custom sources persist in the browser you open it in. Nothing is uploaded anywhere.

### Run it locally

1. Download [`OSINT-Learning-Tool.html`](OSINT-Learning-Tool.html) (on the file page, click the download / raw button and save it).
2. Double-click the file. It opens in your default browser and runs fully offline.
3. That is it. No install, no accounts, no server.

To grab the whole repo instead:

```
git clone https://github.com/exempliar/osint-toolkit.git
```

Then open `OSINT-Learning-Tool.html` from the folder.

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
7. **Export the Case to Markdown** when you are done, for your notes or a report.

### Privacy and safety

- The tool is a single static HTML file. It makes no network calls of its own and has no backend.
- Anything you type stays in your browser. Favorites and notes use local browser storage, which never leaves your machine.
- Prompts are copy and paste on purpose, so the tool stays model-agnostic and you stay in control of what goes to any AI.
- Passive vs active sources are labeled so you can avoid tipping off a target when that matters.

Use it only against targets you are authorized to investigate, and follow the terms of service of the sources you visit.

## Roadmap

Planned and in consideration:

- Session map: draw the collected Case as a small node graph so a chain of pivots is visible.
- Step-by-step playbooks per indicator type (ordered first moves).
- A query and dork builder to teach search operators.
- More self-contained tools alongside the Learning Tool.

## Contributing

Issues and pull requests are welcome. The house style is simple: one self-contained file per tool, offline first, no build step, and every feature should teach the method as well as run it.

## License

Released under the [MIT License](LICENSE). Use it, fork it, build on it.
