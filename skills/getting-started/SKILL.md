---
name: getting-started
description: "Get oriented with Best Bike Split in Claude: check the connection, the account tier and what can be done. Use when the user asks what Best Bike Split can do here, how to connect it, whether their account is connected, or what to try first."
---

# Getting Started with Best Bike Split

Shows the user where they stand and what they can ask for.

## How to work

1. Call `whoami`. It reports the account tier, whether the account is a coach, whether the connection is read-only, and the toolset version.
2. Call `get_workflow_guide` with `workflow: "catalog"` to get the current list of guided reviews, with an example request for each.
3. Tell the user, briefly:
   - who is connected and on which tier;
   - whether this connection can make changes or is read-only;
   - three or four things worth trying, picked from the catalog to suit them (a coach gets the coach overview; someone with an upcoming plan gets the race briefing).
4. Offer one next step. Do not start a review they did not ask for.

If no Best Bike Split tools are available in this conversation, the account is not connected yet. Say so, point the user to https://www.bestbikesplit.com/connect-best-bike-split-to-ai-apps for the two-minute setup, and stop there.

## What needs what

- **Basic account:** connection status, upgrade information and the list of guided reviews. Athlete data and actions need Best Bike Split Premium. If the account is Basic, say so plainly and call `get_upgrade_info` for the upgrade link.
- **Read-only connection:** questions and analysis only. To create plans or workouts, or send to a device or calendar, the user reconnects and chooses "Read and make changes".
- **Partner data:** TrainingPeaks, Intervals.icu, Garmin, Wahoo and Zwift are connected in Best Bike Split itself, on the website or in the app. `list_connections` shows what is linked.

## Skills in this plugin

- Before a race: `plan-a-race`, `race-briefing`, `race-rehearsal`, `compare-plans`
- After a ride: `race-review`, `plan-vs-ride`, `compare-rides`, `ride-dynamics`, `aero-review`
- Training: `build-workout`, `workout-check`, `weekly-review`
- Coaches: `coach-overview`
- Troubleshooting: `connection-check`

## Rules that always apply

- **A review changes nothing.** Do not refresh weather, re-import a ride, edit a plan or bike, or send or schedule anything just to complete a review. Do those only when the user asks for that action.
- **Use saved names.** Show each plan, ride or workout by its saved name first with its ID beside it, plus the date or course when two look alike. Never swap a name for a bare ID or a label you made up such as "pre-race plan".
- **Report what the records show.** Give units and where each number came from. Keep what was observed separate from possible explanations, and say when data is missing instead of filling it with a default. Missing analytics are not zero events.
- **Premium.** Athlete data needs Best Bike Split Premium. If a tool says an upgrade is required, explain that plainly, call `get_upgrade_info` for the upgrade link, and do not try other tools to get around it.
- **Access errors are final.** On a not-found or not-accessible error, stop that lookup and ask the user for the right account or record. Do not guess other IDs or retry in a loop.
