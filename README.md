# Pronto — Self-serve recovery with live visit status

An interactive, clickable prototype of a single proposed feature for **Pronto** (withpronto.com),
the on-demand house-help platform. Open `index.html` in any browser — no build step, no
dependencies, no network calls.

---

## The problem this feature addresses

Today a Pronto booking has **two states the customer can see: "booked" and "done."** Everything in
between — is the Pro actually coming, are they nearby, did something go wrong — is invisible. So the
customer's only tool when something feels off is to contact support and ask.

That produces a support queue full of contacts that were never really support problems:

| What the customer contacts support about | What it actually is |
|---|---|
| "Where is my Pro?" | A visibility gap the app could have answered itself |
| "I want to cancel, it's very late" | A self-serve action that isn't available |
| "Where is my refund?" | A status the app never shows |
| Re-explaining to a second agent | Context that was never attached to the ticket |

And the queue itself is only staffed roughly **7 AM – 10 PM** while booking is marketed as 24/7 —
nine hours a day where a customer can book but cannot reach help if it fails.

**The insight this prototype is built on:** the best support fix is making most contacts unnecessary,
and resolving the rest on first touch — not adding headcount.

---

## What the feature is

One always-on screen per booking that does two jobs at once:

1. **Live visit status** — the visit is visible while it happens, so the customer never has to wonder.
2. **Self-serve recovery** — when something breaks, the customer fixes it themselves, in the same screen.

Neither half works alone. Visibility without recovery just shows you your Pro is late. Recovery
without visibility means you don't know something's wrong until you go looking.

### The states, and what's attached to each

| State | What the customer sees | What they can do without a human |
|---|---|---|
| **Assigned** | Pro's name/photo, live ETA *window* (a range, not a fixed promise) | Nothing needed yet — just visibility |
| **On the way** | The window narrowing in real time | Nothing needed |
| **ETA slipping** | "Running later than expected — revised arrival 10:57" | Wait with a real number, or open a structured report |
| **Pro unreachable** | "We've lost contact and are checking" — volunteered early | Nothing; automatic resolution clock is already running |
| **Grace period exceeded (no-show)** | "Your Pro didn't arrive" — flagged automatically, not by the customer noticing | One tap → full refund initiated, no ticket, no waiting |
| **Arrived / In progress** | "Started at 10:42" + the task checklist ticking off live | Nothing needed — this is the anti-black-box part |
| **Issue reported** | Chosen from categories, not a free-text box | Watch it move: Reported → Checked automatically → Resolved |
| **Completed** | Final summary: tasks, times, charges, credits | Nothing to fix, nothing to ask |

---

## Three design decisions the prototype is making

**1. The system is the sensor, not the customer.**
Every transition carries a *"Detected automatically at 11:02"* badge. Nobody should have to notice
it's been 40 minutes and go looking for a help button. The delay credit lands *before* anyone asks.

**2. Structured categories, not a free-text box.**
Free text is deliberately the **last** option. Categories are what make automatic resolution
possible: a no-show is a no-show because the GPS pings and timestamps say so, not because a
customer describes it convincingly. Each category shows the evidence the app has already attached —
so the customer never has to prove anything, and never re-explains to a second agent.

**3. Human support still exists — for a much smaller queue.**
Categories are tagged **Auto** (checkable against the visit record: no-show, lateness, unfinished
tasks, a cash demand on a prepaid booking) or **Human** (genuinely ambiguous: safety concerns,
anything else). Safety is the one path that is always live, 24/7, never queued.

**The trust effect:** a failure the customer can see, that's flagged automatically, with a refund
already moving, reads as *"this company is on top of things"* rather than *"this company is
unreliable."* Same bad outcome, opposite feeling.

---

## How to demo it

Open `index.html`. The phone is flanked by a scenario panel (left) and a live annotation of the
current state (right).

| Control | What it does |
|---|---|
| **Scenario** | *Arrives on time* / *Runs late* / *Never arrives* — same booking, three outcomes |
| **▶ Play** | Runs the simulated clock (1 visit-minute ≈ 0.5s) |
| **Next event ⇥** | Jumps straight to the next thing that happens |
| **↺** | Restarts the scenario |
| **Proposed / Today** | Switches the phone between the proposed feature and today's experience |

**Suggested 90-second walkthrough**

1. **"Never arrives"** → *Next event* until the no-show is confirmed. Point at the
   *Detected automatically* badge — the customer never reported anything.
2. Tap **Refund ₹549 now**. Watch the three-step refund tracker fill in. No ticket was created.
3. Switch to **Today** with the clock past 30 minutes. The screen still says
   "Arriving in 15 minutes." Tap **Help → Chat with us** and land on the free-text box, the
   7 AM–10 PM notice, and the 24-hour response time. That contrast is the pitch.
4. Switch back to **Proposed**, run **"Runs late"** — the credit applies without being asked.
5. Run **"Arrives on time"** to show that in the happy path, recovery never fires: the feature is
   just visibility, and the goal is a support contact that never happens.

---

## How success would be measured

- **Support contact rate per booking**, trending down — the main one. Success is a contact that never happens.
- **Median time from failure to resolved-or-refunded**, trending down.
- **Repeat booking rate after a failed first booking**, converging toward the rate after a successful
  one. Hardest to move, and the one the work should be defended on.

---

## Scope and honesty notes

- **Customer-side only.** Dispatch, payments, and the Pro app are mocked with scripted data. The
  prototype's job is to prove the interaction model is better, not to prove the infrastructure.
- **The "Today" view is a reconstruction**, assembled from public app-store reviews, the live
  withpronto.com site, and press coverage. It is illustrative — not a screenshot of Pronto's app.
- **All money, names, addresses, and timings are fictional sample data.**
- Visual language (green `#05AC5F`, ink `#0C0C0C`, Lexend, rounded pills) is matched to the live
  Pronto site so the proposal reads as native to the product.

## Files

```
index.html    the entire prototype — self-contained, no dependencies
README.md     this file
```
