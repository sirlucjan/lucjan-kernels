# My own kernels. Use at your own risk.
###### Dell Inspiron 15-3542 (3542-2538) with Fourth Gen Intel Core i3/i5/i7 optimized.
###### linux-lucjan varies considerably from stock kernel. 
***
###### linux-lucjan incorporates:

* [bfq improvements](https://groups.google.com/forum/#!forum/bfq-iosched) - latest fixes authored by Paolo Valente and BFQ Team

* [bfq-dev](https://github.com/Algodev-github/bfq-mq/tree/dev-bfq-on-5.6) - latest fixes authored by Paolo Valente and BFQ Team

* [bfq-dev-lucjan](https://github.com/sirlucjan/bfq-mq-lucjan/tree/dev-bfq-on-5.6-lucjan) - latest fixes authored by Paolo Valente and BFQ Team and forked by Piotr Gorski

* [bfq-dev-lucjan-rc](https://github.com/sirlucjan/kernel-patches/tree/master/5.8/bfq-dev-lucjan) / [bfq-dev-lucjan-rc](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.8/bfq-dev-lucjan) - specific patches authored by Paolo Valente and Piotr Gorski

* [graysky's GCC patch](https://github.com/graysky2/kernel_gcc_patch) - version for gcc 10.1

* [Project C](https://gitlab.com/alfredchen/linux-prjc/tree/linux-5.8.y-prjc) / [Project C blog](http://cchalpha.blogspot.com) - contains the newest vesion with latest fixes

* [random fixes from zen-kernel](https://github.com/zen-kernel/zen-kernel/tree/5.8/master) - specific patches authored by Jan Alexander Steffens and ZEN Kernel Team

* [random fixes from pfkernel](https://github.com/pfactum/pf-kernel/tree/pf-5.8) / [random fixes from pfkernel](https://gitlab.com/post-factum/pf-kernel/tree/pf-5.8) - for example patches from Arch Linux or specific patches authored by Oleksandr Natalenko

* [fixes from ClearLinux](https://github.com/clearlinux-pkgs/linux) - specific patches authored by ClearLinux Team

* [UKSM (sources)](https://github.com/dolohow/uksm) / [UKSM (info)](https://www.usenix.org/sites/default/files/conference/protected-files/fast18_slides_xia.pdf) - resync from dolohow’s github

* [LL-patches](https://github.com/sirlucjan/kernel-patches/tree/master/5.8/ll-patches) / [LL-patches](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.8/ll-patches) - specific patches authored by Piotr Gorski

* [LL-branding](https://github.com/sirlucjan/kernel-patches/tree/master/5.8/ll-branding) / [LL-branding](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.8/ll-branding) - specific patches authored by Piotr Gorski

***

###### Some patches for BFQ conflict with patches for BFQ-dev.

###### To use lucjan-kernels smoothly apply bfq-reverts before linux-lucjan patch. Otherwise the kernel will not compile.

* [bfq-reverts](https://github.com/sirlucjan/kernel-patches/tree/master/5.8/bfq-reverts) / [bfq-reverts](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.8/bfq-reverts) - specific patches authored by Piotr Gorski

***
# Download:

```
git clone https://github.com/sirlucjan/lucjan-kernels.git

```

or

```
git clone https://gitlab.com/sirlucjan/lucjan-kernels.git

```

# Install:


### Testing

```
cd /some_path/lucjan-kernels/lucjan-kernels-testing/package_name
makepkg -srci

```

### Unstable

```
cd /some_path/lucjan-kernels/lucjan-kernels-unstable/package_name
makepkg -srci

```
***
# Enable bfq

~~For now, you can use `sudo tee /sys/block/sda/queue/scheduler <<< bfq` to enable "bfq".~~

~~You can also add this to file `60-schedulers.rules`:~~

```
# Non-rotational disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="bfq"
# Rotational disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="bfq"
```

~~and run a command `sudo udevadm control --reload && sudo udevadm trigger`~~

For now, bfq is enabled by default! [(since 5.0-lucjan-ll1-rc1.patch and LL-elevator-set-default-scheduler-to-bfq-for-blk-mq.patch)](https://github.com/sirlucjan/kernel-patches/blob/master/5.0/ll-patches/0002-LL-elevator-set-default-scheduler-to-bfq-for-blk-mq.patch)


***
# You've been warned.
