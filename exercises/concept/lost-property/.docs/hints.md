# Hints

## General

- Inside the class, `T` is used exactly where a type name would go: in an
  attribute, an argument, or a return type.
- The tests use `LOST_BOX{STR}` and `LOST_BOX{INT}`, so nothing may assume
  the thing is a string — except through the constraint in task 5.

## 1. Take something in

- The stub declares the three attributes: the item, whose it is, and
  whether it has been claimed. `create` sets the first two from its
  arguments.
- `claimed` needs no setting. A `BOOL` attribute starts false.

## 2. Claim it

- No return type at all, and one line in the body.

## 3. Is it still waiting?

- The opposite of `claimed`, and `~` flips an answer over. No `if` needed.

## 4. Swap the contents

- Keep the old item in a variable before overwriting, then return it.
  Assigning first loses it.
- Both the argument and the return type are `T`.

## 5. Write it up

- Change the class header to `class LOST_BOX{T < $STR}`.
- Without that, `item.str` does not compile, because nothing is known
  about a bare `T` beyond being able to move it about.
- The item comes first in the line, so start the join with `item.str`.
