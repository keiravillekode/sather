# Instructions

A detective's notebook fills up as a case goes on, and empties again as
lines of enquiry are ruled out.

All five tasks go in the `CASE_NOTES` class.

## 1. Open a case

Return a new, empty notebook.

```sather
notes ::= CASE_NOTES::new_case;
notes.size
-- => 0
```

## 2. How many clues?

```sather
CASE_NOTES::clue_count(notes)
-- => 0
```

## 3. Write a clue down

Add a clue to the end of the notebook. This answers nothing — it changes
the notebook it is given.

```sather
CASE_NOTES::add_clue(notes, "muddy boots");
CASE_NOTES::clue_count(notes)
-- => 1
```

## 4. Read the case back

Return every clue in the notebook, joined with `"; "`. An empty notebook
reads as the empty string.

```sather
CASE_NOTES::summary(notes)
-- => "muddy boots; broken window"
```

## 5. Rule one out

Take the clue at a position out of the notebook. Everything after it moves
up. This also answers nothing.

```sather
CASE_NOTES::rule_out(notes, 0);
```
