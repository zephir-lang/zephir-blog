---
layout: post
title: What's New in Zephir (III)
date: 2013-09-30 00:00:00
tags:
  - zephir
---

Welcome to the new edition of our `what's new` series. These days, more bugs have been fixed and a number of small improvements have been made.

### Polymorphic Return-Type Hints
Last week, we were implementing return-type hints, basically, with this feature, Zephir can know that a method returns a particular type of data or returns an instance of a specific class.

In the following example, we have a method returns that traverses a set of registered paths and return the first one that meet the property of being allowed:

```zephir
public function getFirstAllowedPaths() -> <App\Path>
{
    var path;
    
    for path in this->_paths {
        if path->isAllowed() == true {
            return path;
        }
    }
}
```

In the previous method, Zephir will complaint because it reaches its end without returning a valid instance of `<App\Path>`. To fix this, a developer could throw an exception telling the user about this exceptional situation:

```zephir
public function getFirstAllowedPaths() -> <App\Path>
{
    var path;
    
    for path in this->_paths {
        if path->isAllowed() == true {
            return path;
        }
    }

    throw new App\Exception("error!!");
}
```

However, if there is no path that meets this condition, a developer may return `false` or `null` as a signal that no data is available (instead of throwing an exception).

By using polymorphic return-type hints a developer can specify more than one type of data or class instances allowed to be returned by the method.

```zephir
public function getFirstAllowedPaths() -> <App\Path> | boolean
{
    var path;
    
    for path in this->_paths {
        if path->isAllowed() == true {
            return path;
        }
    }

    return false;
}
```

### Strict/Flexible Parameter Data-Types
Another feature we're implementing is strict/flexible parameter data types. In Zephir, you can specify the data type of each parameter of a method.

By default, these data-types are flexible, this means that if a value with wrong (but compatible) data-type is passed, Zephir will try to transparently convert it to the expected one:

```zephir
public function filterText(string text, boolean escape=false)
{
    //...
}
```

The above method will work with the following calls:

```zephir
$o->filterText(1111, 1); // OK
$o->filterText("some text", null); // OK
$o->filterText(null, true); // OK
$o->filterText("some text", true); // OK
$o->filterText(array(1, 2, 3), true); // FAIL
```

However, passing a wrong type could be often leads to bugs, a bad use of a specific API would produce unexpected results. You can disallow the automatic conversion by setting the parameter with a strict data-type:

```zephir
public function filterText(string! text, boolean escape=false)
{
    //...
}
```

Now, most of the calls with a wrong type will cause an exception due to the invalid data types passed:

```zephir
$o->filterText(1111, 1); // FAIL
$o->filterText("some text", null); // OK
$o->filterText(null, true); // FAIL
$o->filterText("some text", true); // OK
$o->filterText(array(1, 2, 3), true); // FAIL
```

By specifying what parameters are strict and what must be flexible, a developer can set the specific behavior he/she really wants.

### Return-Type: Void
From now, methods can be marked as ‘void'. This means that a method is not allowed to return any data:

```zephir
public function setConnection( connection) -> void
{
    this->_connection = connection;
}
Why is this useful? Because the compiler can detect if you're expecting a value from these methods and produce a compiler exception:

let myDb = db->setConnection(connection);
myDb->execute("SELECT * FROM robots"); // this will produce an exception
```

### Branch Prediction Hints
Now a developer can specify branch prediction hints. What is branch prediction? Check the Wikipedia article out. In environments where performance is very important, it may be useful to introduce these hints.

Consider the following example:

```zephir
let allPaths = [];
for path in this->_paths {
    if path->isAllowed() == false {
        throw new App\Exception("error!!");
    } else {
        let allPaths[] = path;
    }
}
```

We, as the authors of the above code, know in advance that the condition that throws the exception is unlikely to happen. This means that 99.9% of the time, our method executes that condition, but it is probably never evaluated as true. For the processor, this is hard to know, so we could introduce a hint there:

```zephir
let allPaths = [];
for path in this->_paths {
    if unlikely path->isAllowed() == false {
        throw new App\Exception("error!!");
    } else {
        let allPaths[] = path;
    }
}
```

Check also this article to know more about branch prediction.

This is all for this week. Visit our blog again for more updates!

<3 Zephir Team