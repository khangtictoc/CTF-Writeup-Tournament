# Hidden Fox

**Point**: 200

I let Firefox save some of my stuff while browsing, it should be written somewhere in it's directory, can you find it? Flag is in two parts.

Author: Pixel#1111

File: [Firefox.zip](Firefox.zip)

## Solution:

We have a Firefox folder. 

> NOTE: There's also a same folder in our computer (if Firefox is installed) with path `%AppData%\Mozilla\Firefox\Profiles`

We should only notice the _Profile_ folder. This is where Firefox stores your bookmarks, passwords and other user data. See more in [Profiles](https://support.mozilla.org/en-US/kb/profiles-where-firefox-stores-user-data). With the challenge's description, we don't really determine what _"some stuff"_ is. And the flag contains 2 segments, I guess these are **browser's password** and **history's browser**. Now, let's find them out !

Passwords is stored in 2 files below:
- key4.db
- logins.json

I try to read the files and retrieve password :

![image](https://user-images.githubusercontent.com/48288606/163697438-64a53622-f7cf-4df4-afc6-81e172a4893b.png)

But _"The only way to decrypt logins stored in a logins.json file is to place this logins.json file along with the matching key4.db in a Firefox profile folder and export the logins to CSV."_. According to [account and password from logins.json file](https://support.mozilla.org/en-US/questions/1352064#:~:text=The%20only%20way%20to%20decrypt,export%20the%20logins%20to%20CSV.)

Which means we could **recovery information** of a specific account by these 2 files. Open "Run command" (Window + R) --> Paste `%AppData%\Mozilla\Firefox\Profiles` --> Hit Enter

Copy 2 files `logins.json` and `key4.db` in challenge's folder into this location.

> NOTE: Admin's priviledges may be required and if these files existed, replace it ! Open _Firefox_ and move to `about:logins` URL:


<p align="center"><img width=600 height=450 src="https://user-images.githubusercontent.com/48288606/163697628-293a2875-54ad-4f04-bb2d-1d758d9721d1.png"></p>

We have the first fragment: `dctf{1_b00km4rk3d_`.

Now with this fragment, we change our direction a little bit, they say something about **bookmarks** , i found this info (in the Profile's files link above)

"**places.sqlite **<br>
This file contains all your Firefox bookmarks and lists of all the files you've downloaded and websites you’ve visited"

This file is SQLite format, let's retrieve the data from this. Use sqlite3 Linux command: 

```bash
┌──(virus㉿virus)-[~/Desktop]
└─$ sqlite3 places.sqlite
SQLite version 3.38.2 2022-03-26 13:51:10
Enter ".help" for usage hints.
```

All the worth-mentioning colunmns are listed [here](http://kb.mozillazine.org/Places.sqlite). Try getting information from each column with `select * from {column_name}`

The right columns is `moz_places`:

```
sqlite> select * from moz_places;
1|https://support.mozilla.org/products/firefox||gro.allizom.troppus.|0|0|0|140||bew1ljtsvWMG|1|47358327123126||||1
2|https://support.mozilla.org/kb/customize-firefox-controls-buttons-and-toolbars?utm_source=firefox-browser&utm_medium=default-bookmarks&utm_campaign=customize||gro.allizom.troppus.|0|0|0|140||2-8jSXGE10oO|1|47359956450016||||1
3|https://www.mozilla.org/contribute/||gro.allizom.www.|0|0|0|140||P9_q5kTlvFJo|1|47357364218428||||2
4|https://www.mozilla.org/about/||gro.allizom.www.|0|0|0|140||5QcP8AsXsadx|1|47357608426557||||2
5|https://www.mozilla.org/firefox/central/||gro.allizom.www.|0|0|0|140||G9hmLxo6sCFe|1|47359969280417||||2
6|about:blank||.|0|0|0|0||ymJwHGBAObVu|0|175532304468422||||3
7|http://dctf.dragonsec.si/||is.cesnogard.ftcd.|0|0|0|140||ktppGpUqRORF|0|125510471171359||||4
8|http://_th15_p455w0rd}/||}dr0w554p_51ht_.|0|0|0|140||Pwebe5bDioa9|3|125507539440179||||5
```

The second fragment is: `_th15_p455w0rd}` 

> NOTE: At the time i  find out second flag, i didn't realize this. I dump all data from every **SQLite** files (that i thought they're useful) which are enumerated [here](https://support.mozilla.org/en-US/kb/profiles-where-firefox-stores-user-data). In this case, we may encounter some broken flags, which is not the true one like `4nd_v151t3d_` , `RK4Y3_JaZwGO`, ... 

Full flag: **dctf{1_b00km4rk3d__th15_p455w0rd}**
