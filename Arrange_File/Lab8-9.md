# Enumeration
ALL 10 Challenge pick<br>

## Challenge 1 (1)
Netbious Enumeration (Window)<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20215555.png)

## Challenge 2 (2)
Fast nmap scan<br>
Window<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20225157.png)

Linux<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20215807.png)

## Challenge 6 (3)
Anonymous LDAP Query<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20220349.png)
This mean it isn't allowed or it doesnt have it

## Challenge 9 (4)
FTP Banner<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20220507.png)

## Challenge 10 (5)
Anonymous FTP Login<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20220621.png)

## Challenge 11 (6)
SMB NSE Enumeration<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20220848.png)

## Challenge 12 (7)
Enum4linux
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20220900.png)
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20221427.png)
1. enum4linux output:

[+] Server 192.168.56.104 allows sessions using username '', password ''

This confirms the server allows Null Sessions. Without providing any username or password, you successfully extracted the entire user list, the domain SID, the internal password complexity policy, and the SMB share names.

2. Valid Usernames Discovered
Your Nmap and enum4linux outputs leaked several active user accounts. The most critical ones to take note of are:

msfadmin: This is the default administrator account for Metasploitable 2. (Hint: Its password is also msfadmin).

user: A standard account with the full name just a user.
root: The ultimate Linux administrative account.

3. Exposed SMB Shares (With Read Access)
In the Share Enumeration section, we see several network shares hosted via Samba:
- print$ (Printer Drivers)
- opt
- tmp (Commented as "oh noes!")

When enum4linux attempted to map them, it found:

`//192.168.56.104/tmp  Mapping: OK Listing: OK Writing: N/A`

The /tmp directory share is readable by anyone without authentication. You can easily connect to this share from Kali to look for sensitive leftover files.

4. Vulnerable Software Version Detected
Your enum4linux scan pulled the exact version of the file-sharing service running on the box:<br>
**Samba 3.0.20-Debian**

## Challenge 16 (8)
Version Detection
Linux<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20225010.png)

Window<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20224951.png)

## Challenge 17 (9)
OS Detection<br>
Window<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20224305.png)

Linux<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/c7399cc21f2d7e50614c4091bd3e72276bdd0313/ImageGit/Lab8-9/Screenshot%202026-06-07%20224256.png)

## Challenge 4 : TTL OS Fingerprinting (10)
DNS Cache Snooping<br>
![linkimg](https://github.com/MeerTrayed/All_LabVA/blob/58c55164afa208c30ac2fb65ea6681750aae69e0/ImageGit/Lab8-9/Screenshot%202026-06-07%20233813.png)
