# What's the Difference

**Author**: SwitchBlade

I made a mistake while making a writeup for a challenge from MetaCTF 2021. Can you find it?

## Solution:

The title "What's the Difference" gives a clue about the different content when committing codes. There's also a folder `.git`  containing all information that is necessary for the project. So this chall wants us to take insight into repo's info, we could execute command to view these data. 

> NOTE: This task does not need to be handled with **README.md** file

What's inside this ? 

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/163671037-85f58cf2-1ae3-4e4d-961f-5fe311fdae28.png"></p>

See the detail of information stored here in this [site](https://www.tutorialspoint.com/what-is-git-folder-and-why-is-it-hidden#:~:text=The%20.,desired%20version%20of%20the%20code.).<br>
Other reference: https://stackoverflow.com/questions/29217859/what-is-the-git-folder#:~:text=on%20this%20post.-,The%20.,can%20roll%20back%20to%20history.

View commit history: 

```bash
git log .
```

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/163671453-d16aa299-b472-4cb7-a1a4-e2a0b8245b3d.png"></p>

"Whoops wrong flag" ?? Maybe this guy commit our flag to this. Read the **commit** content with _id_object_ is `0b055455560bce16787d2e2a7b0ae36b3ddd2b35`

```bash
git show 0b055455560bce16787d2e2a7b0ae36b3ddd2b35
```

<p align="center"> <img src="https://user-images.githubusercontent.com/48288606/163671495-0651ab29-1509-4119-9062-679f1737ec1a.png"></p>

Flag: **gigem{b3_car3ful_b3for3_y0u_c0mmit}**
