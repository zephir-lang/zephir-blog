---
layout: post
title: Zephir 0.12.9 Released
date: 2019-10-14T15:21:59.586Z
tags:
  - zephir
  - 0.12.x
  - release
---
New Zephir released

### Added
- Added a single hyphen version of `dumpversion` option (just `-dumpversion`)
- Added `--vernum` option to print compiler version as integer

### Fixed
- Create local `.zephir` only when necessary
- Fixed IDE stubs generation [#1778](https://github.com/phalcon/zephir/issues/1778)
- Fixed segfault on cast `IS_UNDEF` to array
  [#1941](https://github.com/phalcon/zephir/issues/1941)
- Disables some regression changes introduced in the version `0.12.5`
  [#1941 (comment)](https://github.com/phalcon/zephir/issues/1941#issuecomment-538654340)
- Fixed memory leak on update array [#1937](https://github.com/phalcon/zephir/issues/1937)
- Fixed IDE stubs generation for classes that extends base classes
  [#1907](https://github.com/phalcon/zephir/issues/1907)
- Proper escape slashes in strings [#1495](https://github.com/phalcon/zephir/issues/1495)

### Changed
- Print warning during the code generation if the `timecop` extension was detected
  [#1950](https://github.com/phalcon/zephir/issues/1950)
- Improved error handling to not print stack trace on PHP error `ZEPHIR_DEBUG` is not set

### Removed
- Removed no longer used `zephir_dtor` macro
