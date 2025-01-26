# Flash-Orin-Nano-Super-via-CLI

## Download the Driver Package and Sample Root File System

cd Downloads

wget https://developer.nvidia.com/downloads/embedded/l4t/r36_release_v4.3/release/jetson_linux_r36.4.3_aarch64.tbz2

wget https://developer.nvidia.com/downloads/embedded/l4t/r36_release_v4.3/release/tegra_linux_sample-root-filesystem_r36.4.3_aarch64.tbz2

## Unzip the packages

cd  // to get back to home

tar xf Downloads/jetson_linux_r36.2.0_aarch64.tbz2

sudo tar xf Downloads/tegra_linux_sample-root-filesystem_r36.2.0_aarch64.tbz2 -C Linux_for_Tegra/rootfs/

## Create an Image to write the the Orin Nano
cd Linux_for_Tegra

sudo apt install -y qemu-user-static

sudo ./apply_binaries.sh

## Place Orin Nno in Recovery Mode

// Place jumper wire between Force Recovery Mode and Gnd  (Pins 10 & 11)

## Connect the Orin to the host via USB and confirm the it is in Recovery mode

// On the host, run this command and you should see the USB port showing APX device

$ lsusb |grep -i nvidia

Bus 003 Device 006: ID 0955:7523 NVIDIA Corp. APX

## Once confirmed, flash the Orin with the following command

sudo ./tools/kernel_flash/l4t_initrd_flash.sh --external-device nvme0n1p1 \
  -c tools/kernel_flash/flash_l4t_external.xml -p "-c bootloader/generic/cfg/flash_t234_qspi.xml" \
  --showlogs --network usb0 jetson-orin-nano-devkit internal

  ## Verify that Orin Nano displays login screen on the monitor

  // Be sure and remove jumper wire.

  

  
