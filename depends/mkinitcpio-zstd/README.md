# Enable zstd compressed modules

###### To build a kernel with modules compressed in zstd format, insert any character here (it can be "y", "x" or any other value):

```
### Enable MODULE_COMPRESS_ZSTD
# WARNING Not recommended.
# An experimental solution, still in testing phase.
# Possible compilation and installation errors.
# Leave it unselected.
# However, if you want to test the new solution,
# first install mkinitcpio-zstd:
# https://gitlab.com/sirlucjan/lucjan-kernels/tree/master/depends
# or
# https://github.com/sirlucjan/lucjan-kernels/tree/master/depends
_zstd_modules=
```
###### Remember that to do this you need to install modified version of mkinitcpio (mkinitcpio-zstd). To do this, run the following command:

```
cd /some_path/lucjan-kernels/depends/package_name
makepkg -srci

```

###### NOTE: mkinitcpio-zstd will overwrite the mkinitcpio.conf file and the old one will be saved as mkinitcpio.conf.pacsave - however, I recommend backing up this file before installing the modified mkinitcpio version.

# Enable zstd ultra compressed modules

###### To build a kernel with modules compressed with ultra flag insert any character here (it can be "y", "x" or any other value):

```
### Enable MODULE_COMPRESS_ZSTD_ULTRA
# WARNING Not recommended.
# An experimental solution, still in testing phase.
# Possible compilation and installation errors.
# Leave it unselected.
# However, if you want to test the new solution,
# first enable "_zstd_modules" (above flag).
# ATTENTION Without selecting the previous flag
# this one will not work!
# Remember: the ultra settings can sometimes
# be counterproductive in both size and speed.
_zstd_modules_ultra=
```
###### It is worth mentioning once again that the ultra flag does not guarantee that you will build significantly smaller modules - on the contrary, you may achieve the counterproductive effect. 
