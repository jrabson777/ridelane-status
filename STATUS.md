# RideLane — loop status

_Generated 2026-10-05 17:11:54 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## Heartbeat

- probe heartbeat: 2s ago
- last pass: 2026-10-05 17:11:51 TRIGGER cause=state-change prev=ab85dd85 now=b9c684e8
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
|  **FD-17**  |  **The quote gate says 6 passengers and enforces 14**  |  **MERGED — not published, not device-proved**  |
|  **FD-18**  |  **A driver goes invisible when the phone is backgrounded or locked**  |  **IN-PR, STILL BLOCKED — DISPATCH-CRITICAL**  |
|  **FD-19**  |  **Beyond 600 miles the customer is told "prices unavailable, try again" and no lead reaches the CRM**  |  **OPEN**  |

## Open PRs, verdict at head

| repo | pr | head | checks | verdict at head | age (m) |
|---|---|---|---|---|---|
| ridelane-api | #565 | `6a82a645c61a` | 7 total, 1 failed | YES | 681 |
| ridelane-api | #562 | `4cd691581aa1` | 7 total, 0 failed | YES | 753 |
| ridelane-api | #517 | `42e34e5b3515` | 4 total, 0 failed | YES | 16931 |
| ridelane-api | #505 | `e1d9243859bf` | 4 total, 0 failed | YES | 17353 |
| ridelane-api | #459 | `b648529c23b3` | 3 total, 0 failed | YES | 28234 |
| ridelane-passenger-app | #97 | `c58551c6ba8d` | 3 total, 0 failed | YES | 817 |
| ridelane-passenger-app | #78 | `fa2a02daf47d` | 2 total, 1 failed | YES | 11169 |
| jrax-driver-app | #278 | `b9b254180f2c` | 3 total, 3 failed | **none** | 38 |

## Last standing-orders run

```
(from the last pass, 1m ago)
NOTE: another check-so is running (248s) and there is no cached result. Reporting nothing rather than a half board.
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
