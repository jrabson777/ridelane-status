# RideLane — loop status

_Generated 2026-10-09 05:29:10 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## PLAN

**Phase 1 goal: an update running on his phone.** Plan of record: `PLAN.md`.

| milestone | state | proof id | blocker |
|---|---|---|---|
| **M1a** staging redeploy ACTIVE | **DONE** | deploy `b08f1358` · health 200 `commit=e9698534dd4c` `bootedAt=2026-10-06T04:27:26Z` · CRM 200 | — |
| **M1b** Stripe TEST key | **DONE (Path B, D-20)** | `stripeMode=test` · `/api/stripe/config` pk_test_ acct `51QY4ZQCxi29dqjf` | restricted-key dialog won't render; using the test secret key |
| **M1c** staging store for realtime | **DONE** | `persistence=redis` `ping=1ms` · engine.io handshake on `/socket.io/` · redis:7-alpine internal, `basic-xxs` **$5/mo** | — |
| **M1d** boot-completeness CI step | **PR OPEN, GREEN, RETARGETED TO `master`** | `ridelane-api#571` `cd88aea9` (head unchanged) · 8/8 SUCCESS · 6 boots: 1 completeness + 5 necessity controls · **SO-43** mirrors it onto the staging spec | reviewer verdict |
| **Safety** `CRM_BASE_URL` fail closed | **MERGED** `d0f4d0b2` | `ridelane-api#569` on `VERDICT: APPROVE 4e6312be…` at the exact head · **FOUR** fallbacks, not two — `index.ts` and `employeeRoutes.ts:88` build the EMAILED invite/reset urls · **production DID deploy and is healthy** — master auto-deploys; production booted `d0f4d0b2` at 06:14:19Z, `nodeEnv=production`, hydrated, 184 bookings, Redis up, a distance lookup succeeding 06:35:23Z. I first wrote "not deployed" from a check taken three minutes after the merge; that was too early · follow-up `#572` closes the evasion the reviewer found in my own gate | — |
| **M2** EAS walk green on staging ×3 | **WIRING MERGED; NO RUN STARTED** | `ridelane-passenger-app#101` **MERGED** `7f48d35a` on `VERDICT: APPROVE b1ebd81f…` at the exact head — the reviewer verified the EAS Precedence table independently · follow-up `#102` refuses a blank `api_url` on the EAS worker (measured: unset → **production**, `""` → broken, so that job cannot reach production because it always *sets* the var) | **founder: is an EAS e2e build a "new native build" (hard stop) or inside the approved $100/mo cap?** · someone with `EXPO_TOKEN` must confirm `OTP_TEST_*` exist in the job's EAS `preview` environment |
| **M3** OTA to build 12's runtime | **PUBLISH SOURCE PREPARED; BUILD 12'S REAL RUNTIME NOW KNOWN** | `pax#78` merged (`39c82d9b`) and I dispatched it: **build 12 is `appBuildVersion 12`, profile `preview`, `isForIosSimulator: false`, runtime **`a0b43caeaf16610e19c9735c1b164c88df8c5123`** — EAS's own number, computed with the real Maps secret. Locally (one dummy key held constant) `ca4304ec` and `ca4304ec + main's JS` resolve IDENTICALLY, while `main` differs — so branch `ota/build12-runtime-js-only` `cf9d11f` should resolve to `a0b43cae…` in CI and be accepted. 30/30 gates, 289 tests, tsc and lint clean on it. Rollback target recorded: the embedded bundle. | **founder: may I publish?** · the absolute match is still CI's to confirm — my local numbers are relative, and `eas-update.yml` resolves with the real secret |
| **M4** his booking's R-number in Dispatch | NOT STARTED | UNKNOWN | M3 |
| **D-17** a binary on his phone | **BUILD 12 IS CUT AND INSTALLABLE** | run `37179820368` from `ca4304ec`, 4 Oct: *"Shipping CFBundleVersion: 12 (prior: 11)"*, *"Build is safe to install"*, GMSApiKey asserted in the shipped `.ipa` · install link on his page · **his page said "NEVER CUT" for two days; corrected** | he installs it |
| **FD-15 / FD-14** money correctness | **FD-14 IS LIVE — and its test passes** | measured on the twin: Fare **$89.10** + Tax **$5.35** = $94.45 against a displayed Total **$112.27**; the missing **$17.82** is the api's `gratuity`, which the card never renders. `summary.tsx` on `main` has only Fare/Tax/Total rows. The test passes because its fixture carries **no gratuity field**, so its own two-sided staleness guard can never fire. Screenshot + api payload captured; dispatched to PAX, component untouched | PAX to decide the fix |
| *(parallel)* A7 chat | **5 of 6 ON THE WIRE · 0 of 6 ON THE CLIENT** | wire: 4a 10.9 ms · 4b 6 ms · 4c `ops` · 4e 9 clean + planted control · 4f unread 1→4 after exactly 3 · all three now COMMITTED tests: `#574` (4b), `#576` (4f/4c, merged `70cf751d`), `#575` (flushDb opt-in, `61ed0c5e`) | **client blocked TWICE**: (1) founder's pricing ruling — no passenger booking can complete; (2) **my flush removed the dispatch-eligible driver's durable row**, so no assignment, so no thread. Not papering over (2): re-seeding risks paused DRV's credentials, which was my own ruling. Added `C-00002` to the rig, disclosed |

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

