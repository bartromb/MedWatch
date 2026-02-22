# MedWatch — Wachtplanning / On-Call Scheduler

<div align="center">

![MedWatch](https://img.shields.io/badge/MedWatch-v2.1-3b82f6?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-10b981?style=for-the-badge)
![HTML](https://img.shields.io/badge/HTML-Single%20File-f97316?style=for-the-badge&logo=html5)
![React](https://img.shields.io/badge/React-18-61dafb?style=for-the-badge&logo=react)
![No Backend](https://img.shields.io/badge/Backend-None%20required-8b5cf6?style=for-the-badge)

**🇳🇱 [Nederlands](#nederlands) · 🇬🇧 [English](#english)**

</div>

---

## 📸 Screenshots

<table>
  <tr>
    <td align="center"><b>Kalender</b></td>
    <td align="center"><b>Overzicht</b></td>
  </tr>
  <tr>
    <td><img src="screenshots/screenshot-calendar.svg" alt="Kalender" width="540"/></td>
    <td><img src="screenshots/screenshot-overview.svg" alt="Overzicht" width="540"/></td>
  </tr>
  <tr>
    <td align="center"><b>Instellingen — rolbenaming</b></td>
    <td align="center"><b>Login</b></td>
  </tr>
  <tr>
    <td><img src="screenshots/screenshot-settings.svg" alt="Instellingen" width="540"/></td>
    <td><img src="screenshots/screenshot-login.svg" alt="Login" width="540"/></td>
  </tr>
</table>

---

## 🇳🇱 Nederlands <a name="nederlands"></a>

### Wat is MedWatch?

MedWatch is een **volledig browser-gebaseerde wachtplanningsapplicatie** voor medische teams, zorgpersoneel en andere organisaties met roterende diensten. De applicatie bestaat uit **één enkel HTML-bestand** en vereist geen server, geen installatie en geen internetverbinding na het eerste laden.

---

### ✨ Functies

#### 📅 Planning
- **Interactieve kalender** — maandoverzicht met kleurgecodeerde medewerkers, weekendmarkering, feestdagen en vergrendelde periodes in één oogopslag
- **Auto-inplannen** — kies tussen *evenredige* of *volledig willekeurige* verdeling (zie [Verdeelmodus](#verdeelmodus-nl))
- **Meerdere slots per dag** — 1e, 2e, ... medewerker met rang-consistentie per week: dezelfde persoon houdt dezelfde rang binnen een ISO-week
- **Wachtperiodes** — definieer periodes met een afwijkend aantal medewerkers per dag, met aparte instellingen per dagtype (weekdag / weekend / feestdag)

#### ⚖️ Eerlijkheid & Analyse
- **Evenredigheidsscore** — real-time equity score (0–100%) met kleurgecodeerde voortgangsbalk
- **Overdracht vorige periode** — neem historische tellingen mee over planningsperiodes voor eerlijkheid op lange termijn
- **Overzicht** — tabel per medewerker met totalen, weekdagen, weekends, feestdagen en maximale aaneengesloten weken
- **Probleemdetectie met oplossingsvoorstellen** — bij equity-afwijkingen stelt de app concreet voor welke wacht van wie naar wie verschoven kan worden, inclusief een specifieke datum (zie [Probleemdetectie](#probleemdetectie-nl))

#### 🔧 Beheer
- **Vergrendelingen** — sluit datumranges af zodat ze niet meer bewerkt kunnen worden; vergrendelde dagen worden overgeslagen bij auto-inplannen
- **Admin-bewerkingen** — manuele aanpassingen worden paars gemarkeerd (✏) en apart geteld
- **Feestdagen** — Belgische feestdagen 2025–2027 ingebouwd + eigen aangepaste feestdagen per organisatie
- **Aanpasbare rolbenaming** — hernoem "arts/artsen" naar bv. "verpleger/verplegers", "medewerker", "technicus" — 8 snelle presets + volledig vrij in te stellen (enkelvoud, meervoud, icoon, planningstitel)
- **PDF-export** — afdrukbare planning per maand, per wachtperiode of vrij gekozen datumrange
- **Admin doet niet mee** — gebruikers met de rol *Admin* worden automatisch uitgesloten van de wachtverdeling, statistieken en evenredigheidberekening

#### 👤 Gebruikers
- **Rolgebaseerde toegang** — *Admin* (volledig beheer) en *medewerker* (eigen kalender + voorkeuren)
- **Voorkeuren per dag** — positieve ✓ of negatieve ✕ datumvoorkeur, met snelle maandknoppen om een volledige maand in één klik in te stellen en daarna dag per dag bij te sturen
- **Lokale authenticatie** — gebruikersnaam/wachtwoord, opgeslagen als hash in `localStorage`

---

### 🔍 Functies in detail

#### <a name="verdeelmodus-nl"></a>Verdeelmodus bij auto-inplannen

Bij het starten van auto-inplannen kies je een verdeelmodus:

| Modus | Werking |
|-------|---------|
| **⚖ Evenredig — per week** *(standaard)* | Zoveel mogelijk dezelfde persoon een volledige week (+40 bonus per dag reeds in die week). Eerlijk verdeeld per dagtype, geen opeenvolgende weken (−100 straf), voorkeuren (+5/−10), rang-consistentie (+50). |
| **🎲 Willekeurig — gespreid** | Losse dagen at random over de periode, niet per week gebundeld. Wél eerlijk verdeeld en voorkeuren gerespecteerd. Wie weinig beschikbaar is (weinig positieve of veel negatieve dagen) krijgt voorrang voor die dagen. |

#### <a name="probleemdetectie-nl"></a>Probleemdetectie & oplossingsvoorstellen

Het probleempaneel (kalender én overzicht) analyseert automatisch:

- **Equity-afwijkingen** (≥ 1.5 van het gemiddelde) — met vermelding of iemand te veel of te weinig heeft, en een concreet voorstel: *"Verschuif een wacht van Dr. Peters naar Dr. Martens (bv. 15 jul, +2 andere mogelijkheden)"*. Vergrendelde datums worden uitgesloten van suggesties.
- **Opeenvolgende weken** — wie meer dan één week aaneengesloten ingepland staat, met advies welke wacht verplaatst kan worden
- **Open slots** — datums binnen een periode die nog niet volledig ingevuld zijn, met de concrete datums vermeld

#### Maanddefault voor voorkeuren

Per maand in het voorkeursscherm staan drie kleine knoppen boven het minikalendraster:

- **✓ alles** — zet de volledige maand op positief. Is de maand al volledig positief, dan wist de knop alles.
- **✕ alles** — zelfde logica voor negatief.
- **🗑** — wist alle voorkeuren voor die maand (verschijnt alleen als er al iets ingesteld is).

Daarna kan elke dag nog afzonderlijk worden aangepast door erop te klikken (geen → positief → negatief → geen).

---

### 🚀 Snel starten

1. Download `index.html`
2. Open het bestand in een browser (Chrome, Firefox, Edge, Safari)
3. Login met gebruikersnaam `admin` en wachtwoord `admin123`
4. Voeg medewerkers toe via **Gebruikers** → **+ Gebruiker toevoegen**
5. Stel eventueel een wachtperiode in via **Wachtperiodes**
6. Klik op **⚡ Auto-inplannen** en kies een verdeelmodus

> **Geen server nodig.** Het bestand werkt volledig lokaal. Alle data wordt opgeslagen in `localStorage` van de browser.

---

### 💾 Data & Privacy

- Alle data blijft **lokaal op uw toestel** in de browser `localStorage` onder sleutel `medwatch_v2`
- Geen externe servers, geen tracking, geen cookies
- Exporteren: `localStorage.getItem('medwatch_v2')` in de browserconsole
- Importeren: `localStorage.setItem('medwatch_v2', '...')` en herlaad de pagina
- Wissen: klik **Reset** op de kalender of wis de browser-opslag voor deze pagina

### ⚠️ Beperkingen

| Beperking | Toelichting |
|-----------|-------------|
| Gedeeld gebruik | `localStorage` is per browser/toestel — geen real-time synchronisatie tussen gebruikers |
| Offline-only | Na het eerste laden is geen internet nodig, maar data is niet cloudgesynchroniseerd |
| Browseropslag | Typisch 5–10 MB limiet; ruim voldoende voor jaren planning |

Voor gedeeld gebruik op meerdere apparaten: exporteer/importeer de JSON-data manueel via de browserconsole.

---

## 🇬🇧 English <a name="english"></a>

### What is MedWatch?

MedWatch is a **fully browser-based on-call scheduling application** for medical teams, care staff, and any organisation with rotating duties. The entire application is a **single HTML file** — no server, no installation, no internet connection required after initial load.

---

### ✨ Features

#### 📅 Scheduling
- **Interactive calendar** — monthly view with colour-coded staff, weekend highlighting, holidays and locked ranges visible at a glance
- **Auto-schedule** — choose between *equity-based* or *fully random* distribution (see [Distribution mode](#distribution-mode-en))
- **Multiple slots per day** — 1st, 2nd, ... staff member with rank consistency per week: the same person keeps the same rank within an ISO week
- **On-call periods** — define periods with custom staffing levels, with separate settings per day type (weekday / weekend / holiday)

#### ⚖️ Fairness & Analysis
- **Equity score** — real-time fairness indicator (0–100%) with colour-coded progress bar
- **Carry-over from previous period** — bring historical shift counts forward across planning cycles for long-term fairness
- **Overview** — per-staff table with totals, weekdays, weekends, holidays and max consecutive weeks
- **Problem detection with fix suggestions** — on equity deviations, the app proposes a specific swap: who should give a shift to whom, and on which date (see [Problem detection](#problem-detection-en))

#### 🔧 Administration
- **Period locking** — lock date ranges to prevent further edits; locked days are automatically skipped during auto-scheduling
- **Admin edits** — manual changes are highlighted in purple (✏) and counted separately
- **Holidays** — Belgian public holidays 2025–2027 built in + custom organisation-specific holidays
- **Configurable role labels** — rename "doctor/doctors" to e.g. "nurse/nurses", "employee", "technician" — 8 quick presets + fully custom (singular, plural, icon, planning title)
- **PDF export** — printable schedule per month, per on-call period, or custom date range
- **Admins excluded from scheduling** — users with the *Admin* role are automatically excluded from shift distribution, statistics and equity calculations

#### 👤 Users
- **Role-based access** — *Admin* (full control) and *staff* (own calendar + preferences)
- **Per-day preferences** — positive ✓ or negative ✕ date preference, with one-click month buttons to set an entire month at once and fine-tune day by day afterwards
- **Local authentication** — username/password stored as a hash in `localStorage`

---

### 🔍 Features in detail

#### <a name="distribution-mode-en"></a>Distribution mode

When starting auto-schedule, choose a distribution mode:

| Mode | Behaviour |
|------|-----------|
| **⚖ Equity — per week** *(default)* | Same person keeps the full week where possible (+40 per day already in that week). Fair distribution per day type, no consecutive weeks (−100 penalty), preferences (+5/−10), rank affinity (+50). |
| **🎲 Random — spread** | Individual days assigned at random across the period, not bundled per week. Still fair (equity scoring) and preferences still respected. Staff with limited availability (few positive / many negative days) get priority for those days. |

#### <a name="problem-detection-en"></a>Problem detection & fix suggestions

The problems panel (calendar and overview) automatically analyses:

- **Equity deviations** (≥ 1.5 from average) — stating whether someone has too many or too few shifts, with a concrete proposal: *"Move a shift from Dr. Peters to Dr. Martens (e.g. 15 Jul, +2 other options)"*. Locked dates are excluded from suggestions.
- **Consecutive weeks** — anyone scheduled for more than one consecutive week, with advice on which shift to move
- **Open slots** — dates within a period not yet fully filled, listing the specific dates

#### Month defaults for preferences

Each month in the preferences screen has three small buttons above the mini-calendar grid:

- **✓ all** — sets the entire month to positive. If already fully positive, the button clears it instead.
- **✕ all** — same logic for negative.
- **🗑** — clears all preferences for that month (only shown when something is already set).

Individual days can still be toggled afterwards by clicking them (none → positive → negative → none).

---

### 🚀 Quick Start

1. Download `index.html`
2. Open the file in a browser (Chrome, Firefox, Edge, Safari)
3. Log in with username `admin` and password `admin123`
4. Add staff via **Users** → **+ Add User**
5. Optionally create an on-call period via **On-call Periods**
6. Click **⚡ Auto-schedule** and choose a distribution mode

> **No server required.** The file runs entirely locally. All data is stored in the browser's `localStorage`.

---

### 💾 Data & Privacy

- All data stays **locally on your device** in browser `localStorage` under key `medwatch_v2`
- No external servers, no tracking, no cookies
- Export: `localStorage.getItem('medwatch_v2')` in the browser console
- Import: `localStorage.setItem('medwatch_v2', '...')` and reload the page
- Clear: click **Reset** on the calendar or clear browser storage for this page

### ⚠️ Limitations

| Limitation | Notes |
|------------|-------|
| Shared use | `localStorage` is per browser/device — no real-time sync between users |
| Offline only | No internet needed after first load, but data is not cloud-synced |
| Browser storage | Typically 5–10 MB limit; sufficient for years of scheduling |

For multi-device shared use: manually export/import the JSON data via the browser console.

---

## 🛠️ Technical Background / Technische Achtergrond

### Architecture

MedWatch is intentionally a **zero-dependency, zero-build, single-file application**. This design choice prioritises:

- **Portability** — the file can be emailed, put on a USB stick, or hosted on any static file server
- **Longevity** — no `npm install`, no build pipeline, no dependency rot
- **Simplicity** — non-technical users can open it directly without any setup

```
index.html
├── <style>          CSS custom properties, dark theme, layout, component styles
├── <script CDN>     React 18, ReactDOM, Babel Standalone (from cdnjs)
└── <script babel>   Complete application: components, state, scheduling algorithm
```

### Technologies Used / Gebruikte technologieën

| Technology | Version | Role |
|------------|---------|------|
| **React** | 18.2 | UI component framework, hooks-based state management (`useState`, `useMemo`) |
| **ReactDOM** | 18.2 | DOM rendering |
| **Babel Standalone** | 7.23 | In-browser JSX transpilation — no build step required |
| **CSS Custom Properties** | — | Dark theme variables, consistent component styling |
| **localStorage API** | — | Client-side persistent data storage |
| **Browser Print API** | — | PDF generation via `window.print()` |
| **Google Fonts** | — | DM Serif Display + DM Sans typography |

> All CDN resources load from `cdnjs.cloudflare.com` and `fonts.googleapis.com`. For a fully offline setup, download these assets locally and update the relevant `<script src>` and `<link href>` tags.

### State Management

The application uses React's `useState` + `useMemo` hooks exclusively — no external state library. All state serialises to a single JSON object in `localStorage` under the key `medwatch_v2`:

```json
{
  "users": [{ "id": 1, "name": "Admin", "role": "admin" }, { "id": 2, "name": "Dr. Janssen", "role": "doctor" }],
  "schedule": { "2025-07-01": [2, 3], "2025-07-02": [4] },
  "preferences": { "2025-07-05": { "2": "positive", "3": "negative" } },
  "periods": [{ "id": 1, "name": "Zomervakantie", "start": "2025-07-14", "end": "2025-07-20", "slots": 2 }],
  "adminEdits": { "2025-07-10": true },
  "lockedRanges": [{ "id": 1, "start": "2025-07-01", "end": "2025-07-31", "label": "Juli definitief" }],
  "customHolidays": { "2025-07-11": "Vlaamse feestdag" },
  "carryOver": { "2": { "total": 12, "weekday": 8, "weekend": 3, "holiday": 1 } },
  "roleLabel": { "singular": "arts", "plural": "artsen", "icon": "👨‍⚕️", "planningTitle": "Wachtplanning" }
}
```

> Users with `"role": "admin"` are stored but never appear in `schedule` assignments, statistics, or equity calculations.

### Scheduling Algorithm

The auto-scheduler supports two modes:

#### Equity mode — greedy weighted assignment

1. Iterates over each date in the requested range (locked dates skipped)
2. Determines required slots from the active period definition
3. For each slot, scores every eligible (non-admin, not yet assigned today) staff member:

| Score component | Value | Description |
|-----------------|-------|-------------|
| Day-type count | −1 / −2 / −3 | Weekday / weekend / holiday shifts already assigned (incl. carry-over) |
| Consecutive week penalty | −100 | Prevents back-to-back scheduled weeks |
| Positive preference | +5 | Staff member marked this date as preferred |
| Negative preference | −10 | Staff member marked this date as undesirable |
| Rank affinity bonus | +50 | Person already held this rank slot earlier in the same ISO week |
| Tie-break noise | ±0.2 | Small random value to break exact ties |

4. Assigns the highest-scoring candidate; updates running counts for subsequent dates

#### Random mode — uniform random selection

Each slot is filled by selecting uniformly at random from eligible staff. No scoring, no equity tracking, no preference checking.

**Complexity (both modes):** O(d × s × n) — days × slots × staff count. Sub-millisecond for a full year.

### Problem Detection Engine

`detectProblems()` runs reactively via `useMemo` on every schedule change. For equity deviations it finds a concrete swap candidate by:

1. Identifying the over- or under-scheduled staff member
2. Scanning all dates where the over-scheduled person is assigned but the target is not
3. Filtering out locked dates
4. Returning the earliest viable swap date and total count of alternatives

### ISO Week & Consecutive Detection

Rank consistency and consecutive-week detection use ISO 8601 week numbering (`YYYY-Www`). Year-boundary edge cases (week 52/53 → week 1) are handled explicitly.

### PDF Export

PDF generation uses the **browser's native print dialog** (`window.print()`). A self-contained HTML document is opened in a new window with print-optimised CSS — white backgrounds, `page-break-inside: avoid`, no sidebar. No external PDF library required.

---

## 📁 Repository Structure

```
medwatch/
├── index.html               # Complete application (single file)
├── README.md                # This file (NL + EN + technical docs)
├── CHANGELOG.md             # Version history
├── CONTRIBUTING.md          # Contribution guidelines (NL + EN)
├── SECURITY.md              # Security policy (NL + EN)
├── LICENSE                  # MIT License
├── screenshots/
│   ├── screenshot-calendar.svg
│   ├── screenshot-overview.svg
│   ├── screenshot-settings.svg
│   └── screenshot-login.svg
└── .github/
    ├── workflows/
    │   └── deploy.yml       # GitHub Pages auto-deploy on push to main
    └── ISSUE_TEMPLATE/
        ├── bug_report.md
        └── feature_request.md
```

---

## 🔧 Self-Hosting / Zelf hosten

### GitHub Pages (aanbevolen / recommended)

1. Fork this repository
2. Go to **Settings → Pages**
3. Set source: **Deploy from branch** → `main` → `/ (root)`
4. Your app will be live at `https://yourusername.github.io/medwatch/`

The included `deploy.yml` workflow redeploys automatically on every push to `main`.

### Any static host

Upload `index.html` (and optionally `screenshots/`) to any static file host — Netlify, Vercel, Cloudflare Pages, your own server. No build step needed.

### Fully offline

```bash
# Download once
curl -O https://raw.githubusercontent.com/yourusername/medwatch/main/index.html

# Open directly
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

---

## 🤝 Contributing / Bijdragen

Contributions welcome! / Bijdragen zijn welkom!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit: `git commit -m 'Add: description'`
4. Push: `git push origin feature/my-feature`
5. Open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for style guidelines.

**Ideas / Ideeën:**
- [ ] Import/export JSON backup via UI
- [ ] Multi-language UI (i18n)
- [ ] Email notifications (via `mailto:` links)
- [ ] iCal (`.ics`) export
- [ ] Dark/light mode toggle
- [ ] Mobile-optimised layout
- [ ] Optional shared backend for multi-device sync

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.  
Free to use, modify and distribute for any purpose, including commercial use.

---

<div align="center">
Built with ❤️ as a single HTML file · Geen server nodig · No server required
</div>
