# Shape Up Pitch Template

**Author:** Ryan Singer (Basecamp)
**Source:** [Shape Up - Chapter 6: Write the Pitch](https://basecamp.com/shapeup/1.5-chapter-06)
**Category:** Planning / Documentation
**Last Updated:** January 2026

---

## The Five Ingredients

Every pitch needs all five components to be ready for betting:

1. **Problem** - Why this matters
2. **Appetite** - How much time it's worth
3. **Solution** - What we'll build (rough)
4. **Rabbit Holes** - Known risks to flag
5. **No-Gos** - What we're explicitly NOT doing

---

## Pitch Structure

```markdown
# [Feature Name]

## Problem

[Describe the specific situation that doesn't work today.
Use a story or scenario. Show the friction.]

## Appetite

[State the time budget: Small Batch (1-2 weeks) or Big Batch (6 weeks)]

## Solution

[Breadboards, fat marker sketches, and explanation.
Show the main elements and how they connect.
Keep it rough but solved.]

## Rabbit Holes

[List specific risks worth flagging:
- Technical unknowns
- Integration challenges
- Design complexity]

## No-Gos

[Explicitly state what's out of scope:
- Features we won't include
- Use cases we won't handle
- Platforms we won't support]
```

---

## Ingredient 1: Problem

### What Makes a Good Problem Statement

**Shows specific friction:**
- Real scenario, not abstract complaint
- Names who experiences the problem
- Describes what goes wrong

**Provides baseline:**
- What customers do today
- Why current approach doesn't work
- Evidence the problem matters

### Examples

**Weak:**
> Customers want a calendar feature.

**Better:**
> Customers can't see upcoming appointments at a glance, so they miss scheduled calls.

**Best:**
> When a loan officer opens Homebot, they see their client list but have no visibility into upcoming appointments. Sarah (LO at Guild) told us she missed two client calls last month because she "forgot to check her calendar app." She wants appointment reminders where she already is - in Homebot.

**The difference:**
- Weak: Feature request (what they want)
- Better: Friction statement (what's broken)
- Best: Story with evidence (why it matters)

---

## Ingredient 2: Appetite

### Stating the Appetite

Be explicit about the time budget:

**Small Batch:**
> **Appetite: Small Batch (1-2 weeks)**
> This is a focused improvement to an existing flow. One designer and one programmer can ship this in under two weeks.

**Big Batch:**
> **Appetite: Big Batch (6 weeks)**
> This is a new capability requiring new UI, backend logic, and integration work. Worth a full cycle investment.

### Appetite Drives Scope

The appetite constrains what solution is acceptable:

| Appetite | Solution Scope |
|----------|---------------|
| 1-2 weeks | Fix the specific friction, nothing more |
| 6 weeks | Build the complete feature, but no gold-plating |

**If the shaped solution doesn't fit the appetite:**
- Reduce scope (cut features)
- Split into multiple pitches
- Revisit whether the problem is worth solving

---

## Ingredient 3: Solution

### What to Include

**Breadboards** for workflow:
```
[Dashboard]
    |
    └── "Upcoming" widget
            |
            ├── Shows next 3 appointments
            ├── Each row: Client name, date, time
            └── "View all" link → [Calendar page]
```

**Fat marker sketches** for layout:
```
┌─────────────────────────────┐
│  Dashboard                  │
├─────────────────────────────┤
│  ┌─────────┐  ┌──────────┐  │
│  │ Clients │  │ Upcoming │  │
│  │  List   │  │ Appts    │  │
│  │         │  │ • Call   │  │
│  │         │  │ • Review │  │
│  │         │  │ • Call   │  │
│  └─────────┘  └──────────┘  │
└─────────────────────────────┘
```

**Explanatory text:**
- How elements connect
- Key interactions
- Why this approach (briefly)

### What NOT to Include

- Pixel-perfect mockups
- Exact copy/labels
- Visual design (colors, fonts)
- Every edge case
- Implementation details

**The test:** Could a designer read this and have freedom to make it their own?

---

## Ingredient 4: Rabbit Holes

### What to Flag

**Technical unknowns:**
> - We've never integrated with Google Calendar before. Need to confirm OAuth flow works with our auth system.

**Integration challenges:**
> - Appointment data lives in the CRM. API calls might be slow - may need caching.

**Design complexity:**
> - Timezone handling could get tricky if LOs travel. Flagging for design to consider.

**Scope creep risks:**
> - Tempting to add recurring appointments, but that's a rabbit hole. See No-Gos.

### How to Present

Be specific, not vague:

**Weak:**
> This might be technically challenging.

**Better:**
> The Google Calendar API has rate limits (10 requests/second). If an LO has 500 clients, syncing appointments could take 50+ seconds. We should either paginate or use webhooks for real-time sync.

---

## Ingredient 5: No-Gos

### What to Exclude

**Features that expand scope:**
> - **No recurring appointments.** Manual entry only for v1.
> - **No two-way sync.** Homebot displays appointments, doesn't create them.

**Use cases we won't handle:**
> - **No multi-timezone support.** Appointments display in LO's local time only.
> - **No mobile push notifications.** Email reminders only.

**Platforms/contexts:**
> - **No mobile app changes.** Dashboard widget is web-only for this pitch.

### Why No-Gos Matter

**For the betting table:**
- Shows you've thought about scope
- Prevents "while we're at it" additions
- Makes appetite believable

**For the team:**
- Clear boundaries during execution
- Permission to say "that's out of scope"
- Prevents scope creep mid-cycle

---

## Complete Pitch Example

```markdown
# Upcoming Appointments Widget

## Problem

Loan officers using Homebot can't see their upcoming appointments without
switching to their calendar app. Sarah Chen (Guild Mortgage) told us she
missed two client calls last month because she "forgot to check her calendar."
She's in Homebot daily but appointments are invisible there.

This friction is common. In our last 10 user interviews, 6 mentioned wanting
appointment visibility inside Homebot.

## Appetite

**Big Batch (6 weeks)**

This requires calendar integration, new dashboard component, and reminder
system. Worth a full cycle to get right.

## Solution

### Dashboard Integration

[Dashboard]
    |
    └── "Upcoming" widget (right sidebar)
            |
            ├── Shows next 5 appointments (chronological)
            ├── Each row: Client name, date/time, appointment type
            ├── Click row → Client detail page
            └── "Sync Calendar" link → [Calendar Settings]

### Fat Marker Sketch

┌─────────────────────────────────┐
│  Dashboard                      │
├──────────────────┬──────────────┤
│                  │  UPCOMING    │
│   Client List    │  ─────────── │
│                  │  Tomorrow    │
│   [existing]     │  • J. Smith  │
│                  │    10am call │
│                  │  Thursday    │
│                  │  • M. Jones  │
│                  │    2pm review│
│                  │              │
│                  │  [Sync Cal]  │
└──────────────────┴──────────────┘

### Calendar Sync Flow

[Calendar Settings]
    |
    ├── "Connect Google Calendar" button
    │       ↓
    │   [Google OAuth flow]
    │       ↓
    │   [Select calendars to sync] (checkboxes)
    │       ↓
    │   "Save" → webhooks registered, initial sync
    │
    └── Connected calendars list
            └── "Disconnect" option per calendar

### Email Reminders

- Daily digest email at 7am: "You have 3 appointments today"
- Links to client profiles in Homebot
- Unsubscribe option

## Rabbit Holes

- **Google Calendar API rate limits:** 10 req/sec. Initial sync for LOs with
  many appointments could be slow. Solution: queue syncs, show progress bar.

- **Timezone handling:** Appointments should display in LO's local timezone.
  Need to store timezone preference. Don't attempt multi-timezone display.

- **OAuth token refresh:** Google tokens expire. Need background job to
  refresh before expiration. If refresh fails, surface error in UI.

## No-Gos

- **No Outlook/iCal support.** Google Calendar only for v1.
- **No two-way sync.** We display appointments, don't create them.
- **No recurring appointment handling.** Each occurrence is a separate event.
- **No mobile push notifications.** Email reminders only.
- **No appointment creation from Homebot.** Read-only integration.
```

---

## Common Pitch Mistakes

### Problem Too Vague
- "Users want better organization"
- "The dashboard is cluttered"

**Fix:** Find the specific friction. Who? When? What breaks?

### Solution Too Detailed
- Full wireframes
- Exact copy
- Every state and edge case

**Fix:** Step back to breadboards. Leave room for team creativity.

### Missing Rabbit Holes
- "Should be straightforward"
- No technical risks mentioned

**Fix:** Walk through implementation mentally. What could go wrong?

### No-Gos Not Explicit
- Scope boundaries assumed, not stated
- "We'll figure out what to cut later"

**Fix:** Decide what's out NOW. Write it down.

### Appetite Mismatch
- Big feature crammed into small batch
- Tiny improvement given 6 weeks

**Fix:** Reshape or re-scope. Appetite drives what's possible.

---

## Using Pitches

### Before Betting
- Post asynchronously for review
- Colleagues comment with questions/concerns
- Shaper addresses feedback or updates pitch

### At the Betting Table
- Review pitched work (not a backlog)
- Decide which pitches get cycles
- Assign teams to winning bets

### After Betting
- Winning pitches go to teams as starting point
- Teams own execution (not the pitch author)
- Pitch provides boundaries, not instructions

---

## Resources

- [Shape Up - Chapter 6: Write the Pitch](https://basecamp.com/shapeup/1.5-chapter-06)
- [Shape Up - Complete Examples](https://basecamp.com/shapeup/1.5-chapter-06#examples)
