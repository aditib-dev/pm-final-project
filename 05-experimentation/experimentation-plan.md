# Experimentation Plan (Module 5)

## Get your documents ready
- **From M3, your hypothesis sentence:** Based on a dispatcher's account that reassigned routes take 10–15 minutes to reach drivers, forcing the team to run a WhatsApp group as "the real system" (UXR-02, BUG-2044), together with a 30-point collapse in Coordinator NPS and a 3.4× rise in daily workaround time to 31 minutes, I believe that delivering route changes to drivers immediately with in-app acknowledgment for fleet dispatchers will result in dispatchers coordinating in RouteLogic instead of WhatsApp. This will be measured by a reduction of at least 75% in the median time from route change to driver acknowledgment. I will protect Manager Reporting CSAT, keeping it at 4.0 or above, and will make a go/no-go decision after a 4-week pilot against control, following a 2-week baseline.
- **From M3, your primary success metric & guardrail metric:** Median time from a route change being issued to the driver acknowledging it in the app.
Supporting metric: the share of route changes acknowledged in-app within 2 minutes.
Baseline: none exists in the data, so capture one before launch.
Primary: Manager Reporting CSAT must stay at 4.0 or above. It's currently 4.5, and reporting is why customers buy (UXR-10).
Secondary: Coordinators × Core Dispatch CSAT must stay at 4.0 or above. It's currently 4.1, so there's almost no headroom for disruption.
- **From M4, the feature you scoped in your PRD this is what you're testing:** B6 · Driver Alert Notifications , why: BUG-2044 says changes take 8–15 min to reach the driver app, so the delay sits in sync, not in the missing alert. An alert sent after a slow sync arrives just as late, and adding driver acknowledgment is extra work on the driver app.
Feature: B1, old: 3 , new: 4, why: M3 shows compliance as the worst coordinator step on every measure: 14.6 min against 3.0, 48% completion, CSAT 2.2 at 77% adoption. It's also about 39% of the measured time gaps (11.6 of 29.8 min). It still doesn't move the primary metric, so it stays below 4.

## Define your experiment parameters
- **Feature under test pull from your M4 PRD:** B6 · Driver Alert Notifications
- **Persona pull your M2 persona:** The dispatcher (composite of UXR-02, 09), A fleet dispatcher at a mid-size logistics company who assigns and reassigns routes and monitors drivers in real time.
- **Expected outcome the behaviour change you expect, from your M3 hypothesis:** dispatchers make and confirm route changes in RouteLogic instead of relaying them through WhatsApp.
- **Primary success metric the one number that defines success, from M3:** Median time from a route change being issued to the driver acknowledging it in the app. Target: under 2 minutes, a reduction of at least 75% from the 8–15 minutes logged in BUG-2044, measured against a 2-week pre-launch baseline.
- **Baseline rate today's rate of your primary metric, from your M3 data:** Assign Routes via Optimizer avg time 8.2 min( +4.2 min then expected 4 min)
- **Guardrail metric & boundary what must not break, and how far it can move before you investigate:** Primary: Manager Reporting CSAT must stay at 4.0 or above. It's currently 4.5, and reporting is why customers buy (UXR-10).
Secondary: Coordinators × Core Dispatch CSAT must stay at 4.0 or above. It's currently 4.1, so there's almost no headroom for disruption.
- **Minimum Detectable Effect (MDE) the smallest improvement worth shipping, your floor:** A 50% reduction in median time from route change to driver acknowledgment against control. For example, from 8 minutes to 4 minutes at the low end of BUG-2044's range.
- **Sample size per arm use the calculator in the builder, baseline + MDE:** 27
- **Traffic split & test duration 50/50 standard · cover ≥ 2 weekly cycles:** 50/50
- **Significance threshold p < 0.05 is standard, explain any deviation:** p<0.05

## Define your control and variant
- **Control (A) the current experience, reference your M2 moment of misery and M3 funnel/workflow data:** The current RouteLogic experience. When a dispatcher reassigns a route, the change takes 8–15 minutes to reach the driver's app, and no push notification is sent (BUG-2044). The board has no acknowledgment status, so the dispatcher can't see whether the driver has received the change. The moment of misery: "I reassign a route and the driver doesn't see it for ten, fifteen minutes. By then they've driven the wrong way. We keep a WhatsApp group as the real system." (UXR-02). Stop statuses on the board lag 20–60 minutes (BUG-2072, UXR-09). In M3, route assignment takes 8.2 min against a 4.0 min benchmark, with 23 points of coordinators dropping off at that step (94% to 71%).
- **Variant (B) your single change, copy the relevant screens & functional requirements from your M4 PRD:** One change: B6 Driver Route-Change Alerts, as specified in the M4 PRD.

Screens

