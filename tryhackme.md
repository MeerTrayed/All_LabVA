Nmap -sC -sV  10.49.129.47

 
There apache(web):  http://10.49.129.47
Just a blog about Arrowverse

Next step, try to check for a hidden directory using:
gobuster dir --url 10.10.104.199 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

Highlighting the text reveals a hidden text. Possibly for username?

 
gobuster dir --url http://10.10.104.199/island  --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 
 
 web 2100 and  Web page Resource for 2100

gobuster dir --url http://10.10.104.199/island/2100 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .ticket 
why -x .ticket:
-x = extension || while .ticket indicates: “Also try each word in the wordlist with .ticket added at the end”
 
 
RTy8yhBQdscx what is decode for this in Google
The string RTy8yhBQdscx is a Base58 encoded 
 
Now we already have the username and the password.
Username: vigilante Password: !#th3h00d
Access the FTP 10.49.175.208

Let's check if there's another user
 
Download the file into your computer environment
Cat Leave_me_alone.png
Cat Queen’s_Gambit.png
Cat aa.png


View them, seen Leave_me_alone.png isn’t in the correct file format. It might be a file disguised as a PNG image or hidden text?
 
HexEdit can be used to check and edit the binary header of this file.
Checking and comparing PNG

hexedit Queen\’s_Gambit.png (Press tab)
 
hexedit Leave_me_alone.png

notice how Leave_me_alone.png binaries are different. Let's try to change the Leave_me_alone.png binary to .PNG (Copy from Queen's_Gambit.png
89 50 4E 47 0D 0A


The image is now able to be viewed.
Steghide in general, hide or extract secret data inside images. It can be used here to reveal what is actually inside aa.jpg.
-sf actually for extracting hidden data inside image for steghide


Now we can extract the .zip file and read it:

shado contains the password for slade
M3tahuman

ssh slade@10.10.104.199
password:M3tahuman

now time to check and views the directory 
ls -a

cat user.txt
containing the flag for the user
THM{P30P7E_K33P_53CRET5__C0MPUT3R5_D0N'T}

Now, to access the root user, upon doing sudo -l, it reveals this
Why sudo -l?
which shows what commands you’re allowed to run as another user (usually root) without needing full root access.
What it reveals:
1. Which commands you can run with sudo
2. Whether you need a password or not (NOPASSWD)
3. Which user you can run commands as (root or other




sudo pkexec /bin/bash
Got the root user, read the file
boom root flag
THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D}

 






