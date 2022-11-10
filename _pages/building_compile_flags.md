---
layout: single
title: Building Compile Flags
overview: true
permalink: /building_compile_flags/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## Introduction

This page describes the compile flags.

The build system being used is CMake, and thus the compile flags are made available as CMake cache variables, which can be enabled or disabled using the CMake GUI on Windows, or by typing the command the following command in the build directory on Linux:

```bash
ccmake .
```

## The compile flags

| Flag         | Cmake switch   |  Description |
| -------------- | -------------- |--------------|
| OC_DNS_SD      | OC_DNS_SD_ENABLED | enable/disable DNS-SD |
| OC_OSCORE      | OC_OSCORE_ENABLED | enable/disable OSCORE security |
| OC_SPAKE       | OC_OSCORE_ENABLED | enable/disable SPAKE (master secret) handshake |
| OC_DEBUG       | OC_DEBUG_ENABLED | exhaustive DEBUG info |
| OC_PUBLISHER_TABLE | - | enable PUBLISHER table (optional feature) |
| OC_GM_TABLE  | - | enable gm (gateway) table (optional feature) |
