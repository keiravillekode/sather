# Hints

## General

- An `include` goes inside the class, usually as its first line.
- Only what you rename or leave out changes. Everything else comes in as
  it was.
- Delete each class's placeholder routines as you go. A placeholder left
  behind clashes with the included routine of the same name.

## 1. The jazz routine

- One line inside the class: `include WARM_UP;`
- Nothing else. The class body is that line and no more.

## 2. The tap routine

- Leave `describe` out of the include by renaming it to nothing — `-> ;`
  with nothing after the arrow — which is what makes room for the one you
  write.
- Without that, the compiler complains that `describe` is defined twice.
  The error is the feature: Sather will not silently pick one.

## 3. The finale

- Two entries in one include, separated by a comma: rename `counts` and
  leave `describe` out.
- Then write `counts` returning twice `warm_up_counts`, and `describe`.
- `describe` should call `counts`, not work the number out again.
- Remember that a number cannot have a string added to it, so start the
  description with its words, and the counts join on fine.
