# Tests

Each exercise has three Sather files: your solution, its tests, and
`exercism_test.sa`, which the tests use.
For an exercise such as `leap`, compile them together and run the result:

```shell
sacomp -chk *.sa -main LEAP_TEST -o leap_tests
./leap_tests
```

The `-main` class is the test file's name in capitals: `leap_test.sa` holds `LEAP_TEST`.

Keep `-chk`.
It turns on checking of `pre`, `post`, `assert` and class invariants, as well as array bounds and void access.
The online test runner uses it, so without it your solution can pass locally and fail on the website.
