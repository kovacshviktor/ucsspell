# ucsspell

**ucsspell** is an experimental, Unicode-extended continuation of the [Hunspell](https://github.com/hunspell/hunspell) project.  
It was created to provide full support for the **Supplementary Multilingual Plane (SMP)** and other Unicode code points beyond the Basic Multilingual Plane (BMP).

## Background

Hunspell was originally designed around UTF-8 text processing, but internally relied on 16-bit character handling, which limits direct support for Unicode characters outside the BMP (e.g. historical scripts and rare symbols).  
To handle modern and historical scripts encoded in the SMP — such as **Old Turkic**, **Old Hungarian**,  and **Old Persian** — an extended Unicode-aware infrastructure became necessary.

The **ucsspell** project introduces this capability while maintaining compatibility with existing Hunspell dictionaries and tools.

## Key Features

- **EXT-UTF-8 encoding mode**  
  A new `.aff` file setting `SET EXT-UTF-8` signals that the engine must operate on full Unicode code points (UTF-32 internally).  
  The legacy `SET UTF-8` mode continues to use the traditional Hunspell logic.

- **ICU integration**  
  The project integrates [ICU4C (International Components for Unicode)](https://github.com/unicode-org/icu) for all Unicode conversions, case-folding, and script-aware operations.  
  This ensures correct handling of surrogate pairs and SMP code points across all supported platforms.

- **Language extension: hu-Hung**  
  Adds `LANG hu-Hung` (or `hu-Hung-HU`) as a new language tag for Old Hungarian.  
  This allows proper distinction between modern Hungarian (`hu-HU`) and its historical orthography.

- **Cross-platform build system**  
  Uses **CMake** for unified builds on Linux, Windows (MSYS2/MinGW, MSVC optional), and macOS.  
  The ICU library is included as a git submodule for reproducible source-based builds.

## Goals

- Provide a clean, SMP-ready Unicode backend for Hunspell.  
- Maintain full compatibility with existing Hunspell dictionaries.  
- Allow historical and non-BMP scripts to be processed without data loss.  
- Serve as a testing ground for future integration into upstream Hunspell and LibreOffice.

## Build Instructions

```bash
git clone https://github.com/<yourname>/ucsspell.git
cd ucsspell
git submodule update --init --recursive
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
