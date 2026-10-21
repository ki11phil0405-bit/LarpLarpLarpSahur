# Mirrorkit: project context

Working notes for the whole project. Read this before starting new work.

## What the project is

- **Name:** Mirrorkit. A site of mobile-first dashboards, all linked from one place.
- **Naming rule:** dashboards use off-brand names on the site and in the repo (for example "striped dashboard", "larp tube studio"). Do not use real brand names (Stripe, YouTube) in titles, labels or the README.
- **Root page:** `index.html` redirects to `striped-dashboard/index.html`.
- **Backup:** the original YouTube-style simulator is kept verbatim in `backup/larp-tube-studio/`. It is not linked from anywhere. Its page still has the original red logo and "Studio" wording.
- **Branch:** `claude/margin-drive-dashboard`. The repo was on a detached HEAD; no pull request has been opened.
- **Hosting status:** GitHub Pages is not confirmed as enabled for this branch. The user must turn it on in repo settings (Settings → Pages → deploy from branch `claude/margin-drive-dashboard`, folder `/`). The sandbox cannot change that setting.

## The striped dashboard (built)

Location: `striped-dashboard/index.html` (one file, no dependencies). Icon: `icon.svg` and `apple-touch-icon.png`.

- Tiers for random data: Low, Medium, High, Income. "Randomize" rebuilds 400 days of payments for the tier.
- Report ranges: 1W, 4W, 1Y, MTD, QTD, YTD, ALL, shown in a fixed row under the title bar on Home. Each card shows the current period against the previous period with % change and a chart.
- Chart scrubbing: drag a finger (or hover with a mouse) to read the value and date.
- Editable home: Edit mode to reorder, hide or show reports. Today tiles and the default range are set in settings.
- Custom widgets: a number with a "+ amount" button for each sale. Chart widgets plot every tap.
- Triple-tap any report total, Today tile or widget number to type a new value. Changes spread across the days in that range, so every screen showing the number updates.
- Plain-English description (settings → "Describe your business"): a rule-based reader picks up prices ($60, or $799 $999 $1200), sales a week or day (12-18 a week), drops (2x a month), "random", and an all-time sales total ("$1,200,000 in all time sales"). It regenerates the numbers to match. "Use tier instead" clears it.
- Customers screen: estimated customers for fewest (top price), typical (middle price) and most (lowest price), calculated as all-time sales divided by each price. Works for every business.
- Settings (store icon, top left): accounts, business name, avatar, currency, tier, theme and accent colour, chart style, number format, card fee, widgets, notifications, description, backup export and import, erase everything.
- Notifications: native pop-ups (Notification API) for payments over a threshold, a daily goal, refunds, and a daily summary at a set time. Each rule has an editable title and message. Optional simulated sales run while the app is open.
- Bottom tab bar keeps at least 22px below the labels; the top bar starts below the safe area.
- Storage: everything is saved in the browser under one key (`margin-drive-v1`). Settings stay on that device only.

Known limits:
- Native alerts only fire while the app is open. Background alerts need a push server.
- On iPhone, notifications need the app added to the Home Screen first.
- Settings do not sync between devices.
- The iPhone home-indicator and notch spacing has been checked only in desktop Chromium, not on a real phone.
- Settings controls work in desktop and phone-sized Chromium. The user reported they could not change settings on their phone; this has not been reproduced yet.

## Requirements gathered from the user

- Make the dashboards editable and customizable from an account settings screen.
- Show native pop-up notifications with customizable rules.
- Charts that show the value when you drag a finger across them.
- Numbers that respond to taps (custom widgets).
- Triple-tap editing, with the same number synced everywhere it appears.
- Time ranges and search keep working after a description is read.
- A plain-English description of the business should set the numbers. It should work for every category, not just one.
- Customer estimates (fewest / typical / most) from all-time sales and price points, for every category.
- The top bar should match the reference: store icon left, name in the middle, + on the right, range tabs underneath.
- Each dashboard gets its own sub-link on the site, with its own settings and everything.
- Layout should adapt automatically to every phone size and the phone's own settings (light/dark, text size, reduced motion). Not yet built.

