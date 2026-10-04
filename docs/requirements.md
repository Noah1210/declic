# Requirements

What v1 does, sorted with MoSCoW:

- **Must**: v1 isn't done without it
- **Should**: in v1 if time allows, planned for
- **Could**: nice to have, first to cut
- **Won't**: explicitly not in v1

Based on the [vision](vision.md) and the [habit research](habit-research.md).

## Words used

- **Habit**: something to do N times per day or per week (skincare 2×/day, gym 3×/week).
- **Completion**: one logged instance of a habit, with a time and an optional amount.
- **Lock**: a group of blocked apps, with a relock rule, the tags that open it, and the habits it's linked to.
- **Tag**: a physical NFC tag registered in the app.
- **Unlock**: what opens a lock. A tag scan, a wait unlock or an emergency unlock.

Unlocking and completing a habit are separate on purpose. Scanning a tag in the
middle of the day without doing the routine shouldn't count as done.

## Habits

| ID | Story | Priority |
|---|---|---|
| H1 | As a user, I want to create a habit with a name and a frequency (N times per day or N times per week), so it matches how often I actually do it. | Must |
| H2 | As a user, I want to note where and after what I do a habit ("at the bathroom mirror, after waking up"), so I have a clear plan. | Must |
| H3 | As a user, I want to log a habit as done, up to 24 hours later, with the time I actually did it, so logging never gets in my way. | Must |
| H4 | As a user, I want to add an optional amount to a habit (2 hours, 10 km) with an optional target, so I can track how much and not only whether. | Should |
| H5 | As a user, I want to edit and archive habits without losing their history. | Must |
| H6 | As a user, I want a list of common habits to start from, so creating my first ones is quick. | Could |

## Locks

| ID | Story | Priority |
|---|---|---|
| L1 | As a user, I want to create a lock by choosing which apps it blocks, so I only block my distractions. | Must |
| L2 | As a user, I want a lock to come back N hours after my last unlock, so it works without a fixed schedule. | Must |
| L3 | As a user, I want a lock to come back at fixed times of day, for when I do have a schedule. | Must |
| L4 | As a user, when I open a blocked app, I want Déclic's lock screen to appear over it, showing which lock is active, with the ways to open it (scan, start the wait timer, emergency). Going back from it takes me home, not into the blocked app. | Must |
| L5 | As a user, I want to link a lock to one or more habits, so after unlocking, the app asks me about them. The question can be answered later and never blocks the unlock. | Must |
| L6 | As a user without my tag nearby, I want a wait unlock: I start a timer (5 minutes by default, set per lock), go do the routine, and the apps open when it ends. Once open, they stay open until the next relock, like after a scan. | Must |
| L7 | As a user, I want a limited instant emergency unlock (default 1 per week), for real emergencies. | Must |
| L8 | As a user, I want locks to keep working after my phone restarts. | Must |
| L9 | As a user, I want clear setup screens explaining each permission (accessibility, NFC, battery) and why it's needed. | Must |
| L10 | As a user, I want changes that loosen a lock to apply only the next day, and to be asked that day if I still want them, so I can't weaken a lock in a weak moment. | Should |
| L11 | As a user, I can never block the phone app or Déclic itself. | Must |

## Tags

| ID | Story | Priority |
|---|---|---|
| T1 | As a user, I want to register an NFC tag and link it to one or more locks. | Must |
| T2 | As a user, I want scanning a registered tag to unlock its locks instantly, with no extra step. | Must |
| T3 | As a user, I want to use several tags. | Must |
| T4 | As a user, I want a tag that starts a lock when I scan it (bedside, before sleep). | Should |
| T5 | As a user, if I lose a tag, I want its locks to switch to wait unlock until I register a new tag, then go back to the tag. | Must |
| T6 | As a user without an NFC tag, I want to use the app fully for tracking, and use locks that open with a wait unlock only. | Should |
| T7 | As a user without an NFC tag, I want to use a printed QR code instead. | Should |

## Tracking

| ID | Story | Priority |
|---|---|---|
| S1 | As a user, I want a current streak per habit, counted in days or weeks depending on its frequency. | Must |
| S2 | As a user, I want to restore a broken streak (3 times a month), so one bad day doesn't erase my progress. | Must |
| S3 | As a user, I want a calendar history for each habit. | Must |
| S4 | As a user, I want a completion rate for each habit. | Must |
| S5 | As a user, I want a detail page for each habit with its stats. | Must |
| S6 | As a user, I want a weekly summary. | Should |
| S7 | As a user, I want my unlock history (scans, wait unlocks, emergency unlocks). | Should |
| S8 | As a user, I want a monthly and yearly summary. | Could |
| S9 | As a user, I want to see my best streak. | Could |

## Pause

| ID | Story | Priority |
|---|---|---|
| P1 | As a user, I want to pause some habits and locks for a period (sick, holidays), without breaking streaks. | Could |

## General

| ID | Story | Priority |
|---|---|---|
| G1 | As a user, I want the app in English and French. | Must |
| G2 | As a user, I want to use the app without creating an account. | Must |

## Won't have in v1

- iOS
- Accounts, backend, sync, export and import (accounts stay optional when they come)
- Notifications as the main cue (the lock is the reminder)
- Proof that a habit was actually done
- Social features
- Heavy gamification, ads, payments
- Selling or linking to NFC tags

## Quality attributes

In order of priority, with how each one gets checked.

1. **Blocking reliability.** A blocked app never stays usable during a lock, including after a restart. Checked by two weeks of daily use on the Galaxy A15.
2. **Smooth unlock.** Scanning a tag unlocks in under 2 seconds, with no screen to go through. Checked on the device.
3. **Privacy.** No data leaves the phone in v1. No analytics. Only the permissions the features need.
4. **Battery.** Déclic doesn't show up as a heavy battery user in Android's battery settings over a normal day.
5. **Maintainability.** The domain rules (streaks, relock timing, unlock limits) are plain Kotlin covered by unit tests.

## Constraints

- Developed on Windows, no Mac
- Android first, tested on a Samsung Galaxy A15 (Android 15). Supports a wide range of Android versions.
- Solo developer
- Blocking relies on Android's AccessibilityService, so Google Play rules apply when it's published.

## Decided

- A wait unlock takes 5 minutes by default and opens the apps until the next relock.
- Habits can be logged up to 24 hours late.
- A lost tag switches its locks to wait unlock until it's replaced.
