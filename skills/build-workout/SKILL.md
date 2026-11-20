---
name: build-workout
description: "Build a structured cycling power workout in Best Bike Split, then optionally export it or put it on a calendar. Use when the user asks to create, write or build a workout or interval session, e.g. \"build me a 2x20 threshold workout\", or to schedule one on TrainingPeaks, Intervals.icu, Garmin or Wahoo. Requires Premium and a connection that can make changes."
---

# Build a Workout

Creates a saved workout made of timed steps at a percentage of FTP.

## How to work

1. **Check the account.** Call `whoami`. Stop early if the account is Basic (offer `get_upgrade_info`) or the connection is read-only.
2. **Look before you build.** `list_workouts` and `browse_workout_library` may already hold what the user wants; offer it if so.
3. **Settle the session.** Purpose, total time, and the event type it supports (triathlon, time trial, road race, mountain bike, gravel or other). Ask only for what the request leaves open.
4. **Lay out the steps and confirm.** Show the session as a short table (step, duration, % of FTP) and get a yes before saving.
5. **Create it** with `create_workout`. For a coach, pass the athlete ID from `list_my_athletes` to save it in that athlete's library.
6. **Read it back.** Report the saved name and ID, total time, intensity factor and TSS, and the event type it was filed under.
7. **Offer what comes next:** a file for an indoor trainer app (`export_workout_file`), or a place on the calendar.

If no Best Bike Split tools are available in this conversation, the account is not connected yet. Say so, point the user to https://www.bestbikesplit.com/connect-best-bike-split-to-ai-apps for the two-minute setup, and stop there.

## Get these right

- **Cycling power only.** Every step is a duration in seconds and a target as a percentage of FTP. Do not write running or swimming sessions this way; say that those are scheduled in TrainingPeaks or Intervals.icu directly.
- **Ramps run from the start value to the end value.** A warm-up goes up (for example 45 to 65), a cool-down goes down (60 to 45). Put the higher value first for anything that should descend.
- **A worked example.** 2 x 20 minutes at threshold: 900 s at 55%, 1200 s at 95%, 300 s at 50%, 1200 s at 95%, 600 s at 45%.
- **Zone totals use Best Bike Split's zone edges** (under 60, 60-75, 76-90, 91-105, 106-120, over 120 percent of FTP). Do not relabel them with another system's names.
- **Scheduling.** `push_workout_to_date` needs the provider and a date. Sending the same workout to the same date again updates it. A different workout on a day that already has one adds a second; clearing the day first removes only entries Best Bike Split created, never the athlete's own.
- **Stay within the athlete's context.** Use the FTP and constraints on file or stated by the user. Do not prescribe all-out efforts or invent physiology.

## Rules that always apply

- **A review changes nothing.** Do not refresh weather, re-import a ride, edit a plan or bike, or send or schedule anything just to complete a review. Do those only when the user asks for that action.
- **Use saved names.** Show each plan, ride or workout by its saved name first with its ID beside it, plus the date or course when two look alike. Never swap a name for a bare ID or a label you made up such as "pre-race plan".
- **Report what the records show.** Give units and where each number came from. Keep what was observed separate from possible explanations, and say when data is missing instead of filling it with a default. Missing analytics are not zero events.
- **Premium.** Athlete data needs Best Bike Split Premium. If a tool says an upgrade is required, explain that plainly, call `get_upgrade_info` for the upgrade link, and do not try other tools to get around it.
- **Access errors are final.** On a not-found or not-accessible error, stop that lookup and ask the user for the right account or record. Do not guess other IDs or retry in a loop.
- **Approval links.** Sending, scheduling and deleting return `approval_required` with a Best Bike Split link. Give the user the link and stop: they open it and choose Approve themselves. Never open or submit it for them. When they confirm, retry the same tool with the same arguments once. If they decline, nothing has changed and you do not try another route.
