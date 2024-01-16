---
title: "How do I generate random bytes with `openssl`?"
justification: "I said I'd learn OpenSSL; `rand` is another tool in the toolbox"
---

Another command in `openssl` is `rand`. We invoke it like this:

```bash
$ openssl-3 rand -hex 120 | fold -w 2 | tr '\n' ' ' | sed 's/ $/\n/'
31 17 cf ee 25 47 c6 19 0c c0 d7 fd 9c e8 28 ff d8 05 44 62 dc e6 b8 5e 54 52 ad 26 7f 5e 9c 9d 63 73 b2 c7 d4 9c 94 6b 1f 7f 49 73 91 85 1f c4 05 58 f5 c9 e5 5d 98 9c 56 67 fb bf 71 cd 4a f9 9e 23 7d 82 a5 3e 1e 4a 80 33 12 9a f0 fc 0d 6a d5 14 88 14 73 1d 69 91 c8 48 f2 db d8 3d 68 5e fc f9 fa b9 b8 29 7f a9 c7 d5 e6 e9 63 42 b1 9f c8 1e 6a 22 0b 86 d7 7f
```

Here, `10` indicates the number of random bytes to print to standard out. `-hex` prints those bytes in hex format - 2 characters per byte, so 20 characters.

The output comes from a PRNG. The PRNG is seeded with, amongst other randomness sources, a file at `~/.rnd`. This file contains random bytes:

```
$ cat ~/.rnd
33k�ɱ��%�*��#Yn�� ]w$Lkn���M|cW@9%V
...
```

OpenSSL apparently uses this location to store previously-gathered entropy. You can delete it at any time without any ill effects.
