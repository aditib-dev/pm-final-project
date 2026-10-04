# Data-Backed Hypothesis, Module 3

- **Scenario:** RouteLogic Velocity (B2B)
- **Bet type:** Optimizing the existing

## The hypothesis
> Based on Sentiment: Coordinator NPS fell 30 points in two years, from +18 to an assumed −12.
Time lost: daily workaround time rose 3.4×, from about 9 to 31 minutes.
Assignment: route assignment takes 8.2 min against a 4.0 min benchmark, with a 23-point drop-off at that step.
Reliance: coordinators can't avoid the core tools: 91% use the Live Dispatch Board and 85% the Route Optimizer.
Pilot: the Velocity pilot improved route-assignment speed by 34%.
Caveat: no snapshot measures how long a change takes to reach the driver; the 8–15 minute figure comes from BUG-2044., we believe that solving Route changes take 8–15 minutes to reach drivers, with no notification, so dispatchers relay every change through WhatsApp instead of trusting RouteLogic. for A fleet dispatcher who assigns and reassigns routes and monitors drivers in real time. I'm treating this as the "Coordinator" in the snapshots. Goal: know where every driver and stop stands, and have route changes acted on immediately. Confirmed friction: route changes reach drivers 8–15 minutes late and statuses reach the board up to an hour late, so dispatchers run live coordination through WhatsApp. Reconciliation confirmed that the friction sits in the core tools dispatchers use most, not in unused features. will result in Behaviour change: dispatchers make and confirm route changes in RouteLogic instead of relaying them through WhatsApp.
Retention: recovers Coordinator NPS and reduces the 31 minutes of daily workaround time.
Churn: reduces the complexity-driven churn now cited by 4 of 5 accounts.
Revenue: protects renewals by restoring RouteLogic as the system of record dispatchers actually rely on., as measured by Metric: median time from a route change being issued to the driver acknowledging it in the app. Supporting metric: the share of route changes acknowledged in-app within 2 minutes. Baseline: none exists in the data, so capture one before launch.. We will protect Primary: Manager Reporting CSAT must stay at 4.0 or above. It's currently 4.5, and reporting is why customers buy (UXR-10). Secondary: Coordinators × Core Dispatch CSAT must stay at 4.0 or above. It's currently 4.1, so there's almost no headroom for disruption. and make a go/no-go decision after Setup: 2 weeks of baseline, then a 4-week pilot with at least two accounts, against a control group. Scale: median time to acknowledgment falls below 2 minutes, and both guardrails hold. Pivot: assignment gets faster but acknowledgment time doesn't move. That would mean the bottleneck is the sync infrastructure, not the interface. Kill: neither metric moves, or a guardrail breaks..

## Evidence
- **Qualitative (M2):** I reassign a route and the driver doesn't see it for ten, fifteen minutes. By then they've driven the wrong way. We keep a WhatsApp group as the real system. (Dispatcher, UXR-02)
- **Quantitative (M3):** Sentiment: Coordinator NPS fell 30 points in two years, from +18 to an assumed −12.
Time lost: daily workaround time rose 3.4×, from about 9 to 31 minutes.
Assignment: route assignment takes 8.2 min against a 4.0 min benchmark, with a 23-point drop-off at that step.
Reliance: coordinators can't avoid the core tools: 91% use the Live Dispatch Board and 85% the Route Optimizer.
Pilot: the Velocity pilot improved route-assignment speed by 34%.
Caveat: no snapshot measures how long a change takes to reach the driver; the 8–15 minute figure comes from BUG-2044.

## Persona & problem
- **Role:** A fleet dispatcher who assigns and reassigns routes and monitors drivers in real time. I'm treating this as the "Coordinator" in the snapshots. Goal: know where every driver and stop stands, and have route changes acted on immediately. Confirmed friction: route changes reach drivers 8–15 minutes late and statuses reach the board up to an hour late, so dispatchers run live coordination through WhatsApp. Reconciliation confirmed that the friction sits in the core tools dispatchers use most, not in unused features.
- **Goal:** Know where every driver and stop stands, and have route changes acted on immediately.
- **Friction:** A reassigned route takes 8–15 minutes to reach the driver, with no notification. By then the driver has often driven the wrong way, so dispatchers relay every change through a WhatsApp group instead of trusting RouteLogic (UXR-02, BUG-2044).
- **Problem you are solving:** Route changes take 8–15 minutes to reach drivers, with no notification, so dispatchers relay every change through WhatsApp instead of trusting RouteLogic.

## Outcome & metrics
- **Strategic outcome:** Behaviour change: dispatchers make and confirm route changes in RouteLogic instead of relaying them through WhatsApp.
Retention: recovers Coordinator NPS and reduces the 31 minutes of daily workaround time.
Churn: reduces the complexity-driven churn now cited by 4 of 5 accounts.
Revenue: protects renewals by restoring RouteLogic as the system of record dispatchers actually rely on.
- **Primary success metric:** Metric: median time from a route change being issued to the driver acknowledging it in the app. Supporting metric: the share of route changes acknowledged in-app within 2 minutes. Baseline: none exists in the data, so capture one before launch.
- **Guardrail metric:** Primary: Manager Reporting CSAT must stay at 4.0 or above. It's currently 4.5, and reporting is why customers buy (UXR-10). Secondary: Coordinators × Core Dispatch CSAT must stay at 4.0 or above. It's currently 4.1, so there's almost no headroom for disruption.
- **Decision window:** Setup: 2 weeks of baseline, then a 4-week pilot with at least two accounts, against a control group. Scale: median time to acknowledgment falls below 2 minutes, and both guardrails hold. Pivot: assignment gets faster but acknowledgment time doesn't move. That would mean the bottleneck is the sync infrastructure, not the interface. Kill: neither metric moves, or a guardrail breaks.
