# Vehicle Fuel Log

Fuel monitoring for the vehicle fleet: fuel entered by date range, computed distance and daily odometer.
Hosted on GitHub Pages, with a Firebase Firestore backend so everyone sees the same live data
(same setup as the Bid Monitoring site).

## Connect it to Firebase (one time)
Use the same Firebase project as the bid monitoring site (`bid-monitoring-f1308`).
It stores its data in separate collections (`fuel_logs`, `fuel_entries`), so nothing is mixed up.

1. Open the bid monitoring site's `index.html` on GitHub and copy the `apiKey` value from its `firebaseConfig`.
2. In this repository's `index.html`, find:
   `const FIREBASE={projectId:"bid-monitoring-f1308",apiKey:""};`
   and paste the apiKey between the empty quotes. (If you use a different Firebase project, change `projectId` too.)
3. In Firebase console -> Firestore Database -> Rules, make sure read/write is allowed (the bid monitoring
   site already uses open rules, so nothing to change if you reuse its project).
4. Commit. Updates appear on every computer within a few seconds.

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
- Without the apiKey, data is saved only in each user's own browser.
- With open rules, anyone with the site link can read and change the data.
- Themes: DPWH (default, blue header + orange accent, Public Sans), Auto, Light, Dark, Forest, Amber, Ocean.
- Vehicle list: edit the `RAW` string near the top of the script (`PropertyNo Plate` per line).
