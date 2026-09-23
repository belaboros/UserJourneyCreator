# Business decisions

Decisions about **what** the product does and for whom. Each entry lists who decided, the alternatives, and the reasoning.

**Decided by:**
- **Bela:** decided or confirmed by Bela.
- **Claude, open:** Claude proposed or built it and Bela hasn't confirmed it. Confirm or reverse these.

A decision is never deleted. When one changes, its status becomes *Replaced by BD-xx* and the new decision gets a new number.

---

### BD-01 · An end-to-end journey is made of sub-journeys
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-01)
- **Decision:** The core model is one end-to-end journey made of several sub-journeys, each with its own steps.
- **Alternatives:** A flat list of steps, or stages nested inside stages as in a classic journey map.
- **Reasoning:** This is how Bela thinks about the work: several parallel workstreams that together form one journey.

### BD-02 · Show sub-journeys as parallel lanes flowing top to bottom
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-03). This replaced the first version's horizontal journey map.
- **Decision:** Each sub-journey is a lane, and its steps flow from top to bottom. The lanes sit side by side.
- **Alternatives:**
  - A classic horizontal journey map, with stage bands, step cards, an emotion curve and rows of pain points. It was built first and replaced.
  - A single flowchart without lanes.
- **Reasoning:** The sub-journeys run in parallel, so parallel lanes show that at a glance. Top to bottom matches how people read a process.

### BD-03 · Sync lanes with AND-gateways and AND-joins at gate steps
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-03)
- **Decision:**
  - An AND-gateway forks the flow into lanes.
  - An AND-join is a named gate step, such as "Product approval". It starts only when every lane that joins it has arrived.
  - After the gate step, those lanes fork again and continue in their own lanes.
- **Alternatives:**
  - A join that ends the lanes, with the rest of the journey continuing as one single flow.
  - Loose dependency arrows between individual steps.
- **Reasoning:** In the data-product example, all three workstreams stop at the same approval points and then carry on separately. The same gate step in several lanes needs to become one shared node.

### BD-04 · Write journeys as text, like PlantUML
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-02)
- **Decision:** Journeys are written as text in an editor, and the diagram is generated from that text. Nobody drags boxes around.
- **Alternatives:** A drag-and-drop diagram editor.
- **Reasoning:** Text is quick to write, easy to review in git and easy to generate. PlantUML is the familiar model.

### BD-05 · Support two formats and let each user choose
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-06, Q-04, Q-06)
- **Decision:** Journeys can be written in a PlantUML-like format or in YAML. Both describe exactly the same thing, and Convert switches between them.
- **Alternatives:**
  - **PlantUML-like only.** Claude recommended this: it's shorter to type, a mistake only affects one line, it needs no library, and git diffs are clearer.
  - **YAML only.** It's standard, other tools and scripts can read it, and a schema can check it.
- **Reasoning:** Users differ. Some prefer compact text and some prefer standard YAML, so the users decide.

### BD-06 · Name files `*.journey` and `*.journey.yaml`
- **Status:** Accepted · 2026-09-23. Proposed by Claude and accepted by Bela when he chose to keep both formats (Q-04).
- **Decision:** PlantUML-like files end in `.journey` and YAML files end in `.journey.yaml`.
- **Alternatives:**
  - **`*.e2euj.yaml`**, Bela's first suggestion. A `.yaml` extension on non-YAML text would make editors flag it as broken, and "e2euj" is hard to guess.
  - **`*.e2euj`.**
- **Reasoning:** Each name says what the file contains, and the YAML name still ends in `.yaml`, so editors treat it as YAML.

### BD-07 · Steps carry a tag, a score and details
- **Status:** Claude, open · 2026-09-23 (Q-09)
- **Decision:** A step can have a tag, such as an environment, an experience score from 1 to 5, and pain, gain, idea and note details.
- **Alternatives:** Steps with a name only.
- **Reasoning:** Tags make the EXP → DEV → ACC → PRD promotion visible. Scores and details come from classic journey mapping and cost nothing when unused.

