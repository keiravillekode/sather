# Hints

## 1. The three acts

- The class header names the abstract class after `<`:
  `class JUGGLING < $ACT is`.
- Each class must define both `name` and `minutes`, exactly as the
  abstract class declares them. Missing one is a compile error naming the
  routine.
- Each also needs a `create`, or `#JUGGLING` has nothing to call. For
  `JUGGLING` and `TUMBLING` the stub's `return new;` is already all there
  is to it.
- `TRAPEZE` keeps its height in the attribute the stub declares, so its
  `create` has to set it.
- `+` joins a number onto a string, so the trapeze's name needs no
  converting.

## 2. The show

- The argument type is `ARRAY{$ACT}`. That is what lets one array hold all
  three kinds.
- `acts.elt!` gives an `$ACT`. Calling `.minutes` on it runs the right one
  by itself — that is dispatch, and it is the point of the exercise. There
  is nothing to check and no `typecase` to write.
- `billing` builds a string in a loop, so `FSTR`, and the `", "` goes
  before every name except the first.
- `longest` keeps the best act so far. Starting the best minutes at `-1`
  means the first act always beats it, which handles the empty show
  without a special case: the name stays `""`.
