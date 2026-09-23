# Working on UserJourneyCreator with Claude

This project uses **specification-driven development**. The `spec/` folder holds everything Bela and Claude have agreed on, and it is the source of truth.

## At the start of every session

1. Read, in this order:
   - `spec/03-product-spec.md`: what the product is now
   - `spec/04-business-decisions.md` and `spec/05-architecture-decisions.md`: what was decided and why
   - `spec/02-questions-and-answers.md`: especially questions marked **OPEN**
   - `spec/01-ideas.md`: Bela's own words, when you need the original intent
2. If an open question matters for the task, ask it before building.
3. Do not contradict an accepted decision without saying so. If a change reverses one, ask first, then record the change.

## While working

- **New idea from Bela:** add it to `spec/01-ideas.md` as `I-nn`, word for word apart from typo fixes.
- **Question asked:** add it to `spec/02-questions-and-answers.md` as `Q-nn` with **OPEN** in its heading. When Bela answers, fill in the answer, remove OPEN and link the decision it led to.
- **Decision made:** add `BD-nn` (what and for whom) or `AD-nn` (how it's built) with status, who decided, alternatives and reasoning.
  - Mark decisions Claude made alone as **Claude, open**, and point them out to Bela.
  - Never delete a decision. Set its status to *Replaced by …* and add a new one.
- **Behavior changed:** update `spec/03-product-spec.md`, meaning the requirements and the status line, so it always describes the product as it should be now.
- **Code changed:** update `README.md`, `docs/syntax.md` and both files in `examples/` when they are affected.
- Commit the spec changes together with the code change they explain.

## Project rules

- The app is one self-contained file, `index.html` (AD-01). It uses no build step and no external scripts. The only external request is the Google Fonts stylesheet, and system fonts work without it.
- Both file formats must keep working and stay convertible without losing content (BD-05, AD-03).
- `examples/data-product.journey` and `examples/data-product.journey.yaml` must describe the same journey.
- Before committing, open `index.html` headlessly and check:
  - no page errors
  - both examples parse without warnings into the same model
  - converting text → YAML → text gives back the same journey
