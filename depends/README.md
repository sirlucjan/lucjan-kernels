# mkinitcpio-zstd

##### mkinitcpio in the current version 30 does not full support modules compressed in zstd format.
##### These changes will significantly reduce the size of initramfs and also simplify the format of system logs.
##### A pull request has been approved by the developers and the next version 31 will support decompression of modules in this format without any problems.
##### Source: https://github.com/archlinux/mkinitcpio/pull/43/commits
##### I have been testing this solution since December 2020 and have not found any irregularities. Please report any bugs in this exact repository.

###### NOTE: mkinitcpio-zstd will overwrite the mkinitcpio.conf file and the old one will be saved as mkinitcpio.conf.pacsave - however, I recommend backing up this file before installing the modified mkinitcpio version.

## Selecting the ZSTD module compression level

###### To select the compression level, choose between "normal" and "ultra".

```
### Selecting the ZSTD module compression level
# If you want to use ZSTD compression,
# first install mkinitcpio-zstd:
# https://gitlab.com/sirlucjan/lucjan-kernels/tree/master/depends
# or
# https://github.com/sirlucjan/lucjan-kernels/tree/master/depends
# ATTENTION - one of two predefined values should be selected!
# 'ultra' - highest compression ratio
# 'normal' - standard compression ratio
# WARNING: the ultra settings can sometimes
# be counterproductive in both size and speed.
_zstd_module_level=''
```
###### The normal flag allows you to select a value between 1 and 19 (the default value zstd offers is 3), while the ultra flag allows you to select a value between 20 and 22. Values other than those suggested (so 19 for the normal flag and 22 for the ultra flag) should be entered here:

```
### Selecting the ZSTD module compression level
	if [ "$_zstd_module_level" = "ultra" ]; then
		echo "Enabling highest ZSTD module compression ratio..."
		scripts/config --set-val CONFIG_MODULE_COMPRESS_ZSTD_LEVEL 19
		scripts/config --enable CONFIG_MODULE_COMPRESS_ZSTD_ULTRA
		scripts/config --set-val CONFIG_MODULE_COMPRESS_ZSTD_LEVEL_ULTRA 22
	elif [ "$_zstd_module_level" = "normal" ]; then
		echo "Enabling standard ZSTD module compression ratio..."
		scripts/config --set-val CONFIG_MODULE_COMPRESS_ZSTD_LEVEL 19
		scripts/config --disable CONFIG_MODULE_COMPRESS_ZSTD_ULTRA
	else
		if [ -n "$_zstd_module_level" ]; then
			error "The value $_zstd_module_level is invalid. Choose the correct one again."
		else
			error "The value is empty. Choose the correct one again."
		fi
		error "Selecting the ZSTD module compression level failed!"
		exit
	fi
```

###### Entering any values other than "normal" and "ultra" as well as leaving the checkbox empty will immediately abort the compilation.

###### It is worth mentioning once again that the ultra flag does not guarantee that you will build significantly smaller modules - on the contrary, you may achieve the counterproductive effect.