## Niche examples (the user's words)

1. **Clothing brand:** "min price is $60", "spikes in sales where clothing drops happen", "these drops are 2x a month", "super successful compared to medium private clothing brands".
2. **Software for dealerships:** "$799 low tier, $999 medium, $1200 max tier", "12-18 sales a week", "large dealership software but still early", "started in April and rapidly grew", "tier based monthly".
3. **Large software company:** "3 tiers", "$1,200,000 in all time sales". Customer estimate from the reader: about 1,000 (fewest), 1,201 (typical) and 1,502 (most).

## Estimate for the software company (not confirmed, not run through an AI)

Assumes a steady ramp from about 3 sales a week in April to 16 a week now. Tier mix 30% low, 45% medium, 25% max (average price about $989).

| Month | Sales/week (est.) | New sales in month | Cumulative |
|---|---|---|---|
| April (from the 1st) | 3 | ~13 | 13 |
| May | 5 | ~22 | 35 |
| June | 7 | ~30 | 65 |
| July | 9 | ~39 | 104 |
| August | 11 | ~48 | 152 |
| September | 14 | ~61 | 213 |
| October (to the 21st) | 16 | ~48 | ~261 |

- If the prices are **monthly subscriptions**: about 240 active dealerships now (about 5% churn), about $237,000 monthly recurring revenue, about $700,000 billed since April.
- If the prices are **one-time sales**: about $258,000 in total.

**Open question:** which reading is correct. This matters for the dashboard's numbers.

## Base launch to-do

The user's list for the base launch, in their order:

1. **Make the website:** the Mirrorkit hub that links every dashboard by its off-brand name, each on its own sub-link with its own settings.
2. **Striped dashboard (Stripe-style), final checks:** check on a real iPhone (notch and home-indicator spacing, settings controls, pull-down sheets, midnight rollover) and confirm GitHub Pages serves the latest build.
3. **Larp tube studio (YouTube Studio-style), polish:** bring it up to the striped dashboard's standard (1:1 layout from screenshots, off-brand name and logo, today-anchored ranges, triple-tap editing, settings, notifications).
4. **Cash App-style dashboard, create.**
5. **Venmo-style dashboard, create.**
6. **Robinhood-style dashboard, create.**

New dashboards are built 1:1 from reference screenshots the user provides, using off-brand names on the site.

## Planned work

1. **AI server for the description reader** (task #1). Options and constraints:
   - A static page cannot call an AI service without exposing the key. A small serverless function (Cloudflare Workers, Vercel or Netlify, all have free tiers) holds the key.
   - The page sends the description and gets back structured fields (prices, sales rate, drops, all-time sales, random, anything else needed).
   - The rule-based reader stays as the fallback when the server is unreachable.
   - Needs: an API key, a host, and a decision on hosting.
2. **Per-dashboard sub-links with their own settings:**
   - One folder per dashboard holding its config, with a shared engine.
   - Each dashboard stores its settings under its own key.
   - A hub page at the root lists the dashboards by off-brand name.
   - Settings stay on the device unless a server is added for sync.
3. **Adaptive layout:** light/dark from the phone's setting, text size, reduced motion, rotation and tablets. Test across a set of phone and tablet sizes.
4. **Fix the settings report:** reproduce the iPhone issue (controls not changing) with the user's details: which controls, whether the sheet scrolls, and whether they opened the page from Safari or the Home Screen icon.

## Open questions for the user

- Are the software prices monthly subscriptions or one-time sales?
- Do dashboard settings need to sync across devices, or is this phone-only for now?
- Where should the site be hosted? GitHub Pages can serve the dashboards. The AI part needs a serverless host.
- Should the backup Studio page be stripped of its YouTube logo and "Studio" wording before anything is published?
- Trademark note: the striped dashboard copies the look of the Stripe app. A different name does not cover the look. Consider changing the colours and layout before publishing.
