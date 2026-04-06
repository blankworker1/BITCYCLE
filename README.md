# BITCYCLE


**A permissionless protocol for human-powered travel, verified by GPS, funded by Bitcoin, and recorded permanently on-chain.**

Bitcycle is a live event hub for a multi-country cycling expedition (Bournemouth, UK to Bosa, Sardinia) departing 22 May 2025. This repository contains the web application: a single-page app that serves as the public face of the event before, during, and after the ride.

---

## What Is Bitcycle?

Bitcycle is not a cycling trip. It is the first real-world deployment of a Bitcoin-native physical protocol - a stack of infrastructure working together to power, fund, coordinate, and verify human movement using Bitcoin.

Each iteration of the protocol produces three things:

- **A story**  a real human journey across countries
- **A system**  Bitcoin-native infrastructure working end-to-end in the real world
- **A record** a permanent, timestamped, GPS-backed proof of ride

---

## The Route

```
Bournemouth - Poole - [Ferry] - Cherbourg - Chartres - Lyon - Toulon - [Ferry] - Porto Torres - Bosa
```

Two sea crossings. Three countries. Entirely by human-powered bike.

---

## The Protocol Stack

Bitcycle operates across five layers. Each layer is supported by a protocol partner.

```
| Layer      | Function                                | Partner      |
| Energy     | Power generation & storage              | TBC |
| Mobility   | Physical transport platform.            | TBC |
| Spendingn  | Bitcoin for real-world goods & services | TBC |
| Social     | Community coordination along the route  | TBC |
| Funding    | Decentralised capital formation.        | TBC |

```

Each partner has a dedicated live module in the web app, updated in real time from their data feed during the event.

---

## The Web App

The app is the homepage. There is no separate marketing site - the live map, route, rider profiles, slot counter, and partner modules are the product.

(https://blankworker1.github.io/BITCYCLE/)

### Three Phases

The app renders differently depending on the current event state, controlled by a single flag:

**PRE-EVENT** (`event_state: pre`)
- Full-width live map with planned route overlay
- Countdown timer to departure
- Slot counter X of 10 claimed
- Rider list as slots fill up
- Join flow claim a slot via Lightning payment

**LIVE** (`event_state: live`)
- Live rider GPS dots on the map, updating every 15 seconds
- Real-time event feed GPS check-ins, rider posts, energy updates
- Partner module dashboard energy, spend, funding, community
- Individual rider profiles with proof-of-ride GPS log

**ARCHIVE** (`event_state: post`)
- Full route replay
- Complete GPS log per rider
- Final statistics and partner impact summary
- Permanent record of the event

### Pages

```

| Path           | Description |

| `/`            | Homepage map, route, riders, partner modules |
| `/join`        | Claim a slot two entry paths (see below) |
| `/riders/[id]` | Individual rider profile, GPS log, posts |
| `/feed`        | Chronological event feed  all activity |
| `/archive`     | Post-event permanent record |

```

---

## Joining the Ride

For this first event there are 10 rider slots are available. Entry is permissionless - no application or approval needed. Claiming a slot requires a Lightning payment.

### Two Entry Paths

**Simple Path**
- Choose a username
- Set a PIN (6 digits)
- Pay the entry fee via Lightning invoice (any wallet)
- Slot confirmed, profile created

**Sovereign Path**
- Connect an Alby browser extension (NIP-07 Nostr wallet)
- Sign a challenge  your private key never leaves your device
- Pay the entry fee via Lightning invoice
- Slot confirmed against your `npub` cryptographically provable identity
- Posts can be optionally broadcast to Nostr relays for decentralised permanence

Both paths give full access to the rider dashboard and GPS tracking during the ride.

---

## GPS Tracking & Proof of Ride

Once the ride begins, logged-in riders open the app on their phone. With one tap, GPS tracking starts and runs in the background - no separate app needed.

- Position submitted every **15 seconds**
- Each ping stored as: `rider_id Â· latitude Â· longitude Â· timestamp Â· accuracy`
- Two writes per ping: latest position (live map) + append to permanent ride log
- Basic anti-cheat filtering: speed cap (>80 km/h flagged), accuracy filter (>50m discarded)

The accumulated GPS log is the **Proof of Ride** â€” a timestamped, immutable record of the journey. Future iterations will hash each ping and anchor the daily record to Bitcoin.

---

## Rider Content

In addition to passive GPS, riders can post manually from the dashboard:

- **Daily update** short text from the road
- **Stage review** longer reflection on a completed stage
- **Comment** short note, optionally tied to a location

All content is timestamped and public. Sovereign-path riders can sign posts with their Nostr key.

---

## Technical Stack

```
| Layer                | Technology |

| Frontend             | HTML + Vanilla JS (no framework) |
| Map                  | Leaflet.js + OpenStreetMap (no API key required) |
| Hosting              | Cloudflare Pages |
| Backend              | Cloudflare Workers |
| Storage              | Cloudflare KV |
| Payments             | Blink API (Lightning invoices + webhooks) |
| Identity (simple)    | Cloudflare KV with hashed PIN |
| Identity (sovereign) | Nostr NIP-07 via Alby |

```

The current file in this repository is the **static demo** a self-contained HTML file with dummy data, no backend required. It is intended for partner review and feedback before the full backend is built.

---

## Repository Structure

```
/
 index.html          # Main application (demo: self-contained, no backend)
 README.md           # This file
```

The production app will expand to include Cloudflare Worker scripts, KV schemas, and route GeoJSON. Those will be added to this repository as the build progresses.

---

## Current Status

```

| Component                      | Status |

| Static demo                    | Live |
| Route & map                    | Complete |
| Rider profiles                 | In demo |
| Partner modules                | Placeholder awaiting partner confirmation |
| Cloudflare Workers backend     | In development |
| Lightning payment flow (Blink) | In development |
| GPS tracking (live)            | In development |
| Nostr identity (NIP-07)        | In development |

```


---

## For Potential Partners

If you are reviewing this as a potential protocol partner, the live demo shows exactly where your layer lives in the app and what visibility you receive.

Each partner module displays:

- Your brand and role in the protocol stack
  
- Live metrics from your data feed (energy generated, sats spent, km funded, etc.)
  
- Presence on every page view for the duration of the ride

The demo currently shows placeholder data. Once confirmed, your module is activated with a single update - no rebuild required.

To discuss a partner slot, please get in touch via the contact details provided separately.

---

## Departure

**22 May 2026 - Bournemouth, UK**

---

*Bitcycle Iteration 1 · Built with Cloudflare Pages, Workers, and KV · Bitcoin-native from the ground up*


