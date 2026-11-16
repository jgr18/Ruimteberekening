# Ruimtebehoefte per faciliteittype en opleiding

Webapp die de ruimtebehoefte van de academie berekent uit Xedule-exports:
per locatie, faciliteittype en periode, voor alle opleidingen samen of voor een combinatie van opleidingen.

**Privacy:** de app draait volledig in de browser. Geïmporteerde Excel-bestanden worden niet geüpload en
niet op een server opgeslagen. In deze repository staan geen roostergegevens.

## Gebruik

1. **Importeren** – sleep de vier Excel-bestanden in de app:
   - Onderwijsregels (export uit Xedule)
   - Onderwijsprogramma's en opleiding (kolommen *Code*, *Team*)
   - Faciliteittypesets (kolommen *Faciliteittypeset*, *Faciliteittype*, *Locatie*, *Meenemen*)
   - Kalenderweken (kolommen *Week*, *lesweek*, *periode*, *Semester*)
2. **Controle** – bekijk wat niet klopt of niet meetelt.
3. **Instellingen** – algemeen (beschikbare uren per lokaal, streefbezetting), weekindeling en koppeling van
   faciliteittypesets aan faciliteittype en locatie.
4. **Analyse** – kies een periode en een selectie van opleidingen.

## Rekenregel

- Blokken (RE/minuten): waarden t/m 17 zijn RE (lesuren); hoger zijn minuten (toetsen) en worden gedeeld door 45.
  Waarden als `3/3` of `12/12/12/12/11` worden opgeteld.
- Lokaaluren per week = RE × aantal lokalen per faciliteittypeset, in elke week waarin het onderwijs gepland is.
- Benodigde lokalen per week = lokaaluren ÷ beschikbare uren per lokaal (standaard 56).
- Per groep weken (semester 1/2, les-/toetsweken) wordt de mediaan genomen.
- Toegewezen = mediaan × (100% ÷ streefbezetting). Bij 80% is dat × 1,25.
- Faciliteittype *Specifiek* en sets die *buiten beschouwing* staan tellen niet mee.

## Gedeelde instellingen

Instellingen worden per browser bewaard. Via *Instellingen → Instellingen delen* exporteer je ze naar
`instellingen.json`. Zet je dat bestand naast `index.html` in deze repository, dan krijgt iedereen die de app
voor het eerst opent deze instellingen als standaard.
