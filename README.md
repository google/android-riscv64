# Android/riscv64

## What is this?

This github project is solely for issue tracking/discussion/documentation
purposes.

All Android/riscv64 work is being done directly in [AOSP](https://source.android.com/).
Patches should be sent to AOSP using the usual
[AOSP contribution process](https://source.android.com/docs/setup/contribute#contribute-to-the-code)
and *not* as pull requests here.

You might also want to subscribe to the
[sig-android@lists.riscv.org](https://lists.riscv.org/g/sig-android)
mailing list. (You need to send mail to
[sig-android+subscribe@lists.riscv.org](mailto:sig-android+subscribe@lists.riscv.org))
and then click "Join" on the mailing list web site.)

## Status

We're currently (2023Q1) still working on
[cuttlefish virtual devices](https://source.android.com/docs/setup/create/cuttlefish)
and
[ART](https://source.android.com/docs/core/runtime),
so for now all you'll have is a
[shell and command-line tools](https://android.googlesource.com/platform/system/core/+/master/shell_and_utilities/README.md),
and all the libraries they rely on. Until we have cuttlefish working you'll have to manually
run them in qemu or on your own hardware.

You can see the current status of the
riscv64 build in the `aosp_riscv64` column of
[ci.android.com](https://ci.android.com/builds/branches/aosp-master/grid?).

## Can I try it?

Download the source using the usual
[AOSP download process](https://source.android.com/docs/setup/download/downloading)
and then:
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
If you want to check whether a particular directory builds, `cd` into
that directory and use `mm -j`.

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
