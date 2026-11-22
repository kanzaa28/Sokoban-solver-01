# Sokoban Solver — make.fun sokoban-solver-01-run-20261121

Push-space BFS solver for Sokoban levels, solved room by room.

## How it works

Scoring counts pushes only (1000 pts at the push-optimal count P*, else
500*P*/pushes), so the search runs over pushes, not steps: a state is the
boxes' squares plus the player's reachable region, one expansion = one push.
Two prunings keep it small: dead squares (a box that can never be pushed to
any goal) and frozen 2x2 wall/box blocks. Levels are a hallway plus rooms of
3-4 boxes off it through one door each; a box pushed through a door into the
hallway can never come back, so each room is solved on its own (other rooms'
boxes treated as walls) and the rooms' optima add up to the level's P*.

## Measured results (official scorer, program/scorer/score.ts)

- Practice set: **1,000,000 / 1,000,000** — all 5 instances at P*
  (13, 16, 29, 47, 60 pushes), ~1.0 s total (budget 60 s).
- Two freshly generated unseen sets (kit generator, random drand-style
  seeds): **1,000,000** on both (P* 12/16/29/47/61 and 15/14/35/44/62).
- House baseline plain-astar 1.0.0 on the same practice set: 200,000
  (only i001 solved).
- Deterministic: two runs write byte-identical solution.txt files.

## Files

- `main.ts` — the entry (Node 22, no dependencies, no installs).
- `LICENSE` — MIT.

## What is missing for a real submission

Practice-only: `handed_over_places` is "none", so an entry built in this
harness is ranked but cannot take a paid place. A real submission needs the
user's public GitHub repo (repo_url + commit_sha), the transcript bundle,
and the user's explicit go-ahead. Prize $100 (10 places x $10), closes
23 Nov 2026 11:00 WITA.
