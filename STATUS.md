# RideLane — loop status

_Generated 2026-10-05 05:00:57 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## Heartbeat

- probe heartbeat: 6s ago
- last pass: 2026-10-05 04:59:48   -> pass SKIPPED (lock held by a real pass)
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
|  **FD-17**  |  **The quote gate says 6 passengers and enforces 14**  |  **IN-PR** — open, not merged, not published  |
|  **FD-18**  |  **A driver goes invisible when the phone is backgrounded or locked**  |  **IN-PR, BLOCKED — DISPATCH-CRITICAL**  |
|  **FD-19**  |  **Beyond 600 miles the customer is told "prices unavailable, try again" and no lead reaches the CRM**  |  **OPEN**  |

## Open PRs, verdict at head

| repo | pr | head | checks | verdict at head | age (m) |
|---|---|---|---|---|---|
| ridelane-api | #564 | `f39245d717ec` | 7 total, 0 failed | **none** | 20 |
| ridelane-api | #563 | `4ae54bfa19f5` | 7 total, 0 failed | **none** | 21 |
| ridelane-api | #562 | `4cd691581aa1` | 0 total, 0 failed | **none** | 31 |
| ridelane-api | #560 | `85536297f823` | 0 total, 0 failed | **none** | 135 |
| ridelane-api | #557 | `42415e49d2af` | 0 total, 0 failed | **none** | 340 |
| ridelane-api | #517 | `42e34e5b3515` | 0 total, 0 failed | **none** | 16208 |
| ridelane-api | #505 | `e1d9243859bf` | 0 total, 0 failed | **none** | 16630 |
| ridelane-api | #459 | `b648529c23b3` | 0 total, 0 failed | **none** | 27511 |
| ridelane-passenger-app | #98 | `27a9002bfaae` | 3 total, 0 failed | **none** | 20 |
| ridelane-passenger-app | #97 | `c58551c6ba8d` | 3 total, 0 failed | YES | 95 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 10446 |
| jrax-driver-app | #271 | `7f188e0e7e77` | 3 total, 0 failed | **none** | 34 |
| jrax-driver-app | #267 | `8a19f2c5ca21` | 3 total, 0 failed | **none** | 347 |

## Last standing-orders run

```
FAIL   SO-1  no [HOURLY] on his page
FAIL   SO-2  3 open PRs >60m with no verdict at head: api#560, api#557, app#267
PASS   SO-3  no build links on the page
PASS   SO-4  every CLAIMS row carries an artifact id
FAIL   SO-5  no scoped blocking list on his page
FAIL   SO-6  FOUNDER-DEFECTS.md untouched 93m
FAIL   SO-7  CLAIMS table has no OTA updates row
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 142m ago
FAIL   SO-11 over WIP limit: api:5 — next item is a review, not a new PR
PASS   SO-12 no approved PR sitting dirty
PASS   SO-13 no open PR was pushed after its approval
UNPROV SO-14 labelling clean, but builds-list.yml exists in 0/2 app repos -- BATCHING half unprovable
PASS   SO-15 reviewer session active 10m ago (10892 lines)
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
FAIL   SO-17 no '## OPEN ASKS' section -- an unstructured page cannot be checked
FAIL   SO-18 no five-row board on his page
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 declared-held PR(s) citing neither D-n nor #474: ridelane-api#562,ridelane-api#246
PASS   SO-22 advisor live: ADV ran 23m ago, 109 ruling(s), file 293m old
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:15 (#268,#265,#262,...)  pax:18 (#96,#95,#92,...) -- a run that was created is not a publish (AR-7)
PASS   SO-20 every dispatched id has been acknowledged in a handback
FAIL   SO-24 heartbeat 723s old -- the loop has STOPPED, not gone quiet
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-REV-0503.md(0p/0t) out-DRV-0450.md(71p/0t)
PASS   SO-26 every queue's newest item cites an FD/phase/QI/AR id
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
UNPROV SO-28 before 07:00; the nightly has not been due yet
FAIL   SO-29 the page neither states AUTOPILOT: NOT YET PROVED nor carries a window table -- silence reads as a claim
FAIL   SO-33 notifier last ran 15m ago, over the 10m line -- the channel to the founder is going quiet
FAIL   SO-34 mirror 15m stale, over the 5m line -- the advisor is reading a dead page
FAIL   SO-35 control-plane verifier 14m stale
PASS   SO-37 dispatch loop sees 6/6 session rows and all 6 queue files exist
PASS   SO-38 no loop script sources the scratchpad; pass.log grew 0m ago
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

**EAS cloud runs: 0.** `ridelane-passenger-app#96` (the walk ported to
Maestro) merged at `f1a02e4b` on 5 Oct after review APPROVE at `d2de3c5a`.
**A merge is not a run** -- the flows have never executed against the app.

They cannot yet, deliberately: the EAS workflow declares an `api_url` input
and never consumes it, so a twin resolves its api base from the `e2e-test`
profile, which inherits the **preview** environment -- production. W10 and
W11 both tap the booking CTA. The trigger refuses to dispatch until that
input is wired, and stops refusing on its own once it is. The target it
needs is STG-1, which does not exist yet.

## OTA

| update id | commit | proving walk id |
|---|---|---|
| — | — | **no OTA has been published** |
