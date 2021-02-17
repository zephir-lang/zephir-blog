---
layout: post
title: Zephir 0.12.19 Released
date: 2020-05-13T10:10:46.636Z
tags:
  - zephir
  - 0.12.x
  - release
---
Fixed scope related issues and improved stubs generation.

### Fixed
- Fixed duplicate definition with GCC 10
  [ice/framework#266](https://github.com/ice/framework/pull/266)
- Fixed initialization of object properties with default values when
  the object is an instance of a child class
  [#2089](https://github.com/zephir-lang/zephir/issues/2089)

### Changed
- Improved stubs generation for methods which may return object or null
  [#2092](https://github.com/zephir-lang/zephir/issues/2092)