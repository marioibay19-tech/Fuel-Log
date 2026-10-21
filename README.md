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

## Password
The page opens with a password screen. The starting password is `DPWH-Fuel-2026` - change it right away in
Settings -> Change password. The new password is stored in the shared database, so it applies to everyone.
This is a light lock to keep casual visitors out. It is not strong security: the data itself is protected only by
the Firestore rules, and anyone who can read the page code could bypass the screen.

## Phones
On a phone the tabs become a bar at the bottom, the weekly odometer list shows one card per vehicle with a large number box,
the Monitoring grid keeps the vehicle column fixed while the days scroll sideways, and the other tables turn into cards.
The laptop layout is unchanged.

## Pages
- **Input**: add fuel by date range, and enter the weekly odometer readings (one box per vehicle for the chosen Monday). Liters are split equally across the days (inclusive);
  overlapping entries add up.
- **Checks**: missing Monday readings, odometer going down, unusual km/L, distance with no fuel, duplicate fuel entries.
- **Maintenance**: latest odometer vs last PM odometer + PM interval -> overdue / due soon / OK; CSV export and a link to the PM/CM monitoring site.
- **Reports**: monthly summary per vehicle with charts; print / save as PDF and CSV.
- **Settings**: add, edit, deactivate vehicles; PM and km/L thresholds; change password.
- **Monitoring**: per-vehicle table with a fuel row and an odometer row per day (type the Monday readings),
  weekly (Mon-Sun) or whole month, search, CSV export/import.

## How the numbers work
- Daily fuel = date-range entries + anything typed in the grid
- Odometer: enter the actual reading every Monday (any day works) in the Odometer row.
  Between two readings, the distance (difference of the readings) is shared out by ratio and proportion
  of the fuel used each day. km/L is not used in the formula.
- Month km and First/Last odo are computed from those readings.
- Saturday/Sunday cells with no fuel (and no typed reading) are left blank.
- Days after the latest reading stay blank until the next reading is entered.
- Readings in the neighbouring months are used, so weeks that cross a month end are computed.

## Notes
- If the apiKey is blank, data is saved only in each user's own browser.
- With open rules, anyone with the site link can read and change the data.
- Background: dotted pattern (default), plain, or your own image (header dropdown; saved per browser).
- Themes: DPWH (default, blue header + orange accent, Public Sans), Auto, Light, Dark, Forest, Amber, Ocean.
- Vehicle list: edit the `RAW` string near the top of the script (`PropertyNo Plate` per line).
