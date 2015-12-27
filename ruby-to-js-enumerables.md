# Ruby To JavaScript Enumerables

Every language needs to have a different set of names for the
functions/methods that they use with collections. This document seeks to
draw parallels between similar functions in [Ruby's Enumerable
module](http://ruby-doc.org/core-2.2.3/Enumerable.html) and JavaScript's
[LoDash library](https://lodash.com/).

- [`#all?` → `.every`](#all--every)
- [`#any?` → `.some`](#any--some)
- [`#chunk` → `???`](#chunk--)
- [`#collect` → `.map`](#collect--map)
- [`#collect_concat` → `???`](#collect_concat--)
- [`#count` → `.size`](#count--size)

---

### `#all?` → `.every`

[`#all?`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-all-3F) (Ruby)

> Passes each element of the collection to the given block. The method
> returns true if the block never returns `false` or `nil`.

```ruby
> [1,2,3].all? { |item| item > 0 }
=> true
> [1,2,3].all? { |item| item.even? }
=> false
```

[`.every`](https://lodash.com/docs#every) (JavaScript)

> Checks if predicate returns truthy for **all** elements of collection.

```javascript
> _.every([1,2,3], function(item) { return item > 0; });
=> true
> _.every([1,2,3], function(item) { return item % 2 === 0; });
=> false
```

---

### `#any?` → `.some`

[`#any?`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-any-3F)
(Ruby)

> Passes each element of the collection to the given block. The method
> returns true if the block ever returns a value other than `false` or `nil`.

```ruby
> [1,2,3].any? { |item| item < 0 }
=> false
> [1,2,3].any? { |item| item.even? }
=> true
```

[`.some`](https://lodash.com/docs#some) (JavaScript)

> Checks if predicate returns truthy for **any** element of collection.

```javascript
> _.some([1,2,3], function(item) { return item < 0; });
=> false
> _.some([1,2,3], function(item) { return item % 2 === 0; });
=> true
```

---

### `#chunk` → `???`

[`#chunk`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-chunk)
(Ruby)

> Enumerates over the items, chunking them together based on the return
> value of the block. Consecutive elements which return the same block
> value are chunked together.

```ruby
> [1,2,3].chunk { |item| item > 0 }.to_a
=> [[true, [1, 2, 3]]]
> (1..10).chunk { |item| item % 3 == 0 }.to_a
=> [[false, [1, 2]],
 [true, [3]],
 [false, [4, 5]],
 [true, [6]],
 [false, [7, 8]],
 [true, [9]],
 [false, [10]]]
```

`???` (JavaScript)

---

### `#collect` → `.map`

[`#collect`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-collect)
(Ruby),
*also known as
[`#map`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-map)*

> Returns a new array with the results of running block once for every
> element in enum.

```ruby
> [1,2,3].collect { |item| item + 1 }
=> [2, 3, 4]
> [1,2,3].collect { |item| item * item }
=> [1, 4, 9]
```

[`map`](https://lodash.com/docs#map) (JavaScript)

> Creates an array of values by running each element in collection through
> iteratee.

```javascript
> _.map([1,2,3], function(item) { return item + 1; });
=> [2, 3, 4]
> _.map([1,2,3], function(item) { return item * item; });
=> [1, 4, 9]
```

---

### `#collect_concat` → `???`

[`#collect_concat`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-collect_concat) (Ruby),
*also known as
[`#flat_map`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-flat_map)*

> Returns a new array with the concatenated results of running block once
> for every element in enum.

```ruby
> [1,2,3].collect_concat { |item| (1..item).to_a }
=> [1, 1, 2, 1, 2, 3]
> ["one", "two", "three"].collect_concat { |item| [item, item.upcase] }
=> ["one", "ONE", "two", "TWO", "three", "THREE"]
```

`???` (JavaScript)

There is no direct equivalent provided by LoDash, however the `.map` and
`.flatten` functions can be combined to achieve the same effect.

```javascript
> _([1,2,3])
    .map(function(item) { return _.range(1,item+1); })
    .flatten()
    .value();
=> [1, 1, 2, 1, 2, 3]
> _(["one","two","three"])
    .map(function(item) { return [item, item.toUpperCase()]; })
    .flatten()
    .value();
=> ["one", "ONE", "two", "TWO", "three", "THREE"]
```

---

### `#count` → `.size`

[`#count`](http://ruby-doc.org/core-2.2.3/Enumerable.html#method-i-count)
(Ruby)

> Returns the number of items in enum through enumeration.

```ruby
> [1,2,3].count
=> 3
> {a: 1, b: 2}.count
=> 2
```

[`.size`](https://lodash.com/docs#size) (JavaScript)

> Gets the size of collection by returning its length for array-like values
> or the number of own enumerable properties for objects.

```javascript
> _.size([1,2,3])
=> 3
> _.size({a: 1, b: 2})
=> 2
```
