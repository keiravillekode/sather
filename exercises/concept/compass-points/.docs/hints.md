# Hints

## General

- There is no `new` in an immutable class. `create` follows the idiom the
  introduction shows: declare a variable of the class, which already
  exists, and build the answer from it.
- Calling an attribute's routine — `b.degrees(x)` — does not change `b`.
  It answers a new object, which is why that answer is the thing to
  return.

## 1. Take a bearing

- `%` brings a number into range, and Sather's `%` never answers negative
  for a positive right-hand side — so one `%` is enough on its own, minus
  signs and all.

## 2. Turn

- Add the turn to the degrees and make a new bearing from the total, with
  `#BEARING`.
- `create` already brings the answer back into range, so there is nothing
  to do about turning past north.

## 3. Compare

- One line: compare the two `degrees`.
- The argument's type is `SAME`, and you read its attribute the usual way:
  `other.degrees`.

## 4. Name the point

- Dividing the degrees by 45 nearly works, but it measures each point from
  its edge rather than its centre. Shifting the degrees by half a segment
  before dividing fixes that; `%` brings the answer for north's upper half
  back round to nought.
- Then a `case` on that number, with the eight names — and an `else`,
  which `case` always needs even when the eight arms cover every possible
  value.

## 5. Write it down

- `+` joins the pieces, but only a string may have things added to it. The
  number comes first here, so it needs `degrees.str` to start the join
  off. `"a" + 1` is fine; `1 + "a"` does not compile.
- Call `point` rather than working the name out again.
