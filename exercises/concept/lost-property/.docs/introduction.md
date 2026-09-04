# Generic Classes

You have used `ARRAY{STR}`, `FMAP{STR,INT}` and `FSET{STR}` since early
on. The braces have always held a type. Now you write a class with braces
of its own.

## The problem

Moving house, everything goes into crates, and a crate should remember
what it holds. A crate for books:

```sather
class BOOK_CRATE is
   attr contents : BOOK;
   ...
end;
```

and then the same class again for lamps, and again for plates. Three
copies that differ in one word.

## The type parameter

```sather
class CRATE{T} is

   attr contents : T;

   create(thing : T) : SAME is
      crate ::= new;
      crate.contents := thing;
      return crate;
   end;

end; -- class CRATE{T}
```

`{T}` after the class name is a **type parameter**. `T` is not a type — it
is a stand-in for whatever type is supplied when the class is used. Inside
the class, `T` is used exactly as any type name would be.

## Using it

Supply the type in braces:

```sather
   lamp ::= #CRATE{STR}("reading lamp");
   count ::= #CRATE{INT}(24);

   lamp.contents      -- "reading lamp", a STR
   count.contents     -- 24, an INT
```

`CRATE{STR}` and `CRATE{INT}` are two different types. Putting one where
the other is wanted is an error the compiler catches, exactly as if you
had written the two classes out by hand — which, in effect, is what
happens: Sather builds a separate class from the pattern for each type
actually used.

So there is no cost to this at run time, and no loss of type information:
`lamp.contents` really is a `STR`, not something that has to be checked or
converted.

## More than one

A class may take several parameters, separated by commas. `FMAP{K,T}` is
the example you already know.

```sather
class LABELLED{L,T} is
   attr label : L;
   attr item : T;
   ...
end;
```

## Naming

Single capital letters by convention: `T` for a thing, `K` for a key, `E`
for an element. The library uses them throughout.
