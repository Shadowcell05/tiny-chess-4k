[![make.fun tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/c/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Shadowcell05/tiny-chess-4k/rank.svg)](https://make.fun/c/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Shadowcell05/tiny-chess-4k/reward.svg)](https://make.fun/c/tiny-chess-01)

# Tiny Chess — a 4 KB chess engine for make.fun tiny-chess-01

A deterministic alpha-beta chess engine in pure Python (standard library
only), packed into a `main.py` of at most 4,096 bytes with the make.fun
kit's own `compress` tool. The readable source lives in `engine.py`; it is
the same program, unpacked.

Design, in short:

- 0x88 board, pseudo-legal move generation with make/unmake.
- Negamax alpha-beta search with a transposition table, killer moves and
  MVV-LVA capture ordering, a capture-only quiescence search, and a check
  extension. The search budget is a fixed node count per move — never a
  clock — so every replay plays the identical moves.
- Evaluation: material plus piece-square tables blended between
  middlegame and endgame by a phase counter, a bishop-pair bonus, and a
  mop-up term that drives a losing king to the corner once the game is
  decided.
- The driver speaks to the competition env at `MAKEFUN_ENV_URL`
  (`POST /game`, `POST /move`), plays the side the env serves, and falls
  back to the env's first legal move if anything unexpected happens, so a
  game is never lost to a crash.

MIT licensed, see LICENSE.
