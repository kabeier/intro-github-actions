# Live demo runbook: GitHub Actions

**The story:** this topic lives on github.com. You and the students push real repos and watch the **Actions** tab. The slides show what real runs look like; every one came from **[kabeier/gh-actions-demo](https://github.com/kabeier/gh-actions-demo/actions)**, which is also your backup if GitHub is slow in class.
- **Lecture 1 (Intro to Workflows):** Event → Workflow → Job → Steps, why CI, the Marketplace, YAML, `hello-world.yml`, the Actions tab, triggers, a branch filter. Student repo: `hello-actions`.
- **Lecture 2 (Managing Workflows):** the lesson's factorial project, confirmed locally in the slide editor, then `run-tests.yml` on `dev`, a red run, a PR into `main`, `workflow_dispatch`, workflows as code, the Docker version. Student repo: `ci-factorial`.

## The demo repo (your backup)

| Where | What it shows |
|---|---|
| Actions tab | Every run: Hello World (any branch), Run Test Suite (dev, PR, manual, Docker), one deliberate red run ("Break a test on purpose") |
| PR #1 (dev → main, merged) | The Run Test Suite check on a pull request |
| PR #2 (feature-greeting → dev) | A PR **into dev**: Run Test Suite does **not** run (it only watches PRs into main) |
| branches `example-*` | Real failures for the activity: broken YAML, YAML typo, a tab, no checkout, no Jest, no pip install pytest, Docker without checkout, a failing test in Docker; plus `example-node-20` (no EBADENGINE warnings) |
| branches `template-*` | The homework templates, each green: Hello Workflows, Jest, pytest |

No `schedule:` workflow is in the demo repo on purpose (it would run every night).

## Setup (before Lecture 1)

- Logged in to github.com in your browser; `git push` works from your terminal (you've pushed before).
- Tabs: the deck, the demo repo's Actions tab, Code Lab 1 / 2, the activity.
- Lecture 2 uses the slide editor for the local test: open the deck in **Chrome** with internet once.

## Lecture 1 in class (Intro to Workflows)

| Slide (~min) | Where | Do | Say |
|---|---|---|---|
| 1 (0) | Deck | Press **T**. Everyone logged in to github.com | "Today the robot runs the checks." |
| 2 (1) | Deck | Who pushed without testing? | "Teams automate it. That's CI." |
| 3 (2) | Deck / video | Optional: 90 s of the exact-instructions video | "The robot does only what you wrote." |
| 4 (4) | Deck | Event → … → Output | Point at each box and its YAML line |
| 5–6 (6–8) | Deck + browser | Why CI; Marketplace: search setup-node | "Official, maintained, pinned. Like Docker Hub." |
| 7 (10) | Deck | YAML three rules | "Indentation is the structure. Spaces, never tabs." |
| 8 (11) | Your terminal | New repo hello-actions; mkdir, git init, .github/workflows | "Exact folder names." |
| 9 (14) | Your VS Code | Type hello-world.yml, commit, push | "This proves the automation works." |
| 10 (18) | Browser | Actions tab → the run → say-hello → Print a message | "Thumbs up for a green ✓." |
| 11 (20) | Deck | The real log | "Command, then what it printed." |
| 12 (21) | Activity page | 6 cards | "RUNS or DOESN'T RUN." |
| 13 (27) | Deck | Triggers table | "For pull_request, the filter is the TARGET branch." |
| 14 (30) | Your terminal + browser | `branches: - main`, push; then push try-filter → no run | "No run is the correct result." |
| 15 (36) | Deck | Homework Part I | "Every push, every branch, Ubuntu, echo." |

**Time check, Lecture 1:** not at the activity by ~min 23 → show slide 11 instead of waiting for everyone's runs. Students' pushes failing (auth) → "watch mine; Code Lab 1 has every step".

## Lecture 2 in class (Managing Workflows)

| Slide (~min) | Where | Do | Say |
|---|---|---|---|
| 1 (0) | Deck | Students: new repo ci-factorial; mkdir, git init, code . | "Today the robot runs our tests." |
| 3 (3) | Codepad | Terminal: `npm test` (jest not found), `npm install --save-dev jest`, `npm test` (7 passed) | "Confirm it works locally first." Click **Dockerfile** / **package.json** in the Explorer to show them (read-only; Esc closes). |
| 4 (8) | Deck | run-tests.yml in plain English | "Your local workflow, in a clean machine." |
| 5 (10) | Your VS Code | run-tests.yml, `git checkout -b dev`, push | "Push to dev starts it." |
| 6 (15) | Browser / deck | Green run, the log | "EBADENGINE = warnings, not errors." |
| 7 (17) | Your VS Code + browser | toBe(7), push, red; read it; fix, push | "Exit code 1 = red." |
| 8 (19) | Activity page | 6 cards | "Test failed, broken YAML, or missing step?" |
| 9 (25) | Browser | PR dev → main, wait for the check, merge | "Only tested code reaches main." |
| 10 (28) | Deck + browser | workflow_dispatch; Run workflow / Re-run all jobs | "Re-run without junk commits." |
| 11 (30) | Deck | Workflows are code | "Branch, PR, review." |
| 12–13 (32–34) | Deck + your VS Code | Native vs Docker; push the Docker version | "Docker = how to run it; workflows = when." |
| 14 (37) | Deck | Homework Part II | "Templates are on the class site." |

**Time check, Lecture 2:** not at the activity by ~min 21 → skip the live fix in slide 7 (show the demo repo's green run). Not at slide 12 by ~min 34 → show the Docker slide only; students do it from Code Lab 2.
