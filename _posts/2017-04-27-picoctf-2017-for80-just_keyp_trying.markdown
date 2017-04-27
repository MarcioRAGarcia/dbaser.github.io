---
title: picoCTF 2017 - Just Keyp Trying
date: 2017-04-27 20:27:00 Z
---

**Category:** Forensics
**Points:** 80
**Description:**

> Here's an interesting capture of some data. But what exactly is this data? Take a look: [data.pcap](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for80-just_keyp_trying/data.pcap)

**Hints:**

> Find out what kind of packets these are. What does the info column say in Wireshark/Cloudshark?

> What changes between packets? What does that data look like?

> Maybe take a look at [http://www.usb.org/developers/hidpage/Hut1_12v2.pdf?](http://www.usb.org/developers/hidpage/Hut1_12v2.pdf?)

# Write-up

we have a lot of usb data on this pcap file

![wireshark](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/picoCTF-2017/for80-just_keyp_trying/for80-just_keyp_trying-01.png)

let´s extract the **Leftover Capture Data** with `tshark`

```bash
[dbaser@pwn4food]$ tshark -r data.pcap -T fields -e usb.capdata

00:00:09:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0f:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:04:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:0a:00:00:00:00:00
00:00:00:00:00:00:00:00
20:00:00:00:00:00:00:00
20:00:2f:00:00:00:00:00
20:00:00:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:13:00:00:00:00:00
00:00:00:00:00:00:00:00
00:00:15:00:00:00:00:00
00:00:00:00:00:00:00:00
...
```    

we need only numbers without zeros and separators

```bash
[dbaser@pwn4food]$ tshark -r data.pcap -T fields -e usb.capdata
 | awk -F: '{print $3}' | grep -v 00 

09
0f
04
0a
2f
13
15
20
22
22
2d
27
11
...
```   

on the [pdf](http://www.usb.org/developers/hidpage/Hut1_12v2.pdf?) (Page 53), we have a key map of a USB Keyboard, just convert the output data with the key map

![keymap](https://raw.githubusercontent.com/dbaser/CTF-Write-ups/master/picoCTF-2017/for80-just_keyp_trying/for80-just_keyp_trying-02.png)

but wait motherfucker! we have 29 lines of data, let's use a python script to do the work for us! :D

{% gist f9f0240b726bca08de9473ab8c9cd9d6 %}

run the script and get the flag!

```bash
[dbaser@pwn4food]$ python usbkeymap1.py
output :FLAG[PR355-0NWARDS-C98CCF99]C
```   
The flag is: `FLAG[PR355-0NWARDS-C98CCF99]`

## Update

When I was writing this write-up, I found this [script](https://github.com/dbaser/CTF-Write-ups/blob/master/picoCTF-2017/for80-just_keyp_trying/usbkeymap2.py) from this [write-up](https://webstersprodigy.net/2012/11/09/csaw-2012-quals-tutorialwriteup/) that do the same job just by specifying the pcap file in the script.