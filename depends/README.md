# mkinitcpio-lucjan

###### NOTE: mkinitcpio-lucjan will overwrite the mkinitcpio.conf file and the old one will be saved as mkinitcpio.conf.pacsave - however, I recommend backing up this file before installing the modified mkinitcpio version.

##### Patchset linux-lucjan adds support for firmware compressed in zstd format.
##### Unfortunately, the current version of mkinitcpio does NOT support such functionality.
##### mkinitcpio-lucjan contains the appropriate patches to support firmware compressed in the zstd format.

## Selecting the ZSTD modules and kernel compression level

###### To select the compression level, choose between "normal" and "ultra".

```
### Selecting the ZSTD kernel and modules compression level
# ATTENTION - one of two predefined values should be selected!
# 'ultra' - highest compression ratio
# 'normal' - standard compression ratio
# WARNING: the ultra settings can sometimes
# be counterproductive in both size and speed.
_zstd_level_value=''
```
###### The normal flag allows you to select a value between 1 and 19 (the default value zstd offers is 3), while the ultra flag allows you to select a value between 20 and 22. Values other than those suggested (so 19 for the normal flag and 22 for the ultra flag) should be entered here:

```
### Selecting the ZSTD modules and kernel compression level
	if [ "$_zstd_level_value" = "ultra" ]; then
		echo "Enabling highest ZSTD modules compression ratio..."
		scripts/config --set-val CONFIG_MODULE_COMPRESS_ZSTD_LEVEL 19
		scripts/config --enable CONFIG_MODULE_COMPRESS_ZSTD_ULTRA
		scripts/config --set-val CONFIG_MODULE_COMPRESS_ZSTD_LEVEL_ULTRA 22
		echo "Enabling highest ZSTD kernel compression ratio..."
		scripts/config --set-val CONFIG_ZSTD_COMP_VAL 22
	elif [ "$__zstd_level_value" = "normal" ]; then
		echo "Enabling standard ZSTD modules compression ratio..."
		scripts/config --set-val CONFIG_MODULE_COMPRESS_ZSTD_LEVEL 19
		scripts/config --disable CONFIG_MODULE_COMPRESS_ZSTD_ULTRA
		echo "Enabling standard ZSTD kernel compression ratio..."
		scripts/config --set-val CONFIG_ZSTD_COMP_VAL 19
	else
		if [ -n "$__zstd_level_value" ]; then
			error "The value $_zstd_level_value is invalid. Choose the correct one again."
		else
			error "The value is empty. Choose the correct one again."
		fi
		error "Selecting the ZSTD modules and kernel compression level failed!"
		exit
	fi
```

###### Entering any values other than "normal" and "ultra" as well as leaving the checkbox empty will immediately abort the compilation.

###### It is worth mentioning once again that the ultra flag does not guarantee that you will build significantly smaller modules - on the contrary, you may achieve the counterproductive effect.

# UKSMD

## Userspace KSM helper daemon.

###### Install uksmd-git and run the command:

```systemctl enable uksmd.service && systemctl start uksmd.service```

###### Upstream info:

https://gitlab.com/post-factum/uksmd
