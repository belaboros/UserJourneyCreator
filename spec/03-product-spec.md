# Product spec: Journeyline

The refined, current description of what the product is and does. It is built from [01-ideas.md](01-ideas.md) and [02-questions-and-answers.md](02-questions-and-answers.md). When something changes, this file is updated so that it always describes the product as it should be now.

**Status:** v0.4 · 2026-09-24 · implemented in `index.html`

## 1. Purpose

Teams describe how a user gets something done from end to end, such as a data team creating a data product. The journey is made of several sub-journeys that happen in parallel and must meet at approval points. Journeyline lets a person write that journey as text and see it immediately as a diagram that shows what runs in parallel and where everything must wait.

## 2. Users

- People who design or document processes, such as product owners, architects and platform teams.
- They use Chrome or Edge on their own computer (AD-01).
- They are comfortable with text formats such as PlantUML or YAML.

## 3. Concepts

| Concept | Meaning |
|---|---|
| End-to-end journey | The whole journey, with a title and a persona |
| Sub-journey | A part of the journey, often one resource or workstream, with an optional tool |
| Step | One thing the user does in a sub-journey |
| Start / end | Where the journey begins, forking into all sub-journeys, and ends, joining all of them |
| AND-gateway | Forks the flow into two or more sub-journeys that run in parallel |
| AND-join / gate step | A shared step that starts only when every sub-journey that joins it has arrived. Afterwards the joined sub-journeys fork again and continue |
| Tag | A short label on a step, such as the environment EXP, DEV, ACC or PRD |

## 4. Functional requirements

### Writing and viewing
- **FR-01** The screen is split: a text editor on the left and the diagram on the right. The divider can be dragged.
- **FR-02** The diagram redraws as the user types.
- **FR-03** Each sub-journey is a lane of steps flowing from top to bottom, and the lanes sit side by side (BD-02).
- **FR-04** AND-gateways and AND-joins are drawn as BPMN-style diamonds with a plus sign. The lanes that join a gate step merge on a bar into the gateway (BD-03).
- **FR-05** A lane that reaches a gate step early shows a longer line down to it, so the slowest lane is visible.
- **FR-06** Clicking anything in the diagram jumps to its line in the text. Moving the cursor in the text highlights the matching element.
- **FR-07** Mistakes are listed under the editor with line numbers and a plain explanation. The rest of the diagram still draws.
- **FR-08** Lanes reach their gate steps in a consistent order. If they don't, the editor warns, because those lanes could never all meet.
- **FR-09** Each tag value gets its own color.
- **FR-10** Zoom in and out, fit to width, and copy the diagram as SVG.

### Files
- **FR-11** Journeys are stored as local files in one of two formats: PlantUML-like `*.journey` or YAML `*.journey.yaml` (BD-05, BD-06).
- **FR-12** New (choose a format), Open, Save and Save as, with Ctrl+O, Ctrl+S and Ctrl+Shift+S. A file can also be opened by dropping it on the editor.
- **FR-13** In Chrome and Edge, Save writes straight back to the opened file. Other browsers download a copy (AD-02).
- **FR-14** The format is detected from the file name.
- **FR-15** **Convert** switches the open journey to the other format. Content is kept, but comments are not.
- **FR-16** Unsaved changes are shown. Discarding them needs a second click.
- **FR-17** The latest edits are kept in the browser, so closing the tab doesn't lose them.

### Content
- **FR-18** Steps can have a tag, a score from 1 to 5, and details: pain, gain, idea and note (BD-07).
- **FR-19** A lane can start after a gate step without joining it (`after`). A lane can contain labeled sections (BD-08).
- **FR-20** The repo contains the data-product example in both formats (BD-10).

### Themes
- **FR-21** 12 themes: 6 light and 6 dark, some multi-color and some single-color (BD-13).
- **FR-22** A **Theme** button opens a picker with the themes as tiles in four groups. Hovering over a tile, or moving to it with the arrow keys, previews it. Click or Enter applies it, and Esc goes back.
- **FR-23** **Apply to** sets the editor and diagram together (the default), or either one on its own.
- **FR-24** An optional "Follow my computer's light or dark mode" toggle, with one theme for light mode and one for dark mode.
- **FR-25** A `theme <name>` or `theme: <name>` line in a journey file sets that file's diagram theme for everyone (BD-14).
- **FR-26** The theme choice is saved per person in the browser. Alt+T switches to the next theme.
- **FR-27** Copy SVG uses the diagram theme on screen.

## 5. Non-functional requirements

- **NFR-01** Runs locally on any modern computer, with nothing to install and no server (AD-01).
- **NFR-02** Works offline. Only the fonts come from the internet, and system fonts are used when they can't load (AD-04).
- **NFR-03** It is one self-contained file, `index.html` (AD-01).
- **NFR-04** Every theme is readable, and the screen is usable on a narrow screen, where the panes stack.
- **NFR-05** The repo is public on GitHub as `UserJourneyCreator` (BD-09).

## 6. Out of scope for now

- Collaboration or shared editing
- A server, accounts or a database
- OR and XOR gateways (only AND)
- Exporting to BPMN, PlantUML or Mermaid

## 7. Open items

No open questions as of 2026-09-24. Architecture decisions AD-05 to AD-08 are still marked **Claude, open** for Bela's review.
