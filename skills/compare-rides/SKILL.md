---
name: compare-rides
description: "Compare two or a few recorded rides in Best Bike Split: totals, aero results and cornering or acceleration behavior. Use when the user asks to compare rides or races against each other, e.g. \"compare my last two time trials\"."
---

# Compare Recorded Rides

Compares recorded rides without forcing routes to match.

## How to work

1. Call the Best Bike Split `get_workflow_guide` tool with `workflow: "compare_rides"` and follow the steps and rules it returns. The guide is kept on the server and updated with the product, so it is the source of truth; this skill tells you when to use it and how to shape the answer. Load it once per task.
2. Settle what the guide needs before you fetch details (below). Ask only for what is missing, and offer a short list of real candidates rather than an open question.
3. Read summaries first and fetch detail pages only to answer a specific question. The guide's tool list is a menu, not a checklist.
4. Write the answer in the report shape below.

If no Best Bike Split tools are available in this conversation, the account is not connected yet. Say so, point the user to https://www.bestbikesplit.com/connect-best-bike-split-to-ai-apps for the two-minute setup, and stop there.

## Settle first

- Which rides: two, or a small set the user names. Prefer the same athlete and event type.
- What differs between them: bike, surface, conditions, route, duration, sensors.

## Report shape

- Records and context
- Comparable metrics
- Observed changes and limitations

Keep it concise. An HTML report is fine if the user asks for one.

## Watch for

- A different course's corner speed, event count or lower CdA is not proof of better skill or fitness.
- Compare like with like: similar grades and pedaling states, with sample counts and ranges beside the averages.

## Rules that always apply

- **A review changes nothing.** Do not refresh weather, re-import a ride, edit a plan or bike, or send or schedule anything just to complete a review. Do those only when the user asks for that action.
- **Use saved names.** Show each plan, ride or workout by its saved name first with its ID beside it, plus the date or course when two look alike. Never swap a name for a bare ID or a label you made up such as "pre-race plan".
- **Report what the records show.** Give units and where each number came from. Keep what was observed separate from possible explanations, and say when data is missing instead of filling it with a default. Missing analytics are not zero events.
- **Premium.** Athlete data needs Best Bike Split Premium. If a tool says an upgrade is required, explain that plainly, call `get_upgrade_info` for the upgrade link, and do not try other tools to get around it.
- **Access errors are final.** On a not-found or not-accessible error, stop that lookup and ask the user for the right account or record. Do not guess other IDs or retry in a loop.
