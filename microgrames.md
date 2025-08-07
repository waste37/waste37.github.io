---
title: Microgames
---

## What is MicroGames?
Microgames is a collection of tiny and self-contained minigames, powered by **C** and **SDL2**,
that aims to be a code representation of my personal interpretation of the
**KISS principle** (Keep It Simple, Stupid).
The project focuses on building playable and decently polished experiences using
minimal code, minimal memory, and maximum simplicity — without compromising the fun.

Each game is a small sandbox where code structure, performance, and usability are balanced with the least number of moving parts.
Every line of code exists to serve a purpose.

If you want to see the code, here is the [repository](https://github.com/waste37/microgames)
The current games are:

* [**flappy**](/microgames/flappy.md): A flappy bird clone, with handdrawn textures and a savefiles!
* [**tetris**](/microgames/tetris.md): A tetris clone, with a data oriented twist


---

## The Microgames Coding Standard

To keep things disciplined and uniform, I’ve adopted a strict set of coding rules and conventions.
In the following sections I will try my best to detail the guidelines.

### Design Philosophy
The basic idea is that of making games that are:

* **Simple**: The games must be made of a bunch of source files, compiled in a single translation unit, where the code does and is the bare minimum to solve the problem at hand: _making said game_.
* **Light**: The assets, the code, the memory requirements. Everything should be as small as possible; The rationale being that _having beefy machines doesnt't imply wasting resources_.
* **Playable**: Regardless of simplicity, the games must feel good.

### Naming and Style

- All names are in `snake_case`, including types, variables, and functions.
- No namespacing or Hungarian notation. In such small codebases, clashes are practically impossible and the added verbosity is not worth the noise.
- Preprocesor macros are written in `ALL_CAPS_SNAKE_CASE`.

### Types
To keep things concise and readable, I use abbreviated type definitions throughout the codebase:
    ```c
    typedef int8_t i8;
    typedef int16_t i16;
    typedef int32_t i32;
    typedef int64_t i64;
    typedef uint8_t u8;
    typedef char16_t c16;
    typedef uint16_t u16;
    typedef uint32_t u32;
    typedef uint64_t u64;
    typedef float f32;
    typedef double f64;
    typedef char byte;
    typedef ptrdiff_t isize;
    typedef uintptr_t uptr;
    typedef intptr_t  iptr;
    typedef size_t usize;
    typedef int32_t b32;
    ```
When expressing sizes the chosen type should always be signed, for many reasons, the main one being the weird behaviours of unsigned arithmetic.

### Const correctness
I never use `const`. It's semantics in C are not obvious, and I can't see any advantage in using the qualifier in such simple coding projects.

### Static everywhere
Every function, and every global symbol is declared `static`.
Since all the minigames are made of a single translation unit this is unnecessary, but I like doing it
as a way of highlighting the fact that the scope of symbols is _contained_ in the translation unit; nothing escapes the sandbox!

### Memory Management
Or lack of. I try to always avoid the heap (in my code, off course SDL does allocate stuff, but I don't have any control over that).
The strategy to memory allocation follows the following algorithm:
1. If data can be stored in static memory, it will. If stuff can be pre-baked it should be!
2. If data is enouch small or volatile, put it on the stack.
3. If you **really** need the heap:
    * No mallocs, no frees means no leaks and no OOM at runtime.
    * Allocate all the memory you need at program startup in a big chunk, if the chosen budget is too small one can increase it!
    * The chunk of memory is then consumed linearly, with an arena allocator.

This approach has the advantages of not thinking at memory management, making leaks impossible, and reducing significantly the number of failure points in the program.

### Data Layout First
Reasoning data layout first means thinking about access patterns, alignment, padding.
It starts in the design of structs, or the ordering of their data members,
but it influences even deeper sides of the architecture of the games.
This way of operation makes the logic simpler, avoids indirect memory access, and helps performance by reducing cache misses.

There is a strong preference for:

* Flat arrays over trees or linked lists.
* Dense structs instead of scattered data.
* Precomputed layout offsets for game entities and tiles.

---

## Final Thoughts

These games are not just coding exercises, but a personal research of what happens when you embrace limitations:

- Can you build something fun with under 500 lines of code?
- What does game dev look like when you don't use OOP, event buses, ECS systems, or huge engines?

Turns out that it looks pretty good.
If you're learning C or SDL, this project may be a useful guide or starting point.

---

For feedback or collaboration:
**Tiuna Pierangelo Angelini**
<tiuna.angelini@gmail.com>
