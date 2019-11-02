---
layout: post
title: Zephir 0.12.11 Released
date: 2019-10-19T13:54:00.000Z
tags:
  - release
  - 0.12.x
  - zephir
---
Bug fixes related to stubs and API docs generation as well as working with data types.

### Fixed
- Fixed arithmetical operations with `zvals` which stores `double` numbers
- Fixed updating static variables in the loop which represents  `double` and
  `integer` data types [#1494](https://github.com/phalcon/zephir/issues/1494)
- Fixed casting char into another of a different type
  [#1988](https://github.com/phalcon/zephir/issues/1988)
- Fixed `internal` methods definition when `internal-call-transformation` is enabled
  [#1956](https://github.com/phalcon/zephir/issues/1956)
- Fixed aliases using in the `use` statement when generating stubs
  [#1986](https://github.com/phalcon/zephir/issues/1986)
- Fixed incorrect namespace on type hinted return when generating API docs
  [#1229](https://github.com/phalcon/zephir/issues/1229)
