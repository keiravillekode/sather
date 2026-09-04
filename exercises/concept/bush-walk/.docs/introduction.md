# Custom Iterators

You have been using iterators since `bird-survey`. Now you write one.

## yield

An iterator looks like a routine with two differences: its name ends in
`!`, and it hands over values with `yield` instead of `return`.

```sather
   squares!(once count : INT) : INT is
      loop
         n ::= 1.upto!(count);
         yield n * n;
      end;
   end;
```

`yield` gives a value to the loop that called the iterator, and then
**waits**. When that loop comes round again, the iterator carries on from
just after the `yield`, with everything exactly as it left it — its
variables, its own loop, its place.

That is what an iterator is: a routine that can pause in the middle and be
resumed.

```sather
   loop
      #OUT + MATHS::squares!(3) + " ";      -- 1 4 9
   end;
```

## Ending

An iterator ends in either of two ways.

**Running out.** When the iterator's own loop finishes, or the routine
reaches its end, it is over — and the loop that called it ends
immediately.

**quit.** `quit` ends it there and then, without yielding.

```sather
   readings!(once temps : ARRAY{INT}) : INT is
      loop
         t ::= temps.elt!;
         -- A sensor that has come unplugged reads -300.
         if t < -273 then quit; end;
         yield t;
      end;
   end;
```

That yields temperatures until it meets an impossible one, and stops.
`quit` is to an iterator what `return` is to a routine, except that it
carries no value — there is nothing left to hand over.

## once

An argument marked `once` is worked out one time only, when the loop
starts, rather than every time round:

```sather
   squares!(once count : INT) : INT is
```

Use it for anything that does not change between turns, which is most
arguments. The library's own iterators do: `upto!(once i : SAME)`.

## Iterators with no value

An iterator need not yield anything. `times!` is one:

```sather
   steps!(once count : INT) is
      loop
         ignored ::= 1.upto!(count);
         yield;
      end;
   end;
```

A bare `yield` hands over nothing and simply lets the loop go round.

## Where the position lives

Each *place in the program* that calls an iterator keeps its own
position — which is why calling the same iterator twice in one loop body
walks it twice over. Now you can see why: the two calls are two separate
paused routines.
