# PRD & Prototype Sprint (Module 4)

## Pick & scope with MoSCoW
- **The “Now” feature I’m scoping (name + one-line core description):** B6 · Driver Alert Notifications
The only feature that moves the primary metric, but BUG-2044 puts the delay in sync, so a real-time alert plus acknowledgment is tight for 2 engineers in 4 weeks.
- **My finalized Must-Haves (after overriding the AI):** 1. The alert fires the moment the change is saved. When a dispatcher saves a reassignment, an alert goes to the affected driver straight away, on its own path rather than waiting for the 8–15 minute route sync (BUG-2044). Otherwise the alert arrives as late as the change does, and nothing improves.
2. Push notification to the affected driver only. It reaches the driver's device even when the app is in the background, and says plainly that the route has changed. Without a push, the driver keeps driving the old route until they happen to open the app.
3. Tapping the alert loads the updated route. Opening the notification pulls the new route from the server before showing it, so the driver never sees the stale version. Without this, the driver acknowledges a change they can't see, and still drives the wrong way.
4. One-tap acknowledgment. A single "Got it" action, with no extra screens. The driver is likely in the vehicle, and a multi-step confirmation repeats the three-screen problem from UXR-01.
5. Acknowledgment status on the dispatcher's board. Each route change shows Pending or Acknowledged, with a timestamp. This is what replaces waiting for a WhatsApp reply. Without it, the dispatcher still can't tell whether the change landed, so the workaround survives.
- **What I demoted from Must → Should/Won’t, and why:** Fixing the root cause of the sync delay and board lag (BUG-2044, BUG-2072). This was the hardest call, because board distrust (UXR-09) is half of the moment of misery. But it's a sync rebuild that 2 engineers can't deliver in 4 weeks. B6 works around the delay rather than fixing it, and the rebuild goes on the roadmap as the next Major Project.
Unacknowledged flag after 2 minutes. The Pending status already shows the dispatcher that a change hasn't been confirmed. The flag makes that more visible but doesn't make the loop work.
A "Delivered" status separate from "Acknowledged." Pending and Acknowledged are enough to replace waiting for a WhatsApp reply. Telling "no signal" apart from "not responding" is useful, but not essential.

## Generate your Simplified PRD
- **One thing my PRD makes explicit that a vague brief would have missed:** My PRD makes explicit what "acknowledged" means: the driver confirmed the exact latest version of their route with one tap, and that confirmation was recorded. A vague brief ("push alerts on route changes") would have missed three rules that follow from this: tapping the alert must load the new route, never a stale one; an acknowledgment of a superseded alert is rejected; and the board never shows Acknowledged without a recorded acknowledgment event. Without them, the board could show green while a driver is still on the wrong route, which recreates UXR-02's moment of misery and makes the primary metric meaningless.

## Prompt-to-prototype sprint
- **Where did the prototype reveal a gap in my PRD logic? (what I had to update):** Functional requirement 1, Instant trigger: saving a route change creates an alert within 10 seconds, independent of route sync.
- **My prototype, as a link or a screenshot (publish or share from your tool; in Lovable that is Share → Share Preview, in Bolt Publish → Web. No share URL? Screenshot the working flow):** https://lovable.dev/preview/57eKmdFb9MvTDUKR1t8nAxyL6fl4M8rj
