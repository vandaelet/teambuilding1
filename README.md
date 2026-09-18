# Klassenquiz 1ste jaar — digitale versie (met klas-login en leerkrachtpagina)

Eén bestand (`index.html`) met drie schermen:

- **Startscherm** — elke klas klikt op de eigen klasnaam (1C t/m 1J) om in te loggen.
- **Klasscherm** (na het kiezen van een klas) — **Projectie**: de vragen groot in beeld voor de
  beamer, met een "Toon antwoord"-knop. **Onze score**: hier vult die klas enkel de eigen scores
  in. Een klas ziet nooit de scores of ranglijst van een andere klas.
- **Leerkrachtscherm** — enkel bereikbaar met een wachtwoord, toont de **live eindranglijst** van
  alle klassen samen, automatisch berekend en gesorteerd. Zodra een klas op "Score opslaan" klikt,
  verandert deze lijst meteen mee, ook al staat ze open op een heel ander toestel.

## Waarom is er een extra installatiestap (Firebase) nodig?

Om scores écht te delen tussen 8 verschillende klaslokalen/toestellen én automatisch een
gezamenlijke ranglijst te tonen, is een gedeelde plek nodig waar alle scores samenkomen. GitHub
Pages host enkel de website zelf, geen gedeelde data. Daarvoor gebruiken we **Firebase**
(een gratis dienst van Google) als "gedeeld schrift" tussen alle klassen en jou. Dit vraagt een
eenmalige, gratis installatie van een paar minuten — zie de stap-voor-stap uitleg in het gesprek
met Claude, of kort hieronder.

### Firebase instellen (eenmalig)

1. Ga naar **console.firebase.google.com** en meld je aan met een Google-account.
2. Klik op **"Project toevoegen"**, geef het een naam (bv. `klassenquiz`) en rond de wizard af
   (Google Analytics mag je uitschakelen, niet nodig).
3. Klik in het project op het **web-icoon (`</>`)** om een "webapp" toe te voegen. Geef ze een
   naam en klik op **"App registreren"**. Je krijgt een blokje code te zien met een object
   `firebaseConfig = { apiKey: ..., authDomain: ..., ... }`.
4. Kopieer die zes waarden en plak ze in `index.html`, bovenaan het `<script>`-gedeelte, in het
   object `FIREBASE_CONFIG` (vervang de teksten die met `PLAK_HIER` beginnen).
5. Ga in het Firebase-menu naar **Build → Firestore Database** → **"Database maken"**. Kies
   **"Test mode"** (dit maakt de data 30 dagen lang open leesbaar/schrijfbaar — voldoende voor een
   eenmalig evenement; er staan geen persoonsgegevens in, enkel klasnamen en scorecijfers).
6. Klaar. Upload `index.html` nu naar GitHub zoals in de stappen hieronder.

### Het leerkrachtwachtwoord aanpassen

Zoek in `index.html` naar de regel met `const ADMIN_PASSWORD = "teambuilding2026";` en verander de
tekst tussen de aanhalingstekens naar een wachtwoord naar keuze, vóór je het bestand naar GitHub
uploadt.

## Publiceren via GitHub Pages

1. Maak een gratis GitHub-account op github.com.
2. Maak een nieuwe **public** repository.
3. Upload `index.html` (en dit `README.md`) via "Add file → Upload files".
4. Ga naar **Settings → Pages**, kies branch `main` en map `/ (root)`, klik **Save**.
5. Na 1–2 minuten is de site live op `https://JOUW-GEBRUIKERSNAAM.github.io/NAAM-REPOSITORY/`.

## Inhoud aanpassen

Open `index.html` in een teksteditor en zoek de blokken `RONDES` en `SCORE_ITEMS` bovenaan het
`<script>`-gedeelte. Vragen, tips, antwoorden, klassenlijst (`CLASSES`) en maximumscores staan
daar in gewoon leesbare tekst. Ronde 6 bevat nog schoolspecifieke antwoorden — vul die in vóór de
quizdag.

## Belangrijk om te weten

- Het leerkrachtwachtwoord staat zichtbaar in de broncode van de website (iedereen die goed zoekt
  kan het vinden). Voor een eenmalig, niet-gevoelig schoolevenement is dit een aanvaardbaar risico;
  gebruik dus geen wachtwoord dat je elders ook gebruikt.
- Een klas kan, met wat technische kennis, in theorie ook de score van een andere klas aanpassen
  (er is geen "echt" account per klas, enkel een knop). Voor een teambuildingsdag tussen 8 klassen
  van hetzelfde jaar is dat een aanvaardbaar risico; voor iets met hogere inzet zou een steviger
  inlogsysteem (Firebase Authentication) nodig zijn.
