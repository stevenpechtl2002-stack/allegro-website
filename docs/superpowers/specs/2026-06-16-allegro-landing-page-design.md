# Allegro Landing Page — Design Spec
**Datum:** 2026-06-16

## Restaurant
- **Name:** Allegro Pizzeria & Restaurant
- **Inhaber:** Artur Grießhaber
- **Adresse:** Stuttgarter Straße 55, 75179 Pforzheim
- **Telefon:** 07231 – 10 16 29
- **E-Mail:** info@allegro-pf.de
- **Website:** https://allegro-pf.de

## Ziele
1. Neue Gäste gewinnen (starker visueller erster Eindruck)
2. Mittagstisch für Stammkunden prominent platzieren

## Design-Richtung: Rustico Italiano
- **Farbpalette:** Dunkelbraun (#2C1A0E, #0F0805), Gold (#D4A853), Creme (#F5DEB3), Mittelbrown (#C8A97A, #8B6642)
- **Typografie:** Serif für Headlines/Branding (Georgia / Playfair Display via Google Fonts), Sans-serif für Fließtext
- **Stil:** Warm, authentisch italienisch, Trattoria-Atmosphäre, dezente Gold-Akzente
- **Bilder:** Unsplash Stock-Fotos (Pizza, Pasta, Restaurant-Ambiente) — austauschbar

## Projekt-Struktur (GitHub + Vercel)
```
allegro-website/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── .gitignore
└── vercel.json
```
Vercel erkennt statische Sites automatisch. Kein Build-Schritt nötig.

## Sektionen (in Reihenfolge)

### 1. Navigation (sticky)
- Logo "Allegro" in Serif/Italic, links
- Links: Mittagstisch · Karte · Über uns · Galerie · Kontakt
- Auf Mobile: Hamburger-Menü
- Hintergrund: transparent → dunkelbraun beim Scrollen (JS)

### 2. Hero
- Vollbild-Hintergrundbild: hochwertiges Pizza/Restaurant-Foto von Unsplash
- Dark overlay (70% Dunkelheit)
- Animierter Slogan: "Cucina Autentica" (fade-in von unten)
- Subtext: "Handgemachte Pizza & Pasta · Pforzheim"
- Zwei CTAs: "Tisch reservieren" (tel: Link) + "Zum Mittagstisch" (Scroll-Anchor)
- Parallax-Scrolleffekt auf Hintergrundbild

### 3. Mittagstisch
- Titel: "Mittagstisch" mit goldener Trennlinie
- Info-Bar: Öffnungszeiten (Mo–Fr 11:30–13:30 Uhr), Hinweis auf Feiertage
- Aktuelle Wochenkarte als elegante Liste (aus aktuellem Inhalt, austauschbar):
  - Kleiner gemischter Salat — 5,50€
  - Insalata Romana (Feta, Paprika, Oliven) — 10,50€
  - Penne (Schinken, Paprika, Sahnesauce) — 9,90€
  - Spaghetti (Mozzarella, Basilikum, Tomatensauce) — 9,90€
  - Pizza Prosciutto — 9,90€
  - Pizza Melanzane (Aubergine, Zucchini) — 9,90€
  - Fitness-Teller (Hähnchenbrust, Salat) — 13,50€
- Hinweis: +1,00€ bei Bestellung auf zwei Tellern
- E-Mail-Abo: Eingabefeld + "Jetzt anmelden" (mailto: Link)

### 4. Über uns
- Zweispaltig: Text links, Bild rechts (Unsplash: Koch/Restaurant-Atmosphäre)
- Headline: "Mit Leidenschaft in Pforzheim"
- Kurztext: Authentische italienische Küche, Inhaber Artur Grießhaber, frische Zutaten
- Gold-Zitat: "Bei uns kommt die Leidenschaft direkt auf den Teller."

### 5. Speisekarte Highlights
- 3 Karten: Pizza · Pasta · Salate
- Jede Karte: Icon/Emoji, Kategorie, 2 Beispielgerichte, Preis "ab X€"
- CTA: "Vollständige Karte anfragen" (tel: oder mailto:)

### 6. Galerie
- Masonry-Grid: 5–6 Bilder (Unsplash: food photography, restaurant interior)
- Hover-Effekt: leichter Gold-Overlay
- Lightbox: Klick öffnet Vollbild (reines CSS oder minimales JS)

### 7. Kontakt & Footer
- Zweispaltig: Kontaktdaten links, Google Maps iframe rechts
- Kontakt: Adresse, Telefon (klickbar), E-Mail (klickbar)
- Footer: Logo, Impressum-Link, Datenschutz-Link, Copyright

## Technische Details
- Vollständig responsiv (Mobile-first)
- Smooth Scroll für Anchor-Links
- Sticky Nav mit Scroll-Hintergrundwechsel (JS)
- CSS-Animationen: fade-in beim Einblenden der Sektionen (IntersectionObserver)
- Keine externen Frameworks (kein Bootstrap, kein React) — reines HTML/CSS/JS
- Google Fonts: Playfair Display (Serif) + Inter (Sans)
- Unsplash-Bilder direkt per URL eingebunden

## Vercel-Deployment
- `vercel.json` mit `"rewrites": [{"source": "/(.*)", "destination": "/index.html"}]`
- `.gitignore`: node_modules, .DS_Store, .vercel
- GitHub Repository: öffentlich, main-Branch → Vercel auto-deploy
