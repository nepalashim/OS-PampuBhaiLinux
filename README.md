# OS-PampuBhaiLinux



# Customization of Puppy Linux

## Introduction
Puppy Linux is a lightweight, fast, and portable operating system designed for low-resource computers. This project focuses on making slight modifications to Puppy Linux to enhance its usability and aesthetics while maintaining its minimal footprint. The customized version includes a new boot splash screen, a modified desktop environment, new software packages, system sound customizations, and kernel parameter tweaks.

## Methodology

### 1. Setting Up Puppy Linux
1. Downloaded Puppy Linux ISO from the official site.
2. Installed it on a Virtual Machine (VM) and a USB drive for testing.

### 2. Modifications Implemented

#### 2.1 Boot Splash Screen Customization
- Extracted and modified `initrd.gz` to replace the default background.
- Replaced the boot image using:
  ```bash
  mkdir /mnt/initrd
  mount -o loop /initrd.gz /mnt/initrd
  cp /path/to/custom_image.jpg /mnt/initrd/back.jpg
  find . | cpio -o -H newc | gzip > /initrd.gz
  ```

#### 2.2 Desktop Environment (JWM) Modifications
- Changed the default wallpaper by replacing:
  ```bash
  cp /path/to/custom_wallpaper.jpg /usr/share/backgrounds/default.jpg
  ```
- Updated the JWM configuration in `~/.jwmrc`:
  ```xml
  <Background type="image">/usr/share/backgrounds/default.jpg</Background>
  <Font>Ubuntu 12</Font>
  ```
- Restarted JWM using:
  ```bash
  jwm -restart
  ```

#### 2.3 Software Optimization
- Removed unnecessary applications:
  ```bash
  rm -rf /usr/bin/abiword
  rm -rf /usr/bin/gnumeric
  ```
- Installed Firefox:
  ```bash
  wget https://ftp.mozilla.org/pub/firefox/releases/latest/linux-x86_64/en-US/firefox.tar.bz2
  tar -xjf firefox.tar.bz2 -C /opt/
  ln -s /opt/firefox/firefox /usr/bin/firefox
  ```

#### 2.4 System Sound Customization
- Replaced startup sound:
  ```bash
  cp /path/to/new_startup_sound.wav /usr/share/sounds/startup.wav
  ```

#### 2.5 Kernel Parameter Tweaks
- Checked the current kernel version:
  ```bash
  uname -r
  ```
- Modified boot parameters in `/boot/grub/menu.lst`:
  ```ini
  kernel /vmlinuz root=/dev/ram0 pmedia=usb acpi=off
  
