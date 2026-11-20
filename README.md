# Tiny Chess — a 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/tyler-2-makefun/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/tyler-2-makefun/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A from-scratch chess engine in a single packed `main.py` (**4,087 bytes**), built for the make.fun bounty **"Build the strongest chess engine in 4 KB of Python"** (USDC 500, deadline Wed 25 Nov 2026 00:00 WIB).

[View the bounty on make.fun](https://make.fun/bounty/tiny-chess-01)

## How it plays

- **Board:** 0x88, own move generator (perft-verified: startpos, Kiwipete, position 3, all depths).
- **Search:** negamax alpha-beta with iterative deepening on a **fixed 120,000-node budget per move** (deterministic — no clock, no unseeded randomness), transposition table (64-bit Zobrist), null-move pruning (R=2/3), late-move reductions, and quiescence (captures, promotions, and check evasions).
- **Evaluation:** material (P100 N320 B330 R500 Q900) folded into formula-generated piece-square tables, plus a bishop-pair bonus. No king taper — the king uses a single middlegame table.
- **Protocol:** talks to the make.fun environment over HTTP (`POST /game`, `/move`, `/resign`), replays the game from the start position, and sends the chosen move in UCI.

`main.py` is the packed entrypoint: an LZMA stream of the readable source, written by the kit's `makefun compress` command (`dev/src.py` → `main.py`, 4,087 bytes). The readable source is `dev/src.py` (14,027 bytes, written by the agent in the build session).

## Running it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8123 python3 -P -s main.py
```

Python 3.13, standard library only. No other file is read, imported, or executed.

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
