Nmap -sC -sV  10.49.129.47
 

There apache(web):  http://10.49.129.47
just a blog about Arrowverse
gobuster dir --url 10.10.104.199 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 
 
gobuster dir --url http://10.10.104.199/island  --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 
 
Page Resource
 



gobuster dir --url http://10.10.104.199/island/2100 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .ticket
 
 
RTy8yhBQdscx what is decode for this search google
The string RTy8yhBQdscx is a Base58 encoded 
 
Now we already have username and the password.
Username: vigilante Password: !#th3h00d
Access the FTP 10.49.175.208
 Other user
 
Download the file
Cat Leave_me_alone.png
Cat Queen’s_Gambit.png
Cat aa.png








View them, seen Leave_me_alone.png isn’t in a correct file format. It might be a file disguise an an png image format
 
HexEdit can be used to check and edit the magic header of this file.
Compare between png format 
hexedit Queen\’s_Gambit.png (Press tab)
 
hexedit Leave_me_alone.png
 
It is now possible to view the image, which reveals a password.
At this point I recalled the CTF mentioned the use of steganography - the practice of concealing a file/image etc within another file/image etc.
Using steghide we can try and extract hidden data from the other image files we downloaded:
 
 






