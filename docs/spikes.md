# Spikes

Throwaway experiments that answer one risky question each, before the real
design. The spike code lives outside this repo. Only the results are kept here.

## Spike A: can my code block an app on my phone?

*2026-10-03, Galaxy A15, Android 15*

**Setup.** An AccessibilityService listens for window changes. When TikTok or
Opera comes to the front and nothing is unlocked, it opens a lock screen
activity on top. The lock screen has a fake "scan" button that unlocks for one
minute, and a "go home" button. Back also goes home.

**Results**

| Test | Result |
|---|---|
| Opening TikTok shows the lock screen | Works |
| Back / "go home" never lead into TikTok | Works |
| Unlock, then relock while staying inside TikTok | Works |
| Still blocking after a restart, without opening the app | Works (the service reconnects on its own) |
| Still blocking after hours idle (Samsung battery optimization) | Pending, overnight test |

**Delay.** From the moment Android reports TikTok in front to the lock screen
being visible: 131 ms at best, usually around 800 ms to 1 s. On a cold start,
TikTok sent two window events and the lock screen took about 1.8 s from the
first one. TikTok is visible during that time.

**Takeaways**

- Blocking works on the A15. It already feels more reliable than my MacroDroid setup.
- The delay is mostly the time it takes to start a new activity. Drawing the lock screen as an overlay from the service itself (accessibility services are allowed to) could make it near-instant. Worth testing before the architecture phase.
- TikTok keeps running under the lock screen. Usually the lock screen wins before any sound, but once its audio played for a moment, even after the lock screen was up. The real app should silence it, for example by taking audio focus when the lock screen shows.
- The service sees every window change, including the keyboard and the launcher. "Which app is in front" needs a bit of care in the real app.

**Decision:** go. AccessibilityService is the blocking mechanism.

## Spike B: can a tag open the app and say which tag it was?

*2026-10-03, Galaxy A15, Android 15, NTAG215 stickers*

**Setup.** The app writes two NDEF records on a blank tag: a random ID under
our own MIME type (`application/vnd.npardon.declic`), and an Android
Application Record so Android opens this app specifically. An invisible
activity handles the scan, reads the ID, unlocks for a minute, shows a short
message and closes.

**Results**

| Test | Result |
|---|---|
| Write a new tag from the app | Works |
| Scan with the app closed | Unlocks right away, no prompt from Android, the screen I was on stays |
| Scan while the lock screen is up | Lock screen closes, the blocked app is usable |
| Scan with the screen off or the phone locked | Nothing happens. Android only reads NFC when the phone is unlocked. |

**Takeaways**

- The scan-to-unlock flow is as smooth as the requirements ask: no screen to go through.
- The phone has to be unlocked to scan. That fits how the app is used (you pick up the phone, see the lock, go scan), but onboarding should say it.
- A tag is identified by the ID we write, not by its hardware ID, so a tag can be rewritten or replaced cleanly. Copying a tag copies the ID too. That's acceptable for v1.

**Decision:** go. Tags carry our own NDEF record with an app record.

## Spike C: can the app list installed apps without a restricted permission?

*2026-10-03, Galaxy A15, Android 15*

**Setup.** Instead of `QUERY_ALL_PACKAGES`, which Google Play restricts, the
manifest declares a `<queries>` block for apps that have a home-screen icon
(`ACTION_MAIN` + `CATEGORY_LAUNCHER`). The screen lists them with icon, name
and package name.

**Results.** Every app I expected was there, including TikTok, Opera, messaging
apps and Samsung's own apps. The list appeared without a noticeable wait.

**Takeaway.** Apps without a home-screen icon don't show up, and that's fine:
those aren't apps anyone opens to scroll.

**Decision:** go. The app picker uses a launcher-intent query.
