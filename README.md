# KFS-1 - Kernel From Scratch

A simple x86 kernel that boots with GRUB and displays "42" on the screen.

## Requirements

- `nasm` - Netwide Assembler for compiling assembly code
- `gcc` - GNU C Compiler with i386 support
- `ld` - GNU Linker
- `grub-mkrescue` - GRUB bootable ISO creator
- `xorriso` - ISO filesystem tool (dependency for grub-mkrescue)
- `qemu-system-i386` (optional) - For testing the kernel

### Installation on macOS

```bash
brew install nasm
brew install i686-elf-gcc
brew install xorriso
brew install grub
brew install qemu
```

Note: You may need to use `i686-elf-gcc` and `i686-elf-ld` on macOS. Update the Makefile if needed.

### Installation on Linux

```bash
sudo apt-get install nasm gcc grub-common xorriso qemu-system-x86
```

## Project Structure

```
kfs-1/
├── boot.asm        # Assembly bootloader with multiboot header
├── kernel.c        # Main kernel code in C
├── kernel.h        # Kernel header file
├── linker.ld       # Linker script for i386
├── Makefile        # Build system
└── README.md       # This file
```

## Building

To build the kernel and create a bootable ISO:

```bash
make
```

This will:
1. Compile `boot.asm` to an object file
2. Compile `kernel.c` to an object file
3. Link both objects using `linker.ld` to create `kernel.bin`
4. Create a bootable ISO with GRUB

## Running

### With QEMU

```bash
make run
```

### With other virtual machines

Use the generated `kfs-1.iso` file with:
- VirtualBox
- VMware
- Real hardware (burn to CD/USB)

## Cleaning

To remove all build artifacts:

```bash
make clean
```

To rebuild everything:

```bash
make re
```

## Features

- Multiboot compliant (bootable with GRUB)
- Protected mode i386 kernel
- VGA text mode output
- Displays "42" on screen

## Implementation Details

### boot.asm
- Contains multiboot header for GRUB
- Sets up kernel stack
- Calls kernel_main function

### kernel.c
- Implements VGA text mode driver
- Provides screen manipulation functions
- Displays "42" on screen at position (0,0)

### linker.ld
- Maps kernel to 1MB memory address
- Organizes sections (.text, .data, .bss, .rodata)
- Sets proper alignment for sections

## License

42 School Project