1. Entry point: dispatcher fleet board
      a. A list of drivers, each with route ID, next stop and stops remaining
      b. A "Reassign" button on each driver row
      c. A status badge column (blank, Pending or Acknowledged)
      d. A header strip showing the pilot account name and a live clock
2. Feature core: reassign and alert, side by side
      a. Left panel (dispatcher): the current route, the edit (move stops, reorder, or move stops to another driver), a change summary such as "2 stops added, next stop changed," and a "Save and alert driver" button
      b. Right panel (driver phone mock): the incoming push notification, the updated route after the tap with changed stops highlighted, and a full-width "Got it" button sized for one-handed use
3. Success and confirmation: board after acknowledgment
      a. The driver row with a green Acknowledged badge, the acknowledgment time and the elapsed time (for example, "Acknowledged in 0:48")
      b. An amber "Not acknowledged, 2:00+" badge on any change still pending past 2 minutes
      c. A collapsible event log per change: issued, alert sent and acknowledged timestamps

Functional requirements

1. Instant trigger: saving a route change creates an alert within 10 seconds, independent of route sync.
2. Correct targeting: alerts go only to drivers whose stops changed; a move between drivers alerts both.
3. Plain headline: the alert headline states that the route changed, in 60 characters or fewer.
4. No stale routes: tapping the alert shows the route version created by that change, never an earlier one.
5. One-tap acknowledgment: acknowledgment takes exactly one tap, with no confirmation step.
6. Board status: the board shows Pending when the alert is sent and Acknowledged within 10 seconds of the tap.
7. Timestamps: each change records three timestamps (issued, alert sent, acknowledged) for the primary metric.
8. Pilot only: the feature is enabled only for the 3 pilot accounts; all other accounts see no change.
- **Isolation check, what has NOT changed? list everything identical between arms (app version, recommendation engine, notifications, onboarding). If something changed inadvertently, your test is compromised.:** 1. The driver app version, apart from the B6 alert and acknowledgment
2. The route sync pipeline: changes still take 8–15 minutes to sync in both arms (BUG-2044 is not fixed). B6 sends its alert separately.
3. Board status sync: stop statuses still lag 20–60 minutes (BUG-2072)
4. Route Optimizer and route assignment
5. Other notifications
6. Offline behaviour
7. The "Mark delivered" flow and proof-of-delivery photo upload
8. Compliance Checklist, Shift Handoff and Daily Report
9. Financial Reporting Suite and AI Predictive ETAs
10. Onboarding and training
11. Dispatcher accounts, permissions and the 3 pilot accounts' fleets
12. The WhatsApp group: not removed or discouraged in either arm, since reliance on it is what's being measured

## Formalize your hypothesis & shipping criteria
- **Your hypothesis (filled in):** I believe that B6 · Driver Alert Notifications for The dispatcher will result in dispatchers make and confirm route changes in RouteLogic instead of relaying them through WhatsApp., as measured by a +30 change in Median time from a route change being issued to the driver acknowledging it in the app. Target: under 2 minutes, a reduction of at least 75% from the 8–15 minutes logged in BUG-2044, measured against a 2-week pre-launch baseline. within 14 days. We will protect Manager Reporting CSAT must stay at 4.0 or above (currently 4.5). throughout the test.
- **Your shipping criteria (filled in):** We will SHIP if Median time from a route change being issued to the driver acknowledging it in the app. Target: under 2 minutes, a reduction of at least 75% from the 8–15 minutes logged in BUG-2044, measured against a 2-week pre-launch baseline. improves by ≥ +30 at p<0.05 and Manager Reporting CSAT must stay at 4.0 or above (currently 4.5). does not reach the pilot must not drop beyond 0.5 points after 14 days. We will ITERATE if direction is positive but lift is below MDE. We will KILL if the primary metric shows no improvement or moves negatively. The read date is fixed at the end of 14 days, no results reviewed before then.
- **Hardest parameter to define, and did it change your hypothesis? quick debrief:** Time to acknowledgment only exists in the variant, because control drivers have no "Got it" button. You can't compare a median time between arms when one arm has no data. As written, the test can't produce a result.

Fix: measure the same event in both arms: time from a route change being issued to the driver first viewing the updated route. Instrument the driver app in both arms to record when the new route version is first displayed. Keep acknowledgment as a variant-only adoption measure.
Yes, it chyanges the hypothesis to : I believe that B6 Driver Route-Change Alerts for fleet dispatchers will lead dispatchers to make and confirm route changes in RouteLogic instead of WhatsApp. This will be measured by at least a 50% reduction against control in median time from route change to the driver viewing the updated route, with a target of under 2 minutes, over a 4-week, 50/50 test randomised by driver across 3 accounts. I will protect driver app crash rate, Manager Reporting CSAT and Coordinators × Core Dispatch CSAT, each at or above its threshold.
