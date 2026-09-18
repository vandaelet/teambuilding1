# Klassenquiz &amp; teambuilding 1ste jaar — digitale versie

Eén bestand (`index.html`) met drie schermen:

- **Startscherm** — elke klas klikt op de eigen klasnaam (1C t/m 1J) om in te loggen.
- **Klasscherm** (na het kiezen van een klas), met twee tabbladen:
  - **📽 Kwis** — per ronde wordt elke vraag groot geprojecteerd; de klas typt één gezamenlijk
    antwoord in. Zolang de ronde niet is ingediend, kan elk antwoord nog aangepast worden (via
    "Vorige"/"Volgende"). Na de laatste vraag verschijnt een letterraadsel-scherm: de tip wordt
    herhaald en de beginletters van de zonet ingevulde antwoorden verschijnen automatisch in
    vakjes. Pas na "Ronde indienen" worden de juiste antwoorden getoond (met ✓/✗) en telt het
    programma zelf de rondescore — die ronde kan dan niet meer bewerkt worden. Voor de ene vraag
    waarvan het antwoord van school tot school of van geluidsfragment tot geluidsfragment
    verschilt (het afgespeelde lied, en de volledige Ronde 6 "Ontdek onze school"), beoordeelt de
    klas zelf "Juist"/"Fout" na het indienen — precies zoals bij klassikale verbetering op papier.
  - **🏃 Teambuilding-activiteiten** — hier vult de begeleidende leerkracht per doe-opdracht het
    gemeten resultaat in (tijd in seconden, afstand/hoogte in cm, aantal). Voor Opdracht 1
    (klasfoto) en Opdracht 7 (dierenalfabet) vult de leerkracht rechtstreeks het resultaat in.
  - Een klas ziet nooit de scores, antwoorden of ranglijst van een andere klas.
- **Leerkrachtscherm** — enkel bereikbaar met een wachtwoord, toont de **live eindranglijst** van
  alle klassen samen: kwispunten (automatisch verbeterd) + teambuildingpunten (automatisch
  gerangschikt op basis van de ingevulde tijden/afstanden/aantallen, telkens 10 punten voor de
  beste klas tot 1 punt voor de laatste, nadien gehalveerd — exact zoals in het originele
  draaiboek). Zodra een klas iets opslaat, werkt deze lijst overal automatisch mee bij.

## Belangrijk als je een eerdere versie al had ingesteld

Dit bestand is volledig herschreven. Als je op je live site al een eigen `FIREBASE_CONFIG` en
`ADMIN_PASSWORD` had ingevuld, moet je die **opnieuw** plakken in dit nieuwe bestand vóór je het
opnieuw naar GitHub uploadt (zoek ze op in je Firebase-projectconsole, of open je oude,
al-geüploade `index.html` in GitHub om ze over te kopiëren). De opslagstructuur in Firestore
("scores"-verzameling) blijft dezelfde; er is geen nieuwe Firebase-installatie nodig.

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
