# Plain

**Point**: 100

**Author**: SwitchBlade

Someone logged into my computer and stole my flag. Can you get it back for me?

**File**: [Plain](plain.zip)

## Solution:

With the hint, we could guess that "stoling flag" is often acted by protocols like **SSH, Telnet, ...**. Let's have an general protocol analysis: 

![image](https://user-images.githubusercontent.com/48288606/163670305-233bf82f-b794-4111-b0f7-778fcbf805f7.png)

As the image shown, **Telnet** was used to transfer data (Address Resolution Protocol - ARP, Internet Control Message Protocol - ICMP, ... we don't care about this protocol, this does nothing with data transfer process) 

Filter syntax: `telnet`. Then choose first packet, follow this **Telnet** stream and watch it content:

![image](https://user-images.githubusercontent.com/48288606/163670479-abdeb673-18ea-4483-8a8f-6639663c79e9.png)

"Stranger" has move (**cd**) to `/tmp/` and read **flag.txt**. The output is decoded with base64, which is `Z2lnZW17ZDBudF91czNfdDNsbmV0X2V2M3J9Cg==`. 

Decode with base64 command:

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/163670608-55622597-0601-468f-9065-81ec57368b1c.png"></p>

Flag: **gigem{d0nt_us3_t3lnet_ev3r}**
