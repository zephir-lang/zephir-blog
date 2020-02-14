---
layout: post
title: Zephir 0.12.17 Released
date: 2020-02-14T11:52:49.206Z
tags:
  - zephir
  - 0.12.x release
---
Fixes related to character conversion in `filer.c`.

### Fixed
- On some platforms special alpha characters aren't correctly escaped
  [#2058](https://github.com/phalcon/zephir/pull/2058)

### Changed
- Changed the internal DI environment mode when compile PHAR
  [#2049](https://github.com/phalcon/zephir/pull/2049)
