# FactoryGate — Global Sourcing & U.S. Landed-Cost Decision Engine (v1.0)

## 1. Mission & Definition of Done
Build **FactoryGate — Global Sourcing & U.S. Landed-Cost Decision Engine**, a single-page, executive light-mode web app created by **Waleed Ahmad (Supply Chain Management & Quantitative Methods)**.

A U.S. supply chain buyer selects a product category, compares two global supplier quotes side-by-side, and sees which hub is truly cheaper once export agent markup (+18%), international freight, cargo insurance, U.S. import duty, and U.S. Customs Merchandise Processing Fees (MPF) are counted—not just the factory sticker price.

**Non-Negotiables**
- **100% Deterministic & Bug-Free:** Every number comes from exact formulas in Section 4. Strict input validation blocks negative numbers, zero/blank/fractional quantities, NaN, and Infinity.
- **Zero External Dependencies:** Plain HTML, CSS, and vanilla JavaScript (ES2020) using classic `<script defer src="...">` tags (`no type="module"`, `no npm install`, `no external chart libraries`). Works both on GitHub Pages and when opened from disk.
- **Executive Human Design:** Calm, data-first light-mode layout (`navy #0B1F3A`, `slate #334155`, `emerald #047857` for savings/winner, `amber #B45309` for cautions/broker markup, `rose #BE123C` for duty/errors). No emoji, no purple gradients, no AI buzzwords.
- **Verified Creator Credit:** Display **Created by Waleed Ahmad | Supply Chain Analytics** in the top-right header badge, bottom permanent footer, and first row of every downloaded CSV audit report.

## 2. File Structure & Automated Tests
Create this exact structure using Node 22 built-in tests (`node --test`):

- `index.html`: Skip link, header with creator badge, navy sub-banner, 5-link section nav (`#scenario`, `#compare`, `#stop-the-line`, `#export`, `#method`), 5 main sections, and permanent footer.
- `styles.css`: Responsive layout (`360px`, `768px`, `1280px` with zero horizontal scrolling), crisp white cards (`1px solid #E2E8F0`, `12px` radius), segmented radio pills, accessible focus rings, and clean print styles.
- `package.json`: `{ "name": "factorygate", "version": "1.0.0", "private": true, "license": "MIT", "author": "Waleed Ahmad", "engines": { "node": ">=22" }, "scripts": { "test": "node --test" } }`
- `src/config.js`: `window.FactoryGateConfig = Object.freeze({ authorName: 'Waleed Ahmad', authorTitle: 'Supply Chain Management & Quantitative Methods', linkedinUrl: '', githubUrl: '', repoUrl: '' });`
- `src/engine.js`: Pure math & validation module (`UMD-lite` wrapper for browser + Node).
- `src/presets.js`: 5 industry scenarios and 10 supplier quotes.
- `src/format.js`: `Intl.NumberFormat('en-US')` display formatting (`2 decimals >= $1.00`, `3 decimals < $1.00`, `2 decimals for shipments`, `1 decimal for % and blended days`).
- `src/brief.js`: Generates the Buyer's Sourcing Brief, cost-bridge insight sentence, and negotiation target sentence.
- `src/exports.js`: Generates UTF-8 BOM CSV (`FactoryGate_Supplier_Comparison_YYYY-MM-DD.csv`), 5-line Executive Summary memo, and `#s=` base64url share links.
- `src/chart.js`: Responsive inline SVG horizontal stacked bar chart comparing Factory Price, Agent Markup, Freight & Insurance, and U.S. Duty & MPF, plus a "View as table" toggle.
- `src/app.js`: Single state object driving instant updates, toast notifications (`role="status"`), clipboard copy, and CSV download.
- `tests/engine.test.js`: Automated `node:test` suite verifying all formulas, USMCA exemptions, MPF clamps (`$34.58` min / `$670.86` max), 80/20 splits, input validation, CSV escaping, and share links.
- `.github/workflows/ci.yml` & `.github/workflows/pages.yml`: Automated test runner and GitHub Pages deployment workflow.
- `README.md`, `docs/METHODOLOGY.md`, `LICENSE` (MIT, Copyright 2026 Waleed Ahmad), `.gitignore`.

## 3. Five Page Sections
1. **Header & Creator Badge:** Title `FactoryGate`, subtitle `Global Sourcing & U.S. Landed-Cost Decision Engine`, top-right badge `Created by Waleed Ahmad | Supply Chain Analytics` (links to `linkedinUrl` if set), `Planning estimates · Nov 18, 2026` badge, and navy sub-banner: `Compare global manufacturing clusters by export-quality score, true U.S. landed cost, and direct factory-gate savings.`
2. **Section 01 · Scenario (`#scenario`):**
   - Product category `<select>` with 5 presets (`straps`, `hinges`, `cases`, `ecopack`, `utensils`).
   - Buying priority radio pills: `Best Price-to-Quality Balance` (default), `Lowest Landed Cost`, and `Fastest U.S. Delivery`.
   - `Buyer's Sourcing Brief` card naming `#1 pick`, priority reason, manufacturing cluster strength, amber sticker-price trap alert (when applicable), watch-out, `#2 backup`, and `80/20` continuity blend.
