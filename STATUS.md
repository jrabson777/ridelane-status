# RideLane — loop status

_Generated 2026-10-06 00:28:15 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## PLAN

**Phase 1 goal: an update running on his phone.** Plan of record: `PLAN.md`.

| milestone | state | proof id | blocker |
|---|---|---|---|
| **M1a** staging redeploy ACTIVE | **DONE** | deploy `b08f1358` · health 200 `commit=e9698534dd4c` `bootedAt=2026-10-06T04:27:26Z` · CRM 200 | — |
| **M1b** Stripe TEST restricted key | WAITING ON FOUNDER | UNKNOWN (`stripeMode=unknown` now) | he signs in at dashboard.stripe.com |
| **M1c** staging store for realtime (≤ +$15/mo) | NOT STARTED | UNKNOWN | price the options first |
| **M1d** boot-completeness CI step | NOT STARTED | UNKNOWN | none |
| **Safety** `rbac.ts:50` fail closed on `CRM_BASE_URL` | NOT STARTED | UNKNOWN | none |
| **M2** EAS walk green on staging ×3 | NOT STARTED | UNKNOWN | M1 |
| **M3** OTA to build 12's runtime | NOT STARTED | UNKNOWN | M2 |
| **M4** his booking's R-number in Dispatch | NOT STARTED | UNKNOWN | M3 |
| *(parallel)* A7 chat server half | NOT STARTED | UNKNOWN | M1c — no store ⇒ no socket |

**Live:** `https://ridelane-staging-mgvis.ondigitalocean.app` — api on `ridelane-api@staging` `e9698534`, crm on `jrax-admin@staging` `0c605d2e`, in-memory store (no socket until M1c).

**Done and carried in:** `ridelane-staging` `36db9a85` created at $10/mo ·
production unchanged (`ridelane-api` `835c47ae`, `monkfish-app` `13cbce10`) ·
token containment `POST /v2/droplets` → 403 · first-deploy root cause fixed in
`e0fd45c`.

**Frozen until M4:** no new standing orders; no loop-infra work unless it blocks
M1–M4; DRIVER and CRM sessions paused.


## Heartbeat

- probe heartbeat: 69s ago
- last pass: 2026-10-06 00:27:12 TRIGGER cause=state-change NOT RUN -- lock held 11s
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
|  **FD-17**  |  **The quote gate says 6 passengers and enforces 14**  |  **MERGED — not published, not device-proved**  |
|  **FD-18**  |  **A driver goes invisible when the phone is backgrounded or locked**  |  **IN-PR, STILL BLOCKED — DISPATCH-CRITICAL**  |
|  **FD-19**  |  **Beyond 600 miles the customer is told "prices unavailable, try again" and no lead reaches the CRM**  |  **OPEN**  |

## Open PRs, verdict at head

| repo | pr | head | checks | verdict at head | age (m) |
|---|---|---|---|---|---|
| ridelane-api | #568 | `8dae9431e2c9` | 7 total, 1 failed | YES | 431 |
| ridelane-api | #565 | `6a82a645c61a` | 7 total, 1 failed | YES | 1118 |
| ridelane-api | #562 | `4cd691581aa1` | 7 total, 0 failed | YES | 1190 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 17367 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 17789 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 28671 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 11605 |
| jrax-driver-app | #266 | `541b9b65f261` | 4 total, 0 failed | YES | 1898 |

## Last standing-orders run

