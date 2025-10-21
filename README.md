# nmap-scan-tryhackme
TryHackMe Nmap port scanning project — 10.10.245.172

## 1) Purpose: 
Practiced network discovery and port enumeration with nmap. 

## 2) What I did: 
- Performed quick and detailed Nmap scans on the target host.
- Analyzed service/version information and NSE script results.
- Documented findings and suggested mitigations in `report.md`

## 3) Commands used: 
- `nmap 10.10.245.172`
- `nmap -v -sV -sC -Pn -p 21,53,80,135,3389,5357 10.10.245.172 -oN nmap-results.txt`
- `cat nmap-results.txt`

## 4) Files in this repo: 
- nmap-results.txt` — raw scan output  
- `screenshots/` — terminal screenshots

## 5) What I learned
- How to enumerate services with Nmap and interpret service/version output.
