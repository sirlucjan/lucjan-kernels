# My own kernels. Use at your own risk.
# Dell Inspiron 15-3542 (3542-2538) with Fourth Gen Intel Core i3/i5/i7 optimized.
# linux-lucjan varies considerably from stock kernel. 
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



