# St3g0 ❓

**Tags:** Forensics

**Point:** 300 points

**Description:** 
Download this image and find the flag. <br>
[Download image](pico.flag.png)

**Hint**: We know the end sequence of the message will be $t3g0.

### Solution: 💯

With the hint, we know this type is "LSB steganography". I reference a blog here to solve this challeng and FYI: https://blog.katastros.com/a?ID=01800-ffe13f08-1b4e-4d2b-a7e3-a85d5a5afb96

He also provide a tool we can use easily. I also save the [Python Code Solve](Decode_LSB_Steganography.py). Install required library and run it. 

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/159521187-f0a234c1-bc55-4dce-aa7d-4f9748d60291.png"> </p>

**NOTE: This is a quick-use tool. If you want, you should learn and find out the algorithm, the working flow of this kind of steganography as well as find out how to decode it.**


#### The Flag (for reference): ✔️
```
picoCTF{7h3r3_15_n0_5p00n_87ef5b0b}
```
