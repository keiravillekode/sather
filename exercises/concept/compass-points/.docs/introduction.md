# Immutable Classes

A `SCOREBOARD` is a thing that changes. Two names for one scoreboard see
the same score, because there is only one board and both names point at
it.

A distance is not like that. Three kilometres does not become something
else; it simply *is*. Numbers behave that way, and so do strings — and so
can classes of your own.

## immutable

```sather
immutable class DISTANCE is

   readonly attr metres : INT;

end; -- class DISTANCE
```

Two words change everything. An object of an immutable class is a
**value**, not a thing pointed at:

- it is copied when assigned or passed, so nobody else can change yours;
- it can never be void;
- and its attributes cannot be assigned to.

## Changing one by making another

Since `metres := 500` is not allowed, `attr` gives something else: a
routine taking the new value and answering **a new object** with it
changed.

```sather
   d ::= d.metres(500);      -- not d.metres := 500
```

The original is untouched. That is the whole idiom, and it is how `create`
is written:

```sather
   create(m : INT) : SAME is
      d : SAME;                     -- starts with everything at nought
      return d.metres(m);
   end;
```

There is no `new` here. An immutable object always exists, so `d : SAME`
already is one, with every attribute at its empty value.

A routine that "changes" a distance therefore returns a new one:

```sather
   further(by : INT) : SAME is
      return #DISTANCE(metres + by);
   end;
```

## Comparing

Values are compared by what they hold, not by which object they are — but
you have to say how. Write `is_eq`, and `=` will use it:

```sather
   is_eq(other : SAME) : BOOL is
      return metres = other.metres;
   end;
```

Without it, `=` on two distances will not compile.

## Which to choose

Use an immutable class when the thing has no identity and nothing about it
can sensibly change: a distance, a point, a date, a bearing. Use an
ordinary class when the thing is one particular thing that things happen
to: a scoreboard, a harness, a file.

The test is whether "the same" means "equal" or "the very same one".