### BD-08 · Lanes can start after a gate step, and can have sections
- **Status:** Claude, open · 2026-09-23 (Q-09)
- **Decision:**
  - `after <gate step>` starts a lane after that gate step without the lane joining it.
  - An indented `sub` inside a lane becomes a labeled section.
- **Alternatives:** Every lane starts at the start event.
- **Reasoning:** Real journeys often have a workstream that begins only after an approval.

### BD-09 · Public GitHub repo "UserJourneyCreator"
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-04). Bela created it on GitHub himself at 23:01, with an Apache 2.0 `LICENSE` as the first commit.
- **Decision:** The code and the spec live in a public GitHub repo named `UserJourneyCreator`, which holds the app, the docs, the examples and this spec.
- **Alternatives:** A private repo.
- **Reasoning:** Bela's choice.

### BD-10 · The data-product journey is the reference example
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-03, I-05 item 3)
- **Decision:** `examples/data-product.journey` and `examples/data-product.journey.yaml` hold Bela's data-product journey. The editor opens with it the first time.
- **Reasoning:** It's a real case that uses every core feature: three lanes and three AND-joins.
- **Note:** The tool names on the lanes are placeholders (Q-08).

### BD-11 · Work in a specification-driven way
- **Status:** Accepted · 2026-09-23 · Decided by Bela (I-07, and point 5 of I-05 as confirmed in Q-07)
- **Decision:** Ideas, questions and answers, the refined spec and all decisions are kept in `spec/` in the repo. Claude reads them at the start of every session and keeps them up to date.
- **Alternatives:** Keep this only in the Claude Project or in chat history.
- **Reasoning:** The repo is the one lasting place, and it can be read in any session and by anyone.

### BD-12 · Apache 2.0 license
- **Status:** Accepted · 2026-09-23 · Decided by Bela, who picked it when creating the GitHub repo
- **Decision:** The project is licensed under Apache License 2.0 (`LICENSE`).
- **Alternatives:** MIT, or no license (all rights reserved).
- **Reasoning:** Not recorded. Apache 2.0 is a permissive license that also grants patent rights. It is compatible with the MIT-licensed js-yaml that `index.html` includes (AD-04).

### BD-13 · Twelve themes, chosen with a picker
- **Status:** Accepted · 2026-09-24 · Decided by Bela (I-08, Q-10, Q-11, Q-13, Q-14, Q-15)
- **Decision:**
  - Journeyline ships 12 themes:
    - light, multi-color: Harbor, Stone, Vivid, Pastel
    - light, single-color: Mono Ink, Forest
    - dark, multi-color: Harbor Night, Midnight, High Contrast
    - dark, single-color: Graphite, Blueprint, Amber Terminal
  - A **Theme** button in the top bar opens a picker with the 12 themes as tiles in those four groups.
  - Hovering over a tile, or moving to it with the arrow keys, previews it. Click or Enter applies it, and Esc goes back.
  - **Apply to** sets the editor and the diagram together by default. You can also set either one on its own.
  - An optional toggle, off by default, follows the computer's light or dark mode, with one theme chosen for each mode.
  - Alt+T switches to the next theme.
  - The choice is saved per person, in the browser.
  - **Copy SVG** copies the diagram in the theme shown on screen.
- **Alternatives:**
  - a plain dropdown
  - fewer themes
  - the editor and diagram always chosen separately
  - always following the computer's mode
  - Copy SVG always in a light, document-friendly theme
- **Reasoning:** Bela wanted all the options. The picker shows the colors before you choose. Keeping one theme for both by default makes the common case simple, and the split covers slides. What you see is what you copy.

### BD-14 · A journey file can set its diagram theme for everyone
- **Status:** Accepted · 2026-09-24 · Decided by Bela (Q-12)
- **Decision:**
  - The optional line `theme <name>` (PlantUML-like) or `theme: <name>` (YAML) draws that file's diagram in the named theme for everyone who opens it. It overrides the person's own diagram choice.
  - The editor theme stays personal.
  - An unknown name is listed as a mistake, and the diagram falls back to the personal choice.
- **Alternatives:**
  - **Personal setting only.** Claude recommended this, because it keeps the file format unchanged.
  - **A suggestion that each person can override.**
- **Reasoning:** A shared diagram should look the same for everyone who opens the file.
