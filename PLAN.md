# Contrails (working name) — Plan (working draft)

> Working notes for the proposal, not the proposal itself. The brief requires the
> proposal page to be in your own words and informed by your user interviews.
> Items marked **(verify)** are assumptions to confirm before relying on them.
> Research below was checked on Oct 31, 2026.

## One line

A free social app for avgeeks, built by an avgeek: log the flights you take and
the planes you spot, follow friends, and see them live on the map while they fly.
All in one place, and on any phone.

---

## The problem

Avgeeks spread their hobby across many apps, and the good parts usually cost money
or only work on iPhone.

| What avgeeks want | Where it lives today | What's wrong |
|---|---|---|
| Log past and future flights, stats | Flighty, My Flight Path, myFlightradar24 | Flighty is **iPhone-only** and puts flights older than 365 days behind Pro ($60/yr). myFlightradar24 is reportedly no longer updated. |
| See friends' flights live | Flighty Friends, Jumpseat, My Flight Path | Jumpseat is iPhone-only with paid tiers. None of them include spotting. |
| Log and share spotted planes | Aviatter, Squawk, AeroNatics, Skycards | Separate apps. Skycards (the biggest) has no friends list, and users keep asking for one. |
| Show off photos | JetPhotos, Instagram, Reddit, Discord | Not tied to your flight history or stats |
| Complain or celebrate about a flight | X, Instagram stories, group chats | Lost in general social media, with no flight context |
| Replacement for App in the Air | — | **Shut down Sept–Oct 2024.** Users moved to TripIt or Flighty. |

**The gap:** no free app combines *flights I take* and *planes I spot* in one
social profile that works on both Android and iPhone.

**Check with interviews:** whether people actually want one app for this, or are
happy with separate ones. See "User interviews" below.

---

## Features

| Feature | What it does | Version |
|---|---|---|
| Profile | Photo, home airport, bio, headline stats, **dream destinations** | v1 (dream destinations in v2) |
| Previous flights | Add by flight number + date, or pick airports by hand. Map of all your routes. | v1 |
| Future flights | Upcoming trips, shared with friends | v1 |
| Friends | Follow requests, mutual friends only | v1 |
| **Live friends map** | Friends currently in the air, with **their profile photo on their plane** | v1 |
| Flying feed | Posts tied to a flight ("AA delayed again..."), with a live status and cause chip attached automatically | v1 (basic), v2 (auto cause chips) |
| Spotting feed | Photo + aircraft registration, rarity tag, airport. From friends and the wider community. | v2 |
| Achievements + stats | Countries, airports, airlines, aircraft types, miles, rare catches. Badges like "World Traveler", "Rare catch: B-52", "10 A380s". | v2 |
| Import history | CSV import from other trackers' exports | v2 **(verify each app's export format)** |
| Notifications | "Your friend just took off", "Friend landing at ORD in 20 min" | v2 |
| Out (for now) | Rare-aircraft "look up" alerts, native app store apps, messaging/DMs, paid anything |

### Privacy (decide this up front)
Future flights show when someone's home is empty.
- Each flight is **friends-only by default**, never public or searchable.
- Live position is shown only to approved friends, and only while in the air.
- Any flight or post can be hidden.
- Spotting posts can be public. Flying posts default to friends.

---

## Data sources

### Live flight tracking (friends on the map)
| Source | Use | Limit / cost | Status |
|---|---|---|---|
| **adsb.fi open data** | Find a friend's plane by callsign (`/v2/callsign/UAL1234`) and update it every minute | Free, **1 request/sec**, personal non-commercial use, must credit adsb.fi with a link | Tested: works, no key |
| **OpenSky Network** | Backup for live positions | 4,000 credits/day with a free account | Tested: works |
| **OpenFlights airlines list** | Turn a flight number into the callsign planes broadcast: "UA 1234" → "UAL1234" | Free download | Tested: has UA→UAL, OO→SKW |

### Turning "flight number + date" into a route
| Source | Use | Limit / cost | Status |
|---|---|---|---|
| **BTS on-time data, marketing-carrier version** | Usual origin, destination and times for every US domestic flight number. Also maps codeshares: "UA 5432" is flown by SkyWest. | Free monthly CSV, ~2 months behind | Tested on Aug 2026: 673k flights, 8 airlines |
| **OpenSky flight history** | Actual departure and arrival airports for recent flights, by callsign | Free account needed | Returned 403 without an account; retest with one |
| **AeroDataBox** | Exact schedule for a future or international flight, once per flight added | Free tier ~700 calls/month | **(verify)** limit and whether flight status is in the free tier |
| **Manual entry** | International or older flights: pick airports, airline, aircraft type | — | Always available as a fallback |
| ~~adsbdb~~ | **Don't use for routes.** Matched only ~1 in 4 live flights in our test. | — | Tested: unreliable |

