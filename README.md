
````md
# Metasploit-for-reconnaissance

# AIM:

To get introduced to Metasploit Framework and to perform reconnaissance in pentesting.

## DESIGN STEPS:

### Step 1:
Install Kali Linux either in partition or virtual box or in live mode.

### Step 2:
Investigate on the various categories of tools.

### Step 3:
Open terminal and try executing some Kali Linux commands.

---

# EXECUTION STEPS AND ITS OUTPUT:

## PROGRAM:

### Find out the IP address of the attacker's system

Use the following command to identify the IP address of the attacker system.

```bash
ifconfig
````

or

```bash
ip a
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/f53b0ba8-f1d7-4ef8-996e-f483d621920b)

### Observation:

The command displayed the network configuration details of the attacker machine, including the IP address, subnet mask, and network interface details. The IP address was successfully identified for further reconnaissance activities.

---

## Invoke msfconsole

Launch the Metasploit Framework using the following command:

```bash
msfconsole
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/a1185fb2-2e51-4946-b0af-89bb59d0f9f8)

Type `help` or `?` to see the list of all available commands inside msfconsole.

### Observation:

The Metasploit Framework console was launched successfully. It provided an interactive environment for penetration testing and reconnaissance operations.

---

## OUTPUT:

Use the help command inside msfconsole:

```bash
help
```

or

```bash
?
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/faccad26-5e12-41b2-9e73-2ee30b700df3)

### Observation:

The help command displayed the list of available commands and functionalities in Metasploit, helping users understand the framework navigation.

---

## Port Scanning

The following command is executed for scanning the systems on the local area network with a TCP scan (`-sT`) looking for open ports between 1 and 1000 (`-p1-1000`).

```bash
nmap -sT 192.168.181.0/24 -p1-1000
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/9af59f80-3f5d-44b5-9d17-849e543ea7a2)

### Observation:

A TCP connect scan was performed successfully on the local network. Open ports and active hosts were identified, which helped in gathering information about the target systems.

---

## Listing Auxiliary Scanner Modules

Metasploit contains many built-in scanning modules. Navigate to the auxiliary modules directory and list all scanner modules.

```bash
cd /usr/share/metasploit-framework/modules/auxiliary
ls -l
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/6cb480c3-9aff-4437-aa80-201a1a828521)

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/3789786f-7b1e-48c1-822d-6136a90b5eca)

### Observation:

The auxiliary scanner modules available in Metasploit were listed successfully. Different modules for scanning and enumeration purposes were identified.

---

## Searching for Exploit Modules

Search is a powerful command in Metasploit used to locate specific modules.

```bash
search name:Microsoft type:exploit
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/e3454c47-211d-46ff-bb79-44dbe16bf7f1)

### Observation:

The search command displayed Microsoft-related exploit modules, making it easier to find specific exploits based on name and type.

---

## Module Information

The `info` command provides information regarding a selected module or platform.

```bash
info
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/41800261-758b-4f96-a075-d4b52b09cbbd)

### Observation:

Detailed information about the selected module was displayed, including module description, references, options, and target details.

---

## Starting Metasploit Database

Before beginning, start the PostgreSQL server and initialize the Metasploit database.

```bash
systemctl start postgresql
msfdb init
```

### Observation:

The PostgreSQL service started successfully, and the Metasploit database was initialized for storing scan results and reconnaissance information.

---

# MYSQL ENUMERATION

Find the IP address of the Metasploitable machine first. Then, use the `db_nmap` command in msfconsole with Nmap flags to scan the MySQL database running on port 3306.

```bash
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/373e5067-5493-433d-a7d3-31807ab2ee6c)

### Observation:

The MySQL service running on port 3306 was scanned successfully. Service version details and default scripts were executed to gather database information.

---

## Search for MySQL Auxiliary Modules

Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.

```bash
search type:auxiliary mysql
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/3674e541-9567-46dc-b5cf-65951469fbf3)

### Observation:

Various MySQL auxiliary modules were displayed, including modules for login, version detection, and enumeration.

---

## MySQL Version Scanner Module

Use the MySQL version scanner module to gather MySQL version details.

```bash
use auxiliary/scanner/mysql/mysql_version
```

or

```bash
use 11
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/cc1b70e5-42e1-43b6-b2af-af33f1d1d97b)

### Observation:

The MySQL version scanner module was selected successfully and used to detect version information about the target MySQL server.

---

## MySQL Login Brute Force

After scanning, brute force the MySQL root account using Metasploit's login scanner module.

```bash
use auxiliary/scanner/mysql/mysql_login
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/7a4ec53c-038e-41a4-8d38-f166dd8eb8fd)

Set the password wordlist path:

```bash
set PASS_FILE /usr/share/wordlists/rockyou.txt
```

Specify the target IP address:

```bash
set RHOSTS <target_ip_address>
```

Enable blank password testing:

```bash
set BLANK_PASSWORDS true
```

![image](https://github.com/NAVEENKUMAR4325/Metasploit-for-reconnaissance/assets/119479566/873017db-58af-4e5b-b0ec-054cadbe24a5)

### Observation:

The MySQL login module was configured successfully with a password wordlist and target IP address. Blank password testing was enabled to check if the root account had no password.

---

# RESULT:

The Metasploit Framework for reconnaissance was examined successfully. Various reconnaissance activities such as scanning, module searching, MySQL enumeration, and information gathering were performed successfully.

