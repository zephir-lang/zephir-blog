---
layout: post
title: Zephir 0.12.2 Released
date: 2019-08-05T13:54:00.000Z
tags:
  - zephir
  - 0.12.x
  - release
---
Provide an ability to declare module dependencies.

### Added
- Introduced initial ability to generate `zend_module_deps`
  [#1900](https://github.com/phalcon/zephir/pull/1900),
  [phalcon/cphalcon#13702](https://github.com/phalcon/cphalcon/issues/13702),
  [phalcon/cphalcon#13794](https://github.com/phalcon/cphalcon/pull/13794)

### Changed
- Write compiler errors to stderr if available
