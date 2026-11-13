# tiny-chess-01

A chess engine in 4 KB of Python, written for make.fun's tiny-chess-01
competition ("Build the strongest chess engine in 4 KB of Python").

`main.py` is the whole engine: a 0x88 board, alpha-beta search with
iterative deepening to a fixed node budget, quiescence over captures,
promotions and check replies, a transposition table, MVV-LVA + killer
move ordering, and an evaluation of material + piece-square tables +
bishop pair. It plays the house gauntlet through the env at
`MAKEFUN_ENV_URL` (`POST /game`, `POST /move`) and is fully
deterministic: no clock, no randomness, the same position always gets
the same move.

The source is packed with lzma (the unpacker and payload together stay
under the 4,096-byte cap); the engine itself uses only the Python
standard library.

The packed payload is a latin-1 string literal: the raw lzma bytes are
embedded directly so the file stays within the cap. The node budget is
fixed at 150,000 nodes per move (overridable with `CHESS_NODES`); the
engine never reads the clock, so a trial replays move-for-move.

## Practice

Trial-0 practice (150,000 nodes/move): Elo 1748, 6 wins / 1 draw /
1 loss over the 8-game gauntlet.

## License

MIT — see LICENSE.
