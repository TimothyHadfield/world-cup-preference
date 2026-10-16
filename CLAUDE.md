# Who Should I Cheer For? (world-cup-preference)

Tim's single-page 2026 World Cup tool. A fan ranks up to five favorite teams; the page simulates the
whole tournament thousands of times (Monte Carlo from Elo ratings) and says which result in every match
gives those favorites the best shot at the trophy. Used on iPhone and laptop. No accounts, no backend,
no data saved anywhere: everything runs in the browser.

- **Live:** https://timothyhadfield.github.io/world-cup-preference/
- **Repo:** TimothyHadfield/world-cup-preference (public)
- **Deploys:** GitHub Pages from `main`, root folder. A push to `main` is live in about a minute.

## File map
- `index.html`: the whole app (CSS, HTML and plain JavaScript in one file, no build step, no libraries).
  - Data: `GROUPS_RAW` (real 2026 draw, 12 groups x 4, `[name, flag, elo]`), `HOSTS`, `R32` / `LATER`
    (official 2026 knockout slots, matches 73-103; third-place slots list their eligible groups).
  - Model: `groupProbs` (win/draw/loss from Elo, draw share up to 30%), `koWinProb`, `HOME_BONUS = 75`
    for the three hosts unless both teams are hosts.
  - Engine: `simulateOnce`, `runMonteCarlo` (chunks of 400 with `setTimeout` so the progress bar moves),
    `assignThirds` (matching of the 8 best thirds to their slots), `gatherFinish` (extra 1,500 sims for
    projected group finishes and the bracket).
  - Advice: `recGroupMatch`, `recPair`, `buildRec` (best vs worst outcome swing, minus 1.5 standard errors
    of sim noise, then `confidence` 0-100), `overallSide` (blend of favorites weighted 5,4,3,2,1).
  - UI: sections 1-5 (pick favorites, trophy odds, match lookup, group stage, projected bracket).
- `README.md`: GitHub showcase page. `docs/screenshots/*.png`: images used only by the README.
- `progress.md`: handoff notes for the next Claude.

## Run locally
`python -m http.server 8121` in the project folder (background option), then open http://localhost:8121/.
Any static server works; the page also works opened straight from disk.

## Test
No test suite (one HTML file). Verify with phone-view, for example:
`node ~/.claude/tools/phone-view.mjs http://localhost:8121/ --do "click:#runBtn" --do "wait:#results:not(.hidden)" --eval "<js>"`
Globals such as `RESULT`, `TEAMS`, `FAVS` are reachable from `--eval` after a run. The engine can also be
loaded in Node by eval-ing the `<script>` body up to `/* ---- boot ---- */` (no DOM needed for the sim).

## Traps
- Flags are emoji. Windows shows them as two letters (and Scotland/England as a black flag); iPhone shows
  real flags. Not a bug.
- Elo ratings are a frozen June 2026 snapshot hard-coded in `GROUPS_RAW`; nothing updates them.
- Simulation results are random each run; compare numbers with tolerance, not exact values.
- Group-card "advance %" is the share of the full run that reached the Round of 32 (`reachedKO`), the
  same number as "Advance" in section 2. Before 2026-10-16 it wrongly counted only 1st/2nd place.
- The projected bracket is deterministic (higher win chance always advances) and picks the 8 thirds by
  Elo of each group's most likely 3rd-place team, so it is a picture, not a simulation result.
- `.gitignore` keeps `.claude/` out of the public repo.

## Standing instructions
No project-specific instructions from Tim recorded yet; the global rules in `~/.claude/CLAUDE.md` apply.
Looks, wording, model numbers (draw share, home bonus, Elo values) are Tim's: don't change them uninvited.
