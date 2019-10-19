---
layout: post
title: Zephir 0.12.10 Released
date: 2019-10-19T13:54:00.000Z
tags:
  - release
  - 0.12.x
  - zephir
---
Bug fixes related to Super Global usage.

### Fixed
- Fixed incorrect behavior in `zephir_get_global` if `zval` reference count <= 1 [#1961](https://github.com/phalcon/zephir/issues/1961)

### Removed
- Removed `--vernum` option from the help for regular commands
- Removed `void` from the return type hint in the generated stubs
  [#1977](https://github.com/phalcon/zephir/issues/1977)
- Remove no longer supported `TSRMLS_CC` usage
  [#1865](https://github.com/phalcon/zephir/issues/1865)

### Changed
- Disabled PHP warnings for PHP >= 7.3.0 to be able correct work with lowest versions of dependencies
  [zendframework/zend-code#160](https://github.com/zendframework/zend-code/issues/160)
- Introduced support of multiline `@param` body for generated stubs
  [#1968](https://github.com/phalcon/zephir/issues/1968)
