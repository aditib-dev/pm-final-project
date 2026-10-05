# RouteLogic Velocity, A Frontline-First Dispatch View

> Route changes now reach your drivers the moment you save them, and you see the second they confirm, so you can run dispatch from RouteLogic instead of a WhatsApp group.

**Aditi Chaudahry · Product Management Cohort · Jun 2026**

- **Repo:** https://github.com/aditib-dev/pm-final-project
- **Prototype:** https://github.com/aditib-dev/pm-final-project/blob/main/02-discovery/journey-map.html

| The delay today | Coordinator NPS | Pilot target |
|---|---|---|
| **8–15 min** for a reassigned route to reach the driver, with no notification (BUG-2044) | **+18 → −12**, a 30-point fall in two years (current value assumed) | **< 2 min** median time from route change to driver confirmation |

---

## Slide 5 · Strategy

### Dispatch decisions land too late, so the real system moved to WhatsApp.

**Problem hook**
RouteLogic’s complexity is slowing frontline coordinators down, driving work into spreadsheets and competing tools, and putting valuable enterprise accounts at risk of churn.

**Value proposition**
Velocity makes RouteLogic dramatically faster and easier for frontline coordinators to use, reducing administrative work so they can manage logistics efficiently without leaving the platform.

**Data-backed hypothesis (M3)**

> Based on a dispatcher's account that reassigned routes take 10–15 minutes to reach drivers, forcing the team to run a WhatsApp group as "the real system" (UXR-02, BUG-2044), together with a 30-point collapse in Coordinator NPS and a 3.4× rise in daily workaround time to 31 minutes, **I believe that delivering route changes to drivers immediately with in-app acknowledgment for fleet dispatchers will result in dispatchers coordinating in RouteLogic instead of WhatsApp.** This will be measured by a reduction of at least 75% in the median time from route change to driver acknowledgment. I will protect Manager Reporting CSAT, keeping it at 4.0 or above, and will make a go/no-go decision after a 4-week pilot against control, following a 2-week baseline.

- **Bet type:** Optimizing the existing
- **Persona:** Fleet dispatcher
- **Guardrail:** Manager Reporting CSAT ≥ 4.0

**Qualitative evidence (M2)**

> "I reassign a route and the driver doesn't see it for ten, fifteen minutes. By then they've driven the wrong way. We keep a WhatsApp group as the real system." (Dispatcher, UXR-02)

**Quantitative evidence (M3)**

| Signal | Figure | Detail |
|---|---|---|
| Sentiment | −30 pts | Coordinator NPS fell 30 points in two years, from +18 to an assumed −12. |
| Time lost | 3.4× | Daily workaround time rose 3.4×, from about 9 to 31 minutes. |
| Assignment | 8.2 vs 4.0 min | Route assignment, with a 23-point drop-off at that step. |
| Reliance | 91% | Coordinators use the Live Dispatch Board; 85% the Route Optimizer. |
| Pilot | +34% | The Velocity pilot improved route-assignment speed by 34%. |

---

## Slide 6 · Research

### The workaround: WhatsApp as "the real system."

**Persona:** The dispatcher (UXR-02, 09)
**Goal:** Know where every driver and stop stands, and have route changes acted on immediately.
**External tool:** WhatsApp group (UXR-02), which replaces RouteLogic for live route changes and coordination.

**The process**

1. *Documented (UXR-02):* Reassign the route in RouteLogic.
2. *Documented (BUG-2044):* The change takes 8–15 minutes to reach the driver, and no notification is sent.
3. *Inferred:* Post the change in the WhatsApp group so the driver acts on it now.
4. *Inferred:* Wait for the driver to reply in the chat to confirm. The board can't be relied on, because statuses lag up to an hour (UXR-09, BUG-2072).
5. *Documented (UXR-02):* Treat the WhatsApp thread, not RouteLogic, as the record of what's actually happening.

**Core frustration**
The process feels most broken between steps 2 and 3. The dispatcher has made the decision and entered it correctly in RouteLogic, but the driver doesn't see it and keeps driving on the old route. When the change finally lands, "they've driven the wrong way" (UXR-02).

**Competitive advantages over the workaround**

- **One record per change:** the route change and the driver's confirmation live on the route, not in a chat.
- **No parallel channel to run:** dispatchers stop relaying every change by hand in WhatsApp.
- **Handoff-ready history:** the next shift sees every change and acknowledgment without scrolling a group chat.

