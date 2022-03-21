# Eavesdrop ❓

**Tags:** Forensics

**Point:** 300 points

**Description:** 
Download this packet capture and find the flag.
[Download packet capture](capture.flag.pcap)

### Solution: 💯

Open **pcap** file with "Wire Shark". Move through each packet and you will realize this is a conversation between 2 sides. One side want to know how to send encrypted message and the other will instruct how to do that.

There're 2 main essential packet:
- Packet No.18: Instruction for how to send encrypted message by using `openssl` command. Extract syntax to use: `openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123`

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/159299647-e1703e98-d9e9-46ed-8fc6-9c93c4d57bdb.png"> </p>

- Packet No.57: Data in file **file.des3**. **\*.des3** file is always specified by a starting string "Salt__". 
**NOTE: We can use decrypt and encrypt a sample file for testing this**

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/159300460-25e70d19-0dfb-44c0-ac5f-b95dc38c692a.png"> </p>

Use **"Hex Editor"** (HxD) in Window, or **"Bless"** in Linux for creating and editing hex file.

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/159301070-6735344e-b161-4c58-a878-92ed14fdca59.png"> </p>

Then use this command again to decrypt. 
**NOTE**: For explaining, (Not necessary, just FYI) the command will decrypt`-d` `file.des3` and export to `file.txt` with key `supersecretpassword123` and use **DES** as algorithm. [Reference more!](https://www.openssl.org/docs/man1.0.2/man1/openssl-enc.html)

```bash
openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123
```

Then read output file **file.txt**:

#### The Flag (for reference): ✔️
```
picoCTF{nc_73115_411_77b05957}
```
