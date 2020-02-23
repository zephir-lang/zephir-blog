---
layout: post
title: "What's New in Zephir (IV)"
date: 2014-01-24 00:00:00
tags:
  - zephir
---

This is our first post from the `What's New in Zephir` series after Zephir v0.3.0 was released and we have great improvements to share with you.

### Bitwise operators
Rack Lin has implemented bitwise operators in Zephir allowing evaluation and manipulation of specific bits within an integer:

```zep
class Unicode
{
    public function ord(string! c)
    {
        uchar ch;

        let ch = c[0];

        if ch <= 0x7F {
            return ch;
        }

        if ch < 0xC2 {
            return false;
        }

        if ch <= 0xDF {
            return (ch & 0x1F) << 6  | (c[1] & 0x3F);
        }

        if ch <= 0xEF {
            return (ch & 0x0F) << 12 | (c[1] & 0x3F) << 6  | 
                    (c[2] & 0x3F);
        }

        if ch <= 0xF4 {
            return (ch & 0x0F) << 18 | (c[1] & 0x3F) << 12 | 
                    (c[2] & 0x3F) << 6 | (c[3] & 0x3F);
        }

        return false;
    }
}
```

Bitwise operations are incredibly simple and thus usually faster than common arithmetic operations.

### Built-In methods for Static Types
In Zephir, we have been always promoting object-oriented programming instead of procedural programming. Previously, static types in Zephir were not encapsulating any kind of functionality associated to its type, therefore it was necessary to use procedural functions to manipulate or use these types:

```zep
class MyClass
{
    public function getLength(string! someStr)
    {
        return strlen(someStr);
    }
}
```

Now, you can just invoke a similar method directly from the static-typed variable:

```zep
class MyClass
{
    public function getLength(string! someStr)
    {
        return someStr->length();
    }
}
```

Compare these two methods:

```zep
public function binaryTohex(string! s) -> string
{
    var o = "", n; char ch;

    for ch in range(0, strlen(s)) {
        let n = sprintf("%X", ch);
        if strlen(n) < 2 {
            let o .= "0" . n;
        } else {
            let o .= n;
        }
    }
    return o;
}
```

And:

```zep
public function binaryTohex(string! s) -> string
{
    var o = "", n; char ch;

    for ch in range(0, s->length()) {
        let n = ch->toHex();
        if n->length() < 2 {
            let o .= "0" . n;
        } else {
            let o .= n;
        }
    }
    return o;
}
```

They both have the same functionality, but the second one uses object-oriented programming.

### Thanks
Special thanks to [Dmitry Patsura](https://github.com/ovr) for contributing fixes and improvements to Zephir as well to all contributors.

Thank you all and see you next time!


<3 Zephir Team