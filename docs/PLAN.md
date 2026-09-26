# Plan: LineSafe, digital Permit-to-Work and violation alerts for LESCO

## Context
The first idea was a broadcast "safety call" to 3000 to 4000 field staff. The user pointed out that a call system is easy for LESCO's in-house IT department to copy, and that the real value is **preventing accidents**, including alerting when there is a violation on the line.

Most lineman deaths in the DISCOs come from a few repeat causes:
- a feeder re-energised while a crew is still on it
- work started without a proper shutdown or earthing
- backfeed from generators or solar
- missing safety gear

The user has an **SDO friend in LESCO**. That makes a discovery step possible: learn the real shutdown / PTW process before designing screens. Matching the existing process and paper forms is what gets a tool adopted.

**Outcome:** a pilot-ready system for one subdivision that has:
1. a digital PTW with a feeder lock
2. violation alerts
3. a gear and earthing photo check
4. the broadcast / emergency ring (the earlier Option B plan) as its alarm channel

It is designed as a product for all DISCOs, not a one-off for LESCO.

Stack is unchanged: Next.js App Router (JS), Tailwind v4, Supabase, Vercel, and an Expo Android app. The repo `ammar-sagheer/broadcaster` is empty.

## Phase 0: Discovery with the SDO (before any code)
Goal: replace every assumption below with how LESCO actually works. Take photos of real blank forms.

**Questions for the SDO**
1. **The shutdown chain.** Who requests a shutdown? Who approves (SDO / XEN)? Who switches the feeder off (SSO at the grid station)? How is it communicated today: phone, register, wireless?
2. **The PTW form.** Can we get a photo of a blank permit and the register? What fields does it have? Who signs it and in what order?
3. **Restoring supply.** How does the SSO know every crew is clear? Where has this gone wrong before?
4. **Accidents.** What are the last 3 to 5 accidents they know of, and what went wrong in each? This tells us which violation alerts matter most.
5. **Earthing and gear.** What must be done on site before climbing (testing, discharge rods, earthing on both sides)? Is it checked by anyone today?
6. **Backfeed.** How common are generators, solar and interconnected feeders? Are LT lines handled differently from 11 kV?
7. **Data.** Is there a list of feeders per grid station and poles or transformers per feeder, even in Excel? Does SCADA or AMR show feeder on/off anywhere?
8. **People and phones.** How big are crews (LS, lineman, ALM)? Who carries a smartphone? Is data coverage available at sites?
9. **Politics.** Who would champion a pilot (SDO, XEN, SE, the safety directorate)? What would make IT or management block it?
10. **Pilot site.** Could we run it in the SDO's own subdivision, with 1 grid station, a few feeders and 3 to 5 crews?

**Deliverable:**
- `docs/DISCOVERY.md` with the real workflow, as-is and to-be
- the form fields
- the accident causes, ranked

Screens and field names come from this document.

## How the system works (assumed, to be corrected by Phase 0)
```
Crew leader (app)             SDO (app/web)             SSO at grid station (web)
Request shutdown  ------->    Approve  ------------->   Switch feeder OFF, confirm in app
(feeder, poles, time,                                   Feeder screen turns RED "LOCKED:
 crew members, reason)                                    PTW #123, 2 crews, until 14:00"
      |
On site: test line, earth both sides, photo of earthing + crew in gear  -> AI gear check
      |
PTW ACTIVE -> work
      |
Each crew marks "work done, men and earthing clear"  -> permit can close
      |
SSO may re-energise only when ALL permits on that feeder are closed. Every switch-on is logged.
```

## Modules
**1. Digital PTW (the core)**
- **Records:**
  - `permits`, with a state machine: requested → approved → switched_off → earthed → active → cleared → closed, plus cancelled / expired
  - `permit_crews` and `permit_members`, for everyone on the line
  - `permit_events`, an append-only audit trail with who, when, GPS and photo
- **Rules in Postgres:**
  - a feeder with an open permit cannot be marked energised
  - a permit cannot become `active` without earthing photos
  - a permit cannot close until every crew has cleared
