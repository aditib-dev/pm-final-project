# GTM Launch Plan, RouteLogic (B2B)

| Field | Value |
|---|---|
| Feature | B6 : Driver Route-Change Alerts. A route change alerts the affected driver the moment it's saved, and the driver confirms with one tap. |
| Goal | Engagement |
| Launch tier | M, Targeted |

## Goal & Audience
- **Goal:** Engagement, B6 is for existing customers, not new ones. Its success depends on dispatchers changing behaviour: making and confirming route changes in RouteLogic instead of WhatsApp (UXR-02). Engagement is the goal that measures that shift. Retention and renewals (UXR-10, complexity churn at 4 of 5 accounts) follow from it, but they're lagging outcomes the launch can't move within weeks.
- **Target audience:** Primary: fleet dispatchers (Coordinators) at existing accounts who reassign routes mid-shift, starting with mid-size 3PLs running WhatsApp groups alongside RouteLogic. Coordinator NPS has fallen 30 points, and 91% of coordinators use the dispatch board daily.
Secondary: drivers at those accounts, whose one-tap acknowledgment the feature depends on, and ops managers at renewal-risk accounts, who decide whether to roll it out.

## Launch Tier
- **M, Targeted**, Reach: existing customers only, no new market. Only accounts with live mid-shift reassignment benefit.
Revenue impact: indirect. It protects renewals rather than creating new revenue.
Risk of silence: high within accounts. If drivers don't know to tap "Got it" and dispatchers don't trust the badge, the WhatsApp group survives and the feature looks like it failed.
That calls for focused, account-by-account communication, not press or paid reach.

## Channels
1. **Owned: In-app announcement and first-use guidance on the dispatcher board, plus a one-time tip on the driver's first alert explaining "Got it." This reaches dispatchers and drivers exactly where the new behaviour happens.**
2. **Owned: CS-led account rollout. The CS lead runs a 30-minute enablement session with each account's dispatch lead and emails ops managers a short "what changes for your team" note. In B2B, adoption is decided per account, not per user.**
3. **Earned: A pilot customer story ("how [account] retired its WhatsApp dispatch group"), with the account's consent, shared in renewal conversations and customer newsletters. Peer proof carries more weight with ops managers than vendor claims.**

## Enablement & Assets
CS one-pager: what the alert does, what Pending and Acknowledged mean, and what happens with no signal.
Driver quick-start card and 30-second video: the alert and the one-tap "Got it."
Support FAQ and known issues: no-signal behaviour, superseded alerts, and the Android crash risk on routes over about 40 stops (BUG-2031).
Admin guide: enabling the feature per account.
Renewal talk track: for account owners at at-risk accounts.
Release notes
Pilot story: one page, once the pilot account agrees.

## Ownership, Budget & Timeline
- **Ownership & budget:** Aditi (PM): owns the plan, the go/no-go decision and post-launch metrics.
John (CS lead): owns account rollout sessions, the ops-manager email, the renewal talk track and the pilot story.
Pedro(Designer): owns the in-app announcement, the driver tip, the quick-start card and the video.
Yuriy(Engineer 1): owns the per-account feature flag and GA rollout.
Eldho(Engineer 2): owns the event timestamps and the metrics dashboard.
Merin(Support lead): briefed before GA; no extra budget.

Budget: no paid spend.

Gaps:
There's no marketing owner, so the pilot story and newsletter sit with the CS lead.
The 30-second video may need outside production budget.
The pilot story depends on customer consent.
- **Timeline:** Phase 1 · Beta (weeks -2 to 4):

Weeks -2 to 0: capture the 2-week baseline.
Weeks 1 to 4: pilot across 3 accounts, with a 50/50 split by driver.
End of week 4: go/no-go decision against the ship rule.

Phase 2 · Launch (weeks 5 to 8):

Week 5: Support briefed; assets finished.
Week 6: GA enabled account by account, each with a CS enablement session and the ops-manager email.
Weeks 7 to 8: in-app announcement live for all enabled accounts; pilot story shared.

Phase 3 · Post-launch (weeks 9 to 12): weekly metric reviews, account check-ins and a decision on what comes next.

## Success Metrics
- **Metrics:** 1. Speed: median time from route change to driver viewing the updated route is under 2 minutes in enabled accounts.
2. Acknowledgment: at least 70% of route changes are acknowledged in-app within 2 minutes.
3. Behaviour: WhatsApp route-change messages per dispatcher per week fall from baseline (self-reported or counted with account consent).
- **Bad signal to watch for:** High acknowledgment rates while WhatsApp use doesn't fall. That would mean drivers are tapping "Got it," but dispatchers still don't trust the board, so the problem is trust, not speed. A second warning sign is acknowledgment rates that drop after week 1, which would point to alert fatigue.
- **Likely post-launch decision:** Double down, if acknowledgment holds at 70% or above and WhatsApp messages fall. That means expanding to all accounts with mid-shift reassignment and funding the board status sync fix (BUG-2072) as the next Major Project. Iterate if speed improves but WhatsApp use doesn't fall: prioritise board trust before any wider rollout.
