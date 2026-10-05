# RideLane — loop status

_Generated 2026-10-05 01:58:01 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## Heartbeat

- probe heartbeat: 7s ago
- last pass: 2026-10-05 01:47:44 PASS cause=idle-floor-10m prev=60e570b0 now=60e570b0
- notifier last ran: 5m ago

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
|  **FD-17**  |  **The quote gate says 6 passengers and enforces 14**  |  **OPEN**  |
|  **FD-18**  |  **A driver goes invisible when the phone is backgrounded or locked**  |  **OPEN — DISPATCH-CRITICAL**  |
|  **FD-19**  |  **Beyond 600 miles the customer is told "prices unavailable, try again" and no lead reaches the CRM**  |  **OPEN**  |

## Open PRs, verdict at head

| repo | pr | head | checks | verdict at head | age (m) |
|---|---|---|---|---|---|
| ridelane-api | #559 | `55bcaeb36ef6` | 7 total, 0 failed | **none** | 53 |
| ridelane-api | #558 | `52a25bcffe6f` | 6 total, 0 failed | **none** | 54 |
| ridelane-api | #557 | `6c12229f1efb` | 5 total, 0 failed | YES | 157 |
| ridelane-api | #556 | `d53cf66c24b0` | 5 total, 0 failed | YES | 162 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 16025 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 16447 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 27329 |
| ridelane-passenger-app | #96 | `51e44972345b` | 3 total, 1 failed | YES | 113 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 10263 |
| jrax-driver-app | #267 | `480b624ad010` | 3 total, 0 failed | YES | 164 |
| jrax-driver-app | #261 | `8b83110103f9` | 3 total, 0 failed | YES | 1038 |
| jrax-driver-app | #260 | `0f65527a0194` | 3 total, 0 failed | **none** | 1428 |

## Last standing-orders run

```
FAIL   SO-1  no [HOURLY] on his page
FAIL   SO-2  1 open PRs >60m with no verdict at head: app#260
PASS   SO-3  no build links on the page
FAIL   SO-4  7 CLAIMS row(s) without an id
FAIL   SO-5  no scoped blocking list on his page
FAIL   SO-6  FOUNDER-DEFECTS.md untouched 177m
FAIL   SO-7  CLAIMS table has no OTA updates row
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 97m ago
PASS   SO-11 no author over the WIP limit
PASS   SO-12 no approved PR sitting dirty
FAIL   SO-13 1 pushed after APPROVE:  jrax-driver-app#260 approved 6e2240b126f6 but head is 0f65527a0194; 
FAIL   SO-14 2 native PR(s) with no [native] in the title:  jrax-driver-app#261 touches app.config.js with no [native] in the title;  jrax-driver-app#260 touches app.config.js with no [native] in the title; 
PASS   SO-15 reviewer session active 6m ago (10253 lines)
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
FAIL   SO-17 no '## OPEN ASKS' section -- an unstructured page cannot be checked
FAIL   SO-18 no five-row board on his page
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 declared-held PR(s) citing neither D-n nor #474: ridelane-api#246
PASS   SO-22 advisor live: ADV ran 1m ago, 109 ruling(s), file 98m old
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:18 (#268,#265,#262,...)  pax:19 (#95,#92,#91,...) -- a run that was created is not a publish (AR-7)
PASS   SO-20 every dispatched id has been acknowledged in a handback
PASS   SO-24 heartbeat 103s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-ADV-0126.md(1p/0t) out-REV-0114.md(7p/0t) out-API-0111.md(6p/8t)
PASS   SO-26 every queue's newest item cites an FD/phase/QI/AR id
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
UNPROV SO-28 before 07:00; the nightly has not been due yet
FAIL   SO-29 the page neither states AUTOPILOT: NOT YET PROVED nor carries a window table -- silence reads as a claim
PASS   SO-33 notifier ran 0m ago; 10 event(s) delivered to date
FAIL   SO-34 mirror 8m stale, over the 5m line -- the advisor is reading a dead page
PASS   SO-35 control plane intact: 7 files present, lib.sh matches the committed copy, 6/6 sessions have transcripts
PASS   SO-37 dispatch loop sees 6/6 session rows and all 6 queue files exist
PASS   SO-38 no loop script sources the scratchpad; pass.log grew 1m ago
FAIL   SO-39 PR(s) with an EXPECTED CHECK ABSENT (reads green, was never run): jrax-driver-app#260 -- a missing check is a failing one
PASS   SO-41 6 remote(s) checked, none carries userinfo; 0 private-key bodies in publishable paths
---
FAILS: 16   (UNPROV is not a pass and not counted as a fail)
```

## LOOP-ALERTS, tail

```
```

## WALKS

| run id | repo | commit | result | failed step |
|---|---|---|---|---|
| `37204201794` | jrax-driver-app | `e54e07a2` | FAIL | no jobs created — reusable workflow uncallable (Actions access=none) |
| `37204417084` | jrax-driver-app | `4711ffef` | FAIL | Build the .app — '' is not a workspace file (pods not installed) |
| `37205943775` | jrax-driver-app | `e833efc2` | FAIL | no jobs created — error parsing called workflow (YAML block ended early) |
| `37223229178` | jrax-driver-app | `07e65a5d` | FAIL | log not retained — class unknown |
| `37223723681` | jrax-driver-app | `3189ad83` | FAIL | Build the .app — no device matching destination (Xcode 16.4) |
| `37224581375` | jrax-driver-app | `07e65a5d` | FAIL | Build the .app — ExpoModulesCore Swift errors (SDK vs Xcode 16.4) |
| `37230349450` | jrax-driver-app | `07e65a5d` | FAIL | Build the .app — sentry-cli needs an organization |
| `37231443545` | jrax-driver-app | `07e65a5d` | FAIL | Prove the twin — guard asserted the impossible (production host is a source fallback) |
| `37232686444` | jrax-driver-app | `8e157399` | FAIL | Prove the twin — bundle lacked localhost:4010 (export died at the step boundary) |
| `37257186190` | jrax-driver-app | `8e157399` | GREEN (evidence wrong) | all steps passed; both screenshots were byte-identical SPLASH frames |
| `37259006809` | jrax-driver-app | `92db0032` | FAIL | Boot the simulator and install — hung, hit the 60-minute timeout |

## OTA

| update id | commit | proving walk id |
|---|---|---|
| — | — | **no OTA has been published** |
