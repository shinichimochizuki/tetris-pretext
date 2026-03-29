# Tetris-Pretext — a pretext demo

Tetris-style blocks fall through a page of text. As each piece drops, the words
step aside in real time. When a row fills and clears, the text flows back in.

**[Live demo](https://shinichimochizuki.github.io/tetris-pretext/)** <!-- update URL -->

---

## What's happening

Every frame, the layout is computed from scratch using
[pretext](https://github.com/chenglou/pretext) — a browser-accurate text
measurement library by [@chenglou](https://github.com/chenglou).

The key call is `layoutNextLine(prepared, cursor, width)`. For each row of the
page, the code checks which grid cells are occupied by blocks, subtracts those
pixel spans from the available line width, then passes the remaining width to
`layoutNextLine`. The result is text that wraps live around whatever is sitting
on the board — falling pieces, stacked blocks, and all.

When a full row clears, nothing special has to happen for the text. The
exclusion zones disappear, `layoutNextLine` gets the full column width back,
and the displaced words settle back into the freed space.

## Controls

| Key | Action |
|-----|--------|
| `←` `→` | Move piece |
| `↑` | Rotate |
| `↓` | Soft drop |
| `Space` | Hard drop |

## Built with

- [pretext](https://github.com/chenglou/pretext) — text layout engine
- Canvas 2D API — rendering
- Bun — local dev server

## Acknowledgement

All text measurement and line-breaking is powered by
[pretext](https://github.com/chenglou/pretext), created by
[@chenglou](https://github.com/chenglou). This demo would not be possible
without the `layoutNextLine` API it exposes for variable-width, per-line
userland layout.
