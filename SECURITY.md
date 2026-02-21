# Security Policy / Beveiligingsbeleid

## 🇳🇱 Nederlands

### Belangrijke noot over beveiliging

MedWatch is ontworpen als een **lokale, single-user of intranet-applicatie**. De beveiliging is bewust lichtgewicht gehouden:

- Wachtwoorden worden opgeslagen als een **eenvoudige hash** (niet crypto-grade)
- Alle data staat in **browseropslag (localStorage)** — zichtbaar voor iedereen met fysieke toegang tot de browser
- Er is **geen HTTPS-vereiste**, geen server-side validatie, geen sessie-tokens

**Gebruik MedWatch NIET** voor gevoelige patiëntdata, persoonlijke gezondheidsinfo (PHI/PII) of andere privacygevoelige informatie. Het is een planningshulpmiddel, geen beveiligd informatiesysteem.

### Een kwetsbaarheid melden

Open een [GitHub Issue](../../issues) met het label `security` of stuur een e-mail naar de beheerder van deze repository.

---

## 🇬🇧 English

### Important security note

MedWatch is designed as a **local, single-user or intranet application**. Security is intentionally lightweight:

- Passwords are stored as a **simple hash** (not cryptographically secure)
- All data lives in **browser storage (localStorage)** — visible to anyone with physical access to the browser
- There is **no HTTPS requirement**, no server-side validation, no session tokens

**Do NOT use MedWatch** for sensitive patient data, personal health information (PHI/PII), or any privacy-sensitive information. It is a scheduling aid, not a secure information system.

### Reporting a vulnerability

Please open a [GitHub Issue](../../issues) with the `security` label or contact the repository maintainer directly.
