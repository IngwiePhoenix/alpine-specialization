# Alpine, specialized.

This repository is inspired by the work done in [Armbian](https://armbian.org), [BreadOS](https://bredos.org/) and [PostmarketOS](https://postmarketos.org/).

The idea is simple: Provide a vanilla Alpine Linux installation with as few/minimal additions as possible - to the point, that when a board reaches that upstream status, you could basically remove this repository and reinstall `linux-lts`, and `linux-headers`. U-Boot and EDK2 are probably a different situation and very dependant of the board. But, you get the idea; let Alpine be Alpine and just provide enough coverage to ensure that vendor-provided hardware works (i.e., their VPU, NPU and other components that are only properly covered in vendor/BSP kernels untill they become upstreamed, accepted and merged).

## Why Alpine?

Most of the SBCs I have end up being used to serve stuff; all the way from singular Podman deployments to Kubernetes. And so far I have been (successfuly) using Armbian. Since I base most of my images off of Alpine already and use it in WSL and on test hardware, I figured I would do my attempt at building "vendor images". This is already heavily covered by PostmarketOS - but their "mainly mainline" approach does not work with many SBCs. So, this repo here is ment to be the "stopgap"; not as heavily integrated as Armbian, but not as strictly tied to upstream as PostmarketOS.

## Devices

I am attempting to, currently, cover these devices and (sub)projects:

### RISC-V
- SpacemiT MUSE Pi Pro
  * UEFI Boot via their EDK2 implementation.
  * Vendor kernel + VPU firmware (ArmChina Linlon-v5)
- Milk-V Pioneer
  * UEFI booting via provided EDK2 image
  * Requires additional files in `riscv/` folder on ESP and has a rather stuffy SPI...
  * Vendor kernel build
    - Might genuenly be obsolete; see here: https://github.com/sophgo/linux/wiki
    
### ARM
- Radxa Orion O6
  * UEFI Boot as provided via Radxa/CIX's EDK2 implementation
  * Tidied up kernel patches by Stuart: https://github.com/srcshelton/linux-cix
  * Upstream portwork by Entropi: https://github.com/Sky1-Linux
- Radxa Dragon Q6a
  * Boot is provided via EDK2
  * Needs >6.19 kernel, so I will probably build it here and see if I can add tweaks to it.
- FriendlyElec NanoPi R6s, Radxa Rock 5 ITX
  * Boot via community port of EDK2: https://github.com/edk2-porting/edk2-rk3588
  * Will likely need vendor image/s; not fully upstream just yet.
- FriendlyElec NANO3
  * Needs the whole chain from U-Boot to Kernel and friends.
  * My appliance is a 2GB model, it won't build a kernel ever...

# Do not take this too serious.

I am quite new to building my own OS images and using this opportunity to learn packaging and build infrastructure as used in (very) large projects. Ultimatively, I want to build my CI/CD off of that and effectively feed my own homelab with automated, updated builds. So this is both me learning things and also trying to provide something useful in the process.

And, why learn this in the first place? Because I can, want to, and have the resources to do so. :) Nothing special - just a dude hacking away on hsi keyboard and trying things out!
