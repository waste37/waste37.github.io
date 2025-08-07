---
title: `flappy`
---

This game is a reimagination of the classic Flappy Bird, built with static memory, minimal dependencies, and a clean render loop.

### Features

- Uses SDL2, SDL_image, and SDL_ttf for rendering.
- Background parallax scrolling.
- Bird animation with physics-based jump and gravity.
- Procedurally spawned pipe obstacles.
- Score tracking with local high score saving to file.
- Three states: Menu, Playing, and Game Over.
- All assets are preloaded once at startup.

### Design Notes

- The bird has simple physics: gravity pulls down; spacebar triggers a jump.
- Pipes are reused in a ring buffer, controlled via a `spawner` structure.
- Collision is handled with `AABBcollide` using slightly trimmed bird hitboxes.
- The background scrolls continuously, cycling two textures.
- Assets are organized in a unified sprite array.

### Example Snippet: Pipe Spawner

```c
if (SCREEN_WIDTH - pipes[spawner.current].top.x >= spawner.distance) {
    spawner.current = (spawner.current + 1) % 5;
    spawner.visible[spawner.current] = 1;
    f32 pos_x = SCREEN_WIDTH + sprites[SPRITE_PIPE].width;
    f32 pos_y = fmin(SCREEN_HEIGHT - 200, fmax(200, rand() % SCREEN_HEIGHT));
    set_pipe(spawner.current, pos_x, pos_y);
}
```

