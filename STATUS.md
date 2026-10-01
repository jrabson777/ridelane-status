# RideLane — loop status

_Generated 2026-09-30 21:02:37 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## Heartbeat

- probe heartbeat: 48s ago
- last pass: 2026-09-30 20:49:32 PASS cause=state-change prev=f4eac87e now=214477de
- notifier last ran: 0m ago

## Phase board

| id | item | state | gate |
|---|---|---|---|
| **A5** | driver lifecycle: accept → en route → arrived → complete | in progress | a seeded driver is assignable; `/me` reports `dispatchEligible` |
| **A7** | **rider ↔ driver chat** (this order, 29 Sep) | **inventory done: [A7-INVENTORY.md](A7-INVENTORY.md). Row 4: NOT one root (`dt_*` driver inbox vs `thr_*` CRM inbox); ride = filter over the driver's one thread; no rider participant** | a message crosses apps in < 2s and survives a cold start |
| **A6** | push notifications | not started | **after A7** — chat is the first consumer that makes push mean anything |


## Founder defect rows

|  **FD-1**  |  "Apple Pay opened, nothing completed"  |  **OPEN**  |
|  **FD-2**  |  "autocomplete returns cities — typing *Tampa* returns the city Tampa"  |  **MERGED (api half) / IN-PR (clients)**  |
|  **FD-3**  |  "schedule time not editable"  |  **OPEN**  |
|  **FD-4**  |  "no light theme"  |  **OPEN**  |
|  **FD-5**  |  "no route line / miles / breakdown on map"  |  **OPEN**  |
|  **FD-6**  |  "wrong install link delivered — Sep 16 build 2 sent as build 8"  |  **ANSWERED — awaiting his install**  |
|  **FD-7**  |  "the app does not tell him which build/update he is running"  |  **IN-PR**  |
|  **FD-8**  |  runtime-version audit  |  **IN-PR — blocks the next OTA. Build 2 and build 8 are ORPHANED BY DESIGN: nothing publishes to runtime `0.2.0` again.**  |
|  **FD-9**  |  "after installing passenger build 10, it still shows **Tampa Bay** as an area — no areas, cities, neighborhoods or zones; a result must have a **physical address**"  |  **MERGED `#536` 15:12 Mon AND LIVE** — running api is 19 commits past the merge  |
|  **FD-10**  |  "I CAN'T CHANGE TIME !!! STILL STATIC" — the schedule sheet's `6 40 AM` time wheel does not move **+ 15-min increments only (founder, 28 Sep): the minute column offers :00 :15 :30 :45 and nothing else, matching the website**  |  **MERGED `#79` (wheel, 01:03 Mon) + `#82` (quarter-hour slots, 17:25 Mon
|  **FD-11**  |  **Every customer booking email carries a FAKE phone number.** `[REDACTED-PHONE]` is hardcoded in the live v3 templates  |  **MERGED `#537` 17:03 Mon** — verify the footer prints no New York address  |
|  **FD-13**  |  **REGRESSION on build 11: "Tap to pay" says payment is not available and the booking cannot complete.** Build 10 booked; build 11 does not  |  **ORDER 0 — DISPATCHED**  |
|  **FD-4**  |  Theme does not change on build 11  |  **OPEN (tokens merged, nothing visible)**  |

## Open PRs, verdict at head

| repo | pr | head | checks | verdict at head | age (m) |
|---|---|---|---|---|---|
| ridelane-api | #548 | `654160c4fc62` | 5 total, 0 failed | **none** | 36 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 9970 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 10392 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 21273 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 4208 |

## Last standing-orders run

```
PASS   SO-1  an [HOURLY] is on his page: 2450:**[HOURLY] 15:13 EDT, 27 Sep — the first one ever p
PASS   SO-2  every open PR has a verdict at its current head
PASS   SO-3  all 6 build link(s) named by content
FAIL   SO-4  7 CLAIMS row(s) without an id
PASS   SO-5  blocking list stated and scoped
FAIL   SO-6  FOUNDER-DEFECTS.md untouched 2601m
PASS   SO-7  CLAIMS: zero OTAs published — none can target an unposted runtime
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 1321m ago
PASS   SO-11 no author over the WIP limit
PASS   SO-12 no approved PR sitting dirty
PASS   SO-13 no open PR was pushed after its approval
UNPROV SO-14 labelling clean, but builds-list.yml exists in 0/2 app repos -- BATCHING half unprovable
PASS   SO-15 reviewer session active 15m ago (8343 lines)
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
PASS   SO-17 3 ask(s), all [MONEY] or [PHONE-OPTIONAL] -- no legwork on his page
FAIL   SO-18 board 785m stale -- it is an hourly board
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 declared-held PR(s) citing neither D-n nor #474: ridelane-api#246
PASS   SO-22 advisor live: ADV ran 15m ago, 104 ruling(s), file 16m old
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:18 (#253,#252,#251,...)  pax:19 (#92,#91,#90,...) -- a run that was created is not a publish (AR-7)
PASS   SO-20 every dispatched id has been acknowledged in a handback
PASS   SO-24 heartbeat 103s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-REV-2046.md(5p/0t) out-DRV-1951.md(50p/0t)
FAIL   SO-26 queue item(s) with no FD or phase-board id: REVIEWER
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
PASS   SO-28 nightly section present on the page (page 785m old)
PASS   SO-29 page states AUTOPILOT: NOT YET PROVED -- no unproved claim is being made
PASS   SO-33 notifier ran 0m ago; 7 event(s) delivered to date
---
FAILS: 7   (UNPROV is not a pass and not counted as a fail)
```

## LOOP-ALERTS, tail

```

**[WATCHDOG 20:46]** no orchestrator pass in 25 minutes — launching one.

**[HEARTBEAT 20:55 EDT]** **The orchestrator has not completed a turn in 6832 minutes.** Work may be stalled; the cause is not known from here. If this repeats, the loop is not running.

**[HEARTBEAT 21:02 EDT]** **PAX session idle 15 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.

**[HEARTBEAT 21:02 EDT]** **DRV session idle 15 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.

**[HEARTBEAT 21:02 EDT]** **API session idle 15 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.

**[HEARTBEAT 21:02 EDT]** **CRM session idle 15 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.
```
