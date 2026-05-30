# ⏰ Time Zone Converter

A simple, beautiful web app for sharing times across timezones. Perfect for distributed teams and global meetings.

## ✨ Features

- 🌍 **City/timezone search** - Search by city name, country, region, or GMT offset (e.g. "New York", "Japan", "GMT+8")
- ⚡ **Quick paste** - Paste a time string like `tomorrow 8PM NZDT` or `Feb 15 5:30 PM PST` and the form fills itself in automatically
- 🗓️ **Relative time parsing** - Natural phrases like `tomorrow 8PM NZDT`, `next Monday 9AM KST`, or `in 2 hours` are understood
- 🔗 **Shareable links** - Generate URLs that convert automatically to each viewer's local timezone
- 👁️ **Link preview** - See exactly what recipients will see before you share
- 🎨 **Light & Dark mode** - Themes that save your preference
- ⏳ **Live countdown** - Real-time countdown to future events
- 📅 **Google Calendar** - One-click "Add to Calendar" on shared links
- 🕐 **12h / 24h toggle** - Choose your preferred time format when creating links
- 📆 **Optional date** - Toggle off the date to use today as the anchor; the link is still a clean ISO URL
- 📱 **Fully responsive** - Works on all devices
- 🔒 **Privacy-first** - Everything runs in the browser, no data sent to servers

## 🚀 Quick Start

### Use Online

1. Open the app
2. Paste a time string into the **Quick paste** field, or fill in the form manually
3. Click "Generate shareable link"
4. Share the URL with anyone — it shows in their local time automatically

### Shared link view

- Shows the original scheduled time in UTC so the context is clear
- Displays the event converted to the viewer's local timezone
- Live countdown timer for future events
- Buttons to add to Google Calendar, copy the link, or create a new one

## ⚡ Quick Paste

Paste almost any natural time string and the form will auto-fill the time, date, and timezone fields.

### Absolute times

| Input | Interpreted as |
|-------|----------------|
| `5:30 PM PST` | 17:30, America/Los_Angeles, no date |
| `14:00 UTC` | 14:00, UTC, no date |
| `9.30AM EST` | 09:30, America/New_York, no date |
| `Feb 15 5:30 PM PST` | 17:30, America/Los_Angeles, 2026-02-15 |
| `15 Feb 2026 17:00 GMT` | 17:00, UTC, 2026-02-15 |
| `2026-03-01 14:00 SGT` | 14:00, Asia/Singapore, 2026-03-01 |
| `03/15/26 9AM EST` | 09:00, America/New_York, 2026-03-15 |
| `15/03/26 9AM GMT` | 09:00, UTC, 2026-03-15 |
| `2/18 11PM new york` | 23:00, America/New_York, Feb 18 (current year) |
| `17:00 GMT+8` | 17:00, GMT+8 fixed offset |
| `9AM JST` | 09:00, Asia/Tokyo, no date |

### Relative times

Relative expressions are resolved against your local time at the moment you paste them. The form is filled with the computed date and time in your local timezone.

| Input | Interpreted as |
|-------|----------------|
| `tomorrow 8PM NZDT` | Next calendar day, 20:00, Pacific/Auckland |
| `today 3PM JST` | Today, 15:00, Asia/Tokyo |
| `tonight 11PM EST` | Today, 23:00, America/New_York |
| `next Monday 9AM KST` | Coming Monday, 09:00, Asia/Seoul |
| `this Friday 5PM IST` | This Friday, 17:00, Asia/Kolkata |
| `day after tomorrow 6PM SGT` | In 2 days, 18:00, Asia/Singapore |
| `in 2 hours` | Now + 2h, your local timezone |
| `in 90 minutes` | Now + 90 min, your local timezone |
| `two hours from now` | Now + 2h, your local timezone |
| `in 3 days` | 3 days from now, your local timezone |

> **Note:** Pure offsets (`in 2 hours`, `in 90 minutes`) always resolve in your local timezone since no source timezone is implied.

### Date format disambiguation

When a numeric date is ambiguous (e.g. `03/04/26`), the timezone in the string is used as a hint. Two-part dates without a year (e.g. `2/18`) default to the current year.

| Timezone | Convention assumed | `03/04/26` reads as |
|----------|--------------------|---------------------|
| US zones (PST, EST, CDT…) | MM/DD/YY | March 4 |
| UK/EU/AU/Asia zones (GMT, CET, SGT, IST…) | DD/MM/YY | 3 April |
| East Asia (JST, KST, CST…) | YY/MM/DD | 2026 March 4 |

If no date is found in the pasted string, the date field is automatically hidden so the link is time-only.

The feedback line always shows exactly what was interpreted — e.g. `✓ Filled in 17:00 · 2026-03-15 · London (read as DD/MM — international format)` — so you can catch any misreads before generating the link.

### Supported timezone abbreviations

Over 80 abbreviations are recognised, including DST variants:

| Region | Examples |
|--------|---------|
| North America | `PST` `PDT` `MST` `MDT` `CST` `CDT` `EST` `EDT` `ET` `PT` `MT` `CT` `AKST` `AKDT` `HST` |
| Atlantic / South America | `AST` `ADT` `NST` `NDT` `BRT` `BRST` `ART` `CLT` `CLST` `COT` `VET` |
| Europe | `GMT` `BST` `CET` `CEST` `EET` `EEST` `WET` `WEST` `MSK` `TRT` `FET` |
| Africa | `WAT` `CAT` `EAT` `SAST` |
| Middle East | `IRST` `IRDT` `GST` `PKT` |
| Asia | `IST` `NPT` `BDT` `ICT` `WIB` `SGT` `MYT` `HKT` `PHT` `KST` `KDT` `JST` |
| Oceania | `AEST` `AEDT` `ACST` `ACDT` `AWST` `AWDT` `NZST` `NZDT` `FJT` `FJST` `TOT` `WST` |

