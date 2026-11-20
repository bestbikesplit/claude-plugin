---
name: plan-a-race
description: "Create a Best Bike Split race plan for an upcoming event: find the course, choose the bike, set the goal and conditions, then build and read back the pacing plan. Use when the user asks to build, create or make a race plan or pacing plan, or to plan power for a race. Requires Premium and a connection that can make changes."
---

# Plan a Race

Builds a saved race plan. This writes to the user's account, so collect the inputs, confirm them, then create once.

## How to work

1. **Check the account.** Call `whoami`. Stop early if the account is Basic (offer `get_upgrade_info`) or the connection is read-only (the user reconnects and chooses "Read and make changes").
2. **Read what is already saved.** `get_athlete_profile` for FTP, weight and units; `list_bikes` for bikes. For a coach planning for an athlete, get the athlete from `list_my_athletes` and pass that athlete ID on every call; the course and bike must be the athlete's own.
3. **Find the course.** Look in `list_courses` first, then `search_public_courses` by race name or location. If it is not there, the user can give a direct link to a GPX or FIT file (`create_course_from_url`) or import a connected RideWithGPS route (`import_rwgps_route`). Show a short list of real matches and let the user choose.
4. **Ask for what cannot be looked up.** Ask these together, once:
   - race date and start time (the start time drives the weather);
   - the main road surface, from perfect track to rough chip seal, gravel or dirt. This is required; do not guess it;
   - the event type: triathlon, time trial, road race, mountain bike, gravel or other. Do not assume every event is a time trial;
   - one goal: a normalized power target, a finish time, or a TSS target.
5. **Confirm, then create.** Summarize the course, bike, date, surface, event type and goal in a few lines and get a yes. Then call `create_race_plan` once, with a small `max_segments` such as 10 since you only need the result and the plan ID.
6. **Read it back.** Report the predicted time, normalized power and average power, the weather used, and every item in `plan_warnings`. Use the plan's saved name and ID.
7. **Offer what comes next.** A briefing (`race-briefing`), sending the plan to a bike computer or calendar, or a rehearsal workout (`race-rehearsal`).

If no Best Bike Split tools are available in this conversation, the account is not connected yet. Say so, point the user to https://www.bestbikesplit.com/connect-best-bike-split-to-ai-apps for the two-minute setup, and stop there.

## Get these right

- **One goal only.** Give a power target, a time target or a TSS target, not two. Conflicting goals are rejected.
- **The power goal is normalized power, not average power.** Say "NP" when you confirm it, and compare the result's normalized power with the goal.
- **Weather.** Leave the default so the forecast is fetched along the course for the race date and time. More than 14 days out, the plan uses historical weather as a placeholder: say so, and suggest refreshing within 14 days of the race. Refreshing is its own action; do it only when asked.
- **Manual weather** is used only if the user asks for it and gives the numbers, in the athlete's units.
- **Limits are model settings.** A maximum segment power or maximum descent speed shapes the plan; it is not a guarantee, and a modeled descent speed is not advice about a safe road speed.
- **Do not rebuild to preview.** Each create saves a new plan and each update changes a saved one. To try a different goal, ask first whether the user wants a second plan or a change to this one.
- **Describe results, not the engine.** Explain the plan in terms of power, speed, time and conditions. Do not speculate about how the plan is calculated.

## Rules that always apply

- **A review changes nothing.** Do not refresh weather, re-import a ride, edit a plan or bike, or send or schedule anything just to complete a review. Do those only when the user asks for that action.
- **Use saved names.** Show each plan, ride or workout by its saved name first with its ID beside it, plus the date or course when two look alike. Never swap a name for a bare ID or a label you made up such as "pre-race plan".
- **Report what the records show.** Give units and where each number came from. Keep what was observed separate from possible explanations, and say when data is missing instead of filling it with a default. Missing analytics are not zero events.
- **Premium.** Athlete data needs Best Bike Split Premium. If a tool says an upgrade is required, explain that plainly, call `get_upgrade_info` for the upgrade link, and do not try other tools to get around it.
- **Access errors are final.** On a not-found or not-accessible error, stop that lookup and ask the user for the right account or record. Do not guess other IDs or retry in a loop.
- **Approval links.** Sending, scheduling and deleting return `approval_required` with a Best Bike Split link. Give the user the link and stop: they open it and choose Approve themselves. Never open or submit it for them. When they confirm, retry the same tool with the same arguments once. If they decline, nothing has changed and you do not try another route.
