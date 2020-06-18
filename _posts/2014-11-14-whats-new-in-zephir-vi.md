---
layout: post
title: What's New in Zephir (VI)
date: 2014-11-14 00:00:00
tags:
  - zephir
---

Last weeks many improvements have been added to Zephir. We have nailed down a concrete list of features and are hard at work on implementing them. Zephir has gone through a long evolution. If you haven't looked at Zephir in a while, you may be now feel a better and stable version than early alpha versions.

### Closures
A very hard feature to implement is now available in Zephir. Closures allow to implement custom scopes of logic that are isolated of the current method and you can use to implement promises or just make them work as callbacks:

```zephir
call_user_func(function() { echo "hello"; });
```

Alongside with built-in methods you can do amazing and elegant things as:

```zephir
print_r([4, 8, 12, 32, 5]->map(
    function(int! x) { return x * x; }
));
```

Or use the short syntax for closures:

```zephir
print_r([4, 8, 12, 32, 5]->map(x => x * x));
```

In plain PHP you need to do something like this:

```php
print_r(array_map(
    function($x) { return $x * $x; },
    [4, 8, 12, 32, 5]
));
```

### Anonymous Variables
A new useful warning was introduced recently in Zephir. It warns you whenever a variable is unused aside from its declaration:

```zephir
public static function some(var v)
{
    var z;
    if !empty v {
        let z = v;
    }
}
```

Variable `z` is assigned within the `if` block however its value is never used:

```sh
Warning: Variable "z" assigned but not used in Zafiro\Functional::some in 
/Users/scott/zafiro/zafiro/functional.zep on 118 [unused-variable]

              let z = v;
------------------^
```

However, sometimes a language may require create unnecessary variables, in the case of Zephir, define these variables produces a warning when they are not used:

```zephir
public static function some(var data)
{
    var v;

    for v in data {
        echo "hello";
    }
}
```

Producing the following warning:

```zephir
Warning: Variable "v" assigned but not used in Zafiro\Functional::some in 
/Users/scott/zafiro/zafiro/functional.zep on 117 [unused-variable]

      for v in data {
    ----------------^
```

How to avoid this warning if you really don't need that variable? Anonymous variables come to the rescue! To create an anonymous variable, you just have to use an underscore where required:

```zephir
public static function some(var data)
{
    for _ in data {
        echo "hello";
    }
}
```

This way the warning is gone, also you tell Zephir to avoid allocate unnecessary data or assignments.

Other uses of anonymous variables could be receive parameters in closures:

```zephir
data->walk(
    function(_, int key) { echo key; }
);
```

### Windows Support
We're near to fully support Zephir on Windows, currently you can generate the code of your extension and manually compile it using MS Visual C++. Keep in touch for a full guide about this topic.

### References
We're discussing the best way to implement references under the computational model of Zephir, you can give us your opinion here

Follow [@zephirlang](https://twitter.com/zephirlang) on Twitter for more updates


<3 Zephir Team