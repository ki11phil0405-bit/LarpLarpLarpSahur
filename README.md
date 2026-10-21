# LarpLarpLarpSahur

A YouTube Studio–style analytics simulator (mobile first). Open `studio/index.html` on your phone.

- **Tap any number** (views, watch time, subscribers, realtime, total subs, status-bar time) to edit it and its % change. The chart is regenerated to match.
- **Triple-tap the "Studio" logo** for every setting: chart shape, end date, number format, avatar, top-content videos, status bar.
- **New random chart** reshuffles the line while keeping your totals.
- Edits are saved in the browser.

For a clean full-screen view on iPhone: Safari → Share → **Add to Home Screen**, then open it from the home screen. The fake status bar hides itself there and the real one shows.

## Margin Drive dashboard (`dashboard/`)

The main page (`index.html`) opens this Stripe-style dashboard, which lives in `dashboard/`. The original Studio simulator moved to `studio/index.html`.

- **Tiers**: Low, Medium, High, Income. Account settings → **Randomize** rebuilds 400 days of payments for that tier.
- **Reports**: 1W / 4W / 1Y / MTD / QTD / YTD / ALL ranges with % change. **Drag your finger** on any chart to read the value and date (hover with a mouse).
- **Editable home**: Edit to reorder, hide or show reports. Summary tiles and the default range are set in settings.
- **Custom widgets**: add a number that adds its amount on each tap. Chart widgets plot every tap.
- **Account and settings** (the store icon, top left): accounts, business, currency, theme and accent, chart style, number format, fees, widgets, notifications and backup export/import.
- **Notifications**: native pop-ups via the Notification API. Rules for payment threshold, daily goal, refunds and a daily summary, each with editable title and message. Optional simulated sales while the app is open.

Native alerts only fire while the app is open. Background alerts need a push server. On iPhone, add the app to the Home Screen first (Share → Add to Home Screen), then allow notifications.
