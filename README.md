# c3-fahrplan-druck

[![Live Demo](https://img.shields.io/badge/Live%20Demo-c3--fahrplan--druck.divo.link%2Fweb-blue?style=flat-square)](https://c3-fahrplan-druck.divo.link/web)

The [Fahrplan](https://fahrplan.events.ccc.de/congress/2025/fahrplan) in the style of a [Fahrplan](https://upload.wikimedia.org/wikipedia/commons/e/ed/Bremen%2C_Fahrplan_(Hbf).jpg).

## Quick use

1) Open `index.html` in a browser (no build steps needed).
2) Append URL parameters to filter the rendered plan:
   - `only-day=<n>`: Render a single conference day (e.g., `only-day=1`). Days use the indices from the JSON feed (see below; currently 0–4). Omit to show all days in one sheet.
   - `only-track=<nameOrCode>`: Filter by track. Accepts full track names or the short codes from the track map (see table). Examples: `only-track=Science`, `only-track=SCI`.
   - `only-room=<room>`: Filter by room, case-insensitively (e.g., `only-room=Stonewall IO`). Abbreviations are intentionally not supported, but substrings work (e.g., `only-room=Stonewall`).
3) Parameters can be combined, e.g., `?only-day=2&only-track=SCI`.

## Single-day vs. all-days view

- Without parameters: renders all days sequentially with a day header and legend at the end.
- With `only-day`: renders that day, groups rows into time bands, updates the header date, and adjusts the legend footer text accordingly.

## Printing

We had some issues printing this to PDF if the size grows beyond DIN A0+. However, directly using the system (not the browser-provided) printing dialog and saving that as PDF or directly printing from that worked for us.

We strongly recommend directly using yellow paper for physical prints.

## Data source and customization

Feel free to fork this and use it on your event! However, it would be cool to collect the created Fahrpläne somewhere (make a museum).

Top-level constants near the start of `index.html` control event-specific behavior:

- `scheduleUrl`: JSON feed to load (currently the 39C3 schedule).
- `trackMap`: Map track names from the feed to short codes shown in the table.
- `totalDays`: Number of conference days used for day labels and footer copy.
- `headerDateRange`: Text shown in the top-left header.
- `stationName`: Main title in the header area (also used when showing active filters).
- `timeRanges`: Time-band labels for single-day grouping.

To point the page at another event:
1) Change `scheduleUrl` to your event’s feed.
2) Update `trackMap` and the track table above if the codes differ.
3) Set `totalDays`, `headerDateRange`, and `stationName` to match your event.
4) (Optional) Adjust `timeRanges` for different grouping, `abbreviateRoom()` for room codes/icons, and legend text inside `renderLegend()`.

For deeper layout or style tweaks, edit `index.html` and `style.css` directly. If anything feels unclear, ask for help and we’ll iterate together.
