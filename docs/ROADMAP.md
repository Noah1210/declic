# Roadmap

How this project goes from idea to an app running on my phone. Each phase ends
with a concrete deliverable. A phase starts only when the previous one is done.

Guiding principle: **just enough architecture**. Design effort goes where the
risk is. Simple beats complex.

## Phase 0: Framing

- [x] Create the GitHub repository and start committing the planning work
- [x] Choose the project name: Déclic
- [x] Choose a license: none for now (all rights reserved, code public and readable)
- [x] Vision: the problem, who it's for, and why it differs from existing apps
- [x] Non-goals for v1: no iOS, no accounts, no social features. Backend is deferred, not ruled out.
- Deliverable: `docs/vision.md`

## Phase 1: Requirements

- [x] User stories for the core loop: create a habit -> link an NFC tag -> choose apps to block -> apps lock -> scan tag -> apps unlock -> daily reset
- [x] Prioritize with MoSCoW and freeze the v1 scope
- [x] Rank quality attributes: blocking reliability > smooth unlock > privacy > battery > maintainability
- [x] Constraints: Windows dev machine, Android first, solo developer, no Mac
- [x] Safety requirement: an emergency unlock always exists
- Deliverable: `docs/requirements.md`

## Phase 2: Risks and spikes

Throwaway code to kill the biggest unknowns before committing to a design.

- [x] Spike A: an AccessibilityService blocks one app on the Galaxy A15 by showing a lock screen over it, and keeps working after a reboot and under Samsung battery optimization. Note how long the blocked app is visible before the lock screen appears.
- [x] Spike B: scanning a tag launches the app and identifies which tag it was
- [x] Spike C: list launchable installed apps for a picker without `QUERY_ALL_PACKAGES`
- [ ] Spike A, battery part: still blocking after a night idle
- [ ] Spike D: draw the lock screen as an overlay from the service to remove the ~1 s delay, and silence the blocked app's audio
- Deliverable: `docs/spikes.md` with findings and a go/no-go

## Phase 3: Domain model

- [ ] Entities: Habit, Tag, BlockedApp, Completion, Schedule
- [ ] State diagram: Locked -> (right tag scanned) -> Unlocked -> (new day) -> Locked, plus the emergency path
- [ ] Glossary: one word per concept, used everywhere in code and docs
- Deliverable: `docs/domain.md`

## Phase 4: Architecture

- [ ] C4 level 1 (context) and level 2 (containers)
- [ ] Package structure: one Gradle module, packages by feature, a pure-Kotlin `domain` package
- [ ] Choose `minSdk` from Android Studio's distribution data
- [ ] ADRs for hard-to-reverse decisions only (expected ~5–8)
- Deliverable: `docs/architecture.md`, `docs/adr/`

## Phase 5: UX/UI design

- [ ] User flows -> low-fidelity wireframes
- [ ] Design system: color, type and spacing tokens, core components
- [ ] High-fidelity Figma mockups of the key screens
- Deliverable: Figma file, `docs/design.md`

## Phase 6: Tooling

- [ ] Android Studio project inside this repo
- [ ] ktlint or detekt
- [ ] GitHub Actions CI: build, test, lint on every push
- [ ] GitHub Projects board with the v1 stories

## Phase 7: Walking skeleton

- [ ] One habit, one tag, one blocked app, end to end on the phone. Real architecture, no polish.

## Phase 8: Vertical slices

- [ ] One user story at a time through UI -> ViewModel -> domain -> data, verified on device
- [ ] Domain rules written test-first

## Phase 9: Hardening

- [ ] Reboot, midnight and time zones, lost tag, permission revoked, phone locked while scanning
- [ ] Battery check, accessibility of the app's own UI

## Phase 10: Dogfooding

- [ ] Signed release build used daily for 2 weeks, with a bug log

## Phase 11: Portfolio packaging

- [ ] Case study: problem, constraints, key decisions (linking ADRs), what went wrong, what I'd change
- [ ] Demo video, polished README, screenshots

## Later

- iOS (evaluate Kotlin Multiplatform for the domain layer)
- Backend, if a feature needs one (sync, accounts, multi-device)
- Google Play release

## Guardrails

- One Gradle module until a real pain appears
- A domain class exists only when it holds an actual rule
- An ADR only for decisions that are hard to undo
- Anything outside the frozen v1 scope goes under "Later", not into the code
