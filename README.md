# Benchmarks of NDSS'25 Paper "Translating C To Rust: Lessons from a User Study"

This repository contains 8 benchmarks used in the user study in the NDSS'25 paper "Translating C To Rust: Lessons from a User Study" ([paper link](https://www.ndss-symposium.org/wp-content/uploads/2025-1407-paper.pdf)). Each benchmark includes a C program, a Makefile, and the test script that the C program passes. The C program is self-contained and compilable, requiring only the C standard library. These programs are representative of the C programs that implement lower-level functionality and self-manage memory where memory safety errors may arise.

## Benchmark Description

The benchmarks consist of 6 binaries (subdirs whose name starts with `bsd-`) from the BSDCoreUtils collection of system utilities ([Github repo](https://github.com/DiegoMagdaleno/BSDCoreUtils)) and 2 libraries shoco ([Github repo](https://github.com/Ed-von-Schleck/shoco)) and urlparser ([Github repo](https://github.com/jwerle/url.h)). 

- Four programs—`csplit`, `fmt`, `join`, and `test`—perform file processing. 
- The `expr` and `printf` are pure computation utilities for strings and numbers. 
- The `shoco` library is for data compression.
- The `urlparser` library parses URL strings.

We preprocessed the collected code to be independently compilable and pass tests we provide (see the file [preprocess.md](preprocess.md) for details). After the preprocessing, the LOC of these programs ranges from 322 to 536. 

### Testing with Coverage Reported

Each benchmark comes with tests that have different line coverage. The given Makefile compiles the C code with code coverage analysis enabled. Each test script generates the code coverage report after running tests.

```bash
# Taking bsd-csplit as an example
# compile the C program
cd bsd-csplit
make

# run tests with code coverage report
./tests.sh
```

The code coverage analysis of `urlparser` may fail when compiled with certain hardened libc. As additional information, existing tests of `urlparser` can cover 97.73% of 309 lines.

Note that these benchmarks are the versions given to participants in the user study, not all initial test scripts achieve high line coverage, which ranges from 43.21% to 97.73% across benchmarks. Participants wrote their own tests to reach at least 85% coverage. Testing-related experiments in the NDSS'25 paper also use participants' tests, not only the initial tests in the benchmarks. Due to the IRB rules, we cannot directly release any code written by the students of the class (i.e., our participants), including their unit tests.

## Citation

If you use these benchmarks in your research, please cite our paper:

```bibtex
@article{li2024translating,
  title={Translating c to rust: Lessons from a user study},
  author={Li, Ruishi and Wang, Bo and Li, Tianyu and Saxena, Prateek and Kundu, Ashish},
  journal={arXiv preprint arXiv:2411.14174},
  year={2024}
}
```