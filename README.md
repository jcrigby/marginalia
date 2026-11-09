# writerhelper

> **This is a clone of [icanwrite.app](https://icanwrite.app/).** It was built as a look-alike study of that product. The concept, the feature set, the page structure and the 29-check catalogue are theirs. This project is not affiliated with icanwrite and is not a substitute for it; if you want the real editor, go to icanwrite.app.

A markdown editor for novelists with AI in the margins, as a single-file web app.

Live page: https://claude.ai/artifact/YHP1XbEU5JB9Rt761xF3rE

## What it does

- **Landing page** with feature sections, the 29-check catalogue and an FAQ.
- **Editor** at `#write`: file list with word counts, colour tags, reorder, rename and delete; serif, sans or mono manuscript sheet; Zen Mode; live preview; word and character counts per file and per project.
- **Local folders** through the File System Access API (Chrome or Edge). Saves write back to disk. Elsewhere it falls back to an in-browser project kept in local storage.
- **Checks**: 29 built-in checks grouped as Story, Line edit, Copyedit, Proofing and Writers. Six run offline as pattern matching (Repetitions, Muscular verbs, Cliché, Show don't tell, Pacing, Punctuation). The rest, and any custom checks, call Claude through the artifact's `sample` capability and return comments anchored to the text, with Apply, Chat and Dismiss.
- **Chat** about a selected passage, with editable snippet shortcuts (variants, simplify, punch up).
- **Export** of chosen chapters to Markdown, HTML with four themes, or plain text, saved through the artifact's `downloads` capability.

## Files

- `index.html` — the whole app. It is written as an artifact page: the publish step wraps it in a document skeleton, so the file starts with `<title>` rather than `<!doctype html>`.

## Running it outside claude.ai

Open `index.html` in a browser, or serve the folder with any static server. Everything works except the AI checks, chat and the download button, which rely on `window.claude` capabilities that only exist inside the claude.ai artifact viewer. Outside it the app says so and keeps the six offline checks.

## Publishing changes

Edit `index.html` and republish it to the artifact URL above from a Claude Code session.
