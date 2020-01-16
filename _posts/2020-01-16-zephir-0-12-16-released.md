---
layout: post
title: Zephir 0.12.16 Released
date: 2020-01-16T19:30:00.000Z
tags:
  - zephir
  - 0.12.x
  - release
---
Fixes related to project configuration, internal cache as well as IDE stubs.
﻿
### Fixed
- Do not dump config file if config was changed. Usually we need dump configuration exactly once - at project initialization. There are no needs to dump it for every config change. Also, this patch removes `Config::$changed` variable that is no longer needed [#2035](https://github.com/phalcon/zephir/pull/2035)
- Use a different path for the Kernel cache if possible. This patch fixes a cache collision issue. The issue is after creating the cache and filling it with a project-specific configuration, there is no way to invalidate it. Any next project will use the same Kernel cache and the same Kernel configuration (if any) [#2036](https://github.com/phalcon/zephir/pull/2036)
- Fixed `-V` CLI flag purpose. Initially it was designed to disable verbose mode on the fly, e.g. to override project configuration for a single Zephir pass. This behavior was returned back.
- Fix increment array elements operation [#2020](https://github.com/phalcon/zephir/issues/2020)
- Fixed compound addition and subtraction assignment operators for static properties [#2038](https://github.com/phalcon/zephir/issues/2038)
