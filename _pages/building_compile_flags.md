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

The build system is CMake and thus the compile flags can be used via Cmake switches.

## The compile flags

The compile flags

| Flag         | Cmake switch   |  Description |
| -------------- | -------------- |--------------|
| OC_OSCOR       | OC_OSCORE_ENABLED | enable/disable OSCORE security |
| OC_SPAKE       | OC_OSCORE_ENABLED | enable/disable SPAKE (master secret) handshake |
| OC_DEBUG       | OC_DEBUG_ENABLED | exhaustive DEBUG info |
| OC_PUBLISHER_TABLE | - | enable PUBLISHER table (optional feature) |
| OC_GM_TABLE  | - | enable gm (gateway) table (optional feature) |
