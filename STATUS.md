# RideLane — loop status

_Generated 2026-10-06 02:00:42 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## PLAN

**Phase 1 goal: an update running on his phone.** Plan of record: `PLAN.md`.

| milestone | state | proof id | blocker |
|---|---|---|---|
| **M1a** staging redeploy ACTIVE | **DONE** | deploy `b08f1358` · health 200 `commit=e9698534dd4c` `bootedAt=2026-10-06T04:27:26Z` · CRM 200 | — |
| **M1b** Stripe TEST key | **DONE (Path B, D-20)** | `stripeMode=test` · `/api/stripe/config` pk_test_ acct `51QY4ZQCxi29dqjf` | restricted-key dialog won't render; using the test secret key |
| **M1c** staging store for realtime | **DONE** | `persistence=redis` `ping=1ms` · engine.io handshake on `/socket.io/` · redis:7-alpine internal, `basic-xxs` **$5/mo** | — |
| **M1d** boot-completeness CI step | **PR OPEN** | `ridelane-api#571` `cd88aea9` · **`boot-env` SUCCESS in CI** · 6 boots: 1 completeness + 5 necessity controls · drilled both ways · **SO-43** mirrors it onto the staging spec (`8c37174`) | reviewer verdict; stacked on #569 |
| **Safety** `CRM_BASE_URL` fail closed | **PR OPEN, ALL CHECKS GREEN** | `ridelane-api#569` `4e6312be` · **FOUR** fallbacks, not two — `index.ts` and `employeeRoutes.ts:88` build the EMAILED invite/reset urls · 10/10 at head · class gate counts the literal per file · `ride-chat-sockets` + `test` SUCCESS | reviewer verdict |
| **M2** EAS walk green on staging ×3 | NOT STARTED | UNKNOWN | M1 |
| **M3** OTA to build 12's runtime | NOT STARTED | UNKNOWN | M2 |
| **M4** his booking's R-number in Dispatch | NOT STARTED | UNKNOWN | M3 |
| *(parallel)* A7 chat server half | DISPATCHED to API | UNKNOWN | none — staging store is live |

**Live:** `https://ridelane-staging-mgvis.ondigitalocean.app` — api on `ridelane-api@staging` `e9698534`, crm on `jrax-admin@staging` `0c605d2e`, **redis:7-alpine store, engine.io handshake proved on `/socket.io/`** (the "in-memory, no socket until M1c" note that stood here was stale the moment M1c landed).

**Done and carried in:** `ridelane-staging` `36db9a85` created at $10/mo ·
production unchanged (`ridelane-api` `835c47ae`, `monkfish-app` `13cbce10`) ·
token containment `POST /v2/droplets` → 403 · first-deploy root cause fixed in
`e0fd45c`.

**Cost:** staging $10/mo + store $5/mo = **$15/mo** (cap: $10 + up to $15).

**Frozen until M4:** no new standing orders; no loop-infra work unless it blocks
M1–M4; DRIVER and CRM sessions paused.

**Instruments fixed tonight, each drilled both ways:** SO-41 called four committed
test fixtures a leaked private key the moment a worktree of that repo sat under a
scanned root — a header is not a key, and a scanner that cries wolf on fixtures
gets ignored when it catches the real `.pem` · SO-20 can now retire an id that
can never be acked (closed PR, paused session), derived not curated, with the
count surfaced — my first rule hid two LIVE work items and was narrowed · SO-43
added and wired at birth · `sync-v4.sh` with no arguments no longer publishes
nothing and exits 0, which is how check-so's own SO-43 fix briefly looked shipped
while the running loop read a copy 2KB older.

## Heartbeat

- probe heartbeat: 2s ago
- last pass: 2026-10-06 01:54:48 TRIGGER cause=state-change NOT RUN -- lock held 54s
- notifier last ran: 2m ago

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
| ridelane-api | #571 | `cd88aea97f67` | 8 total, 0 failed | **none** | 10 |
| ridelane-api | #570 | `32dd9504fc4b` | 7 total, 0 failed | YES | 41 |
| ridelane-api | #569 | `4e6312beea10` | 7 total, 0 failed | YES | 51 |
| ridelane-api | #568 | `8dae9431e2c9` | 7 total, 1 failed | YES | 527 |
| ridelane-api | #565 | `6a82a645c61a` | 7 total, 1 failed | YES | 1214 |
| ridelane-api | #562 | `4cd691581aa1` | 7 total, 0 failed | YES | 1286 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 17463 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 17885 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 28767 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 11701 |

