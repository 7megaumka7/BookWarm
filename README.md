# BookWarm



This repository provides a simple automated Bash script (`bh_collecotr.sh`) to install and run  Active Directory enumeration tools: **BloodHound-python**, **RustHound**, and **ldapdomaindump**. The script is designed for red team operators, penetration testers, and advanced defenders seeking to understand or audit AD environments.

## Quick Start

1. **Clone the repository and make the script executable:**
   ```
   git clone 
   cd 
   chmod +x bh_scr.sh
   ```

2. **Run the script as root:**
   ```
   sudo ./bh_scr.sh
   ```

3. **Follow the interactive prompts:**
   - Enter Domain Controller IP (e.g., `192.168.1.10`)
   - Enter Domain Controller hostname (e.g., `DC01.corp.local`)
   - Enter domain FQDN, username, and password

4. **Results:**  
   All output is saved in a timestamped `bloodhound_data_*` directory.

---

## Features

- **Automated Dependency Installation:**  
  Installs Python, Rust, compilers, and all required libraries via `apt` and `pip`.
- **BloodHound-python Integration:**  
  Collects comprehensive AD data (users, groups, ACLs, sessions, trusts, etc.).
- **RustHound Support:**  
  Fast, Rust-based alternative collector with ADCS and FQDN resolver options.
- **ldapdomaindump:**  
  Dumps LDAP structure and objects for blue team and red team analysis.
- **Interactive /etc/hosts Management:**  
  Ensures the DC is resolvable by hostname.
- **Colorized Output:**  
  Progress and errors are clearly color-coded for readability.
- **OPSEC Considerations:**  
  Passwords are not echoed; output is isolated per run.

---

## Usage Example

```
┌──(root㉿kali)-[/home/kali]
└─# sudo ./bh_scr.sh

[+] Updating packages and installing dependencies
[+] Installing required security tools
[+] Network configuration
Enter Domain Controller IP: 192.168.1.10
Enter Domain Controller hostname: DC01.corp.local
[+] Added 192.168.1.10 DC01.corp.local to /etc/hosts

[+] Authentication details
Enter domain name (FQDN): CORP.LOCAL
Enter username: svc_bloodhound
Enter password: ****

[+] Starting Active Directory reconnaissance

[*] Running BloodHound-python...
[*] Running RustHound...
[*] Running ldapdomaindump...

[+] Collection complete. Output saved to: bloodhound_data_20250616_101600
```

All output files (`*.out`, JSON, CSV, ZIP) are stored in the created folder.


## Troubleshooting

- **RustHound Not Found:**  
  If you see `[-] Error: rusthound installation failed!`, ensure `/root/.cargo/bin` is in your PATH:
  ```
  export PATH=$PATH:/root/.cargo/bin
  echo 'export PATH=$PATH:/root/.cargo/bin' >> /root/.bashrc
  source /root/.bashrc
  ```
  Or run RustHound directly:
  ```
  /root/.cargo/bin/rusthound ...
  ```

- **Permission Issues:**  
  Always run as root (especially for package installation and /etc/hosts modification).

- **Proxy/Offline Environments:**  
  Set up appropriate proxy variables for `apt`, `pip`, and `cargo` if behind a proxy.
