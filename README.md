
# Return-to-libc Attack — CS442 Software Security

Lab assignment for **CS442: Software Security**, College of Computer and Information Sciences, Imam Mohammad Ibn Saud Islamic University (First Semester 2025-2026).

## Overview

This assignment demonstrates a classic **return-to-libc** buffer overflow attack, where a vulnerable program's return address is redirected to a library function (`system()`) instead of injected shellcode, bypassing non-executable stack protections.

## Steps

1. **Find the address of `system()` and `exit()`**
   Disabled address space layout randomization (ASLR), compiled the vulnerable program, and used GDB to locate the addresses of `system` and `exit` in memory.

2. **Find the address of the `"/bin/sh"` string**
   Set the environment variable `MYSHELL="/bin/sh"`, compiled a helper program, and used GDB to find where the string lives in memory.

3. **Find the offset to the return address**
   Set a breakpoint, compared the stack base pointer (`$ebp`) and the buffer's address, and calculated the distance between them (282 bytes).

4. **Build and launch the exploit**
   Used the calculated addresses and offset to construct the malicious input (`badfile`) with `exploit.py`, then ran the vulnerable program to spawn a shell.

## Environment

- GDB for debugging and memory inspection
- A vulnerable C program with a buffer overflow (`retlib.c`)
- Python exploit script (`exploit.py`)

## Note

This exploit was built and run in an isolated lab environment for educational purposes, as part of a university course on software security.
