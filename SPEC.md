# ⚡ Bitcycle — Technical Specification
**MVP v1.1**

> *"Bitcycle is a permissionless protocol for human-powered travel, verified by GPS, funded by Bitcoin, and recorded permanently on-chain."*

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [What Is Bitcycle?](#2-what-is-bitcycle)
3. [Protocol Stack](#3-protocol-stack)
4. [Protocol Partners — Detail](#4-protocol-partners--detail)
5. [App as Partner Pitch Tool](#5-app-as-partner-pitch-tool)
6. [Route](#6-route)
7. [App — Core Concept](#7-app--core-concept)
8. [User Types](#8-user-types)
9. [Pages & Views](#9-pages--views)
10. [Slot Reservation & Identity](#10-slot-reservation--identity)
11. [GPS Tracking & Proof of Ride](#11-gps-tracking--proof-of-ride)
12. [Technical Stack](#12-technical-stack)
13. [API Endpoints](#13-api-endpoints)
14. [Build Order](#14-build-order--7-weeks-to-may-22)
15. [Future Iterations](#15-future-iterations)

---

## 1. Project Overview

Bitcycle is a permissionless, Bitcoin-native event protocol. The first real-world iteration is a multi-country cycling journey — Bournemouth to Bosa, Sardinia — launching 22 May 2025. The web application is the single source of truth: a live event hub for participants, spectators, and partners, and a permanent record once the ride concludes.

| | |
|---|---|
| **Event name** | Bitcycle — Iteration 1 |
| **Event start** | 22 May 2025 |
| **Route** | Bournemouth → Poole → Cherbourg → Paris → Lyon → Toulon → Porto Torres → Bosa |
| **Participants** | Maximum 10 riders (permissionless entry) |
| **Entry method** | Lightning payment via Blink API |
| **Identity** | Username + PIN  or  Nostr npub (NIP-07) |
| **Infrastructure** | Cloudflare Pages + Workers + KV |
| **Map** | Leaflet.js + OpenStreetMap (no API key required) |
| **Payments** | Blink API (Lightning invoices + webhooks) |

---

## 2. What Is Bitcycle?

Bitcycle is not a cycling trip. It is a live deployment of a Bitcoin-native physical protocol — a real-world system that demonstrates how Bitcoin infrastructure (payments, identity, community, energy) can power human movement end-to-end.

Each iteration of the protocol produces three things:

- **A story** — a real human journey across countries
- **A system** — a stack of Bitcoin-native infrastructure working in the real world
- **A record** — a permanent, timestamped, GPS-backed proof of ride

---

## 3. Protocol Stack

Bitcycle operates across five layers. Each layer is powered by a protocol partner. Partners are currently TBC — placeholder slots are shown in the app to demonstrate the value proposition.

| Layer | Function | Partner (TBC) | App Module |
|---|---|---|---|
| ⚡ Energy | Power generation & storage for the ride | Lemon Energy (TBC) | Energy dashboard |
| 🚲 Mobility | Physical transport platform (cargo e-bike) | Cargo bike brand (TBC) | Map / ride stats |
| 🟠 Spending | Bitcoin → real-world goods and services | Bitrefill (TBC) | Spend tracker |
| 🌐 Social | Community coordination along the route | Orange Pill App (TBC) | Meetups & community |
| 💸 Funding | Decentralised capital formation | Geyser (TBC) | Funding progress |

---

## 4. Protocol Partners — Detail

Each partner occupies a dedicated module in the web app. This section defines the role, contribution, and value proposition for each layer.

---

### ⚡ Energy Layer — Lemon Energy (TBC)

**Role:** Power infrastructure for the expedition

**Contribution:** Cargo bike battery architecture (3–5 kWh onboard), charging optimisation, future PV integration

**App module:** Live energy dashboard — kWh generated vs consumed, battery state, charging events

**Value to partner:** Real-world proof of product — a moving vehicle powered by your system, documented daily in public

---

### 🚲 Mobility Layer — Cargo Bike Manufacturer (TBC)

**Role:** Physical transport platform — the vehicle that carries everything

**Contribution:** Base cargo e-bike, load capacity and reliability across multiple countries, branding on vehicle

**App module:** Hero vehicle on the map — every rider dot represents your bike moving across Europe

**Value to partner:** Continuous public visibility across the entire route — every GPS ping is a brand impression

---

### 🟠 Spending Layer — Bitrefill (TBC)

**Role:** Real-world Bitcoin spending infrastructure

**Contribution:** Gift cards for food, accommodation and transport — enabling Bitcoin-only living for the full duration

**App module:** Spend tracker — weekly log of what was purchased with Bitcoin, running total in sats

**Value to partner:** Live demonstration that Bitcoin works as money in the real world, documented publicly

---

### 🌐 Social Layer — Orange Pill App (TBC)

**Role:** Community coordination and discovery along the route

**Contribution:** Find Bitcoiners along the route, organise meetups in key cities, discover hosts and support

**App module:** Meetups & community tab — upcoming events, cities visited, Bitcoiner encounters logged

**Value to partner:** Real-world activation of your user base along the entire route from UK to Sardinia

---

### 💸 Funding Layer — Geyser (TBC)

**Role:** Decentralised crowdfunding and expedition capital

**Contribution:** Crowdfund the expedition, sponsor-a-km mechanic, support individual riders, transparent funding

**App module:** Live funding progress bar on homepage — total raised, milestones unlocked, top supporters

**Value to partner:** Campaign visibility to your entire user base with a compelling real-world narrative

---

## 5. App as Partner Pitch Tool

Until partners are confirmed, the app displays placeholder slots for each layer. This serves two purposes: it shows the public the full vision, and it gives potential partners a live demo of exactly what their involvement looks like.

| Module | Placeholder display |
|---|---|
| Energy tab | Energy dashboard UI — *"Powered by: Energy Partner TBC"* |
| Spending tab | Spend tracker UI — *"Bitcoin spending layer: Partner TBC"* |
| Community tab | Meetup map — *"Social coordination layer: Partner TBC"* |
| Funding bar | Funding progress UI — *"Funding layer: Partner TBC"* |
| Map / bike | Route and rider dots live — *"Mobility partner: TBC"* |

When a partner is confirmed, their name, logo link, and live data replace the placeholder. No rebuild required — it is a single KV update.

---

## 6. Route

The route is pre-loaded as a GeoJSON file and displayed as a static overlay on the map. Rider GPS dots animate on top of the route in real time during the live phase.

| Stage | From | To | Notes |
|---|---|---|---|
| 1 | Bournemouth | Poole | Departure point, road transfer |
| 2 | Poole | Cherbourg | Ferry crossing |
| 3 | Cherbourg | Paris | Through Normandy |
| 4 | Paris | Lyon | Through central France |
| 5 | Lyon | Toulon | South through the Rhône valley |
| 6 | Toulon | Porto Torres | Ferry crossing to Sardinia |
| 7 | Porto Torres | Bosa | Final stage by road |

---

## 7. App — Core Concept

The app is the homepage. There is no separate marketing site. The live map, route, rider list, slot counter, and partner modules are the product. Anyone landing on the URL immediately understands the event by seeing it.

### Three phases, one URL

| Phase | What the page shows |
|---|---|
| **PRE-EVENT** | Route on map, countdown, X/10 slot counter, rider list, partner placeholder modules, join flow |
| **LIVE** | Live rider dots updating every 15s, feed panel, active partner modules |
| **POST-EVENT** | Static map with full trace, final stats, archive link |

Phase is controlled by a single KV flag: `event_state: pre | live | post`

---

## 8. User Types

| User | Access | What they can do |
|---|---|---|
| Public / spectator | No login | View map, route, riders, feed, partner modules |
| Participant — simple | Username + PIN | All public views + GPS tracking, posts, own dashboard |
| Participant — sovereign | Nostr npub (NIP-07) | Same as simple + cryptographic identity, Nostr broadcasting |
| Organiser | Reserved slot (no fee) | All participant features + set event_state, manage partner data |

---

## 9. Pages & Views

### 9.1  `/` — Homepage

- **PRE-EVENT:** Full-width map with planned route, countdown, X/10 slot counter, rider list, partner placeholder modules, Join button
- **LIVE:** Live rider dots updating every 15s, feed panel, active partner modules
- **POST-EVENT:** Static map with full trace, final stats, archive link

### 9.2  `/join` — Claim a Slot

- Shows remaining slot count
- Two entry paths side by side: Simple (username + PIN) and Sovereign (Nostr NIP-07)
- Both paths generate a Blink Lightning invoice for the entry fee
- On payment confirmation: slot marked claimed, rider profile created

### 9.3  `/riders/[id]` — Rider Profile

- Public page — no login to view
- Name, bio, join date, live position on mini-map
- GPS log — timestamped Proof-of-Ride history
- Posts, daily updates, stage reviews
- Stats: km ridden, days active, stages completed

### 9.4  `/feed` — Event Feed

- Chronological stream: GPS check-ins, posts, comments, meetups
- All partner module events (spend, energy, funding milestones) appear here
- Public, no login required

### 9.5  `/archive` — Permanent Record

- Visible post-event only
- Full route replay, per-rider GPS log, final statistics
- Partner impact summary: energy used, sats spent, km funded, meetups held
- The permanent record of the protocol in action

---

## 10. Slot Reservation & Identity

### 10.1  Slot System

10 slots. Permissionless entry. First to pay claims a slot. Entry fee paid via Lightning (Blink API).

| Step | Action |
|---|---|
| 1 | User selects entry path on `/join` |
| 2 | Worker calls Blink API → generates Lightning invoice |
| 3 | QR code + payment string shown to user |
| 4 | User pays from any Lightning wallet |
| 5 | Blink webhook → Worker verifies payment |
| 6 | Slot claimed in KV, rider profile created |

### 10.2  Simple Path (username + PIN)

- Choose display name, set 4–6 digit PIN
- Assigned a hidden Blink Lightning address for payment
- Return login: username + PIN
- Trust-based identity stored in KV (hashed PIN)

### 10.3  Sovereign Path (Nostr NIP-07)

- Connect Alby browser extension
- Sign a challenge — private key never leaves the device
- `npub` becomes permanent rider ID
- Return login: sign again (no password)
- Posts can be broadcast to Nostr relays for decentralised permanence

### 10.4  Comparison

| | Simple | Sovereign (Nostr) |
|---|---|---|
| Login method | Username + PIN | NIP-07 signature (Alby) |
| Works on mobile | Yes — any browser | Requires Alby extension |
| Identity proof | Trust-based | Cryptographic |
| Posts on Nostr | No | Optional |
| Recommended for | Casual participants | Protocol-native participants |

---

## 11. GPS Tracking & Proof of Ride

The core data layer. Every position ping is stored as an immutable timestamped record. Together they form the Proof-of-Ride log — the cryptographic backbone of the protocol.

| | |
|---|---|
| **Update interval** | Every 15 seconds while tracking active |
| **Data per ping** | Rider ID, lat, lng, timestamp, GPS accuracy |
| **Storage** | Latest position (overwrite) + append to ride log (permanent) |
| **Anti-cheat** | Speed filter >80 km/h, accuracy filter >50m, gap detection >30 min |
| **Future** | SHA-256 hash per ping, daily anchoring to Bitcoin |

---

## 12. Technical Stack

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | HTML + Vanilla JS | No framework — fast, simple, works on any device |
| Hosting | Cloudflare Pages | Static site, global CDN, free tier |
| Backend | Cloudflare Workers | Serverless API, runs at the edge |
| Storage | Cloudflare KV | All state: riders, positions, slots, posts, partner data |
| Map | Leaflet.js + OpenStreetMap | No API key, lightweight, mobile-friendly |
| Payments | Blink API | Lightning invoice generation + payment webhooks |
| Auth (simple) | KV with hashed PIN | Username + PIN session |
| Auth (sovereign) | Nostr NIP-07 | Cryptographic identity via Alby |
| Route data | GeoJSON (static file) | Pre-loaded route overlay |
| Partner data | Cloudflare KV | Partner names, status, live metrics per module |

### KV Key Structure

| Key | Value |
|---|---|
| `event:state` | `pre \| live \| post` |
| `slots:count` | Integer 0–10 |
| `rider:[id]` | JSON: name, path, joined, bio |
| `rider:[id]:auth` | Hashed PIN or npub |
| `rider:[id]:latest` | JSON: lat, lng, timestamp |
| `rider:[id]:log:[ts]` | JSON: lat, lng, timestamp, accuracy (append-only) |
| `rider:[id]:posts` | JSON array of post objects |
| `partner:[layer]` | JSON: name, confirmed, logoUrl, liveData |
| `payment:[invoice_id]` | JSON: rider_id, amount, status, timestamp |

---

## 13. API Endpoints

| Method + Path | Auth | Description |
|---|---|---|
| `GET /api/state` | Public | Current event_state + slot count |
| `GET /api/riders` | Public | All riders with latest positions |
| `GET /api/riders/[id]` | Public | Single rider profile, posts, stats |
| `GET /api/feed` | Public | Chronological event feed |
| `GET /api/partners` | Public | All partner module data (confirmed or placeholder) |
| `GET /api/slots` | Public | Slots claimed / total |
| `POST /api/join` | None | Initiate slot claim — returns Lightning invoice |
| `POST /api/join/confirm` | Blink webhook | Payment confirmed — creates rider profile |
| `POST /api/auth` | None | Authenticate rider (PIN or Nostr sig) |
| `POST /api/location` | Rider auth | Submit GPS ping |
| `POST /api/post` | Rider auth | Submit text post or update |
| `POST /api/partner/update` | Organiser | Update partner live data |

---

## 14. Build Order — 7 Weeks to May 22

| Week | Focus | Deliverable |
|---|---|---|
| Week 1 | Foundation | CF Pages + Workers + KV setup, GeoJSON route on Leaflet, event_state flag, countdown, slot counter |
| Week 2 | Payments | Blink API integration, invoice generation, webhook handler, `/join` page skeleton |
| Week 3 | Identity | Simple path (username + PIN), sovereign path (Nostr NIP-07), full `/join` flow |
| Week 4 | GPS tracking | Location submission from mobile browser, live rider dots, ride log to KV |
| Week 5 | Content + feed | Rider posts, `/feed` page, `/riders/[id]` profile, partner placeholder modules |
| Week 6 | Partners + polish | Partner module UI with placeholders, mobile testing, rider dashboard |
| Week 7 | Live mode + archive | Switch to live state on May 22, archive mode, final testing |

---

## 15. Future Iterations

Out of scope for MVP but architecturally compatible with the current stack:

- **Proof-of-Ride hashing** — SHA-256(rider_id + lat + lng + timestamp) anchored to Bitcoin
- **Distance-based sats rewards** — daily work score → Lightning payout to riders
- **Alby Hub / self-hosted Lightning node** — replace Blink for full sovereignty
- **Nostr event broadcasting** — all posts and GPS events published to public relays
- **Geyser integration** — live funding progress pulled directly from Geyser API
- **Lemon Energy API** — live battery and energy data streamed to energy dashboard
- **Bitrefill spend log** — public weekly breakdown of Bitcoin purchases
- **Leaderboard** — km ridden, elevation gain, stages complete, sats spent
- **Multi-event protocol** — Bitcycle as a reusable framework for future iterations
- **Protocol whitepaper** — formal definition of Proof-of-Ride for external adoption

---

*Bitcycle MVP Technical Specification v1.1 · Bournemouth → Bosa · 22 May 2025*
