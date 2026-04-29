# tryhackme Lian Yu
 ### Note the ip changes in the images because I use other accountr timers sorry for inconvenience
 Start with a scan:
`Nmap -sC -sV  10.49.129.47`<br>
![img alt]()
 
There apache(web):  _http://10.49.129.47_<br>
Just a blog about Arrowverse
Next step, try to check for a hidden directory using:<br>
`gobuster dir --url 10.10.104.199 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`<br>
![img alt]()<br>
![img alt]()

Highlighting the text reveals a hidden text. Possibly for username?<br>

 
`gobuster dir --url http://10.10.104.199/island  --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`<br>
 ![img alt]()
 
Web 2100 and  Web page Resource for 2100<br>
 ![img alt]()<br>
`gobuster dir --url http://10.10.104.199/island/2100 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .ticket `<br>
why -x .ticket:<br>
***-x = extension || while .ticket indicates: “Also try each word in the wordlist with .ticket added at the end”***<br>
 ![img alt]()<br>
 
 
**RTy8yhBQdscx** what is decode for this in Google, The string RTy8yhBQdscx is a **Base58** encoded <br>
![img alt]()<br>
Now we already have the username and the password.<br>
Username: **vigilante** Password: **!#th3h00d** <br>
Access the `ftp 10.49.175.208`<br>
![img alt]()<br>

Let's check if there's another user<br>
![img alt]()<br>

Download the file into your computer environment.
```
Cat Leave_me_alone.png
Cat Queen’s_Gambit.png
Cat aa.png
```
<br>
View them, seen Leave_me_alone.png isn’t in the correct file format. might it be a file disguised as a PNG image or hidden text?<br>
![img alt]()<br/>
HexEdit can be used to check and edit the binary header of this file.<br/>
Checking and comparing PNG:

`hexedit Queen\’s_Gambit.png` (Press tab)<br>
 ![img alt]()<br/>
`hexedit Leave_me_alone.png`<br>
 ![img alt]()<br/>
 
Notice how Leave_me_alone.png binaries are different from Queen's_Gambint.png even they are the same format?.
Let's try to change the Leave_me_alone.png binary to .PNG (Copy from Queen's_Gambit.png)<br/>
89 50 4E 47 0D 0A


The image is now able to be viewed.<br/>
![img alt]()<br/>
Steghide in general, hide or extract secret data inside images. It can be used here to reveal what is actually inside aa.jpg.
-sf actually for extracting hidden data inside image for steghide<br/>
Now we can extract the .zip file and read it:<br>
![img alt]()<br/>
shado contains the password for slade
**M3tahuman**<br/>

`ssh slade@10.10.104.199`<br/>
password: M3tahuman<br>
now time to check and views the directory <br/>
`ls -a`<br/>
` user.txt` <br/>
containing the flag for the user<br/>
![img alt]()<br/>

Now, to access the root user, upon doing sudo -l, it reveals this<br/>
Why sudo -l , which shows what commands you’re allowed to run as another user (usually root) without needing full root access.<br>
What it reveals:
1. Which commands can you run with sudo
2. Whether you need a password or not (NOPASSWD)
3. Which user can you run commands as (root or other)<br>

reveal /usr/bin/pkexec with permissions like -rwsr-xr-x which indicates the SUID (Set User ID) bit is enabled. This means that whenever any user executes pkexec, it runs with the privileges of the file owner, which is root, instead of the current user. The program pkexec is part of Polkit and is designed to allow users to execute commands as another user, typically root, after proper authentication<br>
![img alt]()<br/>


sudo pkexec /bin/bash<br>
Got the root user, read the file<br>
boom root flag<br>
![img alt]()<br/>
 






