---
layout: post
title: Zephir 0.12.1 Released
date: 2019-07-30T20:08:00.000Z
tags:
  - zephir
  - 0.12.1
  - release
---
New Zephir released

## Changelog
### Added
- Added initial bash completion support (see `zephir-autocomplete` file)

### Changed
- Use local memory management
  [#1859](https://github.com/phalcon/zephir/pull/1859),
  [#1880](https://github.com/phalcon/zephir/pull/1880)
- Rephrase help strings for common compiler options

### Removed
- Remove HAVE_SPL usage
  [phalcon/cphalcon#14215](https://github.com/phalcon/cphalcon/pull/14215)
- Remove not used redundant command line options
- Cleaning up redundant CLI options

### Fixed
- Fixed segfault when auto-loading class with syntax error
  [#1885](https://github.com/phalcon/zephir/issues/1885)
- Optimize memory usage [#1882](https://github.com/phalcon/zephir/pull/1882)
- Fixed modifying array values in loops
  [#1879](https://github.com/phalcon/zephir/issues/1879)

Big thank you to all of our contributors

<3 Zephir Team
