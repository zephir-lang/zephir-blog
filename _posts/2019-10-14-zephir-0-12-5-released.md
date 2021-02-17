---
layout: post
title: Zephir 0.12.5 Released
date: 2019-10-02T15:54:35.976Z
tags:
  - zephir
  - 0.12.x
  - release
---
Bug fixes in the Super Globals area usage.

### Changed
- Update `zend_update_static_property` to be compatible with PHP >= 7.3
  [#1904](https://github.com/zephir-lang/zephir/issues/1904)
- Improved error handling

### Fixed
- Fixed IDE stubs generation to properly generate return type hint for `var | null`
  [#1922](https://github.com/zephir-lang/zephir/issues/1922)
- Fixed updating Super Globals [#1917](https://github.com/zephir-lang/zephir/issues/1917)
- Fixed casting variables to array [#1923](https://github.com/zephir-lang/zephir/issues/1923)
- Fixed work with constant which are not present
  [#1928](https://github.com/zephir-lang/zephir/issues/1928)
- Fixed access to Super Globals
  [#1934](https://github.com/zephir-lang/zephir/issues/1934),
  [phalcon/cphalcon#14426](https://github.com/phalcon/cphalcon/issues/14426)
