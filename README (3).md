# 🎓 Meesterproef Studio

Een hulpmiddel voor docenten en onderwijsdirecteuren om een gekwalificeerd eindwerk
("meesterproef") te ontwerpen — passend bij het NLQF-niveau van de opleiding (bachelor of
master), en voorbereid op het gesprek met de vice-decaan onderwijs (OER) en de
examencommissie.

Onderdeel van de [AI App Store](https://aigovernanceofficer.github.io/AI-app-store/) van
AIGovernanceofficer.nl.

---

## Wat doet de app?

De app bestaat uit drie onderdelen:

1. **Kader** — uitleg over wat een eindwerk wettelijk moet borgen (WHW), de rolverdeling
   tussen vice-decaan onderwijs, examencommissie en docent, en het verschil tussen
   NLQF-niveau 6 (bachelor) en niveau 7 (master).
2. **Vormenbibliotheek** — een overzicht van zeven mogelijke vormen van een eindwerk
   (scriptie, scriptie met verdediging, portfolio, ontwerpend onderzoek/beroepsproduct,
   praktijkgericht projectwerk, adviesrapport, expositie/presentatie), elk met sterke
   punten, risico's en aandachtspunten.
3. **Ontwerphulp** — een wizard van vijf vragen die op basis van het opleidingsniveau,
   de aard van de opleiding en een aantal randvoorwaarden 1-2 passende vormen aanbeveelt,
   inclusief een NLQF-checklist en vervolgstappen richting de OER en de examencommissie.
   Het resultaat kan worden geëxporteerd als Word-document in UU-huisstijl.

---

## Voor wie

Docenten, opleidingscoördinatoren en onderwijsdirecteuren die overwegen om de vorm van het
eindwerk binnen hun opleiding te herzien of te vernieuwen, en die dit goed willen
voorbereiden voordat ze het gesprek aangaan met de vice-decaan onderwijs en/of de
examencommissie.

---

## Hoe is de app ontwikkeld? — logica en algoritmes

De app bevat **geen AI, geen taalmodel en geen externe modelaanroepen**. Alle inhoud en
logica zijn **rule-based** (op vaste regels gebaseerd) en volledig inzichtelijk in de
broncode (`meesterproef-studio.html`):

- **Inhoud (Kader en Vormenbibliotheek)**: vast geschreven teksten, gebaseerd op de
  wettelijke kaders en kwalificatieraamwerken die hieronder bij "Bronnen" staan
  beschreven. Deze teksten zijn door de auteur opgesteld en gecontroleerd aan de hand van
  de genoemde bronnen — niet door een taalmodel gegenereerd tijdens gebruik.
- **Ontwerphulp (wizard)**: een eenvoudig **scoringsalgoritme**. Elke vorm van eindwerk in
  de `VORMEN`-lijst heeft vaste kenmerken (geschikt niveau, aard van de opleiding,
  organisatievorm, wel/geen externe partij, wel/geen verdediging). Op basis van de
  antwoorden van de gebruiker wordt per vorm een score berekend:
  - vormen die niet passen bij het gekozen NLQF-niveau (bachelor/master) worden
    uitgesloten;
  - een match op de aard van de opleiding levert de meeste punten op;
  - matches op organisatievorm, externe partij en verdediging leveren elk een extra punt
    op.

  De twee vormen met de hoogste score worden getoond, samen met de bijbehorende
  NLQF-checklist en aandachtspunten. Er wordt **niets verzonden naar een server** om dit
  te berekenen — alles gebeurt in de browser van de gebruiker.
- **Word-export**: het resultaat van de wizard wordt in de browser omgezet naar een
  `.docx`-bestand met de open source bibliotheek [`docx`](https://docx.js.org/)
  (client-side, via een CDN-script), opgemaakt in UU-huisstijl.

> Kortom: de app *informeert en structureert*, maar **neemt geen besluit**. De uiteindelijke
> keuze voor een vorm van eindwerk en de formele vaststelling daarvan verlopen via de OER
> (vice-decaan onderwijs) en het toezicht van de examencommissie — zie "Kader" in de app.

---

## Veiligheid en privacy (AVG)

- **Geen gegevensverzameling**: de app slaat niets op en stuurt niets naar een server. Alle
  invoer (antwoorden in de wizard) blijft in het geheugen van de browser en verdwijnt zodra
  de pagina wordt gesloten of vernieuwd.
- **Geen account, geen login, geen tracking.**
- **Geen AI/LLM**: er wordt geen tekst naar Anthropic, OpenAI of een andere AI-aanbieder
  gestuurd. Er is dus ook geen API-key nodig.
- **Eén externe afhankelijkheid**: voor de Word-export wordt bij gebruik eenmalig de
  JavaScript-bibliotheek `docx` geladen via een CDN (unpkg.com). Dit gebeurt alleen lokaal
  in de browser van de gebruiker en bevat geen persoonsgegevens. Bij gebruik zonder
  internetverbinding werkt de export-knop niet, maar de rest van de app (Kader,
  Vormenbibliotheek, wizard) blijft functioneren.
- **Gegenereerd Word-document**: dit bestand wordt rechtstreeks naar de eigen computer van
  de gebruiker gedownload (geen cloudopslag) en bevat alleen de antwoorden die de gebruiker
  zelf heeft ingevoerd (opleidingsniveau, aard van de opleiding, organisatievorm, etc.) —
  geen namen, studentgegevens of andere persoonsgegevens.

**Disclaimer**: deze app is een ontwerphulp en informatiebron. Zij vervangt geen wettelijke
procedure, geen besluit van het faculteitsbestuur/vice-decaan onderwijs over de OER, en geen
toezicht of advies van de examencommissie.

---

## Bronnen

De inhoud van de app is gebaseerd op de volgende bronnen:

**Wet- en regelgeving (WHW)**
- [Wet op het hoger onderwijs en wetenschappelijk onderzoek (WHW)](https://wetten.overheid.nl/BWBR0005682)
  *(oorspronkelijke wet: 1992; geraadpleegde, geldende tekst: 2026)*
  - Art. 7.13 — Onderwijs- en examenregeling (OER): vaststelling van eindkwalificaties en de
    vorm van het eindwerk, verantwoordelijkheid van het faculteitsbestuur (bij UU gemandateerd
    aan de vice-decaan onderwijs).
  - Art. 7.12 — Examencommissie: objectieve en deskundige vaststelling of een student aan de
    OER-eisen voldoet.
  - Art. 7.12b — Taken en bevoegdheden examencommissie: kwaliteitsborging van tentamens/examens
    en richtlijnen binnen het kader van de OER.
  - Art. 7.12c — Examinatoren.

**Kwalificatieraamwerken**
- [Nederlands kwalificatieraamwerk (NLQF) — Rijksoverheid](https://www.rijksoverheid.nl/themas/onderwijs/leven-lang-ontwikkelen/nederlands-kwalificatieraamwerk-nlqf)
  *(NLQF ontwikkeld: 2012; pagina geraadpleegd: 2026)*
- [NLQF-niveaubeschrijvingen per descriptor](https://nlqf.nl/hoe-kom-je-tot-ingeschaalde-opleiding/niveaubeschrijvingen-nlqf-descriptoren/)
  *(2025)*
- [NLQF/EQF-niveau 6](https://nlqf.nl/nlqf-niveaus-waaier/nlqf-eqf-niveau-6/) en
  [NLQF/EQF-niveau 7](https://nlqf.nl/nlqf-niveaus-waaier/nlqf-eqf-niveau-7/) *(2026)*
- [NLQF-niveauwaaier (alle 8 niveaus)](https://nlqf.nl/impact-nlqf/nlqf-niveaus-waaier/) *(2025)*
- [Wet NLQF (36.341) — Eerste Kamer](https://www.eerstekamer.nl/wetsvoorstel/36341_wet_nlqf)
  *(aangenomen: 25 juni 2024)* — geeft het NLQF een wettelijke grondslag, regelt verplichte
  vermelding van NLQF-/EQF-niveau op diploma's, en maakt het NCP NLQF een zelfstandig
  bestuursorgaan.
- [Niveau van Nederlandse diploma's — Nuffic](https://www.nuffic.nl/en/education-systems/the-netherlands/level-of-dutch-diplomas)
  *(jaartal niet vermeld op de bron; doorlopend bijgewerkte informatiepagina)* —
  koppeling van bachelor/master/promotietraject aan NLQF/EQF-niveau 6/7/8.

**Achtergrond over vormen van het eindwerk**
- [Een bachelorprogramma zonder scriptie, kan dat? — DUB (Universiteit Utrecht)](https://dub.uu.nl/nl/achtergrond/een-bachelorprogramma-zonder-scriptie-kan-dat)
  *(2026)* — discussie binnen UU (faculteit Geesteswetenschappen) over alternatieven voor de
  bachelorscriptie/meesterproef.
- Onderwijsinspectie, *Verder vooruit: Examencommissies in een veranderend hoger onderwijs*
  *(2025)*
- Hobéon, *Van onderzoeksscriptie naar beroepsproduct — trends in afstuderen*
  *(jaartal niet vermeld op de bron)*
- Advalvas (VU), *De scriptie is dood, leve de scriptie* *(2026)*
- Diverse hbo-bronnen over alternatieve afstudeervormen (portfolio, ontwerpend onderzoek)
  *(jaartallen variëren, circa 2020-2025)*

---

## Technisch

Eén self-contained HTML-bestand (`meesterproef-studio.html`) — geen installatie nodig, werkt
direct in de browser. Werkt offline, met uitzondering van de Word-exportknop (die eenmalig
een bibliotheek via CDN laadt).

---

## Feedback en doorontwikkeling

Deze app is een ontwerphulp en wordt mogelijk uitgebreid met meer vormen van eindwerk of
verfijning van de wizard-logica. Suggesties en correcties zijn welkom via
[aionderwijs@uu.nl](mailto:aionderwijs@uu.nl).

---

## Licentie

© 2026 [AIGovernanceofficer.nl](https://aigovernanceofficer.nl) ·
Licentie: [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.nl)
(Naamsvermelding – Niet-commercieel – Geen afgeleide werken), conform de overige apps in de
[AI App Store](https://aigovernanceofficer.github.io/AI-app-store/).

