# My own kernels. Use at your own risk.
# Dell Inspiron 15-3542 (3542-2538) with Fourth Gen Intel Core i3/i5/i7 optimized.
# linux-lucjan varies considerably from stock kernel. 
# linx-lucjan incorporates:

* [bfq improvements](https://groups.google.com/forum/#!forum/bfq-iosched)

* [bfq-mq from Algodev-github](https://github.com/Algodev-github/bfq-mq)

* [graysky's GCC patch](https://github.com/graysky2/kernel_gcc_patch)

* [UKSM](https://github.com/dolohow/uksm)

* [PDS-mq](https://bitbucket.org/alfredchen/linux-gc/downloads)

* [random fixes from pfkernel](https://github.com/pfactum/pf-kernel)


# You've been warned.

# Download:

```
git clone https://github.com/sirlucjan/lucjan-kernels.git

```

or

```
git clone https://gitlab.com/sirlucjan/lucjan-kernels.git

```

# Install:


# Testing

```
cd /some_path/lucjan-kernels/lucjan-kernels-testing/package_name
makepkg -srci

```

# Unstable

```
cd /some_path/lucjan-kernels/lucjan-kernels-unstable/package_name
makepkg -srci

```

# Enable bfq-mq

For now, you can use `sudo tee /sys/block/sda/queue/scheduler <<< bfq-mq` to enable "bfq-mq".

You can also add this to your udev rules:
```
# Non-rotational disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="bfq-mq"
# Rotational disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="bfq-mq"
```
and run a command `sudo udevadm control --reload && sudo udevadm trigger`



