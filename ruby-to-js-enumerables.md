# Ruby To JavaScript Enumerables

Every language needs to have a different set of names for the
functions/methods that they use with collections. This document seeks to
draw parallels between similar functions in [Ruby's Enumerable
module](http://ruby-doc.org/core-2.2.3/Enumerable.html) and JavaScript's
[LoDash library](https://lodash.com/).

---

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