**Founder's open question, answered.** *"Show which pk the e2e profile uses."* **It uses
none.** No Stripe dependency in the passenger app (0 of 49), no `StripeProvider`, no
`publishableKey`; `.env.example` says the key "is fetched at runtime from
`/api/stripe/config` on the api. Do not put a Stripe key here." So **the api base
decides the pk** — which is the same lever M2 just wired. Point the twin at STG-1 and
it gets staging's `pk_test_` (acct `51QY4ZQCxi29dqjf`, already proved); leave it as it
was and it got production's.

**Runner note for M2/M3:** `proof1-cloud-walk.yml` and `e2e-pax.yml` run on
`ubuntu-latest`, so **SO-42 does not gate them**. `render-ios.yml` is `macos-15` and
does.

**CORRECTION, and it is worse than I first reported: I WIPED the `:4010` rig's store.**
Not "added test rows". `tests/rideChatSocketWire.spec.ts:78` calls `flushDb()` on any
loopback Redis — `if (["127.0.0.1","localhost","::1","redis"].includes(host))`, with the
comment *"a throwaway test store only"*. I ran it against `redis://127.0.0.1:6390`, the
KV behind the live rig, **twice**. The comment asserts a property nothing enforces, and
`127.0.0.1` means local, not disposable. **DO NOT RESTART `:4010`** — it booted 23:35:15Z
and still serves the original fixture from memory; a restart rehydrates from the flushed
store. API holds a partial backup (booking and thread rows only). My decision: restore
those rows with the process up, **do not** re-seed the driver (it would change DRV's
credentials and DRV is paused), verify against what the process still serves, and nobody
restarts until API says it is verified. **REV avoided this exact trap and said so in a
handback before I hit it**, by running on their own disposable Redis at `:6399`.

**The OTA publish source is fully de-risked, and I still did not publish.**
`eas-update.yml` runs four steps before its runtime gate; all four pass on
`ota/build12-runtime-js-only` (`cf9d11f`): **30/30 gates**, **19 suites / 289 tests**,
**`tsc` 0 errors**, **lint 0 errors**. So a dispatch reaches the runtime gate, which is
the real decision point — and that gate refuses unless an installed build accepts the
runtime, so the dispatch is safe by construction either way.

**Why I held anyway:** an OTA only matters once build 12 is ON his phone. Publishing
before he installs gains nothing he could see, and spends an outward-facing action
that no reviewer has checked yet. It is one line in the 07:00 email instead.

**Not a blocker, measured:** the walk's flows hardcode `appId: com.ride.ridelane`,
which **matches** `app.json`'s `ios.bundleIdentifier`, and the `e2e-test` profile does
not override it. So ADV's `${APP_ID}` item is a durability improvement, not an M2
blocker — the walk would launch.

**`ridelane-passenger-app#78` is the key that is actually stuck.** It is the only
read either app repo has of what a build *is* — Build ID, commit, version and
**runtime** — and its own comment says it best: *an OTA published to a runtime no
build is listening on succeeds silently and reaches nobody.* It is **M3's gate** and
**SO-14's unprovable half**, and it sat BLOCKED for 8 days on **one missing comment
line**: `check:gates-enumerated` treats a workflow that declares nothing about gates
as a failure, and `builds-list.yml` declared nothing. Fixed at `e8e26414`, `gates`
now **SUCCESS**. The BLOCK clears only on a verdict at that newer sha — a green gate
is not a lifted block.

## Heartbeat

- probe heartbeat: 2s ago
- last pass: 2026-10-09 05:23:45 TRIGGER cause=state-change prev=7007f818 now=10ed3a8d
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
| ridelane-api | #590 | `81c496f7aa8b` | 8 total, 0 failed | YES | 217 |
| ridelane-api | #589 | `cd02a1b3cce4` | 8 total, 0 failed | YES | 335 |
| ridelane-api | #568 | `8dae9431e2c9` | 7 total, 1 failed | YES | 5053 |
| ridelane-api | #565 | `6a82a645c61a` | 7 total, 1 failed | YES | 5740 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 21989 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 22412 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 33293 |
| ridelane-passenger-app | #122 | `6e511d689ed2` | 4 total, 0 failed | **none** | 44 |
| ridelane-passenger-app | #121 | `e243a387e3fd` | 4 total, 0 failed | YES | 257 |
| ridelane-passenger-app | #120 | `8ba67a0a302a` | 4 total, 0 failed | **none** | 267 |
| ridelane-passenger-app | #115 | `ee6ba9c95098` | 4 total, 0 failed | **none** | 1073 |
| ridelane-passenger-app | #114 | `a0814ed7aadd` | 4 total, 0 failed | **none** | 1254 |
| jrax-driver-app | #285 | `835594682c03` | 3 total, 0 failed | **none** | 7 |
| jrax-driver-app | #284 | `aece405be902` | 3 total, 1 failed | **none** | 124 |
| jrax-driver-app | #273 | `1e91d443c9e6` | 3 total, 0 failed | YES | 5654 |

