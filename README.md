Explanation
===========

Lets say we have the following hierarchy and we want to be able to query it
level by level in firebase.

- Drinks
  - Coffee
      - Irish
      - Latte
  - Soda
      - Coke
      - Fanta

We can achieve this by flattening to a map with some careful encoding of the
key. Doing that will give us the following structure.
```
{
  "001" : {"name": "Drinks"},
  "001|>001" : {"name": "Coffee"},
  "001|001|>001" : {"name":"Irish"},
  "001|001|>002" : {"name":"Latte"},
  "001|>002" : {"name": "soda"},
  "001|002|>001" : {"name": "Coke"},
  "001|002|>002" : {"name": "Fanta"}
}
```
I choose to use "|" and "|>" as separators but they can be substituted by
something else.

We can then use `orderByKey()`, `startAt()` and `endAt()` to retrieve a slice
only containing direct children for any node we want.

See `Fetcher` class for implementation.
