# c3-fahrplan-druck

[![Live Demo](https://img.shields.io/badge/Live%20Demo-mobile-blue?style=flat-square)](https://c3-fahrplan-druck.divo.link/events/39c3?columns=mobile)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-A0+%20print-blue?style=flat-square)](https://c3-fahrplan-druck.divo.link/events/39c3?tinted-background=false)

The [Fahrplan](https://fahrplan.events.ccc.de/congress/2025/fahrplan) in the style of a [Fahrplan](https://upload.wikimedia.org/wikipedia/commons/e/ed/Bremen%2C_Fahrplan_(Hbf).jpg).

## Quick use

1) Open `index.html` in a browser (no build steps needed).
2) Append URL parameters to filter the rendered plan:
   - `only-day=<n>`: Render a single conference day (e.g., `only-day=1`). Days use the indices from the JSON feed (see below; currently 0–4). Omit to show all days in one sheet.
   - `only-track=<nameOrCode>`: Filter by track. Accepts full track names or the short codes from the track map (see table). Examples: `only-track=Science`, `only-track=SCI`.
   - `only-room=<room>`: Filter by room, case-insensitively (e.g., `only-room=Stonewall IO`). Abbreviations are intentionally not supported, but substrings work (e.g., `only-room=Stonewall`).
   - `tinted-background=false`: Disable the default yellow-tinted background color.
   - `columns=<n>`: Set the number of columns (e.g., `columns=1` for a single-column layout). The page width scales proportionally from the 8-column default.
     The special mode `columns=mobile` enables a single-column view that uses the full device width.
3) Parameters can be combined, e.g., `?only-day=2&only-track=SCI`.

## Single-day vs. all-days view

- Without parameters: renders all days sequentially with a day header and legend at the end.
- With `only-day`: renders that day, groups rows into time bands, updates the header date, and adjusts the legend footer text accordingly.

## Printing

We had some issues printing this to PDF if the size grows beyond DIN A0+. However, directly using the system (not the browser-provided) printing dialog and saving that as PDF or directly printing from that worked for us.

We strongly recommend directly using yellow paper for physical prints (and setting `tinted-background=false`).

## Contributing new events

Feel free to fork this and use it on your event!

We plan to collect and archive Fahrpläne for various events. ❤️
If you create one for your event, please consider sharing it back with us so we can add it to the collection!
It should be as easy as forking this repo, adding a unique folder under `events/` (possibly copying content from an existing event), and creating a pull request.

### Customization

Top-level constants near the start of each event's `index.html` control basic event-specific behavior:
- `scheduleUrl`: JSON feed to load (currently the 39C3 schedule).
- `trackMap`: Map track names from the feed to short codes shown in the table.
- `totalDays`: Number of conference days used for day labels and footer copy.
- `headerDateRange`: Text shown in the top-left header.
- `stationName`: Main title in the header area (also used when showing active filters).
- `timeRanges`: Time-band labels for single-day grouping.
- `roomAbbrevMap`: Exact room name to abbreviation/icon mapping.
- `roomAbbrevPartial`: Partial room name matches to abbreviation/icon mapping.

For deeper layout or style tweaks, edit `index.html` and `style.css` directly.
If anything feels unclear, feel free to reach out (e.g., open an [issue](https://github.com/felixdivo/c3-fahrplan-druck/issues))!
