# Wingmates — Project Plan

*Your flights, your spots, your crew.*

A free social app for avgeeks, built by an avgeek: log the flights you take and
the planes you spot, follow friends, and see them live on the map while they fly.
See user-reported and current aviation news. All in one place, on any phone.

---

## The problem

Aviation apps are each good at one piece of the hobby. Avgeeks end up using one app
to log flights, another to track them, another to spot planes, plus news sites and
general social media to share and keep up.

| Need | Today | What's missing |
|---|---|---|
| Flight log and stats | Flighty, Jumpseat, myFlightradar24 | Flighty is Apple-only; importing flights older than a year needs Pro ($59.99/yr). Jumpseat is iPhone-only. |
| Friends' flights and stats | Flighty Friends, Jumpseat | Can't open a friend's profile to see their map, stats, or shared routes. |
| Spotting log | Skycards, Aviatter, spreadsheets | Kept separate from your flights and from live data. Friends features feel shallow. |
| Aviation news | News sites, Reddit, X | Scattered, and not tied to the airports, airlines, or flights you care about. |

**The gap:** no free app connects flights you take, planes you spot, your friends,
and the news around them, on both Android and iPhone. Wingmates competes on
**integration**, not on features that are missing everywhere else.

---

## What users say

From Reddit aviation communities and App Store reviews, Nov 2025 – Oct 2026.

- "No android version is why I haven't paid for lifetime." — Flighty user, Apr 2026
- "Now why can't I see my friends' maps? The same planes we've been on? Our common routes?" — Flighty user, May 2026
- "I really really really wish we could click on their profiles and see their flight maps and flight stats" — Flighty user, Jun 2026
- "I still don't know what the value is in having friends in this game" — Skycards user, May 2026
- "The only thing I'd love to see is some sort of integration with the likes of FR24" — spotter, Apr 2026

**Strongest needs:** richer friend profiles and stats, Android support, spotting
tied to live data, and easier flight history.

**Counterpoint:** some users prefer minimal social features, and parents worry
about kids and chat. So social is optional, private by default, and there are no DMs.

---

## Features

| Feature | What it does | Version |
|---|---|---|
| Profile | Photo, home airport, flight map, stats | v1 |
| Flights | Add past and future flights by flight number + date, or by hand | v1 |
| Friends | Mutual follows; open a friend's flight map | v1 (stats in week 2) |
| **Live friends map** | Friends in the air, with their photo on their plane | v1 |
| **News feed** | Aviation headlines from news sites, plus live alerts like ground stops and delays | v1 |
| **User reports** | Users post what they see: diversions, delays, rare visitors, airport news. Tagged by airport or flight. | v1 (basic), v2 (upvotes, trending) |
| Spotting | Photo + registration, rarity tag, "what's near me now?" | v2 |
| Friend comparisons | Shared routes, airports, and planes you've both been on | v2 |
| Achievements | Countries, airports, aircraft types, miles, rare catches | v2 |
| Notifications | "Your friend just took off", alerts for your home airport | v2 |
| Out | DMs, app store apps, paid features | — |

**Privacy:** flights are friends-only by default, live position only shows to
friends while in the air, and any flight or post can be hidden.

---

## Data sources (all free)

| Need | Source |
|---|---|
| Live positions | adsb.fi (1 request/sec, tested), OpenSky as backup |
| Flight number → route | BTS on-time data for US flights (tested), manual entry for the rest |
| Flight number → callsign | OpenFlights airline codes |
| News headlines | RSS feeds from aviation news sites, showing headline, source, and link |
| Live alerts | FAA NAS Status (ground stops, delays), aviationweather.gov |
| Spotting | adsb.fi nearby search, plane-alert-db for rarity, Planespotters photos |
| Airports and maps | OurAirports, OpenFreeMap + MapLibre |

---

## How it works

**Stack:** Next.js on Vercel, Supabase (database, storage, realtime, scheduled jobs).
Installable web app, so it works on Android and iPhone for $0.

- **Live map:** every minute, a job checks flights that should be in the air, looks
  them up on adsb.fi, and pushes positions to friends' maps.
- **News:** a job pulls RSS feeds and FAA alerts every 15 minutes into one feed,
  next to user reports. Users can filter by their airports and airlines.
- **Adding a flight:** "UA 1234, Nov 20" → route from BTS → user confirms → saved.

---

## Roadmap

| Dates | Build |
|---|---|
| **Now → Nov 3** | Publish proposal. Set up Supabase and Vercel. |
| **Nov 10–17 (v1)** | Profiles, flights, friends, live map, news feed, basic user reports. |
| **Nov 17–24** | Spotting, stats on friend profiles. |
| **Nov 24 → Dec 1 (v2)** | Comparisons, achievements, notifications, trending reports. Polish for the fair. |

**Build first:** flight number → live position on the map. It's the riskiest part.

**Focus:** Holistic Journey — sign up → add a flight → add a friend → see them on
the map → read and post news.

---

## Risks

| Risk | Plan |
|---|---|
| Too many features | v1 is flights, friends, live map, and news. The rest waits. |
| Flight number doesn't match the plane (codeshares) | BTS carrier mapping, or pick the plane from a nearby list |
| False or spammy user reports | Tie reports to an airport or flight, let users flag them, show the source |

---

## Competitors

| App | Platform | Overlap |
|---|---|---|
| Flighty | Apple only | Flight log, friends, stats |
| Jumpseat | iPhone only | Social flight log, photos. Closest competitor. |
| Skycards | iPhone, Android | Spotting card game with friends |
| Aviatter | iPhone | Spotting log with a social feed |
| myFlightradar24 | Web | Flight log and stats |
| Simple Flying, AeroTime | Web | Aviation news only |

**Where Wingmates fits:** the only free app with flights, spotting, friends, and
news together, on Android and iPhone.

---

## Sources

- adsb.fi: https://github.com/adsbfi/opendata
- OpenSky: https://openskynetwork.github.io/opensky-api/rest.html
- BTS on-time data: https://transtats.bts.gov/PREZIP/
- FAA NAS Status: https://nasstatus.faa.gov/
- plane-alert-db: https://github.com/sdr-enthusiasts/plane-alert-db
- Flighty: https://apps.apple.com/us/app/1358823008
- Jumpseat: https://apps.apple.com/us/app/jumpseat-social-flight-log/id6757955101
- App in the Air shutdown: https://alternativeto.net/news/2024/9/app-in-the-air-to-shut-down-on-september-19-2024-users-advised-to-export-their-data-now
- User quotes: Reddit aviation communities and App Store reviews, Nov 2025 – Oct 2026
