# 4 Gewinnt – CLAUDE.md

## URLs
- **Live:** https://seppofaz.github.io/4gewinnt/
- **GitHub:** https://github.com/sEppofaz/4gewinnt

## Deployment
```bash
cd ~/Dropbox/Apps/Claude/4Gewinnt
git add . && git commit -m "Beschreibung" && git push
# GitHub Pages deployt automatisch in ~30s
```

## Stack
- Statische PWA (HTML/CSS/JS, alles in index.html)
- GitHub Pages Hosting
- Service Worker: `4gewinnt-v1` (bei Icon/Manifest-Änderung hochzählen → `v2`, `v3` …)
- Icon-Methode: Methode A (macOS qlmanage + sips aus icon.svg)

## Spiellogik
- Spielfeld: 7 Spalten × 6 Reihen
- Spielmodi: 2 Spieler lokal + Gegen KI (Minimax, Alpha-Beta, Tiefe 5)
- Spieler 1: Weiß – Spieler 2: Blau
- Spalten-Tap: `touchstart`-Event auf Col-Overlay-Divs
- KI bevorzugt Mittelspalten (COL_ORDER: 3,2,4,1,5,0,6)

## Design
- Bayern-Rautenmuster: CSS linear-gradient (28×28px, Blau auf Weiß)
- Brett: #001A4D (Navy), leere Zellen: #000f30
- Bayern-Blau: #003F8A, Blau-Hell (Chip): #1565C0
- Querformat erzwungen: Portrait-Warnung via CSS @media

## Pitfalls
- `--silent` gibt es bei sips nicht → weglassen
- manifest.json `"purpose": "any"` (NICHT "any maskable" → iOS schneidet ab)
- SW Scope `'./'` relativ zur HTML-Datei (GitHub Pages Sub-Path)
- `updateCellSize()` bei `orientationchange` mit `setTimeout(..., 150)` (iOS braucht Delay)
