# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A single-notebook data science project: visualize the NBA's East/West conference split by
training a linear SVM on arena coordinates and projecting its decision boundary onto a map
of North America.

## Commands

The environment is managed by uv — never `pip install` into it directly.

- `uv sync` — create the venv and install dependencies
- `uv run jupyter lab` — work on the notebook interactively
- `uv run jupyter nbconvert --to notebook --execute --inplace notebooks/east_west_svm.ipynb` —
  execute the notebook headlessly. This is the project's de-facto test: every cell must run
  clean, the data-loading cell asserts 30 teams / 15 per conference, and the fit cell should
  report 100% training accuracy.

## Architecture

- `data/arenas.csv` is the hand-curated source of truth: 30 teams, conference labels, arena
  name/city, lat/lon (2025–26 season). When arena facts change (renamings, relocations),
  edit this file — the notebook contains no team data.
- `notebooks/east_west_svm.ipynb` holds the entire analysis: load CSV → fetch/cache the
  Natural Earth basemap → fit a `StandardScaler + SVC(kernel="linear")` pipeline on
  (lon, lat) → render `DecisionBoundaryDisplay` layers under the basemap.
- `data/naturalearth/` is a gitignored download cache for Natural Earth zips. First
  execution needs network access; deleting the directory just re-triggers the download.
- The notebook resolves paths relative to `notebooks/` (`../data/...`), so run it with that
  working directory (nbconvert and Jupyter do this automatically).
- The notebook is kept committed *with* outputs so the figures render on GitHub — re-execute
  it before committing changes to it.
