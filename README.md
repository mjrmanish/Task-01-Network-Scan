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



Interview Questions


  1. What is an open port?

    Ans. -> An open port is a network port on a device or server that is actively listening for incoming connections from other devices.
            Example:
              Port 80 open → means a web server (HTTP) is running and ready to serve web pages.
              Port 22 open → means SSH is available for remote login.
            Security Note:
                       An open port can be useful, but if it’s not properly secured, attackers can try to exploit the service running behind it.   

  2. How does Nmap perform a TCP SYN scan?

    Ans. -> Nmap performs a TCP SYN scan (also called a “half-open” scan) by sending only the first part of the TCP handshake, then stopping before a full connection is made.

       how it works step-by-step:

         1. Send SYN Packet → Nmap sends a TCP SYN packet to the target port (this is the “hello” in TCP handshake).
         
         2. Check Response:

                 SYN-ACK received → The port is open (service is listening).

                 RST received → The port is closed (no service listening).

                 No response / ICMP error → The port is filtered (blocked by firewall).

          3. Send RST → If the port is open, instead of sending an ACK to complete the handshake, Nmap sends a RST (reset) packet to close the connection immediately.

  3. What risks are associated with open ports?

    Ans. -> Open ports can create several security risks, especially if the services running behind them are misconfigured, outdated, or not needed.

          1. Unauthorized Access
          2. Exploitation of Vulnerabilities 
          3. Information Leakage
          4. Malware/Ransomware Delivery
          5. Denial-of-Service (DoS) Attacks

  4. Explain the difference between TCP and UDP scanning.

 | Feature              | TCP Scanning                                                                                                       | UDP Scanning                                                                                    |
| -------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **Protocol Type**    | Connection-oriented                                                                                                | Connectionless                                                                                  |
| **How It Works**     | Sends TCP packets (like SYN in SYN scan) and checks responses to determine if a port is open, closed, or filtered. | Sends UDP packets to a port and waits for a response or ICMP error message to determine status. |
| **Speed**            | Generally faster                                                                                                   | Slower (because many UDP ports give no response if open)                                        |
| **Reliability**      | More reliable – TCP handshakes give clear status                                                                   | Less reliable – no response could mean “open” or “filtered”                                     |
| **Common Use Cases** | Finding web servers, SSH, RDP, etc.                                                                                | Finding DNS, SNMP, TFTP, and other UDP services                                                 |
| **Example Command**  | `nmap -sS 192.168.1.1`                                                                                             | `nmap -sU 192.168.1.1`                                                                          |


 
   5. How can open ports be secured?

     Ans. ->
           How to secure open ports:

               Close Unused Ports – Disable services you don’t need so their ports are no longer listening.
               Use a Firewall – Restrict which IP addresses can access certain ports.
               Enable Encryption – Use secure protocols (e.g., HTTPS instead of HTTP, SSH instead of Telnet).
               Strong Authentication – Use strong, unique passwords or key-based login for services like SSH or RDP.
               Regular Updates – Keep software and operating systems patched to fix known vulnerabilities.
               Port Knocking / VPN Access – Hide critical services behind VPN or use port knocking to make them accessible only after a secret trigger.
               Monitor and Log Access – Keep logs and monitor for unusual activity on open ports.
     Example:
         If you must keep port 22 (SSH) open, restrict it to specific IPs, use key authentication, and disable password logins.

   6. What is a firewall's role regarding ports?

    Ans. -> A firewall controls which network traffic is allowed in or out of a device or network based on rules, including rules for specific ports.

   7. What is a port scan and why do attackers perform it?

    Ans. -> A port scan is the process of sending network requests to a range of ports on a target device to find out which ones are open, closed, or filtered.
           Why attackers perform it:
                Reconnaissance –> To gather information about what services and applications are running on a target.

                Identify Vulnerabilities –> Open ports can reveal exploitable services.

                Map the Network –> Helps attackers understand the network layout and active hosts.

                Plan Attacks –> Knowing which services are exposed allows attackers to choose specific exploits

   8.How does Wireshark complement port scanning?

    Ans. -> Wireshark complements port scanning by letting you see the actual network packets exchanged during the scan, which helps in analysis and troubleshooting.


    
Note:
For privacy and security reasons, I have masked or omitted real IP addresses and host-specific details from the scan results. This is done to protect my local network and follow responsible disclosure practices, while still demonstrating understanding of the task.
