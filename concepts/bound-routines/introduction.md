# Bound Routines

Everything so far has passed *values* around: numbers, strings, objects. A
**bound routine** lets you pass around a routine itself — something to be
called later, by code that does not know what it is.

An understudy is the idea exactly: the stage manager holds a way of
playing the part, without knowing who it is or what they will do.

## Making one

`bind` takes a call with holes in it, written `_`:

```sather
   exclaim(text : STR) : STR is return text + "!"; end;

   ...

   voice ::= bind(exclaim(_));
```

`voice` is now a value like any other. Calling it happens later:

```sather
   voice.call("places everyone")      -- "places everyone!"
```

## The type

The type of a bound routine is `ROUT`, with the argument types in braces
and the return type after a colon:

```sather
   voice : ROUT{STR}:STR := bind(exclaim(_));
```

Read `ROUT{STR}:STR` as "a routine taking a `STR` and answering a `STR`".

| Written | Means |
| --- | --- |
| `ROUT{STR}:STR` | takes a `STR`, answers a `STR` |
| `ROUT{INT,INT}:BOOL` | takes two `INT`s, answers a `BOOL` |
| `ROUT{STR}` | takes a `STR`, answers nothing |
| `ROUT:INT` | takes nothing, answers an `INT` |

Since it is a type, it can be an argument:

```sather
   announce(text : STR, voice : ROUT{STR}:STR) : STR is
      return voice.call(text);
   end;
```

`announce` has no idea what `voice` does. That is the point: it can be
handed `exclaim`, or anything else of that shape.

## Filling in some of the arguments

Not every argument has to be a hole. Anything written out is fixed when
the bind happens:

```sather
   print_run(copies : INT, page : STR) : STR is ... end;

   pair ::= bind(print_run(2, _));      -- ROUT{STR}:STR
```

`pair` takes only the page, because the `2` is already decided. The value
is worked out at the moment of binding and kept, so changing the variable
it came from afterwards makes no difference.

This is how one general routine becomes many specific ones.

## Binding the object too

For a routine on an object, the object is the first thing in the call and
can be fixed or left as a hole:

```sather
   bind(board.home_goal)      -- this board's, always
   bind(_.home_goal)          -- whichever board is handed in later
```
