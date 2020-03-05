---
layout: post
title: AeroCTF - DrawingOnTheWalls
subtitle: Dumping Paints from memory
comments: false
---

* **Category:** Forensics
* **Points:** 100

## Challenge

> My friend started having problems with his head and he began to draw some nonsense on the walls.

Can you make out these notes?

https://mega.nz/#!WJ4mGaBB!tW9Ls1Zlx-LBhUiEqVfWajUqTy9UT5lJk44jYqvBx_w


## Solution

so we start by doing our usual thing with volatility 
```  $volatility -f memory.dmp imageinfo 
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
WARNING : volatility.debug    : Alignment of WindowsCrashDumpSpace64 is too small, plugins will be extremely slow
```
volatility wasnt able to determine the profile so we have to manually suggest and lets assume its a Win7SP1x64
now we can dump the process list 
but why ? we need to check the running process to find out where the notes are saved or what process was used to take the notes !

so we can just do : 

```$volatility -f memory.dmp --profile=Win7SP1x64 pslist  ```
![Alt text](https://github.com/blackwarriorxtn/CTF_Writeups/blob/master/AeroCTF/Forensics/DrawingOnWalls/pstree.png?raw=true)
next step is to dump the memory of the process "mspaint.exe" 
why ? its very obvious since the challenge was talking about drawings .
so we might find something by dumping that, and we can pass it to gimp so we can view the raw bytes as an image 
and in order to view the raw data with gimp we need to change the extension to .data or it wont work 
there is different pids of the mspaint and we will get to that later but we can just choose anyone  for now !
``` 
$mkdir dump  
$volatility -f memory.dmp  --profile=Win7SP1x64 memdump -p 2804 --dump-dir dump/ 
$mv 2804.dmp 2804.data 
$gimp 2804.data
```
now we have to play with the width and height to make the flag clear 
![Alt text](https://github.com/blackwarriorxtn/CTF_Writeups/blob/master/AeroCTF/Forensics/DrawingOnWalls/gimp1.png?raw=true)
after doing that we can just flip vertically the whole image to reverse back the flag
![Alt text](https://github.com/blackwarriorxtn/CTF_Writeups/blob/master/AeroCTF/Forensics/DrawingOnWalls/gimp2.png?raw=true)
but thats just the part of the flag ! why ? seems like  multiple mspaints were running and in each window a part of the flag was drawn
so we have to do the same thing for each pid till we get all the flags 
