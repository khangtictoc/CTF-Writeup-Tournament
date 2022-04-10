# dns-joke

**Point**: 100

**Description**: A system administrator hasn't smiled in days. Legend has it, there is a DNS joke hidden somewhere in www.jerseyctf.com. Can you help us find it to make our system administrator laugh?

## Solution: 

Just a challenge about DNS enumerations and resolvings. Use `dnsrecon` in Kali Linux:

```bash
dnsrecon -d www.jerseyctf.com
```

<p align=c"center"> <img src="https://user-images.githubusercontent.com/48288606/162598716-4c4c3b1f-230e-4b68-9eb6-bd31b293d98d.png" > </p>

Flag: **jctf{DNS_J0k3s_t@k3_24_hrs}**
