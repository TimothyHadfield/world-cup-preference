# progress.md — Who Should I Cheer For? (world-cup-preference)

## START HERE
Last updated 2026-10-16. Read `CLAUDE.md` (file map, how to run and verify), then this file.

## Goal right now
Finished and live; maintenance only. Tim has asked for nothing new since publishing it (2026-09-27).

## Status
| Area | State |
|---|---|
| Site icon | Added 2026-10-17: `icon.svg` (white soccer ball, green rim, on #0a1410) as tab favicon + `apple-touch-icon.png` 180px for iPhone home screen |
| App (`index.html`) | Live at https://timothyhadfield.github.io/world-cup-preference/ |
| Tests | None (single HTML file); verified with phone-view |
| 2026-10-16 sweep | Fixed group-card advance % (now includes third-place qualifiers), escaped typed text in match lookup, added labels for screen readers, meta description, no favicon 404 |

## Authorized next steps
None.

## Standing instructions
None project-specific yet. Global rules apply.

## Traps
- Emoji flags show as letters on Windows; real flags on iPhone.
- Sim results are random; compare with tolerance.
- No accounts or backend, so no test account is needed.

## Decisions
- 2026-10-16: group-card "advance %" uses the full run's Round of 32 rate (`reachedKO`), matching its own label and section 2.

## NOT verified
- Real iPhone rendering (only Safari's engine via phone-view at 393px).

## Rejected / parked
None yet.
