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
![LinkImage]()
