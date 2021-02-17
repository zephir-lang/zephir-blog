---
layout: post
title: Zephir 0.12.8 Released
date: 2019-10-03T17:34:00.000Z
tags:
  - zephir
  - 0.12.x
  - release
---

A small release with patches for annoying issues.

### Fixed
- Fixed `zephir_preg_match` to use `ZVAL_NULL` instead of `ZEPHIR_NULL`
  [#1946](https://github.com/zephir-lang/zephir/issues/1946)
- Fixed `Extension\InternalClassesTest` test to be able run full test suite
  without Phalcon [#1949](https://github.com/zephir-lang/zephir/issues/1949)
