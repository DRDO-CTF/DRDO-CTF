# DRDO CTF 2017 : ReverseEngg-8

**Category:** Reverse Engineering

**Level:** Hard

**Points:** 200

**Solves:** 41

**Description:**

Mounting a temporary file system is simple isn't it. The given ELF64 binary does the same thing with some flags, including NOEXEC. Now wear a hat of an attacker and modify a single byte in the binary to mount the same file system without NOEXEC flag. Remaining flags must remain unchanged. Identify the offset byte, from the beginning of the code, which need to be changed. Your answer must be in the following format
* Fixed Prefix: “DRDO@60_{“
(Excluding Quotations)
* Offset byte in HEX in capital letters without any leading zero's, followed by the binary representation of the value of the modified byte without any leading zero's.
* Fixed Suffix: “}_FLAG!”
(Excluding Quotations)

## Write-up

(TODO)
