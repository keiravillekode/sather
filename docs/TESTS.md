# Tests

## The files

Each exercise comes with three Sather files.
For `leap` they are:

| File | Holds |
| --- | --- |
| `leap.sa` | your solution, class `LEAP` |
| `leap_test.sa` | the tests, class `LEAP_TEST` |
| `exercism_test.sa` | `EXERCISM_TEST`, which the tests include |

The test class's `main` calls your routines and compares what they return with what they should return.
Every test runs; none are skipped.

## Running the tests

Compile all three files together, naming the test class as the program's `main`, and run the result:

```shell
sacomp -chk *.sa -main LEAP_TEST -o leap_tests
./leap_tests
```

For another exercise, swap in its name: `two-fer` is `two_fer_test.sa` and `TWO_FER_TEST`.

The program prints a summary of the results and exits with a non-zero status if any test failed.
Lines starting `##EX` are for the online test runner, which reads results from them, and can be ignored.

`sacomp` writes the generated C into a directory next to the program, `leap_tests.code`.
It is safe to delete, and you don't need to submit it.

## Always use `-chk`

`-chk` switches on Sather's runtime checks:

- `pre` and `post` on routines, `assert`, and class invariants
- array bounds
- attribute access through a void reference
- arithmetic overflow

Without it, a contract is read and type-checked but never tested, and a mistake that would have been reported plainly can instead give a wrong answer or crash with no explanation.

The online test runner compiles with `-chk`, so test with it locally too, or a solution that passes on your machine can fail when you submit it.

A broken contract stops the whole program at that point, printing the routine and the source line.
It is not an exception: `protect` does not catch it, and no tests after it run.
When that happens, the contract or the code that called it needs fixing, whichever is wrong.

## Submitting

Submit only your solution file:

```shell
exercism submit leap.sa
```

The tests and `exercism_test.sa` are supplied by Exercism and are not changed by you.
