---
title: "What's New in Zephir (II)"
date: 2013-09-30 00:00:00
excerpt: Zephir development has been progressing at a steady pace and there are quite a few new things we're going to have a look at today. Getter/Setter shortcuts...
---

Zephir development has been progressing at a steady pace and there are quite a few new things we're going to have a look at today.

### Getter/Setter shortcuts
Like in C#, you can use get/set/toString shortcuts in Zephir, this feature allows to easily write setters and getters for properties without explicitly implementing those methods as such.

For example, without shortcuts we could find code like:

```php
<?php

 class MyClass
 {
    protected $myProperty;

    protected $someProperty = 10;

    public function setMyProperty($myProperty)
    {
        $this->myProperty = $myProperty;
    }

    public function getMyProperty()
    {
        return $this->myProperty;
    }

    public function setSomeProperty($someProperty)
    {
        $this->someProperty = $someProperty;
    }

    public function getSomeProperty()
    {
        return $this->someProperty;
    }

    public function __toString()
    {
        return $this->myProperty;
    }
 }
```

You can write the same code using shortcuts as follows:

```php
namespace App;

class MyClass
{
    protected myProperty {
        set, get, toString
    };

    protected someProperty = 10 {
        set, get
    }

}
```

When the code is compiled those methods are exported as real methods but you don't have to write them one by one.

### Return Type Hints
Now, methods in classes and interfaces can have return type hints, these will provide useful extra information to the compiler to inform you about errors in your application. Consider the following example:

```php
namespace App;

class MyClass
{
    public function getSomeData() -> string
    {
        // this will throw a compiler exception
        // since the returned value (boolean) does not match
        // the expected returned type string
        return false; 
    }

    public function getSomeOther() -> <App\MyInterface>
    {
        // this will throw a compiler exception
        // if the returned object does not implement
        // the expected interface App\MyInterface
        return new App\MyObject;    
    }

    public function process()
    {
        var myObject;

        // the type-hint will tell the compiler that 
        // myObject is an instance of a class
        // that implement App\MyInterface
        let myObject = this->getSomeOther();

        // the compiler will check if App\MyInterface
        // implements a method called "someMethod"
        echo myObject->someMethod();
    }
}
```

That's it for this edition. Don't forget to go read the docs if you want to know more about Zephir and help us improve them :)

Thank you all and see you next time!

<3 Zephir Team