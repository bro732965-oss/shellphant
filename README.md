# shellphant bios console 16-bit

shellphant is a 16-bit shell (monitor) that interacts directly with the BIOS. It is designed for low-level exploration of disks, memory, and hardware.

Compatibility: Any device with a 16-bit BIOS (x86).

Commands (entered at the > prompt):

· d (Disk Read) — Reads a sector from the disk into the buffer at 0x8000.
· w (Disk Write) — Writes data from the buffer at 0x8000 to the disk.
· b (Boot) — Loads a sector to memory at 0x1000:0x0000 and transfers control.
· l (Load) — Same as b, but the load address (segment:offset) is specified manually.
· f (Find / Dir) — Scans the entire disk, finds the first non-empty sector, and prints its coordinates (Cylinder:Head:Sector).
· t (Text / Hex Dump) — Prints 512 bytes of the buffer in hex format (16 bytes per line).
· s (Scan Memory) — Reads 16 bytes starting at 0x7C00 and prints them in hex.
· o (Out byte) — Writes a specified byte to memory at a given segment:offset address.
· r (Read sector → RAM) — Reads a sector directly into a specified memory address.
· i (System Info) — Prints base memory size, FPU presence, and the number of floppy drives.
· q (Quit / Power Off) — Powers off the PC via APM (int 0x15, function 0x5307).