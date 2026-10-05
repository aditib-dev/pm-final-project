# Hypothesis & Success Metrics (Module 3)

## Pre-work · Hypothesis check
- **Role , who you are solving for (from M2):** The dispatcher (composite of UXR-02, 09), A fleet dispatcher at a mid-size logistics company who assigns and reassigns routes and monitors drivers in real time.
- **Goal , what this user is ultimately trying to achieve:** Know where every driver and stop stands, and have route changes acted on immediately.
- **Friction / moment of misery , the specific pain blocking their goal:** A reassigned route takes 10–15 minutes to reach the driver, who has often driven the wrong way by then, so the team runs a WhatsApp group as "the real system" (UXR-02). On the night shift, stops show "in progress" an hour after delivery, and the dispatcher says they can't trust the board (UXR-09).
- **Current workaround , the external tool or manual process they rely on (M2):** WhatsApp group (UXR-02): replaces RouteLogic for live route changes and coordination.
- **Problem Hook , your one-sentence framing of the business crisis (M1):** RouteLogic’s complexity is slowing frontline coordinators down, driving work into spreadsheets and competing tools, and putting valuable enterprise accounts at risk of churn.
- **Value Proposition , the outcome your initiative promised to deliver (M1):** Velocity makes RouteLogic dramatically faster and easier for frontline coordinators to use, reducing administrative work so they can manage logistics efficiently without leaving the platform.

## Read your data snapshots
- **Does the funnel data confirm your M2 friction point, or does it tell a different story? Note where the numbers align with the qualitative pain you found and where they diverge.:** _(not filled in)_
- **Do the retention patterns align with the workaround your M2 persona used to find content? Note what the Mo. 0→1 drop suggests about the onboarding experience your persona described as frustrating.:** _(not filled in)_
- **Does the LTV gap and the content mix (61% trending for Wanderers) confirm the moment of misery your persona described? Note which segment your persona is in and whether the data confirms their pain.:** _(not filled in)_
- **Does the low adoption confirm your persona is burdened by tools they don’t use? Note whether the low scheduling adoption (42%) for coordinators matches your M2 moment of misery.:** Finanicial Reporting suite is only used 8% of times by co-ordinator/dispatcher and AI predictive analysis is only at 23%. Interview and bug tracker does not mention these as point of misery. therefore it is difficult to confirm if the drop is because of issues or features not required by dispatchers. 
Shift scheduling is 42% times used by dispatchers/co-ordinators compared to 79% managers. M2 misery is re-routing or re-assignment failing to reach driver in mid route which is different from scheduling.
- **Does the workflow data match the manual process or hack you documented in M2? Note whether the specific drop-offs or time gaps explain why your persona avoids the digital tool.:** Partly,  snapshot 2 shows that route reassigning is slow with a gap of +4.2 min and cooridnators dropping off from 94 % tp 71% in assign routes via optimizer. Complete shift handoff is at 31% with gap of +6.8 min which shows the co-ordiantion might be happenign outside Routelogic app on whatsapp as mentioned UXR-09. This data does not measure the moment that drives the workaround and also does not capture data on what happens outside app. Time gaps shows there is a friction which forces users to drop from app but does not explain the reason for the friction.
- **Look at the CSAT heatmap. Which specific cell most directly maps to your persona’s friction? Note how the NPS trend justifies the urgency of your M1 Problem Hook.:** With an assumption that Coordinator X Core Dispatch covers the reassignment and live board, Strong score of 4.1 is in tension with Dispatchers describing changes reaching drivers late and a app board they can't trust (UXR-02and 09). The other possible cells AI/Predictions has weak scores of 2.4 which consistent with Assign Routes via Optimizer on snapshot 2 of gap +4.2 mins. The NPS trend justifies the urgency because it measures Coordinator persona where NPS fell 30 points from +18 to -12. Daily manual workaround time has also increased by 3.4x from 9 min to 31 mins and churn has increased from 1 of 8 to 4 of 5 which a significant increase.

