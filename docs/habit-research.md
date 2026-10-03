# Habit research

What the science says about building habits, and what existing apps do. Used to
decide which features Déclic needs and why. Checked 2026-10-03.

Each finding notes how strong the evidence is, because not all of it is equal.

## How habits work

### Habits are triggered by context, not by motivation
A habit is a link in memory between a context (a place, a time, a previous
action) and an action. Once the link is strong, the context triggers the action
almost automatically, and goals or motivation barely matter anymore. When the
context disappears (moving house, holidays), the habit weakens and people fall
back on motivation.

- Wood & Neal (2007), *A new look at habits and the habit-goal interface*, Psychological Review
- Neal, Wood, Labrecque & Lally (2012), *How do habits guide behavior?*, J. of Experimental Social Psychology
- Evidence: strong, decades of research.

For Déclic: this is exactly why showering before school worked and weekends
didn't. Habits need a stable cue. A place is one of the best cues, which is
what the NFC tag gives.

### It takes months, not 21 days
In a 12-week study, the median time for a daily behavior to become automatic was
66 days, with a range of 18 to 254 days. Simple behaviors (a glass of water)
were faster than complex ones (exercise). A large study using gym check-in data
found the gym habit takes around six months, while handwashing at work takes a
few weeks.

- Lally et al. (2010), *How are habits formed*, European J. of Social Psychology
- Buyalskaya et al. (2023), *What can machine learning teach us about habit formation?*, PNAS
- Evidence: Lally is the reference study but small (96 people, 39 modeled). Buyalskaya is large (30,000+ gym members).

For Déclic: the "21 days" idea is a myth. The app should think in months, and
show progress in a way that stays meaningful after day 21.

### Missing once doesn't break a habit
In Lally's study, a single missed day had almost no effect on habit strength.
What hurts is the reaction to the miss: giving up after a slip.

- Lally et al. (2010)
- Evidence: moderate.

## What helps

### Planning when and where (if-then plans)
Deciding in advance "when X happens, I will do Y" has a medium-to-large effect
on reaching goals across 94 studies. The effect is smaller for complex, ongoing
behaviors like exercise.

- Gollwitzer & Sheeran (2006), meta-analysis, Advances in Experimental Social Psychology
- Evidence: strong.

For Déclic: when creating a habit, ask where and after what it happens.

### Anchoring a new habit to an existing one
People who flossed right after brushing their teeth built a stronger habit than
those who flossed before.

- Judah, Gardner & Aunger (2013), British J. of Health Psychology
- Evidence: weak, small exploratory study. Matches the rest of the research on cues though.

For Déclic: grouping habits into a routine (skincare + teeth) makes sense.

### Tracking progress
Monitoring progress has a real effect on reaching goals. The effect is bigger
when progress is physically recorded or shared with others.

- Harkin et al. (2016), meta-analysis, Psychological Bulletin
- Evidence: strong.

For Déclic: tracking isn't decoration, it's part of what works. Sharing could
add more, which supports the social idea for later.

