# Wingmates — Project Plan

> Planning notes for the proposal. The proposal page itself must be in my own words
> and informed by user interviews. Items marked **(verify)** still need a check
> before I rely on them. Research checked Oct 31, 2026.

## Name

**Wingmates** — the app is about the people you fly and spot with, not just the
planes. It's short, easy to say, and signals "social" and "aviation" at once.
Tagline: *Your flights, your spots, your crew.*

Backups if the name is taken: **Contrails**, **Tailspotters**, **Jetset**.
**(verify)** no existing aviation app or domain conflicts before the proposal.

## One line

A free social app for avgeeks, built by an avgeek: log the flights you take and
the planes you spot, follow friends, and see them live on the map while they fly.
All in one place, on any phone.

---

## The problem

Existing aviation apps are good at their piece of the hobby. The problem is that
the hobby is **split across many apps**: one for logging flights, one for live
tracking, one for spotting, and general social media for sharing. Enthusiasts keep
asking for richer social profiles, history they can compare with friends, live data
tied to their spotting logs, and a way to share aviation memories in context.

| What avgeeks want | Where it lives today | What's missing |
|---|---|---|
| Log past and future flights, stats | Flighty, My Flight Path, myFlightradar24, Jumpseat | Flighty is **Apple-only**; importing flights older than 365 days is a Pro feature ($59.99/yr). Already-imported flights stay viewable after Pro ends. |
| See friends' flights and stats | Flighty Friends, Jumpseat, My Flight Path | Flighty Friends shows live flights but not friends' maps or stats. Jumpseat is iPhone-only with paid tiers. |
| Log and share spotted planes | Skycards, Aviatter, Squawk, AeroNatics, spreadsheets | Skycards has friends and battles, but users say friends add little value. Aviatter has a social feed. Spotting is kept separate from the flights you take. |
| Spotting tied to live data | Flightradar24 + a separate log | Spotters ask for live-tracking integration with their logs. |
| Show off photos | JetPhotos, Instagram, Reddit, Discord | Not tied to the aircraft, registration, or your history. Jumpseat links trip photos, but only for flights you take. |
| Complain or celebrate about a flight | X, Instagram stories, group chats | No flight context attached. Plausible gap, least validated. |
| Replacement for App in the Air | — | App distribution ended **Sept 19, 2024**; service and data export ended **Oct 19, 2024**. Some users still miss it. |

### The gap

No free app connects **flights I take** and **planes I spot** in one social profile,
with friends you can actually compare with, on both Android and iPhone.

Wingmates doesn't claim these features are absent elsewhere. Its pitch is
**integration**: one connected aviation community instead of five apps.

### Positioning

> Aviation enthusiasts use a fragmented mix of flight trackers, spotting databases,
> photo-sharing platforms, and social networks. Individual apps cover parts of this,
> but users keep asking for richer social profiles, historical comparisons, live
> spotting integration, and ways to share their aviation memories. Wingmates brings
> these into one connected aviation community.

Three connected experiences to prioritize:
1. **A personal history** of flights taken and planes spotted.
2. **A friends feed with meaningful comparisons** (shared routes, same aircraft, stats).
3. **Posts tied to a specific flight, registration, or airport.** The most
   distinctive idea, and the least validated, so it gets tested in interviews.

---

## Evidence from users (2025–2026)

Direct comments from Reddit aviation communities and App Store reviews.

