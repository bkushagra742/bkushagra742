# Setup

This repo is meant to live at `github.com/bkushagra742/bkushagra742` (a
repo named exactly after your username is the one GitHub renders on your
profile page).

## 1. First push
Push this whole folder as the repo root — `README.md`, `assets/`, and
`.github/` need to sit at the top level.

## 2. Enable the snake workflow
`.github/workflows/snake.yml` runs on a daily schedule and on push to
`main`, but the first run needs a manual trigger:
1. Go to the **Actions** tab → **Generate contribution snake** → **Run workflow**.
2. This creates an `output` branch with `snake-dark.svg` / `snake-light.svg`.
3. The README already points at that branch, so no README edit is needed —
   the graph will just start appearing once the branch exists.

## 3. Enable the metrics workflow (stats / top languages / achievements)
`.github/workflows/metrics.yml` replaces the old github-readme-stats /
streak-stats / profile-trophy widgets — those are free public services
that go down or get rate-limited on their own; this generates the same
kind of information as a static SVG you own instead, published to the
same `output` branch as the snake.

It needs a personal access token (the default `GITHUB_TOKEN` doesn't
have enough scope for some of the plugins used):
1. Create a **classic** PAT at github.com/settings/tokens with the
   `repo` and `read:user` scopes. Give it an expiration you're
   comfortable renewing.
2. In this repo, go to **Settings → Secrets and variables → Actions →
   New repository secret**, name it `METRICS_TOKEN`, and paste the
   token.
3. Go to **Actions → Generate GitHub metrics → Run workflow** once to
   trigger the first run. `metrics-dark.svg` / `metrics-light.svg` will
   appear on the `output` branch.

## 4. Enable the recently-active workflow
`.github/workflows/activity.yml` fills in the `<!--START_SECTION:activity-->
… <!--END_SECTION:activity-->` block in `README.md` with your last few
public GitHub events. It uses the default `GITHUB_TOKEN` — no extra
secret needed. Run it once from the **Actions** tab the same way, or
just wait for its 6-hourly schedule.

## 5. Badges that need no setup
The badges row (last commit, workflow status, "open to opportunities")
uses shields.io, which reads public GitHub data directly — nothing to
host, no token required. The workflow-status badges will go green once
steps 2 and 3 have run successfully at least once.

## 6. Extending the project
See `DESIGN_SYSTEM.md` → **Extending this system** for the exact pattern
to add a new project card, tech pill, or README section without touching
anything else.
