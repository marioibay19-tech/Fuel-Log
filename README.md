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
- **Input**: add fuel by date range. Liters are split equally across the days (inclusive);
  overlapping entries add up.
- **Monitoring**: per-vehicle table with a fuel row and computed odometer row per day,
  weekly (Mon-Sun) or whole month, search, CSV export/import.

## How the numbers work
- Daily fuel = date-range entries + anything typed in the grid
- Distance = liters x km/L (km/L entered per vehicle)
- Odometer = start odometer + cumulative distance; any day can be edited and later days continue from it

## Notes
- If the apiKey is blank, data is saved only in each user's own browser.
- With open rules, anyone with the site link can read and change the data.
- Themes: DPWH (default, blue header + orange accent, Public Sans), Auto, Light, Dark, Forest, Amber, Ocean.
- Vehicle list: edit the `RAW` string near the top of the script (`PropertyNo Plate` per line).
