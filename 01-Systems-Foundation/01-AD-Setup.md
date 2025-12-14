## PRE-REQUISITES (Before Installing AD)
### Installing Windows Server 2022
![00-Install-Winserver](attachments/00-Install-Winserver.png)
### Set a Static IP 
Open PowerShell and type : `ipconfig /all`
![01-PS-IP](attachments/01-PS-IP.png)
- Note your **IPv4 Address**, **Subnet Mask**, and **Default Gateway**.

![02-IP-Conf](attachments/02-IP-Conf.png)
- Note your **IPv4 Address**, **Subnet Mask**, and **Default Gateway**.
- Go to **Control Panel** > **Network and Internet** > **Network Connections**.
- Right-click your adapter > **Properties** > **IPv4** > **Properties**.

Use the IP address of the automatically allocated , and click Ok :
- **IP Address:** `192.168.88.138`
- **Subnet Mask:**  `255.255.255.0`.
- **Gateway:** `192.168.88.2`
- **Preferred DNS Server:** **127.0.0.1** (The DC must point to itself for DNS).
- **Alternate DNS:** `8.8.8.8` (Google, for internet access).

![03-IP-Changed-Conf](attachments/03-IP-Changed-Conf.png)

### Rename the Server
- We change the Computer Name to `DC01`.

![04-DC-Name](attachments/04-DC-Name.png)
## Install & PROMOTE
### Install the AD DS Role
- Click **Manage** (top right) > **Add Roles and Features**.
![alt](attachments/Pasted image 20251214124339.png)

![alt](attachments/Pasted image 20251214124428.png)

![alt](attachments/Pasted image 20251214124446.png)
- On Server Roles : Check **Active Directory Domain Services**. 
![alt](attachments/Pasted image 20251214124606.png)
- Click Add Features.
![alt](attachments/Pasted image 20251214124512.png)
- Click Next all the way to Confirmation.
![alt](attachments/Pasted image 20251214124711.png)
- Install it an wait for the installation to finish.
![alt](attachments/Pasted image 20251214124743.png)
### Promote to Domain Controller
To promote the server to domain controller there is 2 option :
- Click it here after installation :
![alt](attachments/Pasted image 20251214124917.png)
- On the yellow triangle, at the top right flag icon. Click it
![alt](attachments/Pasted image 20251214125005.png)
- Select: **Add a new forest** , and write the root domain name `lab.local`
![alt](attachments/Pasted image 20251214125214.png)
- Then on Domain Controller Options : 
	- Leave Forest/Domain functional level at Windows Server 2016, to ensure compatibility.
	- Type a DSRM Password, that help boot into **Safe Mode**.
![alt](attachments/Pasted image 20251214125611.png)
- Ignore the yellow warning
![alt](attachments/Pasted image 20251214125642.png)
- **Additional Options:** Verify NetBIOS name is `LAB`
![alt](attachments/Pasted image 20251214125719.png)
- **Paths:** Leave defaults.
![alt](attachments/Pasted image 20251214125816.png)
- **Prerequisites Check:** Wait for the green checkmark.
We got 2 problem , 1 which is critical :
- The Administrator password is blank 
![alt](attachments/Pasted image 20251214125938.png)
- So we set a password 
![alt](attachments/Pasted image 20251214130202.png)
- The click **Rerun Prerequisites Check**, and we get the green checkmark.
![alt](attachments/Pasted image 20251214130346.png)
- Click **Install** to begin installation.
![alt](attachments/Pasted image 20251214130432.png)
- The server will reboot automatically. 
## VERIFICATION
### Login & Verify
- When it comes back up, the login screen should say: `LAB\Administrator`.
![alt](attachments/Pasted image 20251214131943.png)
- Login.
- Open **Server Manager** > **Tools** (top right) and verify you see **Active Directory Users and Computers**.
	- Open it. You should see your domain `lab.local`.
![alt](attachments/Pasted image 20251214131530.png)
## Disclaimer 
For the 2 warning we got at the installation :
![alt](attachments/Pasted image 20251214130650.png)
- **The Cryptography Warning:** Means your server is too modern for computers from 1996. **Ignore it.**
- **The DNS Warning:** Means "I cannot find a parent company above you." This is correct because you _are_ the parent company. **Ignore it.**