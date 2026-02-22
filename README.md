# MedWatch — Wachtplanning / Duty Planning

> **Bestandsnaam / Filename:** `medwatch.html`  
> Zelfstandige webapplicatie — geen installatie, geen server, geen internetverbinding vereist.  
> Standalone web application — no installation, no server, no internet connection required.

---

## 🇳🇱 Nederlands

### Wat is MedWatch?

MedWatch is een volledig zelfstandige HTML-applicatie voor het beheren van wacht- en dienstplanning in ziekenhuizen, klinieken of andere organisaties. Alles draait in de browser — geen server, geen database, geen account. Gegevens worden lokaal opgeslagen via `localStorage` en kunnen als JSON-backup worden geëxporteerd en geïmporteerd.

### Installatie & gebruik

1. Sla `medwatch.html` op uw computer of gedeelde schijf op.
2. Open het bestand in een moderne browser (Chrome, Firefox, Edge, Safari).
3. Log in met de standaard beheerdersaccount: gebruikersnaam `admin`, wachtwoord `admin123`.
4. Wijzig het wachtwoord onmiddellijk via **Gebruikers → bewerken**.

> Het bestand kan ook op een intranet-webserver geplaatst worden — dan is het bereikbaar voor alle gebruikers in het netwerk zonder extra configuratie.

---

### Functies

#### Kalender & planning
- Maandkalender met drag-and-drop: sleep een arts naar een andere dag om wachten te verschuiven.
- Klik op een dag om handmatig artsen toe te voegen of te verwijderen.
- Kleurcodering per arts; initialen worden weergegeven in de kalender.
- Slots per dag configureerbaar per dagtype (weekdag / weekend / feestdag), per periode.
- Weekeindenuitbreiding: vrijdag kan worden meegeteld als weekenddag.
- Vergrendelde dagen: beheerders kunnen datums of periodes vergrendelen zodat ze niet meer bewerkt kunnen worden.

#### Automatisch inplannen
- Twee modi:
  - **Evenredig (weken):** dezelfde arts krijgt bij voorkeur een volledige ISO-week. Eerlijk verdeeld over dagtypes en periodes. Voorkeuren gerespecteerd. Geen opeenvolgende weken.
  - **Verspreid (willekeurig):** wachten worden per dag willekeurig verdeeld, voorkeuren gerespecteerd.
- Kies een datumrange en klik op **✓ Inplannen**.

#### Algoritme (Evenredige modus) — stap voor stap

Het algoritme werkt in drie fasen:

**Fase 0 — Gedwongen toewijzing**
Dagen waarop slechts één arts beschikbaar is (geen negatieve voorkeur, alle anderen wel) worden als eerste ingevuld. Dit voorkomt dat die arts later "verdubbeld" wordt doordat het planningsalgoritme haar opnieuw kiest voor onbeperkte slots.

**Fase 1 — Weekverdeling via Bresenham-accumulatie**
Per ISO-week wordt één "eigenaar" aangewezen via een accumulator (vergelijkbaar met een round-robin of Bresenham lijnalgoritme):
- Elke arts bouwt een schuldteller op op basis van zijn/haar pro-rata aandeel.
- De arts met de hoogste schuld die beschikbaar is en zijn/haar streefgetal nog niet bereikt, krijgt de week.
- Zware straf (−10⁸) voor opeenvolgende weken.
- Bonus voor artsen met weinig beschikbare dagen totaal (beschermt schaarse beschikbaarheid).
- Eens een arts een week toegewezen krijgt, wordt zijn accumulator teruggesteld naar het volgende verwachte interval.

**Fase 2 — Residueel herbalanceren**
Na de weekverdeling worden resterende open slots ingevuld via een greedy-herbalancering:
- Swap-kandidaten worden berekend: voor elke over-ingeplande arts worden datums gezocht waarop een onder-ingeplande arts beschikbaar is.
- Maximaal 500 iteraties; stopt zodra de verdeling evenwichtig is.

#### Verdeling & statistieken
- **Overzicht:** tabel met totaal, weekdagen, weekends, feestdagen, positieve/negatieve voorkeursdagen en maximale opeenvolgende weken per arts.
- **Probleempaneel:** detecteert automatisch:
  - Te veel of te weinig wachten (drempel: ±1,5 t.o.v. gemiddelde).
  - Opeenvolgende weken.
  - Openstaande datums (iedereen negatief).
  - **Beschikbaarheidswaarschuwing:** als een arts minder dan 60% van het streefgetal aan beschikbare dagen heeft, verschijnt een expliciete waarschuwing vóórdat het inplannen begint.
- **Auto-fix:** één klik lost alle swappable problemen automatisch op.

