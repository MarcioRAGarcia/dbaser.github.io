---
title: TAMUctf 2017 - Siamese
date: 2017-04-25 18:29:00 Z
categories:
- write-ups
tags:
- stego
- tamuctf
---

Stego - 50 Points

The internet loves cats. Whats not to love?

# Write-up

let´s see what the type of [file](https://github.com/dbaser/ctfs/blob/master/TAMUctf-2017/for50-siamese/8ff4da2f7368f800)

```bash
$ file 8ff4da2f7368f800

8ff4da2f7368f800: GIF image data, version 89a, 320 x 180
```

```bash
$ binwalk 8ff4da2f7368f800  

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             GIF image data, version "89a", 320 x 180
662419        0xA1B93         MySQL MISAM index file Version 10
3204803       0x30E6C3        Zip archive data, at least v1.0 to extract, compressed size: 56, uncompressed size: 56, name: 8ff4da2f7368f800.txt
3205027       0x30E7A3        End of Zip archive
```