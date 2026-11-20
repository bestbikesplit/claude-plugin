# Best Bike Split for Claude

Best Bike Split is a race-planning and power-pacing platform for cyclists and triathletes. This plugin connects Claude to your Best Bike Split account and adds guided workflows for the things athletes and coaches ask for most: building a race plan, briefing a race, reviewing a ride, comparing a plan with what happened, and building workouts.

## What you need

- A Best Bike Split account ([bestbikesplit.com](https://www.bestbikesplit.com) or the mobile app).
- Best Bike Split Premium to read your data and take actions. A Basic account can connect, check its status and see what is available.
- To send workouts or plans to TrainingPeaks, Intervals.icu, Garmin, Wahoo or Zwift, connect those accounts in Best Bike Split first.

## Install

In Claude Code:

```
/plugin install best-bike-split --marketplace bestbikesplit/claude-plugin
```

In the Claude apps, add Best Bike Split from the directory.

## Connecting

The first time a skill needs your data, Claude asks you to sign in to Best Bike Split in your browser. You choose **Read only** (questions and analysis) or **Read and make changes** (also create plans and workouts, and send them). There is no API key to copy and no password is stored in the plugin. Full setup steps are on the [help page](https://www.bestbikesplit.com/connect-best-bike-split-to-ai-apps).

## Skills

| Skill | Use it to |
|---|---|
| `getting-started` | Check your connection and tier, and see what to try |
| `plan-a-race` | Build a race plan: course, bike, goal, weather |
| `race-briefing` | Turn a saved plan into a race-day briefing |
| `race-rehearsal` | Draft a practice session from a plan's targets |
| `compare-plans` | Compare saved plans for the same race |
| `race-review` | Review a recorded race or ride |
| `plan-vs-ride` | Compare the plan with the ride you recorded |
| `compare-rides` | Compare two or more recorded rides |
| `ride-dynamics` | Review cornering, coasting, slowing and acceleration |
| `aero-review` | Weigh the evidence for a position or equipment change |
| `build-workout` | Build a structured power workout, export or schedule it |
| `workout-check` | Check a ride against the workout you planned |
| `weekly-review` | Review a week of training from your connected accounts |
| `coach-overview` | For coaches: which athletes and plans need attention |
| `connection-check` | Find out why a ride or connection is missing |

Claude picks the right skill from what you ask. You can also call one directly, for example `/best-bike-split:race-review`.

## Things to ask

- "Find the Galveston 70.3 course and build a race plan on my TT bike."
- "Give me a briefing for my race plan this weekend."
- "Review my latest time trial, including climbs and cornering."
- "Compare my ride on Saturday with the plan I used."
- "Build a 2x20 threshold workout and put it on my TrainingPeaks calendar for Saturday."

## What this plugin does and does not do

- It contains skills (plain-text instructions) and one connector reference. It has no hooks, scripts or bundled programs, and it runs nothing on your computer.
- It talks to one service: the Best Bike Split connector at `https://www.bestbikesplit.com/mcp`, using your own sign-in. Data from TrainingPeaks, Intervals.icu, Garmin, Wahoo, Zwift and RideWithGPS is reached only through the connections you have already made inside Best Bike Split.
- Reviews never change your account. Actions that send, schedule or delete ask you to approve them on a Best Bike Split page first; Claude cannot approve for you.
- The review skills load their step-by-step guidance from the connector, so they stay current as Best Bike Split changes.

## Privacy and support

- Privacy policy: https://www.bestbikesplit.com/privacy-policy
- Terms of use: https://www.bestbikesplit.com/terms-of-use
- Support: https://support.bestbikesplit.com/
- To disconnect, remove Best Bike Split from Claude's connector settings.

## License

MIT. See [LICENSE](LICENSE).
