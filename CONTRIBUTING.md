# Contributing

Issues and pull requests are welcome. This file describes the house style so a new tool lands consistently with the rest.

## The rule that matters most

**Every feature should teach the method as well as run it.**

A tool that returns an answer is half a tool. A tool that shows *why* that is the answer, and what you would do next, is the whole thing. If you add a lookup, add the reasoning next to it. If you add a source, say what it is good for and what it costs you to touch.

## House style

- **One self-contained file per tool.** All HTML, CSS, and JavaScript in a single `.html` file under `tools/`.
- **Offline first.** No backend, no accounts, no telemetry. A user should be able to download the one file, pull the ethernet cable, and still have it work.
- **No build step.** No bundler, no package.json, no transpile. What is in the repo is what runs.
- **No external dependencies,** with one narrow exception. No CDN scripts, no remote fonts, no remote images. Vendor anything you truly need directly into the file.

  The exception is a library that is genuinely too large to inline — SONAR loads Tesseract for OCR, whose language data runs to megabytes. If you take it, you owe the user three things: the feature must **degrade gracefully** and say so when the library fails to load, no user data may be transmitted (the library runs client-side, it does not send anything out), and the dependency must be **stated plainly** in the README, both in the tool's row in the table and in its own section. A tool that quietly needs the network is not acceptable; one that says so is.
- **Local storage only.** Persistence via `localStorage` is fine and encouraged. Anything that leaves the machine is not.
- **Model-agnostic AI.** Do not call an AI API. Generate a prompt the user copies into whatever model they use, and give them a way to paste the answer back. This keeps the tool free, offline, and neutral.

## Adding a tool

1. Create `tools/Your-Tool-Name.html`, following the conventions above.
2. Match the existing visual language so the toolkit reads as one system. Copy the `:root` custom properties from `tools/OSINT-Learning-Tool.html` rather than inventing a new palette:
   - Background `#050507`, panels `#0d0d11` / `#101016`, borders `#1c1c24` / `#262630`
   - Text `#e7e7ee`, muted `#8b8b98`, dim `#5a5a67`
   - Cyan `#2fe4d4` is the primary accent; magenta `#ff5db1`, amber `#ffcf5c`, green `#7be88a` are secondary
   - Square corners (`border-radius:0`), uppercase letterspaced section labels, monospace for indicators and file names
3. Add a row to the table in `README.md`.
4. If it completes or replaces a roadmap item, update the roadmap in `README.md`.

## Safety conventions

- **Label passive vs. active sources.** Anything that may alert the target must be visibly marked as such. This is a teaching tool; the footprint you leave is part of the method.
- **No credential handling.** Do not add login flows, API key fields that get transmitted, or anything that collects secrets.
- **Authorized use.** Keep the scope on the side of research anyone is entitled to do. Tools here are for investigating targets you are authorized to investigate.

## Testing

There is no test suite, and with no build step there is not much to run. Before opening a PR:

- Open the file directly from disk (`file://`) and confirm it works with no console errors.
- Confirm it still works with the network disconnected.
- Check it in at least one browser other than the one you built it in.
- Check the layout does not break below 900px wide.
