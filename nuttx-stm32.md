# NuttX on STM32

## NuttX

**NuttX** is a real-time operating system (RTOS) with an emphasis on standards compliance and small footprint. Scalable from 8-bit to 32-bit microcontroller environments, the primary governing standards in NuttX are POSIX and ANSI standards. Additional standard APIs from Unix and other common RTOS's (such as VxWorks) are adopted for functionality not available under these standards, or for functionality that is not appropriate for deeply embedded environments – such as fork().

## Build NuttX for STM32

### Preparation

- `arm-none-eabi-` toolchain
- git
- build-essential flex bison texinfo gettext
- libusb-1.0.0 libncurses5-dev minicom
- kconfig-frontends

  ```
  git clone git@bitbucket.org:nuttx/tools.git
  cd tools/kconfig-frontends
  ./configure --enable-mconf
  -or-
  ./configure --disable-shared --enable-static --enable-mconf
  make
  make install
  ```

- ...

### Build

```
mkdir nuttx-git
cd nuttx-git
git clone https://bitbucket.org/nuttx/nuttx.git nuttx
git clone https://bitbucket.org/nuttx/apps.git apps

cd nuttx/tools

# this step will not provide any output, but copy the configuration to
# nuttx-git/nuttx/.config

./configure.sh stm32f4discovery/usbnsh # nsh console/usb - need microUSB to USB cable
# -or-
./configure.sh stm32f4discovery/nsh    # nsh console/UART2 - need UART-TTL to USB cable eg FTDI

# and return to the nuttx directory
cd ..

make menuconfig
make
```

> http://nuttx.org/doku.php?id=wiki:howtos:stm32f4discovery_unix

### Build with `buildroot`

```
mkdir nuttx-git
cd nuttx-git
git clone https://bitbucket.org/nuttx/nuttx.git nuttx
git clone https://bitbucket.org/nuttx/apps.git apps
git clone https://bitbucket.org/nuttx/buildroot.git buildroot

# config nuttx build target
cd nuttx/tools
./configure.sh stm32f4discovery/usbnsh # nsh console/usb - need microUSB to USB cable
# -or-
./configure.sh stm32f4discovery/nsh    # nsh console/UART2 - need UART-TTL to USB cable eg FTDI
cd ../..

cd buildroot
make menuconfig
# set $(NUTTX_DIR) to "$(TOPDIR)/../nuttx" (default "$(TOPDIR)/../../nuttx")
make
```

> https://bitbucket.org/nuttx/buildroot

## Reference

- http://nuttx.org
- https://en.wikipedia.org/wiki/NuttX
- https://bitbucket.org/account/user/nuttx/projects/PROJ
- https://github.com/Samsung/iotjs/wiki/Build-for-NuttX
- https://github.com/Samsung/iotjs/blob/master/targets/nuttx-stm32f4/README.md