3. **Section 02 · Compare (`#compare`):**
   - Shared `Order quantity (units)` input (`1` to `10,000,000`) + `Reset to preset` button.
   - Side-by-side Supplier A & Supplier B cards with inputs: Manufacturing city & country, Factory sticker price ($/unit), Ocean or air freight ($/unit), Cargo insurance ($/unit), All-in U.S. duty rate (%), Quality score (`1.0–10.0` slider), Transit time (`days`), Sourcing route switch (`Direct factory negotiation (0% middleman fee)` vs. `Export broker / agent (+18% markup)`), and `Qualifies for USMCA / FTA duty & MPF exemption` checkbox.
   - Full per-unit build-up list (`Factory price`, `Agent markup`, `Adjusted FOB`, `Freight & insurance`, `CIF value`, `U.S. duty`, `MPF per unit`, `True landed cost`, `Total shipment`, `Value index`).
   - Amber `Sticker-price trap` alert when the supplier with the lower factory sticker price lands higher at the U.S. port.
   - 3 KPI cards: `Recommended winner`, `Net shipment savings ($ and %)`, and `80/20 dual-source blended unit cost`.
   - Inline SVG stacked bar chart + `View as table` toggle + dynamic `Insight` sentence + `Negotiation target` card.
4. **Section 03 · Stop the Line (`#stop-the-line`):**
   - Inputs: `Daily line-stoppage or stockout loss ($ per day)` (default `12000`), `Ocean delay (days)` (default `5`), `Extra cost of emergency air freight ($)` (default `45000`).
   - Status banner: `AIR-SHIP NOW — Saves ${amount}` when `dailyLoss * delayDays > airPremium`, else `HOLD FOR OCEAN — Saves ${amount}`, plus `breakEvenDays` (`airPremium / dailyLoss`).
5. **Section 04 · Export, Method & Footer (`#export`, `#method`):**
   - Buttons: `Download Supplier Comparison (CSV)`, `Copy Executive Summary`, and `Copy share link`, plus a live `Summary preview` monospace box.
   - Method block explaining the 8 formulas and U.S. customs valuation (`19 U.S.C. 1401a`).
   - Permanent Footer: `Designed, built & maintained by Waleed Ahmad — Supply Chain Management & Quantitative Methods | Deterministic Trade & Landed-Cost Decision Tool`, CBP FY2027 MPF footnote (`0.3464%`, `$34.58` min / `$670.86` max), privacy line (`Everything you type stays in your browser.`), and optional LinkedIn/GitHub links.

## 4. Exact Calculation Formulas
- `brokerMarkup = route === 'broker' ? price * 0.18 : 0`
- `adjustedFob = price + brokerMarkup`
- `cifValue = adjustedFob + freight + insurance`
- `entryValue = adjustedFob * quantity`
- `customsDuty = usmca ? 0 : adjustedFob * (tariffPct / 100)` (U.S. duty applies to transaction value `adjustedFob`, excluding international freight/insurance)
- `mpfShipment = usmca ? 0 : Math.min(Math.max(entryValue * 0.003464, 34.58), 670.86)`
- `landedPerUnit = cifValue + customsDuty + (mpfShipment / quantity)`
- `totalShipment = landedPerUnit * quantity`
- `valueIndex = (quality / landedPerUnit) * 10`
- `dualSource`: `primaryQty = Math.floor((8 * quantity + 5) / 10)`, `backupQty = quantity - primaryQty`, computing each portion as its own customs entry.

## 5. Balanced Presets
1. **VR/AR Headset Breathable Straps & Soft-Goods (`straps`, qty `10000`):**
   - A: `Faisalabad, Pakistan`, direct, `$1.45`, freight `$0.09`, ins `$0.01`, duty `17.0%`, USMCA `false`, quality `8.5`, lead `34` days.
   - B: `Shenzhen, China`, broker, `$1.35`, freight `$0.06`, ins `$0.01`, duty `44.5%`, USMCA `false`, quality `8.3`, lead `24` days.
2. **Precision Stainless-Steel Hinges & Hardware (`hinges`, qty `25000`):**
   - A: `Sialkot, Pakistan`, direct, `$2.10`, freight `$0.14`, ins `$0.01`, duty `29.0%`, USMCA `false`, quality `8.7`, lead `36` days.
   - B: `Shenzhen, China`, broker, `$1.95`, freight `$0.09`, ins `$0.01`, duty `54.0%`, USMCA `false`, quality `8.4`, lead `25` days.
3. **Custom Protective Carrying Cases & Pouches (`cases`, qty `5000`):**
   - A: `Sialkot / Lahore, Pakistan`, direct, `$3.10`, freight `$0.22`, ins `$0.02`, duty `13.5%`, USMCA `false`, quality `8.6`, lead `35` days.
   - B: `Monterrey, Mexico`, direct, `$3.95`, freight `$0.10`, ins `$0.01`, duty `13.5%`, USMCA `true`, quality `8.4`, lead `6` days.
4. **Foodservice Eco-Packaging & Molded Pulp Containers (`ecopack`, qty `100000`):**
   - A: `Lahore / Karachi, Pakistan`, direct, `$0.118`, freight `$0.045`, ins `$0.001`, duty `10.0%`, USMCA `false`, quality `8.2`, lead `38` days.
   - B: `East Asia (China-origin, via Export Broker)`, broker, `$0.112`, freight `$0.032`, ins `$0.001`, duty `37.5%`, USMCA `false`, quality `7.8`, lead `28` days.
5. **Commercial Kitchen Stainless Utensils & Trays (`utensils`, qty `12000`):**
   - A: `Gujranwala / Sialkot, Pakistan`, direct, `$3.60`, freight `$0.26`, ins `$0.02`, duty `27.0%`, USMCA `false`, quality `8.5`, lead `37` days.
   - B: `Guangdong, China`, broker, `$3.55`, freight `$0.18`, ins `$0.02`, duty `52.0%`, USMCA `false`, quality `8.4`, lead `26` days.
