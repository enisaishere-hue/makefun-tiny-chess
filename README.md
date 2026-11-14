# makefun-tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88 chess engine in 4 KB of Python. It plays the make.fun tiny-chess-01 gauntlet through the trial environment: alpha-beta search with quiescence, a transposition table, null-move pruning, late-move reductions, tapered piece-square evaluation, threefold-repetition avoidance, a bishop-pair bonus, and a fixed 60,000-node budget per move. No model calls, no clock, no randomness — every move is deterministic.

Move ordering is the difference between a strong engine and a weak one at a fixed node budget. This engine orders moves by transposition-table move, promotions, captures (most-valuable-victim minus least-valuable-attacker), then a single killer move per ply, then quiet moves scored by a history heuristic that rewards moves that caused beta cutoffs. The packed entry keeps the killer table, the history table, and the stable sort.

`main.py` is the engine compressed with LZMA (preset 9, format alone) and base85, unpacked by a one-line loader: 7,472 bytes unpacked, exactly 4,096 bytes of UTF-8 packed, at the limit.

## Local grade

Three trials of the packed `main.py` at 60,000 nodes per move, run 2026-11-13 with the kit's local trial runner: 16 games each against the same opponent set at a different opening.

| Trial | Opening | Elo | W | D | L |
|---|---|---|---|---|---|
| 0 | Semi-Slav | 1530 | 9 | 2 | 5 |
| 1 | Sicilian Classical | 1396 | 7 | 2 | 7 |
| 2 | King's Indian Attack | 1253 | 5 | 2 | 9 |

- **Mean Elo 1393** across the three trials, above the Sunfish 4 KB baseline mean of 1360 and above the 1154 practice floor.
- Trial 0 beats the baseline by 170 Elo; trial 2 trails it by 107. That spread is the honest variance of a 16-game sample; the mean is the grade that matters.
- This build is golf4: golf3 plus history-heuristic ordering and the node budget raised from 50,000 to 60,000 per move. An earlier unpacked build graded 1396 at 30,000 nodes, but its packed form is 4,956 bytes and cannot meet the 4,096-byte limit, so it is not submittable.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 TINYCHESS_NODES=60000 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=m5sysagx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
