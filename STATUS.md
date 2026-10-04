# RideLane — loop status

_Generated 2026-10-04 05:37:52 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## Heartbeat

- probe heartbeat: 4s ago
- last pass: 2026-10-04 05:36:47 PASS cause=state-change prev=f9cbca45 now=7b912c07
- notifier last ran: 1m ago

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
|  **FD-4**  |  "no light theme"  |  **MERGED AND PROVEN ON THE SIMULATOR TWIN**, not on a device build. Walk screenshots `FD4-account-light-pt.png` / `FD4-account-dark-pt.png`: same screen, bone-on-dark-text vs near-black-on-light-text — it genuinely changes. He tested build 11, which predates the screen conversions  |
|  **FD-5**  |  "no route line / miles / breakdown on map"  |  **OPEN**  |
|  **FD-6**  |  "wrong install link delivered — Sep 16 build 2 sent as build 8"  |  **ANSWERED — awaiting his install**  |
|  **FD-7**  |  "the app does not tell him which build/update he is running"  |  **PROVEN** — the twin's account screen reads `RIDELANE · 0.2.0 (1) · embedded`, not a fabricated update id  |
|  **FD-8**  |  runtime-version audit  |  **IN-PR — blocks the next OTA. Build 2 and build 8 are ORPHANED BY DESIGN: nothing publishes to runtime `0.2.0` again.**  |
|  **FD-9**  |  "after installing passenger build 10, it still shows **Tampa Bay** as an area — no areas, cities, neighborhoods or zones; a result must have a **physical address**"  |  **MERGED `#536` 15:12 Mon AND LIVE** — running api is 19 commits past the merge  |
|  **FD-10**  |  "I CAN'T CHANGE TIME !!! STILL STATIC" — the schedule sheet's `6 40 AM` time wheel does not move **+ 15-min increments only (founder, 28 Sep): the minute column offers :00 :15 :30 :45 and nothing else, matching the website**  |  **FOUNDER-CONFIRMED** on build 11, 29 Sep — he reported the wheel works  |
|  **FD-11**  |  **Every customer booking email carries a FAKE phone number.** `[REDACTED-PHONE]` is hardcoded in the live v3 templates  |  **MERGED `#537` 17:03 Mon** — verify the footer prints no New York address  |
|  **FD-13**  |  **REGRESSION on build 11: "Tap to pay" says payment is not available and the booking cannot complete.** Build 10 booked; build 11 does not  |  **MERGED (`#90` + `#91`), PROVEN ON NO BUILD.** The 30 Sep walk stopped at W8; **W9/W10/W11 — the booking spine — have no artefact.** Build 12 is correctly still gated  |
|  **FD-4**  |  Theme does not change on build 11  |  **OPEN (tokens merged, nothing visible)**  |
|  **FD-14**  |  The confirm card's total does not equal its own breakdown  |  **OPEN — scoped**  |
|  **FD-15**  |  **The server stored a different total than the customer was shown**  |  **OPEN — BLOCKS PAYMENT**  |

## Open PRs, verdict at head

| repo | pr | head | checks | verdict at head | age (m) |
|---|---|---|---|---|---|
| ridelane-api | #552 | `8eec76465ef4` | 5 total, 0 failed | **none** | 187 |
| ridelane-api | #551 | `33254f1b34c3` | 5 total, 0 failed | **none** | 188 |
| ridelane-api | #550 | `d0c17a400068` | 5 total, 0 failed | **none** | 206 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 14805 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 15227 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 26108 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 9043 |
| jrax-driver-app | #260 | `f6e5908d1419` | 2 total, 0 failed | **none** | 208 |

## Last standing-orders run

```
FAIL   SO-1  no [HOURLY] on his page
FAIL   SO-2  4 open PRs >60m with no verdict at head: api#552, api#551, api#550, app#260
PASS   SO-3  no build links on the page
FAIL   SO-4  7 CLAIMS row(s) without an id
FAIL   SO-5  no scoped blocking list on his page
FAIL   SO-6  FOUNDER-DEFECTS.md untouched 250m
FAIL   SO-7  CLAIMS table has no OTA updates row
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 6157m ago
PASS   SO-11 no author over the WIP limit
PASS   SO-12 no approved PR sitting dirty
PASS   SO-13 no open PR was pushed after its approval
UNPROV SO-14 labelling clean, but builds-list.yml exists in 0/2 app repos -- BATCHING half unprovable
FAIL   SO-15 reviewer session idle 190m -- over the 60m line
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
FAIL   SO-17 no '## OPEN ASKS' section -- an unstructured page cannot be checked
FAIL   SO-18 no five-row board on his page
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 declared-held PR(s) citing neither D-n nor #474: ridelane-api#246
FAIL   SO-22 ADV idle 223m, over the 30m line -- the loop cannot see its advisor
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:20 (#259,#258,#257,...)  pax:19 (#92,#91,#90,...) -- a run that was created is not a publish (AR-7)
PASS   SO-20 every dispatched id has been acknowledged in a handback
PASS   SO-24 heartbeat 77s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-CRM-0218.md(9p/5t) out-DRV-0218.md(44p/0t) out-REV-0627.md(1p/0t) out-REV-0214.md(0p/0t)
PASS   SO-26 every queue's newest item cites an FD/phase/QI/AR id
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
UNPROV SO-28 before 07:00; the nightly has not been due yet
FAIL   SO-29 the page neither states AUTOPILOT: NOT YET PROVED nor carries a window table -- silence reads as a claim
PASS   SO-33 notifier ran 2m ago; 9 event(s) delivered to date
PASS   SO-34 public mirror pushed 3m ago (raw.githubusercontent.com/jrabson777/ridelane-status/main/STATUS.md)
FAIL   SO-35 CONTROL PLANE BROKEN:PAX:silent-196m DRV:silent-188m REV:silent-189m ADV:silent-222m API:silent-186m CRM:silent-187m -- the loop can report green while this is true, which is how three days were lost
PASS   SO-37 dispatch loop sees 6/6 session rows and all 6 queue files exist
---
FAILS: 15   (UNPROV is not a pass and not counted as a fail)
```

## LOOP-ALERTS, tail

```
```
