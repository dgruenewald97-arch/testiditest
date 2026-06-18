# PROJECT.md — Mitsubishi „WOW" Kampagnen-Modul

> **Single Source of Truth.** Hält Brief, Assets, Entscheidungen und den
> Step-Plan fest, damit der Kontext über Sessions/Resets hinweg nicht verloren
> geht. Bei jedem Schritt hier aktualisieren.

---

## 1. Brief (fix)
- **Was:** Kampagnen-Landingpage „WOW" für Mitsubishi, als **fullwidth Modul**
  (später einbettbar, z. B. TYPO3).
- **Pitch:** morgen, **live im Browser**, Ziel = **Auftrag gewinnen** über
  **Wow & Innovation**. Publikum: gemischte Entscheider-Runde.
- **Tonalität:** laut & verspielt (Pink/Magenta, fettes „WoW").
- **Haupt-CTA:** „Angebot anfragen".
- **Pflicht-Argumente (müssen sichtbar sein):** 189 €/ohne Anzahlung ·
  Gratis Wallbox 599 € · bis 4.500 €/6.000 € Förderung · 8 Jahre Garantie ·
  L200 „Coming Soon" · gültig bis 31.12.2026.

## 2. Vorgehen (WICHTIG)
**Phase 1 — Statik („PowerPoint nachbauen"):** Flyer-Design 1:1 als sauberes,
statisches HTML aufbauen (echte Schrift + Fahrzeuge), Seite für Seite,
**ohne Animation**. Erst abnehmen, dann weiter.
**Phase 2 — Snappy Animation:** Auf das fertige statische Layout die
scroll-/intro-Animationen legen (WoW-Zoom/Puls, Parallax, Reveals).

→ Grund: Animieren geht nur auf echten HTML-Bausteinen. Deshalb Statik zuerst.

## 3. Assets (liegen im Repo)
- **Fahrzeuge (freigestellt, PNG):** `assets/cars/` → `outlander.png`, `asx.png`,
  `grandis.png`, `eclipse-cross.png`, `l200.png` (Outlander Black: kein eigenes Foto).
- **Flyer-Seiten (Screenshots):** `assets/offers/` (Referenz fürs 1:1-Nachbauen).
- **Marken-Schrift:** `assets/fonts/` → MMC Regular/Bold (eingebunden via @font-face).
- **Logo:** `assets/logo-mitsubishi-black.svg` (+ rote Variante).
- **WoW-Grafik:** `assets/header/wow.png` ✅ saubere, transparente PNG (vom User).

## 4. Entscheidungen
- Statik zuerst, dann Animation (s. o.).
- Marken-Schrift **MMC** für Texte/Headlines.
- Dependency-frei (kein CDN/Framework) → läuft live garantiert, auch offline.
- Deploy: GitHub Pages via `.github/workflows/deploy-pages.yml` (aktiv).

## 5. Flow (bestätigt)
- **Hero = NUR das WoW-Bild** (fullwidth). Beim Öffnen Puls/Zoom.
- Beim Scrollen wird WoW **größer + fadet aus**; wenn weg → **sanfter
  Fullwidth-Übergang** zur 1. Angebotskarte → dann nächste, usw.
- Jede Angebotskarte: Modellname, „Jetzt ab XX €" (Text + **lebende Zahl**),
  Highlights, Preisbox, CTA „… Angebot anfordern" (→ modellspez. Formular),
  Fahrzeug, Rechtszeile.

## 6. Step-Plan
**Phase 1 (Statik):**
- [x] Step A — Hero: nur WoW (fullwidth) — steht inkl. Animation (s. Phase 2)
- [x] Step B — 1. Angebotskarte als **Template** (Outlander) — abgenommen
- [x] Step C — restliche Modelle als Klone (ASX, Grandis, Eclipse Cross, Outlander Black, L200)
      → 6 Karten total, Zickzack (jede 2. `is-flip`), L200 = Coming Soon (kein Preis, „vormerken").
      Preise/Werte = Platzhalter (Flyer zeigt XXX). Black & L200-Fotos = Platzhalter.
- [x] Step D — Abschluss/CTA + Argumente + Footer/Legal

**Phase 2 (Animation):**
- [x] WoW: Puls/Zoom beim Öffnen + Wachsen & Ausfaden beim Scrollen
      (gepinnt via sticky, lang/cinematisch 240vh, Climax ~4× + Fade bis 96 %;
      Slogan „Jetzt wird's groß." + Scroll-Hint „Runterscrollen & staunen ↓")
- [x] Sanfte Fullwidth-Übergänge zwischen den Slides (mittels IntersectionObserver)
- [x] Preis: hochzählen, dann nach rechts „swipen" zum Kaufpreis (Glanz-Effekt)
- [x] Blickführungs-Linie („Straße"), die mit dem Scrollen wächst (animierter SVG-Pfad)
- [x] Feinschliff Timing/Easing (IntersectionObserver + Snap Proximity)

## 7. Status-Log
- 2026-06-18: Reset, PROJECT.md, MMC-Font, echte Assets, echte WoW-PNG.
- 2026-06-18: Flow bestätigt (Hero nur WoW; „Jetzt ab" als Text+lebende Zahl).
  Start Phase 1 Statik (Hero + Template-Angebotskarte Outlander).
- 2026-06-18: Hero-Animation fertig & abgenommen. Bugs gefixt: `overflow-x:hidden`
  (brach sticky → WoW scrollte weg, jetzt `clip`) + Intro-`fill-mode:both` überschrieb
  den Scroll-Zoom (jetzt beim ersten Scroll abgeschaltet). Slogan + Scroll-Hint ergänzt.
- 2026-06-18: Angebotskarten-Template (Outlander) steht. Entscheidung UX: **eine Karte
  = genau EIN Viewport** (100vh, Schriftgrößen an vh gekoppelt) + **Scroll-Snap**
  (`proximity`) für süchtig-machenden Rhythmus. Aufbau: 2 Spalten — Infos links
  (Kicker, Preis 1:1 weiß+Schatten, Highlights, Preisbox mit Farbrahmen, CTA, Legal),
  Auto als Held rechts, Wallbox schwebt oben (Platzhalter-SVG: assets/placeholders/wallbox.svg).
  Klon-System: `.offer.is-flip` spiegelt, `--accent-a/b/c` pro Karte. 2. Karte
  (Outlander Black, violetter Accent, gespiegelt) als Klon-Test angelegt.
  OFFEN/Platzhalter: Black hat kein eigenes Foto (nutzt Outlander-PNG), Preis 219 € = Platzhalter
  (Flyer zeigt XXX). Noch fehlend: 8-Jahre-Siegel, „Litho Diamant"-Kennzeichen.
  Nächste Modelle: ASX, Grandis, Eclipse Cross, L200 (Coming Soon).
- 2026-06-18: UX-Feedback umgesetzt: (1) Scroll-Leiste = durchgehender Gesamt-Fortschritt
  (Hero+Karten), immer sichtbar (Führung).
- 2026-06-18: Scrolling NEU gedacht. Wheel-Hijack RAUS (fühlte sich auf Laptop/Trackpad
  schlecht an, kämpfte gegen natives Scrollen). Jetzt rein NATIV: `scroll-snap-type:y proximity`
  + `.offer{scroll-snap-align:start}`. Hero hat KEIN snap-align → frei für Zoom-Scrub.
  `mandatory` bewusst NICHT (würde Hero brechen). → fühlt sich smooth/nativ an wie der Hero.
- 2026-06-18: Layout-Regel FINAL (mit User festgelegt): **Zickzack NUR auf Desktop**.
  Standard-Karte = Info links / Auto rechts. `.is-flip`-Karte = Auto LINKS / Info rechts,
  Info bleibt links-bündig IN ihrer (rechten) Spalte (`align-items:flex-start`, kein Rechtsbündig).
  Flip-CSS liegt in `@media (min-width:821px)` → auf **Mobile kein Flip** (alle Karten gestapelt:
  Auto oben / Info unten). Klon-Regel: jede 2. Karte bekommt `.is-flip` für den Zickzack;
  sonst nur `--accent` + Inhalt tauschen. Karte 2 (Outlander Black) = `.is-flip`.
  Verifiziert: Desktop K1 Auto-rechts / K2 Auto-links; Mobile beide Auto-oben.

## 6a. SESSION-ÜBERGABE (Stand für die nächste KI-Session)
**Wo wir stehen (2026-06-18):**
- Komplette Single-Page in `index.html` (dependency-frei). Hero (WoW-Zoom, gepinnt) + **6
  Angebotskarten** im Zickzack: Outlander Diamant, Outlander Black, ASX, Grandis, Eclipse Cross,
  L200 (Coming Soon). Jede Karte = 1 Viewport, natives `scroll-snap proximity`, Fortschrittsleiste.
- **Klon-Regel:** neue Karte = `<section class="offer [is-flip]" style="--accent-a/b/c:…">` +
  Inhalt tauschen. Jede 2. Karte `is-flip` (Zickzack, nur Desktop). Wallbox-Platzhalter:
  `assets/placeholders/wallbox.svg`. Eindeutige `textPath`-ID pro Karte (`wbArc-<modell>`).

**OFFEN / Platzhalter (wichtig für nächste Session):**
- Alle **Preise/Leasingraten + Preisbox-Werte = Platzhalter** (Flyer zeigt „XXX") → echte Zahlen einsetzen.
- **Outlander-Black-Foto** = nutzt Outlander-PNG; **L200** nutzt l200.png ohne finale Aufbereitung.
- **Wallbox-Grafik** = Platzhalter-SVG; **8-Jahre-Garantie-Siegel** & **„Litho Diamant"-Kennzeichen** fehlen noch.

**Nächste sinnvolle Schritte:**
1. **Step D** — Abschluss-/CTA-Sektion + Pflicht-Argumente (Wallbox 599 €, bis 4.500/6.000 € Förderung,
   8 J. Garantie, gültig bis 31.12.2026) + Footer/Legal.
2. **Phase 2 Karten-Animationen** — Reveal beim Scrollen (Auto fährt rein, Preis zählt hoch & „swipet"
   zum Kaufpreis), Blickführungs-„Straße". Bringt den „Sog".
3. Echte Assets/Preise einpflegen, sobald vorhanden.

## 6. Status-Log
- 2026-06-18: Reset auf sauberen Start. Assets + MMC-Font + Deploy bleiben.
  Beginn Phase 1, Step 1 (statische Cover-Seite).
- 2026-06-18: Step C fertig (6 Karten, Zickzack). Session gesichert & auf `main` (testiditest) gepusht.
- 2026-06-18: Finalisierung des Moduls. Grid auf grid-template-areas umgebaut. Farbverlauf nach Blau am Seitenende integriert. „Litho Diamant" Kennzeichen als absolute CSS-Overlays und „8 Jahre Garantie" Siegel über die Fahrzeuge gelegt. Wallbox SVG-Bereinigung durchgeführt. Interaktivität und Phase 2 implementiert: IntersectionObserver für reveals, JS-Preis-Counter, Pricebox-Shine-Effekt und wachsende SVG-„Straße" (Road-Line). Step D Abschluss-Sektion mit Kontaktformular und Legal Footer eingebaut.
- 2026-06-18: Bereinigung nach Kunden-Feedback: Pinke Kennzeichen-Overlays und animierte SVG-Straße gelöscht. Anfrage-Formular entfernt und durch zentriertes Campaign-Summary (Bullets) und großen externen CTA-Button ersetzt. Alle CTAs auf externe Mitsubishi-Produktseiten verlinkt.
- 2026-06-18: Visuelle Stabilisierung & WOW Matchmaker Quiz: Scroll-Snapping komplett deaktiviert für natürliche, flüssige Navigation. Reveal-Animationen beruhigt (Verschiebung verringert, `backdrop-filter` Ruckeln behoben). Den interaktiven Showroom am Seitenende durch einen 3-stufigen, spielerischen „WOW Matchmaker" Quiz-Konfigurator ersetzt, der das passende Modell und Leasingangebot basierend auf Nutzerbedürfnissen ermittelt.


## 7. Betrieb
- **Live:** https://dgruenewald97-arch.github.io/testiditest/ (Hard-Reload nach Push)
- **Lokal:** `index.html` im Browser öffnen.
- **Branch:** `claude/awesome-cannon-gy2g5u` → Push auf `main` deployt automatisch.