## Step 3 · Craft your hypothesis
- **Qualitative evidence (from M2) , quote the specific friction / moment of misery for your persona:** I reassign a route and the driver doesn't see it for ten, fifteen minutes. By then they've driven the wrong way. We keep a WhatsApp group as the real system. (Dispatcher, UXR-02)
- **Quantitative evidence (from M3) , name the metric or data point that confirms the pain; cite the number:** Sentiment: Coordinator NPS fell 30 points in two years, from +18 to an assumed −12.
Time lost: daily workaround time rose 3.4×, from about 9 to 31 minutes.
Assignment: route assignment takes 8.2 min against a 4.0 min benchmark, with a 23-point drop-off at that step.
Reliance: coordinators can't avoid the core tools: 91% use the Live Dispatch Board and 85% the Route Optimizer.
Pilot: the Velocity pilot improved route-assignment speed by 34%.
Caveat: no snapshot measures how long a change takes to reach the driver; the 8–15 minute figure comes from BUG-2044.
- **Persona , role, goal, and the friction you confirmed in the reconciliation steps:** Role: a fleet dispatcher who assigns and reassigns routes and monitors drivers in real time. I'm treating this as the "Coordinator" in the snapshots.
Goal: know where every driver and stop stands, and have route changes acted on immediately.
Confirmed friction: route changes reach drivers 8–15 minutes late and statuses reach the board up to an hour late, so dispatchers run live coordination through WhatsApp. Reconciliation confirmed that the friction sits in the core tools dispatchers use most, not in unused features.
- **Problem you are solving , one sentence describing the specific friction this initiative removes:** Route changes take 8–15 minutes to reach drivers, with no notification, so dispatchers relay every change through WhatsApp instead of trusting RouteLogic.
- **Strategic outcome , what behaviour change do you expect, and how does it map to retention / revenue / churn?:** Behaviour change: dispatchers make and confirm route changes in RouteLogic instead of relaying them through WhatsApp.
Retention: recovers Coordinator NPS and reduces the 31 minutes of daily workaround time.
Churn: reduces the complexity-driven churn now cited by 4 of 5 accounts.
Revenue: protects renewals by restoring RouteLogic as the system of record dispatchers actually rely on.
- **Primary success metric (initiative signal) , the leading indicator that tells you the gap is closing:** Metric: median time from a route change being issued to the driver acknowledging it in the app.
Supporting metric: the share of route changes acknowledged in-app within 2 minutes.
Baseline: none exists in the data, so capture one before launch.
- **Guardrail metric (product signal) , the metric that must NOT drop; it protects your existing base:** Primary: Manager Reporting CSAT must stay at 4.0 or above. It's currently 4.5, and reporting is why customers buy (UXR-10).
Secondary: Coordinators × Core Dispatch CSAT must stay at 4.0 or above. It's currently 4.1, so there's almost no headroom for disruption.
- **Decision window , how much time or data before you scale, pivot, or kill? minimum threshold to proceed?:** Setup: 2 weeks of baseline, then a 4-week pilot with at least two accounts, against a control group.
Scale: median time to acknowledgment falls below 2 minutes, and both guardrails hold.
Pivot: assignment gets faster but acknowledgment time doesn't move. That would mean the bottleneck is the sync infrastructure, not the interface.
Kill: neither metric moves, or a guardrail breaks.
- **Draft your full hypothesis sentence , one to three sentences; quote the metric, name the persona, name the outcome:** Based on a dispatcher's account that reassigned routes take 10–15 minutes to reach drivers, forcing the team to run a WhatsApp group as "the real system" (UXR-02, BUG-2044), together with a 30-point collapse in Coordinator NPS and a 3.4× rise in daily workaround time to 31 minutes, I believe that delivering route changes to drivers immediately with in-app acknowledgment for fleet dispatchers will result in dispatchers coordinating in RouteLogic instead of WhatsApp. This will be measured by a reduction of at least 75% in the median time from route change to driver acknowledgment. I will protect Manager Reporting CSAT, keeping it at 4.0 or above, and will make a go/no-go decision after a 4-week pilot against control, following a 2-week baseline.
