# Mitsubishi „WOW!" – Kampagnen-Landingpage
## Design- & Scrollytelling-Konzept (Stand: Juni 2026)

> Ziel: Weg vom Corporate-Standard. Eine LP als **Scroll-Erlebnis** mit
> lebendigem Regenbogen-Verlauf, der beim Scrollen mitswitcht, und
> Angebots-Karten, die „reinkrachen". Typo startet klein und springt
> explosiv auf groß. Endausspielung als **TYPO3-Module**.

---

## 1. Leitidee — „Scroll the WOW"

Die Beilage lebt vom Kontrast: knallige Magenta-/Pink-Verläufe, fette
Display-Typo, das „WOW!". Diese Energie übersetzen wir in **Bewegung**.
Der Nutzer scrollt nicht durch eine Seite — er fährt durch eine Farbreise,
bei der jedes Modell einen eigenen „Moment" bekommt.

Vier Prinzipien:

1. **Living Gradient** — ein durchgehender Verlauf im Hintergrund, dessen
   Farbe an die Scroll-Position gekoppelt ist (Regenbogen-Switch).
2. **Crash-In Cards** — Angebots-Karten erscheinen nicht, sie *knallen* rein
   (klein → groß mit Overshoot, leichter Rotation, „Impact"-Moment).
3. **Type that jumps** — Headlines starten winzig, beim Scroll-Trigger
   skalieren sie explosionsartig auf Vollbild („WOW!", „Jetzt ab 189 €").
4. **Geführter Scroll** — ein Zeitstrahl als ständiger Begleiter zeigt, wo
   man ist und was als Nächstes kommt. Orientierung trotz Erlebnis.

---

## 2. Der Regenbogen-Scroll (Herzstück)

**Was passiert:** Während gescrollt wird, wandert der Hintergrund-Verlauf
durch das Farbspektrum der Beilage:

```
Scroll 0%   →  Hero        Sunset/Orange → Magenta   (Titelseite)
Scroll 20%  →  ASX/Grandis Pink → Magenta            (S. 02/03)
Scroll 45%  →  Outlander   Magenta → Violett          (S. 04/05)
Scroll 70%  →  Eclipse/L200 Violett → Blau            (S. 06/07)
Scroll 100% →  CTA/Footer  Blau → tiefes Lila
```

**Technisch (3 Optionen, von robust → modern):**

- **A) GSAP ScrollTrigger** (Empfehlung): Hue/Stops des Gradients werden
  per `scrub` an den Scroll-Fortschritt gebunden. Butterweich, voll
  kontrollierbar, breite Browser-Unterstützung. Bewährt für Scrollytelling.
- **B) CSS Scroll-Driven Animations** (`animation-timeline: scroll()`):
  Kein JS nötig, sehr performant — aber Browser-Support 2026 noch nicht 100%.
  Als Progressive Enhancement nutzbar, mit JS-Fallback.
- **C) Hybrid:** CSS für den Gradient-Shift, GSAP nur für die Card-Impacts.

Umsetzung des Verlaufs: ein `conic`/`linear-gradient` auf einer fixed Layer,
gesteuert über CSS-Custom-Properties (`--hue-a`, `--hue-b`, `--angle`), die
JS/CSS beim Scrollen interpoliert. So bleibt der Effekt eine Zeile Logik
und ist später in TYPO3 leicht konfigurierbar (z. B. Start-/End-Farbe pro
Sektion im Backend setzbar).

**Performance & A11y:** Animation nur auf `transform`/`opacity`/CSS-Vars
(GPU-freundlich). `prefers-reduced-motion` respektieren → dann statischer
Verlauf, Karten faden sanft statt zu krachen.

---

## 2b. Zeitstrahl — Scroll-Orientierung (Down-Navigator)

Damit der Nutzer im langen Scroll-Erlebnis nie die Orientierung verliert,
gibt es einen **vertikalen Zeitstrahl** im Look der Kampagne — fix am
Bildschirmrand (Desktop rechts, Mobile als schlanke Leiste).

**Was er kann:**

- **Fortschritt:** Eine Linie füllt sich von oben nach unten passend zur
  Scroll-Position; der „Füllstand" greift die aktuelle Gradient-Farbe auf,
  läuft also im Regenbogen mit.
- **Stationen:** Ein Punkt pro Sektion (Hero, ASX, Grandis, Outlander …).
  Der aktive Punkt pulsiert/vergrößert sich.
