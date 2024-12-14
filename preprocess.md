# Preparation of Benchmarks

Here are the links (with the corresponding commit hash) to each benchmark's original source code:

- Binaries:
    - [csplit](https://github.com/DiegoMagdaleno/BSDCoreUtils/tree/d2b28e08bd02da5076a876608d6431638f929849/src/csplit)
    - [expr](https://github.com/DiegoMagdaleno/BSDCoreUtils/tree/d2b28e08bd02da5076a876608d6431638f929849/src/expr)
    - [fmt](https://github.com/DiegoMagdaleno/BSDCoreUtils/tree/d2b28e08bd02da5076a876608d6431638f929849/src/fmt)
    - [join](https://github.com/DiegoMagdaleno/BSDCoreUtils/tree/d2b28e08bd02da5076a876608d6431638f929849/src/join)
    - [printf](https://github.com/DiegoMagdaleno/BSDCoreUtils/tree/d2b28e08bd02da5076a876608d6431638f929849/src/printf)
    - [test](https://github.com/DiegoMagdaleno/BSDCoreUtils/tree/d2b28e08bd02da5076a876608d6431638f929849/src/test)
- Libraries:
    - [shoco](https://github.com/Ed-von-Schleck/shoco/tree/4dee0fc850cdec2bdb911093fe0a6a56e3623b71)
    - [urlparser](https://github.com/jwerle/url.h/tree/a65623ad107be19ca4efb5a36379f3440eb48091)

We manually preprocessed the collected code to get a self-contained and compilable C file and check it against tests we provide. The specified platform in the user study is Linux so we check the compilation and test-passing on Ubuntu 22.04. 

Here is the summary of our preprocessing:
- Consolidating dependencies into a single file. For example, copying the header content into the source file for `shoco`; copying the defintion of the `strtonum` function from `strtonum.c` to `test.c` for `test`.
- Removing or adding macros for compilation. For example, commenting out `#ifndef u_long` and 2 following lines in `join.c` since it's not used; adding `#define _GNU_SOURCE` for `fmt`.
- Fix possible bugs. For example, removing the wrong check on the return value of `fputs` in `csplit.c`.
- For libraries (`shoco` and `urlparser`), merge their library code and their C test code into a single file.

## Details

### shoco

1. Remove the macro lines including `emmintrin.h`. Remove `#define _SHOCO_INTERNAL` macro.
2. Remove the version of `check_indices` if `HAVE_SSE2` macro is defined. Remove this macro condition.

### urlparser

1. Merge the `url.h` and `test.c` into `urlparser_lib_test.c`.

### csplit

1. Remove checks on the return value of `fputs`.

### expr

1. Copy the definition of `strtonum` from `strtonum.c` to `expr.c`. 
2. Remove the include of `compat.h`.

### fmt

1. Include the macro definition of `_GNU_SOURCE` in `fmt.c`.

### join

1. Comment out the macro condition to include `compat.h`.

### printf

None

### test

1. Copy the definition of `strtonum` from `strtonum.c` and the definition of `strlcpy` from `strlcpy.c` to `test.c`.
2. Remove the include of `compat.h`.
