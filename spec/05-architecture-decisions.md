# Architecture decisions

Decisions about **how** the product is built. Each entry uses the same format as the business decisions. **Decided by: Claude, open** marks decisions Claude made while building that Bela hasn't reviewed yet.

---

### AD-01 · A single self-contained HTML file, not a local server
- **Status:** Accepted · 2026-09-23 · Decided by Bela (Q-05, I-07)
- **Decision:** The whole app is one file, `index.html`, with its HTML, CSS, JavaScript and libraries inlined. You open it in a browser, and there is no build step, install or server.
- **Alternatives:**
  - **A small local server started with `npx` or Python.** It works the same in every browser, can list every journey in a folder, and can redraw when a file is edited in VS Code. It needs Node or Python installed.
  - **A desktop app built with Electron or Tauri.** It's heavy to build and distribute.
- **Reasoning:** It's simpler, and Chrome or Edge is fine for Bela's users.
- **Consequences:**
  - Firefox and Safari can't save back to the opened file (AD-02).
  - The app can't list the files in a folder.

### AD-02 · Local files through the File System Access API, with a download fallback
- **Status:** Accepted · 2026-09-23. It follows from AD-01.
- **Decision:**
  - Open and Save use `showOpenFilePicker` and `showSaveFilePicker`, and the app keeps the file handle so that Save overwrites the same file.
  - Without that API (Firefox, Safari, or inside an iframe): Open uses a file input, and Save downloads a new copy.
  - A dropped file uses `getAsFileSystemHandle` when the browser has it.
- **Alternatives:** Downloads only in every browser. That's simpler, but Chrome and Edge users would lose save-in-place.
- **Reasoning:** It gives the best experience in the browsers the users have, and still works everywhere.

### AD-03 · Both formats are parsed into one journey model
- **Status:** Accepted · 2026-09-23. It follows from BD-05.
- **Decision:**
  - Both parsers fill one in-memory model through a shared builder: lanes, steps, gates, start and end.
  - The layout, the drawing and the checks only ever see that model.
  - Two serializers write the model back out, `toText` and `toYaml`, and Convert uses them.
- **Alternatives:** Treat YAML as the main format and convert the PlantUML-like text into YAML first.
- **Reasoning:** Each format stays a full equal, and every feature works the same in both.
- **Consequences:**
  - The model doesn't keep comments, so Convert drops them.
  - The headless tests check that converting the example text → YAML → text gives back the same journey.

### AD-04 · The YAML library is inlined in the file
- **Status:** Accepted · 2026-09-23 · Decided by Claude, and it follows from AD-01
- **Decision:** js-yaml 4.1.0 (MIT license, about 39 KB minified) is pasted into `index.html`.
- **Alternatives:**
  - **Loading it from a CDN.** The app would then break offline.
  - **A hand-written parser for part of YAML.** It's fragile and surprises people who know YAML.
- **Reasoning:** The app keeps working offline as one file.

### AD-05 · Hand-built SVG layout instead of a diagram library
- **Status:** Claude, open · 2026-09-23
- **Decision:** The app does its own lane layout and draws SVG directly.
  1. Gate steps are put in order with a topological sort of each lane's sequence.
  2. Each lane is placed up to its next gate step.
  3. The gate is placed below the lowest lane that joins it.
  4. The joined lanes fork again below the gate.
- **Alternatives:**
  - **PlantUML:** it needs a server or Java.
  - **Mermaid:** it can't do lanes that sync on shared gate steps like this.
  - **draw.io or BPMN.js:** heavy, and they are made for manual editing.
- **Reasoning:** The layout is specific to this journey model and small enough to own, and it keeps the app to one file.

### AD-06 · Rules for the PlantUML-like format
- **Status:** Claude, open · 2026-09-23
- **Decision:**
  - The keywords are `title`, `persona`, `start`, `sub`, `-`, `join`, `after`, `end`, `pain`, `gain`, `idea` and `note`.
  - Fields are separated by a colon with whitespace before it, so `Deploy: run tests : DEV` keeps the colon in the name.
  - Indentation only matters for a `sub` inside a lane, which becomes a section.
- **Alternatives:** Split on every colon, which would make names containing a colon impossible.
- **Reasoning:** It's forgiving to type, and names can contain a colon.

### AD-07 · Plain textarea editor with a highlighting layer
- **Status:** Claude, open · 2026-09-23
- **Decision:**
  - The editor is a `<textarea>` with a syntax-highlighted `<pre>` behind it and its own line-number gutter.
  - Tab inserts two spaces, and Enter keeps the indentation.
  - Edits go through `execCommand('insertText')`, so undo keeps working.
- **Alternatives:** CodeMirror or Monaco. They would be richer, but make the file much larger and harder to inline.
- **Reasoning:** It keeps the single file small, and the formats are simple.

### AD-08 · Drafts are kept in the browser
- **Status:** Claude, open · 2026-09-23
- **Decision:** The current text, file name, format and unsaved state are stored in `localStorage` after every change and restored when the page opens. Every read and write is wrapped in try/catch.
- **Alternatives:** Nothing is kept, so closing the tab loses unsaved work.
- **Reasoning:** It's a cheap safety net. The file on disk remains the real copy.

### AD-09 · Theme-aware colors
- **Status:** Replaced by AD-11 · 2026-09-24 (was: Claude, open · 2026-09-23)
- **Decision:**
  - The app's colors are CSS variables for light and dark mode, and they follow the operating system or an explicit `data-theme`.
  - The diagram reads those variables when it draws, so a copied SVG has real colors in it.
- **Reasoning:** It's readable in both modes, and the exported SVG stays correct.

### AD-10 · The repo is the source of truth for the spec
- **Status:** Accepted · 2026-09-23 · Decided by Bela (BD-11)
- **Decision:** `spec/` in the repo holds the ideas, Q&A, product spec and decisions, and `CLAUDE.md` tells Claude how to use them. The Claude Project only keeps a pointer to the repo.
- **Reasoning:** One place that lasts and is under version control.

### AD-11 · How themes are built
- **Status:** Accepted · 2026-09-24 · Decided by Claude (implements BD-13 and BD-14). Replaces AD-09.
- **Decision:**
  - Each theme is a data object in `index.html` with:
    - `ui`: app and editor surfaces
    - `syn`: syntax colors
    - `det`: pain, gain, idea and note colors
    - `flow`: connector lines
    - `scores`: the 1–5 score colors
    - `lanes`: six lane color sets
    - `tags`: six tag color sets
    - `partner`: its light or dark counterpart, used when following the computer's mode
  - The editor theme is applied by setting CSS variables on the page from script.
  - The diagram is drawn straight from its theme object, so a copied SVG has real colors in it.
  - The choice is stored in `localStorage` under `journeyline-theme`. It has three slots: `fixed`, plus `light` and `dark` for following the computer's mode.
  - A file's `theme` line wins over the diagram slot.
  - Score numbers are black or white, whichever reads better on the score color.
  - The host page's own light or dark mode is no longer used.
- **Alternatives:**
  - CSS classes per theme. Harder to keep the editor and diagram separate, and the SVG would lose its colors.
  - Themes in a separate file. That would break the single-file rule (AD-01).
- **Reasoning:** One data object per theme keeps adding a theme to one place, and it works the same for the screen and the copied SVG.
- **Note:** The shortcut in the proposal was Ctrl+Shift+T. Chrome keeps that shortcut for reopening a closed tab, so it is Alt+T instead.
