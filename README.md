# Ruimtebehoefte per faciliteittype en opleiding

Versie 0.8 (concept)

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
2. **Controle** – controleert de invoer op fouten (faciliteit niet conform richtlijn, onbekend faciliteittype,
   RE niet berekend, geen geldige uitvoerweek, programma zonder opleiding, weken buiten de kalender) en
   waarschuwingen (geen faciliteittype, week ingevuld buiten periode), met per melding het onderwijsproduct
   en onderwijsprogramma.
3. **Instellingen** – algemeen (beschikbare uren per lokaal, streefbezetting), weekindeling, koppeling van
   faciliteittypesets aan faciliteittype en locatie, en koppeling van onderwijsprogramma's aan opleidingen.
4. **Analyse** – kies een periode en een selectie van opleidingen, en sorteer de grafieken op weeknummer of grootte.

## Exporteren

- Vul eerst bij *Instellingen → Rapportgegevens* de naam van de academie, het jaar, de geanalyseerde periode en de datum
  van de importbestanden in. Deze komen samen met de datum van de analyse bovenaan elke export.
- **Excel**: één bestand met de tabbladen *Gegevens*, *Toewijzing*, een tabblad met grafieken per periode
  (S1 lesweken, S1 toetsweken, S2 lesweken, S2 toetsweken, studiejaar), *Per opleiding* en *Per week*.
- **PDF**: via het afdrukvenster van de browser; kies daar *Opslaan als PDF*. Dat kan voor de gekozen periode of voor
  alle vier de periodes.

## Rekenregel

- Blokken (RE/minuten): waarden t/m 17 zijn RE (lesuren); hoger zijn minuten (toetsen) en worden gedeeld door 45.
  Waarden als `3/3` of `12/12/12/12/11` worden opgeteld.
- Lokaaluren per week = RE × aantal lokalen per faciliteittypeset, in elke week waarin het onderwijs gepland is.
- Benodigde lokalen per week = lokaaluren ÷ beschikbare uren per lokaal (standaard 56), afgerond op 1 decimaal.
- Per groep weken (semester 1/2, les-/toetsweken) wordt de mediaan genomen (niet tussentijds afgerond).
- Toe te wijzen = mediaan × (100% ÷ streefbezetting), bij 80% is dat × 1,25, naar boven afgerond op 0,1 lokaal (= 1 dagdeel).
- Faciliteittype *Specifiek* en sets die *buiten beschouwing* staan tellen niet mee.

## Gedeelde instellingen

Instellingen worden per browser bewaard. Via *Instellingen → Instellingen delen* exporteer je ze naar
`instellingen.json`. Zet je dat bestand naast `index.html` in deze repository, dan krijgt iedereen die de app
voor het eerst opent deze instellingen als standaard.
