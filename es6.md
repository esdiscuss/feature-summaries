# ES6 Proposals

## Function Improvements

### Arrow Function Syntax

A shorthand syntax for functions:

```js
let identity = x => x;
let square = x => x * x;
let fives = [];
nats.forEach(v => { if (v % 5 === 0) fives.push(v); });
```

`this` is bound lexically, rather than being dynamic

```js
const obj = {
  method: function () {
    return () => this;
  }
};
assert(obj.method()() === obj);
```

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:arrow_function_syntax)

### Function to String

Calling `toString` on a function must return the source code.  If the function inheirted `"use strict"` from a parent context it must be added to the body of the source code.

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:function_to_string)

### Function Name Property

The function `name` property will be specified to match the existing de facto standards.

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:function_name_property)

## Scoping, Binding and Calling

### Block Scoped Bindings

`let` is a new keyword that improves on `var` by providing block scoping and better use before set semantics.  [more...](http://wiki.ecmascript.org/doku.php?id=harmony:let)

`const` is like let, but doesn't allow you to modify a variable after creation.  [more...](http://wiki.ecmascript.org/doku.php?id=harmony:const)

block functions are let-scoped functions declared directly in block statements [more...](http://wiki.ecmascript.org/doku.php?id=harmony:block_functions)

### Destructuring

Object and array desctructuring.  Best explained with a few examples.

Swap two variables:

```js
[a, b] = [b, a]
```

Multi-value returns:

```js
function f() { return [1, 2] }
var [a, b] = f();
```

Object Destructuring:

```js
var { op: a, lhs: { op: b }, rhs: c } = getASTNode()
// a, b and c now have the apropriate values
```

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:destructuring) [even more...](http://wiki.ecmascript.org/doku.php?id=harmony:refutable_matching)

### Optional Parameters

Allow trailing parameters to have default values:

```js
function inc(value, incBy = 1) {
  return value + incBy;
}
assert(inc(0) === 1);
assert(inc(0, 5) === 5);
```

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:parameter_default_values)

### Rest Parameters

Allows getting the remaining arguments of a function as an array:

```js
function all(fn, ...args) {
  args.forEach(fn);
}
all(console.log, 1, 2, 3, 4);
```

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:rest_parameters)

### Spread Parameters

Symetric to Rest Parameters

```js
var list = [1, 2, 3, 4];
all(console.log, ...list);
```

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:spread)

### Proper Tail Calls

Proper tail calls help optimise carefully designed recursive functions.

```js
//not optimised
function factorial(n) {
  if (n === 0) return 1;
  else return n * factorial(n - 1);
}

//optimised
function factorial(n, acc = 1) {
  if (n === 0) return acc;
  else return factorial(n - 1, acc * n);
}
```

[more...](http://wiki.ecmascript.org/doku.php?id=harmony:proper_tail_calls)
