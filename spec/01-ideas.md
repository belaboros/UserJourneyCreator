# Ideas

Bela's high-level ideas in his own words, oldest first. Nothing here is edited except for small typo fixes. These entries are the raw input. The refined version is in [03-product-spec.md](03-product-spec.md).

---

### I-01 · 2026-09-23 · Journeys are made of sub-journeys
> A user journey consists of multiple sub-user-journeys.

### I-02 · 2026-09-23 · Text in, diagram out
> I want to use a text format to define a user journey.
> The user can edit the text file just like PlantUML document on the left-side and the right-side visualizes the user journey as a diagram.

### I-03 · 2026-09-23 · Parallel sub-journeys with AND-gateways and AND-joins
> A sub-user-journey should be visualized as a top-to-down flow of steps.
>
> If the end-to-end user journey consists of 3 sub-user-journeys, then there should be 3 flows next to each other side-by-side, each of them flowing top-to-bottom.
>
> AND-gateway: forks the flow into 2 or more sub-user-journeys. Each of them should happen in parallel.
>
> AND-join: connects execution from 2 or more sub-user-journeys. Each user journey should arrive there before the next step or steps may start.

Example given with this idea:

- A team wants to create a data product.
- They have to create 3 resources: a data contract, a data pipeline and a compute cluster.
- There is a sub-user-journey for each of them, running in parallel with a few AND-gateway and AND-join nodes.
- **Data contract:** create candidate data contract in the EXP environment → register candidate data contract to the catalog → AND-join to "product approval" → promote data contract to DEV → add data quality rules → pass contract tests → AND-join to "product review" → promote data contract to ACC → pass end-to-end integration tests → pass end-to-end UAT tests → AND-join to "final approval" → promote data contract to PRD.
- **Compute cluster:** create a compute cluster visually in the EXP environment → AND-join to "product approval" → migrate / promote the compute cluster to DEV → optimize and reconfigure the cluster for cost and performance → AND-join to "product review" → migrate / promote to ACC → optimize and reconfigure for cost and performance → AND-join to "final approval" → migrate / promote to PRD.
- **Data pipeline:** create data pipeline in a notebook in the EXP environment → deploy and run the pipeline on the compute cluster → pass functional tests (for example, the generated data table complies with the data contract) → AND-join to "product approval" → promote to DEV → migrate / reimplement the business logic from notebook to PySpark → implement unit tests → AND-join to "product review" → promote to ACC → pass end-to-end integration tests → pass end-to-end UAT tests → AND-join to "final approval" → promote to PRD.
- The 3 sub-user-journeys are performed by the same team, mostly in parallel, using different tools.

### I-04 · 2026-09-23 · Public GitHub repo
> Can you create a GitHub repo for me with the "UserJourneyCreator" as the repo name?
> It should be a public GitHub repo.

### I-05 · 2026-09-23 · How the application should work
> 1. The application runs locally on any modern computer
> 2. The user journey files are saved/loaded to/from the local filesystem
> 3. Save the sample user journey file to the git repo as an example
> 4. Let's use the `*.e2euj.yaml` filename pattern (let me know if you have a better suggestion)
> 5. *(left unfinished at the time. Bela later said it meant the specification-driven development in I-07, see Q-07)*

### I-06 · 2026-09-23 · Keep both formats
> Let's keep both formats. The users will decide which one they prefer.

### I-07 · 2026-09-23 · Work in a specification-driven way
> Can I use you to work in an SDD (Specification-Driven Development) way?
> Store extra files in the git repo: my high-level ideas, the questions you asked, my answers, the refined and more complete idea, the list of business decisions (with the alternatives and the reasoning, if there is any), and the list of architectural decisions (e.g. this is a single HTML file rather than a locally running server, because it is simpler and Chrome/Edge is OK for my users). Save all this valuable information into the UserJourneyCreator GitHub repo and use it next time I work on it with you.

### I-08 · 2026-09-24 · Selectable color themes (first incremental feature)
> Let's start the first incremental feature. Idea: the user can select from multiple color palettes/themes both for the text editor and for the diagrams.
> Show me multiple light, dark, single-color and multi-color options to choose from.
