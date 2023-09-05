---
title: how to set up ARM environments for emulation
date: 2023-09-05
description: for dynamic analysis, since static analysis of ARM binaries don't need a full ARM environment
tags: [ARM, emulation, dynamic analysis]
---

There are generally 3 options when setting up an ARM environments:

1. using a local env on physical ARM hardware
   - like a laptop, server, or board
   - some possible options are Raspberry Pis, and Macs with Apple's custom M1/M2 chip 
(most Mac devices are now based on ARM architecture)
2.  using an emulator
    - QEMU 
    (virtual ARM env to run target binary, where the ARM CPU is software running on a CPU in different architecture)
3. using a cloud-based ARM env
   - like EC2 A1 instances on AWS
   - AWS EC2 C6g and R6g instances are also using Armv8-A architecture


We'll first talk about Arm boards, and then get right into emulation. 

## Arm boards
This is the easiest way to run Arm programs. There are a lot of different Arm boards to choose, and one thing to keep in mind is how consumer boards and development boards are usually in a different price range. For example, the dev boards are more expensive, and some inclide:
- [these ARM Cortex-A Dev boards](https://microcontrollershop.com/default.php?cPath=154_170_481)
- [Juno Dev Board](https://developer.arm.com/Tools%20and%20Software/Juno%20Development%20Board)
- [HiKey 960 Dev board](https://www.96boards.org/product/hikey960/)

For consumer boards, the best known one is the Raspberry Pi. Also, another good one is the [RK3399 board](https://opensource.rock-chips.com/wiki_RK3399).

Keep in mind what architecture the binaries are compiled for, because the board needs to support that architecture too.

## QEMU Emulation
Now let's start with emulation, specifically using QEMU.

QEMU has two main ways of emulation, `full system emulation` and `user-mode emulation`.

### Full System Emulation

In this mode, QEMU makes a complete self-contained "virtual machine". It basically emulates the Arm CPU with virtualized peripherals like hard drives, networking adapters, etc. Then, an OS can be installed onto this VM and the Arm binary can be copied here and executed.

This is useful for needing an environment for firmware emulation or dynamic analysis of malware. For working with Arm assembly, debugging, and testing nonmalicious binaries, user-mode emulation is more suited.

### User-Mode Emulation
Here, QEMU runs on a single binary compiled for a different architecture than the one supported by the host system. It basically decodes and runs each Arm instruction in software to emulate an Arm processor. Issued syscalls are intercepted and sent to the host system, which allows for seamless interaction for you. 

We will talk about how to set up user-mode emulation to run binaries compiled for Arm 32-bit and 64-bit architectures.


## Emulation Steps

### for User-Mode Emulation

For this example, I'll be using AArch64, and I'm running it on a Intel-based x64 Linux host.

First we need to install packages:

```
user@ubuntu:~$ sudo apt install qemu-user qemu-user-static
```

Next, **`for Arm 32-bit`** , install:

```
user@ubuntu:~$ sudo apt install gcc-arm-linux-gnueabihf binutils-arm-
linux-gnueabihf binutils-arm-linux-gnueabihf-dbg
```

**`For AArch64`** , install:

```
user@ubuntu:~$ sudo apt install gcc-aarch64-linux-gnu binutils-aarch64-
linux-gnu binutils-aarch64-linux-gnu-dbg
```

We have now installed QEMU. 

We can compile a simple program for AArch64, and this is our example code:

`hello64.c`
```
#include <stdio.h>
int main(void) { return printf("Hello, I am an ARM64 binary!\n"); }
```

Then we can cross-compile this with AArch64's version of GCC:

```
user@ubuntu:~$ aarch64-linux-gnu-gcc -static -o hello64 hello64.c
```

We can check the host system by typing `uname -a`, and we can check if our binary was correctly compiled with `file hello64`

```
user@ubuntu:~$ file hello64
hello64: ELF 64-bit LSB executable, ARM aarch64, version 1 (GNU/Linux),
statically linked, BuildID[sha1]=66307a9ec0ecfdcb05002f8ceecd310cc
6f6792e, for GNU/Linux 3.7.0, not stripped
```

Finally, we can run this binary with `QEMU's user-mode emulation`: 

```
user@ubuntu:~$ qemu-aarch64 ./hello64
Hello, I am an ARM64 binary!
```

In fact, we can even run it with 
```
user@ubuntu:~$ ./hello64
Hello, I am an ARM64 binary!
```

The reason for this is the `qemu-user-binfmt` package that tells the Linux kernel how to interpret files with it's signature. 

This is the same for 32-bit binaries:

```
user@ubuntu:~$ arm-linux-gnueabihf-gcc -static -o hello32 hello32.c
user@ubuntu:~$ ./hello32
Hello, I am an ARM32 binary!
```

And for dynamically linked executables use `-L` to supply libraries + interpreter:

```
user@ubuntu:~$ aarch64-linux-gnu-gcc -o hello64dyn hello64.c
user@ubuntu:~$ qemu-aarch64 -L /usr/aarch64-linux-gnu ./hello64dyn
Hello, I'm executing ARM64 instructions!
```

Same for 32-bit dynamically linked libraries:
```
user@ubuntu:~$ qemu-arm -L /usr/arm-linux-gnueabihf ./hello32
Hello, I am an ARM32 binary!
```

### for Full-System Emulation
In this example, we'll be using information from the official Debian Wiki page and use a prebuilt Debian image:

```
user@ubuntu:~$ wget https://cdimage.debian.org/cdimage/openstack/
current/debian-<VERSION>-arm64.qcow2
```

Before we add the recommended SSH key, we start system emulation:

```
user@ubuntu:~$ qemu-system-aarch64 -m 2G -M virt -cpu max \
-bios /usr/share/qemu-efi-aarch64/QEMU_EFI.fd \
-nographic \
-drive if=none,file=debian-<VERSION>-arm64.qcow2,id=hd0 \
-device virtio-blk-device,drive=hd0 \
```

The image has now been booted, and the user directory has been created automatically. Shut down the emulation and run these commands to add your SSH key.

```
user@ubuntu:~$ sudo modprobe nbd
user@ubuntu:~$ sudo qemu-nbd -c /dev/nbd0 debian-<VERSION>-arm64.qcow2
user@ubuntu:~$ sudo mount /dev/nbd0p2 /mnt
user@ubuntu:~$ ssh-add -L > /mnt/home/debian/.ssh/authorized_keys
user@ubuntu:~$ sudo umount /mnt
user@ubuntu:~$ sudo qemu-nbd -d /dev/nbd0
```

Now, you can SSH into your QEMU environment, and basically use it as you would a VM or your host system. 

Remember that if you need to use a different Arm environment, you will need to use the right images (and not the exact one from the example).