### Slack in the goal: skip days
People with a goal framed with emergency reserves ("gym 7 days a week, with 2
skip days") came back after a failure more often than people with the same goal
framed without them ("gym 5 days a week"). In a large gym study, the single
most effective of 54 interventions was a small reward for coming back after a
missed workout.

- Sharif & Shu (2017, 2019), J. of Marketing Research / Organizational Behavior and Human Decision Processes
- Milkman et al. (2021), *Megastudies improve the impact of applied behavioural science*, Nature
- Evidence: good.

For Déclic: built-in skip days, and celebrate the comeback rather than punish the miss.

### Restricting your future self (commitment devices)
People willingly set up arrangements that take options away from their future
self, because they know that self will be tempted. "Hard" devices have real
consequences, "soft" ones only psychological ones. When given the choice, many
people pick a weak version that doesn't bite.

- Bryan, Karlan & Nelson (2010), *Commitment Devices*, Annual Review of Economics
- Evidence: good.

For Déclic: the app is a commitment device. The strictness should be chosen
calmly in advance, and be harder to weaken in the moment than to set up.

### Locking a pleasure behind the hard thing (temptation bundling)
Students who could only listen to their favorite audiobooks at the gym went 51%
more often at first. The effect faded after a holiday break. Afterwards, 61%
were willing to pay to keep the restriction.

- Milkman, Minson & Volpp (2014), *Holding the Hunger Games Hostage at the Gym*, Management Science
- Evidence: good, but the effect fades after disruptions.

For Déclic: this is close to the core mechanism (TikTok behind skincare). The
fade after holidays matters: the app should help people restart after a break.

### Friction works, even small
An app that shows a short pause before opening a chosen app made people give up
36% of their attempts, and over six weeks they tried to open those apps 37% less.

- Grüning, Riedel & Lorenz-Spreen (2023), *Directing smartphone use through the self-nudge app one sec*, PNAS
- Evidence: good (280 people, 6 weeks).

For Déclic: a waiting delay on the emergency unlock has evidence behind it.

### Fresh starts
Motivation spikes at "temporal landmarks": a new week, a new month, a birthday,
after a holiday.

- Dai, Milkman & Riis (2014), *The Fresh Start Effect*, Management Science
- Evidence: good.

For Déclic: after a bad week, a new week is a natural moment to restart.

### Make it easy rather than relying on motivation
Behavior happens when motivation, ability and a prompt meet at the same moment.
Making the behavior easier is more reliable than raising motivation. Fogg
suggests starting tiny, anchoring, and celebrating.

- Fogg (2009, 2019), *Tiny Habits*
- Evidence: the model is widely used. The celebration step is mostly practitioner experience, not tested.

For Déclic: a "minimum version" of a habit could count on bad days.

## What hurts

### Reminders can create dependency
A study comparing cues found that reminders helped people repeat a behavior but
slowed down the habit becoming automatic. Event-based cues (doing it after
something that already happens) built more automaticity. Positive reinforcement
in the app had no effect. A review of 115 habit apps found almost all of them
rely on tracking and reminders, and none support event-based cues.

A follow-up found people stopped their habits when they stopped using the app:
the habit was tied to the app, not to their life.

- Stawarz, Cox & Blandford (2015), *Beyond self-tracking and reminders*, CHI
- Renfree et al. (2016), *Don't kick the habit: the role of dependency in habit formation apps*, CHI
- Evidence: moderate (HCI studies, smaller samples).

For Déclic: this supports the core idea, since the tag cue is an event and a
place, not a notification. But it's also a warning: the blocking could become
the only reason the habit happens. A later feature could loosen the blocking as
a habit gets stronger.

### Streaks cut both ways
An intact streak makes people more likely to keep going. A broken streak makes
them more likely to quit the behavior entirely, because keeping the streak had
become a goal in itself. Letting people repair a broken streak reduces that drop.

- Silverman & Barasch (2023), *On or Off Track: How (Broken) Streaks Affect Consumer Decisions*, J. of Consumer Research
- Evidence: good (seven studies, real behavior).

For Déclic: streaks are useful, but they need a repair or freeze mechanism, and
shouldn't be the only measure of progress.

## ADHD

ADHD is described as a problem of self-regulation and executive function rather
than of knowledge or will. Two ideas from Barkley are relevant: "time blindness"
(future consequences don't feel real until they're urgent) and "point of
performance" (support works when it's placed exactly where and when the
behavior has to happen). External structure and immediate consequences help
more than reminders of long-term goals.

- Barkley, *Executive Functions* (2012) and related work
- Evidence: expert framework from clinical research, not tested on apps like this one.

For Déclic: an NFC tag next to the mirror is a point-of-performance tool. The
blocked app gives an immediate consequence instead of a distant one.

## Existing apps

### Habit trackers
| App | Platform | What stands out |
|---|---|---|
| Loop Habit Tracker | Android | Free, open source, offline. Has a "habit strength" score instead of only streaks. |
| HabitKit | iOS, Android | GitHub-style grid of completed days. |
| HabitNow | Android | Habits plus tasks and a calendar, one-time purchase. |
| Streaks | iOS only | Simple chain counter, one-time purchase. |
| Way of Life | iOS, Android | Yes / No / Skip logging, long-term trends. |
| Habitica | All | Turns habits into an RPG, with group accountability. |
| Finch | iOS, Android | Gentle self-care with a virtual pet. |
| Tiimo | All | Visual day planner built for ADHD. |
| Routinery | iOS, Android | Runs a routine step by step with timers. |

### App blockers
| App | What stands out |
|---|---|
| Opal (iOS) | Scheduled focus sessions, analytics. Easy to end a session outside its strict mode. ~$100/year. |
| one sec | A pause before opening an app. The one with the PNAS study. |
| ScreenZen | Free, delays that grow each time you open an app. |
| Brick | $59 physical NFC puck. Tap to block, tap to unblock. 5 emergency unlocks, refilled only by contacting support. Strict mode prevents deleting the app. |
| Lock (Android) | Free NFC tag blocker, offline. |
| Clearspace | You do push-ups to unlock apps. The closest to "habit as the key", but the task is generic. |
| TaskGate | A small task (breathing, affirmation) before a blocked app opens. |
| unhookd | Apps locked by default, open only in chosen windows. |

### The gap
Habit trackers record, remind and reward, but have no teeth. Blockers have teeth
but don't know anything about your habits. A few blockers ask for a task before
unlocking, but the task is generic and happens inside the phone. None of them
tie the unlock to a real habit, done in the place where it happens, and track
it as a habit.
