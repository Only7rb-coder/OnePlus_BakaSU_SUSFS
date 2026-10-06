# OnePlus Kernels with ZSU and SUSFS

A ZSU-only adaptation of [huangdihd/OnePlus_BakaSU_SUSFS](https://github.com/huangdihd/OnePlus_BakaSU_SUSFS), based on release `v2.3.0-r2`. It preserves that project's OnePlus/Oppo/Realme device configurations, kernel-source manifests, build options, SUSFS integration and AnyKernel3 packaging, while changing the kernel root integration to the matching [Only7rb-coder/zsu](https://github.com/Only7rb-coder/zsu) fork.

> **ZSU only:** this repository's build workflow exposes ZSU as its sole root solution. It is intended for the matching ZSU manager (`com.zsu.zsu`), not as a BakaSU or upstream KernelSU build.

## Compatibility and builds

- Device list and supported OS/kernel combinations are in [compatibility.md](compatibility.md) and the JSON profiles in [`configs/`](configs/).
- Build jobs are started from **Actions → Build and Release OnePlus Kernels → Run workflow**.
- Choose the Android/OxygenOS/kernel matrix to build; choose `ZSU` (the only available root option).
- For initial validation, build a single device through `config_path` and keep `make_release` disabled. Only publish and flash builds after the target device has been tested.

The upstream ZSU repository documents Android kernel integration separately; feature availability may vary by kernel branch. Confirm a successful build and manager handshake for each device/profile before treating a ZIP as supported.

## Installation safety

1. Confirm the exact device model, region/variant, and OxygenOS version against the compatibility profile.
2. Unlocking/flashing can erase data or make a device unbootable. Back up data and the original boot image, and retain a tested recovery method.
3. Use Kernel Flasher only with the exact matching ZIP. Do not flash a package intended for another model or kernel branch.
4. Install the matching ZSU manager from its official release page and verify that it recognizes the kernel after reboot.
5. If the device fails to boot or ZSU does not recognize the kernel, restore the backed-up boot image; do not distribute the build as working.

## Features and current limitations

For ZSU builds, SUSFS is deliberately disabled. The reference SUSFS KernelSU patch rewrites the root driver initialization and removes hook declarations that this ZSU fork needs; applying it caused compile failures. A ZSU-specific SUSFS port has not yet been implemented or validated. Other device-profile features (such as optional Baseband Guard, BBR, TTL, IP_SET/IPv6 NAT, Unicode-related patches, LTO, build caching and device tuning) remain subject to the selected kernel profile. Each release must state its exact enabled features.

## Attribution

- Kernel sources and device configurations: OnePlus and the respective device/kernel maintainers.
- Base build workflow and features: [huangdihd/OnePlus_BakaSU_SUSFS](https://github.com/huangdihd/OnePlus_BakaSU_SUSFS), release `v2.3.0-r2`.
- ZSU manager and kernel-side root integration: [Only7rb-coder/zsu](https://github.com/Only7rb-coder/zsu).
- SUSFS: [simonpunk/susfs4ksu](https://gitlab.com/simonpunk/susfs4ksu).

Respect all upstream licenses and retain notices in redistributed source and binaries. This is a community adaptation, not an official release from OnePlus or the upstream project authors.
