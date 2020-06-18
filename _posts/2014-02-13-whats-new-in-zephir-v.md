---
layout: post
title: What's New in Zephir (V)
date: 2014-02-13 00:00:00
tags:
  - zephir
---

These last weeks a lot of bugs have been fixed and new exciting features have been added to Zephir. Additionally, the core has been improved by adding namespaces, an autoloader, composer support and adopting PSR2 as coding standard. Main features added are highlighted as follows:

### Parameters by Name
We have recently begun to implement parameters by name or keyword arguments. Check the description from Wikipedia out:

In computer programming, named parameters, pass-by-name, or keyword arguments refer to a computer language's support for function calls that clearly state the name of each parameter within the function call itself.

Named parameters can be useful if you want to pass parameters in an arbitrary order, document the meaning of parameters or specify parameters in a more elegant way.

Consider the following example, a class called “Image” has a method that receive four parameters:

```zep
class Image
{
 public function chop(width=600, height=400, x=0, y=0)
 {
   //...
 }
}
```

Using the standard way of calling methods:

```zep
i->chop(100); // width=100, height=400, x=0, y=0
i->chop(100, 50, 10, 20); // width=100, height=50, x=10, y=20
```

Using named parameters you can:

```zep
i->chop(width: 100); // width=100, height=400, x=0, y=0
i->chop(height: 200); // width=600, height=200, x=0, y=0
i->chop(height: 200, width: 100); // width=100, height=200, x=0, y=0
i->chop(x: 20, y: 30); // width=600, height=400, x=20, y=30
```

Do parameters by name make my extension slower?. This depends on how much information the compiler has on the method that is being called.

When the compiler has accurate knowledge of the class and method being called it simply check the parameters and orders them as they're expected:

```zep
let i = new Image();
i->chop(y:30, x: 20); // chop(null, null, 20, 30);
```

When the compiler (at compile time) does not know the correct order of these parameters they must be resolved at runtime, in this case there could be a minimum additional overhead:

```zep
let i = new {someClass}();
i->chop(y:30, x: 20);
```

### Read-Only Parameters
Knowing in advance that parameters of a method will not be mutated (modifed) inside it offers advantages for the developer and the compiler. A developer can control that specific parameters will be not modified by mistake when this is not expected, see const correctness. Moreover, the compiler may in some cases generate more efficient code if it knows the value of a parameter is constant or inmutable:

```zep
class Utils
{
 public function checkSum(const string! str)
 {
   char ch; int sum = 0;
   for ch in str { sum += ch->toInt(); }
   return sum;
 }
}
```

### Static Analysis
Another feature we are implementing is static analysis on conditional assignments. The idea is to help the developer to find potential problems and avoid unexpected behaviors.

```zep
class Utils
{
	public function someMethod(b)
	{
		string a; char c;

		if b == 10 {
			let a = "hello";
		}
	
		// a could be unitialized here
		for c in a {
			echo c, PHP_EOL;
		}
	}
}
```

The above example illustrates a common situation. The variable `a` is assigned only when `b` is equal to 10, then it's required to use the value of this variable but it could be uninitialized. Zephir detects this and automatically initializes the variable to an empty string and generates a warning alerting the developer:

```sh
Warning: Variable 'a' was assigned for the first time in conditional branch,
 consider initialize it in its declaration in 
/home/scott/test/test/utils.zep on 21 [conditional-initialization]

     for c in a {
```

Finding such errors is sometimes tricky, however to the extent that static analysis can be improved, it will help the programmer to find bugs in advance.

That's all for now. See you soon!


<3 Zephir Team