# Marginalia

> **This is a clone of [icanwrite.app](https://icanwrite.app/).** It was built as a look-alike study of that product. The concept, the feature set, the page structure and the 29-check catalogue are theirs. This project is not affiliated with icanwrite and is not a substitute for it; if you want the real editor, go to icanwrite.app.

A markdown editor for novelists with AI in the margins, as a single-file web app.

Live page: https://claude.ai/artifact/YHP1XbEU5JB9Rt761xF3rE

## What it does

- **Landing page** with feature sections, the 29-check catalogue and an FAQ.
- **Editor** at `#write`: file list with word counts, colour tags, reorder, rename and delete; serif, sans or mono manuscript sheet; Zen Mode; live preview; word and character counts per file and per project.
- **Local folders** through the File System Access API (Chrome or Edge, top-level window). Saves write back to disk while the folder is connected; the folder handle is remembered in IndexedDB, so after a reload one click reconnects it. Files changed on disk (for example in Obsidian) are re-read when you return to the tab, and a two-sided change is reported rather than silently overwritten. Adding a folder keeps the in-browser project aside; "leave folder" restores it. Elsewhere the app uses the in-browser project kept in local storage, and tells you when storage is full instead of claiming a save.
- **Checks**: 29 built-in checks grouped as Story, Line edit, Copyedit, Proofing and Writers. Six (Repetitions, Muscular verbs, Cliché, Show don't tell, Pacing, Punctuation) have a pattern-matching version that runs with no connection at all; when the AI is available they use it instead. The rest, and any custom checks, call Claude through the artifact's `sample` capability. Results arrive as comments anchored to the nearest occurrence of the quoted passage, with Apply (undoable with Ctrl+Z), Chat and Dismiss. Per-project **AI rules** (Settings) are sent with every check and chat message. Checks or messages started while offline are queued and run when the connection returns.
- **Chat** about a selected passage, with editable snippet shortcuts (variants, simplify, punch up), streaming replies, insert-at-cursor and copy. Failed requests are shown as errors and dropped from the history sent to the model.
- **Model tier** (Quick, Default, Complex) set in Settings and switchable from the top bar.
- **Export** of chosen chapters to Markdown, HTML with four themes, or plain text, saved through the artifact's `downloads` capability.

## Files

- `index.html` — the whole app. It is written as an artifact page: the publish step wraps it in a document skeleton, so the file starts with `<title>` rather than `<!doctype html>`. Markdown preview and HTML export use `marked` and `DOMPurify` from cdnjs, with a small built-in renderer as the fallback when those scripts cannot load.

## Running it outside claude.ai

Open `index.html` in a browser, or serve the folder with any static server. Everything works except the AI checks, chat and the download button, which rely on `window.claude` capabilities that only exist inside the claude.ai artifact viewer. Outside it the app says so and keeps the six offline checks; Export falls back to Copy or a text box. Over plain `http://` the clipboard API is unavailable and the text-box fallback is used.

## Known limits

- Opening a folder needs the page in its own tab in Chrome or Edge; inside an embedded frame the picker may be refused, and the app then says so.
- Only `.md`, `.markdown` and `.txt` files at the top level of the chosen folder are opened. Subfolders are skipped.
- Renaming does not rename the file on disk, and deleting removes a file from the project only.
- No EPUB or Word import or export, and no Scrivener sync.
- The offline pattern checks are deliberately narrow (for example, Muscular verbs offline only finds -ly adverbs). The AI versions of the same checks read for the full intent.

## Publishing changes

Edit `index.html` and republish it to the artifact URL above from a Claude Code session.
