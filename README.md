# KernelSU - Samsung late-load fork

**This fork ships the vanilla KernelSU app and kernel module, unchanged from upstream, with exactly one addition: Samsung late-load support.** No extra patches, no behavior changes, no rebranding. The only other difference is that the app's update checker points at this fork's releases, so an update can never install an upstream build that lacks Samsung support.

## What this is

KernelSU is a kernel-based root solution for Android. Samsung's stock kernels are protected (RKP/DEFEX/KDP), so KernelSU cannot be integrated the usual way on those devices. This fork tracks upstream KernelSU and adds support for late-loading the KernelSU kernel module at runtime on Samsung devices, through DFRoot. The Samsung support is a port of diabl0w's pull request to upstream (tiann/KernelSU#3899).

One build targets all supported Samsung devices: device and kernel differences are detected at runtime, not at build time.

## Who this is for

Samsung Galaxy devices running the stock Samsung kernel (One UI), using DFRoot as the entry point. If your device is not a Samsung, or already runs regular KernelSU, use upstream KernelSU instead.

## Status: test builds

**These are experimental test builds.** Rooting through an exploit plus a late-loaded kernel module can crash or bootloop your phone. Before you start:

- Keep a full backup and the stock firmware for your exact model.
- Know how to recover with Odin.
- Expect that a bad run can force a reboot or a reflash.

You use this at your own risk. This fork is not affiliated with or endorsed by upstream KernelSU. Please do not report issues with this fork to the upstream project.

## Install

1. Download the manager APK from this repo's [Releases](../../releases) (or a CI artifact for test builds).
2. Get [DFRoot](https://github.com/diabl0w/DFRoot) and follow its instructions. DFRoot handles the exploit and late-loads KernelSU.
3. Recommended DFRoot settings for a first run: **Start on Boot OFF**, **Disable KSU Modules ON**, and do a normal reboot before running.

## Updating

The manager's update checker reads this fork's releases. Release APKs are signed with a persistent release key, so a new release installs over the previous one as a normal update. CI and pull-request test builds use throwaway keys, so those must be uninstalled before installing a different build.

## Building and releases

Pushing to `main` builds the manager APK in CI signed with the release key. Tagging `v*` cuts a GitHub release with the signed manager APK attached. Pull requests build with a temporary key for testing.

## Credits

- [tiann](https://github.com/tiann) and the [KernelSU](https://github.com/tiann/KernelSU) contributors, for upstream KernelSU. Almost everything in this repo is their work.
- [diabl0w](https://github.com/diabl0w), for the Samsung late-load patch ([tiann/KernelSU#3899](https://github.com/tiann/KernelSU/pull/3899)) and for [DFRoot](https://github.com/diabl0w/DFRoot).
- [backslashxx](https://github.com/backslashxx), whose earlier Samsung KernelSU fork ([tests/samsung](https://github.com/backslashxx/KernelSU/tree/tests/samsung)) proved and informed this approach.

## License

Same as upstream: GPL-3.0 for the project (see [LICENSE](LICENSE)), GPL-2.0 for the kernel code under [kernel/](kernel/LICENSE).
