---
layout: post
title: "Installing & Testing Zephir on Vagrant"
date: 2014-01-18 00:00:00
excerpt: Vagrant is an excellent tool you can use to create and deploy a linux-based development environment for your applications. In this tutorial, we are going to explain how to set it up for Zephir.
---

[Vagrant](https://www.vagrantup.com) is an excellent tool you can use to create and deploy a linux-based development environment for your applications. In this tutorial, we are going to explain how to set it up for Zephir.

### Setting up Vagrant
First of all you need Vagrant installed on your machine, this should be possible without major complications, in any case, check its documentation out if you fall in any trouble.

Once you have vagrant installed, a virtual machine can be installed this way:

```sh
$ vagrant init precise32 http://files.vagrantup.com/precise32.box 
$ vagrant up 
$ vagrant ssh
```

After this, you'll have a fully running Ubuntu (Precise Pangolin) linux. Now, you must be able to work inside an isolated development environment you can play with.

### Required Packages
The following packages are needed to be installed in order to use Zephir.

```sh
$ sudo apt-get update
$ sudo apt-get install git gcc make re2c php5 php5-dev libpcre3-dev 
```

If you are working on any other debian-based distribution these instructions also might be useful.

### Installing Zephir
Clone the repository and run the installer is enough to get Zephir running:

```sh
$ git clone https://github.com/phalcon/zephir
$ cd zephir
$ ./install -c
$ cd .. 
```

### Testing Zephir
Now, we can create an skeleton for a simple extension:

```sh
 $ zephir init utils 
```

The following files are created:

```sh
$ ls utils/
config.json ext utils
```

Note that a directory called `utils` is created inside the skeleton directory also called `utils`. This subdirectory is used to place the Zephir code. Now, let's create a simple class to test our extension:

```zep
// utils/utils/math.zep 

namespace Utils; 

class Math
{
	public static function sum(int a, int b) {
		return a + b;
	}
}
```

Enter the extension directory and compile the code:

```sh
$ cd utils
$ zephir build
```sh

Edit the php.ini (`/etc/php5/cli/php.ini`) and append

```sh
extension=utils.so
```

Create a file `test.php` with the following to test the extension:

```php
<?php echo Utils\Math::sum(100, 200), "\n";
```

If everything goes well you must see the following:

```sh
 $ php test.php
300
```

### Conclusion
It's easy to test Zephir in a Vagrant Box. Check the Zephir documentation to know what more is this language capable of.


<3 Zephir Team