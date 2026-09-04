# Code Inclusion

`circus-acts` used `<` to say that a class *can do* what an abstract class
describes. It said nothing about how.

`include` is the other half: it takes the actual code from another class
and puts a copy of it in this one.

```sather
class SOUND_CHECK is

   steps : INT is return 3; end;

   describe : STR is return steps.str + " steps"; end;

end; -- class SOUND_CHECK

class MIC_CHECK is

   include SOUND_CHECK;

   -- steps and describe are now here too, as though written out.

end; -- class MIC_CHECK
```

`MIC_CHECK::steps` is 3, without `MIC_CHECK` mentioning it.

## These are two separate decisions

Most languages join them: one `extends` both hands down the code and makes
the subclass usable wherever the superclass is. Sather keeps them apart.

| Written | Says |
| --- | --- |
| `class A < $B` | an `A` can be used wherever a `$B` is wanted |
| `class A is include B` | `A` starts with a copy of `B`'s code |

Either without the other, or both. Including a class does **not** make it
a subtype: after `include SOUND_CHECK`, a `MIC_CHECK` still cannot be used
where a `SOUND_CHECK` is wanted, and nothing pretends otherwise.

## Renaming

An included routine can be brought in under a different name:

```sather
   include SOUND_CHECK steps -> sound_steps;
```

Several are separated by commas:

```sather
   include SOUND_CHECK steps -> sound_steps, describe -> sound_describe;
```

## Leaving one out

Renaming to *nothing* leaves it out, which is how to replace it:

```sather
class LIGHT_CHECK is

   include SOUND_CHECK describe -> ;

   describe : STR is return "Lights: " + steps + " steps"; end;

end; -- class LIGHT_CHECK
```

`steps` comes in as usual; `describe` does not, so writing one here is not
a clash. Without the `describe -> ;` the compiler would refuse: two
routines of the same name and arguments in one class is an error, and
Sather will not guess which you meant.

That is the difference from an override in most languages: the replacement
is announced rather than implied.
