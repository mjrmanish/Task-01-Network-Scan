# Cybersecurity Internship - Task 1  
## 🔍 Nmap Port Scanning in Local Network

### 🧠 Objective:
To scan the local network and identify devices with open ports, helping understand the exposure of services running on the network.

---

### 🛠️ Tools Used:
- **Nmap**: For network scanning and port discovery.
- **Wireshark (optional)**: For packet-level analysis.

---

### 📶 Steps Performed:

1. **Installed Nmap**
2. **Found local IP range** using:
   - 'ipconfig' (Windows)
     
3. Ran Nmap SYN scan:

       nmap -sS 192.168.1.0/24
   
5. Open Ports Identified:

| Port | Protocol | Common Service    |
| ---- | -------- | ----------------- |
| 22   | TCP      | SSH               |
| 80   | TCP      | HTTP              |
| 443  | TCP      | HTTPS             |
| 139  | TCP      | NetBIOS (Windows) |
| 3389 | TCP      | Remote Desktop    |

✅6. Common Services Running on Those Ports:


| Port | Protocol | Common Service       | Description                                                              |
| ---- | -------- | -------------------- | ------------------------------------------------------------------------ |
| 22   | TCP      | SSH (Secure Shell)   | Remote command-line access to servers; encrypted. Used by system admins. |
| 80   | TCP      | HTTP                 | Unsecured web traffic; used by websites that don’t use encryption.       |
| 443  | TCP      | HTTPS                | Secure version of HTTP; uses SSL/TLS encryption.                         |
| 139  | TCP      | NetBIOS              | Used in Windows file/printer sharing (SMB over NetBIOS).                 |
| 3389 | TCP      | RDP (Remote Desktop) | Allows remote graphical desktop access to Windows machines.              |


7. Potential Security Risks from These Open Ports:

 | Port              | Common Risks                                                                            | Recommendations                                                                     |
| ----------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **22 (SSH)**      | Brute-force attacks; if default username/password used, attackers can get shell access. | Use strong passwords or key-based authentication; restrict IPs with firewall.       |
| **80 (HTTP)**     | Transmits data in **plaintext** — can be intercepted (e.g., passwords, cookies).        | Redirect to HTTPS; don’t expose sensitive web apps over HTTP.                       |
| **443 (HTTPS)**   | Generally secure, but misconfigurations (e.g., outdated TLS versions) can be exploited. | Keep SSL/TLS updated; disable weak ciphers. Use valid certificates.                 |
| **139 (NetBIOS)** | Vulnerable to SMB-related exploits like **EternalBlue**; common in ransomware attacks.  | Disable if not needed; block on public-facing networks.                             |
| **3389 (RDP)**    | Frequent target for brute-force & ransomware attacks (like BlueKeep vulnerability).     | Use VPN + strong credentials; enable account lockout; restrict access via firewall. |


💾 8. Save Scan Results as .txt or .HTML File

   Text file:

    nmap -sS 192.168.1.0/24 -oN scanresult.txt

   HTML:

    nmap -sS 192.168.1.0/24 -oX scanresult.xml
