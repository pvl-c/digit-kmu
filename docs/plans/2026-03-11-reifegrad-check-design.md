# Digitaler Reifegrad-Check — Design Document

## Overview

Interactive self-service digital maturity assessment for German SME manufacturers. Lives on a separate page (`check.html`) with a CTA banner on the main landing page. Pure HTML/CSS/JS, no frameworks. Matches existing dark theme with gold accent (#c8a96e).

## Architecture

- **check.html**: Standalone assessment page (full-screen quiz flow + report)
- **index.html**: Add CTA banner between "Module" and "Über uns" sections linking to check.html
- **No backend**: All scoring and report generation happens client-side in JS
- **No email gate**: Report shown immediately, CTA to contact at the end

## Assessment Structure

### 6 Categories, 16 Questions

| Category | Questions | Max Score |
|----------|-----------|-----------|
| Datenverwaltung | 3 | 9 |
| Prozesse | 3 | 9 |
| Produktion & Qualität | 3 | 9 |
| IT-Infrastruktur | 2 | 6 |
| Mitarbeiter & Wissen | 3 | 9 |
| Strategie & Führung | 2 | 6 |
| **Total** | **16** | **48** |

### Scoring

Each answer: 0 (analog) → 3 (advanced). Normalized to percentage per category and overall.

### 5 Maturity Levels

1. **Stufe 1: Analog** (0-20%)
2. **Stufe 2: Teildigital** (21-40%)
3. **Stufe 3: Vernetzt** (41-60%)
4. **Stufe 4: Datengetrieben** (61-80%)
5. **Stufe 5: Intelligent** (81-100%)

## UI Design

### Quiz Flow

- One question per screen, full viewport
- Progress bar at top (thin line + percentage + category label)
- 4 answer buttons per question (full-width cards with hover glow)
- Click answer → auto-advance to next question (300ms delay)
- Back button available
- Slide transitions (left→right forward, right→left back)
- Category transitions with label animation

### Report Screen

- Animated SVG radar chart (6 axes = 6 categories)
- Overall score with maturity level badge
- Per-category breakdown bars with status indicators
- Prioritized recommendations linked to M0-M3 modules
- CTA: "Gespräch vereinbaren" linking to contact section or mailto

### CTA Banner on Landing

- Placed between #module and #ueber-uns
- Accent-styled section with "Wo steht Ihr Betrieb?" heading
- Button: "Kostenlosen Reifegrad-Check starten →"

## Implementation Plan

1. Create check.html with quiz engine (questions data, state machine, scoring)
2. Build quiz UI (progress bar, question display, answer buttons, transitions)
3. Build report UI (radar chart SVG, category bars, recommendations engine)
4. Add CTA banner to index.html
5. Test and push to GitHub
