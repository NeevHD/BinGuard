#  BinGuard — Smart Waste Management

BinGuard is a single-file, AI-powered smart waste management dashboard built for Indian cities. It simulates an IoT-connected bin network with real-time monitoring, AI waste classification, admin analytics, and a collector route management system — all in one self-contained HTML file.

---

##  Features

###  Home / Landing Page
- Hero section with key statistics (bins monitored, waste collected, cities covered, uptime)
- Feature highlights: Real-time monitoring, AI classification, route optimization, and instant alerts

###  Bin Kiosk (Public-facing)
A guided 4-step disposal flow for users at a physical kiosk:
1. **Select Bin** — Choose from nearby bins by ID; view fill level and capacity
2. **Select Category** — Dry Waste, Wet Waste, Medical Waste, or E-Waste
3. **AI Classification** — Type an item name; Claude AI verifies if it belongs in the selected category
4. **Dispose** — Confirms disposal and updates bin fill level

**AI Classification:**
- Powered by `claude-sonnet-4-20250514` via the Anthropic API
- Returns item name, correct category, confidence level, and a plain-English explanation
- Falls back to local keyword matching if the API is unavailable (offline mode)

**Sidebar features:**
- Live area selector (GPS simulation)
- Nearby bin availability with fill status
- Kiosk statistics (items classified today, accuracy rate, avg wait time)

###  Admin Panel (PIN-protected)
Default PIN: `1234`

Sections accessible from a sidebar:
- **Dashboard** — Key metrics (total bins, fill rate, active alerts, collections today), bin status table, and an SVG city map with live bin markers
- **All Bins** — Full bin inventory table with fill bars, status badges, and per-bin actions (Mark Full, Schedule)
- **Analytics** — Bar charts for waste volume by zone and hourly activity, plus a category breakdown
- **Alerts** — Real-time alert feed (bin full, sensor errors); supports resolving individual alerts
- **Settings** — Alert thresholds (fill warning %, full %), auto-schedule toggle, notification preferences, and data export

###  Collector Panel (PIN-protected)
Default PIN: `5678`

- Daily route summary with stats (bins to collect, estimated time, distance)
- Optimized collection route rendered on the city map
- Per-bin checklist with "Mark Empty" actions that update fill levels in real time
- Progress bars for route completion and category breakdown

---

##  Tech Stack

| Layer | Technology |
|---|---|
| Language | Vanilla HTML, CSS, JavaScript |
| Fonts | Syne, DM Sans, Space Mono (Google Fonts) |
| AI | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Storage | `localStorage` for bin state persistence |
| Charts | Pure CSS/SVG bar charts |
| Map | Custom SVG city grid with animated bin markers |

No external JS frameworks, build tools, or backend required.

---

##  Getting Started

1. **Download** `binguard.html`
2. **Open** it in any modern browser (Chrome, Firefox, Edge, Safari)
3. That's it — the app runs fully client-side

> **Note:** The AI waste classification feature requires a valid Anthropic API key. The app calls `https://api.anthropic.com/v1/messages` directly from the browser. If the API call fails, the app falls back to local keyword-based classification automatically.

---

##  Access PINs

| Panel | Default PIN |
|---|---|
| Admin Panel | `1234` |
| Collector Panel | `5678` |

PINs can be changed in the JavaScript source (`ADMIN_PIN` and `COLLECTOR_PIN` constants).

---

##  Simulated Data

BinGuard ships with mock data for 10 bins across 4 city zones:

| Zone | Bins |
|---|---|
| Tambaram East | BIN-001, BIN-005 |
| Pallavaram | BIN-002, BIN-006 |
| Chromepet | BIN-003, BIN-007 |
| Mudichur | BIN-004, BIN-008 |
| Vandalur | BIN-009, BIN-010 |

Bin fill levels update automatically every 30 seconds to simulate live IoT sensor data. State is persisted in `localStorage` between page refreshes.

---

##  Waste Categories

| Category | Tag Color | Examples |
|---|---|---|
| Dry Waste | Yellow | Paper, plastic, glass, metal, cardboard |
| Wet Waste | Green | Food scraps, vegetable peels, organic matter |
| Medical Waste | Red | Syringes, medicine, bandages, PPE |
| E-Waste | Blue | Batteries, cables, electronics, appliances |

---

##  Project Structure

```
binguard.html          # Entire application (single file)
README.md              # This file
```

---

##  Customization

| What to change | Where to look |
|---|---|
| Bin locations and initial data | `const bins = [...]` in the `<script>` block |
| Admin / Collector PINs | `const ADMIN_PIN` and `const COLLECTOR_PIN` |
| Alert thresholds | Settings panel UI or `warnThreshold` / `fullThreshold` variables |
| AI model | `model` field in the `fetch` call inside `classifyItem()` |
| City zones | `area-chip` elements in the Kiosk sidebar HTML |

---

##  Panels Overview

```
┌─────────────────────────────────────────────┐
│   BinGuard   [Home] [Kiosk] [Admin] [Collector]  Live │
├─────────────────────────────────────────────┤
│                                             │
│  Home       → Landing page & feature list  │
│  Kiosk      → Public bin disposal flow     │
│  Admin    → Dashboard, analytics, alerts │
│  Collector  → Route & collection tracker  │
│                                             │
└─────────────────────────────────────────────┘
```

---

##  License

This project is open for personal and educational use. Attribution appreciated.
