# makefun-tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/enisaishere-hue/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88 chess engine in 4 KB of Python. It plays the make.fun tiny-chess-01 gauntlet through the trial environment: alpha-beta search with quiescence, a transposition table, null-move pruning, late-move reductions, tapered piece-square evaluation, and a fixed 30,000-node budget per move. No model calls, no clock, no randomness — every move is deterministic.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 TINYCHESS_NODES=30000 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=m5sysagx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
