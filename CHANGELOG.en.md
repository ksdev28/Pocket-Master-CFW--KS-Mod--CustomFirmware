# Changelog — Pocket Master CFW 1.0.2 (KS Mod)

[Português](CHANGELOG.md) | **English**

All notable changes applied on top of **Pocket Master CFW 1.0.2 (1.3.3)** are listed below.

---

## [1.0.2-KSMod]

### Added (Firmware)
* **`Tone Hammer`** (`AMP`): Aguilar® Tone Hammer®-inspired bass preamp/DI with 3-band EQ, sweepable `MidFreq`, extended `VOL` headroom, and `AGS` toggle.
* **`Ages OD`** (`DRV`): 5-mode bass overdrive (`1–5`) with parallel `Dry` blend, `Bass`, and `Treble`.
* **`OC-2 Oct`** (`FX1` & `FX2`): Boss® OC-2®-style analog sub-octave divider with `Oct1` (-1 Oct), `Dry`, and `Oct2` (-2 Oct).
* **`J-60 Chorus`** (`FX1` & `FX2`): Roland® Juno-60®-inspired stereo chorus with `I` and `II` mode switches, `Mix`, `Tone`, and `VOL`.
* **`MicroSynth`** (`FX2`): EHX® Bass Micro Synthesizer®-inspired bass synth with `Sub`, `Dry`, `Octave`, `Square`, and swept resonant filter (`Reso`, `Start`, `Stop`, `Rate`).
* **Custom boot animation:** updated `KS Mod` startup screen.

### Improvements & Fixes
* **Performance optimization:** DSP execution tuned across all 5 modules to keep CPU usage low and stable even with the full chain active.
* **`OC-2 Oct` fix:** fixed octave divider initialization so `Oct1` and `Oct2` process properly alongside `Dry`.
* **`MicroSynth` fix:** fixed filter trigger and sweep state initialization.

### Windows Editor (`SonicakeCFW-Setup-1.0.2-KSMod.exe`)
* Full support for all 5 new modules (names, controls, descriptions, and USB/SysEx parameter updates).
* Updated origin badge to `KSM`.
* Removed `"This file is not a published release: flash it only if you know where it comes from."` and `" (not a published release)"` notices when selecting `.bin` files.
