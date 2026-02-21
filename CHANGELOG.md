# Changelog

All notable changes to MedWatch are documented here.  
Alle wijzigingen aan MedWatch worden hier gedocumenteerd.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [2.0.0] — 2025

### Added / Toegevoegd
- **Admin edit tracking** — manual changes highlighted in purple (`✏`), separately counted and listed in overview
- **Period locking** — admin can lock date ranges to prevent further edits (`🔒`)
- **PDF export** — printable schedule per month, per on-call period, or custom date range
- **Rank assignment** (1st, 2nd, ... staff per day) — rank consistency enforced within the same ISO week and period; rank shown on calendar tags and in assignment modal
- **Carry-over from previous period** — seed equity counts from a prior planning cycle for long-term fairness
- **Weekend & holiday visual distinction** — weekend column headers highlighted in orange; holiday cells in red; custom holidays supported
- **Custom holidays** — admin can add organisation-specific holidays alongside Belgian public holidays (2025–2027)
- **Configurable role labels** — rename "arts/artsen" to any role (8 presets + fully custom singular, plural, icon, planning title)
- **Settings page** — dedicated admin page for role label configuration with live preview
- **Problem detection panel** — automatic flagging of equity deviations ≥3, consecutive weeks, unfilled slots
- **Locked ranges page** — manage all locked periods in a dedicated view

### Changed / Gewijzigd
- Storage key updated to `medwatch_v2` (new data model)
- Auto-scheduler now respects locked ranges (skips locked dates)
- Auto-scheduler now seeds equity from carry-over data
- Auto-scheduler rank-consistency logic (prefers same person in same rank slot within a week)
- `SlotPicker` label now uses configured role label
- All UI text driven by `roleLabel` configuration (56 dynamic label references)
- Navigation extended with Locks, Holidays, Carry-over, Settings pages
- Sidebar subtitle now shows configured planning title and icon

### Fixed / Opgelost
- Date parsing now consistently uses `T00:00:00` suffix to avoid timezone-off-by-one errors

---

## [1.0.0] — 2024

### Added / Toegevoegd
- Interactive monthly calendar view
- Role-based access (Admin / Doctor)
- Auto-scheduling algorithm with equity scoring, preference support, consecutive-week penalty
- On-call period definitions with per-day-type slot counts
- Equity suggestions panel (swap recommendations after manual edits)
- Preferences page (positive/negative date preferences per staff member)
- User management (add, edit, deactivate, delete, change password)
- Overview page with per-staff distribution table and equity score
- Doctors/staff list page with progress bars
- Belgian public holidays 2025–2026 built in
- Local authentication (username + hashed password in localStorage)
- Dark theme with CSS custom properties
- Responsive layout (sidebar collapses on smaller screens)
