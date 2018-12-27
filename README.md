# My own kernels. Use at your own risk.
###### Dell Inspiron 15-3542 (3542-2538) with Fourth Gen Intel Core i3/i5/i7 optimized.
###### linux-lucjan varies considerably from stock kernel. 
***
###### linux-lucjan incorporates:

* [bfq improvements](https://groups.google.com/forum/#!forum/bfq-iosched) - latest fixes authored by Paolo Valente and BFQ Team
 
* [BFQ-SQ and BFQ-MQ Scheduler](https://github.com/Algodev-github/bfq-mq) - bfq-sq and bfq-mq from Algodev-github 

* [graysky's GCC patch](https://github.com/graysky2/kernel_gcc_patch) - version for gcc 8.1

* [UKSM (sources)](https://github.com/dolohow/uksm) / [UKSM (info)](https://www.usenix.org/sites/default/files/conference/protected-files/fast18_slides_xia.pdf) - resync from dolohow’s github

* [PDS-mq](https://github.com/cchalpha/PDS-mq) / [PDS-mq blog](http://cchalpha.blogspot.com) - contains the newest vesion with latest fixes

* [random fixes from pfkernel](https://github.com/pfactum/pf-kernel) - for example patches from Arch Linux or specific patches authored by Oleksandr Natalenko

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


### Experimental V1

```
cd /some_path/lucjan-kernels/lucjan-kernels-experimental-v1/package_name
makepkg -srci

```

### Experimental V2

```
cd /some_path/lucjan-kernels/lucjan-kernels-experimental-v2/package_name
makepkg -srci

```

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
# Enable bfq-mq

For now, you can use `sudo tee /sys/block/sda/queue/scheduler <<< bfq-mq` to enable "bfq-mq".

You can also add this to file `60-schedulers.rules`:

```
# Non-rotational disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="bfq-mq"
# Rotational disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="bfq-mq"
```
and run a command `sudo udevadm control --reload && sudo udevadm trigger`


***
# You've been warned.
