# DRDO CTF 2017 : ReverseEngg-3

**Category:** Reverse Engineering

**Level:** Easy

**Points:** 50

**Solves:** 50

**Description:**

A KEY is HIDDEN inside a SECRET. READing This key will unlock the flag. If key is EMPTY you have to guess the KEY. All SECRETS are in the executable.

## Write-up

This challenge requires a file named `key.bin` to be placed in the `%LOCALAPPDATA%\secret` folder. Also, the attributes of the file should be `hidden` and `read-only`. The challenge binary reads the contents of the file *key.bin* and treats it as a key to decode the stored values in the binary. The expected key value is "FLYTEJAS". The solution python code for this challenge is as follows:

```python
key = "FLYTEJASFLYTEJASFLYTEJASFLYTEJAS"
enc = "021e1d1b057c710c3d6f783001792f0c713e6a14361f336068310612090b0672".decode('hex')
plain = ''.join(hex(ord(a) ^ ord(b))[2:].zfill(2) for a,b in zip(key,enc))
print plain.decode('hex')

# OUTPUT
# DRDO@60_{#!dD3n_7r3@sUr3.}_FLAG!
```

`FLAG: DRDO@60_{#!dD3n_7r3@sUr3.}_FLAG!`
