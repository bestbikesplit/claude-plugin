---
name: race-review
description: "Review a recorded race or ride from Best Bike Split analytics: power, conditions, aero, climbs and cornering. Use when the user asks to review, debrief or analyze a ride or race they have already done, e.g. \"review my latest time trial\" or \"how did my 70.3 bike leg go\"."
---

# Review a Race or Ride

Explains one recorded ride using the analysis Best Bike Split has saved for it.

## How to work

1. Call the Best Bike Split `get_workflow_guide` tool with `workflow: "race_review"` and follow the steps and rules it returns. The guide is kept on the server and updated with the product, so it is the source of truth; this skill tells you when to use it and how to shape the answer. Load it once per task.
2. Settle what the guide needs before you fetch details (below). Ask only for what is missing, and offer a short list of real candidates rather than an open question.
3. Read summaries first and fetch detail pages only to answer a specific question. The guide's tool list is a menu, not a checklist.
4. Write the answer in the report shape below.

If no Best Bike Split tools are available in this conversation, the account is not connected yet. Say so, point the user to https://www.bestbikesplit.com/connect-best-bike-split-to-ai-apps for the two-minute setup, and stop there.

## Settle first

- Which recording. If the user says "latest", check ride dates and event types: the newest import is not always the most recent race.
- Anything the data cannot show: stops, a crash, a mechanical, or race tactics. Ask once, and carry on with the review whether or not they answer.

## Report shape

- Record and context
- Key supported findings
- Data limitations
- Practical next steps

Keep it concise. An HTML report is fine if the user asks for one.

## Watch for

- Do not infer race placings, exact time lost in corners, or physiological limits from the recording.
- Ordinary coasting and stationary sections are expected; they are not a reason to re-import the ride.

## Rules that always apply

- **A review changes nothing.** Do not refresh weather, re-import a ride, edit a plan or bike, or send or schedule anything just to complete a review. Do those only when the user asks for that action.
- **Use saved names.** Show each plan, ride or workout by its saved name first with its ID beside it, plus the date or course when two look alike. Never swap a name for a bare ID or a label you made up such as "pre-race plan".
- **Report what the records show.** Give units and where each number came from. Keep what was observed separate from possible explanations, and say when data is missing instead of filling it with a default. Missing analytics are not zero events.
- **Premium.** Athlete data needs Best Bike Split Premium. If a tool says an upgrade is required, explain that plainly, call `get_upgrade_info` for the upgrade link, and do not try other tools to get around it.
- **Access errors are final.** On a not-found or not-accessible error, stop that lookup and ask the user for the right account or record. Do not guess other IDs or retry in a loop.
