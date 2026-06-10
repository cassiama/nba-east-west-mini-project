# Visualizing the NBA's East–West Conference Split

A mini data-science project that treats the NBA's conference split as a binary
classification problem: train a linear SVM on every team's arena coordinates
(longitude, latitude → East/West) and project the decision boundary onto a map
of North America.

**Result:** the conferences are linearly separable. The maximum-margin boundary
runs near 89°W — roughly down the Mississippi — leaning slightly westward as it
goes north. The support vectors are the border teams: Memphis and Minnesota for
the West; Milwaukee, Chicago, and Atlanta for the East.

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
- Basemap boundaries from [Natural Earth](https://www.naturalearthdata.com/) (public
  domain), downloaded on first run and cached in `data/naturalearth/`.

## Stack

pandas · scikit-learn · geopandas · matplotlib, managed with uv.
