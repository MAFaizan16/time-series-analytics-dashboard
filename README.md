# Time-Series Analytics Dashboard

A lightweight time-series analytics project that reads timestamps from an SQLite database, groups records by day, generates a JavaScript data file, and visualizes daily activity in an interactive D3.js line chart.

## Features

- Generates a sample SQLite database with 25,000 timestamped records when `logs.sqlite` is not present.
- Aggregates timestamps into daily counts and fills missing dates with zero-count days.
- Displays total records, number of daily data points, average daily activity, and peak activity.
- Interactive D3.js line chart with zoom, pan, hover tooltip, and reset-zoom control.
- Uses only Python standard-library modules for the data engine. D3.js is loaded from a CDN in the browser.

## Project files

- `time_series_engine.py` — creates/reads the SQLite database and generates daily time-series data.
- `gline.html` — dashboard page and chart visualization.
- `gline.js` — generated data consumed by the dashboard. The Python script regenerates this file when run.
- `logs.sqlite` — generated locally if missing; intentionally excluded from version control.

## Requirements

- Python 3.9 or newer
- A modern web browser
- Internet access to load D3.js from jsDelivr CDN

No `pip install` is required.

## Run locally

1. Download or clone this repository.
2. Open a terminal in the project folder.
3. Run:

   ```bash
   python time_series_engine.py
   ```

   On some systems, use `python3 time_series_engine.py` instead.

4. The script generates `gline.js` and opens `gline.html` in your default browser.

If the browser does not open automatically, double-click `gline.html` after running the script.

## Use your own data

The engine expects an SQLite database named `logs.sqlite` with a table named `Logs` and a text column named `timestamp`, for example:

```sql
CREATE TABLE Logs (
    id INTEGER PRIMARY KEY,
    timestamp TEXT
);
```

Store timestamps in a format beginning with `YYYY-MM-DD`, such as `2025-01-15 14:30:00`. If `logs.sqlite` does not exist, the script creates sample data automatically. Back up your own database before running the script because the sample-data creation function drops and recreates the `Logs` table; it is only called automatically when the database file is missing.

## Notes

- `gline.js` is generated output and can be regenerated with the Python script.
- The chart currently uses a fixed SVG width calculated when the page loads; resize the page to reload the chart at a different width.
- This project is intended as a simple demonstration/starting point, not a production analytics service.

## License

Choose a license before publishing if you want others to reuse the code. For example, the MIT License is a common option for open-source projects.