## Last standing-orders run

```
(from the last pass, 0m ago)
NOTE: breaking a dead check-so lock after 90s (holder 69944 not alive).
PASS   SO-1  an [HOURLY] is on his page: 2463:**[HOURLY] 15:13 EDT, 27 Sep — the first one ever p
FAIL   SO-2  4 open PRs >60m with no verdict at head: app#120, app#115, app#114, app#284
PASS   SO-3  all 7 build link(s) named by content
PASS   SO-4  every CLAIMS row carries an artifact id
PASS   SO-5  blocking list stated and scoped
UNPROV SO-6  n/a per AR-113 -- the 60m timer is withdrawn (the file changes when a founder defect moves, not on a clock). Rebuild as: no row status ahead of its artifact, plus staleness only against a newer FD-citing event. File is 4236m old, which is no longer a finding
PASS   SO-7  CLAIMS: zero OTAs published — none can target an unposted runtime
PASS   SO-8  no open PR has zero checks
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 4634m ago
FAIL   SO-11 over WIP limit: app:4 — next item is a review, not a new PR
PASS   SO-12 no approved PR sitting dirty
FAIL   SO-13 1 pushed after APPROVE:  ridelane-passenger-app#121 approved a9078e421d5c but head is e243a387e3fd; 
FAIL   SO-14 1 native PR(s) with no [native] in the title:  jrax-driver-app#285 touches app.json with no [native] in the title; 
PASS   SO-15 reviewer session active 2m ago (18879 lines)
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
PASS   SO-17 3 ask(s), all [MONEY] or [PHONE-OPTIONAL] -- no legwork on his page
FAIL   SO-18 board 3095m stale -- it is an hourly board
PASS   SO-19 every queue file is read by a session
FAIL   SO-21 his page calls a STILL-OPEN PR held without a money citation: 3074:4. **The driver-availability fix** — `#565` is the fail-on-old 
PASS   SO-22 advisor live: ADV ran 2m ago, 117 ruling(s), file 3118m old
FAIL   SO-23 merged app PR(s) with no SUCCESSFUL OTA after them: drv:18 (#283,#282,#281,...)  pax:19 (#119,#118,#117,...) -- a run that was created is not a publish (AR-7)
FAIL   SO-20 id(s) dispatched >20m ago and never acknowledged: QI-CHAT-MIGRATE-1004-CORRECTION(API,4748m) QI-NOTIFY-DELIVERY(API,4748m) QI-DRV-UNFROZEN(DRIVER,350m) QI-CHAT-PAX-1004(PASSENGER,4748m) QI-CHAT-PAX-1004-B(PASSENGER,4748m) QI-CHAT-PAX-1004-C(PASSENGER,4748m) QI-PAX-107-BLOCKED(PASSENGER,3411m) QI-PAX-GRATUITY-CONTRACT(PASSENGER,4370m) QI-PAX-SQUASH-CONFIRMED(PASSENGER,3150m) QI-WALK-RESUME-1003(PASSENGER,4748m) QI-WALK-W9-1004(PASSENGER,4748m) QI-CHAT-REV-1004-AMENDMENT(REVIEWER,4748m) QI-CHAT-REV-1004-B(REVIEWER,4748m) QI-PROOF1-REVERDICT-3(REVIEWER,4748m) QI-REV-118-REREVIEW(REVIEWER,340m) [12 retired as unackable -- see state/retired-ids.tsv for the reason on each]
PASS   SO-24 heartbeat 141s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-PAX-0523.md(7p/12t)
PASS   SO-26 every queue's newest item cites an FD/phase/QI/AR id
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
UNPROV SO-28 nightly for 9 Oct not written yet (newest: 6 Oct); not due until 07:00
PASS   SO-29 page states AUTOPILOT: NOT YET PROVED -- no unproved claim is being made
PASS   SO-33 notifier ran 0m ago; 63 event(s) delivered to date
PASS   SO-34 public mirror pushed 2m ago (raw.githubusercontent.com/jrabson777/ridelane-status/main/STATUS.md)
PASS   SO-35 control plane intact: 7 files present, lib.sh matches the committed copy, 7/7 sessions have transcripts
FAIL   SO-37 the dispatch loop sees 7 session rows, not 6 -- it is dispatching to nobody while every other check passes
PASS   SO-38 no loop script sources the scratchpad; pass.log grew 1m ago
PASS   SO-39 every expected check is present as a check run on the open PRs
PASS   SO-41 6 remote(s) checked, none carries userinfo; 0 private-key bodies in publishable paths
PASS   SO-43 all 5 boot-required name(s) bound by the staging spec (11 api keys), contract from origin/master
---
BOARD-COMPUTED: 1791538148 2026-10-09 05:29:08 EDT
FAILS: 10   (UNPROV is not a pass and not counted as a fail)
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
