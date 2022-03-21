# Sleuthkit Intro ❓

**Tags:** Forensics

**Point:** 100 points

**Description:** 
Download the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.<br>
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
[Download disk image](https://mega.nz/file/oplAlRSQ#91TRbxCXSv6qkVQ5ym6bvJLvt-w6uxaIs2--FLGXiqo)<br>
Access checker program: nc saturn.picoctf.net 52279

### Solution: 💯

This challenge teach us more about forensic on a **image** file system. Tool use: `mmls`
Extract file **gzip** extension: `gzip -d disk.img.gz`
Use mmls to find the size of the Linux partition: `mmls disk.img`
Out put:
```
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```
Netcat to server `nc saturn.picoctf.net 52279` and submit result `0000202752`

<p align="center"><img src="https://user-images.githubusercontent.com/48288606/159230074-1ecfd4eb-ffe9-4211-ad50-d46e8d2f3494.png"></p>

#### The Flag (for reference): ✔️
```
picoCTF{mm15_f7w!}
```
