# Visualizing the NBA's East–West Conference Split

A mini data-science project that treats the NBA's conference split as a binary
classification problem: train a linear SVM on every team's arena coordinates
(longitude, latitude → East/West) and project the decision boundary onto a map
of North America.

**Result:** the conferences are linearly separable. The maximum-margin boundary
runs near 89°W — roughly down the Mississippi — leaning slightly westward as it
goes north. The support vectors are the border teams: Memphis and Minnesota for
the West; Milwaukee, Chicago, and Atlanta for the East.

The notebook also quantifies how lopsided the split is (the West region covers
~73% of the lower 48's land but only ~48% of its 2020 Census population; a West
rival is 1,564 km away on average vs 928 km in the East) and runs a what-if:
if Seattle and Las Vegas joined as expansion teams, the SVM says the
Timberwolves are the team to move East.

Two closing studies: a kernel comparison (RBF and a great-circle precomputed
kernel reproduce the same split — complexity buys nothing on separable data)
and era maps from 1980–81 to today showing the max-margin line drifting east
as the league expanded and relocated.

## Quickstart

Requires [uv](https://docs.astral.sh/uv/).

```sh
uv sync
uv run jupyter lab notebooks/east_west_svm.ipynb
```

Or execute headlessly:

```sh
uv run jupyter nbconvert --to notebook --execute --inplace notebooks/east_west_svm.ipynb
```

## Data

- `data/arenas.csv` — hand-curated coordinates of all 30 NBA arenas (2025–26 season).
- `data/state_population_2020.csv` — official 2020 US Census counts, lower 48 + DC.
- `data/nba_champions.csv` — every NBA champion 1947–2025, mapped to its current franchise.
- `data/arenas_historical.csv` — league snapshots (teams, conferences, era arenas) for
  1980–81, 1990–91, 2000–01, and 2010–11.
- Basemap boundaries from [Natural Earth](https://www.naturalearthdata.com/) (public
  domain), downloaded on first run and cached in `data/naturalearth/`.

## Stack

pandas · scikit-learn · geopandas · matplotlib, managed with uv.
