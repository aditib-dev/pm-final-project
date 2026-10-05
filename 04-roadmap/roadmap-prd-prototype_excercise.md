# Roadmap, PRD & Prototype (Module 4)

## Your strategic anchors
- **Persona (M2), who are you solving for?:** The dispatcher (composite of UXR-02, 09), A fleet dispatcher at a mid-size logistics company who assigns and reassigns routes and monitors drivers in real time., goal: Know where every driver and stop stands, and have route changes acted on immediately.
- **Primary success metric (M3), your leading indicator:** Metric: median time from a route change being issued to the driver acknowledging it in the app.
Supporting metric: the share of route changes acknowledged in-app within 2 minutes.
Baseline: none exists in the data, so capture one before launch.
- **Moment of misery (M2), the specific friction blocking the goal:** A reassigned route takes 10–15 minutes to reach the driver, who has often driven the wrong way by then, so the team runs a WhatsApp group as "the real system" (UXR-02). On the night shift, stops show "in progress" an hour after delivery, and the dispatcher says they can't trust the board (UXR-09).
- **Guardrail metric (M3), what must not drop or break:** Primary: Manager Reporting CSAT must stay at 4.0 or above. It's currently 4.5, and reporting is why customers buy (UXR-10).
Secondary: Coordinators × Core Dispatch CSAT must stay at 4.0 or above. It's currently 4.1, so there's almost no headroom for disruption.

## Scan the backlog & set a human baseline
- **My instinctive “quick wins” before touching the AI (2 to 3 feature IDs + why):** B5 - Ste progress Indicator - it is just a signpost in the workflow and not helping to actual speed up the user journey.  
B7 - Contextual AI ETA Display - current adoption is 11%, CSAT score AI is 2.4 and Corrdiantor adoption is 23% - it is just a display of where Driver is at or stands.

## Audit, override & decide
- **Where did you override the AI? (feature + old vs. new score + why):** Feature: B6 , old: 4 , new score: 5, why: BUG-2044 says changes take 8–15 min to reach the driver app, so the delay sits in sync, not in the missing alert. An alert sent after a slow sync arrives just as late, and adding driver acknowledgment is extra work on the driver app.
Feature: B1, old: 3 , new: 4, why: M3 shows compliance as the worst coordinator step on every measure: 14.6 min against 3.0, 48% completion, CSAT 2.2 at 77% adoption. It's also about 39% of the measured time gaps (11.6 of 29.8 min). It still doesn't move the primary metric, so it stays below 4.
- **Did the AI over-value a Sales/Eng request your M2 interviews don’t support?:** No,  B8 - Sales, Value 1, Time Sinker, Cut.
B9 - Legal/CS, Value 12 Fill-In, later
B10 - CS: Value 1, Fill-In, Later
- **Did it underweight something your M3 cohort/funnel data strongly supports?:** Yes, feature B1, AI gave it 3 value , Funnel: the compliance step loses 23 points (71% to 48%), tied for the steepest drop.
Time: 14.6 min against a 3.0 min benchmark, the largest gap at +11.6 min, and about 39% of all measured time lost.
Satisfaction: Coordinators × Compliance CSAT is 2.2 (Weak), even though 77% of coordinators use it daily.

## Generate your interactive roadmap
- **My “Now” lane (this sprint), the 2 to 3 quick wins I’ll build first:** B6 · Driver Alert Notifications
The only feature that moves the primary metric, but BUG-2044 puts the delay in sync, so a real-time alert plus acknowledgment is tight for 2 engineers in 4 weeks.
- **What I cut, and the “no” I’m protecting the scope from:** B2 · Smart Daily Report Auto-Fill, AI work on a step no dispatcher mentioned, and it risks the 4.5 Manager Reporting guardrail.
B3 · Shift Handoff Wizard, Labelled M2 UXR, but no interview mentions handoff; the 6.8-minute figure comes from Snapshot 2.
B4 · Mobile-First Coordinator Dashboard, No Driver or dispatcher asked for mobile first
B7 · Contextual AI ETA Display, ETAs built on statuses that lag up to an hour (BUG-2072) would undermine trust in the board. Coordinator adoption is 23%; the 11% shown is the driver figure.
B8 · Fleet Analytics Manager View, A Sales request for managers who already rate reporting at 4.5, adding the noise Velocity is meant to remove.
- **Prototype/roadmap screenshot link (paste into your deliverables):** https://github.com/aditib-dev/pm-final-project/blob/main/04-roadmap/routelogic-velocity-roadmap.html
