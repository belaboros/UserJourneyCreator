# Journey syntax

A journey can be written in two formats that describe the same thing. Journeyline reads both, and **Convert** switches between them.

- **PlantUML-like**, in files named `*.journey`
- **YAML**, in files named `*.journey.yaml`

## Concepts

| Concept | Meaning | Drawn as |
|---|---|---|
| Journey | The end-to-end journey, with a title and a persona | The diagram |
| Start / end | Where the journey begins and ends | Circles. The start forks into all lanes, and the end joins all lanes |
| Sub-journey | A part of the journey, optionally with the tool used for it | A lane whose steps flow from top to bottom |
| Step | One thing the user does | A card, with an optional tag and a score from 1 to 5 |
| Gate step (join) | A step that waits until every lane that joins it has arrived | Lanes merge into an AND-gateway, then the gate step, then an AND-gateway that forks them again |
| After | A lane that starts after a gate step without joining it | The lane leaves from the gate's fork |
| Section | A labeled group of steps inside a lane | A pill label in the lane |
| Details | `pain`, `gain`, `idea` and `note` on a step, gate, start or end | Colored lines inside the card |

Gate steps are matched by name, and case doesn't matter. `join Product approval` in three lanes creates one shared gate step. Every lane must reach its gate steps in the same order. Otherwise the lanes could never all meet, and the editor shows a warning.

## PlantUML-like (`*.journey`)

| Line | Meaning |
|---|---|
| `@startjourney` / `@endjourney` | Optional wrappers |
| `title <text>` | Title |
| `persona <text>` | Persona (`actor` also works) |
| `theme <name>` | Optional. Draws the diagram in this theme for everyone who opens the file |
| `start <text>` | Start event |
| `sub <name> : <tool>` | A sub-journey. The tool is optional |
| `  - <step> : <tag>` | A step. The tag is optional |
| `  - <step> : <1-5> : <tag>` | A step with a score |
| `  join <gate step>` | AND-join at a shared gate step |
| `  after <gate step>` | Start this lane after the gate step |
| `  sub <name>` | Indented under a lane, this is a section |
| `    pain / gain / idea / note <text>` | A detail for the line above |
| `end <text>` | End event |
| `' comment` | Ignored |

Fields are separated by a colon with a space before it. So `- Deploy: run tests : DEV` has the step name "Deploy: run tests" and the tag "DEV".

## YAML (`*.journey.yaml`)

```yaml
title: Create a data product
persona: Data product team
theme: Vivid                                    # optional, see Themes below
start: Team decides to create a data product    # or an object: {name: ..., note: ...}

subJourneys:
  - name: Data contract
    tool: Contract editor                       # optional
    flow:
      - step: Create candidate data contract
        tag: EXP                                # optional
        score: 4                                # optional, 1-5
        pain: Too many fields to fill in        # text, or a list of texts
      - Register candidate data contract        # a plain string is a step too
      - join: Product approval                  # AND-join
        note: Needs the data owner              # details on the gate step
      - section: Promotion                      # a label inside the lane
      - after: Final approval                   # start after a gate step

end: Data product is live in PRD
```

| Key | Where | Meaning |
|---|---|---|
| `title`, `persona` | top level | Text |
| `theme` | top level | Optional theme name for the diagram |
| `start`, `end` | top level | Text, or an object with `name`, `tag`, `score` and details |
| `subJourneys` | top level | A list of sub-journeys |
| `name`, `tool`, `flow` | sub-journey | `flow` lists the steps and gates in order |
| `step`, `join`, `after`, `section` | flow item | Exactly one of these per item |
| `tag`, `score`, `pain`, `gain`, `idea`, `note` | step, gate, start or end | Optional |

## Themes

The `theme` line draws the diagram in one of these themes, for everyone who opens the file. Case, spaces and hyphens don't matter, so `theme high contrast` and `theme High-Contrast` both work.

| | Multi-color | Single-color |
|---|---|---|
| **Light** | Harbor, Stone, Vivid, Pastel | Mono Ink, Forest |
| **Dark** | Harbor Night, Midnight, High Contrast | Graphite, Blueprint, Amber Terminal |

Without a `theme` line, each person's own choice in the Theme picker is used.

