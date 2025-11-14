# ucsspell

**Kísérleti projekt a Hunspell továbbfejlesztésére.**  
Az ucsspell célja a Hunspell Unicode-támogatásának kiterjesztése, különösen a **Supplementary Multilingual Plane (SMP)** karaktertartományra, hogy olyan történelmi írásokat is kezelhessen, mint az **Old Hungarian**, az **Old Turkic** és az **Old Persian**.  
A fejlesztés eredményei később a Hunspell főágába kerülnek be.

_For English readers → scroll down._

---

**ucsspell** is an experimental, Unicode-extended continuation of the [Hunspell](https://github.com/hunspell/hunspell) project.  
It was created to provide full support for the **Supplementary Multilingual Plane (SMP)** and other Unicode code points beyond the Basic Multilingual Plane (BMP).

## Background

Hunspell was originally designed around UTF-8 text processing, but internally relied on 16-bit character handling, which limits direct support for Unicode characters outside the BMP (e.g. historical scripts and rare symbols).  
To handle modern and historical scripts encoded in the SMP — such as **Old Hungarian**, **Old Turkic**, and **Old Persian** — an extended Unicode-aware infrastructure became necessary.

The **ucsspell** project introduces this capability while maintaining compatibility with existing Hunspell dictionaries and tools.

## Key Features

- **EXT-UTF-8 encoding mode**  
  A new `.aff` file setting `SET EXT-UTF-8` signals that the engine must operate on full Unicode code points (UTF-32 internally).  
  The legacy `SET UTF-8` mode continues to use the traditional Hunspell logic.

- **ICU integration**  
  The project integrates [ICU4C (International Components for Unicode)](https://github.com/unicode-org/icu) for all Unicode conversions, case-folding, and script-aware operations.  
  This ensures correct handling of surrogate pairs and SMP code points across all supported platforms.

### Cloning with ICU submodule (recommended with verbose mode)

The ICU submodule is large, so it is recommended to fetch it in verbose mode
to see download progress:

git clone --recurse-submodules --progress https://github.com/kovacshviktor/ucsspell
cd ucsspell
git submodule update --init --recursive --progress


- **Language extension: hu-Hung**  
  Adds `LANG hu-Hung` (or `hu-Hung-HU`) as a new language tag for Old Hungarian.  
  This allows proper distinction between modern Hungarian (`hu-HU`) and its historical orthography.

- ## Build systems

This project currently supports two build systems:

- **Autotools + Make** (recommended on Linux and macOS)
- **CMake** (recommended on Windows, optional on other platforms)

The ICU library is included as a git submodule for reproducible source-based builds.

### 1. Autotools build (Linux, macOS)

./autogen.sh       # or: autoreconf -vfi
./configure
make -j$(nproc)
sudo make install   # optional


## Goals

- Provide a clean, SMP-ready Unicode backend for Hunspell.  
- Maintain full compatibility with existing Hunspell dictionaries.  
- Allow historical and non-BMP scripts to be processed without data loss.  
- Serve as a testing ground for future integration into upstream Hunspell and LibreOffice.

## Experimental Status

This is a **public experimental project**.  
All new Unicode and ICU-based features are being developed and tested here first.  
After validation and community review, these improvements are planned to be integrated into the main [Hunspell](https://github.com/hunspell/hunspell) project.

