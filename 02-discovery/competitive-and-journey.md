# Competitive Analysis & Journey Map (Module 2)

## Responses
- **Role, who are you solving for? (the specific user segment or profile):** The dispatcher (composite of UXR-02, 09), A fleet dispatcher at a mid-size logistics company who assigns and reassigns routes and monitors drivers in real time.
- **Goal, what is this user ultimately trying to achieve?:** Know where every driver and stop stands, and have route changes acted on immediately.
- **Friction, the main barrier (moment of misery) stopping them from succeeding:** A reassigned route takes 10–15 minutes to reach the driver, who has often driven the wrong way by then, so the team runs a WhatsApp group as "the real system" (UXR-02). On the night shift, stops show "in progress" an hour after delivery, and the dispatcher says they can't trust the board (UXR-09).
- **External tools, the outside platforms or tools the user is forced to use:** WhatsApp group (UXR-02): replaces RouteLogic for live route changes and coordination.
- **The process, the 3 to 5 manual steps the user takes to get the job done:** Steps

Documented (UXR-02): Reassign the route in RouteLogic.
Documented (BUG-2044): The change takes 8–15 minutes to reach the driver, and no notification is sent.
Inferred: Post the change in the WhatsApp group so the driver acts on it now.
Inferred: Wait for the driver to reply in the chat to confirm. The board can't be relied on, because statuses lag up to an hour (UXR-09, BUG-2072).
Documented (UXR-02): Treat the WhatsApp thread, not RouteLogic, as the record of what's actually happening.
- **Core frustration, the exact moment the process feels most “broken”:** The process feels most broken between steps 2 and 3. The dispatcher has made the decision and entered it correctly in RouteLogic, but the driver doesn't see it and keeps driving on the old route. When the change finally lands, "they've driven the wrong way" (UXR-02).
- **The evidence, a specific quote or behavior from the research that proves this:** Primary evidence: fleet dispatcher, mid-size 3PL (UXR-02)

"I reassign a route and the driver doesn't see it for ten, fifteen minutes. By then they've driven the wrong way. We keep a WhatsApp group as the real system."

This one quote covers the whole chain:

Friction: "the driver doesn't see it for ten, fifteen minutes."
The broken moment: "By then they've driven the wrong way."
The behavior: "We keep a WhatsApp group as the real system."
Supporting evidence

Bug report (BUG-2044, severity Critical)

"Dispatch reassignments take 8–15 min to propagate to the driver app; no push notification on route change. Drivers act on stale routes."

This confirms the delay as a logged defect, rated at the highest severity. It adds the technical cause Diego's quote can't: no notification is sent. And it describes the same outcome: drivers acting on stale routes.

Night-shift dispatcher (UXR-09)

"Status updates from drivers lag on my dashboard. A stop shows 'in progress' when it was delivered an hour ago. I can't trust the board."

This shows the problem runs in both directions: changes reach drivers late, and completed work reaches dispatch late. It's a second, independent dispatcher voice. It's backed by BUG-2072, which logs a 20–60 minute lag, rated Medium.
- **Your journey map, a shareable link, or the map file you committed (e.g. journey-map.html):** https://github.com/aditib-dev/pm-final-project/blob/main/02-discovery/journey-map.html
