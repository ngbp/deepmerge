deepmerge
=========

Merge the enumerable attributes of two objects deeply.

example
=======

```js
var util = require('util')
var merge = require('deepmerge')

var x = { foo: { bar: 3 },
  array: [ { does: 'work', too: [ 1, 2, 3 ] } ] }
var y = { foo: { baz: 4 },
  quux: 5,
  array: [ { does: 'work', too: [ 4, 5, 6 ] }, { really: 'yes' } ] }

console.log(util.inspect(merge(x, y), false, null))
```

output:

```js
{ foo: { bar: 3, baz: 4 },
  array: [ { does: 'work', too: [ 1, 2, 3, 4, 5, 6 ] }, { really: 'yes' } ],
  quux: 5 }
```

methods
=======

var merge = require('deepmerge')

merge(x, y, allowOverwrite)
-----------

Merge two objects `x` and `y` deeply, returning a new merged object with the
elements from both `x` and `y`.

If an element at the same key is present for both `x` and `y`, the value from
`y` will appear in the result.

The merge is immutable, so neither `x` nor `y` will be modified.

The merge will also merge arrays and array values.

If `y` has objects whose key have a prefix of `^`, the merge will overwrite the value for
the same key in `x`, rather than merging the values.  For example:

```js
var y = [
    { "^key1": { "subkey": "two" }},
    { "key2": { "subkey": "three" }}
];

var x = [
    { "key1": { "subkey1": "one", "subkey2": "two" }}
]
```

running `merge(x, y)` will actually produce the following, completely overwriting `x.key1`

```js
var merged = [
    { "key1": { "subkey": "two" }},
    { "key2": { "subkey": "three" }}
]
```

You must explicitly pass `false` as the 3rd parameter to the `merge` method to prevent such overwrites.

install
=======

With [npm](http://npmjs.org) do:

```
npm install <TBC>
```

For the browser, you can install with [bower](http://bower.io/):

```
bower install <TBC>
```

test
====

With [npm](http://npmjs.org) do:

```
npm test
```