```
(from the last pass, 1m ago)
NOTE: breaking a stale check-so lock (121s, holder 45741 not alive).
PASS   SO-1  an [HOURLY] is on his page: 2417:**[HOURLY] 15:13 EDT, 27 Sep — the first one ever p
PASS   SO-2  every open PR has a verdict at its current head
PASS   SO-3  all 5 build link(s) named by content
PASS   SO-4  every CLAIMS row carries an artifact id
PASS   SO-5  blocking list stated and scoped
PASS   SO-6  FOUNDER-DEFECTS.md touched 31m ago
PASS   SO-7  CLAIMS: zero OTAs published — none can target an unposted runtime
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 13m ago
PASS   SO-11 no author over the WIP limit
PASS   SO-12 no approved PR sitting dirty
PASS   SO-13 no open PR was pushed after its approval
UNPROV SO-14 labelling clean, but builds-list.yml exists in 0/2 app repos -- BATCHING half unprovable
PASS   SO-15 reviewer session active 0m ago (12824 lines)
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
PASS   SO-17 3 ask(s), all [MONEY] or [PHONE-OPTIONAL] -- no legwork on his page
PASS   SO-18 5 rows, written 22m ago, no status ahead of its artifact
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 his page calls a STILL-OPEN PR held without a money citation: 2809:- **(b)** "held" really is reserved for money, and `#562` should 
PASS   SO-22 advisor live: ADV ran 4m ago, 111 ruling(s), file 147m old
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:16 (#279,#278,#277,...)  pax:18 (#100,#98,#96,...) -- a run that was created is not a publish (AR-7)
FAIL   SO-20 id(s) dispatched >20m ago and never acknowledged: QI-DRV-ACK-NOW(DRIVER,125m) QI-FD18-PRESENCE(DRIVER,127m) QI-A7-CLIENT-0929(PASSENGER,127m) QI-BOOKINGS-UNBLOCKED(PASSENGER,127m) QI-BUILD12-0929(PASSENGER,127m) QI-BUILD12-RUN(PASSENGER,127m) QI-CHAT-TWIN-BUILD(PASSENGER,127m) QI-FD13-0929(PASSENGER,127m) QI-FD13-0929-B(PASSENGER,127m) QI-FD14-REAL(PASSENGER,127m) QI-PLACES-FIXTURE-ON(PASSENGER,127m) AR-54(REVIEWER,127m) QI-CHAT-REV-1004-C(REVIEWER,127m) QI-REV-557(REVIEWER,127m) QI-REV-97(REVIEWER,127m) QI-REV-98(REVIEWER,127m)
PASS   SO-24 heartbeat 23s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-REV-0025.md(1p/0t) out-PAX-0020.md(10p/10t) out-DRV-0020.md(18p/7t)
PASS   SO-26 every queue's newest item cites an FD/phase/QI/AR id
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
PASS   SO-28 nightly section present on the page (page 22m old)
PASS   SO-29 page states AUTOPILOT: NOT YET PROVED -- no unproved claim is being made
PASS   SO-33 notifier ran 1m ago; 37 event(s) delivered to date
PASS   SO-34 public mirror pushed 0m ago (raw.githubusercontent.com/jrabson777/ridelane-status/main/STATUS.md)
PASS   SO-35 control plane intact: 7 files present, lib.sh matches the committed copy, 6/6 sessions have transcripts
PASS   SO-37 dispatch loop sees 6/6 session rows and all 6 queue files exist
PASS   SO-38 no loop script sources the scratchpad; pass.log grew 0m ago
PASS   SO-39 every expected check is present as a check run on the open PRs
PASS   SO-41 6 remote(s) checked, none carries userinfo; 0 private-key bodies in publishable paths
---
FAILS: 4   (UNPROV is not a pass and not counted as a fail)
```

## LOOP-ALERTS, tail

```

**[WATCHDOG 01:13]** no orchestrator pass in 43 minutes — launching one.

**[HEARTBEAT 01:22 EDT]** **The orchestrator has not completed a turn in 29852962 minutes.** Work may be stalled; the cause is not known from here. If this repeats, the loop is not running.

**[HEARTBEAT 01:42 EDT]** **PAX session idle 22 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.

**[HEARTBEAT 01:42 EDT]** **DRV session idle 22 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.

**[HEARTBEAT 01:42 EDT]** **API session idle 22 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.

**[HEARTBEAT 01:42 EDT]** **CRM session idle 22 minutes** with items queued. Nothing is being worked in that repo until it is dispatched.
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