- **Operator screen:** a large-type feeder board for the grid station SSO, showing locked feeders in red with a crew count.

**2. Violation alerts**
- **Energised during a permit.** Marking a feeder energised while a permit is open is blocked. A forced override triggers the **emergency ring** to every crew on that feeder, plus the SDO and XEN.
- **Working without a permit.** A crew's GPS is at a pole on a feeder with no active permit, which alerts the SDO. This needs a pole or feeder geo-map, sourced in Phase 0.
- **Overruns and missing steps.** A permit past its end time, earthing not photographed, or crew members not checked in.
- **Later.** Read the feeder on/off state from SCADA or AMR automatically, if Phase 0 finds an accessible source.

**3. Gear and earthing check**
- The app shows a photo checklist before work: helmet, gloves, body belt, and earthing rods on both sides.
- An AI vision model gives a pass or fail with a reason. The SDO can override it, and the override is logged.

**4. Broadcast and emergency ring (reuses the earlier Option B design)**
- **Transport:** FCM high-priority push with a Notifee full-screen call UI. Audio is pre-downloaded, acknowledgements are queued offline, and delivery is retried.
- **Uses:** emergency alerts from module 2, and daily toolbox talks with "I have understood".
- **Fallback:** a real voice call (Option A) later, for staff with no data.

**5. Dashboards and reports (Next.js)**
- live map and board of active permits per subdivision
- violations log
- a monthly safety report per subdivision, division and circle, from Postgres summary functions
- a PDF of any permit with its full audit trail, for inquiries

## Repo layout
```
web/                    Next.js (house layout: app/_lib/data-service.js, actions.js, helpers.js, 3 supabase clients, siteConfig.js)
mobile/                 Expo app (dev build, Android first)
supabase/migrations/    tables, state-machine triggers, RLS, summary functions, cron
supabase/functions/     dispatch (FCM), gear-check (vision)
docs/DISCOVERY.md  README.md  CLAUDE.md
```
Tenant-ready from day one: a `discos` table (LESCO first) and feeder hierarchy tables `circle → division → subdivision → grid_station → feeder`.

## Build phases
0. **Discovery with the SDO**, then `docs/DISCOVERY.md` (1 to 2 weeks).
1. **Clickable prototype** of the PTW flow on the web, built on the real form fields. The SDO reviews it and the design changes before the backend is built.
2. **Backend:** Supabase schema, the permit state machine and its rules, RLS by role (crew, SDO, SSO, XEN, admin), and an import of the pilot area's feeders and staff.
3. **Mobile app:** crew and SDO screens, earthing photos, GPS check-in, and the emergency ring (with the spike on Infinix, Tecno, Xiaomi and Samsung phones first).
4. **SSO feeder board**, violation alerts and the gear-check function.
5. **Pilot:** one subdivision, 3 to 5 crews, run alongside paper for 4 weeks. Measure time per shutdown, violations caught and user feedback. Use the results to pitch to the XEN, SE and the safety directorate, then to the other DISCOs.

## Verification
- `docs/DISCOVERY.md` is reviewed and signed off by the SDO before Phase 2.
- **SQL tests:**
  - a feeder cannot be energised with an open permit
  - a permit cannot be activated without earthing photos
  - a permit cannot close with an uncleared crew
  - RLS keeps each role in its scope
- **End to end on real phones:**
  - request, approve, switch off, earth, work, clear and close
  - a forced re-energise rings every crew phone within 30 s
- **Pilot metrics** are compared against the paper process.
- The no-em-dash grep from the house skill passes before each commit.

## Risks to state honestly
- Software cannot physically stop someone closing a breaker. It makes the lock visible, logged and alarmed. A hard interlock needs SCADA or hardware, which comes later.
- Adoption depends on the SSO and crews using it every time. That is why Phase 0 and the paper-parallel pilot matter.
- Any software can be copied. What protects the idea is domain depth, pilot results and selling to all DISCOs.
