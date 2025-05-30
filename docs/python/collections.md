# Collections

## Sets

[Docs](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset)

### Modifying

- `s.add(element)` to add a single element, rather than `s | {element}`.
- `s.remove(element)` will raise `KeyError` if `element` is not present.
    Use `.discard(element)` if this doesn't matter.

### Chaining operations

- All the methods except `.symmetric_difference()` can take multiple arguments.
- It's `s1 |= s2 | s3 ...` and `s1 &= s2 & s3`, but `s1 -= s2 | s3` (though this obviously means the same thing).

To apply an operation to an arbitrary list of sets, you could do something like `first, *others = sets; s = first.union(*others)`.
However `s = set.union(*sets)` is both more concise, and also works correctly when the `sets` list contains only one element.

### Caveats

The operators require both operands to be `set` instances, but the methods can take anything iterable as an argument.
This also applies when using them as class methods: only the first argument is required to be a set.

Python's sorting algorithm only uses the objects' `.__lt__()` method.
With sets, this determines whether one is a proper subset of the other and has nothing to do with ordering.
Therefore `sorted([s1, s2, s3])` probably won't do what you want (sorting the content of a set does, of course).
