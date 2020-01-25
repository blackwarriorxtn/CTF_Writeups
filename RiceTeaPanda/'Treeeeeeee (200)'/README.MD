# CTF riceteacatpanda.wtf – Challenge Treeeee

* **Category:** General Skills 
* **Points:** 200

## Challenge

> It appears that my cat has gotten itself stuck in a tree... It's really tall and I can't seem to reach it. Maybe you can throw a snake at the tree to find it?
Oh, you want to know what my cat looks like? I put a picture in the hints.


## Solution
the first thing that came to my mind is tree command whether it is in linux or windows , the tree  is a recursive directory listing program  that  produces  a  depth  indented
listing of files ! 
so after extracting the compressed file given you will notice many folders like at least 1337 folders !
by doing tree you will encounter some jpg files 
if you search for images only u will find like 1300 images. A quick look at the images shows that there are two images that are cloned.
almost all the images are the same so i guess we have to find a different one , we can find that unique image by its size using ls and grepping through the size

lets find that image by doing find ./ -name ENP92.jpg and we can open it with eog later


```
The flag : RTCP{MEOW_SHARP_PIDGION_RICE_TREE}
```
