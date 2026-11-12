# Code Inclusion

`circus-acts` used `<` to say that a class *can do* what an abstract class
blurbs. It said nothing about how.

`include` is the other half: it takes the actual code from another class and
puts a copy of it in this one.

```sather
class ROBOT_BASE is

   wheels : INT is return 4; end;

   blurb : STR is return wheels.str + " wheels"; end;

end; -- class ROBOT_BASE

class DELIVERY_ROBOT is

   include ROBOT_BASE;

   -- wheels and blurb are now here too, as though written out.

   payload : INT is return 20; end;

end; -- class DELIVERY_ROBOT
```

`DELIVERY_ROBOT::wheels` is 4, without `DELIVERY_ROBOT` mentioning it.

## These are two separate decisions

Most languages join them: one `extends` both hands down the code and makes
the subclass usable wherever the superclass is. Sather keeps them apart.

| Written | Says |
| --- | --- |
| `class A < $B` | an `A` can be used wherever a `$B` is wanted |
| `class A is include B` | `A` starts with a copy of `B`'s code |

Either without the other, or both. Including a class does **not** make it a
subtype: after `include ROBOT_BASE`, a `DELIVERY_ROBOT` still cannot be
used where a `ROBOT_BASE` is wanted, and nothing pretends otherwise.

## Renaming

An included routine can be brought in under a different name:

```sather
   include ROBOT_BASE wheels -> base_wheels;
```

Several are separated by commas:

```sather
   include ROBOT_BASE wheels -> base_wheels, blurb -> base_blurb;
```

Only the name changes. The copied `blurb` still calls `wheels` by that
name, so after either of these the class needs a `wheels` of its own, or
the compiler refuses.

## Leaving one out

Renaming to *nothing* leaves it out, which is how to replace it:

```sather
class TRACKED_ROBOT is

   include ROBOT_BASE blurb -> ;

   blurb : STR is return "Runs on tracks"; end;

end; -- class TRACKED_ROBOT
```

`wheels` comes in as usual; `blurb` does not, so the one written here is
the only one.

This compiler would in fact let a routine written in the class win over an
included one of the same name even without the `blurb -> ;`, and it would
say nothing. Write the `-> ;` anyway. It announces the replacement on the
include line, where a reader looks to see what came from `ROBOT_BASE`,
rather than leaving it implied. Between two includes there is no such
leniency: two included routines of the same name and arguments in one class
is an error, and Sather will not guess which you meant.
