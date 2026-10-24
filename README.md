# Datacom Field Kit — Field Kit Web

The Datacom Field Kit as a universal web app for **Android and iOS**.
Installable, works offline, no account, no cloud — all data lives in the
browser on the device (localStorage).

**Current version:** v4.6.1

This repo is now the single home of the app. The standalone Android APK
is retired (v2.3 was the last APK build); all new work ships here.

## Install

- **iPhone:** open the URL in Safari → Share → Add to Home Screen.
- **Android:** open the URL in Chrome → menu (⋮) → Install app
  (or Add to Home screen).

## How it works

- `index.html` — the entire app in one file: project hub, time tracker
  (timers + manual entries), cable pull, camera storage, PoE budget,
  subnet/IP planner, port log, materials log, and the always-on final
  materials log.
- `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png` —
  PWA install support plus an offline service worker (page is always
  fetched fresh when online, cached copy is the offline fallback).
- `apple-touch-icon.png`, `logo.png` — home-screen icon and branding
  (keystone data jack).
- Backups: the in-app Backup section exports all data as JSON and can
  restore it; each project card can also export/import individually
  (`fieldkit-*.json`), which is the easiest way to move a job between
  devices.

## Hosting

GitHub Pages (Deploy from branch → `main`, root):

https://whitefrostl33t.github.io/datacom-field-kit-web/

## Changelog

- **v4.6.1** — Hotfix: on the first sync, the app now re-downloads time entries once so entries logged before v4.6 pick up their author names (the regular sync only fetches changed entries, so older entries never received their stamps).