- **„Was kommt als Nächstes":** Eine kleine **Pfeil-nach-unten**-Marke am
  unteren Ende mit Mini-Label der nächsten Sektion (z. B. „↓ Outlander
  189 €"). Im Hero zusätzlich ein animierter Bounce-Pfeil als
  Scroll-Einladung.
- **Sprung-Navigation:** Klick/Tap auf einen Punkt scrollt sanft zur Sektion
  (smooth scroll). So wird der Zeitstrahl auch zur Schnellnavigation.

**Technik:** Der Zeitstrahl baut sich **automatisch** aus den vorhandenen
Sektionen auf — er liest beim Laden alle Elemente mit `data-section` und
deren `data-label` aus und erzeugt die Punkte daraus. Dadurch muss in TYPO3
niemand den Zeitstrahl separat pflegen: Wer im Backend eine Angebots-Karte
hinzufügt/entfernt, ändert automatisch auch den Zeitstrahl. Aktiver Zustand
via IntersectionObserver. `prefers-reduced-motion` → statischer Pfeil ohne
Bounce.

---

## 3. Sektions-Storyboard (Scroll-Reihenfolge)

| # | Sektion | Inhalt (aus Beilage) | Animation |
|---|---------|----------------------|-----------|
| 0 | **Intro/Hero** | „WOW!" + Outlander 189 € mtl., ohne Anzahlung | „wow" winzig → Vollbild-Explosion; Auto fährt rein; 189-Zähler |
| 1 | **Aktions-Claim** | „Ohne Anzahlung 189 € – Outlander Diamant mtl. leasen" + Gültig bis 31.12.2026 | Sticky-Claim, Gradient kippt zu Pink |
| 2 | **ASX Diamant** | „Jetzt ab XX €", 25.390 € UPE, Highlights, kompakter SUV | Crash-In Card von klein → groß |
| 3 | **Grandis Diamant** | „Jetzt ab XXX €", 29.390 €, Hybrid-SUV, Highlights | Crash-In, Parallax Auto |
| 4 | **8-Jahre-Garantie** | Garantiepaket bis 160.000 km | Badge zoomt rein |
| 5 | **Outlander Diamant** | Ab 189 €, ohne Anzahlung, 49.990 € UPE, −10.000 € Rabatt, bis 4.500 € Förderung, Gratis-Wallbox 599 € | Hero-Moment, Förder- & Wallbox-Badges fliegen ein |
| 6 | **Outlander Black** | Sondermodell, 63.690 € UPE, Highlights Black | Dark-Switch im Gradient |
| 7 | **Eclipse Cross** | Elektro-SUV, bis 6.000 € Förderung, Wallbox, Highlights | Gradient → Blau |
| 8 | **L200 „Coming Soon"** | Pick-up, Teaser | Großer „COMING SOON"-Type-Jump |
| 9 | **Wallbox & Förderung** | Gratis-Wallbox-Aktion + staatliche Förderung erklärt | Icon-Reveal |
| 10 | **CTA / Händlersuche** | „Kommen Sie vorbei" + Händler in der Nähe | Sticky CTA-Button |
| 11 | **Footer / Rechtliches** | Leasing-Fußnoten, MMD Automobile GmbH, MKG Bank etc. | Statisch, ruhig |

---

## 4. Crash-In Card — Mechanik

Jede Angebots-Karte ist dasselbe Bauteil mit Varianten:

- **Enter:** `scale(0.2)` + `opacity 0` → `scale(1)` mit Overshoot
  (z. B. bis 1.06 und zurück), minimale `rotateZ`, „Impact"-Schatten.
- **Trigger:** Eintritt in den Viewport (ScrollTrigger / IntersectionObserver).
- **Preis-Reveal:** Zahl zählt hoch (z. B. 0 → 189), „€" knallt nach.
- **Inhalt der Karte:** Modellname, Claim („Jetzt ab …"), Preisblock
  (UPE − Rabatt − Förderung = rechnerischer Aufwand), Highlight-Liste,
  Fahrzeugbild, optionale Badges (Wallbox / Förderung / Garantie).

---

## 5. TYPO3-Integration (Modul-Architektur)

Damit die Redaktion alles pflegen kann, bauen wir die LP als Satz
**wiederverwendbarer Content-Elemente** (Fluid-Templates + Assets),
nicht als eine Monolith-Seite.

Vorgeschlagene Module / Content-Elemente:

| TYPO3-Element | Felder (Backend pflegbar) |
|---------------|---------------------------|
| `wow_hero` | Headline, Sub, Preis, „ohne Anzahlung" (Bool), Hero-Bild, Gültig-bis-Datum |
| `wow_angebotskarte` | Modellname, Claim, UPE, Rabatt, Förderung, Endpreis, Highlights (Liste), Bild, Badges (Wallbox/Förderung/Garantie), Gradient-Start-/Endfarbe |
| `wow_garantie_badge` | Jahre, km, Text |
| `wow_foerderung_block` | Betrag, Erklärtext, Bedingungen |
| `wow_coming_soon` | Modellname, Teaser-Text, Bild |
| `wow_cta_haendler` | CTA-Text, Button-Link, Händlersuche-Embed |
| `wow_footer_legal` | Rechtstext (RTE) |

**Frontend-Assets:** ein gebündeltes JS (GSAP + ScrollTrigger) + ein CSS,
die in TYPO3 per `page.includeJSFooter` / `includeCSS` eingebunden werden.
Die Scroll-Logik liest `data-`Attribute aus den gerenderten Elementen
(z. B. `data-gradient-from`, `data-crash="true"`), sodass die Animation
unabhängig von der Reihenfolge funktioniert, die der Redakteur im Backend
zusammenklickt.

**Empfehlung Aufbau:** TYPO3-Sitepackage-Extension (`wow_campaign`) mit
Fluid-Templates, TCA-Definitionen und gebündelten Frontend-Assets.

---

## 6. Tech-Stack-Empfehlung

- **Animation:** GSAP 3 + ScrollTrigger (Industriestandard für Scrollytelling).
- **Styling:** modernes CSS (Custom Properties, `clamp()` für Type-Jumps,
  `min()/max()`), optional Tailwind falls gewünscht — aber für TYPO3-Einbindung
  ist schlankes, eigenes CSS oft sauberer.
- **Build:** Vite zum Bündeln der Assets; Output als statische JS/CSS-Dateien,
  die das Sitepackage einbindet.
- **Prototyp zuerst:** Wir bauen das Erlebnis als **standalone Prototyp**
  (eine HTML + JS + CSS) zum Abstimmen des Look & Feel — und überführen es
  danach 1:1 in die TYPO3-Fluid-Module. So sehen wir den Scroll-Effekt
  schnell live, ohne TYPO3-Setup zu blockieren.

---

## 6b. KI-anpassbare Architektur (damit man sich nicht verrennt)

Leitsatz: **Inhalt, Daten und Effekt sind getrennt.** Eine KI (oder ein
Mensch) soll Modelle, Preise, Farben und Reihenfolge ändern können, ohne
die Animations-Logik anzufassen — und umgekehrt. Dadurch bleiben Änderungen
lokal und vorhersehbar, statt dass eine kleine Anpassung alles kippt.

Konkrete Prinzipien:

1. **Eine zentrale Daten-Quelle.** Alle Angebote leben in *einer* Struktur
   (im Prototyp eine `content.json` / JS-Datenobjekt; in TYPO3 die
   Content-Element-Felder). Neues Modell = ein neuer Eintrag, kein neuer Code.
2. **Deklarativ statt imperativ.** Verhalten wird über `data-`Attribute
   gesteuert (`data-section`, `data-label`, `data-gradient-from/-to`,
   `data-crash`, `data-count-to`). Die KI ändert Attribute/Daten — nicht
   die JS-Engine. Die Engine ist „dumm" und generisch.
3. **Ein Bauteil, viele Instanzen.** Es gibt *eine* Angebots-Karte als
   Template. Alle Modelle nutzen sie. Kein Copy-Paste pro Modell → keine
   Drift, keine Stelle wird vergessen.
4. **Design-Tokens an einem Ort.** Farben, Verlaufs-Stops, Abstände, Typo-
   Größen als CSS-Custom-Properties in *einer* `:root`-Datei. „Mach das
   Pink dunkler" = ein Wert, global wirksam.
5. **Klare Grenzen + Doku.** Jede Datei hat einen Kommentar-Header „Was hier
   geändert werden darf / was nicht". Plus ein `AGENTS.md`/`CLAUDE.md` mit
   Karte des Projekts, damit eine KI sofort weiß, wo was liegt.
6. **Kleine, lesbare Dateien.** Lieber mehrere klar benannte Module
   (`gradient.js`, `crash-cards.js`, `timeline.js`) als eine 1000-Zeilen-Datei.
   So bleibt jeder Eingriff überschaubar und reviewbar.
7. **Defensive Defaults.** Fehlt ein Feld (z. B. kein Förder-Betrag), rendert
   das Bauteil sauber ohne Fehler. Eine KI kann nichts „kaputt" machen, indem
   sie etwas weglässt.

---

## 7. Offene Punkte / Klärungsbedarf

- [ ] Finale Preise/Rabatte für ASX, Grandis, Eclipse Cross (in Beilage „XX €")
- [ ] Echte Fahrzeug-Freisteller (PNG mit Transparenz) in hoher Auflösung
- [ ] Mitsubishi Brand-Font / Lizenz für Display-Typo
- [ ] Händlersuche: eigenes Embed oder Verlinkung auf mitsubishi-motors.de?
- [ ] **TYPO3-Version** — extern nicht ermittelbar (Seite blockt Bots mit
      403, TYPO3 versteckt Version bewusst). Bitte vom TYPO3-Team aus dem
      Backend bestätigen (Maintenance → System-Information). Annahme bis
      dahin: aktuelle LTS (13.4 / 14.x), Module werden versions-agnostisch
      gebaut. Außerdem: bestehendes Sitepackage vorhanden?
- [ ] Rechtstexte final (Leasing-Fußnoten, Förder-Bedingungen)

---

## 8. Vorgeschlagene nächste Schritte

1. **Konzept freigeben** (dieses Dokument abstimmen/anpassen).
2. **Prototyp Hero + Regenbogen-Scroll** bauen → den „WOW"-Moment live sehen.
3. **Crash-In Angebots-Karte** als Bauteil fertigstellen (ein Modell).
4. Restliche Sektionen ausbauen.
5. **In TYPO3-Module überführen** (Sitepackage `wow_campaign`).
