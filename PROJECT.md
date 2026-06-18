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

## 5. Step-Plan
**Phase 1 (Statik):**
- [x] Step 1 — Cover/Hero (Logo, echte WoW-PNG, Outlander, rote 189 €-Leiste, „gültig bis")
- [ ] Step 2 — ASX & Grandis (+ 8-Jahre-Garantie-Siegel)
- [ ] Step 3 — Outlander Diamant & Black (Wallbox, Förderung)
- [ ] Step 4 — Eclipse Cross & L200 „Coming Soon"
- [ ] Step 5 — Abschluss/CTA „Angebot anfragen" + Argumente, Footer/Legal

**Phase 2 (Animation):**
- [ ] WoW-Intro (Zoom + Puls beim Öffnen)
- [ ] Scroll-Parallax (bidirektional)
- [ ] Reveals / „Kick-in" der Angebote
- [ ] Feinschliff Timing/Easing

## 6. Status-Log
- 2026-06-18: Reset auf sauberen Start. Assets + MMC-Font + Deploy bleiben.
  Beginn Phase 1, Step 1 (statische Cover-Seite).

## 7. Betrieb
- **Live:** https://dgruenewald97-arch.github.io/testiditest/ (Hard-Reload nach Push)
- **Lokal:** `index.html` im Browser öffnen.
- **Branch:** `claude/awesome-cannon-gy2g5u` → Push auf `main` deployt automatisch.
