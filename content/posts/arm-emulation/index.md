---
title: how to set up ARM environments for emulation
date: 2023-09-05
description: for dynamic analysis, since static analysis of ARM binaries don't need a full ARM environment
tags: [ARM, emulation, dynamic analysis]
---

There are generally 3 options when setting up an ARM environments:

1. using a local env on physical ARM hardware
   - like a laptop, server, or board
   - some possible options are Raspberry Pis, and Macs with Apple's custom M1 and M2 chip (most Mac devices are now based on ARM architecture)
2.  using an emulator
   - QEMU (virtual ARM env to run target binary, where the ARM CPU is software running on a CPU in different architecture)
3. using a cloud-based ARM env
   - like EC2 A1 instances on AWS
   - AWS EC2 C6g and R6g instances are also using Armv8-A architecture

We'll first talk about Arm boards, and then get right into emulation. 

## Arm boards
This is the easiest way to run Arm programs. There are a lot of different Arm boards to choose, and one thing to keep in mind is how consumer boards and development boards are usually in a different price range. For example, the dev boards are more expensive, and some inclide:
- [these ARM Cortex-A Dev boards](https://microcontrollershop.com/default.php?cPath=154_170_481)
- [Juno Dev Board](https://developer.arm.com/Tools%20and%20Software/Juno%20Development%20Board)
- [HiKey 960 Dev board](https://www.96boards.org/product/hikey960/)

For consumer boards,, the best known one is the Raspberry Pi. Also, another good one is the [RK3399 board](https://opensource.rock-chips.com/wiki_RK3399).

Keep in mind what architecture the binaries are compiled for, because the board needs to support that architecture too.

## QEMU Emulation
Now let's start with emulation, specifically using QEMU.

QEMU has two main ways of emulation, `full system emulation` and `user-mode emulation`.

### `Full System Emulation` 

In this mode, QEMU makes a complete self-contained "virtual machine". It basically emulates the Arm CPU with virtualized peripherals like hard drives, networking adapters, etc. Then, an OS can be installed onto this VM and the Arm binary can be copied here and executed.

This is useful for needing an environment for firmware emulation or dynamic analysis of malware. For working with Arm assembly, debugging, and testing nonmalicious binaries, user-mode emulation is more suited.

### `User-Mode Emulation`
Here, QEMU runs on a single binary compiled for a different architecture than the one supported by the host system. It basically decodes and runs each Arm instruction in software to emulate an Arm processor. Issued syscalls are intercepted and sent to the host system, which allows for seamless interaction for you. 

We will talk about how to set up user-mode emulation to run binaries compiled for Arm 32-bit and 64-bit architectures.

First we need to install packages:

```
user@ubuntu:~$ sudo apt install qemu-user qemu-user-static
```

Next, we 



