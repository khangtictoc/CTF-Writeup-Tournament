# Redaction gone wrong❓

**Tags:** Forensics

**Point:** 100 points

**Description:** 
Now you DON’T see me.
[This](Financial_Report_for_ABC_Labs.pdf) report has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?

### Solution: 💯

The description also contains hints to solve the problem - "some of which have been redacted correctly, while some were not.". Open file with any **PDF Editor** and search for `picoCTF`.

There's 1 result and it's in the end of file,  "fake-redacted" string.
![image](https://user-images.githubusercontent.com/48288606/160042754-504352a7-f98c-460c-801e-f092e6e9b8cd.png)

**NOTE: For those who don't know how to copy this string. We just need to drag the mouse from start to end in that "black box"** 

#### The Flag (for reference): ✔️
```
picoCTF{C4n_Y0u_S33_m3_fully}
```
