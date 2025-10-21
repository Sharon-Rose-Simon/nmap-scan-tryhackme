
cat nmap-results.txt
# Nmap 7.80 scan initiated Tue Oct 21 22:49:00 2025 as: nmap -v -sV -sC -Pn -p 21,53,80,135,3389,5357 -oN nmap-results.txt 10.10.245.172
mass_dns: warning: Unable to open /etc/resolv.conf. Try using --system-dns or specify valid servers with --dns-servers
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 10.10.245.172
Host is up (0.00032s latency).
Scanned at 2025-10-21 22:49:01 BST for 173s

PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           FileZilla ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
| ssl-date: 
|_  ERROR: Unable to obtain data from the target
53/tcp   open  domain?
| fingerprint-strings: 
|   DNSVersionBindReqTCP: 
|     version
|_    bind
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
135/tcp  open  msrpc         Microsoft Windows RPC
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: WIN-SCAN
|   NetBIOS_Domain_Name: WIN-SCAN
|   NetBIOS_Computer_Name: WIN-SCAN
|   DNS_Domain_Name: win-scan
|   DNS_Computer_Name: win-scan
|   Product_Version: 10.0.17763
|_  System_Time: 2025-10-21T21:51:22+00:00
| ssl-cert: Subject: commonName=win-scan
| Issuer: commonName=win-scan
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2025-09-07T17:57:36
| Not valid after:  2026-03-09T17:57:36
| MD5:   4b18 84ea c1c3 553e afe9 b327 e845 8f06
|_SHA-1: a29f d0f4 4b92 08b5 d1ef 3762 7bc3 a67e 261f f745
|_ssl-date: 2025-10-21T21:51:53+00:00; 0s from scanner time.
5357/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.80%I=7%D=10/21%Time=68F7FFD8%P=x86_64-pc-linux-gnu%r(DNS
SF:VersionBindReqTCP,20,"\0\x1e\0\x06\x81\x04\0\x01\0\0\0\0\0\0\x07version
SF:\x04bind\0\0\x10\0\x03");
MAC Address: 02:DF:89:C4:9D:FB (Unknown)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| nbstat: NetBIOS name: WIN-SCAN, NetBIOS user: <unknown>, NetBIOS MAC: 02:df:89:c4:9d:fb (unknown)
| Names:
|   WIN-SCAN<20>         Flags: <unique><active>
|   WIN-SCAN<00>         Flags: <unique><active>
|_  WORKGROUP<00>        Flags: <group><active>

Read from /usr/bin/../share/nmap: nmap-mac-prefixes nmap-payloads nmap-service-probes nmap-services.
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Oct 21 22:51:54 2025 -- 1 IP address (1 host up) scanned in 173.74 seconds

## Commands used
`nmap -v -sV -sC -Pn -p 21,53,80,135,3389,5357 10.10.245.172 -oN nmap-results.txt`  
(Raw full output saved in `nmap-results.txt`)

## Interpretation / Risks
- FTP (21) — FileZilla FTP is running and **anonymous login is allowed**. Risk: potential data exposure and credential leakage; FTP is unencrypted.  
- HTTP (80) — Microsoft IIS 10.0 is serving HTTP and allows the `TRACE` method (a potential information‑disclosure risk). No HTTPS observed.  
- RDP (3389) — Remote Desktop is exposed. High risk: attackers commonly target RDP for unauthorized access and lateral movement. Nmap captured NTLM info showing Windows build `10.0.17763`.  
- Other services (DNS 53, MSRPC 135, HTTPAPI 5357) may reveal further attack surface and should be examined/patched.

# Recommendations (prioritised)
1. Restrict RDP (3389)** — block direct access; require VPN or a jump host; enable Network Level Authentication (NLA) and multi‑factor authentication (MFA); enforce strong passwords and account lockout policies.
2. Disable anonymous FTP / use encrypted transfer** — turn off anonymous login or replace FTP with SFTP/FTPS; restrict FTP access to trusted IPs and enable logging.
3. Harden the web server (IIS)** — disable risky HTTP methods (e.g., TRACE), enable HTTPS with a valid certificate and secure TLS settings, and keep IIS and web applications up to date.
4. Network controls & monitoring** — implement firewall rules to limit exposure, enable logging/monitoring for high‑risk ports, and re‑scan after remediation.

## Conclusion
The lab host exposes several Windows services (FTP, IIS, RPC, RDP) that increase attack surface — RDP and anonymous FTP are highest priority to secure. Full scan output is provided in `nmap-results.txt` and screenshots are in `screenshots/`.
