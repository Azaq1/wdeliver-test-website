# WDeliver — website (5 pagina's, statisch HTML/CSS)

Conversiegerichte website voor WDeliver (transport & bezorging, Deventer) en de installatieservice W-Install.
Gebouwd als **statische, zelfstandige HTML-bestanden** met gewone CSS in een `<style>`-blok per pagina — geen frameworks, geen build-stap — zodat elke pagina los in **YOOforged** geplakt en naar YOOtheme Pro geconverteerd kan worden.

## Structuur

```
/wdeliver-site
  index.html        Home
  wdeliver.html     WDeliver (transport & bezorging)
  w-install.html    W-Install (installatieservice)
  werken-bij.html   Werken bij (vacature installateurs)
  contact.html      Neem contact op (offerteformulier)
  /media            Alle gebruikte beelden
  README.md
```

## Huisstijl (dark theme)

De site gebruikt een **donker thema**: near-black achtergrond, witte tekst, rood als accent.

- **Primair rood: `#DD0419`** — geëxtraheerd uit het aangeleverde logobestand (`imgi_3_Wdeliver-LOGO.jpg`); dit is de meest voorkomende verzadigde kernkleur van het logo. Gemiddelde over alle rode pixels (incl. anti-aliasing): `#CE0E23`. Bij twijfel: check het vectorbestand van de klant en corrigeer `--red` bovenaan elk bestand.
- Donker rood (hover): `#B00313`. Helder rood voor tekst/links op donker: `#FF4D5E` / `#FF3B4E` (beter leesbaar dan #DD0419 op zwart).
- Achtergrond: `#0F1115` (body), `#161920` (kaarten/panelen, `--bg-raise`), footer `#0B0D10`, partner-strip `#030407`.
- Tekst: `#F2F4F7` (--ink), gedempt `#9AA3B0` (--muted). Randen: `rgba(255,255,255,0.09)`.
- **Achtergrondpatroon** (alle pagina's, via `body::before`): subtiele diagonale "speed lines" (115°, verwijzing naar de logo-swoosh) + dunne rode lijnen + twee zachte rode radial-gloeden. De laag is een vaste (`position: fixed`), iets oversized (`inset: -8%`) vlak dat als geheel heel langzaam meedrijft via `transform: translate3d(...)` (`bgDrift`, 80s) — bewust géén `background-position`/tegels, want dat gaf een zichtbare bewegende rechthoek-rand. `background-repeat: no-repeat` op de gloeden; de line-gradients vullen zelf naadloos. Uitgeschakeld bij `prefers-reduced-motion`.
- Het WDeliver-logo (JPG) staat in header en footer op een witte afgeronde chip, omdat het logo zelf een dichte witte achtergrond heeft.
- **Openstaand punt:** er is een poging gedaan om de door de klant aangeleverde "no background"-bestanden (map `logo's website wdeliver` op het Bureaublad) te gebruiken, maar die bleken zelf nog een dichte witte achtergrond te bevatten (geen echte transparantie) — teruggedraaid naar de originele JPG/PNG + witte chip. Zodra de klant écht vrijgestelde (transparante) logo-bestanden aanlevert, kunnen `media/logo-wdeliver.jpg` en `media/logo-wdeliver-w-install.png` 1-op-1 vervangen worden en kan de witte chip in de CSS (`.brand`, `.footer-logo`) verwijderd worden.
- Typografie: **Inter** via Google Fonts.

## Media per pagina

Bronbestanden kwamen uit `Wdeliver-media` (duplicaten in kleinere formaten zijn overgeslagen; steeds de grootste versie gebruikt en hernoemd):

| Bestand in /media | Origineel | Gebruikt op |
|---|---|---|
| `logo-wdeliver.jpg` | imgi_3_Wdeliver-LOGO.jpg | Header van alle 5 pagina's (op witte chip) |
| `logo-wdeliver-w-install.png` | imgi_1_Logos-WDeliver-W-install-2 | Footer van alle 5 pagina's (op witte chip) |
| `logo-w-install.jpg` | imgi_4_W-install-LOGO.jpg | *(reserve — nu niet gebruikt; W-Install draait onder het WDeliver-merk)* |
| `logo-wdeliver-wit.png` / `logo-combo-wit.png` / `logo-w-install-wit.png` | "no background"-bestanden van de klant | *(ongebruikt — bleken geen echte transparantie te bevatten; wachten op nieuwe aanlevering)* |
| `team-wagenpark.jpg` | imgi_2_WDeliver-13.jpg | Home (hero-collage + dienstkaart), WDeliver (team-sectie) |
| `pand-deventer.jpg` | imgi_5_WDeliver-0.jpg | Home (intro), WDeliver (historie), W-Install (team), Contact (locatie/kaart-placeholder) |
| `bezorging-witgoed.jpg` | imgi_21_WDeliver-15.jpg | Home (hero-collage + dienstkaart), WDeliver (hero) |
| `installatie-witgoed.jpg` | imgi_22_WDeliver-17.jpg | Home (dienstkaart), W-Install (hero), Werken bij (functie) |
| `chauffeurs-onderweg.jpg` | imgi_23_WDeliver-7.jpg | Home (parallax-fotoband), WDeliver (personeel), Werken bij (hero) |
| `partner-sluyter.png` | imgi_19 (980×255-versie) | Home (partners) |
| `partner-naduvi.jpg` | imgi_8_ce-channel-naduvi.jpg | Home (partners) |
| `partner-mailstreet.png` | imgi_6_logo-mailstreet.png | Home (partners) |
| `partner-first-logistics.jpg` | imgi_7_first-logistics-logo.jpg | Home (partners) |
| `partner-wuunder.png` | imgi_10_wuunder-logo.png | Home (partners) |

**Placeholders:** er is geen echte kaart-embed op de contactpagina; daar staat nu `pand-deventer.jpg` met een figcaption dat de kaart in YOOtheme/WordPress gekoppeld wordt. De link "Algemene Voorwaarden" in de footer is een placeholder (`#`). Het contactformulier heeft bewust geen backend — verwerking koppel je later in YOOtheme/WordPress.

## YOOforged-conversietips per pagina

Plak per pagina de volledige HTML in YOOforged en gebruik onderstaande context-zin:

- **index.html** — *"Dit is de homepage van een Nederlands transport- en bezorgbedrijf: hero met fotocollage en dubbele CTA, partnerlogo-strip, intro met statistieken, 3 dienstkaarten, donkere fotoband met CTA, 6 USP-blokken en een rode CTA-band."*
- **wdeliver.html** — *"Dit is de dienstpagina over transport en bezorging van een Nederlands transportbedrijf: hero, historie met tijdlijn, 3 voertuigtypes, service-sectie met checklijst en team-sectie."*
- **w-install.html** — *"Dit is de dienstpagina van de installatieservice (W-Install) van een Nederlands transportbedrijf: hero, 3 installatiecategorieën, 3-staps werkwijze en team-sectie."*
- **werken-bij.html** — *"Dit is de vacaturepagina van een Nederlands transport- en installatiebedrijf: hero, functieomschrijving, twee lijstpanelen (eisen en taken) en een sollicitatieblok met e-mail-CTA."*
- **contact.html** — *"Dit is de contact-/offertepagina van een Nederlands transportbedrijf: contactformulier met dropdown, contactgegevens-zijbalk, locatiesectie met foto en een rode CTA-band."*

Algemeen: elke pagina heeft dezelfde sticky header (logo + navigatie + rode CTA-knop) en dezelfde donkere footer (contact, navigatie, bedrijfsgegevens, AVC 2002/CMR-regel). Secties zijn opgebouwd als standaard `<section>` + container + grid en mappen 1-op-1 naar YOOtheme-secties/rijen/kolommen.

### Animaties (let op bij conversie)

De site bevat lichte, progressief-degraderende dynamiek. Zonder JavaScript blijft alle content gewoon zichtbaar en bruikbaar:

- **Header** (alle 5 pagina's): een dunne rode "speed line" bovenaan (verwijzing naar de logo-swoosh), een subtiele gloed-rand + hover-lift op het logo-vlak, en scroll-gedrag — de header schuift weg bij scrollen omlaag en komt direct terug zodra je omhoog scrollt (`.header-hide` / `.header-scrolled`, JS onderaan elke pagina). Zonder JS blijft de header gewoon altijd zichtbaar (sticky). In YOOtheme: de sticky-header heeft vaak een ingebouwde "hide on scroll down"-optie; anders met een klein custom-JS-blok reproduceren.
- **Hero**: CSS-entrance-animaties (fadeUp/fadeScale), fotocollage (hoofdfoto + overlappende subfoto) en een zwevende rode badge ("2010"). In YOOtheme na te bouwen met een afbeelding + overlay-element, of vervang de collage door één afbeelding.
- **Mobiele hero-volgorde** (via CSS `grid-template-areas`, omslag < 920px): op desktop staat de tekst links (titel → subtekst → knoppen) met de fotocollage rechts; op mobiel wordt de volgorde **titel → foto's → subtekst → knoppen**, met de partner-strip er direct onder. In YOOtheme reproduceer je dit door de kolomvolgorde per breakpoint te zetten (of losse rijen met "Order"-instelling).
- **Kortere koppen op mobiel**: enkele koppen hebben twee varianten in één element — `<span class="t-long">` (desktop) en `<span class="t-short">` (mobiel), waarbij CSS er per breakpoint één toont. Betreft de hero-H1, de dienstenkop, de "Waarom WDeliver"-kop, de fotoband-kop en de CTA-kop. In YOOtheme kun je één kop aanhouden, of de responsive zichtbaarheid per element gebruiken.
- **Partners-strip** (direct onder de hero): CSS-only oneindige logo-marquee op een near-black band. Er staan **4 identieke `.marquee-set`-blokken** in de track (3 zijn `aria-hidden` duplicaten) zodat de loop naadloos doorloopt zonder gat — bij conversie in YOOtheme vervangen door het **Slider/Grid-element met autoplay**, en de duplicaten weggooien. De logo's krijgen `filter: invert(1) grayscale(1)` zodat donkere logo's en witte JPG-achtergronden netjes licht worden op de donkere band; in YOOtheme kun je in plaats daarvan witte/lichte logovarianten van de klant gebruiken.
- **Scroll-reveal**: elementen met class `.reveal` faden in via een klein IntersectionObserver-script onderaan de pagina. In YOOtheme vervang je dit door de ingebouwde **Animation/Parallax-opties per element** (bv. "Fade + Slide Bottom").
- **Tellers**: `[data-count]`-spans in de statistieken tellen op bij inscrollen (JS). YOOtheme Pro heeft hiervoor het **Countdown/Counter-element**, of laat statisch.
- **Fotoband**: sectie met `background-attachment: fixed` (parallax-gevoel) en donkere overlay. In YOOtheme: sectie-achtergrondafbeelding met "Fixed/Parallax" + overlay.
- `prefers-reduced-motion` schakelt alle beweging uit.
