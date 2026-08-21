# Code Inclusion

`circus-acts` used `<` to say that a class *can do* what an abstract class
describes. It said nothing about how.

`include` is the other half: it takes the actual code from another class and
puts a copy of it in this one.

```sather
class WARM_UP is

   count : INT is return 8; end;

   describe : STR is return count + " counts"; end;

end; -- class WARM_UP

class JAZZ_ROUTINE is

   include WARM_UP;

   -- count and describe are now here too, as though written out.

end; -- class JAZZ_ROUTINE
```

`JAZZ_ROUTINE::count` is 8, without `JAZZ_ROUTINE` mentioning it.

## These are two separate decisions

Most languages join them: one `extends` both hands down the code and makes
the subclass usable wherever the superclass is. Sather keeps them apart.

| Written | Says |
| --- | --- |
| `class A < $B` | an `A` can be used wherever a `$B` is wanted |
| `class A is include B` | `A` starts with a copy of `B`'s code |

Either without the other, or both. Including a class does **not** make it a
subtype: after `include WARM_UP`, a `JAZZ_ROUTINE` still cannot be used
where a `WARM_UP` is wanted, and nothing pretends otherwise.

## Renaming

An included routine can be brought in under a different name:

```sather
   include WARM_UP count -> warm_up_count;
```

Several are separated by commas:

```sather
   include WARM_UP count -> warm_up_count, describe -> warm_up_describe;
```

## Leaving one out

Renaming to *nothing* leaves it out, which is how to replace it:

```sather
class TAP_ROUTINE is

   include WARM_UP describe -> ;

   describe : STR is return "Tap: " + count + " counts"; end;

end; -- class TAP_ROUTINE
```

`count` comes in as usual; `describe` does not, so writing one here is not a
clash. Without the `describe -> ;` the compiler would refuse: two routines
of the same name and arguments in one class is an error, and Sather will not
guess which you meant.

That is the difference from an override in most languages: the replacement
is announced rather than implied.
