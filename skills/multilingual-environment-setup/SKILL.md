---
name: multilingual-environment-setup
description: "Bootstraps isolated conda and python virtual environments across diverse project dependencies."
---

# Multilingual Environment Setup

## Overview
The `multilingual-environment-setup` skill configures isolated execution environments for heterogeneous open-source repositories, resolving native dependencies and package version conflicts.

## Environment Protocol
- Detect whether the repository relies on Conda, Poetry, Pipenv, or uv.
- Bootstrap exact Python versions and C-extension build dependencies.
- Verify environment readiness prior to running reproduction scripts.
