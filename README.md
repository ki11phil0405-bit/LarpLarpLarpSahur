# Mirrorkit

A set of mobile-first dashboards, all linked from one site. Open `index.html` on your phone to start.

## Dashboards

- **Striped dashboard** (`striped-dashboard/`): the main dashboard. Tiered random numbers, reports with range switching, finger-drag chart readouts, an editable home screen, tap-to-add widgets, account settings and native notifications.
- **Larp tube studio** (`backup/larp-tube-studio/`): an older analytics mock kept as a backup. It isn't linked from the main page.

## Using the striped dashboard

- **Tiers**: Low, Medium, High, Income. Settings → **Randomize** rebuilds 400 days of payments for that tier.
- **Reports**: 1W / 4W / 1Y / MTD / QTD / YTD / ALL ranges with % change. Drag a finger on any chart to read the value and date (hover with a mouse).
- **Editable home**: Edit to reorder, hide or show reports. Summary tiles and the default range are set in settings.
- **Custom widgets**: add a number that adds its amount on each tap. Chart widgets plot every tap.
- **Settings** (store icon, top left): accounts, business, currency, theme and accent, chart style, number format, fees, widgets, notifications and backup export/import.
- **Notifications**: native pop-ups for payments over a threshold, a daily goal, refunds and a daily summary. Each rule has an editable title and message. Optional simulated sales run while the app is open.

Native alerts only fire while the app is open. Background alerts need a push server. On iPhone, add the app to the Home Screen first (Share → Add to Home Screen), then allow notifications.
