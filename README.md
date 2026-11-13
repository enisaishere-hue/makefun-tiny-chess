# makefun-tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88 chess engine in 4 KB of Python. It plays the make.fun tiny-chess-01 gauntlet through the trial environment: alpha-beta search with quiescence, a transposition table, null-move pruning, late-move reductions, tapered piece-square evaluation, threefold-repetition avoidance, a bishop-pair bonus, and a fixed 50,000-node budget per move. No model calls, no clock, no randomness — every move is deterministic.

Move ordering is the difference between a strong engine and a weak one at a fixed node budget. This engine orders moves by transposition-table move, promotions, captures (most-valuable-victim minus least-valuable-attacker), then a single killer move per ply, then the remaining quiet moves in generation order. The packed entry keeps the killer table and the stable sort.

`main.py` is the engine compressed with LZMA (preset 9, format alone) and base85, unpacked by a one-line loader. The unpacked source is 7,453 bytes; the packed file is 4,081 bytes of UTF-8, inside the 4,096-byte limit.

## Local grade

Trial 0, packed `main.py` (4,081 bytes), 50,000 nodes per move, run 2026-11-13 with the kit's local trial runner:

- **Elo 1362** — 7 wins, 1 draw, 8 losses over 16 games, 820 moves, max think 3,934 ms, average 2,082 ms, no move near the 10-second limit.
- Wins: depth-2 (white and black), depth-3 (white), depth-4 (white and black), nodes-100k (white and black).
- Draw: nodes-250k (black).
- Losses: depth-3 (black), nodes-250k (white), nodes-500k, nodes-1M, nodes-2M (both colours).
- The 1362 Elo sits above the Sunfish 4 KB baseline mean of 1360 and above the 1154 practice floor.

An earlier unpacked build graded 1396 at 30,000 nodes, but its packed form is 4,956 bytes and cannot meet the 4,096-byte UTF-8 limit, so it is not submittable. This entry is a golfed rebuild of the same search: repetition avoidance and the bishop-pair bonus restored, node budget raised to 50,000 per move. Trials 1 and 2 (different openings) are run to confirm the grade before submission.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 TINYCHESS_NODES=50000 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=m5sysagx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