### Spotting
| Source | Use | Limit / cost | Status |
|---|---|---|---|
| **adsb.fi nearby** (`/v3/lat/../lon/../dist/..`) | "What's near me now?", so users can tag what they just photographed | Same 1 req/sec | Tested: 149 aircraft near ORD |
| **plane-alert-db** (GitHub) | Rarity tags: military, government, historic, special paint schemes, firefighting... | Free, 17,276 aircraft | Tested |
| **adsb.fi `/v2/mil`** | All military aircraft being tracked right now | Same limit | Tested |
| **OpenSky aircraft database** | Registration → type, operator | Free download | — |
| **FAA aircraft registry** | US planes: owner, year built | Free download | — |
| **Planespotters.net photo API** | A photo of any aircraft by hex code, with credit to the photographer | Free. Each request must say who you are, with a contact URL or email. | Tested: works with that requirement |
| **User uploads** | Spotting photos | Supabase Storage (1 GB free) | Compress before uploading |

### Context for the flying feed (v2)
| Source | Use |
|---|---|
| **FAA NAS Status** | Ground stops and delay programs: "DFW ground stop, thunderstorms" |
| **aviationweather.gov** | Weather at the airport |
| **BTS on-time data** | "This flight is late 40% of the time" |

### Reference data (load once)
| Source | Use |
|---|---|
| **OurAirports** | Airport search, coordinates, country (for "countries visited" and miles) |
| **OpenFlights airlines list** | Airline names, IATA/ICAO codes |
| **OpenFreeMap + MapLibre** | Free map tiles, no key |

---

## How it works

```
                 ┌──────────────────── Supabase ─────────────────────┐
 adsb.fi  ──►    │ pg_cron ─► Edge Fn: track-active-flights (1/min)    │
 OpenSky (backup)│            only flights in the air right now        │
                 │ pg_cron ─► monthly: import BTS → route_lookup        │
                 │                                                     │
                 │ Postgres: profiles, friendships, flights, positions, │
                 │   posts, spots, aircraft, rare_aircraft, airports,   │
                 │   achievements, dream_destinations                   │
                 │ Storage: profile + spotting photos                   │
                 │ Realtime: live friend positions → map                │
                 └──────────────────────────┬─────────────────────────┘
                                            ▼
                ┌──────────── Vercel (Next.js, installable web app) ───┐
                │ Pages: feed, map, profile, add flight, spot, friends │
                └──────────────────────────────────────────────────────┘
```

**Adding a flight:** enter "UA 1234, Nov 20" → look it up in `route_lookup` (from
BTS) → user confirms or edits the airports and times → saved.

**Live map:** every minute, a job finds flights scheduled to be in the air now
(departure − 1 h to arrival + 2 h), looks up each callsign on adsb.fi about 1 second
apart, saves the position, and pushes it to friends' maps with Supabase Realtime.
At class scale (a few dozen flights at once) this stays far under the limits.

**Posting a spot:** take or upload a photo → "what's near me?" suggests aircraft →
pick one, or type a registration → rarity from plane-alert-db → posted to feed.

**Achievements:** computed from your own data: countries from OurAirports, miles
from airport coordinates, types from the aircraft database, rare catches from
plane-alert-db.

### Data model (first pass)
- `profiles` — id, username, photo, home_airport, bio
- `friendships` — user_a, user_b, status (`pending | accepted`)
- `flights` — id, user_id, airline, flight_number, callsign, date, origin, dest, sched_dep, sched_arr, aircraft_type, registration, visibility, status (`upcoming | in_air | landed`)
- `flight_positions` — flight_id, ts, lat, lon, alt, speed, heading (kept only while in the air)
- `posts` — id, user_id, kind (`flying | spotting`), flight_id?, spot_id?, text, photo, created_at
- `spots` — id, user_id, registration, hex, type, airport, taken_at, photo, rarity_category
- `aircraft` — hex, registration, type, operator (from the downloads)
- `rare_aircraft` — from plane-alert-db
- `route_lookup` — marketing airline, flight number, origin, dest, usual times, operating airline/callsign (from BTS)
- `airports`, `airlines`
- `achievements` — user_id, badge, earned_at
- `dream_destinations` — user_id, airport or city

---

## Focus

**Holistic Journey (likely pick):** sign up → add a flight → add a friend → see them
on the map → post. It touches every part of the course and doesn't need AI.

Alternative: **Design**, if the main goal is a polished profile, map and feed.

---

## Roadmap

| Dates | Build |
|---|---|
| **Now → Nov 3** | Interview 3+ avgeeks. Make a free OpenSky account. Write and publish the proposal page. |
| **Nov 10–17 (v1)** | Sign-up and profile, add past and future flights (BTS lookup + manual entry), friends, live friends map with profile photos, simple flying feed. Deploy. Get 3 real users. |
| **Nov 17–24** | Spotting posts and feed, rarity tags, aircraft photos, stats page. |
| **Nov 24 → Dec 1 (v2)** | Achievements and badges, dream destinations, feed cause chips (FAA status, weather), notifications, import. Polish for the fair. |
| **Out** | Rare-aircraft "look up" alerts, App Store / Play Store apps, DMs, worldwide schedule data. |

**Riskiest part, build first:** flight number → callsign → live position on the map.
Test it on a real flight in the first two days.

**Fair demo:** add a classmate's real flight beforehand, or replay a recorded one if
nobody is flying that day.

