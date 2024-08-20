# My dotfiles
My hyprland config that I got tired of reconfiguring over and over again

## Notes to self

### Fix insanely slow boot time
My laptop experiences a prolonged boot process due to the /dev/tpmrm0 device (Kernel Time Sync)
Check this by removing "quiet" option of grub in ```/etc/default/grub```, then updating grub and reboot.
```
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet"
```

If its by that device, put it to sleep
```sh
systemctl mask dev-tpmrm0.device
```

### Possibly Missing Packages (after archinstall'ing Hyprland)

#### Add chaotic-aur to pacman
Before installing, add chaotic-aur repo to your pacman.conf by following instructions  [here](https://aur.chaotic.cx/docs)
<br><br>
Then install the packages below
```sh
sudo pacman -S --needed waybar brightnessctl hyprlock wl-clipboard unzip p7zip less htop fastfetch vesktop
```

### Symlinking configs
A config of an each program needs to be symlinked to this dotfiles directory as its shown below
```sh
# Make a directory for the desired program
mkdir /path/to/dotfiles/config/<program>

# Move the contents of the original config to dotfiles
mv ~/.config/<program>/* /path/to/dotfiles/<program>

# Purge the emptied program config
rm -rf ~/.config/<program>/

# Link!!!
ln -s /path/to/dotfiles/<program> ~/.config/<program>
```

### Arch Linux broke once again, Oh Noooo!
Man up and grab your fresh Arch Linux bootable USB stick and plug it.

Instead of powering off and holding down F2 like a normie, order your pc to do it via commandline:
```sh
systemctl reboot --firmware-setup
```

Or just reboot and pick UEFI Firmware Settings on the GRUB menu... boring.

### Chrooting
Mount the partitions
```
# The big partition

## If it is btrfs
mount /dev/sdaX /mnt -o subvol=@

## If it is ext4
mount /dev/sdaX /mnt

# The 1G boot partition
mount /dev/sdaY /mnt/boot
```

Chroot
```
arch-chroot /mnt
```

Dont forget to unmount afterwards to exit gracefully
```
umount -R /mnt
```