## Last standing-orders run

```
(from the last pass, 0m ago)
NOTE: breaking a stale check-so lock (116s, holder 69122 not alive).
PASS   SO-1  an [HOURLY] is on his page: 2417:**[HOURLY] 15:13 EDT, 27 Sep — the first one ever p
PASS   SO-2  every open PR has a verdict at its current head
PASS   SO-3  all 5 build link(s) named by content
PASS   SO-4  every CLAIMS row carries an artifact id
PASS   SO-5  blocking list stated and scoped
PASS   SO-6  FOUNDER-DEFECTS.md touched 25m ago
PASS   SO-7  CLAIMS: zero OTAs published — none can target an unposted runtime
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 107m ago
PASS   SO-11 no author over the WIP limit
PASS   SO-12 no approved PR sitting dirty
PASS   SO-13 no open PR was pushed after its approval
UNPROV SO-14 labelling clean, but builds-list.yml exists in 0/2 app repos -- BATCHING half unprovable
PASS   SO-15 reviewer session active 3m ago (13099 lines)
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
PASS   SO-17 3 ask(s), all [MONEY] or [PHONE-OPTIONAL] -- no legwork on his page
FAIL   SO-18 board 72m stale -- it is an hourly board
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 his page calls a STILL-OPEN PR held without a money citation: 2809:- **(b)** "held" really is reserved for money, and `#562` should 
PASS   SO-22 advisor live: ADV ran 13m ago, 111 ruling(s), file 241m old
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:17 (#279,#278,#277,...)  pax:17 (#100,#98,#96,...) -- a run that was created is not a publish (AR-7)
FAIL   SO-20 id(s) dispatched >20m ago and never acknowledged: QI-A7-CLIENT-0929(PASSENGER,221m) QI-BOOKINGS-UNBLOCKED(PASSENGER,221m) QI-BUILD12-0929(PASSENGER,221m) QI-BUILD12-RUN(PASSENGER,221m) QI-CHAT-TWIN-BUILD(PASSENGER,221m) QI-FD13-0929(PASSENGER,221m) QI-FD13-0929-B(PASSENGER,221m) QI-FD14-REAL(PASSENGER,221m) QI-PLACES-FIXTURE-ON(PASSENGER,221m) [4 retired as unackable -- see state/retired-ids.tsv for the reason on each]
PASS   SO-24 heartbeat 24s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-CRM-0158.md(4p/0t) out-PAX-0142.md(10p/11t) out-CRM-0142.md(4p/0t)
PASS   SO-26 every queue's newest item cites an FD/phase/QI/AR id
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
PASS   SO-28 nightly section present on the page (page 72m old)
PASS   SO-29 page states AUTOPILOT: NOT YET PROVED -- no unproved claim is being made
PASS   SO-33 notifier ran 1m ago; 38 event(s) delivered to date
PASS   SO-34 public mirror pushed 0m ago (raw.githubusercontent.com/jrabson777/ridelane-status/main/STATUS.md)
PASS   SO-35 control plane intact: 7 files present, lib.sh matches the committed copy, 6/6 sessions have transcripts
PASS   SO-37 dispatch loop sees 6/6 session rows and all 6 queue files exist
PASS   SO-38 no loop script sources the scratchpad; pass.log grew 0m ago
FAIL   SO-39 PR(s) with an EXPECTED CHECK ABSENT (reads green, was never run): ridelane-api#565 -- a missing check is a failing one
PASS   SO-41 6 remote(s) checked, none carries userinfo; 0 private-key bodies in publishable paths
UNPROV SO-43 all 5 boot-required name(s) ARE bound by the spec (11 keys), but the
---
FAILS: 6   (UNPROV is not a pass and not counted as a fail)
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
