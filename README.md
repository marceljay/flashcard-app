# Flashcards

A lightweight, single-page flashcard web app for studying any subject. Create your own cards, organize them with tags, run through them in a flip-and-rate study session, and load ready-made sample sets. Everything runs in the browser — no account, no backend, no build step.

## Features

- **Create, edit, and delete cards** — each card has a front, a back, and an optional tag.
- **Search & tag filtering** — full-text search across cards plus one-click tag pills to narrow the deck.
- **Study mode** — flip cards, rate each as *Know it* or *Need practice*, shuffle, and see a results summary at the end.
- **Sample sets** — built-in decks (Fun Facts, Advanced Vocabulary, World Capitals, Space & Astronomy) you can load with one click.
- **Import / export** — back up or share your deck as a JSON file.
- **Dark mode** — follows your operating system's light/dark preference automatically.
- **Offline & private** — all data lives in your browser via `localStorage`; nothing is sent anywhere.

## Architecture

The whole app is intentionally simple — a single static page with no dependencies or tooling.

```
.
├── index.html      # The entire app: HTML, CSS, and vanilla JS in one file
└── sets/           # Sample flashcard decks as JSON
    ├── fun-facts.json
    ├── advanced-vocab.json
    ├── world-capitals.json
    └── space-astronomy.json
```

- **One file, no framework.** `index.html` contains the markup, all styles (a CSS-variable theme with a dark-mode override via `prefers-color-scheme`), and the application logic in plain JavaScript — no React, no bundler, no `node_modules`.
- **Client-side state.** Cards are kept in memory and persisted to `localStorage` under the key `flashcards_v2`. The app migrates data from older versions automatically, so your cards survive page reloads.
- **Sample decks.** The sample sets are bundled both inline in `index.html` and as standalone JSON files in `sets/` (same `{ front, back, tag }` shape), so they can be loaded instantly and also serve as a reference for the import format.

That's the whole stack — open the file and it runs.

## Running locally

Because it's a static page, you have two options.

### Option 1 — Open the file directly

Just open `index.html` in any modern browser (double-click it, or drag it into a browser window). This is enough to use every feature, since the sample decks are embedded in the page.

### Option 2 — Serve it (recommended)

Running a tiny static server avoids any `file://` quirks and matches how you'd host it. From the project root:

```bash
# Python 3
python3 -m http.server 8000

# …or Node
npx serve .
```

Then visit **http://localhost:8000** in your browser.

## Importing your own cards

Use **Import** in the header to load a JSON file shaped like the sample sets:

```json
[
  { "front": "What is the capital of France?", "back": "Paris", "tag": "Geography" }
]
```

`tag` is optional. Use **Export** to download your current deck in the same format.
