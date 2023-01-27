# Android/riscv64

## What is this?

This github project is solely for issue tracking/discussion/documentation
purposes. All Android/riscv64 work is being done directly in
[AOSP](https://source.android.com/), and patches should be sent
there as usual for AOSP rather than as pull requests.

The [sig-android@lists.riscv.org](https://lists.riscv.org/g/sig-android)
mailing list is also likely of interest.

## Can I try it?

```
$ cd aosp
$ source build/envsetup.sh
$ lunch aosp_riscv64-userdebug

============================================
PLATFORM_VERSION_CODENAME=UpsideDownCake
PLATFORM_VERSION=UpsideDownCake
TARGET_PRODUCT=aosp_riscv64
TARGET_BUILD_VARIANT=userdebug
TARGET_ARCH=riscv64
TARGET_ARCH_VARIANT=riscv64
TARGET_CPU_VARIANT=generic
HOST_OS=linux
HOST_OS_EXTRA=Linux-5.19.11-1rodete1-amd64-x86_64-Debian-GNU/Linux-rodete
HOST_CROSS_OS=windows
BUILD_ID=AOSP.MASTER
OUT_DIR=out
============================================
$ make -j
```

We're currently (2023Q1) still working on cuttlefish and ART, so
for now all you'll have is a shell, command-line tools, and relevant
libraries that you can manually run in qemu.

## How do I contribute?

Consult the regular AOSP
[Contributing](https://source.android.com/docs/setup/contribute#contribute-to-the-code)
documentation for more information on how to send us your patches.

Note that changes to projects under `external/` (other than to
`Android.bp` files) typically need to go to the upstream open source
project in question first, and will then be merged into AOSP from
there. In many cases, the `METADATA` file will point you to the
upstream source, but feel free to ask here if not!

## Review our Community Guidelines

This project follows [Google's Open Source Community
Guidelines](https://opensource.google/conduct/).