| # | Date | Source | Quote | What it shows |
|---|---|---|---|---|
| 1 | Apr 4, 2026 | Reddit (Flighty) | "No android version is why I haven't paid for lifetime." | Platform lock-in blocks paying users |
| 2 | Nov 28, 2025 | Reddit (Flighty) | "The free tier gave me 1 year of import, and I upgraded to Pro because I thought I needed it for unlimited historical import." | Historical import paywall pushes upgrades |
| 3 | May 30, 2026 | Reddit (Flighty) | "Now why can't I see my friends' maps? The same planes we've been on? Our common routes?" | Demand for social comparison |
| 4 | Jun 28, 2026 | Reddit (Flighty) | "I really really really wish we could click on their profiles and see their flight maps and flight stats" | Demand for rich profiles |
| 5 | Mar 9, 2026 | Reddit (Skycards) | "Chat with friends. It would build community" | Spotting apps want deeper social |
| 6 | May 12, 2026 | Reddit (Skycards) | "I still don't know what the value is in having friends in this game" | A friends list alone isn't enough |
| 7 | Jan 21, 2026 | Reddit (spotting) | "Is there a go to app or do I continue to use spreadsheets?" | No obvious home for a lifetime spotting log |
| 8 | Apr 2, 2026 | Reddit (spotting) | "The only thing I'd love to see is some sort of integration with the likes of FR24" | Spotting logs want live data |
| 9 | Jun 14, 2026 | App Store (Skycards) | "I thought you could catch airplanes by capturing a real photo of them." | Users expect real photos in spotting |
| 10 | Oct 11, 2026 | Reddit (JetPhotos) | "if not, ill make it cool and dramatic for my instagram" | Database photos vs. creative sharing are split |
| 11 | Sep 6, 2026 | Reddit | "For logging, I still miss App in the Air. I use Flighty now." | App in the Air left a lasting gap |

**Strongest five for the proposal:** #1, #3, #4, #6, #8.

### How strong is the evidence?

Qualitative read of the comments above, not a survey or market size.

| Need | Support |
|---|---|
| Richer social profiles and stats | Strong |
| Works on any platform | Strong |
| Live tracking tied to spotting logs | Strong |
| Easier historical flight logging | Strong |
| Photo-based spotting and sharing | Moderate |
| Flight-specific complaints and celebrations | Limited |

### Counterpoints

- Some Flighty users (June 2026) said they **prefer** its minimal social features.
- A Skycards parent worried about **exposing kids to chat**.

So social features must be **optional and private by default**. This shapes the
privacy rules below, and is why DMs are out of scope.

---

## Features

