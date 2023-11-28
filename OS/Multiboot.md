Multiboot specification is a standard that enables kernels to be booted
by a Multiboot-compliant bootloader (i.e. GRUB)

The Multiboot standard provides an interface between the bootloader and 
the OS kernel by putting a few magic values in some global variables
(multiboot header). The bootloader is parsing that header to determine
if the OS kernel is multiboot compliant.


```asm
<boot.s>

/* Declare constants for the multiboot header. */
.set ALIGN,    1<<0             /* align loaded modules on page boundaries */
.set MEMINFO,  1<<1             /* provide memory map */
.set FLAGS,    ALIGN | MEMINFO  /* this is the Multiboot 'flag' field */
.set MAGIC,    0x1BADB002       /* 'magic number' lets bootloader find the header */
.set CHECKSUM, -(MAGIC + FLAGS) /* checksum of above, to prove we are multiboot */

/* 
Declare a multiboot header that marks the program as a kernel. These are magic
values that are documented in the multiboot standard. The bootloader will
search for this signature in the first 8 KiB of the kernel file, aligned at a
32-bit boundary. The signature is in its own section so the header can be
forced to be within the first 8 KiB of the kernel file.
*/
.section .multiboot
.align 4
.long MAGIC
.long FLAGS
.long CHECKSUM
```
#### FLAGS
Bitfield representing multiple options or settings for the bootloader or the
system initialization.

1<<0 = 0001
1<<1 = 0010
0001 | 0010 = 0011

#### ALIGN and Page Boundary
Refers to the division of memory into fixed-size blocks called "pages."
These pages are the smallest units of memory that the operating system manages.
The usual page size is 4KiB or 4096 bits.

A page boundary represents the end of on page and the beginning of another.
When something is aligned on a page boundary, it means it starts at an address
that is a multiple of the page size.

0x0000 is a multiple of the usual page size (4096 = 0x1000)
0x1000, 0x2000, 0x3000 are also multiples of the page size
0x1FFF is one bit short of being align with the page size

#### MEMINFO and Memory Map
Setting the MEMINFO bit in the multiboot flag used in the  header forces the 
bootloader to provide the OS a Memory Map.

The Memory Map is a data structure that is passed from the bootloader that 
represents the memory layout. It contains information regarding the size of total
memory, any reserved regions and may contains other detaisl specific to the 
CPU architecture

[**source**](https://wiki.osdev.org/Bare_Bones)
