---
layout: post
title: Zephir 0.12.18 Released
date: 2020-04-24T22:24:39.015Z
tags:
  - zephir
  - 0.12.x
  - release
---
Fixed scope related issues.

### Fixed
- In some cases for C "control characters" aren't properly escaped
  [#2065](https://github.com/phalcon/zephir/issues/2065)
- Zephir ignored property visibility and has not thrown error when setting
  private/protected properties in scope that shouldn't intended for it
  [#2078](https://github.com/phalcon/zephir/pull/2078),
  [phalcon/cphalcon#14810](https://github.com/phalcon/cphalcon/issues/14810),
  [phalcon/cphalcon#14766](https://github.com/phalcon/cphalcon/issues/14766)

