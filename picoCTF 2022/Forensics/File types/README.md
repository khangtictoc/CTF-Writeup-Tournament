# File types❓

**Tags:** Forensics

**Point:** 100 points

**Description:** 
This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can.<br>
You can download the file from [here.]()

### Solution: 💯

A PDF file? It's not an actually PDF format, let's check up by read its raw format. Open with "Notepad"

We see a `bash script`. Create a `run.sh` file, copy the content into this file, then change permission for execution `sudo chmod 777 run.sh `

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/160062532-6f07e171-281c-4adc-b1dd-6d452d87e7af.png"></p>

This file contains multi-compressed data. You can use `file {file}` to get the file's format. For example:
```bash
$ file flag      
flag: current ar archive
```

Just following these step until we reach **ASCII text file**:

| Stage | File type                   | Rename (For correct extenstion) | Command to decompress    | Output file |
| ----- | --------------------------- | ------------------------------- | ------------------------ | ----------- |
|   1   | ar Archive                  | mv flag flag.a                  | ar x flag.a              | flag        |
|   2   | cpio archive                | mv flag flag.cpio               | cpio -i --file flag.cpio | flag        |
|   3   | bzip2 compressed data       | mv flag flag.bz2                | bzip2 -d flag.bz2        | flag        |
|   4   | gzip compressed data        | mv flag flag.gz                 | gzip -d flag.gz          | flag        |
|   5   | lzip compressed data        | mv flag flag.lz                 | lzip -d flag.lz          | flag        |
|   6   | LZ4 compressed data (v1.4+) | mv flag flag.lz4                | lz4 -d flag.lz4          | flag        |
|   7   | LZMA compressed data        | mv flag flag.lzma               | lzma -d flag.lzma        | flag        |
|   8   | lzop compressed data        | mv flag flag.lzo                | lzop -d flag.lzo         | flag        |
|   9   | lzip compressed data        | mv flag flag.lz                 | lzip -d flag.lz          | flag        |
|   10  | XZ compressed data          | mv flag flag.xz                 | xz -d flag.xz            | flag        |
|   11  | ASCII text                  |                                 |                          | flag        |

Open file `flag`: 

```text
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f35613833373565307d0a
```

Convert "byte" to "hexadecimal" or paste all this to **HexEditor**, I use **bless**

<p align="center"><img src="https://user-images.githubusercontent.com/48288606/160101411-203db285-461d-4029-b93c-1e7bd1b96a0a.png"></p>


 



#### The Flag (for reference): ✔️
```
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_5a8375e0}
```
