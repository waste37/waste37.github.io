---
title: Migrogames
---

Microgames is a collection of minigames, all made with C and SDL2, that aim to be as close as possible to my personal interpretation of the KISS principles.

The basic idea is that of making games that are:
* Simple: The games must be made of a bunch of source files, compiled in a single translation unit, where the code does and is the bare minimum to solve the problem at hand: _making said game_.
* Light: The sprite, the code, the memory requirements. Everything should be as small as possible, while being **playable**.

The standards i followed are strict, and here i will try to detail them. After pointing down what these ethereal rules are, I will try to walk through the development process of each minigame.

# The Microgames Coding Standard
## Stylistic Conventions
### Names
Variable names, function names and also type names are in snake case.
I always prefer simple names; don't use namespace prefixes, since the code shouldn't be long, and name clashes are easily avoidable;
### Types
For the standard types there are a couple of rules:
* Short types: I use throughout the projects some abbreviated names for types. The complete list follows:
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
* Signed sizes: the size types should always be signed, for many reasons, the main one being the weird behaviours of unsigned arithmetic.

## Memory Management


## Data Layout First