## 👁️ Link Preview

After clicking **Generate shareable link**, a preview panel appears below the URL showing exactly what recipients will see — including the UTC source time, the converted local time, and a live countdown — before you send anything.

## 📖 URL Formats

### Date + time link (recommended for meetings)

Generated by the app, or construct manually. The `iso` parameter is always **UTC**:

```
?iso=YYYYMMDDTHHMMSS
```

| Part | Description |
|------|-------------|
| `YYYY` | 4-digit year |
| `MM` | 2-digit month (01–12) |
| `DD` | 2-digit day (01–31) |
| `T` | Literal separator |
| `HH` | Hour in UTC (00–23) |
| `MM` | Minute (00–59) |
| `SS` | Second (00–59) |

**Example** — meeting on Feb 15, 2026 at 5:00 PM UTC:
```
https://utc-to-local-7f6388.gitlab.io/?iso=20260215T170000
```

### Time-only links (legacy)

Old `?t=HHMM&tz=IANA_TIMEZONE` links are still supported for backwards compatibility, but the app no longer generates them. All new links use the `?iso=` format, with today's date used as the anchor when the date toggle is off.

## 🤖 Integration with Slack Bots

Pass a UTC datetime in the `?iso=` format — all existing links remain fully compatible.

```python
# Python example
from datetime import datetime, timezone

def generate_time_link(dt_utc: datetime) -> str:
    """dt_utc must be a UTC datetime."""
    iso = dt_utc.strftime('%Y%m%dT%H%M%S')
    return f"https://utc-to-local-7f6388.gitlab.io/?iso={iso}"

# Usage
meeting = datetime(2026, 2, 15, 17, 0, 0, tzinfo=timezone.utc)
link = generate_time_link(meeting)
# → https://utc-to-local-7f6388.gitlab.io/?iso=20260215T170000
```

```javascript
// JavaScript / Node example
function generateTimeLink(dateUtc) {
  const pad = n => String(n).padStart(2, '0');
  const iso =
    dateUtc.getUTCFullYear() +
    pad(dateUtc.getUTCMonth() + 1) +
    pad(dateUtc.getUTCDate()) + 'T' +
    pad(dateUtc.getUTCHours()) +
    pad(dateUtc.getUTCMinutes()) +
    pad(dateUtc.getUTCSeconds());
  return `https://utc-to-local-7f6388.gitlab.io/?iso=${iso}`;
}
```

## 📦 Deploy on GitLab Pages

### 1. Create a new repository on GitLab

### 2. Add these files

**`index.html`** — the single HTML file from this project

**`.gitlab-ci.yml`**:
```yaml
pages:
  stage: deploy
  script:
    - mkdir .public
    - cp index.html .public
    - mv .public public
  artifacts:
    paths:
      - public
  only:
    - main
```

### 3. Commit and push

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### 4. Access your site

Your site will be live at: `https://username.gitlab.io/repo-name/`

## 🛠️ Local Development

Open `index.html` directly in your browser. No build process, no dependencies, no server required.

## 🎨 Themes

Click the ☀️/🌙 icon in the top right to toggle light and dark mode. Your preference is saved automatically.

## 📝 License

Free to use and modify for any purpose.


## 📋 Changelog

### 2026-02-27

**New features**
- **Link preview** — after generating a shareable link, a "what recipients see" panel renders inline below the URL, including the live countdown timer, so you can verify the conversion before sending
- **Relative time parsing in Quick paste** — natural phrases are now understood:
  - Day references: `tomorrow`, `today`, `tonight`, `yesterday`, `day after tomorrow`
  - Weekday references: `next Monday`, `this Friday`, `last Tuesday`
  - Offset expressions: `in 2 hours`, `in 90 minutes`, `two hours from now`, `in 3 days`
- **City name matching in Quick paste** — multi-word city names now resolve correctly (e.g. `2/18 11PM new york`, `tomorrow 8PM los angeles`, `3PM kuala lumpur`). Previously only single-word abbreviations and GMT offsets were supported
- **Expanded timezone abbreviation coverage** — ~80 abbreviations now recognised, including DST variants: `NZDT`, `AEDT`, `ACDT`, `AWDT`, `BRST`, `CLST`, `FJST`, `KDT`, `BST`, `CEST`, `EEST`, `WEST` and more
- **Source button** — GitLab link added to the page header next to the theme toggle

**Bug fixes**
- **Two-part dates without year** — `2/18 11PM EST` (no year component) now parses correctly instead of erroring. The `/` separator was previously being captured as the start of a timezone token
- **Timezone regex** — the timezone capture group now requires an initial letter, preventing bare `/` from being mistaken for a timezone abbreviation
- **GMT offset links always use ISO format** — pasting `GMT+7` previously generated a `?t=&tz=Etc%2FGMT-7` URL where the POSIX-inverted sign looked wrong. All links now use `?iso=` (UTC). When the date toggle is off, today's date in the source timezone is used as the anchor

---

Made with ❤️ for distributed teams
