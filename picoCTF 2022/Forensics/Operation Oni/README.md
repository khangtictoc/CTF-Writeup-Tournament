# Operation Oni ❓

**Tags:** Forensics

**Point:** 300 points

**Description:** 
Download this disk image, find the key and log into the remote machine. <br>
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.<br>
[Download disk image](https://mega.nz/file/4s1XxDYA#TBWI6IaqCNslV5j_dbxmupYhx36wC3o_Iagd0WZ_Al4)<br>
Remote machine: ssh -i key_file -p 61248 ctf-player@saturn.picoctf.net

### Solution: 💯

This challenge examine whether you know `ssh` with `private key` or not. Extract file **gzip** extension: `gzip -d disk.img.gz`

Extract file: `gzip -d disk.img.gz`

A **Disk Image Data File** (.img) again. In this chall, we have to show all the folder structure of the image, find and read the flag. There are many way to do this. Normally, we often clone this image and mount it into a loopback device **(/dev/loop)** and move to there to read all the content. But I will use the most convenient and powerful tool to make this quick.

Install and using [AutoSpy](https://www.sleuthkit.org/autopsy/). Create a "case" project with optional name and choose folder to store -> Skip "Optional Information" -> Generate new host name based on data source name -> Disk Image or VM file -> Select path to "disk.flag.img" -> Next -> Finish

Open **volume 3** sector. 

<p align="center"> <img  src="https://user-images.githubusercontent.com/48288606/159508390-e9f38273-2704-4764-9158-bb284c03800a.png"></p>

Find **SSH private key files**. They're often in `~/.ssh/` path. But file image doesn't have any specific user, so maybe we guess it's in `/root`. Find in the path `/root/.ssh`

![image](https://user-images.githubusercontent.com/48288606/159508870-c1657344-1774-4a3a-86e7-6ed6ad5fc368.png)

There's 1 private key file. See raw content in "text".

<p align="center"> <img  src="https://user-images.githubusercontent.com/48288606/159511287-f1ae1749-cf96-4246-8f0e-e9ccc1fd3563.png"></p>

 Copy that key into our `id_ed25519`. Then SSH to server 

```bash
ssh -i id_ed25519 -p 61248 ctf-player@saturn.picoctf.net 
```

Make sure private key file "id_ed25519" has permission "400" or "600". Use `chmod` to conduct this, then read the `flag.txt` 

<p align="center"> <img  src="https://user-images.githubusercontent.com/48288606/159507202-4faac79a-5069-4e65-9a3d-2bdf3ee3fc2a.png"></p>

#### The Flag (for reference): ✔️
```
picoCTF{k3y_5l3u7h_af277f77}
```
