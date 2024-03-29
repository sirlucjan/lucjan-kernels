# My own kernels. Use at your own risk.
###### HP 850 G3 with Sixth Gen Intel Core i3/i5/i7 optimized.
###### linux-lucjan varies considerably from stock kernel. 
***

# As of July 19, 2022, the project will cease to be developed. Thank you to all users for their willingness to use the project and bug reports.
# I encourage all users to use [CachyOS kernels](https://github.com/CachyOS/linux-cachyos), in the development of which I will take an active part from now on.

###### linux-lucjan incorporates:

* [bfq improvements](https://groups.google.com/forum/#!forum/bfq-iosched) - latest fixes authored by Paolo Valente and BFQ Team

* ~~[bfq-dev](https://github.com/Algodev-github/bfq-mq/tree/dev-bfq-on-5.17) - latest fixes authored by Paolo Valente and BFQ Team~~

* ~~[bfq-dev-lucjan](https://github.com/sirlucjan/bfq-mq-lucjan/tree/dev-bfq-on-5.17-lucjan) - latest fixes authored by Paolo Valente and BFQ Team and forked by Piotr Gorski~~

* ~~[bfq-dev-lucjan-patches](https://github.com/sirlucjan/kernel-patches/tree/master/5.17/bfq-dev-lucjan) / [bfq-dev-lucjan-patches](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.17/bfq-dev-lucjan) - specific patches authored by Paolo Valente and Piotr Gorski~~

* [bfq-lucjan](https://github.com/sirlucjan/kernel-patches/tree/master/5.18/bfq-lucjan) / [bfq-lucjan](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.18/bfq-lucjan) - specific patches authored by Paolo Valente and Piotr Gorski

* [graysky's GCC/Clang patch](https://github.com/graysky2/kernel_compiler_patch) - version for gcc v12/clang v13

* [Project C](https://gitlab.com/alfredchen/linux-prjc/tree/linux-5.18.y-prjc) / [Project C blog](http://cchalpha.blogspot.com) - contains the newest vesion with latest fixes

* [random fixes from zen-kernel](https://github.com/zen-kernel/zen-kernel/tree/5.18/master) - specific patches authored by Jan Alexander Steffens and ZEN Kernel Team

* [random fixes from xanmod-linux](https://github.com/xanmod/linux/tree/5.18) - specific patches authored by Alexandre Frade

* [random fixes from pfkernel](https://codeberg.org/pf-kernel/linux/src/branch/pf-5.18) - for example patches from Arch Linux or specific patches authored by Oleksandr Natalenko

* [random fixes from CachyOS](https://github.com/CachyOS/linux-cachyos) - specific patches authored by CachyOS Team

* [UKSMD](https://codeberg.org/pf-kernel/uksmd) - Userspace KSM helper daemon authored by Oleksandr Natalenko

* [LL-patches](https://github.com/sirlucjan/kernel-patches/tree/master/5.18/ll-patches) / [LL-patches](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.18/ll-patches) - specific patches authored by Piotr Gorski

* [LL-branding](https://github.com/sirlucjan/kernel-patches/tree/master/5.18/ll-branding) / [LL-branding](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.18/ll-branding) - specific patches authored by Piotr Gorski

***

###### Some patches for BFQ/block-stable conflict with patches for BFQ-dev/block-mainline.

###### To use lucjan-kernels smoothly apply ll-reverts before linux-lucjan patch. Otherwise the kernel will not compile.

* ~~[ll-reverts](https://github.com/sirlucjan/kernel-patches/tree/master/5.11-dev/ll-reverts) / [ll-reverts](https://gitlab.com/sirlucjan/kernel-patches/tree/master/5.11-dev/ll-reverts) - specific patches authored by Piotr Gorski~~

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

### Rolling

```
cd /some_path/lucjan-kernels/lucjan-kernels-rolling/package_name
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