#### Voorkeuren
- Per arts per dag: positief ✓ / negatief ✕ / geen voorkeur.
- Klik cycleert door de statussen.
- Hele maand in één klik op negatief of wissen.
- Voorkeursdagen worden in groen/rood weergegeven op de kalender.

#### Periodes
- Definieer meerdere wachtperiodes (naam, kleur, datumrange).
- Per periode: aantal slots op weekdagen, weekends en feestdagen afzonderlijk instellen.
- Optioneel: beperk welke artsen mogen deelnemen aan een periode.

#### Feestdagen
- Belgische feestdagen automatisch berekend per jaar (Pasen, Pinksteren, enz.).
- Aangepaste feestdagen toevoegen.
- Feestdagen worden rood gemarkeerd op de kalender.

#### Vergrendelingen
- Vergrendel datumranges met een optioneel label.
- Vergrendelde dagen zijn niet meer bewerkbaar maar blijven zichtbaar.

#### Overdracht
- Neem telwaarden mee van een vorige planningsperiode voor een correcte evenredige verdeling.

#### Gebruikersbeheer
- Meerdere gebruikers met eigen login.
- Twee rollen: **admin** (volledige toegang) en **arts** (alleen eigen kalender en voorkeuren).
- Gebruikers activeren/deactiveren zonder te verwijderen.

#### Instellingen & rolbenaming
- Pas de rolnaam aan: enkelvoud, meervoud, icoon en planningstitel (bijv. "stagiair / stagiairs / 🎓 / Stageplanning").
- Zeven snelle presets: arts, verpleegkundige (gender-neutraal), medewerker, stagiair, vrijwilliger, technicus, bewaker.
- **Taalschakelaar:** kies de taal voor de rolpresets: 🇳🇱 Nederlands · 🇬🇧 English · 🇫🇷 Français · 🇩🇪 Deutsch · 🇨🇳 中文 · 🇯🇵 日本語. De presets vertalen automatisch mee.

#### Exporteren
- **PDF:** maand- of periodeoverzicht met kalender en verdeling.
- **iCal (.ics):** exporteer het rooster per arts als agenda-bestand.
- **E-mail (mailto):** stuur een wachtoverzicht naar een arts.
- **JSON backup:** volledige export van alle data; importeer op een ander apparaat.

---

### Wijzigingslog

| Versie | Wijzigingen |
|--------|-------------|
| v1 | Initiële release: kalender, drag-and-drop, voorkeuren, PDF |
| v2 | Gebruikersbeheer, meerdere rollen, login |
| v3 | Wachtperiodes, feestdagen, vergrendelingen, overdracht, auto-inplannen (equity-algoritme), probleempaneel, auto-fix |
| v6 | Fase 0 singleton-fix, beschikbaarheidswaarschuwing, taalschakelaar rolpresets, verpleegkundige (gender-neutraal), bestandsnaam `medwatch.html` |

---

### Technische opmerkingen

- **Geen installatie:** het bestand gebruikt React 18, ReactDOM en Babel Standalone geladen van cdnjs.cloudflare.com. Voor volledig offline gebruik, download die drie scripts en verwijs er lokaal naar.
- **Opslag:** alle data wordt bewaard in `localStorage` onder de sleutel `medwatch_store`. Browser data wissen = dataverlies. Maak regelmatig een JSON-backup.
- **Beveiliging:** wachtwoorden worden als eenvoudige hash opgeslagen. Voldoende voor intern gebruik op een vertrouwd netwerk; niet geschikt voor publiek toegankelijke omgevingen.
- **Browsercompatibiliteit:** getest in Chrome 120+, Firefox 121+, Edge 120+, Safari 17+. Internet Explorer wordt niet ondersteund.

---

---

## 🇬🇧 English

### What is MedWatch?

MedWatch is a fully self-contained HTML application for managing on-call and duty schedules in hospitals, clinics, or other organisations. Everything runs in the browser — no server, no database, no account. Data is stored locally via `localStorage` and can be exported and imported as a JSON backup.

### Installation & usage

1. Save `medwatch.html` to your computer or shared drive.
2. Open the file in a modern browser (Chrome, Firefox, Edge, Safari).
3. Log in with the default administrator account: username `admin`, password `admin123`.
4. Change the password immediately via **Users → edit**.

> The file can also be placed on an intranet web server — it will then be accessible to all users on the network without any additional configuration.

---

### Features

#### Calendar & scheduling
- Monthly calendar with drag-and-drop: drag a doctor to a different day to move shifts.
- Click on a day to manually add or remove doctors.
- Colour coding per doctor; initials are displayed on the calendar.
- Slots per day configurable per day type (weekday / weekend / holiday), per period.
- Weekend extension: Friday can be counted as a weekend day.
- Locked days: administrators can lock dates or periods to prevent further editing.