**Future-state journey map** ([journey-map.html](https://github.com/aditib-dev/pm-final-project/blob/main/02-discovery/journey-map.html))

| Stage | User action | Pain addressed |
|---|---|---|
| 1 · Open the fleet board | Loads the fleet view with live stop statuses → sees the real state instantly. | Replaces stops showing "in progress" an hour after delivery (UXR-09, BUG-2072). |
| 2 · Assign routes | Assigns routes through the optimizer in minutes → more time for live exceptions. | Closes the 8.2-minute vs 4.0-minute assignment gap; the pilot showed +34%. |
| **3 · Reassign mid-route (moment of misery)** | Pushes a route change → the driver is notified and acknowledges in the app. | Ends 8–15 minute propagation with no notification (UXR-02, BUG-2044). |
| 4 · Hand off the shift | Hands over a board that matches reality → the next dispatcher starts informed. | Retires WhatsApp as "the real system" (UXR-02). |

---

## Slide 7 · Blueprint

### One feature in the pilot. Everything else waits or is cut.

**Team:** 2 engineers + 1 designer + 1 CS lead

| Lane | Feature | Quadrant | Value · Effort | Rationale |
|---|---|---|---|---|
| **NOW** · Pilot (4 weeks, 3 accounts) | B6 Driver Alert Notifications | Major Project | V5 · E4 | The only feature that moves the primary metric, but BUG-2044 puts the delay in sync, so a real-time alert plus acknowledgment is tight for 2 engineers in 4 weeks. |
| **NEXT** · GA (weeks 5–8) | B1 One-Click Compliance Checklist | Major Project | V4 · E3 | The strongest M3 signal (14.6 vs 3.0 min, 48% completion, CSAT 2.2), but it doesn't change how fast a route change reaches the driver. |
| **LATER** · Backlog | B5 Step Progress Indicator | Fill-In | V1 · E1 | It labels a slow workflow without touching reassignment or board trust. |
| **LATER** · Backlog | B9 Compliance Audit Trail Export | Fill-In | V2 · E2 | A legal need with no link to the dispatcher's friction or primary metric. |
| **LATER** · Backlog | B10 In-App Coordinator Training | Fill-In | V1 · E1 | The CS lead could deliver it without engineers, but training can't fix a sync delay. |
| **CUT** | B2 Smart Daily Report Auto-Fill | Time Sinker | V1 · E4 | AI work on a step no dispatcher mentioned, and it risks the 4.5 Manager Reporting guardrail. |
| **CUT** | B3 Shift Handoff Wizard | Time Sinker | V1 · E3 | Labelled M2 UXR, but no interview mentions handoff; the 6.8-minute figure comes from Snapshot 2. |
| **CUT** | B4 Mobile-First Coordinator Dashboard | Time Sinker | V1 · E5 | No driver or dispatcher asked for mobile-first. |
| **CUT** | B7 Contextual AI ETA Display | Time Sinker | V1 · E3 | ETAs built on statuses that lag up to an hour (BUG-2072) would undermine trust in the board. |
| **CUT** | B8 Fleet Analytics Manager View | Time Sinker | V1 · E4 | A Sales request for managers who already rate reporting at 4.5, adding the noise Velocity is meant to remove. |

**PRD highlights · B6 Driver Alert Notifications**

**Vision:** Every route change a dispatcher makes reaches the driver within seconds and comes back confirmed, so RouteLogic, not a WhatsApp group, is where dispatch actually runs.

**Must have**

1. The alert fires the moment the change is saved.
2. Push notification to the affected driver only.
3. Tapping the alert loads the updated route.
4. One-tap acknowledgment.
5. Acknowledgment status on the dispatcher's board.

- **Success metric:** Median time from route change issued to driver acknowledgment in-app. Under 2 minutes, a reduction of at least 75% from the 8–15 minutes in BUG-2044.
- **Guardrail:** Manager Reporting CSAT, stays at 4.0 or above (currently 4.5).

**[View prototype ↗](https://github.com/aditib-dev/pm-final-project/blob/main/02-discovery/journey-map.html)**

---

## Slide 8 · Validation

### A 50/50 test, randomised by driver, across 3 accounts.

**Hypothesis**

> I believe that B6 Driver Route-Change Alerts for fleet dispatchers will lead dispatchers to make and confirm route changes in RouteLogic instead of WhatsApp. This will be measured by at least a 50% reduction against control in median time from route change to the driver viewing the updated route, with a target of under 2 minutes, over a 4-week, 50/50 test randomised by driver across 3 accounts. I will protect driver app crash rate, Manager Reporting CSAT and Coordinators × Core Dispatch CSAT, each at or above its threshold.

**Control (A)**
The current RouteLogic experience. When a dispatcher reassigns a route, the change takes 8–15 minutes to reach the driver's app, and no push notification is sent (BUG-2044). The board has no acknowledgment status, so the dispatcher can't see whether the driver has received the change. Stop statuses on the board lag 20–60 minutes (BUG-2072, UXR-09).

**Variant (B), one change**
B6 Driver Route-Change Alerts, as specified in the M4 PRD: instant trigger · correct targeting · plain headline · no stale routes · one-tap acknowledgment · board status · timestamps · pilot only.

**Parameters**

| Parameter | Value |
|---|---|
| Primary metric | Median time from a route change being issued to the driver acknowledging it in the app. Target: under 2 minutes, a reduction of at least 75% from the 8–15 minutes logged in BUG-2044. |
| Baseline | 8.2 min: Assign Routes via Optimizer avg time (+4.2 min vs expected 4 min) |
| MDE | −50%: median time to acknowledgment against control, e.g. 8 → 4 min |
| Sample per arm | 27 |
| Split · significance | 50/50 · p < 0.05 |
| Guardrail | Manager Reporting CSAT ≥ 4.0 (now 4.5). Coordinators × Core Dispatch CSAT ≥ 4.0 (now 4.1). |

**Decision rules**

- **Ship:** if median time from a route change being issued to the driver acknowledging it in the app improves to under 2 minutes, a reduction of at least 75% from the 8–15 minutes logged in BUG-2044, at p < 0.05, and Manager Reporting CSAT stays at 4.0 or above, not dropping beyond 0.5 points.
- **Iterate:** if direction is positive but lift is below MDE.
- **Kill:** if the primary metric shows no improvement or moves negatively. The read date is fixed, with no results reviewed before then.

---

## Slide 9 · Launch

### A targeted launch to existing accounts, built on engagement.

| Field | Value |
|---|---|
| Goal | Engagement |
| Audience | Fleet dispatchers (Coordinators) at existing accounts who reassign routes mid-shift |
| Secondary audience | Drivers, whose one-tap acknowledgment the feature depends on, and ops managers at renewal-risk accounts |
| Tier | M, Targeted |
| Budget | No paid spend |

**Why engagement:** B6 is for existing customers, not new ones. Its success depends on dispatchers changing behaviour: making and confirming route changes in RouteLogic instead of WhatsApp (UXR-02). Retention and renewals follow from it, but they're lagging outcomes the launch can't move within weeks.

**Channels**

1. **Owned:** In-app announcement and first-use guidance on the dispatcher board, plus a one-time tip on the driver's first alert explaining "Got it."
2. **Owned:** CS-led account rollout: a 30-minute enablement session with each account's dispatch lead, and a "what changes for your team" note to ops managers.
3. **Earned:** A pilot customer story ("how [account] retired its WhatsApp dispatch group"), with the account's consent, shared in renewal conversations.

**Owners:** Aditi (PM) · John (CS lead) · Pedro (Design) · Yuriy (Eng) · Eldho (Eng) · Merin (Support)

**Timeline**

- **Beta, weeks −2 to 4:** baseline, then pilot; go/no-go at week 4.
- **Launch, weeks 5 to 8:** GA account by account.
- **Post-launch, weeks 9 to 12:** weekly metric reviews.

**Success metrics**

| Metric | Target |
|---|---|
| Speed | Median time from route change to driver viewing the updated route is under 2 minutes in enabled accounts |
| Acknowledgment | At least 70% of route changes acknowledged in-app within 2 minutes |
| Behaviour | WhatsApp route-change messages per dispatcher per week fall from baseline |

**Bad signal:** High acknowledgment rates while WhatsApp use doesn't fall: drivers are tapping "Got it," but dispatchers still don't trust the board, so the problem is trust, not speed. A second warning sign is acknowledgment rates that drop after week 1, which would point to alert fatigue.

---

## Slide 10 · Story

### The workflow at the moment of decision beats feature breadth.

**Friction and aha moment**

> The aha moment was realising the fix was subtraction, not features, coordinators did not need more power, they needed the live view unburied. The hardest part was protecting enterprise depth while making the frontline the default.

**Key takeaways and next steps**

> Biggest takeaway: for B2B tools, the workflow at the moment of decision beats feature breadth. Next I would instrument the reroute flow and A/B test exception-alert timing to cut time-to-action further.

---

## Thank you · Questions?

**RouteLogic Velocity, A Frontline-First Dispatch View**

- **Repo:** https://github.com/aditib-dev/pm-final-project
- **Cohort:** Product Management Cohort · Jun 2026
- **Author:** Aditi Chaudahry

**↗ Submit to the learning platform**
