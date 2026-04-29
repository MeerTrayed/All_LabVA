# tryhackme Lian Yu
 ### Note the ip changes in the images because I use other accounts' timers. Sorry for the inconvenience
 Start with a scan:
`Nmap -sC -sV  10.49.129.47`<br>
This picture shows ssh and ftp service is existed in this IP.
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/nmap2.png)
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/nmap3.png)

 
There apache(web):  _http://10.49.129.47_<br/>
Just a blog about Arrowverse

gobuster discover hidden directories and files on a web server. When you visit a website normally, you only see pages that are linked in the UI, but many servers contain unlisted or hidden paths
Next step, try to check for a hidden directory using:<br>
`gobuster dir --url 10.10.104.199 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/0eabbfdd942e12580481d5c9cd0ca9c72ac1169d/ImageGit/Ditbuster1.png)<br>

Highlighting the text reveals a hidden text. Possibly for username?<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/IslandWeb.png)


`gobuster dir --url http://10.10.104.199/island  --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`<br>
 ![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/GobusterIsland.png)
 
Web 2100 and  Web page Resource for 2100, shows that theres something we can search for with .ticket<br>
 ![img alt](https://github.com/MeerTrayed/All_LabVA/blob/f034678e3371d196962df66bb9eb8b8994f2459a/ImageGit/2100SourceCode.png)<br>
`gobuster dir --url http://10.10.104.199/island/2100 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .ticket `<br>

why -x .ticket?<br>
*-x = extension || while .ticket indicates: “Also try each word in the wordlist with .ticket added at the end"*<br>
 ![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/GobusterTicket.png)
 ![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/GreenArrow.png)<br>
 
**RTy8yhBQdscx** what is decode for this in Google, The string RTy8yhBQdscx is a **Base58** encoded <br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/63b16c1703e62baaf077c112b418b45a188e8291/ImageGit/DecodeGreenA.png)<br>

Now we already have the username and the password.<br>
Username: **vigilante** Password: **!#th3h00d** <br>
Access the `ftp 10.49.175.208`<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/FtpVigilante.png)<br>

Let's check if there's another user<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/UserLs.png)<br>

Download the file into your computer environment.
```
Cat Leave_me_alone.png
Cat Queen’s_Gambit.png
Cat aa.png
```
<br>
View them, seen Leave_me_alone.png isn’t in the correct file format. might it be a file disguised as a PNG image or hidden text?<br>

![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/ViewImage.png)<br/>
HexEdit can be used to check and edit the binary header of this file.<br/>
Checking and comparing PNG:

`hexedit Queen\’s_Gambit.png` (Press tab)<br>
 ![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/hexedit1.png)<br/>
 
`hexedit Leave_me_alone.png`<br>
 ![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/hexedit2.png)<br/>
 
Notice how Leave_me_alone.png binaries are different from Queen's_Gambint.png even they are the same format?.
Let's try to change the Leave_me_alone.png binary to .PNG (Copy from Queen's_Gambit.png)<br/>
89 50 4E 47 0D 0A


The image is now able to be viewed.<br/>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/PictureGood.png)<br/>

Steghide in general, hide or extract secret data inside images. It can be used here to reveal what is actually inside aa.jpg.
-sf actually for extracting hidden data inside image for steghide<br/>

Now we can extract the .zip file and read it:<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/9b4b11b09108ab27fc7e36227e03377d8fa7675c/ImageGit/TimeForaa.png)<br/>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/aea2e37fea30ca2d422ae746c4eccf37186e2a1e/ImageGit/viewzip.png)<br/>
shado contains the password for slade
**M3tahuman**<br/>
`ssh slade@10.10.104.199`<br/>
password: M3tahuman<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/aea2e37fea30ca2d422ae746c4eccf37186e2a1e/ImageGit/sladeboi.png)><br>
now time to check and views the directory <br/>
`ls -a`<br/>
Found single txt file, time to views it.<br>
`cat user.txt` <br/>
containing the flag for the user<br/>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/aea2e37fea30ca2d422ae746c4eccf37186e2a1e/ImageGit/sladels.png)<br/>

Now, to access the root user, upon doing sudo -l, it reveals this<br/>
Why sudo -l , which shows what commands you’re allowed to run as another user (usually root) without needing full root access.<br>
What it reveals:
1. Which commands can you run with sudo
2. Whether you need a password or not (NOPASSWD)
3. Which user can you run commands as (root or other)<br>

reveal /usr/bin/pkexec with permissions like -rwsr-xr-x which indicates the SUID (Set User ID) bit is enabled. This means that whenever any user executes pkexec, it runs with the privileges of the file owner, which is root, instead of the current user. The program pkexec is part of Polkit and is designed to allow users to execute commands as another user, typically root, after proper authentication<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/aea2e37fea30ca2d422ae746c4eccf37186e2a1e/ImageGit/sudo%20l.png)<br/>


`sudo pkexec /bin/bash<br>`
Got the root user, read the file<br>
boom root flag<br>
![img alt](https://github.com/MeerTrayed/All_LabVA/blob/aea2e37fea30ca2d422ae746c4eccf37186e2a1e/ImageGit/pkexec.png)<br/>
 






