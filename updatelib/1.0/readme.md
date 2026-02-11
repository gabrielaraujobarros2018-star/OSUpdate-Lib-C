# OSUPDATElib.c – Lumen OS A/B Update Library

**OSUPDATElib** is a compact but fully featured update library for ARMv7‑A (e.g. Motorola Nexus 6) and the Lumen OS ecosystem. It provides modules for update‑checking, secure crypto‑signed downloads, A/B rollback, upcoming and delta‑optimized updates, background / deferred install, and telemetry.

---

## Features

- **Update checking**:  
  HTTP‑based check that respects device policy (WiFi‑only, battery level, time‑between‑checks).

- **Cryptographic engine**:  
  SHA‑256, RSA‑2048 and ECDSA‑P256 for signature and hash verification, integrating NEON‑optimized operations on ARMv7‑A.

- **Rollback system**:  
  Dual‑slot A/B design with automatic rollback on boot failure and manual rollback API.

- **Battery & thermal manager**:  
  Monitors battery percentage, temperature, and charging status; pauses or aborts updates if the device is too hot or too low on power.

- **Configuration engine**:  
  Persistent JSON‑style config for: automatic download, auto‑install, check intervals, minimum battery, WiFi‑only, and update channels.

- **Delta / patching engine**:  
  Uses `bsdiff`‑style delta format with streaming decompression and in‑memory patching, greatly reducing downloaded data size.

- **User notification system**:  
  Progress and action‑ready notifications (install / postpone / cancel) with live progress bars and proper Android notification semantics.

- **Installer & apply engine**:  
  Multi‑stage, mount‑and‑remount safe upgrader that brings Lumen from an old image to a new one, including support for A/B slots.

- **Telemetry & analytics**:  
  Event‑based upload of telemetry, including update checks, download/install outcomes, and rollback incidents, with optional opt‑in consent.

- **A/B testing and canary engine**:  
  Canary rollout with nested stages (e.g. 1%, 10%, 50%, 100%) and automatic rollback if crash rates exceed defined thresholds.

- **Multi‑partition orchestrator**:  
  Handles modern A‑only / A/B layout (`system_a/b`, `vendor_a/b`, `boot_a/b`, etc.) with dependency chaining and sparse‑image processing.

- **Deferred & background installer**:  
  Install only when the device is idle, on battery (but above threshold), on charger, and on sufficient free storage, in small slices that survive reboots.

- **Complete build system**:  
  Shipping ready `Makefile` and `CMakeLists.txt` plus Android NDK / AOSP‑style build hooks (`android.mk` / `Android.bp`).

---

## Build Instructions

### Quick Production Build

```bash
sudo apt install gcc-arm-linux-gnueabi binutils-arm-linux-gnueabi
make -j$(nproc)
sudo make install
