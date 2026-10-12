# Vehicle Fuel Log

A single-page web app for logging daily fuel (liters) per vehicle for a month.

## Features
- Daily liters entry per vehicle, with per-vehicle and per-day totals
- km/L per vehicle (entered manually) -> computed distance
- Start odometer per vehicle -> computed daily odometer (shown under the fuel row) and end odometer
- Weekly view (Mon-Sun) or whole month; month picker, vehicle/plate search, CSV export/import
- Daily odometer cells can be edited manually; later days recalculate from the edited reading
- Data is saved in the browser (localStorage). Export CSV regularly as a backup.

## Usage
Open `index.html` in a browser, or host it with GitHub Pages
(Settings -> Pages -> Deploy from branch -> `main` / root).

## Editing the vehicle list
The fleet list is the `RAW` string near the top of the script in `index.html`
(one vehicle per line: `PropertyNo Plate`).