| Feature | What it does | Version |
|---|---|---|
| Profile | Photo, home airport, bio, headline stats, flight map, dream destinations | v1 (dream destinations in v2) |
| Previous flights | Add by flight number + date, or pick airports by hand. Map of all your routes. | v1 |
| Future flights | Upcoming trips, shared with friends | v1 |
| Friends | Follow requests, mutual friends only | v1 |
| **Friend profiles and comparisons** | Open a friend's profile to see their map and stats, plus **shared routes, airports, and aircraft you've both flown** | v1 (profiles), v2 (comparisons) |
| **Live friends map** | Friends currently in the air, with **their profile photo on their plane** | v1 |
| Flying feed | Posts tied to a flight ("AA delayed again..."), with live status and a cause chip attached automatically | v1 (basic), v2 (cause chips) |
| Spotting feed | Photo + registration, rarity tag, airport, live data on what was overhead. From friends and the community. | v2 |
| Achievements + stats | Countries, airports, airlines, aircraft types, miles, rare catches. Badges like "World Traveler", "Rare catch: B-52", "10 A380s". | v2 |
| Import history | Free, unlimited CSV import from other trackers | v2 **(verify each app's export format)** |
| Notifications | "Your friend just took off", "Friend landing at ORD in 20 min" | v2 |
| Out (for now) | Rare-aircraft "look up" alerts, app store apps, messaging/DMs, paid anything | — |

### Privacy

Future flights show when someone's home is empty, and not everyone wants social.
- Each flight is **friends-only by default**, never public or searchable.
- Live position is shown only to approved friends, and only while in the air.
- Any flight or post can be hidden. Social features can be ignored entirely; the
  app still works as a private log.
- Spotting posts can be public. Flying posts default to friends.
- No direct messages.

---

## Data sources

### Live flight tracking (friends on the map)
| Source | Use | Limit / cost | Status |
|---|---|---|---|
| **adsb.fi open data** | Find a friend's plane by callsign (`/v2/callsign/UAL1234`) and update it every minute | Free, **1 request/sec**, personal non-commercial use, must credit adsb.fi with a link | Tested: works, no key |
| **OpenSky Network** | Backup for live positions | 4,000 credits/day with a free account | Tested: works |
| **OpenFlights airlines list** | Turn a flight number into the broadcast callsign: "UA 1234" → "UAL1234" | Free download | Tested: has UA→UAL, OO→SKW |

### Turning "flight number + date" into a route
| Source | Use | Limit / cost | Status |
|---|---|---|---|
| **BTS on-time data, marketing-carrier version** | Usual origin, destination and times for every US domestic flight number. Also maps codeshares: "UA 5432" is flown by SkyWest. | Free monthly CSV, ~2 months behind | Tested on Aug 2026: 673k flights, 8 airlines |
| **OpenSky flight history** | Actual departure and arrival airports for recent flights, by callsign | Free account needed | Returned 403 without an account; retest with one |
| **AeroDataBox** | Exact schedule for a future or international flight, once per flight added | Free tier ~700 calls/month | **(verify)** limit and whether flight status is included |
| **Manual entry** | International or older flights: pick airports, airline, aircraft type | — | Always available as a fallback |
| ~~adsbdb~~ | **Don't use for routes.** Matched only ~1 in 4 live flights in testing. | — | Tested: unreliable |

### Spotting
| Source | Use | Limit / cost | Status |
|---|---|---|---|
| **adsb.fi nearby** (`/v3/lat/../lon/../dist/..`) | "What's near me now?", so users can tag what they just photographed | Same 1 req/sec | Tested: 149 aircraft near ORD |
| **plane-alert-db** (GitHub) | Rarity tags: military, government, historic, special liveries, firefighting | Free, 17,276 aircraft | Tested |
| **adsb.fi `/v2/mil`** | All military aircraft tracked right now | Same limit | Tested |
| **OpenSky aircraft database** | Registration → type, operator | Free download | — |
| **FAA aircraft registry** | US planes: owner, year built | Free download | — |
| **Planespotters.net photo API** | A photo of any aircraft by hex code, credited to the photographer | Free. Requests must identify the app with a contact URL or email. | Tested: works with that requirement |
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

**Friend comparisons:** join two users' flights on route, airport, and
registration/type to show "routes you've both flown" and "planes you've both been on".

**Achievements:** computed from your own data: countries from OurAirports, miles
from airport coordinates, types from the aircraft database, rare catches from
plane-alert-db.

### Data model
- `profiles` — id, username, photo, home_airport, bio
- `friendships` — user_a, user_b, status (`pending | accepted`)
- `flights` — id, user_id, airline, flight_number, callsign, date, origin, dest, sched_dep, sched_arr, aircraft_type, registration, visibility, status (`upcoming | in_air | landed`)
- `flight_positions` — flight_id, ts, lat, lon, alt, speed, heading (kept only while in the air)
- `posts` — id, user_id, kind (`flying | spotting`), flight_id?, spot_id?, text, photo, visibility, created_at
- `spots` — id, user_id, registration, hex, type, airport, taken_at, photo, rarity_category
- `aircraft` — hex, registration, type, operator (from the downloads)
- `rare_aircraft` — from plane-alert-db
- `route_lookup` — marketing airline, flight number, origin, dest, usual times, operating airline/callsign (from BTS)
- `airports`, `airlines`
- `achievements` — user_id, badge, earned_at
- `dream_destinations` — user_id, airport or city

---

## Focus

**Holistic Journey:** sign up → add a flight → add a friend → see them on the map →
compare profiles → post. It touches every part of the course and doesn't need AI.

Alternative: **Design**, if the main goal is a polished profile, map and feed.

---

## Roadmap

| Dates | Build |
|---|---|
| **Now → Nov 3** | Interview 3+ avgeeks. Make a free OpenSky account. Write and publish the proposal page. |
| **Nov 10–17 (v1)** | Sign-up and profile, add past and future flights (BTS lookup + manual entry), friends and friend profiles, live friends map with profile photos, simple flying feed. Deploy. Get 3 real users. |
| **Nov 17–24** | Spotting posts and feed, rarity tags, aircraft photos, stats page, friend comparisons. |
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

Working on Android from day one is a selling point: Flighty and Jumpseat are Apple-only.

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

Online comments show the frustrations exist. Interviews check the one thing they
don't: **do people want these combined in one app?**

Talk to 3+ avgeeks. Don't describe the app until the end.
1. "Tell me about the last flight you took. How did you track it, and who did you tell?"
2. "How do you keep a record of flights you've taken? Show me."
3. "Tell me about the last plane you spotted. What did you do with the photo?"
4. "Which aviation apps do you use, and which do you pay for? What made you pay?"
5. "When a friend is flying, how do you follow along?"
6. "Have you ever wanted to compare your flights or spots with a friend's?"
7. (After describing the app) "Would you want this in one app, or keep using separate ones? What would you want kept private?"

**Signs it's worth building:** they use 3+ apps, pay for something they'd rather
not, are on Android and miss Flighty, share spots in a group chat, or want to see
friends' stats.

**Signs to rethink:** they're happy with separate apps, or don't want social at all.

---

## Risks

| Risk | Fallback |
|---|---|
| Users don't want flights and spotting combined | Interviews first; keep the app useful as a private log, social optional |
| Jumpseat or Flighty add the same features | Compete on Android support, free history, and spotting, which they don't cover |
| Flight number → callsign doesn't match (codeshares, regionals) | BTS operating-carrier mapping, then let the user pick the plane from a list near the airport |
| adsb.fi is down or blocks shared Supabase addresses | OpenSky backup, or slower polling |
| No free schedule data for international flights | Manual entry, filled in on the day from live data |
| Scope: this is many features | v1 = flights + friends + live map. Spotting and badges wait for v2. |
| Few users at launch | Seed with classmates and avgeek friends from interviews |
| Photo storage fills 1 GB | Compress to ~300 KB, limit uploads per user |
| Privacy mistakes | Friends-only defaults, hide flights after landing, test with a second account |

---

## Competitors

| App | Platform | Overlap | Price |
|---|---|---|---|
| **My Flight Path** | Web | Closest: flight log, stats, badges, friends airborne on a map | **(verify)** |
| **Flighty** | Apple only (Android waitlist) | Flight log, Flighty Friends, Passport stats | Free; historical import beyond 365 days needs Pro ($59.99/yr) |
| **Jumpseat** | iPhone only | Social flight log, live tracking, trip photos, sharing. Most direct competitor. | Free with paid tiers |
| **Aviate, byAir** | Android (byAir also iPhone) | Flighty-style tracking on Android | Free + Pro |
| **Skycards** | iPhone, Android | Spotting as a card game, friends and battles, airport leaderboards | Free |
| **Aviatter** | iPhone | Spotting log with friends, sightings feed, photo posts | Free / freemium |
| **Squawk, AeroNatics** | iPhone | Spotting logs | Free / freemium |
| **myFlightradar24** | Web | Flight log and stats | Free; back online Oct 26, 2026 after maintenance |
| **App in the Air** | — | Was the go-to flight log | Shut down Oct 2024 |

**Where Wingmates fits:** the only one combining flights taken + planes spotted +
friend comparisons, free, on Android and iPhone.

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
- User quotes: Reddit aviation communities (r/flighty, Skycards, spotting, JetPhotos threads) and App Store reviews, Nov 2025 – Oct 2026. **(verify)** save direct links to each quote before the proposal.
