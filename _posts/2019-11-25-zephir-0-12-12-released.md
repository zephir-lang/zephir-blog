---
layout: post
title: Zephir 0.12.12 Released
date: 2019-11-25T06:12:44.495Z
tags:
  - release
  - 0.12.x
  - zephir
---
Fixes related to internal call transformations as well as stubs generation.

### Added
- Option to set banner for stubs generator
  [#1987](https://github.com/phalcon/zephir/1987)

### Fixed
- Calling object methods from static context yields segmentation fault when
  `internal-call-transformation` is set to `TRUE`
  [#2000](https://github.com/phalcon/zephir/issues/2000)
- Certain method calls fail when called from static context when
  `internal-call-transformation` is set to `TRUE`
  [#2005](https://github.com/phalcon/zephir/issues/2005)
- Method context loses track of `this` after calling static method when
  `internal-call-transformation` is set to `TRUE`
  [#2007](https://github.com/phalcon/zephir/issues/2007)
- Fixed incorrect stubs generation for return type hint
  [#1990](https://github.com/phalcon/zephir/issues/1990)
- Fixed incorrect stubs generation for classes in the same namespace
  [#2016](https://github.com/phalcon/zephir/issues/2016)
