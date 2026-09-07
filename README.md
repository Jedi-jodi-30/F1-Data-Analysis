# F1 Telemetry Analysis

A Python and FastF1 workspace for exploring Formula 1 car telemetry, lap performance, and session data.

The current analysis is notebook-driven. It loads qualifying or race sessions, combines car telemetry with lap metadata, filters usable laps, and compares drivers and teams through speed and sector-time visualizations.

## What It Analyzes

The notebook currently supports:

- Loading Formula 1 sessions through [FastF1](https://docs.fastf1.dev/)
- Caching downloaded session data locally
- Combining car telemetry with lap information
- Filtering accurate race laps and timed qualifying laps
- Identifying flying laps within 107% of the session best
- Comparing team mean speed, top speed, and lap pace
- Comparing the fastest drivers using speed-versus-distance traces
- Breaking lap differences down by sector

## Project Structure

```text
.
├── requirements.txt
└── notebooks/
    ├── notebook_analysis_I.ipynb
    └── fastf1_cache/       # locally cached FastF1 session data
```

## Requirements

- Python 3.10 or newer
- Jupyter Notebook or VS Code with the Jupyter extension
- Internet access the first time a session is loaded

## Setup

Create and activate a virtual environment, then install the dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

On macOS or Linux, activate the environment with:

```bash
source .venv/bin/activate
```

## Run the Analysis

Open [`notebooks/notebook_analysis_I.ipynb`](notebooks/notebook_analysis_I.ipynb) in VS Code or Jupyter and run the cells from top to bottom.

To launch Jupyter from the repository root:

```bash
jupyter notebook notebooks/notebook_analysis_I.ipynb
```

The notebook uses a relative `fastf1_cache` path. Running it with `notebooks/` as the notebook working directory keeps cached sessions in `notebooks/fastf1_cache/`.

To analyze another session, update the session-loading call in the notebook, for example:

```python
session = get_session(2026, "Monza", "q")
session.load()
```

FastF1 downloads session data on the first run and reuses the local cache on later runs.

## Data Handling Notes

- `R` selects race sessions and `Q` selects qualifying sessions in `combine_telemetry_with_laps`.
- Race analysis excludes inaccurate laps, pit-lane laps, and laps that are not under green-track conditions.
- Qualifying analysis keeps laps with a recorded lap time.
- Telemetry is aligned to lap metadata with `pandas.merge_asof`.
- Cached data can become large; keep it local unless a specific dataset is intentionally being shared.

## Future Directions

Potential extensions include reusable analysis modules, automated session reports, weather and track-condition analysis, stint and tyre degradation analysis, and comparisons across circuits or seasons.

## License

No license has been defined for this repository yet.
