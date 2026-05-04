# Vulnerability Analysis Lab - Week 7
## Question 1:
- consists entirely of ICMP (Internet Control Message Protocol) packets.
- Inside the payload, string: U1VDVEYyMDIze2FpX2lzX2Nvb2x9<br/>
![LinkImage]()

- I use this website to identify the Cipher _https://www.boxentriq.com/analysis/cipher-identifier_<br/>
![LinkImage]()

- When decoded: SUCTF2023{ai_is_cool}<br/>
![LinkImage]()

## Question 2:
- Opening the file search for ftp -data <br/>
  = Reason: <br/>
  
| Scenario | Why it's in the ICMP file | Intent |
|--------|---------------------------|--------|
| Network Error | ICMP wraps the original FTP header to report a failure. | Troubleshooting |
| Data Tunneling | FTP content is hidden inside the ICMP payload. | Malicious (Exfiltration) |
| Firewall Block | Router sends"Communication Administratively Prohibited."| Security Policy Audit |

- The file contains a URL: https://tinyurl.com/yr5zprz4
  - Contain pigpen ciper, the zero is a single dot, <br> while the x is double dot.
![LinkImage]()

- Using this website to decipher it https://www.boxentriq.com/alphabets/pigpen-cipher
![LinkImage]()

We got `EXMACHINAAVA`

## Question 3: NMAP OUTPUT ANALYSIS

 1. What can an attacker do with each port?
    | No. | Ports | Service | Attacker Action |
    |--------|-------------|--------|----------|
    | 1 | 21 (FTP) | vsftpd | An attacker can attempt an Anonymous Login, brute force credentials to steal, upload/download files, or gain backdoor access. |
    | 2 | 22 (SSH) | OpenSSH | Primarily used for remote command-line access. Attackers would attempt brute-force weak credentials or look for leaked SSH keys. |
    | 3 | 80(HTTP) | Apache  | Enumerating host information, Web attacks (SQLi, XSS), and master browsers to map the internal network. |
    | 4 | 139/445(SMB) | Windows 7 SP1 | These are the "ultimate target" for lateral movement. An attacker can attempt to enumerate user shares, steal password hashes, or execute remote code. |

    SMB additional note:
    Port 445 is usually the bigger target because it’s the default for modern Windows. However, seeing both open (as in your scan) tells an attacker that the system is likely configured for legacy compatibility, which       often means it's running older, more vulnerable code.
   - Access to Sensitive Data
    Port 445 is the gateway to the "jewels" themselves. It handles file sharing, which means if an attacker breaks in through this port, they gain access to:
        - Financial Records: Spreadsheets, payroll, and tax info.
        - Customer Data: Databases containing names, addresses, and credit card info.  
        - Intellectual Property: Project plans, source code, and internal memos.
  - High-Level Control (The "Master Key")<br/>
     In Windows environments, SMB is deeply tied to Active Directory.  

    If an attacker exploits Port 445, they aren't just a "guest" on the computer. They often gain SYSTEM or Administrator privileges. <br/>
    This is the "master key" to the castle. From here, they can see every other computer on the network, steal more passwords, and eventually take over the entire company network (lateral movement).
  
2. What vulnerabilities are likely present based on the version?
   | Service Version | Vulnerabilities |
   |-----------------|-----------------|
   | vsftpd 2.3.4 | This specific version is famous for a backdoor (CVE-2011-2523). If a user logs in with a username ending in :), a shell opens on port 6200. |
   | Apache 2.2.8 | This version is over a decade old and is susceptible to various Denial of Service (DoS) attacks and potential memory leaks. |
   | OpenSSH 5.3p1 | Weak crypto, User enumeration and Brute-force attacks |
   | Windows 7 SP1(SNB) | This is highly likely to be vulnerable to EternalBlue (CVE-2017-0144), the exploit used in the WannaCry ransomware attacks. |

3. Which one is the highest risk and why?
   Higher risk port 445. While the FTP backdoor is critical, Port 445 on an unpatched Windows 7 machine represents the highest risk because it typically allows for Remote Code Execution (RCE) with SYSTEM privileges. It     requires no user interaction and provides the attacker with total control over the operating system instantly.
     
4. What attack path can be built from this? <br/>
   HTTP -> FTP (backdoor) OR SMB (EternalBlue) → initial access → privilege escalation → pivot to SSH/SMB
   
5. What should be the remediation?
   - Upgrade and patch = Move to a modern OS or apply the MS17-010 patch immediately. Regularly update all software to fix known vulnerabilities.
   - Access control = Use firewalls and network segmentation to limit access to authorized IPs only. Restrict ports like 22, 139, and 445.
   - Disable anonymous and default access = Turn off anonymous FTP login and remove default credentials from all services.
   - Encryption enforcement = Use secure protocols such as HTTPS instead of HTTP and disable weak encryption algorithms in SSH.
   - Monitoring and logging = Enable logging for FTP, SSH, and SMB. Use intrusion detection systems (IDS) to detect suspicious activities.

# Question 4
ttl = time to live | ***Think of the TTL as a countdown timer for a packet.***
### Image 1
| Field | OS | Explanation |
|-----|------|------|
| ttl 64 | Linux, macOS, dan Unix | The reply is exactly 64, the device is likely on your local network (0 hops away). Common for Linux, macOS, and mobile devices (Android/iOS). |

### Image 2
| Field | OS | Explanation |
|-----|------|------|
| ttl 255 | Network Infrastructure | almost exclusively the signature of Network Infrastructure (Mainframes, Cisco Routers and Switches, Solaris/HP-UX).

### Image 3
| Field | OS | Explanation |
|-----|------|------|
| ttl 128 | Microsoft Windows | its default starting value for the TCP/IP stack in the early days of Windows (NT/95) |

# Question 5

