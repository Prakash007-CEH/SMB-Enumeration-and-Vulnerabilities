## SMB-Lab-Setup-and-Basics
This repository demonstrates a hands-on SMB lab setup and basic SMB access testing using Kali Linux and Windows virtual machines.


## What is SMB?

SMB (Server Message Block):
A network protocol used to share files, folders, printers, and services between computers—mainly in Windows networks.

SMB Vulnerability:
Security weaknesses in SMB (like misconfigurations, weak authentication, or outdated versions) that attackers can exploit to gain unauthorized access, steal data, or execute remote code.

## 🧰 Tools Used

- Kali Linux
- Windows 10/11
- VirtualBox
- SMB Protocol
- Windows File Sharing

## 🔍 SMB Enumeration (Overview)

This repository focuses on lab setup and SMB access validation.
Enumeration techniques are intentionally not included in this project.


# 💻 Lab Setup

## ⭐ 💡 Best Beginner Setup (ONLY ONE LAPTOP NEEDED)

You will use:

1️⃣ Kali Linux VM (attacker)

2️⃣ Windows 10/11 VM (target)

Both run on the same laptop using VirtualBox.

## ⭐ STEP 1 — Create a Windows VM (Target Machine)

In VirtualBox:

New → Windows 11

RAM: 3–4 GB

Disk: 40 GB

Install Windows normally

After install:

Go to:

Control Panel →

Network and Sharing Center →

Advanced Sharing Settings →

Turn ON these:

✔ Network discovery

✔ File and printer sharing

<img width="500" height="394" alt="Screenshot 2025-12-15 103804" src="https://github.com/user-attachments/assets/0fd2ac07-0536-4b60-8ae8-3df10cb49f4f" />

Windows is now ready to share files using SMB.


## ⭐ STEP 2 — Put Both VMs on Same Network

VirtualBox →
Select Kali VM → Settings → Network →

➡️ Host-only Adapter

<img width="568" height="390" alt="Screenshot 2025-12-15 104238" src="https://github.com/user-attachments/assets/d07c0eb8-d401-479d-901b-da22adf91046" />
<img width="570" height="394" alt="Screenshot 2025-12-15 104255" src="https://github.com/user-attachments/assets/d52b41f6-ae92-4b70-8602-a3c6a7b54912" />

Now both VMs are connected to the same isolated host-only network.

## ⭐ STEP 3 — Get Windows VM IP

Inside Windows VM, open CMD: 

Type: `ipconfig`

<img width="587" height="365" alt="Screenshot 2025-12-15 201226" src="https://github.com/user-attachments/assets/b612e978-aa11-4094-b8dc-9eb6de793304" />

IP Address: 192.168.56.101


## ⭐ STEP 4 — Create a Shared Folder in Windows VM

Make a folder → right-click → Properties → Sharing → Share → Everyone.

Done.

Shared folder name used in this lab: sharetest


## ⭐ STEP 5: Test SMB
In Kali

File Manager → Ctrl + L


Enter: `smb://192.168.56.101`

Username → Windows username

Password → Windows password


✔ Folder should open now.

<img width="508" height="371" alt="Screenshot 2025-12-15 203850" src="https://github.com/user-attachments/assets/aaa29682-e45b-4808-b2ae-e27e1f733c69" />

Now Folder is open in Kali:

<img width="410" height="342" alt="Screenshot 2025-12-15 205416" src="https://github.com/user-attachments/assets/cbfe6bf0-7c18-4bf0-b633-a6a2b89e8be4" />
<img width="449" height="285" alt="Screenshot 2025-12-15 205527" src="https://github.com/user-attachments/assets/6c939774-1a4e-4426-88b4-c3fa1f3893e2" />

## Now using Kali terminal.

CONNECT TO SMB AGAIN

On Kali Terminal: `smbclient //192.168.56.101/sharetest -U Hackerr -m SMB1`

You should see: `smb: \>`

<img width="407" height="212" alt="Screenshot 2025-12-16 124330" src="https://github.com/user-attachments/assets/9bccb869-14d4-4dcc-a450-89367ddd987f" />

 ## Note: SMB1 is used here to avoid SMB2/SMB3 negotiation issues in lab environments.
SMB1 is insecure and should never be enabled on production systems.


## CREATE A PERSISTENCE MARKER FILE

Exit smb session for a moment: `exit`

Now on Kali terminal:

` echo "SMB persistence marker - lab test" > persistence.txt` 

Check: 

`cat persistence.txt`

<img width="497" height="200" alt="Screenshot 2025-12-16 161159" src="https://github.com/user-attachments/assets/e91e2089-e20e-49c6-b6ae-57d93c4501db" />


## UPLOAD MARKER TO WINDOWS

Reconnect to SMB:
`smbclient //192.168.56.101/sharetest -U Hackerr -m SMB1`

Inside smb: 

`put persistence.txt`

You should see the file:

`putting file persistence.txt`

<img width="475" height="239" alt="Screenshot 2025-12-16 125219" src="https://github.com/user-attachments/assets/e1333fb7-a4e1-49dc-a863-efe81142167c" />

## VERIFY FROM WINDOWS (VERY IMPORTANT)
On Windows VM:

1. Open shared folder

2. You should see:
 file name: persistence.txt


3. Open it → text is visible

<img width="439" height="289" alt="Screenshot 2025-12-16 125712" src="https://github.com/user-attachments/assets/deb5d3b5-bf9a-454d-a0cb-e0740ac82dc3" />

## 🎯 Persistence confirmed

## ✅ Conclusion

This repository demonstrates a hands-on SMB lab setup using Kali Linux and Windows virtual machines to understand how SMB works in real-world environments.

The lab highlights how improper SMB configurations can introduce security risks and serves as a foundation for SMB access testing in controlled environments.

This project is intended for students and beginners in ethical hacking and cybersecurity labs.



## 🛡️ Security Note & Disclaimer


⚠️ This repository is strictly for educational and ethical purposes only.

All testing was performed in a self-owned lab environment using virtual machines.
Do NOT test SMB vulnerabilities on real systems or networks without explicit permission, as it may be illegal and unethical.

The author is not responsible for misuse of the techniques demonstrated here.
