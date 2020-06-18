---
layout: post
title: What's New in Zephir (I)
date: 2013-09-23 00:00:00
tags:
  - zephir
  - features
  - improvements
---

In the last few weeks Zephir has seen a lot of new features, improvements, and bug fixes. In this brief post we're going to highlight some of the most prominent ones:

### Static Type Inference
We have implemented a multi-pass static type inference optimizer for Zephir. Basically, thanks to these passes, the compiler can automatically convert dynamic variables into static variables producing simpler and possibly code that performs at best.

Let's assume we have the following code:

```zephir
var a, b; int c;

let a = "1", b = 2, c = b + a;
return c;
```

There are clear opportunities to declare `a` and `b` as `integer` variables, the compiler can address these opportunities producing better code without modifying the original behavior.

```zephir
int a, b, c;

a = 1;
b = 2;
c = (b + a);
RETURN_LONG(c);
```

The compiler also performs an additional optimization called: [Constant Propagation](https://en.wikipedia.org/wiki/Constant_folding). Since `a` and `b` can be easily replaced by their constant values the final compiled code will be:

```zephir
RETURN_LONG(3);
```

This example above showed how there was a code reduction starting from a high-level language representation.

### Type Hints
Zephir always tries to check whether an object implements methods and properties called/accessed on a variable that is inferred to be an object:

```zephir
let o = new MyObject();

// Zephir checks if "myMethod" is implemented on MyObject
o->myMethod(); 
```

However, due to the dynamism inherited from PHP, sometimes it is not easy to know the class of an object so Zephir can not produce errors reports effectively. A `type hint` tells the compiler which class is related to a dynamic variable allowing the compiler to perform more compilation checks:

```zephir
// Tell the compiler that "o"
// is an instance of class MyClass
let o = <MyClass> this->_myObject; 
o->myMethod();	
```

### Fetch Operator
`Fetch` is an operator that reduce a common operation in PHP into a single instruction:

```php
<?php

if (isset($myArray[$key])) {
	$value = $myArray[$key];
	echo $value;
}
```

In Zephir, you can write the same code as:

```zephir
if fetch value, myArray[key] {
	echo value;
}
```

`Fetch` only returns `true` if the `key` is a valid item in the array, only in that case, `value` is populated.

That's it for this week. Thank you all and see you next week.

<3 Zephir Team