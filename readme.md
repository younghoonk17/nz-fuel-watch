# NZ Fuel Watch

A real-time dashboard monitoring New Zealand's fuel supply situation during national emergencies.

**Live Site:** [https://fuelwatch.nz](https://fuelwatch.nz)

---

## Purpose

Tracks and visualises NZ's fuel stock levels (petrol, diesel, jet fuel) during supply disruptions, particularly during the **March 2026 Middle East crisis**. Displays:

- National Fuel Plan phase status (Phase 1–4)
- Onshore + on-water stock levels vs MSO minimums
- Incoming vessel schedules
- Live energy commodity prices
- Embedded fuel price map (Gaspy)
- Hormuz Strait vessel tracker

---

## Data Sources

| Source | What It Provides |
|--------|------------------|
| **[MBIE](https://www.mbie.govt.nz/building-and-energy/energy-and-natural-resources/energy-generation-and-markets/liquid-fuel-market/fuel-supply-disruption-response/middle-east-conflict-and-new-zealands-fuel-stocks)** | Fuel stock levels, vessel schedules, phase status |
| **Gaspy** | Live retail fuel prices (embedded map) |
| **Marine Vessel Traffic** | Hormuz Strait ship tracking (embedded map) |
| **Trading Economics** | Crude oil commodity prices (Brent) |

---

## Tech Stack

- **Pure HTML/CSS/JS** — No frameworks or build tools
- **Google Fonts** — Noto Sans KR, Share Tech Mono, Barlow Condensed
- **CSS Variables** — Dark cyberpunk theme
- **Bilingual** — English/Korean toggle via `data-t` attributes
- **Google AdSense** — Monetisation enabled

---

## File Structure

```
nz-fuel-watch/
├── index.html          # Main dashboard (all-in-one file)
├── 15March.html        # Snapshot archive (15 March 2026)
├── ads.txt             # AdSense verification
├── CNAME               # GitHub Pages custom domain
├── readme.md           # This file
└── .git/               # Git repository
```

---

## Manual Update Process

When MBIE publishes new data (typically weekly on Wednesdays):

### 1. Update Header
```html
<!-- Header updated date -->
<span data-t="updated" data-en="Updated: 25 Mar 2026" data-ko="업데이트: 2026 년 3 월 25 일">

<!-- Phase badge -->
<span class="phase-badge">PHASE 1 — MINOR</span>
```

### 2. Update Ticker
```html
<!-- Ticker items t1–t7 -->
<span data-t="t1" data-en="⛽ Petrol: 48.7d total..." ...>
```

### 3. Update Fuel Tiles
```html
<!-- Petrol tile -->
<div class="total-days">48.7<span style="font-size:1.2rem">d</span></div>
<span class="onshore">24.5d</span>
<span class="onwater">24.2d</span>
<span>28d</span> <!-- MSO Required -->

<!-- Repeat for Diesel + Jet Fuel -->
```

### 4. Update Gauge Bars
```html
<!-- Width % = (onshore days / 40) * 100 -->
<div class="gauge-bar-fill" style="width:61.25%"></div>
<!-- MSO line % = (MSO min / 40) * 100 -->
<div class="gauge-min-line" style="left:70%"></div>
```

### 5. Update Tables
```html
<!-- Full Stock Breakdown table -->
<tr class="row-onshore"><td>Onshore</td><td>24.5d</td><td>18.1d</td><td>20.1d</td></tr>
<tr class="row-onwater"><td>On-water</td><td>24.2d</td><td>28.3d</td><td>23.4d</td></tr>
<tr class="row-total"><td>Total</td><td>48.7d</td><td>46.4d</td><td>43.4d</td></tr>
<tr class="row-mso"><td>MSO Min.</td><td>28d</td><td>21d</td><td>24d</td></tr>
<tr class="row-buffer"><td>Buffer</td><td style="color:var(--red)">-3.5d</td><td style="color:var(--red)">-2.9d</td><td style="color:var(--red)">-3.9d</td></tr>

<!-- Vessels table -->
<tr class="row-vessel"><td>Mar 23–29</td><td>1</td><td>4.4d</td><td>0d</td><td>2d</td></tr>
```

### 6. Update Status Panel
```html
<!-- MSO Compliance -->
<span class="status-val warn">MET via EEZ</span>
<!-- National Fuel Plan -->
<span class="status-val ok">Phase 1 — Minor</span>
<!-- Supply Disruption -->
<span class="status-val warn">MONITORING</span>
```

### 7. Update Assessment Cards
```html
<!-- Short Term, Watch Points, Global Context -->
<p data-t="short_term_txt" data-en="..." data-ko="...">...</p>
```

### 8. Update Footer
```html
v2.1 — Built 25 Mar 2026
```

### 9. Commit & Deploy
```bash
git add index.html
git commit -m "Update: 25 Mar 2026 — MBIE weekly data"
git push
# GitHub Pages auto-deploys
```

---

## Key Metrics Explained

| Metric | Meaning |
|--------|---------|
| **Onshore** | Fuel physically stored in NZ tanks |
| **On-water** | Fuel on tankers within NZ's supply chain |
| **MSO Required** | Minimum Supply Obligation — legal minimum stock (Petrol: 28d, Diesel: 21d, Jet: 24d) |
| **Buffer** | Days above MSO minimum (negative values mean relying on on-water stocks) |
| **Phase 1–4** | National Fuel Plan escalation levels (Minor → Severe) |

---

## Future Enhancements

- [ ] Auto-fetch MBIE data via scraper
- [ ] JSON config file for easier updates
- [ ] Build script to generate HTML from structured data
- [ ] Email/SMS alerts when phase changes
- [ ] Historical data archive page

---

## License

MIT — Built for public service during national emergencies.

---

**Last Updated:** 25 March 2026  
**Version:** 2.1