#### Auto-scheduling
- Two modes:
  - **Equity (weeks):** the same doctor preferably receives a full ISO week. Fairly distributed across day types and periods. Preferences respected. No consecutive weeks.
  - **Spread (random):** shifts are distributed randomly per day, with preferences respected.
- Choose a date range and click **✓ Schedule**.

#### Algorithm (Equity mode) — step by step

The algorithm works in three phases:

**Phase 0 — Forced assignment**
Days on which only one doctor is available (no negative preference, all others blocked) are filled in first. This prevents that doctor from being assigned additional shifts later because the scheduling algorithm selects them again for unconstrained slots.

**Phase 1 — Week assignment via Bresenham accumulation**
For each ISO week, one "owner" is designated via an accumulator (similar to a round-robin or Bresenham line algorithm):
- Each doctor builds up a debt counter based on their pro-rata share.
- The doctor with the highest debt who is available and has not yet reached their target receives the week.
- Heavy penalty (−10⁸) for consecutive weeks.
- Bonus for doctors with few available days in total (protects scarce availability).
- Once a doctor is assigned a week, their accumulator is reset to the next expected interval.

**Phase 2 — Residual rebalancing**
After week assignment, remaining open slots are filled via greedy rebalancing:
- Swap candidates are calculated: for each over-scheduled doctor, dates are found on which an under-scheduled doctor is available.
- Maximum 500 iterations; stops once the distribution is balanced.

#### Distribution & statistics
- **Overview:** table with total, weekdays, weekends, holidays, positive/negative preference days and maximum consecutive weeks per doctor.
- **Problems panel:** automatically detects:
  - Too many or too few shifts (threshold: ±1.5 relative to average).
  - Consecutive weeks.
  - Open dates (everyone negative).
  - **Availability warning:** if a doctor has fewer than 60% of the target number of available days, an explicit warning appears before scheduling begins.
- **Auto-fix:** one click automatically resolves all swappable problems.

#### Preferences
- Per doctor per day: positive ✓ / negative ✕ / no preference.
- Click cycles through statuses.
- Set an entire month to negative or clear it in one click.
- Preference days are displayed in green/red on the calendar.

#### Periods
- Define multiple duty periods (name, colour, date range).
- Per period: set the number of slots on weekdays, weekends and holidays separately.
- Optional: restrict which doctors may participate in a period.

#### Holidays
- Belgian public holidays automatically calculated per year (Easter, Pentecost, etc.).
- Add custom holidays.
- Holidays are marked red on the calendar.

#### Locks
- Lock date ranges with an optional label.
- Locked days can no longer be edited but remain visible.

#### Carry-over
- Carry forward counts from a previous planning period for correct equitable distribution.

#### User management
- Multiple users with their own login.
- Two roles: **admin** (full access) and **doctor** (own calendar and preferences only).
- Activate/deactivate users without deleting them.

#### Settings & role naming
- Customise the role name: singular, plural, icon and planning title (e.g. "intern / interns / 🎓 / Internship planning").
- Seven quick presets: doctor, nurse (gender-neutral, replaces the previous separate male/female presets), employee, intern, volunteer, technician, guard.
- **Language switcher:** choose the language for role presets: 🇳🇱 Nederlands · 🇬🇧 English · 🇫🇷 Français · 🇩🇪 Deutsch · 🇨🇳 中文 · 🇯🇵 日本語. Presets translate automatically.

#### Export
- **PDF:** monthly or period overview with calendar and distribution table.
- **iCal (.ics):** export the schedule per doctor as a calendar file.
- **Email (mailto):** send a shift overview to a doctor.
- **JSON backup:** full export of all data; import on another device.

---

### Changelog

| Version | Changes |
|---------|---------|
| v1 | Initial release: calendar, drag-and-drop, preferences, PDF |
| v2 | User management, multiple roles, login |
| v3 | Duty periods, holidays, locks, carry-over, auto-scheduling (equity algorithm), problems panel, auto-fix |
| v6 | Phase 0 singleton fix, availability warning, language switcher for role presets, nurse preset gender-neutral, filename `medwatch.html` |

---

### Technical notes

- **No installation:** the file uses React 18, ReactDOM and Babel Standalone loaded from cdnjs.cloudflare.com. For fully offline use, download those three scripts and reference them locally.
- **Storage:** all data is stored in `localStorage` under the key `medwatch_store`. Clearing browser data = data loss. Use the JSON backup regularly.
- **Security:** passwords are stored as a simple hash. Sufficient for internal use on a trusted network; not suitable for public-facing deployments.
- **Browser compatibility:** tested in Chrome 120+, Firefox 121+, Edge 120+, Safari 17+. Internet Explorer is not supported.
