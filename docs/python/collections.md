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

## Counter

[Docs](https://docs.python.org/3/library/collections.html#counter-objects)

### Mathematical operations

`Counter`s can be combined using the `.update()` and `.subtract()` methods, which will perform in-place addition and subtraction between corresponding elements.

There is also a second, operator-based interface that makes them behave like multisets.
As such, the results of these operations will *only* include elements whose counts are greater than zero.

- Binary `+` and `-` do what you would expect.
- Unary `+` and `-` are equivalent to adding to/subtracting from an empty `Counter`.
    This effectively selects only the positive and (the absolute values of) the negative elements, respectively.
- Binary `&` and `|` return the minimum and maximum of each corresponding pair of elements.

(In-place versions of these are also available.)

The comparison operators (`>`, `>=`, `<`, `<=`) check for inclusion of one within the other, ie. that one is the subset of the other.

## Deque

[Docs](https://docs.python.org/3/library/collections.html#collections.deque)

Double-ended queues.

Unlike lists, `deque`s provide constant-time pushes and pops at *either* end, not just at the tail.
They have the same `.append()`, `.extend()` and `.pop()` methods that operate at the tail, as well as homologous `.{append,extend,pop}left()` that operate at the head.
The trade-off is that accessing the element at a given index is no longer constant-time, unless it's the head or tail.

There is also a `.rotate()` method that rotates the elements `n` steps right (`n` positive) or left (`n` negative).

They're unbounded, unless `maxlen` was provided to the constructor.
In that case the `deque` will not grow beyond that size: once it's full, adding an element will result in an element being dropped from the opposite end.

The documentation includes some [recipes](https://docs.python.org/3/library/collections.html#deque-recipes).
