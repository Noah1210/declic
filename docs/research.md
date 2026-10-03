# Research notes

Findings that shape the design. Each entry says where it came from and when it
was checked, so stale ones can be re-verified. Decisions don't live here, they
go in ADRs, which can link back to these notes.

## Platform

### App blocking on Android uses the AccessibilityService
*Checked 2026-10-03*

- Existing NFC blockers state it is "the only reliable way to block apps on Android": the service detects which app is in the foreground and sends the user back to the home screen.
- Google Play allows it for non-accessibility apps, with conditions: an accessibility declaration in the Play Console, a prominent in-app disclosure, explicit user consent, and the use documented in the store listing. The `isAccessibilityTool` flag is reserved for apps that serve people with disabilities, so it doesn't apply here.
- The policy also says to use narrower APIs when they can do the job.
- Implication: build the disclosure and consent screen from the start, even though v1 is sideloaded.
- Sources: [Play Console policy](https://support.google.com/googleplay/android-developer/answer/16558241), [Lock on Play](https://play.google.com/store/apps/details?id=com.nathanb.lock)

### NFC tags can launch the app directly
*Checked 2026-10-03*

- Android's tag dispatch system starts the app that declares a matching `ACTION_NDEF_DISCOVERED` intent filter. Adding an Android Application Record to the tag ties it to this app.
- Recent Android versions have a per-app allowlist: *Settings > Apps > Special app access > Launch via NFC*. Onboarding has to cover it.
- While the app is open, foreground dispatch or reader mode can handle scans instead.
- Source: [Android NFC basics](https://developer.android.com/develop/connectivity/nfc/nfc)

### Cheap tags can be cloned
- A plain NTAG213 sticker can be copied. NTAG 424 DNA tags give signed, rolling-counter scans. This is a possible later feature, not a v1 one.

### Device
- Development phone: Samsung Galaxy A15 (Android 14).
- Samsung's battery optimization ("sleeping apps") is known to kill background services. That makes it the top risk (Spike A).
- My current setup (MacroDroid, one NTAG215 tag next to the bathroom mirror, TikTok and Opera blocked, apps relock 6h after the last scan) has blocked apps reliably on this phone. So blocking is doable on the A15, though it still needs to be proven in my own code.
- The app should target a wide range of Android versions. Choose `minSdk` in Phase 4 using Android Studio's distribution data.

## Architecture

### Google's recommended Android architecture
*Checked 2026-10-03*

- A UI layer and a data layer, plus an optional domain layer when it simplifies things.
- Jetpack Compose for the UI. A ViewModel exposes state as `StateFlow`, and the UI collects it with `collectAsStateWithLifecycle()`.
- Repositories are the only entry point to data sources. The UI never touches the database directly.
- Offline-first is a documented pattern.
- Source: [Guide to app architecture](https://developer.android.com/topic/architecture), [Recommendations](https://developer.android.com/topic/architecture/recommendations)

### Keeping iOS possible without paying for it now
*Checked 2026-10-03*

- Kotlin Multiplatform has been stable since late 2023. Room, ViewModel, DataStore and Navigation now work in shared code. Compose Multiplatform for iOS has been stable since May 2025.
- Common advice: share the business logic, keep the UI native.
- Implication: don't adopt KMP now. Keep the `domain` package as pure Kotlin with no Android imports so it can move to shared code later.

### Keeping a backend possible
- The repository pattern already isolates data sources. A remote data source can be added behind the same repository later without touching the UI or domain.
- Implication: v1 is local-only, and no decision should assume the data never leaves the device. Example: use IDs that would survive a sync, like UUIDs rather than auto-increment.

## Method

### Risk-driven, "just enough" architecture
- Identify and prioritize risks, apply the techniques that reduce them, then check whether the risk went down. No heavy design where risks are small. Source: George Fairbanks, *Just Enough Software Architecture*.

### Walking skeleton
- A tiny end-to-end implementation linking all the main components, built with production habits and kept, unlike a spike. It comes before the MVP.

### Documentation set
- ADRs: context, options, decision, consequences. One page each.
- C4 model: context and container levels answer most questions. Go deeper only when complexity demands it.

## Market

*Checked 2026-10-03*

- **Lock – NFC App Blocker** (Android 14+): tag toggles blocking, fully offline, no account.
- **TaskGate**: a small task before a blocked app opens (breathing, affirmation).
- **Brick, Opal, Unplugged**: blocking toggles, mostly iOS.
- None of these ties the unlock to a habit with a physical tag as proof. That gap is this app's angle.

## Open questions

- **License.** Depends on the goal. If it's a portfolio and possibly a product, a permissive license (MIT) lets anyone ship a copy. Publishing with no license keeps all rights reserved while the code stays readable. Decide in Phase 0.
- **Name.** Decided 2026-10-03: **Déclic** ("Declic" in the repo, package and store). Shortlist was Keystone and Déclic.
  - *Checked 2026-10-03:* "Keystone – Habits & AI Planner" is on Google Play, and "Keystone – Social Habit Tracker" exists too. Both are habit apps, so the name collides directly.
  - "Declic" exists as a social meetup app on both stores. That's a different category. Before any commercial launch, check French trademarks (INPI) and EU trademarks (EUIPO).
- **A scan is not always a completed habit.** With the 6h relock, I sometimes scan midday just to unlock, without doing the routine. If every scan counted as "skincare done", the stats would lie. Unlocking and completing a habit need to be separate things. To settle in Phase 1/3.
- **Habit types.** The app covers many habits with different shapes: daily (skincare), weekly frequency (gym 3×/week), measurable (10 km run), time-bound (bedtime). NFC proof fits place-bound habits. Other habits need other kinds of proof, to be explored in Phase 1.
