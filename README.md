# Vehicle Fuel Log

A single-page web app for logging fuel per vehicle and monitoring distance and odometer.

## Pages
- **Input**: add fuel by date range. Liters are split equally across the days (inclusive);
  overlapping entries add up. Entries can be deleted from the list.
- **Monitoring**: per-vehicle table with a fuel row and a computed odometer row per day,
  weekly (Mon-Sun) or whole-month view, search, CSV export/import.

## How the numbers work
- Daily fuel = date-range entries + anything typed directly in the grid
- Distance = liters x km/L (km/L entered per vehicle)
- Odometer = start odometer + cumulative distance; any day's odometer can be edited manually
  and later days continue from it

## Notes
- Data is saved in the browser (localStorage). Export CSV regularly as a backup.
- Manual odometer edits are not included in the CSV.
- Vehicle list: edit the `RAW` string near the top of the script in `index.html`
  (one vehicle per line: `PropertyNo Plate`).

## Hosting
Open `index.html` directly, or use GitHub Pages (Settings -> Pages -> Deploy from branch -> `main` / root).
