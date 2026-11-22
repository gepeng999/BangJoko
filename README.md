# tiny-chess-engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in at most 4,096 bytes of Python, built for the make.fun
tiny-chess-01 bounty: it plays the house gauntlet (eight fixed-strength
engines) through the make.fun env, one game after another.

## How it plays

- 120-square board, fully legal move generation (castling, en passant,
  promotions, check evasion).
- Negamax alpha-beta search with a transposition table, quiescence search
  over captures, promotions and check evasions, null-move pruning, killer
  move ordering and check extensions.
- Deterministic: iterative deepening runs to a fixed node budget, never a
  clock, so a replayed trial plays the same moves.
- Evaluation: material plus piece-square tables.

## Layout

- `main.py` — the whole engine (Python 3.13, standard library only), packed
  from the readable source with the make.fun compressor. It talks to the
  env at `MAKEFUN_ENV_URL`: `POST /game` serves the game in play,
  `POST /move` plays a move, and it exits when every game is over.

## Local practice

Against the kit's practice gauntlet (depth-2, depth-3, depth-4,
nodes-100k, nodes-250k, nodes-500k) the engine scored 3.5/6 — wins against
depth-2 and nodes-250k, draws against depth-3 and depth-4 — for an
estimated Elo around 1,360, above the house baseline.