---

## Distribution and cost

| Option | Cost | Decision |
|---|---|---|
| **Installable web app (PWA)** | **$0** | **Use this.** Works on Android and iPhone ("Add to Home Screen"). Push notifications work on Android and on iPhone (iOS 16.4+) once installed. |
| Google Play | $25 one-time | Later. New personal accounts need a 12-tester, 14-day closed test first **(verify)**. |
| Apple App Store | $99/year | Later, if ever |

Working on Android from day one is a selling point: Flighty and Jumpseat are iPhone-only.

### Free-tier budget
| Service | Free limit | Our use |
|---|---|---|
| Vercel Hobby | Non-commercial | Website and API |
| Supabase | 500 MB database, 1 GB storage, 500k function calls/month, Realtime **(verify connection limit)** | ~43k scheduled runs/month |
| adsb.fi | 1 request/sec | One call per friend in the air, once a minute |
| OpenSky | 4,000 credits/day | Backup only |
| AeroDataBox | ~700 calls/month **(verify)** | One call per flight added, v2 |
| Resend (email) | ~100/day | Friend requests, v2 |

Set usage alerts on every service. No payment methods.

---

## Tools for building

- **Supabase CLI + MCP** — database changes, Edge Functions, checking data
- **Vercel CLI** — deploys, environment variables, logs
- **GitHub CLI** — repo, PRs
- **Playwright MCP** — test the feed, map and profile in a real browser
- **Docs lookup MCP (e.g. Context7)** — current docs for Supabase, MapLibre, Next.js

---

## User interviews (before Nov 3)

Talk to 3+ avgeeks. Don't describe the app until the end.
1. "Tell me about the last flight you took. How did you track it, and who did you tell?"
2. "How do you keep a record of flights you've taken? Show me."
3. "Tell me about the last plane you spotted. What did you do with the photo?"
4. "Which aviation apps do you use, and which do you pay for? What made you pay?"
5. "When a friend is flying, how do you follow along?"

Signs it's worth building: they use 3+ apps, they pay for something they'd rather
not, they're on Android and miss Flighty, or they share spots in a group chat.

---

## Risks

| Risk | Fallback |
|---|---|
| Flight number → callsign doesn't match (codeshares, regionals) | BTS operating-carrier mapping, then let the user pick the plane from a list near the airport |
| adsb.fi is down or blocks shared Supabase addresses | OpenSky backup, or slower polling |
| No free schedule data for international flights | Manual entry, filled in on the day from live data |
| Scope: this is many features | v1 = flights + friends + live map. Spotting and badges wait for v2. |
| Few users at launch | Seed with classmates and avgeek friends from interviews |
| Photo storage fills 1 GB | Compress to ~300 KB, limit uploads per user |
| Privacy mistakes | Friends-only defaults, hide flights after landing, test with a second account |

---

## Competitors (to try before the proposal)

| App | Platform | Overlap | Free? |
|---|---|---|---|
| **My Flight Path** | Web | Closest: flight log, stats, badges, friends airborne on a map | Price not stated **(verify)** |
| **Flighty** | iPhone only (no Android plans) | Flight log, Flighty Friends, Passport stats | Mostly free; older history needs Pro ($60/yr) |
| **Jumpseat** | iPhone only | Social flight log, friends' upcoming flights | Free with paid tiers |
| **Aviate, byAir** | Android (byAir also iPhone) | Flighty-style tracking on Android | Free + Pro |
| **Skycards** | iPhone, Android | Spotting as a card game, airport leaderboards, no friends | Free |
| **Aviatter, Squawk, AeroNatics** | iPhone | Spotting logs with some social | Free / freemium |
| **myFlightradar24** | Web | Flight log and stats | Free, reportedly no longer updated |

### Sources
- adsb.fi API and terms: https://github.com/adsbfi/opendata
- OpenSky REST API: https://openskynetwork.github.io/opensky-api/rest.html
- BTS on-time data (monthly files): https://transtats.bts.gov/PREZIP/
- plane-alert-db: https://github.com/sdr-enthusiasts/plane-alert-db
- Planespotters photo API: https://www.planespotters.net/photo/api
- OpenFlights data: https://github.com/jpatokal/openflights
- OurAirports: https://ourairports.com/data/
- My Flight Path: https://myflightpath.club/
- Flighty (App Store): https://apps.apple.com/us/app/1358823008
- Flighty Android waitlist: https://flighty.com/android-waitlist
- Jumpseat: https://apps.apple.com/us/app/jumpseat-social-flight-log/id6757955101
- Aviate on Android: https://9to5google.com/2026/07/27/aviate-androids-answer-to-flighty-is-now-available-to-download/
- byAir and Aviate review: https://androidauthority.com/i-tried-two-flighty-alternatives-android-3696341
- Skycards: https://www.flightradar24.com/blog/flight-tracking-news/just-for-fun/skycards-collectible-aviation-card-game/
- App in the Air shutdown: https://alternativeto.net/news/2024/9/app-in-the-air-to-shut-down-on-september-19-2024-users-advised-to-export-their-data-now