- **v4.6** — Per-user time entries: every entry shows who logged it, the ConnectWise log groups entries by person with per-person totals, you can only edit your own entries (the project owner can edit anyone's), and a teammate's save no longer repaints over a form you're filling in — you get a tap-to-refresh pill instead.

- **v4.5.2** — Sync fix: projects shared with you after your last sync now arrive with their history; projects you are removed from leave your device

- **v4.5.1** — Dashboard week chart labels show the exact hours (7.25, 7.5, 7.75) instead of rounding to one decimal

- **v4.5** — Admin: permanent project delete (with record counts), all row actions under three-dot menus, Create user on the floating + button

- **v4.4.2** — Sync fix: settings for a deleted project could block every sync with a server security error - they are now skipped, and a refused settings row no longer stops the rest of the sync

- **v4.4.1** — Desktop: content stretches the full width of the window on every page - no more empty gap on the right of wide screens

- **v4.4** — Admins can set a display name per user (Admin > Users > Set name); names show instead of emails in sharing, Technicians and Admin. One-time setup: run migration-4.4-display-names.sql and re-deploy the admin Edge Function

- **v4.3.2** — Desktop Dashboard: Hours this week and Recent activity are now stacked full-width instead of side by side

- **v4.3.1** — Desktop: removed the empty space at the top (content starts at the top, three-dot menu floats in the corner); Hours this week card no longer stretches with a gap underneath; long notes in Recent activity trimmed to two lines on the Dashboard

- **v4.3** — New Dashboard screen is now the app's landing page (greeting, stats, hours chart, recent activity); Projects is its own screen with search + New Project; Done is now called Closed; desktop top bar removed (sidebar carries the branding), three-dot menu stays top-right

- **v4.2** — Renamed the Dashboard tab to Activity (it is the activity log) and moved it below Projects and Timer in the sidebar; desktop Hours-this-week chart is taller so the card has no dead space

- **v4.1.1** — Fix: materials without a unit no longer print (undefined) in Connectwise Notes.

- **v4.1** — Desktop layout now matches the design: left sidebar with your projects and sync status, project search, stat cards (today, this week, cable this week, active projects) and chart + activity side by side on wide screens.

- **v4.0** — Visual Dashboard redesign complete (home header, color-banded tiles, project interior, new Timer and PoE screens, desktop sidebar layout) plus a new Admin area: in-app user creation, admin assign/remove, project oversight and repairs (one-time setup: migration-4.0-admin.sql + admin Edge Function).

- **v3.0.22** — New look, step 4: inside a project — color header band, total-time hero, module tiles, recent activity and a Start Timer button.

- **v3.0.21** — New look, step 3: project cards are now color-banded tiles with total hours in the project's color.

- **v3.0.20** — New look, step 2: Projects screen opens with a home header — today's time, this week's hours chart and recent activity.

- **v3.0.19** — New look, step 1 of the Visual Dashboard redesign: refreshed colors and pill tab bar.

- **v3.0.18** — Importing a project now always makes a fresh copy with
  new IDs (fixes sync conflicts with the original project).

- **v3.0.17** — Fixed sync: projects stuck only on a device (never
  uploaded) now heal themselves and upload instead of failing every sync.

- **v3.0.16** — Connectwise Notes: copying a single entry now includes
  the day's materials on the last "On site" entry (also shown in the list).

- **v3.0.15** — Fixed: removing a shared project on your device now
  leaves it instead of deleting it for the owner; re-inviting a member
  works again. (Needs the one-time migration-3.0.15.sql policies.)

- **v3.0.14** — Fixed (iOS): header no longer slides under the notch /
  status bar (safe-area padding).

- **v3.0.13** — Fixed: missing gap between the Active / Done tabs and
  the first project card.

- **v3.0.12** — Materials: "Your picks" is now a single swipeable row
  of pills (name and remove in one pill).

- **v3.0.11** — Projects view: Active / Done tabs with counts; status
  is now a colored pill on each card (green active, red done).

- **v3.0.10** — Time entries now snap start and end to the nearest
  15 minutes (timer and manual entries); 15-minute minimum.

- **v3.0.9** — Fixed: Copy buttons in "Copy a single entry" squeezed the
  entry text — buttons now use the compact inline style.

- **v3.0.8** — Fixed: Share picker checkboxes rendered full-width above
  each email — now inline beside it.

- **v3.0.7** — Fixed: Copy buttons in "Copy a single entry" stretched to
  full row height — now compact.

- **v3.0.6** — Share project: pick people from a list with checkboxes
  instead of typing emails. Ticket shows as CW # next to the project name
  everywhere (cards, timer, dashboard, export). Connectwise Notes: copy a
  single time entry (project header + that entry) for split days.

- **v3.0.5** — Technicians card now reflects project membership (owner +
  invited members, badged); hand-typed names kept as read-only legacy rows;
  manual add/remove removed.

- **v3.0.4** — Fixed projects sync (the real root cause): Postgres enforces
  both INSERT and UPDATE RLS policies on upsert, and the update check fails
  for rows that do not exist yet — so projects now use explicit INSERT,
  falling back to UPDATE on conflict.

- **v3.0.3** — New ⋮ menu item: Sync diagnostics (sign-in, token match,
  project ownership); fixed a background pull marking failed uploads as synced.

- **v3.0.2** — Fixed sync 403 on projects: edits now use an explicit UPDATE
  (Postgres re-checks the INSERT RLS policy on upsert, failing when owner_id
  is omitted from the row).

- **v3.0.1** — Fixed first sync failing on projects with technicians/calculator
  data (child rows now push after their project); sync errors show the reason.

- **v3.0** — Accounts + multi-user sync (Supabase): sign in, projects sync
  across devices in real time, per-project invites, offline-first.

- **v2.9.7** — Export moved into the card ⋮ menu; new module icons
  (cable spool, patch panel, ethernet port); About line removed.

- **v2.9.6** — module toggles moved into a gear dialog in the Details
  card; Technicians card: shorter title, + button to add, trash icon
  to remove.

- **v2.9.5** — About page shows only the last 4 changelog entries.

- **v2.9.4** — swipe-back walks through app screens instead of
  closing the app; refresh/reopen picks up where you left off.

- **v2.9.3** — fixed the active tab rendering as a blue pill that hid
  its icon (old CSS class collision); tab icons stay visible now.

- **v2.9.2** — tab bar icons stay visible when selected; inside a
  project the bottom bar becomes an icons-only switcher for that
  project's enabled modules (replaces the dropdown).

- **v2.9.1** — bottom tab bar (Projects / Timer / Dashboard); Timer
  tab with quick-start and live timer; Dashboard activity feed
  (time, cable, materials); Backup, Import and About in the header
  menu; About page shows version + changelog.

- **v2.9** — projects list refresh: whole card taps to open, Delete
  moved into a per-card overflow menu (Export stays visible), + New
  Project is now a floating action button, Import lives in the header
  menu.

- **v2.8** — hotfix: restored the backup/restore screen and materials-tab
  functions that a bad edit had removed in v2.7.

- **v2.7** — new Connectwise Notes section: time entries, cable and
  materials combined in one professional export that grows to fit
  (no scrolling); the old Time-tab summary box is gone.

- **v2.6.1** — backup export simplified: no more raw JSON preview,
  single full-width Backup button.
- **v2.6** — fixed iOS date/time fields overflowing their card.

- **v2.5** — footer now reads "Field Kit Web".
- **v2.4** — backup/project imports accept `.txt` files; `.json`
  downloads keep the right file type on Android.
- **v2.3** — version number shown in the footer.
- **v2.2** — spacing fix: Import button no longer touches the top
  project card.
- **v2.1** — Import Project is a toggle button like + New Project.
- **v2.0** — import a project from a `fieldkit-*.json` export
  (merges everything; re-import creates a copy); time entry notes
  field wraps and grows as you type.
- **v1.9** — projects sort newest-first; per-project Export button
  (self-contained JSON).
- **v1.8** — removed the preset quick picks; "Your picks" learns
  from what you type.
- **v1.7** — removed the locked Final materials log row from the
  module toggles.
- **v1.6** — section tabs became a dropdown; new always-on Final
  materials log; export moved there; personal quick picks.
- **v1.5** — stopwatch rounds up to 15-minute increments; materials
  export leads with project name + ConnectWise #; cable footage
  grouped by cable type.
- **v1.4** — "Run label" renamed to "Cable type".
