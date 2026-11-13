# Walmart Hurricane Analytics

DS2002 Data Science Systems, Midterm Project (Fall 2026)
Team: Ben Freilich (BenFreilichUVA) and Thomas Snyder (TommySnyd)

This project cleans five messy Walmart data files, joins them with real weather data from the Open-Meteo API, and answers five questions about how sales changed before Hurricane Helene made landfall in Florida on September 26, 2024.

## Where everything is

| File | What it is |
|---|---|
| `notebooks/team_notebook.ipynb` | The final notebook with cleaning, weather integration, and all five questions |
| `REFLECTION.md` | Answers to the five reflection questions |
| `CHARTER.md` | Team charter, roles, and question ownership |
| `data/` | The five supplied data files, plus `weather_by_store.csv`, a saved copy of the weather pull used only if the API is down |

## How to run the notebook

**In Google Colab (recommended)**

1. Open the notebook in Colab using this link: https://colab.research.google.com/github/BenFreilichUVA/walmart-hurricane-project/blob/main/notebooks/team_notebook.ipynb
2. Click Runtime, then Restart session and run all.

The first cell clones this repository into Colab, so no files need to be uploaded. No API key is needed.

**Locally in Jupyter**

1. Clone the repository and install the libraries.
```
git clone https://github.com/BenFreilichUVA/walmart-hurricane-project.git
pip install pandas matplotlib requests jupyter
```
2. Open `notebooks/team_notebook.ipynb`. In the first code cell, delete the `!rm` and `!git clone` lines and set `MY_REPO` to the folder you cloned into.
3. Restart the kernel and run all cells.

`sqlite3`, `pathlib`, and `time` come with Python and do not need to be installed.

## Weather data

Weather comes from the Open-Meteo Historical Weather API (https://open-meteo.com/), which is free and needs no key.
Base URL: `https://archive-api.open-meteo.com/v1/archive`

The notebook pulls hourly wind speed, precipitation, and sea-level pressure for each of the 12 stores in Eastern time, then rolls them up to daily values. If the API is unreachable, it falls back to `data/weather_by_store.csv`, a saved copy of an earlier pull, and the `source` column says which one was used.

## Key findings

- **Demand surge.** In the 7 days before landfall, orders ran about 2.4 times the September 1 to 15 baseline. Breakfast (strawberry Pop-Tarts) rose the most at +414%, while Emergency supplies added the most actual units.
- **The Pop-Tarts effect.** Pop-Tarts was split across four SKUs. No single SKU averaged more than about 103 units a day in the surge, but combined it sold about 377 a day and was the top-selling product, ahead of bottled water.
- **Weather.** Sales lined up most closely with the wind two days later (r = 0.79), meaning customers bought before the storm arrived.
- **Stores.** Every store surged by about 2.2 to 2.5 times regardless of distance from landfall. Orlando was the only statistical outlier.
- **Board games.** The surge is real but the +250% figure overstates it. That number only appears on the peak day. Across the full week the increase was about +125% to +145%, so we recommend stocking about double normal demand, mostly Monopoly.

## Reflection

The reflection answers are in [REFLECTION.md](REFLECTION.md).
