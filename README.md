# UserJourneyCreator

Journeyline is a small editor for user journeys. You write the journey as text, and it draws the journey as a flow while you type.

An end-to-end journey is made of **sub-journeys**. Each sub-journey is drawn as its own lane, and its steps flow from top to bottom. The lanes sit side by side and run in parallel:

- An **AND-gateway** forks the flow into several sub-journeys that run at the same time.
- An **AND-join** is a shared gate step. Every sub-journey that joins it must arrive before the gate step starts. After the gate step, the sub-journeys fork again and continue.

## Run it

Journeyline is one HTML file with nothing to install and no server. Download or clone this repo and open `index.html` in a modern browser. It works offline. The IBM Plex fonts load from Google Fonts when you are online, and system fonts are used otherwise.

## Files

Journeys are ordinary text files on your computer. You can write them in either of two formats, and each person can pick the one they like:

| Format | File name | Good for |
|---|---|---|
| PlantUML-like | `*.journey` | Quick to type and read, one line per step |
| YAML | `*.journey.yaml` | Standard YAML that other tools and scripts can read |

Both formats describe exactly the same thing. **Convert** switches the open journey to the other format. Comments are not carried over when you convert.

| Action | How |
|---|---|
| New journey | **New**, then choose a format |
| Open a file | **Open** or Ctrl+O, or drop the file on the editor |
| Save | **Save** or Ctrl+S |
| Save under a new name | **Save as** or Ctrl+Shift+S |

How saving works depends on the browser:

- **Chrome, Edge and other Chromium browsers:** Save writes straight back to the file you opened.
- **Firefox and Safari:** these browsers don't let web pages write to your files, so each save downloads a new copy.

Your latest edits are also kept in the browser, so closing the tab doesn't lose them.

## Using the editor

- The flow on the right redraws as you type.
- Click anything in the flow to jump to its line. Moving the cursor in the text highlights the matching card.
- Mistakes are listed under the editor with their line numbers.
- **Copy SVG** copies the diagram so you can paste it into docs or slides.

## Themes

The **Theme** button opens a picker with 12 themes: light and dark, multi-color and single-color. Hovering over a tile previews it, and clicking applies it. Alt+T switches to the next theme.

- **Apply to:** set the editor and diagram together, or each on its own. For example, use a dark editor for yourself and a Vivid diagram for slides.
- **Follow my computer's light or dark mode:** choose one theme for each mode, and Journeyline switches with your computer.
- **The `theme` line:** a journey file can set its own diagram theme with `theme Vivid` (or `theme: Vivid` in YAML). Everyone who opens the file then sees the diagram in that theme.
- **Copy SVG** copies the diagram in the theme you see.

## Example

`examples/` has the same journey in both formats: a team creating a data product, with a data contract, a data pipeline and a compute cluster built in parallel.

```
start Team decides to create a data product

sub Data contract : Contract editor
  - Create candidate data contract : EXP
  - Register candidate data contract to the catalog : EXP
  join Product approval
  - Promote data contract : DEV
```

```yaml
start: Team decides to create a data product

subJourneys:
  - name: Data contract
    tool: Contract editor
    flow:
      - step: Create candidate data contract
        tag: EXP
      - step: Register candidate data contract to the catalog
        tag: EXP
      - join: Product approval
      - step: Promote data contract
        tag: DEV
```

The full reference for both formats is in [docs/syntax.md](docs/syntax.md).

## How this project is specified

The project is developed spec-first. The [spec/](spec/) folder holds the original ideas, the questions and answers, the product spec, and the business and architecture decisions with their alternatives and reasoning. [CLAUDE.md](CLAUDE.md) describes how Claude keeps them up to date.

## Third-party code

`index.html` includes [js-yaml](https://github.com/nodeca/js-yaml) 4.1.0 (MIT license) so that YAML files work offline.

## License

[Apache License 2.0](LICENSE).
