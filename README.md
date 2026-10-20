# Vehicle Fuel Log

Fuel monitoring for the vehicle fleet: fuel entered by date range, computed distance and daily odometer.
Hosted on GitHub Pages, with a Firebase Firestore backend so everyone sees the same live data
(same setup as the Bid Monitoring site).

## Firebase (already connected)
`index.html` is already set to the same Firebase project as the Bid Monitoring site
(`bid-monitoring-f1308`) with its web apiKey, so there is nothing to paste.
Data is stored in separate collections (`fuel_logs`, `fuel_entries`), so it does not mix with the bid data.
Firestore rules must allow read/write (the bid site already uses open rules).
Updates appear on every computer within a few seconds.
If the header shows "Shared: connection problem", re-copy the apiKey from Firebase
(Project settings -> General -> Your apps -> Config) into `const FIREBASE={...}` in `index.html`.

## Hosting on GitHub Pages
Repository Settings -> Pages -> Deploy from a branch -> `main` / root.
The site is at `https://<username>.github.io/<repository>/`.

## Pages
- **Input**: add fuel by date range, and enter the weekly odometer readings (one box per vehicle for the chosen Monday). Liters are split equally across the days (inclusive);
  overlapping entries add up.
- **Monitoring**: per-vehicle table with a fuel row and an odometer row per day (type the Monday readings),
  weekly (Mon-Sun) or whole month, search, CSV export/import.

## How the numbers work
- Daily fuel = date-range entries + anything typed in the grid
- Odometer: enter the actual reading every Monday (any day works) in the Odometer row.
  Between two readings, the distance (difference of the readings) is shared out by ratio and proportion
  of the fuel used each day. km/L is not used in the formula.
- Month km, km/L (distance / fuel) and First/Last odo are computed from those readings.
- Saturday/Sunday cells with no fuel (and no typed reading) are left blank.
- Days after the latest reading stay blank until the next reading is entered.
- Readings in the neighbouring months are used, so weeks that cross a month end are computed.

## Notes
- If the apiKey is blank, data is saved only in each user's own browser.
- With open rules, anyone with the site link can read and change the data.
- Themes: DPWH (default, blue header + orange accent, Public Sans), Auto, Light, Dark, Forest, Amber, Ocean.
- Vehicle list: edit the `RAW` string near the top of the script (`PropertyNo Plate` per line).
