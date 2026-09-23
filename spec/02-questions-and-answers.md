# Questions and answers

The questions Claude asked and Bela's answers, oldest first. **Open** questions are still waiting for an answer. When an answer leads to a decision, the entry links to it.

---

### Q-01 · 2026-09-23 · What should we do with the idea of sub-journeys?
**Asked:** Should I map a specific journey into sub-journeys, draw it as a diagram, define a data model, or something else?
**Answer:** A text format like PlantUML, with the editor on the left and a live diagram on the right (I-02).
**Led to:** BD-02, AD-01

### Q-02 · 2026-09-23 · Should the repo be private or public?
**Asked:** Not asked outright. Claude was about to create the repo as private, which is the safe default.
**Answer:** Public (I-04).
**Led to:** BD-09

### Q-03 · 2026-09-23 · Empty repo, or with the editor in it?
**Asked:** When you're signed in, should I push the editor, README, syntax reference and example, or create an empty repo?
**Answer:** Bela created the public repo on GitHub himself, with an Apache 2.0 license. The app, docs, examples and spec are pushed on top of that first commit.
**Led to:** BD-09, BD-12

### Q-04 · 2026-09-23 · `.e2euj.yaml` suggests YAML. Which format do you want?
**Asked:** The PlantUML-like text isn't YAML, so a `.yaml` extension would make editors flag it as broken. Keep the PlantUML-like format with its own extension, or switch to YAML? If YAML, `*.journey.yaml` reads more clearly than `*.e2euj.yaml`.
**Answer:** Asked which one Claude recommends. Claude recommended the PlantUML-like format. Then asked to see both side by side, and decided to keep both (I-06).
**Led to:** BD-05, BD-06

### Q-05 · 2026-09-23 · One HTML file or a small local server?
**Asked:** Should the app be one HTML file with nothing to install, or a small local server started with `npx` or Python?
- **One HTML file:** in Chrome and Edge it saves straight to your files. In Firefox and Safari, each save downloads a new copy.
- **Local server:** it works the same in every browser, can list every journey in a folder, and redraws when a file changes in VS Code. You need Node or Python installed.

**Answer:** "I prefer the One HTML file, nothing to install option." Later reason (I-07): simpler, and Chrome/Edge is fine for the users.
**Led to:** AD-01, AD-02

### Q-06 · 2026-09-23 · Do you recommend YAML or the PlantUML-like format?
**Asked by Bela.** Claude recommended the PlantUML-like format:
- It's about half the typing.
- One wrong indent can't break the whole file.
- It needs no YAML library.
- Git diffs are clearer.

Claude noted that YAML wins when other tools must create or read the files.
**Answer:** Keep both, and let users choose (I-06).
**Led to:** BD-05

### Q-07 · 2026-09-23 · OPEN · What was point 5?
**Asked:** Your list of how the app should work stopped at "5.". What was it?
**Answer:** *(open)*

### Q-08 · 2026-09-23 · OPEN · Which tools does each sub-journey use?
**Asked:** The example's tools (Contract editor, Notebook then PySpark, Cluster console) are placeholders Claude made up. Which tools does the team really use?
**Answer:** *(open)*

### Q-09 · 2026-09-23 · OPEN · Keep the features Claude added without being asked?
**Asked:** Claude added these on its own:
- `after` (a lane that starts after a gate step without joining it)
- sections inside a lane
- experience scores from 1 to 5
- `pain`, `gain`, `idea` and `note` details
- tags such as EXP, DEV, ACC and PRD

Should they stay?
**Answer:** *(open)*. They stay until you decide otherwise. See BD-07 and BD-08.

### Q-10 · 2026-09-24 · OPEN · Which themes should ship?
**Asked:** Claude showed 12 options in a gallery. Each one is applied to the real editor and flow diagram:
- **Light, multi-color:** 01 Harbor (the current look), 03 Stone, 04 Vivid, 05 Pastel
- **Light, single-color:** 06 Mono Ink, 07 Forest
- **Dark, multi-color:** 02 Harbor Night (the current dark look), 08 Midnight, 09 High Contrast
- **Dark, single-color:** 10 Graphite, 11 Blueprint, 12 Amber Terminal

Which ones should Journeyline include?
**Answer:** *(open)*

### Q-11 · 2026-09-24 · OPEN · One theme for both editor and diagram, or separate choices?
**Asked:** Should one choice style both the editor and the diagram? Or should they be chosen separately, for example a dark editor with a light diagram for slides?
**Answer:** *(open)*

### Q-12 · 2026-09-24 · OPEN · Where is the choice remembered?
**Asked:**
- **(a)** Per person, in their browser only.
- **(b)** In the journey file, for example `theme Vivid` or `theme: Vivid`, so a diagram looks the same for everyone who opens it.
- **(c)** Both. The file sets the diagram theme, and each person can override it for themselves.

**Answer:** *(open)*

### Q-13 · 2026-09-24 · OPEN · Follow the computer's light or dark mode?
**Asked:** Should Journeyline switch between a light theme and its dark partner (such as Harbor and Harbor Night) when the operating system switches? Or should the chosen theme stay fixed?
**Answer:** *(open)*

### Q-14 · 2026-09-24 · OPEN · Which theme does Copy SVG use?
**Asked:** Should the copied diagram use the theme on screen, or always a document-friendly light theme such as Harbor or Mono Ink?
**Answer:** *(open)*
