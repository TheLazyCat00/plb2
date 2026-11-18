# Zane

The four plb2 tasks in [Zane](https://github.com/zane-lang/zane), ported from
the C versions with the same algorithms and no library help beyond `core`'s
lists and `math`'s bit operations. The manifest pins compiler **v0.40** and
`std` **v0.14**, built from source.

## Build and run

Install the [Zane CLI](https://github.com/zane-lang/zane) and a compiler
(`zane toolchain install v0.40`), then:

```sh
make            # builds ./nqueen ./matmul ./sudoku ./bedcov, optimized
./nqueen        # 2279184
./matmul        # -143.5001666666568
./sudoku > /dev/null
./bedcov        # 8195494005
```

Each program takes the C version's optional size argument (`./nqueen 8`).

## Notes on the port

- Zane lists count from 1, so C's `x[i]` is `x[i + 1]`; every position and
  count keeps its C value, counted from 0. Sudoku's and bedcov's
  two-dimensional arrays are flattened into one list.
- Zane has no `while`. A loop that runs until a condition holds is a
  *worker* (`work`), which is how nqueen's backtracking, sudoku's solver
  loop and bedcov's tree traversal run. Inner loops that exit early are
  counted `to` loops in a helper that `return`s.
- Only a method's `this` may be written, so the state each algorithm mutates
  (sudoku's vectors, bedcov's arrays, buckets and stack) is gathered in one
  struct whose methods do the work.
- C's `uint32_t` arithmetic in bedcov's `splitmix32` is done on `Int` with an
  explicit 32-bit mask.
- `matmul` prints Zane's shortest round-trip form of the double, as the Rust
  and Go versions do, rather than C's `%f`.
- `sudoku`'s output is byte-identical to the C version's.
