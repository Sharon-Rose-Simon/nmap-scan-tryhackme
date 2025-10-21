# nmap-scan-tryhackme
TryHackMe Nmap port scanning project — 10.10.245.172

**Repository:** nmap-scan-tryhackme  
**Description:** TryHackMe Nmap port scanning project — target IP: 10.10.245.172

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

## 5) Screenshots

# Image 1: ![img 1 - Nmap](https://github.com/user-attachments/assets/585fcd74-139d-4c85-b44a-78ab745a6e4f)


# Image 2: ![img 2 - nmap](https://github.com/user-attachments/assets/e0f22c21-dcd2-4dae-8b96-818079353c19)
