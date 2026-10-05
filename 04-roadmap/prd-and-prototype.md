# B6 · Driver Alert Notifications, Simplified PRD (RouteLogic)

**Author:** Me · **Status:** Draft · **Target:** High-Fidelity Prototype · **Persona:** The dispatcher

## 1. The Big Picture
- **Vision:** Every route change a dispatcher makes reaches the driver within seconds and comes back confirmed, so RouteLogic, not a WhatsApp group, is where dispatch actually runs.
- **Press release:** RouteLogic dispatchers can now see the moment a driver accepts a route change. Until now, a reassigned route took 8–15 minutes to reach the driver's app, with no notification (BUG-2044). One fleet dispatcher told us that by the time the change landed, drivers had "driven the wrong way," so the team kept a WhatsApp group as "the real system" (UXR-02). Velocity's Driver Route-Change Alerts fix the moment that pushed them out: saving a change now alerts the affected driver immediately.
The driver taps the alert, sees the updated route, and confirms with one tap. On the dispatcher's board, the change flips from Pending to Acknowledged with a timestamp, so there is no chat thread to watch and no reply to chase. The pilot runs with 3 accounts for 4 weeks, aiming to cut the time from route change to driver acknowledgment to under 2 minutes.
- **Success metric:** Median time from route change issued to driver acknowledgment in-app. Under 2 minutes, a reduction of at least 75% from the 8–15 minutes in BUG-2044. Baseline captured in the 2 weeks before launch.
- **Guardrail:** Manager Reporting CSAT, Stays at 4.0 or above (currently 4.5)

## 2. The Details
### User stories
- 1. As a dispatcher, I want a route change to alert the affected driver the moment I save it, so that they don't keep driving the old route.
- ◦ Saving a reassignment sends an alert to every driver whose route changed, and to no one else.
- ◦ The alert is sent within 10 seconds of saving, without waiting for the route sync.
- ◦ The board shows the change as Pending as soon as the alert is sent.
- 2. As a driver, I want to open the alert, see my updated route and confirm it with one tap, so that I can act on it without working through extra screens.
- ◦ Tapping the alert opens the updated route, never the previous version.
- ◦ A single "Got it" tap acknowledges the change, with no confirmation dialog.
- ◦ The alert headline says the route changed and names what changed, in 60 characters or fewer.
- 3. As a dispatcher, I want to see on the board whether each driver has acknowledged the change, so that I don't need WhatsApp to confirm it landed.
- ◦ The change switches from Pending to Acknowledged within 10 seconds of the driver's tap.
- ◦ Acknowledged shows the time of acknowledgment and the elapsed time since the change was issued.
- ◦ A change still Pending after 2 minutes is highlighted.
### Screens to build
- 1. Entry point: dispatcher fleet board
- ◦ A list of drivers, each with route ID, next stop and stops remaining
- ◦ A "Reassign" button on each driver row
- ◦ A status badge column (blank, Pending or Acknowledged)
- ◦ A header strip showing the pilot account name and a live clock
- 2. Feature core: reassign and alert, side by side
- ◦ Left panel (dispatcher): the current route, the edit (move stops, reorder, or move stops to another driver), a change summary such as "2 stops added, next stop changed," and a "Save and alert driver" button
- ◦ Right panel (driver phone mock): the incoming push notification, the updated route after the tap with changed stops highlighted, and a full-width "Got it" button sized for one-handed use
- 3. Success and confirmation: board after acknowledgment
- ◦ The driver row with a green Acknowledged badge, the acknowledgment time and the elapsed time (for example, "Acknowledged in 0:48")
- ◦ An amber "Not acknowledged, 2:00+" badge on any change still pending past 2 minutes
- ◦ A collapsible event log per change: issued, alert sent and acknowledged timestamps
### Functional requirements
- 1. Instant trigger: saving a route change creates an alert within 10 seconds, independent of route sync.
- 2. Correct targeting: alerts go only to drivers whose stops changed; a move between drivers alerts both.
- 3. Plain headline: the alert headline states that the route changed, in 60 characters or fewer.
- 4. No stale routes: tapping the alert shows the route version created by that change, never an earlier one.
- 5. One-tap acknowledgment: acknowledgment takes exactly one tap, with no confirmation step.
- 6. Board status: the board shows Pending when the alert is sent and Acknowledged within 10 seconds of the tap.
- 7. Timestamps: each change records three timestamps (issued, alert sent, acknowledged) for the primary metric.
- 8. Pilot only: the feature is enabled only for the 3 pilot accounts; all other accounts see no change.
### Smart behaviors (Situation → Outcome)
- 1. A change has been Pending for 2 minutes -> The board badge turns amber: "Not acknowledged, 2:00+"
- 2. The dispatcher edits the same route again before acknowledgment -> The earlier alert is superseded; the driver sees only the latest version, and timing restarts from the new change
- 3. The driver taps "Got it" on a superseded alert -> The acknowledgment is rejected and the latest route opens with a fresh "Got it"
- 4. Stops move from one driver to another -> Both drivers are alerted: one sees stops removed, the other stops added
- 5. The driver's device has no signal -> The board stays Pending and shows "No signal" in the prototype; no acknowledgment is recorded
- 6. The change summary can't be worked out from the route data -> The alert says only "Your route has changed, tap to view"
### Technical constraints
- • No external APIs: no push service, maps, routing or messaging APIs. Notifications are simulated inside the driver phone mock.
- • No login: one hard-coded pilot dispatcher and 3 mock drivers with fixed routes.
- • useState only: no backend, database, browser storage or state library. Refreshing resets the demo.
- • No sync simulation beyond a toggle: a single "Simulate no signal" switch per driver covers the unhappy path.
- • Single-file prototype: one React file, no build step beyond what the prototype tool provides.

