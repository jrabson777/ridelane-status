# RideLane — loop status

_Generated 2026-10-03 19:03:51 EDT by the probe. Public mirror; no tokens, keys, phone numbers or env values._

**AUTOPILOT: NOT YET PROVED** — SO-29 requires a 24h window with zero human touches.

## Heartbeat

- probe heartbeat: 3s ago
- last pass: 2026-10-03 18:59:14 PASS cause=state-change prev=ca8a4ce6 now=6d26a434
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
|  **FD-4**  |  "no light theme"  |  **OPEN**  |
|  **FD-5**  |  "no route line / miles / breakdown on map"  |  **OPEN**  |
|  **FD-6**  |  "wrong install link delivered — Sep 16 build 2 sent as build 8"  |  **ANSWERED — awaiting his install**  |
|  **FD-7**  |  "the app does not tell him which build/update he is running"  |  **IN-PR**  |
|  **FD-8**  |  runtime-version audit  |  **IN-PR — blocks the next OTA. Build 2 and build 8 are ORPHANED BY DESIGN: nothing publishes to runtime `0.2.0` again.**  |
|  **FD-9**  |  "after installing passenger build 10, it still shows **Tampa Bay** as an area — no areas, cities, neighborhoods or zones; a result must have a **physical address**"  |  **MERGED `#536` 15:12 Mon AND LIVE** — running api is 19 commits past the merge  |
|  **FD-10**  |  "I CAN'T CHANGE TIME !!! STILL STATIC" — the schedule sheet's `6 40 AM` time wheel does not move **+ 15-min increments only (founder, 28 Sep): the minute column offers :00 :15 :30 :45 and nothing else, matching the website**  |  **MERGED `#79` (wheel, 01:03 Mon) + `#82` (quarter-hour slots, 17:25 Mon) — ON NO PHONE UNTIL BUILD 11** (`3a6f03a1`, CFBundleVersion 11, cut 00:35 Tue)  |
|  **FD-11**  |  **Every customer booking email carries a FAKE phone number.** `[REDACTED-PHONE]` is hardcoded in the live v3 templates  |  **MERGED `#537` 17:03 Mon** — verify the footer prints no New York address  |
|  **FD-13**  |  **REGRESSION on build 11: "Tap to pay" says payment is not available and the booking cannot complete.** Build 10 booked; build 11 does not  |  **ORDER 0 — DISPATCHED**  |
|  **FD-4**  |  Theme does not change on build 11  |  **OPEN (tokens merged, nothing visible)**  |

## Open PRs, verdict at head

REFUSED: the PR read did not answer. Not reporting an empty board.

## Last standing-orders run

```
FAIL   SO-1  no [HOURLY] on his page
FAIL   SO-2  ? open PRs >60m with no verdict at head: Expecting value: line 1 column 1 (char 0)
PASS   SO-3  no build links on the page
FAIL   SO-4   CLAIMS row(s) without an id
FAIL   SO-5  no scoped blocking list on his page
FAIL   SO-6  FOUNDER-DEFECTS.md untouched 6802m
FAIL   SO-7  CLAIMS table has no OTA updates row
FAIL   SO-8  ? open PRs have ZERO checks — red, not unknown
UNPROV SO-9  no automated proof yet — relay/page hash comparison not built
PASS   SO-10 STANDING-ORDERS.md updated 5522m ago
FAIL   SO-11 over WIP limit: ? — next item is a review, not a new PR
FAIL   SO-12 approved and dirty, refresh this pass: ?
FAIL   SO-13  pushed after APPROVE: 
FAIL   SO-14  native PR(s) with no [native] in the title: 
FAIL   SO-15 no REV row in lib.sh -- there is no reviewer session
PASS   SO-16 file-watch loaded (com.ridelane.watch); tick remains the fallback
FAIL   SO-17 no '## OPEN ASKS' section -- an unstructured page cannot be checked
FAIL   SO-18 no five-row board on his page
FAIL   SO-19 orphan queue file(s), written but never read: QUEUED-FOR-API.md QUEUED-FOR-PAX.md QUEUED-FOR-REVIEWER.md
PASS   SO-21 no undeclared holds; no PR held without a money citation; his page uses no PR-held language
FAIL   SO-22 THE LOOP HAS NO ADVISOR -- no ADV row in lib.sh
PASS   SO-23 every merged app PR has an OTA published after it
FAIL   SO-20 id(s) dispatched >20m ago and never acknowledged: QI-A7-INVENTORY-0929(API)
PASS   SO-24 heartbeat 4s old
FAIL   SO-25 handback(s) over the format bar -- a table cannot bury a null: out-REV-1901.md(0p/0t) out-REV-2237.md(0p/0t)
FAIL   SO-26 queue item(s) with no FD or phase-board id: REVIEWER
UNPROV SO-27 proof-bar completeness is a judgement on item text -- ADV rules it; no mechanical check claimed
FAIL   SO-28 no nightly result table on his page and it is past 07:00 -- an absent report is not a passing night
FAIL   SO-29 the page neither states AUTOPILOT: NOT YET PROVED nor carries a window table -- silence reads as a claim
PASS   SO-33 notifier ran 1m ago; 8 event(s) delivered to date
PASS   SO-34 public mirror pushed 1m ago (raw.githubusercontent.com/jrabson777/ridelane-status/main/STATUS.md)
---
FAILS: 21   (UNPROV is not a pass and not counted as a fail)
```

## LOOP-ALERTS, tail

```
```
