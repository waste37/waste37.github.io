---
title: `tetris`
---

A minimal yet fully functional Tetris clone, with a data oriented twist!

### Features

- Built using only SDL2 (no image/font dependencies).
- Full implementation of all 7 tetromino types with rotation states.
- Color-coded blocks with custom grid rendering.
- Collision detection, row clearing, and gravity.
- Manual left/right movement, fast drop, and rotation.
- No wall kicks (intentionally not implemented).
- Restart via spacebar.

### Technical Breakdown

- The game operates on a `NUMCOLS x NUMROWS` integer grid, holding color values (`0xRRGGBB`).
- Each tetromino is defined using a 4x4 grid offset table for all 4 rotation states.
- The core logic is handled via the `update_game()` function.

### Example Snippet: Tetromino Rotation

```c
static tetromino trotate(tetromino t, b32 clockwise) {
    t.state = (t.state + 1 + (!clockwise * 2)) % 4;
    t.off = offsets_table[t.type][t.state];
    return t;
}
```

### Grid Management

Grid cells are precomputed once using `init_cell_rects()`. There is no dynamic allocation or pointer juggling. All pieces are rendered directly with `SDL_RenderFillRect()`.

---

