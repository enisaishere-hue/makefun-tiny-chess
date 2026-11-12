# makefun-tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88 chess engine in 4 KB of Python. It plays the make.fun tiny-chess-01 gauntlet through the trial environment: alpha-beta search with quiescence, a transposition table, null-move pruning, late-move reductions, tapered piece-square evaluation, and a fixed 30,000-node budget per move. No model calls, no clock, no randomness — every move is deterministic.

Move ordering is the difference between a strong engine and a weak one at a fixed node budget. This engine orders moves by transposition-table move, promotions, captures (most-valuable-victim minus least-valuable-attacker), then a single killer move per ply, then the remaining quiet moves in generation order. Dropping the killer moves and the stable sort cost 182 Elo in local grading (1396 down to 1214); restoring them recovered the full strength. The packed entry keeps the killer table and the stable sort.

## Local grade

Trial 0, packed `main.py` (4092 bytes), 30,000 nodes per move, run 2026-11-12 with the kit's local trial runner:

- **Elo 1396** — 8 wins, 0 draws, 8 losses over 16 games, 697 moves, max think 2,154 ms, median 1,265 ms, no move near the 10-second limit.
- Wins: depth-2 (white and black), depth-3 (white and black), depth-4 (white), nodes-100k (white), nodes-250k (white and black).
- Losses: depth-4 (black), nodes-100k (black), nodes-500k, nodes-1M, nodes-2M (both colours).
- The 1396 Elo sits above the Sunfish 4 KB baseline mean of 1360 and above the 1154 practice floor.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 TINYCHESS_NODES=30000 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=m5sysagx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
