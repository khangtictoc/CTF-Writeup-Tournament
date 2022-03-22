# Sleuthkit Apprentice ❓

**Tags:** Forensics

**Point:** 200 points

**Description:** 
Download this disk image and find the flag.<br>
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.<br>
[Download compressed disk image](https://mega.nz/file/VwUgyQaJ#odwFUesiJDSHmZATifv0puw6xjV4Z0tgUI4ABP2FJKM)

### Solution: 💯

Extract file **gzip** extension: `gzip -d disk.flag.img.gz`

A **Disk Image Data File** (.img) again. In this chall, we have to show all the folder structure of the image, find and read the flag. There are many way to do this. Normally, we often clone this image and mount it into a loopback device **(/dev/loop)** and move to there to read all the content. But I will use the most convenient and powerful tool to make this quick.

Install and using [AutoSpy](https://www.sleuthkit.org/autopsy/). Create a "case" project with optional name and choose folder to store -> Skip "Optional Information" -> Generate new host name based on data source name -> Disk Image or VM file -> Select path to "disk.flag.img" -> Next -> Finish

Open mounted **disk.flag.img** file. Move to volume 4 (Other volume has no content):

![image](https://user-images.githubusercontent.com/48288606/159490676-8377f7c1-139d-453f-84b6-cf7f9f46a842.png)


Examine `/root` folder (this often contains important data). Cut to `/root/my_folder`.

![image](https://user-images.githubusercontent.com/48288606/159491241-2282c175-bcf6-40ea-84e6-aa0a7d4a3495.png)

 Read "flag.uni.txt" :

<p align="center"><img src="https://user-images.githubusercontent.com/48288606/159491694-0fd85901-98f1-4182-bc9d-72edba225d77.png" ></p>


#### The Flag (for reference): ✔️
```
picoCTF{by73_5urf3r_42028120}
```
