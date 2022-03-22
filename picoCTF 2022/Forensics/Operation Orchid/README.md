# Operation Orchid❓

**Tags:** Forensics

**Point:** 400 points

**Description:** 
Download this disk image and find the flag.<br>
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.<br>
[Download compressed disk image](https://mega.nz/file/9gkkwBTL#2CajCIPne49ujCu9B6dnoqIG8L643c0ATKm6R5P-j30)

### Solution: 💯

Extract file: `gzip -d disk.img.gz`

A **Disk Image Data File** (.img) again. In this chall, we have to show all the folder structure of the image, find and read the flag. There are many way to do this. Normally, we often clone this image and mount it into a loopback device **(/dev/loop)** and move to there to read all the content. But I will use the most convenient and powerful tool to make this quick.

Install and using [AutoSpy](https://www.sleuthkit.org/autopsy/). Create a "case" project with optional name and choose folder to store -> Skip "Optional Information" -> Generate new host name based on data source name -> Disk Image or VM file -> Select path to "disk.flag.img" -> Next -> Finish

Open **volume 4** sector. 

<p align="center"> <img  src="https://user-images.githubusercontent.com/48288606/159508390-e9f38273-2704-4764-9158-bb284c03800a.png"></p>

Move to "dangerous zone" `/root`. 

![image](https://user-images.githubusercontent.com/48288606/159528700-c5e81f7f-fd85-4d72-9a43-d0f1efece98c.png)

Here, there's 2 two sensitive-data file: 

- `.ash_history` : show all history command logs
- `flag.txt.enc`: The content start with "Salted__". It means this maybe encoded with `openssl`

Read `.ash_history`. 

![image](https://user-images.githubusercontent.com/48288606/159528608-5cd99d14-dcaa-4ea9-88e1-a166f0af58d4.png)

We know that user has do something with create a file, edit it with `nano`, do something with `apk` (not important), then encrypt the `flag.txt` file and output to `flag.txt.enc` with the key is `unbreakablepassword1234567`. 

But the one important is `flag.txt` file has been removed with `shred -u flag.txt`. Our task is recovering this file.

Luckily, we have all needed parameter. We just need to decrypt the data . First, use bless to create a same `flag.txt.enc` file by using **bless**.

<p align="center"><img width=700px height=350px src="https://user-images.githubusercontent.com/48288606/159528574-e5af8a96-1cad-405a-b933-25cede72b335.png"></p>

Then use similar command to decrypt the file and output the original `flag.txt` with `-d` option (decrypt): 

```bash
openssl aes256 -salt -d -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567
```

<p align="center"><img src="https://user-images.githubusercontent.com/48288606/159529453-b204128d-1a32-4514-8e7e-40265a0d39d9.png"></p>

#### The Flag (for reference): ✔️
```
picoCTF{h4un71ng_p457_17237fce}
```