## 3. The Logistics
### Features out
- • Route sync and board status fixes (BUG-2044, BUG-2072): B6 works around the slow sync rather than rebuilding it. The rebuild is the next Major Project.
- • Compliance flag alerts: in B6's backlog description, but a different problem that would split a 2-engineer sprint.
- • SMS, WhatsApp or email fallback: would keep coordination outside RouteLogic, the behaviour the pilot is meant to end.
- • In-app chat between dispatcher and driver: replacing WhatsApp entirely is a larger product.
- • Driver app navigation changes: B4 territory, and a risk to the Core Dispatch guardrail (4.1).
- • Any change to reporting: protects the Manager Reporting guardrail (4.5).
- • Rollout beyond the 3 pilot accounts.
### Edge cases & safety guard
- • No signal: the driver is out of coverage (UXR-06). The change stays Pending and turns amber at 2 minutes, so the dispatcher can act. It is never shown as delivered.
- • Repeated edits: the dispatcher changes the same route twice before acknowledgment. Only the latest version can be acknowledged; earlier alerts are superseded.
- • Driver crash on reload: on Android 12/13, the app crashes once a route exceeds about 40 stops (BUG-2031). Test routes above 40 stops in the pilot before relying on the forced reload.
- • No response: the driver never acknowledges. The change stays amber with no automatic escalation in sprint 1; the dispatcher decides what to do.
- • Driver in a moving vehicle: acknowledgment needs a single large tap and no reading beyond the headline. The designer checks pilot accounts' phone-use policies before testing.
- • Accuracy guard: the board never shows Acknowledged without a recorded acknowledgment event, and never infers it from the driver opening the app. Alert text is built only from route data fields. If a field is missing, the alert falls back to the generic headline rather than guessing a stop or address.
### Decision log
- Decision:
- Work around the 8–15 minute sync delay instead of fixing it.
- Why:
- A sync rebuild doesn't fit 2 engineers in 4 weeks. Firing the alert on save tests the hypothesis without it.
- Decision:
- No SMS or WhatsApp fallback.
- Why:
- Reliability now would come at the cost of keeping dispatch outside RouteLogic, which is the outcome the pilot measures against.
### Evals
- 1. Accuracy: targeting
- Target: 100% of alerts reach only the drivers whose stops changed, with 0 sent to the wrong driver.
- How it's checked: 20 scripted reassignments in the prototype, including stops moved between drivers. Both drivers must be alerted in a move.
- 2. Time-on-task
- Target: the dispatcher goes from "Reassign" to alert sent in 30 seconds or less. The driver acknowledges with one tap, within 5 seconds of opening the alert.
- How it's checked: moderated prototype sessions with dispatchers and drivers from the 3 pilot accounts.
- Link to the pilot metric: this supports the primary metric target of a median under 2 minutes from route change to acknowledgment.
- 3. Safety triggers
- Target: 0 Acknowledged badges without a recorded acknowledgment event, and 0 stale routes shown after a driver taps an alert.
- How it's checked: every scripted scenario, including no signal and superseded alerts.

