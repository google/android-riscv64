# Android/riscv64

## What is this?

If you don't know what Android is, what risc-v is, or what they have to do with one another,
start by reading [Android and RISC-V: What you need to know to be ready](https://opensource.googleblog.com/2023/10/android-and-risc-v-what-you-need-to-know.html).

This github project is solely for issue tracking/discussion/documentation
purposes.

All Android/riscv64 work is being done directly in [AOSP](https://source.android.com/).
Patches should be sent to AOSP using the usual
[AOSP contribution process](https://source.android.com/docs/setup/contribute#contribute-to-the-code)
and *not* as pull requests here.
(This is true even after [Changes to AOSP](https://source.android.com/docs/whatsnew/site-updates#aosp-changes).)

You might also want to subscribe to the
[sig-android mailing list](https://lists.riscv.org/g/sig-android).
(You need to send mail to
[sig-android+subscribe@lists.riscv.org](mailto:sig-android+subscribe@lists.riscv.org)
and then click "Join" on the mailing list web site.) You can see the topics up for discussion --
or add your own -- for the monthly meeting in the
[Android SIG meeting topics](https://docs.google.com/document/d/1fwPYBpA85_gUP4meGKajS1chLhzNJ0dSkGKmmOzTQVE/edit)
doc. But there's no need to wait for the meeting: you can ask questions on the mailing list at any time!

## Status

We're currently (2025Q2) using
[cuttlefish virtual devices](https://source.android.com/docs/setup/create/cuttlefish)
to run
[ART](https://source.android.com/docs/core/runtime)
to boot to the homescreen,
and the usual
[shell and command-line tools](https://android.googlesource.com/platform/system/core/+/main/shell_and_utilities/README.md)
(and all the libraries they rely on) all work.

We have not defined the Android NDK ABI for riscv64 yet, but we're working on it, and it will be added to the
[Android ABIs](https://developer.android.com/ndk/guides/abis)
page (and announced on the SIG mailing list) when it's done.
In the meantime, you can download [the latest NDK](https://developer.android.com/ndk/downloads)
which has provisional support for riscv64.
The ABI it targets is _less than_ what the final ABI will be,
so although code compiled with it will not take full advantage of Android/riscv64 hardware,
it should at least be _compatible_ with those devices.
(Though obviously part of the point of giving early access to it is to try to find any serious mistakes we need to fix,
and those fixes may involve ABI breaks!)

## Can I try it?

Download the source using the usual
[AOSP download process](https://source.android.com/docs/setup/download/downloading)
and then:
```
$ cd aosp
$ source build/envsetup.sh
$ lunch aosp_cf_riscv64_phone-trunk_staging-userdebug

============================================
PLATFORM_VERSION_CODENAME=VanillaIceCream
PLATFORM_VERSION=VanillaIceCream
PRODUCT_INCLUDE_TAGS=com.android.mainline mainline_module_prebuilt_nightly
TARGET_PRODUCT=aosp_cf_riscv64_phone
TARGET_BUILD_VARIANT=userdebug
TARGET_ARCH=riscv64
TARGET_ARCH_VARIANT=riscv64
TARGET_CPU_VARIANT=generic
HOST_OS=linux
HOST_OS_EXTRA=Linux-6.5.13-1rodete2-amd64-x86_64-Debian-GNU/Linux-rodete
HOST_CROSS_OS=linux_musl
BUILD_ID=MAIN
OUT_DIR=out
============================================
$ make -j
```
If you want to check whether a particular directory builds, `cd` into
that directory and use `mm -j`.

(For more tips on building in general, see
[Building Android](https://source.android.com/docs/setup/build/building).)

### Cuttlefish (emulator) setup

To launch cuttlefish, follow the general
[AOSP cuttlefish setup](https://source.android.com/docs/setup/create/cuttlefish-use)
instructions.

Note that you need at least qemu 8.1.
qemu 9.0 has important fixes for the V extension,
and qemu 9.2 has some good speedups for V too.

### Getting to a shell (faster, but no graphics)

After building, run this following command from the same shell:
```
$ launch_cvd -cpus=4 --memory_mb=8192 --gpu_mode=none
```
After about 10s you should be able to use `adb shell` to connect to your riscv64 cuttlefish!

### Getting to the home screen (slower, but with graphics)

After building, run this following command from the same shell:
```
$ launch_cvd -cpus=8 --memory_mb=8192
```
You can then use `vncviewer localhost:6444` to connect to your riscv64 cuttlefish!

(Note that even on a fast Xeon workstation it takes several minutes to get to
the boot animation and ten minutes to get to the home screen!)

## How do I contribute?

Consult the regular AOSP
[Contributing](https://source.android.com/docs/setup/contribute#contribute-to-the-code)
documentation for more information on how to send us your patches.

Note that changes to projects under `external/` (other than to
`Android.bp` files) typically need to go to the upstream open source
project in question first, and will then be merged into AOSP from
there. In many cases, the `METADATA` file will point you to the
upstream source, but feel free to ask here if not!
You can also let us know whenever there's an important or useful update we should take!

## Review our Community Guidelines

This project follows [Google's Open Source Community
Guidelines](https://opensource.google/conduct/).