## MoSCoW scope
- **Must:** 1. The alert fires the moment the change is saved. When a dispatcher saves a reassignment, an alert goes to the affected driver straight away, on its own path rather than waiting for the 8–15 minute route sync (BUG-2044). Otherwise the alert arrives as late as the change does, and nothing improves.; 2. Push notification to the affected driver only. It reaches the driver's device even when the app is in the background, and says plainly that the route has changed. Without a push, the driver keeps driving the old route until they happen to open the app.; 3. Tapping the alert loads the updated route. Opening the notification pulls the new route from the server before showing it, so the driver never sees the stale version. Without this, the driver acknowledges a change they can't see, and still drives the wrong way.; 4. One-tap acknowledgment. A single "Got it" action, with no extra screens. The driver is likely in the vehicle, and a multi-step confirmation repeats the three-screen problem from UXR-01.; 5. Acknowledgment status on the dispatcher's board. Each route change shows Pending or Acknowledged, with a timestamp. This is what replaces waiting for a WhatsApp reply. Without it, the dispatcher still can't tell whether the change landed, so the workaround survives.
- **Should:** 1. Unacknowledged flag after 2 minutes. Highlight a change on the board if it isn't acknowledged in time. This matches your supporting metric and tells the dispatcher when to step in.; 2. A "Delivered" status separate from "Acknowledged." This tells the dispatcher whether the driver lacks signal or simply hasn't responded. It matters for rural routes (UXR-06).; 3. Queue and deliver when signal returns. Alerts sent with no signal arrive when coverage resumes, and the board shows them as undelivered meanwhile.; 4. Acknowledge from the notification itself. "Got it" works from the lock screen without opening the app, which is fewer steps for a driver in a vehicle.; 5. A short change summary in the alert, such as "Next stop changed" or "2 stops added," so the driver knows what to expect before opening.
- **Could:** 1. Reply options for drivers: "Can't do this" or "Call me," so drivers can push back without switching to WhatsApp.; 2. Re-notify an unacknowledged driver after a set interval.; 3. One action for several drivers when a dispatcher reassigns more than one route at once.; 4. An alert history in the driver app.; 5. A manager view of acknowledgment times. Kept separate so it doesn't touch the Reporting guardrail.
- **Won't (now):** 1. Fixing the route sync pipeline (BUG-2044's root cause) or real-time board status (BUG-2072). B6 works around the slow sync; it doesn't rebuild it. Those are the next Major Project.; 2. Compliance flag alerts. B6's backlog description includes them, but they solve a different problem and would split a 2-engineer sprint.; 3. SMS, WhatsApp or email fallback. These would keep coordination outside RouteLogic, which is the behaviour you're trying to end.; 4. In-app chat between dispatchers and drivers. Replacing WhatsApp entirely is a larger product.; 5. Driver app navigation changes. That's B4 territory, and it would put the Core Dispatch guardrail at risk.; 6. Any change to reporting. This protects the Manager  Reporting guardrail (4.5).; 7. Rollout beyond the 3 pilot accounts.

---
**Builder hook:** Build a working prototype based on this PRD. Use the User Story as the core flow, Functional Requirements as build constraints, and prioritize speed and clarity over visual complexity.
